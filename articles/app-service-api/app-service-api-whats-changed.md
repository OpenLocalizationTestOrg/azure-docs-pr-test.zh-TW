---
title: "aaaApp Service API 應用程式-已變更的內容 |Microsoft 文件"
description: "了解 Azure App Service 中 API Apps 的新功能"
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>App Service API Apps - 變更的項目
一些改善 tooAzure 應用程式服務已在 2015 年 11 月中的 hello connect （） 事件，[宣布](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/)。 這些改良包括基礎變更 tooAPI 應用程式 toobetter 配合行動和 Web 應用程式、 降低概念計數，以及改善部署和執行階段效能。 從 2015 年 11 月 30 日，新的應用程式開發介面應用程式，您建立使用 hello Azure 管理入口網站或 hello 最新工具將會反映這些變更。 本文說明這些變更，以及如何 tooredeploy 現有應用程式 tootake 利用 hello 功能。

## <a name="feature-changes"></a>功能變更
hello API 應用程式 – 驗證、 CORS 和 API 的中繼資料的主要功能 – 已直接在應用程式服務。 這項變更，與 hello 功能都可跨 Web、 行動裝置和應用程式開發介面應用程式。 事實上，所有三個共用相同 hello **Microsoft.Web/sites**資源類型資源管理員 中。 hello API 應用程式閘道已不再需要或提供 API 應用程式。 這也讓您更輕鬆 toouse Azure API 管理因為只要 hello 單一 API 管理閘道。

![API Apps 概觀](./media/app-service-api-whats-changed/api-apps-overview.png)

重要的設計原則，以更新 API 應用程式的 hello 就是 tooenable 您 toobring 是做為您的 API，以您選擇的語言。  如果您的 API 已經部署為 Web 應用程式或行動裝置應用程式時，您沒有 tooredeploy tootake 您應用程式利用 hello 新功能。 如果您目前是在 API Apps 預覽，詳細的移轉指南如下。

### <a name="authentication"></a>驗證
hello 現有通行應用程式開發介面應用程式、 行動服務應用程式和 Web 應用程式驗證功能已被整合和 hello 管理入口網站中的單一 Azure 應用程式服務驗證刀鋒視窗中可用。 簡介 tooauthentication 中的服務應用程式服務，請參閱[展開應用程式服務驗證 / 授權](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)。

對於 API 案例，有一些相關的新功能：

* **支援直接使用 Azure Active Directory**，而不需要工作階段權杖的 tooexchange hello AAD 語彙基元的用戶端程式碼： 您的用戶端可以只包含 hello AAD 語彙基元中 hello 授權標頭，根據 toohello 持有人權杖規格。 這也表示沒有應用程式特定的服務需要 SDK hello 用戶端或伺服器端上。 
* **服務對服務或 「 內部 」 存取**： 如果您有背景程式處理序或某些其他需要不含介面存取 tooAPIs 的用戶端，您可以要求使用 AAD 服務主體的權杖，並將它傳遞 tooApp 服務進行驗證的程式應用程式。
* **延遲授權**： 許多應用程式有不同的 hello 應用程式的不同部分的存取限制。 也許您想公開使用的是，某些應用程式開發介面 toobe，而有些則需要登入。 hello 原始驗證和授權功能已想到，與 hello 整個站台需要登入。 此選項仍存在，但您可以或者允許應用程式程式碼 toorender 存取決策之後 hello 使用者驗證應用程式服務。

如需 hello 新驗證功能的詳細資訊，請參閱[Azure App Service 中的應用程式開發介面應用程式的驗證和授權](app-service-api-authentication.md)。 如需有關如何 toomigrate 現有 API 的應用程式從 hello 先前 API 應用程式模型 toohello 新一個，請參閱資訊[移轉現有的應用程式開發介面應用程式](#migrating-existing-api-apps)本文稍後。

### <a name="cors"></a>CORS
而不是以逗號分隔**MS_CrossDomainOrigins**應用程式設定，現在刀鋒視窗中沒有設定 CORS hello Azure 管理入口網站。 或者，可以使用資源管理員工具，例如 Azure PowerShell、CLI 或 [資源總管](https://resources.azure.com/)來進行設定。 設定 hello **cors**屬性 hello **Microsoft.Web/sites/config**資源類型您**&lt;站台名稱&gt;/web**資源。 例如：

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>API 中繼資料
跨 Web、 行動裝置和應用程式開發介面應用程式，就可 hello API 定義刀鋒視窗。 在 hello 管理入口網站中，您可以指定相對的 url 或您的應用程式開發介面的該主機的 Swagger 2.0 表示指向 tooan 端點的絕對 url。 或者，可以使用資源管理員工具進行設定。 設定 hello **apiDefinition**屬性 hello **Microsoft.Web/sites/config**資源類型您**&lt;站台名稱&gt;/web**資源。 例如：

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

此時，hello 中繼資料端點需要 toobe 可公開存取未經驗證的許多下游的用戶端 （例如 Visual Studio REST API 用戶端產生和 PowerApps 「 新增應用程式開發介面 」 流程） tooconsume 它。 這表示如果您使用應用程式服務驗證，且想從 tooexpose hello API 定義本身的應用程式中，您必須使 hello 路由 tooyour Swagger 中繼資料公用稍早所述的 toouse hello 延後的驗證選項。

## <a name="management-portal"></a>管理入口網站
選取**新增 > Web + 行動 > API 應用程式**hello 在入口網站將建立反映 hello hello 文章所述的新功能的應用程式開發介面應用程式。 [瀏覽] > [API Apps] 只會顯示這些新的 API 應用程式。 一旦您瀏覽到應用程式開發介面應用程式，hello 刀鋒視窗共用 hello 相同的配置和功能的 Web 和行動應用程式。 hello 唯一差異是快速入門內容和排序設定。

現有的應用程式開發介面應用程式 （或從邏輯應用程式建立服務商場應用程式開發介面應用程式） 以 hello 先前預覽功能仍會顯示在 hello Logic Apps 設計師，然後瀏覽資源群組中的所有資源時。

## <a name="visual-studio"></a>Visual Studio
大部分 Web 應用程式，因為它們會共用，工具會與新的應用程式開發介面應用程式一起 hello 相同的基礎**Microsoft.Web/sites**資源類型。 hello Azure Visual Studio 工具，不過，應該是升級的 tooversion 2.8.1 或更新版本，因為它會公開的功能特定 tooAPIs 的數字。 從 hello 下載 hello SDK [Azure 下載頁面](https://azure.microsoft.com/downloads/)。

使用的應用程式服務類型的 hello hello 合理化，發佈也有統一下**發行 > Microsoft Azure App Service**:

![API Apps 發佈](./media/app-service-api-whats-changed/api-apps-publish.png)

深入了解 SDK 2.8.1，讀取的 hello 公告 toolearn[部落格文章](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/)。

或者，您可以手動匯入 hello 發行設定檔與 hello management 入口網站 tooenable 發行。 不過，雲端總管、程式碼產生和 API 應用程式選取/建立需要 SDK 2.8.1 或更高版本。

## <a name="migrating-existing-api-apps"></a>移轉現有的 API 應用程式
如果您的自訂 API 是已部署的 toohello 預覽舊版的 API 應用程式，我們會要求應用程式開發介面應用程式移轉 toohello 新模型，由 2015 年 12 月 31 日。 因為同時 hello 舊的和新的模型根據應用程式服務中裝載的 Web Api，可重複使用 hello 大部分現有的程式碼。

### <a name="hosting-and-redeployment"></a>裝載和重新部署
重新部署的 hello 步驟是 hello 與部署任何現有的 Web API tooApp 服務相同。 步驟：

1. 建立空的 API 應用程式。 作法是在 hello 入口網站中使用 New > API 的應用程式，Visual Studio 從發行，或資源管理員工具中。 如果使用資源管理員工具或範本，設定 hello**種類**值太**api**上 hello **Microsoft.Web/sites**資源類型 toohave hello 快速入門和中的設定API 」 案例為目標的 hello 管理入口網站。
2. 連線並部署您的專案 toohello 空白應用程式開發介面的應用程式使用任何支援的應用程式服務的 hello 部署機制。 讀取[Azure App Service 部署文件](../app-service-web/web-sites-deploy.md)toolearn 更多。 

### <a name="authentication"></a>驗證
hello 應用程式服務驗證服務支援 hello 件以 hello 先前的應用程式開發介面應用程式模型的相同功能。 如果您使用工作階段權杖，並需要 Sdk，請使用下列用戶端和伺服器 Sdk 的 hello:

* 用戶端： [Azure 行動用戶端 SDK](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* 伺服器： [Microsoft Azure 行動應用程式 .NET 驗證延伸模組](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

如果您改為使用 hello App Service alpha Sdk，這些是目前已被取代：

* 用戶端： [Microsoft Azure AppService SDK](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* 伺服器： [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

特別與 Azure Active Directory，不過，沒有應用程式特定服務時需要您直接使用 hello AAD 語彙基元。

### <a name="internal-access"></a>內部存取
hello 先前 API 應用程式的模型中包含內建的內部存取層級。 需要使用 hello SDK 的簽署要求。 如前文所述，使用新的 API 應用程式模型 hello，AAD 服務主體可用的替代方式來服務對服務驗證而不需要應用程式服務-特定 SDK。 在 [在 Azure App Service 中 API Apps 的服務主體驗證](app-service-api-dotnet-service-principal-auth.md)中深入了解。

### <a name="discovery"></a>探索
前一個應用程式開發介面應用程式模型來探索其他應用程式開發介面的應用程式在執行階段中有應用程式開發介面 hello 後方的相同資源群組的 hello hello 相同閘道器。 這在實作微服務模式的架構中特別有用。 雖然不直接支援，但是有許多選項可用：

1. 使用 Azure 資源管理員 API 的 hello 進行探索。
2. 將 Azure API 管理放在您的 App Service 裝載 API 的前面。 Azure API 管理做為外觀，可以提供穩定的對外 URL，即使您的內部拓撲變更。
3. 建置您自己探索 API 應用程式，並有向 hello 探索應用程式在啟動其他應用程式開發介面應用程式。
4. 在部署期間填入 hello 應用程式設定，所有 hello API 應用程式 （和用戶端） 的 hello hello 端點其他應用程式開發介面應用程式。 這是可在範本部署，但因為應用程式開發介面應用程式現在讓您控制的 hello url。

## <a name="using-api-apps-with-logic-apps"></a>搭配使用 API Apps 與 Logic Apps
hello 新 API 的應用程式模型適用於[Logic Apps 結構描述版本 2015年-08-01](../logic-apps/logic-apps-schema-2015-08-01.md)。

## <a name="next-steps"></a>後續步驟
toolearn 詳細資訊，讀取 hello 文件以 hello [API 應用程式文件章節](https://azure.microsoft.com/documentation/services/app-service/api/)。 已更新的 tooreflect hello 新模型的 API 應用程式。 此外，請勿連接上的其他詳細資料] 或 [移轉指引的 hello 論壇：

* [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)

