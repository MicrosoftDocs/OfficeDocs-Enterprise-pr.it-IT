---
title: Utilizzo di PowerShell per eseguire una migrazione IMAP a Office 365
ms.author: sirkkuw
author: sirkkuw
manager: scotv
ms.date: 12/15/2017
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom: DecEntMigration
ms.assetid: c28de4a5-1e8e-4491-9421-af066cde7cdd
description: 'Riepilogo: informazioni sull''utilizzo di Windows PowerShell per eseguire una migrazione IMAP a Office 365.'
ms.openlocfilehash: 6187207d57723c9c69fa6fdc7885c91de6d5080f
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2017
---
# <a name="use-powershell-to-perform-an-imap-migration-to-office-365"></a><span data-ttu-id="21468-103">Utilizzo di PowerShell per eseguire una migrazione IMAP a Office 365</span><span class="sxs-lookup"><span data-stu-id="21468-103">Use PowerShell to perform an IMAP migration to Office 365</span></span>

 <span data-ttu-id="21468-104">**Riepilogo:** Informazioni su come utilizzare Windows PowerShell per eseguire una migrazione IMAP a Office 365.</span><span class="sxs-lookup"><span data-stu-id="21468-104">**Summary:** Learn how to use Windows PowerShell to perform an IMAP migration to Office 365.</span></span>
  
<span data-ttu-id="21468-p101">Come parte del processo di distribuzione di Office 365, è possibile scegliere di eseguire la migrazione dei contenuti delle cassette postali degli utenti da un servizio di posta elettronica IMAP (Internet Mail Access Protocol) a Office 365. In questo articolo vengono illustrate le attività per una migrazione IMAP della posta elettronica tramite PowerShell di Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="21468-p101">As part of the process of deploying Office 365, you can choose to migrate the contents of user mailboxes from an Internet Mail Access Protocol (IMAP) email service to Office 365. This article walks you through the tasks for an email IMAP migration by using Exchange Online PowerShell.</span></span> 
  
> [!NOTE]
> <span data-ttu-id="21468-p102">È anche possibile utilizzare l'interfaccia di amministrazione di Exchange per eseguire una migrazione IMAP. Vedere [Eseguire la migrazione di cassette postali IMAP a Office 365](https://go.microsoft.com/fwlink/p/?LinkId=536685).</span><span class="sxs-lookup"><span data-stu-id="21468-p102">You can also use the Exchange admin center to perform an IMAP migration. See [Migrate your IMAP mailboxes to Office 365](https://go.microsoft.com/fwlink/p/?LinkId=536685).</span></span> 
  
## <a name="what-do-you-need-to-know-before-you-begin"></a><span data-ttu-id="21468-109">Che cosa è necessario sapere prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="21468-109">What do you need to know before you begin?</span></span>

<span data-ttu-id="21468-p103">Tempo stimato per il completamento di questa attività: tra i 2 e i 5 minuti per creare un batch di migrazione. Dopo l'avvio del batch di migrazione, la durata della migrazione varia in base al numero di cassette postali nel batch, alla dimensione di ogni cassetta postale e alla capacità di rete disponibile. Per informazioni su altri fattori che influenzano il tempo necessario per eseguire la migrazione delle cassette postali su Office 365, vedere l'articolo relativo alle [prestazioni della migrazione](https://go.microsoft.com/fwlink/p/?LinkId=275079).</span><span class="sxs-lookup"><span data-stu-id="21468-p103">Estimated time to complete this task: 2-5 minutes to create a migration batch. After the migration batch is started, the duration of the migration will vary based on the number of mailboxes in the batch, the size of each mailbox, and your available network capacity. For information about other factors that affect how long it takes to migrate mailboxes to Office 365, see [Migration Performance](https://go.microsoft.com/fwlink/p/?LinkId=275079).</span></span>
  
<span data-ttu-id="21468-p104">È necessario disporre delle autorizzazioni per poter eseguire queste procedure. Per verificare le autorizzazioni necessarie, vedere la voce "Migrazione" in una tabella nell'argomento [Autorizzazioni di destinatari](https://go.microsoft.com/fwlink/p/?LinkId=534105).</span><span class="sxs-lookup"><span data-stu-id="21468-p104">You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Migration" entry in a table in the [Recipients Permissions](https://go.microsoft.com/fwlink/p/?LinkId=534105) topic.</span></span>
  
<span data-ttu-id="21468-p105">Per utilizzare i cmdlet di PowerShell di Exchange Online, è necessario eseguire l'accesso e importare i cmdlet nella sessione di Windows PowerShell locale. Per le istruzioni, vedere [Connettersi a Exchange Online tramite Remote PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=534121).</span><span class="sxs-lookup"><span data-stu-id="21468-p105">To use the Exchange Online PowerShell cmdlets, you need to sign in and import the cmdlets into your local Windows PowerShell session. See [Connect to Exchange Online using remote PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=534121) for instructions.</span></span>
  
<span data-ttu-id="21468-117">Per un elenco completo dei comandi di migrazione, vedere [Cmdlet di spostamento e migrazione](https://go.microsoft.com/fwlink/p/?LinkId=534750).</span><span class="sxs-lookup"><span data-stu-id="21468-117">For a full list of migration commands, see [Move and migration cmdlets](https://go.microsoft.com/fwlink/p/?LinkId=534750).</span></span>
  
<span data-ttu-id="21468-118">Le seguenti limitazioni valgono per le migrazioni IMAP:</span><span class="sxs-lookup"><span data-stu-id="21468-118">The following restrictions apply to IMAP migrations:</span></span>
  
- <span data-ttu-id="21468-p106">È possibile eseguire la migrazione solo degli elementi nella cartella Posta in arrivo o in altre cartelle di posta di un utente. Non è possibile migrare i contatti, gli elementi del calendario e le attività.</span><span class="sxs-lookup"><span data-stu-id="21468-p106">Only items in a user's inbox or other mail folders can be migrated. You can't migrate contacts, calendar items, or tasks.</span></span>
    
- <span data-ttu-id="21468-121">È possibile eseguire la migrazione di un massimo di 500.000 elementi dalla cassetta postale di un utente.</span><span class="sxs-lookup"><span data-stu-id="21468-121">A maximum of 500,000 items can be migrated from a user's mailbox.</span></span>
    
- <span data-ttu-id="21468-122">La dimensione massima di un messaggio di posta elettronica di cui è possibile eseguire la migrazione è 35 MB.</span><span class="sxs-lookup"><span data-stu-id="21468-122">The maximum message size that can be migrated is 35 MB.</span></span>
    
## <a name="migration-steps"></a><span data-ttu-id="21468-123">Procedura della migrazione</span><span class="sxs-lookup"><span data-stu-id="21468-123">Migration steps</span></span>

### <a name="step-1-prepare-for-an-imap-migration"></a><span data-ttu-id="21468-124">Passaggio 1: predisporre una migrazione IMAP</span><span class="sxs-lookup"><span data-stu-id="21468-124">Step 1: Prepare for an IMAP migration</span></span>
<span data-ttu-id="21468-125"><a name="BK_Step1"> </a></span><span class="sxs-lookup"><span data-stu-id="21468-125"><a name="BK_Step1"> </a></span></span>

- <span data-ttu-id="21468-p107">**Se si dispone di un dominio per l'organizzazione IMAP, è possibile aggiungerlo a Office 365 come dominio accettato.** Se si desidera utilizzare lo stesso dominio già in uso per le cassette postali di Office 365, sarà necessario aggiungerlo a Office 365 come dominio accettato. Dopo averlo aggiunto, è possibile creare utenti in Office 365. Per ulteriori informazioni, vedere[Verificare il dominio in Office 365](https://go.microsoft.com/fwlink/p/?LinkId=534110).</span><span class="sxs-lookup"><span data-stu-id="21468-p107">**If you have a domain for you IMAP organization, add it as an accepted domain of your Office 365 organization.** If you want to use the same domain you already own for your Office 365 mailboxes, you first have to add it as an accepted domain to Office 365. After you have added it, you can create your users in Office 365. For more information, see[Verify your domain in Office 365](https://go.microsoft.com/fwlink/p/?LinkId=534110).</span></span>
    
- <span data-ttu-id="21468-p108">**Aggiungere ciascun utente a Office 365 affinché possa disporre di una cassetta postale di Office 365.** Per istruzioni, vedere[Aggiungere utenti a Office 365 per le aziende](https://go.microsoft.com/fwlink/p/?LinkId=535065).</span><span class="sxs-lookup"><span data-stu-id="21468-p108">**Add each user to Office 365 so that they have an Office 365 mailbox.** For instructions, see[Add users to Office 365 for business](https://go.microsoft.com/fwlink/p/?LinkId=535065).</span></span>
    
- <span data-ttu-id="21468-p109">**Ottenere il nome di dominio completo (FQDN) del server IMAP**. È necessario fornire il nome di dominio completo (FQDN), denominato anche nome completo del computer, del server IMAP dal quale si desidera migrare i dati delle cassette postali quando si crea un endpoint di migrazione IMAP. Utilizzare un client IMAP o il comando PING per verificare che sia possibile utilizzare il nome di dominio completo per comunicare con il server IMAP tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="21468-p109">**Obtain the FQDN of the IMAP server**. You need to provide the fully qualified domain name (FQDN) (also called the full computer name) of the IMAP server that you will migrate mailbox data from when you create an IMAP migration endpoint. Use an IMAP client or the PING command to verify that you can use the FQDN to communicate with the IMAP server over the Internet.</span></span>
    
- <span data-ttu-id="21468-p110">**Configurare il firewall per consentire connessioni IMAP**. Potrebbe essere necessario aprire porte nel firewall dell'organizzazione che ospita il server IMAP, in modo che il traffico di rete proveniente dal datacenter Microsoft durante la migrazione sia in grado di accedere all'organizzazione che ospita il server IMAP. Per un elenco di indirizzi IP utilizzati dai datacenter Microsoft, vedere l'articolo relativo agli [URL e intervalli di indirizzi IP per Office 365](https://go.microsoft.com/fwlink/p/?LinkId=535066).</span><span class="sxs-lookup"><span data-stu-id="21468-p110">**Configure the firewall to allow IMAP connections**. You might have to open ports in the firewall of the organization that hosts the IMAP server so network traffic originating from the Microsoft datacenter during the migration is allowed to enter the organization that hosts the IMAP server. For a list of IP addresses used by Microsoft datacenters, see [Exchange Online URLs and IP Address Ranges](https://go.microsoft.com/fwlink/p/?LinkId=535066).</span></span>
    
- <span data-ttu-id="21468-p111">**Assegnare all'account dell'amministratore le autorizzazioni necessarie per accedere alle cassette postali nell'organizzazione IMAP**. Se si utilizzano le credenziali di amministratore nel file CSV, l'account in uso deve disporre delle autorizzazioni necessarie per accedere alle cassette postali locali. Le autorizzazioni necessarie per accedere alle cassette postali dell'utente sono determinate da uno specifico server IMAP.</span><span class="sxs-lookup"><span data-stu-id="21468-p111">**Assign the administrator account permissions to access mailboxes in your IMAP organization**. If you use administrator credentials in the CSV file, the account that you use must have the necessary permissions to access the on-premises mailboxes. The permissions required to access user mailboxes is determined by the particular IMAP server.</span></span> 
    
- <span data-ttu-id="21468-p112">**Per utilizzare i cmdlet di PowerShell di Exchange Online**, è necessario eseguire l'accesso e importare i cmdlet nella sessione di Windows PowerShell locale. Per le istruzioni, vedere [Connettersi a Exchange Online tramite Remote PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=534121).</span><span class="sxs-lookup"><span data-stu-id="21468-p112">**To use the Exchange Online PowerShell cmdlets**, you need to sign in and import the cmdlets into your local Windows PowerShell session. See [Connect to Exchange Online using remote PowerShell](https://go.microsoft.com/fwlink/p/?LinkId=534121) for instructions.</span></span>
    
    <span data-ttu-id="21468-143">Per un elenco completo dei comandi di migrazione, vedere [Cmdlet di spostamento e migrazione](https://go.microsoft.com/fwlink/p/?LinkId=534750).</span><span class="sxs-lookup"><span data-stu-id="21468-143">For a full list of migration commands, see [Move and migration cmdlets](https://go.microsoft.com/fwlink/p/?LinkId=534750).</span></span>
    
- <span data-ttu-id="21468-p113">**Verificare che sia possibile connettersi al server IMAP**. Eseguire il seguente comando di PowerShell di Exchange Online per verificare le impostazioni di connessione al server IMAP.</span><span class="sxs-lookup"><span data-stu-id="21468-p113">**Verify that you can connect to your IMAP server**. Run the following command in Exchange Online PowerShell to test the connection settings to your IMAP server.</span></span>
    
  ```
  Test-MigrationServerAvailability -IMAP -RemoteServer <FQDN of IMAP server> -Port <143 or 993> -Security <None, Ssl, or Tls>
  ```

    <span data-ttu-id="21468-146">Per il valore del parametro **Port**, in genere si utilizza 143 per le connessioni non crittografate o Transport Layer Security (TLS) e 993 per le connessioni SSL.</span><span class="sxs-lookup"><span data-stu-id="21468-146">For the value of the **Port** parameter, it's typical to use 143 for unencrypted or Transport Layer Security (TLS) connections and to use 993 for SSL connections.</span></span>
    
### <a name="step-2-create-a-csv-file-for-an-imap-migration-batch"></a><span data-ttu-id="21468-147">Passaggio 2: creare un file CSV per un batch di migrazione IMAP</span><span class="sxs-lookup"><span data-stu-id="21468-147">Step 2: Create a CSV file for an IMAP migration batch</span></span>
<span data-ttu-id="21468-148"><a name="BK_Step2"> </a></span><span class="sxs-lookup"><span data-stu-id="21468-148"><a name="BK_Step2"> </a></span></span>

<span data-ttu-id="21468-p114">Identificare il gruppo di utenti per i quali si desidera effettuare la migrazione delle cassette postali in un batch di migrazione IMAP. Ogni riga nel file CSV contiene informazioni necessarie per connettersi a una cassetta postale nel sistema di messaggistica IMAP.</span><span class="sxs-lookup"><span data-stu-id="21468-p114">Identify the group of users whose mailboxes you want to migrate in an IMAP migration batch. Each row in the CSV file contains information necessary to connect to a mailbox in the IMAP messaging system.</span></span>
  
<span data-ttu-id="21468-151">Di seguito sono riportati gli attributi necessari per ogni utente:</span><span class="sxs-lookup"><span data-stu-id="21468-151">Here are the required attributes for each user:</span></span> 
  
- <span data-ttu-id="21468-152">**EmailAddress** specifica l'ID utente per la cassetta postale di Office 365 dell'utente.</span><span class="sxs-lookup"><span data-stu-id="21468-152">**EmailAddress** specifies the user ID for the user's Office 365 mailbox.</span></span>
    
- <span data-ttu-id="21468-153">**UserName** specifica il nome di accesso per l'account da utilizzare per accedere alla cassetta postale sul server IMAP.</span><span class="sxs-lookup"><span data-stu-id="21468-153">**UserName** specifies the logon name for the account to use to access the mailbox on the IMAP server.</span></span>
    
- <span data-ttu-id="21468-154">**Password** specifica la password per l'account nella colonna **UserName**.</span><span class="sxs-lookup"><span data-stu-id="21468-154">**Password** specifies the password for the account in the **UserName** column.</span></span>
    
<span data-ttu-id="21468-p115">Di seguito viene illustrato un esempio di formato per il file CSV. In questo esempio viene eseguita la migrazione di tre cassette postali:</span><span class="sxs-lookup"><span data-stu-id="21468-p115">Here's an example of the format for the CSV file. In this example, three mailboxes are migrated:</span></span>
  
```
EmailAddress,UserName,Password
terrya@contoso.edu,terry.adams,1091990
annb@contoso.edu,ann.beebe,2111991
paulc@contoso.edu,paul.cannon,3281986
```

<span data-ttu-id="21468-157">Per l'attributo **UserName**, oltre al nome utente, è possibile utilizzare le credenziali di un account al quale sono state assegnate le autorizzazioni necessarie per accedere alle cassette postali nel server IMAP. Di seguito, sono riportati alcuni dei formati specifici utilizzati per alcuni server IMAP:</span><span class="sxs-lookup"><span data-stu-id="21468-157">For the **UserName** attribute, in addition to the user name, you can use the credentials of an account that has been assigned the necessary permissions to access mailboxes on the IMAP server, the following are some of the specific formats used for some of the IMAP servers:</span></span>
  
 <span data-ttu-id="21468-158">**Microsoft Exchange:**</span><span class="sxs-lookup"><span data-stu-id="21468-158">**Microsoft Exchange:**</span></span>
  
<span data-ttu-id="21468-p116">Se si sta eseguendo la migrazione della posta elettronica dall'implementazione IMAP per Microsoft Exchange, utilizzare il formato **Dominio/NomeUtente_Amministratore/NomeUtente_Utente** per l'attributo **UserName** nel file CSV. Si supponga di eseguire la migrazione della posta elettronica da Exchange per Terry Adams, Ann Beebe e Paul Cannon. Si dispone di un account di amministratore della posta, con nome utente **mailadmin** e password **P@ssw0rd**. Il file CSV risulterà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="21468-p116">If you're migrating email from the IMAP implementation for Microsoft Exchange, use the format **Domain/Admin_UserName/User_UserName** for the **UserName** attribute in the CSV file. Let's say you're migrating email from Exchange for Terry Adams, Ann Beebe, and Paul Cannon. You have a mail administrator account, where the user name is **mailadmin** and the password is **P@ssw0rd**. Here's what your CSV file would look like:</span></span>
  
```
EmailAddress,UserName,Password
terrya@contoso.edu,contoso-students/mailadmin/terry.adams,P@ssw0rd
annb@contoso.edu,contoso-students/mailadmin/ann.beebe,P@ssw0rd
paulc@contoso.edu,contoso-students/mailadmin/paul.cannon,P@ssw0rd
```

 <span data-ttu-id="21468-163">**Dovecot:**</span><span class="sxs-lookup"><span data-stu-id="21468-163">**Dovecot:**</span></span>
  
<span data-ttu-id="21468-p117">Per i server IMAP che supportano SASL (Simple Authentication and Security Layer), come ad esempio il server IMAP Dovecot, utilizzare il formato **NomeUtente_Utente*NomeUtente_Amministratore**, dove l'asterisco ( * ) è un carattere separatore configurabile. Si supponga di eseguire la migrazione della posta elettronica degli stessi utenti da un server IMAP Dovecot, con le credenziali di amministratore **mailadmin** e **P@ssw0rd**. Il file CSV risulterà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="21468-p117">For IMAP servers that support Simple Authentication and Security Layer (SASL), such as a Dovecot IMAP server, use the format **User_UserName*Admin_UserName**, where the asterisk ( * ) is a configurable separator character. Let's say you're migrating those same users' email from a Dovecot IMAP server using the administrator credentials **mailadmin** and **P@ssw0rd**. Here's what your CSV file would look like:</span></span>
  
```
EmailAddress,UserName,Password
terrya@contoso.edu,terry.adams*mailadmin,P@ssw0rd
annb@contoso.edu,ann.beebe*mailadmin,P@ssw0rd
paulc@contoso.edu,paul.cannon*mailadmin,P@ssw0rd
```

 <span data-ttu-id="21468-167">**Mirapoint:**</span><span class="sxs-lookup"><span data-stu-id="21468-167">**Mirapoint:**</span></span>
  
<span data-ttu-id="21468-p118">Se si sta eseguendo la migrazione della posta elettronica da Mirapoint Message Server, utilizzare il formato **#utente@dominio#NomeUtente_Amministratore#** per le credenziali di amministratore. Per eseguire la migrazione della posta elettronica da Mirapoint con le credenziali di amministratore **mailadmin** e **P@ssw0rd**, il file CSV risulterà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="21468-p118">If you're migrating email from Mirapoint Message Server, use the format **#user@domain#Admin_UserName#** for the administrator credentials. To migrate email from Mirapoint using the administrator credentials **mailadmin** and **P@ssw0rd**, your CSV file would look like this:</span></span>
  
```
EmailAddress,UserName,Password
terrya@contoso.edu,#terry.adams@contoso-students.edu#mailadmin#,P@ssw0rd
annb@contoso.edu,#ann.beebe@contoso-students.edu#mailadmin#,P@ssw0rd
paulc@contoso.edu,#paul.cannon@contoso-students.edu#mailadmin#,P@ssw0rd
```

 <span data-ttu-id="21468-170">**Courier IMAP:**</span><span class="sxs-lookup"><span data-stu-id="21468-170">**Courier IMAP:**</span></span>
  
<span data-ttu-id="21468-p119">Alcuni sistemi di posta elettronica di origine, ad esempio Courier IMAP, non supportano l'utilizzo di credenziali di amministratore delle cassette postali per eseguire la migrazione delle cassette postali a Office 365. Al contrario, è possibile configurare il sistema di posta elettronica di origine affinché utilizzi le cartelle condivise virtuali. Con le cartelle condivise virtuali, è possibile utilizzare le credenziali di amministratore delle cassette postali per accedere alle cassette postali dell'utente nel sistema di posta elettronica di origine. Per ulteriori informazioni su come configurare le cartelle condivise virtuali per Courier IMAP, vedere [Cartelle condivise](https://go.microsoft.com/fwlink/p/?LinkId=398870).</span><span class="sxs-lookup"><span data-stu-id="21468-p119">Some source email systems, such as Courier IMAP, don't support using mailbox admin credentials to migrate mailboxes to Office 365. Instead, you can set up your source email system to use virtual shared folders. By using virtual shared folders, you can use the mailbox admin credentials to access user mailboxes on the source email system. For more information about how to configure virtual shared folders for Courier IMAP, see [Shared Folders](https://go.microsoft.com/fwlink/p/?LinkId=398870).</span></span>
  
<span data-ttu-id="21468-p120">Per eseguire la migrazione delle cassette postali dopo avere configurato le cartelle condivise virtuali nel sistema di posta elettronica di origine, è necessario includere l'attributo **UserRoot** facoltativo nel file di migrazione. Questo attributo consente di specificare il percorso della cassetta postale di ogni utente nella struttura di cartelle condivise virtuali nel sistema di posta elettronica di origine. Ad esempio, il percorso per la cassetta postale di Terry è /utenti/terry.adams.</span><span class="sxs-lookup"><span data-stu-id="21468-p120">To migrate mailboxes after you set up virtual shared folders on your source email system, you have to include the optional attribute **UserRoot** in the migration file. This attribute specifies the location of each user's mailbox in the virtual shared folder structure on the source email system. For example, the path to Terry's mailbox is /users/terry.adams.</span></span>
  
<span data-ttu-id="21468-178">Di seguito è riportato un esempio di file CSV contenente l'attributo **UserRoot**:</span><span class="sxs-lookup"><span data-stu-id="21468-178">Here's an example of a CSV file that contains the **UserRoot** attribute:</span></span>
  
```
EmailAddress,UserName,Password,UserRoot
terrya@contoso.edu,mailadmin,P@ssw0rd,/users/terry.adams
annb@contoso.edu,mailadmin,P@ssw0rd,/users/ann.beebe
paulc@contoso.edu,mailadmin,P@ssw0rd,/users/paul.cannon
```

### <a name="step-3-create-an-imap-migration-endpoint"></a><span data-ttu-id="21468-179">Passaggio 3: creare un endpoint di migrazione IMAP</span><span class="sxs-lookup"><span data-stu-id="21468-179">Step 3: Create an IMAP migration endpoint</span></span>
<span data-ttu-id="21468-180"><a name="BK_Step3"> </a></span><span class="sxs-lookup"><span data-stu-id="21468-180"><a name="BK_Step3"> </a></span></span>

<span data-ttu-id="21468-p121">Per eseguire la migrazione della posta elettronica correttamente, Office 365 deve essere in grado di connettersi e comunicare con il sistema di posta elettronica di origine. A tale scopo, in Office 365 viene utilizzato un endpoint di migrazione. L'endpoint di migrazione definisce inoltre il numero di cassette postali da migrare contemporaneamente e il numero di cassette postali da sincronizzare contemporaneamente durante la sincronizzazione incrementale, che si verifica ogni 24 ore. Per creare un endpoint di migrazione per la migrazione IMAP, è necessario innanzitutto [connettersi a Exchange Online](https://go.microsoft.com/fwlink/p/?LinkId=534121).</span><span class="sxs-lookup"><span data-stu-id="21468-p121">To migrate email successfully, Office 365 needs to connect to and communicate with the source email system. To do this, Office 365 uses a migration endpoint. The migration endpoint also defines the number of mailboxes to migrate simultaneously and the number of mailboxes to synchronize simultaneously during incremental synchronization, which occurs once every 24 hours. To create a migration end point for IMAP migration, first [connect to Exchange Online](https://go.microsoft.com/fwlink/p/?LinkId=534121).</span></span> 
  
<span data-ttu-id="21468-185">Per un elenco completo dei comandi di migrazione, vedere [Cmdlet di spostamento e migrazione](https://go.microsoft.com/fwlink/p/?LinkId=534750).</span><span class="sxs-lookup"><span data-stu-id="21468-185">For a full list of migration commands, see [Move and migration cmdlets](https://go.microsoft.com/fwlink/p/?LinkId=534750).</span></span>
  
<span data-ttu-id="21468-186">Per creare l'endpoint di migrazione IMAP denominato "IMAPEndpoint" in PowerShell di Exchange Online, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="21468-186">To create the IMAP migration endpoint called "IMAPEndpoint" in Exchange Online PowerShell, run the following command:</span></span>
  
```
New-MigrationEndpoint -IMAP -Name IMAPEndpoint -RemoteServer imap.contoso.com -Port 993 -Security Ssl

```

<span data-ttu-id="21468-p122">È inoltre possibile aggiungere i parametri per specificare le migrazioni contemporanee, le migrazioni incrementali contemporanee e le porte da utilizzare. Il seguente comando di PowerShell di Exchange Online consente di creare un endpoint di migrazione IMAP denominato "IMAPEndpoint" che supporta 50 migrazioni contemporanee e fino a 25 sincronizzazioni incrementali contemporanee. Inoltre, consente di configurare l'endpoint per l'utilizzo della porta 143 per la crittografia TLS.</span><span class="sxs-lookup"><span data-stu-id="21468-p122">You can also add parameters to specify concurrent migrations, concurrent incremental migrations, and the port to use. The following Exchange Online PowerShell command creates an IMAP migration endpoint called "IMAPEndpoint" that supports 50 concurrent migrations and up to 25 concurrent incremental synchronizations. It also configures the endpoint to use port 143 for TLS encryption.</span></span>
  
```
New-MigrationEndpoint -IMAP -Name IMAPEndpoint -RemoteServer imap.contoso.com -Port 143 -Security Tls -MaxConcurrentMigrations
50 -MaxConcurrentIncrementalSyncs 25
```

<span data-ttu-id="21468-190">Per ulteriori informazioni sul cmdlet **New-MigrationEndpoint**, vedere[New-MigrationEndpoint](https://go.microsoft.com/fwlink/p/?LinkId=536437).</span><span class="sxs-lookup"><span data-stu-id="21468-190">For more information about the **New-MigrationEndpoint** cmdlet, see[New-MigrationEndpoint](https://go.microsoft.com/fwlink/p/?LinkId=536437).</span></span>
  
#### <a name="verify-it-worked"></a><span data-ttu-id="21468-191">Verificare che il passaggio di migrazione sia avvenuto correttamente</span><span class="sxs-lookup"><span data-stu-id="21468-191">Verify it worked</span></span>

<span data-ttu-id="21468-192">Eseguire il seguente comando in PowerShell di Exchange Online per visualizzare informazioni su "IMAPEndpoint":</span><span class="sxs-lookup"><span data-stu-id="21468-192">Run the following command in Exchange Online PowerShell to display information about the "IMAPEndpoint":</span></span>
  
```
Get-MigrationEndpoint IMAPEndpoint | Format-List EndpointType,RemoteServer,Port,Security,Max*
```

### <a name="step-4-create-and-start-an-imap-migration-batch"></a><span data-ttu-id="21468-193">Passaggio 4: creare e avviare un batch di migrazione IMAP</span><span class="sxs-lookup"><span data-stu-id="21468-193">Step 4: Create and start an IMAP migration batch</span></span>
<span data-ttu-id="21468-194"><a name="BK_Step4"> </a></span><span class="sxs-lookup"><span data-stu-id="21468-194"><a name="BK_Step4"> </a></span></span>

<span data-ttu-id="21468-p123">È possibile utilizzare il cmdlet [New-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536439) per creare un batch di migrazione per una migrazione IMAP. È possibile creare un batch di migrazione e avviarlo automaticamente includendo il parametro _AutoStart_. In alternativa, è possibile creare il batch di migrazione e avviarlo in un secondo momento utilizzando il cmdlet [Start-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536440).</span><span class="sxs-lookup"><span data-stu-id="21468-p123">You can use the [New-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536439) cmdlet to create a migration batch for an IMAP migration. You can create a migration batch and start it automatically by including the _AutoStart_ parameter. Alternatively, you can create the migration batch and then start it afterwards by using the[Start-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536440) cmdlet.</span></span>
  
<span data-ttu-id="21468-198">Il seguente comando di PowerShell di Exchange Online avvierà automaticamente il batch di migrazione denominato "IMAPBatch1" utilizzando un endpoint IMAP denominato "IMAPEndpoint":</span><span class="sxs-lookup"><span data-stu-id="21468-198">The following Exchange Online PowerShell command will automatically start the migration batch called "IMAPBatch1" using the IMAP endpoint called "IMAPEndpoint":</span></span>
  
```
New-MigrationBatch -Name IMAPBatch1 -SourceEndpoint IMAPEndpoint -CSVData ([System.IO.File]::ReadAllBytes("C:\\Users\\Administrator\\Desktop\\IMAPmigration_1.csv")) -AutoStart
```

#### <a name="verify-it-worked"></a><span data-ttu-id="21468-199">Verificare che il passaggio di migrazione sia avvenuto correttamente</span><span class="sxs-lookup"><span data-stu-id="21468-199">Verify it worked</span></span>

<span data-ttu-id="21468-200">Eseguire il cmdlet [Get-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536441) per visualizzare informazioni su "IMAPBatch1":</span><span class="sxs-lookup"><span data-stu-id="21468-200">Run the [Get-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536441) cmdlet to display information about the "IMAPBatch1":</span></span>
  
```
Get-MigrationBatch -Identity IMAPBatch1 | Format-List
```

<span data-ttu-id="21468-201">È inoltre possibile verificare che il batch sia stato avviato eseguendo il comando riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="21468-201">You can also verify that the batch has started by running the following command:</span></span>
  
```
Get-MigrationBatch -Identity IMAPBatch1 | Format-List Status
```

### <a name="step-5-route-your-email-to-office-365"></a><span data-ttu-id="21468-202">Passaggio 5: instradare la posta elettronica a Office 365</span><span class="sxs-lookup"><span data-stu-id="21468-202">Step 5: Route your email to Office 365</span></span>
<span data-ttu-id="21468-203"><a name="BK_Step5"> </a></span><span class="sxs-lookup"><span data-stu-id="21468-203"><a name="BK_Step5"> </a></span></span>

<span data-ttu-id="21468-p124">I sistemi di posta elettronica utilizzano un record DNS denominato record MX per individuare dove recapitare i messaggi di posta elettronica. Durante il processo di migrazione della posta elettronica, il record MX fa riferimento al sistema di posta elettronica di origine. Al termine della migrazione della posta elettronica a Office 365, il record MX fa riferimento a Office 365. Ciò contribuisce a garantire che la posta elettronica sia recapitata alle cassette postali di Office 365. Spostando il record MX, è inoltre possibile disattivare il sistema di posta elettronica precedente al momento più opportuno.</span><span class="sxs-lookup"><span data-stu-id="21468-p124">Email systems use a DNS record called an MX record to figure out where to deliver emails. During the email migration process, your MX record was pointing to your source email system. Now that the email migration to Office 365 is complete, it's time to point your MX record at Office 365. This helps make sure that email is delivered to your Office 365 mailboxes. By moving the MX record, you can also turn off your old email system when you're ready.</span></span> 
  
<span data-ttu-id="21468-p125">Per molti provider DNS, sono disponibili istruzioni specifiche per [modificare il record MX](https://go.microsoft.com/fwlink/p/?LinkId=279163). Se il provider DNS non è incluso oppure si desidera farsi un'idea delle direzioni generali, vengono fornite anche [istruzioni generali sul record MX](https://go.microsoft.com/fwlink/?LinkId=397449).</span><span class="sxs-lookup"><span data-stu-id="21468-p125">For many DNS providers, there are specific instructions to [change your MX record](https://go.microsoft.com/fwlink/p/?LinkId=279163). If your DNS provider isn't included, or if you want to get a sense of the general directions, [general MX record instructions ](https://go.microsoft.com/fwlink/?LinkId=397449) are provided as well.</span></span>
  
<span data-ttu-id="21468-p126">È possibile che i sistemi di posta elettronica dei propri clienti e partner impieghino fino a 72 ore per riconoscere il record MX modificato. Attendere almeno 72 ore prima di procedere con l'attività successiva: Passaggio 6: eliminare il batch di migrazione IMAP.</span><span class="sxs-lookup"><span data-stu-id="21468-p126">It can take up to 72 hours for the email systems of your customers and partners to recognize the changed MX record. Wait at least 72 hours before you proceed to the next task: Step 6: Delete IMAP migration batch.</span></span> 
  
### <a name="step-6-delete-imap-migration-batch"></a><span data-ttu-id="21468-213">Passaggio 6: eliminare il batch di migrazione IMAP</span><span class="sxs-lookup"><span data-stu-id="21468-213">Step 6: Delete IMAP migration batch</span></span>
<span data-ttu-id="21468-214"><a name="BK_Step6"> </a></span><span class="sxs-lookup"><span data-stu-id="21468-214"><a name="BK_Step6"> </a></span></span>

<span data-ttu-id="21468-p127">Dopo aver modificato il record MX e verificato che tutta la posta elettronica venga instradata alle cassette postali di Office 365, informare gli utenti che la loro posta sarà spostata in Office 365. Dopo questa operazione, è possibile eliminare il batch di migrazione IMAP. Verificare le seguenti condizioni prima di eliminare il batch di migrazione.</span><span class="sxs-lookup"><span data-stu-id="21468-p127">After you change the MX record and verify that all email is being routed to Office 365 mailboxes, notify the users that their mail is going to Office 365. After this, you can delete the IMAP migration batch. Verify the following before you delete the migration batch.</span></span>
  
- <span data-ttu-id="21468-p128">Tutti gli utenti utilizzano cassette postali di Office 365. Dopo l'eliminazione del batch, la posta inviata alle cassette postali nel server di Exchange locale non viene copiata nelle cassette postali di Office 365 corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="21468-p128">All users are using Office 365 mailboxes. After the batch is deleted, mail sent to mailboxes on the on-premises Exchange Server isn't copied to the corresponding Office 365 mailboxes.</span></span>
    
- <span data-ttu-id="21468-p129">Le cassette postali di Office 365 sono state sincronizzate almeno una volta dal momento in cui ha avuto inizio l'invio della posta elettronica direttamente verso di loro. A tale scopo, assicurarsi che il valore nella casella Ultima sincronizzazione per il batch di migrazione sia più recente di quello dell'inizio dell'invio della posta direttamente alle cassette postali di Office 365.</span><span class="sxs-lookup"><span data-stu-id="21468-p129">Office 365 mailboxes were synchronized at least once after mail began being sent directly to them. To do this, make sure that the value in the Last Synced Time box for the migration batch is more recent than when mail started being routed directly to Office 365 mailboxes.</span></span>
    
<span data-ttu-id="21468-222">Per eliminare il batch di migrazione "IMAPBatch1" da PowerShell di Exchange Online, eseguire il comando riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="21468-222">To delete the "IMAPBatch1" migration batch from Exchange Online PowerShell, run the following command:</span></span>
  
```
Remove-MigrationBatch -Identity IMAPBatch1
```

<span data-ttu-id="21468-223">Per ulteriori informazioni sul cmdlet **Remove-MigrationBatch**, vedere[Remove-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536481).</span><span class="sxs-lookup"><span data-stu-id="21468-223">For more information about the **Remove-MigrationBatch** cmdlet, see[Remove-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536481).</span></span>
  
#### <a name="verify-it-worked"></a><span data-ttu-id="21468-224">Verificare che il passaggio di migrazione sia avvenuto correttamente</span><span class="sxs-lookup"><span data-stu-id="21468-224">Verify it worked</span></span>

<span data-ttu-id="21468-225">Eseguire il seguente comando in PowerShell di Exchange Online per visualizzare informazioni su "IMAPBatch1":</span><span class="sxs-lookup"><span data-stu-id="21468-225">Run the following command in Exchange Online PowerShell to display information about the "IMAPBatch1":</span></span>
  
```
Get-MigrationBatch IMAPBatch1"
```

<span data-ttu-id="21468-226">Il comando restituirà il batch di migrazione con uno stato di **Rimozione in corso** o restituirà un errore che informa che non è possibile trovare il batch di migrazione, confermandone l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="21468-226">The command will return either the migration batch with a status of **Removing**, or it will return an error stating that migration batch couldn't be found, verifying that the batch was deleted.</span></span>
  
<span data-ttu-id="21468-227">Per ulteriori informazioni sul cmdlet **Get-MigrationBatch**, vedere[Get-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536441).</span><span class="sxs-lookup"><span data-stu-id="21468-227">For more information about the **Get-MigrationBatch** cmdlet, see[Get-MigrationBatch](https://go.microsoft.com/fwlink/p/?LinkId=536441).</span></span>
  
## <a name="see-also"></a><span data-ttu-id="21468-228">See also</span><span class="sxs-lookup"><span data-stu-id="21468-228">See also</span></span>

#### 

[<span data-ttu-id="21468-229">Risoluzione dei problemi della migrazione IMAP</span><span class="sxs-lookup"><span data-stu-id="21468-229">IMAP Migration Troubleshooter</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=536482)
