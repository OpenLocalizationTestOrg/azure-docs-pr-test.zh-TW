---
title: "在 Azure CDN 中管理 Web 內容的到期 | Microsoft Docs"
description: "了解如何在 Azure CDN 中管理 Azure Web Apps/雲端服務、ASP.NET 或 IIS 內容的到期。"
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
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="5d7a1-103">在 Azure CDN 中管理 Azure Web Apps/雲端服務、ASP.NET 或 IIS 內容的到期</span><span class="sxs-lookup"><span data-stu-id="5d7a1-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d7a1-104">Azure Web Apps/雲端服務、ASP.NET 或 IIS</span><span class="sxs-lookup"><span data-stu-id="5d7a1-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="5d7a1-105">Azure 儲存體 Blob 服務</span><span class="sxs-lookup"><span data-stu-id="5d7a1-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="5d7a1-106">來自任何可公開存取的原始 Web 伺服器的檔案均可在 Azure CDN 中加以快取，直到其存留時間 (TTL) 結束。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="5d7a1-107">TTL 是由來自原始伺服器之 HTTP 回應中的 [*Cache-Control* 標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)所決定。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="5d7a1-108">本文說明如何設定Azure Web Apps、Azure 雲端服務、ASP.NET 應用程式和 Internet Information Services 網站的 `Cache-Control` 標頭，上述所有項目的設定方式均類似。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="5d7a1-109">您可以選擇不對檔案設定 TTL。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="5d7a1-110">在此情況下，Azure CDN 會自動套用預設為期 7 天的 TTL。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="5d7a1-111">如需 Azure CDN 如何運作以加快檔案和其他資源存取速度的詳細資訊，請參閱 [Azure CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="5d7a1-112">在組態中設定 Cache-Control 標頭</span><span class="sxs-lookup"><span data-stu-id="5d7a1-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="5d7a1-113">針對影像和樣式表之類的靜態內容，您可以藉由修改 Web 應用程式的 **applicationHost.config** 或 **web.config** 檔案來控制更新頻率。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="5d7a1-114">組態檔中的 **system.webServer\staticContent\clientCache** 項目會設定內容的 `Cache-Control` 標頭。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="5d7a1-115">針對 **web.config**，除非在子資料夾層級中加以覆寫，否則組態設定會影響資料夾和所有子資料夾中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="5d7a1-116">例如，您可以設定根目錄的預設存留時間具有快取 3 天的所有靜態內容，但是有一個子資料夾具有快取設定為 6 小時的更多變數內容。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="5d7a1-117">針對 **applicationHost.config**，網站上的所有應用程式都會受到影響，但可在應用程式的 **web.config** 檔案中加以覆寫。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="5d7a1-118">下列 XML 說明設定 **clientCache** 以指定最長使用期限 (3 天) 的範例：</span><span class="sxs-lookup"><span data-stu-id="5d7a1-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="5d7a1-119">指定 **UseMaxAge**，會根據 **CacheControlMaxAge** 屬性中所指定的值，將 `Cache-Control: max-age=<nnn>` 標頭加入回應。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="5d7a1-120">**cacheControlMaxAge** 屬性的 timespan 格式為 <days>.<hours>:<min>:<sec>。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="5d7a1-121">如需 **clientCache** 節點的詳細資訊，請參閱[用戶端快取<clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="5d7a1-122">在程式碼中設定 Cache-Control 標頭</span><span class="sxs-lookup"><span data-stu-id="5d7a1-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="5d7a1-123">針對 ASP.NET 應用程式，設定 **HttpResponse.Cache** 屬性即可透過程式設計方式設定 CDN 快取行為。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="5d7a1-124">如需 **HttpResponse.Cache** 屬性的詳細資訊，請參閱 [HttpResponse.Cache 屬性](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx)和 [HttpCachePolicy 類別](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="5d7a1-125">如果您想要在 ASP.NET 中以程式設計方式快取應用程式內容，請務必將 HttpCacheability 設為「Public」 ，以將內容標示為可進行快取。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="5d7a1-126">也請確定已設定快取驗證程式。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="5d7a1-127">快取驗證程式可以是透過呼叫 SetLastModified 所設定的上次修改時間戳記，或透過呼叫 SetETag 所設定的 etag 值。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="5d7a1-128">您也可以選擇性地透過呼叫 SetExpires 來指定快取到期時間，或可以依賴本文件稍早所述的預設快取啟發學習法。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="5d7a1-129">例如，若要快取一個小時的內容，請加入下列內容：</span><span class="sxs-lookup"><span data-stu-id="5d7a1-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="5d7a1-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d7a1-130">Next Steps</span></span>
* [<span data-ttu-id="5d7a1-131">深入了解 **clientCache** 項目</span><span class="sxs-lookup"><span data-stu-id="5d7a1-131">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="5d7a1-132">閱讀 **HttpResponse.Cache** 屬性的文件</span><span class="sxs-lookup"><span data-stu-id="5d7a1-132">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="5d7a1-133">[閱讀 **HttpCachePolicy 類別**的文件](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d7a1-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

