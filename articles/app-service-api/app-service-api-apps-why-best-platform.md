---
title: "API Apps 簡介 | Microsoft Docs"
description: "了解 Azure App Service 如何協助您開發、裝載和使用 RESTful API。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: 9b7118b22c07fc527f6bdfe5c57345fa9e2cfea2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="api-apps-overview"></a>API Apps 概觀
Azure App Service 中的 API Apps 提供各種功能，讓您更輕鬆地在雲端和內部部署當中開發、裝載和使用 API。 使用 API Apps，即可受益於企業級安全性、簡單的存取控制、混合式連線和自動 SDK 產生等功能，並與 [Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)完美整合。

[Azure App Service](../app-service/app-service-value-prop-what-is.md) 是一個完全受管理的平台，適用於 Web、行動和整合案例。 API Apps 是 [Azure App Service](../app-service/app-service-value-prop-what-is.md)提供的四個應用程式類型之一。

![Azure App Service 中的應用程式類型](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>為何要使用 API Apps？
以下是 API Apps 的一些主要功能︰

* **繼續使用現有的 API** - 您不必變更現有 API 的任何程式碼，就能利用 API Apps，只要將程式碼部署至 API 應用程式即可。 您的 API 可以使用 App Service 支援的任何語言或架構，包括 ASP.NET 和 C#、Java、PHP、Node.js 和 Python。
* **輕鬆使用** - 藉由 [Swagger API 中繼資料](http://swagger.io/) 的整合支援，各種用戶端都能輕鬆使用您的 API。  使用各種語言 (包括 C#、Java 和 Javascript) 為您的 API 自動產生用戶端程式碼。 輕鬆設定 [CORS](app-service-api-cors-consume-javascript.md) 而不需變更您的程式碼。 如需詳細資訊，請參閱[適用於 API 探索及產生程式碼用的 App Service API Apps 中繼資料](app-service-api-metadata.md)與[使用 CORS 從 JavaScript 取用 API 應用程式](app-service-api-cors-consume-javascript.md)。 
* **簡單存取控制** - 您可以保護 API 應用程式避免其遭到未經驗證的存取，且不必變更程式碼。 其他服務或代表使用者的用戶端存取 API 時，內建的驗證服務會提供保護。 支援的識別提供者包括：Azure Active Directory、Facebook、Twitter、Google 和 Microsoft 帳戶。 用戶端可以使用 Active Directory Authentication Library (ADAL) 或行動應用程式 SDK。 如需詳細資訊，請參閱 [Azure App Service 中的 API Apps 驗證與授權](app-service-api-authentication.md)。
* **Visual Studio 整合** - Visual Studio 中的專用工具，可簡化建立、部署、使用、偵錯和管理 API Apps 的工作。 如需詳細資訊，請參閱 [發表 Azure SDK 2.8.1 for .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/)。
* **與邏輯應用程式整合** - 您建立的 API 應用程式可供 [App Service Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)使用。  如需詳細資訊，請參閱[將您裝載在 App Service 上的自訂 API 與邏輯應用程式一起使用](../logic-apps/logic-apps-custom-hosted-api.md)和[新結構描述版本 2015-08-01 預覽](../logic-apps/logic-apps-schema-2015-08-01.md)。

此外，API 應用程式可以利用 [Web Apps](../app-service-web/app-service-web-overview.md) 和 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) 所提供的功能。 反之亦然，如果您使用 Web 應用程式或行動應用程式應用程式來裝載 API，它就能夠利用像是 Swagger 中繼資料的 API Apps 功能來產生用戶端程式碼，以及利用 CORS 進行跨網域瀏覽器存取。 這三個應用程式類型 (API、Web、行動) 之間的唯一差異是它們在 Azure 入口網站中所使用的名稱和圖示。

## <a name="whats-the-difference-between-api-apps-and-azure-api-management"></a>API Apps 和 Azure API 管理之間的差異為何？
API Apps 和 [Azure API 管理](../api-management/api-management-key-concepts.md) 是互補的服務︰

* API 管理是關於管理 API。 您會將 API 管理前端放在 API 上，以監視及節流使用量、操作輸入和輸出、將多個 API 合併為一個端點等等。 受管理的 API 可以裝載於任何位置。
* API 應用程式是關於裝載 API。 此服務包含的功能可方便開發和使用 API，但它不會執行 API 管理所執行的監視、節流、操作或合併。 如果您不需要 API 管理功能，可以將 API 裝載在 API Apps 中，而不需要使用 API 管理。

下圖說明裝載在 API Apps 及其他地方之 API 所使用的 API 管理。

![Azure API 管理和 API Apps](./media/app-service-api-apps-why-best-platform/apia-apim.png)

API 管理和 API 應用程式的某些功能具有類似的功能。  例如，兩者都可以將 CORS 支援自動化。 當您同時使用這兩項服務時，您會使用 API 管理進行 CORS，因為它是作為您 API 應用程式的前端。 

## <a name="getting-started"></a>開始使用
若要透過將範例程式碼部署至其中一個應用程式以開始使用 API Apps，請參閱您所需架構適用的教學課程︰

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

若要詢問有關 API Apps 的問題，請在 [API Apps 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)中發問。 

