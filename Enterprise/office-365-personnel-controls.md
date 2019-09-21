---
title: Controlli del personale di Office 365
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
description: 'Riepilogo: Panoramica delle procedure di screening del personale Microsoft per Office 365.'
ms.openlocfilehash: 82a8578ef5b5812dc3dfcfa69ccff604d2254286
ms.sourcegitcommit: 55a046bdf49bf7c62ab74da73be1fd1cf6f0ad86
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/20/2019
ms.locfileid: "37067497"
---
# <a name="office-365-personnel-controls"></a><span data-ttu-id="2021b-103">Controlli del personale di Office 365</span><span class="sxs-lookup"><span data-stu-id="2021b-103">Office 365 Personnel Controls</span></span> 

<span data-ttu-id="2021b-104">Lo screening del personale, il processo di revisione e la convalida del comportamento e dello stato del passato per un richiedente, è un importante controllo di attenuazione per impedire il compromesso di servizio di Office 365.</span><span class="sxs-lookup"><span data-stu-id="2021b-104">Personnel screening, the process of review and validation of the past behavior and status for an applicant, is an important mitigation control to prevent Office 365 service compromise.</span></span> <span data-ttu-id="2021b-105">Anche se il comportamento passato non è un fattore predittivo perfetto per il comportamento futuro, contribuisce all'identificazione di potenziali attori cattivi.</span><span class="sxs-lookup"><span data-stu-id="2021b-105">While past behavior is not a perfect predictor of future behavior, it does help to identify potential bad actors.</span></span> <span data-ttu-id="2021b-106">Lo standard di screening del personale Microsoft si applica a tutti i dipendenti Microsoft, gli stagisti e il personale contingente coinvolti nello sviluppo, nel funzionamento o nella distribuzione dei servizi online ai clienti cloud governativi o commerciali.</span><span class="sxs-lookup"><span data-stu-id="2021b-106">The Microsoft Personnel Screening Standard applies to all Microsoft employees, interns, and contingent staff involved in the development, operation, or delivery of online services to government or commercial cloud customers.</span></span> <span data-ttu-id="2021b-107">Gli standard di screening per gli ambienti cloud nazionali non gestiti da Microsoft sono definiti dal personale dei partner operativi per ogni ambiente specifico.</span><span class="sxs-lookup"><span data-stu-id="2021b-107">Screening standards for National Cloud environments not operated by Microsoft are defined by the operating partner personnel for each specific environment.</span></span>

## <a name="the-microsoft-personnel-screening-standard"></a><span data-ttu-id="2021b-108">Standard di screening del personale Microsoft</span><span class="sxs-lookup"><span data-stu-id="2021b-108">The Microsoft Personnel Screening Standard</span></span>

<span data-ttu-id="2021b-109">Le procedure di screening del personale per Office 365 sono conformi agli standard aziendali di Microsoft e ai controlli di National Institute of Standards and Technology (NIST) per lo screening del personale.</span><span class="sxs-lookup"><span data-stu-id="2021b-109">The personnel screening practices for Office 365 align with Microsoft's corporate standards and National Institute of Standards and Technology (NIST) controls for personnel screening.</span></span> <span data-ttu-id="2021b-110">Gli addetti Microsoft che richiedono l'accesso ai seguenti elementi sono soggetti allo standard di screening del personale Microsoft:</span><span class="sxs-lookup"><span data-stu-id="2021b-110">Microsoft staff who require access to the following are subject to the Microsoft Personnel Screening Standard:</span></span>

- <span data-ttu-id="2021b-111">Accesso fisico ai centri dati, colocazioni, sale protette, gabbie, server rack o siti perimetrali che forniscono l'infrastruttura che supporta i servizi online per i clienti governativi o commerciali del cloud.</span><span class="sxs-lookup"><span data-stu-id="2021b-111">Physical access to datacenters, colocations, secured rooms, cages, server racks, or edge sites that provide the infrastructure supporting online services for government or commercial cloud customers.</span></span>
- <span data-ttu-id="2021b-112">Accesso logico ai dati dei clienti cloud governativi o commerciali forniti tramite ambienti gestiti specifici.</span><span class="sxs-lookup"><span data-stu-id="2021b-112">Logical access to government or commercial cloud Customer Data provided through specific managed environments.</span></span>
- <span data-ttu-id="2021b-113">Accesso alla gestione della rete ai dispositivi e ai servizi che trasportano o archiviano i dati dei clienti del cloud governativo o commerciale.</span><span class="sxs-lookup"><span data-stu-id="2021b-113">Network management access to devices and services that transport or store government or commercial cloud Customer Data.</span></span>

<span data-ttu-id="2021b-114">Gli eventi specifici relativi al personale che attivano i requisiti di screening includono:</span><span class="sxs-lookup"><span data-stu-id="2021b-114">Specific personnel-related events that trigger screening requirements include:</span></span>

- <span data-ttu-id="2021b-115">Nuovo personale Microsoft inserito nei ruoli in cui la selezione è un requisito definito.</span><span class="sxs-lookup"><span data-stu-id="2021b-115">New Microsoft staff placed in roles where screening is a defined requirement.</span></span>
- <span data-ttu-id="2021b-116">Personale Microsoft interno trasferito o spostato a un ruolo esistente che attualmente include la schermatura come requisito definito.</span><span class="sxs-lookup"><span data-stu-id="2021b-116">Internal Microsoft staff transferred or moved to an existing role that currently includes screening as a defined requirement.</span></span>
- <span data-ttu-id="2021b-117">Ruoli esistenti che modificano l'ambito per includere lo screening come requisito definito.</span><span class="sxs-lookup"><span data-stu-id="2021b-117">Existing roles that change scope to include screening as a defined requirement.</span></span>

## <a name="screening-enforcement-criteria"></a><span data-ttu-id="2021b-118">Criteri di applicazione della schermatura</span><span class="sxs-lookup"><span data-stu-id="2021b-118">Screening enforcement criteria</span></span>

<span data-ttu-id="2021b-119">Per garantire che solo il personale autorizzato abbia accesso ai dati dei clienti o agli ambienti che richiedono la selezione, si applicano i criteri di applicazione seguenti.</span><span class="sxs-lookup"><span data-stu-id="2021b-119">To ensure that only approved personnel have access to Customer Data or environments that require screening, the following enforcement criteria applies.</span></span>

<span data-ttu-id="2021b-120">**Solo ambienti cloud degli Stati Uniti**:</span><span class="sxs-lookup"><span data-stu-id="2021b-120">**United States cloud environments only**:</span></span>

- <span data-ttu-id="2021b-121">L'accesso ai dati dei clienti o agli ambienti che richiedono la selezione è consentito solo dopo il completamento dell'aggiudicazione e vengono passati i requisiti di screening.</span><span class="sxs-lookup"><span data-stu-id="2021b-121">Access to Customer Data or environments that require screening is permitted only after adjudication is completed and screening requirements are passed.</span></span>
- <span data-ttu-id="2021b-122">Il personale Microsoft che non richiede più l'accesso ai dati dei clienti o agli ambienti correlati ha accesso rimosso al momento di lasciare Microsoft o passare a un nuovo ruolo.</span><span class="sxs-lookup"><span data-stu-id="2021b-122">Microsoft staff who no longer require access to Customer Data or related environments have access removed upon leaving Microsoft or moving to a new role.</span></span>
- <span data-ttu-id="2021b-123">Il personale Microsoft lascia le smart card dell'ambiente schermato con la gestione prima di lasciare gli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="2021b-123">Microsoft staff leave screened environment smart cards with management before leaving the United States.</span></span>

<span data-ttu-id="2021b-124">**Ambienti cloud nazionali**:</span><span class="sxs-lookup"><span data-stu-id="2021b-124">**National cloud environments**:</span></span>

- <span data-ttu-id="2021b-125">L'operatore di terze parti o il personale trustee dei dati è responsabile della gestione e dell'applicazione dell'accesso per gli ambienti cloud nazionali.</span><span class="sxs-lookup"><span data-stu-id="2021b-125">Third-party operator or data trustee personnel are responsible for managing and enforcing access for National Cloud environments.</span></span>

<span data-ttu-id="2021b-126">Negli ambienti Microsoft Cloud Services, Access è limitato in base al ruolo di una persona e al tipo di dati coinvolti, come descritto nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="2021b-126">Within Microsoft's cloud services environments, access is restricted based on a person's role and the type of data involved, as detailed in the table below.</span></span> <span data-ttu-id="2021b-127">Non è consentito l'accesso ai dati dei clienti all'interno di un cloud degli Stati Uniti in un sito personale qualificato o non qualificato fisicamente all'esterno degli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="2021b-127">Qualified or unqualified personnel physically located outside of the United States are not permitted to have access to Customer Data within a United States cloud.</span></span> <span data-ttu-id="2021b-128">L'accesso agli ambienti cloud nazionali è limitato in modo che il personale Microsoft non disponga di accesso tecnico ai dati dei clienti, o sistemi che contengono dati dei clienti, senza l'approvazione da parte dell'operatore di terze parti o del trustee dei dati.</span><span class="sxs-lookup"><span data-stu-id="2021b-128">Access to National Cloud environments is restricted so that Microsoft personnel do not have technical access to Customer Data, or systems that contain Customer Data, without approval by the third-party operator or data trustee.</span></span>

| <span data-ttu-id="2021b-129">Ruolo</span><span class="sxs-lookup"><span data-stu-id="2021b-129">Role</span></span> | <span data-ttu-id="2021b-130">Accesso ai dati dei clienti</span><span class="sxs-lookup"><span data-stu-id="2021b-130">Access to Customer Data</span></span> | <span data-ttu-id="2021b-131">Accesso ai dati di sistema</span><span class="sxs-lookup"><span data-stu-id="2021b-131">Access to System Data</span></span> |
|---------------------------------------------------------------------------|------------------------------|---------------------------------|
| <span data-ttu-id="2021b-132">Personale qualificato che si trova fisicamente negli Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="2021b-132">Qualified Personnel physically located in the United States</span></span> | <span data-ttu-id="2021b-133">Consentito</span><span class="sxs-lookup"><span data-stu-id="2021b-133">Permitted</span></span> | <span data-ttu-id="2021b-134">Consentito</span><span class="sxs-lookup"><span data-stu-id="2021b-134">Permitted</span></span> |
| <span data-ttu-id="2021b-135">Personale qualificato che si trova fisicamente all'esterno degli Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="2021b-135">Qualified Personnel physically located outside of the United States</span></span> | <span data-ttu-id="2021b-136">Non consentita</span><span class="sxs-lookup"><span data-stu-id="2021b-136">Not Permitted</span></span> | <span data-ttu-id="2021b-137">Consentito</span><span class="sxs-lookup"><span data-stu-id="2021b-137">Permitted</span></span> |
| <span data-ttu-id="2021b-138">Accesso alle eccezioni internazionali per il personale Microsoft: consente l'accesso logico per il personale Microsoft che non risiede nel paese in cui il governo o i dati del cliente commerciale sono a riposo</span><span class="sxs-lookup"><span data-stu-id="2021b-138">International Exception Access for Microsoft Staff: Enables logical access for Microsoft staff not residing in the country where the government or commercial Customer Data is at rest</span></span> | <span data-ttu-id="2021b-139">Non consentita</span><span class="sxs-lookup"><span data-stu-id="2021b-139">Not Permitted</span></span> | <span data-ttu-id="2021b-140">Consentito</span><span class="sxs-lookup"><span data-stu-id="2021b-140">Permitted</span></span> |
| <span data-ttu-id="2021b-141">Personale non qualificato (personale non sottoposto a screening che richiede una scorta da personale qualificato)</span><span class="sxs-lookup"><span data-stu-id="2021b-141">Unqualified Personnel (unscreened personnel that require an escort by qualified personnel)</span></span> | <span data-ttu-id="2021b-142">Consentito con autorizzazione</span><span class="sxs-lookup"><span data-stu-id="2021b-142">Permitted with authorization</span></span> | <span data-ttu-id="2021b-143">Consentito con supervisione Escort</span><span class="sxs-lookup"><span data-stu-id="2021b-143">Permitted with escort oversight</span></span> |

## <a name="microsoft-pre-employment-screening"></a><span data-ttu-id="2021b-144">Screening preimpiego Microsoft</span><span class="sxs-lookup"><span data-stu-id="2021b-144">Microsoft pre-employment screening</span></span>

<span data-ttu-id="2021b-145">Laddove la legge locale lo consente, il dipartimento di sicurezza globale di Microsoft conduce lo screening di preimpiego.</span><span class="sxs-lookup"><span data-stu-id="2021b-145">Where local law allows for it, Microsoft's Global Security Department conducts pre-employment screening.</span></span> <span data-ttu-id="2021b-146">Si tratta di un'analisi di sfondo formale che include i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="2021b-146">This is a formal background investigation that includes the following criteria:</span></span>

- <span data-ttu-id="2021b-147">Verifica del riassunto del richiedente per completezza e accuratezza</span><span class="sxs-lookup"><span data-stu-id="2021b-147">A check of the applicant's resume for completeness and accuracy</span></span>
- <span data-ttu-id="2021b-148">Conferma dei diplomi accademici e professionali</span><span class="sxs-lookup"><span data-stu-id="2021b-148">Confirmation of academic and professional qualifications</span></span>
- <span data-ttu-id="2021b-149">Indagini su eventuali perdite di credenziali professionali</span><span class="sxs-lookup"><span data-stu-id="2021b-149">Investigation of any loss of professional credentials</span></span>
- <span data-ttu-id="2021b-150">Verifica degli ultimi tre datori di lavoro</span><span class="sxs-lookup"><span data-stu-id="2021b-150">Verification of past three employers</span></span>
- <span data-ttu-id="2021b-151">Un controllo dei record di polizia per condanne a reato</span><span class="sxs-lookup"><span data-stu-id="2021b-151">A check of police records for felony convictions</span></span>
- <span data-ttu-id="2021b-152">Conferma dell'identità da un'identificazione emessa dal governo</span><span class="sxs-lookup"><span data-stu-id="2021b-152">Confirmation of identity from a government-issued identification</span></span>
- <span data-ttu-id="2021b-153">Verifiche del credito se appropriate</span><span class="sxs-lookup"><span data-stu-id="2021b-153">Credit checks where appropriate</span></span>

<span data-ttu-id="2021b-154">Possono essere necessari riesami periodici e/o controlli in background aggiuntivi per alcuni ruoli di gestione, sicurezza o di altro genere, tra cui i dipendenti basati su Stati Uniti nei ruoli che richiedono l'accesso ai dati dei clienti.</span><span class="sxs-lookup"><span data-stu-id="2021b-154">Periodic re-screening and/or additional background checks may be required for certain management, security, or other roles, including but not limited to United States-based employees in roles that require access to Customer Data.</span></span>
<span data-ttu-id="2021b-155">Per il personale contingente, il contratto con la terza parte specifica i requisiti di Microsoft per la selezione che devono essere eseguiti da terze parti.</span><span class="sxs-lookup"><span data-stu-id="2021b-155">For contingent staff, the contract with the third party specifies Microsoft's requirements for screening that must be conducted by the third party.</span></span> <span data-ttu-id="2021b-156">Per i controlli in background, la società di terze parti è responsabile di fornire alla verifica Microsoft che è stato eseguito un controllo in background.</span><span class="sxs-lookup"><span data-stu-id="2021b-156">For background checks, the third-party company is responsible for providing to Microsoft verification that a background check has been performed.</span></span> <span data-ttu-id="2021b-157">I risultati del controllo dei precedenti vengono in genere ricevuti tramite posta elettronica dal reparto risorse umane di terze parti.</span><span class="sxs-lookup"><span data-stu-id="2021b-157">The results of the background check are typically received via email from the third party's human resources department.</span></span> <span data-ttu-id="2021b-158">I dipendenti internazionali del personale contrattuale possono essere esonerati dal processo di screening in background a causa di leggi nei paesi che proibiscono i controlli in background.</span><span class="sxs-lookup"><span data-stu-id="2021b-158">International employees of contract staff may be exempt from the background screening process due to laws in countries that prohibit background checks.</span></span>

## <a name="microsoft-employment-screening"></a><span data-ttu-id="2021b-159">Screening di Microsoft Employment</span><span class="sxs-lookup"><span data-stu-id="2021b-159">Microsoft employment screening</span></span>

<span data-ttu-id="2021b-160">Poiché 2004 negli Stati Uniti, Microsoft richiede dipendenti e stagisti a passare una schermata di registrazione criminale di sette anni nell'ambito dello screening di preimpiego.</span><span class="sxs-lookup"><span data-stu-id="2021b-160">Since 2004 in the United States, Microsoft requires employees and interns to pass a seven-year criminal record screen as part of pre-employment screening.</span></span> <span data-ttu-id="2021b-161">È incluso lo screening per reati, reati e verifica dell'istruzione e della storia del lavoro.</span><span class="sxs-lookup"><span data-stu-id="2021b-161">Screening for felonies, misdemeanors, and verification of education and employment history is included.</span></span>

<span data-ttu-id="2021b-162">Prima di assegnare a qualsiasi dipendente Microsoft statunitense o a un subappaltatore assegnato Microsoft statunitense per fornire servizi correlati a Office 365, Microsoft esegue e richiede che i subappaltatori effettuino un controllo dei precedenti costituito da una traccia del numero di previdenza sociale e controllo di fedina penale.</span><span class="sxs-lookup"><span data-stu-id="2021b-162">Before assigning any US Microsoft employee or any US Microsoft-assigned subcontractor to provide Office 365-related services, Microsoft conducts and requires subcontractors to conduct a background check consisting of a Social Security number trace and criminal record check.</span></span> <span data-ttu-id="2021b-163">I dati di questo controllo di sfondo sono un fattore della decisione di assunzione.</span><span class="sxs-lookup"><span data-stu-id="2021b-163">The data from this background check is a factor in the hiring decision.</span></span> <span data-ttu-id="2021b-164">Il controllo di fedina penale include un reato di sette anni e un controllo dei precedenti penali nei registri federali, statali e della contea (se applicabile).</span><span class="sxs-lookup"><span data-stu-id="2021b-164">The criminal record check includes a seven-year felony and misdemeanor criminal records check of federal, state, and county records (as applicable).</span></span>

<span data-ttu-id="2021b-165">Come condizione di impiego e al momento del noleggio, tutti i dipendenti Microsoft sono tenuti a firmare contratti di riservatezza e non divulgazione e a verificare di aver esaminato il manuale dei dipendenti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2021b-165">As a condition of employment and at the time of hire, all Microsoft employees are required to sign confidentiality and non-disclosure agreements, and to verify that they have reviewed the Microsoft Employee Handbook.</span></span>

## <a name="microsoft-cloud-background-check"></a><span data-ttu-id="2021b-166">Controllo del background di Microsoft Cloud</span><span class="sxs-lookup"><span data-stu-id="2021b-166">Microsoft cloud background check</span></span>

<span data-ttu-id="2021b-167">È necessario un controllo dei precedenti cloud di Microsoft per i candidati assunti come dipendenti che forniscono servizi correlati a Office 365 negli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="2021b-167">A Microsoft Cloud Background Check is required for candidates hired as employees providing Office 365-related services in the United States.</span></span> <span data-ttu-id="2021b-168">Gli impiegati Microsoft negli Stati Uniti con accesso ai dati dei clienti devono seguire il processo di controllo dei precedenti del cloud Microsoft richiesto da tutti i servizi di Office 365.</span><span class="sxs-lookup"><span data-stu-id="2021b-168">Microsoft employees in the United States with access to Customer Data must follow the Microsoft Cloud Background Check process required by all Office 365 services.</span></span> <span data-ttu-id="2021b-169">Al di fuori degli Stati Uniti, il processo varia.</span><span class="sxs-lookup"><span data-stu-id="2021b-169">Outside of the United States, the process varies.</span></span> <span data-ttu-id="2021b-170">Ad esempio, il cloud Microsoft per la Germania utilizza un modello di approvazione del trustee dei dati, studiato per garantire che il trustee dei dati (società tedesca) e non Microsoft sia in grado di controllare l'accesso ai dati dei clienti.</span><span class="sxs-lookup"><span data-stu-id="2021b-170">For example, the Microsoft Cloud for Germany uses a Data Trustee approval model, designed to ensure that the Data Trustee (a German company), and not Microsoft, is in control of access to Customer Data.</span></span> <span data-ttu-id="2021b-171">Il cloud Microsoft in Germania viene recapitato dai data center in Germania e i centri operativi (OC) contenenti il personale tecnico del trustee dei dati sono anche in Germania.</span><span class="sxs-lookup"><span data-stu-id="2021b-171">The Microsoft Cloud in Germany is delivered from datacenters in Germany, and the Operations Centers (OC) containing the technical staff of the Data Trustee are also in Germany.</span></span> <span data-ttu-id="2021b-172">Sia il datacenter sia le strutture OC sono gestite, gestite e controllate dal trustee dei dati.</span><span class="sxs-lookup"><span data-stu-id="2021b-172">Both the datacenter and the OC facilities are operated, maintained and controlled by the Data Trustee.</span></span>

<span data-ttu-id="2021b-173">Nella tabella seguente sono elencati i controlli eseguiti come parte del controllo dei precedenti del cloud di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2021b-173">The following table lists the checks that are performed as part of the Microsoft Cloud Background Check.</span></span>

| <span data-ttu-id="2021b-174">Screening</span><span class="sxs-lookup"><span data-stu-id="2021b-174">Screening</span></span> | <span data-ttu-id="2021b-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2021b-175">Description</span></span> |
|--------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2021b-176">Ricerca del numero di previdenza sociale</span><span class="sxs-lookup"><span data-stu-id="2021b-176">Social Security Number Search</span></span> | <span data-ttu-id="2021b-177">Verifica che il numero di previdenza sociale fornito sia valido.</span><span class="sxs-lookup"><span data-stu-id="2021b-177">Verifies that the provided Social Security number is valid.</span></span> |
| <span data-ttu-id="2021b-178">Controllo di precedenti penali</span><span class="sxs-lookup"><span data-stu-id="2021b-178">Criminal History Check</span></span> | <span data-ttu-id="2021b-179">I record penali di sette anni controllano reati di reato e reato allo stato, alla contea e ai livelli locali e, a seconda dei casi, a livello federale.</span><span class="sxs-lookup"><span data-stu-id="2021b-179">Seven-year criminal records check for felony and misdemeanor offenses at the state, county, and local levels, and as appropriate, at the federal level.</span></span> |
| <span data-ttu-id="2021b-180">Elenco di controllo delle risorse esterne di Office</span><span class="sxs-lookup"><span data-stu-id="2021b-180">Office of Foreign Assets Control List</span></span> | <span data-ttu-id="2021b-181">Dipartimento del Tesoro elenco di persone e organizzazioni con cui non è consentito ai cittadini degli Stati Uniti e ai residenti permanenti di svolgere attività commerciali.</span><span class="sxs-lookup"><span data-stu-id="2021b-181">Department of Treasury list of individuals and organizations with whom United States citizens and permanent residents are not allowed to do business.</span></span> |
| <span data-ttu-id="2021b-182">Bureau of Industry and Security List</span><span class="sxs-lookup"><span data-stu-id="2021b-182">Bureau of Industry and Security List</span></span> | <span data-ttu-id="2021b-183">Elenco del dipartimento di commercio delle persone e degli enti esclusi dall'attività di esportazione.</span><span class="sxs-lookup"><span data-stu-id="2021b-183">Department of Commerce list of individuals and entities barred from engaging in export activities.</span></span> |
| <span data-ttu-id="2021b-184">Office of Defense Trade Controls Debarred Persons List (*Aggiunta il 1 ° luglio 2010*)</span><span class="sxs-lookup"><span data-stu-id="2021b-184">Office of Defense Trade Controls Debarred Persons List (*added on July 1, 2010*)</span></span> | <span data-ttu-id="2021b-185">Dipartimento di stato elenco delle persone e degli enti esclusi dall'impegno nelle attività di esportazione relative al settore della difesa.</span><span class="sxs-lookup"><span data-stu-id="2021b-185">Department of State list of individuals and entities barred from engaging in export activities related to the Defense industry.</span></span> |

<span data-ttu-id="2021b-186">I risultati del controllo dei precedenti cloud di Microsoft sono archiviati nel database dei dipendenti e sono connessi ai sistemi di controllo di accesso di datacenter.</span><span class="sxs-lookup"><span data-stu-id="2021b-186">The results from the Microsoft Cloud Background Check are stored in our employee database and connected to our datacenter access control systems.</span></span> <span data-ttu-id="2021b-187">Se il controllo dei precedenti cloud di Microsoft scade e il dipendente non lo rinnova, l'accesso ai servizi di Office 365 è revocato e non è più disponibile finché non è stato completato il controllo dei precedenti di Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="2021b-187">If the Microsoft Cloud Background Check expires and the employee does not renew it, access to Office 365 services is revoked and no longer available until the Microsoft Cloud Background Check is completed.</span></span> <span data-ttu-id="2021b-188">Quando la relazione di lavoro con Microsoft termina, l'accesso a tutti i datacenter è immediatamente revocato.</span><span class="sxs-lookup"><span data-stu-id="2021b-188">When the employment relationship with Microsoft ends, all datacenter access is immediately revoked.</span></span>

<span data-ttu-id="2021b-189">La cittadinanza degli Stati Uniti è verificata per tutti i dipendenti con accesso fisico o logico ai servizi governativi di Office 365 United States.</span><span class="sxs-lookup"><span data-stu-id="2021b-189">United States citizenship is verified for all employees with physical or logical access to the Office 365 United States Government services.</span></span> <span data-ttu-id="2021b-190">Per verificare la cittadinanza, i dipendenti e/o i nuovi candidati a noleggio si incontrano con un delegato di cittadinanza statunitense che è addestrato a esaminare la documentazione per verificare la cittadinanza statunitense.</span><span class="sxs-lookup"><span data-stu-id="2021b-190">To verify citizenship, employees and/or new hire candidates meet with a U.S. Citizenship Delegate who is trained to review documentation verifying U.S. citizenship.</span></span> <span data-ttu-id="2021b-191">I dipendenti o i nuovi candidati a noleggio devono portare la documentazione richiesta e firmare un modulo di attestazione durante una riunione con il delegato di cittadinanza per la propria area geografica.</span><span class="sxs-lookup"><span data-stu-id="2021b-191">Employees or new hire candidates must bring the required documentation and sign an attestation form at a meeting with the Citizenship Delegate for their region.</span></span> <span data-ttu-id="2021b-192">La riunione deve essere svolta personalmente.</span><span class="sxs-lookup"><span data-stu-id="2021b-192">The meeting must be done in person.</span></span> <span data-ttu-id="2021b-193">Una volta che l'individuo ha incontrato il delegato di cittadinanza e ha fornito la documentazione e le firme necessarie, la cittadinanza delega inoltra una copia dei documenti a Microsoft Staffing Operations che invia la copia per la conservazione dei record.</span><span class="sxs-lookup"><span data-stu-id="2021b-193">Once the individual has met with the Citizenship Delegate and provided the necessary documentation and signatures, the Citizenship Delegate forwards a copy of the documents to Microsoft Staffing Operations who submit the copy to record keeping.</span></span>

<span data-ttu-id="2021b-194">Il personale con accesso logico al cloud del governo degli Stati Uniti di Office 365, o l'accesso logico o fisico alle offerte del governo degli Stati Uniti di Azure, è tenuto a conformarsi ai requisiti del governo federale delle [informazioni sulla giustizia penale dell'FBI Services](https://www.fbi.gov/services/cjis) (CJIS), inclusa la selezione del personale.</span><span class="sxs-lookup"><span data-stu-id="2021b-194">Personnel with logical access to the Office 365 U.S. Government Community Cloud, or logical or physical access to the Azure U.S. government offerings, are required to comply with federal government requirements of the FBI's [Criminal Justice Information Services](https://www.fbi.gov/services/cjis) (CJIS), including personnel screening.</span></span> <span data-ttu-id="2021b-195">Lo screening di CJIS a sostegno del servizio governativo degli Stati Uniti di Office 365 include un controllo dei precedenti penali basato sull'impronta digitale, aggiudicato dal giudice dell'agenzia di sistema CJIS negli [Stati che si sono iscritti](https://blogs.office.com/2013/10/23/california-and-microsoft-sign-cjis-security-policy-agreement/) ai servizi Microsoft Online CJIS programma di supporto.</span><span class="sxs-lookup"><span data-stu-id="2021b-195">CJIS screening in support of the Office 365 U.S. Government service includes a fingerprint-based criminal background check adjudicated by the CJIS system agency designated adjudicator in [states that have enrolled](https://blogs.office.com/2013/10/23/california-and-microsoft-sign-cjis-security-policy-agreement/) in the Microsoft Online Services CJIS support program.</span></span>