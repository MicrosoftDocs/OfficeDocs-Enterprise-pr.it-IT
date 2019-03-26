---
title: Proteggere gli account di amministratore globale di Office 365
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 4/10/2018
ms.audience: Admin
ms.topic: get-started-article
ms.service: o365-administration
localization_priority: Normal
ms.collection: Strat_O365_IP
search.appverid:
- MET150
- MOE150
- MED150
- MBS150
- BCS160
ms.assetid: 6b4ded77-ac8d-42ed-8606-c014fd947560
description: Proteggere l'accesso dell'amministratore globale all'abbonamento a Office 365 con questi tre passaggi.
ms.openlocfilehash: 23d47ec1f5fc4126113dd69e1ac6400d003ca41f
ms.sourcegitcommit: 4ef8e113fa20b539de1087422455fc26ff123d55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/19/2019
ms.locfileid: "30573920"
---
# <a name="protect-your-office-365-global-administrator-accounts"></a><span data-ttu-id="6ed6a-103">Proteggere gli account di amministratore globale di Office 365</span><span class="sxs-lookup"><span data-stu-id="6ed6a-103">Protect your Office 365 global administrator accounts</span></span>

 <span data-ttu-id="6ed6a-104">**Riepilogo:** Proteggere la sottoscrizione di Office 365 da attacchi basati sul compromesso di un account di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-104">**Summary:** Protect your Office 365 subscription from attacks based on the compromise of a global administrator account.</span></span> 
  
<span data-ttu-id="6ed6a-105">Le violazioni della sicurezza di un abbonamento a Office 365, incluse le informazioni sulla raccolta e gli attacchi di phishing, vengono in genere eseguite compromettendo le credenziali di un account di amministratore globale di Office 365.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-105">Security breaches of an Office 365 subscription, including information harvesting and phishing attacks, are typically done by compromising the credentials of an Office 365 global administrator account.</span></span> <span data-ttu-id="6ed6a-106">La sicurezza nel cloud è una partnership tra l'utente e Microsoft:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-106">Security in the cloud is a partnership between you and Microsoft:</span></span>
  
- <span data-ttu-id="6ed6a-107">I servizi cloud Microsoft sono basati su una base di attendibilità e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-107">Microsoft cloud services are built on a foundation of trust and security.</span></span> <span data-ttu-id="6ed6a-108">Microsoft fornisce controlli e funzionalità di sicurezza che consentono di proteggere i dati e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-108">Microsoft provides you security controls and capabilities to help you protect your data and applications.</span></span>
    
- <span data-ttu-id="6ed6a-109">Possiedi i dati e le identità e la responsabilità di proteggerli, la sicurezza delle risorse locali e la sicurezza dei componenti cloud che controlli.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-109">You own your data and identities and the responsibility for protecting them, the security of your on-premises resources, and the security of cloud components you control.</span></span>
    
<span data-ttu-id="6ed6a-110">Microsoft fornisce funzionalità che consentono di proteggere l'organizzazione, ma sono effettive solo se vengono utilizzate.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-110">Microsoft provides capabilities to help protect your organization, but they are effective only if you use them.</span></span> <span data-ttu-id="6ed6a-111">Se non vengono utilizzati, potrebbe essere vulnerabile all'attacco.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-111">If you do not use them, you may be vulnerable to attack.</span></span> <span data-ttu-id="6ed6a-112">Per proteggere gli account di amministratore globale, Microsoft è qui per informazioni dettagliate su come eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-112">To protect your global administrator accounts, Microsoft is here to help you with detailed instructions to:</span></span>
  
1. <span data-ttu-id="6ed6a-113">Creare account di amministratore globale di Office 365 dedicati e utilizzarli solo quando necessario.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-113">Create dedicated Office 365 global administrator accounts and use them only when necessary.</span></span>
    
2. <span data-ttu-id="6ed6a-114">Configurare l'autenticazione a più fattori per gli account di amministratore globale di Office 365 dedicati e utilizzare la forma più complessa di autenticazione secondaria.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-114">Configure multi-factor authentication for your dedicated Office 365 global administrator accounts and use the strongest form of secondary authentication.</span></span>
    
3. <span data-ttu-id="6ed6a-115">Abilitare e configurare Office 365 cloud app Security per il monitoraggio dell'attività account amministratore globale sospetta.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-115">Enable and configure Office 365 Cloud App Security to monitor for suspicious global administrator account activity.</span></span>
    
> [!NOTE]
> <span data-ttu-id="6ed6a-116">Anche se questo articolo è concentrato sugli account di amministratore globale, è opportuno considerare anche se gli account aggiuntivi con autorizzazioni di vasta portata per accedere ai dati dell'abbonamento, ad esempio eDiscovery Administrator o la sicurezza o la conformità gli account di amministratore devono essere protetti nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-116">Although this article is focused on global administrator accounts, you should also consider whether additional accounts with wide-ranging permissions to access the data in your subscription, such as eDiscovery administrator or security or compliance administrator accounts, should be protected in the same way.</span></span> 
  
## <a name="step-1-create-dedicated-office-365-global-administrator-accounts-and-use-them-only-when-necessary"></a><span data-ttu-id="6ed6a-117">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-117">Step 1.</span></span> <span data-ttu-id="6ed6a-118">Creare account di amministratore globale di Office 365 dedicati e utilizzarli solo se necessario</span><span class="sxs-lookup"><span data-stu-id="6ed6a-118">Create dedicated Office 365 global administrator accounts and use them only when necessary</span></span>

<span data-ttu-id="6ed6a-119">Vi sono relativamente poche attività amministrative, ad esempio l'assegnazione di ruoli agli account utente, che richiedono privilegi di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-119">There are relatively few administrative tasks, such as assigning roles to user accounts, that require global administrator privileges.</span></span> <span data-ttu-id="6ed6a-120">Pertanto, anziché utilizzare gli account utente giornalieri a cui è stato assegnato il ruolo di amministratore globale, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-120">Therefore, instead of using everyday user accounts that have been assigned the global admin role, do these steps:</span></span>
  
1. <span data-ttu-id="6ed6a-121">Determinare il set di account utente a cui è stato assegnato il ruolo di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-121">Determine the set of user accounts that have been assigned the global admin role.</span></span> <span data-ttu-id="6ed6a-122">È possibile eseguire questa operazione con questo comando nel prompt dei comandi del modulo di Microsoft Azure Active Directory per Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-122">You can do this with this command at the Microsoft Azure Active Directory Module for Windows PowerShell command prompt:</span></span>
    
  ```
  Get-MsolRoleMember -RoleObjectId (Get-MsolRole -RoleName "Company Administrator").ObjectId
  ```

2. <span data-ttu-id="6ed6a-123">Accedere all'abbonamento a Office 365 con un account utente a cui è stato assegnato il ruolo di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-123">Sign into your Office 365 subscription with a user account that has been assigned the global admin role.</span></span>
    
3. <span data-ttu-id="6ed6a-124">Creare almeno un massimo di cinque account utente di amministratore globale dedicati.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-124">Create at least one and up to a maximum of five dedicated global administrator user accounts.</span></span> <span data-ttu-id="6ed6a-125">**Utilizzare password complesse con una lunghezza di almeno 12 caratteri.**</span><span class="sxs-lookup"><span data-stu-id="6ed6a-125">**Use strong passwords at least 12 characters long.**</span></span> <span data-ttu-id="6ed6a-126">Per ulteriori informazioni, vedere [creare una password complessa](https://support.microsoft.com/help/4026406/microsoft-account-create-a-strong-password) .</span><span class="sxs-lookup"><span data-stu-id="6ed6a-126">See [Create a strong password](https://support.microsoft.com/help/4026406/microsoft-account-create-a-strong-password) for more information.</span></span> <span data-ttu-id="6ed6a-127">Archiviare le password per i nuovi account in una posizione sicura.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-127">Store the passwords for the new accounts in a secure location.</span></span> 
    
4. <span data-ttu-id="6ed6a-128">Assegnare il ruolo di amministratore globale a ognuno dei nuovi account utente di amministratore globale dedicato.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-128">Assign the global admin role to each of the new dedicated global administrator user accounts.</span></span>
    
5. <span data-ttu-id="6ed6a-129">DisConnettersi da Office 365.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-129">Sign out of Office 365.</span></span>
    
6. <span data-ttu-id="6ed6a-130">Accedere con uno dei nuovi account utente di amministratore globale dedicati.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-130">Sign in with one of the new dedicated global administrator user accounts.</span></span>
    
7. <span data-ttu-id="6ed6a-131">Per ogni account utente esistente a cui è stato assegnato il ruolo di amministratore globale dal passaggio 1:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-131">For each existing user account that had been assigned the global admin role from step 1:</span></span>
    
  - <span data-ttu-id="6ed6a-132">Rimuovere il ruolo di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-132">Remove the global admin role.</span></span>
    
  - <span data-ttu-id="6ed6a-133">Assegnare i ruoli di amministratore all'account appropriato per la funzione e la responsabilità del processo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-133">Assign admin roles to the account that are appropriate to that user's job function and responsibility.</span></span> <span data-ttu-id="6ed6a-134">Per ulteriori informazioni sui vari ruoli di amministratore in Office 365, vedere [informazioni sui ruoli di amministratore di office 365](https://support.office.com/article/da585eea-f576-4f55-a1e0-87090b6aaa9d).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-134">For more information about various admin roles in Office 365, see [About Office 365 admin roles](https://support.office.com/article/da585eea-f576-4f55-a1e0-87090b6aaa9d).</span></span>
    
8. <span data-ttu-id="6ed6a-135">DisConnettersi da Office 365.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-135">Sign out of Office 365.</span></span>
    
<span data-ttu-id="6ed6a-136">Il risultato deve essere:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-136">The result should be:</span></span>
  
- <span data-ttu-id="6ed6a-137">Gli unici account utente dell'abbonamento che dispongono del ruolo di amministratore globale sono il nuovo set di account di amministratore globale dedicati.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-137">The only user accounts in your subscription that have the global admin role are the new set of dedicated global administrator accounts.</span></span> <span data-ttu-id="6ed6a-138">Verificarlo con il seguente comando di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-138">Verify this with the following PowerShell command:</span></span>
    
  ```
  Get-MsolRoleMember -RoleObjectId (Get-MsolRole -RoleName "Company Administrator").ObjectId
  ```

- <span data-ttu-id="6ed6a-139">A tutti gli altri account utente quotidiani che gestiscono l'abbonamento sono assegnati ruoli di amministratore associati ai propri ruoli professionali.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-139">All other everyday user accounts that manage your subscription have admin roles assigned that are associated with their job responsibilities.</span></span>
    
<span data-ttu-id="6ed6a-140">Da questo momento in poi, si accede con gli account amministratore globale dedicato solo per le attività che richiedono privilegi di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-140">From this moment onward, you sign in with the dedicated global administrator accounts only for tasks that require global administrator privileges.</span></span> <span data-ttu-id="6ed6a-141">Tutte le altre attività di amministrazione di Office 365 devono essere eseguite assegnando altri ruoli di amministrazione agli account utente.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-141">All other Office 365 administration must be done by assigning other administration roles to user accounts.</span></span>
  
> [!NOTE]
> <span data-ttu-id="6ed6a-142">Sì, è necessario eseguire ulteriori passaggi per disconnettersi come account utente giornaliero e accedere con un account di amministratore globale dedicato.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-142">Yes, this requires additional steps to sign out as your everyday user account and sign in with a dedicated global administrator account.</span></span> <span data-ttu-id="6ed6a-143">Tuttavia, è necessario eseguire questa operazione solo occasionalmente per le operazioni di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-143">But this only needs to be done occasionally for global administrator operations.</span></span> <span data-ttu-id="6ed6a-144">Si conSideri che il ripristino dell'abbonamento a Office 365 dopo una violazione di un account amministratore globale richiede passaggi molto più.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-144">Consider that recovering your Office 365 subscription after a global administrator account breach requires a lot more steps.</span></span> 
  
## <a name="step-2-configure-multi-factor-authentication-for-your-dedicated-office-365-global-administrator-accounts-and-use-the-strongest-form-of-secondary-authentication"></a><span data-ttu-id="6ed6a-145">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-145">Step 2.</span></span> <span data-ttu-id="6ed6a-146">Configurare l'autenticazione a più fattori per gli account di amministratore globale di Office 365 dedicati e utilizzare la forma più complessa di autenticazione secondaria</span><span class="sxs-lookup"><span data-stu-id="6ed6a-146">Configure multi-factor authentication for your dedicated Office 365 global administrator accounts and use the strongest form of secondary authentication</span></span>

<span data-ttu-id="6ed6a-147">L'autenticazione a più fattori per gli account di amministratore globale richiede ulteriori informazioni oltre il nome e la password dell'account.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-147">Multi-factor authentication (MFA) for your global administrator accounts requires additional information beyond the account name and password.</span></span> <span data-ttu-id="6ed6a-148">Office 365 supporta questi metodi di verifica:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-148">Office 365 supports these verification methods:</span></span>
  
- <span data-ttu-id="6ed6a-149">Una telefonata</span><span class="sxs-lookup"><span data-stu-id="6ed6a-149">A phone call</span></span>
    
- <span data-ttu-id="6ed6a-150">Un passcode generato casualmente</span><span class="sxs-lookup"><span data-stu-id="6ed6a-150">A randomly generated pass code</span></span>
    
- <span data-ttu-id="6ed6a-151">Una smart card virtuale o fisica</span><span class="sxs-lookup"><span data-stu-id="6ed6a-151">A smart card (virtual or physical)</span></span>
    
- <span data-ttu-id="6ed6a-152">Un dispositivo biometrico</span><span class="sxs-lookup"><span data-stu-id="6ed6a-152">A biometric device</span></span>
    
<span data-ttu-id="6ed6a-153">Se si è una società di piccole dimensioni che utilizza account utente archiviati solo nel cloud (modello di identità cloud), attenersi alla procedura seguente per configurare l'utilizzo di una chiamata telefonica o di un codice di verifica dei messaggi di testo inviati a uno Smart Phone:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-153">If you are a small business that is using user accounts stored only in the cloud (the cloud identity model), use these steps to configure MFA using a phone call or a text message verification code sent to a smart phone:</span></span>
  
1. <span data-ttu-id="6ed6a-154">[Abilitazione dell'AMF](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-154">[Enable MFA](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6).</span></span>
    
2. <span data-ttu-id="6ed6a-155">[Impostare la verifica in due passaggi per Office 365](https://support.office.com/article/Set-up-2-step-verification-for-Office-365-ace1d096-61e5-449b-a875-58eb3d74de14) per configurare ogni account amministratore globale dedicato per la chiamata telefonica o il messaggio di testo come metodo di verifica.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-155">[Set up 2-step verification for Office 365](https://support.office.com/article/Set-up-2-step-verification-for-Office-365-ace1d096-61e5-449b-a875-58eb3d74de14) to configure each dedicated global administrator account for phone call or text message as the verification method.</span></span> 
    
<span data-ttu-id="6ed6a-156">Se si è un'organizzazione più grande che utilizza un modello di identità ibrido di Office 365, sono disponibili altre opzioni di verifica.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-156">If you are a larger organization that is using an Office 365 hybrid identity model, you have more verification options.</span></span> <span data-ttu-id="6ed6a-157">Se l'infrastruttura di sicurezza è già attiva per un metodo di autenticazione secondario più forte, attenersi alla seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-157">If you have the security infrastructure already in place for a stronger secondary authentication method, use these steps:</span></span>
  
1. <span data-ttu-id="6ed6a-158">[Abilitazione dell'AMF](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-158">[Enable MFA](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6).</span></span>
    
2. <span data-ttu-id="6ed6a-159">[Impostare la verifica in due passaggi per Office 365](https://support.office.com/article/Set-up-2-step-verification-for-Office-365-ace1d096-61e5-449b-a875-58eb3d74de14) per configurare ogni account amministratore globale dedicato per il metodo di verifica appropriato.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-159">[Set up 2-step verification for Office 365](https://support.office.com/article/Set-up-2-step-verification-for-Office-365-ace1d096-61e5-449b-a875-58eb3d74de14) to configure each dedicated global administrator account for the appropriate verification method.</span></span> 
    
<span data-ttu-id="6ed6a-160">Se l'infrastruttura di sicurezza per il metodo di verifica più sicuro desiderato non è in esecuzione e funziona per Office 365 AMF, è consigliabile configurare gli account di amministratore globale dedicati con AMF tramite una telefonata o un messaggio di testo codice di verifica inviato a uno Smart Phone per gli account di amministratore globale come misura di sicurezza provvisoria.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-160">If the security infrastructure for the desired stronger verification method is not in place and functioning for Office 365 MFA, we strongly recommend that you configure dedicated global administrator accounts with MFA using a phone call or a text message verification code sent to a smart phone for your global administrator accounts as an interim security measure.</span></span> <span data-ttu-id="6ed6a-161">Non lasciare gli account di amministratore globale dedicati senza l'ulteriore protezione fornita dall'AMF.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-161">Do not leave your dedicated global administrator accounts without the additional protection provided by MFA.</span></span>
  
<span data-ttu-id="6ed6a-162">Per maggiori informazioni, vedere [Pianificare l'autenticazione a più fattori per le distribuzioni di Office 365](https://support.office.com/article/043807b2-21db-4d5c-b430-c8a6dee0e6ba)</span><span class="sxs-lookup"><span data-stu-id="6ed6a-162">For more information, see [Plan for multi-factor authentication for Office 365 Deployments](https://support.office.com/article/043807b2-21db-4d5c-b430-c8a6dee0e6ba).</span></span>
  
<span data-ttu-id="6ed6a-163">Per connettersi ai servizi di Office 365 con AMF e PowerShell, vedere [questo articolo](https://blogs.technet.microsoft.com/solutions_advisory_board/2017/04/27/connect-to-office-365-services-with-multifactor-authentication-mfa-and-powershell/).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-163">To connect to Office 365 services with MFA and PowerShell, see [this article](https://blogs.technet.microsoft.com/solutions_advisory_board/2017/04/27/connect-to-office-365-services-with-multifactor-authentication-mfa-and-powershell/).</span></span>
  
## <a name="step-3-monitor-for-suspicious-global-administrator-account-activity"></a><span data-ttu-id="6ed6a-164">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-164">Step 3.</span></span> <span data-ttu-id="6ed6a-165">Monitoraggio dell'attività dell'account amministratore globale sospetto</span><span class="sxs-lookup"><span data-stu-id="6ed6a-165">Monitor for suspicious global administrator account activity</span></span>

<span data-ttu-id="6ed6a-166">Office 365 cloud app Security consente di creare criteri per notificare il comportamento sospetto nell'abbonamento.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-166">Office 365 Cloud App Security lets you create policies to notify you of suspicious behavior in your subscription.</span></span> <span data-ttu-id="6ed6a-167">Cloud app Security è integrato in Office 365 E5, ma è anche disponibile come servizio separato.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-167">Cloud App Security is built into Office 365 E5, but is also available as a separate service.</span></span> <span data-ttu-id="6ed6a-168">Ad esempio, se non si dispone di Office 365 E5, è possibile acquistare singole licenze di sicurezza delle app cloud per gli account utente a cui sono assegnati i ruoli amministratore globale, amministratore sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-168">For example, if you do not have Office 365 E5, you can purchase individual Cloud App Security licenses for the user accounts that are assigned the global administrator, security administrator, and compliance administrator roles.</span></span>
  
<span data-ttu-id="6ed6a-169">Se si dispone di cloud app Security nell'abbonamento a Office 365, attenersi alla seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-169">If you have Cloud App Security in your Office 365 subscription, use these steps:</span></span>
  
1. <span data-ttu-id="6ed6a-170">Accedere all'interfaccia di amministrazione di Microsoft 365 con un account a cui è stato assegnato il ruolo amministratore della sicurezza o amministratore conformità.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-170">Sign into the Microsoft 365 admin center with an account that is assigned the Security Administrator or Compliance Administrator role.</span></span>
    
2. <span data-ttu-id="6ed6a-171">[Attiva la sicurezza delle app cloud di Office 365](https://support.office.com/article/ba919c73-d021-404d-9850-eec57e78678c).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-171">[Turn on Office 365 Cloud App Security](https://support.office.com/article/ba919c73-d021-404d-9850-eec57e78678c).</span></span>
    
3. <span data-ttu-id="6ed6a-172">Esaminare i [criteri di rilevamento delle anomalie in Office 365 cloud app Security](https://support.office.com/article/88935b4e-dcb1-47f1-8aca-1bf8fb069db6) per inviare una notifica tramite posta elettronica dei modelli anomali di attività amministrative privilegiate.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-172">Review your [Anomaly detection policies in Office 365 Cloud App Security](https://support.office.com/article/88935b4e-dcb1-47f1-8aca-1bf8fb069db6) to notify you by email of anomalous patterns of privileged administrative activity.</span></span> 
    
<span data-ttu-id="6ed6a-173">Per aggiungere un account utente al ruolo amministratore della sicurezza, [connettersi a Office 365 PowerShell](https://technet.microsoft.com/library/dn975125.aspx#step3) con un account di amministratore globale dedicato e l'AMF, immettere il nome dell'entità utente dell'account utente, quindi eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-173">To add a user account to the Security Administrator role, [connect to Office 365 PowerShell](https://technet.microsoft.com/library/dn975125.aspx#step3) with a dedicated global administrator account and MFA, fill in the user principal name of the user account, and then run these commands:</span></span> 
  
```
$upn="<User principal name of the account>"
Add-MsolRoleMember -RoleMemberEmailAddress $upn -RoleName "Security Administrator"
```

<span data-ttu-id="6ed6a-174">Per aggiungere un account utente al ruolo amministratore conformità, immettere il nome dell'entità utente dell'account utente, quindi eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-174">To add a user account to the Compliance Administrator role, fill in the user principal name of the user account, and then run these commands:</span></span>
  
```
$upn="<User principal name of the account>"
Add-MsolRoleMember -RoleMemberEmailAddress  $upn -RoleName "Compliance Administrator"
```

## <a name="additional-protections-for-enterprise-organizations"></a><span data-ttu-id="6ed6a-175">Protezioni aggiuntive per le organizzazioni aziendali</span><span class="sxs-lookup"><span data-stu-id="6ed6a-175">Additional protections for enterprise organizations</span></span>

<span data-ttu-id="6ed6a-176">Dopo i passaggi 1-3, utilizzare questi metodi aggiuntivi per verificare che l'account di amministratore globale e la configurazione che si esegue utilizzando l'utente siano il più sicuro possibile.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-176">After steps 1-3, use these additional methods to ensure that your global administrator account, and the configuration that you perform using it, are as secure as possible.</span></span>
  
### <a name="privileged-access-workstation-paw"></a><span data-ttu-id="6ed6a-177">Workstation con accesso privilegiato (ZAMPa)</span><span class="sxs-lookup"><span data-stu-id="6ed6a-177">Privileged Access Workstation (PAW)</span></span>

<span data-ttu-id="6ed6a-178">Per garantire che l'esecuzione di attività con privilegi elevati sia la più sicura possibile, utilizzare una ZAMPa.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-178">To ensure that the execution of highly privileged tasks is as secure as possible, use a PAW.</span></span> <span data-ttu-id="6ed6a-179">La ZAMPa è un computer dedicato utilizzato solo per le attività di configurazione sensibili, ad esempio la configurazione di Office 365 che richiede un account di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-179">A PAW is a dedicated computer that is only used for sensitive configuration tasks, such as Office 365 configuration that requires a global administrator account.</span></span> <span data-ttu-id="6ed6a-180">Poiché questo computer non viene utilizzato giornalmente per la navigazione Internet o la posta elettronica, è meglio proteggerlo dagli attacchi e dalle minacce di Internet.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-180">Because this computer is not used daily for Internet browsing or email, it is better protected from Internet attacks and threats.</span></span>
  
<span data-ttu-id="6ed6a-181">Per istruzioni su come configurare una ZAMPa, vedere [http://aka.ms/cyberpaw](http://aka.ms/cyberpaw).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-181">For instructions on how to set up a PAW, see [http://aka.ms/cyberpaw](http://aka.ms/cyberpaw).</span></span>
  
### <a name="azure-ad-privileged-identity-management-pim"></a><span data-ttu-id="6ed6a-182">Gestione delle identità di Azure AD Privileged Identity Management (PIM)</span><span class="sxs-lookup"><span data-stu-id="6ed6a-182">Azure AD Privileged Identity Management (PIM)</span></span>

<span data-ttu-id="6ed6a-183">Invece di avere gli account di amministratore globale assegnati definitivamente al ruolo di amministratore globale, è possibile utilizzare Azure AD PIM per abilitare l'assegnazione su richiesta del ruolo di amministratore globale quando necessario.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-183">Rather than having your global administrator accounts be permanently assigned the global administrator role, you can use Azure AD PIM to enable on-demand, just-in-time assignment of the global administrator role when it is needed.</span></span>
  
<span data-ttu-id="6ed6a-184">Gli account di amministratore globale, invece di essere amministratori permanenti, diventano amministratori idonei.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-184">Instead of your global administrator accounts being a permanent admin, they become eligible administrators.</span></span> <span data-ttu-id="6ed6a-185">Il ruolo di amministratore globale è inattivo finché non è necessario per un utente.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-185">The global administrator role is inactive until someone needs it.</span></span> <span data-ttu-id="6ed6a-186">Completare quindi un processo di attivazione per aggiungere il ruolo di amministratore globale all'account di amministratore globale per un periodo di tempo predeterminato.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-186">You then complete an activation process to add the global administrator role to the global administrator account for a predetermined amount of time.</span></span> <span data-ttu-id="6ed6a-187">Quando il tempo scade, PIM rimuove il ruolo di amministratore globale dall'account di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-187">When the time expires, PIM removes the global administrator role from the global administrator account.</span></span>
  
<span data-ttu-id="6ed6a-188">L'utilizzo di PIM e questo processo riduce significativamente la quantità di tempo in cui gli account di amministratore globale sono vulnerabili all'attacco e all'utilizzo da parte di utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-188">Using PIM and this process significantly reduces the amount of time that your global administrator accounts are vulnerable to attack and use by malicious users.</span></span>
  
<span data-ttu-id="6ed6a-189">Per ulteriori informazioni, vedere [Configure Azure ad privilegEd Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-189">For more information, see [Configure Azure AD Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure).</span></span>
  
> [!NOTE]
> <span data-ttu-id="6ed6a-190">PIM è disponibile con Azure Active Directory Premium P2, incluso in Enterprise Mobility + Security (EMS) E5, oppure è possibile acquistare licenze individuali per gli account di amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-190">PIM is available with Azure Active Directory Premium P2, which is included with Enterprise Mobility + Security (EMS) E5, or you can purchase individual licenses for your global administrator accounts.</span></span> 
  
### <a name="security-information-and-event-management-siem-software-for-office-365-logging"></a><span data-ttu-id="6ed6a-191">Software di sicurezza e gestione eventi (SIEM) per la registrazione di Office 365</span><span class="sxs-lookup"><span data-stu-id="6ed6a-191">Security information and event management (SIEM) software for Office 365 logging</span></span>

<span data-ttu-id="6ed6a-192">Il software di SIEM eseguito su un server esegue un'analisi in tempo reale degli avvisi di sicurezza e degli eventi creati dalle applicazioni e dall'hardware di rete.</span><span class="sxs-lookup"><span data-stu-id="6ed6a-192">SIEM software run on a server performs real-time analysis of security alerts and events created by applications and network hardware.</span></span> <span data-ttu-id="6ed6a-193">Per consentire al server SIEM di includere gli eventi e gli avvisi di sicurezza di Office 365 nelle relative funzioni di analisi e Reporting, integrarle nel sistema SIEM:</span><span class="sxs-lookup"><span data-stu-id="6ed6a-193">To allow your SIEM server to include Office 365 security alerts and events in its analysis and reporting functions, integrate these in your SIEM system:</span></span>
  
- <span data-ttu-id="6ed6a-194">Azure AD</span><span class="sxs-lookup"><span data-stu-id="6ed6a-194">Azure AD</span></span>
    
    <span data-ttu-id="6ed6a-195">Per ulteriori informazioni, vedere [integrare i log dalle risorse di Azure nei sistemi Siem](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-195">For more information, see [Integrate logs from Azure resources into your SIEM systems](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).</span></span>
    
- <span data-ttu-id="6ed6a-196">Office 365 Cloud App Security</span><span class="sxs-lookup"><span data-stu-id="6ed6a-196">Office 365 Cloud App Security</span></span>
    
    <span data-ttu-id="6ed6a-197">Per ulteriori informazioni, vedere [integrare il server Siem con Office 365 cloud app Security](https://support.office.com/article/dd6d2417-49c4-4de6-9294-67fdabbf8532).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-197">For more information, see [Integrate your SIEM server with Office 365 Cloud App Security](https://support.office.com/article/dd6d2417-49c4-4de6-9294-67fdabbf8532).</span></span>
    
## <a name="next-step"></a><span data-ttu-id="6ed6a-198">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="6ed6a-198">Next step</span></span>

<span data-ttu-id="6ed6a-199">Vedere [procedure consigliate per la sicurezza per Office 365](https://support.office.com/article/9295e396-e53d-49b9-ae9b-0b5828cdedc3).</span><span class="sxs-lookup"><span data-stu-id="6ed6a-199">See [Security best practices for Office 365](https://support.office.com/article/9295e396-e53d-49b9-ae9b-0b5828cdedc3).</span></span>
  

