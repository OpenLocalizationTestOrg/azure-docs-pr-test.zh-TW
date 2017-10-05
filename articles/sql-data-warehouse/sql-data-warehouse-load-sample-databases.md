---
title: "將範例資料載入 SQL 資料倉儲 | Microsoft Docs"
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
ms.openlocfilehash: 1e0df958a2f18fe1e988168918e5cfd293f84e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="767c7-103">將範例資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="767c7-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="767c7-104">請遵循下列簡單的步驟來載入和查詢 Adventure Works 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="767c7-104">Follow these simple steps to load and query the Adventure Works Sample database.</span></span> <span data-ttu-id="767c7-105">這些指令碼會先使用 sqlcmd 來執行將建立資料表和檢視表的 SQL。</span><span class="sxs-lookup"><span data-stu-id="767c7-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span></span> <span data-ttu-id="767c7-106">一旦建立資料表之後，指令碼將使用 bcp 來載入資料。</span><span class="sxs-lookup"><span data-stu-id="767c7-106">Once tables have been created, the scripts will use bcp to load data.</span></span>  <span data-ttu-id="767c7-107">如果您還沒有安裝 sqlcmd 和 bcp，請依照下列連結來[安裝 bcp][install bcp] 和[安裝 sqlcmd][install sqlcmd]。</span><span class="sxs-lookup"><span data-stu-id="767c7-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="767c7-108">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="767c7-108">Load sample data</span></span>
1. <span data-ttu-id="767c7-109">下載[適用於 SQL 資料倉儲的 Adventure Works 範例指令碼][Adventure Works Sample Scripts for SQL Data Warehouse] zip 檔。</span><span class="sxs-lookup"><span data-stu-id="767c7-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="767c7-110">請從下載的 zip 將檔案解壓縮到本機電腦上的目錄。</span><span class="sxs-lookup"><span data-stu-id="767c7-110">Extract the files from downloaded zip to a directory on your local machine.</span></span>
3. <span data-ttu-id="767c7-111">編輯解壓縮的 aw_create.bat 檔案，並設定下列可在檔案頂端找到的變數。</span><span class="sxs-lookup"><span data-stu-id="767c7-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span></span>  <span data-ttu-id="767c7-112">請務必不要在 "=" 和參數之間留有空白。</span><span class="sxs-lookup"><span data-stu-id="767c7-112">Be sure to leave no whitespace between the "=" and the parameter.</span></span>  <span data-ttu-id="767c7-113">以下是您可能會想看看如何編輯的範例。</span><span class="sxs-lookup"><span data-stu-id="767c7-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="767c7-114">從 Windows 命令提示字元執行編輯過的 aw_create.bat。</span><span class="sxs-lookup"><span data-stu-id="767c7-114">From a Windows cmd prompt, run the edited aw_create.bat.</span></span>  <span data-ttu-id="767c7-115">請確定您所在的目錄是您儲存編輯過之 aw_create.bat 版本的位置。</span><span class="sxs-lookup"><span data-stu-id="767c7-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="767c7-116">此指令碼將...</span><span class="sxs-lookup"><span data-stu-id="767c7-116">This script will...</span></span>
   
   * <span data-ttu-id="767c7-117">卸除任何 Adventure Works 資料表或任何已存在資料庫中的檢視表</span><span class="sxs-lookup"><span data-stu-id="767c7-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="767c7-118">建立 Adventure Works 資料表和檢視表</span><span class="sxs-lookup"><span data-stu-id="767c7-118">Create the Adventure Works tables and views</span></span>
   * <span data-ttu-id="767c7-119">使用 bcp 載入每個 Adventure Works 資料表</span><span class="sxs-lookup"><span data-stu-id="767c7-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="767c7-120">驗證每個 Adventure Works 資料表的資料列計數</span><span class="sxs-lookup"><span data-stu-id="767c7-120">Validate the row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="767c7-121">收集每個 Adventure Works 資料表之所有資料行上的統計資料</span><span class="sxs-lookup"><span data-stu-id="767c7-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="767c7-122">查詢範例資料</span><span class="sxs-lookup"><span data-stu-id="767c7-122">Query sample data</span></span>
<span data-ttu-id="767c7-123">一旦已經將某些範例資料載入您的 SQL 資料倉儲中，就可以快速地執行幾個查詢。</span><span class="sxs-lookup"><span data-stu-id="767c7-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="767c7-124">若要執行查詢，請使用 Visual Studio 和 SSDT 連接 Azure SQL DW 中新建立的 Adventure Works 資料庫，如[使用 Visual Studio 查詢][query with Visual Studio]文件中所述。</span><span class="sxs-lookup"><span data-stu-id="767c7-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="767c7-125">可取得員工之所有資訊的簡單 select 陳述式範例：</span><span class="sxs-lookup"><span data-stu-id="767c7-125">Example of simple select statement to get all the info of the employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="767c7-126">使用建構 (例如 GROUP BY) 來查看每一天所有銷售之總金額的較複雜查詢範例：</span><span class="sxs-lookup"><span data-stu-id="767c7-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="767c7-127">可篩選掉特定日期前之訂單的 SELECT 搭配 WHERE 子句的範例：</span><span class="sxs-lookup"><span data-stu-id="767c7-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="767c7-128">SQL 資料倉儲幾乎支援所有 SQL Server 支援的 T-SQL 建構。</span><span class="sxs-lookup"><span data-stu-id="767c7-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="767c7-129">所有的差異都記錄在[移轉程式碼][migrate code]文件中。</span><span class="sxs-lookup"><span data-stu-id="767c7-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="767c7-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="767c7-130">Next steps</span></span>
<span data-ttu-id="767c7-131">現在您已經有機會搭配範例資料嘗試一些查詢，請參閱以了解如何[開發][develop]、[載入][load]，或[移轉][migrate]到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="767c7-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span></span>

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
