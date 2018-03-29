---
title: I driver USB necessario eseguire il debug di Android in Windows
ms.topic: article
ms.prod: xamarin
ms.assetid: 36EC7341-A2A4-409C-BD4F-330BAC505123
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 06/19/2017
ms.openlocfilehash: 97803c0496c7f5f6ea40e86023caad66c675037e
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2018
---
# <a name="what-usb-drivers-do-i-need-to-debug-android-on-windows"></a>I driver USB necessario eseguire il debug di Android in Windows

## <a name="finding-usb-drivers"></a>Come trovare i driver USB

Per eseguire il debug in un dispositivo Android quando si sviluppa in Windows. è necessario installare un driver USB compatibile. Android SDK Manager include il "Driver USB Google" per impostazione predefinita, che aggiunge il supporto per i dispositivi Nexus come descritto qui: [http://developer.android.com/sdk/win-usb.html](http://developer.android.com/sdk/win-usb.html)

I driver USB pubblicati appositamente dal produttore del dispositivo sono necessari altri dispositivi. Alcuni collegamenti per i produttori più comuni sono inclusi in questa guida: [http://developer.android.com/tools/extras/oem-usb.html](http://developer.android.com/tools/extras/oem-usb.html)

## <a name="alternatives"></a>Alternative

A seconda fabbricante, può essere difficile individuare i driver USB esatti Necessito. Sono disponibili alcune alternative per il test di App Android sviluppate in Windows inclusi usando un emulatore Android o verificare i servizi esterni. tra cui:

- [Xamarin Test Cloud](https://xamarin.com/test-cloud) - test eseguiti su centinaia di dispositivi Android reale i servizi Cloud.

- [Visual Studio Emulator for Android](https://www.visualstudio.com/en-us/features/msft-android-emulator-vs.aspx)

- [Emulatore Android di Google SDK](~/android/deploy-test/debugging/android-sdk-emulator/index.md)
