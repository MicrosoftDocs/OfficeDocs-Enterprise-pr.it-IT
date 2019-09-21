---
title: Isolamento e controllo di accesso di Office 365 in Office 365
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
description: "Sintesi: una spiegazione dell'isolamento e del controllo di accesso all'interno delle diverse applicazioni di Office 365."
ms.openlocfilehash: 541aef20e885f6d7fbd505ffe2fe32a8525999d4
ms.sourcegitcommit: 55a046bdf49bf7c62ab74da73be1fd1cf6f0ad86
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/20/2019
ms.locfileid: "37067510"
---
# <a name="isolation-and-access-control-in-office-365"></a><span data-ttu-id="1c7d0-103">Isolamento e controllo di accesso in Office 365</span><span class="sxs-lookup"><span data-stu-id="1c7d0-103">Isolation and Access Control in Office 365</span></span>

<span data-ttu-id="1c7d0-104">Azure Active Directory e Office 365 utilizzano un modello di dati di elevata complessità che include decine di servizi, centinaia di entità, migliaia di relazioni e decine di migliaia di attributi.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-104">Azure Active Directory and Office 365 use a highly complex data model that includes tens of services, hundreds of entities, thousands of relationships, and tens of thousands of attributes.</span></span> <span data-ttu-id="1c7d0-105">A livello elevato, Azure Active Directory e le directory del servizio sono contenitori di tenant e destinatari mantenuti sincronizzati tramite protocolli di replica basati sullo stato.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-105">At a high level, Azure Active Directory and the service directories are the containers of tenants and recipients kept in sync using state-based replication protocols.</span></span> <span data-ttu-id="1c7d0-106">Oltre alle informazioni sulla directory conservate all'interno di Azure Active Directory, ognuno dei carichi di lavoro del servizio dispone di un'infrastruttura di servizi directory.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-106">In addition to the directory information held within Azure Active Directory, each of the service workloads have their own directory services infrastructure.</span></span>
 
![Sincronizzazione dei dati del tenant di Office 365](media/office-365-isolation-tenant-data-sync.png)

<span data-ttu-id="1c7d0-108">All'interno di questo modello non esiste un'unica origine di dati di directory.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-108">Within this model, there is no single source of directory data.</span></span> <span data-ttu-id="1c7d0-109">I sistemi specifici specificano singoli pezzi di dati, ma nessun singolo sistema contiene tutti i dati.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-109">Specific systems own individual pieces of data, but no single system holds all the data.</span></span> <span data-ttu-id="1c7d0-110">I servizi di Office 365 cooperano con Azure Active Directory in questo modello di dati.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-110">Office 365 services cooperate with Azure Active Directory in this data model.</span></span> <span data-ttu-id="1c7d0-111">Azure Active Directory è il "sistema di verità" per i dati condivisi, che in genere sono dati di piccole dimensioni e statici utilizzati da tutti i servizi.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-111">Azure Active Directory is the "system of truth" for shared data, which is typically small and static data used by every service.</span></span> <span data-ttu-id="1c7d0-112">Il modello federato utilizzato all'interno di Office 365 e Azure Active Directory fornisce la visualizzazione condivisa dei dati.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-112">The federated model used within Office 365 and Azure Active Directory provides the shared view of the data.</span></span>

<span data-ttu-id="1c7d0-113">Office 365 utilizza sia l'archiviazione fisica che lo spazio di archiviazione cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-113">Office 365 uses both physical storage and Azure cloud storage.</span></span> <span data-ttu-id="1c7d0-114">Exchange Online (incluso Exchange Online Protection) e Skype for business utilizzano la propria archiviazione per i dati dei clienti.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-114">Exchange Online (including Exchange Online Protection) and Skype for Business use their own storage for customer data.</span></span> <span data-ttu-id="1c7d0-115">SharePoint Online utilizza l'archiviazione di SQL Server e lo spazio di archiviazione di Azure, quindi la necessità di un ulteriore isolamento dei dati del cliente a livello di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-115">SharePoint Online uses both SQL Server storage and Azure Storage, hence the need for additional isolation of customer data at the storage level.</span></span>

## <a name="exchange-online"></a><span data-ttu-id="1c7d0-116">Exchange Online</span><span class="sxs-lookup"><span data-stu-id="1c7d0-116">Exchange Online</span></span>

<span data-ttu-id="1c7d0-117">Exchange Online memorizza i dati dei clienti all'interno delle cassette postali.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-117">Exchange Online stores customer data within mailboxes.</span></span> <span data-ttu-id="1c7d0-118">Le cassette postali sono ospitate all'interno dei database ESE (Extensible Storage Engine) chiamati database delle cassette postali</span><span class="sxs-lookup"><span data-stu-id="1c7d0-118">Mailboxes are hosted within Extensible Storage Engine (ESE) databases called mailbox databases.</span></span> <span data-ttu-id="1c7d0-119">Sono incluse le cassette postali utente, le cassette postali collegate, le cassette postali condivise e le cartelle pubbliche.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-119">This includes user mailboxes, linked mailboxes, shared mailboxes, and public folder mailboxes.</span></span> <span data-ttu-id="1c7d0-120">Le cassette postali degli utenti includono il contenuto salvato di Skype for business, ad esempio le storie di conversazione.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-120">User mailboxes include saved Skype for Business content, such as conversation histories.</span></span>

<span data-ttu-id="1c7d0-121">Il contenuto della cassetta postale dell'utente include:</span><span class="sxs-lookup"><span data-stu-id="1c7d0-121">User mailbox content includes:</span></span>

- <span data-ttu-id="1c7d0-122">Messaggi di posta elettronica e allegati e-mail</span><span class="sxs-lookup"><span data-stu-id="1c7d0-122">Emails and email attachments</span></span>
- <span data-ttu-id="1c7d0-123">Informazioni sulla disponibilità e sul calendario</span><span class="sxs-lookup"><span data-stu-id="1c7d0-123">Calendaring and free/busy information</span></span>
- <span data-ttu-id="1c7d0-124">Contacts</span><span class="sxs-lookup"><span data-stu-id="1c7d0-124">Contacts</span></span>
- <span data-ttu-id="1c7d0-125">Attività</span><span class="sxs-lookup"><span data-stu-id="1c7d0-125">Tasks</span></span>
- <span data-ttu-id="1c7d0-126">Note</span><span class="sxs-lookup"><span data-stu-id="1c7d0-126">Notes</span></span>
- <span data-ttu-id="1c7d0-127">Gruppi</span><span class="sxs-lookup"><span data-stu-id="1c7d0-127">Groups</span></span>
- <span data-ttu-id="1c7d0-128">Dati di inferenza</span><span class="sxs-lookup"><span data-stu-id="1c7d0-128">Inference data</span></span>

<span data-ttu-id="1c7d0-129">Ogni database delle cassette postali in Exchange Online contiene cassette postali provenienti da più tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-129">Each mailbox database within Exchange Online contains mailboxes from multiple tenants.</span></span> <span data-ttu-id="1c7d0-130">Un codice di autorizzazione protegge ogni cassetta postale, anche all'interno di una locazione.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-130">An authorization code secures each mailbox, including within a tenancy.</span></span> <span data-ttu-id="1c7d0-131">Per impostazione predefinita, solo l'utente assegnato ha accesso a una cassetta postale.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-131">By default, only the assigned user has access to a mailbox.</span></span> <span data-ttu-id="1c7d0-132">L'elenco di controllo di accesso (ACL, Access Control List) che protegge una cassetta postale contiene un'identità autenticata da Azure Active Directory a livello di tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-132">The access control list (ACL) that secures a mailbox contains an identity authenticated by Azure Active Directory at the tenant level.</span></span> <span data-ttu-id="1c7d0-133">Le cassette postali per ogni tenant sono limitate alle identità autenticate con il provider di autenticazione del tenant, che include solo gli utenti di tale tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-133">The mailboxes for each tenant are limited to identities authenticated against the tenant's authentication provider, which includes only users from that tenant.</span></span> <span data-ttu-id="1c7d0-134">Il contenuto del tenant a non può in alcun modo essere ottenuto dagli utenti nel tenant B, a meno che non sia esplicitamente approvato dal tenant A.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-134">Content in tenant A cannot in any way be obtained by users in tenant B, unless explicitly approved by tenant A.</span></span>

## <a name="skype-for-business"></a><span data-ttu-id="1c7d0-135">Skype for Business</span><span class="sxs-lookup"><span data-stu-id="1c7d0-135">Skype for Business</span></span>

<span data-ttu-id="1c7d0-136">Skype for business archivia i dati in vari punti:</span><span class="sxs-lookup"><span data-stu-id="1c7d0-136">Skype for Business stores data in various places:</span></span>

- <span data-ttu-id="1c7d0-137">Le informazioni sull'utente e sugli account, che includono gli endpoint di connessione, gli ID tenant, i dial plan, le impostazioni di roaming, lo stato di presenza, gli elenchi di contatti e così via, vengono archiviati nei server Skype for business Active Directory e in vari server di database di Skype for business.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-137">User and account information, which includes connection endpoints, tenant IDs, dial plans, roaming settings, presence state, contact lists, etc., is stored in the Skype for Business Active Directory servers, and in various Skype for Business database servers.</span></span> <span data-ttu-id="1c7d0-138">Gli elenchi di contatti vengono archiviati nella cassetta postale di Exchange Online dell'utente se l'utente è abilitato per entrambi i prodotti o su server Skype for business se l'utente non lo è.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-138">Contact lists are stored in the user's Exchange Online mailbox if the user is enabled for both products, or on Skype for Business servers if the user is not.</span></span> <span data-ttu-id="1c7d0-139">I server di database di Skype for business non sono partizionati per-tenant, ma l'isolamento dei dati in più locazioni viene applicato tramite il controllo di accesso basato sui ruoli (RBAC).</span><span class="sxs-lookup"><span data-stu-id="1c7d0-139">Skype for Business database servers are not partitioned per-tenant, but multi-tenancy isolation of data is enforced through role-based access control (RBAC).</span></span>
- <span data-ttu-id="1c7d0-140">Il contenuto delle riunioni e i dati caricati sono archiviati in condivisioni di file System (DFS) distribuiti.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-140">Meeting content and uploaded data is stored on Distributed File System (DFS) shares.</span></span> <span data-ttu-id="1c7d0-141">Questo contenuto può anche essere archiviato in Exchange Online se abilitato.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-141">This content can also be archived in Exchange Online if enabled.</span></span> <span data-ttu-id="1c7d0-142">Le condivisioni DFS non sono partizionate per-tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-142">The DFS shares are not partitioned per-tenant.</span></span> <span data-ttu-id="1c7d0-143">il contenuto è protetto con gli elenchi di controllo di accesso e la multilocazione viene applicata tramite RBAC.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-143">the content is secured with ACLs and multi-tenancy is enforced through RBAC.</span></span>
- <span data-ttu-id="1c7d0-144">I record dettagli chiamata, ovvero la cronologia delle attività, ad esempio la cronologia delle chiamate, le sessioni di messaggistica istantanea, la condivisione di applicazioni, la cronologia di messaggistica istantanea e così via, possono essere archiviati anche in Exchange Online, ma la maggior parte dei record dettagli chiamata è temporaneamente memorizzata nei server registrazione dettagli chiamata (CDR).</span><span class="sxs-lookup"><span data-stu-id="1c7d0-144">Call detail records, which are the activity history, such as call history, IM sessions, application sharing, IM history, etc., can also be stored in Exchange Online, but most call detail records are temporarily stored on call detail record (CDR) servers.</span></span> <span data-ttu-id="1c7d0-145">Il contenuto non viene partizionato per tenant, ma viene applicato tramite RBAC.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-145">Content is not partitioned per tenant, but multi-tenancy is enforced through RBAC.</span></span>

## <a name="sharepoint-online"></a><span data-ttu-id="1c7d0-146">SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="1c7d0-146">SharePoint Online</span></span>

<span data-ttu-id="1c7d0-147">SharePoint Online dispone di diversi meccanismi indipendenti che forniscono l'isolamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-147">SharePoint Online has several independent mechanisms that provide data isolation.</span></span> <span data-ttu-id="1c7d0-148">Archivia gli oggetti come codice astratto all'interno dei database dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-148">It stores objects as abstracted code within application databases.</span></span> <span data-ttu-id="1c7d0-149">Ad esempio, quando un utente carica un file in SharePoint Online, il file viene disassemblato, convertito nel codice dell'applicazione e archiviato in più tabelle tra più database.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-149">For example, when a user uploads a file to SharePoint Online, the file is disassembled, translated into application code, and stored in multiple tables across multiple databases.</span></span>

<span data-ttu-id="1c7d0-150">Se un utente può accedere direttamente allo spazio di archiviazione contenente i dati, il contenuto non può essere interpretato da un essere umano o da un sistema diverso da SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-150">If a user could gain direct access to the storage containing the data, the content is not interpretable to a human or any system other than SharePoint Online.</span></span> <span data-ttu-id="1c7d0-151">Tali meccanismi includono il controllo dell'accesso alla sicurezza e le proprietà.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-151">These mechanisms include security access control and properties.</span></span> <span data-ttu-id="1c7d0-152">Tutte le risorse di SharePoint Online sono protette dal codice di autorizzazione e dai criteri RBAC, anche all'interno di una locazione.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-152">All SharePoint Online resources are secured by the authorization code and RBAC policy, including within a tenancy.</span></span> <span data-ttu-id="1c7d0-153">L'elenco di controllo di accesso (ACL, Access Control List) che protegge una risorsa contiene un'identità autenticata a livello di tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-153">The access control list (ACL) that secures a resource contains an identity authenticated at the tenant level.</span></span> <span data-ttu-id="1c7d0-154">I dati di SharePoint Online per un tenant sono limitati alle identità autenticate dal provider di autenticazione per il tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-154">SharePoint Online data for a tenant is limited to identities authenticated by the authentication provider for the tenant.</span></span>

<span data-ttu-id="1c7d0-155">Oltre agli elenchi ACL, una proprietà a livello di tenant che specifica il provider di autenticazione (ovvero Azure Active Directory specifica del tenant) viene scritta una sola volta e non può essere modificata dopo l'impostazione.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-155">In addition to the ACLs, a tenant level property that specifies the authentication provider (which is the tenant-specific Azure Active Directory), is written once and cannot be changed once set.</span></span> <span data-ttu-id="1c7d0-156">Dopo aver impostato la proprietà tenant del provider di autenticazione per un tenant, non è possibile modificarla utilizzando le API esposte a un tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-156">Once the authentication provider tenant property has been set for a tenant, it cannot be changed using any APIs exposed to a tenant.</span></span>

<span data-ttu-id="1c7d0-157">Per ogni tenant viene utilizzato un *SubscriptionId* univoco.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-157">A unique *SubscriptionId* is used for each tenant.</span></span> <span data-ttu-id="1c7d0-158">Tutti i siti dei clienti sono di proprietà di un tenant e sono assegnati a un *SubscriptionId* univoco per il tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-158">All customer sites are owned by a tenant and assigned a *SubscriptionId* unique to the tenant.</span></span> <span data-ttu-id="1c7d0-159">La proprietà *SubscriptionId* di un sito viene scritta una volta ed è permanente.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-159">The *SubscriptionId* property on a site is written once and is permanent.</span></span> <span data-ttu-id="1c7d0-160">Una volta assegnata a un tenant, un sito non può essere spostato in un altro tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-160">Once assigned to a tenant, a site cannot be moved to a different tenant.</span></span> <span data-ttu-id="1c7d0-161">*SubscriptionId* è la chiave utilizzata per creare l'ambito di sicurezza per il provider di autenticazione ed è associato al tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-161">The *SubscriptionId* is the key used to create the security scope for the authentication provider and is tied to the tenant.</span></span>

<span data-ttu-id="1c7d0-162">SharePoint Online utilizza SQL Server e lo spazio di archiviazione di Azure per l'archiviazione dei metadati del contenuto.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-162">SharePoint Online uses SQL Server and Azure Storage for content metadata storage.</span></span> <span data-ttu-id="1c7d0-163">La chiave di partizione per l'archivio di contenuto è *siteID* in SQL.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-163">The partition key for the content store is *SiteId* in SQL.</span></span> <span data-ttu-id="1c7d0-164">Quando si esegue una query SQL, SharePoint Online utilizza un *siteID* verificato come parte di un controllo *SubscriptionId* a livello di tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-164">When running a SQL query, SharePoint Online uses a *SiteId* verified as part of a tenant-level *SubscriptionId* check.</span></span>

<span data-ttu-id="1c7d0-165">SharePoint Online archivia il contenuto del file crittografato nei BLOB di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-165">SharePoint Online stores encrypted file content in Microsoft Azure blobs.</span></span> <span data-ttu-id="1c7d0-166">Ogni farm di SharePoint Online dispone di un proprio account di Microsoft Azure e tutti gli oggetti BLOB salvati in Azure vengono crittografati singolarmente con una chiave memorizzata nell'archivio di contenuto SQL.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-166">Each SharePoint Online farm has its own Microsoft Azure account and all the blobs saved in Azure are encrypted individually with a key stored in the SQL content store.</span></span> <span data-ttu-id="1c7d0-167">La chiave di crittografia protetta nel codice dal livello di autorizzazione e non esposta direttamente all'utente finale.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-167">The encryption key protected in code by the authorization layer and not exposed directly to the end user.</span></span> <span data-ttu-id="1c7d0-168">SharePoint Online ha Monitoring in tempo reale per rilevare quando una richiesta HTTP legge o scrive i dati per più di un tenant.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-168">SharePoint Online has real-time monitoring to detect when an HTTP request reads or writes data for more than one tenant.</span></span> <span data-ttu-id="1c7d0-169">La richiesta Identity *SubscriptionId* viene registrata in base alla *SubscriptionId* della risorsa a cui si accede.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-169">The request identity *SubscriptionId* is tracked against the *SubscriptionId* of the accessed resource.</span></span> <span data-ttu-id="1c7d0-170">Le richieste di accesso alle risorse di più tenant non devono mai essere eseguite dagli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-170">Requests to access resources of more than one tenant should never happen by end users.</span></span> <span data-ttu-id="1c7d0-171">Le richieste di servizio in un ambiente multi-tenant sono l'unica eccezione.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-171">Service requests in a multi-tenant environment are the only exception.</span></span> <span data-ttu-id="1c7d0-172">Ad esempio, il crawler di ricerca estrae tutte le modifiche del contenuto per un intero database contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-172">For example, the search crawler pulls content changes for an entire database all at once.</span></span> <span data-ttu-id="1c7d0-173">Questo comporta di solito l'esecuzione di query su siti di più tenant in una singola richiesta di servizio, operazione eseguita per motivi di efficienza.</span><span class="sxs-lookup"><span data-stu-id="1c7d0-173">This usually involves querying sites of more than one tenant in a single service request, which is done for efficiency reasons.</span></span>