---
title: "aaaHow tootroubleshoot Azure Redis 快取 |Microsoft 文件"
description: "了解如何 tooresolve 常見問題與 Azure Redis 快取。"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>如何 tootroubleshoot Azure Redis 快取
本文章提供 hello 下列類別的 Azure Redis 快取問題的疑難排解指引。

* [用戶端端疑難排解](#client-side-troubleshooting)-此章節提供的指導方針識別並解決問題 hello 連接 tooAzure Redis 快取的應用程式所造成。
* [伺服器端疑難排解](#server-side-troubleshooting)-此章節提供的指導方針識別並解決問題造成 hello Azure Redis 快取伺服器端。
* [StackExchange.Redis 逾時例外狀況](#stackexchangeredis-timeout-exceptions)-此章節提供有關疑難排解時使用 hello StackExchange.Redis 用戶端的問題。

> [!NOTE]
> 疑難排解步驟，本指南中的 hello 的數個包含 toorun Redis 命令，並監視各種效能度量的指示。 如需詳細資訊和指示，請參閱 hello 文件以 hello[更多資訊](#additional-information)> 一節。
> 
> 

## <a name="client-side-troubleshooting"></a>用戶端疑難排解
本節討論因為 hello 用戶端應用程式上的條件而產生的疑難排解問題。

* [記憶體不足的壓力 hello 用戶端上](#memory-pressure-on-the-client)
* [流量暴增](#burst-of-traffic)
* [用戶端 CPU 使用量很高](#high-client-cpu-usage)
* [超過用戶端頻寬](#client-side-bandwidth-exceeded)
* [要求/回應大小很大](#large-requestresponse-size)
* [Redis 在何種情形的 toomy 資料？](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>記憶體不足的壓力 hello 用戶端上
#### <a name="problem"></a>問題
Hello 用戶端電腦上的記憶體壓力會導致 tooall 類效能問題可能會延遲處理已送出 hello Redis 執行個體沒有任何延遲的資料。 當叫用的記憶體不足的壓力時，hello 系統通常會有 toopage 資料從實體記憶體 toovirtual 記憶體，也就是在磁碟上。 這*頁面判定為失敗*原因 hello 系統 tooslow 向明顯。

#### <a name="measurement"></a>測量
1. 監視電腦 toomake 確定它不會超過可用的記憶體上的記憶體使用量。 
2. 監視 hello`Page Faults/Sec`效能計數器。 即使在正常作業期間，大部分的系統還是會有一些分頁錯誤，因此請留意這個與逾時對應的分頁錯誤效能計數器尖峰。

#### <a name="resolution"></a>解決方案
升級用戶端 tooa 較大用戶端更多記憶體的 VM 大小，或深入了解您的記憶體使用量模式 tooreduce 記憶體 consuption。

### <a name="burst-of-traffic"></a>流量暴增
#### <a name="problem"></a>問題
暴增的流量結合不良`ThreadPool`設定可能會導致延遲處理已由 hello Redis 伺服器傳送，但尚未使用 hello 用戶端上的資料。

#### <a name="measurement"></a>測量
使用[如這裡所提供的](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs)程式碼，監視 `ThreadPool` 統計資料如何隨著時間變更。 您也可以查看 hello `TimeoutException` StackExchange.Redis 中的訊息。 範例如下：

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

在上面訊息 hello，有幾個有趣的問題：

1. 請注意，在 hello`IOCP`區段和 hello `WORKER` > 一節，您有`Busy`值大於 hello`Min`值。 這表示 `ThreadPool` 設定需要調整。
2. 您也可以查看 `in: 64221`。 這表示已在 hello 核心通訊端層接收 64211 位元組，但您尚未尚未讀取 hello 應用程式 (例如 StackExchange.Redis)。 這通常表示，您的應用程式不從 hello 網路的速度一樣快 hello 伺服器傳送它 tooyou 讀取資料。

#### <a name="resolution"></a>解決方案
設定您[執行緒集區設定](https://gist.github.com/JonCole/e65411214030f0d823cb)toomake 確定您在執行緒集區將會快速地在向上發送案例。

### <a name="high-client-cpu-usage"></a>用戶端 CPU 使用量很高
#### <a name="problem"></a>問題
Hello 用戶端上的高 CPU 使用量是 hello 系統趕不上它已被要求 tooperform hello 工作指示。 這表示即使 Redis 非常快速地傳送 hello 回應 hello 用戶端可能會失敗 tooprocess Redis 能夠及時的回應。

#### <a name="measurement"></a>測量
監視 hello 透過 hello Azure 入口網站或透過 hello 系統寬 CPU 使用量相關效能計數器。 請小心不 toomonitor*程序*CPU 因為單一處理序可以有低 CPU 使用率在 hello 相同時間整體系統 CPU 可能會很高。 請監看與逾時對應的 CPU 使用量暴增。 由於高 CPU，您可能也會看到高`in: XXX`值`TimeoutException`hello 中所述的錯誤訊息[批突發之流量](#burst-of-traffic)> 一節。

> [!NOTE]
> StackExchange.Redis 1.1.603 和更新版本包含 hello`local-cpu`度量中`TimeoutException`錯誤訊息。 請確定您使用 hello 最新版 hello [StackExchange.Redis NuGet 封裝](https://www.nuget.org/packages/StackExchange.Redis/)。 錯誤經常被中修正 hello 程式碼 toomake 它更穩固 tootimeouts hello 最新版本相當重要，因此。
> 
> 

#### <a name="resolution"></a>解決方案
升級具有更多的 CPU 容量 tooa 較大 VM 大小，或調查導致 CPU 尖峰。 

### <a name="client-side-bandwidth-exceeded"></a>超過用戶端頻寬
#### <a name="problem"></a>問題
不同大小的用戶端電腦對於其可用的網路頻寬多寡會有限制。 如果超過 hello 用戶端 hello 可用頻寬，則資料將不會處理 hello 用戶端盡 hello 伺服器傳送它。 這可能會導致 tootimeouts。

#### <a name="measurement"></a>測量
使用 [如這裡所提供的](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs)程式碼，監視頻寬使用量如何隨著時間變更。 請注意，此程式碼可能無法在具有限制權限的某些環境 (例如 Azure 網站) 中順利執行。

#### <a name="resolution"></a>解決方案
增加用戶端 VM 大小或減少網路頻寬耗用。

### <a name="large-requestresponse-size"></a>要求/回應大小很大
#### <a name="problem"></a>問題
大型的要求/回應可能會導致逾時。 例如，假設您在用戶端上設定的逾時值為 1 秒。 應用程式同時 (使用相同的實體網路連線) 要求'A' 和 'B'） 在 hello 相同的時間 (使用 hello 相同的實體網路連線)。 大部分的用戶端支援 「 Pipelining"的要求，例如，'A' 和 'B' 這兩個要求傳送一個 hello 網路 toohello 伺服器上之後 hello 其他不需等到 hello 回應。 hello 伺服器會傳送 hello 回應 hello 中相同的順序。 如果回應 'A' 大夠它可以吃掉大部分的 hello 逾時的後續要求。 

hello 下列範例示範此案例。 在此案例中，'A' 和 'B' 傳送快速，hello 伺服器啟動快速，傳送回應，'A' 和 'B'，但是因為資料傳輸的時間，'B' 堵塞背後的要求 hello 其他要求，並發生逾時即使 hello 伺服器快速回應。

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>測量
這是很困難的一個 toomeasure。 您的用戶端程式碼 tootrack 大型要求和回應時，基本上有 tooinstrument。 

#### <a name="resolution"></a>解決方案
1. Redis 最適合大量的較小值，而不是少數幾個較大值。 hello 慣用的解決方案是 toobreak 註冊您的資料相關的較小值。 請參閱 hello [hello redis 的理想值大小範圍是什麼？100 KB 是否會太大？](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ)文章，以取得為何建議使用較小值的詳細資料。
2. Hello 大小增加您的 VM （適用於用戶端和 Redis 快取伺服器），tooget 高頻寬的功能，減少資料傳輸的較大的回應時間。 請注意，只需要 hello 伺服器上，取得更多的頻寬，或只在 hello 用戶端可能不夠。 測量您的頻寬使用量，並比較您目前擁有的 VM 大小與 hello toohello 功能。
3. Hello 數目增加`ConnectionMultiplexer`透過不同的連接使用和循環配置資源的要求物件。

### <a name="what-happened-toomy-data-in-redis"></a>Redis 在何種情形的 toomy 資料？
#### <a name="problem"></a>問題
我應該針對特定資料 toobe 我的 Azure Redis 快取執行個體中但似乎未那里的 toobe。

#### <a name="resolution"></a>解決方案
請參閱[Redis 在何種情形的 toomy 資料？](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)的可能原因和解決方式。

## <a name="server-side-troubleshooting"></a>伺服器端疑難排解
本節討論因為 hello 快取伺服器上的條件而產生的疑難排解問題。

* [記憶體不足的壓力 hello 伺服器上](#memory-pressure-on-the-server)
* [高 CPU 使用率/伺服器負載](#high-cpu-usage-server-load)
* [超過伺服器端頻寬](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>記憶體不足的壓力 hello 伺服器上
#### <a name="problem"></a>問題
Hello 伺服器端上的記憶體壓力會導致效能問題可能會延遲處理要求的 tooall 種類。 當叫用的記憶體不足的壓力時，hello 系統通常會有 toopage 資料從實體記憶體 toovirtual 記憶體，也就是在磁碟上。 這*頁面判定為失敗*原因 hello 系統 tooslow 向明顯。 此記憶體壓力有幾個可能的原因︰ 

1. 您已填入 hello 快取 toofull 容量資料。 
2. Redis 查看高記憶體分散-最常造成儲存大型物件 (Redis 最適合用於小型物件，請參閱 hello [hello redis 的理想值大小範圍是什麼？100 KB 是否會太大？](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ)文章)。 

#### <a name="measurement"></a>測量
Redis 會公開兩個可協助您識別此問題的度量。 第一個是 hello `used_memory` hello 其他且`used_memory_rss`。 [這些度量](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)可用在 hello Azure 入口網站或透過 hello [Redis 資訊](http://redis.io/commands/info)命令。

#### <a name="resolution"></a>解決方案
有數個可能發生的變更，您可以進行 toohelp 保留記憶體使用量狀況良好：

1. [設定記憶體原則](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) 並在金鑰上設定到期時間。 請注意，如果記憶體分散，這麼做可能還不夠。
2. [設定 maxmemory 保留值](cache-configure.md#maxmemory-policy-and-maxmemory-reserved)也就是夠大 toocompensate 的記憶體分散程度。
3. 將大型快取物件分割為較小的相關物件。
4. [標尺](cache-how-to-scale.md)tooa 較大的快取大小。
5. 如果您使用[進階版快取與啟用的 Redis 叢集](cache-how-to-premium-clustering.md)可以[hello 分區數目增加](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache)。

### <a name="high-cpu-usage--server-load"></a>高 CPU 使用率/伺服器負載
#### <a name="problem"></a>問題
高 CPU 使用率可能代表即使 Redis 非常快速地傳送 hello 回應 hello 用戶端可以失敗 tooprocess Redis 能夠及時的回應。

#### <a name="measurement"></a>測量
監視 hello 透過 hello Azure 入口網站或透過 hello 系統寬 CPU 使用量相關效能計數器。 請小心不 toomonitor*程序*CPU 因為單一處理序可以有低 CPU 使用率在 hello 相同時間整體系統 CPU 可能會很高。 請監看與逾時對應的 CPU 使用量暴增。

#### <a name="resolution"></a>解決方案
[標尺](cache-how-to-scale.md)tooa 大的快取層與更多的 CPU 容量，或調查導致 CPU 尖峰。 

### <a name="server-side-bandwidth-exceeded"></a>超過伺服器端頻寬
#### <a name="problem"></a>問題
不同大小的快取執行個體對於其可用的網路頻寬多寡會有限制。 如果伺服器 hello 超過 hello 可用頻寬，然後資料會傳送 toohello 用戶端快速。 這可能會導致 tootimeouts。

#### <a name="measurement"></a>測量
您可以監視 hello`Cache Read`度量 hello hello 指定報告的時間間隔期間，從以 mb 為單位每秒 (MB/s) 的 hello 快取讀取的資料量。 此值與這個快取所使用的 toohello 網路頻寬。 如果您想要的警示 tooset 伺服器端網路頻寬限制，您可以建立使用這個它們`Cache Read`計數器。 比較中的 hello 值與您讀數[本表](cache-faq.md#cache-performance)hello 觀察到的定價層和大小的各種快取的頻寬限制。

#### <a name="resolution"></a>解決方案
如果您持續觀察到的定價層和快取大小的最大頻寬的 hello 附近，請考慮[調整](cache-how-to-scale.md)tooa 定價層或有更大的網路頻寬的大小、 使用中的 hello 值[本表](cache-faq.md#cache-performance)作為指南。

## <a name="stackexchangeredis-timeout-exceptions"></a>StackExchange.Redis 逾時例外狀況
StackExchange.Redis 使用名為 `synctimeout` 的組態設定來進行預設值為 1000 毫秒的同步作業。 如果在未完成的同步呼叫 hello 約定 hello StackExchange.Redis 用戶端會擲回的時間，下列範例逾時的錯誤類似 toohello。

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


這則錯誤訊息包含可協助您點 toohello hello 問題的原因和可能的解析的度量。 hello 下表包含有關 hello 錯誤訊息計量的詳細資料。

| 錯誤訊息度量 | 詳細資料 |
| --- | --- |
| inst |在最後一個時間配量 hello: 0 命令已發行 |
| mgr |hello 通訊端管理員正在執行`socket.select`這表示它正在詢問 hello OS tooindicate 具有內容的通訊端 toodo; 基本上： hello 讀取器不是正在主動讀取從 hello 網路因為它不會認為有任何項目 toodo |
| 佇列 |總共有 73 個進行中的作業 |
| qu |6 hello 進行中作業的 hello 未傳送佇列中，尚未寫入 toohello 輸出網路 |
| qs |已傳送的他進行中作業的 67 toohello 伺服器，但回應尚無法使用。 可能是 hello 回應`Not yet sent by hello server`或`sent by hello server but not yet processed by hello client.` |
| qc |0 的 hello 進行中作業已經看過的回覆，但尚未尚未標示為完成，因為 toowaiting hello 完成迴圈上 |
| wr |沒有使用中的寫入器 （這表示 hello 6 未傳送的要求沒有被忽略） 位元組/activewriters |
| 了嗎 |有任何作用中的讀取裝置，而零個位元組可用 toobe hello NIC 位元組/activereaders 上讀取 |

### <a name="steps-tooinvestigate"></a>步驟 tooinvestigate
1. 最佳作法請確定您正在使用時使用 hello StackExchange.Redis 用戶端，下列模式 tooconnect hello。

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    如需詳細資訊，請參閱[連接 toohello 快取使用 StackExchange.Redis](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache)。

1. 請確定您的 Azure Redis 快取和 hello 用戶端應用程式中 hello Azure 中相同的區域。 例如，您可能會收到逾時後您的快取在美國東部但 hello 用戶端位於美國西部 hello 要求未完成內 hello`synctimeout`間隔，或您可能會發生逾時從本機開發電腦的偵錯時。 
   
    強烈建議您 toohave hello 快取並 hello 中的用戶端 hello 相同 Azure 區域。 如果您有包含跨區域呼叫的案例中，您應該設定 hello`synctimeout`間隔 tooa 值高於 hello 預設 1000 毫秒的間隔，藉以`synctimeout`hello 連接字串中的屬性。 hello 下列範例示範 StackExchange.Redis 快取的連接字串的程式碼片段`synctimeout`為 2000 毫秒。
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. 請確定您使用 hello 最新版 hello [StackExchange.Redis NuGet 封裝](https://www.nuget.org/packages/StackExchange.Redis/)。 錯誤經常被中修正 hello 程式碼 toomake 它更穩固 tootimeouts hello 最新版本相當重要，因此。
3. 如果沒有要求取得繫結的 hello 伺服器或用戶端上的頻寬限制，它會比較長，toocomplete 因而導致逾時。 toosee 如果您的逾時到期 toonetwork 頻寬 hello 在伺服器上，請參閱[超過伺服器端頻寬](#server-side-bandwidth-exceeded)。 toosee，如果您的逾時到期 tooclient 網路頻寬，請參閱[超過用戶端端頻寬](#client-side-bandwidth-exceeded)。
4. 您可以取得 CPU 繫結 hello 伺服器或 hello 用戶端上？
   
   * 如果您取得繫結 cpu 可能會導致 hello 要求 toonot 用戶端上的核取 hello 內處理`synctimeout`間隔，因此會造成逾時。 移動 tooa 大用戶端或 hello 負載可以幫助 toocontrol 這。 
   * 如果您要取得 CPU 的核取受限於 hello 伺服器上監視 hello `CPU` [快取效能計量](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)。 雖然 Redis 會受限於 CPU 可能會導致這些傳入要求要求 tootimeout。 您可以將發佈 hello 這橫跨多個分區進階版快取中載入或 tooa 較大的大小或定價層升級 tooaddress。 如需詳細資訊，請參閱 [超過伺服器端頻寬](#server-side-bandwidth-exceeded)。
5. 是否有花費很長的時間 tooprocess hello 伺服器上的命令？ 長時間執行的很長的時間 tooprocess hello redis 伺服器的命令可能會導致逾時。 長時間執行之命令的部分範例包括有大量金鑰的 `mget`、`keys *` 或編寫得不好的 lua 指令碼。 您可以使用 hello redis cli 用戶端 tooyour Azure Redis 快取執行個體連接，或使用 hello [Redis 主控台](cache-configure.md#redis-console)和執行的 hello [SlowLog](http://redis.io/commands/slowlog)命令 toosee 如果沒有要求花費時間超出預期。 Redis 伺服器和 StackExchange.Redis 最適合許多小型要求，而非少數幾個大型要求。 將資料分割成較小的區塊可以改善這些問題。 
   
    如需使用 redis cli 和 stunnel toohello Azure Redis 快取 SSL 端點連接資訊，請參閱 hello[宣佈適用於 ASP.NET 工作階段狀態提供者 Redis 預覽版本](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)部落格文章。 如需詳細資訊，請參閱 [SlowLog](http://redis.io/commands/slowlog)。
6. 高 Redis 伺服器負載可能會導致逾時。 您可以監視 hello 伺服器負載，藉由監視 hello `Redis Server Load` [快取效能計量](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)。 伺服器負載為 100 （最大值），表示該 hello redis 伺服器已經過忙碌中，沒有閒置的時間，處理要求。 toosee 如果特定要求會佔用所有 hello 伺服器功能，請在 hello 前段中所述執行 hello SlowLog 命令。 如需詳細資訊，請參閱 [高 CPU 使用率/伺服器負載](#high-cpu-usage-server-load)。
7. 可能是造成網路 blip 的 hello 用戶端上是否有任何其他事件？ 檢查 hello 用戶端 （web、 背景工作角色或 Iaas VM） 時發生的事件，例如向上或向下調整的用戶端執行個體的 hello 數目，或部署的 hello 用戶端新版本，或已啟用自動調整規模嗎？在我們的測試中我們發現自動調整或調整向上/向下可能會導致輸出的網路連線的幾秒鐘的時間可能會遺失的。 StackExchange.Redis 程式碼是有彈性的 toosuch 事件，並會重新連線。 在這段時間重新連線的 hello 佇列中的任何要求可以逾時。
8. 是否有大型的要求前幾個小型要求 toohello 已逾時的 Redis 快取？hello 參數`qs`hello 錯誤訊息會告知您 toohello hello 用戶端的伺服器，從所送出多少要求，但尚未處理回應。 這個值會不斷成長，因為 StackExchange.Redis 使用單一 TCP 連線，而且一次只能讀取一個回應。 即使 hello 第一項作業已逾時，不會停止從 hello 伺服器送出 hello 資料和其他要求會封鎖，直到完成這個作業時，造成逾時。 其中一種解決方案是確保您的快取已經很大，您的工作負載，並將較大的值分割成較小區塊 toominimize hello 可能發生逾時。 另一個可能的解決方案是 toouse 的集區`ConnectionMultiplexer`在您的用戶端物件，並選擇至少載入 hello`ConnectionMultiplexer`時，傳送新的要求。 這應該防止單一逾時引發的其他要求 tooalso 逾時。
9. 如果您使用`RedisSessionStateprovider`，請確定您已正確設定 hello 重試逾時。 `retrytimeoutInMilliseconds` 應高於 `operationTimeoutinMilliseonds`，否則不會發生任何重試。 在下列範例中的 hello `retrytimeoutInMilliseconds` too3000 設定。 如需詳細資訊，請參閱[Azure Redis 快取的 ASP.NET 工作階段狀態提供者](cache-aspnet-session-state-provider.md)和[toouse hello 工作階段狀態提供者和輸出快取提供者的組態參數的方式](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration)。

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. 請檢查 hello Azure Redis 快取伺服器上的記憶體使用量[監視](cache-how-to-monitor.md#available-metrics-and-reporting-intervals)`Used Memory RSS`和`Used Memory`。 如果收回原則位於，Redis 會開始收回金鑰時`Used_Memory`到達 hello 快取大小。 理想情況下，`Used Memory RSS` 應該只稍微高於 `Used memory`。 差異很大表示記憶體分散 (內部或外部)。 當`Used Memory RSS`是小於`Used Memory`，則表示已 hello 作業系統所交換的 hello 快取記憶體的一部分。 如果發生這種情況，您應該就會遇到顯著的延遲。 因為透過 Redis 沒有控制其配置的方式對應 toomemory 頁面，高`Used Memory RSS`通常是記憶體使用量的高峰 hello 結果。 當 Redis 會釋出記憶體時，hello 記憶體提供回 toohello 配置器，並 hello 配置器可能會或可能不會產生 hello 記憶體後 toohello 系統。 Hello 之間可能有不一致的情形`Used Memory`值和記憶體耗用量 hello 作業系統所報告。 可能是因為已用記憶體和釋放 Redis，但不是指定回復 toohello 系統 toohello 事實。 toohelp 降低記憶體問題，您可以執行下列步驟的 hello。
   
   * 升級 hello 快取 tooa 較大的大小，以便讓您不執行記憶體限制樣板 hello 系統上。
   * 設定，讓較舊的值會主動收回 hello 金鑰到期時間。
   * 監視 hello hello`used_memory_rss`快取度量。 當這個值會接近 hello 其快取大小時，您會發現效能問題的可能 toostart。 如果您使用進階版快取，或升級 tooa 較大的快取大小，請將 hello 資料分散在多個分區。
   
   如需詳細資訊，請參閱[hello 伺服器上記憶體不足的壓力](#memory-pressure-on-the-server)。

## <a name="additional-information"></a>其他資訊
* [應該使用哪個 Redis 快取供應項目和大小？](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [如何建立基準和測試 hello 我快取的效能？](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [如何執行 Redis 命令？](cache-faq.md#how-can-i-run-redis-commands)
* [如何 toomonitor Azure Redis 快取](cache-how-to-monitor.md)

