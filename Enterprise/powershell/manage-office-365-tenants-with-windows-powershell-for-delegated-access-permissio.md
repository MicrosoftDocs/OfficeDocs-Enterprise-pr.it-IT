---
title: Gestire i tenant Microsoft 365 con Windows PowerShell per i partner di autorizzazione accesso delegato (DAP, Delegate Access Permissions)
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
search.appverid:
- MET150
ms.collection:
- Ent_O365
- M365-subscription-management
f1.keywords:
- NOCSH
ms.custom: ''
ms.assetid: f92d5116-5b66-4150-ad20-1452fc3dd712
description: 'Riepilogo: utilizzare Windows PowerShell per Microsoft 365 per gestire le locazione del cliente.'
ms.openlocfilehash: a57f66ec02f5ba69006c17a9cf734e622017b8fb
ms.sourcegitcommit: 6e608d957082244d1b4ffb47942e5847ec18c0b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "44998232"
---
# <a name="manage-microsoft-365-tenants-with-windows-powershell-for-delegated-access-permissions-dap-partners"></a><span data-ttu-id="0002b-103">Gestire i tenant Microsoft 365 con Windows PowerShell per i partner di autorizzazione accesso delegato (DAP, Delegate Access Permissions)</span><span class="sxs-lookup"><span data-stu-id="0002b-103">Manage Microsoft 365 tenants with Windows PowerShell for Delegated Access Permissions (DAP) partners</span></span>

<span data-ttu-id="0002b-104">Windows PowerShell consente ai partner di syndication e Cloud Solution Provider (CSP) di amministrare e segnalare facilmente le impostazioni di locazione dei clienti che non sono disponibili nell'interfaccia di amministrazione di Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="0002b-104">Windows PowerShell allows Syndication and Cloud Solution Provider (CSP) partners to easily administer and report on customer tenancy settings that are not available in the Microsoft 365 admin center.</span></span> <span data-ttu-id="0002b-105">Tenere presente che le autorizzazioni Amministra per conto terzi (AOBO, Administer On Behalf Of) sono necessarie all'account amministratore del partner per connettersi ai tenancy dei clienti.</span><span class="sxs-lookup"><span data-stu-id="0002b-105">Note that Administer on Behalf Of (AOBO) permissions are required for the partner administrator account to connect to its customer tenancies.</span></span>
  
<span data-ttu-id="0002b-106">I partner di autorizzazione accesso delegato (DAP, Delegated Access Permission) sono partner di Syndication e Cloud Solution Provider (CSP).</span><span class="sxs-lookup"><span data-stu-id="0002b-106">Delegated Access Permission (DAP) partners are Syndication and Cloud Solution Providers (CSP) Partners.</span></span> <span data-ttu-id="0002b-107">Di solito, rappresentano fornitori di rete o telecomunicazioni di altre aziende.</span><span class="sxs-lookup"><span data-stu-id="0002b-107">They are frequently network or telecom providers to other companies.</span></span> <span data-ttu-id="0002b-108">Essi bundle Microsoft 365 abbonamenti nelle loro offerte di servizi ai propri clienti.</span><span class="sxs-lookup"><span data-stu-id="0002b-108">They bundle Microsoft 365 subscriptions into their service offerings to their customers.</span></span> <span data-ttu-id="0002b-109">Quando vendono un abbonamento a Microsoft 365, vengono concesse automaticamente amministra per conto di (AOBO) le autorizzazioni per il cliente locazione in modo che possano amministrare e segnalare sul locazione cliente.</span><span class="sxs-lookup"><span data-stu-id="0002b-109">When they sell a Microsoft 365 subscription, they are automatically granted Administer On Behalf Of (AOBO) permissions to the customer tenancies so they can administer and report on the customer tenancies.</span></span>
## <a name="what-do-you-need-to-know-before-you-begin"></a><span data-ttu-id="0002b-110">Che cosa è necessario sapere prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0002b-110">What do you need to know before you begin?</span></span>

<span data-ttu-id="0002b-111">The procedures in this topic require you to connect to Windows PowerShell for Office 365.</span><span class="sxs-lookup"><span data-stu-id="0002b-111">The procedures in this topic require you to connect to Windows PowerShell for Office 365.</span></span> <span data-ttu-id="0002b-112">For instructions, see [Connect to Office 365 PowerShell](connect-to-office-365-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0002b-112">For instructions, see [Connect to Office 365 PowerShell](connect-to-office-365-powershell.md).</span></span>
  
<span data-ttu-id="0002b-113">Sono necessarie anche le credenziali di amministratore tenant del partner.</span><span class="sxs-lookup"><span data-stu-id="0002b-113">You also need your partner tenant administrator credentials.</span></span>
  
## <a name="what-do-you-want-to-do"></a><span data-ttu-id="0002b-114">Operazione desiderata</span><span class="sxs-lookup"><span data-stu-id="0002b-114">What do you want to do?</span></span>

### <a name="list-all-tenant-ids"></a><span data-ttu-id="0002b-115">Elencare tutti gli ID tenant</span><span class="sxs-lookup"><span data-stu-id="0002b-115">List all tenant IDs</span></span>

> [!NOTE]
> <span data-ttu-id="0002b-116">If you have more than 500 tenants, scope the cmdlet syntax with either  _-All_ or _-MaxResultsParameter_.</span><span class="sxs-lookup"><span data-stu-id="0002b-116">If you have more than 500 tenants, scope the cmdlet syntax with either  _-All_ or _-MaxResultsParameter_.</span></span> <span data-ttu-id="0002b-117">This applies to other cmdlets that can give a large output, such as **Get-MsolUser**.</span><span class="sxs-lookup"><span data-stu-id="0002b-117">This applies to other cmdlets that can give a large output, such as **Get-MsolUser**.</span></span>
  
<span data-ttu-id="0002b-118">Per elencare tutti gli ID tenant dei clienti ai quali si ha accesso, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="0002b-118">To list all customer tenant Ids that you have access to, run this command.</span></span>
  
```
Get-MsolPartnerContract -All | Select-Object TenantId
```

<span data-ttu-id="0002b-119">In questo modo verrà visualizzato un elenco di tutti i tenant dei clienti tramite **TenantId**.</span><span class="sxs-lookup"><span data-stu-id="0002b-119">This will display a listing of all your customer tenants by **TenantId**.</span></span>

>[!Note]
><span data-ttu-id="0002b-120">PowerShell Core non supporta il modulo di Microsoft Azure Active Directory per Windows PowerShell e i cmdlet con **MSOL** all'interno del nome.</span><span class="sxs-lookup"><span data-stu-id="0002b-120">PowerShell Core does not support the Microsoft Azure Active Directory Module for Windows PowerShell module and cmdlets with **Msol** in their name.</span></span> <span data-ttu-id="0002b-121">Per continuare a usare i cmdlet, è necessario eseguirli in Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0002b-121">To continue using these cmdlets, you must run them from Windows PowerShell.</span></span>
>
  
### <a name="get-a-tenant-id-by-using-the-domain-name"></a><span data-ttu-id="0002b-122">Ottenere un ID tenant tramite il nome di dominio</span><span class="sxs-lookup"><span data-stu-id="0002b-122">Get a tenant ID by using the domain name</span></span>

<span data-ttu-id="0002b-123">To get the **TenantId** for a specific customer tenant by domain name, run this command.</span><span class="sxs-lookup"><span data-stu-id="0002b-123">To get the **TenantId** for a specific customer tenant by domain name, run this command.</span></span> <span data-ttu-id="0002b-124">Replace _<domainname.onmicrosoft.com>_ with the actual domain name of the customer tenant that you want.</span><span class="sxs-lookup"><span data-stu-id="0002b-124">Replace _<domainname.onmicrosoft.com>_ with the actual domain name of the customer tenant that you want.</span></span>
  
```
Get-MsolPartnerContract -DomainName <domainname.onmicrosoft.com> | Select-Object TenantId
```

### <a name="list-all-domains-for-a-tenant"></a><span data-ttu-id="0002b-125">Elencare tutti i domini per un tenant</span><span class="sxs-lookup"><span data-stu-id="0002b-125">List all domains for a tenant</span></span>

<span data-ttu-id="0002b-126">To get all domains for any one customer tenant, run this command.</span><span class="sxs-lookup"><span data-stu-id="0002b-126">To get all domains for any one customer tenant, run this command.</span></span> <span data-ttu-id="0002b-127">Replace  _<customer TenantId value>_ with the actual value.</span><span class="sxs-lookup"><span data-stu-id="0002b-127">Replace  _<customer TenantId value>_ with the actual value.</span></span>
  
```
Get-MsolDomain -TenantId <customer TenantId value>
```

<span data-ttu-id="0002b-128">Se sono stati registrati ulteriori domini, verranno restituiti tutti i domini associati al **TenantId** del cliente.</span><span class="sxs-lookup"><span data-stu-id="0002b-128">If you have registered additional domains, this will return all domains associated with the customer **TenantId**.</span></span>
  
### <a name="get-a-mapping-of-all-tenants-and-registered-domains"></a><span data-ttu-id="0002b-129">Ottenere un mapping di tutti i tenant e i domini registrati</span><span class="sxs-lookup"><span data-stu-id="0002b-129">Get a mapping of all tenants and registered domains</span></span>

<span data-ttu-id="0002b-130">The previous Windows PowerShell for Office 365 commands showed you how to retrieve either tenant IDs or domains but not both at the same time, and with no clear mapping between them all.</span><span class="sxs-lookup"><span data-stu-id="0002b-130">The previous Windows PowerShell for Office 365 commands showed you how to retrieve either tenant IDs or domains but not both at the same time, and with no clear mapping between them all.</span></span> <span data-ttu-id="0002b-131">This command generates a listing of all your customer tenant IDs and their domains.</span><span class="sxs-lookup"><span data-stu-id="0002b-131">This command generates a listing of all your customer tenant IDs and their domains.</span></span>
  
```
$Tenants = Get-MsolPartnerContract -All; $Tenants | foreach {$Domains = $_.TenantId; Get-MsolDomain -TenantId $Domains | fl @{Label="TenantId";Expression={$Domains}},name}
```

### <a name="get-all-users-for-a-tenant"></a><span data-ttu-id="0002b-132">Ottenere tutti gli utenti per un tenant</span><span class="sxs-lookup"><span data-stu-id="0002b-132">Get all users for a tenant</span></span>

<span data-ttu-id="0002b-133">This will display the **UserPrincipalName**, the **DisplayName**, and the **isLicensed** status for all users for a particular tenant.</span><span class="sxs-lookup"><span data-stu-id="0002b-133">This will display the **UserPrincipalName**, the **DisplayName**, and the **isLicensed** status for all users for a particular tenant.</span></span> <span data-ttu-id="0002b-134">Replace _<customer TenantId value>_ with the actual value.</span><span class="sxs-lookup"><span data-stu-id="0002b-134">Replace _<customer TenantId value>_ with the actual value.</span></span>
  
```
Get-MsolUser -TenantID <customer TenantId value>
```

### <a name="get-all-details-about-a-user"></a><span data-ttu-id="0002b-135">Ottenere tutti i dettagli di un utente</span><span class="sxs-lookup"><span data-stu-id="0002b-135">Get all details about a user</span></span>

<span data-ttu-id="0002b-136">If you want to see all the properties of a particular user, run this command.</span><span class="sxs-lookup"><span data-stu-id="0002b-136">If you want to see all the properties of a particular user, run this command.</span></span> <span data-ttu-id="0002b-137">Replace  _<customer TenantId value>_ and _<user principal name value>_ with the actual values.</span><span class="sxs-lookup"><span data-stu-id="0002b-137">Replace  _<customer TenantId value>_ and _<user principal name value>_ with the actual values.</span></span>
  
```
Get-MsolUser -TenantId <customer TenantId value> -UserPrincipalName <user principal name value>
```

### <a name="add-users-set-options-and-assign-licenses"></a><span data-ttu-id="0002b-138">Aggiungere utenti, impostare opzioni e assegnare licenze</span><span class="sxs-lookup"><span data-stu-id="0002b-138">Add users, set options, and assign licenses</span></span>

<span data-ttu-id="0002b-139">La creazione in blocco, la configurazione e la gestione delle licenze degli utenti di Microsoft 365 sono particolarmente efficienti utilizzando Windows PowerShell per Office 365.</span><span class="sxs-lookup"><span data-stu-id="0002b-139">The bulk creation, configuration, and licensing of Microsoft 365 users is particularly efficient by using Windows PowerShell for Office 365.</span></span> <span data-ttu-id="0002b-140">In questa procedura di due passaggi, prima vengono create le voci per tutti gli utenti che si desidera aggiungere in un file CSV (con valori delimitati da virgole), per poi importare tale file usando Windows PowerShell per Office 365.</span><span class="sxs-lookup"><span data-stu-id="0002b-140">In this two-step process, you first create entries for all the users you want to add in a comma-separated value (CSV) file and then import that file by using Windows PowerShell for Office 365.</span></span> 
  
#### <a name="create-a-csv-file"></a><span data-ttu-id="0002b-141">Creare un file CSV</span><span class="sxs-lookup"><span data-stu-id="0002b-141">Create a CSV file</span></span>

<span data-ttu-id="0002b-142">Creare un file CSV utilizzando questo formato:</span><span class="sxs-lookup"><span data-stu-id="0002b-142">Create a CSV file by using this format:</span></span>
  
-  `UserPrincipalName,FirstName,LastName,DisplayName,Password,TenantId,UsageLocation,LicenseAssignment`
    
<span data-ttu-id="0002b-143">dove:</span><span class="sxs-lookup"><span data-stu-id="0002b-143">where:</span></span>
  
- <span data-ttu-id="0002b-144">**UsageLocation**: The value for this is the two-letter ISO country/region code of the user.</span><span class="sxs-lookup"><span data-stu-id="0002b-144">**UsageLocation**: The value for this is the two-letter ISO country/region code of the user.</span></span> <span data-ttu-id="0002b-145">The country/region codes can be looked up at the[ISO Online Browsing Platform](https://go.microsoft.com/fwlink/p/?LinkId=532703).</span><span class="sxs-lookup"><span data-stu-id="0002b-145">The country/region codes can be looked up at the[ISO Online Browsing Platform](https://go.microsoft.com/fwlink/p/?LinkId=532703).</span></span> <span data-ttu-id="0002b-146">For example, the code for the United States is US, and the code for Brazil is BR.</span><span class="sxs-lookup"><span data-stu-id="0002b-146">For example, the code for the United States is US, and the code for Brazil is BR.</span></span> 
    
- <span data-ttu-id="0002b-147">**LicenseAssignment**: The value for this uses this format: `syndication-account:<PROVISIONING_ID>`.</span><span class="sxs-lookup"><span data-stu-id="0002b-147">**LicenseAssignment**: The value for this uses this format: `syndication-account:<PROVISIONING_ID>`.</span></span> <span data-ttu-id="0002b-148">For example, if you are assigning customer tenant users O365_Business_Premium licenses, the **LicenseAssignment** value looks like this: **syndication-account:O365_Business_Premium**.</span><span class="sxs-lookup"><span data-stu-id="0002b-148">For example, if you are assigning customer tenant users O365_Business_Premium licenses, the **LicenseAssignment** value looks like this: **syndication-account:O365_Business_Premium**.</span></span> <span data-ttu-id="0002b-149">You will find the PROVISIONING_IDs in the Syndication Partner Portal that you have access to as a Syndication or CSP partner.</span><span class="sxs-lookup"><span data-stu-id="0002b-149">You will find the PROVISIONING_IDs in the Syndication Partner Portal that you have access to as a Syndication or CSP partner.</span></span>
    
#### <a name="import-the-csv-file-and-create-the-users"></a><span data-ttu-id="0002b-150">Importare il file CSV e creare gli utenti</span><span class="sxs-lookup"><span data-stu-id="0002b-150">Import the CSV file and create the users</span></span>

<span data-ttu-id="0002b-151">After you have your CSV file created, run this command to create user accounts with non-expiring passwords that the user must change at first sign-in and that assigns the license you specify.</span><span class="sxs-lookup"><span data-stu-id="0002b-151">After you have your CSV file created, run this command to create user accounts with non-expiring passwords that the user must change at first sign-in and that assigns the license you specify.</span></span> <span data-ttu-id="0002b-152">Be sure to substitute the correct CSV file name.</span><span class="sxs-lookup"><span data-stu-id="0002b-152">Be sure to substitute the correct CSV file name.</span></span>
  
```
Import-Csv .\FILENAME.CSV | foreach {New-MsolUser -UserPrincipalName $_.UserPrincipalName -DisplayName $_.DisplayName -FirstName $_.FirstName -LastName $_.LastName -Password $_.Password -UsageLocation $_.UsageLocation -LicenseAssignment $_.LicenseAssignment -ForceChangePassword:$true -PasswordNeverExpires:$true -TenantId $_.TenantId}
```

## <a name="see-also"></a><span data-ttu-id="0002b-153">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0002b-153">See also</span></span>

#### 

[<span data-ttu-id="0002b-154">Guida per partner</span><span class="sxs-lookup"><span data-stu-id="0002b-154">Help for partners</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=533477)

