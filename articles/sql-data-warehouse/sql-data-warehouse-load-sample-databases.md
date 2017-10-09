---
title: "aaaLoad 範例資料插入 SQL 資料倉儲 |Microsoft 文件"
description: "將範例資料載入 SQL 資料倉儲"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="451d4-103">將範例資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="451d4-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="451d4-104">請遵循這些簡單的步驟 tooload 和查詢 hello Adventure Works 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="451d4-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="451d4-105">這些指令碼會先使用 sqlcmd toorun SQL 將會建立資料表和檢視表。</span><span class="sxs-lookup"><span data-stu-id="451d4-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="451d4-106">一旦已建立資料表，hello 指令碼會使用 bcp tooload 資料。</span><span class="sxs-lookup"><span data-stu-id="451d4-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="451d4-107">如果您還沒有 sqlcmd 和 bcp 安裝，請遵循這些連結太[安裝 bcp] [ install bcp]和太[安裝 sqlcmd][install sqlcmd]。</span><span class="sxs-lookup"><span data-stu-id="451d4-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="451d4-108">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="451d4-108">Load sample data</span></span>
1. <span data-ttu-id="451d4-109">下載 hello [SQL 資料倉儲的 Adventure Works 範例指令碼][ Adventure Works Sample Scripts for SQL Data Warehouse] zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="451d4-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="451d4-110">解壓縮 hello 檔案從本機電腦上的已下載之 zip tooa 目錄。</span><span class="sxs-lookup"><span data-stu-id="451d4-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="451d4-111">編輯 hello 解壓縮檔案 aw_create.bat，並設定下列在 hello hello 檔案頂端找到變數 hello。</span><span class="sxs-lookup"><span data-stu-id="451d4-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="451d4-112">為確定 tooleave hello"="hello 參數之間沒有空格。</span><span class="sxs-lookup"><span data-stu-id="451d4-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="451d4-113">以下是您可能會想看看如何編輯的範例。</span><span class="sxs-lookup"><span data-stu-id="451d4-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="451d4-114">從 Windows 命令提示字元中，執行編輯的 hello aw_create.bat。</span><span class="sxs-lookup"><span data-stu-id="451d4-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="451d4-115">請確定您是在您儲存 aw_create.bat 您編輯的過的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="451d4-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="451d4-116">此指令碼將...</span><span class="sxs-lookup"><span data-stu-id="451d4-116">This script will...</span></span>
   
   * <span data-ttu-id="451d4-117">卸除任何 Adventure Works 資料表或任何已存在資料庫中的檢視表</span><span class="sxs-lookup"><span data-stu-id="451d4-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="451d4-118">建立 hello Adventure Works 資料表和檢視表</span><span class="sxs-lookup"><span data-stu-id="451d4-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="451d4-119">使用 bcp 載入每個 Adventure Works 資料表</span><span class="sxs-lookup"><span data-stu-id="451d4-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="451d4-120">驗證 hello Adventure Works 的每個資料表的資料列計數</span><span class="sxs-lookup"><span data-stu-id="451d4-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="451d4-121">收集每個 Adventure Works 資料表之所有資料行上的統計資料</span><span class="sxs-lookup"><span data-stu-id="451d4-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="451d4-122">查詢範例資料</span><span class="sxs-lookup"><span data-stu-id="451d4-122">Query sample data</span></span>
<span data-ttu-id="451d4-123">一旦已經將某些範例資料載入您的 SQL 資料倉儲中，就可以快速地執行幾個查詢。</span><span class="sxs-lookup"><span data-stu-id="451d4-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="451d4-124">hello 中所述，toorun 查詢時，連接 tooyour 新建 Adventure Works 資料庫中使用 Visual Studio 和 SSDT 中，Azure SQL DW [Visual Studio 中的查詢][ query with Visual Studio]文件。</span><span class="sxs-lookup"><span data-stu-id="451d4-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="451d4-125">簡單的範例選取陳述式 tooget hello 員工的所有 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="451d4-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="451d4-126">每一天所有銷售使用建構，例如 GROUP BY toolook hello 總量在更複雜的查詢範例：</span><span class="sxs-lookup"><span data-stu-id="451d4-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="451d4-127">SELECT 與 WHERE 子句 toofilter 出訂單在特定日期之前的範例：</span><span class="sxs-lookup"><span data-stu-id="451d4-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="451d4-128">SQL 資料倉儲幾乎支援所有 SQL Server 支援的 T-SQL 建構。</span><span class="sxs-lookup"><span data-stu-id="451d4-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="451d4-129">所有的差異都記錄在[移轉程式碼][migrate code]文件中。</span><span class="sxs-lookup"><span data-stu-id="451d4-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="451d4-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="451d4-130">Next steps</span></span>
<span data-ttu-id="451d4-131">既然您已有機會 tootry 某些查詢的範例資料，請參閱如何太[開發][develop]，[載入][load]，或[移轉][ migrate] tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="451d4-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
