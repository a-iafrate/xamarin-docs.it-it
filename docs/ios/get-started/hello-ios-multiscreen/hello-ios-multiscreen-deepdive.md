---
title: Hello, iOS Multiscreen - Approfondimento
description: Questo documento esamina in modo dettagliato l'applicazione Phoneword espansa, prendendo in considerazione in particolare lo schema MVC (Model, View, Controller), la navigazione in iOS e altri concetti di sviluppo di app iOS.
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: c866e5f4-8154-4342-876e-efa0693d66f5
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 12/02/2016
ms.openlocfilehash: eaf77dd68895a3fbf677e1d0aa68125d81d709c1
ms.sourcegitcommit: e98a9ce8b716796f15de7cec8c9465c4b6bb2997
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2018
ms.locfileid: "39111225"
---
# <a name="hello-ios-multiscreen--deep-dive"></a>Hello, iOS Multiscreen - approfondimento

Nella procedura dettagliata di avvio rapido è stata compilata ed eseguita la prima applicazione Xamarin.iOS multi-schermata. A questo punto è necessario sviluppare una comprensione più approfondita della navigazione e dell'architettura di iOS.

In questa guida verrà introdotto lo schema *MVC (Model, View, Controller)* e il suo ruolo nell'architettura e nella navigazione di iOS.
Approfondiremo quindi il controller di spostamento e spiegheremo come offrire un'esperienza di navigazione intuitiva in iOS.

<a name="Model_View_Controller" />

## <a name="model-view-controller-mvc"></a>MVC (Model-View-Controller)

Nell'esercitazione [Hello, iOS](~/ios/get-started/hello-ios/index.md) abbiamo appreso che le applicazioni iOS hanno una sola *finestra* e che i controller di visualizzazione sono responsabili del caricamento delle rispettive *gerarchie di visualizzazione del contenuto* nella finestra. Nella seconda procedura dettagliata relativa a Phoneword abbiamo aggiunto una seconda schermata all'applicazione e passato alcuni dati (un elenco di numeri di telefono) tra le due schermate, come illustrato nella figura seguente:

 [![](hello-ios-multiscreen-deepdive-images/08.png "Questa figura illustra il passaggio dei dati tra le due schermate")](hello-ios-multiscreen-deepdive-images/08.png#lightbox)

Nel nostro esempio, i dati sono stati raccolti nella prima schermata, passati dal primo controller di visualizzazione al secondo e visualizzati dalla seconda schermata. Questa separazione di schermate, controller di visualizzazione e dati segue lo schema *MCV (Model, View, Controller)*. Nelle prossime sezioni esamineremo i vantaggi dello schema, i suoi componenti e spiegheremo come vengono usati nell'applicazione Phoneword.

### <a name="benefits-of-the-mvc-pattern"></a>Vantaggi dello schema MVC

MVC è uno *schema progettuale*, vale a dire una soluzione di architettura riutilizzabile per un problema comune o un caso d'uso nel codice. MVC è un'architettura per applicazioni con un'*interfaccia utente grafica (GUI)*. Assegna agli oggetti nell'applicazione uno dei tre ruoli *Modello* (logica di dati o applicazione), *Visualizzazione* (interfaccia utente) e *Controller* (code-behind). La figura seguente illustra le relazioni tra le tre parti dello schema MVC e l'utente:

 [![](hello-ios-multiscreen-deepdive-images/00.png "Questa figura illustra le relazioni tra le tre parti dello schema MVC e l'utente")](hello-ios-multiscreen-deepdive-images/00.png#lightbox)

Lo schema MVC è utile perché consente la separazione logica tra diverse parti di un'applicazione GUI e rende più semplice per noi riusare il codice e le visualizzazioni. Passiamo ora a osservare in modo più dettagliato ognuno dei tre ruoli.

> [!NOTE]
> Lo schema MVC ricorda vagamente la struttura delle pagine ASP.NET o delle applicazioni WPF. In questi esempi, la visualizzazione è il componente che è effettivamente responsabile della descrizione dell'interfaccia utente e corrisponde alla pagina ASPX (HTML) in ASP.NET o a XAML in un'applicazione WPF. Il controller è il componente responsabile della gestione della visualizzazione, che corrisponde al code-behind in ASP.NET o WPF.

### <a name="model"></a>Modello

L'oggetto modello è in genere una rappresentazione specifica dell'applicazione dei dati che devono essere visualizzati o inseriti nella visualizzazione. Il modello viene spesso definito genericamente, ad esempio, nella nostra app **Phoneword_iOS**, l'elenco dei numeri di telefono (rappresentato come un elenco di stringhe) è il modello. Se si compila un'applicazione multipiattaforma, è possibile scegliere di condividere il codice **PhonewordTranslator** tra le applicazioni iOS e Android. Si può anche pensare al codice condiviso come al modello.

MVC è completamente indipendente dalla *persistenza dei dati* e dall'*accesso* del modello. In altre parole, per MVC non è rilevante l'aspetto dei dati o come vengono archiviati, ma solo come vengono *rappresentati*. Si può scegliere, ad esempio, di archiviare i dati in un database SQL, oppure di salvarli in modo permanente in un meccanismo di archiviazione cloud, o ancora di usare semplicemente un elemento `List<string>`. Ai fini di MVC, nello schema è inclusa solo la rappresentazione dei dati.

In alcuni casi, la parte relativa al modello di MVC può essere vuota. Si può scegliere, ad esempio, di aggiungere alcune pagine statiche all'app per spiegare come funziona il traduttore telefonico, perché lo abbiamo compilato e come contattarci per segnalare eventuali bug. Queste schermate dell'app verranno comunque create usando le visualizzazioni e i controller, ma non hanno dati di modello reali.

> [!NOTE]
> In alcune parti della documentazione, la parte relativa al modello dello schema MVC può fare riferimento al back-end dell'intera applicazione e non solo ai dati visualizzati nell'interfaccia utente. In questa guida si usa un'interpretazione moderna del modello, ma la distinzione non è particolarmente importante.

### <a name="view"></a>Visualizza

Una visualizzazione è il componente responsabile del rendering dell'interfaccia utente. In quasi tutte le piattaforme che usano lo schema MVC l'interfaccia utente è costituita da una gerarchia di visualizzazioni. Una visualizzazione in MVC può essere considerata come una gerarchia di visualizzazioni con una singola visualizzazione, detta visualizzazione radice, in cima alla gerarchia e un numero qualsiasi di visualizzazioni figlio (dette visualizzazioni secondarie) sotto di essa. In iOS, la gerarchia di visualizzazione del contenuto di una schermata corrisponde al componente di visualizzazione in MVC.

### <a name="controller"></a>Controller

L'oggetto controller è il componente che collega tutti gli elementi insieme e viene rappresentato in iOS dall'elemento `UIViewController`. Il controller può essere considerato come il codice di supporto per una schermata o un set di visualizzazioni. Il controller è responsabile dell'ascolto delle richieste da parte dell'utente e della restituzione della gerarchia di visualizzazione appropriata. Ascolta le richieste provenienti dalla visualizzazione (clic di pulsanti, input di testo e così via) ed esegue l'elaborazione, la modifica e il ricaricamento della visualizzazione appropriati. Il controller è anche responsabile di creare o recuperare il modello da qualsiasi archivio dati di backup esistente nell'applicazione e di popolare la visualizzazione con i relativi dati.

I controller possono anche gestire altri controller. Un controller potrebbe ad esempio caricare un altro controller se è necessario visualizzare una schermata diversa o gestire uno stack di controller per monitorarne l'ordine e le relative transizioni. Nella sezione successiva vedremo l'esempio di un controller che gestisce gli altri controller presentando un tipo particolare di controller di visualizzazione iOS chiamato *controller di spostamento*.

## <a name="navigation-controller"></a>Controller di spostamento

Nell'applicazione Phoneword abbiamo usato un controller di spostamento per gestire la navigazione tra più schermate. Il controller di spostamento è un oggetto `UIViewController` specializzato rappresentato dalla classe `UINavigationController`. Anziché gestire una singola gerarchia di visualizzazione del contenuto, il controller di spostamento gestisce altri controller di visualizzazione, oltre alla propria gerarchia di visualizzazione del contenuto speciale, sotto forma di una barra degli strumenti di navigazione che include un titolo, un pulsante Indietro e altre funzionalità facoltative.

Il controller di spostamento è comune nelle applicazioni iOS e offre funzioni di navigazione per le applicazioni iOS di base come l'app **Settings** (Impostazioni), come illustrato nella schermata seguente:

 [![](hello-ios-multiscreen-deepdive-images/01.png "Il controller di spostamento offre funzioni di navigazione per le applicazioni iOS come l'app Settings (Impostazioni) visualizzata qui")](hello-ios-multiscreen-deepdive-images/01.png#lightbox)

Il controller di spostamento svolge tre funzioni principali:

-  **Offre hook per la navigazione in avanti**: il controller di spostamento usa una metafora di navigazione gerarchica in cui le gerarchie di visualizzazione del contenuto vengono *inviate* su uno *stack di navigazione*. Lo stack di navigazione può essere considerato come un mazzo di carte impilato in cui è visibile solo la carta situata più in alto, come illustrato nella figura seguente:  

    [![](hello-ios-multiscreen-deepdive-images/02.png "Questa figura illustra la navigazione come un mazzo di carte")](hello-ios-multiscreen-deepdive-images/02.png#lightbox)


-  **Facoltativamente, offre un pulsante Indietro**: quando si inserisce un nuovo elemento nello stack di navigazione, la barra del titolo può visualizzare automaticamente un *pulsante Indietro* che consente all'utente di spostarsi all'indietro. Premendo il pulsante Indietro, il controller di navigazione corrente viene *estratto* dallo stack di navigazione e viene caricata la gerarchia di visualizzazione del contenuto precedente nella finestra:  

    [![](hello-ios-multiscreen-deepdive-images/03.png "Questa figura illustra l'estrazione di una carta dal mazzo")](hello-ios-multiscreen-deepdive-images/03.png#lightbox)


-  **Include una barra del titolo**: la parte superiore del controller di spostamento viene chiamata *barra del titolo*. È responsabile della visualizzazione del titolo del controller di spostamento, come illustrato nella figura seguente:  

    [![](hello-ios-multiscreen-deepdive-images/04.png "La barra del titolo è responsabile della visualizzazione del titolo del controller di spostamento")](hello-ios-multiscreen-deepdive-images/04.png#lightbox)

### <a name="root-view-controller"></a>Controller visualizzazione radice

Un controller di spostamento non gestisce una gerarchia di visualizzazione del contenuto, pertanto non ha nulla da visualizzare di per sé.
Un controller di spostamento è invece associato a un *controller visualizzazione radice*:

 [![](hello-ios-multiscreen-deepdive-images/05.png "Un controller di spostamento è associato a un controller visualizzazione radice")](hello-ios-multiscreen-deepdive-images/05.png#lightbox)

Il controller visualizzazione radice rappresenta il primo controller di visualizzazione nello stack del controller di spostamento e la gerarchia di visualizzazione del contenuto del controller visualizzazione radice è la prima gerarchia di visualizzazione del contenuto a essere caricata nella finestra. Se si intende inserire l'intera applicazione nello stack del controller di spostamento, è possibile spostare l'elemento Sourceless Segue nel controller di spostamento e impostare il controller di visualizzazione della prima schermata come controller visualizzazione radice, come abbiamo fatto nell'app Phoneword:

 [![](hello-ios-multiscreen-deepdive-images/06.png "L'elemento Sourceless Segue imposta il controller di visualizzazione delle prime schermate come controller visualizzazione radice")](hello-ios-multiscreen-deepdive-images/06.png#lightbox)

### <a name="additional-navigation-options"></a>Opzioni di navigazione aggiuntive

Il controller di spostamento è un modo comune per gestire la navigazione in iOS, ma non è l'unica opzione. Ad esempio, un [controller di barra schede](~/ios/user-interface/controls/creating-tabbed-applications.md) può suddividere un'applicazione in diverse aree funzionali e un [controller doppia visualizzazione](https://github.com/xamarin/recipes/tree/master/Recipes/ios/content_controls/split_view/use_split_view_to_show_two_controllers) può essere usato per creare visualizzazioni master/dettagli. La combinazione dei controller di spostamento con questi altri paradigmi di spostamento offre molti metodi flessibili per la presentazione e la navigazione del contenuto in iOS.

## <a name="handling-transitions"></a>Gestione delle transizioni

Nella procedura dettagliata relativa a Phoneword è stata gestita la transizione tra i due controller di visualizzazione in due modi diversi: prima con un elemento Storyboard Segue e poi a livello di codice. Vediamo in modo più dettagliato entrambe le opzioni.

### <a name="prepareforsegue"></a>PrepareForSegue

Quando si aggiunge un elemento Segue con un'azione **Show** (Mostra) allo storyboard, indicare a iOS di inserire il secondo controller di visualizzazione nello stack del controller di spostamento:

 [![](hello-ios-multiscreen-deepdive-images/09.png "Impostazione del tipo di elemento Segue da un elenco a discesa")](hello-ios-multiscreen-deepdive-images/09.png#lightbox)

L'aggiunta di un elemento Segue allo storyboard è sufficiente a creare una semplice transizione tra le schermate. Se si intende passare i dati tra i controller di visualizzazione, è necessario eseguire l'override del metodo `PrepareForSegue` e gestire i dati direttamente:

```csharp
public override void PrepareForSegue (UIStoryboardSegue segue, NSObject sender)
{
    base.PrepareForSegue (segue, sender);
    ...
}
```

iOS chiama `PrepareForSegue` appena prima del verificarsi della transizione e passa l'elemento Segue creato nello storyboard nel metodo.
A questo punto, è necessario impostare manualmente il controller di visualizzazione di destinazione dell'elemento Segue. Il codice seguente ottiene un punto di controllo per il controller di visualizzazione di destinazione e ne esegue il cast alla classe appropriata, in questo caso CallHistoryController:

```csharp
CallHistoryController callHistoryContoller = segue.DestinationViewController as CallHistoryController;
```

Passiamo infine l'elenco di numeri di telefono (il modello) da `ViewController` a `CallHistoryController` impostando la proprietà `PhoneHistory` di `CallHistoryController` sull'elenco dei numeri di telefono composti:

```csharp
callHistoryContoller.PhoneNumbers = PhoneNumbers;
```

Il codice completo per il passaggio dei dati tramite un elemento Segue è il seguente:

```csharp
public override void PrepareForSegue (UIStoryboardSegue segue, NSObject sender)
{
    base.PrepareForSegue (segue, sender);

    var callHistoryContoller = segue.DestinationViewController as CallHistoryController;

    if (callHistoryContoller != null) {
         callHistoryContoller.PhoneNumbers = PhoneNumbers;
    }
 }
```

### <a name="navigation-without-segues"></a>Navigazione senza elementi Segue

La transizione dal primo controller di visualizzazione al secondo nel codice implica lo stesso processo di un elemento Segue, ma alcuni passaggi devono essere eseguiti manualmente.
Usiamo prima `this.NavigationController` per ottenere un riferimento al controller di spostamento sul cui stack ci troviamo attualmente. Usiamo quindi il metodo `PushViewController` del controller di spostamento per eseguire manualmente il push del controller di visualizzazione nello stack, passando il controller di visualizzazione e un'opzione per aggiungere un'animazione alla transizione (lo abbiamo impostato su `true`).

Il codice seguente gestisce la transizione dalla schermata di Phoneword alla schermata Call History (Cronologia chiamate):

```csharp
this.NavigationController.PushViewController (callHistory, true);
```

Prima di poter eseguire la transizione al controller di visualizzazione successivo, è necessario crearne manualmente un'istanza dallo storyboard chiamando `this.Storyboard.InstantiateViewController` e passando l'ID di uno storyboard di `CallHistoryController`:

```csharp
CallHistoryController callHistory =
this.Storyboard.InstantiateViewController
("CallHistoryController") as CallHistoryController;
```

Passiamo infine l'elenco di numeri di telefono (il modello) da `ViewController` a `CallHistoryController` impostando la proprietà `PhoneHistory` di `CallHistoryController` sull'elenco dei numeri di telefono composti, come abbiamo fatto per la gestione della transizione con un elemento Segue:

```csharp
callHistory.PhoneNumbers = PhoneNumbers;
```

Il codice completo per la transizione a livello di codice è il seguente:

```csharp
CallHistoryButton.TouchUpInside += (object sender, EventArgs e) => {
    // Launches a new instance of CallHistoryController
    CallHistoryController callHistory = this.Storyboard.InstantiateViewController ("CallHistoryController") as CallHistoryController;
    if (callHistory != null) {
     callHistory.PhoneNumbers = PhoneNumbers;
     this.NavigationController.PushViewController (callHistory, true);
    }
};
```

## <a name="additional-concepts-introduced-in-phoneword"></a>Altri concetti introdotti in Phoneword

L'applicazione Phoneword ha introdotto alcuni concetti non trattati in questa guida. Essi includono:

-  **Creazione automatica dei controller di visualizzazione**: quando si immette un nome di classe per il controller di visualizzazione nel **riquadro delle proprietà**, la finestra di progettazione iOS verifica se quella classe esiste e genera quindi automaticamente la classe sottostante del controller di visualizzazione. Per altre informazioni su questa e altre funzionalità di progettazione iOS, vedere la guida [Introduction to the iOS Designer](~/ios/user-interface/designer/introduction.md) (Introduzione alla finestra di progettazione iOS).
-  **Controller di visualizzazione tabella**: `CallHistoryController` è un controller di visualizzazione tabella. Un controller di visualizzazione tabella contiene una visualizzazione tabella, lo strumento di visualizzazione di layout e dati più comune in iOS. Le tabelle non rientrano nell'ambito di questa guida. Per altre informazioni sul controller di visualizzazione tabella, vedere la guida [Working with Tables and Cells](~/ios/user-interface/controls/tables/index.md) (Uso di tabelle e celle).
-   **ID storyboard**: l'impostazione dell'ID storyboard crea una classe del controller di visualizzazione in Objective-C, che contiene il code-behind per il controller di visualizzazione nello storyboard. L'ID di storyboard viene usato per trovare la classe Objective-C e creare un'istanza del controller di visualizzazione nello storyboard. Per altre informazioni sugli ID storyboard, vedere la guida [Introduction to Storyboards](~/ios/user-interface/storyboards/index.md) (Introduzione agli storyboard).

## <a name="summary"></a>Riepilogo

Complimenti, è stata completata la prima applicazione multi-schermata iOS.

In questa guida abbiamo presentato lo schema MVC e lo abbiamo usato per creare un'applicazione multi-schermata. Abbiamo anche analizzato i controller di spostamento e il loro ruolo nel potenziamento della navigazione in iOS. Hai acquisito le competenze di base necessarie per iniziare a sviluppare le tue applicazioni Xamarin.iOS.

In seguito spiegheremo come compilare applicazioni multipiattaforma con Xamarin tramite le guide [Introduction to Mobile Development](~/cross-platform/get-started/introduction-to-mobile-development.md) (Introduzione allo sviluppo mobile) e [Building Cross-Platform Applications](~/cross-platform/app-fundamentals/building-cross-platform-applications/index.md) (Compilazione di applicazioni multipiattaforma).

## <a name="related-links"></a>Collegamenti correlati

- [Hello, iOS (sample)](https://developer.xamarin.com/samples/monotouch/Hello_iOS/) (Hello, iOS - Esempio)
- [Linee guida dell'interfaccia umana iOS](http://developer.apple.com/library/ios/#documentation/UserExperience/Conceptual/MobileHIG/Introduction/Introduction.html)
- [Portale di provisioning iOS](https://developer.apple.com/ios/manage/overview/index.action)
