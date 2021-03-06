---
title: Testo in xamarin. Forms
description: Xamarin. Forms offre tre visualizzazioni principali per l'utilizzo di testo e questo articolo spiega come usarli per immettere e visualizzare il testo nelle applicazioni di xamarin. Forms.
ms.prod: xamarin
ms.assetid: 4DBA7689-E5C8-4583-8FB4-02AB208B4416
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/22/2017
ms.openlocfilehash: c5bd157299c9388b561f316e65f2ba290bd15224
ms.sourcegitcommit: 66682dd8e93c0e4f5dee69f32b5fc5a96443e307
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2018
ms.locfileid: "35244987"
---
# <a name="text-in-xamarinforms"></a>Testo in xamarin. Forms

_Con xamarin. Forms consente di immettere o visualizzare il testo._

Xamarin. Forms presenta tre visualizzazioni principali per l'utilizzo di testo:

- **[Etichetta](#Label)**  &mdash; per la presentazione di testo singolo o multilinea. Può visualizzare il testo con più opzioni di formattazione nella stessa riga.
- **[Voce](#Entry)**  &mdash; per l'immissione di testo che rappresenta solo una riga. Voce dispone di una modalità di password.
- **[Editor](#Editor)**  &mdash; per l'immissione di testo che potrebbe richiedere più di una riga.

Aspetto del testo può essere modificato utilizzando incorporato o personalizzato [stili](#Styles) e alcuni controlli supportano personalizzato [tipi di carattere](#Fonts).

<a name="Label" />

## <a name="labellabelmd"></a>[Etichetta](label.md)

Il `Label` vista viene usata per visualizzare il testo. Consente di visualizzare più righe di testo o una singola riga di testo. `Label` può presentare un testo con più opzioni di formattazione utilizzati in linea. La visualizzazione dell'etichetta possa eseguire il wrapping o il troncamento di testo quando non rientrano in una sola riga.

![](images/label.png "Esempio di etichetta")

Vedere il [etichetta](label.md) articolo per informazioni più dettagliate.

Per informazioni sulla personalizzazione di tipo di carattere utilizzato in un'etichetta, vedere [tipi di carattere](fonts.md).

<a name="Entry" />

## <a name="entryentrymd"></a>[Entry](entry.md)

`Entry` è possibile accettare l'input di testo a riga singola. `Entry` offre controllano sui colori, ma non sono stato personalizzato dei tipi di carattere. `Entry` Consente di visualizzare il testo segnaposto fino a quando non viene immesso il testo ha una modalità di password.

![](images/entry.png "Esempio di voce")

Vedere il [voce](entry.md) per ulteriori informazioni.

Si noti che, a differenza di `Label`, `Entry` non può avere impostazioni del tipo di carattere personalizzato.

<a name="Editor" />

## <a name="editoreditormd"></a>[Editor](editor.md)

`Editor` è possibile accettare l'input di testo multilinea. `Editor` può avere un colore di sfondo personalizzato, ma il colore del testo e tipo di carattere non può essere modificato.

![](images/editor.png "Esempio di editor")

Vedere il [Editor](editor.md) per ulteriori informazioni.

<a name="Fonts" />

## <a name="fontsfontsmd"></a>[Tipi di carattere](fonts.md)

Il `Label` controllo supporta le impostazioni di diverso tipo di carattere utilizzando i tipi di carattere incorporati in ogni piattaforma o tipi di carattere personalizzati inclusi con l'app. Vedere il [caratteri](fonts.md) articolo per informazioni più dettagliate.

<a name="Styles" />

## <a name="stylesstylesmd"></a>[Stili](styles.md)

Fare riferimento a [utilizzo degli stili](~/xamarin-forms/user-interface/styles/index.md) per informazioni su come impostare il tipo di carattere, [colore](~/xamarin-forms/user-interface/colors.md)e altre proprietà di visualizzazione che si applicano a più controlli.



## <a name="related-links"></a>Collegamenti correlati

- [Testo (esempio)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Text)
