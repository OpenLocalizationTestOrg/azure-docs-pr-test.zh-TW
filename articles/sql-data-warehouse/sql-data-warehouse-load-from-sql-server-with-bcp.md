---
title: "aaaLoad 資料從 SQL Server 到 Azure SQL 資料倉儲 (bcp) |Microsoft 文件"
description: "對於小型資料大小，使用 bcp tooexport 資料從 SQL Server tooflat 檔案和資料匯入 hello 直接在 Azure SQL 資料倉儲。"
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
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="7be82-103">將資料從 SQL Server 載入 Azure SQL 資料倉儲 (一般檔案)</span><span class="sxs-lookup"><span data-stu-id="7be82-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7be82-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="7be82-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="7be82-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="7be82-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="7be82-106">bcp</span><span class="sxs-lookup"><span data-stu-id="7be82-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="7be82-107">對於小型資料集，您可以使用 hello bcp 命令列公用程式 tooexport 資料從 SQL Server，並再將其載入直接 tooAzure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="7be82-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="7be82-108">在本教學課程中，您將使用 bcp 來：</span><span class="sxs-lookup"><span data-stu-id="7be82-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="7be82-109">從 SQL Server 匯出的資料表，使用 hello bcp 命令 （或建立簡單的範例檔案）</span><span class="sxs-lookup"><span data-stu-id="7be82-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="7be82-110">Hello 資料表匯入從一般檔案 tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="7be82-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="7be82-111">建立 hello 載入資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="7be82-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="7be82-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="7be82-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7be82-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="7be82-113">Prerequisites</span></span>
<span data-ttu-id="7be82-114">在本教學課程 toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="7be82-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="7be82-115">SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="7be82-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="7be82-116">hello bcp 命令列公用程式安裝</span><span class="sxs-lookup"><span data-stu-id="7be82-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="7be82-117">hello sqlcmd 命令列公用程式安裝</span><span class="sxs-lookup"><span data-stu-id="7be82-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="7be82-118">您可以下載 hello bcp 和 sqlcmd 公用程式從 hello [Microsoft Download Center][Microsoft Download Center]。</span><span class="sxs-lookup"><span data-stu-id="7be82-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="7be82-119">ASCII 或 UTF-16 格式的資料</span><span class="sxs-lookup"><span data-stu-id="7be82-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="7be82-120">如果您嘗試本教學課程使用您自己的資料，您的資料需要 toouse hello ASCII 或因為 bcp 不支援 utf-8，utf-16 編碼方式。</span><span class="sxs-lookup"><span data-stu-id="7be82-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="7be82-121">PolyBase 支援 UTF-8，但尚未支援 UTF-16。</span><span class="sxs-lookup"><span data-stu-id="7be82-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="7be82-122">請注意，是否您想要使用 PolyBase toocombine bcp 就會需要 tootransform hello 資料 tooUTF-8，從 SQL Server 匯出之後。</span><span class="sxs-lookup"><span data-stu-id="7be82-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="7be82-123">1.建立目的資料表</span><span class="sxs-lookup"><span data-stu-id="7be82-123">1. Create a destination table</span></span>
<span data-ttu-id="7be82-124">定義將 hello 負載 hello 目的地資料表的 SQL 資料倉儲中的資料表。</span><span class="sxs-lookup"><span data-stu-id="7be82-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="7be82-125">hello hello 資料表中的資料行必須對應 toohello 每一個資料列的資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7be82-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="7be82-126">toocreate 資料表中，開啟命令提示字元，並使用 sqlcmd.exe toorun hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="7be82-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="7be82-127">2.建立來源資料檔</span><span class="sxs-lookup"><span data-stu-id="7be82-127">2. Create a source data file</span></span>
<span data-ttu-id="7be82-128">開啟 [記事本] 及複製 hello 下列行資料到新的文字檔，然後儲存此檔案 tooyour 本機暫存目錄中，C:\Temp\DimDate2.txt。</span><span class="sxs-lookup"><span data-stu-id="7be82-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="7be82-129">此資料是 ASCII 格式。</span><span class="sxs-lookup"><span data-stu-id="7be82-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="7be82-130">（選擇性） tooexport 您自己的資料從 SQL Server 資料庫，開啟命令提示字元並執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="7be82-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="7be82-131">使用您自己的資訊取代 TableName、ServerName、DatabaseName、Username 和 Password。</span><span class="sxs-lookup"><span data-stu-id="7be82-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="7be82-132">3.將資料載入 hello</span><span class="sxs-lookup"><span data-stu-id="7be82-132">3. Load hello data</span></span>
<span data-ttu-id="7be82-133">tooload hello 資料，開啟命令提示字元，並執行下列命令，為伺服器名稱、 資料庫名稱、 使用者名稱和密碼的 hello 值取代您自己的資訊 hello。</span><span class="sxs-lookup"><span data-stu-id="7be82-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="7be82-134">使用此資料已載入正確的命令 tooverify hello</span><span class="sxs-lookup"><span data-stu-id="7be82-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="7be82-135">hello 結果看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="7be82-135">hello results should look like this:</span></span>

| <span data-ttu-id="7be82-136">DateId</span><span class="sxs-lookup"><span data-stu-id="7be82-136">DateId</span></span> | <span data-ttu-id="7be82-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="7be82-137">CalendarQuarter</span></span> | <span data-ttu-id="7be82-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="7be82-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7be82-139">20150101</span><span class="sxs-lookup"><span data-stu-id="7be82-139">20150101</span></span> |<span data-ttu-id="7be82-140">1</span><span class="sxs-lookup"><span data-stu-id="7be82-140">1</span></span> |<span data-ttu-id="7be82-141">3</span><span class="sxs-lookup"><span data-stu-id="7be82-141">3</span></span> |
| <span data-ttu-id="7be82-142">20150201</span><span class="sxs-lookup"><span data-stu-id="7be82-142">20150201</span></span> |<span data-ttu-id="7be82-143">1</span><span class="sxs-lookup"><span data-stu-id="7be82-143">1</span></span> |<span data-ttu-id="7be82-144">3</span><span class="sxs-lookup"><span data-stu-id="7be82-144">3</span></span> |
| <span data-ttu-id="7be82-145">20150301</span><span class="sxs-lookup"><span data-stu-id="7be82-145">20150301</span></span> |<span data-ttu-id="7be82-146">1</span><span class="sxs-lookup"><span data-stu-id="7be82-146">1</span></span> |<span data-ttu-id="7be82-147">3</span><span class="sxs-lookup"><span data-stu-id="7be82-147">3</span></span> |
| <span data-ttu-id="7be82-148">20150401</span><span class="sxs-lookup"><span data-stu-id="7be82-148">20150401</span></span> |<span data-ttu-id="7be82-149">2</span><span class="sxs-lookup"><span data-stu-id="7be82-149">2</span></span> |<span data-ttu-id="7be82-150">4</span><span class="sxs-lookup"><span data-stu-id="7be82-150">4</span></span> |
| <span data-ttu-id="7be82-151">20150501</span><span class="sxs-lookup"><span data-stu-id="7be82-151">20150501</span></span> |<span data-ttu-id="7be82-152">2</span><span class="sxs-lookup"><span data-stu-id="7be82-152">2</span></span> |<span data-ttu-id="7be82-153">4</span><span class="sxs-lookup"><span data-stu-id="7be82-153">4</span></span> |
| <span data-ttu-id="7be82-154">20150601</span><span class="sxs-lookup"><span data-stu-id="7be82-154">20150601</span></span> |<span data-ttu-id="7be82-155">2</span><span class="sxs-lookup"><span data-stu-id="7be82-155">2</span></span> |<span data-ttu-id="7be82-156">4</span><span class="sxs-lookup"><span data-stu-id="7be82-156">4</span></span> |
| <span data-ttu-id="7be82-157">20150701</span><span class="sxs-lookup"><span data-stu-id="7be82-157">20150701</span></span> |<span data-ttu-id="7be82-158">3</span><span class="sxs-lookup"><span data-stu-id="7be82-158">3</span></span> |<span data-ttu-id="7be82-159">1</span><span class="sxs-lookup"><span data-stu-id="7be82-159">1</span></span> |
| <span data-ttu-id="7be82-160">20150801</span><span class="sxs-lookup"><span data-stu-id="7be82-160">20150801</span></span> |<span data-ttu-id="7be82-161">3</span><span class="sxs-lookup"><span data-stu-id="7be82-161">3</span></span> |<span data-ttu-id="7be82-162">1</span><span class="sxs-lookup"><span data-stu-id="7be82-162">1</span></span> |
| <span data-ttu-id="7be82-163">20150801</span><span class="sxs-lookup"><span data-stu-id="7be82-163">20150801</span></span> |<span data-ttu-id="7be82-164">3</span><span class="sxs-lookup"><span data-stu-id="7be82-164">3</span></span> |<span data-ttu-id="7be82-165">1</span><span class="sxs-lookup"><span data-stu-id="7be82-165">1</span></span> |
| <span data-ttu-id="7be82-166">20151001</span><span class="sxs-lookup"><span data-stu-id="7be82-166">20151001</span></span> |<span data-ttu-id="7be82-167">4</span><span class="sxs-lookup"><span data-stu-id="7be82-167">4</span></span> |<span data-ttu-id="7be82-168">2</span><span class="sxs-lookup"><span data-stu-id="7be82-168">2</span></span> |
| <span data-ttu-id="7be82-169">20151101</span><span class="sxs-lookup"><span data-stu-id="7be82-169">20151101</span></span> |<span data-ttu-id="7be82-170">4</span><span class="sxs-lookup"><span data-stu-id="7be82-170">4</span></span> |<span data-ttu-id="7be82-171">2</span><span class="sxs-lookup"><span data-stu-id="7be82-171">2</span></span> |
| <span data-ttu-id="7be82-172">20151201</span><span class="sxs-lookup"><span data-stu-id="7be82-172">20151201</span></span> |<span data-ttu-id="7be82-173">4</span><span class="sxs-lookup"><span data-stu-id="7be82-173">4</span></span> |<span data-ttu-id="7be82-174">2</span><span class="sxs-lookup"><span data-stu-id="7be82-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="7be82-175">4.建立統計資料</span><span class="sxs-lookup"><span data-stu-id="7be82-175">4. Create statistics</span></span>
<span data-ttu-id="7be82-176">SQL 資料倉儲尚未支援自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="7be82-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="7be82-177">tooget hello 最佳查詢效能，很重要 toocreate 統計資料的所有資料表的所有資料行上 hello 第一次載入或之後 hello 資料會發生任何大量變更。</span><span class="sxs-lookup"><span data-stu-id="7be82-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="7be82-178">如需統計資料的詳細說明，請參閱[統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="7be82-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="7be82-179">Hello 執行的下列命令 toocreate 您載入新的資料表上的統計資料。</span><span class="sxs-lookup"><span data-stu-id="7be82-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="7be82-180">5.從 SQL 資料倉儲匯出資料</span><span class="sxs-lookup"><span data-stu-id="7be82-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="7be82-181">玩看，您可以匯出只載入 SQL 資料倉儲從傳回的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7be82-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="7be82-182">hello 命令 tooexport 完全 hello 與匯出從 SQL Server 相同。</span><span class="sxs-lookup"><span data-stu-id="7be82-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="7be82-183">不過，沒有 hello 結果上的差異。</span><span class="sxs-lookup"><span data-stu-id="7be82-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="7be82-184">因為 hello 資料會儲存 SQL 資料倉儲內的分散式位置中，當您匯出資料的每個計算節點將它寫入資料 toohello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="7be82-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="7be82-185">hello hello 輸出檔案中的 hello 資料順序是可能 toobe 不同 hello hello 中的資料順序 hello 輸入檔。</span><span class="sxs-lookup"><span data-stu-id="7be82-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="7be82-186">匯出資料表和比較匯出的結果</span><span class="sxs-lookup"><span data-stu-id="7be82-186">Export a table and compare exported results</span></span>
<span data-ttu-id="7be82-187">toosee hello 匯出的資料，開啟命令提示字元並執行此命令使用您自己的參數。</span><span class="sxs-lookup"><span data-stu-id="7be82-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="7be82-188">為 hello Azure 邏輯的 SQL Server 名稱。</span><span class="sxs-lookup"><span data-stu-id="7be82-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="7be82-189">您可以確認資料已正確開啟 hello 新檔案匯出的 hello。</span><span class="sxs-lookup"><span data-stu-id="7be82-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="7be82-190">hello 檔案中的 hello 資料應符合下列的 hello 文字，但可能會以不同的順序排序：</span><span class="sxs-lookup"><span data-stu-id="7be82-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="7be82-191">匯出 hello 查詢的結果</span><span class="sxs-lookup"><span data-stu-id="7be82-191">Export hello results of a query</span></span>
<span data-ttu-id="7be82-192">您可以使用 hello **queryout**函式的 bcp tooexport hello 查詢的結果，而不要匯出 hello 整份資料表。</span><span class="sxs-lookup"><span data-stu-id="7be82-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7be82-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7be82-193">Next steps</span></span>
<span data-ttu-id="7be82-194">如需載入的概觀，請參閱[將資料載入 SQL 資料倉儲][Load data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="7be82-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="7be82-195">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="7be82-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="7be82-196">如需有關在 SQL 資料倉儲上建立資料表的詳細資訊，請參閱[資料表概觀][Table Overview]或 [CREATE TABLE 語法][CREATE TABLE syntax]。</span><span class="sxs-lookup"><span data-stu-id="7be82-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
