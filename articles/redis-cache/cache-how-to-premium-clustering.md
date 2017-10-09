---
title: "aaaHow tooconfigure Redis Premium Azure Redis 快取叢集 |Microsoft 文件"
description: "深入了解如何 toocreate 和管理 Redis 叢集高檔的 Azure Redis 快取執行個體"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Tooconfigure Redis Premium Azure Redis 快取叢集
Azure Redis 快取都有不同的快取提供項目，提供有彈性地 hello 選擇的快取大小和功能，包括 Premium 層功能，例如叢集、 持續性和虛擬網路支援。 本文說明如何 tooconfigure 叢集的高階 Azure Redis 快取執行個體。

如需其他進階快取功能的資訊，請參閱[簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)。

## <a name="what-is-redis-cluster"></a>Redis 叢集是什麼？
Azure Redis 快取提供 Redis 叢集的方式，就像 [實作於 Redis](http://redis.io/topics/cluster-tutorial)一樣。 Redis 叢集後，您會收到 hello 下列優點： 

* hello 能力 tooautomatically 分割您在多個節點之間的資料集。 
* hello 能力 toocontinue 作業時子集的 hello 節點發生失敗或無法 toocommunicate 與 hello hello 叢集其餘部分。 
* 增加輸送量： 輸送量增加以線性方式隨著您增加 hello 分區的數目。 
* 更多的記憶體大小： 以線性方式隨著您增加 hello 分區的數目。  

如需進階快取的大小、輸送量和頻寬的詳細資訊，請參閱[應該使用哪個 Redis 快取供應項目和大小？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

在 Azure 中，Redis 叢集被提供做為主要/複本模型，其中每個分區都有複寫的主要/複本組 hello 複寫受 Azure Redis 快取服務的位置。 

## <a name="clustering"></a>叢集
叢集上 hello 啟用**新增 Redis 快取**快取建立期間的刀鋒視窗。 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

叢集上 hello 設定**Redis 叢集**刀鋒視窗。

![叢集][redis-cache-clustering]

您可以向上 too10 分區 hello 叢集中。 按一下**啟用**和滑桿 hello 或輸入介於 1 到 10 之間的數字**分區計數**按一下**確定**。

每個分區都是一個主要/複本快取配對受 Azure，而 hello hello 快取的大小總計的計算方式是 hello 分區數目乘以 hello 定價層中選取的 hello 快取大小。 

![叢集][redis-cache-clustering-selected]

一旦建立 hello 快取連接 tooit 和使用，只要有非叢集的快取，並 Redis 散發整個 hello 快取分區的 hello 資料。 如果是診斷[啟用](cache-how-to-monitor.md#enable-cache-diagnostics)，度量資訊會為每個分區分別擷取，而且可以是[檢視](cache-how-to-monitor.md)hello Redis 快取刀鋒視窗中。 

> [!NOTE]
> 
> 在設定叢集時，用戶端應用程式中的必要設定有些微差異。 如需詳細資訊，請參閱[需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse 嗎？](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

如需使用的群集與 hello StackExchange.Redis 用戶端的範例程式碼，請參閱 hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs)部分 hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld)範例。

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>變更 hello 叢集大小上執行的進階版快取
toochange hello 叢集大小上執行的高階快取叢集的已啟用，按一下**Redis 叢集大小**從 hello**資源功能表**。

> [!NOTE]
> 雖然 hello Azure Redis 快取進階層已被釋放 tooGeneral 可用性，hello Redis 叢集大小功能目前為預覽狀態。
> 
> 

![Redis 叢集大小][redis-cache-redis-cluster-size]

toochange hello 叢集大小，使用 hello 滑桿，或輸入介於 1 到 10 之間的數字 hello**分區計數**文字方塊中，然後按一下**確定**toosave。

> [!NOTE]
> 調整叢集中執行 hello[移轉](https://redis.io/commands/migrate)命令，它是高度耗費資源的命令，因此影響降到最低，請考慮執行這項作業在非尖峰時間。 在 hello 移轉過程中，您會看到伺服器負載中的突然增加。 調整叢集長時間執行程序，並且 hello 所需的時間取決於 hello 索引鍵的數目和大小 hello 這些索引鍵相關聯的值。
> 
> 

## <a name="clustering-faq"></a>叢集常見問題集
hello 下列清單包含 Azure Redis 快取叢集的相關常見問題的解答 toocommonly。

* [我需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse？](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [如何在叢集中散發索引鍵？](#how-are-keys-distributed-in-a-cluster)
* [Hello 我可以建立最大快取大小為何？](#what-is-the-largest-cache-size-i-can-create)
* [所有 Redis 用戶端都支援叢集嗎？](#do-all-redis-clients-support-clustering)
* [當叢集已啟用時如何連接 toomy 快取？](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [我可以直接連接 我的快取 toohello 個別的分區嗎？](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [我可以為先前建立的快取設定叢集嗎？](#can-i-configure-clustering-for-a-previously-created-cache)
* [我可以設定基本或標準快取的叢集嗎？](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [我可以使用群集與 hello Redis 的 ASP.NET 工作階段狀態和輸出快取提供者嗎？](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [當我使用 StackExchange.Redis 和叢集時收到 MOVE 例外狀況，該怎麼辦？](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>我需要 toomake 叢集任何變更 toomy 用戶端應用程式 toouse？
* 啟用叢集時，只可以使用資料庫 0。 如果用戶端應用程式會使用多個資料庫，而且它會嘗試 tooread 或寫入 tooa 資料庫不是 0，hello 下列擲回例外狀況。 `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  如需詳細資訊，請參閱 [Redis 叢集規格 - 實作的子集](http://redis.io/topics/cluster-spec#implemented-subset)。
* 如果您使用 [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/)，則必須使用 1.0.481 或更新版本。 連接 toohello 快取使用 hello 相同[端點、 連接埠和索引鍵](cache-configure.md#properties)連接 tooa 快取，但是沒有啟用叢集時，所使用。 hello 唯一的差異在於，所有讀取和寫入必須都以 toodatabase 0。
  
  * 其他用戶端可能有不同的需求。 請參閱 [所有 Redis 用戶端都支援叢集嗎？](#do-all-redis-clients-support-clustering)
* 如果您的應用程式使用多個索引鍵作業批次處理到單一命令，必須位於所有索引鍵中 hello 相同分區。 toolocate 金鑰在 hello 相同分區，請參閱[金鑰散發在叢集中的方式？](#how-are-keys-distributed-in-a-cluster)
* 如果您使用 Redis ASP.NET 工作階段狀態提供者，則必須使用 2.0.1 或更高版本。 請參閱[使用群集與 hello Redis 的 ASP.NET 工作階段狀態和輸出快取提供者嗎？](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>如何在叢集中散發索引鍵？
每個 hello Redis[金鑰散發模型](http://redis.io/topics/cluster-spec#keys-distribution-model)文件： hello 金鑰空間分割成 16384 的位置。 每個索引鍵是雜湊，並指派 tooone 的這些介面槽分散於 hello hello 叢集節點。 您可以設定 hello 索引鍵的一部分是位於多個索引鍵的雜湊的 tooensure hello 相同分區使用雜湊標記。

* 索引鍵，並雜湊標記-如果 hello 索引鍵的任何一部分住`{`和`}`，只有該 hello 索引鍵的一部分會基於 hello 判斷 hello 雜湊位置索引鍵的雜湊。 例如，下列 3 個索引鍵的 hello 可能位在 hello 相同分區： `{key}1`， `{key}2`，和`{key}3`自只 hello `key` hello 名稱的一部分進行雜湊處理。 如需索引鍵主題標籤規格的完整清單，請參閱[索引鍵主題標籤](http://redis.io/topics/cluster-spec#keys-hash-tags)。
* 沒有雜湊標記-hello 整個索引鍵名稱的索引鍵使用雜湊。 這會導致統計上平均分佈在 hello 分區 hello 快取。

為了最佳效能和輸送量，建議您平均散發 hello 索引鍵。 如果您正在使用的雜湊標記中的索引鍵是平均分佈 hello 應用程式的責任 tooensure hello 索引鍵。

如需詳細資訊，請參閱[金鑰散發模型](http://redis.io/topics/cluster-spec#keys-distribution-model)、[Redis 叢集資料分區化](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding)和[金鑰主題標籤](http://redis.io/topics/cluster-spec#keys-hash-tags)。

使用叢集和在 hello 中尋找機碼的範例程式碼相同的分區，與 hello StackExchange.Redis 用戶端，請參閱 hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs)部分 hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld)範例。

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>Hello 我可以建立最大快取大小為何？
hello 最大 premium 快取大小為 53 GB。 您可以建立註冊 too10 分區，提供 530 GB 的最大大小。 如果您需要較大的大小，可以 [要求更多](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase)。 如需詳細資訊，請參閱 [Azure Redis 快取價格](https://azure.microsoft.com/pricing/details/cache/)。

### <a name="do-all-redis-clients-support-clustering"></a>所有 Redis 用戶端都支援叢集嗎？ 
在 hello 目前時間並非所有支援的用戶端都 Redis 叢集。 StackExchange.Redis 就是不支援的其中一例。 如需其他用戶端的詳細資訊，請參閱 hello[播放與 hello 叢集](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster)區段 hello [Redis 叢集教學課程](http://redis.io/topics/cluster-tutorial)。

> [!NOTE]
> 如果您使用 StackExchange.Redis 作為您的用戶端，請確定您使用 hello 最新版本的[StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 或更新版本的正確叢集 toowork。 如果您有任何關於 Move 例外狀況的問題，請參閱 [Move 例外狀況](#move-exceptions) ，以取得詳細資訊。
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>當叢集已啟用時如何連接 toomy 快取？
您可以連接 tooyour 快取使用 hello 相同[端點](cache-configure.md#properties)，[連接埠](cache-configure.md#properties)，和[金鑰](cache-configure.md#access-keys)連接 tooa 快取，但是沒有啟用叢集時，所使用。 Redis 管理叢集 hello 後端上，所以您不需 toomanage hello 從您的用戶端。

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>我可以直接連接 我的快取 toohello 個別的分區嗎？
目前官方尚未提供支援。 如前所述，每個分區都包含一個主要/複本快取組，統稱為快取執行個體。 您可以連接 toothese 快取執行個體使用 hello redis cli 公用程式在 hello[不穩定](http://redis.io/download)hello Redis GitHub 儲存機制分支。 這個版本會實作基本支援啟動與 hello`-c`切換。 如需詳細資訊，請參閱[播放與 hello 叢集](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster)上[http://redis.io](http://redis.io)在 hello [Redis 叢集教學課程](http://redis.io/topics/cluster-tutorial)。

非 ssl，使用下列命令的 hello。

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

如為 SSL，將 `1300N` 取代為 `1500N`。

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>我可以為先前建立的快取設定叢集嗎？
目前您只能在建立快取時啟用叢集。 之後，建立 hello 快取，但您無法加入叢集 tooa 進階版快取，或移除建立 hello 快取之後，從進階版快取叢集，您可以變更 hello 叢集大小。 進階版快取與啟用叢集只有一個分區是 hello 的不同的大小與任何叢集相同進階版快取。

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>我可以設定基本或標準快取的叢集嗎？
叢集僅適用於進階快取。

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>我可以使用群集與 hello Redis 的 ASP.NET 工作階段狀態和輸出快取提供者嗎？
* **Redis 輸出快取提供者** - 不需要變更。
* **Redis 工作階段狀態提供者**-toouse 叢集，您必須使用[RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 或更高版本，或例外狀況就會擲回。 這是一項重大變更。如需詳細資訊，請參閱 [v2.0.0 重大變更詳細資料](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details)。

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>當我使用 StackExchange.Redis 和叢集時收到 MOVE 例外狀況，該怎麼辦？
如果您正在使用 StackExchange.Redis，並且在使用叢集時收到 `MOVE` 例外狀況，請確定您使用的是 [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) 或更新版本。 如需設定您的.NET 應用程式 toouse StackExchange.Redis 指示，請參閱[設定 hello 快取用戶端](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients)。

## <a name="next-steps"></a>後續步驟
了解如何更進階的 toouse 快取功能。

* [簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







