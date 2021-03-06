---
title: Approfondimento su Xamarin.Forms
description: Questo articolo esamina i concetti fondamentali dello sviluppo di applicazioni con Xamarin.Forms. Gli argomenti trattati includono l'anatomia di un'applicazione Xamarin.Forms, le nozioni di base su architettura e applicazione e l'interfaccia utente.
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: d97aa580-1eb9-48b3-b15b-0d7421ea7ae
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 06/13/2018
ms.openlocfilehash: 7eff7f4413b533caadcf2aa8b5eed8c4ab65449d
ms.sourcegitcommit: b56b3f906d2c05a3f1be219ef41be8b79e519b8e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2018
ms.locfileid: "39242225"
---
# <a name="xamarinforms-deep-dive"></a>Approfondimento su Xamarin.Forms

Nella [guida introduttiva a Xamarin.Forms](~/xamarin-forms/get-started/hello-xamarin-forms/quickstart.md) è stata compilata l'applicazione Phoneword. Questo articolo esamina ciò che è stato compilato per comprendere meglio le nozioni di base del funzionamento delle applicazioni Xamarin.Forms.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

## <a name="introduction-to-visual-studio"></a>Introduzione a Visual Studio

Visual Studio è un potente ambiente di sviluppo integrato di Microsoft. Include una finestra di progettazione visiva completamente integrata, un editor di testo completo di strumenti di refactoring, un browser di assembly, l'integrazione del codice sorgente e altro ancora. Questo articolo tratta in particolare dell'uso di alcune funzionalità di base di Visual Studio con il plug-in Xamarin.

Visual Studio consente di organizzare il codice in *soluzioni* e *progetti*. Una soluzione è un contenitore per uno o più progetti. Un progetto può essere un'applicazione, una libreria di supporto, un'applicazione di test e altro ancora. L'applicazione Phoneword è costituita da una soluzione contenente quattro progetti, come illustra lo screenshot seguente.

![](deepdive-images/vs/solution.png "Esplora soluzioni di Visual Studio")

I progetti sono:

- Phoneword: progetto di libreria .NET Standard che contiene tutto il codice condiviso e l'interfaccia utente condivisa.
- Phoneword.Android: progetto che contiene il codice specifico di Android ed è il punto di ingresso per l'applicazione Android.
- Phoneword.iOS: progetto che contiene il codice specifico di iOS ed è il punto di ingresso per l'applicazione iOS.
- Phoneword.UWP: progetto che contiene il codice specifico della piattaforma UWP (Universal Windows Platform) ed è il punto di ingresso per l'applicazione UWP.

## <a name="anatomy-of-a-xamarinforms-application"></a>Anatomia di un'applicazione Xamarin.Forms

Lo screenshot seguente illustra il contenuto del progetto di libreria .NET Standard Phoneword in Visual Studio:

![](deepdive-images/vs/net-standard-project.png "Contenuti del progetto .NET Standard Phoneword")

Il progetto ha un nodo **Dipendenze** contenente i nodi **NuGet** e **SDK**. Il nodo **NuGet** contiene il pacchetto NuGet Xamarin.Forms aggiunto al progetto e il nodo **SDK** contiene il `NETStandard.Library` metapacchetto che fa riferimento al set completo di pacchetti NuGet che definiscono .NET Standard.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio per Mac](#tab/vsmac)

## <a name="introduction-to-visual-studio-for-mac"></a>Introduzione a Visual Studio per Mac

Visual Studio per Mac è un ambiente di sviluppo integrato open source gratuito simile a Visual Studio. Include una finestra di progettazione visiva completamente integrata, un editor di testo completo di strumenti di refactoring, un browser di assembly, l'integrazione del codice sorgente e altro ancora. Per altre informazioni su Visual Studio per Mac, vedere [Introduzione a Visual Studio per Mac](/visualstudio/mac/).

Visual Studio per Mac segue la prassi di Visual Studio di organizzare il codice in *soluzioni* e *progetti*. Una soluzione è un contenitore per uno o più progetti. Un progetto può essere un'applicazione, una libreria di supporto, un'applicazione di test e altro ancora. L'applicazione Phoneword è costituita da una soluzione contenente tre progetti, come illustra lo screenshot seguente.

![](deepdive-images/xs/solution.png "Riquadro di Visual Studio per Mac")

I progetti sono:

- Phoneword: progetto di libreria .NET Standard che contiene tutto il codice condiviso e l'interfaccia utente condivisa.
- Phoneword.Droid: progetto che contiene il codice specifico di Android ed è il punto di ingresso per le applicazioni Android.
- Phoneword.iOS: progetto che contiene il codice specifico di iOS ed è il punto di ingresso per le applicazioni iOS.

## <a name="anatomy-of-a-xamarinforms-application"></a>Anatomia di un'applicazione Xamarin.Forms

Lo screenshot seguente illustra il contenuto del progetto di libreria .NET Standard Phoneword in Visual Studio per Mac:

![](deepdive-images/xs/library-project.png "Contenuti del progetto Libreria .NET Standard Phoneword")

Il progetto ha un nodo **Dipendenze** contenente i nodi **NuGet** e **SDK**. Il nodo **NuGet** contiene il pacchetto NuGet Xamarin.Forms aggiunto al progetto e il nodo **SDK** contiene il `NETStandard.Library` metapacchetto che fa riferimento al set completo di pacchetti NuGet che definiscono .NET Standard.

-----

Il progetto è costituito anche da alcuni file:

- **App.xaml**: markup XAML per la classe `App`, che definisce un dizionario risorse per l'applicazione.
- **App.Xaml.cs**: code-behind per la classe `App`, che è responsabile della creazione di istanze della prima pagina visualizzata dall'applicazione in ogni piattaforma e della gestione degli eventi del ciclo di vita dell'applicazione.
- **IDialer.cs**: interfaccia di `IDialer`, che specifica che il metodo `Dial` deve essere indicato dalle classi di implementazione.
- **MainPage.xaml**: markup XAML per la classe `MainPage`, che definisce l'interfaccia utente per la pagina visualizzata all'avvio dell'applicazione.
- **MainPage.xaml.cs**: code-behind per la classe `MainPage`, che contiene la logica di business eseguita quando l'utente interagisce con la pagina.
- **PhoneTranslator.cs**: logica di business responsabile della conversione di una parola telefonica in un numero telefonico, richiamata da **MainPage.xaml.cs**.

Per altre informazioni sull'anatomia di un'applicazione Xamarin.iOS, vedere l'[analisi dettagliata di un'applicazione Xamarin.iOS](~/ios/get-started/hello-ios/hello-ios-deepdive.md#anatomy-of-a-xamarinios-application). Per altre informazioni sull'anatomia di un'applicazione Xamarin.Android, vedere l'[analisi dettagliata di un'applicazione Xamarin.Android](~/android/get-started/hello-android/hello-android-deepdive.md#anatomy).

## <a name="architecture-and-application-fundamentals"></a>Architettura e concetti fondamentali dell'applicazione

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Un'applicazione Xamarin.Forms ha la stessa struttura di un'applicazione multipiattaforma tradizionale. Il codice condiviso in genere viene inserito in una libreria .NET Standard e le applicazioni specifiche della piattaforma usano il codice condiviso. Il diagramma seguente illustra una panoramica di questa relazione per l'applicazione Phoneword:

![](deepdive-images/vs/architecture.png "Architettura Phoneword")

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio per Mac](#tab/vsmac)

Un'applicazione Xamarin.Forms ha la stessa struttura di un'applicazione multipiattaforma tradizionale. Il codice condiviso in genere viene inserito in una libreria .NET Standard e le applicazioni specifiche della piattaforma usano il codice condiviso. Il diagramma seguente illustra una panoramica di questa relazione per l'applicazione Phoneword:

![](deepdive-images/xs/architecture.png "Architettura Phoneword")

-----

Per ottimizzare il riuso del codice di avvio, le applicazioni Xamarin.Forms hanno una sola classe denominata `App`, responsabile della creazione dell'istanza della prima pagina visualizzata dall'applicazione in ogni piattaforma, come illustra l'esempio di codice che segue:

```csharp
using Xamarin.Forms;
using Xamarin.Forms.Xaml;

[assembly: XamlCompilation(XamlCompilationOptions.Compile)]
namespace Phoneword
{
    public partial class App : Application
    {
        public App()
        {
            InitializeComponent();
            MainPage = new MainPage();
        }
        ...
    }
}
```

Questo codice imposta la proprietà `MainPage` della classe `App` su una nuova istanza della classe [`MainPage`](xref:Xamarin.Forms.Application.MainPage). Inoltre, l'attributo [`XamlCompilation`](xref:Xamarin.Forms.Xaml.XamlCompilationAttribute) attiva il compilatore XAML, in modo che il codice XAML venga compilato direttamente in linguaggio intermedio. Per altre informazioni, vedere [XAML Compilation](~/xamarin-forms/xaml/xamlc.md) (Compilazione XAML).

## <a name="launching-the-application-on-each-platform"></a>Avvio dell'applicazione in ogni piattaforma

### <a name="ios"></a>iOS

Per l'avvio della pagina iniziale di Xamarin.Forms in iOS, il progetto Phoneword.iOS include la classe `AppDelegate` che eredita dalla classe `FormsApplicationDelegate`, come illustrato nell'esempio di codice seguente:

```csharp
namespace Phoneword.iOS
{
    [Register ("AppDelegate")]
    public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
    {
        public override bool FinishedLaunching (UIApplication app, NSDictionary options)
        {
            global::Xamarin.Forms.Forms.Init ();
            LoadApplication (new App ());
            return base.FinishedLaunching (app, options);
        }
    }
}
```

La sostituzione `FinishedLaunching` inizializza il framework Xamarin.Forms chiamando il metodo `Init`. In questo modo l'implementazione specifica di Xamarin.Forms per iOS viene caricata nell'applicazione prima che il controller della visualizzazione radice sia impostato dalla chiamata del metodo `LoadApplication`.

### <a name="android"></a>Android

Per l'avvio della pagina iniziale di Xamarin.Forms in Android, il progetto Phoneword.Droid include codice che crea un elemento `Activity` con l'attributo `MainLauncher` e con l'attività che eredita dalla classe `FormsAppCompatActivity`, come visualizzato nell'esempio di codice seguente:

```csharp
namespace Phoneword.Droid
{
    [Activity(Label = "Phoneword", 
              Icon = "@mipmap/icon", 
              Theme = "@style/MainTheme", 
              MainLauncher = true,
              ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation)]
    public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
    {
        internal static MainActivity Instance { get; private set; }

        protected override void OnCreate(Bundle bundle)
        {
            TabLayoutResource = Resource.Layout.Tabbar;
            ToolbarResource = Resource.Layout.Toolbar;

            base.OnCreate(bundle);
            Instance = this;
            global::Xamarin.Forms.Forms.Init(this, bundle);
            LoadApplication(new App());
        }
    }
}
```

La sostituzione `OnCreate` inizializza il framework Xamarin.Forms chiamando il metodo `Init`. In questo modo l'implementazione specifica di Xamarin.Forms per Android viene caricata nell'applicazione prima del caricamento dell'applicazione Xamarin.Forms. La classe `MainActivity` archivia anche un riferimento a se stessa nella proprietà `Instance`. La proprietà `Instance` è nota come contesto locale e vi fa riferimento la classe `PhoneDialer`.

## <a name="universal-windows-platform"></a>Piattaforma UWP (Universal Windows Platform)

Nelle applicazioni della piattaforma UWP (Universal Windows Platform) il metodo `Init` che inizializza il framework Xamarin.Forms viene chiamato dalla classe `App`:

```csharp
Xamarin.Forms.Forms.Init (e);

if (e.PreviousExecutionState == ApplicationExecutionState.Terminated)
{
  ...
}
```

Di conseguenza viene caricata nell'applicazione l'implementazione di Xamarin.Forms specifica per la piattaforma UWP. La pagina iniziale di Xamarin.Forms viene avviata dalla classe `MainPage`, come illustrato nell'esempio di codice seguente:

```csharp
namespace Phoneword.UWP
{
    public sealed partial class MainPage
    {
        public MainPage()
        {
            this.InitializeComponent();
            this.LoadApplication(new Phoneword.App());
        }
    }
}
```

L'applicazione Xamarin.Forms viene caricata con il metodo `LoadApplication`.

> [!NOTE]
> Le app della piattaforma UWP (Universal Windows Platform) si possono compilare con Xamarin.Forms, ma solo usando Visual Studio in Windows.

## <a name="user-interface"></a>Interfaccia utente

Per creare l'interfaccia utente di un'applicazione in Xamarin.Forms è possibile usare quattro gruppi di controlli principali.

1. **Pagine**: le pagine di Xamarin.Forms rappresentano le schermate dell'applicazione multipiattaforma per dispositivi mobili. L'applicazione Phoneword usa la classe [`ContentPage`](xref:Xamarin.Forms.ContentPage) per visualizzare una singola schermata. Per altre informazioni sulle pagine, vedere [Xamarin.Forms Pages](~/xamarin-forms/user-interface/controls/pages.md) (Pagine di Xamarin.Forms).
1. **Layout**: i layout di Xamarin.Forms sono contenitori usati per convertire le visualizzazioni in strutture logiche. L'applicazione Phoneword usa la classe [`StackLayout`](xref:Xamarin.Forms.StackLayout) per disporre i controlli in uno stack orizzontale. Per altre informazioni sui layout, vedere [Xamarin.Forms Layouts](~/xamarin-forms/user-interface/controls/layouts.md) (Layout di Xamarin.Forms).
1. **Visualizzazioni**: le visualizzazioni di Xamarin.Forms sono i controlli visualizzati nell'interfaccia utente, ad esempio le etichette, i pulsanti e le caselle di immissione testo. L'applicazione Phoneword usa i controlli [`Label`](xref:Xamarin.Forms.Label), [`Entry`](xref:Xamarin.Forms.Entry) e [`Button`](xref:Xamarin.Forms.Button). Per altre informazioni sulle visualizzazioni, vedere [Xamarin.Forms Views](~/xamarin-forms/user-interface/controls/views.md) (Visualizzazioni di Xamarin.Forms).
1. **Celle**: le celle di Xamarin.Forms sono elementi speciali usati per le voci di un elenco e descrivono la rappresentazione di ogni elemento di un elenco. L'applicazione Phoneword non usa alcuna cella. Per altre informazioni sulle celle, vedere [Xamarin.Forms Cells](~/xamarin-forms/user-interface/controls/cells.md) (Celle di Xamarin.Forms).

In fase di runtime ogni controllo viene mappato al controllo nativo equivalente, che viene restituito nel rendering.

Quando l'applicazione Phoneword viene eseguita in qualsiasi piattaforma, visualizza una singola schermata che corrisponde a un elemento [`Page`](xref:Xamarin.Forms.Page) in Xamarin.Forms. L'elemento `Page` rappresenta un *ViewGroup* in Android, un *Controller di visualizzazione* in iOS o una *Pagina* nella piattaforma UWP (Universal Windows Platform). L'applicazione Phoneword crea anche un'istanza di un oggetto [`ContentPage`](xref:Xamarin.Forms.ContentPage) che rappresenta la classe `MainPage`, il cui markup XAML è illustrato nell'esempio di codice seguente:

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                         xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                         x:Class="Phoneword.MainPage">
        ...
        <StackLayout>
            <Label Text="Enter a Phoneword:" />
            <Entry x:Name="phoneNumberText" Text="1-855-XAMARIN" />
            <Button x:Name="translateButon" Text="Translate" Clicked="OnTranslate" />
            <Button x:Name="callButton" Text="Call" IsEnabled="false" Clicked="OnCall" />
        </StackLayout>
</ContentPage>
```

La classe `MainPage` usa un controllo [`StackLayout`](xref:Xamarin.Forms.StackLayout) per disporre automaticamente i controlli nella schermata indipendentemente dalle dimensioni dello schermo. Gli elementi figlio vengono posizionati uno dopo l'altro, verticalmente, nell'ordine in cui sono stati aggiunti. Il controllo `StackLayout` contiene un controllo [`Label`](xref:Xamarin.Forms.Label)per visualizzare il testo nella pagina, un controllo [`Entry`](xref:Xamarin.Forms.Entry) per accettare l'input di testo dell'utente e due controlli [`Button`](xref:Xamarin.Forms.Button) usati per eseguire codice in risposta a eventi di tocco.

Per altre informazioni su XAML in Xamarin.Forms, vedere [Xamarin.Forms XAML Basics](~/xamarin-forms/xaml/xaml-basics/index.md) (Concetti fondamentali di XAML in Xamarin.Forms).

### <a name="responding-to-user-interaction"></a>Risposta all'interazione dell'utente

Un oggetto definito in XAML può generare un evento che viene gestito nel file code-behind. Nell'esempio di codice riportato di seguito viene illustrato il metodo `OnTranslate` nel code-behind per la classe `MainPage`, eseguito in risposta alla generazione dell'evento [`Clicked`](xref:Xamarin.Forms.Button.Clicked) per il pulsante *Traduci*.

```csharp
void OnTranslate(object sender, EventArgs e)
{
    translatedNumber = Core.PhonewordTranslator.ToNumber (phoneNumberText.Text);
    if (!string.IsNullOrWhiteSpace (translatedNumber)) {
        callButton.IsEnabled = true;
        callButton.Text = "Call " + translatedNumber;
    } else {
        callButton.IsEnabled = false;
        callButton.Text = "Call";
    }
}
```

Il metodo `OnTranslate` converte la parola telefonica nel numero telefonico corrispondente e, come risposta, imposta le proprietà per il pulsante di chiamata. Il file code-behind per una classe XAML è in grado di accedere a un oggetto definito in XAML usando il nome assegnato con l'attributo `x:Name`. Il valore assegnato a questo attributo ha le stesse regole delle variabili di C#, poiché deve iniziare con una lettera o un carattere di sottolineatura e non contenere spazi incorporati.

L'associazione del pulsante di traduzione al metodo `OnTranslate` si verifica nel markup XAML per la classe `MainPage`:

```xaml
<Button x:Name="translateButon" Text="Translate" Clicked="OnTranslate" />
```

## <a name="additional-concepts-introduced-in-phoneword"></a>Altri concetti introdotti in Phoneword

L'applicazione Phoneword per Xamarin.Forms ha introdotto alcuni concetti non trattati in questo articolo. Essi includono:

- Abilitazione e disabilitazione dei pulsanti. Un oggetto [`Button`](xref:Xamarin.Forms.Button) può essere attivato o disattivato modificando la relativa proprietà [`IsEnabled`](xref:Xamarin.Forms.VisualElement.IsEnabled). Ad esempio, il codice seguente disabilita `callButton`:

    ```csharp
    callButton.IsEnabled = false;
    ```

- Visualizzazione di una finestra di dialogo di avviso. Quando l'utente preme il **pulsante** di chiamata l'applicazione Phoneword visualizza una *finestra di dialogo di avviso* che offre la possibilità di effettuare o annullare la chiamata. Per creare la finestra di dialogo viene usato il metodo [`DisplayAlert`](xref:Xamarin.Forms.Page.DisplayAlert(System.String,System.String,System.String,System.String)), come illustra l'esempio di codice seguente:

    ```csharp
    await this.DisplayAlert (
            "Dial a Number",
            "Would you like to call " + translatedNumber + "?",
            "Yes",
            "No");
    ```

- Accesso a funzionalità native usando la classe [`DependencyService`](xref:Xamarin.Forms.DependencyService). L'applicazione Phoneword usa la classe `DependencyService` per risolvere l'interfaccia `IDialer` in implementazioni della composizione telefonica specifiche della piattaforma, come illustrato nel seguente esempio di codice del progetto Phoneword:

    ```csharp
    async void OnCall (object sender, EventArgs e)
    {
        ...
        var dialer = DependencyService.Get<IDialer> ();
        ...
    }
    ```

  Per altre informazioni sulla classe [`DependencyService`](xref:Xamarin.Forms.DependencyService), vedere [Accessing Native Features with DependencyService](~/xamarin-forms/app-fundamentals/dependency-service/index.md) (Accesso alle funzionalità native con DependencyService).

- Effettuazione di una telefonata con un URL. L'applicazione Phoneword usa `OpenURL` per avviare l'app telefonica di sistema. L'URL è costituito da un prefisso `tel:` seguito dal numero di telefono da chiamare, come illustrato nel seguente esempio di codice del progetto iOS:

    ```csharp
    return UIApplication.SharedApplication.OpenUrl (new NSUrl ("tel:" + number));
    ```

- Adattamento del layout della piattaforma. La classe [`Device`](xref:Xamarin.Forms.Device) consente agli sviluppatori di personalizzare il layout e le funzionalità dell'applicazione in ogni singola piattaforma, come illustrato nell'esempio di codice seguente in cui sono usati valori diversi di [`Padding`](xref:Xamarin.Forms.Layout.Padding) per le diverse piattaforme in modo da visualizzare correttamente ogni pagina:

    ```xaml
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms" ... >
        <ContentPage.Padding>
            <OnPlatform x:TypeArguments="Thickness">
                <On Platform="iOS" Value="20, 40, 20, 20" />
                <On Platform="Android, UWP" Value="20" />
            </OnPlatform>
        </ContentPage.Padding>
        ...
    </ContentPage>
    ```

  Per altre informazioni sull'adattamento in base alla piattaforma, vedere la [classe Device](~/xamarin-forms/platform/device.md).

## <a name="testing-and-deployment"></a>Test e distribuzione

Visual Studio per Mac e Visual Studio offrono entrambi numerose opzioni per il test e la distribuzione di un'applicazione. Il debug delle applicazioni fa parte del ciclo di vita dello sviluppo delle applicazioni e consente di diagnosticare i problemi del codice. Per altre informazioni, vedere gli articoli relativi all'[impostazione di un punto di interruzione](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/ide/debugging/set_a_breakpoint), al [passaggio attraverso il codice](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/ide/debugging/step_through_code) e all'[output di informazioni alla finestra del log](https://github.com/xamarin/recipes/tree/master/Recipes/cross-platform/ide/debugging/output_information_to_log_window).

I simulatori sono un ottimo strumento per iniziare a distribuire e testare e offrono funzionalità utili per testare le applicazioni. Tuttavia, gli utenti non useranno l'applicazione finale in un simulatore, quindi le applicazioni devono essere testate nei dispositivi reali presto e spesso. Per altre informazioni sul provisioning dei dispositivi iOS, vedere [Provisioning dei dispositivi](~/ios/get-started/installation/device-provisioning/index.md). Per altre informazioni sul provisioning dei dispositivi Android, vedere [Set Up Device for Development](~/android/get-started/installation/set-up-device-for-development.md) (Configurare il dispositivo per lo sviluppo).

## <a name="summary"></a>Riepilogo

In questo articolo sono stati esaminati i concetti fondamentali dello sviluppo di applicazioni con Xamarin.Forms. Gli argomenti trattati includono l'anatomia di un'applicazione Xamarin.Forms, le nozioni di base su architettura e applicazione e l'interfaccia utente.

Nella sezione successiva di questa guida l'applicazione verrà estesa in modo da includere più schermate, per esplorare l'architettura e i concetti più avanzati di Xamarin.Forms.
