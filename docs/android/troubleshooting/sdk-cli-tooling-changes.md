---
title: Modifiche agli strumenti di Android SDK
description: Modifiche come Android SDK gestisce i livelli di API e i AVDs installati.
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 5AC61C00-0FF6-4C2D-80E7-D67A3EE30A5A
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 06/21/2018
ms.openlocfilehash: 4e808736fd92fa40ecbf0c24938c0fedd7afcff9
ms.sourcegitcommit: 26033c087f49873243751deded8037d2da701655
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2018
ms.locfileid: "36935451"
---
# <a name="changes-to-the-android-sdk-tooling"></a>Modifiche agli strumenti di Android SDK

_Modifiche come Android SDK gestisce i livelli di API e i AVDs installati._

## <a name="changes-to-android-sdk-tooling"></a>Modifiche per gli strumenti di Android SDK

Nelle versioni recenti degli strumenti di SDK per Android, Google ha rimosso i gestori di SDK e AVD esistenti a favore di nuovi strumenti CLI (interfaccia della riga di comando). Il **android** programma è stato rimosso e i gestori di Google GUI (interfaccia utente grafica) in Visual Studio per Mac e le versioni precedenti di Visual Studio Tools per Xamarin non funzionerà più dopo versione 25.2.5 di strumenti Android SDK. Ad esempio, il tentativo di utilizzare il **android** programma tramite la riga di comando comporterà un messaggio di errore simile al seguente:

```shell
The "android" command is deprecated.
For manual SDK, AVD, and project management, please use Android Studio.
For command-line tools, use tools\bin\sdkmanager.bat
and tools\bin\avdmanager.bat
```

Le sezioni seguenti illustrano come gestire il Android SDK e i dispositivi virtuali Android usando Android SDK 25.3.0 e versioni successive.

### <a name="ui-tools"></a>Strumenti dell'interfaccia utente

Visual Studio e Visual Studio per Mac forniscono ora Xamarin sostituzioni per i gestori di Google con interfaccia grafica non più utilizzate:

-   Per scaricare gli strumenti, piattaforme e altri componenti necessari per lo sviluppo di App xamarin Android SDK, usare il [Xamarin Android SDK Manager](~/android/get-started/installation/android-sdk.md) anziché legacy gestione SDK Google.

-   Per creare e configurare i dispositivi virtuali Android, usare il [gestione di dispositivi Android](~/android/get-started/installation/android-emulator/device-manager.md) anziché legacy Gestione emulatori Google.

Questi strumenti sono funzionalmente equivalenti al Google grafica responsabili sostituiscono.

### <a name="cli-tools"></a>Strumenti di CLI

In alternativa, è possibile utilizzare gli strumenti CLI per gestire e aggiornare le emulatori e Android SDK. Ora che i programmi seguenti costituiscono l'interfaccia della riga di comando per gli strumenti di Android SDK:

#### <a name="sdkmanager"></a>sdkmanager

**Aggiunto In:** strumenti Android SDK 25.2.3 (novembre 2016) e versioni successive.

È un nuovo programma chiamato **sdkmanager** nel **tools/bin** cartella del Android SDK. Questo strumento viene usato per mantenere il Android SDK dalla riga di comando. Per ulteriori informazioni sull'utilizzo di questo strumento, vedere [sdkmanager](https://developer.android.com/studio/command-line/sdkmanager.html).

#### <a name="avdmanager"></a>avdmanager

**Aggiunto In:** strumenti Android SDK 25.3.0 (marzo, 2017) e versioni successive.

È un nuovo programma chiamato **avdmanager** nel **tools/bin** cartella del Android SDK. Questo strumento viene usato per gestire il AVDs per l'emulatore Android. Per ulteriori informazioni sull'utilizzo di questo strumento, vedere [avdmanager](https://developer.android.com/studio/command-line/avdmanager.html).

### <a name="downgrading"></a>Downgrade

È possibile effettuare il downgrade del **strumenti Android SDK** installa una versione precedente di Android SDK da una versione di [sito Web Android Developer](https://developer.android.com/studio/index.html).

### <a name="using-the-old-gui"></a>Tramite la GUI precedente

È comunque possibile usare l'interfaccia utente grafica originale eseguendo il **android** programma all'interno del **strumenti** fino a quando si è nella cartella **strumenti Android SDK** versione **25.2.5**  o inferiore.


## <a name="related-links"></a>Collegamenti correlati

- [Installazione di Android SDK](~/android/get-started/installation/android-sdk.md)
- [Gestione di dispositivi Android](~/android/get-started/installation/android-emulator/device-manager.md)
- [Understanding Android API Levels](~/android/app-fundamentals/android-api-levels.md) (Informazioni sui livelli API Android)
- [Note sulla versione di SDK Tools (Google)](https://developer.android.com/studio/releases/sdk-tools.html)
- [sdkmanager](https://developer.android.com/studio/command-line/sdkmanager.html)
- [avdmanager](https://developer.android.com/studio/command-line/avdmanager.html)
