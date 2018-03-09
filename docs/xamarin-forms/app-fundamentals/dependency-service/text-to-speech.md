---
title: Implementazione di sintesi vocale
description: Utilizzare DependencyService eseguire chiamate nell'API di sintesi vocale native di ciascuna piattaforma
ms.topic: article
ms.prod: xamarin
ms.assetid: 1D6164F9-4ECE-43A6-B583-1F5D5EFC1DDF
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/18/2017
ms.openlocfilehash: c5bd753aaa3a9e807a03a9fb05b233cfa39d0dc3
ms.sourcegitcommit: 61f5ecc5a2b5dcfbefdef91664d7460c0ee2f357
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2018
---
# <a name="implementing-text-to-speech"></a>Implementazione di sintesi vocale

In questo articolo guiderà l'utente durante la creazione di un'app multipiattaforma che usa [ `DependencyService` ](https://developer.xamarin.com/api/type/Xamarin.Forms.DependencyService/) per accedere ad API sintesi vocale native:

- **[La creazione dell'interfaccia](#Creating_the_Interface)**  &ndash; comprendere la modalità di creazione dell'interfaccia nel codice condiviso.
- **[iOS implementazione](#iOS_Implementation)**  &ndash; informazioni su come implementare l'interfaccia nel codice nativo per iOS.
- **[Implementazione Android](#Android_Implementation)**  &ndash; informazioni su come implementare l'interfaccia nel codice nativo per Android.
- **[Implementazione di Windows](#WindowsImplementation)**  &ndash; informazioni su come implementare l'interfaccia nel codice nativo per Windows Phone e la piattaforma UWP (Universal Windows).
- **[Implementazione di codice condiviso](#Implementing_in_Shared_Code)**  &ndash; imparare a usare `DependencyService` chiamino l'implementazione native da codice condiviso.

L'applicazione utilizzando `DependencyService` avrà la struttura seguente:

![](text-to-speech-images/tts-diagram.png "Struttura dell'applicazione DependencyService")

<a name="Creating_the_Interface" />

## <a name="creating-the-interface"></a>Creazione dell'interfaccia

Innanzitutto, creare un'interfaccia nel codice condiviso che esprime la funzionalità che si intende implementare. Per questo esempio, l'interfaccia contiene un singolo metodo, `Speak`:

```csharp
public interface ITextToSpeech
{
    void Speak (string text);
}
```

Scrivere codice per questa interfaccia nel codice condiviso consentirà l'app xamarin. Forms accedere il riconoscimento vocale API in ciascuna piattaforma.

> [!NOTE]
> **Nota**: le classi che implementano l'interfaccia devono avere un costruttore senza parametri per funzionare con il `DependencyService`.

<a name="iOS_Implementation" />

## <a name="ios-implementation"></a>Implementazione di iOS

L'interfaccia deve essere implementata in ogni progetto di applicazione specifico della piattaforma. Si noti che la classe ha un costruttore senza parametri in modo che il `DependencyService` possibile creare nuove istanze.

```csharp
[assembly: Dependency(typeof(TextToSpeechImplementation))]
namespace DependencyServiceSample.iOS
{

    public class TextToSpeechImplementation : ITextToSpeech
    {
        public TextToSpeechImplementation() { }

        public void Speak(string text)
        {
            var speechSynthesizer = new AVSpeechSynthesizer();
            var speechUtterance = new AVSpeechUtterance(text)
            {
                Rate = AVSpeechUtterance.MaximumSpeechRate / 4,
                Voice = AVSpeechSynthesisVoice.FromLanguage("en-US"),
                Volume = 0.5f,
                PitchMultiplier = 1.0f
            };

            speechSynthesizer.SpeakUtterance(speechUtterance);
        }
    }
}
```

Il `[assembly]` attributo consente di registrare la classe come un'implementazione del `ITextToSpeech` interfaccia, il che significa che `DependencyService.Get<ITextToSpeech>()` può essere utilizzato nel codice condiviso per creare un'istanza.

<a name="Android_Implementation" />

## <a name="android-implementation"></a>Implementazione di Android

Il codice Android è più complesso rispetto alla versione di iOS: richiede la classe di implementazione per ereditare da Android specifico `Java.Lang.Object` e implementare il `IOnInitListener` anche l'interfaccia.

Xamarin. Forms fornisce anche il `Forms.Context` oggetto, ovvero un'istanza del contesto corrente Android. Molti metodi di Android SDK, richiedono un buon esempio è la possibilità di chiamare `StartActivity()`.

```csharp
[assembly: Dependency(typeof(TextToSpeechImplementation))]
namespace DependencyServiceSample.Droid
{

    public class TextToSpeechImplementation : Java.Lang.Object, ITextToSpeech, TextToSpeech.IOnInitListener
    {
        TextToSpeech speaker;
        string toSpeak;

        public void Speak(string text)
        {
            toSpeak = text;
            if (speaker == null)
            {
                speaker = new TextToSpeech(Forms.Context, this);
            }
            else
            {
                speaker.Speak(toSpeak, QueueMode.Flush, null, null);
            }
        }

        public void OnInit(OperationResult status)
        {
            if (status.Equals(OperationResult.Success))
            {
                speaker.Speak(toSpeak, QueueMode.Flush, null, null);
            }
        }
    }
}
```

Il `[assembly]` attributo consente di registrare la classe come un'implementazione del `ITextToSpeech` interfaccia, il che significa che `DependencyService.Get<ITextToSpeech>()` può essere utilizzato nel codice condiviso per creare un'istanza.

<a name="WindowsImplementation" />

## <a name="windows-phone-and-universal-windows-platform-implementation"></a>Windows Phone e l'implementazione della piattaforma Windows universale

Windows Phone e la piattaforma Windows universale hanno una API di sintesi vocale nel `Windows.Media.SpeechSynthesis` dello spazio dei nomi. L'unico problema è da ricordare tick il **microfono** funzionalità nel manifesto, in caso contrario l'accesso a del contenuto vocale API sono bloccate.

```csharp
[assembly:Dependency(typeof(TextToSpeechImplementation))]
public class TextToSpeechImplementation : ITextToSpeech
{
    public async void Speak(string text)
    {
        var mediaElement = new MediaElement();
        var synth = new Windows.Media.SpeechSynthesis.SpeechSynthesizer();
        var stream = await synth.SynthesizeTextToStreamAsync(text);

        mediaElement.SetSource(stream, stream.ContentType);
        mediaElement.Play();
    }
}
```

Il `[assembly]` attributo consente di registrare la classe come un'implementazione del `ITextToSpeech` interfaccia, il che significa che `DependencyService.Get<ITextToSpeech>()` può essere utilizzato nel codice condiviso per creare un'istanza.

<a name="Implementing_in_Shared_Code" />

## <a name="implementing-in-shared-code"></a>Implementazione di codice condiviso

Ora è possibile scrivere e testare il codice condiviso che accede all'interfaccia di sintesi vocale. Questa pagina semplice include un pulsante che attiva la funzionalità di riconoscimento vocale. Usa il `DependencyService` per ottenere un'istanza del `ITextToSpeech` interfaccia &ndash; in fase di esecuzione questa istanza è l'implementazione specifica della piattaforma che dispone dell'accesso completo a SDK nativo.

```csharp
public MainPage ()
{
    var speak = new Button {
        Text = "Hello, Forms !",
        VerticalOptions = LayoutOptions.CenterAndExpand,
        HorizontalOptions = LayoutOptions.CenterAndExpand,
    };
    speak.Clicked += (sender, e) => {
        DependencyService.Get<ITextToSpeech>().Speak("Hello from Xamarin Forms");
    };
    Content = speak;
}
```

Esecuzione dell'applicazione in iOS, Android, o le piattaforme Windows e premendo che il pulsante comporterà l'applicazione utilizzando il SDK di riconoscimento vocale nativo in ogni piattaforma vocale.

 ![iOS e Android pulsante sintesi vocale](text-to-speech-images/running.png "esempio sintesi vocale")


## <a name="related-links"></a>Collegamenti correlati

- [Utilizzando DependencyService (esempio)](https://developer.xamarin.com/samples/xamarin-forms/UsingDependencyService/)
- [DependencyServiceSample](https://developer.xamarin.com/samples/xamarin-forms/DependencyService/DependencyServiceSample/)
- [Cartella di lavoro di sintesi vocale](https://developer.xamarin.com/workbooks/xamarin-forms/application-fundamentals/text-to-speech/text-to-speech.workbook)