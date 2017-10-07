---
title: "Azure SQL 資料倉儲 aaaLoad 資料 |Microsoft 文件"
description: "了解 hello 常見的資料載入到 SQL 資料倉儲案例。 這包含使用 PolyBase、Azure Blob 儲存體、一般檔案及寄送磁碟。 您也可以使用協力廠商工具。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>將資料載入 Azure SQL 資料倉儲
Hello 的情節選項和建議將 SQL 資料倉儲載入資料的摘要。

hello 困難的部分載入資料的通常準備 hello 資料 hello 負載。 Azure 利用 Azure blob 儲存體做為一般資料存放區，讓許多 hello 服務簡化載入和使用 Azure Data Factory tooorchestrate 之間的通訊和資料移動 hello Azure 服務。 這些程序會與它使用大量平行處理以平行方式從 Azure blob 儲存體 (MPP) tooload 資料到 SQL 資料倉儲 PolyBase 技術整合。 

如需有關載入範例資料庫的教學課程，請參閱[載入範例資料庫][Load sample databases]。

## <a name="load-from-azure-blob-storage"></a>從 Azure Blob 儲存體載入
toouse PolyBase tooload 資料從 Azure blob 儲存體 hello 最快方式 tooimport 資料到 SQL 資料倉儲。 PolyBase 會使用 SQL 資料倉儲的大量平行處理以平行方式從 Azure blob 儲存體 (MPP) 設計 tooload 資料。 toouse PolyBase，您可以使用 T-SQL 命令或 Azure Data Factory 管線。

### <a name="1-use-polybase-and-t-sql"></a>1.使用 PolyBase 和 T-SQL
載入流程的摘要：

1. 移動資料 tooAzure blob 儲存體或 Azure 資料湖存放區，並將它儲存在文字檔中。
2. 設定 SQL 資料倉儲 toodefine hello 位置與格式 hello 資料中的外部物件
3. 平行執行 T-SQL 命令 tooload hello 資料到新的資料庫資料表。

<!-- 5. Schedule and run a loading job. --> 

如需教學課程，請參閱[資料從 Azure blob 儲存體 tooSQL 資料倉儲 (PolyBase) 載入][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]。

### <a name="2-use-azure-data-factory"></a>2.使用 Azure Data Factory
更簡單的方式 toouse PolyBase，您可以建立使用 SQL 資料倉儲 PolyBase tooload 資料從 Azure blob 儲存體的 Azure Data Factory 管線。 這是快速 tooconfigure，因為您不再需要 toodefine hello T-SQL 物件。 如果您未匯入需要 tooquery hello 外部資料，請使用 T-SQL。 

載入流程的摘要：

1. 移動資料 tooAzure blob 儲存體，並將它儲存在文字檔中。 Azure Data Factory 目前不支援 ADLS 和 PolyBase 連線。
2. 建立 Azure Data Factory 管線 tooingest hello 資料。 使用 hello PolyBase 選項。
4. 排程和執行 hello 管線。

如需教學課程，請參閱[資料從 Azure blob 儲存體 tooSQL 資料倉儲 (Azure Data Factory) 載入][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]。

## <a name="load-from-sql-server"></a>從 SQL Server 載入
tooload 資料從 SQL Server tooSQL 您可以使用 Integration Services (SSIS) 資料倉儲會傳送一般檔案，或寄送磁碟 tooMicrosoft。 閱讀 toosee hello 不同載入處理序和連結 tootutorials 的摘要。

tooplan 來自 SQL Server tooSQL 資料倉儲，完整的資料移轉，請參閱 hello[移轉概觀][Migration overview]。 

### <a name="use-integration-services-ssis"></a>使用 Integration Services (SSIS)
如果您已經在使用 SQL server Integration Services (SSIS) 封裝 tooload，您可以更新您為 hello 來源和 SQL 資料倉儲，做為 hello 目的地的封裝 toouse SQL Server。 這是快速和輕鬆 toodo，是不錯的選擇，如果您不想 toomigrate 您載入和處理 toouse 已經在 hello 雲端中的資料。 hello 代價是 hello 負載將會比使用 PolyBase，因為此 SSIS 不會以平行方式執行 hello 負載變慢。

載入流程的摘要：

1. 請修訂您 Integration Services 封裝 toopoint toohello SQL Server 執行個體 hello 來源和目的地 hello 的 hello SQL 資料倉儲資料庫。
2. 如果它尚未有，移轉您的結構描述 tooSQL 資料倉儲。
3. 在封裝中的變更 hello 對應僅使用 hello 資料類型所支援的 SQL 資料倉儲。
4. 排程和執行 hello 封裝。

如需教學課程，請參閱[從 SQL Server tooAzure SQL 資料倉儲 (SSIS) 資料載入][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]。

### <a name="use-azcopy-recommended-for--10-tb-data"></a>使用 AZCopy (建議於資料 < 10 TB 的情況使用)
如果 < 10 TB 的資料大小，您可以從 SQL Server tooflat 檔案匯出 hello 資料、 將複製 hello 檔案 tooAzure blob 儲存體，並再使用 PolyBase tooload hello 資料到 SQL 資料倉儲

載入流程的摘要：

1. 使用 SQL Server tooflat 檔案 hello bcp 命令列公用程式 tooexport 資料。
2. 使用 hello AZCopy 命令列公用程式 toocopy 資料從一般檔案 tooAzure blob 儲存體。
3. 使用 PolyBase tooload 到 SQL 資料倉儲。

如需教學課程，請參閱[資料從 Azure blob 儲存體 tooSQL 資料倉儲 (PolyBase) 載入][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]。

### <a name="use-bcp"></a>使用 bcp
如果您有少量資料您可以使用 bcp tooload 直接在 Azure SQL 資料倉儲。

載入流程的摘要：

1. 使用 SQL Server tooflat 檔案 hello bcp 命令列公用程式 tooexport 資料。
2. 使用 bcp tooload 資料從一般檔案直接 tooSQL 資料倉儲。

如需教學課程，請參閱[資料從 SQL Server tooAzure SQL 資料倉儲 (bcp) 載入][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]。

### <a name="use-importexport-recommended-for--10-tb-data"></a>使用匯入/匯出 (建議於資料 > 10 TB 的情況使用)
如果您的資料大小 > 10 TB，而且您想 toomove 它 tooAzure，建議您將傳送服務我們磁碟[匯入/匯出][Import/Export]。 

載入流程的摘要

1. 使用可傳輸的磁碟上的 SQL Server tooflat 檔案 hello bcp 命令列公用程式 tooexport 資料。
2. 出貨 hello 磁碟 tooMicrosoft。
3. Microsoft 會將 SQL 資料倉儲 hello 資料載入

## <a name="load-from-hdinsight"></a>從 HDInsight 載入
SQL 資料倉儲支援從 HDInsight 透過 PolyBase 載入資料。 hello 程序是 hello 與從 Azure Blob 儲存體-使用 PolyBase tooconnect tooHDInsight tooload 資料載入資料相同。 

### <a name="1-use-polybase-and-t-sql"></a>1.使用 PolyBase 和 T-SQL
載入流程的摘要：

1. 移動資料 tooHDInsight 並將它儲存在文字檔、 ORC 或 Parquet 格式。
2. SQL 資料倉儲 toodefine hello 位置及 hello 資料的格式設定外部物件。
3. 平行執行 T-SQL 命令 tooload hello 資料到新的資料庫資料表。

如需教學課程，請參閱[資料從 Azure blob 儲存體 tooSQL 資料倉儲 (PolyBase) 載入][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]。

## <a name="recommendations"></a>建議
我們有許多合作夥伴皆提供載入解決方案。 toofind 出的詳細資訊，請參閱一份我們[解決方案合作夥伴][solution partners]。 

如果您的資料來自非關聯式資料來源，而且您想 tooload 到 SQL 資料倉儲您將需要 tootransform 成資料列和資料行之前將其載入它。 hello 轉換的資料不需要 toobe 儲存在資料庫中，可以將訊息儲存在文字檔中。

建立新載入資料的統計資料。 Azure 資料倉儲尚未支援自動建立或自動更新統計資料。  順序 tooget hello 最佳效能降低從您的查詢，請務必 toocreate hello 之後的所有資料表的所有資料行的統計資料先載入或 hello 資料會發生任何大量變更。  如需詳細資料，請參閱[統計資料][Statistics]。

## <a name="next-steps"></a>後續步驟
如需開發秘訣，請參閱 hello[開發概觀][development overview]。

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
