---
title: Applicare le etichette ai dati personali in Office 365
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
description: Informazioni su come utilizzare le etichette di Office per il piano di protezione RGPD.
ms.openlocfilehash: be09afa8efa19d48d6bed2ad818adbcaf2aafcda
ms.sourcegitcommit: 07be28bd96826e61b893b9bacbf64ba936400229
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="apply-labels-to-personal-data-in-office-365"></a>Applicare le etichette ai dati personali in Office 365

 Utilizzare questo argomento se si utilizzano le etichette per il piano di protezione RGPD. Oggi è possibile creare le etichette nel Centro sicurezza e conformità di Office 365 e in Azure Information Protection. Nel corso del tempo queste tecnologie convergeranno in un'esperienza di classificazione e creazione delle etichette unificata e sarà possibile aggiungerne anche altre.

Se si utilizzano le etichette per la protezione dei dati personali in Office 365, Microsoft suggerisce di iniziare con le etichette di Office. È possibile utilizzare Advanced Data Governance per applicare automaticamente le etichette in base ai tipi di informazioni riservate o altri criteri. È possibile utilizzare le etichette di Office con la prevenzione della perdita di dati per applicare la protezione. È inoltre possibile usarle con eDiscovery e Ricerca contenuto. Presto sarà possibile usare le etichette e i tipi di informazioni riservate con Cloud App Security per monitorare i dati personali che si trovano in altre applicazioni SaaS.

Le etichette di Azure Information Protection al momento sono consigliate per l'applicazione di etichette ai file in locale e in altri servizi e provider cloud. Sono consigliate anche per i file in Office 365 che richiedono la crittografia di Azure Rights Management (Azure RMS) per la protezione dei dati, come file contenenti segreti commerciali.

Al momento, l'uso di Azure Information Protection per applicare la crittografia di Azure RMS non è consigliabile per i file in Office 365 contenti dati soggetti all'RGPD. I servizi di Office 365 attualmente non possono leggere i file crittografati con RMS. Di conseguenza, il servizio non può trovare i dati riservati in questi file.

Le etichette di Azure Information Protection possono essere applicate alla posta in Exchange Online e funzionano con la prevenzione della perdita di dati di Office 365. Presto, con il motore di classificazione e di creazione di etichette unificato, sarà possibile usare le stesse etichette per i messaggi di posta elettronica e i file, inclusa la creazione di etichette e la protezione della posta elettronica in transito.

![Le etichette di Office 365 e di Azure Information Protection](Media/Apply-labels-to-personal-data-in-Office-365-image1.png)

Nella figura:

-   Uso delle etichette di Office 365 per i dati personali per i file con segreti commerciali e altamente regolamentati in SharePoint Online e OneDrive for Business.

-   Utilizzare le etichette di Azure Information Protection (AIP) per i file con segreti commerciali e altamente regolamentati, la posta elettronica di Exchange Online, file in altri servizi SaaS, file in datacenter in locale e file in altri provider cloud.

-   A breve: entrambi i tipi di etichette convergeranno in un'unica esperienza di classificazione e creazione di etichette.

## <a name="use-office-labels-and-sensitive-information-types-across-microsoft-365-for-information-protection"></a>Usare le etichette di Office e i tipi di informazioni riservate in Microsoft 365 per la protezione delle informazioni

La figura seguente mostra il modo in cui le etichette di Office e i tipi di informazioni riservate possono essere utilizzati nei criteri delle etichette, nei criteri di prevenzione della perdita di dati e con i criteri di Cloud App Security.

![Etichette di Office e tipi di informazioni riservate](Media/Apply-labels-to-personal-data-in-Office-365-image2.png)

Ai fini dell'accessibilità, la seguente tabella fornisce le stesse informazioni dell'illustrazione.

<table>
<thead>
<tr class="header">
<th align="left"><strong>Elementi di classificazione</strong></th>
<th align="left"><strong>Criteri delle etichette - 2 esempi</strong></th>
<th align="left"><strong>Criteri di prevenzione della perdita dei dati - 2 esempi</strong></th>
<th align="left"><strong>I criteri di Cloud App Security per tutte le app SaaS - 1 esempio</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Etichette di Office. Esempi: Personale, Pubblico, Dati cliente, Dati risorse umano, Riservato, Estremamente riservato</td>
<td align="left"><p>Applicare automaticamente questa etichetta...</p>
<p>Dati del cliente</p>
<p>... ai documenti che corrispondono a questi tipi di informazioni riservate...</p>
<p>&lt;elenco dei tipi di informazioni riservate&gt;</p></td>
<td align="left"><p>Applicare la protezione...</p>
<p>&lt;definire la protezione&gt;</p>
<p>... ai documenti con questa etichetta...</p>
<p>Dati del cliente</p></td>
<td align="left"><p>Avvisa quando i file con questi attributi...</p>
<p>&lt;Attributo PII predefinito oppure espressione personalizzata&gt;</p>
<p>... in qualsiasi app SaaS approvata vengono condivisi all'esterno dell'organizzazione</p></td>
</tr>
<tr class="even">
<td align="left">Tipi di informazioni riservate. Esempi: Codice fiscale belga, numero di carta di credito, numero identità Croazia, codice fiscale Finlandese</td>
<td align="left"><p>Pubblicare le etichette per gli utenti da applicare manualmente...</p>
<p>&lt;selezionare etichette&gt;</p>
<p>... a questi percorsi...</p>
<p>&lt;tutte i percorsi oppure percorsi specifici&gt;</p></td>
<td align="left"><p>Applicare la protezione...</p>
<p>&lt;definire la protezione&gt;</p>
<p>... ai documenti che corrispondono a questi tipi di informazioni riservate&gt;</p></td>
<td align="left">Nota: gli attributi di Cloud App Security presto includeranno i tipi di informazioni riservate di Office 365 e le etichette unificate in Office 365 e Azure Information Protection.</td>
</tr>
</tbody>
</table>

## <a name="prioritize-auto-apply-label-policies"></a>Determinare la priorità per applicare automaticamente i criteri delle etichette

Per i dati personali soggetti all'RGPD, Microsoft consiglia di applicare automaticamente le etichette utilizzando i tipi di informazioni riservate creati per l'ambiente. È importante che i criteri applicati automaticamente siano ben progettati e testati per evitare problemi.

L'ordine con cui vengono creati i criteri da applicare automaticamente e il fatto che gli utenti applichino o meno queste etichette influisce sul risultato. È quindi importante pianificare attentamente l'implementazione. Ecco cosa serve sapere.

### <a name="one-label-at-a-time"></a>Un'etichetta alla volta

È possibile assegnare solo un'etichetta a un documento.

### <a name="older-auto-apply-policies-win"></a>I criteri da applicare automaticamente meno recenti vincono

Se sono presenti più regole che assegnano un'etichetta da applicare automaticamente e il contenuto soddisfa le condizioni di più regole, viene assegnata l'etichetta della regola meno recente. Per questo motivo, è importante pianificare con attenzione i criteri delle etichette prima di configurarli. Se un'organizzazione richiede una modifica alla priorità dei criteri delle etichette, questi dovranno essere eliminate e creati di nuovo.

### <a name="manual-user-applied-labels-trump-auto-applied-labels"></a>Le etichette applicate manualmente dall'utente battono quelle applicate automaticamente

Le etichette applicate manualmente dall'utente battono quelle applicate automaticamente. I criteri di applicazione automatica non possono sostituire un'etichetta già applicata da un utente. Gli utenti possono sostituire le etichette applicate automaticamente.

### <a name="auto-assigned-labels-can-be-updated"></a>Le etichette assegnate automaticamente possono essere aggiornate

Le etichette assegnate automaticamente possono essere aggiornate non nuovi criteri o aggiornando quelli esistenti.

Assicurarsi che il piano di implementazione delle etichette includa:

-   Assegnare la priorità nell'ordine con cui vengono creati i criteri applicati automaticamente.

-   Concedere il tempo sufficiente alle etichette per essere applicate automaticamente prima di implementarle affinché gli utenti le applichino manualmente. Potrebbero essere necessari fino a 7 giorni affinché le etichette vengano applicate in tutti i contenuti che corrispondono alle condizioni.

### <a name="example-priority-for-creating-the-auto-apply-policies"></a>Priorità di esempio per la creazione di criteri di applicazione automatica

<table>
<thead>
<tr class="header">
<th align="left"><strong>Etichette</strong></th>
<th align="left"><strong>Ordine di priorità per creare criteri da applicare automaticamente</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Risorse umane - Dati dipendenti</td>
<td align="left">1</td>
</tr>
<tr class="even">
<td align="left">Dati del cliente</td>
<td align="left">2</td>
</tr>
<tr class="odd">
<td align="left">Highly Confidential (Riservatezza elevata)</td>
<td align="left">3</td>
</tr>
<tr class="even">
<td align="left">Risorse umane - Dati sugli stipendi</td>
<td align="left">4</td>
</tr>
<tr class="odd">
<td align="left">Riservato</td>
<td align="left">5</td>
</tr>
<tr class="even">
<td align="left">Pubblico</td>
<td align="left">6</td>
</tr>
<tr class="odd">
<td align="left">Personale</td>
<td align="left">Nessun criterio di applicazione automatica</td>
</tr>
</tbody>
</table>

## <a name="create-labels-and-auto-apply-label-policies"></a>Creare le etichette i criteri delle etichette da applicare automaticamente

Creare le etichette e i criteri nel Centro sicurezza e conformità.

<table>
<thead>
<tr class="header">
<th align="left"><strong>Passaggio</strong></th>
<th align="left"><strong>Descrizione</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Assegnare autorizzazioni ai membri del team di conformità.</p></td>
<td align="left"><p>I membri del team di conformità che creeranno le etichette necessitano di autorizzazioni per utilizzare il Centro sicurezza e conformità. Andare a Autorizzazioni nel Centro sicurezza e conformità e modificare i membri del gruppo Amministratori di conformità.</p>
<p>Vedere <a href="https://support.office.com/en-ie/article/Give-users-access-to-the-Office-365-Security-Compliance-Center-2cfce2c8-20c5-47f9-afc4-24b059c1bd76">Fornire agli utenti l'accesso al Centro sicurezza e conformità di Office 365</a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p>Creare etichette di Office</p></td>
<td align="left">Andare a Classificazioni in Centro sicurezza e conformità, scegliere Etichette e creare etichette per il proprio ambiente.</td>
</tr>
<tr class="odd">
<td align="left"><p>Creare criteri di applicazione automatica per le etichette.</p></td>
<td align="left">Andare a Classificazione nel Centro sicurezza e conformità, scegliere Criteri etichette e creare i criteri di applicazione automatica delle etichette. Assicurarsi di creare questi criteri nell'ordine di priorità.</td>
</tr>
</tbody>
</table>

La figura seguente mostra come creare un'etichetta da applicare automaticamente per l'etichetta Dati del cliente.

![Creare e applicare un'etichetta per i dati del cliente](Media/Apply-labels-to-personal-data-in-Office-365-image3.png)

Nella figura:

-   Viene creata l'etichetta "Dati del cliente".

-   I tipi di informazioni riservate desiderate per l'RGPD sono: codice fiscale belga, numero di carta di credito, numero identità Croazia, codice fiscale Finlandese.

-   La creazione di un criterio di applicazione automatica assegna l'etichetta "Dati del cliente" a qualsiasi file che include uno dei tipi di informazioni riservate aggiunto al criterio.