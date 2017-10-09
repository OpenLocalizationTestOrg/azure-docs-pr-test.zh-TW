---
title: "監視度量的每個資源類型的支援度量 aaaAzure |Microsoft 文件"
description: "AAzure 監視器每一個資源類型的可用計量清單。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>支援 Azure 監視器的計量
Azure 監視度量，包括圖表它們 hello 入口網站中，透過 hello REST API 存取他們或查詢它們提供數種方式 toointeract 使用 PowerShell 或 CLI。 以下是目前可供 Azure 監視器計量管線使用的所有計量完整清單。

> [!NOTE]
> 其他度量資訊可能用於 hello 入口網站或使用舊版 Api。 此清單只會包含可用使用 hello 公開預覽狀態的彙總的 hello Azure 監視度量管線的公用預覽度量。
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|qpu_metric|QPU|Count|平均值|QPU。 範圍 0-100 (S1)、0-200 (S2) 和 0-400 (S4)|
|memory_metric|記憶體|位元組|平均值|記憶體。 範圍 0-25 GB (S1)、0-50 GB (S2) 和 0-100 GB (S4)|
|TotalConnectionRequests|連線要求的總計|Count|平均值|連線要求的總計。 這些是達到的。|
|SuccessfullConnectionsPerSec|每秒連線成功的次數|每秒計數|平均值|成功完成連線的速率。|
|TotalConnectionFailures|連線失敗的總計|Count|平均值|連線嘗試失敗的總計。|
|CurrentUserSessions|目前的使用者工作階段|Count|平均值|目前建立的使用者工作階段數目。|
|QueryPoolBusyThreads|查詢集區忙碌執行緒|Count|平均值|Hello 查詢執行緒集區中的忙碌執行緒數目。|
|CommandPoolJobQueueLength|命令集區作業佇列長度|Count|平均值|Hello hello 命令執行緒集區佇列中的作業數目。|
|ProcessingPoolJobQueueLength|處理集區作業佇列長度|Count|平均值|Hello hello 處理執行緒集區佇列中的非 i/o 作業數目。|
|CurrentConnections|連接：目前的連接|Count|平均值|目前已建立的用戶端連接數目。|
|CleanerCurrentPrice|記憶體︰清除工具目前價格|Count|平均值|目前的記憶體，$/ 位元組/時間、 標準化的 too1000 價格。|
|CleanerMemoryShrinkable|記憶體︰可壓縮的清除器記憶體|位元組|平均值|記憶體數量，以位元組為單位，主旨 toopurging hello 背景清除器造成的。|
|CleanerMemoryNonshrinkable|記憶體︰不可壓縮的清除器記憶體|位元組|平均值|記憶體數量，以位元組為單位，不主旨 toopurging hello 背景清除器造成的。|
|MemoryUsage|記憶體：記憶體使用量|位元組|平均值|Hello 伺服器處理序用於計算清除器記憶體價格的記憶體使用量。 等於 toocounter Process\PrivateBytes 加上 hello 的記憶體對應資料大小，忽略對應或 hello xVelocity 記憶體中分析引擎 (VertiPaq) hello xVelocity 引擎記憶體限制超過配置任何記憶體。|
|MemoryLimitHard|記憶體︰固定記憶體限制|位元組|平均值|組態檔中的固定記憶體限制。|
|MemoryLimitHigh|記憶體︰記憶體上限|位元組|平均值|來自組態檔的記憶體上限。|
|MemoryLimitLow|記憶體︰記憶體下限|位元組|平均值|來自組態檔的記憶體下限。|
|MemoryLimitVertiPaq|記憶體︰記憶體限制 VertiPaq|位元組|平均值|來自組態檔的記憶體內部限制。|
|Quota|記憶體︰配額|位元組|平均值|目前的記憶體配額，以位元組為單位。 記憶體配額也就是指授與使用的記憶體，或是保留的記憶體。|
|QuotaBlocked|記憶體︰封鎖的配額|Count|平均值|在釋放其他記憶體配額之前，目前已封鎖的配額要求數目。|
|VertiPaqNonpaged|記憶體︰未分頁的 VertiPaq|位元組|平均值|Hello 記憶體中引擎 hello 工作集，用於鎖定的記憶體位元組數。|
|VertiPaqPaged|記憶體︰分頁的 VertiPaq|位元組|平均值|可供記憶體內部資料使用的分頁記憶體位元組。|
|RowsReadPerSec|處理︰每秒讀取的資料列|每秒計數|平均值|從所有關聯式資料庫讀取資料列的速率。|
|RowsConvertedPerSec|處理︰每秒轉換的資料列|每秒計數|平均值|處理期間資料列轉換的速率。|
|RowsWrittenPerSec|處理︰每秒寫入的資料列|每秒計數|平均值|處理期間資料列寫入的速率。|
|CommandPoolBusyThreads|執行緒︰命令集區的忙碌執行緒數|Count|平均值|Hello 命令執行緒集區中的忙碌執行緒數目。|
|CommandPoolIdleThreads|執行緒︰命令集區的閒置執行緒數|Count|平均值|Hello 命令執行緒集區中的閒置執行緒數目。|
|LongParsingBusyThreads|執行緒︰完整剖析的忙碌執行緒數|Count|平均值|Hello 完整剖析執行緒集區中的忙碌執行緒數目。|
|LongParsingIdleThreads|執行緒︰完整剖析的閒置執行緒數|Count|平均值|Hello 完整剖析執行緒集區中的閒置執行緒數目。|
|LongParsingJobQueueLength|執行緒︰完整剖析的作業佇列長度|Count|平均值|Hello hello 完整剖析執行緒集區佇列中的作業數目。|
|ProcessingPoolBusyIOJobThreads|執行緒︰處理集區的忙碌 I/O 作業執行緒數|Count|平均值|Hello 處理執行緒集區中執行 I/O 作業的執行緒數目。|
|ProcessingPoolBusyNonIOThreads|執行緒︰處理集區的忙碌非 I/O 執行緒數|Count|平均值|Hello 處理執行緒集區中執行非 i/o 作業的執行緒數目。|
|ProcessingPoolIOJobQueueLength|執行緒：處理集區 I/O 作業佇列長度|Count|平均值|Hello hello 處理執行緒集區佇列中的 I/O 作業數目。|
|ProcessingPoolIdleIOJobThreads|執行緒︰處理集區的閒置 I/O 作業執行緒數|Count|平均值|Hello 處理執行緒集區中 I/O 作業的閒置執行緒數目。|
|ProcessingPoolIdleNonIOThreads|執行緒︰處理集區的閒置非 I/O 執行緒數|Count|平均值|Hello 處理執行緒集區中的閒置執行緒數目的專用 toonon i/o 作業。|
|QueryPoolIdleThreads|執行緒︰查詢集區的閒置執行緒數|Count|平均值|Hello 處理執行緒集區中 I/O 作業的閒置執行緒數目。|
|QueryPoolJobQueueLength|執行緒︰查詢集區的作業佇列長度|Count|平均值|Hello hello 查詢執行緒集區佇列中的作業數目。|
|ShortParsingBusyThreads|執行緒︰簡短剖析的忙碌執行緒數|Count|平均值|Hello 簡短剖析執行緒集區中的忙碌執行緒數目。|
|ShortParsingIdleThreads|執行緒︰簡短剖析的閒置執行緒數|Count|平均值|Hello 簡短剖析執行緒集區中的閒置執行緒數目。|
|ShortParsingJobQueueLength|執行緒︰簡短剖析的作業佇列長度|Count|平均值|Hello hello 簡短剖析執行緒集區佇列中的作業數目。|
|memory_thrashing_metric|記憶體猛移|百分比|平均值|記憶體猛移的平均值。|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|TotalRequests|閘道要求總數|Count|總計|閘道器要求數目|
|SuccessfulRequests|成功的閘道要求|Count|總計|成功閘道器要求數目|
|UnauthorizedRequests|未經授權閘道器要求|Count|總計|未經授權閘道器要求數目|
|FailedRequests|失敗的閘道要求|Count|總計|閘道要求中的失敗數目|
|OtherRequests|其他閘道器要求|Count|總計|其他閘道器要求數目|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|CoreCount|專用核心計數|Count|總計|Hello 批次帳戶中的專用核心總數|
|TotalNodeCount|專用節點計數|Count|總計|專用 hello 批次帳戶中的節點總數|
|LowPriorityCoreCount|LowPriority 核心計數|Count|總計|Hello 批次帳戶中的低優先順序核心總數|
|TotalLowPriorityNodeCount|低優先順序節點計數|Count|總計|Hello 批次帳戶中的低優先權的節點總數|
|CreatingNodeCount|建立節點計數|Count|總計|正在建立的節點數目|
|StartingNodeCount|啟動節點計數|Count|總計|啟動的節點數目|
|WaitingForStartTaskNodeCount|等候啟動工作節點計數|Count|總計|等候 hello 開始工作 toocomplete 的節點數目|
|StartTaskFailedNodeCount|啟動工作失敗的節點計數|Count|總計|未能 hello 開始工作的節點數目|
|IdleNodeCount|閒置的節點計數|Count|總計|閒置節點的數目|
|OfflineNodeCount|離線節點計數|Count|總計|離線節點的數目|
|RebootingNodeCount|重新啟動節點計數|Count|總計|重新啟動節點的數目|
|RebootingNodeCount|重新安裝映像節點計數|Count|總計|重新安裝映像的節點數目|
|RunningNodeCount|執行節點計數|Count|總計|執行節點的數目|
|LeavingPoolNodeCount|離開集區節點計數|Count|總計|離開 hello 集區的節點數目|
|UnusableNodeCount|無法使用的節點計數|Count|總計|無法使用的節點數目|
|PreemptedNodeCount|先占節點計數|Count|總計|先占節點的數量|
|TaskStartEvent|工作啟動的事件|Count|總計|已啟動的工作總次數|
|TaskCompleteEvent|工作完成事件|Count|總計|已完成的工作總次數|
|TaskFailEvent|工作失敗事件|Count|總計|失敗狀態中已完成的工作總數|
|PoolCreateEvent|集區建立事件|Count|總計|已建立集區的總數|
|PoolResizeStartEvent|調整集區大小啟動事件|Count|總計|已啟動的調整集區大小總次數|
|PoolResizeCompleteEvent|調整集區大小完成事件|Count|總計|已完成的調整集區大小總次數|
|PoolDeleteStartEvent|集區刪除啟動事件|Count|總計|已啟動的集區刪除總次數|
|PoolDeleteCompleteEvent|集區刪除完成事件|Count|總計|已完成的集區刪除總次數|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|connectedclients|連線的用戶端|Count|最大值||
|totalcommandsprocessed|總作業數|Count|總計||
|cachehits|快取點擊|Count|總計||
|cachemisses|快取遺漏|Count|總計||
|getcommands|取得|Count|總計||
|setcommands|設定|Count|總計||
|evictedkeys|收回的金鑰|Count|總計||
|totalkeys|索引鍵總計|Count|最大值||
|expiredkeys|到期的金鑰|Count|總計||
|usedmemory|已使用的記憶體|位元組|最大值||
|usedmemoryRss|已用的記憶體 RSS|位元組|最大值||
|serverLoad|伺服器負載|百分比|最大值||
|cacheWrite|快取寫入|每秒位元組|最大值||
|cacheRead|快取讀取|每秒位元組|最大值||
|percentProcessorTime|CPU|百分比|最大值||
|connectedclients0|連線的用戶端 (分區 0)|Count|最大值||
|totalcommandsprocessed0|總作業數 (分區 0)|Count|總計||
|cachehits0|快取點擊 (分區 0)|Count|總計||
|cachemisses0|快取遺漏 (分區 0)|Count|總計||
|getcommands0|取得 (分區 0)|Count|總計||
|setcommands0|設定 (分區 0)|Count|總計||
|evictedkeys0|收回的金鑰 (分區 0)|Count|總計||
|totalkeys0|金鑰總數 (分區 0)|Count|最大值||
|expiredkeys0|到期的金鑰 (分區 0)|Count|總計||
|usedmemory0|已用的記憶體 (分區 0)|位元組|最大值||
|usedmemoryRss0|已用的記憶體 RSS (分區 0)|位元組|最大值||
|serverLoad0|伺服器負載 (分區 0)|百分比|最大值||
|cacheWrite0|快取寫入 (分區 0)|每秒位元組|最大值||
|cacheRead0|快取讀取 (分區 0)|每秒位元組|最大值||
|percentProcessorTime0|CPU (分區 0)|百分比|最大值||
|connectedclients1|連線的用戶端 (分區 1)|Count|最大值||
|totalcommandsprocessed1|總作業數 (分區 1)|Count|總計||
|cachehits1|快取點擊 (分區 1)|Count|總計||
|cachemisses1|快取遺漏 (分區 1)|Count|總計||
|getcommands1|取得 (分區 1)|Count|總計||
|setcommands1|設定 (分區 1)|Count|總計||
|evictedkeys1|收回的金鑰 (分區 1)|Count|總計||
|totalkeys1|金鑰總數 (分區 1)|Count|最大值||
|expiredkeys1|到期的金鑰 (分區 1)|Count|總計||
|usedmemory1|已用的記憶體 (分區 1)|位元組|最大值||
|usedmemoryRss1|已用的記憶體 RSS (分區 1)|位元組|最大值||
|serverLoad1|伺服器負載 (分區 1)|百分比|最大值||
|cacheWrite1|快取寫入 (分區 1)|每秒位元組|最大值||
|cacheRead1|快取讀取 (分區 1)|每秒位元組|最大值||
|percentProcessorTime1|CPU (分區 1)|百分比|最大值||
|connectedclients2|連線的用戶端 (分區 2)|Count|最大值||
|totalcommandsprocessed2|總作業數 (分區 2)|Count|總計||
|cachehits2|快取點擊 (分區 2)|Count|總計||
|cachemisses2|快取遺漏 (分區 2)|Count|總計||
|getcommands2|取得 (分區 2)|Count|總計||
|setcommands2|設定 (分區 2)|Count|總計||
|evictedkeys2|收回的金鑰 (分區 2)|Count|總計||
|totalkeys2|金鑰總數 (分區 2)|Count|最大值||
|expiredkeys2|到期的金鑰 (分區 2)|Count|總計||
|usedmemory2|已用的記憶體 (分區 2)|位元組|最大值||
|usedmemoryRss2|已用的記憶體 RSS (分區 2)|位元組|最大值||
|serverLoad2|伺服器負載 (分區 2)|百分比|最大值||
|cacheWrite2|快取寫入 (分區 2)|每秒位元組|最大值||
|cacheRead2|快取讀取 (分區 2)|每秒位元組|最大值||
|percentProcessorTime2|CPU (分區 2)|百分比|最大值||
|connectedclients3|連線的用戶端 (分區 3)|Count|最大值||
|totalcommandsprocessed3|總作業數 (分區 3)|Count|總計||
|cachehits3|快取點擊 (分區 3)|Count|總計||
|cachemisses3|快取遺漏 (分區 3)|Count|總計||
|getcommands3|取得 (分區 3)|Count|總計||
|setcommands3|設定 (分區 3)|Count|總計||
|evictedkeys3|收回的金鑰 (分區 3)|Count|總計||
|totalkeys3|金鑰總數 (分區 3)|Count|最大值||
|expiredkeys3|到期的金鑰 (分區 3)|Count|總計||
|usedmemory3|已用的記憶體 (分區 3)|位元組|最大值||
|usedmemoryRss3|已用的記憶體 RSS (分區 3)|位元組|最大值||
|serverLoad3|伺服器負載 (分區 3)|百分比|最大值||
|cacheWrite3|快取寫入 (分區 3)|每秒位元組|最大值||
|cacheRead3|快取讀取 (分區 3)|每秒位元組|最大值||
|percentProcessorTime3|CPU (分區 3)|百分比|最大值||
|connectedclients4|連線的用戶端 (分區 4)|Count|最大值||
|totalcommandsprocessed4|總作業數 (分區 4)|Count|總計||
|cachehits4|快取點擊 (分區 4)|Count|總計||
|cachemisses4|快取遺漏 (分區 4)|Count|總計||
|getcommands4|取得 (分區 4)|Count|總計||
|setcommands4|設定 (分區 4)|Count|總計||
|evictedkeys4|收回的金鑰 (分區 4)|Count|總計||
|totalkeys4|金鑰總數 (分區 4)|Count|最大值||
|expiredkeys4|到期的金鑰 (分區 4)|Count|總計||
|usedmemory4|已用的記憶體 (分區 4)|位元組|最大值||
|usedmemoryRss4|已用的記憶體 RSS (分區 4)|位元組|最大值||
|serverLoad4|伺服器負載 (分區 4)|百分比|最大值||
|cacheWrite4|快取寫入 (分區 4)|每秒位元組|最大值||
|cacheRead4|快取讀取 (分區 4)|每秒位元組|最大值||
|percentProcessorTime4|CPU (分區 4)|百分比|最大值||
|connectedclients5|連線的用戶端 (分區 5)|Count|最大值||
|totalcommandsprocessed5|總作業數 (分區 5)|Count|總計||
|cachehits5|快取點擊 (分區 5)|Count|總計||
|cachemisses5|快取遺漏 (分區 5)|Count|總計||
|getcommands5|取得 (分區 5)|Count|總計||
|setcommands5|設定 (分區 5)|Count|總計||
|evictedkeys5|收回的金鑰 (分區 5)|Count|總計||
|totalkeys5|金鑰總數 (分區 5)|Count|最大值||
|expiredkeys5|到期的金鑰 (分區 5)|Count|總計||
|usedmemory5|已用的記憶體 (分區 5)|位元組|最大值||
|usedmemoryRss5|已用的記憶體 RSS (分區 5)|位元組|最大值||
|serverLoad5|伺服器負載 (分區 5)|百分比|最大值||
|cacheWrite5|快取寫入 (分區 5)|每秒位元組|最大值||
|cacheRead5|快取讀取 (分區 5)|每秒位元組|最大值||
|percentProcessorTime5|CPU (分區 5)|百分比|最大值||
|connectedclients6|連線的用戶端 (分區 6)|Count|最大值||
|totalcommandsprocessed6|總作業數 (分區 6)|Count|總計||
|cachehits6|快取點擊 (分區 6)|Count|總計||
|cachemisses6|快取遺漏 (分區 6)|Count|總計||
|getcommands6|取得 (分區 6)|Count|總計||
|setcommands6|設定 (分區 6)|Count|總計||
|evictedkeys6|收回的金鑰 (分區 6)|Count|總計||
|totalkeys6|金鑰總數 (分區 6)|Count|最大值||
|expiredkeys6|到期的金鑰 (分區 6)|Count|總計||
|usedmemory6|已用的記憶體 (分區 6)|位元組|最大值||
|usedmemoryRss6|已用的記憶體 RSS (分區 6)|位元組|最大值||
|serverLoad6|伺服器負載 (分區 6)|百分比|最大值||
|cacheWrite6|快取寫入 (分區 6)|每秒位元組|最大值||
|cacheRead6|快取讀取 (分區 6)|每秒位元組|最大值||
|percentProcessorTime6|CPU (分區 6)|百分比|最大值||
|connectedclients7|連線的用戶端 (分區 7)|Count|最大值||
|totalcommandsprocessed7|總作業數 (分區 7)|Count|總計||
|cachehits7|快取點擊 (分區 7)|Count|總計||
|cachemisses7|快取遺漏 (分區 7)|Count|總計||
|getcommands7|取得 (分區 7)|Count|總計||
|setcommands7|設定 (分區 7)|Count|總計||
|evictedkeys7|收回的金鑰 (分區 7)|Count|總計||
|totalkeys7|金鑰總數 (分區 7)|Count|最大值||
|expiredkeys7|到期的金鑰 (分區 7)|Count|總計||
|usedmemory7|已用的記憶體 (分區 7)|位元組|最大值||
|usedmemoryRss7|已用的記憶體 RSS (分區 7)|位元組|最大值||
|serverLoad7|伺服器負載 (分區 7)|百分比|最大值||
|cacheWrite7|快取寫入 (分區 7)|每秒位元組|最大值||
|cacheRead7|快取讀取 (分區 7)|每秒位元組|最大值||
|percentProcessorTime7|CPU (分區 7)|百分比|最大值||
|connectedclients8|連線的用戶端 (分區 8)|Count|最大值||
|totalcommandsprocessed8|總作業數 (分區 8)|Count|總計||
|cachehits8|快取點擊 (分區 8)|Count|總計||
|cachemisses8|快取遺漏 (分區 8)|Count|總計||
|getcommands8|取得 (分區 8)|Count|總計||
|setcommands8|設定 (分區 8)|Count|總計||
|evictedkeys8|收回的金鑰 (分區 8)|Count|總計||
|totalkeys8|金鑰總數 (分區 8)|Count|最大值||
|expiredkeys8|到期的金鑰 (分區 8)|Count|總計||
|usedmemory8|已用的記憶體 (分區 8)|位元組|最大值||
|usedmemoryRss8|已用的記憶體 RSS (分區 8)|位元組|最大值||
|serverLoad8|伺服器負載 (分區 8)|百分比|最大值||
|cacheWrite8|快取寫入 (分區 8)|每秒位元組|最大值||
|cacheRead8|快取讀取 (分區 8)|每秒位元組|最大值||
|percentProcessorTime8|CPU (分區 8)|百分比|最大值||
|connectedclients9|連線的用戶端 (分區 9)|Count|最大值||
|totalcommandsprocessed9|總作業數 (分區 9)|Count|總計||
|cachehits9|快取點擊 (分區 9)|Count|總計||
|cachemisses9|快取遺漏 (分區 9)|Count|總計||
|getcommands9|取得 (分區 9)|Count|總計||
|setcommands9|設定 (分區 9)|Count|總計||
|evictedkeys9|收回的金鑰 (分區 9)|Count|總計||
|totalkeys9|金鑰總數 (分區 9)|Count|最大值||
|expiredkeys9|到期的金鑰 (分區 9)|Count|總計||
|usedmemory9|已用的記憶體 (分區 9)|位元組|最大值||
|usedmemoryRss9|已用的記憶體 RSS (分區 9)|位元組|最大值||
|serverLoad9|伺服器負載 (分區 9)|百分比|最大值||
|cacheWrite9|快取寫入 (分區 9)|每秒位元組|最大值||
|cacheRead9|快取讀取 (分區 9)|每秒位元組|最大值||
|percentProcessorTime9|CPU (分區 9)|百分比|最大值||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|TotalCalls|呼叫總數|Count|總計|呼叫總數。|
|SuccessfulCalls|成功的呼叫|Count|總計|成功的呼叫數。|
|TotalErrors|錯誤總數|Count|總計|具有錯誤回應 (HTTP 回應碼 4xx 或 5xx) 的呼叫總數。|
|BlockedCalls|已封鎖的呼叫|Count|總計|超過速率或配額限制的呼叫數目。|
|ServerErrors|伺服器錯誤|Count|總計|具有服務內部錯誤 (HTTP 回應碼 5xx) 的呼叫數目。|
|ClientErrors|用戶端錯誤|Count|總計|具有用戶端錯誤 (HTTP 回應碼 4xx) 的呼叫數目。|
|DataIn|資料輸入|位元組|總計|內送資料大小，以位元組為單位。|
|DataOut|資料輸出|位元組|總計|輸出資料大小，以位元組為單位。|
|Latency|Latency|毫秒|平均值|延遲，以毫秒為單位。|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|百分比|平均值|目前正在使用 hello 虛擬機器的已配置的計算單位的 hello 百分比|
|Network In|Network In|位元組|總計|hello 接收位元組數所有網路介面上的 hello 虛擬機器 （連入流量）|
|Network Out|Network Out|位元組|總計|hello 數字的位元組所 hello （傳出流量） 的虛擬機器的所有網路介面上的逾時|
|Disk Read Bytes|Disk Read Bytes|位元組|總計|在監視期間從磁碟讀取的位元組總計|
|Disk Write Bytes|Disk Write Bytes|位元組|總計|在監視期間寫入 toodisk 的位元組總數|
|Disk Read Operations/Sec|Disk Read Operations/Sec|每秒計數|平均值|磁碟讀取 IOPS|
|Disk Write Operations/Sec|Disk Write Operations/Sec|每秒計數|平均值|磁碟寫入 IOPS|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|百分比|平均值|目前正在使用 hello 虛擬機器的已配置的計算單位的 hello 百分比|
|Network In|Network In|位元組|總計|hello 接收位元組數所有網路介面上的 hello 虛擬機器 （連入流量）|
|Network Out|Network Out|位元組|總計|hello 數字的位元組所 hello （傳出流量） 的虛擬機器的所有網路介面上的逾時|
|Disk Read Bytes|Disk Read Bytes|位元組|總計|在監視期間從磁碟讀取的位元組總計|
|Disk Write Bytes|Disk Write Bytes|位元組|總計|在監視期間寫入 toodisk 的位元組總數|
|Disk Read Operations/Sec|Disk Read Operations/Sec|每秒計數|平均值|磁碟讀取 IOPS|
|Disk Write Operations/Sec|Disk Write Operations/Sec|每秒計數|平均值|磁碟寫入 IOPS|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|百分比|平均值|目前正在使用 hello 虛擬機器的已配置的計算單位的 hello 百分比|
|Network In|Network In|位元組|總計|hello 接收位元組數所有網路介面上的 hello 虛擬機器 （連入流量）|
|Network Out|Network Out|位元組|總計|hello 數字的位元組所 hello （傳出流量） 的虛擬機器的所有網路介面上的逾時|
|Disk Read Bytes|Disk Read Bytes|位元組|總計|在監視期間從磁碟讀取的位元組總計|
|Disk Write Bytes|Disk Write Bytes|位元組|總計|在監視期間寫入 toodisk 的位元組總數|
|Disk Read Operations/Sec|Disk Read Operations/Sec|每秒計數|平均值|磁碟讀取 IOPS|
|Disk Write Operations/Sec|Disk Write Operations/Sec|每秒計數|平均值|磁碟寫入 IOPS|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|DCIApiCalls|Customer Insights API 呼叫|Count|總計||
|DCIMappingImportOperationSuccessfulLines|對應匯入作業成功行|Count|總計||
|DCIMappingImportOperationFailedLines|對應匯入作業失敗行|Count|總計||
|DCIMappingImportOperationTotalLines|對應匯入作業行總計|Count|總計||
|DCIMappingImportOperationRuntimeInSeconds|對應匯入作業執行階段 (以秒為單位)|秒|總計||
|DCIOutboundProfileExportSucceeded|輸出設定檔匯出成功|Count|總計||
|DCIOutboundProfileExportFailed|輸出設定檔匯出失敗|Count|總計||
|DCIOutboundProfileExportDuration|輸出設定檔匯出持續時間|秒|總計||
|DCIOutboundKpiExportSucceeded|輸出 KPI 匯出成功|Count|總計||
|DCIOutboundKpiExportFailed|輸出 KPI 匯出失敗|Count|總計||
|DCIOutboundKpiExportDuration|輸出 KPI 匯出持續時間|秒|總計||
|DCIOutboundKpiExportStarted|輸出 KPI 匯出開始|秒|總計||
|DCIOutboundKpiRecordCount|輸出 KPI 記錄計數|秒|總計||
|DCIOutboundProfileExportCount|輸出設定檔匯出計數|秒|總計||
|DCIOutboundInitialProfileExportFailed|輸出初始設定檔匯出失敗|秒|總計||
|DCIOutboundInitialProfileExportSucceeded|輸出初始設定檔匯出成功|秒|總計||
|DCIOutboundInitialKpiExportFailed|輸出初始 KPI 匯出失敗|秒|總計||
|DCIOutboundInitialKpiExportSucceeded|輸出初始 KPI 匯出成功|秒|總計||
|DCIOutboundInitialProfileExportDurationInSeconds|輸出初始設定檔匯出持續時間 (以秒為單位)|秒|總計||
|AdlaJobForStandardKpiFailed|標準 KPI 的 Adla 作業失敗 (以秒為單位)|秒|總計||
|AdlaJobForStandardKpiTimeOut|標準 KPI 的 Adla 作業逾時 (以秒為單位)|秒|總計||
|AdlaJobForStandardKpiCompleted|標準 KPI 的 Adla 作業完成 (以秒為單位)|秒|總計||
|ImportASAValuesFailed|匯入 ASA 值失敗計數|Count|總計||
|ImportASAValuesSucceeded|匯入 ASA 值成功計數|Count|總計||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|JobEndedSuccess|成功的作業|Count|總計|成功作業計數。|
|JobEndedFailure|失敗的作業|Count|總計|失敗作業計數。|
|JobEndedCancelled|取消的作業|Count|總計|取消作業計數。|
|JobAUEndedSuccess|成功 AU 時間|秒|總計|成功作業的 AU 時間總計。|
|JobAUEndedFailure|失敗 AU 時間|秒|總計|失敗作業的 AU 時間總計。|
|JobAUEndedCancelled|取消的 AU 時間|秒|總計|取消作業的 AU 時間總計。|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|cpu_percent|CPU 百分比|百分比|平均值|CPU 百分比|
|compute_limit|計算單位限制|Count|平均值|計算單位限制|
|compute_consumption_percent|計算單位百分比|百分比|平均值|計算單位百分比|
|memory_percent|記憶體百分比|百分比|平均值|記憶體百分比|
|io_consumption_percent|IO 百分比|百分比|平均值|IO 百分比|
|storage_percent|儲存體百分比|百分比|平均值|儲存體百分比|
|storage_used|已使用儲存體|位元組|平均值|已使用儲存體|
|storage_limit|儲存體限制|位元組|平均值|儲存體限制|
|active_connections|作用中的連接總數|Count|平均值|作用中的連接總數|
|connections_failed|失敗的連接總數|Count|平均值|失敗的連接總數|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|cpu_percent|CPU 百分比|百分比|平均值|CPU 百分比|
|compute_limit|計算單位限制|Count|平均值|計算單位限制|
|compute_consumption_percent|計算單位百分比|百分比|平均值|計算單位百分比|
|memory_percent|記憶體百分比|百分比|平均值|記憶體百分比|
|io_consumption_percent|IO 百分比|百分比|平均值|IO 百分比|
|storage_percent|儲存體百分比|百分比|平均值|儲存體百分比|
|storage_used|已使用儲存體|位元組|平均值|已使用儲存體|
|storage_limit|儲存體限制|位元組|平均值|儲存體限制|
|active_connections|作用中的連接總數|Count|平均值|作用中的連接總數|
|connections_failed|失敗的連接總數|Count|平均值|失敗的連接總數|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|遙測訊息傳送嘗試|Count|總計|送出的遙測裝置到雲端訊息嘗試 toobe 數目 tooyour IoT 中樞|
|d2c.telemetry.ingress.success|已傳送的遙測訊息|Count|總計|裝置到雲端遙測訊息數目已成功傳送 tooyour IoT 中樞|
|c2d.commands.egress.complete.success|完成的命令|Count|總計|雲端到裝置命令已順利完成 hello 裝置數目|
|c2d.commands.egress.abandon.success|放棄的命令|Count|總計|放棄 hello 裝置的雲端到裝置命令數目|
|c2d.commands.egress.reject.success|拒絕的命令|Count|總計|雲端到裝置 hello 裝置被拒絕的命令數目|
|devices.totalDevices|裝置總計|Count|總計|已登錄的裝置數 tooyour IoT 中樞|
|devices.connectedDevices.allProtocol|連接的裝置|Count|總計|連接的裝置數目 tooyour IoT 中樞|
|d2c.telemetry.egress.success|已傳遞的遙測訊息|Count|總計|訊息已成功地寫入 tooendpoints （總計） 的次數|
|d2c.telemetry.egress.dropped|捨棄的訊息|Count|總計|卸除，因為 hello 傳遞端點已無作用的訊息數目|
|d2c.telemetry.egress.orphaned|被遺棄的訊息|Count|總計|訊息不符合任何包括 hello 後援路由的路由的 hello 數目|
|d2c.telemetry.egress.invalid|無效的訊息|Count|總計|hello 的訊息計數不會傳遞到期 tooincompatibility 與 hello 端點|
|d2c.telemetry.egress.fallback|符合後援條件的訊息|Count|總計|寫入 toohello 後援端點的訊息數|
|d2c.endpoints.egress.eventHubs|訊息傳遞 tooEvent 中樞端點|Count|總計|訊息已成功寫入的 tooEvent 中心端點的次數|
|d2c.endpoints.latency.eventHubs|事件中樞端點的訊息延遲|毫秒|平均值|hello 之間的平均延遲訊息輸入 toohello IoT 中樞與訊息輸入至事件中心的端點，以毫秒為單位|
|d2c.endpoints.egress.serviceBusQueues|訊息傳遞 tooService 匯流排佇列端點|Count|總計|訊息已成功寫入的 tooService 匯流排佇列端點的次數|
|d2c.endpoints.latency.serviceBusQueues|服務匯流排佇列端點的訊息延遲|毫秒|平均值|hello 之間的平均延遲訊息輸入 toohello IoT 中樞與訊息輸入至服務匯流排佇列端點，以毫秒為單位|
|d2c.endpoints.egress.serviceBusTopics|訊息傳遞 tooService 匯流排主題端點|Count|總計|訊息已成功寫入的 tooService 匯流排主題端點的次數|
|d2c.endpoints.latency.serviceBusTopics|服務匯流排主題端點的訊息延遲|毫秒|平均值|hello 之間的平均延遲訊息輸入 toohello IoT 中樞與訊息輸入至服務匯流排主題端點，以毫秒為單位|
|d2c.endpoints.egress.builtIn.events|訊息傳遞 toohello 內建端點 （訊息/事件）|Count|總計|訊息已成功寫入的 toohello 內建端點 （訊息/事件） 的次數|
|d2c.endpoints.latency.builtIn.events|Hello 內建端點 （訊息/事件） 的訊息延遲|毫秒|平均值|hello 之間的平均延遲訊息輸入 toohello IoT 中樞與訊息輸入至 hello 內建端點 （訊息/事件），以毫秒為單位 |
|d2c.twin.read.success|裝置的成功對應項讀取|Count|總計|讀取所有成功的裝置啟動兩個 hello 計數。|
|d2c.twin.read.failure|裝置的失敗對應項讀取|Count|總計|所有的 hello 計數失敗裝置起始兩個讀取。|
|d2c.twin.read.size|裝置的對應項讀取回應大小|位元組|平均值|hello 平均、 最小值 和所有成功的最大裝置起始 twin 讀取。|
|d2c.twin.update.success|裝置的成功對應項更新|Count|總計|所有成功的裝置啟動兩個更新的 hello 計數。|
|d2c.twin.update.failure|裝置的失敗對應項更新|Count|總計|hello 計數的所有失敗的裝置啟動兩個更新。|
|d2c.twin.update.size|裝置的對應項更新大小|位元組|平均值|hello 平均、 最小值 和所有成功的最大大小裝置起始 twin 更新。|
|c2d.methods.success|成功直接方法叫用|Count|總計|所有成功的直接方法呼叫 hello 計數。|
|c2d.methods.failure|失敗直接方法叫用|Count|總計|所有的 hello 計數無法直接方法呼叫。|
|c2d.methods.requestSize|直接方法叫用的要求大小|位元組|平均值|hello 平均、 最小值 和所有成功的直接方法要求的最大值。|
|c2d.methods.responseSize|直接方法叫用的回應大小|位元組|平均值|hello 平均、 最小值 和所有成功的直接方法回應的最大值。|
|c2d.twin.read.success|後端的成功對應項讀取|Count|總計|讀取所有成功的後端初始化兩個 hello 計數。|
|c2d.twin.read.failure|後端的失敗對應項讀取|Count|總計|所有的 hello 計數失敗後結束起始兩個讀取。|
|c2d.twin.read.size|後端的對應項讀取回應大小|位元組|平均值|hello 平均、 最小值和最大值的所有成功後結束起始 twin 讀取。|
|c2d.twin.update.success|後端的成功對應項更新|Count|總計|所有成功的後端初始化兩個更新的 hello 計數。|
|c2d.twin.update.failure|後端的失敗對應項更新|Count|總計|所有的 hello 計數失敗後結束起始兩個更新。|
|c2d.twin.update.size|後端的對應項更新大小|位元組|平均值|hello 平均、 最小值 和所有成功的最大大小後結束起始 twin 更新。|
|twinQueries.success|成功對應項查詢|Count|總計|所有成功的兩個查詢的 hello 計數。|
|twinQueries.failure|失敗對應項查詢|Count|總計|所有失敗的兩個查詢的 hello 計數。|
|twinQueries.resultSize|對應項查詢結果大小|位元組|平均值|hello 平均、 最小值、 和 hello 所有成功的兩個查詢的結果大小的最大值。|
|jobs.createTwinUpdateJob.success|成功建立的對應項更新作業|Count|總計|hello 所有成功建立兩個更新作業數目。|
|jobs.createTwinUpdateJob.failure|建立失敗的對應項更新作業|Count|總計|建立兩個更新作業的所有失敗的 hello 計數。|
|jobs.createDirectMethodJob.success|成功建立的方法叫用作業|Count|總計|hello 所有成功建立直接的方法引動過程作業數目。|
|jobs.createDirectMethodJob.failure|建立失敗的方法叫用作業|Count|總計|建立直接的方法引動過程作業的所有失敗的 hello 計數。|
|jobs.listJobs.success|成功呼叫 toolist 工作|Count|總計|所有成功呼叫 toolist 作業 hello 計數。|
|jobs.listJobs.failure|失敗的呼叫 toolist 工作|Count|總計|所有的失敗的呼叫 toolist 作業 hello 計數。|
|jobs.cancelJob.success|成功取消作業|Count|總計|所有成功的 hello 計數呼叫 toocancel 作業。|
|jobs.cancelJob.failure|取消作業失敗|Count|總計|所有失敗的呼叫 toocancel 作業 hello 計數。|
|jobs.queryJobs.success|成功作業查詢|Count|總計|所有成功呼叫 tooquery 作業 hello 計數。|
|jobs.queryJobs.failure|失敗作業查詢|Count|總計|所有的失敗的呼叫 tooquery 作業 hello 計數。|
|jobs.completed|已完成的工作|Count|總計|hello 與所有已完成的工作數目。|
|jobs.failed|失敗作業|Count|總計|hello 所有失敗的作業數目。|
|d2c.telemetry.ingress.sendThrottle|節流錯誤數目|Count|總計|由於 toodevice 輸送量流速節流錯誤的數目|
|dailyMessageQuotaUsed|已使用的訊息總數|Count|平均值|今日已使用的總訊息數|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|INREQS|傳入的傳送要求|Count|總計|針對通知中樞傳入的傳送要求總數|
|SUCCREQ|成功的要求|Count|總計|命名空間的成功要求總數|
|FAILREQ|失敗的要求|Count|總計|命名空間的失敗要求總數|
|SVRBSY|伺服器忙線錯誤|Count|總計|命名空間的伺服器忙線錯誤總數|
|INTERR|內部伺服器錯誤|Count|總計|命名空間的內部伺服器錯誤總數|
|MISCERR|其他錯誤|Count|總計|命名空間的失敗要求總數|
|INMSGS|傳入訊息|Count|總計|命名空間的內送訊息總數|
|OUTMSGS|外送訊息|Count|總計|命名空間的外送訊息總數|
|EHINMBS|傳入位元組|位元組|總計|命名空間的事件中樞內送訊息輸送量|
|EHOUTMBS|傳出位元組|位元組|總計|命名空間的外送訊息總數|
|EHABL|封存待處理項目訊息|Count|總計|命名空間的事件中樞封存於待處理項目中訊息|
|EHAMSGS|封存訊息|Count|總計|命名空間中的事件中樞已封存訊息|
|EHAMBS|封存訊息輸送量|位元組|總計|命名空間中的事件中樞已封存訊息輸送量|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|RunsStarted|執行已啟動|Count|總計|已啟動的工作流程執行數目。|
|RunsCompleted|完成的執行|Count|總計|已完成的工作流程執行數目。|
|RunsSucceeded|已成功的執行|Count|總計|已成功的工作流程執行數目。|
|RunsFailed|失敗的執行|Count|總計|已失敗的工作流程執行數目。|
|RunsCancelled|取消的執行|Count|總計|已取消的工作流程執行數目。|
|RunLatency|執行延遲|秒|平均值|已完成的工作流程執行延遲。|
|RunSuccessLatency|執行成功的延遲|秒|平均值|已成功的工作流程執行延遲。|
|RunThrottledEvents|執行節流的事件|Count|總計|工作流程動作或觸發節流的事件數目。|
|RunFailurePercentage|執行失敗百分比|百分比|總計|已失敗的工作流程執行百分比。|
|ActionsStarted|啟動的動作 |Count|總計|已啟動的工作流程動作數目。|
|ActionsCompleted|完成的動作 |Count|總計|已完成的工作流程動作數目。|
|ActionsSucceeded|成功的動作 |Count|總計|已成功的工作流程動作數目。|
|ActionsFailed|動作的失敗|Count|總計|已失敗的工作流程動作數目。|
|ActionsSkipped|略過的動作 |Count|總計|已略過的工作流程動作數目。|
|ActionLatency|動作延遲 |秒|平均值|已完成的工作流程動作延遲。|
|ActionSuccessLatency|動作成功延遲 |秒|平均值|已成功的工作流程動作延遲。|
|ActionThrottledEvents|動作節流的事件|Count|總計|工作流程動作已節流的事件數目。|
|TriggersStarted|啟動的觸發程序 |Count|總計|已啟動的工作流程觸發程序數目。|
|TriggersCompleted|完成的觸發程序 |Count|總計|已完成的工作流程觸發程序數目。|
|TriggersSucceeded|成功的觸發程序 |Count|總計|已成功的工作流程觸發程序數目。|
|TriggersFailed|失敗的觸發程序 |Count|總計|已失敗的工作流程觸發程序數目。|
|TriggersSkipped|略過的觸發程序|Count|總計|已略過的工作流程觸發程序數目。|
|TriggersFired|引發的觸發程序 |Count|總計|已引發的工作流程觸發程序數目。|
|TriggerLatency|觸發程序延遲 |秒|平均值|已完成的工作流程觸發程序延遲。|
|TriggerFireLatency|觸發程序引發延遲 |秒|平均值|已引發的工作流程觸發程序延遲。|
|TriggerSuccessLatency|觸發程序成功延遲 |秒|平均值|已成功的工作流程觸發程序延遲。|
|TriggerThrottledEvents|觸發程序節流的事件|Count|總計|工作流程觸發程序節流的事件數目。|
|BillableActionExecutions|可計費的動作執行|Count|總計|計費的工作流程動作執行數目。|
|BillableTriggerExecutions|可計費的觸發程序執行|Count|總計|計費的工作流程觸發程序執行數目。|
|TotalBillableExecutions|可計費的總執行次數|Count|總計|計費的工作流程執行數目。|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|Throughput|Throughput|每秒位元組|平均值||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|BytesIn|BytesIn|Count|總計||
|BytesOut|BytesOut|Count|總計||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|registration.all|註冊作業|Count|總計|hello （建立更新查詢和刪除） 的所有註冊成功的作業數目。 |
|registration.create|註冊建立作業|Count|總計|所有成功的登錄建立 hello 計數。|
|registration.update|註冊更新作業|Count|總計|hello 所有註冊成功的更新計數。|
|registration.get|註冊讀取作業|Count|總計|hello 所有註冊成功的查詢數目。|
|registration.delete|註冊刪除作業|Count|總計|所有註冊成功的刪除動作的 hello 計數。|
|incoming|傳入訊息|Count|總計|hello 計數的所有成功傳送的 API 呼叫。 |
|incoming.scheduled|傳送已排程的推播通知|Count|總計|取消已排程的推播通知|
|incoming.scheduled.cancel|取消已排程的推播通知|Count|總計|取消已排程的推播通知|
|scheduled.pending|暫止已排程的通知|Count|總計|暫止已排程的通知|
|installation.all|安裝管理作業|Count|總計|安裝管理作業|
|installation.get|取得安裝作業|Count|總計|取得安裝作業|
|installation.upsert|建立或更新安裝作業|Count|總計|建立或更新安裝作業|
|installation.patch|修補安裝作業|Count|總計|修補安裝作業|
|installation.delete|刪除安裝作業|Count|總計|刪除安裝作業|
|outgoing.allpns.success|成功通知|Count|總計|hello 所有成功通知數目。|
|outgoing.allpns.invalidpayload|承載錯誤|Count|總計|hello 失敗，因為 hello PNS 傳回不正確的承載錯誤的推播通知數目。|
|outgoing.allpns.pnserror|外部通知系統錯誤|Count|總計|hello 失敗，因為發生問題，與 hello PNS （不包括驗證問題） 進行通訊的推播通知數目。|
|outgoing.allpns.channelerror|通道錯誤|Count|總計|推播通知失敗，因為 hello 通道無效未正確調整應用程式，或已過期的 hello 與相關聯的 hello 計數。|
|outgoing.allpns.badorexpiredchannel|錯誤或過期的通道錯誤|Count|總計|推播通知失敗，因為 hello 通道/語彙基元/registrationId hello 註冊中已過期或無效的 hello 計數。|
|outgoing.wns.success|WNS 成功通知|Count|總計|hello 所有成功通知數目。|
|outgoing.wns.invalidcredentials|WNS 授權錯誤 (無效認證)|Count|總計|推播通知失敗，因為 hello PNS 並未接受 hello 提供封鎖或認證 hello hello 計數。 （Windows Live 無法辨識 hello 認證）。|
|outgoing.wns.badchannel|WNS 不正確的通道錯誤|Count|總計|hello 失敗，因為無法辨識 hello ChannelURI hello 註冊中的推播通知的計數 (WNS 狀態： 404 找不到)。|
|outgoing.wns.expiredchannel|WNS 過期通道錯誤|Count|總計|hello 失敗，因為 hello ChannelURI 已過期的推播通知的計數 (WNS 狀態： 410 已移走)。|
|outgoing.wns.throttled|WNS 節流通知|Count|總計|hello 失敗，因為 WNS 節流時設定此應用程式的推播通知的計數 (WNS 狀態： 406 無法接受)。|
|outgoing.wns.tokenproviderunreachable|WNS 授權錯誤 (無法連線)|Count|總計|無法連線到 Windows Live。|
|outgoing.wns.invalidtoken|WNS 授權錯誤 (無效權杖)|Count|總計|hello 提供語彙基元 tooWNS 無效 (WNS 狀態： 401 未經授權)。|
|outgoing.wns.wrongtoken|WNS 授權錯誤 (錯誤權杖)|Count|總計|hello 語彙基元提供 tooWNS 是否有效，但另一個應用程式 (WNS 狀態： 403 禁止)。 這可能會發生在 hello 登錄中的 hello ChannelURI 是否與另一個應用程式相關聯。 請檢查該 hello 用戶端應用程式是否 hello 與相關聯的認證都在 hello 通知中樞的同一個應用程式。|
|outgoing.wns.invalidnotificationformat|WNS 無效通知格式|Count|總計|hello 通知 hello 格式不正確 (WNS 狀態： 400)。 請注意，WNS 不會拒絕所有無效承載。|
|outgoing.wns.invalidnotificationsize|WNS 無效通知大小錯誤|Count|總計|hello 通知裝載會太大 (WNS 狀態： 413)。|
|outgoing.wns.channelthrottled|WNS 通道已節流處理|Count|總計|hello 通知已遭丟棄，因為已節流 hello 註冊中的 hello ChannelURI (WNS 回應標頭： X-WNS-NotificationStatus:channelThrottled)。|
|outgoing.wns.channeldisconnected|WNS 通道已中斷連線|Count|總計|hello 通知已遭丟棄，因為已節流 hello 註冊中的 hello ChannelURI (WNS 回應標頭： X-WNS-DeviceConnectionStatus： 中斷連接)。|
|outgoing.wns.dropped|WNS 已捨棄通知|Count|總計|hello 通知已遭丟棄，因為已節流 hello ChannelURI hello 註冊中的 (X-WNS-NotificationStatus： 已卸除，但不是 X-WNS-DeviceConnectionStatus： 中斷連接)。|
|outgoing.wns.pnserror|WNS 錯誤|Count|總計|因為與 WNS 通訊錯誤而未傳遞通知。|
|outgoing.wns.authenticationerror|WNS 驗證錯誤|Count|總計|因為與 Windows Live 通訊錯誤、無效認證或不正確的權杖，導致未傳遞通知。|
|outgoing.apns.success|APNS 成功通知|Count|總計|hello 所有成功通知數目。|
|outgoing.apns.invalidcredentials|APNS 授權錯誤|Count|總計|推播通知失敗，因為 hello PNS 並未接受 hello 提供封鎖或認證 hello hello 計數。|
|outgoing.apns.badchannel|APNS 不正確的通道錯誤|Count|總計|hello 計數失敗，因為 hello 語彙基元不正確的推播通知 (APNS 狀態碼： 8)。|
|outgoing.apns.expiredchannel|APNS 過期通道錯誤|Count|總計|hello 計數失效 hello APNS 回饋通道語彙基元。|
|outgoing.apns.invalidnotificationsize|APNS 無效通知大小錯誤|Count|總計|hello 計數失敗，因為 hello 承載太大的推播通知 (APNS 狀態碼： 7)。|
|outgoing.apns.pnserror|APNS 錯誤|Count|總計|hello 計數的推播通知，因為與 APNS 通訊錯誤而失敗。|
|outgoing.gcm.success|GCM 成功通知|Count|總計|hello 所有成功通知數目。|
|outgoing.gcm.invalidcredentials|GCM 授權錯誤 (無效認證)|Count|總計|推播通知失敗，因為 hello PNS 並未接受 hello 提供封鎖或認證 hello hello 計數。|
|outgoing.gcm.badchannel|GCM 不正確的通道錯誤|Count|總計|hello 失敗，因為無法辨識 hello registrationId hello 註冊中的推播通知的計數 (GCM 結果： 無效的登錄)。|
|outgoing.gcm.expiredchannel|GCM 過期通道錯誤|Count|總計|hello 失敗，因為在 hello 登錄中的 hello registrationId 已過期的推播通知的計數 (GCM 結果： NotRegistered)。|
|outgoing.gcm.throttled|GCM 已將通知節流處理|Count|總計|hello 失敗，因為 GCM 節流此應用程式的推播通知的計數 (GCM 狀態碼： 501-599 或結果： 無法使用)。|
|outgoing.gcm.invalidnotificationformat|GCM 無效通知格式|Count|總計|hello 失敗，因為 hello 承載格式不正確的推播通知的計數 (GCM 結果： InvalidDataKey 或 InvalidTtl)。|
|outgoing.gcm.invalidnotificationsize|GCM 無效通知大小錯誤|Count|總計|hello 失敗，因為 hello 承載太大的推播通知的計數 (GCM 結果： MessageTooBig)。|
|outgoing.gcm.wrongchannel|GCM 不正確的通道錯誤|Count|總計|hello 計數失敗，因為在 hello 登錄中的 hello registrationId 的推播通知的相關聯 toohello 目前的應用程式 (GCM 結果： InvalidPackageName)。|
|outgoing.gcm.pnserror|GCM 錯誤|Count|總計|hello 計數的推播通知，因為與 GCM 通訊錯誤而失敗。|
|outgoing.gcm.authenticationerror|GCM 驗證錯誤|Count|總計|hello 失敗，因為 hello PNS 並未接受 hello 可讓您提供認證 hello 認證遭到封鎖或 hello SenderId 未正確設定 hello 應用程式中的推播通知的計數 (GCM 結果： MismatchedSenderId)。|
|outgoing.mpns.success|MPNS 成功通知|Count|總計|hello 所有成功通知數目。|
|outgoing.mpns.invalidcredentials|MPNS 無效認證|Count|總計|推播通知失敗，因為 hello PNS 並未接受 hello 提供封鎖或認證 hello hello 計數。|
|outgoing.mpns.badchannel|MPNS 不正確的通道錯誤|Count|總計|hello 失敗，因為無法辨識 hello ChannelURI hello 註冊中的推播通知的計數 (MPNS 狀態： 404 找不到)。|
|outgoing.mpns.throttled|MPNS 已將通知節流處理|Count|總計|hello 失敗，因為此應用程式調整流速 MPNS 的推播通知的計數 (WNS MPNS: 406 無法接受)。|
|outgoing.mpns.invalidnotificationformat|MPNS 無效通知格式|Count|總計|推播通知失敗，因為 hello hello 通知裝載過大的 hello 計數。|
|outgoing.mpns.channeldisconnected|MPNS 通道已中斷連線|Count|總計|hello 失敗，因為在 hello 登錄中的 hello ChannelURI 已中斷連線的推播通知的計數 (MPNS 狀態： 412 找不到)。|
|outgoing.mpns.dropped|MPNS 已捨棄通知|Count|總計|hello 丟棄 mpns 的推播通知的計數 (MPNS 回應標頭： X NotificationStatus: QueueFull 或 Suppressed)。|
|outgoing.mpns.pnserror|MPNS 錯誤|Count|總計|hello 計數的推播通知，因為與 MPNS 通訊錯誤而失敗。|
|outgoing.mpns.authenticationerror|MPNS 驗證錯誤|Count|總計|推播通知失敗，因為 hello PNS 並未接受 hello 提供封鎖或認證 hello hello 計數。|
|notificationhub.pushes|所有外寄通知|Count|總計|Hello 通知中樞的所有外寄通知|
|incoming.all.requests|所有傳入要求|Count|總計|針對通知中樞傳入的要求總數|
|incoming.all.failedrequests|所有傳入的失敗要求|Count|總計|針對通知中樞傳入的失敗要求總數|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|度量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|qpu_metric|QPU|Count|平均值|QPU。 範圍 0-100 (S1)、0-200 (S2) 和 0-400 (S4)|
|memory_metric|記憶體|位元組|平均值|記憶體。 範圍 0-25 GB (S1)、0-50 GB (S2) 和 0-100 GB (S4)|
|TotalConnectionRequests|連線要求的總計|Count|平均值|連線要求的總計。 這些是達到的。|
|SuccessfullConnectionsPerSec|每秒連線成功的次數|每秒計數|平均值|成功完成連線的速率。|
|TotalConnectionFailures|連線失敗的總計|Count|平均值|連線嘗試失敗的總計。|
|CurrentUserSessions|目前的使用者工作階段|Count|平均值|目前建立的使用者工作階段數目。|
|QueryPoolBusyThreads|查詢集區忙碌執行緒|Count|平均值|Hello 查詢執行緒集區中的忙碌執行緒數目。|
|CommandPoolJobQueueLength|命令集區作業佇列長度|Count|平均值|Hello hello 命令執行緒集區佇列中的作業數目。|
|ProcessingPoolJobQueueLength|處理集區作業佇列長度|Count|平均值|Hello hello 處理執行緒集區佇列中的非 i/o 作業數目。|
|CurrentConnections|連接：目前的連接|Count|平均值|目前已建立的用戶端連接數目。|
|CleanerCurrentPrice|記憶體︰清除工具目前價格|Count|平均值|目前的記憶體，$/ 位元組/時間、 標準化的 too1000 價格。|
|CleanerMemoryShrinkable|記憶體︰可壓縮的清除器記憶體|位元組|平均值|記憶體數量，以位元組為單位，主旨 toopurging hello 背景清除器造成的。|
|CleanerMemoryNonshrinkable|記憶體︰不可壓縮的清除器記憶體|位元組|平均值|記憶體數量，以位元組為單位，不主旨 toopurging hello 背景清除器造成的。|
|MemoryUsage|記憶體：記憶體使用量|位元組|平均值|Hello 伺服器處理序用於計算清除器記憶體價格的記憶體使用量。 等於 toocounter Process\PrivateBytes 加上 hello 的記憶體對應資料大小，忽略對應或 hello xVelocity 記憶體中分析引擎 (VertiPaq) hello xVelocity 引擎記憶體限制超過配置任何記憶體。|
|MemoryLimitHard|記憶體︰固定記憶體限制|位元組|平均值|組態檔中的固定記憶體限制。|
|MemoryLimitHigh|記憶體︰記憶體上限|位元組|平均值|來自組態檔的記憶體上限。|
|MemoryLimitLow|記憶體︰記憶體下限|位元組|平均值|來自組態檔的記憶體下限。|
|MemoryLimitVertiPaq|記憶體︰記憶體限制 VertiPaq|位元組|平均值|來自組態檔的記憶體內部限制。|
|Quota|記憶體︰配額|位元組|平均值|目前的記憶體配額，以位元組為單位。 記憶體配額也就是指授與使用的記憶體，或是保留的記憶體。|
|QuotaBlocked|記憶體︰封鎖的配額|Count|平均值|在釋放其他記憶體配額之前，目前已封鎖的配額要求數目。|
|VertiPaqNonpaged|記憶體︰未分頁的 VertiPaq|位元組|平均值|Hello 記憶體中引擎 hello 工作集，用於鎖定的記憶體位元組數。|
|VertiPaqPaged|記憶體︰分頁的 VertiPaq|位元組|平均值|可供記憶體內部資料使用的分頁記憶體位元組。|
|RowsReadPerSec|處理︰每秒讀取的資料列|每秒計數|平均值|從所有關聯式資料庫讀取資料列的速率。|
|RowsConvertedPerSec|處理︰每秒轉換的資料列|每秒計數|平均值|處理期間資料列轉換的速率。|
|RowsWrittenPerSec|處理︰每秒寫入的資料列|每秒計數|平均值|處理期間資料列寫入的速率。|
|CommandPoolBusyThreads|執行緒︰命令集區的忙碌執行緒數|Count|平均值|Hello 命令執行緒集區中的忙碌執行緒數目。|
|CommandPoolIdleThreads|執行緒︰命令集區的閒置執行緒數|Count|平均值|Hello 命令執行緒集區中的閒置執行緒數目。|
|LongParsingBusyThreads|執行緒︰完整剖析的忙碌執行緒數|Count|平均值|Hello 完整剖析執行緒集區中的忙碌執行緒數目。|
|LongParsingIdleThreads|執行緒︰完整剖析的閒置執行緒數|Count|平均值|Hello 完整剖析執行緒集區中的閒置執行緒數目。|
|LongParsingJobQueueLength|執行緒︰完整剖析的作業佇列長度|Count|平均值|Hello hello 完整剖析執行緒集區佇列中的作業數目。|
|ProcessingPoolBusyIOJobThreads|執行緒︰處理集區的忙碌 I/O 作業執行緒數|Count|平均值|Hello 處理執行緒集區中執行 I/O 作業的執行緒數目。|
|ProcessingPoolBusyNonIOThreads|執行緒︰處理集區的忙碌非 I/O 執行緒數|Count|平均值|Hello 處理執行緒集區中執行非 i/o 作業的執行緒數目。|
|ProcessingPoolIOJobQueueLength|執行緒：處理集區 I/O 作業佇列長度|Count|平均值|Hello hello 處理執行緒集區佇列中的 I/O 作業數目。|
|ProcessingPoolIdleIOJobThreads|執行緒︰處理集區的閒置 I/O 作業執行緒數|Count|平均值|Hello 處理執行緒集區中 I/O 作業的閒置執行緒數目。|
|ProcessingPoolIdleNonIOThreads|執行緒︰處理集區的閒置非 I/O 執行緒數|Count|平均值|Hello 處理執行緒集區中的閒置執行緒數目的專用 toonon i/o 作業。|
|QueryPoolIdleThreads|執行緒︰查詢集區的閒置執行緒數|Count|平均值|Hello 處理執行緒集區中 I/O 作業的閒置執行緒數目。|
|QueryPoolJobQueueLength|執行緒︰查詢集區的作業佇列長度|Count|平均值|Hello hello 查詢執行緒集區佇列中的作業數目。|
|ShortParsingBusyThreads|執行緒︰簡短剖析的忙碌執行緒數|Count|平均值|Hello 簡短剖析執行緒集區中的忙碌執行緒數目。|
|ShortParsingIdleThreads|執行緒︰簡短剖析的閒置執行緒數|Count|平均值|Hello 簡短剖析執行緒集區中的閒置執行緒數目。|
|ShortParsingJobQueueLength|執行緒︰簡短剖析的作業佇列長度|Count|平均值|Hello hello 簡短剖析執行緒集區佇列中的作業數目。|
|memory_thrashing_metric|記憶體猛移|百分比|平均值|記憶體猛移的平均值。|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|SearchLatency|搜尋延遲|秒|平均值|平均搜尋延遲 hello 搜尋服務|
|SearchQueriesPerSecond|每秒搜尋查詢|每秒計數|平均值|每秒的 hello 搜尋服務的搜尋查詢|
|ThrottledSearchQueriesPercentage|節流的搜尋查詢百分比|百分比|平均值|搜尋查詢，hello 搜尋服務已節流的百分比|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|CPUXNS|每個命名空間的 CPU 使用量|百分比|最大值|服務匯流排進階命名空間 CPU 使用量計量|
|WSXNS|每個命名空間的記憶體大小使用量|百分比|最大值|服務匯流排進階命名空間記憶體使用量計量|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|cpu_percent|CPU 百分比|百分比|平均值|CPU 百分比|
|physical_data_read_percent|資料 IO 百分比|百分比|平均值|資料 IO 百分比|
|log_write_percent|記錄 IO 百分比|百分比|平均值|記錄 IO 百分比|
|dtu_consumption_percent|DTU 百分比|百分比|平均值|DTU 百分比|
|storage|資料庫大小總計|位元組|最大值|資料庫大小總計|
|connection_successful|成功的連線|Count|總計|成功的連線|
|connection_failed|失敗的連線|Count|總計|失敗的連線|
|blocked_by_firewall|遭到防火牆封鎖|Count|總計|遭到防火牆封鎖|
|deadlock|死結|Count|總計|死結|
|storage_percent|資料庫大小百分比|百分比|最大值|資料庫大小百分比|
|xtp_storage_percent|記憶體內部 OLTP 儲存體百分比|百分比|平均值|記憶體內部 OLTP 儲存體百分比|
|workers_percent|背景工作角色百分比|百分比|平均值|背景工作角色百分比|
|sessions_percent|工作階段百分比|百分比|平均值|工作階段百分比|
|dtu_limit|DTU 限制|Count|平均值|DTU 限制|
|dtu_used|已使用 DTU|Count|平均值|已使用 DTU|
|dwu_limit|DWU 限制|Count|最大值|DWU 限制|
|dwu_consumption_percent|DWU 百分比|百分比|最大值|DWU 百分比|
|dwu_used|已使用 DWU|Count|最大值|已使用 DWU|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|cpu_percent|CPU 百分比|百分比|平均值|CPU 百分比|
|database_cpu_percent|CPU 百分比|百分比|平均值|CPU 百分比|
|physical_data_read_percent|資料 IO 百分比|百分比|平均值|資料 IO 百分比|
|database_physical_data_read_percent|資料 IO 百分比|百分比|平均值|資料 IO 百分比|
|log_write_percent|記錄 IO 百分比|百分比|平均值|記錄 IO 百分比|
|database_log_write_percent|記錄 IO 百分比|百分比|平均值|記錄 IO 百分比|
|dtu_consumption_percent|DTU 百分比|百分比|平均值|DTU 百分比|
|database_dtu_consumption_percent|DTU 百分比|百分比|平均值|DTU 百分比|
|storage_percent|儲存體百分比|百分比|平均值|儲存體百分比|
|workers_percent|背景工作角色百分比|百分比|平均值|背景工作角色百分比|
|database_workers_percent|背景工作角色百分比|百分比|平均值|背景工作角色百分比|
|sessions_percent|工作階段百分比|百分比|平均值|工作階段百分比|
|database_sessions_percent|工作階段百分比|百分比|平均值|工作階段百分比|
|eDTU_limit|eDTU 限制|Count|平均值|eDTU 限制|
|storage_limit|儲存體限制|位元組|平均值|儲存體限制|
|eDTU_used|已使用 eDTU|Count|平均值|已使用 eDTU|
|storage_used|已使用儲存體|位元組|平均值|已使用儲存體|
|database_storage_used|已使用儲存體|位元組|平均值|已使用儲存體|
|xtp_storage_percent|記憶體內部 OLTP 儲存體百分比|百分比|平均值|記憶體內部 OLTP 儲存體百分比|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|dtu_consumption_percent|DTU 百分比|百分比|平均值|DTU 百分比|
|database_dtu_consumption_percent|DTU 百分比|百分比|平均值|DTU 百分比|
|storage_used|已使用儲存體|位元組|平均值|已使用儲存體|
|database_storage_used|已使用儲存體|位元組|平均值|已使用儲存體|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|ResourceUtilization|SU % 使用率|百分比|最大值|SU % 使用率|
|InputEvents|輸入事件|Count|總計|輸入事件|
|InputEventBytes|輸入事件位元組|位元組|總計|輸入事件位元組|
|LateInputEvents|延遲輸入事件|Count|總計|延遲輸入事件|
|OutputEvents|輸出事件|Count|總計|輸出事件|
|ConversionErrors|資料轉換錯誤|Count|總計|資料轉換錯誤|
|Errors|執行階段錯誤|Count|總計|執行階段錯誤|
|DroppedOrAdjustedEvents|次序錯誤事件|Count|總計|次序錯誤事件|
|AMLCalloutRequests|函式要求|Count|總計|函式要求|
|AMLCalloutFailedRequests|失敗的函式要求|Count|總計|失敗的函式要求|
|AMLCalloutInputEvents|函式事件|Count|總計|函式事件|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|CpuPercentage|CPU 百分比|百分比|平均值|CPU 百分比|
|MemoryPercentage|記憶體百分比|百分比|平均值|記憶體百分比|
|DiskQueueLength|磁碟佇列長度|Count|總計|磁碟佇列長度|
|HttpQueueLength|Http 佇列長度|Count|總計|Http 佇列長度|
|BytesReceived|資料輸入|位元組|總計|資料輸入|
|BytesSent|資料輸出|位元組|總計|資料輸出|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (不包括函式)

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|CpuTime|CPU 時間|秒|總計|CPU 時間|
|Requests|Requests|Count|總計|Requests|
|BytesReceived|資料輸入|位元組|總計|資料輸入|
|BytesSent|資料輸出|位元組|總計|資料輸出|
|Http101|Http 101|Count|總計|Http 101|
|Http2xx|Http 2xx|Count|總計|Http 2xx|
|Http3xx|Http 3xx|Count|總計|Http 3xx|
|Http401|Http 401|Count|總計|Http 401|
|Http403|Http 403|Count|總計|Http 403|
|Http404|Http 404|Count|總計|Http 404|
|Http406|Http 406|Count|總計|Http 406|
|Http4xx|Http 4xx|Count|總計|Http 4xx|
|Http5xx|Http 伺服器錯誤|Count|總計|Http 伺服器錯誤|
|MemoryWorkingSet|記憶體工作集|位元組|平均值|記憶體工作集|
|AverageMemoryWorkingSet|平均記憶體工作集|位元組|平均值|平均記憶體工作集|
|AverageResponseTime|平均回應時間|秒|平均值|平均回應時間|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (函式)

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|BytesReceived|資料輸入|位元組|總計|資料輸入|
|BytesSent|資料輸出|位元組|總計|資料輸出|
|Http5xx|Http 伺服器錯誤|Count|總計|Http 伺服器錯誤|
|MemoryWorkingSet|記憶體工作集|位元組|平均值|記憶體工作集|
|AverageMemoryWorkingSet|平均記憶體工作集|位元組|平均值|平均記憶體工作集|
|FunctionExecutionUnits|函式執行單位|Count|平均值|函式執行單位|
|FunctionExecutionCount|函式執行計數|Count|平均值|函式執行計數|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|計量|計量顯示名稱|單位|彙總類型|說明|
|---|---|---|---|---|
|CpuTime|CPU 時間|秒|總計|CPU 時間|
|Requests|Requests|Count|總計|Requests|
|BytesReceived|資料輸入|位元組|總計|資料輸入|
|BytesSent|資料輸出|位元組|總計|資料輸出|
|Http101|Http 101|Count|總計|Http 101|
|Http2xx|Http 2xx|Count|總計|Http 2xx|
|Http3xx|Http 3xx|Count|總計|Http 3xx|
|Http401|Http 401|Count|總計|Http 401|
|Http403|Http 403|Count|總計|Http 403|
|Http404|Http 404|Count|總計|Http 404|
|Http406|Http 406|Count|總計|Http 406|
|Http4xx|Http 4xx|Count|總計|Http 4xx|
|Http5xx|Http 伺服器錯誤|Count|總計|Http 伺服器錯誤|
|MemoryWorkingSet|記憶體工作集|位元組|平均值|記憶體工作集|
|AverageMemoryWorkingSet|平均記憶體工作集|位元組|平均值|平均記憶體工作集|
|AverageResponseTime|平均回應時間|秒|平均值|平均回應時間|
|FunctionExecutionUnits|函式執行單位|Count|平均值|函式執行單位|
|FunctionExecutionCount|函式執行計數|Count|平均值|函式執行計數|

## <a name="next-steps"></a>後續步驟
* [了解 Azure 監視器中的計量](monitoring-overview-metrics.md)
* [建立計量警示](insights-receive-alert-notifications.md)
* [匯出度量 toostorage、 事件中心或記錄分析](monitoring-overview-of-diagnostic-logs.md)
