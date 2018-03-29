---
title: Emulatore della riga di comando
ms.topic: article
ms.prod: xamarin
ms.assetid: E592AA32-5E83-B7E5-1753-12416551B23C
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/09/2018
ms.openlocfilehash: 01ae4e1477ff5a05a5690ef24ed266b73f862748
ms.sourcegitcommit: 0fdb243b46cf21be47584900805cadcd077121bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2018
---
# <a name="command-line-emulator"></a>Emulatore della riga di comando


## <a name="running-the-android-emulator-from-the-command-line"></a>Esecuzione dell'emulatore Android dalla scheda riga di comando

Per abilitare l'esecuzione dell'emulatore Android dalla riga di comando, è possibile usare lo strumento "emulatore" disponibile in Android SDK. Questo strumento può essere usato per eseguire l'emulatore dal terminale in OS X o dal prompt dei comandi in un computer Windows.

Per avviare uno specifico emulatore Android, eseguire il comando seguente dalla directory tools nella posizione di Android SDK (ad esempio, C:\android-sdk-windows\tools):

In Windows

```cmd
emulator.exe -avd NameOfYourEmulator -partition-size 512
```

In macOS

```bash
./emulator -avd NameOfYourEmulator -partition-size 512
```

Le dimensioni della partizione sono necessarie per consentire all'emulatore di avere spazio sufficiente per l'installazione della piattaforma Xamarin.Android nell'emulatore perché, per impostazione predefinita, l'emulatore è di piccole dimensioni.

Per altre informazioni sui parametri aggiuntivi, vedere il sito Android all'indirizzo [http://developer.android.com/guide/developing/tools/emulator.html](http://developer.android.com/guide/developing/tools/emulator.html)