---
title: Integrazioni debug
description: Questo documento viene descritto come eseguire il debug le integrazioni per le cartelle di lavoro di Xamarin, lato agente sia lato client in Windows e Mac.
ms.prod: xamarin
ms.assetid: 90143544-084D-49BF-B44D-7AF943668F6C
author: topgenorth
ms.author: toopge
ms.date: 06/19/2018
ms.openlocfilehash: 6e37b1ac3d0fb78b5737ebe97b5a28ab40adb648
ms.sourcegitcommit: d70fcc6380834127fdc58595aace55b7821f9098
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2018
ms.locfileid: "36269057"
---
# <a name="debugging-integrations"></a>Integrazioni debug

## <a name="debugging-agent-side-integrations"></a>Il debug sul lato agente integrazioni

Il debug di integrazioni lato agente viene eseguito meglio utilizzando i metodi di registrazione forniti dal `Log` classe `Xamarin.Interactive.Logging`. Vedere il [ `API docs` ](https://developer.xamarin.com/api/type/Xamarin.Interactive.Logging.Log/) per i metodi da chiamare.

Nel macOS, messaggi di log vengono visualizzati nel menu entrambi Visualizzatore log (**finestra > Log Viewer**) e nel Registro di client. In Windows, messaggi vengono visualizzati solo nel Registro di client, poiché non è presente alcun visualizzatore log.

Il log del client è disponibili nelle posizioni seguenti in macOS e Windows:

- Mac: `~/Library/Logs/Xamarin/Workbooks/Xamarin Workbooks {date}.log`
- Windows: `%LOCALAPPDATA%\Xamarin\Workbooks\logs\Xamarin Workbooks {date}.log`

È necessario tenere presente è che, durante il caricamento di integrazioni tramite le normali attività `#r` meccanismo durante lo sviluppo, l'assembly di integrazione verrà prelevato come un _dipendenza_ della cartella di lavoro e incluso nel pacchetto, se è un percorso assoluto non usato. Ciò può provocare modifiche per la propagazione non, come se l'integrazione di ricompilazione non aveva alcun effetto.

## <a name="debugging-client-side-integrations"></a>Il debug sul lato client integrazioni

Integrazioni sul lato client vengono scritte in JavaScript e caricate la superficie di web browser (vedere il [architettura](~/tools/workbooks/sdk/architecture.md) documentazione), il modo migliore per eseguirne il debug utilizzando gli strumenti di sviluppo WebKit su Mac oppure mediante F12 selezione in Windows .

Entrambi i set di strumenti consentono di visualizzare l'origine JavaScript o TypeScript, impostare punti di interruzione, visualizzazione dell'output di console e controllare e modificare il modello DOM.

### <a name="mac"></a>Mac

Per abilitare gli strumenti di sviluppo per le cartelle di lavoro di Xamarin su Mac, eseguire il comando seguente in terminale:

```shell
defaults write com.xamarin.Workbooks WebKitDeveloperExtras -bool true
```

e quindi riavviare le cartelle di lavoro di Xamarin. Una volta eseguita questa operazione, dovrebbe essere **controllare elemento** visualizzato il menu di scelta rapida e un nuovo **Developer** riquadro sarà disponibile nelle preferenze di cartelle di lavoro. Questa opzione consente di scegliere se si desidera che gli strumenti di sviluppo aperti all'avvio:

[![Riquadro Developer](debugging-images/developer-pane-small.png)](debugging-images/developer-pane.png#lightbox)

Questa preferenza viene anche solo il riavvio, sarà necessario riavviare il client di cartelle di lavoro affinché abbia effetto sulle nuove cartelle di lavoro. Gli strumenti di sviluppo tramite il menu di scelta rapida o le preferenze per l'attivazione verrà visualizzata l'interfaccia utente familiare di Safari:

[![Strumenti di sviluppo Safari](debugging-images/mac-dev-tools.png)](debugging-images/mac-dev-tools.png#lightbox)

Per informazioni sull'utilizzo di strumenti di sviluppo di Safari, vedere il [documentazione controllo WebKit][webkit-docs].

### <a name="windows"></a>WINDOWS

In Windows, il team di Internet Explorer fornisce uno strumento noto come "Selezione F12" vale a dire un debugger remoto per le istanze di Internet Explorer incorporate. È possibile trovare lo strumento nel percorso seguente:

```shell
C:\Windows\System32\F12\F12Chooser.exe
```

Selezione F12 esecuzione e si dovrebbe essere l'istanza incorporata che alimenta area client di cartelle di lavoro nell'elenco. Scegliere e la familiarità F12 verranno visualizzati gli strumenti di debug di Internet Explorer, collegata al client:

[![Strumenti F12](debugging-images/windows-dev-tools.png)](debugging-images/windows-dev-tools.png#lightbox)

[webkit-docs]: https://trac.webkit.org/wiki/WebInspector
