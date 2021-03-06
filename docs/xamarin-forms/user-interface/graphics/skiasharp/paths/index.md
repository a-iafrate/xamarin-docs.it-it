---
title: I percorsi e le linee di SkiaSharp
description: Questo articolo illustra come usare SkiaSharp per tracciare linee e i percorsi di grafica nelle applicazioni xamarin. Forms e questo concetto è illustrato con esempio di codice.
ms.prod: xamarin
ms.assetid: 316A15FE-383D-4D06-8641-BAC7EE7474CA
ms.technology: xamarin-skiasharp
author: charlespetzold
ms.author: chape
ms.date: 03/10/2017
ms.openlocfilehash: 9febfabb7b44b1ec09abda4b352691b37565cb48
ms.sourcegitcommit: 12d48cdf99f0d916536d562e137d0e840d818fa1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2018
ms.locfileid: "39615135"
---
# <a name="skiasharp-lines-and-paths"></a>I percorsi e le linee di SkiaSharp

_Consente di disegnare linee e grafici percorsi SkiaSharp_

Il [sezione precedente](~/xamarin-forms/user-interface/graphics/skiasharp/basics/index.md) dimostrato che di SkiaSharp `SKCanvas` classe include diversi metodi per disegnare rettangoli, ellissi e rettangoli con angoli arrotondati. Questa sezione e nelle sezioni successive illustrano le varie classi connesse con la creazione e il rendering *percorsi di oggetti graphics*.

Il percorso della grafica è l'approccio più generalizzato per disegnando linee e curve di SkiaSharp. In questa sezione viene illustrato l'uso un `SKPath` oggetto per tracciare linee rette e usare una raccolta di linee rette piccola (chiamato un' *polilinea*) per tracciare le curve che è possibile definire matematicamente. Una sezione successiva verrà vengono illustrati i vari tipi di curve supportati da `SKPath`.

Tutti i programmi di esempio in questa sezione appaiono sotto l'intestazione **linee e tracciati** nella home page del [ **SkiaSharpFormsDemos** ](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/) programma e nel [ **Tracciati** ](https://github.com/xamarin/xamarin-forms-samples/tree/master/SkiaSharpForms/Demos/Demos/SkiaSharpFormsDemos/Paths) cartella della soluzione.

## <a name="lines-and-stroke-capslinesmd"></a>[Linee ed estremità dei tratti](lines.md)

Informazioni su come usare SkiaSharp per disegnare linee con estremità dei tratti diversi.

## <a name="path-basicspathsmd"></a>[Nozioni di base sui tracciati](paths.md)

Esplorare l'oggetto di SkiaSharp SKPath per la combinazione di linee e curve.

## <a name="the-path-fill-typesfill-typesmd"></a>[Tipi di riempimento dei tracciati](fill-types.md)

Scopri i diversi effetti possibili con i tipi di riempimento di SkiaSharp percorso.

## <a name="polylines-and-parametric-equationspolylinesmd"></a>[Polilinee ed equazioni parametriche](polylines.md)

Consente di eseguire il rendering di qualsiasi riga che è possibile definire con equazioni parametriche SkiaSharp.

## <a name="dots-and-dashesdotsmd"></a>[Punti e trattini](dots.md)

Master le complicazioni del disegno di linee con tratteggiate o in SkiaSharp.

## <a name="finger-paintingfinger-paintmd"></a>[Disegno con le dita](finger-paint.md)

Usare le dita per disegnare nell'area di disegno.


## <a name="related-links"></a>Collegamenti correlati

- [API di SkiaSharp](https://developer.xamarin.com/api/root/SkiaSharp/)
- [SkiaSharpFormsDemos (esempio)](https://developer.xamarin.com/samples/xamarin-forms/SkiaSharpForms/Demos/)
