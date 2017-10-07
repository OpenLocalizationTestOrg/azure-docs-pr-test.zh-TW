---
title: "aaaAzure SQL Database 基準測試概觀"
description: "本主題描述 hello Azure SQL Database Benchmark 用於測量 hello Azure SQL database 的效能。"
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
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Azure SQL Database 基準測試概觀
## <a name="overview"></a>概觀
Microsoft Azure SQL Database 提供三個 [服務層](sql-database-service-tiers.md) 以及多個效能等級。 每個效能層級提供遞增是設計的資源，或 'power' 組 toodeliver 逐漸較高的輸送量。

很重要的 toobe 無法 tooquantify hello 增加每個效能層級的能力會將轉譯成提高的資料庫效能。 此 Microsoft 開發了的 toodo hello Azure SQL Database Benchmark (ASDB)。 hello 基準測試會執行所有 OLTP 工作負載中找到的基本作業的混合。 我們會測量每個效能層級中執行的資料庫所獲得的 hello 輸送量。

hello 資源與電源的每個服務層和效能層級會表示的[資料庫交易單位 (Dtu)](sql-database-what-is-a-dtu.md)。 Dtu 可用 toodescribe hello 相對容量的效能層級為基礎的混合測量結果的 CPU、 記憶體與讀取和寫入每個效能層級所提供的費率。 加倍 hello 資料庫 DTU 評等等同 toodoubling hello 資料庫電源。 hello 基準測試可讓我們 tooassess hello 影響對資料庫效能的 hello 增加每個效能層級藉以實際資料庫作業，而比例調整資料庫大小、 使用者和交易率的能力toohello toohello 提供資源的資料庫。

所表示的 hello Basic 服務層使用交易每小時的 hello 輸送量，hello Standard 服務層使用交易每分鐘，並使用交易每秒，它可讓您更輕鬆 tooquickly hello Premium 服務層與 hello效能可能造成應用程式的每個服務層 toohello 需求。

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>相互關聯的基準測試結果 tooreal 世界資料庫效能
重要 toounderstand 該 ASDB，如所有基準測試，只是具有參考價值。 hello 達成與 hello 基準測試應用程式的速度將會是 hello 相同，可能會與其他應用程式達成這些不交易。 hello 基準測試包含類型執行包含的資料表和資料類型範圍的結構描述的不同交易的集合。 雖然 hello 基準練習 hello 常見 tooall OLTP 工作負載的相同基本作業，它不代表任何特定類別的資料庫或應用程式。 hello 基準 hello 目標是 tooprovide 可能效能層級之間預期時擴增或縮減資料庫合理指南 toohello 相對效能。 實際上，資料庫的大小和複雜度都不一樣，會遭遇到不同的工作負載混合，並以不同的方式回應。 例如，IO 密集的應用程式可能會更快達到 IO 臨界值，或者 CPU 密集應用程式可能會更快達到 CPU 限制。 沒有任何特定的資料庫會調整的相同方式為下增加 hello 基準載入的 hello 保證。

hello 基準測試和其方法詳述於以下更詳細。

## <a name="benchmark-summary"></a>基準測試摘要
ASDB 可測量線上交易處理 (OLTP) 工作負載中最常發生的基本資料庫作業的混合 hello 效能。 設計雲端運算記住 hello 基準測試，雖然 hello 資料庫結構描述、 資料母體和交易已設計的 toobe 廣泛代表 OLTP 工作負載中最常用的 hello 基本項目。

## <a name="schema"></a>結構描述
hello 結構描述是設計的 toohave 足夠的多樣性和複雜性 toosupport 廣泛的作業。 包含六個資料表的資料庫來執行 hello 基準測試。 hello 資料表分成三個類別： 固定大小、 調整和成長。 有兩個固定大小資料表、三個調整資料表，和一個成長資料表。 固定大小資料表有固定數目的資料列。 調整資料表有比例 toodatabase 效能，但不會變更 hello 基準測試期間的基數。 hello 成長資料表的大小類似於調整資料表在初始載入，但 hello 基數然後在插入及刪除資料列時，執行 hello 基準測試中的 hello 過程中變更。

hello 結構描述包含混合資料類型，包括整數、 數值、 字元和日期/時間。 hello 結構描述包含主要和次要金鑰，但不是含任何外部索引鍵-也就是有沒有參考完整性條件約束的資料表之間。

資料產生程式會產生 hello hello 初始資料庫的資料。 運用各種策略產生整數和數值資料。 在某些情況下，會在某範圍中隨機分佈值。 在其他情況下，一組值會是隨機置換 tooensure，維持特定的分佈。 從字 tooproduce 真實的資料的粗細清單中產生文字欄位。

hello 的資料庫大小根據 「 調整係數 」。 hello 調整係數 （簡寫為 SF） 可決定 hello 的 hello 調整和成長中資料表的基數。 如下所述在 hello 區段使用者及步調，hello 資料庫大小、 使用者和所有縮放比例 tooeach 其他的效能達到最高的數字。

## <a name="transactions"></a>交易
hello 工作負載包含九種交易類型 hello 下表所示。 每個交易並設計的 toohighlight 特定的一組系統特性 hello 資料庫引擎和系統硬體中，從高對比與 hello 其他交易。 這種方法可讓您更輕鬆 tooassess hello 影響的不同元件 toooverall 效能。 例如，hello 交易 「 頻繁讀取 」 會產生大量的磁碟讀取作業。

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
交易中隨機選取從加權分佈 hello 下列整體混合使用。 hello 整體混合的讀/寫比率約為 2:1。

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
hello 基準測試工作負載是一種工具，提交交易在連接 toosimulate hello 行為的並行使用者數目的一組由工具驅動。 雖然 hello 連線和交易的所有機器產生，為了簡單起見都我們 toothese 連線稱為 「 使用者 」。 雖然每個使用者操作可與其他所有使用者不同，所有使用者都會都執行 hello 相同的循環的步驟如下所示：

1. 建立資料庫連接。
2. 重複此選項，直到收到信號 tooexit:
   * 隨機選取交易 (從加權分佈中)。
   * 執行選取的 hello 交易及測量 hello 回應時間。
   * 等候步調延遲。
3. 關閉 hello 資料庫連接。
4. [結束]。

hello 步調延遲 （步驟 2c） 隨機選取的但具有 1.0 秒平均分配。 因此每位使用者平均每秒可以產生最多一筆交易。

## <a name="scaling-rules"></a>調整規則
使用者的 hello 數目取決於 hello 資料庫大小 （利用調整係數單元）。 每五個縮放比例單位有一名使用者。 Hello 步調延遲，因為一位使用者可以產生最多一交易每秒平均。

例如，縮放比例為 500 (SF = 500) 的資料庫會有 100 位使用者，並可達到最大速率 100 TPS。 toodrive 較高的 TPS 速率需要更多使用者和更大的資料庫。

hello 表顯示每個服務層和效能層級實際上持續存在的 hello 人數。

| 服務層 (效能等級) | 使用者 | 資料庫大小 |
| --- | --- | --- |
| 基本 |5 |720 MB |
| 標準 (S0) |10 |1 GB |
| 標準 (S1) |20 |2.1 GB |
| 標準 (S2) |50 |7.1 GB |
| 高階 (P1) |100 |14 GB |
| 高階 (P2) |200 |28 GB |
| 高階 (P6/P3) |800 |114 GB |

## <a name="measurement-duration"></a>測量持續時間
有效的基準測試執行需要至少一個小時的穩定狀態測量持續時間。

## <a name="metrics"></a>度量
hello hello 基準測試中的關鍵度量是輸送量和回應時間。

* 輸送量是 hello 基準測試中的 hello 基礎效能測量。 每個單位時間都會在交易中報告輸送量，計算所有交易類型。
* 回應時間是效能可預測性的測量。 hello 回應時間限制隨服務等級較高的服務類別有更嚴格的回應時間需求，如下所示的類別。

| 服務類別 | 輸送量測量 | 回應時間需求 |
| --- | --- | --- |
| 高級 |每秒交易 |0.5 秒時第 95 個百分位數 |
| 標準 |每分鐘交易 |1.0 秒時第 90 個百分位數 |
| 基本 |每小時交易 |2.0 秒時第 80 個百分位數 |

## <a name="conclusion"></a>結論
hello Azure SQL Database Benchmark 測量跨可用的服務層和效能層級 hello 範圍執行的 Azure SQL Database 的 hello 相對效能。 hello 基準測試執行線上交易處理 (OLTP) 工作負載中最常發生的基本資料庫作業的混合。 藉由測量實際效能，hello 基準測試會提供更有意義的評估 hello 影響輸送量的變更 hello 效能層級，而不是僅列出每個層級，例如 CPU 速度、 記憶體大小和 IOPS 所提供的 hello 資源. 在 hello 未來，我們將繼續 tooevolve hello 基準 toobroaden 其範圍，然後展開 hello 所提供的資料。

## <a name="resources"></a>資源
[簡介 tooSQL 資料庫](sql-database-technical-overview.md)

[服務層和效能層級](sql-database-service-tiers.md)

[單一資料庫的效能指引](sql-database-performance-guidance.md)
