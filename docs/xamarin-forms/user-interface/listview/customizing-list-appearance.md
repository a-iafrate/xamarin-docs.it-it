---
title: Personalizzazione dell'aspetto di ListView
description: Questo articolo illustra come personalizzare ListView che nelle applicazioni xamarin. Forms usando le intestazioni, piè di pagina, gruppi e le celle di altezza variabile.
ms.prod: xamarin
ms.assetid: DC8009B0-4371-4D60-885A-5362FC7EE3E5
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 03/08/2016
ms.openlocfilehash: 1326a1326b4a88459e4e0a01ef590e770e3a88c0
ms.sourcegitcommit: 6e955f6851794d58334d41f7a550d93a47e834d2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2018
ms.locfileid: "38997348"
---
# <a name="customizing-listview-appearance"></a>Personalizzazione dell'aspetto di ListView

`ListView` sono disponibili opzioni per controllare la presentazione dell'elenco globale, oltre a sottostante `ViewCell`s. Le opzioni includono:

- [**Raggruppamento** ](#Grouping) &ndash; raggruppare gli elementi in ListView per semplificare l'esplorazione e organizzazione migliorata.
- [**Informazioni sulle intestazioni e piè di pagina** ](#Headers_and_Footers) &ndash; visualizzare le informazioni all'inizio e alla fine della visualizzazione che supporta lo scorrimento con gli altri elementi.
- [**Separatori di riga** ](#Row_Separators) &ndash; mostrare o nascondere le righe di separazione tra gli elementi.
- [**Righe di altezza variabile** ](#Row_Heights) &ndash; per impostazione predefinita tutte le righe sono della stessa altezza, ma può essere modificato per consentire le righe con altezze diverse da visualizzare.

<a name="Grouping" />

## <a name="grouping"></a>Raggruppamento
Spesso, grandi set di dati può diventare difficile da gestire quando viene visualizzata in un elenco a scorrimento continuo. L'abilitazione di raggruppamento può migliorare l'esperienza utente in questi casi organizzare meglio il contenuto e attivando controlli specifici della piattaforma che semplificano l'esplorazione dei dati.

Quando il raggruppamento viene attivato per un `ListView`, viene aggiunta una riga di intestazione per ogni gruppo.

Per abilitare il raggruppamento:

- Creare un elenco di elenchi (un elenco di gruppi, ogni gruppo da un elenco di elementi).
- Impostare il `ListView`del `ItemsSource` a tale elenco.
- Impostare `IsGroupingEnabled` su true.
- Impostare [ `GroupDisplayBinding` ](xref:Xamarin.Forms.ListView.GroupDisplayBinding) da associare alla proprietà dei gruppi di cui viene utilizzata come titolo del gruppo.
- [Facoltativo] Impostare [ `GroupShortNameBinding` ](xref:Xamarin.Forms.ListView.GroupShortNameBinding) da associare alla proprietà dei gruppi di cui viene utilizzata come il nome breve per il gruppo. Il nome breve viene usato per il jump List (colonna destra in iOS).

Iniziare creando una classe per i gruppi:

```csharp
public class PageTypeGroup : List<PageModel>
    {
        public string Title { get; set; }
        public string ShortName { get; set; } //will be used for jump lists
        public string Subtitle { get; set; }
        private PageTypeGroup(string title, string shortName)
        {
            Title = title;
            ShortName = shortName;
        }

        public static IList<PageTypeGroup> All { private set; get; }
    }
```

Nel codice precedente, `All` è riportato l'elenco che verrà assegnato al nostro ListView come origine del binding. `Title` e `ShortName` sono le proprietà che verranno usate per le intestazioni di gruppo.

In questa fase, `All` è un elenco vuoto. Aggiungere un costruttore statico, in modo che verrà popolato l'elenco all'avvio del programma:

```csharp
static PageTypeGroup()
{
    List<PageTypeGroup> Groups = new List<PageTypeGroup> {
            new PageTypeGroup ("Alfa", "A"){
                new PageModel("Amelia", "Cedar", new switchCellPage(),""),
                new PageModel("Alfie", "Spruce", new switchCellPage(), "grapefruit.jpg"),
                new PageModel("Ava", "Pine", new switchCellPage(), "grapefruit.jpg"),
                new PageModel("Archie", "Maple", new switchCellPage(), "grapefruit.jpg")
            },
            new PageTypeGroup ("Bravo", "B"){
                new PageModel("Brooke", "Lumia", new switchCellPage(),""),
                new PageModel("Bobby", "Xperia", new switchCellPage(), "grapefruit.jpg"),
                new PageModel("Bella", "Desire", new switchCellPage(), "grapefruit.jpg"),
                new PageModel("Ben", "Chocolate", new switchCellPage(), "grapefruit.jpg")
            }
        }
        All = Groups; //set the publicly accessible list
}
```

Nel codice precedente è anche possibile chiamare `Add` sugli elementi della `groups`, che sono istanze del tipo `PageTypeGroup`. Ciò è possibile in quanto `PageTypeGroup` eredita da `List<PageModel>`. Questo è un esempio dell'elenco di elenchi modello indicato in precedenza.

Ecco il XAML per la visualizzazione elenco raggruppato:

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
x:Class="DemoListView.GroupingViewPage"
    <ContentPage.Content>
        <ListView  x:Name="GroupedView"
        GroupDisplayBinding="{Binding Title}"
        GroupShortNameBinding="{Binding ShortName}"
        IsGroupingEnabled="true">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding Title}"
                     Detail="{Binding Subtitle}" />
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    </ContentPage.Content>
</ContentPage>
```

L'opzione produce quanto segue:

![](customizing-list-appearance-images/grouping-depth.png "Esempio di raggruppamento di ListView")

Si noti che è necessario:

- Impostare `GroupShortNameBinding` per il `ShortName` proprietà definita nella classe gruppo
- Impostare `GroupDisplayBinding` per il `Title` proprietà definita nella classe gruppo
- Impostare `IsGroupingEnabled` su true
- Modificare il `ListView`del `ItemsSource` all'elenco di raggruppamenti

### <a name="customizing-grouping"></a>Personalizzazione di raggruppamento

Se è stato abilitato il raggruppamento nell'elenco, è anche possibile personalizzare l'intestazione di gruppo.

Simile al modo in cui il `ListView` ha un `ItemTemplate` per la definizione delle modalità di visualizzazione, le righe `ListView` ha un `GroupHeaderTemplate`.

Di seguito è riportato un esempio di personalizzazione di intestazione del gruppo in XAML:

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
x:Class="DemoListView.GroupingViewPage">
    <ContentPage.Content>
        <ListView x:Name="GroupedView"
         GroupDisplayBinding="{Binding Title}"
         GroupShortNameBinding="{Binding ShortName}"
         IsGroupingEnabled="true">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding Title}"
                    Detail="{Binding Subtitle}"
                    TextColor="#f35e20"
                    DetailColor="#503026" />
                </DataTemplate>
            </ListView.ItemTemplate>
            <!-- Group Header Customization-->
            <ListView.GroupHeaderTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding Title}"
                    Detail="{Binding ShortName}"
                    TextColor="#f35e20"
                    DetailColor="#503026" />
                </DataTemplate>
            </ListView.GroupHeaderTemplate>
            <!-- End Group Header Customization -->
        </ListView>
    </ContentPage.Content>
</ContentPage>
```

<a name="Headers_and_Footers" />

## <a name="headers-and-footers"></a>Intestazioni e piè di pagina
È possibile che un ListView presentare un'intestazione e piè di pagina che scorrono con gli elementi dell'elenco. L'intestazione e piè di pagina possono essere stringhe di testo o un layout più complesso. Si noti che è separato dal [sezione gruppi](#Grouping).

È possibile impostare il `Header` e/o `Footer` in una stringa semplice oppure è possibile impostarli su un layout più complesso.
Esistono inoltre `HeaderTemplate` e `FooterTemplate` proprietà che consentono di creare un layout più complessi per l'intestazione e piè di pagina che supportano il data binding.

Per creare una semplice intestazione/piè di pagina, è sufficiente impostare le proprietà di intestazione o piè di pagina per il testo da visualizzare. In codice:

```csharp
ListView HeaderList = new ListView() {
    Header = "Header",
    Footer = "Footer"
    };
```

In XAML:

```xaml
<ListView  x:Name="HeaderList"  Header="Header" Footer="Footer"></ListView>
```

![](customizing-list-appearance-images/header-default.png "ListView con intestazione e piè di pagina")

Per creare un'intestazione personalizzata e un piè di pagina, definire le visualizzazioni di intestazione e piè di pagina:

```xaml
<ListView.Header>
    <StackLayout Orientation="Horizontal">
        <Label Text="Header"
        TextColor="Olive"
        BackgroundColor="Red" />
    </StackLayout>
</ListView.Header>
<ListView.Footer>
    <StackLayout Orientation="Horizontal">
        <Label Text="Footer"
        TextColor="Gray"
        BackgroundColor="Blue" />
    </StackLayout>
</ListView.Footer>
```

![](customizing-list-appearance-images/header-custom.png "ListView con intestazione personalizzata e un piè di pagina")

<a name="Row_Separators" />

## <a name="row-separators"></a>Separatori di riga
Vengono visualizzate le righe di separazione tra `ListView` elementi per impostazione predefinita in iOS e Android. Se si preferisce nascondere le righe di separazione in iOS e Android, impostare il `SeparatorVisibility` proprietà nella finestra di ListView. Le opzioni per `SeparatorVisibility` sono:

* **Default** -Mostra una linea di separazione in iOS e Android.
* **Nessuno** -nasconde il separatore in tutte le piattaforme.

Visibilità predefinita:

C#:

```csharp
SepratorDemoListView.SeparatorVisibility = SeparatorVisibility.Default;
```

XAML:

```xaml
<ListView x:Name="SeparatorDemoListView" SeparatorVisibility="Default" />
```

![](customizing-list-appearance-images/separator-default.png "ListView con separatori di riga predefinita")

None:

C#:

```csharp
SepratorDemoListView.SeparatorVisibility = SeparatorVisibility.None;
```

XAML:

```xaml
<ListView x:Name="SeparatorDemoListView" SeparatorVisibility="None" />
```

![](customizing-list-appearance-images/separator-none.png "ListView senza separatori di riga")

È anche possibile impostare il colore della linea di separazione tramite il `SeparatorColor` proprietà:

C#:

```csharp
SepratorDemoListView.SeparatorColor = Color.Green;
```

XAML:

```xaml
<ListView x:Name="SeparatorDemoListView" SeparatorColor="Green" />
```

![](customizing-list-appearance-images/separator-custom.png "ListView con separatori di riga di colore verde")

> [!NOTE]
> Impostazione di queste proprietà in Android dopo il caricamento di `ListView` comporta una riduzione delle prestazioni di grandi dimensioni.

<a name="Row_Heights" />

## <a name="row-heights"></a>Altezza delle righe
Impostazione predefinita, tutte le righe in un ListView dispongono della stessa altezza. ListView ha due proprietà che può essere utilizzata per modificare questo comportamento:

- `HasUnevenRows` &ndash; `true`/`false` valore, le righe hanno altezza diversa se impostato su `true`. Il valore predefinito è `false`.
- `RowHeight` &ndash; Imposta l'altezza di ogni riga durante `HasUnevenRows` è `false`.

È possibile impostare l'altezza di tutte le righe, impostando il `RowHeight` proprietà di `ListView`.

### <a name="custom-fixed-row-height"></a>Altezza di riga fissa personalizzato

C#:

```csharp
RowHeightDemoListView.RowHeight = 100;
```

XAML:

```xaml
<ListView x:Name="RowHeightDemoListView" RowHeight="100" />
```

![](customizing-list-appearance-images/height-custom.png "ListView con l'altezza di riga fisso")


### <a name="uneven-rows"></a>Righe non uniformi

Se si desidera singole righe affinché altezza diversa, è possibile impostare il `HasUnevenRows` proprietà `true`.
Si noti che non devono essere impostato manualmente una volta altezze `HasUnevenRows` è stata impostata su `true`, poiché l'altezza verrà automaticamente calcolato da xamarin. Forms.


C#:

```csharp
RowHeightDemoListView.HasUnevenRows = true;
```

XAML:

```xaml
<ListView x:Name="RowHeightDemoListView" HasUnevenRows="true" />
```

![](customizing-list-appearance-images/height-uneven.png "ListView con righe non uniformi")

### <a name="runtime-resizing-of-rows"></a>Runtime di ridimensionamento di righe

Singoli `ListView` righe possono essere ridimensionate a livello di codice in fase di esecuzione, a condizione che il `HasUnevenRows` è impostata su `true`. Il [ `Cell.ForceUpdateSize` ](xref:Xamarin.Forms.Cell.ForceUpdateSize) metodo aggiorna le dimensioni della cella, anche quando non è attualmente visibile, come illustrato nell'esempio di codice seguente:

```csharp
void OnImageTapped (object sender, EventArgs args)
{
    var image = sender as Image;
    var viewCell = image.Parent.Parent as ViewCell;

    if (image.HeightRequest < 250) {
        image.HeightRequest = image.Height + 100;
        viewCell.ForceUpdateSize ();
    }
}
```

Il `OnImageTapped` gestore eventi viene eseguito in risposta a un [ `Image` ](xref:Xamarin.Forms.Image) vengano utilizzate in una cella e aumenta la dimensione del `Image` visualizzato nella cella in modo che sia facilmente è visualizzarlo.

![](customizing-list-appearance-images/dynamic-row-resizing.png "ListView con ridimensionamento di righe di Runtime")

Si noti che esiste una forte possibilità di riduzione delle prestazioni se questa funzionalità è eccessivo.



## <a name="related-links"></a>Collegamenti correlati

- [Raggruppamento (esempio)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/ListView/Grouping)
- [Visualizzazione di Renderer personalizzato (esempio)](https://developer.xamarin.com/samples/xamarin-forms/WorkingWithListviewNative/)
- [Ridimensionamento di righe dinamiche (esempio)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/ListView/DynamicUnevenListCells/)
- [note sulla versione 1.4](http://forums.xamarin.com/discussion/35451/xamarin-forms-1-4-0-released/)
- [note sulla versione 1.3](http://forums.xamarin.com/discussion/29934/xamarin-forms-1-3-0-released/)
