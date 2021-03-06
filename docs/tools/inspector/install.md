---
title: Controllo installazione e requisiti
description: Questo documento viene descritto come installare il controllo di Xamarin e ne illustra il sistema operativo supportato, IDE e piattaforme di app.
ms.prod: xamarin
ms.assetid: 81174493-02D3-4FF5-AD57-04F3288A7F94
author: topgenorth
ms.author: toopge
ms.date: 06/19/2018
ms.openlocfilehash: 690329aa1577c66b3aa2794342a8e367477d3a74
ms.sourcegitcommit: 3f2737f8abf9b855edf060474aa222e973abda3f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37066923"
---
# <a name="inspector-installation-and-requirements"></a>Controllo installazione e requisiti

## <a name="download-and-installation"></a>Download e installazione

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

1. Scaricare e installare [Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/) e selezionare il **sviluppo per dispositivi Mobile con .NET** carico di lavoro.
1. [Accedi](https://docs.microsoft.com/visualstudio/ide/signing-in-to-visual-studio) per abilitare la sottoscrizione dell'organizzazione.
1. [Controllare](~/tools/inspector/inspect.md) la propria app.

# <a name="macostabmacos"></a>[macOS](#tab/macos)

1. Scaricare e installare [Visual Studio per Mac](https://visualstudio.microsoft.com/vs/mac/).
1. [Accedi](https://docs.microsoft.com/visualstudio/mac/activation) per abilitare la sottoscrizione dell'organizzazione.
1. [Controllare](~/tools/inspector/inspect.md) la propria app.

-----

## <a name="requirements"></a>Requisiti

### <a name="supported-operating-systems"></a>Supported Operating Systems

- **Mac** -OS X 10.11 o versione successiva
- **Windows** -Windows 7 o versione successiva (con Internet Explorer 11 o versione successiva e .NET 4.6.1 o versione successiva)

### <a name="supported-ides"></a>IDE supportati

- Visual Studio per Mac
- Visual Studio 2017 con **sviluppo per dispositivi Mobile con .NET** carico di lavoro

L'ispezione applicazione in tempo reale è disponibile per i clienti aziendali.

<a name="supported-platforms" />

### <a name="supported-app-platforms"></a>Piattaforme di App supportate

|App della piattaforma|Supporto IDE|Note|
|--- |--- |--- |
|Mac|Supportato solo in Visual Studio per Mac|
|iOS|Supportata in Visual Studio 2017 e Visual Studio per Mac| |
|Android|Supportata in Visual Studio 2017 e Visual Studio per Mac|Deve avere come destinazione Android > = 4.0.3, con **fastdev** abilitato.<br />È necessario usare gli emulatori di Google, Visual Studio o Xamarin Android. Emulatori Android 7 potrebbero non consentire il controllo in questo momento.|
|WPF|Supportato solo in Visual Studio 2017|

<a name="reporting-bugs" />

## <a name="reporting-bugs"></a>Segnalazione dei bug

I bug devono essere segnalati direttamente tramite Visual Studio:

- **Guida > Invia commenti e suggerimenti > segnala un problema**

Includere tutte le informazioni seguenti:

### <a name="platform-version-information"></a>Informazioni sulla versione della piattaforma

Queste informazioni sono fondamentali.

Visual Studio per Mac

- **Visual Studio > su Visual Studio > Mostra dettagli > Copia informazioni**
- Incollare in report di bug

Visual Studio

- **Guida > su Visual Studio > Copia informazioni**
- Inviare suggerimenti versione del sistema operativo e che sia in esecuzione Windows a 32 o 64 bit.

### <a name="log-files"></a>File di registro

Collegare sempre file di log client IDE e di controllo.

Client di controllo

- Mac: `~/Library/Logs/Xamarin/Inspector/Xamarin Inspector {date}.log`
- Windows: `%LOCALAPPDATA%\Xamarin\Inspector\logs\Xamarin Inspector {date}.log`

1.4.x offre inoltre la possibilità di selezionare il file di log in Finder (macOS) o Esplora risorse (Windows) direttamente dal menu principale:

- **Guida > Visualizza File di Log**

Visual Studio per Mac

- `~/Library/Logs/VisualStudio/7.0/Ide.log`

Visual Studio

- `%LOCALAPPDATA%\Xamarin\Logs\{VS version}\Inspector {date}.log`
- Il contenuto di Visual Studio **Output** riquadro può anche essere informativo.

### <a name="project-settings"></a>Impostazioni progetto

Se è possibile collegare il **csproj** per il progetto che si desidera controllare, sarebbe molto utile. Questo è più semplice rispetto a cui viene richiesto sulle singole impostazioni.

Anche confermare che sei in configurazione di Debug.

### <a name="selected-devices"></a>Dispositivi selezionati

Per Android e iOS, è essenziale che si sa quale periferica si esegue il debug quando si desidera controllare. È necessario conoscere:

- Nome del dispositivo come illustrato dell'IDE
- Versione del sistema operativo del dispositivo
- Android: Verificare che si sta utilizzando un x86 emulator
- Android: Quale piattaforma emulatore usi? Emulatore di Google? Emulatore Android di Visual Studio? Xamarin Android Player?
- L'app che si esegue il debug correttamente vengono visualizzati e funzione nel dispositivo?
- Il dispositivo dispone di connettività di rete (controllo tramite browser web)?

[client-bugs]: https://github.com/Microsoft/workbooks/issues/new
