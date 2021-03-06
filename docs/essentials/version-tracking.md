---
title: 'Xamarin.Essentials: Rilevamento versione'
description: La classe VersionTracking in Xamarin.Essentials consente di controllare la versione delle applicazioni e i numeri di build e visualizzare informazioni aggiuntive tali come se fosse la prima ora l'applicazione avviata mai o per la versione corrente, ottengono la compilazione precedente informazioni e altro ancora.
ms.assetid: 670C7E8A-E882-4AC0-97D2-A53D90ADD6A3
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 81dc67fa5a4975f31d0fbf9f7219637596a827ce
ms.sourcegitcommit: 51c274f37369d8965b68ff587e1c2d9865f85da7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2018
ms.locfileid: "39353659"
---
# <a name="xamarinessentials-version-tracking"></a>Xamarin.Essentials: Rilevamento versione

![Versione non definitiva NuGet](~/media/shared/pre-release.png)

Il **VersionTracking** classe consente di controllare la versione delle applicazioni e i numeri di build e visualizzare informazioni aggiuntive tali come se fosse la prima ora l'applicazione avviata mai o per la versione corrente, ottengono il precedente le informazioni di compilazione e altro ancora.

## <a name="using-version-tracking"></a>Uso del rilevamento di versione

Aggiungere un riferimento a Xamarin.Essentials nella classe:

```csharp
using Xamarin.Essentials;
```

La prima volta che utilizza il **VersionTracking** classe verrà avviata la versione corrente di rilevamento. È necessario chiamare `Track` anticipata solo all'interno dell'applicazione ogni volta che viene caricato per assicurarsi che le informazioni sulla versione corrente viene tenuta traccia:

```csharp
VersionTracking.Track();
```

Dopo l'iniziale `Track` viene chiamato possono leggere le informazioni di versione:

```csharp

// First time ever launched application
var firstLaunch = VersionTracking.IsFirstLaunchEver;

// First time launching current version
var firstLaunchCurrent = VersionTracking.IsFirstLaunchForCurrentVersion;

// First time launching current build
var firstLaunchBuild = VersionTracking.IsFirstLaunchForCurrentBuild;

// Current app version (2.0.0)
var currentVersion = VersionTracking.CurrentVersion;

// Current build (2)
var currentBuild = VersionTracking.CurrentBuild;

// Previous app version (1.0.0)
var previousVersion = VersionTracking.PreviousVersion;

// Previous app build (1)
var previousBuild = VersionTracking.PreviousBuild;

// First version of app installed (1.0.0)
var firstVersion = VersionTracking.FirstInstalledVersion;

// First build of app installed (1)
var firstBuild = VersionTracking.FirstInstalledBuild;

// List of versions installed (1.0.0, 2.0.0)
var versionHistory = VersionTracking.VersionHistory;

// List of builds installed (1, 2)
var buildHistory = VersionTracking.BuildHistory;
```

## <a name="platform-implementation-specifics"></a>Funzionalità specifiche di implementazione della piattaforma

Tutte le informazioni sulla versione vengono archiviati utilizzando il [preferenze](preferences.md) API in Xamarin.Essentials e viene archiviato con il nome della **.xamarinessentials.versiontracking [YOUR-APP-PACKAGE-ID]** e segue lo stesso persistenza dei dati descritti nella [preferenze](preferences.md#persistence) documentazione.

## <a name="api"></a>API

- [Codice sorgente di rilevamento versione](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/VersionTracking)
- [Documentazione dell'API di rilevamento versione](xref:Xamarin.Essentials.VersionTracking)
