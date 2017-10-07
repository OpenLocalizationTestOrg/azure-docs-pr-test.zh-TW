---
title: "受管理快取服務應用程式 tooRedis Azure aaaMigrate |Microsoft 文件"
description: "深入了解如何 toomigrate 受管理快取服務和角色中快取應用程式 tooAzure Redis 快取"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>從受管理快取服務 tooAzure Redis 快取移轉
使用 Azure 受管理快取服務 tooAzure Redis 快取的應用程式移轉就可完成幾乎不需要變更 tooyour 應用程式中，視應用程式快取所使用的 hello 受管理快取服務功能而定。 當 hello Api 並非完全 hello 相同它們很相似，和大部分使用受管理快取服務 tooaccess 快取的現有程式碼的可重複使用最少變更。 本主題顯示如何 toomake hello 必要的設定和應用程式變更 toomigrate 您受管理快取服務應用程式 toouse Azure Redis 快取，並顯示方式的一些 hello Azure Redis 快取功能可以是使用的 tooimplement hello 功能受管理快取服務快取。

>[!NOTE]
>受管理的快取服務及 In-Role Cache 已於 2016 年 11 月 30 日起[淘汰](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)。 如果您有任何您想 toomigrate tooAzure Redis 快取的角色中快取部署，您可以遵循本文章中的 hello 步驟。

## <a name="migration-steps"></a>移轉步驟
hello 步驟是必要的 toomigrate 受管理快取服務應用程式 toouse Azure Redis 快取。

* 將對應的受管理快取服務功能 tooAzure Redis 快取
* 選擇快取服務
* 建立快取
* 設定 hello 快取用戶端
  * 移除 hello 受管理快取服務組態
  * 設定快取用戶端，使用 StackExchange.Redis NuGet 封裝 hello
* 移轉受管理的快取服務程式碼
  * 連接 toohello 快取使用 hello ConnectionMultiplexer 類別
  * Hello 快取中存取基本資料型別
  * 使用 hello 快取中的.NET 物件
* 移轉 ASP.NET 工作階段狀態和輸出快取 tooAzure Redis 快取 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>將對應的受管理快取服務功能 tooAzure Redis 快取
Azure 受管理的快取服務與 Azure Redis 快取類似，但兩者在實作某些功能時會使用不同的方式。 本節描述一些 hello 差異，並提供有關實作 Azure Redis 快取中的受管理快取服務的 hello 功能的指引。

| 受管理的快取服務功能 | 受管理的快取服務支援 | Azure Redis 快取支援 |
| --- | --- | --- |
| 具名快取 |設定預設快取，而在 hello 標準和進階版快取提供項目，向上 toonine 其他具名快取可以設定視。 |Azure Redis 快取有可設定一些可以在使用的 tooimplement 類似的功能 toonamed 會快取的資料庫 （預設值為 16）。 如需詳細資訊，請參閱 [Redis 資料庫是什麼？](cache-faq.md#what-are-redis-databases)和[預設 Redis 伺服器組態](cache-configure.md#default-redis-server-configuration)。 |
| 高可用性 |Hello 標準和進階版快取提供項目中的 hello 快取中的項目提供高可用性。 如果項目遺失到期 tooa 失敗，備份副本 hello hello 快取中的項目都仍然可用。 寫入 toohello 次要快取會以同步方式進行。 |高可用性是 hello 標準和進階版快取提供項目中，其中具有兩個節點的主要/複本組態 （進階版快取中的每個分區有主要/複本組）。 寫入 toohello 複本會以非同步方式進行。 如需詳細資訊，請參閱 [Azure Redis 快取定價](https://azure.microsoft.com/pricing/details/cache/)。 |
| 通知 |可讓用戶端 tooreceive 非同步通知時各種快取作業發生在具名快取。 |用戶端應用程式可以使用 Redis pub/sub 或[Keyspace 通知](cache-configure.md#keyspace-notifications-advanced-settings)tooachieve 類似的功能 toonotifications。 |
| 本機快取 |Hello 用戶端，以加快存取速度上的本機存放快取物件的複本。 |用戶端應用程式需要 tooimplement 這項功能使用字典或類似的資料結構。 |
| 收回原則 |無或 LRU。 hello 預設原則為 LRU。 |Azure Redis 快取支援下列收回原則 hello: volatile lru、 allkeys lru、 volatile 隨機、 allkeys 隨機，volatile ttl、 noeviction。 hello 預設原則為 volatile-lru。 如需詳細資訊，請參閱 [預設 Redis 伺服器組態](cache-configure.md#default-redis-server-configuration)。 |
| 到期原則 |hello 預設到期原則為 Absolute 和 hello 預設的到期間隔是 10 分鐘。 另外也提供 [滑動] 和 [永不] 原則。 |依預設不會過期 hello 快取中的項目，但可以使用快取集多載的每秒寫入基礎上設定到期日。 如需詳細資訊，請參閱[新增和擷取物件從 hello 快取](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache)。 |
| 區域和標記 |區域是快取項目的子群組。 區域也支援稱為標籤的額外描述性字串 hello 註釋的快取項目。 區域支援在該區域中的 hello 能力 tooperform 搜尋作業上任何已加上標籤的項目。 區域內的所有項目位於 hello 快取叢集的單一節點內。 |Redis 快取所組成的單一節點 （除非已啟用 Redis 叢集） 讓 hello 概念的受管理快取服務區域不會套用。 擷取索引鍵，因此描述性標籤可以內嵌在 hello 索引鍵名稱，並稍後用 tooretrieve hello 項目時，redis 支援搜尋和萬用字元作業。 如需使用 Redis 實作標記解決方案的範例，請參閱 [使用 Redis 實作快取標記](http://stackify.com/implementing-cache-tagging-redis/)。 |
| 序列化 |受管理快取支援 NetDataContractSerializer、 BinaryFormatter，以及自訂序列化程式的 hello 使用。 hello 預設值為 NetDataContractSerializer。 |負責 hello hello 用戶端應用程式 tooserialize.NET 物件之前將它們放入 hello 的快取中，與 hello 選擇向上 toohello 用戶端應用程式開發人員的 hello 序列化程式。 如需詳細資訊和範例程式碼，請參閱[hello 快取中的.NET 物件處理](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)。 |
| 快取模擬器 |受管理的快取提供本機快取模擬器。 |Azure Redis 快取沒有模擬器，不過您也可以[在本機執行 redis server.exe hello MSOpenTech 組建](cache-faq.md#cache-emulator)tooprovide 模擬器體驗。 |

## <a name="choose-a-cache-offering"></a>選擇快取服務
Microsoft Azure Redis 快取位於下列層 hello:

* **基本** - 單一節點。 多個向上 too53 GB 的大小。
* **標準** – 兩個節點 (主要/從屬)。 多個向上 too53 GB 的大小。 99.9% SLA。
* **Premium** – 雙節點主要/複本向上 too10 分區。 多個大小為 6 GB too530 GB。 所有「標準」層級的功能以及更多功能，可支援 [Redis 叢集](cache-how-to-premium-clustering.md)、[Redis 持續性](cache-how-to-premium-persistence.md)和 [Azure 虛擬網路](cache-how-to-premium-vnet.md)。 99.9% SLA。

每一個階層都有不同的功能和價格。 hello 功能都會涵蓋在內稍後在本指南中，以及如需定價的詳細資訊，請參閱[快取定價詳細資料](https://azure.microsoft.com/pricing/details/cache/)。

移轉的起始點是 toopick hello 大小符合 hello 您先前受管理快取服務快取大小，並再相應增加或減少，視您的應用程式的 hello 需求而定。 如需詳細指引選擇 hello 右 Azure Redis 快取提供項目的的詳細資訊，請參閱[何種 Redis 快取提供項目和大小應該使用？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)。

## <a name="create-a-cache"></a>建立快取
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>設定 hello 快取用戶端
Hello 快取會建立並設定後，hello 下一個步驟是 tooremove hello 受管理快取服務的設定，並新增 hello 新增 hello Azure Redis 快取設定和參考，讓快取用戶端可以存取 hello 快取。

* 移除 hello 受管理快取服務組態
* 設定快取用戶端，使用 StackExchange.Redis NuGet 封裝 hello

### <a name="remove-hello-managed-cache-service-configuration"></a>移除 hello 受管理快取服務組態
Hello 前用戶端應用程式可以設定 Azure Redis 快取，hello 現有受管理快取服務的組態，您必須移除組件參考，解除安裝 hello 受管理快取服務 NuGet 封裝。

toouninstall hello 受管理快取服務 NuGet 封裝，以滑鼠右鍵按一下中的 hello 用戶端專案**方案總管 中**選擇**管理 NuGet 封裝**。 選取 hello**安裝封裝** 節點，然後輸入 W**indowsAzure.Caching** hello 到搜尋已安裝的封裝 方塊。 選取**Windows** **Azure 快取**(或**Windows** **Azure 快取**視 hello hello NuGet 封裝的版本而定)，按一下**解除安裝**，然後按一下**關閉**。

![解除安裝 Azure 受管理的快取服務 NuGet 套件](./media/cache-migrate-to-redis/IC757666.jpg)

解除安裝的 hello 受管理快取服務 NuGet 封裝會移除 hello app.config 或 web.config 的 hello 用戶端應用程式中的 hello 受管理快取服務組件和 hello 受管理快取服務項目。 因為解除安裝 hello NuGet 封裝時，可能不會移除部分自訂的設定，開啟 web.config 或 app.config，並確保系統會完全移除該 hello 下列項目。

請確定該 hello`dataCacheClients`項目已移除從 hello`configSections`項目。 請勿移除 hello 整個`configSections`項目，則只移除 hello`dataCacheClients`項目，如果有的話。

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

請確定該 hello`dataCacheClients`在移除區段。 hello `dataCacheClients` > 一節將會類似下列範例的 toohello。

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

一旦移除 hello 受管理快取服務組態時，您可以設定 hello 快取用戶端 hello 之後 > 一節中所述。

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>設定快取用戶端，使用 StackExchange.Redis NuGet 封裝 hello
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>移轉受管理的快取服務程式碼
hello StackExchange.Redis 快取用戶端的 hello API 是類似 toohello 受管理的快取服務。 本節中的 hello 差異的概觀。

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>連接 toohello 快取使用 hello ConnectionMultiplexer 類別
在受管理快取服務中，連接 toohello 快取已由 hello`DataCacheFactory`和`DataCache`類別。 Azure Redis 快取中，這些連線都受 hello`ConnectionMultiplexer`類別。

新增 hello 下列使用陳述式 toohello 頂端的任何您想要從中 tooaccess hello 快取的檔案。

```c#
using StackExchange.Redis
```

如果此命名空間未解析，請確定您加入 hello StackExchange.Redis NuGet 封裝中所述[設定 hello 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。

> [!NOTE]
> 請注意該 hello StackExchange.Redis 用戶端需要.NET Framework 4 或更新版本。
> 
> 

tooconnect tooan Azure Redis 快取執行個體，呼叫 hello 靜態`ConnectionMultiplexer.Connect`方法並傳入 hello 端點和金鑰。 其中一個方法 toosharing`ConnectionMultiplexer`應用程式中的執行個體是 toohave 傳回連接的執行個體，下列範例類似 toohello 的靜態屬性。 這會提供執行緒安全的方式 tooinitialize 僅連接單一`ConnectionMultiplexer`執行個體。 在此範例中`abortConnect`是集 toofalse，這表示將會成功 hello 呼叫，即使沒有建立連線 toohello 快取。 一項重要功能`ConnectionMultiplexer`是，它會自動還原連線 toohello 快取之後 hello 網路問題或其他原因，在解決。

```c#
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
```

hello 快取端點、 金鑰和連接埠可以取自 hello **Redis 快取**刀鋒視窗中的快取執行個體。 如需詳細資訊，請參閱 [Redis 快取屬性](cache-configure.md#properties)。

一旦建立 hello 連線之後，傳回參考 toohello Redis 快取資料庫呼叫 hello`ConnectionMultiplexer.GetDatabase`方法。 傳回的 hello hello 物件`GetDatabase`方法是輕量的傳遞物件，而且不需要 toobe 儲存。

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

hello StackExchange.Redis 用戶端會使用 hello`RedisKey`和`RedisValue`存取並儲存在 hello 快取中的項目類型。 這些型別會對應到最基本的語言型別 (包括字串)，但通常不會直接使用。 Redis 和字串 hello 最基本的 Redis 值，並且可以包含許多類型的資料，包括序列化的二進位資料流，而您不可以直接使用 hello 類型，您會使用包含的方法`String`hello 名稱中。 最基本的資料類型儲存和擷取項目從 hello 快取使用 hello`StringSet`和`StringGet`方法，除非您儲存了集合或其他 Redis 資料型別 hello 快取中。 

`StringSet`和`StringGet`是非常類似 toohello 受管理的快取服務`Put`和`Get`方法，其中包含一個主要差異在於您設定並取得 a.NET 物件至 hello 快取之前您必須先序列化。 

當呼叫`StringGet`、 如果 hello 物件存在，會將它傳回，而如果沒有，則傳回 null。 在此情況下，您可以從 hello 所需的資料來源擷取 hello 值，並將它儲存 hello 快取供後續使用。 這稱為 hello 另行快取模式。

hello 快取中，使用 hello 項目的 toospecify hello 到期`TimeSpan`參數`StringSet`。

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Azure Redis 快取可以使用 .NET 物件及基本資料型別，但必須先將 .NET 物件序列化，才能加以快取。 這是 hello 的 hello 應用程式開發人員的責任。 如此 hello 開發人員彈性 hello 選擇 hello 序列化程式。 如需詳細資訊和範例程式碼，請參閱[hello 快取中的.NET 物件處理](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)。

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>移轉 ASP.NET 工作階段狀態和輸出快取 tooAzure Redis 快取
Azure Redis 快取有適用於 ASP.NET 工作階段狀態和頁面輸出快取的提供者。 toomigrate 使用 hello 受管理快取服務版本的這些提供者，您的應用程式第一次移除 hello web.config 中，從現有的區段，然後設定 hello Azure Redis 快取版本 hello 提供者。 如需有關使用指示 hello Azure Redis 快取 ASP.NET 提供者，請參閱 < [Azure Redis 快取的 ASP.NET 工作階段狀態提供者](cache-aspnet-session-state-provider.md)和[Azure Redis 快取的 ASP.NET 輸出快取提供者](cache-aspnet-output-cache-provider.md)。

## <a name="next-steps"></a>後續步驟
瀏覽 hello [Azure Redis 快取文件](https://azure.microsoft.com/documentation/services/cache/)教學課程、 範例、 影片，等等。

