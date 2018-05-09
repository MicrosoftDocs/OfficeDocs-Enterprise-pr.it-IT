---
title: Gestire i gruppi del sito SharePoint Online con Office 365 PowerShell
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 05/01/2018
ms.audience: Admin
ms.topic: hub-page
ms.service: o365-administration
localization_priority: Normal
ms.collection: Ent_O365
ms.custom:
- PowerShell
- Ent_Office_Other
ms.assetid: d0d3877a-831f-4744-96b0-d8167f06cca2
description: 'Riepilogo: Utilizzare Office 365 PowerShell per gestire i gruppi del sito SharePoint Online.'
ms.openlocfilehash: 881e67b7eb2d8bb5e04f83e28569aa54341d16b9
ms.sourcegitcommit: 5c5489db5d1000296945c9774198bd911bee4f14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2018
---
# <a name="manage-sharepoint-online-site-groups-with-office-365-powershell"></a>Gestire i gruppi del sito SharePoint Online con Office 365 PowerShell

 **Riepilogo:** Utilizzare Office 365 PowerShell per gestire i gruppi del sito SharePoint Online.
  
Sebbene sia possibile utilizzare l'interfaccia di amministrazione di Office 365, è inoltre possibile utilizzare Office 365 PowerShell per gestire i gruppi del sito di SharePoint Online.

## <a name="before-you-begin"></a>Prima di iniziare

Le procedure descritte in questo articolo è necessario per la connessione a SharePoint Online. Per ulteriori informazioni, vedere [connettersi a PowerShell per SharePoint Online](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps).

## <a name="view-sharepoint-online-with-office-365-powershell"></a>Visualizzazione SharePoint Online con Office 365 PowerShell

Interfaccia di amministrazione di SharePoint Online include alcuni metodi da utilizzare per la gestione dei gruppi del sito. Ad esempio, si supponga che si desidera esaminare i gruppi e i membri del gruppo, per il protocollo https\://litwareinc.sharepoint.com/sites/finance sito. Ecco che cosa è necessario effettuare per:

1. Dall'interfaccia di amministrazione di Office 365, fare clic su **risorse** > di**siti**e quindi fare clic sull'URL del sito.
2. Nella finestra di dialogo raccolta siti, fare clic su **Vai a questo sito**.
3. Nella pagina sito fare clic sull'icona **Impostazioni** (si trova nell'angolo superiore destro della pagina) e quindi fare clic su **Impostazioni sito**:</br>
![Impostazioni del sito di SharePoint Online](images/spo-site-settings.png)</br>
4. Nella pagina Impostazioni sito fare clic su **autorizzazioni di siti** in **utenti e autorizzazioni**.

Ripetere quindi la procedura per il sito successivo.

Per ottenere un elenco dei gruppi con Office 365 PowerShell, utilizzare il set di comandi seguenti:

```
$siteURL = "https://litwareinc.sharepoint.com/sites/finance"
$x = Get-SPOSiteGroup -Site $siteURL
foreach ($y in $x)
    {
        Write-Host $y.Title -ForegroundColor "Yellow"
        Get-SPOSiteGroup -Site $siteURL -Group $y.Title | Select-Object -ExpandProperty Users
        Write-Host
    }
```

Esistono due modi per eseguire questo comando impostato nel prompt dei comandi di SharePoint Online Management Shell:

- Copiare i comandi nel blocco note (o un altro editor di testo), modificare il valore della variabile **$siteURL** , selezionare i comandi e quindi incollarle al prompt dei comandi di SharePoint Online Management Shell. In questo caso, PowerShell verrà interrotta in una **>>** prompt dei comandi. Premere INVIO per eseguire il comando **foreach** .</br>
- Copiare i comandi nel blocco note (o un altro editor di testo), modificare il valore della variabile **$siteURL** e quindi salvare il file di testo con un nome e l'estensione ps1 in una cartella appropriata. Successivamente, eseguire lo script dal prompt dei comandi di SharePoint Online Management Shell specificando il percorso e nome file. Ecco un comando di esempio:

```
C:\Scripts\SiteGroupsAndUsers.ps1
```

In entrambi i casi, verrà visualizzato qualcosa di simile alla seguente:

![Gruppi di siti di SharePoint Online](images/SPO-site-groups.png)

Si tratta di tutti i gruppi che sono stati creati per i siti https\:/ / litwareinc.sharepoint.com/sites/finance, nonché tutti gli utenti assegnati a tali gruppi. I nomi dei gruppi sono di colore giallo che consentono di nomi di gruppi separati dai relativi membri.

Come ulteriore esempio, di seguito è un set di comandi in cui sono elencati i gruppi e tutte le appartenenze a gruppi, per tutti i siti di SharePoint Online.

```
$x = Get-SPOSite
foreach ($y in $x)
    {
        Write-Host $y.Url -ForegroundColor "Yellow"
        $z = Get-SPOSiteGroup -Site $y.Url
        foreach ($a in $z)
            {
                 $b = Get-SPOSiteGroup -Site $y.Url -Group $a.Title 
                 Write-Host $b.Title -ForegroundColor "Cyan"
                 $b | Select-Object -ExpandProperty Users
                 Write-Host
            }
    }
```
    
## <a name="see-also"></a>Vedere anche

[Connettersi a PowerShell per SharePoint Online](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps)

[Creare siti di SharePoint Online e aggiungere utenti a Office 365 PowerShell](create-sharepoint-sites-and-add-users-with-powershell.md)

[Gestire gli utenti e i gruppi di SharePoint Online con PowerShell di Office 365](manage-sharepoint-users-and-groups-with-powershell.md)

[Gestire Office 365 con PowerShell di Office 365](manage-office-365-with-office-365-powershell.md)
  
[Guida introduttiva a PowerShell di Office 365](getting-started-with-office-365-powershell.md)
