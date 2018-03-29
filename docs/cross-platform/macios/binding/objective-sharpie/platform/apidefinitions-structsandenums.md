---
title: ApiDefinitions & file StructsAndEnums
ms.topic: article
ms.prod: xamarin
ms.assetid: AC2087C0-BA54-46D8-B70C-6972941C8F73
ms.technology: xamarin-cross-platform
author: asb3993
ms.author: amburns
ms.date: 03/29/2017
ms.openlocfilehash: 0dedc6f574fbe2f2bf4ffaf4e70fb972670e9a8c
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2018
---
# <a name="apidefinitions--structsandenums-files"></a>ApiDefinitions & file StructsAndEnums

Quando l'obiettivo Sharpie è stata eseguita correttamente, viene generato `Binding/ApiDefinitions.cs` e `Binding/StructsAndEnums.cs` file.
Questi due file vengono aggiunti a un progetto di associazione in Visual Studio per Mac o passati direttamente al `btouch` o `bmac` strumenti per produrre l'associazione finale.

In *alcuni* casi potrebbero essere sufficiente, i file generati ma più spesso lo sviluppatore sarà necessario modificare manualmente questi generati i file per risolvere i problemi che non possono essere gestiti automaticamente dallo strumento (ad esempio con i flag con un [ `Verify` attributo](~/cross-platform/macios/binding/objective-sharpie/platform/verify.md)).

Alcuni dei passaggi successivi:

- **Modificare i nomi**: talvolta è necessario modificare i nomi di metodi e classi per la corrispondenza delle linee guida di progettazione di .NET Framework.
- **Metodi o proprietà**: approccio euristico utilizzato dall'obiettivo Sharpie talvolta sceglierà un metodo può essere trasformato in una proprietà. A questo punto, è possibile decidere se questo è il comportamento previsto o meno.
- **Associare gli eventi**: È possibile collegare le classi con classi di delegato e generare automaticamente gli eventi per tali.
- **Collegare le notifiche**: non è possibile estrarre il contratto dell'API di notifiche dai file di intestazione pure, sarà necessario un andata e ritorno per la documentazione dell'API. Se si desidera fortemente tipizzata delle notifiche, è necessario aggiornare il risultato.
- **Selezione di informazioni su API**: A questo punto, è possibile scegliere di costruttori aggiuntivi, aggiungere metodi (per consentire la sintassi c#-inizializzazione in costruzione), l'overload degli operatori e implementare interfacce personalizzate nel file di definizione aggiuntiva.

Vedere il [un'API di associazione](~/cross-platform/macios/binding/objective-c-libraries.md) descrizione per visualizzare il adattano di questi file nel processo di associazione, come illustrato nel diagramma seguente:

![](apidefinitions-structsandenums-images/binding-flowchart.png "In questo diagramma viene illustrato il processo di associazione")

Consultare la [riferimento ai tipi di associazione](~/cross-platform/macios/binding/binding-types-reference.md) per ulteriori informazioni sul contenuto di questi file.
