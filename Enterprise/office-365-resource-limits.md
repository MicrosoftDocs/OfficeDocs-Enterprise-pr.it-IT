---
title: Limiti relativi alle risorse di Office 365
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
description: "Riepilogo: informazioni sui limiti delle risorse per le diverse applicazioni all'interno di Office 365."
ms.openlocfilehash: ece25deece5a0f2eec7ab0295a2af68f47e1c50c
ms.sourcegitcommit: 55a046bdf49bf7c62ab74da73be1fd1cf6f0ad86
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/20/2019
ms.locfileid: "37067532"
---
# <a name="resource-limits"></a><span data-ttu-id="b5637-103">Limiti della risorsa</span><span class="sxs-lookup"><span data-stu-id="b5637-103">Resource Limits</span></span>

<span data-ttu-id="b5637-104">I limiti delle risorse vengono applicati utilizzando le quote (limiti) e la limitazione.</span><span class="sxs-lookup"><span data-stu-id="b5637-104">Resource limits are enforced using quotas (limits) and throttling.</span></span> <span data-ttu-id="b5637-105">Azure Active Directory e i singoli servizi di Office 365 utilizzano entrambi.</span><span class="sxs-lookup"><span data-stu-id="b5637-105">Azure Active Directory and the individual Office 365 services use both.</span></span> <span data-ttu-id="b5637-106">I limiti sono specifici del servizio e cambiano nel tempo man mano che vengono aggiunte nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b5637-106">Limits are service-specific and change over time as new capabilities are added.</span></span> <span data-ttu-id="b5637-107">Per informazioni dettagliate sui limiti correnti per i diversi servizi, vedere i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="b5637-107">For details on the current limits for the various services, see the following topics:</span></span>
- [<span data-ttu-id="b5637-108">Limiti e restrizioni dei servizi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5637-108">Azure Active Directory service limits and restrictions</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn764971.aspx)
- [<span data-ttu-id="b5637-109">Limiti di Exchange Online</span><span class="sxs-lookup"><span data-stu-id="b5637-109">Exchange Online Limits</span></span>](https://technet.microsoft.com/en-us/library/exchange-online-limits.aspx)
- [<span data-ttu-id="b5637-110">Limiti di Exchange Online Protection</span><span class="sxs-lookup"><span data-stu-id="b5637-110">Exchange Online Protection Limits</span></span>](https://technet.microsoft.com/en-us/library/exchange-online-protection-limits.aspx)
- [<span data-ttu-id="b5637-111">Confini e limiti del software di SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="b5637-111">SharePoint Online software boundaries and limits</span></span>](https://support.office.com/article/SharePoint-Online-software-boundaries-and-limits-8F34FF47-B749-408B-ABC0-B605E1F6D498)
- [<span data-ttu-id="b5637-112">Limiti relativi a Skype for business</span><span class="sxs-lookup"><span data-stu-id="b5637-112">Skype for Business Limits</span></span>](https://technet.microsoft.com/en-us/library/skype-for-business-online-limits.aspx)
- [<span data-ttu-id="b5637-113">API REST di Yammer e limiti di velocità</span><span class="sxs-lookup"><span data-stu-id="b5637-113">Yammer REST API and Rate Limits</span></span>](https://developer.yammer.com/docs/rest-api-rate-limits)
- [<span data-ttu-id="b5637-114">Limiti relativi alle dimensioni dei file in Sway</span><span class="sxs-lookup"><span data-stu-id="b5637-114">File Size Limits in Sway</span></span>](https://support.office.com/article/File-size-limits-in-Sway-4db21bc6-b42b-499f-9272-66e089db109f)

<span data-ttu-id="b5637-115">Oltre a questi limiti, vengono utilizzati diversi meccanismi di limitazione in Azure Active Directory e Office 365.</span><span class="sxs-lookup"><span data-stu-id="b5637-115">In addition to these limits, several throttling mechanisms are used throughout Azure Active Directory and Office 365.</span></span> <span data-ttu-id="b5637-116">La limitazione all'interno del servizio è particolarmente importante, dato che le risorse di rete nei datacenter di Microsoft sono ottimizzate per il vasto insieme di clienti che utilizzano i servizi.</span><span class="sxs-lookup"><span data-stu-id="b5637-116">Throttling within the service is especially important, given that network resources in Microsoft's datacenters are optimized for the broad set of customers that use the services.</span></span> <span data-ttu-id="b5637-117">I meccanismi di limitazione includono:</span><span class="sxs-lookup"><span data-stu-id="b5637-117">Throttling mechanisms include:</span></span>
- <span data-ttu-id="b5637-118">Azure Active Directory e Office 365 dispongono di limitazione a livello di utente, che limitano il numero di transazioni o di chiamate simultanee (tramite script o codice) che possono essere eseguite da un singolo utente.</span><span class="sxs-lookup"><span data-stu-id="b5637-118">Azure Active Directory and Office 365 feature user-level throttling, which limit the number of transactions or concurrent calls (by script or code) that can be performed by a single user.</span></span>
- <span data-ttu-id="b5637-119">Un criterio di limitazione predefinito di PowerShell viene assegnato a ogni tenant alla creazione del tenant.</span><span class="sxs-lookup"><span data-stu-id="b5637-119">A default PowerShell throttling policy is assigned to each tenant at tenant creation.</span></span> <span data-ttu-id="b5637-120">Queste impostazioni influiscono su altri elementi, ad esempio il numero massimo di sessioni di PowerShell simultanee che possono essere aperte da un singolo amministratore.</span><span class="sxs-lookup"><span data-stu-id="b5637-120">These settings affect other items, such as the maximum number of simultaneous PowerShell sessions that can be opened by a single administrator.</span></span>
- <span data-ttu-id="b5637-121">Ogni cliente di Exchange Online ha un criterio di servizi Web Exchange (EWS) predefinito che è stato ottimizzato per le operazioni client EWS e la limitazione che si applica a tutti i client Outlook.</span><span class="sxs-lookup"><span data-stu-id="b5637-121">Each Exchange Online customer has a default Exchange Web Services (EWS) policy that is tuned for EWS client operations, and throttling that applies to all Outlook clients.</span></span>