---
title: Embeddinator 4000 procedure consigliate per ObjC
ms.topic: article
ms.prod: xamarin
ms.assetid: 932C3F0C-D968-42D1-BB14-D97C73361983
ms.technology: xamarin-cross-platform
author: topgenorth
ms.author: toopge
ms.date: 11/14/2017
ms.openlocfilehash: 0000cbfdd690b8478b52cbcb84230ed878746daa
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/27/2018
---
# <a name="embeddinator-4000-best-practices-for-objc"></a>Embeddinator 4000 procedure consigliate per ObjC

Si tratta di una bozza e potrebbe non essere sincronizzata con le funzionalità attualmente supportato dallo strumento. Ci auguriamo che questo documento verrà evolvere separatamente e corrisponde alla fine dello strumento finale, ad esempio consigliabile sarà a lungo termine migliori approcci - soluzioni alternative non immediati.

Gran parte di questo documento si applica anche ad altri linguaggi supportati. Sono tuttavia tutti gli esempi in c# e Objective-C.


# <a name="exposing-a-subset-of-the-managed-code"></a>Esposizione di un subset del codice gestito

Il libreria/framework nativo generato contiene codice Objective-C per la chiamata di API gestite che viene esposto ognuna. L'API di più superficie di attacco (Rendi pubblico) quindi maggiore nativo _glue_ diventerà libreria.

Potrebbe essere opportuno creare un assembly diverso di piccole dimensioni, per esporre solo le API necessarie per lo sviluppatore nativo. La facciata anche consente maggiore controllo sulla visibilità, denominazione, errore durante la verifica... il codice generato.


# <a name="exposing-a-chunkier-api"></a>Esposizione di un'API chunkier

È presente un prezzo da pagare per la transizione da nativo a gestito (e indietro). Di conseguenza, è consigliabile esporre _soluzioni "voluminose" anziché "frammentate"_ API per gli sviluppatori nativi, ad esempio,

**"Frammentate"**
```
public class Person {
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

```csharp
// this requires 3 calls / transitions to initialize the instance
Person *p = [[Person alloc] init];
p.firstName = @"Sebastien";
p.lastName = @"Pouliot";
```

**Chunky**
```
public class Person {
    public Person (string firstName, string lastName) {}
}
```

```csharp
// a single call / transition will perform better
Person *p = [[Person alloc] initWithFirstName:@"Sebastien" lastName:@"Pouliot"];
```

Poiché il numero di transizioni più piccolo le prestazioni risulteranno migliori. Richiede inoltre meno codice da generare, pertanto questa sintassi produrrà anche una libreria nativa più piccola.


# <a name="naming"></a>Denominazione

Denominazione di elementi è uno dei due problemi più difficili in informatica, gli altri da cache gli errori di invalidamento e off-da-1. Probabilmente .NET incorporamento può non richiedono tutto tranne denominazione.

## <a name="types"></a>Tipi

Objective-C non supporta gli spazi dei nomi. In generale, i tipi sono preceduti 2 (per Apple) o 3 (per le parti 3rd) carattere di prefisso, ad esempio `UIView` per visualizzazione della UIKit, che indica il framework.

Per i tipi .NET ignorando lo spazio dei nomi non è possibile come nomi duplicati o ambigui, può introdurre. In questo modo i tipi .NET esistenti molto lunghi, ad esempio

```csharp
namespace Xamarin.Xml.Configuration {
    public class Reader {}
}
```

potrebbe essere utilizzata come:

```csharp
id reader = [[Xamarin_Xml_Configuration_Reader alloc] init];
```

È tuttavia possibile esporre nuovamente il tipo come:

```csharp
public class XAMXmlConfigReader : Xamarin.Xml.Configuration.Reader {}
```

rende più semplice di Objective-C da utilizzare, ad esempio:

```csharp
id reader = [[XAMXmlConfigReader alloc] init];
```

## <a name="methods"></a>Metodi

Anche i tempi nomi .NET potrebbero non essere ideali per un'API Objective-C.

Convenzioni di denominazione in Objective-C sono diverse rispetto a .NET (maiuscole-minuscole camel anziché maiuscole minuscole pascal, più dettagliata).
Leggere la [codifica linee guida per Cocoa](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html#//apple_ref/doc/uid/20001282-BCIGIJJF).

Da punto di vista di uno sviluppatore di Objective-C, un metodo con un `Get` prefisso implica non si è proprietari di istanza, ad esempio il [Ottieni regola](https://developer.apple.com/library/content/documentation/CoreFoundation/Conceptual/CFMemoryMgmt/Concepts/Ownership.html#//apple_ref/doc/uid/20001148-SW1).

Questa regola di denominazione non esistono corrispondenze nell'ambiente di GC .NET; un metodo .NET con un `Create` prefisso si comporterà in modo identico in .NET. Tuttavia, per gli sviluppatori Objective-C, in genere significa che si è proprietari di istanza restituita, ovvero il [creare regola](https://developer.apple.com/library/content/documentation/CoreFoundation/Conceptual/CFMemoryMgmt/Concepts/Ownership.html#//apple_ref/doc/uid/20001148-103029).

# <a name="exceptions"></a>Eccezioni

È ancora pronti commont in .NET per utilizzare le eccezioni in modo esteso per segnalare gli errori. Tuttavia, sono lente e non è abbastanza identica in ObjC. Quando possibile è consigliabile nascondere da parte dello sviluppatore Objective-C.

Ad esempio, .NET `Try` pattern è molto più semplice da utilizzare dal codice Objective-C:

```csharp
public int Parse (string number)
{
    return Int32.Parse (number);
}
```

rispetto a

```csharp
public bool TryParse (string number, out int value)
{
    return Int32.TryParse (number, out value);
}
```

## <a name="exceptions-inside-init"></a>Eccezioni all'interno `init*`

In .NET un costruttore deve avere esito positivo o restituire una (_probabilmente_) genera un'eccezione o istanza valido.

È invece Objective-C `init*` per restituire `nil` quando non è possibile creare un'istanza. Si tratta di un modello comune, ma non è generico, utilizzato in molti dei framework di Apple. In altri casi un `assert` possono verificarsi (e terminare il processo corrente).

Il generatore di seguire lo stesso `return nil` di schema per generare `init*` metodi. Se viene generata un'eccezione gestita, quindi verrà stampato (utilizzando `NSLog`) e `nil` verrà restituito al chiamante.

## <a name="operators"></a>Operatori

ObjC non consentire operatori in overload come c#, pertanto vengono convertiti di selettori di classe.

["Descrittivo"](https://msdn.microsoft.com/en-us/library/ms229032(v=vs.110).aspx) metodo denominato generati anziché gli overload dell'operatore trovato, quindi in grado di produrre un semplice utilizzare l'API.

Le classi che eseguono l'override gli operatori = = e/o! = deve eseguire l'override anche il metodo Equals (Object) standard.