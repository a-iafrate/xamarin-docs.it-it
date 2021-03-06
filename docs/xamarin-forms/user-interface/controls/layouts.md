---
title: Layout di xamarin. Forms
description: Layout di xamarin. Forms vengono utilizzati per la composizione di controlli dell'interfaccia utente nelle strutture visual. Questo articolo elenca i layout inclusi in xamarin. Forms.
ms.prod: xamarin
ms.assetid: F4180997-BA21-453A-9958-D1E2940DF050
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/21/2018
ms.openlocfilehash: 224eb2ee3958e5979382a3dc5e70110fdce51879
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2018
ms.locfileid: "38994602"
---
# <a name="xamarinforms-layouts"></a>Layout di xamarin. Forms

_Layout di xamarin. Forms vengono utilizzati per comporre i controlli dell'interfaccia utente in strutture visual._

Il [ `Layout` ](xref:Xamarin.Forms.Layout) e [ `Layout<T>` ](xref:Xamarin.Forms.Layout`1) classi in xamarin. Forms sono specializzati sottotipi di viste che fungono da contenitori per le visualizzazioni e altri layout. Il `Layout` stessa classe deriva da [ `View` ](views.md). Oggetto `Layout` derivato contiene in genere per la logica per impostare la posizione e dimensioni degli elementi figlio nelle applicazioni xamarin. Forms.

[![I tipi di Layout di xamarin. Forms](layouts-images/layouts-sml.png "tipi di Layout di xamarin. Forms")](layouts-images/layouts.png#lightbox "i tipi di Layout di xamarin. Forms")

Le classi che derivano da `Layout` possono essere suddivisi in due categorie:

## <a name="layouts-with-single-content"></a>Layout con contenuto singolo

Tali classi derivano da [ `Layout` ](xref:Xamarin.Forms.Layout), che definisce [ `Padding` ](xref:Xamarin.Forms.Layout.Padding) e [ `IsClippedToBounds` ](xref:Xamarin.Forms.Layout.IsClippedToBounds) proprietà.

<a name="contentView" />

### <a name="contentview"></a>ContentView

|     |     |
| --- | --- |
| [`ContentView`](xref:Xamarin.Forms.ContentView) contiene un singolo elemento figlio che viene impostato con il [ `Content` ](xref:Xamarin.Forms.ContentView.Content) proprietà. Il `Content` proprietà può essere impostata su qualsiasi `View` derivati, inclusi altri `Layout` derivati. `ContentView` viene principalmente utilizzato come un elemento strutturale e funge da classe base per [ `Frame` ](#frame).<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.ContentView) | [![Esempio ContentView](layouts-images/ContentView.png "esempio ContentView")](layouts-images/ContentView-Large.png#lightbox "ContentView esempio")<br />[Codice c# per questa pagina](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ContentViewDemoPage.cs) / [pagina XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ContentViewDemoPage.xaml) |
|     |     |

<a named="frame" />

### <a name="frame"></a>Frame

|     |     |
| --- | --- |
| Il [ `Frame` ](xref:Xamarin.Forms.Frame) deriva dalla classe [ `ContentView` ](#contentView) e visualizza una cornice rettangolare intorno al relativo elemento figlio. `Frame` è un valore predefinito [ `Padding` ](xref:Xamarin.Forms.Layout.Padding) pari a 20 e definisce anche [ `OutlineColor` ](xref:Xamarin.Forms.Frame.OutlineColor), [ `CornerRadius` ](xref:Xamarin.Forms.Frame.CornerRadius), e [ `HasShadow` ](xref:Xamarin.Forms.Frame.HasShadow)delle proprietà.<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.Frame) | [![Esempio di frame](layouts-images/Frame.png "Frame riportato")](layouts-images/Frame-Large.png#lightbox "Frame esempio")<br />[Codice c# per questa pagina](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/FrameDemoPage.cs) / [pagina XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/FrameDemoPage.xaml) |
|     |     |

<a name="scrollView" />

### <a name="scrollview"></a>ScrollView

|     |     |
| --- | --- |
| [`ScrollView`](xref:Xamarin.Forms.ScrollView) è in grado di scorrere il contenuto. Impostare il [ `Content` ](xref:Xamarin.Forms.ScrollView.Content) proprietà su una vista o a un layout troppo grande per adattarlo sullo schermo. (Il contenuto di un `ScrollView` molto spesso è una [ `StackLayout` ](#stackLayout).) Impostare il [ `Orientation` ](xref:Xamarin.Forms.ScrollView.Orientation) proprietà che indica se lo scorrimento dovrebbe essere verticale, orizzontale, o entrambi.<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.ScrollView) / [Guida](~/xamarin-forms/user-interface/layouts/scroll-view.md) / [esempio](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![Esempio di ScrollView](layouts-images/ScrollView.png "esempio ScrollView")](layouts-images/ScrollView-Large.png#lightbox "esempio ScrollView")<br />[Codice c# per questa pagina](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ScrollViewDemoPage.cs) / [pagina XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ScrollViewDemoPage.xaml) |
|     |     |

### <a name="templatedview"></a>TemplatedView

|     |     |
| --- | --- |
| [`TemplatedView`](xref:Xamarin.Forms.TemplatedView) Visualizza il contenuto con un modello di controllo ed è la classe base per [ `ContentView` ](#contentView).<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.TemplatedView) / [Guida](~/xamarin-forms/app-fundamentals/templates/control-templates/index.md) | [![Esempio TemplatedView](layouts-images/TemplatedView.png "esempio TemplatedView")](layouts-images/TemplatedView.png#lightbox "TemplatedView esempio") |
|     |     |

### <a name="contentpresenter"></a>ContentPresenter

|     |     |
| --- | --- |
| [`ContentPresenter`](xref:Xamarin.Forms.ContentPresenter) rappresenta un gestore di layout per le viste basate su modelli, utilizzato all'interno di un [ `ControlTemplate` ](xref:Xamarin.Forms.ControlTemplate) per contrassegnare in cui viene visualizzato il contenuto che deve essere presentato.<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.ContentPresenter) / [Guida](~/xamarin-forms/app-fundamentals/templates/control-templates/index.md) | [![Esempio di ContentPresenter](layouts-images/ContentPresenter.png "esempio ContentPresenter")](layouts-images/ContentPresenter.png#lightbox "ContentPresenter esempio") |
|     |     |

## <a name="layouts-with-multiple-children"></a>Layout con più elementi figlio

Tali classi derivano da [ `Layout<View>` ](xref:Xamarin.Forms.Layout`1).

<a name="stackLayout" />

### <a name="stacklayout"></a>StackLayout

|     |     |
| --- | --- |
| [`StackLayout`](xref:Xamarin.Forms.StackLayout) Posiziona gli elementi figlio in uno stack orizzontalmente o verticalmente in base il [ `Orientation` ](xref:Xamarin.Forms.StackLayout.Orientation) proprietà. Il [ `Spacing` ](xref:Xamarin.Forms.StackLayout.Spacing) proprietà determina la spaziatura tra gli elementi figlio e ha un valore predefinito pari a 6.<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.StackLayout) / [Guida](~/xamarin-forms/user-interface/layouts/stack-layout.md) / [esempio](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/)| [![Esempio StackLayout](layouts-images/StackLayout.png "StackLayout riportato")](layouts-images/StackLayout-Large.png#lightbox "StackLayout esempio")<br />[Codice c# per questa pagina](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/StackLayoutDemoPage.cs) / [pagina XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/StackLayoutDemoPage.xaml) |
|     |     |

<a name="grid" />

### <a name="grid"></a>Grid

|     |     |
| --- | --- |
| [`Grid`](xref:Xamarin.Forms.Grid) Posiziona gli elementi figlio in una griglia di righe e colonne. Posizione del figlio sia indicato utilizzando il [le proprietà associate](~/xamarin-forms/xaml/attached-properties.md) [ `Row` ](xref:Xamarin.Forms.Grid.RowProperty), [ `Column` ](xref:Xamarin.Forms.Grid.ColumnProperty), [ `RowSpan` ](xref:Xamarin.Forms.Grid.RowSpanProperty), e [ `ColumnSpan` ](xref:Xamarin.Forms.Grid.ColumnSpanProperty).<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.Grid) / [Guida](~/xamarin-forms/user-interface/layouts/grid.md) / [esempio](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![Esempio di Grid](layouts-images/Grid.png "esempio di Grid")](layouts-images/Grid-Large.png#lightbox "di griglia di esempio")<br />[Codice c# per questa pagina](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/GridDemoPage.cs) / [pagina XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/GridDemoPage.xaml) |
|     |     |

### <a name="absolutelayout"></a>AbsoluteLayout

|     |     |
| --- | --- |
| [`AbsoluteLayout`](xref:Xamarin.Forms.AbsoluteLayout) Posiziona gli elementi figlio in percorsi specifici rispetto al padre. Posizione del figlio sia indicato utilizzando il [le proprietà associate](~/xamarin-forms/xaml/attached-properties.md) [ `LayoutBounds` ](xref:Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty) e [ `LayoutFlags` ](xref:Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty). Un `AbsoluteLayout` è utile per l'animazione le posizioni delle visualizzazioni.<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.AbsoluteLayout) / [Guida](~/xamarin-forms/user-interface/layouts/absolute-layout.md) / [esempio](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![Esempio AbsoluteLayout](layouts-images/AbsoluteLayout.png "esempio AbsoluteLayout")](layouts-images/AbsoluteLayout-Large.png#lightbox "AbsoluteLayout esempio")<br />[Codice c# per questa pagina](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/AbsoluteLayoutdDemoPage.cs) / [pagina XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/AbsoluteLayoutDemoPage.xaml) con [code-behind](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/AbsoluteLayoutDemoPage.xaml.cs) |
|     |     |

### <a name="relativelayout"></a>RelativeLayout

|     |     |
| --- | --- |
| [`RelativeLayout`](xref:Xamarin.Forms.RelativeLayout) Posiziona gli elementi figlio relativa al `RelativeLayout` stesso o per i nodi di pari livello. Posizione del figlio sia indicato utilizzando il [le proprietà associate](~/xamarin-forms/xaml/attached-properties.md) impostati su oggetti di tipo [ `Constraint` ](xref:Xamarin.Forms.Constraint) e [ `BoundsConstraint` ](xref:Xamarin.Forms.Constraint).<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.RelativeLayout) / [Guida](~/xamarin-forms/user-interface/layouts/relative-layout.md) / [esempio](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![Esempio RelativeLayout](layouts-images/RelativeLayout.png "esempio RelativeLayout")](layouts-images/RelativeLayout-Large.png#lightbox "RelativeLayout esempio")<br />[Codice c# per questa pagina](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/RelativeLayoutDemoPage.cs) / [pagina XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/RelativeLayoutDemoPage.xaml) |
|     |     |

### <a name="flexlayout"></a>FlexLayout

|     |     |
| --- | --- |
| [`FlexLayout`](xref:Xamarin.Forms.FlexLayout) è basato sul foglio di stile CSS [flessibile Box Layout Module](http://www.w3.org/TR/css-flexbox-1/), noto come _flex layout_ oppure _flex-finestra_. `FlexLayout` definisce le proprietà associabili sei e cinque proprietà associabili associate che gli elementi figlio possano essere disposti in pila o stato eseguito il wrapping con molte opzioni di allineamento e orientamento.<br /><br />[Documentazione dell'API](xref:Xamarin.Forms.FlexLayout) / [Guida](~/xamarin-forms/user-interface/layouts/flex-layout.md) / [esempio](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/FlexLayoutDemos/) | [![Esempio FlexLayout](layouts-images/FlexLayout.png "esempio FlexLayout")](layouts-images/FlexLayout-Large.png#lightbox "FlexLayout esempio")<br />[Codice c# per questa pagina](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/FlexLayoutDemoPage.cs) / [pagina XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/FlexLayoutDemoPage.xaml) |
|     |     |

## <a name="related-links"></a>Collegamenti correlati

- [Introduction to Xamarin.Forms (Introduzione a Xamarin.Forms)](~/xamarin-forms/get-started/introduction-to-xamarin-forms.md)
- [Esempio di xamarin. Forms FormsGallery](https://developer.xamarin.com/samples/FormsGallery/)
- [Esempi di Xamarin.Forms](https://developer.xamarin.com/samples/xamarin-forms/all/)
- [Documentazione di xamarin. Forms API](https://docs.microsoft.com/dotnet/api/xamarin.forms?view=xamarin-forms)
