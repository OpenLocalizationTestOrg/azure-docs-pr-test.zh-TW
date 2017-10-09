---
title: "aaaCache ASP.NET 輸出快取提供者"
description: "深入了解如何使用 Azure Redis 快取 toocache ASP.NET 頁面輸出"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="599f3-103">Azure Redis 快取的 ASP.NET 輸出快取提供者</span><span class="sxs-lookup"><span data-stu-id="599f3-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="599f3-104">hello Redis 輸出快取提供者是輸出快取資料的跨處理序儲存機制。</span><span class="sxs-lookup"><span data-stu-id="599f3-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="599f3-105">此資料特別適用於完整 HTTP 回應 (頁面輸出快取)。</span><span class="sxs-lookup"><span data-stu-id="599f3-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="599f3-106">hello 提供者插入 hello 新輸出快取提供者擴充性點 ASP.NET 4 中導入。</span><span class="sxs-lookup"><span data-stu-id="599f3-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="599f3-107">toouse hello Redis 的輸出快取提供者，先設定您的快取，然後再設定您的 ASP.NET 應用程式使用 hello Redis 輸出快取提供者 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="599f3-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="599f3-108">本主題提供指引，設定您的應用程式 toouse hello Redis 輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="599f3-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="599f3-109">如需建立和設定 Azure Redis 快取執行個體的相關詳細資訊，請參閱 [建立快取](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)。</span><span class="sxs-lookup"><span data-stu-id="599f3-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="599f3-110">Hello 快取中儲存 ASP.NET 頁面輸出</span><span class="sxs-lookup"><span data-stu-id="599f3-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="599f3-111">tooconfigure 用戶端應用程式，在 Visual Studio 中使用 hello Redis 快取工作階段狀態 NuGet 封裝，按一下**NuGet 套件管理員**， **Package Manager Console**從 hello**工具**功能表。</span><span class="sxs-lookup"><span data-stu-id="599f3-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="599f3-112">執行 hello 下列命令從 hello`Package Manager Console`視窗。</span><span class="sxs-lookup"><span data-stu-id="599f3-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="599f3-113">hello Redis 輸出快取提供者 NuGet 封裝 hello StackExchange.Redis.StrongName 封裝上具有相依性。</span><span class="sxs-lookup"><span data-stu-id="599f3-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="599f3-114">如果 hello StackExchange.Redis.StrongName 封裝不存在專案中，它會安裝。</span><span class="sxs-lookup"><span data-stu-id="599f3-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="599f3-115">如需 hello Redis 輸出快取提供者 NuGet 封裝的詳細資訊，請參閱 hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet 頁面。</span><span class="sxs-lookup"><span data-stu-id="599f3-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="599f3-116">在加法 toohello 強式名稱 StackExchange.Redis.StrongName 封裝，還有 hello StackExchange.Redis 非強式命名版本。</span><span class="sxs-lookup"><span data-stu-id="599f3-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="599f3-117">如果您的專案使用 hello 非強式命名 StackExchange.Redis 版本必須先解除安裝，否則您發生命名衝突專案中。</span><span class="sxs-lookup"><span data-stu-id="599f3-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="599f3-118">如需這些封裝的相關詳細資訊，請參閱 [設定 .NET 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。</span><span class="sxs-lookup"><span data-stu-id="599f3-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="599f3-119">hello NuGet 封裝下載並新增 hello 需要組件參考，並新增下列區段到您的 web.config 檔案的 hello。</span><span class="sxs-lookup"><span data-stu-id="599f3-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="599f3-120">本節包含您 ASP.NET 應用程式 toouse hello Redis 輸出快取提供者的 hello 必要的設定。</span><span class="sxs-lookup"><span data-stu-id="599f3-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="599f3-121">hello 標記為註解 > 一節提供 hello 屬性和每個屬性的範例設定的範例。</span><span class="sxs-lookup"><span data-stu-id="599f3-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="599f3-122">設定您在 hello Microsoft Azure 入口網站的快取刀鋒伺服器中的 hello 值 hello 屬性並設定 hello 所需的其他值。</span><span class="sxs-lookup"><span data-stu-id="599f3-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="599f3-123">如需存取快取屬性的指示，請參閱 [設定 Redis 快取設定](cache-configure.md#configure-redis-cache-settings)。</span><span class="sxs-lookup"><span data-stu-id="599f3-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="599f3-124">**主機** – 指定您的快取端點。</span><span class="sxs-lookup"><span data-stu-id="599f3-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="599f3-125">**連接埠**– 使用非 SSL 連接埠或您的 SSL 連接埠，取決於 hello ssl 設定。</span><span class="sxs-lookup"><span data-stu-id="599f3-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="599f3-126">**accessKey** – 用於您的快取中的任一 hello 主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="599f3-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="599f3-127">**ssl** – 如果您想要以 ssl toosecure 快取/用戶端通訊，則為 true，否則為 false。</span><span class="sxs-lookup"><span data-stu-id="599f3-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="599f3-128">為確定 toospecify hello 正確的連接埠。</span><span class="sxs-lookup"><span data-stu-id="599f3-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="599f3-129">新的快取預設為停用 hello 非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="599f3-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="599f3-130">指定 true，此設定 toouse hello SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="599f3-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="599f3-131">如需有關如何啟用 hello 非 SSL 連接埠的詳細資訊，請參閱 hello[存取連接埠](cache-configure.md#access-ports)> 一節中 hello[設定快取](cache-configure.md)主題。</span><span class="sxs-lookup"><span data-stu-id="599f3-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="599f3-132">**databaseId** – 指定快取哪些資料庫 toouse 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="599f3-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="599f3-133">如果未指定，會使用 hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="599f3-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="599f3-134">**applicationName** – 金鑰在 redis 中會儲存為 `<AppName>_<SessionId>_Data`。</span><span class="sxs-lookup"><span data-stu-id="599f3-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="599f3-135">這個命名配置可讓多個應用程式 tooshare hello 相同索引鍵。</span><span class="sxs-lookup"><span data-stu-id="599f3-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="599f3-136">此參數是選擇性的，如果您未提供，將會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="599f3-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="599f3-137">**connectionTimeoutInMilliseconds** – 此設定可讓您 toooverride hello connectTimeout hello StackExchange.Redis 用戶端中設定。</span><span class="sxs-lookup"><span data-stu-id="599f3-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="599f3-138">如果未指定，會使用 hello 預設 connectTimeout 值為 5000。</span><span class="sxs-lookup"><span data-stu-id="599f3-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="599f3-139">如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。</span><span class="sxs-lookup"><span data-stu-id="599f3-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="599f3-140">**operationTimeoutInMilliseconds** – 此設定可讓您 toooverride hello syncTimeout hello StackExchange.Redis 用戶端中設定。</span><span class="sxs-lookup"><span data-stu-id="599f3-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="599f3-141">如果未指定，會使用 hello syncTimeout 預設為 1000年。</span><span class="sxs-lookup"><span data-stu-id="599f3-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="599f3-142">如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。</span><span class="sxs-lookup"><span data-stu-id="599f3-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="599f3-143">新增您想 toocache hello 輸出 OutputCache 指示詞 tooeach 頁面。</span><span class="sxs-lookup"><span data-stu-id="599f3-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="599f3-144">Hello 上述範例中，在 hello 快取頁面 hello 快取中的資料仍會保留 60 秒，而每一個參數組合快取不同版本的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="599f3-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="599f3-145">如需 hello OutputCache 指示詞的詳細資訊，請參閱[ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837)。</span><span class="sxs-lookup"><span data-stu-id="599f3-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="599f3-146">一旦執行了這些步驟，您的應用程式是設定的 toouse hello Redis 輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="599f3-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="599f3-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="599f3-147">Next steps</span></span>
<span data-ttu-id="599f3-148">簽出 hello [Azure Redis 快取的 ASP.NET 工作階段狀態提供者](cache-aspnet-session-state-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="599f3-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

