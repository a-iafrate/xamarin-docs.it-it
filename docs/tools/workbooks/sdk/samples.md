---
title: Integrazioni di esempio
ms.topic: article
ms.prod: xamarin
ms.assetid: 327DAD2E-1F76-4EB5-BCD0-9E7384D99E48
ms.technology: xamarin-cross-platform
author: topgenorth
ms.author: toopge
ms.openlocfilehash: f71da0f522c6c028981637a9797c3836063516f0
ms.sourcegitcommit: 30055c534d9caf5dffcfdeafd6f08e666fb870a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2018
---
# <a name="sample-integrations"></a>Integrazioni di esempio

## <a name="sample-integrations"></a>Integrazioni di esempio

Vedere il [cucina Sink] [ KitchenSink] per un esempio funzionante di un'integrazione. Semplicemente compilare `KitchenSink.sln` in Visual Studio per Mac o Visual Studio e quindi aprire `KitchenSink.workbook`.

[![Schermata di integrazione di cucina Sink](samples-images/kitchensinkintegrationscreenshot.png)](samples-images/kitchensinkintegrationscreenshot.png#lightbox)

L'esempio cucina Sink illustra entrambi i set di concetti:

* Le parti di rappresentazione viene illustrato come utilizzare `RepresentationManager` per migliorare il rendering con le rappresentazioni predefinite.
* Il `Person` oggetto e il renderer JavaScript associato illustrano l'utilizzo di `ISerializableObject` senza passare attraverso un provider di rappresentazione.

Vedere anche [SkiaSharp] [ skiasharp] per un esempio reale di un'integrazione che utilizzerà il [rappresentazioni](~/tools/workbooks/sdk/representations.md) fornito da cartelle di lavoro di Xamarin per eseguire il rendering nei relativi tipi.

[KitchenSink]: https://github.com/xamarin/Workbooks/tree/master/SDK/Samples/KitchenSink
[skiasharp]: https://github.com/mono/SkiaSharp/tree/master/source/SkiaSharp.Workbooks