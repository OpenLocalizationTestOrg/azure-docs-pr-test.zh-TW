---
title: "SQL 資料倉儲中的 PolyBase 教學課程 | Microsoft Docs"
description: "瞭解 PolyBase 是什麼及如何用於資料倉儲案例。"
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
ms.openlocfilehash: 1a26fe127448f794bbad11043aa3c8770bc2ac8c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="1e145-103">在 SQL 資料倉儲中使用 PolyBase 載入資料</span><span class="sxs-lookup"><span data-stu-id="1e145-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e145-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="1e145-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="1e145-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="1e145-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="1e145-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="1e145-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="1e145-107">BCP</span><span class="sxs-lookup"><span data-stu-id="1e145-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="1e145-108">本教學課程示範如何使用 AzCopy 和 PolyBase 將資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="1e145-108">This tutorial shows how to load data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="1e145-109">課程結束後，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="1e145-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="1e145-110">使用 AzCopy 將資料複製到 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="1e145-110">Use AzCopy to copy data to Azure blob storage</span></span>
* <span data-ttu-id="1e145-111">建立資料庫物件以定義資料</span><span class="sxs-lookup"><span data-stu-id="1e145-111">Create database objects to define the data</span></span>
* <span data-ttu-id="1e145-112">執行 T-SQL 查詢以載入資料</span><span class="sxs-lookup"><span data-stu-id="1e145-112">Run a T-SQL query to load the data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1e145-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="1e145-113">Prerequisites</span></span>
<span data-ttu-id="1e145-114">若要逐步執行本教學課程，您需要</span><span class="sxs-lookup"><span data-stu-id="1e145-114">To step through this tutorial, you need</span></span>

* <span data-ttu-id="1e145-115">SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e145-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="1e145-116">類型為標準本地備援儲存體 (標準 LRS)、標準異地備援儲存體 (標準 GRS) 或標準讀取存取異地備援儲存體 (標準 RAGRS) 的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e145-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="1e145-117">AzCopy 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="1e145-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="1e145-118">下載並安裝[最新版 AzCopy][latest version of AzCopy]，此公用程式會隨 Microsoft Azure 儲存體工具一起安裝。</span><span class="sxs-lookup"><span data-stu-id="1e145-118">Download and install the [latest version of AzCopy][latest version of AzCopy] which is installed with the Microsoft Azure Storage Tools.</span></span>
  
    ![Azure 儲存體工具](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-to-azure-blob-storage"></a><span data-ttu-id="1e145-120">步驟 1：將範例資料新增至 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="1e145-120">Step 1: Add sample data to Azure blob storage</span></span>
<span data-ttu-id="1e145-121">為了載入資料，我們需要在 Azure Blob 儲存體中放入一些範例資料。</span><span class="sxs-lookup"><span data-stu-id="1e145-121">In order to load data, we need to put some sample data into an Azure blob storage.</span></span> <span data-ttu-id="1e145-122">在此步驟中，我們會在 Azure 儲存體 Blob 中填入範例資料。</span><span class="sxs-lookup"><span data-stu-id="1e145-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="1e145-123">稍後，我們將使用 PolyBase 將此範例資料載入 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e145-123">Later, we will use PolyBase to load this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="1e145-124">A.</span><span class="sxs-lookup"><span data-stu-id="1e145-124">A.</span></span> <span data-ttu-id="1e145-125">準備範例文字檔</span><span class="sxs-lookup"><span data-stu-id="1e145-125">Prepare a sample text file</span></span>
<span data-ttu-id="1e145-126">若要準備範例文字檔：</span><span class="sxs-lookup"><span data-stu-id="1e145-126">To prepare a sample text file:</span></span>

1. <span data-ttu-id="1e145-127">開啟 [記事本]，並將下列幾行資料複製到新的檔案。</span><span class="sxs-lookup"><span data-stu-id="1e145-127">Open Notepad and copy the following lines of data into a new file.</span></span> <span data-ttu-id="1e145-128">將此檔案儲存到本機暫存目錄 %temp%\DimDate2.txt。</span><span class="sxs-lookup"><span data-stu-id="1e145-128">Save this to your local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="1e145-129">B.</span><span class="sxs-lookup"><span data-stu-id="1e145-129">B.</span></span> <span data-ttu-id="1e145-130">尋找您的 Blob 服務端點</span><span class="sxs-lookup"><span data-stu-id="1e145-130">Find your blob service endpoint</span></span>
<span data-ttu-id="1e145-131">若要尋找您的 Blob 服務端點：</span><span class="sxs-lookup"><span data-stu-id="1e145-131">To find your blob service endpoint:</span></span>

1. <span data-ttu-id="1e145-132">從 Azure 入口網站選取 [瀏覽] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="1e145-132">From the Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="1e145-133">按一下您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e145-133">Click the storage account you want to use.</span></span>
3. <span data-ttu-id="1e145-134">在儲存體帳戶刀鋒視窗中，按一下 [Blob]。</span><span class="sxs-lookup"><span data-stu-id="1e145-134">In the Storage account blade, click Blobs</span></span>
   
    ![按一下 Blob](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="1e145-136">儲存您的 Blob 服務端點 URL，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="1e145-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Blob 服務端點](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="1e145-138">C.</span><span class="sxs-lookup"><span data-stu-id="1e145-138">C.</span></span> <span data-ttu-id="1e145-139">找出您的 Azure 儲存體金鑰</span><span class="sxs-lookup"><span data-stu-id="1e145-139">Find your Azure storage key</span></span>
<span data-ttu-id="1e145-140">若要找出您的 Azure 儲存體金鑰：</span><span class="sxs-lookup"><span data-stu-id="1e145-140">To find your Azure storage key:</span></span>

1. <span data-ttu-id="1e145-141">從 Azure 入口網站選取 [瀏覽] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="1e145-141">From the Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="1e145-142">按一下您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e145-142">Click on the storage account you want to use.</span></span>
3. <span data-ttu-id="1e145-143">選取 [所有設定] > [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="1e145-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="1e145-144">按一下複製方塊，將其中一個存取金鑰複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="1e145-144">Click the copy box to copy one of your access keys to the clipboard.</span></span>
   
    ![複製 Azure 儲存體金鑰](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-the-sample-file-to-azure-blob-storage"></a><span data-ttu-id="1e145-146">D.</span><span class="sxs-lookup"><span data-stu-id="1e145-146">D.</span></span> <span data-ttu-id="1e145-147">將範例檔案複製到 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="1e145-147">Copy the sample file to Azure blob storage</span></span>
<span data-ttu-id="1e145-148">若要將資料複製到 Azure Blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="1e145-148">To copy your data to Azure blob storage:</span></span>

1. <span data-ttu-id="1e145-149">開啟命令提示字元，切換至 AzCopy 安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="1e145-149">Open a command prompt, and change directories to the AzCopy installation directory.</span></span> <span data-ttu-id="1e145-150">此命令會切換至 64 位元 Windows 用戶端上的預設安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="1e145-150">This command changes to the default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="1e145-151">執行下列命令以上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="1e145-151">Run the following command to upload the file.</span></span> <span data-ttu-id="1e145-152">針對 <blob service endpoint URL> 指定 Blob 服務端點 URL，並針對 <azure_storage_account_key> 指定 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="1e145-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="1e145-153">另請參閱[開始使用 AzCopy 命令列公用程式][Getting Started with the AzCopy Command-Line Utility]。</span><span class="sxs-lookup"><span data-stu-id="1e145-153">See also [Getting Started with the AzCopy Command-Line Utility][Getting Started with the AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="1e145-154">E.</span><span class="sxs-lookup"><span data-stu-id="1e145-154">E.</span></span> <span data-ttu-id="1e145-155">瀏覽 Blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="1e145-155">Explore your blob storage container</span></span>
<span data-ttu-id="1e145-156">若要查看您上傳至 Blob 儲存體的檔案：</span><span class="sxs-lookup"><span data-stu-id="1e145-156">To see the file you uploaded to blob storage:</span></span>

1. <span data-ttu-id="1e145-157">回到您的 [Blob 服務] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1e145-157">Go back to your Blob service blade.</span></span>
2. <span data-ttu-id="1e145-158">在 [容器] 下，按兩下 [資料容器] 。</span><span class="sxs-lookup"><span data-stu-id="1e145-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="1e145-159">若要瀏覽資料路徑，請按一下 **datedimension** 資料夾，然後您就會看到所上傳的檔案 **DimDate2.txt**。</span><span class="sxs-lookup"><span data-stu-id="1e145-159">To explore the path to your data, click the folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="1e145-160">若要檢視屬性，請按一下 [DimDate2.txt] 。</span><span class="sxs-lookup"><span data-stu-id="1e145-160">To view properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="1e145-161">請注意，在 [Blob 屬性] 刀鋒視窗中，您可以下載或刪除此檔案。</span><span class="sxs-lookup"><span data-stu-id="1e145-161">Note that in the Blob properties blade, you can download or delete the file.</span></span>
   
    ![檢視 Azure 儲存體 Blob](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-the-sample-data"></a><span data-ttu-id="1e145-163">步驟 2：為範例資料建立外部資料表</span><span class="sxs-lookup"><span data-stu-id="1e145-163">Step 2: Create an external table for the sample data</span></span>
<span data-ttu-id="1e145-164">本節中，我們會建立外部資料表來定義範例資料。</span><span class="sxs-lookup"><span data-stu-id="1e145-164">In this section we create an external table that defines the sample data.</span></span>

<span data-ttu-id="1e145-165">PolyBase 使用外部資料表存取 Azure Blob 儲存體中的資料。</span><span class="sxs-lookup"><span data-stu-id="1e145-165">PolyBase uses external tables to access data in Azure blob storage.</span></span> <span data-ttu-id="1e145-166">因為資料不會儲存在 SQL 資料倉儲內，PolyBase 使用資料庫範圍認證來處理外部資料的驗證。</span><span class="sxs-lookup"><span data-stu-id="1e145-166">Since the data is not stored within SQL Data Warehouse, PolyBase handles authentication to the external data by using a database-scoped credential.</span></span>

<span data-ttu-id="1e145-167">此步驟中的範例使用這些 Transact-SQL 陳述式建立外部資料表。</span><span class="sxs-lookup"><span data-stu-id="1e145-167">The example in this step uses these Transact-SQL statements to create an external table.</span></span>

* <span data-ttu-id="1e145-168">[建立主要金鑰 (Transact-SQL)][Create Master Key (Transact-SQL)]，以加密資料庫範圍認證的密碼。</span><span class="sxs-lookup"><span data-stu-id="1e145-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] to encrypt the secret of your database scoped credential.</span></span>
* <span data-ttu-id="1e145-169">[建立資料庫範圍認證 (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)]，以指定 Azure 儲存體帳戶的驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="1e145-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] to specify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="1e145-170">[建立外部資料來源 (Transact-SQL)][Create External Data Source (Transact-SQL)]，以指定 Azure Blob 儲存體的位置。</span><span class="sxs-lookup"><span data-stu-id="1e145-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] to specify the location of your Azure blob storage.</span></span>
* <span data-ttu-id="1e145-171">[建立外部檔案格式 (Transact-SQL)][Create External File Format (Transact-SQL)]，以指定資料的格式。</span><span class="sxs-lookup"><span data-stu-id="1e145-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] to specify the format of your data.</span></span>
* <span data-ttu-id="1e145-172">[建立外部資料表 (Transact-SQL)][Create External Table (Transact-SQL)]，以指定資料表定義和資料的位置。</span><span class="sxs-lookup"><span data-stu-id="1e145-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] to specify the table definition and location of the data.</span></span>

<span data-ttu-id="1e145-173">對 SQL 資料倉儲資料庫執行這個查詢。</span><span class="sxs-lookup"><span data-stu-id="1e145-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="1e145-174">它會在 dbo 結構描述中建立指向 Azure Blob 儲存體中 DimDate2.txt 範例資料的外部資料表 (名稱為 DimDate2External)。</span><span class="sxs-lookup"><span data-stu-id="1e145-174">It will create an external table named DimDate2External in the dbo schema that points to the DimDate2.txt sample data in the Azure blob storage.</span></span>

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create the external table
-- Specify column names and data types. This needs to match the data in the sample file.
-- LOCATION: Specify path to file or directory that contains the data (relative to the blob container).
-- To point to all files under the blob container, use LOCATION='.'

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


-- Run a query on the external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="1e145-175">在 Visual Studio 的 [SQL Server 物件總管] 內，您可以看到外部檔案格式、外部資料來源和 DimDate2External 資料表。</span><span class="sxs-lookup"><span data-stu-id="1e145-175">In SQL Server Object Explorer in Visual Studio, you can see the external file format, external data source, and the DimDate2External table.</span></span>

![檢視外部資料表](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="1e145-177">步驟 3：將資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="1e145-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="1e145-178">外部資料表建立好後，您可以將資料載入至新資料表，或將其插入到現有資料表。</span><span class="sxs-lookup"><span data-stu-id="1e145-178">Once the external table is created, you can either load the data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="1e145-179">若要將資料載入至新資料表，請執行 [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1e145-179">To load the data into a new table, run the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="1e145-180">新資料表會擁有查詢中指名的資料行。</span><span class="sxs-lookup"><span data-stu-id="1e145-180">The new table will have the columns named in the query.</span></span> <span data-ttu-id="1e145-181">資料行的資料類型會符合外部資料表定義中的資料類型。</span><span class="sxs-lookup"><span data-stu-id="1e145-181">The data types of the columns will match the data types in the external table definition.</span></span>
* <span data-ttu-id="1e145-182">若要將資料載入至現有資料表，請使用 [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1e145-182">To load the data into an existing table, use the [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load the data from Azure blob storage to SQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="1e145-183">步驟 4：建立新載入資料的統計資料</span><span class="sxs-lookup"><span data-stu-id="1e145-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="1e145-184">SQL 資料倉儲不會自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="1e145-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="1e145-185">因此，若要達到高查詢效能，請務必在第一次載入後，於每個資料表的每個資料行上建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="1e145-185">Therefore, to achieve high query performance, it's important to create statistics on each column of each table after the first load.</span></span> <span data-ttu-id="1e145-186">另外，也請務必在大幅變更資料後更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="1e145-186">It's also important to update statistics after substantial changes in the data.</span></span>

<span data-ttu-id="1e145-187">本範例會在新的 DimDate2 資料表上建立單一資料行統計資料。</span><span class="sxs-lookup"><span data-stu-id="1e145-187">This example creates single-column statistics on the new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="1e145-188">若要深入了解，請參閱[統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="1e145-188">To learn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1e145-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e145-189">Next steps</span></span>
<span data-ttu-id="1e145-190">請參閱 [PolyBase 指南][PolyBase guide]，以取得開發使用 PolyBase 的解決方案時，您應該知道的進一步資訊。</span><span class="sxs-lookup"><span data-stu-id="1e145-190">See the [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with the AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
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
