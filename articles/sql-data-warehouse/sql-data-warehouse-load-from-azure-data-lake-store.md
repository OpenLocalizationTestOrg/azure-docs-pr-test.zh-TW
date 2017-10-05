---
title: "載入 - Azure Data Lake Store 到 SQL 資料倉儲 | Microsoft Docs"
description: "了解如何使用 PolyBase 外部資料表將資料從 Azure Data Lake Store 載入到 Azure SQL 資料倉儲。"
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
ms.openlocfilehash: ab951c30aae0d4afdd931e245f25d4645bba1681
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="47b27-103">將資料從 Azure Data Lake Store 載入到 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="47b27-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="47b27-104">本文件說明使用 PolyBase 將您自己的資料從 Azure Data Lake Store (ADLS) 載入到 SQL 資料倉儲時需要執行的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="47b27-104">This document gives you all steps you  need to load your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="47b27-105">雖然您能夠使用外部資料表對 ADLS 中儲存的資料執行臨機操作查詢，但是我們建議的最佳做法是將資料匯入到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="47b27-105">While you are able to run adhoc queries over the data stored in ADLS using the External Tables, as a best practice we suggest importing the data into the SQL Data Warehouse.</span></span>
<span data-ttu-id="47b27-106">預估時間：假設您有完成作業之必要條件的情況下，所需時間為 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="47b27-106">Time Estimate: 10 minutes assuming you have the prerequisites need to complete.</span></span>
<span data-ttu-id="47b27-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="47b27-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="47b27-108">建立要從 Azure Data Lake Store 載入的外部資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="47b27-108">Create External Database objects to load from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="47b27-109">連接到 Azure Data Lake Store 目錄。</span><span class="sxs-lookup"><span data-stu-id="47b27-109">Connect to an Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="47b27-110">將資料載入到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="47b27-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="47b27-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="47b27-111">Before you begin</span></span>
<span data-ttu-id="47b27-112">若要執行此教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="47b27-112">To run this tutorial, you need:</span></span>

* <span data-ttu-id="47b27-113">Azure Active Directory 應用程式，用於服務對服務驗證。</span><span class="sxs-lookup"><span data-stu-id="47b27-113">Azure Active Directory Application to use for Service-to-Service authentication.</span></span> <span data-ttu-id="47b27-114">若要建立，請依照 [Active Directory 驗證](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)中的指示執行</span><span class="sxs-lookup"><span data-stu-id="47b27-114">To create, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="47b27-115">您需要 Active Directory 應用程式的用戶端識別碼、金鑰及 OAuth2.0 Token 端點值，以便從 SQL 資料倉儲連接到 Azure Data Lake。</span><span class="sxs-lookup"><span data-stu-id="47b27-115">You need the client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application to connect to your Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="47b27-116">上面的連結提供如何取得這些值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="47b27-116">Details for how to get these values are in the link above.</span></span>
><span data-ttu-id="47b27-117">請注意，Azure Active Directory 應用程式註冊使用「應用程式識別碼」作為「用 戶端」。</span><span class="sxs-lookup"><span data-stu-id="47b27-117">Note for Azure Active Directory App Registration use the 'Application ID' as the Client ID.</span></span>

* <span data-ttu-id="47b27-118">SQL Server Management Studio 或 SQL Server Data Tools，用來下載 SSMS 和連接，請參閱[查詢 SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="47b27-118">SQL Server Management Studio or SQL Server Data Tools, to download SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="47b27-119">一個 Azure SQL 資料倉儲，若要建立一個，請依照下列連結中的指示執行：https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="47b27-119">An Azure SQL Data Warehouse, to create one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="47b27-120">一個啟用或未啟用加密的 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="47b27-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="47b27-121">若要建立一個，請依照下列連結中的指示執行：https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="47b27-121">To create one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-the-data-source"></a><span data-ttu-id="47b27-122">設定資料來源</span><span class="sxs-lookup"><span data-stu-id="47b27-122">Configure the data source</span></span>
<span data-ttu-id="47b27-123">PolyBase 使用 T-SQL 外部物件以定義外部資料的位置和屬性。</span><span class="sxs-lookup"><span data-stu-id="47b27-123">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="47b27-124">外部物件儲存在 SQL 資料倉儲中，而且它會參考儲存在外部的資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-124">The external objects are stored in SQL Data Warehouse and reference the data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="47b27-125">建立認證</span><span class="sxs-lookup"><span data-stu-id="47b27-125">Create a credential</span></span>
<span data-ttu-id="47b27-126">若要存取您的 Azure Data Lake Store，您將需要建立一個資料庫主要金鑰，以加密要在下一個步驟中使用的認證密碼。</span><span class="sxs-lookup"><span data-stu-id="47b27-126">To access your Azure Data Lake Store, you will need to create a Database Master Key to encrypt your credential secret used in the next step.</span></span>
<span data-ttu-id="47b27-127">接著，您必須建立資料庫範圍認證，其中儲存了在 AAD 中設定的服務主體認證。</span><span class="sxs-lookup"><span data-stu-id="47b27-127">You then create a Database scoped credential, which stores the service principal credentials set up in AAD.</span></span> <span data-ttu-id="47b27-128">對於使用 PolyBase 連接到 Windows Azure 儲存體 Blob 的人來說，請注意認證語法是不同的。</span><span class="sxs-lookup"><span data-stu-id="47b27-128">For those of you who have used PolyBase to connect to Windows Azure Storage Blobs, note that the credential syntax is different.</span></span>
<span data-ttu-id="47b27-129">若要連線到 Azure Data Lake Store，您必須**先**建立 Azure Active Directory 應用程式、建立存取金鑰，並對應用程式授與 Azure Data Lake 資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="47b27-129">To connect to Azure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant the application access to the Azure Data Lake resource.</span></span> <span data-ttu-id="47b27-130">這些步驟的執行指示位於[這裡](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)。</span><span class="sxs-lookup"><span data-stu-id="47b27-130">Instrucitons to perform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass the client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
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


### <a name="create-the-external-data-source"></a><span data-ttu-id="47b27-131">建立外部資料來源</span><span class="sxs-lookup"><span data-stu-id="47b27-131">Create the external data source</span></span>
<span data-ttu-id="47b27-132">使用此 [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] 命令以儲存資料的位置及類型。</span><span class="sxs-lookup"><span data-stu-id="47b27-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span>
<span data-ttu-id="47b27-133">您可以在 Azure 入口網站和 www.portal.azure.com 中找到 ADL URI。</span><span class="sxs-lookup"><span data-stu-id="47b27-133">You can find the ADL URI in the Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="47b27-134">設定資料格式</span><span class="sxs-lookup"><span data-stu-id="47b27-134">Configure data format</span></span>
<span data-ttu-id="47b27-135">若要從 ADLS 匯入資料，您需要指定外部檔案格式。</span><span class="sxs-lookup"><span data-stu-id="47b27-135">To import the data from ADLS, you need to specify the external file format.</span></span> <span data-ttu-id="47b27-136">這個命令有特定的格式選項，用以描述您的資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-136">This command has format-specific options to describe your data.</span></span>
<span data-ttu-id="47b27-137">以下是常用檔案格式的範例，它是一個以管線符號分隔的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="47b27-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="47b27-138">請查閱我們的 T-SQL 文件，以取得 [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] 的完整清單</span><span class="sxs-lookup"><span data-stu-id="47b27-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks the end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies the field terminator for data of type string in the text-delimited file.
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

## <a name="create-the-external-tables"></a><span data-ttu-id="47b27-139">建立外部資料表</span><span class="sxs-lookup"><span data-stu-id="47b27-139">Create the external tables</span></span>
<span data-ttu-id="47b27-140">您在指定資料來源和檔案格式之後，便可以開始建立外部資料表。</span><span class="sxs-lookup"><span data-stu-id="47b27-140">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> <span data-ttu-id="47b27-141">外部資料表是您與外部資料進行互動的方式。</span><span class="sxs-lookup"><span data-stu-id="47b27-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="47b27-142">PolyBase 使用遞迴目錄周遊，來讀取在位置參數中指定之目錄下所有子目錄中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="47b27-142">PolyBase uses recursive directory traversal to read all files in all subdirectories of the directory specified in the location parameter.</span></span> <span data-ttu-id="47b27-143">此外，下列範例將示範如何建立物件。</span><span class="sxs-lookup"><span data-stu-id="47b27-143">Also, the following example shows how to create the object.</span></span> <span data-ttu-id="47b27-144">您需要自訂陳述式，以處理 ADLS 中的資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-144">You need to customize the statement to work with the data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under the ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object to use.
-- FILE_FORMAT: Specifies which File Format Object to use
-- REJECT_TYPE: Specifies how you want to deal with rejected rows. Either Value or percentage of the total
-- REJECT_VALUE: Sets the Reject value based on the reject type.

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

## <a name="external-table-considerations"></a><span data-ttu-id="47b27-145">外部資料表考量</span><span class="sxs-lookup"><span data-stu-id="47b27-145">External Table Considerations</span></span>
<span data-ttu-id="47b27-146">建立外部資料表很簡單，但是有一些必須討論的細微差異。</span><span class="sxs-lookup"><span data-stu-id="47b27-146">Creating an external table is easy, but there are some nuances that need to be discussed.</span></span>

<span data-ttu-id="47b27-147">使用 PolyBase 載入資料屬於強型別。</span><span class="sxs-lookup"><span data-stu-id="47b27-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="47b27-148">這表示內嵌的每個資料列都必須滿足資料表結構描述定義。</span><span class="sxs-lookup"><span data-stu-id="47b27-148">This means that each row of the data being ingested must satisfy the table schema definition.</span></span>
<span data-ttu-id="47b27-149">如果指定的資料列不符合結構描述定義，載入時就會拒絕該列。</span><span class="sxs-lookup"><span data-stu-id="47b27-149">If a given row does not match the schema definition, the row is rejected from the load.</span></span>

<span data-ttu-id="47b27-150">REJECT_TYPE 和 REJECT_VALUE 選項可讓您定義最終的資料表中必須出現多少資料列或多少百分比的資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-150">The REJECT_TYPE and REJECT_VALUE options allow you to define how many rows or what percentage of the data must be present in the final table.</span></span>
<span data-ttu-id="47b27-151">在載入期間，如果達到拒絕值，載入即失敗。</span><span class="sxs-lookup"><span data-stu-id="47b27-151">During load, if the reject value is reached, the load fails.</span></span> <span data-ttu-id="47b27-152">資料列遭拒最常見的原因是結構描述定義不相符。</span><span class="sxs-lookup"><span data-stu-id="47b27-152">The most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="47b27-153">例如，如果檔案中的資料是字串，卻對資料行指定不正確的整數結構描述，則會無法載入每個資料列。</span><span class="sxs-lookup"><span data-stu-id="47b27-153">For example, if a column is incorrectly given the schema of int when the data in the file is a string, every row will fail to load.</span></span>

<span data-ttu-id="47b27-154">[位置] 會指定您想要開始讀取資料的最上層目錄。</span><span class="sxs-lookup"><span data-stu-id="47b27-154">The Location specifies the topmost directory that you want to read data from.</span></span>
<span data-ttu-id="47b27-155">在此案例中，如果 /DimProduct/ 下面有子目錄，PolyBase 將匯入子目錄內的所有資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all the data within the subdirectories.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="47b27-156">載入資料</span><span class="sxs-lookup"><span data-stu-id="47b27-156">Load the data</span></span>
<span data-ttu-id="47b27-157">若要從 Azure Data Lake Store 載入資料，請使用 [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] 陳述式。</span><span class="sxs-lookup"><span data-stu-id="47b27-157">To load data from Azure Data Lake Store use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="47b27-158">使用 CTAS 執行載入作業會使用您已建立的強型別外部資料表。</span><span class="sxs-lookup"><span data-stu-id="47b27-158">Loading with CTAS uses the strongly typed external table you have created.</span></span>

<span data-ttu-id="47b27-159">CTAS 建立新的資料表，並將選取陳述式的結果填入該資料表。</span><span class="sxs-lookup"><span data-stu-id="47b27-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="47b27-160">CTAS 定義新資料表，以使它擁有和選取陳述式之結果相同的資料行和資料類型。</span><span class="sxs-lookup"><span data-stu-id="47b27-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="47b27-161">如果您選取外部資料表上的所有資料行，則新資料表會是外部資料表中資料行和資料類型的複本。</span><span class="sxs-lookup"><span data-stu-id="47b27-161">If you select all the columns from an external table, the new table is a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="47b27-162">在此範例中，我們會從我們的外部資料表 DimProduct_external 建立一個名為 DimProduct 的雜湊分散式資料表。</span><span class="sxs-lookup"><span data-stu-id="47b27-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="47b27-163">最佳化資料行存放區壓縮</span><span class="sxs-lookup"><span data-stu-id="47b27-163">Optimize columnstore compression</span></span>
<span data-ttu-id="47b27-164">根據預設，SQL 資料倉儲會將資料表儲存為叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="47b27-164">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="47b27-165">載入完成後，某些資料列可能不會被壓縮為資料行存放區。</span><span class="sxs-lookup"><span data-stu-id="47b27-165">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="47b27-166">有許多原因會導致發生此情況。</span><span class="sxs-lookup"><span data-stu-id="47b27-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="47b27-167">若要深入了解，請參閱[管理資料行存放區索引][manage columnstore indexes]。</span><span class="sxs-lookup"><span data-stu-id="47b27-167">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="47b27-168">若要最佳化載入後的查詢效能和資料行存放區壓縮，請重建資料表以強制資料行存放區索引對所有資料列進行壓縮。</span><span class="sxs-lookup"><span data-stu-id="47b27-168">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="47b27-169">如需維護資料行存放區索引的詳細資訊，請參閱[管理資料行存放區索引][manage columnstore indexes]一文。</span><span class="sxs-lookup"><span data-stu-id="47b27-169">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="47b27-170">最佳化統計資料</span><span class="sxs-lookup"><span data-stu-id="47b27-170">Optimize statistics</span></span>
<span data-ttu-id="47b27-171">您最好在載入後立刻建立單一資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-171">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="47b27-172">針對統計資料，您將會有一些選項。</span><span class="sxs-lookup"><span data-stu-id="47b27-172">There are some choices for statistics.</span></span> <span data-ttu-id="47b27-173">例如，如果您在每個資料行上建立單一資料行統計資料，可能會需要很長的時間才能重建所有統計資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-173">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="47b27-174">如果您知道某些資料行不會被包含在查詢述詞中，您可以略過為那些資料行建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-174">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="47b27-175">如果您決定要在每個資料表的每個資料行上建立單一資料行統計資料，您可以使用[統計資料][statistics]一文中的預存程序程式碼範例 `prc_sqldw_create_stats`。</span><span class="sxs-lookup"><span data-stu-id="47b27-175">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="47b27-176">下列範例為建立統計資料的好起點。</span><span class="sxs-lookup"><span data-stu-id="47b27-176">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="47b27-177">它會在維度資料表中的每個資料行上，以及在事實資料表中的每個聯結資料行上建立單一資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="47b27-177">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="47b27-178">您之後隨時可以將單一或多個資料行統計資料新增到其他事實資料表資料行上。</span><span class="sxs-lookup"><span data-stu-id="47b27-178">You can always add single or multi-column statistics to other fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="47b27-179">成就解鎖！</span><span class="sxs-lookup"><span data-stu-id="47b27-179">Achievement unlocked!</span></span>
<span data-ttu-id="47b27-180">您已成功將資料載入到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="47b27-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="47b27-181">太棒了！</span><span class="sxs-lookup"><span data-stu-id="47b27-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="47b27-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47b27-182">Next Steps</span></span>
<span data-ttu-id="47b27-183">載入資料是開發使用 SQL 資料倉儲之資料倉儲解決方案的第一步。</span><span class="sxs-lookup"><span data-stu-id="47b27-183">Loading data is the first step to developing a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="47b27-184">請查看我們在[資料表](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview)和 [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md) 上提供的開發資源。</span><span class="sxs-lookup"><span data-stu-id="47b27-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
