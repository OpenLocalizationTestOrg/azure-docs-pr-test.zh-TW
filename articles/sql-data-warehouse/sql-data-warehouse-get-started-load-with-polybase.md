---
title: "在 SQL 資料倉儲教學課程 aaaPolyBase |Microsoft 文件"
description: "了解有什麼 PolyBase 以及 toouse 會針對資料倉儲案例。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>在 SQL 資料倉儲中使用 PolyBase 載入資料
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

本教學課程示範如何使用 AzCopy 和 PolyBase 的 SQL 資料倉儲 tooload 資料。 課程結束後，您將了解如何：

* 使用 AzCopy toocopy 資料 tooAzure blob 儲存體
* 建立資料庫物件 toodefine hello 資料
* 執行 T-SQL 查詢 tooload hello 資料

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>必要條件
您必須完成本教學課程 toostep，

* SQL 資料倉儲資料庫。
* 類型為標準本地備援儲存體 (標準 LRS)、標準異地備援儲存體 (標準 GRS) 或標準讀取存取異地備援儲存體 (標準 RAGRS) 的 Azure 儲存體帳戶。
* AzCopy 命令列公用程式。 下載並安裝 hello[最新版本的 AzCopy] [ latest version of AzCopy]以 hello Microsoft Azure 儲存體 Tools 安裝。
  
    ![Azure 儲存體工具](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>步驟 1： 加入範例資料 tooAzure blob 儲存體
在訂單 tooload 資料，我們需要 tooput 一些範例資料到 Azure blob 儲存體。 在此步驟中，我們會在 Azure 儲存體 Blob 中填入範例資料。 更新版本中，我們將使用 PolyBase tooload 此範例資料插入 SQL 資料倉儲資料庫。

### <a name="a-prepare-a-sample-text-file"></a>A. 準備範例文字檔
tooprepare 範例文字檔案：

1. 開啟 [記事本] 及複製到新的檔案之後的資料行的 hello。 為 %temp%\dimdate2.txt 儲存此 tooyour 本機暫存目錄。

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a>B. 尋找您的 Blob 服務端點
toofind blob 服務端點：

1. 從 hello Azure 入口網站選取**瀏覽** > **儲存體帳戶**。
2. 按一下您想 toouse hello 儲存體帳戶。
3. 在 hello 儲存體帳戶刀鋒視窗中，按一下 Blob
   
    ![按一下 Blob](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. 儲存您的 Blob 服務端點 URL，以供稍後使用。
   
    ![Blob 服務端點](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. 找出您的 Azure 儲存體金鑰
toofind Azure 儲存體金鑰：

1. Hello Azure 入口網站，從選取**瀏覽** > **儲存體帳戶**。
2. 按一下您想 toouse hello 儲存體帳戶。
3. 選取 [所有設定] > [存取金鑰]。
4. 按一下 hello 複製方塊 toocopy toohello 剪貼簿存取金鑰的其中一個。
   
    ![複製 Azure 儲存體金鑰](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. 複製 hello 範例檔案 tooAzure blob 儲存體
toocopy 資料 tooAzure blob 儲存體：

1. 開啟命令提示字元，並變更目錄 toohello AzCopy 安裝目錄。 此命令會變更 toohello 預設 64 位元的 Windows 用戶端上的安裝目錄。
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. 執行下列命令 tooupload hello 檔 hello。 針對 <blob service endpoint URL> 指定 Blob 服務端點 URL，並針對 <azure_storage_account_key> 指定 Azure 儲存體帳戶金鑰。
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

另請參閱[開始使用 AzCopy 命令列公用程式的 hello][Getting Started with hello AzCopy Command-Line Utility]。

### <a name="e-explore-your-blob-storage-container"></a>E. 瀏覽 Blob 儲存體容器
您上傳 tooblob 儲存體 toosee hello 檔案：

1. 返回 tooyour Blob 服務刀鋒視窗。
2. 在 [容器] 下，按兩下 [資料容器] 。
3. tooexplore hello 路徑 tooyour 資料按一下 hello 資料夾**datedimension** ，您會看到您上傳的檔案**DimDate2.txt**。
4. tooview 內容，然後按一下**DimDate2.txt**。
5. 請注意，在 hello Blob 屬性刀鋒視窗中，您可以下載或刪除 hello 檔案。
   
    ![檢視 Azure 儲存體 Blob](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>步驟 2： 建立 hello 範例資料的外部資料表
本節中，我們會建立定義 hello 範例資料的外部資料表。

PolyBase 會在 Azure blob 儲存體中使用外部資料表 tooaccess 資料。 因為 hello 資料不會儲存 SQL 資料倉儲內，PolyBase 會處理驗證 toohello 外部資料使用的資料庫範圍認證。

在此步驟中的 hello 範例會使用這些 TRANSACT-SQL 陳述式 toocreate 外部資料表。

* [建立主要金鑰 (TRANSACT-SQL)] [ Create Master Key (Transact-SQL)] tooencrypt hello 密碼，您的資料庫範圍認證。
* [建立資料庫範圍認證 (TRANSACT-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify 驗證您的 Azure 儲存體帳戶資訊。
* [建立外部資料來源 (TRANSACT-SQL)] [ Create External Data Source (Transact-SQL)] toospecify hello 位置，您的 Azure blob 儲存體。
* [建立外部檔案格式 (TRANSACT-SQL)] [ Create External File Format (Transact-SQL)] toospecify hello 格式的資料。
* [建立外部資料表 (TRANSACT-SQL)] [ Create External Table (Transact-SQL)] toospecify hello 資料表定義和位置 hello 資料。

對 SQL 資料倉儲資料庫執行這個查詢。 它會建立具名 DimDate2External toohello DimDate2.txt 範例資料點 hello Azure blob 儲存體中的 hello dbo 結構描述中的外部資料表。

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


在 Visual Studio 中的 SQL Server 物件總管，您可以看到 hello 外部檔案格式、 外部資料來源，以及 hello DimDate2External 資料表。

![檢視外部資料表](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>步驟 3：將資料載入 SQL 資料倉儲
Hello 外部資料表建立之後，您可以 hello 資料載入新的資料表，或將其插入到現有的資料表。

* tooload hello 資料到新資料表，執行 hello [CREATE TABLE AS SELECT (TRANSACT-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)]陳述式。 hello 新資料表會有命名 hello 查詢中的 hello 資料行。 hello hello 資料行資料類型會比 hello 外部資料表定義中的 hello 資料類型。
* tooload hello 資料到現有資料表中，使用 hello [INSERT...選取 (TRANSACT-SQL)] [ INSERT...SELECT (Transact-SQL)]陳述式。

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>步驟 4：建立新載入資料的統計資料
SQL 資料倉儲不會自動建立或自動更新統計資料。 因此，tooachieve 高的查詢效能，務必先載入 toocreate hello 之後每個資料表的每個資料行的統計資料。 它也是在 hello 資料大量變更後重要 tooupdate 統計資料。

此範例 hello 新 DimDate2 資料表上建立單一資料行統計資料。

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

詳細資訊，請參閱 toolearn[統計資料][Statistics]。  

## <a name="next-steps"></a>後續步驟
請參閱 hello [PolyBase 指南][ PolyBase guide]進一步開發使用 PolyBase 的解決方案時，您應該知道的資訊。

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
