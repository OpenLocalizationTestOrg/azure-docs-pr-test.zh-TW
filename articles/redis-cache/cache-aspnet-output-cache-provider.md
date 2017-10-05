---
title: "快取 ASP.NET 輸出快取提供者"
description: "了解如何使用 Azure Redis 快取進行 ASP.NET 頁面輸出快取"
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
ms.openlocfilehash: 845f25637a0e48460fc76c1ee36060274b3cec38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="98683-103">Azure Redis 快取的 ASP.NET 輸出快取提供者</span><span class="sxs-lookup"><span data-stu-id="98683-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="98683-104">Redis 輸出快取提供者為輸出快取資料的程序外儲存體機制。</span><span class="sxs-lookup"><span data-stu-id="98683-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="98683-105">此資料特別適用於完整 HTTP 回應 (頁面輸出快取)。</span><span class="sxs-lookup"><span data-stu-id="98683-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="98683-106">提供者插入 ASP.NET 4 中導入的新輸出快取提供者擴充點。</span><span class="sxs-lookup"><span data-stu-id="98683-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="98683-107">若要使用 Redis 輸出快取提供者，請先設定您的快取，然後使用「Redis 輸出快取提供者 NuGet 封裝」設定 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98683-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="98683-108">本主題提供為使用 Redis 輸出快取提供者而進行應用程式設定的相關指引。</span><span class="sxs-lookup"><span data-stu-id="98683-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span></span> <span data-ttu-id="98683-109">如需建立和設定 Azure Redis 快取執行個體的相關詳細資訊，請參閱 [建立快取](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)。</span><span class="sxs-lookup"><span data-stu-id="98683-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-the-cache"></a><span data-ttu-id="98683-110">將 ASP.NET 頁面輸出儲存在快取中</span><span class="sxs-lookup"><span data-stu-id="98683-110">Store ASP.NET page output in the cache</span></span>
<span data-ttu-id="98683-111">若要在 Visual Studio 中使用「Redis 快取工作階段狀態 NuGet 套件」來設定用戶端應用程式，請依序按一下 [工具] 功能表中的 [NuGet 套件管理員] 和 [套件管理器主控台]。</span><span class="sxs-lookup"><span data-stu-id="98683-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="98683-112">從 `Package Manager Console` 視窗執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="98683-112">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="98683-113">「Redis 輸出快取提供者 NuGet 封裝」對「StackExchange.Redis.StrongName 封裝」有相依性。</span><span class="sxs-lookup"><span data-stu-id="98683-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="98683-114">如果 StackExchange.Redis.StrongName 封裝不在專案中，代表已經安裝。</span><span class="sxs-lookup"><span data-stu-id="98683-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="98683-115">如需「Redis 輸出快取提供者 NuGet 套件」的詳細資訊，請參閱 [RedisOutputCacheProvider (英文)](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet 頁面。</span><span class="sxs-lookup"><span data-stu-id="98683-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="98683-116">除了強式名稱的 StackExchange.Redis.StrongName 封裝外，另外還有非強式名稱版本的 StackExchange.Redis。</span><span class="sxs-lookup"><span data-stu-id="98683-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="98683-117">如果您的專案使用非強式名稱的 StackExchange.Redis 版本，您必須將它解除安裝，否則專案中會發生命名衝突。</span><span class="sxs-lookup"><span data-stu-id="98683-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="98683-118">如需這些封裝的相關詳細資訊，請參閱 [設定 .NET 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。</span><span class="sxs-lookup"><span data-stu-id="98683-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="98683-119">NuGet 封裝會下載和加入必要的組件參考，並將下列區段加入您的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="98683-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="98683-120">此區段包含讓您的 ASP.NET 應用程式使用 Redis 輸出快取提供者所需的設定。</span><span class="sxs-lookup"><span data-stu-id="98683-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="98683-121">標示註解的區段可提供屬性的範例和每個屬性的範例設定。</span><span class="sxs-lookup"><span data-stu-id="98683-121">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="98683-122">以來自 Microsoft Azure 入口網站之快取刀鋒視窗的值來設定屬性，並視需要設定其他值。</span><span class="sxs-lookup"><span data-stu-id="98683-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="98683-123">如需存取快取屬性的指示，請參閱 [設定 Redis 快取設定](cache-configure.md#configure-redis-cache-settings)。</span><span class="sxs-lookup"><span data-stu-id="98683-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="98683-124">**主機** – 指定您的快取端點。</span><span class="sxs-lookup"><span data-stu-id="98683-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="98683-125">**連接埠** – 使用您的非 SSL 連接埠或 SSL 連接埠，依 ssl 設定而定。</span><span class="sxs-lookup"><span data-stu-id="98683-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="98683-126">**accessKey** – 用於快取的主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="98683-126">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="98683-127">**ssl** – 如果您想要使用 ssl 保護快取/用戶端通訊則為 true，否則為 false。</span><span class="sxs-lookup"><span data-stu-id="98683-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="98683-128">請務必指定正確的連接埠。</span><span class="sxs-lookup"><span data-stu-id="98683-128">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="98683-129">預設會為新快取停用非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="98683-129">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="98683-130">請於此設定指定為 true，使用 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="98683-130">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="98683-131">如需啟用非 SSL 連接埠的相關詳細資訊，請參閱[設定快取](cache-configure.md)主題中的[存取連接埠](cache-configure.md#access-ports)一節。</span><span class="sxs-lookup"><span data-stu-id="98683-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="98683-132">**databaseId** – 指定快取輸出資料所使用的資料庫。</span><span class="sxs-lookup"><span data-stu-id="98683-132">**databaseId** – Specified which database to use for cache output data.</span></span> <span data-ttu-id="98683-133">若未指定，就會使用預設值 0。</span><span class="sxs-lookup"><span data-stu-id="98683-133">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="98683-134">**applicationName** – 金鑰在 redis 中會儲存為 `<AppName>_<SessionId>_Data`。</span><span class="sxs-lookup"><span data-stu-id="98683-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="98683-135">這個命名配置可讓多個應用程式共用同一金鑰。</span><span class="sxs-lookup"><span data-stu-id="98683-135">This naming scheme enables multiple applications to share the same key.</span></span> <span data-ttu-id="98683-136">此參數是選擇性的，如果您未提供，將會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="98683-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="98683-137">**connectionTimeoutInMilliseconds** – 此設定可讓您覆寫 StackExchange.Redis 用戶端中的 connectTimeout 設定。</span><span class="sxs-lookup"><span data-stu-id="98683-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="98683-138">若未指定，將會使用預設的 connectTimeout 設定為 5000。</span><span class="sxs-lookup"><span data-stu-id="98683-138">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="98683-139">如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。</span><span class="sxs-lookup"><span data-stu-id="98683-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="98683-140">**operationTimeoutInMilliseconds** – 此設定可讓您覆寫 StackExchange.Redis 用戶端中的 syncTimeout 設定。</span><span class="sxs-lookup"><span data-stu-id="98683-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="98683-141">若未指定，將會使用預設的 syncTimeout 設定為 1000。</span><span class="sxs-lookup"><span data-stu-id="98683-141">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="98683-142">如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。</span><span class="sxs-lookup"><span data-stu-id="98683-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="98683-143">將 OutputCache 指示詞新增至每一個您要快取輸出的頁面。</span><span class="sxs-lookup"><span data-stu-id="98683-143">Add an OutputCache directive to each page for which you wish to cache the output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="98683-144">在上一個範例中，已快取的頁面資料會留在快取中 60 秒，而且會對每一個參數組合快取不同版本的頁面。</span><span class="sxs-lookup"><span data-stu-id="98683-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span></span> <span data-ttu-id="98683-145">如需 OutputCache 指示詞的相關詳細資訊，請參閱 [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837)。</span><span class="sxs-lookup"><span data-stu-id="98683-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="98683-146">一旦執行這些步驟，您的應用程式將設定為使用 Redis 輸出快取提供者。</span><span class="sxs-lookup"><span data-stu-id="98683-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98683-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98683-147">Next steps</span></span>
<span data-ttu-id="98683-148">請查看 [Azure Redis 快取的 ASP.NET 工作階段狀態提供者](cache-aspnet-session-state-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="98683-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

