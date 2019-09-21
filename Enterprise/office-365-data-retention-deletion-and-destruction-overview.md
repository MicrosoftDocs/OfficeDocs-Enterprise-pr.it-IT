---
title: Conservazione, eliminazione e distruzione dei dati in Office 365
ms.author: robmazz
author: robmazz
manager: laurawi
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
ms.collection:
- Strat_O365_IP
- M365-security-compliance
description: Una panoramica dei criteri Microsoft per Office 365 relativa a conservazione, eliminazione e distruzione dei dati.
ms.openlocfilehash: 08b04e4fec762249208acb626fa20562ffecb82f
ms.sourcegitcommit: 55a046bdf49bf7c62ab74da73be1fd1cf6f0ad86
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/20/2019
ms.locfileid: "37067546"
---
# <a name="data-retention-deletion-and-destruction-in-office-365"></a><span data-ttu-id="2c742-103">Conservazione, eliminazione e distruzione dei dati in Office 365</span><span class="sxs-lookup"><span data-stu-id="2c742-103">Data Retention, Deletion, and Destruction in Office 365</span></span>

<span data-ttu-id="2c742-104">Microsoft dispone di un criterio di gestione dei dati standard per Office 365 che specifica la durata di conservazione dei dati del cliente dopo l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="2c742-104">Microsoft has a Data Handling Standard policy for Office 365 that specifies how long customer data is retained after deletion.</span></span> <span data-ttu-id="2c742-105">In genere, esistono due scenari in cui vengono eliminati i dati dei clienti:</span><span class="sxs-lookup"><span data-stu-id="2c742-105">There are generally two scenarios in which customer data is deleted:</span></span>

- <span data-ttu-id="2c742-106">**Eliminazione attiva:** Il tenant ha un abbonamento attivo e un utente elimina i dati, oppure Elimina i dati forniti da un utente.</span><span class="sxs-lookup"><span data-stu-id="2c742-106">**Active Deletion:** The tenant has an active subscription and a user deletes data, or administrators delete data provided by a user.</span></span>
- <span data-ttu-id="2c742-107">**Eliminazione passiva:** La sottoscrizione tenant termina.</span><span class="sxs-lookup"><span data-stu-id="2c742-107">**Passive Deletion:** The tenant subscription ends.</span></span>

## <a name="data-retention"></a><span data-ttu-id="2c742-108">Conservazione dei dati</span><span class="sxs-lookup"><span data-stu-id="2c742-108">Data Retention</span></span>

<span data-ttu-id="2c742-109">Per ognuno di questi scenari di eliminazione, nella tabella seguente viene mostrato il periodo di conservazione dei dati massimo, per categoria e classificazione dei dati:</span><span class="sxs-lookup"><span data-stu-id="2c742-109">For each of these deletion scenarios, the following table shows the maximum data retention period, by data category and classification:</span></span>

| <span data-ttu-id="2c742-110">Categoria di dati</span><span class="sxs-lookup"><span data-stu-id="2c742-110">Data Category</span></span> | <span data-ttu-id="2c742-111">Classificazione dei dati</span><span class="sxs-lookup"><span data-stu-id="2c742-111">Data Classification</span></span> | <span data-ttu-id="2c742-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2c742-112">Description</span></span> | <span data-ttu-id="2c742-113">Esempi</span><span class="sxs-lookup"><span data-stu-id="2c742-113">Examples</span></span> | <span data-ttu-id="2c742-114">Periodo di conservazione</span><span class="sxs-lookup"><span data-stu-id="2c742-114">Retention Period</span></span> |
|-----------------|-----------------|-----------------|----------------------------------|-------------------------------|
| <span data-ttu-id="2c742-115">Dati cliente
</span><span class="sxs-lookup"><span data-stu-id="2c742-115">Customer Data</span></span> | <span data-ttu-id="2c742-116">Contenuto del cliente</span><span class="sxs-lookup"><span data-stu-id="2c742-116">Customer Content</span></span>| <span data-ttu-id="2c742-117">Contenuto direttamente fornito/creato da amministratori e utenti</span><span class="sxs-lookup"><span data-stu-id="2c742-117">Content directly provided/created by admins and users</span></span> <br><br> <span data-ttu-id="2c742-118">Include tutto il testo, audio, video, file di immagine e software creati e archiviati nei data center di Microsoft quando si utilizzano i servizi in Office 365</span><span class="sxs-lookup"><span data-stu-id="2c742-118">Includes all text, sound, video, image files, and software created and stored in Microsoft data centers when using the services in Office 365</span></span> | <span data-ttu-id="2c742-119">Esempi delle applicazioni di Office 365 più comunemente utilizzate che consentono agli utenti di creare dati includono Word, Excel, PowerPoint, Outlook e OneNote</span><span class="sxs-lookup"><span data-stu-id="2c742-119">Examples of the most commonly used Office 365 applications that allow users to author data include Word, Excel, PowerPoint, Outlook, and OneNote</span></span> <br><br> <span data-ttu-id="2c742-120">Il contenuto del cliente include anche i segreti di proprietà dei clienti/forniti (password, certificati, chiavi di crittografia, chiavi di archiviazione)</span><span class="sxs-lookup"><span data-stu-id="2c742-120">Customer content also includes customer-owned/provided secrets (passwords, certificates, encryption keys, storage keys)</span></span> | <span data-ttu-id="2c742-121">**Scenario di eliminazione attiva:** al massimo 30 giorni</span><span class="sxs-lookup"><span data-stu-id="2c742-121">**Active Deletion Scenario:** at most 30 days</span></span> <br><br> <span data-ttu-id="2c742-122">**Scenario di eliminazione passiva:** al massimo 180 giorni</span><span class="sxs-lookup"><span data-stu-id="2c742-122">**Passive Deletion Scenario:** at most 180 days</span></span> |
| <span data-ttu-id="2c742-123">Dati cliente
</span><span class="sxs-lookup"><span data-stu-id="2c742-123">Customer Data</span></span> | <span data-ttu-id="2c742-124">Informazioni identificabili dall'utente finale (EUII)</span><span class="sxs-lookup"><span data-stu-id="2c742-124">End User Identifiable Information (EUII)</span></span> | <span data-ttu-id="2c742-125">Dati che identificano o possono essere utilizzati per identificare l'utente di un servizio Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c742-125">Data that identifies or could be used to identify the user of a Microsoft service.</span></span> <span data-ttu-id="2c742-126">EUII non contiene contenuto del cliente</span><span class="sxs-lookup"><span data-stu-id="2c742-126">EUII does not contain Customer content</span></span> | <span data-ttu-id="2c742-127">Nome utente o nome visualizzato (dominio\nomeutente)</span><span class="sxs-lookup"><span data-stu-id="2c742-127">User name or display name (DOMAIN\UserName)</span></span> <br><br> <span data-ttu-id="2c742-128">Nome dell'entità utente (nome @ dominio)</span><span class="sxs-lookup"><span data-stu-id="2c742-128">User principal name (name@domain)</span></span> <br><br>  <span data-ttu-id="2c742-129">Indirizzi IP specifici dell'utente</span><span class="sxs-lookup"><span data-stu-id="2c742-129">User-specific IP addresses</span></span> | <span data-ttu-id="2c742-130">**Scenario di eliminazione attiva:** al massimo 180 giorni (solo un'azione di amministratore tenant)</span><span class="sxs-lookup"><span data-stu-id="2c742-130">**Active Deletion Scenario:** at most 180 days (only a tenant administrator action)</span></span> <br><br> <span data-ttu-id="2c742-131">**Scenario di eliminazione passiva:** al massimo 180 giorni</span><span class="sxs-lookup"><span data-stu-id="2c742-131">**Passive Deletion Scenario:** at most 180 days</span></span> |
| <span data-ttu-id="2c742-132">Dati personali</span><span class="sxs-lookup"><span data-stu-id="2c742-132">Personal Data</span></span> <br> <span data-ttu-id="2c742-133">(dati non inclusi nei dati del cliente)</span><span class="sxs-lookup"><span data-stu-id="2c742-133">(data not included in Customer Data)</span></span> | <span data-ttu-id="2c742-134">Identificatori pseudonimi dell'utente finale (EUPI)</span><span class="sxs-lookup"><span data-stu-id="2c742-134">End User Pseudonymous Identifiers (EUPI)</span></span> | <span data-ttu-id="2c742-135">Identificatore creato da Microsoft associato all'utente di un servizio Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c742-135">An identifier created by Microsoft tied to the user of a Microsoft service.</span></span> <span data-ttu-id="2c742-136">Se in combinazione con altre informazioni, ad esempio una tabella di mapping, EUPI identifica l'utente finale</span><span class="sxs-lookup"><span data-stu-id="2c742-136">When combined with other information, such as a mapping table, EUPI identifies the end user</span></span> <br><br> <span data-ttu-id="2c742-137">EUPI non contiene informazioni caricate o create dal cliente</span><span class="sxs-lookup"><span data-stu-id="2c742-137">EUPI does not contain information uploaded or created by the customer</span></span> | <span data-ttu-id="2c742-138">GUID utente, PUID o SID</span><span class="sxs-lookup"><span data-stu-id="2c742-138">User GUIDs, PUIDs, or SIDs</span></span> <br><br> <span data-ttu-id="2c742-139">ID di sessione</span><span class="sxs-lookup"><span data-stu-id="2c742-139">Session IDs</span></span> | <span data-ttu-id="2c742-140">**Scenario di eliminazione attiva:** al massimo 30 giorni</span><span class="sxs-lookup"><span data-stu-id="2c742-140">**Active Deletion Scenario:** at most 30 days</span></span> <br><br> <span data-ttu-id="2c742-141">**Scenario di eliminazione passiva:** al massimo 180 giorni</span><span class="sxs-lookup"><span data-stu-id="2c742-141">**Passive Deletion Scenario:** at most 180 days</span></span> |

## <a name="subscription-retention"></a><span data-ttu-id="2c742-142">Conservazione della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="2c742-142">Subscription Retention</span></span>

<span data-ttu-id="2c742-143">Nel termine di un abbonamento attivo, un Sottoscrittore può accedere, estrarre o eliminare i dati dei clienti archiviati in Office 365.</span><span class="sxs-lookup"><span data-stu-id="2c742-143">In the term of an active subscription, a subscriber can access, extract, or delete customer data stored in Office 365.</span></span> <span data-ttu-id="2c742-144">Se una sottoscrizione a pagamento termina o è terminata, Microsoft conserva i dati dei clienti archiviati in Office 365 in un account con funzione limitata per 90 giorni per consentire al Sottoscrittore di estrarre i dati.</span><span class="sxs-lookup"><span data-stu-id="2c742-144">If a paid subscription ends or is terminated, Microsoft retains customer data stored in Office 365 in a limited-function account for 90 days to enable the subscriber to extract the data.</span></span> <span data-ttu-id="2c742-145">Al termine del periodo di conservazione di 90 giorni, Microsoft disattiva l'account ed Elimina i dati del cliente.</span><span class="sxs-lookup"><span data-stu-id="2c742-145">After the 90-day retention period ends, Microsoft disables the account and deletes the customer data.</span></span> <span data-ttu-id="2c742-146">Non più di 180 giorni dopo la scadenza o la terminazione di un abbonamento a Office 365, Microsoft disattiva l'account ed Elimina tutti i dati dei clienti dall'account.</span><span class="sxs-lookup"><span data-stu-id="2c742-146">No more than 180 days after expiration or termination of a subscription to Office 365, Microsoft disables the account and deletes all customer data from the account.</span></span> <span data-ttu-id="2c742-147">Una volta trascorso il periodo di conservazione massimo per tutti i dati, i dati vengono resi commercialmente irrecuperabili.</span><span class="sxs-lookup"><span data-stu-id="2c742-147">Once the maximum retention period for any data has elapsed, the data is rendered commercially unrecoverable.</span></span>

<span data-ttu-id="2c742-148">Per una versione di valutazione gratuita, il tuo account si sposta in uno stato di grazia per 30 giorni nella maggior parte dei paesi e delle aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="2c742-148">For a free trial, your account moves into a grace status for 30 days in most countries and regions.</span></span> <span data-ttu-id="2c742-149">Durante questo periodo di tolleranza è possibile acquistare Office 365.</span><span class="sxs-lookup"><span data-stu-id="2c742-149">During this grace period, you can purchase Office 365.</span></span> <span data-ttu-id="2c742-150">Se si decide di non acquistare Office 365, è possibile annullare la versione di valutazione o lasciare scadere il periodo di prova e le informazioni e i dati dell'account di valutazione vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="2c742-150">If you decide not to buy Office 365, you can either cancel your trial or let the grace period expire, and your trial account information and data is deleted.</span></span>

## <a name="expedited-deletion"></a><span data-ttu-id="2c742-151">Eliminazione rapida</span><span class="sxs-lookup"><span data-stu-id="2c742-151">Expedited Deletion</span></span>

<span data-ttu-id="2c742-152">Per qualsiasi sottoscrizione, un Sottoscrittore può contattare il supporto tecnico Microsoft e richiedere il deprovisioning di sottoscrizione celere.</span><span class="sxs-lookup"><span data-stu-id="2c742-152">For any subscription, a subscriber can contact Microsoft Support and request expedited subscription de-provisioning.</span></span> <span data-ttu-id="2c742-153">In questo processo, tutti i dati degli utenti vengono eliminati tre giorni dopo l'immissione del codice di blocco fornito da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2c742-153">In this process, all user data is deleted three days after the administrator enters the lockout code provided by Microsoft.</span></span> <span data-ttu-id="2c742-154">Sono inclusi i dati in SharePoint Online e Exchange online in blocco o archiviati in cassette postali inattive.</span><span class="sxs-lookup"><span data-stu-id="2c742-154">This includes data in SharePoint Online and Exchange Online under hold or stored in inactive mailboxes.</span></span>

<span data-ttu-id="2c742-155">Per ulteriori informazioni sul deprovisioning rapido, vedere [Annulla Office 365](https://support.office.com/article/Cancel-Office-365-for-business-b1bc0bef-4608-4601-813a-cdd9f746709a).</span><span class="sxs-lookup"><span data-stu-id="2c742-155">For more information on expedited de-provisioning, see [Cancel Office 365](https://support.office.com/article/Cancel-Office-365-for-business-b1bc0bef-4608-4601-813a-cdd9f746709a).</span></span>

## <a name="related-links"></a><span data-ttu-id="2c742-156">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="2c742-156">Related Links</span></span>
- [<span data-ttu-id="2c742-157">Distruzione dei dati</span><span class="sxs-lookup"><span data-stu-id="2c742-157">Data Destruction</span></span>](office-365-data-destruction.md)
- [<span data-ttu-id="2c742-158">Capacità di immutabilità in Office 365</span><span class="sxs-lookup"><span data-stu-id="2c742-158">Immutability in Office 365</span></span>](office-365-data-immutability.md)
- [<span data-ttu-id="2c742-159">Eliminazione dei dati di Exchange Online</span><span class="sxs-lookup"><span data-stu-id="2c742-159">Exchange Online Data Deletion</span></span>](office-365-exchange-online-data-deletion.md)
- [<span data-ttu-id="2c742-160">Eliminazione dei dati di SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2c742-160">SharePoint Online Data Deletion</span></span>](office-365-sharepoint-online-data-deletion.md)
- [<span data-ttu-id="2c742-161">Eliminazione dei dati di Skype for Business</span><span class="sxs-lookup"><span data-stu-id="2c742-161">Skype for Business Data Deletion</span></span>](office-365-skype-data-deletion.md)