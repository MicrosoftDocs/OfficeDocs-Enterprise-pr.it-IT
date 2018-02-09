---
title: Test Lab Guide Configure un Exchange integrato, Lync e SharePoint laboratorio di testing
ms.author: jhendr
author: JoanneHendrickson
manager: laurawi
ms.date: 12/15/2017
ms.audience: ITPro
ms.topic: article
ms.collection: Ent_O365
ms.service: o365-solutions
localization_priority: Normal
ms.assetid: 48e16935-3429-456a-8fe6-50afa257924c
description: 'Riepilogo: Informazioni su come creare un laboratorio di testing integrato che include un server che esegue Exchange Server 2013, un server che esegue Lync Server 2013 e un server che esegue SharePoint Server 2013.'
ms.openlocfilehash: 4bc9c48782c7693368c304f5f9d5bae56242111d
ms.sourcegitcommit: d1a1480982c773f2241cb17f85072be8724ea841
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="test-lab-guide-configure-an-integrated-exchange-lync-and-sharepoint-test-lab"></a><span data-ttu-id="fdbaf-103">Guida del laboratorio di testing: Configurare un laboratorio di testing integrato di Exchange, Lync e SharePoint</span><span class="sxs-lookup"><span data-stu-id="fdbaf-103">Test Lab Guide: Configure an integrated Exchange, Lync, and SharePoint test lab</span></span>

 <span data-ttu-id="fdbaf-104">**Riepilogo:** Informazioni su come creare un laboratorio di testing integrato che include un server che esegue Exchange Server 2013, un server che esegue Lync Server 2013 e un server che esegue SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-104">**Summary:** Learn how to create an integrated test lab that contains a server that runs Exchange Server 2013, a server that runs Lync Server 2013, and a server that runs SharePoint Server 2013.</span></span>
  
<span data-ttu-id="fdbaf-105">Laboratorio di testing risultati da questa configurazione, che include l'autenticazione da server a server tra tutti i tre tipi di server, può essere utilizzato per preparare ed effettuare una dimostrazione multi-prodotto scenari e soluzioni che utilizzano un server che esegue Exchange Server 2013, un server che esegue Lync Server 2013 e un server che esegue SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-105">The test lab that results from this configuration, which includes server-to-server authentication between all three types of servers, can be used to build out and demonstrate multi-product scenarios and solutions that use a server that runs Exchange Server 2013, a server that runs Lync Server 2013, and a server that runs SharePoint Server 2013.</span></span>
  
<span data-ttu-id="fdbaf-106">Questo documento contiene istruzioni per le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fdbaf-106">This document contains instructions for the following:</span></span>
  
1. <span data-ttu-id="fdbaf-107">Configurazione del laboratorio di testing di configurazione di Base di Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-107">Configuring the Windows Server 2012 Base Configuration test lab.</span></span>
    
2. <span data-ttu-id="fdbaf-108">Installazione e configurazione di un nuovo server denominato SQL1.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-108">Installing and configuring a new server named SQL1.</span></span>
    
3. <span data-ttu-id="fdbaf-109">Installazione di SQL Server 2012 nel server SQL1.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-109">Installing SQL Server 2012 on the SQL1 server.</span></span>
    
4. <span data-ttu-id="fdbaf-110">Installazione e configurazione di un nuovo computer client denominato CLIENT2.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-110">Installing and configuring a new client computer named CLIENT2.</span></span>
    
5. <span data-ttu-id="fdbaf-111">Installazione e configurazione di Exchange Server 2013 in EX1.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-111">Installing and configuring Exchange Server 2013 on EX1.</span></span>
    
6. <span data-ttu-id="fdbaf-112">Installazione e configurazione di un nuovo server denominato LYNC1.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-112">Installing and configuring a new server named LYNC1.</span></span>
    
7. <span data-ttu-id="fdbaf-113">Installazione di Lync Server 2013 Standard Edition in LYNC1.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-113">Installing Lync Server 2013 Standard Edition on LYNC1.</span></span>
    
8. <span data-ttu-id="fdbaf-114">Installazione di SharePoint Server 2013 in SP1.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-114">Installing SharePoint Server 2013 on SP1.</span></span>
    
9. <span data-ttu-id="fdbaf-115">Configurazione dell'integrazione tra EX1, LYNC1 e SP1.</span><span class="sxs-lookup"><span data-stu-id="fdbaf-115">Configuring integration between EX1, LYNC1, and SP1.</span></span>
    
<span data-ttu-id="fdbaf-116">**Guardare la Exchange integrata, Lync e SharePoint video Cenni preliminari sulla Guida del laboratorio di testing**</span><span class="sxs-lookup"><span data-stu-id="fdbaf-116">**Watch the integrated Exchange, Lync, and SharePoint test lab guide overview video**</span></span>

![Icona video (pulsante riproduzione)](images/mod_icon_video_M.png)
  
<span data-ttu-id="fdbaf-118">Per informazioni su come configurare questo laboratorio di testing di Hyper-V, vedere [Hosting di Exchange integrata, SharePoint e Lync, ambiente di test con Windows Server 2012 Hyper-V](https://social.technet.microsoft.com/wiki/contents/articles/18483.hosting-the-integrated-exchange-lync-and-sharepoint-test-lab-with-windows-server-2012-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="fdbaf-118">For information about how to configure this test lab in Hyper-V, see [Hosting the integrated Exchange, Lync, and SharePoint test lab with Windows Server 2012 Hyper-V](https://social.technet.microsoft.com/wiki/contents/articles/18483.hosting-the-integrated-exchange-lync-and-sharepoint-test-lab-with-windows-server-2012-hyper-v.aspx).</span></span>
  
## <a name="download-the-test-lab-guide"></a><span data-ttu-id="fdbaf-119">Scaricare la guida del laboratorio di testing</span><span class="sxs-lookup"><span data-stu-id="fdbaf-119">Download the test lab guide</span></span>

<span data-ttu-id="fdbaf-120">[Guida del laboratorio di testing: configurare un Exchange integrata, Lync e laboratorio di testing di SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=313670) (https://go.microsoft.com/fwlink/p/?LinkId=313670)</span><span class="sxs-lookup"><span data-stu-id="fdbaf-120">[Test Lab Guide: Configure an Integrated Exchange, Lync, and SharePoint Test Lab](https://go.microsoft.com/fwlink/p/?LinkId=313670) (https://go.microsoft.com/fwlink/p/?LinkId=313670)</span></span>
  
## <a name="see-also"></a><span data-ttu-id="fdbaf-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fdbaf-121">See Also</span></span>

[<span data-ttu-id="fdbaf-122">Guide dei laboratori di testing</span><span class="sxs-lookup"><span data-stu-id="fdbaf-122">Test Lab Guides</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=202817)




