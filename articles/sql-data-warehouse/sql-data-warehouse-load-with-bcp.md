---
title: "SQL 資料倉儲 aaaUse bcp tooload 資料 |Microsoft 文件"
description: "了解哪些 bcp 和如何 toouse 會針對資料倉儲案例。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="e1396-103">使用 bcp 載入資料</span><span class="sxs-lookup"><span data-stu-id="e1396-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1396-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="e1396-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="e1396-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="e1396-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="e1396-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="e1396-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="e1396-107">BCP</span><span class="sxs-lookup"><span data-stu-id="e1396-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="e1396-108">**[bcp] [ bcp]** 是命令列大量載入公用程式，可讓您 toocopy SQL Server、 資料檔和 SQL 資料倉儲之間的資料。</span><span class="sxs-lookup"><span data-stu-id="e1396-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="e1396-109">使用 bcp tooimport 大量的資料列到的 SQL 資料倉儲資料表或 tooexport 至資料檔案的 SQL Server 資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="e1396-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="e1396-110">Hello queryout 選項使用時，除外 bcp 不需要知道的 Transact SQL。</span><span class="sxs-lookup"><span data-stu-id="e1396-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="e1396-111">bcp 就會是快速且輕鬆 toomove 小型資料集執行和跳離的 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1396-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="e1396-112">hello 確切建議透過 bcp 的 tooload/擷取的資料量將取決於您的網路連線 toohello Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="e1396-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="e1396-113">一般而言，維度資料表可輕易透過 bcp 載入和擷取，不過，不建議將 bcp 用於載入或擷取大量資料。</span><span class="sxs-lookup"><span data-stu-id="e1396-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="e1396-114">Polybase 是 hello 建議載入和擷取大型資料磁碟區，會利用 SQL 資料倉儲的 hello 大量平行處理架構更好的工具。</span><span class="sxs-lookup"><span data-stu-id="e1396-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="e1396-115">您可以透過 bcp：</span><span class="sxs-lookup"><span data-stu-id="e1396-115">With bcp you can:</span></span>

* <span data-ttu-id="e1396-116">使用簡單的命令列公用程式 tooload 資料到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e1396-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="e1396-117">使用簡單的命令列公用程式 tooextract 資料從 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e1396-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="e1396-118">此教學課程將為您示範如何：</span><span class="sxs-lookup"><span data-stu-id="e1396-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="e1396-119">資料匯入資料表，在命令中使用 hello bcp</span><span class="sxs-lookup"><span data-stu-id="e1396-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="e1396-120">從資料表 uisng hello bcp out 命令匯出資料</span><span class="sxs-lookup"><span data-stu-id="e1396-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e1396-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="e1396-121">Prerequisites</span></span>
<span data-ttu-id="e1396-122">在本教學課程 toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="e1396-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="e1396-123">SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="e1396-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="e1396-124">hello bcp 命令列公用程式安裝</span><span class="sxs-lookup"><span data-stu-id="e1396-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="e1396-125">hello SQLCMD 命令列公用程式安裝</span><span class="sxs-lookup"><span data-stu-id="e1396-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="e1396-126">您可以下載 hello bcp 和 sqlcmd 公用程式從 hello [Microsoft Download Center][Microsoft Download Center]。</span><span class="sxs-lookup"><span data-stu-id="e1396-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="e1396-127">將資料匯入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="e1396-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="e1396-128">在本教學課程中，您將 Azure SQL 資料倉儲中建立資料表並 hello 資料表將資料匯入。</span><span class="sxs-lookup"><span data-stu-id="e1396-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="e1396-129">步驟 1：在 Azure SQL 資料倉儲中建立資料表</span><span class="sxs-lookup"><span data-stu-id="e1396-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="e1396-130">從命令提示字元中，使用下列查詢 toocreate 資料表執行個體上的 sqlcmd toorun hello:</span><span class="sxs-lookup"><span data-stu-id="e1396-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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

> [!NOTE]
> <span data-ttu-id="e1396-131">請參閱[資料表概觀][ Table Overview]或[CREATE TABLE 語法][ CREATE TABLE syntax]如需有關 SQL 資料倉儲與 hello 上建立資料表 hello WITH 子句中可用的選項。</span><span class="sxs-lookup"><span data-stu-id="e1396-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="e1396-132">步驟 2：建立來源資料檔</span><span class="sxs-lookup"><span data-stu-id="e1396-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="e1396-133">開啟 [記事本] 及複製 hello 下列行資料到新的文字檔，然後儲存此檔案 tooyour 本機暫存目錄中，C:\Temp\DimDate2.txt。</span><span class="sxs-lookup"><span data-stu-id="e1396-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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

> [!NOTE]
> <span data-ttu-id="e1396-134">它是重要的 tooremember 該 bcp.exe 不支援 hello utf-8 的檔案編碼方式。</span><span class="sxs-lookup"><span data-stu-id="e1396-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="e1396-135">使用 bcp.exe 時，請使用 ASCII 檔案或 UTF-16 編碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="e1396-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="e1396-136">步驟 3： 連接及匯入 hello 資料</span><span class="sxs-lookup"><span data-stu-id="e1396-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="e1396-137">您可以使用 bcp，來連接並使用下列命令並將 hello 值做為適當的 hello hello 資料匯入項目：</span><span class="sxs-lookup"><span data-stu-id="e1396-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="e1396-138">您可以確認資料已由執行下列查詢中使用 sqlcmd hello 載入的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1396-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="e1396-139">這應該會傳回下列結果 hello:</span><span class="sxs-lookup"><span data-stu-id="e1396-139">This should return hello following results:</span></span>

| <span data-ttu-id="e1396-140">DateId</span><span class="sxs-lookup"><span data-stu-id="e1396-140">DateId</span></span> | <span data-ttu-id="e1396-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="e1396-141">CalendarQuarter</span></span> | <span data-ttu-id="e1396-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="e1396-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1396-143">20150101</span><span class="sxs-lookup"><span data-stu-id="e1396-143">20150101</span></span> |<span data-ttu-id="e1396-144">1</span><span class="sxs-lookup"><span data-stu-id="e1396-144">1</span></span> |<span data-ttu-id="e1396-145">3</span><span class="sxs-lookup"><span data-stu-id="e1396-145">3</span></span> |
| <span data-ttu-id="e1396-146">20150201</span><span class="sxs-lookup"><span data-stu-id="e1396-146">20150201</span></span> |<span data-ttu-id="e1396-147">1</span><span class="sxs-lookup"><span data-stu-id="e1396-147">1</span></span> |<span data-ttu-id="e1396-148">3</span><span class="sxs-lookup"><span data-stu-id="e1396-148">3</span></span> |
| <span data-ttu-id="e1396-149">20150301</span><span class="sxs-lookup"><span data-stu-id="e1396-149">20150301</span></span> |<span data-ttu-id="e1396-150">1</span><span class="sxs-lookup"><span data-stu-id="e1396-150">1</span></span> |<span data-ttu-id="e1396-151">3</span><span class="sxs-lookup"><span data-stu-id="e1396-151">3</span></span> |
| <span data-ttu-id="e1396-152">20150401</span><span class="sxs-lookup"><span data-stu-id="e1396-152">20150401</span></span> |<span data-ttu-id="e1396-153">2</span><span class="sxs-lookup"><span data-stu-id="e1396-153">2</span></span> |<span data-ttu-id="e1396-154">4</span><span class="sxs-lookup"><span data-stu-id="e1396-154">4</span></span> |
| <span data-ttu-id="e1396-155">20150501</span><span class="sxs-lookup"><span data-stu-id="e1396-155">20150501</span></span> |<span data-ttu-id="e1396-156">2</span><span class="sxs-lookup"><span data-stu-id="e1396-156">2</span></span> |<span data-ttu-id="e1396-157">4</span><span class="sxs-lookup"><span data-stu-id="e1396-157">4</span></span> |
| <span data-ttu-id="e1396-158">20150601</span><span class="sxs-lookup"><span data-stu-id="e1396-158">20150601</span></span> |<span data-ttu-id="e1396-159">2</span><span class="sxs-lookup"><span data-stu-id="e1396-159">2</span></span> |<span data-ttu-id="e1396-160">4</span><span class="sxs-lookup"><span data-stu-id="e1396-160">4</span></span> |
| <span data-ttu-id="e1396-161">20150701</span><span class="sxs-lookup"><span data-stu-id="e1396-161">20150701</span></span> |<span data-ttu-id="e1396-162">3</span><span class="sxs-lookup"><span data-stu-id="e1396-162">3</span></span> |<span data-ttu-id="e1396-163">1</span><span class="sxs-lookup"><span data-stu-id="e1396-163">1</span></span> |
| <span data-ttu-id="e1396-164">20150801</span><span class="sxs-lookup"><span data-stu-id="e1396-164">20150801</span></span> |<span data-ttu-id="e1396-165">3</span><span class="sxs-lookup"><span data-stu-id="e1396-165">3</span></span> |<span data-ttu-id="e1396-166">1</span><span class="sxs-lookup"><span data-stu-id="e1396-166">1</span></span> |
| <span data-ttu-id="e1396-167">20150801</span><span class="sxs-lookup"><span data-stu-id="e1396-167">20150801</span></span> |<span data-ttu-id="e1396-168">3</span><span class="sxs-lookup"><span data-stu-id="e1396-168">3</span></span> |<span data-ttu-id="e1396-169">1</span><span class="sxs-lookup"><span data-stu-id="e1396-169">1</span></span> |
| <span data-ttu-id="e1396-170">20151001</span><span class="sxs-lookup"><span data-stu-id="e1396-170">20151001</span></span> |<span data-ttu-id="e1396-171">4</span><span class="sxs-lookup"><span data-stu-id="e1396-171">4</span></span> |<span data-ttu-id="e1396-172">2</span><span class="sxs-lookup"><span data-stu-id="e1396-172">2</span></span> |
| <span data-ttu-id="e1396-173">20151101</span><span class="sxs-lookup"><span data-stu-id="e1396-173">20151101</span></span> |<span data-ttu-id="e1396-174">4</span><span class="sxs-lookup"><span data-stu-id="e1396-174">4</span></span> |<span data-ttu-id="e1396-175">2</span><span class="sxs-lookup"><span data-stu-id="e1396-175">2</span></span> |
| <span data-ttu-id="e1396-176">20151201</span><span class="sxs-lookup"><span data-stu-id="e1396-176">20151201</span></span> |<span data-ttu-id="e1396-177">4</span><span class="sxs-lookup"><span data-stu-id="e1396-177">4</span></span> |<span data-ttu-id="e1396-178">2</span><span class="sxs-lookup"><span data-stu-id="e1396-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="e1396-179">步驟 4：建立新載入資料的統計資料</span><span class="sxs-lookup"><span data-stu-id="e1396-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="e1396-180">Azure 資料倉儲尚未支援自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="e1396-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="e1396-181">在順序 tooget hello 達到最佳效能從您的查詢，請務必在所有資料表的所有資料行上建立統計資料，hello 第一次載入之後或 hello 資料會發生任何大量變更。</span><span class="sxs-lookup"><span data-stu-id="e1396-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="e1396-182">統計資料的詳細說明，請參閱 hello[統計資料][ Statistics] hello 開發一組主題中的主題。</span><span class="sxs-lookup"><span data-stu-id="e1396-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="e1396-183">以下是 toocreate hello 資料表的統計資料如何載入在此範例中的快速範例</span><span class="sxs-lookup"><span data-stu-id="e1396-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="e1396-184">執行 hello sqlcmd 提示字元中的下列 CREATE STATISTICS 陳述式：</span><span class="sxs-lookup"><span data-stu-id="e1396-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="e1396-185">從 SQL 資料倉儲匯出資料</span><span class="sxs-lookup"><span data-stu-id="e1396-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="e1396-186">在本教學課程中，您將從 Azure SQL 資料倉儲中的資料表建立資料檔案。</span><span class="sxs-lookup"><span data-stu-id="e1396-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="e1396-187">我們會將 hello 資料前面 tooa 稱為 DimDate2_export.txt 新資料檔案所建立的匯出。</span><span class="sxs-lookup"><span data-stu-id="e1396-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="e1396-188">步驟 1： 匯出 hello 資料</span><span class="sxs-lookup"><span data-stu-id="e1396-188">Step 1: Export hello data</span></span>
<span data-ttu-id="e1396-189">使用 hello bcp 公用程式，您可以連接及匯出資料使用下列命令並將 hello 值做為適當的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1396-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="e1396-190">您可以確認資料已正確開啟 hello 新檔案匯出的 hello。</span><span class="sxs-lookup"><span data-stu-id="e1396-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="e1396-191">hello 檔案中的 hello 資料應符合下列的 hello 文字：</span><span class="sxs-lookup"><span data-stu-id="e1396-191">hello data in hello file should match hello text below:</span></span>

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

> [!NOTE]
> <span data-ttu-id="e1396-192">因為分散式系統的 toohello 本質，hello 資料順序可能不是相同 hello 跨 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1396-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="e1396-193">另一個選項是 toouse hello **queryout**函式的 bcp toowrite 查詢擷取而不匯出 hello 整份資料表。</span><span class="sxs-lookup"><span data-stu-id="e1396-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e1396-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1396-194">Next steps</span></span>
<span data-ttu-id="e1396-195">如需載入的概觀，請參閱[將資料載入 SQL 資料倉儲][Load data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="e1396-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="e1396-196">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="e1396-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
