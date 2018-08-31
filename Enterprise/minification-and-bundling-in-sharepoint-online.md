---
title: Minimizzazione e creazione di bundle in SharePoint Online
ms.author: krowley
author: kccross
manager: laurawi
ms.date: 3/1/2017
ms.audience: Admin
ms.topic: troubleshooting
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom: Adm_O365
search.appverid: SPO160
ms.assetid: 87a52468-994e-43a2-b155-7229ed659291
description: In questo articolo viene descritto come utilizzare la riduzione e vendita abbinata tecniche con Web Essentials per ridurre il numero di richieste HTTP e ridurre il tempo che necessario per caricare le pagine di SharePoint Online.
ms.openlocfilehash: edc959e881b0f22b72fba64969e5984f30bce696
ms.sourcegitcommit: 69d60723e611f3c973a6d6779722aa9da77f647f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2018
ms.locfileid: "22541103"
---
# <a name="minification-and-bundling-in-sharepoint-online"></a><span data-ttu-id="17f02-103">Minimizzazione e creazione di bundle in SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="17f02-103">Minification and bundling in SharePoint Online</span></span>

<span data-ttu-id="17f02-104">In questo articolo viene descritto come utilizzare la riduzione e vendita abbinata tecniche con Web Essentials per ridurre il numero di richieste HTTP e ridurre il tempo che necessario per caricare le pagine di SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="17f02-104">This article describes how to use minification and bundling techniques with Web Essentials to reduce the number of HTTP requests and to reduce the time it takes to load pages in SharePoint Online.</span></span>
  
<span data-ttu-id="17f02-p101">Quando si personalizza il sito Web è possibile aggiungere un numero elevato di file aggiuntivi al server per supportare la personalizzazione. L'aggiunta di ulteriori immagini, CSS e JavaScript aumenta il numero di richieste HTTP al server che a sua volta aumenta il tempo necessario per visualizzare una pagina Web. Se si dispone di più file dello stesso tipo, è possibile creare dei bundle di questi file per accelerarne il download.</span><span class="sxs-lookup"><span data-stu-id="17f02-p101">When you customize your website you can end up adding a large number of extra files to the server to support the customization. Adding extra JavaScript, CSS, and images increases the number of HTTP requests to the server which in turn increases the time it takes to display a web page. If you have multiple files of the same type, you can bundle these files to make downloading these files faster.</span></span>
  
<span data-ttu-id="17f02-108">Per i file JavaScript e CSS, è inoltre possibile utilizzare un metodo chiamato riduzione, dove è ridurre le dimensioni totali dei file rimuovendo gli spazi vuoti e altri caratteri che non sono necessarie.</span><span class="sxs-lookup"><span data-stu-id="17f02-108">For JavaScript and CSS files, you can also use an approach called minification, where you reduce the total size of files by removing whitespace and other characters that aren't necessary.</span></span>
  
## <a name="minification-and-bundling-javascript-and-css-files-with-web-essentials"></a><span data-ttu-id="17f02-109">Minimizzazione e creazione di bundle di file JavaScript e CSS tramite Web Essentials</span><span class="sxs-lookup"><span data-stu-id="17f02-109">Minification and bundling JavaScript and CSS files with Web Essentials</span></span>

<span data-ttu-id="17f02-110">È possibile utilizzare software di terze parti, ad esempio Web Essentials, per raggruppare i file CSS e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="17f02-110">You can use third-party software such as Web Essentials to bundle CSS and JavaScript files.</span></span>
  
> [!IMPORTANT]
> <span data-ttu-id="17f02-p102">Web Essentials è un progetto di terze parti, open source, basate sulla community. Il software è un'estensione di Visual Studio 2012 e Visual Studio 2013 e non è supportato da Microsoft. Per scaricare Web Essentials, visitare il sito Web al [http://vswebessentials.com/download](https://go.microsoft.com/fwlink/p/?LinkId=525629).</span><span class="sxs-lookup"><span data-stu-id="17f02-p102">Web Essentials is a third-party, open-source, community-based project. The software is an extension to Visual Studio 2012 and Visual Studio 2013 and is not supported by Microsoft. To download Web Essentials, visit the website at [http://vswebessentials.com/download](https://go.microsoft.com/fwlink/p/?LinkId=525629).</span></span> 
  
<span data-ttu-id="17f02-114">Web Essentials offre due forme di creazione di bundle:</span><span class="sxs-lookup"><span data-stu-id="17f02-114">Web Essentials offers two forms of bundling:</span></span>
  
- <span data-ttu-id="17f02-115">.bundle: per i file CSS e JavaScript</span><span class="sxs-lookup"><span data-stu-id="17f02-115">.bundle: for CSS and JavaScript files</span></span>
    
- <span data-ttu-id="17f02-116">.sprite: per le immagini (disponibile solo in Visual Studio 2013)</span><span class="sxs-lookup"><span data-stu-id="17f02-116">.sprite: for images (only available in Visual Studio 2013)</span></span>
    
<span data-ttu-id="17f02-117">È possibile utilizzare Web Essentials se si dispone di una funzionalità esistente con alcuni elementi di personalizzazione cui viene fatto riferimento all'interno di una pagina master personalizzata, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="17f02-117">You can use Web Essentials if you have an existing feature with some branding elements that are referenced inside a custom master page, such as:</span></span>
  
![Schermata dell'elemento del marchio nella pagina master personalizzata](media/3a6eba36-973d-482b-8556-a9394b8ba19f.png)
  
 <span data-ttu-id="17f02-119">**Per creare un bundle TE000127218 e CSS in Web Essentials**</span><span class="sxs-lookup"><span data-stu-id="17f02-119">**To create a TE000127218 and CSS bundle in Web Essentials**</span></span>
  
1. <span data-ttu-id="17f02-120">In Visual Studio, in Esplora risorse selezionare i file che si desidera includere nel bundle.</span><span class="sxs-lookup"><span data-stu-id="17f02-120">In Visual Studio, in Solution Explorer, select the files that you want to include in the bundle.</span></span>
    
2. <span data-ttu-id="17f02-p103">Fare clic sui file selezionati e quindi selezionare **Web Essentials** \> **file bundle creare JavaScript** dal menu di scelta rapida. Per esempio:</span><span class="sxs-lookup"><span data-stu-id="17f02-p103">Right-click the selected files and then select **Web Essentials** \> **Create JavaScript bundle file** from the context menu. For example:</span></span> 
    
    ![Schermata che mostra le opzioni del menu di Web Essentials](media/41aac84c-4538-4f78-b454-46e651f868a3.png)
  
## <a name="viewing-the-results-of-bundling-javascript-and-css-files"></a><span data-ttu-id="17f02-124">Visualizzazione dei risultati della creazione di bundle di file JavaScript e CSS</span><span class="sxs-lookup"><span data-stu-id="17f02-124">Viewing the results of bundling JavaScript and CSS files</span></span>

<span data-ttu-id="17f02-125">Quando si crea un bundle di JavaScript e CSS, Web Essentials crea un file XML, denominato file recipe, che identifica i file JavaScript e CSS nonché altre informazioni sulla configurazione:</span><span class="sxs-lookup"><span data-stu-id="17f02-125">When you create a JavaScript and CSS bundle, Web Essentials creates an XML file called a recipe file that identifies the JavaScript and CSS files as well as some other configuration information:</span></span> 
  
![Schermata di file recipe JavaScript e CSS](media/7ba891f8-52d8-467b-a0f6-b062dd1137a4.png)
  
<span data-ttu-id="17f02-p104">Inoltre, se il flag minify è impostato su true nei file recipe aggregati, i file vengono ridimensionati e collegati tra loro. Ciò significa che le nuove versioni minimizzate dei file JavaScript sono state create ed è possibile farvi riferimento nella pagina master.</span><span class="sxs-lookup"><span data-stu-id="17f02-p104">In addition, if the minify flag is set to true in the bundling recipe the files are reduced in size as well as bundled together. This means that new, minified versions of the JavaScript files were created that you can reference in your master page.</span></span>
  
![Schermata del flag minify impostato su true](media/50523af2-6412-4117-ac3d-5bd26f6d562e.png)
  
<span data-ttu-id="17f02-130">Quando si carica una pagina dal sito Web, è possibile utilizzare gli strumenti di sviluppo dal browser, come Internet Explorer 11, per visualizzare il numero di richieste inviate al server e il tempo impiegato da ciascun file per il caricamento.</span><span class="sxs-lookup"><span data-stu-id="17f02-130">When you load a page from your web site, you can use the developer tools from your web browser, such as Internet Explorer 11, to see the number of requests sent to the server and how long each file took to load.</span></span>
  
<span data-ttu-id="17f02-131">La figura seguente mostra il risultato del caricamento di file JavaScript e CSS prima della minimizzazione.</span><span class="sxs-lookup"><span data-stu-id="17f02-131">The following figure is the result of loading the JavaScript and CSS files before minification.</span></span>
  
![Schermata che mostra il download di 80 elementi](media/e2df3912-1923-46e6-8cf2-3015a31554e1.png)
  
<span data-ttu-id="17f02-133">In seguito all'aggregazione dei file CSS e JavaScript, il numero di richieste viene interrotto a 74 e ogni file impiega un tempo leggermente più lungo dei file originali per ogni singolo download:</span><span class="sxs-lookup"><span data-stu-id="17f02-133">After bundling the CSS and JavaScript files together, the number of requests dropped to 74 and each file took only slightly longer than the original files to download individually:</span></span>
  
![Schermata che mostra il download di 74 elementi](media/686c4387-70e8-4a74-9d45-059f33a91184.png)
  
<span data-ttu-id="17f02-135">Dopo l'aggregazione, il file di bundle JavaScript viene ridotto in modo significativo da 815 KB a 365 KB:</span><span class="sxs-lookup"><span data-stu-id="17f02-135">After bundling, the JavaScript bundle file is reduced significantly from 815KB to 365KB:</span></span>
  
![Schermata che mostra dimensioni di download ridotte](media/5e7dbd98-faff-4f68-b320-108fb252e395.png)
  
## <a name="bundling-images-by-creating-an-image-sprite"></a><span data-ttu-id="17f02-137">Aggregazione di immagini tramite la creazione di un'immagine sprite</span><span class="sxs-lookup"><span data-stu-id="17f02-137">Bundling images by creating an image sprite</span></span>

<span data-ttu-id="17f02-p105">Analogamente a come si aggregano file JavaScript e CSS, è possibile combinare molte icone piccole e altre immagini comuni in un foglio sprite più grande e quindi utilizzare CSS per visualizzare le singole immagini. Invece di scaricare ogni immagine, web browser dell'utente scarica il foglio sprite una sola volta e quindi memorizza nella cache del computer locale. Consente di migliorare le prestazioni di caricamento delle pagine riducendo al numero di download e round trip al server web.</span><span class="sxs-lookup"><span data-stu-id="17f02-p105">Similar to how you bundle JavaScript and CSS files, you can combine many small icons and other common images into a larger sprite sheet and then use CSS to reveal the individual images. Instead of downloading each individual image, the user's web browser downloads the sprite sheet once and then caches it on the local computer. This improves page load performance by cutting down on the number of downloads and round trips to the web server.</span></span>
  
 <span data-ttu-id="17f02-141">**Per creare un'immagine sprite in Web Essentials**</span><span class="sxs-lookup"><span data-stu-id="17f02-141">**To create an image sprite in Web Essentials**</span></span>
  
1. <span data-ttu-id="17f02-142">In Visual Studio, in Esplora risorse selezionare i file che si desidera includere nel bundle.</span><span class="sxs-lookup"><span data-stu-id="17f02-142">In Visual Studio, in Solution Explorer, select the files that you want to include in the bundle.</span></span>
    
2. <span data-ttu-id="17f02-p106">Fare clic sui file selezionati e quindi selezionare **Web Essentials** \> **sprite immagine crea** dal menu di scelta rapida. Per esempio:</span><span class="sxs-lookup"><span data-stu-id="17f02-p106">Right-click the selected files and then select **Web Essentials** \> **Create image sprite** from the context menu. For example:</span></span> 
    
    ![Schermata che illustra come creare un'immagine sprite](media/de0fe741-4ef7-4e3b-bafa-ef9f4822dac6.png)
  
3. <span data-ttu-id="17f02-p107">Selezionare il percorso in cui salvare il file sprite. Il file .sprite è un file XML che descrive le impostazioni e i file nello sprite. Le figure seguenti mostrano un esempio di file PNG sprite e il file XML .sprite corrispondente.</span><span class="sxs-lookup"><span data-stu-id="17f02-p107">Choose a location to save the sprite file. The .sprite file is an XML file that describes the settings and files in the sprite. The following figures show an example of a sprite PNG file and its corresponding .sprite XML file.</span></span>
    
    ![Schermata di un file sprite](media/0876bb2a-d1b9-4169-8e95-9c290d628d90.png)
  
    ![Schermata del file XML sprite](media/d1f94776-280d-4d56-abb5-384f145d9989.png)
  
