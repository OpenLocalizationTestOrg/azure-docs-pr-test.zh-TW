---
title: "Azure SQL Database 基準測試概觀"
description: "本主題說明用來測量 Azure SQL Database 效能的 Azure SQL Database 基準測試。"
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: On Demand
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: fb8a5f205ddc143dc47349829048f46f88963d05
ms.sourcegitcommit: 6a6e14fdd9388333d3ededc02b1fb2fb3f8d56e5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Azure SQL Database 基準測試概觀
## <a name="overview"></a>概觀
Microsoft Azure SQL Database 提供三個 [服務層](sql-database-service-tiers.md) 以及多個效能等級。 每個效能等級都提供越來越多的資源集或「能力」，旨在提供愈來愈高的輸送量。

每個效能等級的增加能力會轉譯成提高的資料庫效能，請務必將其量化。 為了執行此作業，Microsoft 開發了 Azure SQL Database 基準測試 (ASDB)。 基準測試會執行所有 OLTP 工作負載中找到的基本作業的混合。 我們會測量在每個效能等級中執行之資料庫所獲得的輸送量。

每個服務層和效能等級的資源與能力都會以[資料庫交易單位 (DTU)](sql-database-what-is-a-dtu.md) 的形式表示。 DTU 會根據每個效能等級所提供的 CPU、記憶體，以及讀寫率的混合量值，提供一個方式來描述相關的效能等級容量。 資料庫的 DTU 評等加倍等同於資料庫能力倍增。 基準測試可讓我們評估每個效能等級藉由執行實際資料庫作業，同時根據提供給資料庫的資源比例來調整資料庫大小、使用者數目以及交易速率，所提供之增加能力對資料庫效能產生的影響。

藉由表示使用每小時交易的基本服務層、使用每分鐘交易的標準服務層以及使用每秒鐘交易的高階服務層等輸送量，可以更容易地快速建立每個服務層之效能潛力與應用程式需求之間的關聯。

## <a name="correlating-benchmark-results-to-real-world-database-performance"></a>建立基準測試結果與實際案例資料庫效能之間的關聯
請務必了解 ASDB 和所有基準測試一樣，都只具備代表性與指標性。 利用基準測試應用程式達成的交易速率與利用其他應用程式可能達成的交易速率不同。 基準測試是由不同的交易類型集合所組成，這些類型是針對包含某個範圍的資料表和資料類型的結構描述來執行。 雖然基準測試會執行所有 OLTP 工作負載常見的相同基本作業，但是它不代表任何特定類別的資料庫或應用程式。 基準測試的目標是提供資料庫相對效能的合理指南，在效能等級之間向上或向下調整時可預期此目標。 實際上，資料庫的大小和複雜度都不一樣，會遭遇到不同的工作負載混合，並以不同的方式回應。 例如，IO 密集的應用程式可能會更快達到 IO 臨界值，或者 CPU 密集應用程式可能會更快達到 CPU 限制。 任何特定的資料庫並不保證能夠在增加負載的情況下使用和基準測試相同的方式調整。

基準測試和其方法會在以下詳細描述。

## <a name="benchmark-summary"></a>基準測試摘要
ASDB 可測量基本資料庫作業混合的效能，這些作業最常發生在線上交易處理 (OLTP) 工作負載中。 雖然基準測試在設計時考量到雲端運算，但是資料庫結構描述、資料母體和交易的設計都廣泛代表 OLTP 工作負載中最常使用的基本元素。

## <a name="schema"></a>結構描述
結構描述的設計具有足夠的多樣性和複雜性才能支援廣泛的作業。 對包含六個資料表的資料庫執行基準測試。 資料表分成三個類別：固定大小、調整和成長。 有兩個固定大小資料表、三個調整資料表，和一個成長資料表。 固定大小資料表有固定數目的資料列。 調整資料表有與資料庫效能成正比但不會在基準測試期間變更的基數。 成長資料表的大小在初始載入時類似調整資料表，但是在執行基準測試做為資料列的過程中，會插入並刪除基數變更。

結構描述包含資料類型的混合，包括整數、數值、字元和日期/時間。 結構描述包含主要和次要索引鍵，但不含任何外部索引鍵 - 也就是資料表之間沒有參考完整性條件約束。

資料產生程式會產生初始資料庫的資料。 運用各種策略產生整數和數值資料。 在某些情況下，會在某範圍中隨機分佈值。 在其他情況下，會隨機排列一組值以確保維護特定的分佈。 從文字的加權清單產生文字欄位以產生實際的查看資料。

資料庫的大小是根據「縮放比例」來設定。 縮放比例 (簡寫為 SF) 可決定調整和成長資料表的基數。 如以下的＜使用者與步調＞一節所述，資料庫大小、使用者數目和最大效能都會根據彼此的比例進行調整。

## <a name="transactions"></a>交易
工作負載包含九種交易類型，如下表所示。 每一筆交易都設計為反白顯示資料庫引擎和系統硬體中特定的一組系統特性，與其他交易呈現高度對比。 此方法可讓您更容易評估不同元件對整體效能的影響。 例如，「頻繁讀取」交易會從磁碟產生大量的讀取作業。

| 交易類型 | 說明 |
| --- | --- |
| 輕度讀取 |SELECT；記憶體中；唯讀 |
| 中度讀取 |SELECT；大部分記憶體中；唯讀 |
| 重度讀取 |SELECT；大部分非記憶體中；唯讀 |
| 輕度更新 |UPDATE；記憶體中；讀寫 |
| 重度更新 |UPDATE；大部分非記憶體中；讀寫 |
| 輕度插入 |INSERT；記憶體中；讀寫 |
| 重度插入 |INSERT；大部分非記憶體中；讀寫 |
| 刪除 |DELETE；記憶體中與非記憶體中的混合；讀寫 |
| 重度 CPU |SELECT；記憶體中；非常重度的 CPU 負載；唯讀 |

## <a name="workload-mix"></a>工作負載混合
利用下列整體混合從加權分佈中隨機選取交易。 整體混合具有大約 2:1 的讀/寫比率。

| 交易類型 | 混合 % |
| --- | --- |
| 輕度讀取 |35 |
| 中度讀取 |20 |
| 重度讀取 |5 |
| 輕度更新 |20 |
| 重度更新 |3 |
| 輕度插入 |3 |
| 重度插入 |2 |
| 刪除 |2 |
| 重度 CPU |10 |

## <a name="users-and-pacing"></a>使用者與步調
基準測試工作負載是由一個工具觸發，它會跨一組連接提交交易，以模擬許多並行使用者的行為。 雖然所有的連接和交易都是由電腦產生，為了簡單起見，我們將這些連接視為「使用者」。 雖然每一位使用者都獨立於其他所有使用者操作，但是所有使用者都執行相同的步驟循環，如下所示：

1. 建立資料庫連接。
2. 發出結束訊號之前請重複：
   * 隨機選取交易 (從加權分佈中)。
   * 執行選取的交易及測量回應時間。
   * 等候步調延遲。
3. 關閉資料庫連接。
4. [結束]。

步調延遲 (在步驟 2c) 為隨機選取，但其分佈具有 1.0 秒的平均值。 因此每位使用者平均每秒可以產生最多一筆交易。

## <a name="scaling-rules"></a>調整規則
使用者數目取決於資料庫大小 (以縮放比例單位表示)。 每五個縮放比例單位有一名使用者。 由於步調延遲，一位使用者平均每秒可以產生最多一筆交易。

例如，縮放比例為 500 (SF = 500) 的資料庫會有 100 位使用者，並可達到最大速率 100 TPS。 若要觸發更高的 TPS 速率，需要更多使用者和更大的資料庫。

下表顯示為每個服務層和效能等級實際持續保留的使用者數目。

| 服務層 (效能等級) | 使用者 | 資料庫大小 |
| --- | --- | --- |
| 基本 |5 |720 MB |
| 標準 (S0) |10 |1 GB |
| 標準 (S1) |20 |2.1 GB |
| 標準 (S2) |50 |7.1 GB |
| 高階 (P1) |100 |14 GB |
| 高階 (P2) |200 |28 GB |
| 高階 (P6) |800 |114 GB |

## <a name="measurement-duration"></a>測量持續時間
有效的基準測試執行需要至少一個小時的穩定狀態測量持續時間。

## <a name="metrics"></a>度量
基準測試中的關鍵度量是輸送量和回應時間。

* 輸送量是基準測試中的基礎效能測量。 每個單位時間都會在交易中報告輸送量，計算所有交易類型。
* 回應時間是效能可預測性的測量。 回應時間條件約束會隨服務類別而有所不同，較高等級的服務類別有更嚴格的回應時間需求，如下所示。

| 服務類別 | 輸送量測量 | 回應時間需求 |
| --- | --- | --- |
| 高級 |每秒交易 |0.5 秒時第 95 個百分位數 |
| 標準 |每分鐘交易 |1.0 秒時第 90 個百分位數 |
| 基本 |每小時交易 |2.0 秒時第 80 個百分位數 |

## <a name="conclusion"></a>結論
Azure SQL Database 基準測試會測量跨某範圍可用服務層和效能等級執行之 Azure SQL Database 的相對效能。 基準測試會執行基本資料庫作業的混合，這些作業最常發生在線上交易處理 (OLTP) 工作負載中。 藉由測量實際效能，基準測試會提供變更效能等級對輸送量的影響評估，比僅列出每個等級所提供的 CPU 速度、記憶體大小和 IOPS 等資源更有意義。 在未來，我們將持續改良基準測試，以擴大其範圍及擴展提供的資料。

## <a name="resources"></a>資源
[SQL Database 簡介](sql-database-technical-overview.md)

[服務層和效能層級](sql-database-service-tiers.md)

[單一資料庫的效能指引](sql-database-performance-guidance.md)