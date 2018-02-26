---
title: Cercare e trovare i dati personali
ms.author: bcarter
author: brendacarter
manager: laurawi
ms.date: 2/7/2018
ms.audience: ITPro
ms.topic: overview
ms.collection:
- Ent_O365
- Strat_O365_Enterprise
ms.service: o365-solutions
localization_priority: Priority
ms.custom:
- Strat_O365_Enterprise
- GDPR
ms.assetid: 
description: Informazioni su come cercare e trovare i dati personali dell'utente in Office 365.
ms.openlocfilehash: f19aed534fe2bb4154edc31f0d1b0c82afcc1f04
ms.sourcegitcommit: 07be28bd96826e61b893b9bacbf64ba936400229
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="search-for-and-find-personal-data"></a>Cercare e trovare i dati personali

I dati personali sono definiti in modo molto ampio nell'RGPD, come qualsiasi dato relativo a una persona fisica identificata o identificabile residente nell'Unione Europea.

Articolo 4 - Definizioni

> con "dati personali" si intende qualsiasi informazione relativa a una persona fisica identificata o identificabile ("soggetto dei dati"); una persona fisica identificabile è una persona che può essere identificata, direttamente o indirettamente, in particolare in riferimento a un identificatore come un nome, un numero di identificazione, dati sulla posizione, un identificatore online o a uno o più fattori specifici per l'identità fisica, psicologica, genetica, mentale, economica, culturale o sociale della persona fisica;

In questo articolo viene illustrato come trovare i dati personali archiviati in SharePoint Online e OneDrive for Business (che include i siti per tutti i gruppi di Office 365 e Microsoft Teams).

L'individuazione dei dati personali soggetti all'RGPD si basa sull'utilizzo di tipi di informazioni riservate in Office 365. Queste definiscono il modo in cui il processo automatico riconosce tipi di informazione specifici come i numeri di previdenza sociale e di carta di credito. Al momento, tali informazioni non possono essere usate per trovare i dati nelle cassette postali di Exchange inattive. Tuttavia, i tipi di informazioni riservate possono essere usate con criteri di prevenzione della perdita dei dati per trovare dati personali nella posta elettronica in transito.

Quindi, attualmente non è possibile usare Ricerca contenuto per trovare i dati personali archiviati nelle cassette postali di Exchange Online, ma è possibile utilizzare i tipi di informazioni riservate gestite per l'RGPD per trovare e proteggere le informazioni personali quando vengono inviate tramite posta elettronica.

## <a name="use-content-search-to-find-personal-data"></a>Usare Ricerca contenuto per trovare dati personali

Microsoft consiglia un approccio in tre fasi per la ricerca di dati personali dell'utente in Office 365. Il resto di questo argomento fornisce informazioni su ognuno di questi passaggi.

<table>
<thead>
<tr class="header">
<th align="left"><strong>Passaggio</strong></th>
<th align="left"><strong>Descrizione</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1. Ricerca per tipi di informazioni riservate</p></td>
<td align="left"><p>Iniziare utilizzando tipi di informazioni riservate per trovare dati personali. Creare una query di Ricerca contenuto per ogni tipo di informazione riservata. Eseguire la query e analizzare i risultati.</p>
Se necessario, è possibile aggiungere parametri alla query per ridurre i falsi positivi: <li>Numero istanze</li>
    <li>Intervallo di confidenza</li>
    <li>Altre proprietà o gli operatori per query più complesse</li>
<p>Se necessario, modificare un tipo di informazione riservata per migliorare l'accuratezza dell'organizzazione:</p>
<p><li>Regolare il livello di probabilità direttamente nel file XML.</li></p>
<p><li>Aggiungere parole chiave.</li></p>
<p><li>Modificare i requisiti di prossimità delle parole chiave.</li></p></td>
</tr>
<tr class="even">
<td align="left"><p>2. Usare Keyword Query Language (KQL) per trovare ulteriori dati personali nell'ambiente</p></td>
<td align="left"><p>Per trovare i dati non inclusi nei tipi di informazioni riservate, usare il linguaggio di query KQL per lo sviluppo di query personalizzate.</p>
<p>Verificare i risultati di queste ricerche e modificare la stringa di query KQL fino a ottenere il risultato previsto.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3. Creare nuovi tipi di informazioni riservate personalizzati con le query KQL</p></td>
<td align="left">Dopo l'ottimizzazione delle query KQL per trovare i dati di destinazione, è possibile creare nuovi tipi di informazioni riservate personalizzati con queste query. Quindi, è possibile usare questi tipi di informazioni riservate personalizzati con Ricerca contenuto, nei criteri DLP e con altri strumenti e in altre query KQL.</td>
</tr>
</tbody>
</table>

A breve, sarà possibile creare e modificare i tipi di informazioni riservate in una nuova interfaccia utente in Centro sicurezza e conformità. Sarà possibile modificare in modo dinamico i risultati corrispondenti e ottimizzare i tipi di informazioni riservate in base alle proprie esigenze.

## <a name="search-for-sensitive-information-types-using-content-search"></a>Ricerca per tipi di informazioni riservate tramite Ricerca contenuto

Iniziare la ricerca dei dati personali utilizzando i tipi di informazioni riservate inclusi in Office 365. Sono elencati nel Centro sicurezza e conformità in Classificazione.

Questo argomento include un elenco dei tipi di informazioni riservate correnti che si applicano ai cittadini dell'Unione europea. Usarli come punto di partenza. Controllare spesso Centro sicurezza e conformità per le nuove aggiunte che semplificano la conformità RGPD.

Vedere anche l'articolo: [Elenco dei tipi di informazioni riservate e l'aspetto di ognuno di essi](https://support.office.com/it-IT/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b).

I tipi di informazioni riservate definiscono il modo in cui il processo automatico riconosce tipi di informazioni specifici come numeri di conto bancario, numeri di previdenza sociale e di carta di credito. I tipi di informazioni riservate sono definiti anche condizioni. Una tipologia di informazioni riservate viene definita da un modello identificato da un'espressione regolare o da una funzione. Inoltre, è possibile utilizzare elementi probatori, ad esempio, parole chiave e checksum per identificare una tipologia di informazioni riservate. In questa procedura di valutazione vengono usati anche il livello di probabilità e la prossimità.

In questo momento, tipi di informazioni riservate non sono utilizzabili per trovare i dati archiviati nelle cassette postali.

### <a name="using-content-search-with-sensitive-information-types"></a>Utilizzo di Ricerca contenuto per tipi di informazioni riservate

<table>
<thead>
<tr class="header">
<th align="left"><strong>Passaggio</strong></th>
<th align="left"><strong>Ulteriori informazioni</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd"><td align="left"><p>Andare a Ricerca contenuto nel Centro sicurezza e conformità</p></td>
<td align="left"><p>Nel riquadro a sinistra del Centro sicurezza e conformità, fare clic su **Ricerca e analisi** &gt; **Ricerca contenuto**.</p>
<p>Vedere <a href="https://support.office.com/en-us/article/Run-a-Content-Search-in-the-Office-365-Security-Compliance-Center-61852fd9-fe8a-4880-a339-cb19ed3bff4a">Eseguire Ricerca contenuto nel Centro sicurezza e conformità di Office 365</a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p>Creare un nuovo elemento di ricerca per ogni tipo di informazioni riservate</p></td>
<td align="left"><p>Utilizzare la sintassi seguente:</p>
<blockquote>
<p>SensitiveType:"&lt;type&gt;"</p>
</blockquote>
<p>Ad esempio:</p>
<blockquote>
<p>SensitiveType:&quot;Numero di passaporto francese&quot;</p>
</blockquote>
<p>Definire l'ambito di ricerca per SharePoint (include OneDrive for Business). Verificare che la sintassi sia esatta e non siano presenti spazi o errori di digitazione.</p>
<p>Vedere <a href="https://support.office.com/it-IT/article/Form-a-query-to-find-sensitive-data-stored-on-sites-3019fbc5-7f15-4972-8d0e-dc182dc7f836">Creare una query per individuare dati riservati memorizzati nei siti</a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Esaminare i risultati per ogni ricerca</p></td>
<td align="left"><p>Cercare i tipi di problemi per determinare se la precisione della query viene rispettata:</p>
<p><li>Molti falsi positivi</li></p>
<p><li>Istanze dei dati note mancanti</li></p>
<p>Vedere <a href="https://support.office.com/en-us/article/Export-Content-Search-results-from-the-Office-365-Security-Compliance-Center-ed48d448-3714-4c42-85f5-10f75f6a4278">Esportare i risultati di Ricerca contenuto dal Centro sicurezza e conformità di Office 365</a>.</p>
<p>Nota: se si utilizza Mozilla Firefox o Chrome, è necessario prima scaricare i report utilizzando Internet Explorer o Edge per installare il componente aggiuntivo necessario.</p></td>
</tr>
</tbody>
</table>

## <a name="sensitive-information-types-for-eu-citizen-data"></a>Tipi di informazioni riservate per i dati dei cittadini dell'Unione europea

Iniziare con questi tipi di informazioni riservate. Molti altri tipi di informazioni riservate sono in fase di rilascio per i dati personali nei paesi dell'Unione europea.

> Belgio - Numero nazionale
>
> Numero di carta di credito
>
> Numero di carta di identità della Croazia
>
> Numero di identificazione personale (OIB) - Croazia
>
> Numero carta d’identità (Repubblica Ceca)
>
> Codice PIN - Danimarca
>
> Unione Europea - Numero di carta di debito
>
> Finland National ID
>
> Finlandia - Numero di passaporto
>
> Francia - Numero della patente di guida
>
> Francia - Carta d'identità nazionale (CNI)
>
> Francia - Numero di passaporto
>
> Francia - Numero di previdenza sociale (INSEE)
>
> Germania - Numero della patente di guida
>
> Germania - Numero carta di identità
>
> Germania - Numero di passaporto
>
> Carta d'identità (Grecia)
>
> Numero di conto bancario internazionale (IBAN)
>
> Indirizzo IP
>
> Irlanda - Numero personale di servizio pubblico (PPS)
>
> Italia - Numero della patente di guida
>
> Paesi Bassi - Numero di servizio cittadino (BSN)
>
> Norvegia - Numero di identificazione
>
> Carta di identità - Polonia
>
> ID nazionale Polonia (PESEL)
>
> Passaporto Polonia
>
> Portogallo - Numero di carta del cittadino
>
> Spagna - Numero di previdenza sociale (SSN)
>
> Svezia - Identificativo nazionale
>
> Svezia - Numero di passaporto
>
> Regno Unito - Numero della patente di guida
>
> Regno Unito - Numero di iscrizione alle liste elettorali
>
> Regno Unito - Codice del servizio sanitario nazionale
>
> Regno Unito - Numero di assicurazione nazionale (NINO)
>
> Stati Uniti/Regno Unito - Numero di passaporto

## <a name="add-parameters-to-a-sensitive-information-type-query-to-hone-the-results"></a>Aggiungere parametri a una query di un tipo di informazione riservata per perfezionare i risultati

È possibile aggiungere i parametri a una query di un tipo di informazioni riservate:

-   Numero istanze - Consente di definire il numero di occorrenze di informazioni riservato che un documento deve contenere prima di essere incluso nei risultati della query.

-   Intervallo di confidenza - Consiste nel livello di confidenza con il quale il tipo di informazione riservata identificata rappresenta effettivamente una corrispondenza, ad esempio 85 (85%).

Sintassi:

-   SensitiveType:”\<type\>|\<count range\>|\<confidence range\>”

Esempi:

-   SensitiveType:“Credit Card Number|5” (restituisce soltanto i documenti che contengono esattamente cinque numeri di carta di credito)

-   SensitiveType:“Credit Card Number|\*|85..” (l'intervallo di confidenza è pari almeno all'85%)

Nota: "SensitiveType" distingue tra maiuscole e minuscole, il resto della query no.

È inoltre possibile usare le proprietà e gli operatori per illustrare il modo in cui è possibile perfezionare le query. Per ulteriori informazioni ed esempi, vedere [Creare una query per trovare i dati riservati archiviati nei siti](https://support.office.com/it-IT/article/Form-a-query-to-find-sensitive-data-stored-on-sites-3019fbc5-7f15-4972-8d0e-dc182dc7f836).