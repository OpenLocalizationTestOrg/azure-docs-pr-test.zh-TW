---
title: "在 SQL 資料倉儲中使用 PolyBase 的指南 | Microsoft Docs"
description: "在 SQL 資料倉儲案例中使用 PolyBase 的指導方針和建議。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="10a2c-103">在 SQL 資料倉儲中使用 PolyBase 的指南</span><span class="sxs-lookup"><span data-stu-id="10a2c-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="10a2c-104">本指南提供在 SQL 資料倉儲中使用 PolyBase 的實用資訊。</span><span class="sxs-lookup"><span data-stu-id="10a2c-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="10a2c-105">如要開始使用，請參閱[使用 PolyBase 載入資料][Load data with PolyBase]教學課程。</span><span class="sxs-lookup"><span data-stu-id="10a2c-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="10a2c-106">替換儲存體金鑰</span><span class="sxs-lookup"><span data-stu-id="10a2c-106">Rotating storage keys</span></span>
<span data-ttu-id="10a2c-107">有時您基於安全性考量，會想要變更存取金鑰至您的 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="10a2c-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="10a2c-108">要執行這項工作的最佳方式是遵循稱為「替換金鑰」的程序。</span><span class="sxs-lookup"><span data-stu-id="10a2c-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="10a2c-109">您可能已經注意到您在 blob 儲存體帳戶有兩個儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="10a2c-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="10a2c-110">如此一來您就可以轉換</span><span class="sxs-lookup"><span data-stu-id="10a2c-110">This is so that you can transition</span></span>

<span data-ttu-id="10a2c-111">替換 Azure 儲存體帳戶金鑰的程序只需要簡單的三個步驟</span><span class="sxs-lookup"><span data-stu-id="10a2c-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="10a2c-112">建立以次要儲存體存取金鑰為基礎的第二個資料庫範圍認證</span><span class="sxs-lookup"><span data-stu-id="10a2c-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="10a2c-113">建立以新的認證為基礎的第二個外部資料來源</span><span class="sxs-lookup"><span data-stu-id="10a2c-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="10a2c-114">卸除並建立指向新的外部資料來源的外部資料表</span><span class="sxs-lookup"><span data-stu-id="10a2c-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="10a2c-115">當您移轉所有的外部資料表到新的外部資料來源時，您就可以執行清除工作：</span><span class="sxs-lookup"><span data-stu-id="10a2c-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="10a2c-116">卸除第一個外部資料來源</span><span class="sxs-lookup"><span data-stu-id="10a2c-116">Drop first external data source</span></span>
2. <span data-ttu-id="10a2c-117">卸除以主要儲存體存取金鑰為基礎的第一個資料庫範圍認證</span><span class="sxs-lookup"><span data-stu-id="10a2c-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="10a2c-118">登入 Azure 並重新產生主要存取金鑰供下一次使用</span><span class="sxs-lookup"><span data-stu-id="10a2c-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="10a2c-119">查詢 Azure blob 儲存體資料</span><span class="sxs-lookup"><span data-stu-id="10a2c-119">Query Azure blob storage data</span></span>
<span data-ttu-id="10a2c-120">針對外部資料表的查詢只使用資料表名稱，如同關聯式資料表一樣。</span><span class="sxs-lookup"><span data-stu-id="10a2c-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="10a2c-121">針對外部資料表的查詢可能會失敗，並顯示 *「查詢已中止 -- 從外部來源讀取時已達最大拒絕閾值」*錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="10a2c-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="10a2c-122">這表示您的外部資料包含 *「錯誤」* 記錄。</span><span class="sxs-lookup"><span data-stu-id="10a2c-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="10a2c-123">如果實際的資料類型/資料行數目不符合外部資料表的資料行定義，或資料不符合指定的外部檔案格式，則會將資料記錄視為「錯誤」。</span><span class="sxs-lookup"><span data-stu-id="10a2c-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="10a2c-124">若要修正此問題，請確定您的外部資料表及外部檔案格式定義皆正確，且這些定義與您的外部資料相符。</span><span class="sxs-lookup"><span data-stu-id="10a2c-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="10a2c-125">萬一外部資料記錄的子集有錯誤，您可以使用 CREATE EXTERNAL TABLE DDL 中的拒絕選項，選擇拒絕這些查詢記錄。</span><span class="sxs-lookup"><span data-stu-id="10a2c-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="10a2c-126">從 Azure blob 儲存體載入資料</span><span class="sxs-lookup"><span data-stu-id="10a2c-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="10a2c-127">此範例將 Azure blob 儲存體中的資料載入至 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="10a2c-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="10a2c-128">直接儲存資料可免除查詢時的資料傳輸時間。</span><span class="sxs-lookup"><span data-stu-id="10a2c-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="10a2c-129">搭配 columnstore 索引儲存資料可讓分析查詢的查詢效能提升 10 倍。</span><span class="sxs-lookup"><span data-stu-id="10a2c-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="10a2c-130">此範例使用 CREATE TABLE AS SELECT 陳述式來載入資料。</span><span class="sxs-lookup"><span data-stu-id="10a2c-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="10a2c-131">新的資料表繼承查詢中指名的資料行。</span><span class="sxs-lookup"><span data-stu-id="10a2c-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="10a2c-132">它會從外部資料表定義繼承這些資料行的資料型別。</span><span class="sxs-lookup"><span data-stu-id="10a2c-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="10a2c-133">CREATE TABLE AS SELECT 是高效能 TRANSACT-SQL 陳述式，可將資料平行載入到您的 SQL 資料倉儲的所有計算節點。</span><span class="sxs-lookup"><span data-stu-id="10a2c-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="10a2c-134">它原本是針對分析平台系統中的大量平行處理 (MPP) 引擎所開發，現在已納入 SQL 資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="10a2c-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="10a2c-135">請參閱 [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)]。</span><span class="sxs-lookup"><span data-stu-id="10a2c-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="10a2c-136">建立新載入資料的統計資料</span><span class="sxs-lookup"><span data-stu-id="10a2c-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="10a2c-137">Azure 資料倉儲尚未支援自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="10a2c-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="10a2c-138">為了獲得查詢的最佳效能，在首次載入資料，或是資料中發生重大變更之後，建立所有資料表的所有資料行統計資料非常重要。</span><span class="sxs-lookup"><span data-stu-id="10a2c-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="10a2c-139">如需統計資料的詳細說明，請參閱「開發」主題群組中的[統計資料][Statistics]主題。</span><span class="sxs-lookup"><span data-stu-id="10a2c-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="10a2c-140">以下是快速範例，說明如何在此範例中建立載入資料表的統計資料。</span><span class="sxs-lookup"><span data-stu-id="10a2c-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="10a2c-141">將資料匯出至 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="10a2c-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="10a2c-142">這一節說明如何將資料從 SQL 資料倉儲匯出至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="10a2c-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="10a2c-143">此範例使用 CREATE EXTERNAL TABLE AS SELECT (高效能 Transact-SQL 陳述式) 將資料從所有計算節點平行匯出。</span><span class="sxs-lookup"><span data-stu-id="10a2c-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="10a2c-144">下列範例會使用 dbo.Weblogs 資料表中的資料行定義和資料從 dbo 建立外部資料表 Weblogs2014。</span><span class="sxs-lookup"><span data-stu-id="10a2c-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="10a2c-145">外部資料表定義會儲存在 SQL 資料倉儲中，而 SELECT 陳述式的結果會匯出至資料來源所指定的 blob 容器下的 "/archive/log2014/" 目錄。</span><span class="sxs-lookup"><span data-stu-id="10a2c-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="10a2c-146">以指定的文字檔案格式匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="10a2c-146">The data is exported in the specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="10a2c-147">隔離載入使用者</span><span class="sxs-lookup"><span data-stu-id="10a2c-147">Isolate Loading Users</span></span>
<span data-ttu-id="10a2c-148">通常會需要多個使用者可將資料載入 SQL DW 中。</span><span class="sxs-lookup"><span data-stu-id="10a2c-148">There is often a need to have multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="10a2c-149">因為 [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] 需要資料庫的 CONTROL 權限，您將得到具有所有結構描述之控制存取的多個使用者。</span><span class="sxs-lookup"><span data-stu-id="10a2c-149">Because the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of the database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="10a2c-150">若要限制這種情況，您可以使用 DENY CONTROL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="10a2c-150">To limit this, you can use the DENY CONTROL statement.</span></span>

<span data-ttu-id="10a2c-151">範例：考慮將資料庫結構描述 schema_A 用於 dept A 以及 schema_B 用於 dept B，讓資料庫使用者 user_A 和 user_B 個別成為 dept A 及 B 中載入的 PolyBase 之使用者。</span><span class="sxs-lookup"><span data-stu-id="10a2c-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="10a2c-152">這兩個使用者皆已獲得 CONTROL 資料庫權限。</span><span class="sxs-lookup"><span data-stu-id="10a2c-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="10a2c-153">結構描述 A 和 B 的建立者現在是使用 DENY 鎖定其結構描述：</span><span class="sxs-lookup"><span data-stu-id="10a2c-153">The creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 <span data-ttu-id="10a2c-154">在此情況下，user_A 和 user_B 現在應該從其他部門的結構描述加以鎖定。</span><span class="sxs-lookup"><span data-stu-id="10a2c-154">With this, user_A and user_B should now be locked out from the other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="10a2c-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10a2c-155">Next steps</span></span>
<span data-ttu-id="10a2c-156">若要了解將資料移到 SQL 資料倉儲的詳細資訊，請參閱 [資料移轉概觀][data migration overview]。</span><span class="sxs-lookup"><span data-stu-id="10a2c-156">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
