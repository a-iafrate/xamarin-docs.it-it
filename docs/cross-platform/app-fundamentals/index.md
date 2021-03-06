---
title: Condivisione del codice su più piattaforme
description: Questo documento include collegamenti alle varie guide che descrivono le tecniche per la condivisione di codice, incluse le librerie di classi portabile, i progetti condivisi, .NET Standard e NuGet.
ms.prod: xamarin
ms.assetid: 7D179ACF-09A6-46EE-B49D-E27AB5F09CD4
author: conceptdev
ms.author: crdun
ms.date: 07/18/2018
ms.openlocfilehash: 3a2c3f98e3ba83db0794a68ff1d62a9845a111c0
ms.sourcegitcommit: 46bb04016d3c35d91ff434b38474e0cb8197961b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2018
ms.locfileid: "39270189"
---
# <a name="sharing-code-on-multiple-platforms"></a>Condivisione del codice su più piattaforme

Questi articoli illustrano le diverse opzioni disponibili per la condivisione di codice tra piattaforme, tra cui Windows, Android, iOS e altro ancora.

## <a name="code-sharing-overviewcode-sharingmd"></a>[Panoramica della condivisione di codice](code-sharing.md)

Scopri le diverso opzioni disponibili per i progetti Xamarin, incluse le librerie .NET Standard e progetti condivisi di condivisione del codice. Librerie di classi portabili sono supportate anche, tuttavia sono considerate deprecate a favore di .NET Standard.

## <a name="net-standardcross-platformapp-fundamentalsnet-standardmd"></a>[.NET Standard](~/cross-platform/app-fundamentals/net-standard.md)

.NET standard è l'opzione preferita per condividere codice tra piattaforme. Codice viene compilato con una versione specifica (2.0 fornisce il migliore compatibilità con le API con il codice di .NET Framework esistente) e possono quindi essere utilizzato da altri progetti che supportano tale livello o versione successiva. I progetti .NET standard sono supportati in Visual Studio 2017 e Visual Studio per Mac.

## <a name="shared-projectscross-platformapp-fundamentalsshared-projectsmd"></a>[Progetti condivisi](~/cross-platform/app-fundamentals/shared-projects.md)

Progetti condivisi consentono di scrivere codice comune a cui viene fatto riferimento da un numero di progetti di applicazione diversi. Il codice viene compilato come parte di ogni progetto di riferimento e può includere le direttive del compilatore per incorporare funzionalità specifiche della piattaforma di base di codice condiviso. Questo articolo illustra come creare e usarli con i progetti Xamarin e funzionamento dei progetti condivisi.

## <a name="portable-class-librariescross-platformapp-fundamentalspclmd"></a>[Librerie di classi portabili](~/cross-platform/app-fundamentals/pcl.md)

Progetti libreria di classi portabili consentono di compilare e distribuire gli assembly contenenti codice condiviso per l'esecuzione su più piattaforme. Per creare una libreria di classi portabile (o "Libreria di classi Portabile") prima di tutto selezionare quali piattaforme di destinazione, quindi scrivere codice in base a un sottoinsieme di .NET Framework che è disponibile nel profilo è definito per tali piattaforme. Librerie di classi portabili sono considerati a essere deprecata nelle versioni più recenti di Visual Studio. gli sviluppatori sono invitati a usare invece di .NET Standard 2.0.

## <a name="nuget-projects-multiplatform-libraries-for-code-sharingcross-platformapp-fundamentalsnuget-multiplatform-librariesindexmd"></a>[Progetti NuGet: librerie multipiattaforma per la condivisione del codice](~/cross-platform/app-fundamentals/nuget-multiplatform-libraries/index.md)

I pacchetti NuGet possono essere generati automaticamente da progetti libreria di classi Portabile o .NET standard. e i progetti condivisi possono essere inseriti in pacchetti NuGet "specchietto per le allodole" utilizzando il tipo di progetto NuGet separato. In questa sezione illustra come creare pacchetti NuGet per ogni scenario di condivisione del codice.

## <a name="manually-creating-nuget-packages-for-xamarincross-platformapp-fundamentalsnuget-manualmd"></a>[Creazione manuale di pacchetti NuGet per Xamarin](~/cross-platform/app-fundamentals/nuget-manual.md)

Suggerimenti per la creazione di pacchetti NuGet che funzionano con la piattaforma Xamarin.
