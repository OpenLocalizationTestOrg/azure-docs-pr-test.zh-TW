---
title: "Azure CDN 中的 web 內容 aaaManage 到期 |Microsoft 文件"
description: "深入了解如何在 Azure CDN 中的 Azure Web 應用程式/雲端服務、 ASP.NET 或 IIS 內容 toomanage 到期。"
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>在 Azure CDN 中管理 Azure Web Apps/雲端服務、ASP.NET 或 IIS 內容的到期
> [!div class="op_single_selector"]
> * [Azure Web Apps/雲端服務、ASP.NET 或 IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure 儲存體 Blob 服務](cdn-manage-expiration-of-blob-content.md)
> 
> 

來自任何可公開存取的原始 Web 伺服器的檔案均可在 Azure CDN 中加以快取，直到其存留時間 (TTL) 結束。  hello TTL 由 hello [ *Cache-control*標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)在 hello HTTP 回應 hello 原始伺服器。  本文說明如何 tooset `Cache-Control` Azure Web 應用程式、 Azure 雲端服務、 ASP.NET 應用程式和 Internet Information Services 站台，同樣地設定所有的標頭。

> [!TIP]
> 您可以選擇 tooset 檔案沒有 TTL。  在此情況下，Azure CDN 會自動套用預設為期 7 天的 TTL。
> 
> 如需有關 Azure CDN toospeed 存取 toofiles 和其他資源的運作方式的詳細資訊，請參閱 hello [Azure CDN 概觀](cdn-overview.md)。
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>在組態中設定 Cache-Control 標頭
針對靜態內容，例如影像和樣式表，您可以藉由修改 hello 控制 hello 更新頻率**applicationHost.config**或**web.config** web 應用程式的檔案。  hello **system.webServer\staticContent\clientCache** hello 組態檔中的項目會設定 hello`Cache-Control`標頭為您的內容。 如**web.config**，hello 組態設定會影響所有項目中 hello 資料夾及所有子資料夾，除非在 hello 子資料夾層級覆寫。  例如，您可以設定預設存留時間在 hello 根 toohave 所有靜態內容 3 天，快取，但是已有多個變數的內容快取設為 6 小時的子資料夾。  如**applicationHost.config**，hello 站台上的所有應用程式會受到影響，但您可以覆寫**web.config** hello 應用程式中的檔案。

hello 下列 XML 顯示範例設定**clientCache** toospecify 的最長使用期限為 3 天：  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

指定**UseMaxAge**新增`Cache-Control: max-age=<nnn>`hello hello 中指定的值為基礎的標頭 toohello 回應**CacheControlMaxAge**屬性。 hello timespan hello 格式為 hello **cacheControlMaxAge**屬性是<days>。<hours>:<min>:<sec>。 如需有關 hello **clientCache**  節點，請參閱[用戶端快取<clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)。  

## <a name="setting-cache-control-headers-in-code"></a>在程式碼中設定 Cache-Control 標頭
ASP.NET 應用程式，您可以設定 hello CDN 快取行為以程式設計方式設定 hello **HttpResponse.Cache**屬性。 如需有關 hello **HttpResponse.Cache**屬性，請參閱[HttpResponse.Cache 屬性](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx)和[HttpCachePolicy 類別](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)。  

如果您想在 ASP.NET 中的 tooprogrammatically 快取應用程式內容，請確定 httpcacheability 太標示為可快取 hello 內容*公用*。 也請確定已設定快取驗證程式。 hello 快取驗證程式的上次修改可由呼叫 SetETag 所設定的時間戳記設定藉由呼叫 SetLastModified 或 etag 值。 （選擇性） 您也可以透過呼叫 SetExpires，指定快取到期時間，或您可以依賴 hello 預設快取本文件稍早所述的啟發學習法。  

例如，一個小時的 toocache 內容加入 hello 下列：  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>後續步驟
* [讀取詳細 hello **clientCache**項目](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [閱讀 hello 文件以 hello **HttpResponse.Cache**屬性](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [閱讀 hello 文件以 hello **HttpCachePolicy 類別**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)。  

