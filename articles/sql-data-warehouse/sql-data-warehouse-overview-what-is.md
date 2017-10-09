---
title: "aaaWhat 是 Azure SQL 資料倉儲？ | Microsoft Docs"
description: "企業級分散式資料庫，可處理資料量高達 PB 的關聯式與非關聯式資料。 它是 hello 業界第一個雲端資料倉儲與成長、 壓縮及暫停以秒為單位。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>什麼是 Azure SQL 資料倉儲？
Azure SQL 資料倉儲是一種巨量平行處理 (MPP) 以雲端為基礎、相應放大的關聯式資料庫，可處理大量的資料。 

SQL 資料倉儲：

* Azure 的雲端擴充功能結合 hello SQL Server 關聯式資料庫。 
* 從計算減少儲存體。
* 啟用增加、減少、暫停或繼續計算。 
* 整合跨 hello Azure 平台。
* 利用 SQL Server Transact-SQL (T-SQL) 和工具。
* 遵守各種法律和商務安全性需求，例如 SOC 和 ISO。

本文說明 hello 的 SQL 資料倉儲的重要功能。

## <a name="massively-parallel-processing-architecture"></a>巨量平行處理架構
SQL 資料倉儲是大量平行處理 (MPP) 分散式資料庫系統。 Hello 幕後 SQL 資料倉儲會將您的資料分散到許多無共用存放裝置和處理單位。 hello 資料會儲存在 Premium 本機備援儲存體的圖層，在其之上動態連結的運算節點執行查詢。 SQL 資料倉儲會採用 「 分割和征服 」 的方法 toorunning 載入和複雜查詢。 接收最佳化散發，，然後傳遞其工作 tooCompute 節點 toodo 以平行方式為控制節點要求。

使用減少的儲存體和計算，SQL 資料倉儲可以︰

* 擴大或縮小獨立計算的儲存體大小。
* 擴大或縮小計算能力，而不移動資料。
* 暫停計算容量，同時讓資料保持不變，只需要支付儲存體的費用。
* 在營運時間期間繼續計算容量。

hello 下列圖表顯示 hello 架構中更多詳細資料。

![SQL 資料倉儲架構][1]

**控制節點：** hello 控制節點管理及最佳化查詢。 它是 hello 前端與所有應用程式與連線互動的。 在 SQL 資料倉儲、 hello 控制節點由 SQL Database 連接 tooit 看起來並替 hello 相同。 在 hello 介面 hello 控制節點會協調所有 hello 資料移動和所需的計算 toorun 對分散式資料的平行查詢。 當您提交 T-SQL 查詢 tooSQL 資料倉儲時，hello 控制節點會將其轉換為每個平行的計算節點執行的個別查詢。

**計算節點：** hello 計算節點做為 SQL 資料倉儲背後的 hello 電源。 它們是儲存資料和處理查詢的 SQL Database。 當您新增資料時，SQL 資料倉儲會發佈 hello 列 tooyour 計算節點。 hello 計算節點是在您的資料執行 hello 平行查詢的 hello 工作者。 經過處理後，傳遞 hello 結果後 toohello 控制節點。 toofinish hello 查詢 hello 控制節點的彙總 hello 結果，並傳回 hello 最終結果。

**儲存體：** 您的資料會儲存在 Azure Blob 儲存體中。 計算節點互動與您的資料，當它們撰寫，並直接讀取從 blob 儲存體 tooand。 因為 Azure 儲存體擴充以透明且大幅，可以執行 SQL 資料倉儲 hello 相同。 計算和儲存體各自獨立，所以 SQL 資料倉儲可以自動調整儲存體，與計算分開調整，反之亦然。 Azure Blob 儲存體也完全提供容錯功能，並簡化 hello 備份和還原程序。

**資料移動服務：**資料移動服務 (DMS) hello 節點之間移動資料。 DMS 提供 hello 計算節點存取 toodata 他們需要聯結和彙總。 DMS 不是 Azure 服務。 它會連同 SQL 資料庫執行 hello 的所有節點的 Windows 服務。 DMS 是背景處理序，無法直接互動。 不過，您可以查看查詢計劃 toosee DMS 作業發生時，因為資料移動是必要的 toorun 每個查詢，以平行方式。

## <a name="optimized-for-data-warehouse-workloads"></a>已針對資料倉儲工作負載最佳化
hello MPP 方法是由數個資料倉儲特定的效能最佳化，包括輔助：

* 一項分散式查詢最佳化工具和一組複雜的統計資料。 使用上資訊的資料大小與散發，hello 服務所能 toooptimize 查詢評估特定分散式的查詢作業的 hello 成本。
* 進階的演算法與技術整合到 hello 資料在為必要 tooperform hello 查詢運算資源之間移動處理序 tooefficiently 移動資料。 這些資料移動作業內建的而且所有最佳化 toohello Data Movement Service 會自動都發生。
* 預設的叢集 **資料行存放** 區索引。 藉由使用資料行為基礎的存放裝置，SQL 資料倉儲會取得平均 5 x 壓縮提升傳統的資料列導向儲存，並向上 too10x 或多個查詢的效能提升。 分析查詢需要 tooscan 大量的資料列使用更好資料行存放區索引。


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>可預測且可調整的效能與資料倉儲單位
SQL 資料倉儲是使用與 SQL Database 類似的技術建置，表示使用者對於分析查詢可以預期一致且可預測的效能。 使用者應以線性方式預期 toosee 效能小數位數，因為它們加法或減法計算節點。 資料倉儲單位 (Dwu) 被以資源 tooyour SQL 資料倉儲的配置。 Dwu 調整為基礎的資源，例如 CPU、 記憶體配置 tooyour SQL 資料倉儲的 IOPS 的量值。 增加 hello Dwu 數目會增加資源和效能。 具體而言，DWU 有助於確保：

* 您就可以 tooscale 資料倉儲，而不需擔心 hello 基礎硬體或軟體。
* 您可以預測效能改進 DWU 層級變更資料倉儲的 hello 計算之前。
* hello 相關的硬體與軟體執行個體可以變更或移動而不影響工作負載效能。
* Microsoft 加以改善而不會影響您的工作負載的 hello 效能基礎架構的 hello 服務的 hello。
* Microsoft 可快速改進效能在 SQL 資料倉儲中，是可擴充的方式，效果 hello 系統的平均。

資料倉儲單位會提供包含三個度量的量值，而這些度量與資料倉儲工作負載效能高度相互關聯。 hello 下列主要工作負載度量以線性方式與 hello Dwu 的小數位數。

**掃描/彙總**：標準資料倉儲查詢，該查詢會掃描大量資料列，然後執行複雜的彙總。 這是 I/O 和 CPU 密集作業。

**載入：** hello 服務 hello 能力 tooingest 資料。 使用來自 Azure 儲存體 Blob 或 Azure Data Lake 的 PolyBase 時的負載效能最佳。 此計量為設計的 toostress 網路和 CPU 方面的 hello 服務。

**為選取 (CTAS) 中建立資料表：** CTAS 測量 hello 能力 toocopy 資料表。 這牽涉到從儲存體，分散 hello 應用裝置 hello 節點和再次寫入 toostorage 讀取資料。 這是 CPU、IO 和網路密集作業。

## <a name="built-on-sql-server"></a>建置在 SQL Server 上
SQL 資料倉儲根據 hello SQL Server 關聯式資料庫引擎，並包含許多預期可從企業資料倉儲的 hello 功能。 如果您已經知道 T-SQL，很容易 tootransfer 您知識 tooSQL 資料倉儲。 您是否進階或剛開始使用，開始有助於 hello 範例 hello 文件。 整體來說，您可以將之視為 hello 方式，我們已建構的 SQL 資料倉儲的 hello 語言項目，如下所示：

* SQL 資料倉儲會將 T-SQL 語法用於許多作業。 並且支援一組廣泛的傳統 SQL 建構，例如預存程序、使用者定義函式、資料表資料分割、索引和定序。
* SQL 資料倉儲也包含各種較新的 SQL Server 功能，包括叢集**資料行存放區**索引、PolyBase 整合和資料稽核 (完整的威脅評估)。
* 某些 T-SQL 語言項目，較不常用資料倉儲工作負載，或較新 tooSQL 伺服器，可能無法目前可用。 如需詳細資訊，請參閱 hello[移轉文件][Migration documentation]。

Hello TRANSACT-SQL 和 SQL Server、 SQL 資料倉儲、 SQL Database 和 Analytics Platform System 之間的功能共通性，您可以開發符合資料需求的解決方案。 您可以決定其中 tookeep 您的資料，根據效能、 安全性，和小數位數的需求，以及視不同系統之間傳輸資料。

## <a name="data-protection"></a>資料保護
SQL 資料倉儲會將所有資料儲存在 Azure Premium 本地備援儲存體中。 多份同步 hello 資料會保留在 hello 本機資料中心 tooguarantee 透明資料保護針對當地語系化的故障。 此外，SQL 資料倉儲會使用 Azure 儲存體快照集，定期自動備份作用中 (未暫停) 的資料庫。 toolearn 更多有關如何備份與還原如何運作，請參閱 hello[備份和還原的概觀][Backup and restore overview]。

## <a name="integrated-with-microsoft-tools"></a>與 Microsoft 工具整合
SQL 資料倉儲也會整合許多 hello 工具該使用者可能很熟悉的 SQL Server。 這些工具包括：

**傳統的 SQL Server 工具** ：SQL 資料倉儲會與 SQL Server Analysis Services、Integration Services 和 Reporting Services 完整整合。

**以雲端為基礎的工具**：SQL 資料倉儲可以與 Azure 中的各種服務整合，包括 Data Factory、串流分析、機器學習服務和 Power BI。 如需更完整的清單，請參閱[整合式工具概觀][Integrated tools overview]。

**協力廠商工具**：許多協力廠商工具提供者與 SQL 資料倉儲整合的工具都已經過認證。 如需完整清單，請參閱 [SQL 資料倉儲解決方案合作夥伴][SQL Data Warehouse solution partners]。

## <a name="hybrid-data-sources-scenarios"></a>混合式資料來源案例
Polybase 可讓您 tooleverage 您使用熟悉的 T-SQL 命令的不同來源的資料。 Polybase 可讓您保留在 Azure Blob 儲存體，如同它是正規資料表 tooquery 非關聯式資料。 使用 Polybase tooquery 非關聯式資料或 tooimport 非關聯式資料到 SQL 資料倉儲。

* PolyBase 會使用外部資料表 tooaccess 非關聯式資料。 hello 資料表定義會儲存在 SQL 資料倉儲中，您可以使用 SQL 存取和工具與您存取標準的關聯式資料。
* 在其整合中無從得知 Polybase。 它會公開 hello 相同的功能，它支援的功能 tooall hello 來源。 Polybase 所讀取的 hello 資料可以是以各種格式，包括分隔的檔案或 ORC 檔案。
* PolyBase 可使用的 tooaccess blob 儲存體，也會被當做使用儲存體 HDInsight 叢集。 這可讓您存取 toohello 關聯式與非關聯式工具相同的資料。

## <a name="sla"></a>SLA
SQL 資料倉儲提供產品層級的服務等級協定 (SLA) 做為 Microsoft Online Services SLA 的一部分。 如需詳細資訊，請參閱 [SQL 資料倉儲的 SLA][SLA for SQL Data Warehouse]。 如需所有其他產品的 SLA 資訊，您可以造訪 hello[服務等級協定]Azure 頁面上，或下載 hello[大量授權][ Volume Licensing]頁面。 

## <a name="next-steps"></a>後續步驟
既然您稍微了解 SQL 資料倉儲，了解如何 tooquickly[建立 SQL 資料倉儲][ create a SQL Data Warehouse]和[範例資料載入][load sample data]。 如果您是新 tooAzure，您可能會發現 hello [Azure 詞彙][ Azure glossary]遇到新的術語很有幫助。 或者，也可以看一下其中一些其他 SQL 資料倉儲資源。  

* [客戶成功案例]
* [部落格]
* [功能要求]
* [影片]
* [客戶諮詢小組部落格]
* [建立支援票證]
* [MSDN 論壇]
* [Stack Overflow 論壇]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[建立支援票證]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[客戶成功案例]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[部落格]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[客戶諮詢小組部落格]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[功能要求]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN 論壇]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Stack Overflow 論壇]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[影片]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[服務等級協定]: https://azure.microsoft.com/en-us/support/legal/sla/
