---
title: "Azure SQL 資料同步 (預覽) | Microsoft Docs"
description: "本概觀介紹 Azure SQL 資料同步 (預覽)"
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: On Demand
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: douglasl
ms.reviewer: douglasl
ms.openlocfilehash: 5cf74140969fb354e426c41552d4d73a06c76890
ms.sourcegitcommit: a036a565bca3e47187eefcaf3cc54e3b5af5b369
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync-preview"></a>使用 SQL 資料同步 (預覽) 跨多個雲端和內部部署資料庫同步資料

「SQL 資料同步」是一種建置在 Azure SQL Database 上的服務，可讓您跨多個 SQL 資料庫和 SQL Server 執行個體，雙向同步您選取的資料。

資料同步以「同步群組」的概念為基礎。 「同步群組」是您想要同步的資料庫群組。

同步群組具有下列屬性：

-   **同步結構描述**說明要同步的資料。

-   **同步處理方向**可以是雙向或只有單向。 也就是說，同步處理方向可以是*中樞到成員*或是*成員到中樞*，或兩者皆可。

-   **同步處理間隔**是進行同步處理的頻率。

-   **衝突解決原則**是群組層級原則，可以是*中樞獲勝*或*成員獲勝*。

資料同步使用中樞和輪輻拓撲來同步資料。 您可以將群組中的其中一個資料庫定義為「中樞資料庫」。 其餘的資料庫則是成員資料庫。 只有中樞和個別成員之間才會進行同步。
-   **中樞資料庫**必須是 Azure SQL Database。
-   **成員資料庫**可以是 SQL 資料庫、內部部署 SQL Server 資料庫，或是在 Azure 虛擬機器上的 SQL Server 執行個體。
-   **同步處理資料庫**包含「資料同步」的中繼資料和記錄。「同步處理資料庫」必須是與「中樞資料庫」位於相同區域的 Azure SQL Database。 「同步處理資料庫」是由客戶建立，並由客戶擁有。

> [!NOTE]
> 如果您使用內部部署資料庫，必須[設定本機代理程式](sql-database-get-started-sql-data-sync.md#add-on-prem)。

![資料庫之間的同步資料](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-to-use-data-sync"></a>使用資料同步的時機

如果您需要讓多個 Azure SQL Database 或 SQL Server 資料庫之間的資料保持在最新狀態，資料同步就很有用。 以下是資料同步主要的使用案例：

-   **混合式資料同步：**使用資料同步，您可以讓內部部署資料庫與 Azure SQL Database 之間的資料保持同步，以啟用混合式應用程式。 此功能對於考慮移轉至雲端，而且想要將部分應用程式放在 Azure 的客戶很有吸引力。

-   **分散式應用程式：**在許多情況下，將不同的工作負載分散到不同的資料庫會有好處。 例如，如果您有大型的實際執行資料庫，但也必須針對這些資料執行報告或分析工作負載，此時有第二個資料庫分擔這額外的工作負載就很有幫助。 這個方法可以減少對您實際執行工作負載的效能影響。 您可以使用「資料同步」，讓這兩個資料庫保持同步。

-   **全域散發的應用程式：**許多企業的業務橫跨多個區域，甚至多個國家/地區。 若要盡可能降低網路延遲，最好讓資料靠近您所在的區域。 使用資料同步，您就可以輕鬆地讓全世界各個區域中的資料庫保持同步。

資料同步不適用於下列案例：

-   災害復原

-   讀取級別

-   ETL (OLTP 到 OLAP)

-   從內部部署 SQL Server 移轉至 Azure SQL Database

## <a name="how-does-data-sync-work"></a>資料同步如何運作？ 

-   **追蹤資料變更：**資料同步使用 insert、update 和 delete 觸發程序追蹤變更。 變更會記錄在使用者資料庫中的資料表。

-   **同步處理資料：**資料同步是以「中樞和輪輻」的模型設計。 中樞會與每個成員個別同步。 中樞的變更會下載到成員，然後成員的變更會上傳到中樞。

-   **解決衝突：**資料同步提供兩個衝突解決選項：*中樞獲勝*或*成員獲勝*。
    -   如果您選取 [中樞獲勝]，中樞的變更永遠會覆寫成員的變更。
    -   如果您選取 [成員獲勝]，成員的變更永遠會覆寫中樞的變更。 如果有多個成員，最終的值則取決於哪一個成員先同步。

## <a name="sync-req-lim"></a> 需求和限制

### <a name="general-considerations"></a>一般考量

#### <a name="eventual-consistency"></a>最終一致性
由於資料同步是以觸發程序為基礎，所以並不保證交易一致性。 Microsoft 保證最終會進行所有變更，而且資料同步不會造成資料遺失。

#### <a name="performance-impact"></a>效能影響
資料同步使用 insert、update 和 delete 觸發程序追蹤變更。 其會在使用者資料庫中建立側邊資料表，以便進行變更追蹤。 這些變更追蹤活動會影響您的資料庫工作負載。 請評估您的服務層，如有必要則請升級。

### <a name="general-requirements"></a>一般需求

-   每個資料表都必須有主索引鍵。 請勿變更任何資料列的主索引鍵值。 如果您必須變更主索引鍵值，請刪除資料列，再利用新的主索引鍵值重新建立。 

-   必須啟用快照集隔離。 如需詳細資訊，請參閱 [SQL Server 中的快照集隔離](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/snapshot-isolation-in-sql-server)。

### <a name="general-limitations"></a>一般限制

-   資料表不能有非主索引鍵的識別欄位。

-   物件 (資料庫、資料表和資料行) 的名稱不能包含可列印的字元句點 (.)、左括弧 (\[\)，或右括弧 (\]\)。

-   不支援 Azure Active Directory 驗證。

#### <a name="unsupported-data-types"></a>不支援的資料類型

-   FileStream

-   SQL/CLR UDT

-   XMLSchemaCollection (支援 XML)

-   Cursor、Timestamp、Hierarchyid

#### <a name="limitations-on-service-and-database-dimensions"></a>服務和資料庫維度的限制

| **維度**                                                      | **限制**              | **因應措施**              |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| 任何資料庫可以隸屬的同步群組數目上限。       | 5                      |                             |
| 單一同步群組中的端點數目上限              | 30                     | 建立多個同步群組 |
| 單一同步群組中的內部部署端點數目上限。 | 5                      | 建立多個同步群組 |
| 資料庫名稱、資料表名稱、結構描述名稱和資料行名稱                       | 每個名稱 50 個字元 |                             |
| 一個同步群組中的資料表                                          | 500                    | 建立多個同步群組 |
| 一個同步群組中一個資料表中的資料行                              | 1000                   |                             |
| 一個資料表上的資料列大小                                        | 24 Mb                  |                             |
| 最小同步處理間隔                                           | 5 分鐘              |                             |
|||

## <a name="faq-about-sql-data-sync"></a>SQL 資料同步常見問題集

### <a name="how-much-does-the-sql-data-sync-preview-service-cost"></a>SQL 資料同步 (預覽) 服務的成本為何？

在預覽期間，SQL 資料同步 (預覽) 服務本身免費。  不過，您仍需對於資料移入和移出您的 SQL Database 執行個體支付資料傳輸費用。 如需詳細資訊，請參閱 [SQL Database 價格](https://azure.microsoft.com/pricing/details/sql-database/)。

### <a name="what-regions-support-data-sync"></a>哪些區域支援資料同步？

SQL 資料同步 (預覽) 適用於所有公用雲端區域。

### <a name="is-a-sql-database-account-required"></a>是否需要 SQL Database 帳戶？ 

是。 您必須具有可裝載中樞資料庫的 SQL Database 帳戶。

### <a name="can-i-use-data-sync-to-sync-between-sql-server-on-premises-databases-only"></a>資料同步能否僅在 SQL Server 內部部署資料庫之間同步？ 
無法直接進行。 您可以間接在 SQL Server 內部部署資料庫之間同步，不過，必須先在 Azure 建立中樞資料庫，然後將內部部署資料庫新增到同步群組。
   
### <a name="can-i-use-data-sync-to-seed-data-from-my-production-database-to-an-empty-database-and-then-keep-them-synchronized"></a>能否使用資料同步將生產環境資料庫的資料植入空白資料庫，然後讓資料保持同步？ 
是。 請從原始結構描述編寫結構描述，藉此在新的資料庫中手動建立結構描述。 建立結構描述之後，請將資料表新增到同步群組，以複製資料並讓資料保持同步。

### <a name="should-i-use-sql-data-sync-to-back-up-and-restore-my-databases"></a>應該使用 SQL 資料同步來備份及還原資料庫嗎？

不建議使用 SQL 資料同步 (預覽) 來建立資料的備份。 您無法備份並還原到特定點時間，因為 SQL 資料同步 (預覽) 同步處理並未設定版本。 此外，SQL 資料同步 (預覽) 不會備份其他 SQL 物件 (例如預存程序)，而且不會快速進行同等的還原作業。

如需建議的備份技術，請參閱[複製 Azure SQL Database](sql-database-copy.md)。

### <a name="is-collation-supported-in-sql-data-sync"></a>SQL 資料同步是否支援定序？

是。 在下列案例中 SQL 資料同步可支援定序：

-   如果所選取的同步結構描述資料表尚未存在您的中樞或成員資料庫中，則當您部署同步群組時，此服務會在空的目的地資料庫中，使用所選的定序設定，自動建立對應的資料表和資料行。

-   如果要同步處理的資料表已存在於您的中樞和成員資料庫中，則 SQL 資料同步會要求主索引鍵資料行在中樞與成員資料庫之間有相同的定序，才能成功部署同步群組。 主索引鍵資料行以外的資料行沒有任何定序限制。

### <a name="is-federation-supported-in-sql-data-sync"></a>SQL 資料同步是否支援同盟？

同盟根資料庫可使用於 SQL 資料同步 (預覽) 服務 (無任何限制)。 您無法將同盟資料庫端點新增至目前的 SQL 資料同步 (預覽) 版本。

## <a name="next-steps"></a>後續步驟

如需 SQL 資料同步的詳細資訊，請參閱：

-   [設定 Azure SQL 資料同步](sql-database-get-started-sql-data-sync.md)
-   [Azure SQL 資料同步最佳做法](sql-database-best-practices-data-sync.md)
-   [透過 OMS Log Analytics 監視 Azure SQL 資料同步](sql-database-sync-monitor-oms.md)
-   [對 Azure SQL 資料同步的問題進行疑難排解](sql-database-troubleshoot-data-sync.md)

-   示範如何設定 SQL 資料同步的完整 PowerShell 範例：
    -   [使用 PowerShell 在多個 Azure SQL Database 之間進行同步處理](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [使用 PowerShell 設定「資料同步」在內部部署的 Azure SQL Database 和 SQL Server 之間進行同步處理](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [下載 SQL 資料同步 REST API 文件](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

如需 SQL Database 的詳細資訊，請參閱：

-   [SQL Database 概觀](sql-database-technical-overview.md)
-   [資料庫生命週期管理](https://msdn.microsoft.com/library/jj907294.aspx)
