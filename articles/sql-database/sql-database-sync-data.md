---
title: "aaaSync 資料 （預覽） |Microsoft 文件"
description: "本概觀介紹 Azure SQL 資料同步 (預覽)。"
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>使用 SQL 資料同步，跨多個雲端和內部部署資料庫同步資料

SQL 資料同步處理是可讓您選取雙向跨多個 SQL database 和 SQL Server 執行個體的 hello 資料同步處理您的 Azure SQL Database 上建置的服務。

資料同步會根據 hello 概念的同步處理群組。 同步處理群組是您想 toosynchronize 資料庫的群組。

同步處理群組具有下列屬性的 hello:

-   hello**同步處理結構描述**說明資料同步處理。

-   hello**同步處理方向**可以是雙向或可以只有一個方向流動。 也就是說，可以是同步處理方向的 hello*中樞 tooMember*或*成員 tooHub*，或兩者。

-   hello**同步處理間隔**頻率進行同步處理。

-   hello**衝突解決原則**是群組層級原則，可以是*中樞獲勝*或*成員 wins*。

資料同步會使用中樞和支點拓撲 toosynchronize 資料。 您定義的其中一個 hello 資料庫 hello 群組中為 hello 中樞資料庫。 hello hello 資料庫其餘部分是成員資料庫。 只有之間 hello 中樞和個別成員進行同步處理。
-   hello**中樞資料庫**必須是 Azure SQL Database。
-   hello**成員資料庫**可以是 SQL 資料庫、 在內部部署 SQL Server 資料庫或在 Azure 虛擬機器上的 SQL Server 執行個體。
-   hello**同步處理資料庫**包含 hello 中繼資料和記錄檔資料同步處理。 hello 同步處理資料庫有 toobe 位於 hello Azure SQL Database 與 hello 中樞資料庫相同的區域。 建立的客戶，而客戶擁有 hello 同步處理資料庫。

> [!NOTE]
> 如果您使用上的內部部署資料庫，您有太[設定本機代理程式。](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![資料庫之間的同步資料](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>當 toouse 資料同步處理

資料同步處理是在需要資料 toobe 維持 toodate 最新狀態跨數個 Azure SQL Database 或 SQL Server 資料庫的情況下很有用。 以下是資料同步的 hello 主要的使用案例：

-   **混合式資料同步處理：**資料同步時，您可以保留在內部部署資料庫和 Azure SQL Database tooenable 混合式應用程式之間的同步處理的資料。 這項功能可能會吸引人考慮移動 toohello 雲端，而且想要 tooput toocustomers 他們在 Azure 中的應用程式部分。

-   **分散式應用程式：**在許多情況下，很有幫助 tooseparate 不同工作負載分散在不同的資料庫。 例如，如果您有大型資料庫，但您也需要 toorun 報告或分析工作負載，此資料，很有幫助 toohave 此額外的工作負載的第二個資料庫。 這種方法 hello 對您的生產工作負載的效能影響降到最低。 您可以使用這兩個資料庫同步處理的資料同步 tookeep。

-   **全域散發的應用程式：**許多企業的業務橫跨多個區域，甚至多個國家/地區。 toominimize 網路延遲，它會關閉您的資料區域中的最佳 toohave tooyou。 資料同步時，您可以輕鬆地資料庫同步處理的 hello 世界各地的區域中。

我們不建議資料同步 hello 下列案例：

-   災害復原

-   讀取級別

-   ETL (OLTP tooOLAP)

-   從內部部署 SQL Server tooAzure SQL Database 移轉

## <a name="how-does-data-sync-work"></a>資料同步如何運作？ 

-   **追蹤資料變更：**資料同步使用 insert、update 和 delete 觸發程序追蹤變更。 hello 變更會記錄在側邊資料表 hello 使用者資料庫中。

-   **同步處理資料：**資料同步是以「中樞和輪輻」的模型設計。 個別 hello 與每個成員的中樞同步處理。 Hello 中樞的變更會下載的 toohello 成員，然後再從 hello 成員變更便會上載的 toohello 中樞。

-   **解決衝突：**資料同步提供兩個衝突解決選項：*中樞獲勝*或*成員獲勝*。
    -   如果您選取*中樞獲勝*，hello 中樞中的 hello 變更一律會覆寫 hello 成員中的變更。
    -   如果您選取*成員 wins*，hello hello 中樞中的 hello 成員覆寫變更的變更。 如果有多個成員，hello 最終值取決於哪一個成員是第一次同步。

## <a name="limitations-and-considerations"></a>限制與注意事項

### <a name="performance-impact"></a>效能影響
資料同步處理會使用插入、 更新和刪除觸發程序 tootrack 變更。 它會變更追蹤的 hello 使用者資料庫中建立的側邊資料表。 這些變更追蹤活動會影響您的資料庫工作負載。 請評估您的服務層，如有必要則請升級。

### <a name="eventual-consistency"></a>最終一致性
由於資料同步是以觸發程序為基礎，所以並不保證交易一致性。 Microsoft 保證最終會進行所有變更，而且資料同步不會造成資料遺失。

### <a name="unsupported-data-types"></a>不支援的資料類型

-   FileStream

-   SQL/CLR UDT

-   XMLSchemaCollection (支援 XML)

-   Cursor、Timestamp、Hierarchyid

### <a name="requirements"></a>需求

-   每個資料表都必須有主索引鍵。

-   資料表不能有不是 hello 主索引鍵的識別資料行。

-   hello 物件 （資料庫、 資料表和資料行） 名稱不能包含 hello 可列印字元句點 （.）、 左方括弧 ([])，或右方括弧 (])。

### <a name="limitations-on-service-and-database-dimensions"></a>服務和資料庫維度的限制

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **維度**                                                      | **限制**              | **因應措施**              |
| 任何資料庫可以隸屬的同步群組數目上限。       | 5                      |                             |
| 單一同步群組中的端點數目上限              | 30                     | 建立多個同步群組 |
| 單一同步群組中的內部部署端點數目上限。 | 5                      | 建立多個同步群組 |
| 資料庫名稱、資料表名稱、結構描述名稱和資料行名稱                       | 每個名稱 50 個字元 |                             |
| 一個同步群組中的資料表                                          | 500                    | 建立多個同步群組 |
| 一個同步群組中一個資料表中的資料行                              | 1000                   |                             |
| 一個資料表上的資料列大小                                        | 24 Mb                  |                             |
| 最小同步處理間隔                                           | 5 分鐘              |                             |

## <a name="common-questions"></a>常見問題

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>資料同步多久會同步我的資料一次？ 
hello 的最小頻率為每隔五分鐘。

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>可以使用 SQL Server 在內部部署資料庫只之間資料同步 toosync 嗎？ 
無法直接進行。 您可以同步處理 SQL Server 在內部部署資料庫之間間接，不過，在 Azure 中建立的中樞資料庫，然後將加入 hello 在內部部署資料庫 toohello 同步處理群組。
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>我可以使用資料同步 tooseed 資料從實際執行資料庫 tooan 空白資料庫，並再讓它們保持同步嗎？ 
是。 指令從原始的 hello hello 新資料庫中手動建立 hello 結構描述。 建立 hello 結構描述之後，加入 hello 資料表 tooa 同步處理群組 toocopy hello 資料，並保持同步。

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>為什麼我會看到並非自己建立的資料表？  
資料同步會在資料庫中建立側邊資料表，以便進行變更追蹤。 請勿刪除它們，否則資料同步無法正常運作。
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>我收到錯誤訊息: 「 無法將 NULL 值的 hello 插入 hello 資料行\<資料行\>。 資料行不允許 Null。」 這是什麼意思，以及如何修正 hello 錯誤？ 
這則錯誤訊息指出其中一個 hello 兩個下列問題：
1.  資料表缺少主索引鍵。 toofix 這個問題，請新增 hello 資料表的主索引鍵 tooall 正在同步處理。
2.  在 CREATE INDEX 陳述式中可能有 WHERE 子句。 同步無法處理這種狀況。 toofix 這個問題，請移除 hello WHERE 子句，或手動變更 hello tooall 資料庫。 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>資料同步如何處理循環參考？ 也就是當 hello 相同的資料已同步處理在多個同步處理群組，並持續變更的結果嗎？
資料同步不會處理循環參考。 要確定 tooavoid 它們。 

## <a name="next-steps"></a>後續步驟

如需 SQL 資料同步的詳細資訊，請參閱：

-   [開始使用 SQL 資料同步](sql-database-get-started-sql-data-sync.md)

-   完成 PowerShell 範例，說明如何 tooconfigure SQL 資料同步：
    -   [使用多個 Azure SQL database 之間的 PowerShell toosync](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [使用 Azure SQL Database 和 SQL Server 在內部部署資料庫之間的 PowerShell toosync](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [下載 hello 完整 SQL 資料同步技術文件](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [下載 SQL 資料同步處理的 REST API 文件以 hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

如需 SQL Database 的詳細資訊，請參閱：

-   [SQL Database 概觀](sql-database-technical-overview.md)

-   [資料庫生命週期管理](https://msdn.microsoft.com/library/jj907294.aspx)
