---
title: Siri remoto e i controller Bluetooth per tvOS in Xamarin
description: In questo articolo viene descritto come utilizzare il remoto Siri e Bluetooth gioco nelle App tvOS scritte con Xamarin.
ms.prod: xamarin
ms.assetid: BDB9894A-236B-424B-9032-ACD12A6C5720
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/16/2017
ms.openlocfilehash: 3fc2abed202f8b2e6993890ca4e6b3c6875522e5
ms.sourcegitcommit: ea1dc12a3c2d7322f234997daacbfdb6ad542507
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2018
ms.locfileid: "34789190"
---
# <a name="siri-remote-and-bluetooth-controllers-for-tvos-in-xamarin"></a>Siri remoto e i controller Bluetooth per tvOS in Xamarin

Gli utenti dell'app Xamarin.tvOS verranno non essere interazione con relativa interfaccia direttamente come con iOS in cui vengono toccati immagini sullo schermo del dispositivo, ma indirettamente da tra la sala utilizzando il [Siri remoto](#The-Siri-Remote).

Se l'app è un gioco, è possibile, facoltativamente, compilare il supporto per 3rd party, apportate per iOS (IFM) [gioco Bluetooth](#Bluetooth-Game-Controllers) nonché dell'app.

[![](remote-bluetooth-images/intro01.png "Il remoto Bluetooth e gioco")](remote-bluetooth-images/intro01.png#lightbox)

Questo articolo viene descritto il [Siri remoto](#The-Siri-Remote), [movimenti tocco di superficie](#Touch-Surface-Gestures) e [pulsanti remoto Siri](#Siri-Remote-Buttons) e viene illustrato come utilizzarle tramite [i movimenti e Gli storyboard](#Gestures-and-Storyboards), [i movimenti e codice](#Gestures-and-Code) e [la gestione degli eventi di basso livello](#Low-Level-Event-Handling). Infine, viene [utilizzo di gioco](#Working-with-Game-Controllers) in un'app Xamarin.tvOS.

<a name="The-Siri-Remote" />

## <a name="the-siri-remote"></a>Siri remoto

Il modo principale che gli utenti verranno interazione Apple TV e app Xamarin.tvOS è tramite remoto Siri incluso. Apple progettati per colmare la distanza tra l'utente su divano e l'interfaccia utente di Apple TV visualizzate sullo schermo TV chat room remoto.

Il compito, uno sviluppatore di app tvOS è la creazione di un'interfaccia utente rapido, semplice da utilizzare e visivamente accattivanti che sfrutta area tocco di Siri Remote, l'accelerometro, Giroscopio e pulsanti.

[![](remote-bluetooth-images/remote01.png "Siri remoto")](remote-bluetooth-images/remote01.png#lightbox)

Siri remoto presenta le seguenti funzionalità e dei relativi utilizzi previsto all'interno dell'app tvOS:

|Funzionalità|Utilizzo delle App generale|Utilizzo delle App di gioco|
|---|---|---|
|**Area tocco**<br />Scorrere rapidamente per spostarsi, premere per selezionare e tenere premuto per i menu di scelta rapida.|**Scelta/Scorri rapidamente verso**<br />Navigazione nell'interfaccia utente tra gli elementi con stato attivabili.<br /><br />**Fare clic su**<br />Attiva selezionato (attivo).|**Scelta/Scorri rapidamente verso**<br />Dipende dalla progettazione di gioco e può essere utilizzato come blocchetto D toccando sui bordi.<br /><br />**Fare clic su**<br />Eseguire la funzione del pulsante primario.|
|**Menu**<br />Premere per tornare alla schermata precedente o dal menu.|Restituisce alla schermata precedente e termina alla schermata Home Apple TV, dalla schermata principale di un'app.|Sospendere e riprendere il gioco, consente di tornare alla schermata precedente e viene chiusa alla schermata Home Apple TV dalla schermata principale di un'app.|
|**Siri/ricerca**<br />In alcuni paesi con Siri, tenere premuto per il controllo voce, tutti gli altri paesi, consente di visualizzare la schermata di ricerca.|N/D|N/D|
|**Riproduci/Pausa**<br />Riprodurre e sospendere media o fornisce una funzione secondaria in App.|Avvia la riproduzione multimediale e la riproduzione di sospendere o riprendere.|Esegue la funzione del pulsante secondario o Ignora video di introduzione (se presente).|
|**Home**<br />Premere per tornare alla schermata Home, fare doppio clic per visualizzare le applicazioni in esecuzione, premere e tenere premuto sospensione dispositivo.|N/D|N/D|
|**Volume**<br />I controlli associati a volume apparecchiature audio e video.|N/D|N/D|

<a name="Touch-Surface-Gestures" />

## <a name="touch-surface-gestures"></a>Superficie di attacco sui movimenti tocco

Area tocco di Siri Remote è in grado di rilevare un'ampia gamma di un singolo dito movimenti che è possibile rispondere nell'app Xamarin.tvOS:

|Scorri rapidamente verso|Clic|Toccare|
|---|---|---|
|![](remote-bluetooth-images/Gesture01.png)|![](remote-bluetooth-images/Gesture02.png)|![](remote-bluetooth-images/Gesture03.png)|
|Selezione (attivo) viene spostata tra gli elementi dell'interfaccia utente sullo schermo (verso l'alto, verso il basso a sinistra, destra). Passaggio consente di scorrere gli elenchi di grandi dimensioni del contenuto con rapidamente inerzia.|Attiva l'elemento selezionato (attivo) o funge da pulsante primario in un gioco. Facendo clic e tenendo possibile attivare i menu contestuali o funzioni secondarie.|Toccando leggermente la superficie tocco sui bordi funziona come pulsanti direzionali D-blocchetto, spostare lo stato attivo su, giù, sinistra o destra, a seconda dell'area di scelte. A seconda dell'app, può essere utilizzato per visualizzare i controlli nascosti.|

Apple fornisce i seguenti suggerimenti per lavorare con i movimenti tocco area:

* **Distinguere tra clic e scelte** -facendo clic su un'azione intenzionale dall'utente ed è particolarmente adatto per la selezione, attivazione e il pulsante primario di un gioco. Toccando è più complesso e deve essere utilizzata con cautela, poiché l'utente è spesso il mantenimento remoto Siri in mano e facilmente può attivare accidentalmente un evento di scelta.
* **Non ridefinire i movimenti Standard** -l'utente dispone di un requisito che i movimenti specifici eseguirà le azioni specifiche, non devono ridefinire il significato o la funzione di questi movimenti nell'app. L'unica eccezione è un'app di gioco durante la modalità di gioco attivo.
* **Definire nuovi movimenti sporadicamente** -nuovamente, l'utente dispone di un requisito che i movimenti specifici verranno eseguire azioni specifiche. È consigliabile evitare la definizione di movimenti personalizzati per eseguire azioni standard. E nuovamente, giochi costituiscono un'eccezione più normale in cui i movimenti personalizzati possono aggiungere gioco divertente, coinvolgente per il gioco.
* **Se appropriato, rispondere a D-Pad tocca** - leggermente toccando nell'angolo bordi dell'area di tocco verranno reagire come un riempimento D lo stato attivo per lo spostamento di gioco sulla direzione verso l'alto, verso il basso, a sinistra o verso destra. Se appropriato, dovrà rispondere a queste movimenti nell'applicazione o nel gioco.

<a name="Siri-Remote-Buttons" />

## <a name="siri-remote-buttons"></a>Pulsanti di Siri remoto

Oltre ai movimenti nell'area di tocco, l'app può rispondere all'utente facendo clic su area di tocco o sul pulsante Riproduci/Pausa. Se si accede usando il Framework di Controller di gioco Siri remoto, è anche possibile rilevare la pressione del pulsante di Menu. 

Inoltre, pulsanti di menu possono essere rilevati tramite un riconoscimento di movimento con standard `UIKit` elementi. Se è intercettare la pressione del pulsante di Menu, si sarà responsabile per chiudere la visualizzazione e i Controller di visualizzazione corrente e tornare a quello precedente.

> [!IMPORTANT]
> È necessario **sempre** assegnare una funzione al pulsante Play/Pausa in remoto. Con un pulsante non funzionale può rendere l'app interrotto all'utente finale. Se non si dispone di una funzione valida per questo pulsante, assegnare la stessa funzione del pulsante primario (tocco area fare clic su).

<a name="Gestures-and-Storyboards" />

## <a name="gestures-and-storyboards"></a>I movimenti e gli storyboard

Il modo più semplice l'utilizzo di Siri remoto nell'app Xamarin.tvOS consiste nell'aggiungere i riconoscitori di movimento alle visualizzazioni nella finestra di progettazione dell'interfaccia.

Per aggiungere un riconoscimento movimenti, eseguire le operazioni seguenti:

1. Nel **Esplora**, fare doppio clic su di `Main.storyboard` e aprirlo per la finestra di progettazione dell'interfaccia di modifica.
2. Trascinare un **toccare riconoscitore di movimento** dal **libreria** e rilasciarla sulla vista: 

    [![](remote-bluetooth-images/storyboard01.png "Un riconoscimento di movimento Tap")](remote-bluetooth-images/storyboard01.png#lightbox)
3. Controllare **selezionare** nel **pulsante** sezione la **attributo controllo**: 

    [![](remote-bluetooth-images/storyboard02.png "Selezionare")](remote-bluetooth-images/storyboard02.png#lightbox)
4. **Selezionare** significa che il movimento risponderà utente facendo clic di **area tocco** in remoto Siri. È anche possibile scegliere di rispondere al **Menu**, **Riproduci/Pausa**, **backup**, **verso il basso**, **sinistra** e **Destra** pulsanti.
5. Successivamente, associare un **azione** dal **toccare riconoscitore di movimento** e chiamarlo `TouchSurfaceClicked`: 

    [![](remote-bluetooth-images/storyboard03.png "Un'azione dal riconoscitore di movimento Tap")](remote-bluetooth-images/storyboard03.png#lightbox)
6. Salvare le modifiche e tornare a Visual Studio per Mac.

Modificare il Controller di visualizzazione (esempio `FirstViewController.cs`) file e aggiungere il codice seguente per gestire l'azione venga attivata:

```csharp
using System;
using UIKit;

namespace tvRemote
{
    public partial class FirstViewController : UIViewController
    {
        ...

        #region Custom Actions
        partial void TouchSurfaceClicked (Foundation.NSObject sender) {
            // Handle click here
            ...
        }
        #endregion
    }
}
```

Per ulteriori informazioni sull'uso di storyboard, consultare il nostro [Hello, tvOS Quick Start Guide](~/ios/tvos/get-started/hello-tvos.md). In particolare il [creazione dell'interfaccia utente](~/ios/tvos/get-started/hello-tvos.md#Creating-the-User-Interface) e [scrittura del codice con punti vendita e le azioni](~/ios/tvos/get-started/hello-tvos.md#Writing-the-Code) sezioni.

<a name="Gestures-and-Code" />

## <a name="gestures-and-code"></a>I movimenti e codice

Facoltativamente, è possibile creare i movimenti direttamente nel codice c# e aggiungerle alle visualizzazioni in un'interfaccia utente. Ad esempio, per aggiungere una serie di scorrere i riconoscitori di movimento, modificare il Controller di visualizzazione e aggiungere il codice seguente:

```csharp
using System;
using UIKit;

namespace tvRemote
{
    public partial class SecondViewController : UIViewController
    {
        #region Constructors
        public SecondViewController (IntPtr handle) : base (handle)
        {
        }
        #endregion

        #region Override Methods
        public override void ViewDidLoad ()
        {
            base.ViewDidLoad ();    

            // Wire-up gestures
            var upGesture = new UISwipeGestureRecognizer (() => {
                RemoteView.ArrowPressed = "Up";
                ButtonLabel.Text = "Swiped Up";
            }) {
                Direction = UISwipeGestureRecognizerDirection.Up
            };
            this.View.AddGestureRecognizer (upGesture);

            var downGesture = new UISwipeGestureRecognizer (() => {
                RemoteView.ArrowPressed = "Down";
                ButtonLabel.Text = "Swiped Down";
            }) {
                Direction = UISwipeGestureRecognizerDirection.Down
            };
            this.View.AddGestureRecognizer (downGesture);

            var leftGesture = new UISwipeGestureRecognizer (() => {
                RemoteView.ArrowPressed = "Left";
                ButtonLabel.Text = "Swiped Left";
            }) {
                Direction = UISwipeGestureRecognizerDirection.Left
            };
            this.View.AddGestureRecognizer (leftGesture);

            var rightGesture = new UISwipeGestureRecognizer (() => {
                RemoteView.ArrowPressed = "Right";
                ButtonLabel.Text = "Swiped Right";
            }) {
                Direction = UISwipeGestureRecognizerDirection.Right
            };
            this.View.AddGestureRecognizer (rightGesture);
        }
        #endregion
    }
}
```

<a name="Low-Level-Event-Handling" />

## <a name="low-level-event-handling"></a>Gestione degli eventi di basso livello

Se si sta creando un tipo personalizzato in base a `UIKit` nell'app Xamarin.tvOS (ad esempio `UIView`), è inoltre la possibilità di fornire la gestione di basso livello del pulsante tramite `UIPress` eventi. 

A `UIPress` evento è tvOS cosa un `UITouch` evento è in iOS, ad eccezione di `UIPress` restituisce informazioni sul pulsante preme Siri remoto o altri collegati dispositivi Bluetooth (ad esempio, un gioco). `UIPress` gli eventi vengono descritti la pressione del pulsante e lo stato (Began, Canceled, modificate o completata). 

Per i pulsanti analogici su dispositivi, ad esempio gioco Bluetooth, `UIPress` restituisce anche la quantità di forza al pulsante. Il `Type` proprietà del `UIPress` evento definisce quale pulsante fisico è stato modificato, mentre il resto delle proprietà di descrivere la modifica che si è verificato.

Il codice seguente viene illustrato un esempio di gestione basso livello `UIPress` gli eventi per un `UIView`:

```csharp
using System;
using Foundation;
using UIKit;

namespace tvRemote
{
    public partial class EventView : UIView
    {
        #region Computed Properties
        public override bool CanBecomeFocused {
            get {
                return true;
            }
        }
        #endregion

        #region 
        public EventView (IntPtr handle) : base (handle)
        {
        }
        #endregion

        #region Override Methods
        public override void PressesBegan (NSSet<UIPress> presses, UIPressesEvent evt)
        {
            base.PressesBegan (presses, evt);

            foreach (UIPress press in presses) {
                // Was the Touch Surface clicked?
                if (press.Type == UIPressType.Select) {
                    BackgroundColor = UIColor.Red;
                }
            }
        }

        public override void PressesCancelled (NSSet<UIPress> presses, UIPressesEvent evt)
        {
            base.PressesCancelled (presses, evt);

            foreach (UIPress press in presses) {
                // Was the Touch Surface clicked?
                if (press.Type == UIPressType.Select) {
                    BackgroundColor = UIColor.Clear;
                }
            }
        }

        public override void PressesChanged (NSSet<UIPress> presses, UIPressesEvent evt)
        {
            base.PressesChanged (presses, evt);
        }

        public override void PressesEnded (NSSet<UIPress> presses, UIPressesEvent evt)
        {
            base.PressesEnded (presses, evt);

            foreach (UIPress press in presses) {
                // Was the Touch Surface clicked?
                if (press.Type == UIPressType.Select) {
                    BackgroundColor = UIColor.Clear;
                }
            }
        }
        #endregion
    }
}
```

Come con `UITouch` eventi, se è necessario implementare qualsiasi il `UIPress` esegue l'override di eventi, è necessario implementare tutti e quattro.

<a name="Bluetooth-Game-Controllers" />

## <a name="bluetooth-game-controllers"></a>Gioco Bluetooth

Oltre a standard Siri remoto fornito con l'apportate per iOS Apple TV, 3rd party periferiche di gioco Bluetooth (IFM) può essere abbinato a Apple TV e utilizzato per controllare l'app Xamarin.tvOS.

[![](remote-bluetooth-images/game01.png "Gioco Bluetooth")](remote-bluetooth-images/game01.png#lightbox)

Gioco consente di migliorare la modalità di gioco e fornire una stima realistica delle immersion in un gioco. Possono inoltre essere utilizzati per controllare l'interfaccia Apple TV standard, pertanto l'uso non è necessario passare tra il computer remoto e il controller.

> [!IMPORTANT]
> Gioco Bluetooth sono un acquisto facoltativo che potrebbe rendere gli utenti finali, l'app non è possibile forzare l'utente a acquistarne uno. Se l'app supporta gioco deve supportare anche Siri remoto in modo che il gioco è utilizzabile da tutti gli utenti di Apple TV.

Un Controller di gioco presenta le seguenti funzionalità e dei relativi utilizzi previsto all'interno dell'app tvOS:

|Funzionalità|Utilizzo delle App generale|Utilizzo delle App di gioco|
|---|---|---|
|**D-Pad**|Consente di spostarsi tra gli elementi dell'interfaccia utente (sposta lo stato attivo).|Dipende dal gioco.|
|**A**|Attiva l'elemento selezionato (attivo).|Esegue una funzione principale del pulsante e azioni di finestra di dialogo di conferma.|
|**B**|Restituisce alla schermata precedente o viene chiuso alla schermata Home se nella schermata principale dell'applicazione.|Esegue la funzione del pulsante secondario o restituisce alla schermata precedente.|
|**X**|Avvia riproduzione o la riproduzione di sospensione/ripresa.|Dipende dal gioco.|
|**Y**|N/D|Dipende dal gioco.|
|**Menu**|Restituisce alla schermata precedente o viene chiuso alla schermata Home se nella schermata principale dell'applicazione.|Sospendere o riprendere il gioco, consente di tornare alla schermata precedente o si chiude la schermata Home se nella schermata principale dell'applicazione.|
|**Pulsante sinistro Shoulder**|Consente di spostarsi a sinistra.|Dipende dal gioco.|
|**Trigger a sinistra**|Consente di spostarsi a sinistra.|Dipende dal gioco.|
|**Pulsante destro Shoulder**|Si sposta a destra.|Dipende dal gioco.|
|**Trigger destro**|Si sposta a destra|Dipende dal gioco.|
|**Thumbstick sinistro**|Consente di spostarsi tra gli elementi dell'interfaccia utente (sposta lo stato attivo).|Dipende dal gioco.|
|**Thumbstick destra**|N/D|Dipende dal gioco.|

Apple fornisce i suggerimenti seguenti per l'utilizzo di gioco:

- **Verificare le connessioni del Controller di gioco** -app tvOS possono essere avviati e interrotti in qualsiasi momento dall'utente finale. È sempre deve verificare la presenza di un Controller di gioco all'avvio dell'app o volte attivi e intraprendere l'azione in base alle esigenze.
- **Verificare il funzionamento di App su Siri remoto sia periferiche di gioco** -non richiedono agli utenti di passare tra Siri remoto e un Controller di gioco per l'uso dell'app. Testare l'app spesso con entrambi i tipi di controller assicurando che tutto ciò che è facile passare e funziona come previsto.
- **Fornire un modo nuovamente** -premendo il pulsante di Menu deve sempre restituire alla schermata precedente. Se l'utente è la schermata principale di un'app, il pulsante di Menu deve restituire li alla schermata Home Apple TV. Durante la modalità di gioco, il pulsante di Menu deve essere visualizzato un avviso fornendo all'utente la possibilità di sospendere o riprendere la modalità di gioco o tornare al menu principale.

<a name="Working-with-Game-Controllers" />

## <a name="working-with-game-controllers"></a>Utilizzo di gioco

Come descritto in precedenza, oltre a standard Siri remoto fornito con Apple TV, l'utente è possibile allegare un 3rd party, apportate per iOS (IFM) Bluetooth gioco e usarlo per controllare l'app Xamarin.tvOS.

Se l'app è necessario input di basso livello di controller, si può usare Apple [gioco Controller Framework](https://developer.apple.com/library/prerelease/tvos/documentation/ServicesDiscovery/Conceptual/GameControllerPG/Introduction/Introduction.html#//apple_ref/doc/uid/TP40013276) che presenta le seguenti modifiche per tvOS:

- Il profilo di gioco Micro (`GCMicroGamepad`) è stato aggiunto a Siri remoto di destinazione.
- Il nuovo `GCEventViewController` classe può essere utilizzata per instradare gli eventi di gioco tramite l'app. Vedere il [determinazione gioco Controller Input](#Determining-Game-Controller-Input) sezione riportata di seguito per ulteriori dettagli.

<a name="Game-Controller-Support-Requirements" />

### <a name="game-controller-support-requirements"></a>Requisiti di supporto di gioco

Apple ha diversi requisiti specifici che devono essere soddisfatte se supportati dall'app Xamarin.tvOS gioco:

- **È necessario il supporto remoto Siri** -è sempre necessario il supporto remoto Siri. Il gioco è possibile richiedere una parte 3 di gioco sia riproducibile.
- **È necessario supportare il Layout del controllo estesa** -tvOS tutte le periferiche di gioco vengono non formfitting estesi controller.
- **Giochi devono essere Playable con controller stand-alone** -se un Controller di gioco estese supportate dall'app, deve essere riproducibile esclusivamente con i Controller di gioco.
- **È necessario supportare pulsante Play/Pausa** -durante la modalità di gioco, se l'utente preme il pulsante Play/Pausa, deve essere visualizzato un avviso fornendo all'utente la possibilità di sospendere o riprendere la modalità di gioco o tornare al menu principale.

<a name="Enabling-Game-Controller-Support" />

### <a name="enabling-game-controller-support"></a>Abilitazione del supporto di gioco

Per abilitare il supporto di gioco nell'app Xamarin.tvOS, fare doppio clic su di `Info.plist` file nel **Esplora** per aprirlo e modificarlo:

[![](remote-bluetooth-images/game02.png "L'editor di Info. plist")](remote-bluetooth-images/game02.png#lightbox)

Sotto il **gioco** sezione, inserire un segno di spunta da **abilitare gioco**, quindi verificare tutti i tipi di gioco che saranno supportati dall'app.

<a name="Using-the-Siri-Remote-as-a-Game-Controller" />

### <a name="using-the-siri-remote-as-a-game-controller"></a>Utilizzo di Siri remota come un gioco

Siri remoto forniti con Apple TV può essere utilizzato come Controller di gioco limitato. Ad esempio altre periferiche di gioco, viene visualizzato nel Framework del Controller di gioco come un `GCController` oggetto e supporta il `GCMotion` e `GCMicroGamepad` profili.

Quando viene utilizzato come un gioco, Siri remoto presenta le caratteristiche seguenti:

- Area di tocco è utilizzabile come D-riquadro che fornisce i dati di input analogici.
- Remoto può essere utilizzato con orientamento orizzontale o verticale e l'app decide se l'oggetto profilo deve invertire automaticamente i dati di input.
- Fare clic su area di tocco funge da pulsante **A** in un Controller di gioco.
- Pulsante Play/Pausa funge da pulsante **X** in un Controller di gioco.
- Il pulsante di Menu deve essere visualizzato un avviso fornendo all'utente la possibilità di sospendere o riprendere la modalità di gioco o tornare al menu principale.

<a name="Summary" />

### <a name="determining-game-controller-input"></a>Determinazione di Input di gioco

A differenza di iOS in cui è possono ricevere gli eventi di gioco in parallelo con eventi tocco, tvOS elabora tutti gli eventi di basso livello per il recapito di alto livello `UIKit` eventi. Di conseguenza, se è necessario accedere agli eventi di gioco di basso livelli, è necessario disattivare `UIKit`del comportamento predefinito.

In tvOS, quando si desidera elaborare un input di gioco direttamente è necessario utilizzare un `GCEventViewController` (o una sottoclasse) per visualizzare il gioco dell'interfaccia utente. Ogni volta che un `GCEventViewController` è il *risponditore prima*, gioco input saranno acquisiti e recapitati all'applicazione tramite il Framework del Controller di gioco.

È possibile utilizzare il `UserInteractionEnabled` proprietà la `GCEventViewController` classe per attivare o disattivare la modalità gli eventi vengono elaborati e gestiti.

Per informazioni sull'implementazione di supporto per il Controller di gioco, vedere Apple [utilizzo di gioco](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/WorkingwithGameControllers.html) sezione la [Guida alla programmazione di App per tvOS](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/index.html) e [di gioco Guida per programmatori](https://developer.apple.com/library/prerelease/tvos/documentation/ServicesDiscovery/Conceptual/GameControllerPG/Introduction/Introduction.html).

<a name="Summary" />

## <a name="summary"></a>Riepilogo

In questo articolo è illustrati nuovo Siri remoto fornito con i pulsanti di Siri remoto e i movimenti tocco di area, Apple TV. Successivamente, che trattato lavoro con i movimenti e gli storyboard, movimenti e codice e gli eventi di basso livello. Infine, se è illustrato l'utilizzo di gioco.



## <a name="related-links"></a>Collegamenti correlati

- [Esempi di tvOS](https://developer.xamarin.com/samples/tvos/all/)
- [tvOS](https://developer.apple.com/tvos/)
- [tvOS Guide interfaccia umana](https://developer.apple.com/tvos/human-interface-guidelines/)
- [Guida alla programmazione di App per tvOS](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/)
