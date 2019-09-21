---
title: Ottimizzare le chiamate di pagina nelle pagine classiche e moderne del sito di pubblicazione di SharePoint Online
ms.author: kvice
author: kelleyvice-msft
manager: laurawi
ms.date: 9/18/2019
audience: ITPro
ms.topic: conceptual
ms.service: o365-administration
localization_priority: Priority
ms.collection:
- Ent_O365
- Strat_O365_Enterprise
ms.custom: Adm_O365
ms.reviewer: sstewart
search.appverid:
- MET150
description: Per informazioni su come ottimizzare le pagine classiche e moderne del sito di pubblicazione di SharePoint Online, è possibile limitare il numero di chiamate agli endpoint dei servizi di SharePoint Online.
ms.openlocfilehash: d44cb2273d550cea3a9ec7bfb1ffaeb10bbdd333
ms.sourcegitcommit: c7764503422922cb333b05d54e8ebbdb894df2f9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/18/2019
ms.locfileid: "37028203"
---
# <a name="optimize-page-calls-in-sharepoint-online-modern-and-classic-publishing-site-pages"></a><span data-ttu-id="73c29-103">Ottimizzare le chiamate di pagina nelle pagine classiche e moderne del sito di pubblicazione di SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="73c29-103">Optimize page calls in SharePoint Online modern and classic publishing site pages</span></span>

<span data-ttu-id="73c29-104">Sia i siti di pubblicazione moderni che quelli classici di SharePoint Online contengono collegamenti che caricano i dati dalle (o effettuano chiamate a) funzionalità di SharePoint e CDN.</span><span class="sxs-lookup"><span data-stu-id="73c29-104">Both SharePoint Online modern and classic publishing sites contain links that load data from (or make calls to) SharePoint features and CDNs.</span></span> <span data-ttu-id="73c29-105">Per altre chiamate effettuate da una pagina, il caricamento della pagina sarà più lungo.</span><span class="sxs-lookup"><span data-stu-id="73c29-105">The more calls made by a page, the longer the page takes to load.</span></span> <span data-ttu-id="73c29-106">Si tratta di una latenza percepita dagli utenti finali\*\* o **EUPL**.</span><span class="sxs-lookup"><span data-stu-id="73c29-106">This is known as **end user perceived latency** or **EUPL**.</span></span>

<span data-ttu-id="73c29-107">Questo articolo illustra come determinare il numero e l'impatto delle chiamate agli endpoint esterni nelle pagine moderne e classiche del sito di pubblicazione e su come limitarne l'effetto sulla latenza percepita dagli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="73c29-107">This article will help you understand how to determine the number and impact of calls to external endpoints from your modern and classic publishing site pages and how to limit their effect on end user perceived latency.</span></span>

>[!NOTE]
><span data-ttu-id="73c29-108">Per ulteriori informazioni sulle prestazioni nei portali moderni di SharePoint Online, vedere [ Prestazioni nell'esperienza moderna di SharePoint](https://docs.microsoft.com/it-IT/sharepoint/modern-experience-performance).</span><span class="sxs-lookup"><span data-stu-id="73c29-108">For more information about performance in SharePoint Online modern portals, see [Performance in the modern SharePoint experience](https://docs.microsoft.com/it-IT/sharepoint/modern-experience-performance).</span></span>

## <a name="use-the-page-diagnostics-for-sharepoint-tool-to-analyze-page-calls"></a><span data-ttu-id="73c29-109">Usare lo strumento Diagnostica pagine per SharePoint per analizzare le chiamate di pagine</span><span class="sxs-lookup"><span data-stu-id="73c29-109">Use the Page Diagnostics for SharePoint tool to analyze page calls</span></span>

<span data-ttu-id="73c29-110">Lo **strumento Diagnostica pagine per SharePoint** è un'estensione del browser per Chrome e per la [versione di Microsoft Edge 77 o versioni successive](https://www.microsoftedgeinsider.com/en-us/download?form=MI13E8&OCID=MI13E8), che consente di analizzare sia le pagine di pubblicazione moderne che quelle classiche di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="73c29-110">The **Page Diagnostics for SharePoint tool** is a browser extension for Chrome and [Microsoft Edge version 77 or later](https://www.microsoftedgeinsider.com/en-us/download?form=MI13E8&OCID=MI13E8) you can use to analyze SharePoint both modern and classic publishing site pages.</span></span> <span data-ttu-id="73c29-111">Lo strumento fornisce un report per ogni pagina analizzata che mostra le prestazioni della pagina rispetto a un set di criteri di prestazioni definito.</span><span class="sxs-lookup"><span data-stu-id="73c29-111">The tool provides a report for each analyzed page showing how the page performs against a defined set of performance criteria.</span></span> <span data-ttu-id="73c29-112">Per installare e conoscere lo strumento Diagnostica pagine per SharePoint, visitare [Usare lo strumento Diagnostica pagine per SharePoint Online](page-diagnostics-for-spo.md).</span><span class="sxs-lookup"><span data-stu-id="73c29-112">To install and learn about the Page Diagnostics for SharePoint tool, visit [Use the Page Diagnostics tool for SharePoint Online](page-diagnostics-for-spo.md).</span></span>

<span data-ttu-id="73c29-113">Quando si analizza una pagina del sito di SharePoint con lo strumento Diagnostica pagine per SharePoint, è possibile visualizzare le informazioni sulle chiamate esterne nel risultato **Richieste a SharePoint** nel riquadro _Test diagnostici_.</span><span class="sxs-lookup"><span data-stu-id="73c29-113">When you analyze a SharePoint site page with the Page Diagnostics for SharePoint tool, you can see information about external calls in the **Requests to SharePoint** result in the _Diagnostic tests_ pane.</span></span> <span data-ttu-id="73c29-114">La riga sarà verde se la pagina del sito contiene una quantità inferiore della linea di base di chiamate, mentre sarà rossa se la pagina supera il numero di linea di base.</span><span class="sxs-lookup"><span data-stu-id="73c29-114">The line will appear in green if the site page contains fewer than the baseline number of calls, and red if the page exceeds the baseline number.</span></span> <span data-ttu-id="73c29-115">Il numero della linea di base varia in base alle pagine moderne e classiche, perché le pagine classiche del sito usano HTTP1.1, mentre le moderne usano HTTP2.0:</span><span class="sxs-lookup"><span data-stu-id="73c29-115">The baseline number is different for modern and classic pages because classic site pages use HTTP1.1 and modern pages use HTTP2.0:</span></span>

- <span data-ttu-id="73c29-116">Le pagine moderne del sito non dovrebbero contenere più di **25** chiamate</span><span class="sxs-lookup"><span data-stu-id="73c29-116">Modern site pages should contain no more than **25** calls</span></span>
- <span data-ttu-id="73c29-117">Le pagine classiche del sito non dovrebbero contenere più di **6** chiamate</span><span class="sxs-lookup"><span data-stu-id="73c29-117">Classic publishing pages should contain no more than **6** calls</span></span>

<span data-ttu-id="73c29-118">I risultati possibili includono:</span><span class="sxs-lookup"><span data-stu-id="73c29-118">Possible results include:</span></span>

- <span data-ttu-id="73c29-119">**Attenzione richiesta** (rosso): la pagina supera il numero di linea di base di chiamate</span><span class="sxs-lookup"><span data-stu-id="73c29-119">**Attention required** (red): The page exceeds the baseline number of calls</span></span>
- <span data-ttu-id="73c29-120">**Nessuna azione richiesta** (verde): la pagina contiene una quantità inferiore di linea di base di chiamate</span><span class="sxs-lookup"><span data-stu-id="73c29-120">**No action required** (green): The page contains fewer than the baseline number of calls</span></span>

<span data-ttu-id="73c29-121">Se il risultato delle **Richieste a SharePoint** viene visualizzato nella sezione **Attenzione richiesta**, è possibile fare clic sul risultato per informazioni dettagliate, tra cui il numero totale di chiamate della pagina e un elenco degli URL.</span><span class="sxs-lookup"><span data-stu-id="73c29-121">If the **Requests to SharePoint** result appears in the **Attention required** section, you can click the result for details, including the total number of calls on the page and a list of the URLs.</span></span>

![Risultati delle Richieste a SharePoint](media/modern-portal-optimization/pagediag-requests.png)

## <a name="remediate-performance-issues-related-to-too-many-calls-on-a-page"></a><span data-ttu-id="73c29-123">Risolvere i problemi di prestazioni relativi a un numero eccessivo di chiamate in una pagina</span><span class="sxs-lookup"><span data-stu-id="73c29-123">Remediate performance issues related to too many calls on a page</span></span>

<span data-ttu-id="73c29-124">Se una pagina contiene troppe chiamate, è possibile usare l'elenco di URL nei risultati delle **Richieste a SharePoint** per determinare se esistono chiamate ripetute, chiamate che devono essere in batch o chiamate che restituiscono dati da memorizzare nella cache.</span><span class="sxs-lookup"><span data-stu-id="73c29-124">If a page contains too many calls, you can use the list of URLs in the **Requests to Sharepoint** results to determine whether there are any repeated calls, calls that should be batched, or calls that return data that should be cached.</span></span>

<span data-ttu-id="73c29-125">Le chiamate REST in batch\*\* consentono di ridurre il sovraccarico delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="73c29-125">**Batching REST calls** can help to reduce performance overhead.</span></span> <span data-ttu-id="73c29-126">Per altre informazioni sulle chiamate API in batch, vedere [Effettuare richieste di batch con le API REST](https://docs.microsoft.com/it-IT/sharepoint/dev/sp-add-ins/make-batch-requests-with-the-rest-apis).</span><span class="sxs-lookup"><span data-stu-id="73c29-126">For more information about API call batching, see [Make batch requests with the REST APIs](https://docs.microsoft.com/it-IT/sharepoint/dev/sp-add-ins/make-batch-requests-with-the-rest-apis).</span></span>

<span data-ttu-id="73c29-127">L'uso di una cache\*\* per archiviare i risultati di una chiamata API può migliorare le prestazioni di una richiesta importante, consentendo al client di usare i dati della cache, anziché eseguire un’altra chiamata per ogni caricamento di pagina successivo.</span><span class="sxs-lookup"><span data-stu-id="73c29-127">**Using a cache** to store the results of an API call can improve the performance of a warm request by allowing the client to use the cached data instead of making an additional call for each subsequent page load.</span></span> <span data-ttu-id="73c29-128">Ci sono diversi modi per affrontare questa soluzione in base ai requisiti aziendali.</span><span class="sxs-lookup"><span data-stu-id="73c29-128">There are multiple ways to approach this solution depending on the business requirement.</span></span> <span data-ttu-id="73c29-129">In genere, se i dati sono identici per tutti gli utenti, l'uso di un servizio di memorizzazione nella cache a livello intermedio, come la cache di[_ Azure Redis_](https://azure.microsoft.com/it-IT/services/cache/), è un'ottima opzione per ridurre significativamente il traffico API in un sito, perché gli utenti richiederebbero i dati del servizio di memorizzazione nella cache anziché direttamente da SPO.</span><span class="sxs-lookup"><span data-stu-id="73c29-129">Typically if the data will be the same for all users, using a middle-tier caching service like [_Azure Redis_ cache](https://azure.microsoft.com/it-IT/services/cache/) is a great option to significantly reduce API traffic against a site, as the users would request the data from the caching service instead of directly from SPO.</span></span> <span data-ttu-id="73c29-130">Le uniche chiamate SPO sono necessarie per aggiornare la cache del livello intermedio.</span><span class="sxs-lookup"><span data-stu-id="73c29-130">The only SPO calls needed would be to refresh the middle-tier's cache.</span></span> <span data-ttu-id="73c29-131">Se i dati variano in base ai singoli utenti, può essere preferibile implementare una cache lato client, ad esempio LocalStorage o anche un cookie.</span><span class="sxs-lookup"><span data-stu-id="73c29-131">If the data will fluctuate on an individual user basis, it may be best to implement a client side cache, like LocalStorage or even a Cookie.</span></span> <span data-ttu-id="73c29-132">Il volume delle chiamate continuerà a essere ridotto eliminando le successive richieste effettuate dallo stesso utente per la durata della cache, ma sarà meno efficiente di un servizio di caching dedicato.</span><span class="sxs-lookup"><span data-stu-id="73c29-132">This will still reduce call volumes by eliminating subsequent requests made by the same user for the cache duration, but will be less efficient than a dedicated caching service.</span></span> <span data-ttu-id="73c29-133">PnP consente di usare LocalStorage con un po’ di strumenti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="73c29-133">PnP allows you to use LocalStorage with little additional development required.</span></span>

<span data-ttu-id="73c29-134">Prima di eseguire le revisioni delle pagine per correggere i problemi di prestazioni, prendere nota del tempo di caricamento delle pagine nei risultati dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="73c29-134">Before you make page revisions to remediate performance issues, make a note of the page load time in the analysis results.</span></span> <span data-ttu-id="73c29-135">Eseguire di nuovo lo strumento dopo la revisione per verificare se il nuovo risultato ora rientra nei parametri di riferimento e controllare il tempo di caricamento della nuova pagina per verificare se è migliorato.</span><span class="sxs-lookup"><span data-stu-id="73c29-135">Run the tool again after your revision to see if the new result is within the baseline standard, and check the new page load time to see if there was an improvement.</span></span>

![Risultati del tempo di caricamento delle pagine](media/modern-portal-optimization/pagediag-page-load-time.png)

>[!NOTE]
><span data-ttu-id="73c29-137">Il tempo di caricamento delle pagine può variare in base a un'ampia varietà di fattori, ad esempio il carico di rete, l'ora del giorno e altre condizioni transitorie.</span><span class="sxs-lookup"><span data-stu-id="73c29-137">Page load time can vary based on a variety of factors such as network load, time of day, and other transient conditions.</span></span> <span data-ttu-id="73c29-138">È consigliabile verificare il tempo di caricamento delle pagine alcune volte prima e dopo aver apportato modifiche per ottenere la media dei risultati.</span><span class="sxs-lookup"><span data-stu-id="73c29-138">You should test page load time a few times before and after making changes to help you average the results.</span></span>

## <a name="related-topics"></a><span data-ttu-id="73c29-139">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="73c29-139">Related topics</span></span>

[<span data-ttu-id="73c29-140">Ottimizzare le prestazioni di SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="73c29-140">Tune SharePoint Online performance</span></span>](tune-sharepoint-online-performance.md)

[<span data-ttu-id="73c29-141">Ottimizzare le prestazioni di Office 365</span><span class="sxs-lookup"><span data-stu-id="73c29-141">Tune Office 365 performance</span></span>](tune-office-365-performance.md)

[<span data-ttu-id="73c29-142">Prestazioni nell'esperienza moderna di SharePoint</span><span class="sxs-lookup"><span data-stu-id="73c29-142">Performance in the modern SharePoint experience</span></span>](https://docs.microsoft.com/it-IT/sharepoint/modern-experience-performance.md)

[<span data-ttu-id="73c29-143">Reti per la distribuzione di contenuti</span><span class="sxs-lookup"><span data-stu-id="73c29-143">Content delivery networks</span></span>](content-delivery-networks.md)

[<span data-ttu-id="73c29-144">Usare la rete per la distribuzione di contenuti di Office 365 con SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="73c29-144">Use the Office 365 Content Delivery Network (CDN) with SharePoint Online</span></span>](use-office-365-cdn-with-spo.md)