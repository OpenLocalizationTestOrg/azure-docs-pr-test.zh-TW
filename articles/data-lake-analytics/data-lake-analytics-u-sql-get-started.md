---
title: "開始使用 U-SQL 語言 | Microsoft Docs"
description: "了解 hello 的 hello U SQL 語言的基本概念。"
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
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="99d63-103">開始使用 U-SQL</span><span class="sxs-lookup"><span data-stu-id="99d63-103">Get started with U-SQL</span></span>
<span data-ttu-id="99d63-104">U SQL 是一種語言，結合了宣告式 SQL 命令式 C# toolet 與您在處理資料的任何標尺。</span><span class="sxs-lookup"><span data-stu-id="99d63-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="99d63-105">透過 hello 可擴充、 分散式查詢功能的 U-SQL，您可以有效率地跨關聯式存放區，例如 Azure SQL Database 中分析資料。</span><span class="sxs-lookup"><span data-stu-id="99d63-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="99d63-106">使用 U-SQL，您可以藉由在讀取時套用結構描述並插入自訂邏輯和 UDF，來處理非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="99d63-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="99d63-107">此外，U-SQL 包括擴充性，可讓您更細微的控制如何在標尺 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="99d63-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="99d63-108">學習資源</span><span class="sxs-lookup"><span data-stu-id="99d63-108">Learning resources</span></span>

* <span data-ttu-id="99d63-109">hello [U-SQL 教學課程](http://aka.ms/usqltutorial)提供的大部分的 hello U-SQL 語言逐步的解說。</span><span class="sxs-lookup"><span data-stu-id="99d63-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="99d63-110">這份文件，建議您使用適用於所有開發人員想 toolearn U-SQL 讀取。</span><span class="sxs-lookup"><span data-stu-id="99d63-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="99d63-111">如需 hello **U-SQL 語言語法**，看到 hello [U SQL 語言參考](http://go.microsoft.com/fwlink/p/?LinkId=691348)。</span><span class="sxs-lookup"><span data-stu-id="99d63-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="99d63-112">toounderstand hello **U-SQL 設計原理**，請參閱 hello Visual Studio 部落格文章[簡介 U-SQL – 語言，以簡化巨量資料處理](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)。</span><span class="sxs-lookup"><span data-stu-id="99d63-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99d63-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="99d63-113">Prerequisites</span></span>

<span data-ttu-id="99d63-114">您瀏覽此文件中的 hello U-SQL 範例之前，請閱讀並完成[教學課程： 使用 Data Lake Tools for Visual Studio 的開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="99d63-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="99d63-115">該教學課程說明使用 Azure 資料湖 Tools for Visual Studio U-SQL 的 hello 機制。</span><span class="sxs-lookup"><span data-stu-id="99d63-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="99d63-116">您的第一個 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="99d63-116">Your first U-SQL script</span></span>

<span data-ttu-id="99d63-117">遵循 U-SQL 指令碼的 hello 很簡單，而且讓我們可探討許多層面 hello U-SQL 語言。</span><span class="sxs-lookup"><span data-stu-id="99d63-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="99d63-118">此指令碼沒有任何轉換步驟。</span><span class="sxs-lookup"><span data-stu-id="99d63-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="99d63-119">它會從呼叫 hello 原始程式檔讀取`SearchLog.tsv`、 schematizes，並寫回至檔案，稱為 SearchLog 第一個-u sql.csv hello 資料列集。</span><span class="sxs-lookup"><span data-stu-id="99d63-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="99d63-120">請注意 hello 問號下一步 toohello 中的資料類型 hello`Duration`欄位。</span><span class="sxs-lookup"><span data-stu-id="99d63-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="99d63-121">這表示該 hello`Duration`欄位可以是 null。</span><span class="sxs-lookup"><span data-stu-id="99d63-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="99d63-122">重要概念</span><span class="sxs-lookup"><span data-stu-id="99d63-122">Key concepts</span></span>
* <span data-ttu-id="99d63-123">**資料列集變數**: tooa 變數可以指派每個產生的資料列集的查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="99d63-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="99d63-124">U-SQL 遵循 hello T-SQL 變數的命名模式 (`@searchlog`，例如) hello 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="99d63-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="99d63-125">hello**擷取**關鍵字會從檔案讀取資料，並在讀取定義 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="99d63-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="99d63-126">`Extractors.Tsv` 是內建的 U-SQL 擷取器，適用於以定位點分隔值的檔案。</span><span class="sxs-lookup"><span data-stu-id="99d63-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="99d63-127">您可以開發自訂擷取器。</span><span class="sxs-lookup"><span data-stu-id="99d63-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="99d63-128">hello**輸出**資料寫入資料列集 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="99d63-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="99d63-129">`Outputters.Csv()`是內建的 U-SQL outputter toocreate 逗點分隔值檔案。</span><span class="sxs-lookup"><span data-stu-id="99d63-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="99d63-130">您可以開發自訂輸出器。</span><span class="sxs-lookup"><span data-stu-id="99d63-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="99d63-131">檔案路徑</span><span class="sxs-lookup"><span data-stu-id="99d63-131">File paths</span></span>

<span data-ttu-id="99d63-132">hello 擷取和輸出的陳述式使用的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="99d63-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="99d63-133">檔案路徑可以是絕對或相對路徑：</span><span class="sxs-lookup"><span data-stu-id="99d63-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="99d63-134">此下列的絕對檔案路徑是指 tooa 檔案中名為 Data Lake Store `mystore`:</span><span class="sxs-lookup"><span data-stu-id="99d63-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="99d63-135">下面這個檔案路徑的開頭為 `"/"`。</span><span class="sxs-lookup"><span data-stu-id="99d63-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="99d63-136">它會參考 tooa hello 預設 Data Lake Store 帳戶中的檔案：</span><span class="sxs-lookup"><span data-stu-id="99d63-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="99d63-137">使用純量變數</span><span class="sxs-lookup"><span data-stu-id="99d63-137">Use scalar variables</span></span>

<span data-ttu-id="99d63-138">您可以使用純量變數作為以及 toomake 指令碼維護更容易。</span><span class="sxs-lookup"><span data-stu-id="99d63-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="99d63-139">hello 先前 U-SQL 指令碼也可以寫成：</span><span class="sxs-lookup"><span data-stu-id="99d63-139">hello previous U-SQL script can also be written as:</span></span>

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
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="99d63-140">轉換資料列集</span><span class="sxs-lookup"><span data-stu-id="99d63-140">Transform rowsets</span></span>

<span data-ttu-id="99d63-141">使用**選取**tootransform 資料列集：</span><span class="sxs-lookup"><span data-stu-id="99d63-141">Use **SELECT** tootransform rowsets:</span></span>

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
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="99d63-142">hello WHERE 子句使用[C# 布林運算式](https://msdn.microsoft.com/library/6a71f45d.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99d63-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="99d63-143">您可以使用 hello C# 運算式語言 toodo 您自己的運算式和函數。</span><span class="sxs-lookup"><span data-stu-id="99d63-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="99d63-144">您甚至可以將它們與邏輯結合 (AND) 和邏輯分離 (OR) 做結合，以執行更複雜的篩選。</span><span class="sxs-lookup"><span data-stu-id="99d63-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="99d63-145">hello 下列指令碼會使用 hello DateTime.Parse() 方法並搭配使用。</span><span class="sxs-lookup"><span data-stu-id="99d63-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="99d63-146">hello 第二個查詢正在對 hello hello 第一個資料列集，會建立複合 hello 的兩個篩選條件的結果。</span><span class="sxs-lookup"><span data-stu-id="99d63-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="99d63-147">您也可以重複使用的變數名稱，並 hello 名稱的語彙範圍。</span><span class="sxs-lookup"><span data-stu-id="99d63-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="99d63-148">彙總資料列集</span><span class="sxs-lookup"><span data-stu-id="99d63-148">Aggregate rowsets</span></span>
<span data-ttu-id="99d63-149">U SQL 可讓您 hello 熟悉 ORDER BY、 GROUP BY 及彙總。</span><span class="sxs-lookup"><span data-stu-id="99d63-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="99d63-150">hello 下列查詢尋找 hello 總持續時間，每個區域，並顯示 hello 前五個持續時間順序。</span><span class="sxs-lookup"><span data-stu-id="99d63-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="99d63-151">U SQL 資料列集不會保留其 hello 下一個查詢的順序。</span><span class="sxs-lookup"><span data-stu-id="99d63-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="99d63-152">因此，tooorder 的輸出，您需要 tooadd ORDER BY toohello 輸出陳述式：</span><span class="sxs-lookup"><span data-stu-id="99d63-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="99d63-153">hello U-SQL ORDER BY 子句時，需要使用 hello FETCH 子句，SELECT 運算式中。</span><span class="sxs-lookup"><span data-stu-id="99d63-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="99d63-154">hello U-SQL HAVING 子句可以使用的 toorestrict hello 輸出 toogroups 滿足 hello HAVING 條件的：</span><span class="sxs-lookup"><span data-stu-id="99d63-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="99d63-155">進階的彙總的情況下，請參閱 hello hello U-SQL 參考文件[彙總、 分析，並參考函式](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="99d63-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="99d63-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99d63-156">Next steps</span></span>
* [<span data-ttu-id="99d63-157">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="99d63-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="99d63-158">使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="99d63-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
