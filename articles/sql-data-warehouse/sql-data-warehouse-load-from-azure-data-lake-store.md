---
title: "aaaLoad-Azure Data Lake Store tooSQL 資料倉儲 |Microsoft 文件"
description: "了解如何 toouse PolyBase 外部資料表到 Azure SQL 資料倉儲的 tooload 資料從 Azure 資料湖存放區。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="eaff9-103">將資料從 Azure Data Lake Store 載入到 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="eaff9-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="eaff9-104">這份文件可讓您所有的必要步驟 tooload 您自己的資料從 Azure 資料湖存放區 (ADLS) 至 SQL 資料倉儲使用 PolyBase。</span><span class="sxs-lookup"><span data-stu-id="eaff9-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="eaff9-105">雖然您無法 toorun 臨機操作查詢 hello 中儲存的資料使用 hello 外部資料表的 ADLS，最佳作法建議 hello 資料匯入 hello SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="eaff9-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="eaff9-106">估計時間： 10 分鐘，假設您擁有 hello 必要條件需要 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="eaff9-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="eaff9-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="eaff9-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="eaff9-108">建立外部資料庫物件 tooload 從 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="eaff9-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="eaff9-109">連接 tooan Azure 資料湖存放區目錄。</span><span class="sxs-lookup"><span data-stu-id="eaff9-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="eaff9-110">將資料載入到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="eaff9-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eaff9-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="eaff9-111">Before you begin</span></span>
<span data-ttu-id="eaff9-112">toorun 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="eaff9-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="eaff9-113">服務對服務驗證的 azure Active Directory 應用程式 toouse。</span><span class="sxs-lookup"><span data-stu-id="eaff9-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="eaff9-114">toocreate，遵循[Active directory 驗證](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="eaff9-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="eaff9-115">您需要 hello 用戶端識別碼、 金鑰和您的 Active Directory 應用程式 tooconnect tooyour 從 SQL 資料倉儲的 Azure Data Lake 的 OAuth2.0 語彙基元端點值。</span><span class="sxs-lookup"><span data-stu-id="eaff9-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="eaff9-116">Tooget 這些值的方式在上面的 hello 連結的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="eaff9-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="eaff9-117">請注意，Azure Active Directory 應用程式註冊的 hello '應用程式識別碼' 做為 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="eaff9-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="eaff9-118">SQL Server Management Studio 或 SQL Server Data Tools，toodownload SSMS 並連接，請參閱[查詢 SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="eaff9-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="eaff9-119">Azure SQL 資料倉儲、 toocreate 一個遵循： https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="eaff9-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="eaff9-120">一個啟用或未啟用加密的 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="eaff9-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="eaff9-121">toocreate 一個後續： https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="eaff9-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="eaff9-122">Hello 資料來源設定</span><span class="sxs-lookup"><span data-stu-id="eaff9-122">Configure hello data source</span></span>
<span data-ttu-id="eaff9-123">PolyBase 會使用 T-SQL 外部物件 toodefine hello 位置及 hello 外部資料的屬性。</span><span class="sxs-lookup"><span data-stu-id="eaff9-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="eaff9-124">hello 外部物件會儲存在第則儲存在外部的 SQL 資料倉儲和參考 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="eaff9-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="eaff9-125">建立認證</span><span class="sxs-lookup"><span data-stu-id="eaff9-125">Create a credential</span></span>
<span data-ttu-id="eaff9-126">tooaccess 您 Azure 資料湖存放區，您將需要 toocreate 資料庫主要金鑰 tooencrypt hello 下一個步驟中所使用的認證秘密。</span><span class="sxs-lookup"><span data-stu-id="eaff9-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="eaff9-127">然後，您會建立資料庫範圍認證，將設定在 AAD 中的 hello 服務主體認證。</span><span class="sxs-lookup"><span data-stu-id="eaff9-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="eaff9-128">使用者已使用 PolyBase tooconnect tooWindows Azure 儲存體 Blob，記下該 hello 認證語法的不同。</span><span class="sxs-lookup"><span data-stu-id="eaff9-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="eaff9-129">tooconnect tooAzure 資料湖存放區，您必須**第一個**建立 Azure Active Directory 應用程式，建立便捷鍵，並授與 hello 應用程式存取 toohello Azure 資料湖資源。</span><span class="sxs-lookup"><span data-stu-id="eaff9-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="eaff9-130">Instrucitons tooperform 依照位於[這裡](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)。</span><span class="sxs-lookup"><span data-stu-id="eaff9-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a><span data-ttu-id="eaff9-131">建立 hello 外部資料來源</span><span class="sxs-lookup"><span data-stu-id="eaff9-131">Create hello external data source</span></span>
<span data-ttu-id="eaff9-132">使用此[CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE]命令 toostore hello 位置 hello 資料和 hello 的資料類型。</span><span class="sxs-lookup"><span data-stu-id="eaff9-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="eaff9-133">您可以在 hello Azure 入口網站和 www.portal.azure.com 找到 hello ADL URI。</span><span class="sxs-lookup"><span data-stu-id="eaff9-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="eaff9-134">設定資料格式</span><span class="sxs-lookup"><span data-stu-id="eaff9-134">Configure data format</span></span>
<span data-ttu-id="eaff9-135">從 ADLS tooimport hello 資料，您需要 toospecify hello 外部檔案格式。</span><span class="sxs-lookup"><span data-stu-id="eaff9-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="eaff9-136">此命令皆具有格式特有的選項 toodescribe 您的資料。</span><span class="sxs-lookup"><span data-stu-id="eaff9-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="eaff9-137">以下是常用檔案格式的範例，它是一個以管線符號分隔的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="eaff9-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="eaff9-138">請查閱我們的 T-SQL 文件，以取得 [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] 的完整清單</span><span class="sxs-lookup"><span data-stu-id="eaff9-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

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

## <a name="create-hello-external-tables"></a><span data-ttu-id="eaff9-139">建立 hello 外部資料表</span><span class="sxs-lookup"><span data-stu-id="eaff9-139">Create hello external tables</span></span>
<span data-ttu-id="eaff9-140">現在您已經指定 hello 資料來源和檔案格式，您就準備好 toocreate hello 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="eaff9-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="eaff9-141">外部資料表是您與外部資料進行互動的方式。</span><span class="sxs-lookup"><span data-stu-id="eaff9-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="eaff9-142">PolyBase 會使用遞迴目錄周遊 tooread hello 目錄 hello 位置參數中指定的所有子目錄中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="eaff9-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="eaff9-143">此外，hello 下列範例顯示如何 toocreate hello 物件。</span><span class="sxs-lookup"><span data-stu-id="eaff9-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="eaff9-144">您必須使用您在 ADLS hello 資料 toocustomize hello 陳述式 toowork。</span><span class="sxs-lookup"><span data-stu-id="eaff9-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a><span data-ttu-id="eaff9-145">外部資料表考量</span><span class="sxs-lookup"><span data-stu-id="eaff9-145">External Table Considerations</span></span>
<span data-ttu-id="eaff9-146">建立外部資料表很簡單，但有一些需要 toobe 所討論的細節。</span><span class="sxs-lookup"><span data-stu-id="eaff9-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="eaff9-147">使用 PolyBase 載入資料屬於強型別。</span><span class="sxs-lookup"><span data-stu-id="eaff9-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="eaff9-148">這表示每個資料列的 hello 所內嵌的資料必須滿足 hello 資料表結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="eaff9-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="eaff9-149">如果給定的資料列與 hello 結構描述定義不相符，hello 負載拒絕 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="eaff9-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="eaff9-150">hello REJECT_TYPE 但 REJECT_VALUE 選項可讓您 toodefine 多少資料列或 hello 資料的百分比必須存在於 hello 最後的資料表。</span><span class="sxs-lookup"><span data-stu-id="eaff9-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="eaff9-151">在載入期間，如果到達 hello 拒絕值時，hello 載入會失敗。</span><span class="sxs-lookup"><span data-stu-id="eaff9-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="eaff9-152">hello 的已拒絕的資料列的最常見原因是結構描述定義不相符。</span><span class="sxs-lookup"><span data-stu-id="eaff9-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="eaff9-153">例如，如果資料行未正確指定 int hello 結構描述字串 hello 檔案中的 hello 資料時，每個資料列將會失敗 tooload。</span><span class="sxs-lookup"><span data-stu-id="eaff9-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="eaff9-154">hello 位置指定您想要從 tooread 資料 hello 最上層目錄。</span><span class="sxs-lookup"><span data-stu-id="eaff9-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="eaff9-155">在此情況下，如果沒有下 /DimProduct/ PolyBase 子目錄會匯入 hello 子目錄內的所有 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="eaff9-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="eaff9-156">將資料載入 hello</span><span class="sxs-lookup"><span data-stu-id="eaff9-156">Load hello data</span></span>
<span data-ttu-id="eaff9-157">從 Azure Data Lake Store tooload 資料使用 hello [CREATE TABLE AS SELECT (TRANSACT-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)]陳述式。</span><span class="sxs-lookup"><span data-stu-id="eaff9-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="eaff9-158">載入 CTAS 搭配使用 hello 強型別已建立的外部資料表。</span><span class="sxs-lookup"><span data-stu-id="eaff9-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="eaff9-159">CTAS 建立新的資料表，並填入 hello select 陳述式的結果。</span><span class="sxs-lookup"><span data-stu-id="eaff9-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="eaff9-160">CTAS 定義新資料表 toohave hello hello 相同資料行和資料類型，如 hello hello 結果 select 陳述式。</span><span class="sxs-lookup"><span data-stu-id="eaff9-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="eaff9-161">如果您從外部資料表選取 hello 的所有資料行，hello 新資料表會是 hello 外部資料表中的 hello 資料行和資料類型的複本。</span><span class="sxs-lookup"><span data-stu-id="eaff9-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="eaff9-162">在此範例中，我們會從我們的外部資料表 DimProduct_external 建立一個名為 DimProduct 的雜湊分散式資料表。</span><span class="sxs-lookup"><span data-stu-id="eaff9-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="eaff9-163">最佳化資料行存放區壓縮</span><span class="sxs-lookup"><span data-stu-id="eaff9-163">Optimize columnstore compression</span></span>
<span data-ttu-id="eaff9-164">根據預設，SQL 資料倉儲會儲存 hello 資料表作為叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="eaff9-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="eaff9-165">載入完成後，部分 hello 資料的資料列可能會不壓縮成 hello 資料行存放區。</span><span class="sxs-lookup"><span data-stu-id="eaff9-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="eaff9-166">有許多原因會導致發生此情況。</span><span class="sxs-lookup"><span data-stu-id="eaff9-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="eaff9-167">詳細資訊，請參閱 toolearn[管理資料行存放區索引][manage columnstore indexes]。</span><span class="sxs-lookup"><span data-stu-id="eaff9-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="eaff9-168">toooptimize 查詢效能和負載之後, 的資料行存放區壓縮重建 hello 資料表 tooforce hello 資料行存放區索引 toocompress hello 的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="eaff9-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="eaff9-169">如需維護資料行存放區索引的詳細資訊，請參閱 hello[管理資料行存放區索引][ manage columnstore indexes]發行項。</span><span class="sxs-lookup"><span data-stu-id="eaff9-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="eaff9-170">最佳化統計資料</span><span class="sxs-lookup"><span data-stu-id="eaff9-170">Optimize statistics</span></span>
<span data-ttu-id="eaff9-171">載入之後立即是最佳的 toocreate 單一資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="eaff9-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="eaff9-172">針對統計資料，您將會有一些選項。</span><span class="sxs-lookup"><span data-stu-id="eaff9-172">There are some choices for statistics.</span></span> <span data-ttu-id="eaff9-173">例如，如果您在每個資料行上建立單一資料行統計資料可能需要很長的時間 toorebuild hello 的所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="eaff9-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="eaff9-174">如果您知道特定資料行不會成為 toobe 查詢述詞中的，您可以跳建立統計資料，這些資料行。</span><span class="sxs-lookup"><span data-stu-id="eaff9-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="eaff9-175">如果您決定 toocreate 每個資料表的每個資料行的單一資料行統計資料，您可以使用 hello 預存程序程式碼範例`prc_sqldw_create_stats`在 hello[統計資料][ statistics]發行項。</span><span class="sxs-lookup"><span data-stu-id="eaff9-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="eaff9-176">下列範例中的 hello 是很好的起點建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="eaff9-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="eaff9-177">在 hello 維度資料表中，每個資料行和 hello 事實資料表中每個聯結資料行，它會建立單一資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="eaff9-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="eaff9-178">您可以在稍後新增單一或多個資料行統計資料 tooother 事實資料表資料行。</span><span class="sxs-lookup"><span data-stu-id="eaff9-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="eaff9-179">成就解鎖！</span><span class="sxs-lookup"><span data-stu-id="eaff9-179">Achievement unlocked!</span></span>
<span data-ttu-id="eaff9-180">您已成功將資料載入到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="eaff9-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="eaff9-181">太棒了！</span><span class="sxs-lookup"><span data-stu-id="eaff9-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="eaff9-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eaff9-182">Next Steps</span></span>
<span data-ttu-id="eaff9-183">載入資料是第一個步驟 toodeveloping hello 使用 SQL 資料倉儲的資料倉儲方案。</span><span class="sxs-lookup"><span data-stu-id="eaff9-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="eaff9-184">請查看我們在[資料表](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview)和 [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md) 上提供的開發資源。</span><span class="sxs-lookup"><span data-stu-id="eaff9-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
