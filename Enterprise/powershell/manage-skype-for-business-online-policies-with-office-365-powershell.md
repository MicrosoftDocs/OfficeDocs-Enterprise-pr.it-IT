---
title: Gestire criteri Skype for Business Online con PowerShell di Office 365
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
ms.assetid: ff93a341-6f0f-4f06-9690-726052e1be64
description: "Riepilogo: Utilizzare PowerShell di Office 365 per gestire le proprietà dell'account utente di Skype for Business online con i criteri."
ms.openlocfilehash: 9b3877d2680b2b36d155cb5dd2a69fa21c972fe3
ms.sourcegitcommit: d31cf57295e8f3d798ab971d405baf3bd3eb7a45
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2017
---
# <a name="manage-skype-for-business-online-policies-with-office-365-powershell"></a><span data-ttu-id="dc625-103">Gestire criteri Skype for Business Online con PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="dc625-103">Manage Skype for Business Online policies with Office 365 PowerShell</span></span>

 <span data-ttu-id="dc625-104">**Riepilogo:** Utilizzare Office 365 PowerShell per gestire i Skype per la proprietà degli account utente in linea Business con i criteri.</span><span class="sxs-lookup"><span data-stu-id="dc625-104">**Summary:** Use Office 365 PowerShell to manage your Skype for Business Online user account properties with policies.</span></span>
  
<span data-ttu-id="dc625-105">Per gestire molte proprietà dell'account utente per Skype for Business online, è necessario specificarle come proprietà dei criteri con PowerShell di Office 365.</span><span class="sxs-lookup"><span data-stu-id="dc625-105">To manage many properties of user account for Skype for Business Online, you must specify them as properties of policies with Office 365 PowerShell.</span></span>
  
## <a name="before-you-begin"></a><span data-ttu-id="dc625-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="dc625-106">Before you begin</span></span>

<span data-ttu-id="dc625-107">Utilizzare queste istruzioni per ottenere la configurazione che consenta di eseguire i comandi (ignorare i passaggi già completati):</span><span class="sxs-lookup"><span data-stu-id="dc625-107">Use these instructions to get set up to run the commands (skip the steps you have already completed):</span></span>
  
1. <span data-ttu-id="dc625-108">Scaricare e installare il [Modulo di Windows PowerShell per Skype for Business Online](https://www.microsoft.com/en-us/download/details.aspx?id=39366).</span><span class="sxs-lookup"><span data-stu-id="dc625-108">Download and install the [Skype for Business Online Connector module](https://www.microsoft.com/en-us/download/details.aspx?id=39366).</span></span>
    
2. <span data-ttu-id="dc625-109">Aprire il prompt dei comandi Windows PowerShell ed eseguire quanto segue:</span><span class="sxs-lookup"><span data-stu-id="dc625-109">Open a Windows PowerShell command prompt and run the following commands:</span></span> 
    
```
Import-Module LyncOnlineConnector
$userCredential = Get-Credential
$sfbSession = New-CsOnlineSession -Credential $userCredential
Import-PSSession $sfbSession
  ```

<span data-ttu-id="dc625-110">Quando richiesto, immettere il nome e la password dell'account Administrator di Skype for Business online.</span><span class="sxs-lookup"><span data-stu-id="dc625-110">When prompted, enter your Skype for Business Online administrator account name and password.</span></span>
    
## <a name="manage-user-account-policies"></a><span data-ttu-id="dc625-111">Gestione dei criteri dell'account utente</span><span class="sxs-lookup"><span data-stu-id="dc625-111">Manage user account policies</span></span>

<span data-ttu-id="dc625-p101">Molte proprietà dell'account utente di Skype for Business online sono configurate utilizzando criteri. I criteri consistono in una raccolta di impostazioni che possono essere applicate a uno o più utenti. Per esaminare la configurazione del criterio, è possibile eseguire il comando di esempio riportato per il criterio FederationAndPICDefault.</span><span class="sxs-lookup"><span data-stu-id="dc625-p101">Many Skype for Business Online user account properties are configured by using policies. Policies are simply collections of settings that can be applied to one or more users. To take a look at how the a policy has been configured, you can run this example command for the FederationAndPICDefault policy:</span></span>
  
```
Get-CsExternalAccessPolicy -Identity "FederationAndPICDefault"
```

<span data-ttu-id="dc625-115">A sua volta, si dovrebbe ottenere qualcosa di simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="dc625-115">In turn, you should get back something similar to this:</span></span>
  
```
Identity                          : Tag:FederationAndPICDefault
Description                       :
EnableFederationAccess            : True
EnableXmppAccess                  : False
EnablePublicCloudAccess           : True
EnablePublicCloudAudioVideoAccess : True
EnableOutsideAccess               : True
```

<span data-ttu-id="dc625-p102">Nell'esempio riportato, i valori compresi nei criteri determinano le operazioni di comunicazione con utenti federati che Alex può davvero effettuare o meno. Ad esempio, la proprietà EnableOutsideAccess deve essere impostata su True affinché un utente possa comunicare con utenti esterni all'organizzazione. Tenere presente che tale proprietà non viene visualizzata nell'interfaccia di amministrazione di Office 365. Al contrario, la proprietà viene impostata automaticamente su True o False in base alle altre selezioni effettuate. Le altre due proprietà di interesse sono:</span><span class="sxs-lookup"><span data-stu-id="dc625-p102">In this example, the values within this policy determine what a use can or cannot do when it comes to communicating with federated users. For example, the EnableOutsideAccess property must be set to True for a user to be able to communicate with people outside the organization. Note that this property does not appear in the Office 365 Admin center. Instead, the property is automatically set to True or False based on the other selections that you make. The other two properties of interest are:</span></span>
  
- <span data-ttu-id="dc625-121">**EnableFederationAccess** indica se l'utente può comunicare con utenti di domini federati.</span><span class="sxs-lookup"><span data-stu-id="dc625-121">**EnableFederationAccess** indicates whether the user can communicate with people from federated domains.</span></span>
    
- <span data-ttu-id="dc625-122">**EnablePublicCloudAccess** indica se l'utente può comunicare con gli utenti di Windows Live.</span><span class="sxs-lookup"><span data-stu-id="dc625-122">**EnablePublicCloudAccess** indicates whether the user can communicate with Windows Live users.</span></span>
    
<span data-ttu-id="dc625-p103">Pertanto, non modificare direttamente le proprietà relativi alla federazione per gli account utente (ad esempio, **Set-CsUser-EnableFederationAccess $True**). Invece di assegnare un account un criterio di accesso esterno con i valori delle proprietà desiderate preconfigurati. Se si desidera che un utente di comunicare con utenti federati e utenti di Windows Live, tale utente deve essere assegnato un criterio che consente di tali tipi di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="dc625-p103">Therefore, you don't directly change federation-related properties on user accounts (for example, **Set-CsUser -EnableFederationAccess $True**). Instead, you assign an account an external access policy that has the desired property values preconfigured. If we want a user to be able to communicate with federated users and with Windows Live users, that user account must be assigned a policy that allows those types of communication.</span></span>
  
<span data-ttu-id="dc625-126">Se si desidera sapere se qualche utente è in grado di comunicare con utenti esterni all'organizzazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="dc625-126">If you want to know whether or not someone can communicate with users from outside the organization, you have to:</span></span>
  
- <span data-ttu-id="dc625-127">Determinare quali criteri di accesso esterno sono stati assegnati all'utente.</span><span class="sxs-lookup"><span data-stu-id="dc625-127">Determine which external access policy has been assigned to that user.</span></span>
    
- <span data-ttu-id="dc625-128">Determinare le funzionalità che sono consentite o meno dal criterio.</span><span class="sxs-lookup"><span data-stu-id="dc625-128">Determine which capabilities are or are not allowed by that policy.</span></span>
    
<span data-ttu-id="dc625-129">Ad esempio, è possibile utilizzare il comando riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="dc625-129">For example, you can do that by using this command:</span></span>
  
```
Get-CsOnlineUser -Identity "Alex Darrow" | ForEach {Get-CsExternalAccessPolicy -Identity $_.ExternalAccessPolicy}
```

<span data-ttu-id="dc625-130">Questo comando consente di individuare il criterio assegnato all'utente, quindi di individuare le funzionalità abilitate o disabilitate all'interno del criterio.</span><span class="sxs-lookup"><span data-stu-id="dc625-130">This command finds the policy assigned to the user, then finds the capabilities enabled or disabled within that policy.</span></span>
  
<span data-ttu-id="dc625-p104">Tenere presente che non esistono cmdlet per la creazione o la modifica dei criteri: è necessario utilizzare i criteri forniti precedentemente da Office 365. Se si desidera controllare i differenti criteri disponibili, utilizzare tali comandi:</span><span class="sxs-lookup"><span data-stu-id="dc625-p104">Note that there are no cmdlets for creating or for modifying policies. You must use the policies pre-supplied by Office 365. If you want to take a look at the different policies available, you can use these commands:</span></span>
  
- <span data-ttu-id="dc625-134">Get-CsClientPolicy</span><span class="sxs-lookup"><span data-stu-id="dc625-134">Get-CsClientPolicy</span></span>       
- <span data-ttu-id="dc625-135">Get-CsConferencingPolicy</span><span class="sxs-lookup"><span data-stu-id="dc625-135">Get-CsConferencingPolicy</span></span>        
- <span data-ttu-id="dc625-136">Get-CsDialPlan</span><span class="sxs-lookup"><span data-stu-id="dc625-136">Get-CsDialPlan</span></span>            
- <span data-ttu-id="dc625-137">Get-CsExternalAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="dc625-137">Get-CsExternalAccessPolicy</span></span>                         
- <span data-ttu-id="dc625-138">Get-CsHostedVoicemailPolicy</span><span class="sxs-lookup"><span data-stu-id="dc625-138">Get-CsHostedVoicemailPolicy</span></span>                        
- <span data-ttu-id="dc625-139">Get-CsPresencePolicy</span><span class="sxs-lookup"><span data-stu-id="dc625-139">Get-CsPresencePolicy</span></span>                               
- <span data-ttu-id="dc625-140">Get-CsVoicePolicy</span><span class="sxs-lookup"><span data-stu-id="dc625-140">Get-CsVoicePolicy</span></span>                                  

> [!NOTE]
> <span data-ttu-id="dc625-p105">Un dial plan di Skype for Business online rappresenta un criterio in tutti i suoi aspetti, con la sola eccezione del nome. Il nome "dial plan" è stato scelto al posto di "criteri di composizione" al fine di essere compatibile con Office Communications Server e con Exchange.</span><span class="sxs-lookup"><span data-stu-id="dc625-p105">A Skype for Business Online dial plan is a policy in every respect except the name. The name "dial plan" was chosen instead of, say, "dialing policy" in order to provide backward compatibility with Office Communications Server and with Exchange.</span></span> 
  
<span data-ttu-id="dc625-143">Ad esempio, per esaminare tutti i criteri vocali che possono essere utilizzati, eseguire tale comando:</span><span class="sxs-lookup"><span data-stu-id="dc625-143">For example, to look at all the voice policies available for your use, run this command:</span></span>
  
```
Get-CsVoicePolicy
```

> [!NOTE]
> <span data-ttu-id="dc625-p106">Che restituisce un elenco di tutti i criteri vocali disponibili per l'utente. Tenere tuttavia presente che non tutti i criteri possono essere assegnati a tutti gli utenti. Ciò è dovuto diverse restrizioni che coinvolgono posizione geografica e licenza. (Cosiddetti "[percorso utilizzo](https://msdn.microsoft.com/en-us/library/azure/dn194136.aspx).") Se si desidera conoscere i criteri di accesso esterno e i criteri di conferenza che possono essere assegnati a un determinato utente, utilizzare i comandi simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc625-p106">That returns a list of all the voice policies available to you. Keep in mind, however, that not all policies can be assigned to all users. This is due to various restrictions involving licensing and geographic location. (The so-called "[usage location](https://msdn.microsoft.com/en-us/library/azure/dn194136.aspx).") If you want to know the external access policies and the conferencing policies that can be assigned to a particular user, use commands similar to these:</span></span> 

```
Get-CsConferencingPolicy -ApplicableTo "Alex Darrow"
Get-CsExternalAccessPolicy -ApplicableTo "Alex Darrow"
```

<span data-ttu-id="dc625-p107">Il parametro ApplicableTo limita i dati restituiti ai criteri che possono essere assegnati a specifici utenti (ad esempio, Alex Darrow). A seconda dei limiti relativi alle licenze o al percorso di utilizzo, potrebbe rappresentare un sottogruppo di tutti i criteri disponibili.</span><span class="sxs-lookup"><span data-stu-id="dc625-p107">The ApplicableTo parameter limits the returned data to policies that can be assigned to the specified user (for example, Alex Darrow). Depending on licensing and usage location restrictions, that might represent a subset of all the available policies.</span></span> 
  
<span data-ttu-id="dc625-150">In alcuni casi, le proprietà dei criteri non vengono utilizzate con Office 365, mentre altre possono essere gestite solo dal personale di supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dc625-150">In some cases, properties of policies are not used with Office 365, while others can only be managed by Microsoft support personnel.</span></span> 
  
<span data-ttu-id="dc625-p108">Con Skype for Business online, gli utenti devono essere gestiti da un criterio di qualche tipo. Se una proprietà correlata a criteri validi è vuota, significa che l'utente in questione viene gestito da un criterio globale, ovvero un criterio che viene applicato automaticamente a un utente a meno che non venga specificamente assegnato un criterio per utente. Poiché un criterio client per un account utente non è disponibile nell'elenco, viene gestito dal criterio globale. È possibile determinare il criterio client globale con questo comando:</span><span class="sxs-lookup"><span data-stu-id="dc625-p108">With Skype for Business Online, users must be managed by a policy of some kind. If a valid policy-related property is blank, that means that the user in question is being managed by a global policy, which is a policy that is automatically applied to a user unless he or she is specifically assigned a per-user policy. Because we don't see a client policy listed for a user account, it is managed by the global policy. You can determine the global client policy with this command:</span></span>
  
```
Get-CsClientPolicy -Identity "Global"
```

## <a name="see-also"></a><span data-ttu-id="dc625-155">See also</span><span class="sxs-lookup"><span data-stu-id="dc625-155">See also</span></span>

#### 

[<span data-ttu-id="dc625-156">Gestire Skype for Business Online con PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="dc625-156">Manage Skype for Business Online with Office 365 PowerShell</span></span>](manage-skype-for-business-online-with-office-365-powershell.md)
  
[<span data-ttu-id="dc625-157">Gestire Office 365 con PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="dc625-157">Manage Office 365 with Office 365 PowerShell</span></span>](manage-office-365-with-office-365-powershell.md)
  
[<span data-ttu-id="dc625-158">Guida introduttiva a PowerShell di Office 365</span><span class="sxs-lookup"><span data-stu-id="dc625-158">Getting started with Office 365 PowerShell</span></span>](getting-started-with-office-365-powershell.md)
