---
title: Utilizzare PowerShell per eseguire una migrazione a fasi a Office 365
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 12/15/2017
audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
search.appverid:
- MET150
ms.collection: Ent_O365
f1.keywords:
- NOCSH
ms.custom: ''
ms.assetid: a20f9dbd-6102-4ffa-b72c-ff813e700930
description: "Riepilogo: informazioni sull'utilizzo di Windows PowerShell per eseguire una migrazione a fasi a Office 365."
ms.openlocfilehash: ca50edd079e17808c46ff5a956ed2efad34eb322
ms.sourcegitcommit: c6a2256f746f55d1cfb739649ffeee1f2f2152aa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "45052559"
---
# <a name="use-powershell-to-perform-a-staged-migration-to-office-365"></a>Utilizzare PowerShell per eseguire una migrazione a fasi a Office 365

È possibile migrare i contenuti delle cassette postali degli utenti da un sistema di posta elettronica di origine a Office 365 nel tempo utilizzando una migrazione a fasi.
  
This article walks you through the tasks involved with for a staged email migration using Exchange Online PowerShell. The topic, [What you need to know about a staged email migration to Office 365](https://go.microsoft.com/fwlink/p/?LinkId=536487), gives you an overview of the migration process. When you're comfortable with the contents of that article, use this one to begin migrating mailboxes from one email system to another.
  
> [!NOTE]
> You can also use the Exchange admin center to perform staged migration. See [Perform a staged migration of email to Office 365](https://go.microsoft.com/fwlink/p/?LinkId=536687). 
  
## <a name="what-do-you-need-to-know-before-you-begin"></a>Che cosa è necessario sapere prima di iniziare

Estimated time to complete this task: 2-5 minutes to create a migration batch. After the migration batch is started, the duration of the migration will vary based on the number of mailboxes in the batch, the size of each mailbox, and your available network capacity. For information about other factors that affect how long it takes to migrate mailboxes to Office 365, see [Migration Performance](https://go.microsoft.com/fwlink/p/?LinkId=275079).
  
You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Migration" entry in the [Recipients Permissions](https://go.microsoft.com/fwlink/p/?LinkId=534105) topic.
  
To use the Exchange Online PowerShell cmdlets, you need to sign in and import the cmdlets into your local Windows PowerShell session. See [Connect to Exchange Online using remote PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=534121) for instructions.
  
Per un elenco completo dei comandi di migrazione, vedere [Cmdlet di spostamento e migrazione](https://go.microsoft.com/fwlink/p/?LinkId=534750).
  
## <a name="migration-steps"></a>Procedura della migrazione

### <a name="step-1-prepare-for-a-staged-migration"></a>Passaggio 1: predisporre la migrazione a fasi

Prima di eseguire la migrazione delle cassette postali a Office 365 utilizzando una migrazione a fasi, esistono alcune modifiche che è necessario apportare al proprio ambiente di Exchange.
  
 **Configure Outlook Anywhere on your on-premises Exchange Server** The email migration service uses Outlook Anywhere (also known as RPC over HTTP), to connect to your on-premises Exchange Server. For information about how to set up Outlook Anywhere for Exchange Server 2007, and Exchange 2003, see the following:
  
- [Exchange 2007: Come abilitare Outlook Anywhere](https://go.microsoft.com/fwlink/?LinkID=167210)
    
- [Configurazione di Outlook via Internet con Exchange 2003](https://go.microsoft.com/fwlink/?LinkID=167209)
    
> [!IMPORTANT]
> You must use a certificate issued by a trusted certification authority (CA) with your Outlook Anywhere configuration. Outlook Anywhere can't be configured with a self-signed certificate. For more information, see [How to configure SSL for Outlook Anywhere](https://go.microsoft.com/fwlink/?LinkID=80875). 
  
 **Facoltativo: verificare che sia possibile connettersi all'organizzazione di Exchange utilizzando Outlook via Internet** Utilizzare uno dei seguenti metodi per verificare le impostazioni di connessione.
  
- Utilizzare Outlook all'esterno della rete aziendale per connettersi alla cassetta postale di Exchange locale.
    
- Utilizzare l' [Analizzatore connettività remota Microsoft](https://https://testconnectivity.microsoft.com/) per testare le impostazioni di connessione. Utilizzare i test di individuazione automatica di Outlook o Outlook via Internet (RPC su HTTP).
    
- In PowerShell di Exchange Online, eseguire i comandi seguenti:
    
  ```powershell
  $Credentials = Get-Credential
  ```

  ```powershell
  Test-MigrationServerAvailability -ExchangeOutlookAnywhere -Autodiscover -EmailAddress <email address for on-premises administrator> -Credentials $credentials
  ```

 **Set permissions** The on-premises user account that you use to connect to your on-premises Exchange organization (also called the migration administrator) must have the necessary permissions to access the on-premises mailboxes that you want to migrate to Office 365. This user account is used when you connect to your email system by creating a migration endpoint later in this procedure ([Step 3: Create a migration endpoint](use-powershell-to-perform-a-staged-migration-to-office-365.md#BK_Endpoint) ).
  
Per eseguire la migrazione delle cassette postali, l'amministratore deve disporre di uno dei seguenti set di autorizzazioni:
  
- Essere un membro del gruppo **Domain Admins** di Active Directory nell'organizzazione locale.
    
    oppure
    
- Disporre dell'autorizzazione **FullAccess** per ogni cassetta postale locale e dell'autorizzazione **WriteProperty** per modificare la proprietà **TargetAddress** negli account utente locali.
    
    oppure
    
- Disporre dell'autorizzazione **Receive As** sul database delle cassette postali locale in cui sono memorizzate le cassette postali degli utenti e dell'autorizzazione **WriteProperty** per modificare la proprietà **TargetAddress** negli account utente locali.
    
Per istruzioni su come impostare queste autorizzazioni, vedere [Assegnazione delle autorizzazioni per la migrazione dalle cassette postali a Office 365](https://go.microsoft.com/fwlink/?LinkId=521656).
  
 **Disable Unified Messaging (UM)** If UM is turned on for the on-premises mailboxes you're migrating, turn off UM before migration. Turn on UM for the mailboxes after migration is complete. For how-to steps, see[disable unified messaging](https://go.microsoft.com/fwlink/?LinkId=521891).
  
 **Use directory synchronization to create new users in Office 365.** You use directory synchronization to create all the on-premises users in your Office 365 organization.
  
You need to license the users after they're created. You have 30 days to add licenses after the users are created. For steps to add licenses, see [Step 8: Complete post-migration tasks](use-powershell-to-perform-a-staged-migration-to-office-365.md#BK_Postmigration).
  
 È possibile utilizzare lo strumento di sincronizzazione di Microsoft Azure Active Directory (Azure AD) o Microsoft Azure AD Sync Services per sincronizzare e creare gli utenti locali in Office 365. Dopo la migrazione delle cassette postali in Office 365, gli account utente verranno gestiti nell'organizzazione locale e saranno sincronizzati con l'organizzazione di Office 365. Per ulteriori informazioni, vedere [Integrazione di directory](https://go.microsoft.com/fwlink/?LinkId=521788) .
  
### <a name="step-2-create-a-csv-file-for-a-staged-migration-batch"></a>Passaggio 2: creazione di un file CSV per un batch di migrazione a fasi

After you identify the users whose on-premises mailboxes you want to migrate to Office 365, you use a comma separated value (CSV ) file to create a migration batch. Each row in the CSV file—used by Office 365 to run the migration—contains information about an on-premises mailbox. 
  
> [!NOTE]
> There isn't a limit for the number of mailboxes that you can migrate to Office 365 using a staged migration. The CSV file for a migration batch can contain a maximum of 2,000 rows. To migrate more than 2,000 mailboxes, create additional CSV files and use each file to create a new migration batch. 
  
 **Attributi supportati**
  
The CSV file for a staged migration supports the following three attributes. Each row in the CSV file corresponds to a mailbox and must contain a value for each of these attributes.
  
|**Attributo**|**Descrizione**|**Obbligatorio?**|
|:-----|:-----|:-----|
|EmailAddress  <br/> |Specifica l'indirizzo di posta elettronica SMTP principale, ad esempio pilarp@contoso.com, per le cassette postali locali.  <br/> Use the primary SMTP address for on-premises mailboxes and not user IDs from the Office 365. For example, if the on-premises domain is named contoso.com but the Office 365 email domain is named service.contoso.com, you would use the contoso.com domain name for email addresses in the CSV file.  <br/> |Obbligatorio  <br/> |
|Password  <br/> |The password to be set for the new Office 365 mailbox. Any password restrictions that are applied to your Office 365 organization also apply to the passwords included in the CSV file.  <br/> |Facoltativo  <br/> |
|ForceChangePassword  <br/> |Specifies whether a user must change the password the first time they sign in to their new Office 365 mailbox. Use **True** or **False** for the value of this parameter. <br/> > [!NOTE]> Se è stata implementata una soluzione Single Sign-On (SSO) distribuendo Active Directory Federation Services (ADFS) o versioni successive nell'organizzazione locale, è necessario usare **False** come valore dell'attributo **ForceChangePassword**.          |Facoltativo  <br/> |
   
 **Formato del file CSV**
  
Here's an example of the format for the CSV file. In this example, three on-premises mailboxes are migrated to Office 365.
  
The first row, or header row, of the CSV file lists the names of the attributes, or fields, specified in the rows that follow. Each attribute name is separated by a comma.
  
```powershell
EmailAddress,Password,ForceChangePassword 
pilarp@contoso.com,Pa$$w0rd,False 
tobyn@contoso.com,Pa$$w0rd,False 
briant@contoso.com,Pa$$w0rd,False 
```

Each row under the header row represents one user and supplies the information that will be used to migrate the user's mailbox. The attribute values in each row must be in the same order as the attribute names in the header row. 
  
Use any text editor, or an application like Excel , to create the CSV file. Save the file as a .csv or .txt file.
  
> [!NOTE]
> If the CSV file contains non-ASCII or special characters, save the CSV file with UTF-8 or other Unicode encoding. Depending on the application, saving the CSV file with UTF-8 or other Unicode encoding can be easier when the system locale of the computer matches the language used in the CSV file. 
  
### <a name="step-3-create-a-migration-endpoint"></a>Passaggio 3: creare un endpoint di migrazione
<a name="BK_Endpoint"> </a>

To migrate email successfully, Office 365 needs to connect and communicate with the source email system. To do this, Office 365 uses a migration endpoint. To create an Outlook Anywhere migration endpoint by using PowerShell, for staged migration, first [connect to Exchange Online](https://go.microsoft.com/fwlink/p/?LinkId=534121). 
  
Per un elenco completo dei comandi di migrazione, vedere [Cmdlet di spostamento e migrazione](https://go.microsoft.com/fwlink/p/?LinkId=534750).
  
Per creare un endpoint di migrazione di Outlook via Internet denominato "StagedEndpoint" in PowerShell di Exchange Online, eseguire i comandi seguenti:
  
```powershell
$Credentials = Get-Credential
```

```powershell
New-MigrationEndpoint -ExchangeOutlookAnywhere -Name StagedEndpoint -Autodiscover -EmailAddress administrator@contoso.com -Credentials $Credentials
```

Per ulteriori informazioni sul cmdlet **New-MigrationEndpoint**, vedere[New-MigrationEndpoint](https://go.microsoft.com/fwlink/p/?LinkId=536437).
  
> [!NOTE]
> The **New-MigrationEndpoint** cmdlet can be used to specify a database for the service to use by using the **-TargetDatabase** option. Otherwise a database is randomly assigned from the Active Directory Federation Services (AD FS) 2.0 site where the management mailbox is located.
  
#### <a name="verify-it-worked"></a>Verificare che il passaggio di migrazione sia avvenuto correttamente

In PowerShell di Exchange Online eseguire il comando riportato di seguito per visualizzare le informazioni sull'endpoint di migrazione "StagedEndpoint":
  
```powershell
Get-MigrationEndpoint StagedEndpoint | Format-List EndpointType,ExchangeServer,UseAutoDiscover,Max*
```

### <a name="step-4-create-and-start-a-stage-migration-batch"></a>Passaggio 4: creare e avviare un batch di migrazione a fasi
<a name="BK_Endpoint"> </a>

You can use the **New-MigrationBatch** cmdlet in Exchange Online PowerShell to create a migration batch for a cutover migration. You can create a migration batch and start it automatically by including the _AutoStart_ parameter. Alternatively, you can create the migration batch and then manually start it afterwards by using the **Start-MigrationBatch** cmdlet. This example creates a migration batch called "StagedBatch1" and uses the migration endpoint that was created in the previous step.
  
```powershell
New-MigrationBatch -Name StagedBatch1 -SourceEndpoint StagedEndpoint -AutoStart
```

This example also creates a migration batch called "StagedBatch1" and uses the migration endpoint that was created in the previous step. Because the  _AutoStart_ parameter isn't included, the migration batch has to be manually started on the migration dashboard or by using **Start-MigrationBatch** cmdlet. As previously stated, only one cutover migration batch can exist at a time.
  
```powershell
New-MigrationBatch -Name StagedBatch1 -SourceEndpoint StagedEndpoint
```

#### <a name="verify-it-worked"></a>Verificare che il passaggio di migrazione sia avvenuto correttamente

Eseguire il seguente comando in PowerShell di Exchange Online per visualizzare informazioni su "StagedBatch1":
  
```powershell
Get-MigrationBatch -Identity StagedBatch1 | Format-List
```

È inoltre possibile verificare che il batch sia stato avviato eseguendo il comando riportato di seguito:
  
```powershell
Get-MigrationBatch -Identity StagedBatch1 | Format-List Status
```

Per ulteriori informazioni sul cmdlet **Get-MigrationBatch**, vedere[Get-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536441).
  
### <a name="step-5-convert-on-premises-mailboxes-to-mail-enabled-users"></a>Passaggio 5: convertire le cassette postali locali in utenti abilitati alla posta
<a name="BK_Endpoint"> </a>

After you have successfully migrated a batch of mailboxes, you need some way to let users get to their mail. A user whose mailbox has been migrated now has both a mailbox on-premises and one in Office 365. Users who have a mailbox in Office 365 will stop receiving new mail in their on-premises mailbox. 
  
Because you are not done with your migrations, you are not yet ready to direct all users to Office 365 for their email. So what do you do for those people who have both? What you can do is change the on-premises mailboxes that you've already migrated to mail-enabled users. When you change from a mailbox to a mail-enabled user, you can direct the user to Office 365 for their email instead of going to their on-premises mailbox. 
  
Another important reason to convert on-premises mailboxes to mail-enabled users is to retain proxy addresses from the Office 365 mailboxes by copying proxy addresses to the mail-enabled users. This lets you manage cloud-based users from your on-premises organization by using Active Directory. Also, if you decide to decommission your on-premises Exchange Server organization after all mailboxes are migrated to Office 365, the proxy addresses you've copied to the mail-enabled users will remain in your on-premises Active Directory.
    
### <a name="step-6-delete-a-staged-migration-batch"></a>Passaggio 6: eliminare un batch di migrazione a fasi
<a name="BK_Endpoint"> </a>

 After all mailboxes in a migration batch have been successfully migrated, and you've converted the on-premises mailboxes in the batch to mail-enabled users, you're ready to delete a staged migration batch. Be sure to verify that mail is being forwarded to the Office 365 mailboxes in the migration batch. When you delete a staged migration batch, the migration service cleans up any records related to the migration batch and deletes the migration batch.
  
Per eliminare il batch di migrazione "StagedBatch1" in PowerShell di Exchange Online, eseguire il comando riportato di seguito.
  
```powershell
Remove-MigrationBatch -Identity StagedBatch1
```

Per ulteriori informazioni sul cmdlet **Remove-MigrationBatch**, vedere[Remove-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536481).
  
#### <a name="verify-it-worked"></a>Verificare che il passaggio di migrazione sia avvenuto correttamente

Eseguire il seguente comando in PowerShell di Exchange Online per visualizzare informazioni su "IMAPBatch1":
  
```powershell
Get-MigrationBatch StagedBatch1
```

Il comando restituirà il batch di migrazione con uno stato di **Rimozione in corso** o restituirà un errore che informa che non è possibile trovare il batch di migrazione, confermandone l'eliminazione.
  
Per ulteriori informazioni sul cmdlet **Get-MigrationBatch**, vedere[Get-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536441).
  
### <a name="step7-assign-licenses-to-office-365-users"></a>Passaggio 7: assegnare le licenze agli utenti di Office 365
<a name="BK_Endpoint"> </a>

Attivare gli account utente di Office 365 per gli account migrati tramite l'assegnazione delle licenze. Se non si assegna una licenza, la cassetta postale viene disabilitata allo scadere del periodo di prova (30 giorni). Per assegnare una licenza nell'interfaccia di amministrazione di Microsoft 365, vedere [Assegnare licenze per Office 365 per le aziende o annullarne l'assegnazione](https://go.microsoft.com/fwlink/?LinkId=536681).
  
### <a name="step-8-complete-post-migration-tasks"></a>Passaggio 8: completare le attività successive alla migrazione
<a name="BK_Postmigration"> </a>

- **Create an Autodiscover DNS record so users can easily get to their mailboxes.** After all on-premises mailboxes are migrated to Office 365, you can configure an Autodiscover DNS record for your Office 365 organization to enable users to easily connect to their new Office 365 mailboxes with Outlook and mobile clients. This new Autodiscover DNS record has to use the same namespace that you're using for your Office 365 organization. For example, if your cloud-based namespace is cloud.contoso.com, the Autodiscover DNS record you need to create is autodiscover.cloud.contoso.com.
    
    Office 365 uses a CNAME record to implement the Autodiscover service for Outlook and mobile clients. The Autodiscover CNAME record must contain the following information:
    
  - **Alias:** individuazione automatica
    
  - **Destinazione:** autodiscover.outlook.com
    
    Per ulteriori informazioni, vedere [Creare record DNS per Office 365 quando si gestiscono i record DNS](https://go.microsoft.com/fwlink/p/?LinkId=535028).
    
- **Decommission on-premises Exchange servers.** After you've verified that all email is being routed directly to the Office 365 mailboxes, and you no longer need to maintain your on-premises email organization or don't plan on implementing an SSO solution, you can uninstall Exchange from your servers and remove your on-premises Exchange organization.
    
    Per ulteriori informazioni, vedere gli argomenti seguenti:
    
  - [Modifica o eliminazione di Exchange 2010](https://go.microsoft.com/fwlink/?LinkId=217936)
    
  - [Come rimuovere un'organizzazione di Exchange 2007](https://go.microsoft.com/fwlink/?LinkID=100485)
    
  - [Disinstallazione di Exchange Server 2003](https://go.microsoft.com/fwlink/?LinkID=56561)
    

