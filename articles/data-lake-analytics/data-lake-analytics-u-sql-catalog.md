---
title: "開始使用 U-SQL 目錄 | Microsoft Docs"
description: "了解如何使用 U-SQL 目錄來共用程式碼和資料。"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="09efa-103">開始使用 U-SQL 目錄</span><span class="sxs-lookup"><span data-stu-id="09efa-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="09efa-104">建立 TVF</span><span class="sxs-lookup"><span data-stu-id="09efa-104">Create a TVF</span></span>

<span data-ttu-id="09efa-105">在先前的 U-SQL 指令碼中，您重複使用 EXTRACT 來從相同原始程式檔進行讀取。</span><span class="sxs-lookup"><span data-stu-id="09efa-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="09efa-106">使用 U-SQL 資料表值函式 (TVF)，您就可以封裝資料以供日後重複使用。</span><span class="sxs-lookup"><span data-stu-id="09efa-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="09efa-107">下列指令碼會在預設的資料庫和結構描述中建立名為 `Searchlog()` 的 TVF：</span><span class="sxs-lookup"><span data-stu-id="09efa-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

<span data-ttu-id="09efa-108">下列指令碼會示範如何使用先前的指令碼中定義的 TVF：</span><span class="sxs-lookup"><span data-stu-id="09efa-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="09efa-109">建立檢視</span><span class="sxs-lookup"><span data-stu-id="09efa-109">Create views</span></span>

<span data-ttu-id="09efa-110">如果您有單一查詢運算式，則您可以不使用 TVF，而是使用「U-SQL 檢視」來封裝該運算式。</span><span class="sxs-lookup"><span data-stu-id="09efa-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="09efa-111">下列指令碼會在預設的資料庫和結構描述中建立名為 `SearchlogView` 的 視：</span><span class="sxs-lookup"><span data-stu-id="09efa-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

<span data-ttu-id="09efa-112">下列指令碼示範如何使用定義的檢視：</span><span class="sxs-lookup"><span data-stu-id="09efa-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="09efa-113">建立資料表</span><span class="sxs-lookup"><span data-stu-id="09efa-113">Create tables</span></span>
<span data-ttu-id="09efa-114">和關聯式資料庫資料表一樣，使用 U-SQL 可讓您使用預先定義的結構描述建立資料表，或建立資料表以從填入資料表的查詢推斷結構描述 (也就是 CREATE TABLE AS SELECT 或 CTAS)。</span><span class="sxs-lookup"><span data-stu-id="09efa-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="09efa-115">使用下列指令碼建立一個資料庫和兩個資料表：</span><span class="sxs-lookup"><span data-stu-id="09efa-115">Create a database and two tables by using the following script:</span></span>

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a><span data-ttu-id="09efa-116">查詢資料表</span><span class="sxs-lookup"><span data-stu-id="09efa-116">Query tables</span></span>
<span data-ttu-id="09efa-117">您可以運用和查詢資料檔案一樣的方式來查詢資料表 (例如，上一個指令碼所建立的資料表)。</span><span class="sxs-lookup"><span data-stu-id="09efa-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="09efa-118">您現在可以直接參考資料表名稱，而不必使用 EXTRACT 建立資料列集。</span><span class="sxs-lookup"><span data-stu-id="09efa-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="09efa-119">若要從資料表進行讀取，請修改您先前使用的轉換指令碼：</span><span class="sxs-lookup"><span data-stu-id="09efa-119">To read from the tables, modify the transform script that you used previously:</span></span>

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="09efa-120">您目前無法在用來建立資料表的相同指令碼中，對該資料表執行 SELECT。</span><span class="sxs-lookup"><span data-stu-id="09efa-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09efa-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09efa-121">Next Steps</span></span>
* [<span data-ttu-id="09efa-122">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="09efa-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="09efa-123">使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="09efa-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="09efa-124">使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 作業</span><span class="sxs-lookup"><span data-stu-id="09efa-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
