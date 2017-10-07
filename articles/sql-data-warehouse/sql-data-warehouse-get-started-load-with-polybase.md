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
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="fd2fc-103">在 SQL 資料倉儲中使用 PolyBase 載入資料</span><span class="sxs-lookup"><span data-stu-id="fd2fc-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd2fc-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="fd2fc-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="fd2fc-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="fd2fc-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="fd2fc-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="fd2fc-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="fd2fc-107">BCP</span><span class="sxs-lookup"><span data-stu-id="fd2fc-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="fd2fc-108">本教學課程示範如何使用 AzCopy 和 PolyBase 的 SQL 資料倉儲 tooload 資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="fd2fc-109">課程結束後，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="fd2fc-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="fd2fc-110">使用 AzCopy toocopy 資料 tooAzure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="fd2fc-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="fd2fc-111">建立資料庫物件 toodefine hello 資料</span><span class="sxs-lookup"><span data-stu-id="fd2fc-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="fd2fc-112">執行 T-SQL 查詢 tooload hello 資料</span><span class="sxs-lookup"><span data-stu-id="fd2fc-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="fd2fc-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="fd2fc-113">Prerequisites</span></span>
<span data-ttu-id="fd2fc-114">您必須完成本教學課程 toostep，</span><span class="sxs-lookup"><span data-stu-id="fd2fc-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="fd2fc-115">SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="fd2fc-116">類型為標準本地備援儲存體 (標準 LRS)、標準異地備援儲存體 (標準 GRS) 或標準讀取存取異地備援儲存體 (標準 RAGRS) 的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="fd2fc-117">AzCopy 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="fd2fc-118">下載並安裝 hello[最新版本的 AzCopy] [ latest version of AzCopy]以 hello Microsoft Azure 儲存體 Tools 安裝。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Azure 儲存體工具](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="fd2fc-120">步驟 1： 加入範例資料 tooAzure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="fd2fc-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="fd2fc-121">在訂單 tooload 資料，我們需要 tooput 一些範例資料到 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="fd2fc-122">在此步驟中，我們會在 Azure 儲存體 Blob 中填入範例資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="fd2fc-123">更新版本中，我們將使用 PolyBase tooload 此範例資料插入 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="fd2fc-124">A.</span><span class="sxs-lookup"><span data-stu-id="fd2fc-124">A.</span></span> <span data-ttu-id="fd2fc-125">準備範例文字檔</span><span class="sxs-lookup"><span data-stu-id="fd2fc-125">Prepare a sample text file</span></span>
<span data-ttu-id="fd2fc-126">tooprepare 範例文字檔案：</span><span class="sxs-lookup"><span data-stu-id="fd2fc-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="fd2fc-127">開啟 [記事本] 及複製到新的檔案之後的資料行的 hello。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="fd2fc-128">為 %temp%\dimdate2.txt 儲存此 tooyour 本機暫存目錄。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="fd2fc-129">B.</span><span class="sxs-lookup"><span data-stu-id="fd2fc-129">B.</span></span> <span data-ttu-id="fd2fc-130">尋找您的 Blob 服務端點</span><span class="sxs-lookup"><span data-stu-id="fd2fc-130">Find your blob service endpoint</span></span>
<span data-ttu-id="fd2fc-131">toofind blob 服務端點：</span><span class="sxs-lookup"><span data-stu-id="fd2fc-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="fd2fc-132">從 hello Azure 入口網站選取**瀏覽** > **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="fd2fc-133">按一下您想 toouse hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="fd2fc-134">在 hello 儲存體帳戶刀鋒視窗中，按一下 Blob</span><span class="sxs-lookup"><span data-stu-id="fd2fc-134">In hello Storage account blade, click Blobs</span></span>
   
    ![按一下 Blob](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="fd2fc-136">儲存您的 Blob 服務端點 URL，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Blob 服務端點](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="fd2fc-138">C.</span><span class="sxs-lookup"><span data-stu-id="fd2fc-138">C.</span></span> <span data-ttu-id="fd2fc-139">找出您的 Azure 儲存體金鑰</span><span class="sxs-lookup"><span data-stu-id="fd2fc-139">Find your Azure storage key</span></span>
<span data-ttu-id="fd2fc-140">toofind Azure 儲存體金鑰：</span><span class="sxs-lookup"><span data-stu-id="fd2fc-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="fd2fc-141">Hello Azure 入口網站，從選取**瀏覽** > **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="fd2fc-142">按一下您想 toouse hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="fd2fc-143">選取 [所有設定] > [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="fd2fc-144">按一下 hello 複製方塊 toocopy toohello 剪貼簿存取金鑰的其中一個。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![複製 Azure 儲存體金鑰](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="fd2fc-146">D.</span><span class="sxs-lookup"><span data-stu-id="fd2fc-146">D.</span></span> <span data-ttu-id="fd2fc-147">複製 hello 範例檔案 tooAzure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="fd2fc-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="fd2fc-148">toocopy 資料 tooAzure blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="fd2fc-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="fd2fc-149">開啟命令提示字元，並變更目錄 toohello AzCopy 安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="fd2fc-150">此命令會變更 toohello 預設 64 位元的 Windows 用戶端上的安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="fd2fc-151">執行下列命令 tooupload hello 檔 hello。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="fd2fc-152">針對 <blob service endpoint URL> 指定 Blob 服務端點 URL，並針對 <azure_storage_account_key> 指定 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="fd2fc-153">另請參閱[開始使用 AzCopy 命令列公用程式的 hello][Getting Started with hello AzCopy Command-Line Utility]。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="fd2fc-154">E.</span><span class="sxs-lookup"><span data-stu-id="fd2fc-154">E.</span></span> <span data-ttu-id="fd2fc-155">瀏覽 Blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="fd2fc-155">Explore your blob storage container</span></span>
<span data-ttu-id="fd2fc-156">您上傳 tooblob 儲存體 toosee hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="fd2fc-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="fd2fc-157">返回 tooyour Blob 服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="fd2fc-158">在 [容器] 下，按兩下 [資料容器] 。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="fd2fc-159">tooexplore hello 路徑 tooyour 資料按一下 hello 資料夾**datedimension** ，您會看到您上傳的檔案**DimDate2.txt**。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="fd2fc-160">tooview 內容，然後按一下**DimDate2.txt**。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="fd2fc-161">請注意，在 hello Blob 屬性刀鋒視窗中，您可以下載或刪除 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![檢視 Azure 儲存體 Blob](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="fd2fc-163">步驟 2： 建立 hello 範例資料的外部資料表</span><span class="sxs-lookup"><span data-stu-id="fd2fc-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="fd2fc-164">本節中，我們會建立定義 hello 範例資料的外部資料表。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="fd2fc-165">PolyBase 會在 Azure blob 儲存體中使用外部資料表 tooaccess 資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="fd2fc-166">因為 hello 資料不會儲存 SQL 資料倉儲內，PolyBase 會處理驗證 toohello 外部資料使用的資料庫範圍認證。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="fd2fc-167">在此步驟中的 hello 範例會使用這些 TRANSACT-SQL 陳述式 toocreate 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="fd2fc-168">[建立主要金鑰 (TRANSACT-SQL)] [ Create Master Key (Transact-SQL)] tooencrypt hello 密碼，您的資料庫範圍認證。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="fd2fc-169">[建立資料庫範圍認證 (TRANSACT-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify 驗證您的 Azure 儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="fd2fc-170">[建立外部資料來源 (TRANSACT-SQL)] [ Create External Data Source (Transact-SQL)] toospecify hello 位置，您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="fd2fc-171">[建立外部檔案格式 (TRANSACT-SQL)] [ Create External File Format (Transact-SQL)] toospecify hello 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="fd2fc-172">[建立外部資料表 (TRANSACT-SQL)] [ Create External Table (Transact-SQL)] toospecify hello 資料表定義和位置 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="fd2fc-173">對 SQL 資料倉儲資料庫執行這個查詢。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="fd2fc-174">它會建立具名 DimDate2External toohello DimDate2.txt 範例資料點 hello Azure blob 儲存體中的 hello dbo 結構描述中的外部資料表。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


<span data-ttu-id="fd2fc-175">在 Visual Studio 中的 SQL Server 物件總管，您可以看到 hello 外部檔案格式、 外部資料來源，以及 hello DimDate2External 資料表。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![檢視外部資料表](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="fd2fc-177">步驟 3：將資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="fd2fc-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="fd2fc-178">Hello 外部資料表建立之後，您可以 hello 資料載入新的資料表，或將其插入到現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="fd2fc-179">tooload hello 資料到新資料表，執行 hello [CREATE TABLE AS SELECT (TRANSACT-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)]陳述式。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="fd2fc-180">hello 新資料表會有命名 hello 查詢中的 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="fd2fc-181">hello hello 資料行資料類型會比 hello 外部資料表定義中的 hello 資料類型。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="fd2fc-182">tooload hello 資料到現有資料表中，使用 hello [INSERT...選取 (TRANSACT-SQL)] [ INSERT...SELECT (Transact-SQL)]陳述式。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

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

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="fd2fc-183">步驟 4：建立新載入資料的統計資料</span><span class="sxs-lookup"><span data-stu-id="fd2fc-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="fd2fc-184">SQL 資料倉儲不會自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="fd2fc-185">因此，tooachieve 高的查詢效能，務必先載入 toocreate hello 之後每個資料表的每個資料行的統計資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="fd2fc-186">它也是在 hello 資料大量變更後重要 tooupdate 統計資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="fd2fc-187">此範例 hello 新 DimDate2 資料表上建立單一資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="fd2fc-188">詳細資訊，請參閱 toolearn[統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="fd2fc-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd2fc-189">Next steps</span></span>
<span data-ttu-id="fd2fc-190">請參閱 hello [PolyBase 指南][ PolyBase guide]進一步開發使用 PolyBase 的解決方案時，您應該知道的資訊。</span><span class="sxs-lookup"><span data-stu-id="fd2fc-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

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
