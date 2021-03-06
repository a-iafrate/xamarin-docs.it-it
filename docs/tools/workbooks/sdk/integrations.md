---
title: Negli argomenti di integrazione avanzata
description: Questo documento illustra argomenti avanzati relativi per le integrazioni per le cartelle di lavoro di Xamarin. Viene descritto il pacchetto Xamarin.Workbook.Integrations NuGet e l'esposizione di API all'interno di una cartella di lavoro di Xamarin.
ms.prod: xamarin
ms.assetid: 002CE0B1-96CC-4AD7-97B7-43B233EF57A6
author: topgenorth
ms.author: toopge
ms.date: 03/30/2017
ms.openlocfilehash: 1aa6b5d0ca574345e1d349ea53df96f554c06bc4
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2018
ms.locfileid: "34793836"
---
# <a name="advanced-integration-topics"></a>Negli argomenti di integrazione avanzata

Assembly di integrazione devono fare riferimento il [ `Xamarin.Workbooks.Integrations` NuGet][nuget]. Estrarre il nostro [documentazione introduttiva](~/tools/workbooks/sdk/index.md) per ulteriori informazioni sulle attività iniziali con il pacchetto NuGet.

Integrazioni client sono inoltre supportate e vengono avviate tramite l'inserimento di un file JavaScript o CSS con lo stesso nome dell'assembly di integrazione dell'agente nella stessa directory. Ad esempio, se l'assembly di integrazione dell'agente (che fa riferimento a NuGet) è denominato `SampleExternalIntegration.dll`, quindi `SampleExternalIntegration.js` e `SampleExternalIntegration.css` verranno integrate nel client anche se esistono. Integrazioni client sono facoltative.

L'integrazione esterno può essere compresso come un NuGet, fornita e a cui fa riferimento direttamente all'interno dell'applicazione che ospita l'agente, o semplicemente inseriti accanto a un `.workbook` file che si desidera utilizzarlo.

Integrazioni esterne (agente e client) in pacchetti NuGet verranno caricate automaticamente quando il pacchetto viene fatto riferimento, in base alla documentazione di avvio rapido, mentre gli assembly di integrazione forniti con la cartella di lavoro saranno necessario farvi riferimento in modo così:

```csharp
#r "SampleExternalIntegration.dll"
```

Quando si fa riferimento un'integrazione in questo modo, non venga caricato dal client subito&mdash;è necessario chiamare parte del codice dall'integrazione da caricare. Si sarà addressing questo bug in futuro.

Il `Xamarin.Interactive` PCL fornisce integrazione importante alcune API. Ogni integrazione necessario fornire almeno un punto di ingresso di integrazione:

```csharp
using Xamarin.Interactive;

[assembly: AgentIntegration (typeof (AgentIntegration))]

class AgentIntegration : IAgentIntegration
{
    const string TAG = nameof (AgentIntegration);

    public void IntegrateWith (IAgent agent)
    {
        // hook into IAgent APIs
    }
}
```

A questo punto, una volta a cui fa riferimento l'assembly di integrazione, il client in modo implicito caricherà i file di integrazione di JavaScript e CSS.

## <a name="apis"></a>API

Come con qualsiasi assembly cui viene fatto riferimento da una cartella di lavoro o in tempo reale controllare sessione, una delle relative API pubbliche sono accessibile per la sessione. È pertanto importante disporre di una superficie API ragionevole e sicura per gli utenti di esplorare.

L'assembly di integrazione è in effetti un ponte tra un'applicazione o SDK di interesse e la sessione. È possibile offrire nuove API che ha senso in particolare nel contesto di una cartella di lavoro o in tempo reale controllare di sessione, o non fornire alcuna API pubbliche e semplicemente eseguire "dietro le quinte" attività cede il controllo oggetto [rappresentazioni](~/tools/workbooks/sdk/representations.md).

> [!NOTE]
> Le API che devono essere pubblici, ma non devono essere resi visibili tramite IntelliSense possono essere contrassegnate con le normali attività `[EditorBrowsable (EditorBrowsableState.Never)]` attributo.

[nuget]: https://nuget.org/packages/Xamarin.Workbooks.Integration
