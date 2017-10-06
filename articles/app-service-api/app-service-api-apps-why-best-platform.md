---
title: "aaaAPI 應用程式簡介 |Microsoft 文件"
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
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>API Apps 概觀
API 應用程式的 Azure 應用程式服務提供功能，使其更容易 toodevelop，裝載，並使用 hello 雲端和內部部署中的 Api。 使用 API Apps，即可受益於企業級安全性、簡單的存取控制、混合式連線和自動 SDK 產生等功能，並與 [Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)完美整合。

[Azure App Service](../app-service/app-service-value-prop-what-is.md) 是一個完全受管理的平台，適用於 Web、行動和整合案例。 API Apps 是 [Azure App Service](../app-service/app-service-value-prop-what-is.md)提供的四個應用程式類型之一。

![Azure App Service 中的應用程式類型](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>為何要使用 API Apps？
以下是 API Apps 的一些主要功能︰

* **讓您為現有的 API-是**-toochange hello 的任何程式碼中沒有現有的應用程式開發介面 tootake 優點的應用程式開發介面應用程式-只部署 tooan API 應用程式程式碼。 您的 API 可以使用 App Service 支援的任何語言或架構，包括 ASP.NET 和 C#、Java、PHP、Node.js 和 Python。
* **輕鬆使用** - 藉由 [Swagger API 中繼資料](http://swagger.io/) 的整合支援，各種用戶端都能輕鬆使用您的 API。  使用各種語言 (包括 C#、Java 和 Javascript) 為您的 API 自動產生用戶端程式碼。 輕鬆設定 [CORS](app-service-api-cors-consume-javascript.md) 而不需變更您的程式碼。 如需詳細資訊，請參閱[適用於 API 探索及產生程式碼用的 App Service API Apps 中繼資料](app-service-api-metadata.md)與[使用 CORS 從 JavaScript 取用 API 應用程式](app-service-api-cors-consume-javascript.md)。 
* **簡單的存取控制**-防止沒有變更 tooyour 程式碼的未驗證存取的 API 應用程式。 其他服務或代表使用者的用戶端存取 API 時，內建的驗證服務會提供保護。 支援的識別提供者包括：Azure Active Directory、Facebook、Twitter、Google 和 Microsoft 帳戶。 用戶端可以使用 Active Directory 驗證程式庫 (ADAL) 或 hello 行動應用程式 SDK。 如需詳細資訊，請參閱 [Azure App Service 中的 API Apps 驗證與授權](app-service-api-authentication.md)。
* **Visual Studio 整合**-Visual Studio 中的專用的工具簡化 hello 工作建立、 部署、 使用、 偵錯，以及管理 API 的應用程式。 如需詳細資訊，請參閱[Announcing hello Azure SDK for.NET 2.8.1](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/)。
* **與邏輯應用程式整合** - 您建立的 API 應用程式可供 [App Service Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)使用。  如需詳細資訊，請參閱[將您裝載在 App Service 上的自訂 API 與邏輯應用程式一起使用](../logic-apps/logic-apps-custom-hosted-api.md)和[新結構描述版本 2015-08-01 預覽](../logic-apps/logic-apps-schema-2015-08-01.md)。

此外，API 應用程式可以利用 [Web Apps](../app-service-web/app-service-web-overview.md) 和 [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) 所提供的功能。 hello 反向也是如此： 如果您使用的 web 應用程式或行動裝置應用程式 toohost 應用程式開發介面，它可以利用 API 應用程式功能，例如用戶端的 Swagger 中繼資料的程式碼產生和 CORS 的跨網域瀏覽器存取。 hello hello 三個應用程式類型 （行動 web 中的 應用程式開發介面） 之間的差異是 hello 名稱與它們在 hello Azure 入口網站中所使用的圖示。

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>Hello Azure API 管理 API 的應用程式之間的差異為何？
API Apps 和 [Azure API 管理](../api-management/api-management-key-concepts.md) 是互補的服務︰

* API 管理是關於管理 API。 您 API 管理前端打 API toomonitor 和節流使用量、 管理輸入和輸出、 將多個 Api 合併成一個端點，等等。 hello 受管理的應用程式開發介面可以裝載任何位置。
* API 應用程式是關於裝載 API。 hello 服務包含可簡化開發和取用 Api 功能，但它不會執行 hello 類型的監視、 節流設定、 操作或 API 管理，並會將合併。 如果您不需要 API 管理功能，可以將 API 裝載在 API Apps 中，而不需要使用 API 管理。

下圖說明裝載在 API Apps 及其他地方之 API 所使用的 API 管理。

![Azure API 管理和 API Apps](./media/app-service-api-apps-why-best-platform/apia-apim.png)

API 管理和 API 應用程式的某些功能具有類似的功能。  例如，兩者都可以將 CORS 支援自動化。 當您一起使用 hello 兩項服務時，您可使用 API 管理 CORS 因為它的功能與 hello 前端 tooyour API 應用程式。 

## <a name="getting-started"></a>開始使用
tooget 入門 API 應用程式部署的範例程式碼 tooone，請參閱 hello 教學課程，不論您偏好的架構：

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

tooask 疑問 API 的應用程式啟動的執行緒在 hello [API 應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)。 

