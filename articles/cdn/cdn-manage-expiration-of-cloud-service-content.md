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
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="52bc5-103">在 Azure CDN 中管理 Azure Web Apps/雲端服務、ASP.NET 或 IIS 內容的到期</span><span class="sxs-lookup"><span data-stu-id="52bc5-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="52bc5-104">Azure Web Apps/雲端服務、ASP.NET 或 IIS</span><span class="sxs-lookup"><span data-stu-id="52bc5-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="52bc5-105">Azure 儲存體 Blob 服務</span><span class="sxs-lookup"><span data-stu-id="52bc5-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="52bc5-106">來自任何可公開存取的原始 Web 伺服器的檔案均可在 Azure CDN 中加以快取，直到其存留時間 (TTL) 結束。</span><span class="sxs-lookup"><span data-stu-id="52bc5-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="52bc5-107">hello TTL 由 hello [ *Cache-control*標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)在 hello HTTP 回應 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="52bc5-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="52bc5-108">本文說明如何 tooset `Cache-Control` Azure Web 應用程式、 Azure 雲端服務、 ASP.NET 應用程式和 Internet Information Services 站台，同樣地設定所有的標頭。</span><span class="sxs-lookup"><span data-stu-id="52bc5-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="52bc5-109">您可以選擇 tooset 檔案沒有 TTL。</span><span class="sxs-lookup"><span data-stu-id="52bc5-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="52bc5-110">在此情況下，Azure CDN 會自動套用預設為期 7 天的 TTL。</span><span class="sxs-lookup"><span data-stu-id="52bc5-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="52bc5-111">如需有關 Azure CDN toospeed 存取 toofiles 和其他資源的運作方式的詳細資訊，請參閱 hello [Azure CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="52bc5-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="52bc5-112">在組態中設定 Cache-Control 標頭</span><span class="sxs-lookup"><span data-stu-id="52bc5-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="52bc5-113">針對靜態內容，例如影像和樣式表，您可以藉由修改 hello 控制 hello 更新頻率**applicationHost.config**或**web.config** web 應用程式的檔案。</span><span class="sxs-lookup"><span data-stu-id="52bc5-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="52bc5-114">hello **system.webServer\staticContent\clientCache** hello 組態檔中的項目會設定 hello`Cache-Control`標頭為您的內容。</span><span class="sxs-lookup"><span data-stu-id="52bc5-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="52bc5-115">如**web.config**，hello 組態設定會影響所有項目中 hello 資料夾及所有子資料夾，除非在 hello 子資料夾層級覆寫。</span><span class="sxs-lookup"><span data-stu-id="52bc5-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="52bc5-116">例如，您可以設定預設存留時間在 hello 根 toohave 所有靜態內容 3 天，快取，但是已有多個變數的內容快取設為 6 小時的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="52bc5-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="52bc5-117">如**applicationHost.config**，hello 站台上的所有應用程式會受到影響，但您可以覆寫**web.config** hello 應用程式中的檔案。</span><span class="sxs-lookup"><span data-stu-id="52bc5-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="52bc5-118">hello 下列 XML 顯示範例設定**clientCache** toospecify 的最長使用期限為 3 天：</span><span class="sxs-lookup"><span data-stu-id="52bc5-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="52bc5-119">指定**UseMaxAge**新增`Cache-Control: max-age=<nnn>`hello hello 中指定的值為基礎的標頭 toohello 回應**CacheControlMaxAge**屬性。</span><span class="sxs-lookup"><span data-stu-id="52bc5-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="52bc5-120">hello timespan hello 格式為 hello **cacheControlMaxAge**屬性是<days>。<hours>:<min>:<sec>。</span><span class="sxs-lookup"><span data-stu-id="52bc5-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="52bc5-121">如需有關 hello **clientCache**  節點，請參閱[用戶端快取<clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)。</span><span class="sxs-lookup"><span data-stu-id="52bc5-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="52bc5-122">在程式碼中設定 Cache-Control 標頭</span><span class="sxs-lookup"><span data-stu-id="52bc5-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="52bc5-123">ASP.NET 應用程式，您可以設定 hello CDN 快取行為以程式設計方式設定 hello **HttpResponse.Cache**屬性。</span><span class="sxs-lookup"><span data-stu-id="52bc5-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="52bc5-124">如需有關 hello **HttpResponse.Cache**屬性，請參閱[HttpResponse.Cache 屬性](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx)和[HttpCachePolicy 類別](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)。</span><span class="sxs-lookup"><span data-stu-id="52bc5-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="52bc5-125">如果您想在 ASP.NET 中的 tooprogrammatically 快取應用程式內容，請確定 httpcacheability 太標示為可快取 hello 內容*公用*。</span><span class="sxs-lookup"><span data-stu-id="52bc5-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="52bc5-126">也請確定已設定快取驗證程式。</span><span class="sxs-lookup"><span data-stu-id="52bc5-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="52bc5-127">hello 快取驗證程式的上次修改可由呼叫 SetETag 所設定的時間戳記設定藉由呼叫 SetLastModified 或 etag 值。</span><span class="sxs-lookup"><span data-stu-id="52bc5-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="52bc5-128">（選擇性） 您也可以透過呼叫 SetExpires，指定快取到期時間，或您可以依賴 hello 預設快取本文件稍早所述的啟發學習法。</span><span class="sxs-lookup"><span data-stu-id="52bc5-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="52bc5-129">例如，一個小時的 toocache 內容加入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="52bc5-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="52bc5-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52bc5-130">Next Steps</span></span>
* [<span data-ttu-id="52bc5-131">讀取詳細 hello **clientCache**項目</span><span class="sxs-lookup"><span data-stu-id="52bc5-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="52bc5-132">閱讀 hello 文件以 hello **HttpResponse.Cache**屬性</span><span class="sxs-lookup"><span data-stu-id="52bc5-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="52bc5-133">[閱讀 hello 文件以 hello **HttpCachePolicy 類別**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)。</span><span class="sxs-lookup"><span data-stu-id="52bc5-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

