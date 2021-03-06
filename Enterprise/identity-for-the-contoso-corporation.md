---
title: "Identità per Contoso Corporation"
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 9/12/2017
ms.audience: ITPro
ms.topic: overview
ms.prod: office-online-server
localization_priority: Normal
ms.collection: Ent_O365
ms.custom:
- DecEntMigration
- Ent_Architecture
ms.assetid: 78a407e4-2d8b-4561-b308-b22c95f60eeb
description: "Sintesi: informazioni su come Contoso trae vantaggio da una soluzione di gestione delle identità e degli accessi distribuita come servizio (IDaaS) e fornisce un'autenticazione ridondante e distribuita a livello geografico per i suoi utenti."
---

# Identità per Contoso Corporation

 **Sintesi:** informazioni su come Contoso trae vantaggio da una soluzione di gestione delle identità e degli accessi distribuita come servizio (IDaaS) e fornisce un'autenticazione ridondante e distribuita a livello geografico per i suoi utenti.
  
Microsoft fornisce una soluzione di gestione delle identità e degli accessi distribuita come servizio (IDaaS) nelle sue offerte cloud. Per adottare un'infrastruttura inclusiva di cloud, la soluzione IDaaS di Contoso deve sfruttare i provider di identità locali e includere l'autenticazione federata con i provider di identità di terze parti esistenti e attendibili.
  
## Foresta di Windows Server AD di Contoso

Contoso usa una foresta di Windows Server Active Directory (AD) singola per contoso.com con sette domini, uno per ogni area geografica del mondo. La sede principale, le sedi centrali regionali e le filiali contengono controller di dominio per l'autorizzazione e l'autenticazione locali.
  
**Figura 1: foresta di Contoso e domini a livello mondiale**

![Domini e foresta di AD di Windows Server di Contoso nel mondo](images/d1395196-bd8b-4d42-9e47-ff6bcd6c77b7.png)
  
Nella figura 1 viene mostrata la foresta di Contoso con domini regionali per le varie parti del mondo in cui sono presenti sedi centrali regionali.
  
Contoso desidera utilizzare gli account e i gruppi della foresta contoso.com per l'autenticazione e l'autorizzazione per le app basate su cloud e per i carichi di lavoro.
  
## Infrastruttura di autenticazione federata di Contoso

Contoso consente:
  
- Ai clienti di usare il proprio account Microsoft, Facebook o Google Mail per accedere al proprio sito Web pubblico.
    
- Ai fornitori e ai partner di usare il proprio account LinkedIn, Salesforce o Google Mail per accedere all'extranet dei partner.
    
**Figura 2: Supporto di Contoso per l'autenticazione federata di clienti e partner**

![Infrastruttura esistente di Contoso per supportare l'autenticazione federata di clienti e partner](images/22388392-06de-4cb0-8b55-b0861c50eb76.png)
  
Nella figura 2 viene mostrata la rete perimetrale di Contoso contenente un sito Web pubblico, una rete extranet partner e un set di server AD FS. La rete perimetrale è connessa a Internet che contiene clienti, partner e servizi Internet.
  
I server di Active Directory Federation Services (AD FS) nella DMZ autenticano le credenziali dei clienti per l'accesso al sito Web pubblico e le credenziali dei partner per l'accesso all'extranet dei partner.
  
Quando Contoso effettua la transizione dal proprio sito Web pubblico in Azure Web App e dall'extranet dei partner a Dynamics 365, desidera continuare a utilizzare i provider di identità di terze parti per clienti e partner. Questo sarà possibile configurando la federazione tra i tenant di Contoso Azure AD e i provider di identità di terze parti.
  
## Sincronizzazione di directory per la foresta Windows Server AD di Contoso

Contoso ha distribuito lo strumento Azure AD Connect su un cluster di server nel suo centro dati di Parigi. Azure AD Connect sincronizza le modifiche alla foresta di Windows Server AD contoso.com con il tenant di Azure AD condiviso dalle sottoscrizioni a Office 365, EMS, Dynamics 365 e Azure di Contoso. Per ulteriori informazioni su sottoscrizioni, licenze, account utente e tenant, vedere [Sottoscrizioni, licenze e account utente per Contoso Corporation](subscriptions-licenses-and-user-accounts-for-the-contoso-corporation.md).
  
**Figura 3: Infrastruttura di sincronizzazione della directory di Contoso**

![Infrastruttura di sincronizzazione della directory di Contoso](images/cc085864-cfb4-40df-9ce0-2cfa165080d1.png)
  
Nella figura 3 viene mostrato un cluster di server che eseguono Azure AD Connect per la sincronizzazione della foresta di Windows Server AD di Contoso con il tenant di Azure AD.
  
Contoso ha configurato l'autenticazione federata, che permette ai dipendenti di Contoso di effettuare l'accesso Single Sign-On. Quando un utente che ha già effettuato l'accesso alla foresta Windows Server AD di contoso.com accede a una risorsa cloud SaaS o PaaS di Microsoft, non verrà richiesta la password.
  
## Distribuzione geografica del traffico di autenticazione di Contoso

Per supportare al meglio le proprie risorse mobili e remote, Contoso ha distribuito insiemi di server di autenticazione nelle proprie filiali. Questa infrastruttura distribuisce il carico e offre ridondanza, nonché prestazioni migliori durante l'autenticazione delle credenziali utente per l'accesso alle offerte cloud di Microsoft che utilizzano il tenant di Azure AD comune.
  
Per distribuire il carico delle richieste di autenticazione, Contoso ha configurato Azure Traffic Manager con un profilo che utilizza il metodo di routing delle prestazioni, che consente di autenticare i client al set di server di autenticazione nell'area geografica più vicina. 
  
**Figura 4: Distribuzione geografica del traffico di autenticazione per le sedi regionali**

![Distribuzione geografica del traffico di autenticazione di Contoso per le sedi regionali](images/b27d8524-dd25-41a7-903d-ff6e669f5531.png)
  
Nella figura 4 vengono mostrati i livelli dei computer client, Gestione traffico di Azure e i server di autenticazione nelle filiali regionali. Ogni filiale regionale usa proxy Web e server AD FS per autenticare le credenziali utente con i controller di dominio di Windows Server AD.
  
Esempio di processo di autenticazione:
  
1. Il computer client avvia la comunicazione con una pagina Web nella tenancy di Office 365 in Europa (ad esempio sharepoint.contoso.com).
    
2. Office 365 inoltra una richiesta di invio per la prova di autenticazione. La richiesta contiene l'URL da contattare per l'autenticazione.
    
3. Il computer client tenta di risolvere il nome DNS nell'URL a un indirizzo IP.
    
4. Azure Traffic Manager riceve la query DNS e risponde al computer client con l'indirizzo IP di un server proxy di applicazione Web nella filiale più vicina al computer client.
    
5.  Il computer client invia una richiesta di autenticazione a un server proxy di applicazione Web, che inoltra la richiesta a un server AD FS.
    
6. Il server AD FS richiede le credenziali utente dal computer client.
    
7. Il computer client invia le credenziali utente senza chiedere conferma all'utente.
    
8. Il server AD FS convalida le credenziali con un controller di dominio Windows Server AD nella filiale e restituisce un token di sicurezza al computer client.
    
9. Il computer client invia il token di sicurezza a Office 365.
    
10. Dopo aver completato la convalida, Office 365 memorizza nella cache il token di sicurezza e invia la pagina Web richiesta nel passaggio 1 al computer client.
    
## Ridondanza per l'infrastruttura di autenticazione della sede centrale in IaaS di Azure

Per garantire la ridondanza a dipendenti remoti e mobili della sede di Parigi con 15.000 dipendenti, Contoso ha distribuito un secondo set di proxy di applicazione e server AD FS in IaaS di Azure.
  
**Figura 5: Infrastruttura di autenticazione ridondante in IaaS di Azure**

![Infrastruttura di autenticazione ridondante in IaaS di Azure per la sede centrale di Parigi](images/13b3c804-73b8-472a-8404-34a6ba3d8dd8.png)
  
Nella figura 5 vengono mostrati i proxy Web e i server AD FS nella rete perimetrale e un set aggiuntivo di ognuno di questi in una rete virtuale di Azure cross-premise.
  
Quando i server di autenticazione principali nella rete perimetrale della sede centrale diventano non disponibili, il personale IT passa al set ridondante distribuito in IaaS di Azure. Le richieste di autenticazione successive provenienti dai computer della sede di Parigi usano il set in IaaS di Azure finché il problema di disponibilità non viene corretto.
  
Per effettuare questi passaggi, Contoso aggiorna il profilo Azure Traffic Manager affinché l'area di Parigi possa utilizzare un set di indirizzi IP diverso per i proxy di applicazioni Web:
  
- Quando l'autenticazione ai server della rete perimetrale torna disponibile, usa gli indirizzi IP dei server nella rete perimetrale.
    
- Quando l'autenticazione ai server della rete perimetrale torna disponibile, usa gli indirizzi IP dei server in IaaS di Azure.
    
## See Also

#### 

[Contoso nel Microsoft Cloud](contoso-in-the-microsoft-cloud.md)
  
[Risorse sull'architettura IT del cloud Microsoft](microsoft-cloud-it-architecture-resources.md)
#### 

[Identità di Microsoft Cloud per Enterprise Architects](http://aka.ms/cloudarchidentity)
  
[Protezione di dispositivi e identità per Office 365](http://aka.ms/o365protect_device)
  
[Guida di orientamento per Enterprise Cloud di Microsoft: risorse per i decision maker del settore IT](https://sway.com/FJ2xsyWtkJc2taRD)

