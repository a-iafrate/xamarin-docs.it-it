---
title: Stili
description: Utilizzando gli stili per personalizzare l'aspetto
ms.topic: article
ms.prod: xamarin
ms.assetid: 344A34AA-B19A-4765-BC8A-875D9A6B5EA8
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/17/2016
ms.openlocfilehash: 934948579e5f3fb19c7afe49f4e86a1ef255b77f
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2018
---
# <a name="styles"></a>Stili

## <a name="introductionintroductionmd"></a>[Introduzione](introduction.md)

Xamarin. Forms applicazioni spesso contengono più controlli che hanno un aspetto identico. Impostare l'aspetto di ogni singolo controllo può essere ricorrenti e soggetta a errori. Invece, gli stili possono essere creati che consentono di personalizzare l'aspetto del controllo da proprietà raggruppamento e le impostazioni disponibili sul tipo di controllo.

## <a name="explicit-stylesexplicitmd"></a>[Stili espliciti](explicit.md)

Un *esplicita* stile è quello che viene applicato in modo selettivo a controlli impostando i relativi [ `Style` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.Style/) proprietà.

## <a name="implicit-stylesimplicitmd"></a>[Stili impliciti](implicit.md)

Un *implicita* stile è utilizzato da tutti i controlli dello stesso [ `TargetType` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Style.TargetType/), senza la necessità di ciascun controllo per fare riferimento allo stile.

## <a name="global-stylesapplicationmd"></a>[Stili globali](application.md)

Gli stili possono essere resi disponibili a livello globale, aggiungerli all'applicazione [ `ResourceDictionary` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ResourceDictionary/). Ciò consente di evitare la duplicazione degli stili nelle pagine o controlli.

## <a name="style-inheritanceinheritancemd"></a>[Ereditarietà degli stili](inheritance.md)

Stili possono ereditare da altri stili per ridurre la duplicazione e consentire il riutilizzo.

## <a name="dynamic-stylesdynamicmd"></a>[Stili dinamici](dynamic.md)

Stili non rispondere alle modifiche di proprietà e rimangono invariati per tutta la durata di un'applicazione. Tuttavia, le applicazioni come rispondere alle modifiche di stile in modo dinamico in fase di esecuzione utilizzando le risorse dinamiche.

## <a name="device-stylesdevicemd"></a>[Stili di dispositivo](device.md)

Xamarin. Forms include sei *dinamica* stili, noti come *dispositivo* gli stili, il [ `Devices.Styles` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Device+Styles/) classe. Tutti i sei stili possono essere applicati a [ `Label` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Label/) solo istanze.