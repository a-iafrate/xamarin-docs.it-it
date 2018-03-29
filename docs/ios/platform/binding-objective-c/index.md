---
title: Associazione iOS librerie
description: Come creare librerie native di iOS (e CocoaPods) accessibili in App Xamarin.
ms.topic: article
ms.prod: xamarin
ms.assetid: EBDC50DC-B44B-4003-AB2B-1EEB868A5E01
ms.technology: xamarin-ios
ms.custom: xamu-video
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/18/2017
ms.openlocfilehash: eb3edb007885d9fe839c2407a2581c9824e109c9
ms.sourcegitcommit: 0fdb243b46cf21be47584900805cadcd077121bf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2018
---
# <a name="binding-ios-libraries"></a>Associazione iOS librerie

_Come creare librerie native di iOS (e CocoaPods) accessibili in App Xamarin._

Vedere i collegamenti seguenti per informazioni sull'associazione di raccolte Objective-C e CocoaPods per xamarin. IOS e Xamarin.Mac:

- [**Panoramica** ](~/cross-platform/macios/binding/overview.md) -
  viene descritto il funzionamento dell'associazione.
- [**Associazione di raccolte Objective-C** ](~/cross-platform/macios/binding/objective-c-libraries.md) -
  istruzioni su come associare le raccolte di Objective-C per l'utilizzo nei progetti di Xamarin.
- [**Guida di riferimento di definizione di tipo** ](~/cross-platform/macios/binding/binding-types-reference.md) -
  descrive tutti gli attributi disponibili per gli autori delle associazioni per gestire il processo di generazione di associazione.

## <a name="objective-sharpiecross-platformmaciosbindingobjective-sharpieindexmd"></a>[Objective Sharpie](~/cross-platform/macios/binding/objective-sharpie/index.md)

Obiettivo Sharpie è uno strumento da riga di comando per avviare il primo passaggio di un'associazione.
Analizzando i file di intestazione di una libreria nativa per eseguire il mapping dell'API pubblica in cui funziona la [definizione di associazioni](~/cross-platform/macios/binding/objective-c-libraries.md) (un processo in caso contrario viene eseguito manualmente). Obiettivo Sharpie non crea un'associazione da sola, ma è possibile iniziare.

Obiettivo Sharpie 3.0 introdotta la possibilità di associare direttamente Cocoapods!

## <a name="walkthrough---binding-an-ios-objective-c-librarywalkthroughmd"></a>[Procedura dettagliata: associazione di una libreria Objective-C per iOS](walkthrough.md)

Questa pagina fornisce una procedura dettagliata Creazione di un progetto di associazione iOS usando open source [ **InfColorPicker** ](https://github.com/InfinitApps/InfColorPicker) progetto Objective-C come esempio. Il **InfColorPicker** libreria fornisce un controller di visualizzazione riutilizzabili che consentono all'utente di selezionare un colore di base nella relativa rappresentazione HSB, rendendo più semplice la selezione dei colori.
Obiettivo Sharpie verrà utilizzato per facilitare il processo di associazione.

## <a name="xamarin-university-lightning-lecture"></a>Lezione fulmine University Xamarin

> [!VIDEO https://youtube.com/embed/ZUoPLcmnf1o]

**iOS associazioni in C/C++, da [University Xamarin](https://university.xamarin.com/)**

## <a name="related-links"></a>Collegamenti correlati

- [Binding di Objective-C](~/cross-platform/macios/binding/index.md)
- [Associazione Mac](~/mac/platform/binding.md)