---
title: "將資料從 SQL Server 載入 Azure SQL 資料倉儲 (bcp) | Microsoft Docs"
description: "對於小型資料，請使用 bcp 將資料從 SQL Server 匯出至一般檔案，以及將資料直接匯入 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: dae7b5f7456f4ec0daf60d55f9c38b780896ff83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="35fa2-103">將資料從 SQL Server 載入 Azure SQL 資料倉儲 (一般檔案)</span><span class="sxs-lookup"><span data-stu-id="35fa2-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35fa2-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="35fa2-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="35fa2-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="35fa2-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="35fa2-106">bcp</span><span class="sxs-lookup"><span data-stu-id="35fa2-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="35fa2-107">對於小型資料集，您可以使用 bcp 命令列公用程式從 SQL Server 匯出資料，然後將它直接載入到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="35fa2-107">For small data sets, you can use the bcp command-line utility to export data from SQL Server and then load it directly to Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="35fa2-108">在本教學課程中，您將使用 bcp 來：</span><span class="sxs-lookup"><span data-stu-id="35fa2-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="35fa2-109">使用 bcp out 命令從 SQL Server 匯出資料表 (或建立簡單的範例檔案)</span><span class="sxs-lookup"><span data-stu-id="35fa2-109">Export a table from from SQL Server by using the bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="35fa2-110">從一般檔案將資料表匯入到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="35fa2-110">Import the table from a flat file to SQL Data Warehouse.</span></span>
* <span data-ttu-id="35fa2-111">建立已載入資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="35fa2-111">Create statistics on the loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="35fa2-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="35fa2-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="35fa2-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="35fa2-113">Prerequisites</span></span>
<span data-ttu-id="35fa2-114">若要逐步執行本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="35fa2-114">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="35fa2-115">SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="35fa2-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="35fa2-116">已安裝的 bcp 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="35fa2-116">The bcp command-line utility installed</span></span>
* <span data-ttu-id="35fa2-117">已安裝的 sqlcmd 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="35fa2-117">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="35fa2-118">您可以從 [Microsoft 下載中心][Microsoft Download Center]下載 bcp 和 sqlcmd 公用程式。</span><span class="sxs-lookup"><span data-stu-id="35fa2-118">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="35fa2-119">ASCII 或 UTF-16 格式的資料</span><span class="sxs-lookup"><span data-stu-id="35fa2-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="35fa2-120">如果您使用您自己的資料嘗試本教學課程，您的資料必須使用 ASCII 或 UTF-16 編碼，因為 bcp 不支援 UFT-8。</span><span class="sxs-lookup"><span data-stu-id="35fa2-120">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="35fa2-121">PolyBase 支援 UTF-8，但尚未支援 UTF-16。</span><span class="sxs-lookup"><span data-stu-id="35fa2-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="35fa2-122">請注意，如果您想要結合 bcp 與 PolyBase，從 SQL Server 匯出資料後，您必須將資料轉換為 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="35fa2-122">Note that if you want to combine bcp with PolyBase you will need to transform the data to UTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="35fa2-123">1.建立目的資料表</span><span class="sxs-lookup"><span data-stu-id="35fa2-123">1. Create a destination table</span></span>
<span data-ttu-id="35fa2-124">在 SQL 資料倉儲中定義將成為載入目的地資料表的資料表。</span><span class="sxs-lookup"><span data-stu-id="35fa2-124">Define a table in SQL Data Warehouse that will be the destination table for the load.</span></span> <span data-ttu-id="35fa2-125">資料表中的資料行必須對應到資料檔的每一個資料列中的資料。</span><span class="sxs-lookup"><span data-stu-id="35fa2-125">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="35fa2-126">若要建立資料表，請開啟命令提示字元並使用 sqlcmd.exe 執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="35fa2-126">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="35fa2-127">2.建立來源資料檔</span><span class="sxs-lookup"><span data-stu-id="35fa2-127">2. Create a source data file</span></span>
<span data-ttu-id="35fa2-128">開啟 [記事本]，將下列幾行資料複製到新的文字檔，然後將此檔案儲存到本機暫存目錄 C:\Temp\DimDate2.txt。</span><span class="sxs-lookup"><span data-stu-id="35fa2-128">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="35fa2-129">此資料是 ASCII 格式。</span><span class="sxs-lookup"><span data-stu-id="35fa2-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="35fa2-130">(選擇性) 若要從 SQL Server 資料庫匯出您自己的資料，請開啟命令提示字元並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="35fa2-130">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="35fa2-131">使用您自己的資訊取代 TableName、ServerName、DatabaseName、Username 和 Password。</span><span class="sxs-lookup"><span data-stu-id="35fa2-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-the-data"></a><span data-ttu-id="35fa2-132">3.載入資料</span><span class="sxs-lookup"><span data-stu-id="35fa2-132">3. Load the data</span></span>
<span data-ttu-id="35fa2-133">若要載入資料，請開啟命令提示字元並執行下列命令，使用您自己的資訊取代 ServerName、DatabaseName、Username 和 Password。</span><span class="sxs-lookup"><span data-stu-id="35fa2-133">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="35fa2-134">使用此命令來確認已正確載入資料</span><span class="sxs-lookup"><span data-stu-id="35fa2-134">Use this command to verify the data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="35fa2-135">結果應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="35fa2-135">The results should look like this:</span></span>

| <span data-ttu-id="35fa2-136">DateId</span><span class="sxs-lookup"><span data-stu-id="35fa2-136">DateId</span></span> | <span data-ttu-id="35fa2-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="35fa2-137">CalendarQuarter</span></span> | <span data-ttu-id="35fa2-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="35fa2-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35fa2-139">20150101</span><span class="sxs-lookup"><span data-stu-id="35fa2-139">20150101</span></span> |<span data-ttu-id="35fa2-140">1</span><span class="sxs-lookup"><span data-stu-id="35fa2-140">1</span></span> |<span data-ttu-id="35fa2-141">3</span><span class="sxs-lookup"><span data-stu-id="35fa2-141">3</span></span> |
| <span data-ttu-id="35fa2-142">20150201</span><span class="sxs-lookup"><span data-stu-id="35fa2-142">20150201</span></span> |<span data-ttu-id="35fa2-143">1</span><span class="sxs-lookup"><span data-stu-id="35fa2-143">1</span></span> |<span data-ttu-id="35fa2-144">3</span><span class="sxs-lookup"><span data-stu-id="35fa2-144">3</span></span> |
| <span data-ttu-id="35fa2-145">20150301</span><span class="sxs-lookup"><span data-stu-id="35fa2-145">20150301</span></span> |<span data-ttu-id="35fa2-146">1</span><span class="sxs-lookup"><span data-stu-id="35fa2-146">1</span></span> |<span data-ttu-id="35fa2-147">3</span><span class="sxs-lookup"><span data-stu-id="35fa2-147">3</span></span> |
| <span data-ttu-id="35fa2-148">20150401</span><span class="sxs-lookup"><span data-stu-id="35fa2-148">20150401</span></span> |<span data-ttu-id="35fa2-149">2</span><span class="sxs-lookup"><span data-stu-id="35fa2-149">2</span></span> |<span data-ttu-id="35fa2-150">4</span><span class="sxs-lookup"><span data-stu-id="35fa2-150">4</span></span> |
| <span data-ttu-id="35fa2-151">20150501</span><span class="sxs-lookup"><span data-stu-id="35fa2-151">20150501</span></span> |<span data-ttu-id="35fa2-152">2</span><span class="sxs-lookup"><span data-stu-id="35fa2-152">2</span></span> |<span data-ttu-id="35fa2-153">4</span><span class="sxs-lookup"><span data-stu-id="35fa2-153">4</span></span> |
| <span data-ttu-id="35fa2-154">20150601</span><span class="sxs-lookup"><span data-stu-id="35fa2-154">20150601</span></span> |<span data-ttu-id="35fa2-155">2</span><span class="sxs-lookup"><span data-stu-id="35fa2-155">2</span></span> |<span data-ttu-id="35fa2-156">4</span><span class="sxs-lookup"><span data-stu-id="35fa2-156">4</span></span> |
| <span data-ttu-id="35fa2-157">20150701</span><span class="sxs-lookup"><span data-stu-id="35fa2-157">20150701</span></span> |<span data-ttu-id="35fa2-158">3</span><span class="sxs-lookup"><span data-stu-id="35fa2-158">3</span></span> |<span data-ttu-id="35fa2-159">1</span><span class="sxs-lookup"><span data-stu-id="35fa2-159">1</span></span> |
| <span data-ttu-id="35fa2-160">20150801</span><span class="sxs-lookup"><span data-stu-id="35fa2-160">20150801</span></span> |<span data-ttu-id="35fa2-161">3</span><span class="sxs-lookup"><span data-stu-id="35fa2-161">3</span></span> |<span data-ttu-id="35fa2-162">1</span><span class="sxs-lookup"><span data-stu-id="35fa2-162">1</span></span> |
| <span data-ttu-id="35fa2-163">20150801</span><span class="sxs-lookup"><span data-stu-id="35fa2-163">20150801</span></span> |<span data-ttu-id="35fa2-164">3</span><span class="sxs-lookup"><span data-stu-id="35fa2-164">3</span></span> |<span data-ttu-id="35fa2-165">1</span><span class="sxs-lookup"><span data-stu-id="35fa2-165">1</span></span> |
| <span data-ttu-id="35fa2-166">20151001</span><span class="sxs-lookup"><span data-stu-id="35fa2-166">20151001</span></span> |<span data-ttu-id="35fa2-167">4</span><span class="sxs-lookup"><span data-stu-id="35fa2-167">4</span></span> |<span data-ttu-id="35fa2-168">2</span><span class="sxs-lookup"><span data-stu-id="35fa2-168">2</span></span> |
| <span data-ttu-id="35fa2-169">20151101</span><span class="sxs-lookup"><span data-stu-id="35fa2-169">20151101</span></span> |<span data-ttu-id="35fa2-170">4</span><span class="sxs-lookup"><span data-stu-id="35fa2-170">4</span></span> |<span data-ttu-id="35fa2-171">2</span><span class="sxs-lookup"><span data-stu-id="35fa2-171">2</span></span> |
| <span data-ttu-id="35fa2-172">20151201</span><span class="sxs-lookup"><span data-stu-id="35fa2-172">20151201</span></span> |<span data-ttu-id="35fa2-173">4</span><span class="sxs-lookup"><span data-stu-id="35fa2-173">4</span></span> |<span data-ttu-id="35fa2-174">2</span><span class="sxs-lookup"><span data-stu-id="35fa2-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="35fa2-175">4.建立統計資料</span><span class="sxs-lookup"><span data-stu-id="35fa2-175">4. Create statistics</span></span>
<span data-ttu-id="35fa2-176">SQL 資料倉儲尚未支援自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="35fa2-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="35fa2-177">為了獲得最佳查詢效能，在首次載入資料或資料發生任何重大變更之後，建立所有資料表的所有資料行統計資料非常重要。</span><span class="sxs-lookup"><span data-stu-id="35fa2-177">To get the best query performance, it's important to create statistics on all columns of all tables after the first load or after any substantial changes occur in the data.</span></span> <span data-ttu-id="35fa2-178">如需統計資料的詳細說明，請參閱[統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="35fa2-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="35fa2-179">執行下列命令以建立新載入資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="35fa2-179">Run the following command to create statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="35fa2-180">5.從 SQL 資料倉儲匯出資料</span><span class="sxs-lookup"><span data-stu-id="35fa2-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="35fa2-181">為了好玩，您可以匯出您剛從 SQL 資料倉儲載入的資料。</span><span class="sxs-lookup"><span data-stu-id="35fa2-181">For fun, you can export the data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="35fa2-182">匯出命令完全與從 SQL Server 匯出的命令相同。</span><span class="sxs-lookup"><span data-stu-id="35fa2-182">The command to export is exactly the same as exporting from SQL Server.</span></span>

<span data-ttu-id="35fa2-183">不過，結果有所差異。</span><span class="sxs-lookup"><span data-stu-id="35fa2-183">However, there is a difference in the results.</span></span> <span data-ttu-id="35fa2-184">因為資料儲存在 SQL 資料倉儲內的分散位置，所以當您匯出資料時，每個計算節點會將資料寫入至輸出檔。</span><span class="sxs-lookup"><span data-stu-id="35fa2-184">Since the data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data to the output file.</span></span> <span data-ttu-id="35fa2-185">輸出檔中的資料順序與輸入檔中的資料順序可能不同。</span><span class="sxs-lookup"><span data-stu-id="35fa2-185">The order of the data in the output file is likely to be different than the order of the data in the input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="35fa2-186">匯出資料表和比較匯出的結果</span><span class="sxs-lookup"><span data-stu-id="35fa2-186">Export a table and compare exported results</span></span>
<span data-ttu-id="35fa2-187">若要查看匯出的資料，請開啟命令提示字元並使用您自己的參數執行此命令。</span><span class="sxs-lookup"><span data-stu-id="35fa2-187">To see the exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="35fa2-188">ServerName 是您的 Azure 邏輯 SQL Server 名稱。</span><span class="sxs-lookup"><span data-stu-id="35fa2-188">ServerName is the name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="35fa2-189">您可以開啟新的檔案來確認資料已正確匯出。</span><span class="sxs-lookup"><span data-stu-id="35fa2-189">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="35fa2-190">檔案中的資料應該符合以下文字，但可能以不同的順序排序：</span><span class="sxs-lookup"><span data-stu-id="35fa2-190">The data in the file should match the text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-the-results-of-a-query"></a><span data-ttu-id="35fa2-191">此查詢的結果如下：</span><span class="sxs-lookup"><span data-stu-id="35fa2-191">Export the results of a query</span></span>
<span data-ttu-id="35fa2-192">您可以使用 bcp 的 **queryout** 函數匯出查詢結果，而不是匯出整份資料表。</span><span class="sxs-lookup"><span data-stu-id="35fa2-192">You can use the **queryout** function of bcp to export the results of a query instead of exporting the entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="35fa2-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35fa2-193">Next steps</span></span>
<span data-ttu-id="35fa2-194">如需載入的概觀，請參閱[將資料載入 SQL 資料倉儲][Load data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="35fa2-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="35fa2-195">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="35fa2-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="35fa2-196">如需有關在 SQL 資料倉儲上建立資料表的詳細資訊，請參閱[資料表概觀][Table Overview]或 [CREATE TABLE 語法][CREATE TABLE syntax]。</span><span class="sxs-lookup"><span data-stu-id="35fa2-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
