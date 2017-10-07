---
title: "aaaHow tooUse Azure Redis 快取 |Microsoft 文件"
description: "了解如何 tooimprove hello Azure Redis 快取與 Azure 應用程式的效能"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a>如何 tooUse Azure Redis 快取
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

本指南也說明如何 tooget 啟動使用**Azure Redis 快取**。 Microsoft Azure Redis 快取根據 hello 熱門開放原始碼 Redis 快取。 它可讓您存取 tooa 安全且專用 Redis 快取中，由 Microsoft 管理。 使用 Azure Redis 快取建立的快取，可透過 Microsoft Azure 內的任何應用程式加以存取。

Microsoft Azure Redis 快取位於下列層 hello:

* **基本** - 單一節點。 多個向上 too53 GB 的大小。
* **標準** – 兩個節點 (主要/從屬)。 多個向上 too53 GB 的大小。 99.9% SLA。
* **Premium** – 雙節點主要/複本向上 too10 分區。 多個大小為 6 GB too530 GB。 所有「標準」層級的功能以及更多功能，可支援 [Redis 叢集](cache-how-to-premium-clustering.md)、[Redis 持續性](cache-how-to-premium-persistence.md)和 [Azure 虛擬網路](cache-how-to-premium-vnet.md)。 99.9% SLA。

每一個階層都有不同的功能和價格。 如需價格的相關資訊，請參閱 [快取價格詳細資料][Cache Pricing Details]。

本指南也說明如何 toouse hello [StackExchange.Redis] [ StackExchange.Redis]用戶端會使用 C\#程式碼。 hello 涵蓋案例包括**建立和設定快取**，**設定快取用戶端**，和**中新增和移除物件 hello 快取**。 如需使用 Azure Redis 快取的詳細資訊，請參閱 [後續步驟][Next Steps]。 建立 ASP.NET MVC web 應用程式使用 Redis 快取的逐步教學課程中，請參閱[如何 toocreate Web 應用程式使用 Redis 快取](cache-web-app-howto.md)。

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>開始使用 Azure Redis 快取
開始使用 Azure Redis 快取相當簡單。 tooget 啟動，您的佈建和設定快取。 接下來，讓他們可以存取 hello 快取設定 hello 快取用戶端。 一旦設定 hello 快取用戶端，您可以開始使用它們。

* [建立 hello 快取][Create hello cache]
* [設定 hello 快取用戶端][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>建立快取
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>您的快取之後，它會建立 tooaccess
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

如需有關設定快取的詳細資訊，請參閱[如何 tooconfigure Azure Redis 快取](cache-configure.md)。

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>設定 hello 快取用戶端
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

一旦用戶端專案設定為快取，您可以使用 hello 下列各節以使用您的快取中所述的 hello 技巧。

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>使用快取
本節中的 hello 步驟說明 tooperform 一般快取的工作。

* [連接 toohello 快取][Connect toohello cache]
* [新增和從 hello 快取擷取物件][Add and retrieve objects from hello cache]
* [使用 hello 快取中的.NET 物件](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>連接 toohello 快取
tooprogrammatically 工作與快取，您需要參考 toohello 快取。 新增 hello 遵循 toohello 前要 toouse hello StackExchange.Redis 用戶端 tooaccess Azure Redis 快取的任何檔案。

    using StackExchange.Redis;

> [!NOTE]
> hello StackExchange.Redis 用戶端需要.NET Framework 4 或更新版本。
> 
> 

hello Azure Redis 快取受 hello 連接 toohello`ConnectionMultiplexer`類別。 這個類別應該共用和在用戶端應用程式中重複使用，而且不需要 toobe 依作業基礎上建立。 

tooconnect tooan Azure Redis 快取，且已連接的執行個體傳回`ConnectionMultiplexer`，呼叫 hello 靜態`Connect`方法並傳入 hello 快取端點和金鑰。 使用 hello hello hello password 參數為 Azure 入口網站所產生的金鑰。

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> 警告：請勿將認證儲存在原始程式碼中。 tookeep 此範例簡單，我有顯示它們 hello 原始程式碼中。 請參閱[如何應用程式字串與連接字串工作][ How Application Strings and Connection Strings Work]如需詳細資訊 toostore 認證。
> 
> 

如果您不想 toouse SSL，請將`ssl=false`或省略 hello`ssl`參數。

> [!NOTE]
> 新的快取預設為停用 hello 非 SSL 連接埠。 如需啟用 hello 非 SSL 連接埠的指示，請參閱[存取連接埠](cache-configure.md#access-ports)。
> 
> 

其中一個方法 toosharing`ConnectionMultiplexer`應用程式中的執行個體是 toohave 傳回連接的執行個體，下列範例類似 toohello 的靜態屬性。 此方法提供的執行緒安全的方式 tooinitialize 僅連接單一`ConnectionMultiplexer`執行個體。 這些範例中`abortConnect`是集 toofalse，這表示即使不會建立連接 toohello Azure Redis 快取，hello 呼叫會成功。 一項重要功能`ConnectionMultiplexer`是它會自動還原連線 toohello 快取，一旦 hello 網路問題或其他原因，在解決。

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

如需進階連線組態選項的詳細資訊，請參閱 [StackExchange.Redis 組態模型][StackExchange.Redis configuration model]。

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

一旦建立 hello 連線之後，傳回參考 toohello redis 快取資料庫呼叫 hello`ConnectionMultiplexer.GetDatabase`方法。 傳回的 hello hello 物件`GetDatabase`方法是輕量的傳遞物件，而且不需要 toobe 儲存。

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

Azure Redis 快取有可以是使用的 toologically Redis 快取內的個別 hello 資料的資料庫 （預設值為 16） 可設定的數目。 如需詳細資訊，請參閱 [Redis 資料庫是什麼？](cache-faq.md#what-are-redis-databases)和[預設 Redis 伺服器組態](cache-configure.md#default-redis-server-configuration)。

您現在知道如何 tooconnect tooan Azure Redis 快取執行個體並傳回參考 toohello 快取資料庫，讓我們看看使用 hello 快取。

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>新增和從 hello 快取擷取物件
可以儲存在與使用 hello 從快取擷取項目`StringSet`和`StringGet`方法。

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

Redis 大部分的資料，做為 Redis 字串，但這些字串可以包含許多類型的資料，包括序列化的二進位資料，可用於儲存.NET 物件時 hello 快取存放區。

呼叫時`StringGet`，如果 hello 物件存在，則會傳回，而且如果沒有，`null`傳回。 如果`null`傳回時，您可以從 hello 所需的資料來源擷取 hello 值，並將它儲存在 hello 快取供後續使用。 此使用方式的模式稱為 hello 另行快取模式。

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

您也可以使用`RedisValue`hello 下列範例所示。 `RedisValue` 有隱含的運算子適用於整數資料類型，而如果 `null` 是預期的快取項目值則很實用。


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


hello 快取中，使用 hello 項目的 toospecify hello 到期`TimeSpan`參數`StringSet`。

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>使用 hello 快取中的.NET 物件
Azure Redis 快取可以快取 .NET 物件及基本資料類型，但必須先將 .NET 物件序列化，才能加以快取。 這個.NET 物件序列化 hello 責任 hello 應用程式開發人員，並且讓 hello 開發人員彈性 hello 選擇 hello 序列化程式。

一個簡單的方式 tooserialize 物件為 toouse hello`JsonConvert`中的序列化方法[Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1)和序列化 tooand 從 JSON。 hello 下列範例示範 get 和 set 使用`Employee`物件執行個體。

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a>後續步驟
既然您已經學會 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure Redis 快取。

* 簽出 hello Azure Redis 快取的 ASP.NET 提供者。
  * [Azure Redis 工作階段狀態提供者](cache-aspnet-session-state-provider.md)
  * [Azure Redis 快取 ASP.NET 輸出快取提供者](cache-aspnet-output-cache-provider.md)
* [啟用快取診斷](cache-how-to-monitor.md#enable-cache-diagnostics)這樣您就可以[監視器](cache-how-to-monitor.md)hello 快取的健全狀況。 您可以檢視度量 hello Azure 入口網站，而且也可以的 hello[下載並檢閱](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring)它們使用您選擇的 hello 工具。
* 簽出 hello [StackExchange.Redis 快取的用戶端文件][StackExchange.Redis cache client documentation]。
  * Azure Redis 快取可以透過許多 Redis 用戶端和開發語言進行存取。 如需詳細資訊，請參閱 [http://redis.io/clients][http://redis.io/clients]。
* Azure Redis 快取也可以與協力廠商服務和工具搭配使用 (例如 Redsmin 和 Redis Desktop Manager)。
  * 如需 Redsmin 的詳細資訊，請參閱[如何 tooretrieve Azure Redis 的連接字串，並使用它搭配 Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin]。
  * 使用 [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager)，透過 GUI 存取和檢查 Azure Redis 快取中的資料。
* 請參閱 hello [redis] [ redis]文件，並了解[redis 資料型別][ redis data types]和[十五分鐘簡介tooRedis 資料型別][a fifteen minute introduction tooRedis data types]。

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


