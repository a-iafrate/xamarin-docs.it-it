---
title: Firmare con un ID sviluppatore
description: Questa guida descrive come firmare un'app Xamarin.Mac con un ID sviluppatore per la pubblicazione.
ms.topic: article
ms.prod: xamarin
ms.assetid: cf7b733b-e08f-4f56-a233-264b29ee4c97
ms.technology: xamarin-mac
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/14/2017
ms.openlocfilehash: 46d5527a33b82a795029f62900e782d644671f0d
ms.sourcegitcommit: 30055c534d9caf5dffcfdeafd6f08e666fb870a8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2018
---
# <a name="sign-with-developer-id"></a>Firmare con un ID sviluppatore

Se lo sviluppatore prevede di distribuire un'app direttamente agli utenti di macOS, Apple consiglia di firmarne il codice con l'ID sviluppatore in modo che possa essere installata nei sistemi macOS con **GateKeeper** abilitato. Se l'app non è stata firmata, **GateKeeper** impedirà agli utenti di installarla visualizzando un messaggio di avviso. Gli utenti possono ignorare questa limitazione tenendo premuto CTRL durante l'avvio.

Per altre informazioni, vedere [ID sviluppatore e GateKeeper](https://developer.apple.com/resources/developer-id/) e [Distributing Outside the Mac App Store](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html) (Distribuzione al di fuori di Mac App Store) nel sito Web Apple.

## <a name="code-signing-options"></a>Opzioni di firma del codice

Per compilare un'app per la distribuzione diretta agli utenti, non tramite Mac App Store, impostare le **impostazioni di firma** per usare l'**ID sviluppatore**. Assicurarsi di modificare la configurazione **Release** (Rilascio).

 [![](signing-images/config02.png "Opzioni della firma Mac")](signing-images/config02.png#lightbox)


## <a name="build"></a>Compilazione

Prima della compilazione, assicurarsi di aver selezionato la configurazione corretta e la creazione di un pacchetto di installazione nelle impostazioni **Compilazione Mac**:

[![](signing-images/config03.png "Opzioni di compilazione")](signing-images/config03.png#lightbox)

Quando compila l'app, lo sviluppatore dovrà usare entrambi i certificati:

 [![](signing-images/image57.png "Consentire l'accesso keychain")](signing-images/image57.png#lightbox)

 [![](signing-images/image58.png "Consentire l'accesso keychain")](signing-images/image58.png#lightbox)

Dopo aver compilato l'applicazione, lo sviluppatore può fare clic con il pulsante destro del mouse sul progetto e scegliere **Apri cartella superiore** per trovare il file del pacchetto nella directory `bin/Release`. Il file include un programma di installazione per l'applicazione, in modo che possa essere distribuita a tutti gli utenti macOS per l'installazione.

 [![](signing-images/image59.png "Selezione del pacchetto dell'app in Finder")](signing-images/image59.png#lightbox)

## <a name="related-links"></a>Collegamenti correlati

- [Installazione](~//mac/get-started/installation.md)
- [Esempio Hello, Mac](~//mac/get-started/hello-mac.md)
- [Distribuire le app in Mac App Store](https://developer.apple.com/devcenter/mac/checklist/)
- [Guida degli strumenti: firma del codice dell'app](https://developer.apple.com/library/mac/#documentation/ToolsLanguages/Conceptual/OSXWorkflowGuide/CodeSigning/CodeSigning.html)
- [ID sviluppatore e GateKeeper](https://developer.apple.com/resources/developer-id/)