---
title: "Azure LBS 概觀 | Microsoft Docs"
description: "Azure LBS (預覽) 簡介"
services: location-based-services
keywords: 
author: dsk-2015
ms.author: dkshir
ms.date: 11/28/2017
ms.topic: overview
ms.service: location-based-services
documentationcenter: 
manager: timlt
ms.devlang: na
ms.custom: mvc
ms.openlocfilehash: 6871f174eb9bae57d9b4767520d0fb2d8d9631d3
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="an-introduction-to-azure-location-based-services-preview"></a>Azure LBS (預覽) 簡介
Azure LBS 是地理空間服務的組合，內含地圖、搜尋、路線規劃、路況和時區的服務 API。 符合 Azure OneAPI 規範的服務組合可讓您使用熟悉的開發人員工具，快速開發和調整解決方案，進而將位置資訊整合到 Azure 解決方案中。 Azure LBS 可提供各產業的開發人員強大的地理空間功能，另納入最新的地圖資料，可提供 Web 和行動裝置應用程式的地理空間內容。 Azure LBS 是符合 Azure One API 規範的 REST API 集合，附有網頁型 JavaScript 控制項可讓開發作業變得超級容易、有彈性且可在多個媒介中轉移。 

Azure LBS 包含五項主要服務，可支持需要地理內容的 Azure 應用程式。 以下將詳細說明每項服務。

**轉譯服務** – 轉譯服務是針對開發人員而設計的服務，可建立以地圖服務為主的 Web 和行動裝置應用程式。 此服務會使用高品質點陣圖形影像 (提供 19 個縮放層級)，或可完全自訂的向量格式地圖影像。

![Azure Location Based Services Map.png](media/about-location-based-services/Introduction_Map.png)

**路線規劃服務**– 路線規劃服務是使用強固的真實世界基礎結構幾何計算與多個傳輸模式方向來建置。 此服務可讓開發人員計算多種行進模式 (例如汽車、卡車、自行車或步行) ，以及多項輸入 (例如路況、重量限制或危險物質運輸) 的方向。

![Azure Location Based Services Route.png](media/about-location-based-services/Introduction_Route.png)

**搜尋服務** - 搜尋服務是針對開發人員而設計的服務，可搜尋地址、位置、依名稱或類別的商務清單，以及其他地理資訊。 搜尋服務也可以根據經緯度進行地址和交叉路口的[反向地理編碼](https://en.wikipedia.org/wiki/Reverse_geocoding)。 

![Azure Location Based Services Search.png](media/about-location-based-services/Introduction_Search.png)

**時區服務** – 時區服務可讓您使用其中一組經緯度或 [IANA 識別碼](http://www.iana.org/)，查詢目前、過去及未來的時區資訊。 時區服務也可將 Microsoft Windows 時區識別碼轉換為 IANA 時區、擷取 UTC 的時區位移，以及取得各自時區中的目前時間。 時區服務查詢的典型 JSON 回應如下所示：

```JSON
{
    "Version": "2017c",
    "ReferenceUtcTimestamp": "2017-11-20T23:09:48.686173Z",
    "TimeZones": [{
        "Id": "America/Los_Angeles",
        "ReferenceTime": {
            "Tag": "PST",
            "StandardOffset": "-08:00:00",
            "DaylightSavings": "00:00:00",
            "WallTime": "2017-11-20T15:09:48.686173-08:00",
            "PosixTzValidYear": 2017,
            "PosixTz": "PST+8PDT,M3.2.0,M11.1.0"
        }
    }]
}
```

**交通服務** – 交通服務是針對開發人員而設計的一套 Web 服務，可建立需要路況的 Web 和行動裝置應用程式。 此供應項目分成下列部分：
1. 交通流量 - 針對網路中的所有重要道路提供即時觀察速度和行進時間；以及 
2. 交通事故 - 提供有關道路網路中塞車和交通事故的精確檢視。

![Azure LBS - 交通](media/about-location-based-services/Introduction_Traffic.png)

Azure LBS 是為了行動性而建置，可以增強跨平台應用程式的功能，因為此程式設計模型無從驗證並透過 REST API 支援 JSON 輸出。 此外，Azure LBS 使用簡單的程式設計模型提供方便的 JavaScript 地圖控制項，以便快速輕鬆開發 Web 和行動裝置應用程式。 

Azure LBS 使用以金鑰為基礎的驗證配置，所以存取服務時需瀏覽至 [Azure 入口網站](http://portal.azure.com)並建立 Azure LBS 帳戶。 您的帳戶隨附預先為您產生的兩個金鑰。 在 Azure LBS 的要求中使用任一個金鑰，開始將這些位置功能直接整合到您的應用程式中。

**與 Bing 地圖的關聯性** - 請注意，本文件中描述的 Azure 位置服務與 Bing 地圖提供的服務有所不同。  雖然兩者共用許多相同的功能，但是這兩項服務不同而且也不相關。  Azure 內這項新服務的可用性不會對 Bing 地圖產品供應項目或藍圖造成影響，它們是個別管理的。

Microsoft 的目標是為開發人員社群提供位置服務供應項目的選擇。  開發人員可以參考下列快速指引，針對各種使用案例和客戶情況決定要使用何種服務。  請注意，此指引目前適用於 Azure LBS，因為它處於公開預覽階段，當它在 2018 年正式運作之後即會更新。

| 客戶準則 | 使用 Azure 位置服務的時機： | 使用 Bing 地圖的時機： |
| ------------- | ------------- | ------------- |
| 開發環境 | 建置或利用其他 Azure 服務 | 使用協力廠商雲端或其他開發人員環境 |
| 開發階段  | 因為 Azure LBS 目前正在公開預覽，它會針對早期階段測試和概念證明開發最佳化 | 生產環境需要企業等級 SLA |
| 定價選項 | 初步開發人員定價選項即足夠 | 需要自訂企業等級定價 |
| 使用案例環境 | 需要車載使用 | 不需要車載使用 |
| 地理涵蓋範圍 | 印度、中國、日本及韓國不是必要項 | 印度、中國、日本及韓國地圖涵蓋範圍是必要項 |
| 地圖內容 | 標準表面地圖就已足夠 | 衛星、鳥瞰和街景圖是必要項 |
| 基礎地圖來源 | 偏好 TomTom 地圖資料 | 偏好 HERE 地圖資料 |

立即註冊 [Azure LBS 帳戶！](http://aka.ms/azurelbsportal)

## <a name="next-steps"></a>後續步驟

您現在已大致了解 Azure LBS (預覽)。 下一個步驟是試用可展示位置服務的範例應用程式，以及在您的 Web 應用程式中建立端對端案例。

> [!div class="nextstepaction"]
> [使用 Azure LBS (預覽) 來啟動示範互動式地圖搜尋](quick-demo-map-app.md)
> [使用 Azure LBS 來搜尋附近景點](tutorial-search-location.md)
