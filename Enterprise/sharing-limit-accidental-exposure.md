---
title: Limitare l'esposizione accidentale
ms.author: mikeplum
author: MikePlumleyMSFT
manager: pamgreen
audience: ITPro
ms.topic: article
ms.service: sharepoint-online
localization_priority: Priority
description: Informazioni su come limitare l'esposizione accidentale di informazioni quando si condividono file con utenti guest.
ms.openlocfilehash: d1a12579bdcce03ad74dbf753ddb1a8a6368c88c
ms.sourcegitcommit: c16ab90d0b9902228ce4337f1c64900592936cce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2019
ms.locfileid: "37108336"
---
# <a name="limit-accidental-exposure-to-files-when-sharing-with-guests"></a>Limitare l'esposizione accidentale ai file durante la condivisione con gli utenti guest

Quando si condividono file e cartelle con utenti guest sono disponibili diverse opzioni per ridurre le possibilità di condivisione accidentale di informazioni riservate. È possibile scegliere tra le opzioni disponibili in questo articolo per soddisfare al meglio le esigenze dell'organizzazione.

## <a name="use-best-practices-for-anyone-links"></a>Usare le procedure consigliate per i collegamenti di tipo “Chiunque”

Se le persone dell'organizzazione devono eseguire una condivisione anonima, ma si incorre nel rischio che gli utenti non autenticati modifichino il contenuto, leggere [Procedure consigliate per la condivisione anonima](best-practices-anonymous-sharing.md) per istruzioni su come gestire la condivisione anonima nell’organizzazione.

## <a name="turn-off-anyone-links"></a>Disattivare i collegamenti di tipo “Chiunque”

È consigliabile lasciare abilitati i collegamenti di tipo *Chiunque* per il contenuto appropriato, perché è il modo più semplice per condividere informazioni e contribuisce a ridurre il rischio che gli utenti cerchino altre soluzioni fuori dal controllo del reparto IT. I collegamenti di tipo *Chiunque* possono essere inoltrati ad altri, ma l'accesso ai file è disponibile solo per gli utenti che dispongono del collegamento.

Se si vuole che gli utenti eseguano sempre l'autenticazione per accedere al contenuto di SharePoint, Groups o Teams, è possibile disattivare la condivisione *Chiunque*. In questo modo è possibile impedire agli utenti di condividere contenuto in modo anonimo.

Se si disabilitano i collegamenti di tipo *Chiunque*, gli utenti potranno comunque condividerli facilmente con gli utenti guest utilizzando i collegamenti di tipo *Persone specifiche*. In questo caso, per poter accedere al contenuto condiviso, tutti gli utenti guest dovranno eseguire l'autenticazione.

In base alle proprie esigenze, è possibile disabilitare i collegamenti di tipo *Chiunque* per siti specifici o per l'intera organizzazione.

Per disattivare i collegamenti di tipo *Chiunque* per l'organizzazione
1. Nella parte sinistra dell'interfaccia di amministrazione di SharePoint, fare clic su **Condivisione**.
2. Impostare le impostazioni di condivisione esterna di SharePoint su **Utenti guest nuovi ed esistenti**.</br>
   ![Screenshot delle impostazioni di condivisione esterna dei siti di SharePoint](media/sharepoint-organization-external-sharing-controls-new-users.png)
3. Fare clic su **Salva**.

Per disattivare i collegamenti di tipo *Chiunque* per un sito
1. Nella parte sinistra dell'interfaccia di amministrazione di SharePoint, espandere **Siti** e fare clic su **Siti attivi**.
2. Selezionare il sito del team appena creato.
3. Sulla barra multifunzione fare clic su **Condivisione**.
4. Verificare che la condivisione sia impostata su **Utenti guest nuovi ed esistenti**.</br>
   ![Screenshot delle impostazioni di condivisione esterna dei siti di SharePoint](media/sharepoint-site-external-sharing-settings.png)
5. Se si apportano modifiche, fare clic su **Salva**.

## <a name="domain-filtering"></a>Filtro domini

È possibile usare gli elenchi di domini consentiti o non consentiti per determinare da quali domini gli utenti possono invitare utenti guest.

Con un elenco di domini consentiti è possibile specificare un elenco di domini da cui gli utenti dell'organizzazione possono invitare utenti guest. Gli inviti guest ad altri domini sono bloccati. Se l'organizzazione collabora solo con utenti guest da un elenco di domini specifici, è possibile usare questa caratteristica per impedire la condivisione con altri domini.

Con un elenco di domini non consentiti è possibile specificare un elenco di domini da cui gli utenti dell'organizzazione non possono invitare utenti guest. Gli inviti guest ai domini presenti nell’elenco sono bloccati. Questa opzione può essere utile, ad esempio, se si vuole impedire che alcuni concorrenti specifici diventino utenti guest nell’organizzazione.

Gli elenchi di domini consentiti e non consentiti influiscono solo sulle condivisioni con utenti guest autenticati. Gli utenti possono continuare a condividere contenuti con utenti guest da domini non consentiti tramite i collegamenti di tipo *Chiunque*, se questi non sono stati disabilitati. Per ottenere risultati ottimali con gli elenchi di domini consentiti e non consentiti, è consigliabile disabilitare i collegamenti di tipo *Chiunque* come descritto sopra.

Per creare un elenco di domini consentiti o non consentiti per la condivisione guest
1. Nella parte sinistra dell'interfaccia di amministrazione di SharePoint, fare clic su **Condivisione**.
2. In **Impostazioni avanzate per la condivisione esterna** selezionare la casella di controllo **Limitare la condivisione esterna in base al dominio**.
3. Fare clic su **Aggiungi domini**.
4. Selezionare se si vogliono bloccare i domini, digitare i domini e quindi fare clic su **OK**.</br>
   ![Screenshot dell’impostazione di SharePoint Limitare la condivisione esterna in base al dominio](media/sharepoint-sharing-block-domain.png)
5. Fare clic su **Salva**.

Se si vuole limitare la condivisione in base al dominio a un livello superiore rispetto a SharePoint e OneDrive, è possibile [consentire o bloccare gli inviti agli utenti B2B da organizzazioni specifiche](https://docs.microsoft.com/azure/active-directory/b2b/allow-deny-list) in Azure Active Directory. (È necessario configurare l’[anteprima dell'integrazione di SharePoint e OneDrive con Azure AD B2B](https://docs.microsoft.com/sharepoint/sharepoint-azureb2b-integration-preview) perché queste impostazioni influiscano su SharePoint e OneDrive.)

## <a name="limit-guest-sharing-of-files-folders-and-sites-to-specified-security-groups"></a>Limitare la condivisione guest di file, cartelle e siti a gruppi di sicurezza specifici

È possibile limitare la condivisione guest di file, cartelle e siti ai membri di un gruppo di sicurezza specifico. Questa opzione è utile se si vuole abilitare la condivisione guest, ma con un flusso di lavoro di approvazione o un processo di richiesta.

Per limitare la condivisione guest ai membri di un gruppo di sicurezza
1. Nella parte sinistra dell'interfaccia di amministrazione di SharePoint, fare clic su **Condivisione**.
2. In **Altre impostazioni** seguire il collegamento **Limitare la condivisione esterna ai gruppi di sicurezza**.
3. In **Chi può condividere all'esterno dell'organizzazione** selezionare una o entrambe le caselle di controllo: a. **Consenti solo agli utenti dei gruppi di sicurezza selezionati di condividere con utenti esterni autenticati** per specificare un gruppo di sicurezza che può condividere con utenti autenticati b. **Consenti la condivisione con utenti esterni autenticati e usando collegamenti anonimi ai soli utenti dei gruppi di sicurezza selezionati** per specificare un gruppo di sicurezza che può condividere con utenti autenticati e usando collegamenti di tipo Chiunque
4. Fare clic su **OK**.

Si noti che questo influisce su file, cartelle e siti, ma non sui gruppi di Office 365 o su Teams. Quando i membri invitano gli utenti guest a un gruppo di Office 365 privato o a un team privato in Microsoft Teams, l'invito viene inviato al proprietario del gruppo o del team per l'approvazione.

## <a name="see-also"></a>Vedere anche

[Creare un ambiente di condivisione guest sicuro](create-a-secure-guest-sharing-environment.md)

[Procedure consigliate per la condivisione di file e cartelle con utenti anonimi](best-practices-anonymous-sharing.md)