---
title: "aaaAzure Redis 快取範例 |Microsoft 文件"
description: "了解如何 toouse Azure Redis 快取"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Azure Redis 快取範例
本主題提供 Azure Redis 快取的範例，涵蓋的案例，例如連接 tooa 快取、 讀取和寫入資料 tooand 從快取，以及使用 hello ASP.NET Redis 快取提供者的清單。 某些 hello 範例可下載專案中，且部分提供的逐步指引，包括程式碼片段，但不是連結 tooa 可下載專案。

## <a name="hello-world-samples"></a>Hello World 範例
本節中的 hello 範例顯示 hello 的連接 tooan Azure Redis 快取執行個體和讀取及寫入資料 toohello 快取使用多種語言的基本概念和 Redis 用戶端。

hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld)範例將示範如何 tooperform 各種快取作業使用 hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET 用戶端。

此範例示範如何：

* 使用各種連線選項
* 從使用同步和非同步作業的 hello 快取的讀取和寫入物件 tooand
* 使用指定的索引鍵的 Redis MGET/MSET 命令 tooreturn 值
* 執行 Redis 交易作業
* 使用 Redis 清單和已排序的集合
* 使用 JsonConvert 序列化程式儲存 .NET 物件
* 使用 Redis 設定 tooimplement 標記
* 使用 Redis 叢集

如需詳細資訊，請參閱 hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis)文件 github，而且可用於多個使用案例，請參閱 「 hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests)單元測試。

[如何 toouse Azure Redis 快取使用 Python](cache-python-get-started.md)顯示 tooget 如何開始使用 Azure Redis 快取使用 Python 和 hello [redis py](https://github.com/andymccurdy/redis-py)用戶端。

[使用 hello 快取中的.NET 物件](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)顯示您的其中一種方式 tooserialize.NET 物件，您可以將它們寫入 tooand 讀取它們從 Azure Redis 快取執行個體。 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>使用 Redis 快取做為 ASP.NET SignalR 的向外延展後擋板
hello[使用 Redis 快取的範圍外後擋板適用於 ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane)範例會示範如何使用 Azure Redis 快取為 SignalR 後擋板。 如需後擋板的詳細資訊，請參閱 [使用 Redis 的 SignalR 向外延展](http://www.asp.net/signalr/overview/performance/scaleout-with-redis)。

## <a name="redis-cache-customer-query-sample"></a>Redis 快取客戶查詢範例
本範例示範如何比較從快取中存取資料與從持續性儲存體中存取資料之間的效能。 此範例有兩個專案。

* [示範 Redis 快取如何透過快取資料來改善效能](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [種子 hello 示範 hello 資料庫與快取](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>ASP.NET 工作階段狀態和輸出快取
hello[使用 Azure Redis 快取 toostore ASP.NET 工作階段狀態和 OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching)範例會示範如何在您 toouse Azure Redis 快取 toostore ASP.NET 工作階段和輸出快取使用 hello 的工作階段狀態和 OutputCache 提供者Redis。

## <a name="manage-azure-redis-cache-with-maml"></a>使用 MAML 管理 Azure Redis 快取
hello[管理 Azure Redis 快取使用 Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML)範例會示範如何使用 Azure Management Libraries toomanage-(建立 / 更新 / 刪除) 您的快取。 

## <a name="custom-monitoring-sample"></a>自訂監視範例
hello[存取 Redis 快取監視資料](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring)範例會示範如何存取監視資料，以及在 Azure Redis 快取之外 hello Azure 入口網站。

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>使用 PHP 和 Redis 撰寫的 Twitter 風格複製品
hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis)範例是 Redis Hello World hello。 它是最小的 Twitter 風格的社交網路複製使用 Redis 和使用 hello 的 PHP 撰寫[Predis](https://github.com/nrk/predis)用戶端。 hello 原始碼，是設計的 toobe 的非常簡單，並在 hello 相同時間 tooshow 不同 Redis 資料結構。

## <a name="bandwidth-monitor"></a>頻寬監視器
hello[頻寬監視器](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor)範例可讓您用戶端 hello toomonitor hello 頻寬。 toomeasure hello 頻寬、 hello 快取的用戶端電腦上執行 hello 範例，請呼叫 toohello 快取，和觀察 hello 頻寬監視器範例所報告的 hello 頻寬。

