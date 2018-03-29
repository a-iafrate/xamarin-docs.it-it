---
title: Aggiunta di un'App di Windows universale Platform (UWP)
description: "In questo articolo viene illustrato come aggiungere un progetto di app UWP a una soluzione xamarin. Forms che è stata creata in Visual Studio per Mac."
ms.topic: article
ms.prod: xamarin
ms.assetid: 34AAA045-64B8-4FDE-BB49-3FF0B4FFA17C
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/16/2016
ms.openlocfilehash: 4a8d2934c4fbdc5b748014cb7dc9a121ade8c37e
ms.sourcegitcommit: 8e722d72c5d1384889f70adb26c5675544897b1f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2018
---
# <a name="adding-a-universal-windows-platform-uwp-app"></a>Aggiunta di un'App di Windows universale Platform (UWP)

_In questo articolo viene illustrato come aggiungere un progetto di app UWP a una soluzione xamarin. Forms che è stata creata in Visual Studio per Mac._

È consigliabile eseguire **Visual Studio 2017** su **Windows 10** per compilare App UWP. Per ulteriori informazioni sulla piattaforma Windows universale, vedere [Introduzione alla piattaforma Windows Universal](/windows/uwp/get-started/universal-application-platform-guide/).

UWP è disponibile in xamarin. Forms 2.1 e versioni successive e Xamarin.Forms.Maps è supportato in xamarin. Forms 2.2 e versioni successive.

Controllare il <a href="#troubleshooting">risoluzione dei problemi</a> sezione per suggerimenti utili.

Seguire queste istruzioni per aggiungere un'app UWP che verrà eseguiti nel desktop, Tablet e telefoni Windows 10:

 1 . Pulsante destro del mouse sulla soluzione e selezionare **Aggiungi > Nuovo progetto...**  e aggiungere un **App vuota (Windows universale)** progetto:

  ![](universal-images/add-wu.png "Aggiungere una finestra di dialogo Nuovo progetto")

 2 . Nel **nuovo progetto di piattaforma Windows Universal** finestra di dialogo, selezionare le versioni minima e di destinazione di Windows 10 in cui verrà eseguita l'app:

  ![](universal-images/target-version.png "Finestra Nuovo progetto di piattaforma Windows universale")

 3 . Fare clic sul progetto UWP e selezionare **Gestisci pacchetti NuGet...**  e aggiungere il **xamarin. Forms** pacchetto. Verificare che gli altri progetti nella soluzione vengono aggiornati anche per la stessa versione del pacchetto xamarin. Forms.

 4 . Verificare che il nuovo progetto UWP sarà compilato nel **compilazione > Configuration Manager** finestra (ciò probabilmente non si sono verificati per impostazione predefinita). Segni di graduazione di **compilare** e **Distribuisci** caselle per il progetto universale:

  [![](universal-images/configuration-sml.png "Finestra di Configuration Manager")](universal-images/configuration.png#lightbox "finestra Configuration Manager")

 5 . Pulsante destro del mouse sul progetto e selezionare **Aggiungi > riferimento** e creare un riferimento al progetto di applicazione xamarin. Forms (PCL, .NET Standard o progetto condiviso).

  ![](universal-images/addref-sml.png "Finestra di dialogo Gestione riferimenti")

 6 . Nel progetto UWP, modificare **App.xaml.cs** per includere il `Init` chiamata al metodo all'interno di `OnLaunched` metodo alla riga 52:

```csharp
// under this line
rootFrame.NavigationFailed += OnNavigationFailed;
// add this line
Xamarin.Forms.Forms.Init (e); // requires the `e` parameter
```

 7 . Nel progetto UWP, modificare **MainPage. XAML** rimuovendo il `Grid` contenuti all'interno di `Page` elemento.

 8 . In **MainPage. XAML**, aggiungere un nuovo `xmlns` voce per `Xamarin.Forms.Platform.UWP`:

```csharp
xmlns:forms="using:Xamarin.Forms.Platform.UWP"
```

 9 . In **MainPage. XAML**, modificare la radice `<Page` elemento `<forms:WindowsPage`:

```xaml
<forms:WindowsPage
...
   xmlns:forms="using:Xamarin.Forms.Platform.UWP"
...
</forms:WindowsPage>
```

 10 . Nel progetto UWP, modificare **MainPage.xaml.cs** per rimuovere il `: Page` identificatore di ereditarietà per il nome di classe (poiché ora erediterà dalla `WindowsPage` a causa della modifica apportata nel passaggio precedente):

```csharp
public sealed partial class MainPage  // REMOVE ": Page"
```

 11 . In **MainPage.xaml.cs**, aggiungere il `LoadApplication` chiamare il `MainPage` costruttore per avviare l'app xamarin. Forms:

```csharp
// below this existing line
this.InitializeComponent();
// add this line
LoadApplication(new YOUR_NAMESPACE.App());
```

<!--
11 . Double-click **Package.appxmanifest** to set these capabilities
  that are often required:

  Capabilities set:

  * Internet (Client)
  * Location
-->

12 . Aggiungere risorse locali (ad es. file di immagine) nei progetti di piattaforma esistenti che sono necessari.

<a name="troubleshooting" />

## <a name="troubleshooting"></a>Risoluzione dei problemi

<a name="target-invocation-exception" />

### <a name="target-invocation-exception-when-using-compile-with-net-native-tool-chain"></a>"Eccezione di chiamata di destinazione" quando si utilizza "Per la compilazione con una catena di strumenti nativo .NET"

Se l'app UWP fa riferimento a più assembly (ad esempio librerie di controlli terze o l'app stessa viene suddivisa in più raccolte), xamarin. Forms potrebbe non essere possibile caricare gli oggetti da tali assembly (ad esempio, il renderer personalizzato).

Questa situazione può verificarsi quando si utilizza il **esegue la compilazione con una catena di strumenti .NET Native** che è un'opzione per App UWP nel **proprietà > compilare > Generale** finestra per il progetto.

È possibile risolvere il problema utilizzando un overload del metodo UWP specifiche di `Forms.Init` chiamare in **App.xaml.cs** come illustrato nel codice seguente (è necessario sostituire `ClassInOtherAssembly` con una classe effettiva fa riferimento il codice):

```csharp
// You'll need to add `using System.Reflection;`
List<Assembly> assembliesToInclude = new List<Assembly>();

// Now, add in all the assemblies your app uses
assembliesToInclude.Add(typeof (ClassInOtherAssembly).GetTypeInfo().Assembly);

// Also do this for all your other 3rd party libraries
Xamarin.Forms.Forms.Init(e, assembliesToInclude);
// replaces Xamarin.Forms.Forms.Init(e);
```

Aggiungere un riferimento a ogni assembly che fa riferimento l'app.

#### <a name="dependency-services-and-net-native-compilation"></a>Compilazione nativa .NET e i servizi di dipendenza

Con .NET Native può non riuscire per risolvere i servizi di dipendenza definite all'esterno dell'eseguibile principale dell'applicazione (ad esempio un progetto separato o libreria) di build di rilascio.

Utilizzare il `DependencyService.Register<T>()` metodo registrare manualmente classi del servizio di dipendenza. In base all'esempio precedente, aggiungere il metodo register simile al seguente:

```csharp
Xamarin.Forms.Forms.Init(e, assembliesToInclude);
Xamarin.Forms.DependencyService.Register<ClassInOtherAssembly>(); // add this
```