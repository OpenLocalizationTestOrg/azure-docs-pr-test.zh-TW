---
title: "從 Azure blob tooAzure 資料倉儲 aaaLoad |Microsoft 文件"
description: "了解如何 toouse PolyBase tooload 資料從 Azure 到 SQL 資料倉儲的 blob 儲存體。 從公用資料載入 hello Contoso 零售資料倉儲結構描述的一些資料表。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>從 Azure Blob 儲存體將資料載入 SQL 資料倉儲 (PolyBase)
> [!div class="op_single_selector"]
> * [Data Factory](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

使用 PolyBase 與 T-SQL 命令 tooload 資料從 Azure blob 儲存體到 Azure SQL 資料倉儲。 

tookeep 它簡單，本教學課程中的載入兩個資料表公開的 Azure 儲存體 Blob hello Contoso 零售資料倉儲結構描述。 tooload hello 完整資料集，執行 hello 範例[負載 hello Contoso 完整的零售資料倉儲][ Load hello full Contoso Retail Data Warehouse] hello Microsoft SQL Server 範例儲存機制中。

在本教學課程中，您將：

1. 設定 PolyBase tooload 從 Azure blob 儲存體
2. 將公用資料載入您的資料庫
3. Hello 載入完成之後，請執行最佳化。

## <a name="before-you-begin"></a>開始之前
toorun 本教學課程中，您必須已有 SQL 資料倉儲資料庫的 Azure 帳戶。 如果您尚未擁有此資料庫，請參閱[建立 SQL 資料倉儲][Create a SQL Data Warehouse]。

## <a name="1-configure-hello-data-source"></a>1.Hello 資料來源設定
PolyBase 會使用 T-SQL 外部物件 toodefine hello 位置及 hello 外部資料的屬性。 hello 外部物件的定義會儲存在 SQL 資料倉儲。 hello 資料本身儲存在外部。

### <a name="11-create-a-credential"></a>1.1. 建立認證
**略過此步驟**如果您載入 hello Contoso 公開資料。 您不需要安全存取 toohello 公用資料，因為它已經是可存取 tooanyone。

**不要略過此步驟** 。 透過認證時，使用下列的 hello tooaccess 資料 toocreate 資料庫範圍認證的指令碼，然後再使用它，定義 hello hello 資料來源位置時。

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
```

略過 toostep 2。

### <a name="12-create-hello-external-data-source"></a>1.2. 建立 hello 外部資料來源
使用此[CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE]命令 toostore hello 位置 hello 資料和 hello 的資料類型。 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> 如果您選擇 toomake azure blob 儲存體容器公開，請記住，hello 資料擁有者為您將支付資料輸出費用資料離開 hello 資料中心時。 
> 
> 

## <a name="2-configure-data-format"></a>2.設定資料格式
hello 資料會儲存在 Azure blob 儲存體中的文字檔案中，每個欄位以分隔符號分隔。 執行此程序[CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] hello 文字檔案中的 hello 資料命令 toospecify hello 格式。 hello Contoso 資料未壓縮和管道分隔。

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-hello-external-tables"></a>3.建立 hello 外部資料表
現在您已經指定 hello 資料來源和檔案格式，您就準備好 toocreate hello 外部資料表。 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. 建立 hello 資料的結構描述。
toocreate 位置 toostore hello Contoso 資料在資料庫中，建立結構描述。

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. 建立 hello 外部資料表。
執行這個指令碼 toocreate hello DimProduct 和 FactOnlineSales 外部資料表。 這裡，我們所做為資料行名稱和資料類型定義，並加以繫結 toohello 位置與 hello Azure blob 儲存體檔案格式。 hello 定義會儲存在 SQL 資料倉儲和 hello 資料仍在 hello Azure 儲存體 Blob 中。

hello**位置**參數是 hello hello hello Azure 儲存體 Blob 中的根資料夾下的資料夾。 每個資料表都位於不同的資料夾中。

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a>4.將資料載入 hello
沒有多種 tooaccess 外部資料。  您可以查詢直接從 hello 外部資料表的資料、 hello 資料載入至新的資料庫資料表，或新增外部 tooexisting 資料庫資料表。  

### <a name="41-create-a-new-schema"></a>4.1. 建立新的結構描述
CTAS 會建立包含資料的新資料表。  首先，建立 hello contoso 資料的結構描述。

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Hello 資料載入至新的資料表
tooload 資料從 Azure blob 儲存體，並儲存在資料庫內資料表中，使用 hello [CREATE TABLE AS SELECT (TRANSACT-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)]陳述式。 載入 CTAS 搭配利用 hello 強型別有只 created.tooload hello 資料加入新資料表的外部資料表，請使用其中一個[CTAS] [ CTAS]每個資料表的陳述式。 
 
CTAS 建立新的資料表，並填入 hello select 陳述式的結果。 CTAS 定義新資料表 toohave hello hello 相同資料行和資料類型，如 hello hello 結果 select 陳述式。 如果您從外部資料表選取 hello 的所有資料行，hello 新資料表會處於 hello 外部資料表的 hello 資料行和資料類型的複本。

在此範例中，我們建立 hello 維度和 hello 事實資料表做為雜湊分散式的資料表。 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 追蹤 hello 負載進度
您可以追蹤您使用動態管理檢視 (Dmv) 的負載 hello 進度。 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a>5.最佳化資料行存放區壓縮
根據預設，SQL 資料倉儲會儲存 hello 資料表作為叢集資料行存放區索引。 載入完成後，部分 hello 資料的資料列可能會不壓縮成 hello 資料行存放區。  有許多原因會導致發生此情況。 詳細資訊，請參閱 toolearn[管理資料行存放區索引][manage columnstore indexes]。

toooptimize 查詢效能和負載之後, 的資料行存放區壓縮重建 hello 資料表 tooforce hello 資料行存放區索引 toocompress hello 的所有資料列。 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

如需維護資料行存放區索引的詳細資訊，請參閱 hello[管理資料行存放區索引][ manage columnstore indexes]發行項。

## <a name="6-optimize-statistics"></a>6.最佳化統計資料
載入之後立即是最佳的 toocreate 單一資料行統計資料。 針對統計資料，您將會有一些選項。 例如，如果您在每個資料行上建立單一資料行統計資料可能需要很長的時間 toorebuild hello 的所有統計資料。 如果您知道特定資料行不會成為 toobe 查詢述詞中的，您可以跳建立統計資料，這些資料行。

如果您決定 toocreate 每個資料表的每個資料行的單一資料行統計資料，您可以使用 hello 預存程序程式碼範例`prc_sqldw_create_stats`在 hello[統計資料][ statistics]發行項。

下列範例中的 hello 是很好的起點建立統計資料。 在 hello 維度資料表中，每個資料行和 hello 事實資料表中每個聯結資料行，它會建立單一資料行統計資料。 您可以在稍後新增單一或多個資料行統計資料 tooother 事實資料表資料行。

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a>成就解鎖！
您已成功將公用資料載入 Azure SQL 資料倉儲。 太棒了！

您現在可以開始查詢 hello 資料表使用類似 hello 下列查詢：

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>後續步驟
tooload hello 完整 Contoso 零售資料倉儲的資料，使用中的 hello 指令碼，如需開發秘訣，請參閱[SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
