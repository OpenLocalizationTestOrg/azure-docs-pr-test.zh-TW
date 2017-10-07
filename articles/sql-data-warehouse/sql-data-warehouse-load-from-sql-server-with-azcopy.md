---
title: "aaaLoad 資料從 SQL Server 到 Azure SQL 資料倉儲 (PolyBase) |Microsoft 文件"
description: "您可以使用 bcp tooexport 資料從 SQL Server tooflat 檔案、 AZCopy tooimport 資料 tooAzure blob 儲存體和 PolyBase tooingest hello 資料至 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="ed513-103">將資料從 SQL Server 載入 Azure SQL 資料倉儲 (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="ed513-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="ed513-104">使用 bcp 並從 SQL Server tooAzure blob 儲存體的 AZCopy 命令列公用程式 tooload 資料。</span><span class="sxs-lookup"><span data-stu-id="ed513-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="ed513-105">再使用 PolyBase 或 Azure Data Factory tooload hello 資料到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ed513-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ed513-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="ed513-106">Prerequisites</span></span>
<span data-ttu-id="ed513-107">在本教學課程 toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="ed513-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="ed513-108">SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="ed513-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="ed513-109">hello bcp 命令列公用程式安裝</span><span class="sxs-lookup"><span data-stu-id="ed513-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="ed513-110">hello SQLCMD 命令列公用程式安裝</span><span class="sxs-lookup"><span data-stu-id="ed513-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="ed513-111">您可以下載 hello bcp 和 sqlcmd 公用程式從 hello [Microsoft Download Center][Microsoft Download Center]。</span><span class="sxs-lookup"><span data-stu-id="ed513-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="ed513-112">將資料匯入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="ed513-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="ed513-113">在本教學課程中，您將 Azure SQL 資料倉儲中建立資料表並 hello 資料表將資料匯入。</span><span class="sxs-lookup"><span data-stu-id="ed513-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="ed513-114">步驟 1：在 Azure SQL 資料倉儲中建立資料表</span><span class="sxs-lookup"><span data-stu-id="ed513-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ed513-115">從命令提示字元中，使用下列查詢 toocreate 資料表執行個體上的 sqlcmd toorun hello:</span><span class="sxs-lookup"><span data-stu-id="ed513-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="ed513-116">請參閱[資料表概觀][ Table Overview]或[CREATE TABLE 語法][ CREATE TABLE syntax]如需有關 SQL 資料倉儲與 hello 上建立資料表 hello WITH 子句中可用的選項。</span><span class="sxs-lookup"><span data-stu-id="ed513-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="ed513-117">步驟 2：建立來源資料檔</span><span class="sxs-lookup"><span data-stu-id="ed513-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="ed513-118">開啟 [記事本] 及複製 hello 下列行資料到新的文字檔，然後儲存此檔案 tooyour 本機暫存目錄中，C:\Temp\DimDate2.txt。</span><span class="sxs-lookup"><span data-stu-id="ed513-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="ed513-119">它是重要的 tooremember 該 bcp.exe 不支援 hello utf-8 的檔案編碼方式。</span><span class="sxs-lookup"><span data-stu-id="ed513-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="ed513-120">使用 bcp.exe 時，請使用 ASCII 檔案或 UTF-16 編碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="ed513-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="ed513-121">步驟 3： 連接及匯入 hello 資料</span><span class="sxs-lookup"><span data-stu-id="ed513-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="ed513-122">您可以使用 bcp，來連接並使用下列命令並將 hello 值做為適當的 hello hello 資料匯入項目：</span><span class="sxs-lookup"><span data-stu-id="ed513-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="ed513-123">您可以確認資料已由執行下列查詢中使用 sqlcmd hello 載入的 hello:</span><span class="sxs-lookup"><span data-stu-id="ed513-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="ed513-124">這應該會傳回下列結果 hello:</span><span class="sxs-lookup"><span data-stu-id="ed513-124">This should return hello following results:</span></span>

| <span data-ttu-id="ed513-125">DateId</span><span class="sxs-lookup"><span data-stu-id="ed513-125">DateId</span></span> | <span data-ttu-id="ed513-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="ed513-126">CalendarQuarter</span></span> | <span data-ttu-id="ed513-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="ed513-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed513-128">20150101</span><span class="sxs-lookup"><span data-stu-id="ed513-128">20150101</span></span> |<span data-ttu-id="ed513-129">1</span><span class="sxs-lookup"><span data-stu-id="ed513-129">1</span></span> |<span data-ttu-id="ed513-130">3</span><span class="sxs-lookup"><span data-stu-id="ed513-130">3</span></span> |
| <span data-ttu-id="ed513-131">20150201</span><span class="sxs-lookup"><span data-stu-id="ed513-131">20150201</span></span> |<span data-ttu-id="ed513-132">1</span><span class="sxs-lookup"><span data-stu-id="ed513-132">1</span></span> |<span data-ttu-id="ed513-133">3</span><span class="sxs-lookup"><span data-stu-id="ed513-133">3</span></span> |
| <span data-ttu-id="ed513-134">20150301</span><span class="sxs-lookup"><span data-stu-id="ed513-134">20150301</span></span> |<span data-ttu-id="ed513-135">1</span><span class="sxs-lookup"><span data-stu-id="ed513-135">1</span></span> |<span data-ttu-id="ed513-136">3</span><span class="sxs-lookup"><span data-stu-id="ed513-136">3</span></span> |
| <span data-ttu-id="ed513-137">20150401</span><span class="sxs-lookup"><span data-stu-id="ed513-137">20150401</span></span> |<span data-ttu-id="ed513-138">2</span><span class="sxs-lookup"><span data-stu-id="ed513-138">2</span></span> |<span data-ttu-id="ed513-139">4</span><span class="sxs-lookup"><span data-stu-id="ed513-139">4</span></span> |
| <span data-ttu-id="ed513-140">20150501</span><span class="sxs-lookup"><span data-stu-id="ed513-140">20150501</span></span> |<span data-ttu-id="ed513-141">2</span><span class="sxs-lookup"><span data-stu-id="ed513-141">2</span></span> |<span data-ttu-id="ed513-142">4</span><span class="sxs-lookup"><span data-stu-id="ed513-142">4</span></span> |
| <span data-ttu-id="ed513-143">20150601</span><span class="sxs-lookup"><span data-stu-id="ed513-143">20150601</span></span> |<span data-ttu-id="ed513-144">2</span><span class="sxs-lookup"><span data-stu-id="ed513-144">2</span></span> |<span data-ttu-id="ed513-145">4</span><span class="sxs-lookup"><span data-stu-id="ed513-145">4</span></span> |
| <span data-ttu-id="ed513-146">20150701</span><span class="sxs-lookup"><span data-stu-id="ed513-146">20150701</span></span> |<span data-ttu-id="ed513-147">3</span><span class="sxs-lookup"><span data-stu-id="ed513-147">3</span></span> |<span data-ttu-id="ed513-148">1</span><span class="sxs-lookup"><span data-stu-id="ed513-148">1</span></span> |
| <span data-ttu-id="ed513-149">20150801</span><span class="sxs-lookup"><span data-stu-id="ed513-149">20150801</span></span> |<span data-ttu-id="ed513-150">3</span><span class="sxs-lookup"><span data-stu-id="ed513-150">3</span></span> |<span data-ttu-id="ed513-151">1</span><span class="sxs-lookup"><span data-stu-id="ed513-151">1</span></span> |
| <span data-ttu-id="ed513-152">20150801</span><span class="sxs-lookup"><span data-stu-id="ed513-152">20150801</span></span> |<span data-ttu-id="ed513-153">3</span><span class="sxs-lookup"><span data-stu-id="ed513-153">3</span></span> |<span data-ttu-id="ed513-154">1</span><span class="sxs-lookup"><span data-stu-id="ed513-154">1</span></span> |
| <span data-ttu-id="ed513-155">20151001</span><span class="sxs-lookup"><span data-stu-id="ed513-155">20151001</span></span> |<span data-ttu-id="ed513-156">4</span><span class="sxs-lookup"><span data-stu-id="ed513-156">4</span></span> |<span data-ttu-id="ed513-157">2</span><span class="sxs-lookup"><span data-stu-id="ed513-157">2</span></span> |
| <span data-ttu-id="ed513-158">20151101</span><span class="sxs-lookup"><span data-stu-id="ed513-158">20151101</span></span> |<span data-ttu-id="ed513-159">4</span><span class="sxs-lookup"><span data-stu-id="ed513-159">4</span></span> |<span data-ttu-id="ed513-160">2</span><span class="sxs-lookup"><span data-stu-id="ed513-160">2</span></span> |
| <span data-ttu-id="ed513-161">20151201</span><span class="sxs-lookup"><span data-stu-id="ed513-161">20151201</span></span> |<span data-ttu-id="ed513-162">4</span><span class="sxs-lookup"><span data-stu-id="ed513-162">4</span></span> |<span data-ttu-id="ed513-163">2</span><span class="sxs-lookup"><span data-stu-id="ed513-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="ed513-164">步驟 4：建立新載入資料的統計資料</span><span class="sxs-lookup"><span data-stu-id="ed513-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="ed513-165">Azure 資料倉儲尚未支援自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="ed513-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="ed513-166">在順序 tooget hello 達到最佳效能從您的查詢，請務必在所有資料表的所有資料行上建立統計資料，hello 第一次載入之後或 hello 資料會發生任何大量變更。</span><span class="sxs-lookup"><span data-stu-id="ed513-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="ed513-167">統計資料的詳細說明，請參閱 hello[統計資料][ Statistics] hello 開發一組主題中的主題。</span><span class="sxs-lookup"><span data-stu-id="ed513-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="ed513-168">以下是 toocreate hello 資料表的統計資料如何載入在此範例中的快速範例</span><span class="sxs-lookup"><span data-stu-id="ed513-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="ed513-169">執行 hello sqlcmd 提示字元中的下列 CREATE STATISTICS 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ed513-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="ed513-170">從 SQL 資料倉儲匯出資料</span><span class="sxs-lookup"><span data-stu-id="ed513-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="ed513-171">在本教學課程中，您將從 Azure SQL 資料倉儲中的資料表建立資料檔案。</span><span class="sxs-lookup"><span data-stu-id="ed513-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="ed513-172">我們會將 hello 資料前面 tooa 稱為 DimDate2_export.txt 新資料檔案所建立的匯出。</span><span class="sxs-lookup"><span data-stu-id="ed513-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="ed513-173">步驟 1： 匯出 hello 資料</span><span class="sxs-lookup"><span data-stu-id="ed513-173">Step 1: Export hello data</span></span>
<span data-ttu-id="ed513-174">使用 hello bcp 公用程式，您可以連接及匯出資料使用下列命令並將 hello 值做為適當的 hello:</span><span class="sxs-lookup"><span data-stu-id="ed513-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="ed513-175">您可以確認資料已正確開啟 hello 新檔案匯出的 hello。</span><span class="sxs-lookup"><span data-stu-id="ed513-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="ed513-176">hello 檔案中的 hello 資料應符合下列的 hello 文字：</span><span class="sxs-lookup"><span data-stu-id="ed513-176">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="ed513-177">因為分散式系統的 toohello 本質，hello 資料順序可能不是相同 hello 跨 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="ed513-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="ed513-178">另一個選項是 toouse hello **queryout**函式的 bcp toowrite 查詢擷取而不匯出 hello 整份資料表。</span><span class="sxs-lookup"><span data-stu-id="ed513-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ed513-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed513-179">Next steps</span></span>
<span data-ttu-id="ed513-180">如需載入的概觀，請參閱[將資料載入 SQL 資料倉儲][Load data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="ed513-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="ed513-181">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="ed513-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
