---
title: Utilizzo di servizi Web
description: Questa guida viene illustrato come comunicare con servizi web diversi per fornire creare, leggere, aggiornare e l'eliminazione (CRUD) a un'applicazione di xamarin. Forms. Gli argomenti trattati includono la comunicazione con i servizi ASMX, WCF services, servizi REST e App per dispositivi mobili di Azure.
ms.prod: xamarin
ms.assetid: 8B360BDA-E4E3-4A3F-9004-0E35362F49F
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/20/2016
ms.openlocfilehash: a4c842ea7fd37ade9be0a9cb3e3ff7e50a6d1491
ms.sourcegitcommit: bc39d85b4585fcb291bd30b8004b3f7edcac4602
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2018
ms.locfileid: "31044574"
---
# <a name="consuming-web-services"></a>Utilizzo di servizi Web

Ques_to Guida viene illustrato come comunicare con i servizi web diversi per fornire creare, leggere, aggiornare ed eliminare funzionalità (CRUD) a un'applicazione di xamarin. Forms. Gli argomenti trattati includono la comunicazione con i servizi ASMX, WCF services, servizi REST e App per dispositivi mobili di Azure.

## <a name="consuming-an-aspnet-web-service-asmxxamarin-formsdata-cloudconsumingasmxmd"></a>[Utilizzo di un servizio Web ASP.NET (ASMX)](~/xamarin-forms/data-cloud/consuming/asmx.md)

Servizi Web ASP.NET (ASMX) offrono la possibilità di creare servizi web che inviano messaggi tramite HTTP mediante SOAP Simple Object Access Protocol (). SOAP è un protocollo indipendente dalla piattaforma e indipendente dal linguaggio per la compilazione e l'accesso ai servizi web. I consumer di un servizio ASMX non è necessario conoscere la piattaforma, un modello a oggetti o un linguaggio di programmazione utilizzato per implementare il servizio. È sufficiente comprendere come inviare e ricevere messaggi SOAP. In questo articolo viene illustrato come utilizzare un servizio web ASMX da un'applicazione di xamarin. Forms.

## <a name="consuming-a-windows-communication-foundation-wcf-web-servicexamarin-formsdata-cloudconsumingwcfmd"></a>[Utilizzo di un servizio Web di Windows Communication Foundation (WCF)](~/xamarin-forms/data-cloud/consuming/wcf.md)

WCF è framework unificato di Microsoft per la creazione di applicazioni orientate ai servizi. Consente agli sviluppatori di compilare applicazioni distribuite protette, affidabile, transazioni e interoperative. Esistono differenze tra i servizi Web ASP.NET (ASMX) e WCF, ma è importante comprendere che WCF supporta le stesse funzionalità che fornisce ASMX: messaggi SOAP su HTTP. In questo articolo viene illustrato come utilizzare un servizio WCF SOAP da un'applicazione di xamarin. Forms.

## <a name="consuming-a-restful-web-servicexamarin-formsdata-cloudconsumingrestmd"></a>[Utilizzo di un servizio Web RESTful](~/xamarin-forms/data-cloud/consuming/rest.md)

Representational State Transfer (REST) è uno stile architetturale per la compilazione di servizi web. Richieste REST vengono effettuate tramite HTTP utilizzando gli stessi verbi HTTP utilizzato dal web browser per recuperare le pagine web e per inviare dati al server. In questo articolo viene illustrato come utilizzare un servizio web RESTful da un'applicazione di xamarin. Forms.

## <a name="consuming-an-azure-mobile-appxamarin-formsdata-cloudconsumingazuremd"></a>[Utilizzo di un'App per dispositivi mobili di Azure](~/xamarin-forms/data-cloud/consuming/azure.md)

Azure App per dispositivi mobili consentono di sviluppare applicazioni con scalabilità back-end ospitato in Azure App Service, con supporto per l'autenticazione per dispositivi mobili, non in linea sincronizzazione e le notifiche push. Questo articolo è applicabile solo alle App mobili di Azure che utilizzano un back-end di Node.js, viene illustrato come eseguire una query, inserimento, aggiornamento ed eliminare i dati archiviati in una tabella in un'istanza di App mobili di Azure.

## <a name="related-links"></a>Collegamenti correlati

- [Introduzione ai servizi Web](~/cross-platform/data-cloud/web-services/index.md)
- [Panoramica del supporto asincrono](~/cross-platform/platform/async.md)
