---
title: Eliminare e ripristinare account utente con Office 365 PowerShell
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 12/15/2017
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom:
- DecEntMigration
- PowerShell
- Ent_Office_Other
- O365ITProTrain
ms.assetid: 209c9868-448c-49bc-baae-11e28b923a39
description: Imparare a utilizzare Office 365 PowerShell per eliminare e ripristinare gli account utente di Office 365.
ms.openlocfilehash: 8404395ea9594cea1a2e772cecbeb011756b7754
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2017
---
# <a name="delete-and-restore-user-accounts-with-office-365-powershell"></a><span data-ttu-id="55fe5-103">Eliminare e ripristinare account utente con Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="55fe5-103">Delete and restore user accounts with Office 365 PowerShell</span></span>

<span data-ttu-id="55fe5-104">**Riepilogo:**  Imparare a utilizzare Office 365 PowerShell per eliminare e ripristinare gli account utente di Office 365.</span><span class="sxs-lookup"><span data-stu-id="55fe5-104">**Summary:**  Learn how to use Office 365 PowerShell to delete and restore Office 365 user accounts.</span></span>
  
<span data-ttu-id="55fe5-p101">Quando si utilizza PowerShell di Office 365 per eliminare un account utente, quest'ultimo non viene rimosso in modo definitivo. Infatti, si hanno a disposizione 30 giorni di tempo per ripristinare l'account utente eliminato.</span><span class="sxs-lookup"><span data-stu-id="55fe5-p101">When you use Office 365 PowerShell to delete a user account, the account isn't permanently deleted. You can restore the deleted user account within 30 days.</span></span>
  
## <a name="before-you-begin"></a><span data-ttu-id="55fe5-107">Informazioni preliminari</span><span class="sxs-lookup"><span data-stu-id="55fe5-107">Before you begin</span></span>

- <span data-ttu-id="55fe5-p102">Le procedure descritte in questo argomento richiedono all'utente di connettersi a PowerShell di Office 365. Per istruzioni, vedere [Connettersi a PowerShell di Office 365](connect-to-office-365-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="55fe5-p102">The procedures in this topic require you to connect to Office 365 PowerShell. For instructions, see [Connect to Office 365 PowerShell](connect-to-office-365-powershell.md).</span></span>
    
- <span data-ttu-id="55fe5-110">Se si utilizza il cmdlet **Get-MsolUser** senza utilizzare il _-tutti_ parametro, vengono restituiti solo i primi 500 account.</span><span class="sxs-lookup"><span data-stu-id="55fe5-110">If you use the **Get-MsolUser** cmdlet without using the _-All_ parameter, only the first 500 accounts are returned.</span></span>
    
## <a name="use-office-365-powershell-to-block-access-to-individual-user-accounts"></a><span data-ttu-id="55fe5-111">Utilizzare PowerShell di Office 365 per bloccare l'accesso a singoli account utente</span><span class="sxs-lookup"><span data-stu-id="55fe5-111">Use Office 365 PowerShell to block access to individual user accounts</span></span>
<span data-ttu-id="55fe5-112"><a name="ShortVersion"> </a></span><span class="sxs-lookup"><span data-stu-id="55fe5-112"><a name="ShortVersion"> </a></span></span>

<span data-ttu-id="55fe5-113">Per eliminare un account utente, utilizzare la sintassi riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="55fe5-113">To delete a user account, use the following syntax:</span></span>
  
```
Remove-MsolUser -UserPrincipalName <Account>
```

<span data-ttu-id="55fe5-114">Questo esempio elimina l'account utente BelindaN@litwareinc.com.</span><span class="sxs-lookup"><span data-stu-id="55fe5-114">This example deletes the user account BelindaN@litwareinc.com.</span></span>
  
```
Remove-MsolUser -UserPrincipalName belindan@litwareinc.com
```

<span data-ttu-id="55fe5-115">Per ripristinare un account utente eliminato entro la fine del periodo di tolleranza di 30 giorni, utilizzare la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="55fe5-115">To restore a deleted user account within the 30-day grace period, use the following syntax:</span></span>
  
```
Restore-MsolUser -UserPrincipalName <Account>
```

<span data-ttu-id="55fe5-116">Questo esempio consente di ripristinare l'account utente eliminato BelindaN@litwareinc.com.</span><span class="sxs-lookup"><span data-stu-id="55fe5-116">This example restores the deleted account BelindaN@litwareinc.com.</span></span>
  
```
Restore-MsolUser -UserPrincipalName BelindaN@litwareinc.com
```

 <span data-ttu-id="55fe5-117">**Note:**</span><span class="sxs-lookup"><span data-stu-id="55fe5-117">**Notes:**</span></span>
  
- <span data-ttu-id="55fe5-118">Per visualizzare un elenco di utenti eliminati che possono essere ripristinati, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="55fe5-118">To see the list of deleted users that can be restored, run the following command:</span></span>
    
  ```
  Get-MsolUser -All -ReturnDeletedUsers
  ```

- <span data-ttu-id="55fe5-119">Se il nome dell'entità utente originale di un account viene usato da un altro account, fare ricorso al parametro  _NewUserPrincipalName_ invece che a quello _UserPrincipalName_ per specificare un differente nome principale dell'utente, quando si ripristina l'account utente.</span><span class="sxs-lookup"><span data-stu-id="55fe5-119">If the user account's original user principal name is used by another account, use the  _NewUserPrincipalName_ parameter instead of _UserPrincipalName_ to specify a different user principal name when you restore the user account.</span></span>
    
## <a name="use-the-azure-active-directory-v2-powershell-module-to-remove-a-user-account"></a><span data-ttu-id="55fe5-120">Utilizzare il modulo Azure Active Directory V2 PowerShell per rimuovere un account utente</span><span class="sxs-lookup"><span data-stu-id="55fe5-120">Use the Azure Active Directory V2 PowerShell module to remove a user account</span></span>
<span data-ttu-id="55fe5-121"><a name="ShortVersion"> </a></span><span class="sxs-lookup"><span data-stu-id="55fe5-121"><a name="ShortVersion"> </a></span></span>

<span data-ttu-id="55fe5-p103">Per utilizzare il cmdlet **Remove-AzureADUser** dal modulo di Azure Active Directory V2 PowerShell, è innanzitutto necessario connettersi alla sottoscrizione. Per ulteriori informazioni, vedere [Connect con il modulo di Azure Active Directory V2 PowerShell](https://go.microsoft.com/fwlink/?linkid=842218).</span><span class="sxs-lookup"><span data-stu-id="55fe5-p103">To use the **Remove-AzureADUser** cmdlet from the Azure Active Directory V2 PowerShell module, you must first connect to your subscription. For the instructions, see [Connect with the Azure Active Directory V2 PowerShell module](https://go.microsoft.com/fwlink/?linkid=842218).</span></span>
  
<span data-ttu-id="55fe5-124">Una volta stabilita la connessione, utilizzare la sintassi seguente per rimuovere un singolo account utente:</span><span class="sxs-lookup"><span data-stu-id="55fe5-124">After you have connected, use the following syntax to remove an individual user account:</span></span>
  
```
Remove-AzureADUser -ObjectID <Account>
```

<span data-ttu-id="55fe5-125">Questo esempio consente di rimuovere l'account utente fabricec@litwareinc.com.</span><span class="sxs-lookup"><span data-stu-id="55fe5-125">This example removes the user account fabricec@litwareinc.com.</span></span>
  
```
Remove-AzureADUser -ObjectID fabricec@litwareinc.com
```

> [!NOTE]
> <span data-ttu-id="55fe5-126">Il parametro **-ObjectID** nel cmdlet **Remove-AzureAD** accetta sia il nome account (anche detto "nome dell'entità utente) sia l'ID oggetto dell'account.</span><span class="sxs-lookup"><span data-stu-id="55fe5-126">The **-ObjectID** parameter in the **Remove-AzureAD** cmdlet accepts either the account name, also known as the User Principal Name, or the account's object ID.</span></span>
  
<span data-ttu-id="55fe5-127">Per visualizzare il nome dell'account in base al nome dell'utente, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="55fe5-127">To display the account name based on the user's name, use the following commands:</span></span>
  
```
$userName="<User name>"
Write-Host (Get-AzureADUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
```

<span data-ttu-id="55fe5-128">Questo esempio permette di visualizzare il nome dell'account per l'utente Caleb Sillis.</span><span class="sxs-lookup"><span data-stu-id="55fe5-128">This example displays the account name for the user named Caleb Sills.</span></span>
  
```
$userName="Caleb Sills"
Write-Host (Get-AzureADUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
```

<span data-ttu-id="55fe5-129">Per rimuovere un account in base al nome dell'utente, utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="55fe5-129">To remove an account based on the user's name, use the following commands:</span></span>
  
```
$userName="<User name>"
Remove-AzureADUser -ObjectID (Get-AzureADUser | where {$_.DisplayName -eq $userName}).UserPrincipalName
```

## <a name="see-also"></a><span data-ttu-id="55fe5-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="55fe5-130">See also</span></span>
<span data-ttu-id="55fe5-131"><a name="SeeAlso"> </a></span><span class="sxs-lookup"><span data-stu-id="55fe5-131"><a name="SeeAlso"> </a></span></span>

<span data-ttu-id="55fe5-132">Vedere i seguenti argomenti aggiuntivi sulla gestione degli utenti con Office 365 PowerShell:</span><span class="sxs-lookup"><span data-stu-id="55fe5-132">See these additional topics about managing users with Office 365 PowerShell:</span></span>
  
- [<span data-ttu-id="55fe5-133">Creare account utente con Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="55fe5-133">Create user accounts with Office 365 PowerShell</span></span>](create-user-accounts-with-office-365-powershell.md)
    
- [<span data-ttu-id="55fe5-134">Bloccare gli account utente con Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="55fe5-134">Block user accounts with Office 365 PowerShell</span></span>](block-user-accounts-with-office-365-powershell.md)
    
- [<span data-ttu-id="55fe5-135">Assegnare le licenze agli account utente con Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="55fe5-135">Assign licenses to user accounts with Office 365 PowerShell</span></span>](assign-licenses-to-user-accounts-with-office-365-powershell.md)
    
- [<span data-ttu-id="55fe5-136">Rimuovere le licenze dagli account utente con Office 365 PowerShell</span><span class="sxs-lookup"><span data-stu-id="55fe5-136">Remove licenses from user accounts with Office 365 PowerShell</span></span>](remove-licenses-from-user-accounts-with-office-365-powershell.md)
    
<span data-ttu-id="55fe5-137">Per ulteriori informazioni sui cmdlet utilizzati in questa procedura, vedere i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="55fe5-137">For more information about the cmdlets that are used in these procedures, see the following topics:</span></span>
  
- [<span data-ttu-id="55fe5-138">Get-MsolUser</span><span class="sxs-lookup"><span data-stu-id="55fe5-138">Get-MsolUser</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=691543)
    
- [<span data-ttu-id="55fe5-139">Remove-MsolUser</span><span class="sxs-lookup"><span data-stu-id="55fe5-139">Remove-MsolUser</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=691636)
    
- [<span data-ttu-id="55fe5-140">Restore-MsolUser</span><span class="sxs-lookup"><span data-stu-id="55fe5-140">Restore-MsolUser</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=691637)
    
- [<span data-ttu-id="55fe5-141">New-AzureADUser</span><span class="sxs-lookup"><span data-stu-id="55fe5-141">New-AzureADUser</span></span>](https://docs.microsoft.com/powershell/module/azuread/new-azureaduser?view=azureadps-2.0)
    
