---
title: Un'introduzione a SkiaSharp
description: Questo documento fornisce una breve introduzione ai concetti di SkiaSharp core. In particolare, illustra come ottenere e disegno in un' SKCanvas.
ms.prod: xamarin
ms.techonology: xamarin-skiasharp
ms.assetid: 19506F08-2603-465E-A806-6BD01638DE90
author: charlespetzold
ms.author: chape
ms.date: 09/14/2017
ms.openlocfilehash: eb4a391c52c598c6d276b75028337bf54455e7b4
ms.sourcegitcommit: 12d48cdf99f0d916536d562e137d0e840d818fa1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2018
ms.locfileid: "39615496"
---
# <a name="an-introduction-to-skiasharp"></a>Un'introduzione a SkiaSharp

_Ciò fornisce una breve introduzione ai concetti di SkiaSharp_

SkiaSharp fornisce una grafica 2D potente e ricco di API che può essere usata per eseguire il rendering nei buffer 2D.  È possibile utilizzare questi per implementare gli elementi dell'interfaccia utente personalizzata e grafica 2D che può essere incorporata nell'applicazione.  SkiaSharp è un'associazione di .NET per le [Skia](https://skia.org) libreria ed eredita le funzionalità di questa libreria.

La libreria è attualmente disponibile come multi-piattaforma [Mobileengagement](https://www.nuget.org/packages/SkiaSharp), è possibile aggiungere al progetto aggiungendo il riferimento di NuGet.

Per disegnare, il codice creerà un `SkCanvas` che descrive l'area in cui le operazioni di disegno verrà eseguita.

## <a name="obtaining-an-skcanvas"></a>Come ottenere un SKCanvas

```csharp
using (var surface = SKSurface.Create (width: 640, height: 480, SKImageInfo.PlatformColorType, SKAlphaType.Premul)) {
    SKCanvas myCanvas = surface.Canvas;

    // Your drawing code goes here.
}
```

## <a name="drawing-on-skcanvas"></a>Disegno su SKCanvas

Il `SKCanvas` Usa un modello di disegno simile come spirito al disegno altri modelli che è possibile avere familiarità con, Usa i colori con un canale di trasparenza facoltativi e possono tracciare linee, archi, testo e immagini.

Di seguito sono solo alcuni degli aspetti diversi possono essere eseguite con SkiaSharp.  Negli esempi seguenti la variabile `canvas` JE typu SKCanvas.

### <a name="drawing-xamagon"></a>Disegno Xamagon

In questo esempio consente di disegnare il logo di Xamarin il Xamagon:

```csharp
// clear the canvas / fill with white
canvas.Clear (SKColors.White);

// set up drawing tools
using (var paint = new SKPaint ()) {
  paint.IsAntialias = true;
  paint.Color = new SKColor (0x2c, 0x3e, 0x50);
  paint.StrokeCap = SKStrokeCap.Round;

  // create the Xamagon path
  using (var path = new SKPath ()) {
    path.MoveTo (71.4311121f, 56f);
    path.CubicTo (68.6763107f, 56.0058575f, 65.9796704f, 57.5737917f, 64.5928855f, 59.965729f);
    path.LineTo (43.0238921f, 97.5342563f);
    path.CubicTo (41.6587026f, 99.9325978f, 41.6587026f, 103.067402f, 43.0238921f, 105.465744f);
    path.LineTo (64.5928855f, 143.034271f);
    path.CubicTo (65.9798162f, 145.426228f, 68.6763107f, 146.994582f, 71.4311121f, 147f);
    path.LineTo (114.568946f, 147f);
    path.CubicTo (117.323748f, 146.994143f, 120.020241f, 145.426228f, 121.407172f, 143.034271f);
    path.LineTo (142.976161f, 105.465744f);
    path.CubicTo (144.34135f, 103.067402f, 144.341209f, 99.9325978f, 142.976161f, 97.5342563f);
    path.LineTo (121.407172f, 59.965729f);
    path.CubicTo (120.020241f, 57.5737917f, 117.323748f, 56.0054182f, 114.568946f, 56f);
    path.LineTo (71.4311121f, 56f);
    path.Close ();

    // draw the Xamagon path
    canvas.DrawPath (path, paint);
  }
}
```

### <a name="drawing-text"></a>Disegno di testo

```csharp
// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// set up drawing tools
using (var paint = new SKPaint ()) {
  paint.TextSize = 64.0f;
  paint.IsAntialias = true;
  paint.Color = new SKColor (0x42, 0x81, 0xA4);
  paint.IsStroke = false;

  // draw the text
  canvas.DrawText ("Skia", 0.0f, 64.0f, paint);
}
```

### <a name="drawing-bitmaps"></a>Disegno di bitmap

```csharp
Stream fileStream = File.OpenRead ("MyImage.png");

// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// decode the bitmap from the stream
using (var stream = new SKManagedStream(fileStream))
using (var bitmap = SKBitmap.Decode(stream))
using (var paint = new SKPaint()) {
  canvas.DrawBitmap(bitmap, SKRect.Create(Width, Height), paint);
}
```

### <a name="drawing-with-image-filters"></a>Disegno con filtri di immagini

```csharp
Stream fileStream = File.OpenRead ("MyImage.png"); // open a stream to an image file

// clear the canvas / fill with white
canvas.DrawColor (SKColors.White);

// decode the bitmap from the stream
using (var stream = new SKManagedStream(fileStream))
using (var bitmap = SKBitmap.Decode(stream))
using (var paint = new SKPaint()) {
  // create the image filter
  using (var filter = SKImageFilter.CreateBlur(5, 5)) {
    paint.ImageFilter = filter;

    // draw the bitmap through the filter
    canvas.DrawBitmap(bitmap, SKRect.Create(width, height), paint);
  }
}
```

## <a name="more-information"></a>Altre informazioni

Altre informazioni sull'uso di SkiaSharp sono reperibile nel [documentazione API online](https://developer.xamarin.com/api/namespace/SkiaSharp/)


## <a name="related-links"></a>Collegamenti correlati

- [Cartella di lavoro iOS SkiaSharp](https://developer.xamarin.com/workbooks/graphics/skiasharp/logo/skialogo-ios.workbook)
