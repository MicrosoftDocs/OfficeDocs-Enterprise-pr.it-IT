---
title: Amministrazione delle cassette postali di Exchange Online in un ambiente multi-geografico
ms.author: chrisda
author: chrisda
manager: serdars
ms.audience: ITPro
ms.topic: article
ms.service: o365-solutions
ms.custom: ''
localization_priority: Priority
description: Informazioni sull'amministrazione delle impostazioni multi-geografiche di Exchange Online con PowerShell di Microsoft.
ms.openlocfilehash: 5e1108c946ab1d9588ad5d1d41f21799e8254257
ms.sourcegitcommit: 8ba20f1b1839630a199585da0c83aaebd1ceb9fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "30934018"
---
# <a name="administering-exchange-online-mailboxes-in-a-multi-geo-environment"></a>Amministrazione delle cassette postali di Exchange Online in un ambiente multi-geografico

È richiesta la Sessione remota di PowerShell per visualizzare e configurare le proprietà multi-geografiche nell’ambiente di Office 365. Per informazioni su come connettersi a PowerShell per Exchange Online, vedere [Connettersi a PowerShell per Exchange Online](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell).

È necessario il [modulo di PowerShell di Microsoft Azure Active Directory](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx) v1.1.166.0 o versione successiva in V1. x per visualizzare la proprietà**PreferredDataLocation** sugli oggetti utente. Gli oggetti utente sincronizzati con AAD Connect in AAD non possono contenere i valori **PreferredDataLocation** modificati direttamente tramite ADD PowerShell. Gli oggetti utente solo cloud possono essere modificati tramite AAD PowerShell. Per connettersi a PowerShell di Azure Active Directory, vedere [Connettersi a PowerShell di Office 365](https://docs.microsoft.com/office365/enterprise/powershell/connect-to-office-365-powershell). 

## <a name="connect-directly-to-a-geo-location-using-exchange-online-powershell"></a>È possibile connettersi direttamente a una posizione geografica con PowerShell di Exchange Online.
In genere, PowerShell di Exchange Online si connetterà alla posizione centrale. Tuttavia, è anche possibile connettersi alla posizioni satellitari. Per una migliore prestazione, è consigliabile connettersi direttamente alla posizione satellitare quando si gestiscono solo gli utenti in una specifica posizione geografica.

Per connettersi a una posizione geografica specifica, il parametro *ConnectionUri* è diversa dalle ordinarie istruzioni di connessione. Il resto dei comandi e i valori sono uguali. Ecco come procedere:

1. Nel computer locale, aprire Windows PowerShell ed eseguire il seguente comando:
    
    ```
    $UserCredential = Get-Credential
    ```
   Nella finestra di dialogo **Richiesta credenziali di Windows PowerShell** digitare l'account e la password aziendale o dell'istituto di istruzione, quindi fare clic su **OK**.
    
2. Sostituire `<emailaddress>` con l'indirizzo di posta elettronica di **eventuali** cassette postali nella specifica posizione geografica e eseguire il comando seguente. Le autorizzazioni per la cassetta postale e la relazione con le credenziali nel passaggio 1 non sono un fattore; l'indirizzo di posta elettronica indica semplicemente a Exchange Online dove connettersi.
  
   ```
   $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell?email=<emailaddress> -Credential $UserCredential -Authentication  Basic -AllowRedirection
   ```

   Ad esempio, se olga@contoso.onmicrosoft.com è l'indirizzo di posta elettronica di una cassetta postale valida nella posizione geografica a cui si desidera connettersi, eseguire il comando seguente:

   ```
   $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell?email=olga@contoso.onmicrosoft.com -Credential $UserCredential -Authentication  Basic -AllowRedirection
   ```
3. Eseguire il comando riportato di seguito:
    
    ```
    Import-PSSession $Session
    ```


## <a name="view-the-available-geo-locations-that-are-configured-in-your-exchange-online-organization"></a>Visualizzare le posizioni geografiche disponibili configurate nella propria organizzazione di Exchange Online
Per visualizzare l'elenco di località geografiche configurate in Office 365 Multi-Geo, eseguire il comando seguente in PowerShell di Exchange Online:

```
Get-OrganizationConfig | Select -ExpandProperty AllowedMailboxRegions | Format-Table
```

## <a name="view-the-central-location-for-your-exchange-online-organization"></a>Visualizzare la posizione centrale per la propria organizzazione di Exchange Online
Per visualizzare la posizione centrale del proprio tenant, eseguire il comando seguente in PowerShell di Exchange Online:

```
Get-OrganizationConfig | Select DefaultMailboxRegion
```

## <a name="find-the-geo-location-of-a-mailbox"></a>Individuare la posizione geografica di una cassetta postale
La cmdlet **Get-Mailbox** in PowerShell di Exchange Online mostra le seguenti proprietà multi-geografica relative alle cassette postali:

- **Database**: le prime 3 lettere del nome del database corrispondono al codice geografico, che indica dove la cassetta postale è attualmente ubicata. Per cassette postali di archiviazione Online, sarà necessario usare le proprietà di **ArchiveDatabase**.

- **MailboxRegion**: specifica il codice posizione geografica impostato dall'amministratore (sincronizzato da **PreferredDataLocation** in Azure AD).

- **MailboxRegionLastUpdateTime**: indica quando MailboxRegion è stato aggiornato l’ultima volta (automaticamente o manualmente).

Per visualizzare le proprietà di una cassetta postale, utilizzare la sintassi seguente:

```
Get-Mailbox -Identity <MailboxIdentity> | Format-List Database,MailboxRegion*
```

Ad esempio, per visualizzare le informazioni geografiche della cassetta postale chris@contoso.onmicrosoft.com, eseguire il comando seguente:

```
Get-Mailbox -Identity chris@contoso.onmicrosoft.com | Format-List Database, MailboxRegion*
```

L'output del comando avrà questo aspetto:

```
Database                    : EURPR03DG077-db007 
MailboxRegion               : EUR 
MailboxRegionLastUpdateTime : 2/6/2018 8:21:01 PM 
```

> **Nota:** se il codice della posizione geografica nel nome del database non corrisponde al valore **MailboxRegion**, la cassetta postale verrà automaticamente verrà inserita in una coda di trasferimento e spostata nella posizione geografica specificata dal valore del ** MailboxRegion**(Exchange Online controlla se esiste una mancata corrispondenza tra questi valori di proprietà).

## <a name="move-an-existing-cloud-only-mailbox-to-a-specific-geo-location"></a>Spostare una cassetta postale esistente solo nel cloud in una posizione geografica specifica
Un utente solo cloud è un utente non sincronizzato nel tenant tramite AAD Connect. Tale utente è stato creato direttamente in Azure AD. Usare il cmdlet**Get-MsolUser** e **Set-MsolUser** nel modulo di Azure Active Directory per Windows PowerShell per visualizzare o specificare la geografica in cui verrà archiviata cassetta postale dell'utente solo cloud.

Per visualizzare i valori **PreferredDataLocation** di un utente, utilizzare la sintassi in Azure AD PowerShell:

```
Get-MsolUser -UserPrincipalName <UserPrincipalName> | Format-List UserPrincipalName,PreferredDataLocation
```

Ad esempio, per visualizzare i valori **PreferredDataLocation** dell’utente michelle@contoso.onmicrosoft.com, eseguire il comando seguente:

```
Get-MsolUser -UserPrincipalName michelle@contoso.onmicrosoft.com | Format-List
```

Per modificare il valore**PreferredDataLocation** per un utente solo cloud, utilizzare la sintassi seguente in Azure AD PowerShell:

``` 
Set-MsolUser -UserPrincipalName <UserPrincipalName> -PreferredDataLocation <GeoCode>
```

Ad esempio, per impostare i valori **PreferredDataLocation** sulla geografica dell’Unione Europea per l’utente michelle@contoso.onmicrosoft.com, eseguire il comando seguente:

``` 
Set-MsolUser -UserPrincipalName michelle@contoso.onmicrosoft.com -PreferredDataLocation EUR
```

**Note**:

- Come già accennato in precedenza non è possibile usare questa procedura per gli oggetti utente sincronizzati dalla Active Directory locale. È necessario modificare il valore **PreferredDataLocation** in Active Directory e sincronizzarlo con AAD Connect. Per ulteriori informazioni, vedere [Sincronizzazione di Azure Active Directory Connect: configurare il percorso di dati preferito per le risorse di Office 365](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-feature-preferreddatalocation). 

- Il tempo necessario per spostare una cassetta postale in una nuova posizione geografica dipende da diversi fattori:
 
  - Le dimensioni e tipo di cassetta postale.
 
  - Il numero totale di cassette postali di cui eseguire la migrazione.
 
  - La disponibilità delle risorse di spostamento.

### <a name="move-disabled-mailboxes-that-are-on-litigation-hold"></a>Disattivazione della migrazione per cassette postali in blocco per controversia legale
Le cassette postali in blocco per controversia legale che vengono conservate per eDiscovery non possono essere spostate modificando i valori **PreferredDataLocation** dal loro stato di disattivazione. Per spostare una cassetta postale disabilitata in blocco per controversia legale:

1. Assegnare una licenza temporanea alla cassetta postale.

2. Modificare il **PreferredDataLocation**.

3. Rimuovere la licenza dalla cassetta postale dopo che è stata spostata nella posizione geografica selezionata per ripristinare la disattivazione.

## <a name="create-new-cloud-mailboxes-in-a-specific-geo-location"></a>Creare nuove cassette postali nel cloud in una posizione geografica specifica
Per creare una nuova cassetta postale in una posizione geografica specifica, è necessario procedere come segue:

- Configurare il valore **PreferredDataLocation** come descritto nella sezione precedente *prima che* venga creata la cassetta postale in Exchange Online. Ad esempio, configurare il valore **PreferredDataLocation** per un utente prima di assegnare una licenza. 

- Assegnare una licenza contemporaneamente all’impostazione del valore **PreferredDataLocation**.

Per creare un nuovo utente solo cloud con licenza (non sincronizzato con AAD Connect) in un determinata posizione geografica, usare la sintassi seguente in Azure AD PowerShell:

```
New-MsolUser -UserPrincipalName <UserPrincipalName> -DisplayName "<Display Name>" [-FirstName <FirstName>] [-LastName <LastName>] [-Password <Password>] [-LicenseAssignment <AccountSkuId>] -PreferredDataLocation <GeoCode> 
```
In questo esempio crea un nuovo account utente per Elizabeth Brunner con i valori seguenti:

- Nome dell'entità utente: ebrunner@contoso.onmicrosoft.com

- Nome: entrambe

- Cognome: Brunner

- Visualizzare nome Elizabeth Brunner

- Password: generata casualmente e visualizzata nei risultati del comando (in quanto non vengono usati i parametri della *Password*)

- Licenza: contoso:ENTERPRISEPREMIUM (E5)

- Posizione: Australia (AUS)

```
New-MsolUser -UserPrincipalName ebrunner@contoso.onmicrosoft.com -DisplayName "Elizabeth Brunner" -FirstName Elizabeth -LastName Brunner -LicenseAssignment contoso:ENTERPRISEPREMIUM -PreferredDataLocation AUS
```

Per ulteriori informazioni sulla creazione di nuovi account utente e la ricerca di valori di LicenseAssignment in Azure AD PowerShell, vedere [Creare account utente con PowerShell di Office 365](https://docs.microsoft.com/office365/enterprise/powershell/create-user-accounts-with-office-365-powershell) e [Visualizzare le licenze e i servizi con Office 365 PowerShell](https://docs.microsoft.com/office365/enterprise/powershell/view-licenses-and-services-with-office-365-powershell).

> **Nota:** se si sta utilizzando PowerShell di Exchange Online per abilitare una cassetta postale si desidera che questa sia creata direttamente nella posizione geografica specificata in **PreferredDataLocation**, è necessario utilizzare un cmdlet di Exchange Online come **Enable-Mailbox** o **New-Mailbox** direttamente con il servizio di cloud. Se si usa il cmdlet di Exchange locale**Enable-RemoteMailbox**, la cassetta postale verrà creata nella posizione centrale.

## <a name="onboard-existing-on-premises-mailboxes-in-a-specific-geo-location"></a>Effettuare l’integrazione di cassette postali locali esistenti in una posizione geografica specifica
È possibile usare i processi e gli strumenti standard di integrazione per eseguire la migrazione di una cassetta postale di un'organizzazione di Exchange locale a Exchange Online, tra cui la [Dashboard di migrazione nell'interfaccia](https://support.office.com/article/d164b35c-f624-4f83-ac58-b7cae96ab331)e il cmdlet [New-MigrationBatch ](https://docs.microsoft.com/powershell/module/exchange/move-and-migration/new-migrationbatch) in PowerShell di Exchange Online.

Il primo passaggio consiste nel verificare che esista un oggetto utente per ogni cassetta postale su cui effettuare l’integrazione e verificare che sia configurato il corretto valore della **PreferredDataLocation** in Azure AD. Gli strumenti di integrazione rispetteranno il valore **PreferredDataLocation** e verrà eseguita la migrazione delle cassette postali direttamente alla posizione geografica specificata.

Oppure, la procedura seguente consente di aggiungere cassette postali direttamente a una posizione geografica specifica tramite il cmdlet [New-MoveRequest](https://docs.microsoft.com/powershell/module/exchange/move-and-migration/new-moverequest) in PowerShell di Exchange Online.

1. Verificare che esista un oggetto utente per ogni cassetta postale su cui effettuare l’integrazione e che la **PreferredDataLocation** sia impostata sul valore desiderato in Azure AD. Il valore di **PreferredDataLocation** sarà sincronizzato con l’attributo di**MailboxRegion** del corrispondente oggetto utente di posta in Exchange Online.

2. Connettersi direttamente a specifici posizioni geografiche satellitari seguendo le istruzioni di connessione dei passaggi precedenti di questo argomento.

3. Nella finestra di PowerShell di Exchange Online, archiviare le credenziali di amministratore locale usate per eseguire la migrazione delle cassette postali in una variabile, eseguendo il comando seguente:

    ```
    $RC = Get-Credential
    ```

4. Su PowerShell di Exchange Online, creare una nuova **New-MoveRequest** simile all’esempio seguente: 

    ```
    New-MoveRequest -Remote -RemoteHostName mail.contoso.com -RemoteCredential $RC -Identity user@contoso.com -TargetDeliveryDomain <YourAppropriateDomain>
    ```

5. Ripetere il passaggio #4 per ogni cassetta postale che per necessario eseguire la migrazione dall’Exchange locale alla posizione satellitare con cui si è attualmente connessi.

6. Se è necessario eseguire la migrazione di altre cassette postali a un percorso satellitare differente, ripetere i passaggi da 2 a 4 per ogni località satellite specifica.

## <a name="multi-geo-reporting"></a>Creazione di report multi-geografici
**I report sull'utilizzo di Multi-Geo** nell’interfaccia di amministrazione di Microsoft 365 mostrano il numero di utenti in base alla località geografica. Il report mostra la distribuzione degli utenti per il mese corrente e fornisce i dati cronologici dagli ultimi 6 mesi.

## <a name="see-also"></a>Vedere anche

[Gestione di Office 365 ed Exchange Online con Windows PowerShell](https://support.office.com//article/06a743bb-ceb6-49a9-a61d-db4ffdf54fa6)