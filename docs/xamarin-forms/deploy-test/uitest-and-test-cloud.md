---
title: Automazione dei test di Xamarin.Forms con App Center
description: Per scrivere test dell'interfaccia utente da eseguire nel cloud su centinaia di dispositivi, è possibile usare il componente Xamarin UITest.
ms.prod: xamarin
ms.assetid: b674db3d-c526-4e31-a9f4-b6d6528ce7a9
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/31/2016
ms.openlocfilehash: dc43d8b5623b83be16d437e30290bc8b059be4bb
ms.sourcegitcommit: 66682dd8e93c0e4f5dee69f32b5fc5a96443e307
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2018
ms.locfileid: "35242947"
---
# <a name="automate-xamarinforms-testing-with-app-center"></a>Automatizzare i test di Xamarin.Forms con App Center

_Per scrivere test dell'interfaccia utente da eseguire nel cloud su centinaia di dispositivi, è possibile usare il componente Xamarin UITest._

## <a name="overview"></a>Panoramica

**[App Center Test](/appcenter/test-cloud/)** consente agli sviluppatori di scrivere test dell'interfaccia utente automatizzati per app iOS e Android. Con alcune modifiche di lieve entità, le app Xamarin.Forms possono essere sottoposte a test tramite Xamarin.UITest, inclusa la condivisione dello stesso codice di test. Questo articolo presenta alcuni suggerimenti specifici per l'uso di Xamarin.UITest con Xamarin.Forms.

Questa guida presuppone che l'utente abbia familiarità con Xamarin.UITest. Per acquisire familiarità con Xamarin.UITest, è consigliata la lettura delle guide seguenti:

- [Introduction to App Center Test](/appcenter/test-cloud/) (Introduzione ad App Center Test)
- [Introduction to UITest](/appcenter/test-cloud/preparing-for-upload/uitest/) (Introduzione a UITest)

Dopo avere aggiunto un progetto UITest a una soluzione Xamarin.Forms, le operazioni richieste per la scrittura e l'esecuzione dei test per un'applicazione Xamarin.Forms sono le stesse per un'applicazione Xamarin.Android o Xamarin.iOS.

## <a name="requirements"></a>Requisiti

Fare riferimento a [Xamarin.UITest](/appcenter/test-cloud/uitest/) per confermare che il progetto è pronto per i test dell'interfaccia utente automatizzati.

## <a name="adding-uitest-support-to-xamarinforms-apps"></a>Aggiunta del supporto UITest nelle app Xamarin.Forms

UITest consente di automatizzare l'interfaccia utente attivando controlli sullo schermo ed eseguendo input in qualsiasi posizione in cui l'utente interagisca normalmente con l'applicazione. Per abilitare test che consentano di *premere un pulsante* o *immettere testo in una casella*, il codice di test dovrà essere in grado di identificare i controlli sullo schermo.

Per consentire al codice UITest di fare riferimento ai controlli, ogni controllo ha bisogno di un identificatore univoco. In Xamarin.Forms il metodo consigliato per impostare questo identificatore è tramite la proprietà `AutomationId`, come illustrato di seguito:

```csharp
var b = new Button {
    Text = "Click me",
    AutomationId = "MyButton"
};
var l = new Label {
    Text = "Hello, Xamarin.Forms!",
    AutomationId = "MyLabel"
};
```

La proprietà `AutomationId` può essere impostata anche in XAML:

```xaml
<Button x:Name="b" AutomationId="MyButton" Text="Click me"/>
<Label x:Name="l" AutomationId="MyLabel" Text="Hello, Xamarin.Forms!" />
```

Un `AutomationId` univoco deve essere aggiunto a tutti i controlli richiesti per i test (tra cui pulsanti, voci di testo ed etichette sul cui valore potrebbe essere necessario eseguire una query).

> [!NOTE]
> Si noti che verrà generata un'eccezione `InvalidOperationException` se viene effettuato un tentativo di impostare la proprietà `AutomationId` di un `Element` più di una volta.

### <a name="ios-application-project"></a>Progetto di applicazione iOS

Per eseguire test in iOS, il [pacchetto NuGet Xamarin Test Cloud Agent](https://www.nuget.org/packages/Xamarin.TestCloud.Agent/) deve essere aggiunto al progetto. Una volta aggiunto, copiare il codice seguente nel metodo `AppDelegate.FinishedLaunching`:

```csharp
#if ENABLE_TEST_CLOUD
// requires Xamarin Test Cloud Agent
Xamarin.Calabash.Start();
#endif
```

L'assembly Calabash usa API Apple non pubbliche che comporteranno l'esclusione delle app da App Store. Tuttavia, il linker Xamarin.iOS rimuoverà assembly Calabash dall'IPA finale se non vi viene fatto riferimento in modo esplicito dal codice.

> [!NOTE]
>  Le build di rilascio non dispongono della variabile del compilatore `ENABLE_TEST_CLOUD` e ciò comporta la rimozione dell'assembly Calabash dal bundle dell'app. Tuttavia, le compilazioni di debug dispongono della direttiva del compilatore definita, impedendo al linker di rimuovere l'assembly.

La schermata seguente mostra la variabile del compilatore `ENABLE_TEST_CLOUD` impostata per le compilazioni di debug:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

![](uitest-and-test-cloud-images/12-compiler-directive-vs.png "Opzioni di compilazione")

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio per Mac](#tab/vsmac)

![](uitest-and-test-cloud-images/11-compiler-directive-xs.png "Opzioni del compilatore")

-----

### <a name="android-application-project"></a>Progetto di applicazione Android

A differenza di iOS, i progetti Android non necessitano di alcun codice di avvio speciale.

## <a name="writing-uitests"></a>Scrittura di test dell'interfaccia utente

Per informazioni sulla scrittura di test dell'interfaccia utente, fare riferimento alla [documentazione relativa a UITest](/appcenter/test-cloud/preparing-for-upload/uitest/). I passaggi riportati di seguito sono un riepilogo e descrivono nello specifico come viene compilata la [demo Xamarin.Forms **UsingUITest**](https://developer.xamarin.com/samples/xamarin-forms/UsingUITest/).

### <a name="use-automationid-in-the-xamarinforms-ui"></a>Usare AutomationId nell'interfaccia utente di Xamarin.Forms

Prima di scrivere qualsiasi test dell'interfaccia utente, l'interfaccia utente dell'applicazione Xamarin.Forms deve essere gestibile tramite script. Verificare che tutti i controlli nell'interfaccia utente dispongano di un `AutomationId`, in modo che sia possibile farvi riferimento nel codice di test.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio per Mac](#tab/vsmac)

### <a name="adding-a-uitest-project-to-a-new-solution"></a>Aggiunta di un progetto UITest a una nuova soluzione

Quando si crea un nuovo progetto Xamarin.Forms in Visual Studio per Mac, è possibile aggiungere un nuovo progetto UITest alla soluzione selezionando **Xamarin Test Cloud: Aggiungi un progetto di test dell'interfaccia utente automatizzato**:

![](uitest-and-test-cloud-images/01-new-solution-xs.png "Configurazione del nuovo progetto")

La nuova soluzione verrà configurata automaticamente per l'esecuzione di Xamarin.UITests nell'applicazione Xamarin.Forms.

-----

#### <a name="referring-to-the-automationid-in-uitests"></a>Riferimento ad AutomationId nei test dell'interfaccia utente

Durante la scrittura di test dell'interfaccia utente, il valore `AutomationId` viene esposto in modo differente in ciascuna piattaforma:

- **iOS** usa il campo `id`.
- **Android** usa il campo `label`.

Per scrivere test dell'interfaccia utente multipiattaforma che troveranno l'`AutomationId` sia in iOS che in Android, usare la query di prova `Marked`:

```csharp
app.Query(c=>c.Marked("MyButton"))
```

Può essere usata anche la forma abbreviata `app.Query("MyButton")`.

### <a name="adding-a-uitest-project-to-an-existing-solution"></a>Aggiunta di un progetto UITest a una soluzione esistente

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Visual Studio include un modello per l'aggiunta di un progetto Xamarin.UITest a una soluzione Xamarin.Forms esistente:

1. Fare clic con il pulsante destro del mouse sulla soluzione e selezionare **File > Nuovo progetto**.
1. Dai modelli **Visual C#** selezionare la categoria **Test**. Selezionare il modello **App per test dell'interfaccia utente > Multipiattaforma**:

    ![](uitest-and-test-cloud-images/08-new-uitest-project-vs.png "Aggiunta di un nuovo progetto")

    Verrà aggiunto un nuovo progetto alla soluzione con i pacchetti NuGet **NUnit**, **Xamarin.UITest** e **NUnitTestAdapter**:

    ![](uitest-and-test-cloud-images/09-new-uitest-project-xs.png "Gestione pacchetti NuGet")

    **NUnitTestAdapter** è un test runner di terze parti che consente a Visual Studio di eseguire test NUnit da Visual Studio.

    Il nuovo progetto include anche due classi. **AppInitializer** contiene codice per inizializzare e configurare i test. L'altra classe, **Tests**, contiene il codice standard per avviare i test dell'interfaccia utente.

1. Aggiungere un riferimento al progetto dal progetto UITest a quello Xamarin.Android:

    ![](uitest-and-test-cloud-images/10-test-apps-vs.png "Project Reference Manager")

    In questo modo **NUnitTestAdapter** potrà eseguire i test dell'interfaccia utente per l'app Android da Visual Studio.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio per Mac](#tab/vsmac)

È possibile aggiungere manualmente un nuovo progetto Xamarin.UITest a una soluzione esistente:

1. Per iniziare, aggiungere un nuovo progetto selezionando la soluzione e facendo clic su **File > Aggiungi nuovo progetto**. Nella finestra di dialogo **Nuovo progetto** selezionare **Multipiattaforma > Test > Xamarin Test Cloud > App per test interfaccia utente**:

    ![](uitest-and-test-cloud-images/02-new-uitest-project-xs.png "Scelta di un modello")

    Verrà aggiunto un nuovo progetto che dispone già dei pacchetti NuGet **NUnit** e **Xamarin.UITest** nella soluzione:

    ![](uitest-and-test-cloud-images/03-new-uitest-project-xs.png "Pacchetti NuGet Xamarin UITest")

    Il nuovo progetto include anche due classi. **AppInitializer** contiene codice per inizializzare e configurare i test. L'altra classe, **Tests**, contiene il codice standard per avviare i test dell'interfaccia utente.

1. Selezionare **Visualizza > Riquadri > Unit test** per visualizzare il riquadro Unit test. Espandere **UsingUITest > UsingUITest.UITests > App di test**:

    ![](uitest-and-test-cloud-images/04-unit-test-pad-xs.png "Riquadro Unit test")

1. Fare clic con il pulsante destro del mouse su **App di test**, fare clic su **Aggiungi progetto app**e selezionare i progetti iOS e Android nella finestra di dialogo visualizzata:

    ![](uitest-and-test-cloud-images/05-add-test-apps-xs.png "Finestra di dialogo App di test")

    Il riquadro **Unit test** dovrebbe ora includere un riferimento ai progetti iOS e Android. In questo modo il test runner di Visual Studio per Mac potrà eseguire localmente i test dell'interfaccia utente nei due progetti Xamarin.Forms.

#### <a name="adding-uitest-to-the-ios-app"></a>Aggiunta di UITest all'app iOS

È necessario apportare alcune modifiche aggiuntive all'applicazione iOS prima di poter usare Xamarin.UITest:

1. Aggiungere il pacchetto NuGet **Xamarin Test Cloud Agent**. Fare clic con il pulsante destro del mouse su **Pacchetti**, selezionare **Aggiungi pacchetti**, cercare **Xamarin Test Cloud Agent** in NuGet e aggiungerlo al progetto Xamarin.iOS:

    ![](uitest-and-test-cloud-images/07-add-test-cloud-agent-xs.png "Aggiunta di pacchetti NuGet")

1. Modificare il metodo `FinishedLaunching` della classe **AppDelegate** per inizializzare Xamarin Test Cloud Agent all'avvio dell'applicazione iOS e per impostare la proprietà `AutomationId` delle proprietà delle visualizzazioni. Il metodo `FinishedLaunching` dovrebbe essere simile all'esempio di codice seguente:

```csharp
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
        #if ENABLE_TEST_CLOUD
        Xamarin.Calabash.Start();
        #endif

        global::Xamarin.Forms.Forms.Init();

        LoadApplication(new App());

        return base.FinishedLaunching(app, options);
}
```

-----

Dopo avere aggiunto Xamarin.UITest alla soluzione Xamarin.Forms, è possibile creare test dell'interfaccia utente, eseguirli in locale e inviarli a Xamarin Test Cloud.

## <a name="summary"></a>Riepilogo

Le applicazioni Xamarin.Forms possono essere facilmente sottoposte a test con **Xamarin.UITest** usando un semplice meccanismo per esporre l'`AutomationId` come identificatore della visualizzazione univoco per l'automazione di test. Dopo avere aggiunto un progetto UITest a una soluzione Xamarin.Forms, le operazioni richieste per la scrittura e l'esecuzione dei test per un'applicazione Xamarin.Forms sono le stesse per un'applicazione Xamarin.Android o Xamarin.iOS.

Per informazioni su come inviare test ad App Center Test, vedere [Submitting UITests](/appcenter/test-cloud/preparing-for-upload/uitest/) (Invio di test dell'interfaccia utente). Per altre informazioni su UITest, fare riferimento alla [documentazione di App Center Test](/appcenter/test-cloud/).


## <a name="related-links"></a>Collegamenti correlati

- [UITestSample](https://developer.xamarin.com/samples/xamarin-forms/UsingUITest/)
- [Esempi di Xamarin.Forms](https://github.com/xamarin/xamarin-forms-samples)
- [App Center Test](/appcenter/test-cloud/)
- [Xamarin.UITest](/appcenter/test-cloud/uitest/)
- [NUnit](http://www.nunit.org)
