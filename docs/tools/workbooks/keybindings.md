---
title: Tasti di scelta rapida di Xamarin Workbooks Editor
description: Questo documento vengono descritti i tasti di scelta rapida disponibili per l'uso nell'editor di Xamarin Workbooks. In particolare, Cerca in vari modi, che viene usata la chiave Return.
ms.prod: xamarin
ms.assetid: 6375A371-3215-4A7C-B97B-A19E58BE96D6
author: topgenorth
ms.author: toopge
ms.date: 03/30/2017
ms.openlocfilehash: c2b4a8c1bcb8f7b88ab2ae1e2906b1c9c702b76a
ms.sourcegitcommit: aa9b9b203ab4cd6a6b4fd51e27d865e2abf582c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2018
ms.locfileid: "39351678"
---
# <a name="xamarin-workbooks-editor-keyboard-shortcuts"></a>Tasti di scelta rapida di Xamarin Workbooks Editor

## <a name="the-return-key-and-its-nuances"></a>La chiave di restituire e le sfumature

La tabella seguente descrive i vari tasti di scelta rapida per l'esecuzione del codice e la creazione di markdown. Sono state prese molta attenzione a scegliere ragionevole e coerenti con tasti di scelta rapida familiari e fluido.

|Tasto di scelta rapida|Cella di codice|Cella di markdown|
|--- |--- |--- |
|<kbd>Return</kbd>|<p>Se il cursore si trova alla fine del buffer di cella e la cella può essere analizzata correttamente, verrà eseguito e i risultati verranno visualizzati sotto il buffer e una nuova cella di codice verrà inserita e con stato attivo cella dopo la cella eseguita.</p><p>Se l'analisi non caso di esito positivo, una nuova riga verrà inserita nel buffer. Diagnostica del compilatore non sarà generata se l'analisi non è riuscita.</p>|<p><kbd>Restituire</kbd> presenta un comportamento diverso a seconda del contesto di Markdown nel punto di inserimento.</p><ul><li>Se il cursore si trova in un blocco di codice Markdown, viene inserita una nuova riga letterale.</li><li>Se il cursore si trova in un blocco di elenco di Markdown, creare un nuovo elemento elenco o dividere l'elemento dell'elenco corrente.</li><li>Se il punto di inserimento si trova in qualsiasi altro tipo di blocco di Markdown, creare un nuovo blocco paragrafo o suddividere il blocco corrente.</li></ul>|
|<dl><dt>Mac</dt><dd><kbd>Command‑Return</kbd></dd><dt>Win</dt><dd><kbd>Control‑Return</kbd></dd></dl>|<p>Tenta sempre di analizzare ed eseguire il contenuto della cella. Se la compilazione ha esito positivo, i risultati (incluse le eccezioni di esecuzione) verranno visualizzati sotto il buffer e, se non sono presenti celle successive, verrà creato e incentrato uno nuovo.</p><p>Se sono presenti errori di compilazione, verrà visualizzata la diagnostica e il buffer di continuare con la posizione del cursore non modificata.</p>|Inserisce e si concentra una nuova cella di codice dopo la cella corrente di markdown.|
|<dl><dt>Mac</dt><dd><kbd>Command‑Shift‑Return</kbd><dd><dt>Win</dt><dd><kbd>Control‑Shift‑Return</kbd></dd></dl>|Inserisce e si concentra una nuova cella di markdown dopo la cella corrente.|Stesso comportamento <kbd>restituire</kbd>|
|<kbd>Shift‑Return</kbd>|Inserisce sempre una nuova riga, indipendentemente dalla posizione del punto di inserimento o un contenuto.|Inserisce un'interruzione di riga rigido all'interno del blocco di Markdown corrente.|
