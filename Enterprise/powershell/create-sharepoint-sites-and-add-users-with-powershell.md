---
title: Creare siti di SharePoint Online e aggiungere utenti con PowerShell di Office 365
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 05/01/2018
ms.audience: Admin
ms.topic: hub-page
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom:
- PowerShell
- Ent_Office_Other
ms.assetid: d0d3877a-831f-4744-96b0-d8167f06cca2
description: 'Riepilogo: Utilizzare Office 365 PowerShell per creare nuovi siti di SharePoint Online e quindi aggiungere utenti e gruppi a tali siti.'
ms.openlocfilehash: 0a0438917f6e7010b56703ce0bf73e89e1db0533
ms.sourcegitcommit: 74cdb2534bce376abc9cf4fef85ff039c46ee790
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="create-sharepoint-online-sites-and-add-users-with-office-365-powershell"></a><span data-ttu-id="7d19f-103">Creare siti di SharePoint Online e aggiungere utenti con PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="7d19f-103">Create SharePoint Online sites and add users with Office 365 PowerShell</span></span>

 <span data-ttu-id="7d19f-104">**Riepilogo:** Utilizzare Office 365 PowerShell per creare nuovi siti di SharePoint Online e quindi aggiungere utenti e gruppi a tali siti.</span><span class="sxs-lookup"><span data-stu-id="7d19f-104">**Summary:** Use Office 365 PowerShell to create new SharePoint Online sites, and then add users and groups to those sites.</span></span>

<span data-ttu-id="7d19f-p101">Quando si utilizza Office 365 PowerShell per creare siti di SharePoint Online e aggiungere gli utenti, è possibile rapidamente e ripetutamente eseguire attività molto più rapidamente rispetto a quanto possibile in interfaccia di amministrazione di Office 356. È inoltre possibile eseguire attività che non sono possibili da eseguire nell'interfaccia di amministrazione di Office 356.</span><span class="sxs-lookup"><span data-stu-id="7d19f-p101">When you use Office 365 PowerShell to create SharePoint Online sites and add users, you can quickly and repeatedly perform tasks much faster than you can in the Office 356 admin center. You can also perform tasks that are not possible to perform in the Office 356 admin center.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="7d19f-107">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="7d19f-107">Before you begin</span></span>

<span data-ttu-id="7d19f-p102">Le procedure descritte in questo argomento richiedono per la connessione a SharePoint Online. Per ulteriori informazioni, vedere [connettersi a PowerShell per SharePoint Online](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps)</span><span class="sxs-lookup"><span data-stu-id="7d19f-p102">The procedures in this topic require you to connect to SharePoint Online. For instructions, see [Connect to SharePoint Online PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps)</span></span>

## <a name="step-1-create-new-site-collections-using-office-365-powershell"></a><span data-ttu-id="7d19f-110">Passaggio 1: Creare nuove raccolte siti con Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d19f-110">Step 1: Create new site collections using Office 365 PowerShell</span></span>

<span data-ttu-id="7d19f-p103">Creare più siti con Office 365 PowerShell e un file csv creato utilizzando il codice riportato di seguito viene fornito e il blocco note. Per questa procedura, saranno sostituzione informazioni segnaposto indicate tra parentesi quadre con le proprie informazioni specifiche del tenant e del sito. Questo processo consente di creare un singolo file ed eseguire un comando di Office 365 PowerShell singolo che utilizza tale file. In questo modo le azioni eseguite ripetibili e portatili ed elimina molte, se non tutti gli errori che possono provenire da digitare i comandi lunghi in SharePoint Online Management Shell. Esistono due parti a questa procedura. Innanzitutto si creerà un file CSV e quindi si sarà fare riferimento file CSV con Office 365 PowerShell, che verrà utilizzato il relativo contenuto per creare i siti.</span><span class="sxs-lookup"><span data-stu-id="7d19f-p103">Create multiple sites using Office 365 PowerShell and a .csv file that you create using the example code provided and Notepad. For this procedure, you’ll be replacing the placeholder information shown in brackets with your own site- and tenant-specific information. This process allows you to create a single file and run a single Office 365 PowerShell command that uses that file. This makes the actions taken both repeatable and portable and eliminates many, if not all, errors that can come from typing long commands into the SharePoint Online Management Shell. There are two parts to this procedure. First you’ll create a .csv file, and then you’ll reference that .csv file using Office 365 PowerShell, which will use its contents to create the sites.</span></span>

<span data-ttu-id="7d19f-p104">Il cmdlet PowerShell di Office 365 consente di importare il file CSV e reindirizzato a un ciclo all'interno delle parentesi graffe indicante la prima riga del file come intestazioni di colonna. Il cmdlet di Office 365 PowerShell quindi scorre i record rimanenti, crea una nuova raccolta siti per ogni record e assegna le proprietà della raccolta siti in base alle intestazioni di colonna.</span><span class="sxs-lookup"><span data-stu-id="7d19f-p104">The Office 365 PowerShell cmdlet imports the .csv file and pipes it to a loop inside the curly brackets that reads the first line of the file as column headers. The Office 365 PowerShell cmdlet then iterates through the remaining records, creates a new site collection for each record, and assigns properties of the site collection according to the column headers.</span></span>

###<a name="create-a-csv-file"></a><span data-ttu-id="7d19f-119">Creare un file .csv</span><span class="sxs-lookup"><span data-stu-id="7d19f-119">Create a .csv file</span></span>

1. <span data-ttu-id="7d19f-120">Aprire Blocco note e incollare il seguente blocco di testo:</span><span class="sxs-lookup"><span data-stu-id="7d19f-120">Open Notepad, and paste the following text block into it:</span></span></br>
```
Owner,StorageQuota,Url,ResourceQuota,Template,TimeZoneID,Name
owner@tenant.onmicrosoft.com,100,https://tenant.sharepoint.com/sites/TeamSite01,25,EHS#1,10,Contoso Team Site
owner@tenant.onmicrosoft.com,100,https://tenant.sharepoint.com/sites/Blog01,25,BLOG#0,10,Contoso Blog
owner@tenant.onmicrosoft.com,150,https://tenant.sharepoint.com/sites/Project01,25,PROJECTSITE#0,10,Project Alpha
owner@tenant.onmicrosoft.com,150,https://tenant.sharepoint.com/sites/Community01,25,COMMUNITY#0,10,Community Site
```</br>Where *tenant* is the name of your tenant, and *owner* is the user name of the user on your tenant to whom you want to grant the role of primary site collection administrator.</br>(You can press Ctrl+H when you use Notepad to bulk replace faster.)</br>
2. Save the file on your desktop as **SiteCollections.csv**.

 > [!TIP]
> Before you use this or any other .csv or Windows PowerShell script file, it is good practice to make sure that there are no extraneous or nonprinting characters. Open the file in Word, and in the ribbon, click the paragraph icon to show nonprinting characters. There should be no extraneous nonprinting characters. For example, there should be no paragraph marks beyond the final one at the end of the file.

### Run the Windows PowerShell command

1. At the Windows PowerShell prompt, type or copy and paste the following cmdlet, and press Enter:</br>
```
<span data-ttu-id="7d19f-121">Import-Csv C:\users\MyAlias\desktop\SiteCollections.csv | ForEach-Object {New-SPOSite-proprietario $_. Proprietario - StorageQuota $_. StorageQuota-Url $_. URL - NoWait - ResourceQuota $_. ResourceQuota-modello $_. Modello - TimeZoneID $_. TimeZoneID-Title $_. Nome}</span><span class="sxs-lookup"><span data-stu-id="7d19f-121">Import-Csv C:\users\MyAlias\desktop\SiteCollections.csv | ForEach-Object {New-SPOSite -Owner $_.Owner -StorageQuota $_.StorageQuota -Url $_.Url -NoWait -ResourceQuota $_.ResourceQuota -Template $_.Template -TimeZoneID $_.TimeZoneID -Title $_.Name}</span></span>
```
</br>Where *MyAlias* equals your user alias.</br>
2. Wait for the Windows PowerShell prompt to reappear. It might take a minute or two.</br>
3. At the Windows PowerShell prompt, type or copy and paste the following cmdlet, and press Enter:</br>
```
<span data-ttu-id="7d19f-122">Get-SPOSite-dettagliate | Format-Table - AutoSize</span><span class="sxs-lookup"><span data-stu-id="7d19f-122">Get-SPOSite -Detailed | Format-Table -AutoSize</span></span>
```</br>
4. Note the new site collections in the list. You should see the following site collections: **contosotest**, **TeamSite01**, **Blog01**, and **Project01**.

That’s it. You’ve created multiple site collections using the .csv file you created and a single Windows PowerShell cmdlet. You’re now ready to create and assign users to these sites.

## Step 2: Add users and groups

Now you’re going to create users and add them to a site collection group. You will then use a .csv file to bulk upload new groups and users.

The following procedures assume that you successfully created the site collections contosotest, TeamSite01, Blog01, and Project01.

### Create .csv and .ps1 files

1. Open Notepad, and paste the following text block into it:</br>
```
<span data-ttu-id="7d19f-123">Sito, gruppo, PermissionLevels https://tenant.sharepoint.com/sites/contosotest, Contoso Project Leads, controllo completo https://tenant.sharepoint.com/sites/contosotest, controllori, Contoso solo visualizzazione https://tenant.sharepoint.com/sites/contosotest, progettisti di Contoso, progettazione https://tenant.sharepoint.com/sites/TeamSite01, XT1000 i responsabili dei Team, controllo completo https://tenant.sharepoint.com/sites/TeamSite01, i consulenti XT1000, modificare https://tenant.sharepoint.com/sites/Blog01, Contoso Blog Finestre di progettazione, progettazione https://tenant.sharepoint.com/sites/Blog01, Contoso Blog redattori, modificare https://tenant.sharepoint.com/sites/Project01, Project alfa responsabili approvazione, controllo completo</span><span class="sxs-lookup"><span data-stu-id="7d19f-123">Site,Group,PermissionLevels https://tenant.sharepoint.com/sites/contosotest,Contoso Project Leads,Full Control https://tenant.sharepoint.com/sites/contosotest,Contoso Auditors,View Only https://tenant.sharepoint.com/sites/contosotest,Contoso Designers,Design https://tenant.sharepoint.com/sites/TeamSite01,XT1000 Team Leads,Full Control https://tenant.sharepoint.com/sites/TeamSite01,XT1000 Advisors,Edit https://tenant.sharepoint.com/sites/Blog01,Contoso Blog Designers,Design https://tenant.sharepoint.com/sites/Blog01,Contoso Blog Editors,Edit https://tenant.sharepoint.com/sites/Project01,Project Alpha Approvers,Full Control</span></span>
```
</br>Where *tenant* equals your tenant name.</br>
2. Save the file to your desktop as **GroupsAndPermissions.csv**.</br>
3. Open a new instance of Notepad, and paste the following text block into it:</br>
```
<span data-ttu-id="7d19f-124">Gruppo, LoginName, sito Contoso Project Leads username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/contosotest Contoso controllori, username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/contosotest Contoso finestre di progettazione, username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/contosotest XT1000 responsabili del Team, UserName@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/TeamSite01 XT1000 consulenti, username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/TeamSite01 progettisti Contoso Blog, username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/Blog01 Contoso Blog redattori, username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/Blog01 Responsabili approvazione alfa Project, username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/Project01</span><span class="sxs-lookup"><span data-stu-id="7d19f-124">Group,LoginName,Site Contoso Project Leads,username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/contosotest Contoso Auditors,username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/contosotest Contoso Designers,username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/contosotest XT1000 Team Leads,username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/TeamSite01 XT1000 Advisors,username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/TeamSite01 Contoso Blog Designers,username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/Blog01 Contoso Blog Editors,username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/Blog01 Project Alpha Approvers,username@tenant.onmicrosoft.com,https://tenant.sharepoint.com/sites/Project01</span></span>
```
</br>Where *tenant* equals your tenant name, and *username* equals the user name of an existing user.</br>
4. Save the file to your desktop as **Users.csv**.</br>
5. Open a new instance of Notepad, and paste the following text block into it:</br>
```
<span data-ttu-id="7d19f-125">Import-Csv C:\users\MyAlias\desktop\GroupsAndPermissions.csv | ForEach-Object {New-SPOSiteGroup-$_di gruppo. Gruppo - PermissionLevels $_. PermissionLevels-$_del sito. C:\users\MyAlias\desktop\Users.csv Import-Csv Site} | dove {aggiungere-SPOUser-gruppo $_. Gruppo – LoginName $_. LoginName-sito $_. Site}</span><span class="sxs-lookup"><span data-stu-id="7d19f-125">Import-Csv C:\users\MyAlias\desktop\GroupsAndPermissions.csv | ForEach-Object {New-SPOSiteGroup -Group $_.Group -PermissionLevels $_.PermissionLevels -Site $_.Site} Import-Csv C:\users\MyAlias\desktop\Users.csv | where {Add-SPOUser -Group $_.Group –LoginName $_.LoginName -Site $_.Site}</span></span>
```
</br>Where MyAlias equals the user name of the user that is currently logged on.</br>
6. Save the file to your desktop as **UsersAndGroups.ps1**. This is a simple Windows PowerShell script.

You’re now ready to run the UsersAndGroup.ps1 script to add users and groups to multiple site collections.

### Run UsersAndGroups.ps1 script

1. Return to the SharePoint Online Management Shell.</br>
2. At the Windows PowerShell prompt, type or copy and paste the following line, and press Enter:</br>
```
<span data-ttu-id="7d19f-126">Set-ExecutionPolicy Bypass</span><span class="sxs-lookup"><span data-stu-id="7d19f-126">Set-ExecutionPolicy Bypass</span></span>
```</br>
3. At the confirmation prompt, press **Y**.</br>
4. At the Windows PowerShell prompt, type or copy and paste the following, and press Enter:</br>
```
<span data-ttu-id="7d19f-127">c:\users\MyAlias\desktop\UsersAndGroups.ps1</span><span class="sxs-lookup"><span data-stu-id="7d19f-127">c:\users\MyAlias\desktop\UsersAndGroups.ps1</span></span>
```
</br>Where *MyAlias* equals your user name.</br>
5. Wait for the prompt to return before moving on. You will first see the groups appear as they are created. Then you will see the group list repeated as users are added.

## See also

[Connect to SharePoint Online PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps)

[Manage SharePoint Online site groups Office 365 PowerShell](manage-sharepoint-site-groups-with-powershell.md)

[Manage Office 365 with Office 365 PowerShell](manage-office-365-with-office-365-powershell.md)
  
[Getting started with Office 365 PowerShell](getting-started-with-office-365-powershell.md)

