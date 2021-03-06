---
title: Associazione di librerie di iOS
description: Questo documento descrive come creare le associazioni c# per il codice Objective-C, rendendo possibile l'uso delle librerie native e CocoaPods in un'applicazione xamarin. IOS.
ms.prod: xamarin
ms.assetid: EBDC50DC-B44B-4003-AB2B-1EEB868A5E01
ms.technology: xamarin-ios
ms.custom: xamu-video
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/18/2017
ms.openlocfilehash: 75c8f9a2eea080c3da031366b314d94929080811
ms.sourcegitcommit: ec50c626613f2f9af51a9f4a52781129bcbf3fcb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2018
ms.locfileid: "37855221"
---
# <a name="binding-ios-libraries"></a>Associazione di librerie di iOS

Seguire i collegamenti seguenti per informazioni sull'associazione di librerie Objective-C e CocoaPods per xamarin. IOS e xamarin. Mac:

- [**Cenni preliminari sulla** ](~/cross-platform/macios/binding/overview.md) -
  viene descritto il funzionamento dell'associazione.
- [**Associazione di librerie Objective-C** ](~/cross-platform/macios/binding/objective-c-libraries.md) -
  istruzioni su come associare le librerie Objective-C per l'uso nei progetti Xamarin.
- [**Guida di riferimento di definizione di tipo** ](~/cross-platform/macios/binding/binding-types-reference.md) -
  descrive tutti gli attributi disponibili per gli autori delle associazioni per guidare il processo di generazione dell'associazione.

## <a name="objective-sharpiecross-platformmaciosbindingobjective-sharpieindexmd"></a>[Objective Sharpie](~/cross-platform/macios/binding/objective-sharpie/index.md)

Obiettivo Sharpie è uno strumento da riga di comando per eseguire il bootstrap del primo passaggio di un'associazione.
Funziona analizzando i file di intestazione di una libreria nativa per eseguire il mapping dell'API pubblica nel [definizione di associazione](~/cross-platform/macios/binding/objective-c-libraries.md) (un processo che in caso contrario, viene eseguito manualmente). Obiettivo Sharpie non crea un'associazione di per sé, ma possa aiutarti a iniziare.

Obiettivo Sharpie 3.0 è stato introdotto la possibilità di associare direttamente Cocoapods.

## <a name="walkthrough---binding-an-ios-objective-c-librarywalkthroughmd"></a>[Procedura dettagliata: associazione di una libreria Objective-C iOS](walkthrough.md)

Questa pagina fornisce una procedura dettagliata di creazione di un progetto di binding iOS Usa open source [ **InfColorPicker** ](https://github.com/InfinitApps/InfColorPicker) progetto Objective-C come esempio. Il **InfColorPicker** libreria fornisce un controller di visualizzazione riutilizzabili che consentono all'utente di selezionare un colore di base nella relativa rappresentazione HSB, rendendo più semplice la selezione del colore.
Obiettivo Sharpie verrà utilizzato per semplificare il processo di associazione.

## <a name="xamarin-university-lightning-lecture"></a>Xamarin University Lightning Lecture

> [!VIDEO https://youtube.com/embed/ZUoPLcmnf1o]

**iOS associazioni in C/C++, da [Xamarin University](https://university.xamarin.com/)**

## <a name="related-links"></a>Collegamenti correlati

- [Binding di Objective-C](~/cross-platform/macios/binding/index.md)
- [Associazione di Mac](~/mac/platform/binding.md)
- [Corso di Xamarin University: Creazione di una libreria di binding di Objective-C](https://university.xamarin.com/classes/track/all#building-an-objective-c-bindings-library)
- [Corsi di Xamarin University: Compilare una libreria di binding Objective-C con Sharpie obiettivo](https://university.xamarin.com/classes/track/all#build-an-objective-c-bindings-library-with-objective-sharpie)