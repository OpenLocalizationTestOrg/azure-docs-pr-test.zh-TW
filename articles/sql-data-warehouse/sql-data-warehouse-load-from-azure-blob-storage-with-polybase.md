---
title: "從 Azure Blob 載入至 Azure 資料倉儲 | Microsoft Docs"
description: "了解如何此用 PolyBase 從 Azure Blob 儲存體將資料載入 SQL 資料倉儲。 從公用資料將幾個資料表載入 Contoso 零售資料倉儲結構描述。"
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
ms.openlocfilehash: 2859c1144f72fd685af89f83024df1409902ab0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="5d4dc-104">從 Azure Blob 儲存體將資料載入 SQL 資料倉儲 (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="5d4dc-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d4dc-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="5d4dc-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="5d4dc-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="5d4dc-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="5d4dc-107">使用 PolyBase 和 T-SQL 命令來從 Azure Blob 儲存體將資料載入 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-107">Use PolyBase and T-SQL commands to load data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="5d4dc-108">為了簡單起見，本教學課程會從公用 Azure 儲存體 Blob 將兩個資料表載入 Contoso 零售資料倉儲結構描述。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-108">To keep it simple, this tutorial loads two tables from a public Azure Storage Blob into the Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="5d4dc-109">若要載入完整的資料集，請從 Microsoft SQL Server 範例儲存機制執行[載入完整 Contoso 零售資料倉儲][Load the full Contoso Retail Data Warehouse]範例。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-109">To load the full data set, run the example [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] from the Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="5d4dc-110">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="5d4dc-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="5d4dc-111">設定 PolyBase 以從 Azure Blob 儲存體載入</span><span class="sxs-lookup"><span data-stu-id="5d4dc-111">Configure PolyBase to load from Azure blob storage</span></span>
2. <span data-ttu-id="5d4dc-112">將公用資料載入您的資料庫</span><span class="sxs-lookup"><span data-stu-id="5d4dc-112">Load public data into your database</span></span>
3. <span data-ttu-id="5d4dc-113">在完成載入後執行最佳化。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-113">Perform optimizations after the load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5d4dc-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="5d4dc-114">Before you begin</span></span>
<span data-ttu-id="5d4dc-115">若要執行本教學課程，您需要已經擁有 SQL 資料倉儲資料庫的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-115">To run this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="5d4dc-116">如果您尚未擁有此資料庫，請參閱[建立 SQL 資料倉儲][Create a SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-the-data-source"></a><span data-ttu-id="5d4dc-117">1.設定資料來源</span><span class="sxs-lookup"><span data-stu-id="5d4dc-117">1. Configure the data source</span></span>
<span data-ttu-id="5d4dc-118">PolyBase 使用 T-SQL 外部物件以定義外部資料的位置和屬性。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-118">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="5d4dc-119">外部物件定義會儲存在 SQL 資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-119">The external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="5d4dc-120">資料本身則會儲存在外部。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-120">The data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="5d4dc-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="5d4dc-121">1.1.</span></span> <span data-ttu-id="5d4dc-122">建立認證</span><span class="sxs-lookup"><span data-stu-id="5d4dc-122">Create a credential</span></span>
<span data-ttu-id="5d4dc-123">**略過此步驟** 。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-123">**Skip this step** if you are loading the Contoso public data.</span></span> <span data-ttu-id="5d4dc-124">您並不需要安全地存取公用資料，因為該資料已經可供所有人存取。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-124">You don't need secure access to the public data since it is already accessible to anyone.</span></span>

<span data-ttu-id="5d4dc-125">**不要略過此步驟** 。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="5d4dc-126">若要透過認證存取資料，請使用下列指令碼來建立資料庫範圍的認證，然後在定義資料來源的位置時使用它。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-126">To access data through a credential, use the following script to create a database-scoped credential, and then use it when defining the location of the data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="5d4dc-127">跳到步驟 2。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-127">Skip to step 2.</span></span>

### <a name="12-create-the-external-data-source"></a><span data-ttu-id="5d4dc-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="5d4dc-128">1.2.</span></span> <span data-ttu-id="5d4dc-129">建立外部資料來源</span><span class="sxs-lookup"><span data-stu-id="5d4dc-129">Create the external data source</span></span>
<span data-ttu-id="5d4dc-130">使用此 [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] 命令以儲存資料的位置及類型。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="5d4dc-131">如果您選擇將 Azure Blob 儲存體容器設為公用，請記住，當資料離開資料中心時，您身為資料擁有者將必須支付資料流出費用。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-131">If you choose to make your azure blob storage containers public, remember that as the data owner you will be charged for data egress charges when data leaves the data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="5d4dc-132">2.設定資料格式</span><span class="sxs-lookup"><span data-stu-id="5d4dc-132">2. Configure data format</span></span>
<span data-ttu-id="5d4dc-133">資料將會以文字檔儲存在 Azure Blob 儲存體中，每個欄位都會以分隔符號分隔。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-133">The data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="5d4dc-134">執行此 [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] 命令以指定文字檔中資料的格式。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command to specify the format of the data in the text files.</span></span> <span data-ttu-id="5d4dc-135">Contoso 資料為未壓縮且以直立線符號分隔。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-135">The Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-the-external-tables"></a><span data-ttu-id="5d4dc-136">3.建立外部資料表</span><span class="sxs-lookup"><span data-stu-id="5d4dc-136">3. Create the external tables</span></span>
<span data-ttu-id="5d4dc-137">您在指定資料來源和檔案格式之後，便可以開始建立外部資料表。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-137">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> 

### <a name="31-create-a-schema-for-the-data"></a><span data-ttu-id="5d4dc-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="5d4dc-138">3.1.</span></span> <span data-ttu-id="5d4dc-139">建立資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-139">Create a schema for the data.</span></span>
<span data-ttu-id="5d4dc-140">若要在您的資料庫中建立儲存 Contoso 資料的位置，請建立結構描述。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-140">To create a place to store the Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-the-external-tables"></a><span data-ttu-id="5d4dc-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="5d4dc-141">3.2.</span></span> <span data-ttu-id="5d4dc-142">建立外部資料表。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-142">Create the external tables.</span></span>
<span data-ttu-id="5d4dc-143">執行此指令碼來建立 DimProduct 和 FactOnlineSales 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-143">Run this script to create the DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="5d4dc-144">我們在這邊只需要定義資料行名稱和資料類型，並將它們繫結至 Azure Blob 儲存體檔案的位置及格式。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-144">All we are doing here is defining column names and data types, and binding them to the location and format of the Azure blob storage files.</span></span> <span data-ttu-id="5d4dc-145">定義會儲存在 SQL 資料倉儲中，而資料則仍然儲存在 Azure 儲存體 Blob 中。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-145">The definition is stored in SQL Data Warehouse and the data is still in the Azure Storage Blob.</span></span>

<span data-ttu-id="5d4dc-146">**LOCATION** 參數為 Azure 儲存體 Blob 中根目錄下方的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-146">The  **LOCATION** parameter is the folder under the root folder in the Azure Storage Blob.</span></span> <span data-ttu-id="5d4dc-147">每個資料表都位於不同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-the-data"></a><span data-ttu-id="5d4dc-148">4.載入資料</span><span class="sxs-lookup"><span data-stu-id="5d4dc-148">4. Load the data</span></span>
<span data-ttu-id="5d4dc-149">存取外部資料有很多不同的方式。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-149">There's different ways to access external data.</span></span>  <span data-ttu-id="5d4dc-150">您可以直接從外部資料表查詢資料、將資料載入新的資料庫資料表，或將外部資料新增到現有資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-150">You can query data directly from the external table, load the data into new database tables, or add external data to existing database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="5d4dc-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="5d4dc-151">4.1.</span></span> <span data-ttu-id="5d4dc-152">建立新的結構描述</span><span class="sxs-lookup"><span data-stu-id="5d4dc-152">Create a new schema</span></span>
<span data-ttu-id="5d4dc-153">CTAS 會建立包含資料的新資料表。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="5d4dc-154">首先，請建立 Contoso 資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-154">First, create a schema for the contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-the-data-into-new-tables"></a><span data-ttu-id="5d4dc-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="5d4dc-155">4.2.</span></span> <span data-ttu-id="5d4dc-156">將資料載入新資料表</span><span class="sxs-lookup"><span data-stu-id="5d4dc-156">Load the data into new tables</span></span>
<span data-ttu-id="5d4dc-157">若要從 Azure Blob 儲存體載入資料，並將它儲存在資料庫內的資料表中，請使用 [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] 陳述式。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-157">To load data from Azure blob storage and save it in a table inside of your database, use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="5d4dc-158">以 CTAS 載入將能利用您剛剛建立的強型別外部資料表。針對每個資料表，請使用一個 [CTAS][CTAS] 陳述式。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-158">Loading with CTAS leverages the strongly typed external tables you have just created.To load the data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="5d4dc-159">CTAS 建立新的資料表，並將選取陳述式的結果填入該資料表。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="5d4dc-160">CTAS 定義新資料表，以使它擁有和選取陳述式之結果相同的資料行和資料類型。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="5d4dc-161">如果您選取外部資料表上的所有資料行，則新資料表將會是外部資料表中資料行和資料類型的複本。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-161">If you select all the columns from an external table, the new table will be a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="5d4dc-162">在此範例中，我們同時將維度和事實資料表建立為雜湊分散式資料表。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-162">In this example, we create both the dimension and the fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-the-load-progress"></a><span data-ttu-id="5d4dc-163">4.3 追蹤載入進度</span><span class="sxs-lookup"><span data-stu-id="5d4dc-163">4.3 Track the load progress</span></span>
<span data-ttu-id="5d4dc-164">您可以使用動態管理檢視 (DMV) 來追蹤載入進度。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-164">You can track the progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- To see all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- To see a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- To track bytes and files
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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="5d4dc-165">5.最佳化資料行存放區壓縮</span><span class="sxs-lookup"><span data-stu-id="5d4dc-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="5d4dc-166">根據預設，SQL 資料倉儲會將資料表儲存為叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-166">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="5d4dc-167">載入完成後，某些資料列可能不會被壓縮為資料行存放區。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-167">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="5d4dc-168">有許多原因會導致發生此情況。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="5d4dc-169">若要深入了解，請參閱[管理資料行存放區索引][manage columnstore indexes]。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-169">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="5d4dc-170">若要最佳化載入後的查詢效能和資料行存放區壓縮，請重建資料表以強制資料行存放區索引對所有資料列進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-170">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="5d4dc-171">如需維護資料行存放區索引的詳細資訊，請參閱[管理資料行存放區索引][manage columnstore indexes]一文。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-171">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="5d4dc-172">6.最佳化統計資料</span><span class="sxs-lookup"><span data-stu-id="5d4dc-172">6. Optimize statistics</span></span>
<span data-ttu-id="5d4dc-173">您最好在載入後立刻建立單一資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-173">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="5d4dc-174">針對統計資料，您將會有一些選項。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-174">There are some choices for statistics.</span></span> <span data-ttu-id="5d4dc-175">例如，如果您在每個資料行上建立單一資料行統計資料，可能會需要很長的時間才能重建所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-175">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="5d4dc-176">如果您知道某些資料行不會被包含在查詢述詞中，您可以略過為那些資料行建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-176">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="5d4dc-177">如果您決定要在每個資料表的每個資料行上建立單一資料行統計資料，您可以使用[統計資料][statistics]一文中的預存程序程式碼範例 `prc_sqldw_create_stats`。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-177">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="5d4dc-178">下列範例為建立統計資料的好起點。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-178">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="5d4dc-179">它會在維度資料表中的每個資料行上，以及在事實資料表中的每個聯結資料行上建立單一資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-179">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="5d4dc-180">您之後隨時可以將單一或多個資料行統計資料新增到其他事實資料表資料行上。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-180">You can always add single or multi-column statistics to other fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="5d4dc-181">成就解鎖！</span><span class="sxs-lookup"><span data-stu-id="5d4dc-181">Achievement unlocked!</span></span>
<span data-ttu-id="5d4dc-182">您已成功將公用資料載入 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="5d4dc-183">太棒了！</span><span class="sxs-lookup"><span data-stu-id="5d4dc-183">Great job!</span></span>

<span data-ttu-id="5d4dc-184">您現在可以使用與下面類似的查詢來開始查詢資料表︰</span><span class="sxs-lookup"><span data-stu-id="5d4dc-184">You can now start querying the tables using queries like the following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="5d4dc-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d4dc-185">Next steps</span></span>
<span data-ttu-id="5d4dc-186">若要載入完整的 Contoso 零售資料倉儲資料，請使用指令碼。如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="5d4dc-186">To load the full Contoso Retail Data Warehouse data, use the script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
