---
title: "aaaHow toomonitor Azure Redis 快取 |Microsoft 文件"
description: "了解如何 toomonitor hello 健全狀況和效能您的 Azure Redis 快取執行個體"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>如何 toomonitor Azure Redis 快取
Azure Redis 快取使用[Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/)tooprovide 監視您的快取執行個體的數個選項。 您可以檢視度量、 釘選度量圖表 toohello 開始面板、 自訂 hello 日期和時間範圍的監控圖表、 加入和從 hello 圖表移除度量和設定警示，當符合特定條件。 這些工具讓您 toomonitor hello 健全狀況的 Azure Redis 快取執行個體，以及協助您管理應用程式快取。

度量的 Azure Redis 快取執行個體所收集使用 hello Redis[資訊](http://redis.io/commands/info)30 天內每分鐘和自動儲存命令約兩次 (請參閱[匯出快取度量](#export-cache-metrics)tooconfigure不同的保留原則），可以顯示的 hello 度量圖表並評估警示規則。 如需 hello 所使用的每個快取度量的不同資訊值的詳細資訊，請參閱[可用的度量和報告間隔](#available-metrics-and-reporting-intervals)。

<a name="view-cache-metrics"></a>

tooview 快取度量，[瀏覽](cache-configure.md#configure-redis-cache-settings)tooyour 快取執行個體在 hello [Azure 入口網站](https://portal.azure.com)。  Azure Redis 快取會提供一些內建的圖表上 hello**概觀**刀鋒視窗，然後 hello **Redis 度量**刀鋒視窗。 加入或移除度量資訊以及變更報表間隔的 hello 可以自訂每個圖表。

![Redis 度量](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>檢視預先設定的計量圖表

hello**概觀**分頁有 hello 下列預先設定的監視圖表。

* [監視圖表](#monitoring-charts)
* [使用量圖表](#usage-charts)

### <a name="monitoring-charts"></a>監視圖表
hello**監視**> 一節中 hello**概觀**分頁有**點擊和遺漏**，**取得及設定**，**連線**，和**命令總數**圖表。

![監視圖表](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>使用量圖表
hello**使用量**> 一節中 hello**概觀**分頁有**Redis 伺服器負載**，**記憶體使用量**，**網路頻寬**，和**CPU 使用量**圖，並顯示 hello**定價層**hello 快取執行個體。

![使用量圖表](./media/cache-how-to-monitor/redis-cache-usage-part.png)

hello**定價層**顯示 hello 快取定價層，而且可用太[標尺](cache-how-to-scale.md)hello 快取 tooa 不同定價層。

## <a name="view-metrics-with-azure-monitor"></a>使用 Azure 監視器檢視計量
tooview Redis 度量使用及建立自訂圖表 Azure 監視器按一下**度量**從 hello**資源功能表**，來自訂圖表使用預期的 hello 度量、 報告時間間隔，圖表類型，並和更多。

![Redis 度量](./media/cache-how-to-monitor/redis-cache-monitor.png)

如需使用 Azure 監視器處理計量的詳細資訊，請參閱 [Microsoft Azure 的計量概觀](../monitoring-and-diagnostics/monitoring-overview-metrics.md)。

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>匯出快取計量
根據預設，Azure 監視器中的快取計量會[儲存 30 天](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive)，而後刪除。 toopersist 的時間超過 30 天您快取度量，您可以[指定儲存體帳戶](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)並指定**保留 （天）**快取度量的原則。 

tooconfigure 快取度量的儲存體帳戶：

1. 按一下**診斷**從 hello**資源功能表**在 hello **Redis 快取**刀鋒視窗。
2. 按一下 [開啟]。
3. 請檢查**封存 tooa 儲存體帳戶**。
4. 選取哪些 toostore hello 快取度量中的 hello 儲存體帳戶。
5. 檢查 hello **1 分鐘**核取方塊，並指定**保留 （天）**原則。 如果您不想 tooapply 任何保留原則與永久保留資料，設定**保留 （天）**太**0**。
6. 按一下 [儲存] 。

![Redis 診斷](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>在加法 tooarchiving 您快取度量 toostorage，您也可以[它們進行串流處理 tooan 事件中心，或將它們傳送 tooLog 分析](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics)。
>
>

tooaccess 您度量 hello 本文，如先前所述的 Azure 入口網站中進行檢視，和您也可以存取它們使用 hello [Azure 監視度量 REST API](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api)。

> [!NOTE]
> 如果您變更儲存體帳戶，先前設定的 hello 儲存體帳戶中的 hello 資料仍然可供下載，但它不會顯示在 hello Azure 入口網站。  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>可用度量和報告間隔
快取度量是使用數個報告間隔所報告，包括 [過去一小時]、[今天]、[過去一週] 和 [自訂]。 hello**度量**刀鋒視窗中的每個度量圖表會顯示 hello 圖表中的 hello 每個度量的平均值、 最小值和最大值和某些度量資訊會顯示 hello 報告間隔的總計。 

每個度量都包含兩個版本。 一個度量來測量效能 hello 整個快取，以及使用的快取[叢集](cache-how-to-premium-clustering.md)，hello 度量資訊會包含第二個版本`(Shard 0-9)`的快取中的單一分區 hello 名稱的量值的效能。 例如，如果快取都有 4 個分區，`Cache Hits`是 hello 總數量 hello 整個快取命中和`Cache Hits (Shard 3)`是只針對該分區 hello 快取的 hello 叫用。

> [!NOTE]
> 即使 hello 快取處於閒置狀態時沒有作用中連線的用戶端安裝應用程式，您可能會看到某些快取活動，例如連線的用戶端、 記憶體使用量，以及正在執行的作業。 Azure Redis 快取執行個體的 hello 作業期間，這個活動是正常的。
> 
> 

| 計量 | 說明 |
| --- | --- |
| 快取點擊 |hello hello 指定報告的時間間隔期間成功的索引鍵查閱數目。 這會對應太`keyspace_hits`從 hello Redis[資訊](http://redis.io/commands/info)命令。 |
| 快取遺漏 |hello hello 指定報告的時間間隔期間失敗的索引鍵查閱數目。 這會對應太`keyspace_misses`從 hello Redis INFO 命令。 快取遺漏並不一定代表 hello 快取發生問題。 例如，當使用另行快取程式設計模式的 hello，應用程式會尋找第一個 hello 快取的項目中。 如果 hello 項目不存在 （快取遺漏），hello 項目從 hello 資料庫擷取，並且加入 toohello 快取下一次。 快取遺漏會另行快取程式設計模式的 hello 正常的行為。 如果 hello 快取遺漏數目超過預期，檢查 hello 應用程式邏輯來填入和讀取 hello 快取。 如果正在收回項目從 hello 快取到期 toomemory 不足的壓力則可能有某些快取遺漏，但是會更好的度量 toomonitor 記憶體不足壓力`Used Memory`或`Evicted Keys`。 |
| 連線的用戶端 |hello hello 指定報告的時間間隔期間的用戶端連線 toohello 快取數目。 這會對應太`connected_clients`從 hello Redis INFO 命令。 一次 hello[連線限制](cache-configure.md#default-redis-server-configuration)達到後續連接嘗試 toohello 快取將會失敗。 請注意，即使沒有任何作用中用戶端應用程式中，有可能仍然是連線的用戶端因為 toointernal 處理程序和連線的少數的執行個體。 |
| 收回的金鑰 |hello hello 期間從 hello 快取收回的項目數目指定報告的時間間隔到期 toohello`maxmemory`限制。 這會對應太`evicted_keys`從 hello Redis INFO 命令。 |
| 到期的金鑰 |hello 指定報告的時間間隔期間，從 hello 快取到期 hello 項目數目。 這個值會對應太`expired_keys`從 hello Redis INFO 命令。 |
| 索引鍵總計  | hello 期間超過報告時間週期的 hello hello 快取中的索引鍵數目上限。 這會對應太`keyspace`從 hello Redis INFO 命令。 由於 tooa 限制 hello 基礎度量系統中，以啟用，叢集的快取的總索引鍵傳回 hello 最大數目 hello 分區 hello 報告時間間隔期間具有 hello 的索引鍵的最大數目的索引鍵。  |
| 取得 |hello hello 指定報告的時間間隔期間，從 hello 快取 get 作業數目。 這個值會是所有命令 hello Redis 資訊 hello 總和 hello 以下的都值： `cmdstat_get`， `cmdstat_hget`， `cmdstat_hgetall`， `cmdstat_hmget`， `cmdstat_mget`， `cmdstat_getbit`，和`cmdstat_getrange`，而且相等 toohello 快取點擊總數，在 hello 報告時間間隔期間的遺漏數。 |
| Redis 伺服器負載 |hello 百分比的循環的 hello Redis 伺服器是忙碌處理，而不等待閒置的訊息。 如果這個計數器達到的 100 表示 hello Redis 伺服器已達到效能上限，而無法處理 hello CPU 速度任何工作。 如果您看到高 Redis 伺服器負載，您會看到在 hello 用戶端的逾時例外狀況。 在此情況下，您應該考慮向上延展，或將資料分割成多個快取。 |
| 設定 |指定報告的時間間隔的設定作業 toohello 快取期間 hello 的 hello 數目。 這個值會是所有命令 hello Redis 資訊 hello 總和 hello 以下的都值： `cmdstat_set`， `cmdstat_hset`， `cmdstat_hmset`， `cmdstat_hsetnx`， `cmdstat_lset`， `cmdstat_mset`， `cmdstat_msetnx`， `cmdstat_setbit`， `cmdstat_setex`， `cmdstat_setrange`與`cmdstat_setnx`。 |
| 總作業數 |hello 命令總數 hello 期間處理 hello 快取伺服器指定報告的時間間隔。 這個值會對應太`total_commands_processed`從 hello Redis INFO 命令。 請注意，當 Azure Redis 快取純粹用於 pub/sub 會有任何的度量`Cache Hits`， `Cache Misses`， `Gets`，或`Sets`，但會有`Total Operations`反映 pub/sub 作業的 hello 快取使用量的度量。 |
| 已使用的記憶體 |hello hello 期間用於 hello 以 mb 為單位的快取中的索引鍵/值組的快取記憶體數量指定報告的時間間隔。 這個值會對應太`used_memory`從 hello Redis INFO 命令。 這不包括中繼資料或片段。 |
| 已用的記憶體 RSS |hello 快取使用的記憶體數量 （mb） hello 期間指定報告的時間間隔，包括片段和中繼資料。 這個值會對應太`used_memory_rss`從 hello Redis INFO 命令。 |
| CPU |hello 伺服器的 CPU 使用率 hello Azure Redis 快取百分比 hello 期間指定報告的時間間隔。 這個值會對應 toohello 作業系統`\Processor(_Total)\% Processor Time`效能計數器。 |
| 快取讀取 |從以 mb 為單位期間每秒 (MB/s) hello 的 hello 快取讀取的資料量 hello 指定報告的時間間隔。 這個值被衍生自 hello 的支援 hello 虛擬機器裝載 hello 快取，且為不 Redis 特定網路介面卡。 **此值與這個快取所使用的 toohello 網路頻寬。如果您想要的警示 tooset 伺服器端網路頻寬限制，然後建立使用這個`Cache Read`計數器。請參閱[本表](cache-faq.md#cache-performance)hello 觀察到的定價層和大小的各種快取的頻寬限制。** |
| 快取寫入 |hello 以 mb 為單位的 toohello 快取寫入期間每秒 (MB/s) hello 指定報告的時間間隔的資料量。 這個值被衍生自 hello 的支援 hello 虛擬機器裝載 hello 快取，且為不 Redis 特定網路介面卡。 此值對應 toohello 網路頻寬從 hello 用戶端傳送 toohello 快取的資料。 |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Alerts
您可以設定 tooreceive 根據度量和活動記錄檔的警示。 Azure 監視器可讓您 tooconfigure 警示 toodo hello，下列情況觸發：

* 傳送電子郵件通知
* 呼叫 Webhook
* 叫用 Azure 邏輯應用程式

tooconfigure 警示規則，以便您的快取中，按一下**警示規則**從 hello**資源功能表**。

![監視](./media/cache-how-to-monitor/redis-cache-monitoring.png)

如需設定和使用警示的詳細資訊，請參閱[警示概觀](../monitoring-and-diagnostics/insights-alerts-portal.md)。

## <a name="activity-logs"></a>活動記錄檔
活動記錄檔提供深入了解您的 Azure Redis 快取執行個體執行的 hello 操作。 此記錄以前稱為「稽核記錄」或「作業記錄」。 使用活動記錄檔，您可以決定 hello 」 功能，對象、 及何時"的任何寫入作業 (PUT、 POST、 DELETE) 您的 Azure Redis 快取執行個體上建立。 

> [!NOTE]
> 活動記錄不包含讀取 (GET) 作業。
>
>

tooview 活動記錄檔中的快取中，按一下**活動記錄**從 hello**資源功能表**。

如需活動記錄檔的詳細資訊，請參閱[hello Azure 活動記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)。











