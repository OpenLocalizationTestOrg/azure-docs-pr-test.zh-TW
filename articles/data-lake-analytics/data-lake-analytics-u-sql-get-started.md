---
title: "開始使用 U-SQL 語言 | Microsoft Docs"
description: "了解 U-SQL 語言的基礎概念。"
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
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 38c4e1b9bd24ef0b8a81f6154620f3f98d3b5ac1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="7a266-103">開始使用 U-SQL</span><span class="sxs-lookup"><span data-stu-id="7a266-103">Get started with U-SQL</span></span>
<span data-ttu-id="7a266-104">U-SQL 是一種語言，結合了宣告式 SQL 與命令式 C#，可讓您處理任何規模的資料。</span><span class="sxs-lookup"><span data-stu-id="7a266-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span></span> <span data-ttu-id="7a266-105">透過 U-SQL 的可調整分散式查詢功能，您可以有效率地分析各關聯式存放區 (Azure SQL Database) 中的資料。</span><span class="sxs-lookup"><span data-stu-id="7a266-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="7a266-106">使用 U-SQL，您可以藉由在讀取時套用結構描述並插入自訂邏輯和 UDF，來處理非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="7a266-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="7a266-107">此外，U-SQL 所含有的擴充性可讓您細微控制如何大規模執行。</span><span class="sxs-lookup"><span data-stu-id="7a266-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="7a266-108">學習資源</span><span class="sxs-lookup"><span data-stu-id="7a266-108">Learning resources</span></span>

* <span data-ttu-id="7a266-109">[U-SQL 教學課程](http://aka.ms/usqltutorial)提供大多數 U-SQL 語言的引導式逐步解說。</span><span class="sxs-lookup"><span data-stu-id="7a266-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span></span> <span data-ttu-id="7a266-110">本文件的建議閱讀對象是所有想要學習 U-SQL 的開發人員。</span><span class="sxs-lookup"><span data-stu-id="7a266-110">This document is recommended reading for all developers wanting to learn U-SQL.</span></span>
* <span data-ttu-id="7a266-111">如需 **U-SQL 語言語法**的詳細資訊，請參閱 [U-SQL 語言參考 (英文)](http://go.microsoft.com/fwlink/p/?LinkId=691348)。</span><span class="sxs-lookup"><span data-stu-id="7a266-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="7a266-112">若要了解 U-SQL 的設計原理，請參閱 Visual Studio 部落格文章[簡介 U-SQL – 讓巨量資料的處理變簡單的語言 (英文)](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)。</span><span class="sxs-lookup"><span data-stu-id="7a266-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a266-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a266-113">Prerequisites</span></span>

<span data-ttu-id="7a266-114">在進行本文中的 U-SQL 範例前，請閱讀並完成[教學課程：使用適用於 Visual Studio 的 Data Lake 工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="7a266-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="7a266-115">本教學課程說明將 U-SQL 搭配 Azure Data Lake Tools for Visual Studio 使用的機制。</span><span class="sxs-lookup"><span data-stu-id="7a266-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="7a266-116">您的第一個 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="7a266-116">Your first U-SQL script</span></span>

<span data-ttu-id="7a266-117">以下是一個簡單的 U-SQL 指令碼，可讓我們探索 U-SQL 語言的許多層面。</span><span class="sxs-lookup"><span data-stu-id="7a266-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span></span>

```
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

OUTPUT @searchlog   
    TO "/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="7a266-118">此指令碼沒有任何轉換步驟。</span><span class="sxs-lookup"><span data-stu-id="7a266-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="7a266-119">它會從名為 `SearchLog.tsv` 的原始程式檔讀取資料，為其建立結構描述，並將資料列集回寫到名為 SearchLog-first-u-sql.csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a266-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="7a266-120">請注意 `Duration` 欄位中資料類型旁的問號，</span><span class="sxs-lookup"><span data-stu-id="7a266-120">Notice the question mark next to the data type in the `Duration` field.</span></span> <span data-ttu-id="7a266-121">它表示 `Duration` 欄位可能是 null。</span><span class="sxs-lookup"><span data-stu-id="7a266-121">It means that the `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="7a266-122">重要概念</span><span class="sxs-lookup"><span data-stu-id="7a266-122">Key concepts</span></span>
* <span data-ttu-id="7a266-123">**資料列集變數**：每個會產生資料列集的查詢運算式都可以指派給變數。</span><span class="sxs-lookup"><span data-stu-id="7a266-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="7a266-124">在指令碼中，U-SQL 會遵循 T-SQL 變數命名模式 (例如 `@searchlog`)。</span><span class="sxs-lookup"><span data-stu-id="7a266-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span></span>
* <span data-ttu-id="7a266-125">EXTRACT 關鍵字會從檔案讀取資料，並在讀取時定義結構描述。</span><span class="sxs-lookup"><span data-stu-id="7a266-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span></span> <span data-ttu-id="7a266-126">`Extractors.Tsv` 是內建的 U-SQL 擷取器，適用於以定位點分隔值的檔案。</span><span class="sxs-lookup"><span data-stu-id="7a266-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="7a266-127">您可以開發自訂擷取器。</span><span class="sxs-lookup"><span data-stu-id="7a266-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="7a266-128">OUTPUT 會將資料列集的資料寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="7a266-128">The **OUTPUT** writes data from a rowset to a file.</span></span> <span data-ttu-id="7a266-129">`Outputters.Csv()` 是內建的 U-SQL 輸出器，用於建立以逗號分隔值的檔案。</span><span class="sxs-lookup"><span data-stu-id="7a266-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span></span> <span data-ttu-id="7a266-130">您可以開發自訂輸出器。</span><span class="sxs-lookup"><span data-stu-id="7a266-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="7a266-131">檔案路徑</span><span class="sxs-lookup"><span data-stu-id="7a266-131">File paths</span></span>

<span data-ttu-id="7a266-132">EXTRACT 與 OUTPUT 陳述式使用檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="7a266-132">The EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="7a266-133">檔案路徑可以是絕對或相對路徑：</span><span class="sxs-lookup"><span data-stu-id="7a266-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="7a266-134">下面這個絕對檔案路徑會參考名為 `mystore` 的 Data Lake Store 中的檔案：</span><span class="sxs-lookup"><span data-stu-id="7a266-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="7a266-135">下面這個檔案路徑的開頭為 `"/"`。</span><span class="sxs-lookup"><span data-stu-id="7a266-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="7a266-136">它會參考預設 Data Lake Store 帳戶中的檔案：</span><span class="sxs-lookup"><span data-stu-id="7a266-136">It refers to a file in the default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="7a266-137">使用純量變數</span><span class="sxs-lookup"><span data-stu-id="7a266-137">Use scalar variables</span></span>

<span data-ttu-id="7a266-138">您也可以使用純量變數以方便維護指令碼。</span><span class="sxs-lookup"><span data-stu-id="7a266-138">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="7a266-139">前述 U-SQL 指令碼也可以撰寫成：</span><span class="sxs-lookup"><span data-stu-id="7a266-139">The previous U-SQL script can also be written as:</span></span>

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO @out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="7a266-140">轉換資料列集</span><span class="sxs-lookup"><span data-stu-id="7a266-140">Transform rowsets</span></span>

<span data-ttu-id="7a266-141">使用 **SELECT** 來轉換資料列集：</span><span class="sxs-lookup"><span data-stu-id="7a266-141">Use **SELECT** to transform rowsets:</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="7a266-142">WHERE 子句使用 [C# 布林運算式](https://msdn.microsoft.com/library/6a71f45d.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7a266-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="7a266-143">您可以使用 C# 運算式語言來建置自己的運算式和函式。</span><span class="sxs-lookup"><span data-stu-id="7a266-143">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="7a266-144">您甚至可以將它們與邏輯結合 (AND) 和邏輯分離 (OR) 做結合，以執行更複雜的篩選。</span><span class="sxs-lookup"><span data-stu-id="7a266-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="7a266-145">下列指令碼使用 DateTime.Parse() 方法和邏輯結合。</span><span class="sxs-lookup"><span data-stu-id="7a266-145">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="7a266-146">第二個查詢會對第一個資料列集的結果起作用，因而建立兩個篩選條件的組合。</span><span class="sxs-lookup"><span data-stu-id="7a266-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="7a266-147">您也可以重複使用變數名稱，因為它們是語彙範圍型名稱。</span><span class="sxs-lookup"><span data-stu-id="7a266-147">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="7a266-148">彙總資料列集</span><span class="sxs-lookup"><span data-stu-id="7a266-148">Aggregate rowsets</span></span>
<span data-ttu-id="7a266-149">U-SQL 提供您已熟悉使用的 ORDER BY、GROUP BY 和各種彙總語法。</span><span class="sxs-lookup"><span data-stu-id="7a266-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="7a266-150">下列查詢會尋找每個區域的總持續時間，然後按順序顯示前五大持續時間。</span><span class="sxs-lookup"><span data-stu-id="7a266-150">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="7a266-151">U-SQL 資料列集不會保留它們的順序以供下一次查詢使用。</span><span class="sxs-lookup"><span data-stu-id="7a266-151">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="7a266-152">因此，若要對輸出排序，您需要將 ORDER BY 新增至 OUTPUT 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7a266-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

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

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        TO @out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        TO @out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="7a266-153">U-SQL ORDER BY 子句必須在 SELECT 運算式中使用 FETCH 子句。</span><span class="sxs-lookup"><span data-stu-id="7a266-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="7a266-154">U-SQL 的 HAVING 子句可以用來將輸出限制為符合 HAVING 條件的群組：</span><span class="sxs-lookup"><span data-stu-id="7a266-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

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

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        TO "/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="7a266-155">如需進階的彙總案例，請參閱 U-SQL 的[彙總、分析及參考函式](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)參考文件</span><span class="sxs-lookup"><span data-stu-id="7a266-155">For advanced aggregation scenarios, see the The U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a266-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a266-156">Next steps</span></span>
* [<span data-ttu-id="7a266-157">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="7a266-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="7a266-158">使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="7a266-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
