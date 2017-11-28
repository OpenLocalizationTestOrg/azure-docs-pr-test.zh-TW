---
title: "ASP.NET 工作階段狀態提供者 aaaCache |Microsoft 文件"
description: "深入了解如何使用 Azure Redis 快取 toostore ASP.NET 工作階段狀態"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a><span data-ttu-id="46d6f-103">Azure Redis 快取的 ASP.NET 工作階段狀態提供者</span><span class="sxs-lookup"><span data-stu-id="46d6f-103">ASP.NET Session State Provider for Azure Redis Cache</span></span>
<span data-ttu-id="46d6f-104">Azure Redis 快取提供工作階段狀態提供者，您可以使用 toostore 快取，而不是記憶體中工作階段狀態，或在 SQL Server 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="46d6f-104">Azure Redis Cache provides a session state provider that you can use toostore your session state in a cache rather than in-memory or in a SQL Server database.</span></span> <span data-ttu-id="46d6f-105">toouse hello 快取工作階段狀態提供者，先設定您的快取，然後設定 快取使用 hello Redis 快取工作階段狀態 NuGet 封裝您的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="46d6f-105">toouse hello caching session state provider, first configure your cache, and then configure your ASP.NET application for cache using hello Redis Cache Session State NuGet package.</span></span>

<span data-ttu-id="46d6f-106">通常不是實際在真實世界雲端應用程式 tooavoid 某種形式的狀態儲存使用者工作階段，但某些方法會影響效能和延展性比其他更多。</span><span class="sxs-lookup"><span data-stu-id="46d6f-106">It's often not practical in a real-world cloud app tooavoid storing some form of state for a user session, but some approaches impact performance and scalability more than others.</span></span> <span data-ttu-id="46d6f-107">如果您有 toostore 狀態，hello 最佳解決方案是 tookeep hello 數量小狀態，並將它儲存在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="46d6f-107">If you have toostore state, hello best solution is tookeep hello amount of state small and store it in cookies.</span></span> <span data-ttu-id="46d6f-108">如果此方法不可行，hello 的下一個最佳解決方案是 toouse ASP.NET 工作階段狀態與分散式、 記憶體中快取提供者。</span><span class="sxs-lookup"><span data-stu-id="46d6f-108">If that isn't feasible, hello next best solution is toouse ASP.NET session state with a provider for distributed, in-memory cache.</span></span> <span data-ttu-id="46d6f-109">hello 效能和延展性的觀點而言最差的解決方式是 toouse 資料庫備份的工作階段狀態提供者。</span><span class="sxs-lookup"><span data-stu-id="46d6f-109">hello worst solution from a performance and scalability standpoint is toouse a database backed session state provider.</span></span> <span data-ttu-id="46d6f-110">本主題提供使用 Azure Redis 快取的 hello ASP.NET 工作階段狀態提供者的指引。</span><span class="sxs-lookup"><span data-stu-id="46d6f-110">This topic provides guidance on using hello ASP.NET Session State Provider for Azure Redis Cache.</span></span> <span data-ttu-id="46d6f-111">如需其他工作階段狀態選項的相關資訊，請參閱 [ASP.NET 工作階段狀態選項](#aspnet-session-state-options)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-111">For information on other session state options, see [ASP.NET Session State options](#aspnet-session-state-options).</span></span>

## <a name="store-aspnet-session-state-in-hello-cache"></a><span data-ttu-id="46d6f-112">Hello 快取中儲存 ASP.NET 工作階段狀態</span><span class="sxs-lookup"><span data-stu-id="46d6f-112">Store ASP.NET session state in hello cache</span></span>
<span data-ttu-id="46d6f-113">tooconfigure 用戶端應用程式，在 Visual Studio 中使用 hello Redis 快取工作階段狀態 NuGet 封裝，按一下**NuGet 套件管理員**， **Package Manager Console**從 hello**工具**功能表。</span><span class="sxs-lookup"><span data-stu-id="46d6f-113">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="46d6f-114">執行 hello 下列命令從 hello`Package Manager Console`視窗。</span><span class="sxs-lookup"><span data-stu-id="46d6f-114">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> <span data-ttu-id="46d6f-115">如果您使用 hello hello premium 層從叢集功能，您必須使用[RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 或更高版本，或例外狀況就會擲回。</span><span class="sxs-lookup"><span data-stu-id="46d6f-115">If you are using hello clustering feature from hello premium tier, you must use [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 or higher or an exception is thrown.</span></span> <span data-ttu-id="46d6f-116">移動 too2.0.1 或更高版本是中斷變更。如需詳細資訊，請參閱[v2.0.0 重大變更詳細資料](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-116">Moving too2.0.1 or higher is a breaking change; for more information, see [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).</span></span> <span data-ttu-id="46d6f-117">Hello 這個更新的發行項時，此封裝的 hello 目前版本是 2.2.3。</span><span class="sxs-lookup"><span data-stu-id="46d6f-117">At hello time of this article update, hello current version of this package is 2.2.3.</span></span>
> 
> 

<span data-ttu-id="46d6f-118">hello Redis 工作階段狀態提供者 NuGet 封裝 hello StackExchange.Redis.StrongName 封裝上具有相依性。</span><span class="sxs-lookup"><span data-stu-id="46d6f-118">hello Redis Session State Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="46d6f-119">如果 hello StackExchange.Redis.StrongName 封裝不存在專案中，它會安裝。</span><span class="sxs-lookup"><span data-stu-id="46d6f-119">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span>

>[!NOTE]
><span data-ttu-id="46d6f-120">在加法 toohello 強式名稱 StackExchange.Redis.StrongName 封裝，還有 hello StackExchange.Redis 非強式命名版本。</span><span class="sxs-lookup"><span data-stu-id="46d6f-120">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="46d6f-121">如果您的專案使用 hello 非強式命名 StackExchange.Redis 版本必須先解除安裝，否則您發生命名衝突專案中。</span><span class="sxs-lookup"><span data-stu-id="46d6f-121">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="46d6f-122">如需這些封裝的相關詳細資訊，請參閱 [設定 .NET 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-122">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="46d6f-123">hello NuGet 封裝下載並新增 hello 需要組件參考，並新增下列區段到您的 web.config 檔案的 hello。</span><span class="sxs-lookup"><span data-stu-id="46d6f-123">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="46d6f-124">本節包含您 ASP.NET 應用程式 toouse hello Redis 的快取工作階段狀態提供者的 hello 必要的設定。</span><span class="sxs-lookup"><span data-stu-id="46d6f-124">This section contains hello required configuration for your ASP.NET application toouse hello Redis Cache Session State Provider.</span></span>

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

<span data-ttu-id="46d6f-125">hello 標記為註解 > 一節提供 hello 屬性和每個屬性的範例設定的範例。</span><span class="sxs-lookup"><span data-stu-id="46d6f-125">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="46d6f-126">設定您在 hello Microsoft Azure 入口網站的快取刀鋒伺服器中的 hello 值 hello 屬性並設定 hello 所需的其他值。</span><span class="sxs-lookup"><span data-stu-id="46d6f-126">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="46d6f-127">如需存取快取屬性的指示，請參閱 [設定 Redis 快取設定](cache-configure.md#configure-redis-cache-settings)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-127">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="46d6f-128">**主機** – 指定您的快取端點。</span><span class="sxs-lookup"><span data-stu-id="46d6f-128">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="46d6f-129">**連接埠**– 使用非 SSL 連接埠或您的 SSL 連接埠，取決於 hello ssl 設定。</span><span class="sxs-lookup"><span data-stu-id="46d6f-129">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="46d6f-130">**accessKey** – 用於您的快取中的任一 hello 主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="46d6f-130">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="46d6f-131">**ssl** – 如果您想要以 ssl toosecure 快取/用戶端通訊，則為 true，否則為 false。</span><span class="sxs-lookup"><span data-stu-id="46d6f-131">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="46d6f-132">為確定 toospecify hello 正確的連接埠。</span><span class="sxs-lookup"><span data-stu-id="46d6f-132">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="46d6f-133">新的快取預設為停用 hello 非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="46d6f-133">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="46d6f-134">指定 true，此設定 toouse hello SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="46d6f-134">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="46d6f-135">如需有關如何啟用 hello 非 SSL 連接埠的詳細資訊，請參閱 hello[存取連接埠](cache-configure.md#access-ports)> 一節中 hello[設定快取](cache-configure.md)主題。</span><span class="sxs-lookup"><span data-stu-id="46d6f-135">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="46d6f-136">**throwOnError** – 如果您想是否有失敗或 false 如果您要以無訊息模式的 hello 作業 toofail 擲回例外狀況 toobe 則為 true。</span><span class="sxs-lookup"><span data-stu-id="46d6f-136">**throwOnError** – true if you want an exception toobe thrown if there is a failure, or false if you want hello operation toofail silently.</span></span> <span data-ttu-id="46d6f-137">您可以藉由檢查靜態 Microsoft.Web.Redis.RedisSessionStateProvider.LastException 屬性 hello 檢查失敗。</span><span class="sxs-lookup"><span data-stu-id="46d6f-137">You can check for a failure by checking hello static Microsoft.Web.Redis.RedisSessionStateProvider.LastException property.</span></span> <span data-ttu-id="46d6f-138">hello 預設值為 true。</span><span class="sxs-lookup"><span data-stu-id="46d6f-138">hello default is true.</span></span>
* <span data-ttu-id="46d6f-139">**retryTimeoutInMilliseconds** – 會在此間隔期間 (以毫秒指定) 重試失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="46d6f-139">**retryTimeoutInMilliseconds** – Operations that fail are retried during this interval, specified in milliseconds.</span></span> <span data-ttu-id="46d6f-140">hello 第一個重試發生之後 20 毫秒，並產生 hello retryTimeoutInMilliseconds 間隔到期之前的每秒然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="46d6f-140">hello first retry occurs after 20 milliseconds, and then retries occur every second until hello retryTimeoutInMilliseconds interval expires.</span></span> <span data-ttu-id="46d6f-141">緊接著此間隔，hello 作業會重試最後一個的一次。</span><span class="sxs-lookup"><span data-stu-id="46d6f-141">Immediately after this interval, hello operation is retried one final time.</span></span> <span data-ttu-id="46d6f-142">如果 hello 作業仍失敗，hello 例外狀況擲回 toohello 呼叫者，根據 hello throwOnError 設定。</span><span class="sxs-lookup"><span data-stu-id="46d6f-142">If hello operation still fails, hello exception is thrown back toohello caller, depending on hello throwOnError setting.</span></span> <span data-ttu-id="46d6f-143">hello 預設值為 0，表示無重試。</span><span class="sxs-lookup"><span data-stu-id="46d6f-143">hello default value is 0, which means no retries.</span></span>
* <span data-ttu-id="46d6f-144">**databaseId** – 指定快取哪些資料庫 toouse 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="46d6f-144">**databaseId** – Specifies which database toouse for cache output data.</span></span> <span data-ttu-id="46d6f-145">如果未指定，會使用 hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="46d6f-145">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="46d6f-146">**applicationName** – 金鑰在 redis 中會儲存為 `{<Application Name>_<Session ID>}_Data`。</span><span class="sxs-lookup"><span data-stu-id="46d6f-146">**applicationName** – Keys are stored in redis as `{<Application Name>_<Session ID>}_Data`.</span></span> <span data-ttu-id="46d6f-147">這個命名配置可讓多個應用程式 tooshare hello 相同的 Redis 執行個體。</span><span class="sxs-lookup"><span data-stu-id="46d6f-147">This naming scheme enables multiple applications tooshare hello same Redis instance.</span></span> <span data-ttu-id="46d6f-148">此參數是選擇性的，如果您未提供，將會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="46d6f-148">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="46d6f-149">**connectionTimeoutInMilliseconds** – 此設定可讓您 toooverride hello connectTimeout hello StackExchange.Redis 用戶端中設定。</span><span class="sxs-lookup"><span data-stu-id="46d6f-149">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="46d6f-150">如果未指定，會使用 hello 預設 connectTimeout 值為 5000。</span><span class="sxs-lookup"><span data-stu-id="46d6f-150">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="46d6f-151">如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-151">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="46d6f-152">**operationTimeoutInMilliseconds** – 此設定可讓您 toooverride hello syncTimeout hello StackExchange.Redis 用戶端中設定。</span><span class="sxs-lookup"><span data-stu-id="46d6f-152">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="46d6f-153">如果未指定，會使用 hello syncTimeout 預設為 1000年。</span><span class="sxs-lookup"><span data-stu-id="46d6f-153">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="46d6f-154">如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-154">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="46d6f-155">如需有關這些屬性的詳細資訊，請參閱 hello 原始部落格文章公告在[宣佈適用於 ASP.NET 工作階段狀態提供者 Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-155">For more information about these properties, see hello original blog post announcement at [Announcing ASP.NET Session State Provider for Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).</span></span>

<span data-ttu-id="46d6f-156">別忘了 toocomment 出 hello 標準 InProc 工作階段狀態提供者區段在 web.config 中。</span><span class="sxs-lookup"><span data-stu-id="46d6f-156">Don’t forget toocomment out hello standard InProc session state provider section in your web.config.</span></span>

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

<span data-ttu-id="46d6f-157">一旦執行了這些步驟，您的應用程式是設定的 toouse hello Redis 的快取工作階段狀態提供者。</span><span class="sxs-lookup"><span data-stu-id="46d6f-157">Once these steps are performed, your application is configured toouse hello Redis Cache Session State Provider.</span></span> <span data-ttu-id="46d6f-158">當您在應用程式中使用工作階段狀態時，會儲存在 Azure Redis 快取執行個體中。</span><span class="sxs-lookup"><span data-stu-id="46d6f-158">When you use session state in your application, it is stored in an Azure Redis Cache instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46d6f-159">Hello 快取中儲存的資料必須是可序列化的與 hello 資料可以儲存在 hello 不同預設記憶體中 ASP.NET 工作階段狀態提供者。</span><span class="sxs-lookup"><span data-stu-id="46d6f-159">Data stored in hello cache must be serializable, unlike hello data that can be stored in hello default in-memory ASP.NET Session State Provider.</span></span> <span data-ttu-id="46d6f-160">使用 hello Redis 工作階段狀態提供者時，請務必儲存工作階段狀態中的 hello 資料型別都是可序列化。</span><span class="sxs-lookup"><span data-stu-id="46d6f-160">When hello Session State Provider for Redis is used, be sure that hello data types that are being stored in session state are serializable.</span></span>
> 
> 

## <a name="aspnet-session-state-options"></a><span data-ttu-id="46d6f-161">ASP.NET 工作階段狀態選項</span><span class="sxs-lookup"><span data-stu-id="46d6f-161">ASP.NET Session State options</span></span>
* <span data-ttu-id="46d6f-162">在記憶體的工作階段狀態提供者-此提供者會儲存在記憶體中的 hello 工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="46d6f-162">In Memory Session State Provider - This provider stores hello Session State in memory.</span></span> <span data-ttu-id="46d6f-163">使用此提供者的 hello 優點是它既簡單又快速。</span><span class="sxs-lookup"><span data-stu-id="46d6f-163">hello benefit of using this provider is it is simple and fast.</span></span> <span data-ttu-id="46d6f-164">不過，您在使用記憶體中提供者時將無法調整 Web Apps，因為它不是分散式的。</span><span class="sxs-lookup"><span data-stu-id="46d6f-164">However you cannot scale your Web Apps if you are using in memory provider since it is not distributed.</span></span>
* <span data-ttu-id="46d6f-165">Sql Server 工作階段狀態提供者-此提供者會將 hello 工作階段狀態儲存在 Sql Server。</span><span class="sxs-lookup"><span data-stu-id="46d6f-165">Sql Server Session State Provider - This provider stores hello Session State in Sql Server.</span></span> <span data-ttu-id="46d6f-166">如果您想 toostore hello 工作階段狀態持續性儲存體中，請使用此提供者。</span><span class="sxs-lookup"><span data-stu-id="46d6f-166">Use this provider if you want toostore hello Session state in persistent storage.</span></span> <span data-ttu-id="46d6f-167">您可以調整您的 Web 應用程式，但將 SQL Server 用於工作階段，會對 Web 應用程式的效能造成影響。</span><span class="sxs-lookup"><span data-stu-id="46d6f-167">You can scale your Web App but using Sql Server for Session has a performance impact on your Web App.</span></span>
* <span data-ttu-id="46d6f-168">分散式中記憶體的工作階段狀態提供者例如 Redis 快取工作階段狀態提供者-這個 hello 兩者之優點的提供者提供。</span><span class="sxs-lookup"><span data-stu-id="46d6f-168">Distributed In Memory Session State Provider such as Redis Cache Session State Provider - This provider gives you hello best of both worlds.</span></span> <span data-ttu-id="46d6f-169">您的 Web 應用程式可擁有簡單、快速而可調整的工作階段狀態供應器。</span><span class="sxs-lookup"><span data-stu-id="46d6f-169">Your Web App can have a simple, fast, and scalable Session State Provider.</span></span> <span data-ttu-id="46d6f-170">因為此工作階段狀態快取中，您的應用程式的提供者存放區 hello tootake 考量所有 hello 與對話 tooa 分散式記憶體內部快取，例如暫時性網路失敗時，相關聯的特性。</span><span class="sxs-lookup"><span data-stu-id="46d6f-170">Because this provider stores hello Session state in a Cache, your app has tootake in consideration all hello characteristics associated when talking tooa Distributed In Memory Cache, such as transient network failures.</span></span> <span data-ttu-id="46d6f-171">如需使用快取的最佳作法，請參閱 Microsoft 模式和作法 [Azure 雲端應用程式設計和實作指引](https://github.com/mspnp/azure-guidance)中的[快取指引](../best-practices-caching.md)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-171">For best practices on using Cache, see [Caching guidance](../best-practices-caching.md) from Microsoft Patterns & Practices [Azure Cloud Application Design and Implementation Guidance](https://github.com/mspnp/azure-guidance).</span></span>

<span data-ttu-id="46d6f-172">如需工作階段狀態和其他最佳作法的相關詳細資訊，請參閱 [Web 開發最佳作法 (使用 Azure 建置實際的雲端應用程式)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices)(英文)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-172">For more information about session state and other best practices, see [Web Development Best Practices (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46d6f-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46d6f-173">Next steps</span></span>
<span data-ttu-id="46d6f-174">簽出 hello [Azure Redis 快取的 ASP.NET 輸出快取提供者](cache-aspnet-output-cache-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="46d6f-174">Check out hello [ASP.NET Output Cache Provider for Azure Redis Cache](cache-aspnet-output-cache-provider.md).</span></span>

