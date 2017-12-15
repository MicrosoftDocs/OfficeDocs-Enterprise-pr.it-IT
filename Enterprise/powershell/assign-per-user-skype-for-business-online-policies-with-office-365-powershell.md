---
title: Assegnare criteri Skype for Business Online con PowerShell di Office 365
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 12/15/2017
ms.audience: ITPro
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom: DecEntMigration
ms.assetid: 36743c86-46c2-46be-b9ed-ad9d4e85d186
description: 'Riepilogo: Utilizzare PowerShell di Office 365 per assegnare impostazioni di comunicazione per utente con criteri Skype for Business online.'
ms.openlocfilehash: 91916b41ba420a204ecabb27eea2e451a91f6f25
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2017
---
# <a name="assign-per-user-skype-for-business-online-policies-with-office-365-powershell"></a><span data-ttu-id="543af-103">Assegnare criteri Skype for Business Online con PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="543af-103">Assign per-user Skype for Business Online policies with Office 365 PowerShell</span></span>

 <span data-ttu-id="543af-104">**Riepilogo:** Utilizzare Office 365 PowerShell per assegnare impostazioni per le comunicazioni con Skype per i criteri aziendali in linea per utente.</span><span class="sxs-lookup"><span data-stu-id="543af-104">**Summary:** Use Office 365 PowerShell to assign per-user communication settings with Skype for Business Online policies.</span></span>
  
<span data-ttu-id="543af-105">L'utilizzo di PowerShell di Office 365 è un modo efficace di assegnare impostazioni di comunicazione per utente con criteri Skype for Business online.</span><span class="sxs-lookup"><span data-stu-id="543af-105">Using Office 365 PowerShell is an efficient way to assign per-user communication settings with Skype for Business Online policies.</span></span>
  
## <a name="before-you-begin"></a><span data-ttu-id="543af-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="543af-106">Before you begin</span></span>

<span data-ttu-id="543af-107">Utilizzare queste istruzioni per ottenere la configurazione che consenta di eseguire i comandi (ignorare i passaggi già completati):</span><span class="sxs-lookup"><span data-stu-id="543af-107">Use these instructions to get set up to run the commands (skip the steps you have already completed):</span></span>
  
1. <span data-ttu-id="543af-108">Scaricare e installare il [Modulo di Windows PowerShell per Skype for Business Online](https://www.microsoft.com/en-us/download/details.aspx?id=39366).</span><span class="sxs-lookup"><span data-stu-id="543af-108">Download and install the [Skype for Business Online Connector module](https://www.microsoft.com/en-us/download/details.aspx?id=39366).</span></span>
    
2. <span data-ttu-id="543af-109">Aprire il prompt dei comandi Windows PowerShell ed eseguire quanto segue:</span><span class="sxs-lookup"><span data-stu-id="543af-109">Open a Windows PowerShell command prompt and run the following commands:</span></span> 
    
  ```
  Import-Module LyncOnlineConnector
$userCredential = Get-Credential
$sfbSession = New-CsOnlineSession -Credential $userCredential
Import-PSSession $sfbSession
  ```
<span data-ttu-id="543af-110">Quando richiesto, immettere il nome e la password dell'account Administrator di Skype for Business online.</span><span class="sxs-lookup"><span data-stu-id="543af-110">When prompted, enter your Skype for Business Online administrator account name and password.</span></span>
    
## <a name="updating-external-communication-settings-for-a-user-account"></a><span data-ttu-id="543af-111">Aggiornamento delle impostazioni di comunicazione esterna per un account utente</span><span class="sxs-lookup"><span data-stu-id="543af-111">Updating external communication settings for a user account</span></span>

<span data-ttu-id="543af-p101">Si supponga di voler modificare le impostazioni di comunicazione esterna in un account utente. Ad esempio, si desidera consentire ad Alex di comunicare con utenti federati (EnableFederationAccess è uguale a True), ma non con utenti di Windows Live (EnablePublicCloudAccess è uguale a False). A tale scopo, è necessario eseguire due operazioni:</span><span class="sxs-lookup"><span data-stu-id="543af-p101">Suppose you want to change external communication settings on a user account. For example, you want to allow Alex to communicate with federated users (EnableFederationAccess is equal to True) but not with Windows Live users (EnablePublicCloudAccess equals False). To do that, you need to do two things:</span></span>
  
1. <span data-ttu-id="543af-115">Individuare un criterio di accesso esterno che soddisfi i criteri necessari.</span><span class="sxs-lookup"><span data-stu-id="543af-115">Find an external access policy that meets our criteria.</span></span>
    
2. <span data-ttu-id="543af-116">Assegnare tale criterio di accesso esterno ad Alex.</span><span class="sxs-lookup"><span data-stu-id="543af-116">Assign that external access policy to Alex.</span></span>
    
> [!NOTE]
>  <span data-ttu-id="543af-p102">Non è possibile creare un criterio personalizzato tutti i propri. Ciò avviene perché Skype Business online non consente di creare criteri personalizzati. In realtà, è necessario assegnare uno dei criteri che sono stati creati specificamente per Office 365. I criteri creati in precedenza includono: 4 criteri client differenti, 224 criteri conferenza differenti, 5 dial plan differenti, 5 criteri di accesso esterno differenti, il criterio di segreteria telefonica ospitata 1 e 4 criteri vocali differenti.</span><span class="sxs-lookup"><span data-stu-id="543af-p102">You can't create a custom policy all our own. That's because Skype for Business Online does not allow you to create custom policies. Instead, you must assign one of the policies that were created specifically for Office 365. Those pre-created policies include: 4 different client policies, 224 different conferencing policies, 5 different dial plans, 5 different external access policies, 1 hosted voicemail policy, and 4 different voice policies.</span></span>
  
<span data-ttu-id="543af-p103">Pertanto, come è possibile determinare qualche criterio di accesso esterno deve essere assegnato ad Alex? Il comando seguente restituisce tutti i criteri di accesso esterno nei quali EnableFederationAccess è impostato su True e EnablePublicCloudAccess è impostato su False:</span><span class="sxs-lookup"><span data-stu-id="543af-p103">So how do you determine which external access policy to assign Alex? The following command returns all the external access policies where EnableFederationAccess is set to True and EnablePublicCloudAccess is set to False:</span></span>
  
```
Get-CsExternalAccessPolicy | Where-Object {$_.EnableFederationAccess -eq $True -and $_.EnablePublicCloudAccess -eq $False}
```

<span data-ttu-id="543af-p104">Il comando non è restituire tutti i criteri che soddisfano due criteri: la proprietà EnableFederationAccess è impostata su True e il criterio EnablePublicCloudAccess è impostato su False. A sua volta, il comando restituisce un criterio che soddisfi i criteri necessari (FederationOnly). Di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="543af-p104">What the command does is return all the policies that meet two criteria: the EnableFederationAccess property is set to True, and the EnablePublicCloudAccess policy is set to False. In turn, that command returns one policy that meets our criteria (FederationOnly). Here is an example:</span></span>
  
```
Identity                          : Tag:FederationOnly
Description                       :
EnableFederationAccess            : True
EnableXmppAccess                  : False
EnablePublicCloudAccess           : False
EnablePublicCloudAudioVideoAccess : False
EnableOutsideAccess               : True
```

> [!NOTE]
> <span data-ttu-id="543af-p105">L'identità del criterio corrisponde a Tag:FederationOnly. In realtà, il Tag: prefisso corrisponde a un carryover di operazioni preliminari eseguite su Microsoft Lync 2013. Quando si assegnano i criteri agli utenti, è necessario eliminare il Tag: prefisso e utilizzare soltanto il nome del criterio: FederationOnly.</span><span class="sxs-lookup"><span data-stu-id="543af-p105">The policy Identity says Tag:FederationOnly. As it turns out, the Tag: prefix is a carryover from the early pre-release work done on Microsoft Lync 2013. When it comes to assigning policies to users, you should delete the Tag: prefix and use just the policy name: FederationOnly.</span></span> 
  
<span data-ttu-id="543af-p106">Quando si conosce il criterio da assegnare ad Alex, è possibile assegnarlo utilizzando il cmdlet [Grant-CsExternalAccessPolicy](https://go.microsoft.com/fwlink/?LinkId=523974). Di seguito viene riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="543af-p106">Now that you know which policy to assign to Alex, we can assign that policy by using the [Grant-CsExternalAccessPolicy](https://go.microsoft.com/fwlink/?LinkId=523974) cmdlet. Here is an example:</span></span>
  
```
Grant-CsExternalAccessPolicy -Identity "Alex Darrow" -PolicyName "FederationOnly"
```

<span data-ttu-id="543af-131">Assegnare un criterio è piuttosto semplice: è necessario specificare soltanto l'identità dell'utente e il nome del criterio da assegnare.</span><span class="sxs-lookup"><span data-stu-id="543af-131">Assigning a policy is pretty simple: you simply specify the Identity of the user and the name of the policy to be assigned.</span></span> 
  
<span data-ttu-id="543af-p107">Nel caso di criteri e assegnazione dei criteri, non ci si limita a effettuare operazioni con account utenti una sola volta. Ad esempio, si supponga che sia necessario disporre di un elenco di tutti gli utenti che possono comunicare con partner federati e con gli utenti di Windows Live. È noto che a tali utenti è stato assegnato il criterio di accesso utente esterno FederationAndPICDefault. Dal momento che si conosce tale informazione, è possibile visualizzare un elenco di tutti gli utenti eseguendo un comando semplice. Di seguito viene riportato il comando:</span><span class="sxs-lookup"><span data-stu-id="543af-p107">And when it comes to policies and policy assignments, you're not limited to working with user accounts one a time. For example, suppose you need a list of all the users who are allowed to communicate with federated partners and with Windows Live users. We already know that those users have been assigned the external user access policy FederationAndPICDefault. Because we know that, you can display a list of all those users by running one simple command. Here is the command:</span></span>
  
```
Get-CsOnlineUser -Filter {ExternalAccessPolicy -eq "FederationAndPICDefault"} | Select-Object DisplayName
```

<span data-ttu-id="543af-p108">in altre parole, è possibile visualizzare tutti gli utenti per i quali la proprietà ExternalAccessPolicy è impostata su FederationAndPICDefault. Per limitare la quantità di informazioni che vengono visualizzate sullo schermo, utilizzare il cmdlet Select-Object per visualizzare soltanto il nome di ogni utente.</span><span class="sxs-lookup"><span data-stu-id="543af-p108">In other words, show us all the users where the ExternalAccessPolicy property is set to FederationAndPICDefault. (And, in order to limit the amount of information that appears onscreen, use the Select-Object cmdlet to display show us only each user's display name.)</span></span> 
  
<span data-ttu-id="543af-139">Per configurare tutti gli account utente affinché utilizzino quello stesso criterio, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="543af-139">To configure all our user accounts to use that same policy, use this command:</span></span>
  
```
Get-CsOnlineUser | Grant-CsExternalAccessPolicy "FederationAndPICDefault"
```

<span data-ttu-id="543af-140">Il comando utilizza Get-CsOnlineUser per restituire una raccolta di tutti gli utenti che sono stati abilitati per Lync. In seguito, invia tutte le informazioni su Grant-CsExternalAccessPolicy che assegna il criterio FederationAndPICDefault a tutti gli utenti presenti nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="543af-140">This command uses Get-CsOnlineUser to return a collection of all the users who have been enabled for Lync, then sends all that information to Grant-CsExternalAccessPolicy, which assigns the FederationAndPICDefault policy to each and every user in the collection.</span></span>
  
<span data-ttu-id="543af-p109">Come esempio aggiuntivo, si supponga di aver assegnato in precedenza il criterio FederationAndPICDefault ad Alex, ma ora si desidera che Alex sia gestito dal criterio di accesso esterno globale. Non è possibile assegnare in modo esplicito il criterio globale. Viene utilizzato solo se nessun altro criterio per utente è assegnato. Pertanto, se si desidera che Alex sia gestito dal criterio globale, è necessario  *non assegnare*  i criteri per utente assegnati in precedenza all'utente. Ecco un esempio di comando:</span><span class="sxs-lookup"><span data-stu-id="543af-p109">As an additional example, suppose you've previously assigned Alex the FederationAndPICDefault policy and now you've changed your mind and would like him to be managed by the global external access policy. You can't explicitly assign the global policy to anyone. It is only used if no other per-user policy is assigned. Therefore, if we want Alex to be managed by the global policy, you need to  *unassign*  any per-user policy previously assigned to him. Here is an example command:</span></span>
  
```
Grant-CsExternalAccessPolicy -Identity "Alex Darrow" -PolicyName $Null
```

<span data-ttu-id="543af-p110">Il comando imposta il nome del criterio di accesso esterno assegnato ad Alex su un valore ($Null). Null vuol dire "niente". In altre parole, nessun criterio di accesso esterno viene assegnato ad Alex. Se non viene assegnato alcun criterio di accesso esterno a un utente, quest'ultimo viene gestito dal criterio globale.</span><span class="sxs-lookup"><span data-stu-id="543af-p110">This command sets the name of the external access policy assigned to Alex to a null value ($Null). Null means "nothing". In other words, no external access policy is assigned to Alex. When no external access policy is assigned to a user, that user then gets managed by the global policy.</span></span>
  
<span data-ttu-id="543af-p111">Per disabilitare un account utente utilizzando Windows PowerShell, utilizzare i cmdlet di Azure Active Directory per rimuovere Skype di Alex per licenza Business Online. Per ulteriori informazioni, vedere [disabilitare l'accesso ai servizi di Office 365 PowerShell](assign-licenses-to-user-accounts-with-office-365-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="543af-p111">To disable a user account using Windows PowerShell, use the Azure Active Directory cmdlets to remove Alex's Skype for Business Online license. For more information, see [Disable access to services with Office 365 PowerShell](assign-licenses-to-user-accounts-with-office-365-powershell.md).</span></span>
  
## <a name="see-also"></a><span data-ttu-id="543af-152">See also</span><span class="sxs-lookup"><span data-stu-id="543af-152">See also</span></span>

#### 

[<span data-ttu-id="543af-153">Gestire Skype for Business Online con PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="543af-153">Manage Skype for Business Online with Office 365 PowerShell</span></span>](manage-skype-for-business-online-with-office-365-powershell.md)
  
[<span data-ttu-id="543af-154">Gestire Office 365 con PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="543af-154">Manage Office 365 with Office 365 PowerShell</span></span>](manage-office-365-with-office-365-powershell.md)
  
[<span data-ttu-id="543af-155">Guida introduttiva a PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="543af-155">Getting started with Office 365 PowerShell</span></span>](getting-started-with-office-365-powershell.md)
