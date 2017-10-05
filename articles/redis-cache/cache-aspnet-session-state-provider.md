---
title: "快取 ASP.NET 工作階段狀態供應器 | Microsoft Docs"
description: "了解如何使用 Azure Redis 快取來儲存 ASP.NET 工作階段狀態"
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
ms.openlocfilehash: 0f3683939ac9646565a0669e19b4c82811d621fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a><span data-ttu-id="046e4-103">Azure Redis 快取的 ASP.NET 工作階段狀態提供者</span><span class="sxs-lookup"><span data-stu-id="046e4-103">ASP.NET Session State Provider for Azure Redis Cache</span></span>
<span data-ttu-id="046e4-104">Azure Redis 快取提供工作階段狀態提供者，可讓您用來將工作階段狀態儲存在快取中，而不是記憶體內或 SQL Server 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="046e4-104">Azure Redis Cache provides a session state provider that you can use to store your session state in a cache rather than in-memory or in a SQL Server database.</span></span> <span data-ttu-id="046e4-105">若要使用快取工作階段狀態提供者，請先設定快取，再使用「Redis 快取工作階段狀態 NuGet 套件」設定 ASP.NET 應用程式的快取。</span><span class="sxs-lookup"><span data-stu-id="046e4-105">To use the caching session state provider, first configure your cache, and then configure your ASP.NET application for cache using the Redis Cache Session State NuGet package.</span></span>

<span data-ttu-id="046e4-106">在實際的雲端應用程式中，避免儲存使用者工作階段某種形式的狀態通常並非理想做法，但某些方法會比其他方法更加影響效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="046e4-106">It's often not practical in a real-world cloud app to avoid storing some form of state for a user session, but some approaches impact performance and scalability more than others.</span></span> <span data-ttu-id="046e4-107">如果您需要儲存狀態，最好的方法是將狀態的數量控制得較低，並將其儲存在 Cookie 中。</span><span class="sxs-lookup"><span data-stu-id="046e4-107">If you have to store state, the best solution is to keep the amount of state small and store it in cookies.</span></span> <span data-ttu-id="046e4-108">如果此方法不可行，次佳的方法是使用 ASP.NET 工作階段狀態搭配提供者，進行分散式的記憶體中快取。</span><span class="sxs-lookup"><span data-stu-id="046e4-108">If that isn't feasible, the next best solution is to use ASP.NET session state with a provider for distributed, in-memory cache.</span></span> <span data-ttu-id="046e4-109">從效能和延展性的觀點來看，最差的解決方法是使用資料庫備份的工作階段狀態提供者。</span><span class="sxs-lookup"><span data-stu-id="046e4-109">The worst solution from a performance and scalability standpoint is to use a database backed session state provider.</span></span> <span data-ttu-id="046e4-110">本主題提供使用 Azure Redis 快取的 ASP.NET 工作階段狀態供應器的指引。</span><span class="sxs-lookup"><span data-stu-id="046e4-110">This topic provides guidance on using the ASP.NET Session State Provider for Azure Redis Cache.</span></span> <span data-ttu-id="046e4-111">如需其他工作階段狀態選項的相關資訊，請參閱 [ASP.NET 工作階段狀態選項](#aspnet-session-state-options)。</span><span class="sxs-lookup"><span data-stu-id="046e4-111">For information on other session state options, see [ASP.NET Session State options](#aspnet-session-state-options).</span></span>

## <a name="store-aspnet-session-state-in-the-cache"></a><span data-ttu-id="046e4-112">將 ASP.NET 工作階段狀態儲存在快取中</span><span class="sxs-lookup"><span data-stu-id="046e4-112">Store ASP.NET session state in the cache</span></span>
<span data-ttu-id="046e4-113">若要在 Visual Studio 中使用「Redis 快取工作階段狀態 NuGet 套件」來設定用戶端應用程式，請依序按一下 [工具] 功能表中的 [NuGet 套件管理員] 和 [套件管理器主控台]。</span><span class="sxs-lookup"><span data-stu-id="046e4-113">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="046e4-114">從 `Package Manager Console` 視窗執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="046e4-114">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> <span data-ttu-id="046e4-115">如果您使用進階層的叢集功能，則必須使用 [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 或更高版本，否則會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="046e4-115">If you are using the clustering feature from the premium tier, you must use [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 or higher or an exception is thrown.</span></span> <span data-ttu-id="046e4-116">移至 2.0.1 或更新版本是一項重大變更；如需詳細資訊，請參閱 [v2.0.0 重大變更詳細資料 (英文)](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)。</span><span class="sxs-lookup"><span data-stu-id="046e4-116">Moving to 2.0.1 or higher is a breaking change; for more information, see [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).</span></span> <span data-ttu-id="046e4-117">此文章更新時，此套件的最新版本是 2.2.3。</span><span class="sxs-lookup"><span data-stu-id="046e4-117">At the time of this article update, the current version of this package is 2.2.3.</span></span>
> 
> 

<span data-ttu-id="046e4-118">「Redis 工作階段狀態提供者 NuGet 封裝」對「StackExchange.Redis.StrongName 封裝」有相依性。</span><span class="sxs-lookup"><span data-stu-id="046e4-118">The Redis Session State Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="046e4-119">如果 StackExchange.Redis.StrongName 封裝不在專案中，代表已經安裝。</span><span class="sxs-lookup"><span data-stu-id="046e4-119">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span>

>[!NOTE]
><span data-ttu-id="046e4-120">除了強式名稱的 StackExchange.Redis.StrongName 封裝外，另外還有非強式名稱版本的 StackExchange.Redis。</span><span class="sxs-lookup"><span data-stu-id="046e4-120">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="046e4-121">如果您的專案使用非強式名稱的 StackExchange.Redis 版本，您必須將它解除安裝，否則專案中會發生命名衝突。</span><span class="sxs-lookup"><span data-stu-id="046e4-121">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="046e4-122">如需這些封裝的相關詳細資訊，請參閱 [設定 .NET 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。</span><span class="sxs-lookup"><span data-stu-id="046e4-122">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="046e4-123">NuGet 封裝會下載和加入必要的組件參考，並將下列區段加入您的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="046e4-123">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="046e4-124">此區段包含讓您的 ASP.NET 應用程式使用 Redis 快取工作階段狀態供應器所需的設定。</span><span class="sxs-lookup"><span data-stu-id="046e4-124">This section contains the required configuration for your ASP.NET application to use the Redis Cache Session State Provider.</span></span>

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

<span data-ttu-id="046e4-125">標示註解的區段可提供屬性的範例和每個屬性的範例設定。</span><span class="sxs-lookup"><span data-stu-id="046e4-125">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="046e4-126">以來自 Microsoft Azure 入口網站之快取刀鋒視窗的值來設定屬性，並視需要設定其他值。</span><span class="sxs-lookup"><span data-stu-id="046e4-126">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="046e4-127">如需存取快取屬性的指示，請參閱 [設定 Redis 快取設定](cache-configure.md#configure-redis-cache-settings)。</span><span class="sxs-lookup"><span data-stu-id="046e4-127">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="046e4-128">**主機** – 指定您的快取端點。</span><span class="sxs-lookup"><span data-stu-id="046e4-128">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="046e4-129">**連接埠** – 使用您的非 SSL 連接埠或 SSL 連接埠，依 ssl 設定而定。</span><span class="sxs-lookup"><span data-stu-id="046e4-129">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="046e4-130">**accessKey** – 用於快取的主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="046e4-130">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="046e4-131">**ssl** – 如果您想要使用 ssl 保護快取/用戶端通訊則為 true，否則為 false。</span><span class="sxs-lookup"><span data-stu-id="046e4-131">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="046e4-132">請務必指定正確的連接埠。</span><span class="sxs-lookup"><span data-stu-id="046e4-132">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="046e4-133">預設會為新快取停用非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="046e4-133">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="046e4-134">請於此設定指定為 true，使用 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="046e4-134">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="046e4-135">如需啟用非 SSL 連接埠的相關詳細資訊，請參閱[設定快取](cache-configure.md)主題中的[存取連接埠](cache-configure.md#access-ports)一節。</span><span class="sxs-lookup"><span data-stu-id="046e4-135">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="046e4-136">**throwOnError** – true (如果您想在發生失敗時擲出例外狀況) 或 false (如果您想在作業失敗時為無訊息模式)。</span><span class="sxs-lookup"><span data-stu-id="046e4-136">**throwOnError** – true if you want an exception to be thrown if there is a failure, or false if you want the operation to fail silently.</span></span> <span data-ttu-id="046e4-137">您可以核取靜態 Microsoft.Web.Redis.RedisSessionStateProvider.LastException 屬性以檢查失敗。</span><span class="sxs-lookup"><span data-stu-id="046e4-137">You can check for a failure by checking the static Microsoft.Web.Redis.RedisSessionStateProvider.LastException property.</span></span> <span data-ttu-id="046e4-138">預設值是 true。</span><span class="sxs-lookup"><span data-stu-id="046e4-138">The default is true.</span></span>
* <span data-ttu-id="046e4-139">**retryTimeoutInMilliseconds** – 會在此間隔期間 (以毫秒指定) 重試失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="046e4-139">**retryTimeoutInMilliseconds** – Operations that fail are retried during this interval, specified in milliseconds.</span></span> <span data-ttu-id="046e4-140">第一次重試會在 20 毫秒後發生，然後每秒進行重試，直到 retryTimeoutInMilliseconds 間隔到期為止。</span><span class="sxs-lookup"><span data-stu-id="046e4-140">The first retry occurs after 20 milliseconds, and then retries occur every second until the retryTimeoutInMilliseconds interval expires.</span></span> <span data-ttu-id="046e4-141">緊接著此間隔之後，作業會進行最後一次重試。</span><span class="sxs-lookup"><span data-stu-id="046e4-141">Immediately after this interval, the operation is retried one final time.</span></span> <span data-ttu-id="046e4-142">如果作業仍失敗，會視 throwOnError 設定將例外狀況擲回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="046e4-142">If the operation still fails, the exception is thrown back to the caller, depending on the throwOnError setting.</span></span> <span data-ttu-id="046e4-143">預設值為 0，表示不會重試。</span><span class="sxs-lookup"><span data-stu-id="046e4-143">The default value is 0, which means no retries.</span></span>
* <span data-ttu-id="046e4-144">**databaseId** – 指定快取輸出資料所使用的資料庫。</span><span class="sxs-lookup"><span data-stu-id="046e4-144">**databaseId** – Specifies which database to use for cache output data.</span></span> <span data-ttu-id="046e4-145">若未指定，就會使用預設值 0。</span><span class="sxs-lookup"><span data-stu-id="046e4-145">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="046e4-146">**applicationName** – 金鑰在 redis 中會儲存為 `{<Application Name>_<Session ID>}_Data`。</span><span class="sxs-lookup"><span data-stu-id="046e4-146">**applicationName** – Keys are stored in redis as `{<Application Name>_<Session ID>}_Data`.</span></span> <span data-ttu-id="046e4-147">這個命名配置可讓多個應用程式共用同一個 Redis 執行個體。</span><span class="sxs-lookup"><span data-stu-id="046e4-147">This naming scheme enables multiple applications to share the same Redis instance.</span></span> <span data-ttu-id="046e4-148">此參數是選擇性的，如果您未提供，將會使用預設值。</span><span class="sxs-lookup"><span data-stu-id="046e4-148">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="046e4-149">**connectionTimeoutInMilliseconds** – 此設定可讓您覆寫 StackExchange.Redis 用戶端中的 connectTimeout 設定。</span><span class="sxs-lookup"><span data-stu-id="046e4-149">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="046e4-150">若未指定，將會使用預設的 connectTimeout 設定為 5000。</span><span class="sxs-lookup"><span data-stu-id="046e4-150">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="046e4-151">如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。</span><span class="sxs-lookup"><span data-stu-id="046e4-151">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="046e4-152">**operationTimeoutInMilliseconds** – 此設定可讓您覆寫 StackExchange.Redis 用戶端中的 syncTimeout 設定。</span><span class="sxs-lookup"><span data-stu-id="046e4-152">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="046e4-153">若未指定，將會使用預設的 syncTimeout 設定為 1000。</span><span class="sxs-lookup"><span data-stu-id="046e4-153">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="046e4-154">如需詳細資訊，請參閱 [StackExchange.Redis 設定模型](http://go.microsoft.com/fwlink/?LinkId=398705)(英文)。</span><span class="sxs-lookup"><span data-stu-id="046e4-154">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="046e4-155">如需這些屬性的相關詳細資訊，請參閱 [發佈 Redis 的 ASP.NET 工作階段狀態提供者](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)(英文) 上的原始部落格文章公告。</span><span class="sxs-lookup"><span data-stu-id="046e4-155">For more information about these properties, see the original blog post announcement at [Announcing ASP.NET Session State Provider for Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).</span></span>

<span data-ttu-id="046e4-156">別忘記備註您 web.config 中的標準 InProc 工作階段狀態提供者區段。</span><span class="sxs-lookup"><span data-stu-id="046e4-156">Don’t forget to comment out the standard InProc session state provider section in your web.config.</span></span>

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

<span data-ttu-id="046e4-157">一旦執行了這些步驟，您的應用程式就會設定為使用 Redis 快取工作階段狀態提供者。</span><span class="sxs-lookup"><span data-stu-id="046e4-157">Once these steps are performed, your application is configured to use the Redis Cache Session State Provider.</span></span> <span data-ttu-id="046e4-158">當您在應用程式中使用工作階段狀態時，會儲存在 Azure Redis 快取執行個體中。</span><span class="sxs-lookup"><span data-stu-id="046e4-158">When you use session state in your application, it is stored in an Azure Redis Cache instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="046e4-159">儲存在快取中的資料必須可序列化，這一點與可以儲存在預設記憶體中 ASP.NET 工作階段狀態供應器的資料不同。</span><span class="sxs-lookup"><span data-stu-id="046e4-159">Data stored in the cache must be serializable, unlike the data that can be stored in the default in-memory ASP.NET Session State Provider.</span></span> <span data-ttu-id="046e4-160">使用 Redis 的工作階段狀態提供者時，請確定儲存在工作階段狀態中的資料類型為可序列化。</span><span class="sxs-lookup"><span data-stu-id="046e4-160">When the Session State Provider for Redis is used, be sure that the data types that are being stored in session state are serializable.</span></span>
> 
> 

## <a name="aspnet-session-state-options"></a><span data-ttu-id="046e4-161">ASP.NET 工作階段狀態選項</span><span class="sxs-lookup"><span data-stu-id="046e4-161">ASP.NET Session State options</span></span>
* <span data-ttu-id="046e4-162">記憶體中工作階段狀態提供者 – 此提供者會將工作階段狀態儲存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="046e4-162">In Memory Session State Provider - This provider stores the Session State in memory.</span></span> <span data-ttu-id="046e4-163">使用此提供者的好處是它既簡單又快速。</span><span class="sxs-lookup"><span data-stu-id="046e4-163">The benefit of using this provider is it is simple and fast.</span></span> <span data-ttu-id="046e4-164">不過，您在使用記憶體中提供者時將無法調整 Web Apps，因為它不是分散式的。</span><span class="sxs-lookup"><span data-stu-id="046e4-164">However you cannot scale your Web Apps if you are using in memory provider since it is not distributed.</span></span>
* <span data-ttu-id="046e4-165">SQL Server 工作階段狀態提供者 – 此提供者會將工作階段狀態儲存在 SQL Server 中。</span><span class="sxs-lookup"><span data-stu-id="046e4-165">Sql Server Session State Provider - This provider stores the Session State in Sql Server.</span></span> <span data-ttu-id="046e4-166">如果您想要在永續性儲存體中儲存工作階段狀態，請使用此供應器。</span><span class="sxs-lookup"><span data-stu-id="046e4-166">Use this provider if you want to store the Session state in persistent storage.</span></span> <span data-ttu-id="046e4-167">您可以調整您的 Web 應用程式，但將 SQL Server 用於工作階段，會對 Web 應用程式的效能造成影響。</span><span class="sxs-lookup"><span data-stu-id="046e4-167">You can scale your Web App but using Sql Server for Session has a performance impact on your Web App.</span></span>
* <span data-ttu-id="046e4-168">分散式記憶體中工作階段狀態提供者，例如 Redis 快取工作階段狀態提供者 – 此提供者可讓您同時兼顧兩方面。</span><span class="sxs-lookup"><span data-stu-id="046e4-168">Distributed In Memory Session State Provider such as Redis Cache Session State Provider - This provider gives you the best of both worlds.</span></span> <span data-ttu-id="046e4-169">您的 Web 應用程式可擁有簡單、快速而可調整的工作階段狀態供應器。</span><span class="sxs-lookup"><span data-stu-id="046e4-169">Your Web App can have a simple, fast, and scalable Session State Provider.</span></span> <span data-ttu-id="046e4-170">因為此供應器會將工作階段狀態儲存在快取中，您的應用程式必須考量與分散式記憶體中快取 (例如暫時性網路失敗) 通訊時的所有相關特性。</span><span class="sxs-lookup"><span data-stu-id="046e4-170">Because this provider stores the Session state in a Cache, your app has to take in consideration all the characteristics associated when talking to a Distributed In Memory Cache, such as transient network failures.</span></span> <span data-ttu-id="046e4-171">如需使用快取的最佳作法，請參閱 Microsoft 模式和作法 [Azure 雲端應用程式設計和實作指引](https://github.com/mspnp/azure-guidance)中的[快取指引](../best-practices-caching.md)。</span><span class="sxs-lookup"><span data-stu-id="046e4-171">For best practices on using Cache, see [Caching guidance](../best-practices-caching.md) from Microsoft Patterns & Practices [Azure Cloud Application Design and Implementation Guidance](https://github.com/mspnp/azure-guidance).</span></span>

<span data-ttu-id="046e4-172">如需工作階段狀態和其他最佳作法的相關詳細資訊，請參閱 [Web 開發最佳作法 (使用 Azure 建置實際的雲端應用程式)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices)(英文)。</span><span class="sxs-lookup"><span data-stu-id="046e4-172">For more information about session state and other best practices, see [Web Development Best Practices (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).</span></span>

## <a name="next-steps"></a><span data-ttu-id="046e4-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="046e4-173">Next steps</span></span>
<span data-ttu-id="046e4-174">查看 [Azure Redis 快取的 ASP.NET 輸出快取提供者](cache-aspnet-output-cache-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="046e4-174">Check out the [ASP.NET Output Cache Provider for Azure Redis Cache](cache-aspnet-output-cache-provider.md).</span></span>

