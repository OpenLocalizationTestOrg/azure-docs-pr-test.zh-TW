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
# <a name="get-started-with-u-sql"></a>開始使用 U-SQL
U SQL 是一種語言，結合了宣告式 SQL 命令式 C# toolet 與您在處理資料的任何標尺。 透過 hello 可擴充、 分散式查詢功能的 U-SQL，您可以有效率地跨關聯式存放區，例如 Azure SQL Database 中分析資料。 使用 U-SQL，您可以藉由在讀取時套用結構描述並插入自訂邏輯和 UDF，來處理非結構化資料。 此外，U-SQL 包括擴充性，可讓您更細微的控制如何在標尺 tooexecute。 

## <a name="learning-resources"></a>學習資源

* hello [U-SQL 教學課程](http://aka.ms/usqltutorial)提供的大部分的 hello U-SQL 語言逐步的解說。 這份文件，建議您使用適用於所有開發人員想 toolearn U-SQL 讀取。
* 如需 hello **U-SQL 語言語法**，看到 hello [U SQL 語言參考](http://go.microsoft.com/fwlink/p/?LinkId=691348)。
* toounderstand hello **U-SQL 設計原理**，請參閱 hello Visual Studio 部落格文章[簡介 U-SQL – 語言，以簡化巨量資料處理](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)。

## <a name="prerequisites"></a>必要條件

您瀏覽此文件中的 hello U-SQL 範例之前，請閱讀並完成[教學課程： 使用 Data Lake Tools for Visual Studio 的開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。 該教學課程說明使用 Azure 資料湖 Tools for Visual Studio U-SQL 的 hello 機制。

## <a name="your-first-u-sql-script"></a>您的第一個 U-SQL 指令碼

遵循 U-SQL 指令碼的 hello 很簡單，而且讓我們可探討許多層面 hello U-SQL 語言。

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

此指令碼沒有任何轉換步驟。 它會從呼叫 hello 原始程式檔讀取`SearchLog.tsv`、 schematizes，並寫回至檔案，稱為 SearchLog 第一個-u sql.csv hello 資料列集。

請注意 hello 問號下一步 toohello 中的資料類型 hello`Duration`欄位。 這表示該 hello`Duration`欄位可以是 null。

### <a name="key-concepts"></a>重要概念
* **資料列集變數**: tooa 變數可以指派每個產生的資料列集的查詢運算式。 U-SQL 遵循 hello T-SQL 變數的命名模式 (`@searchlog`，例如) hello 指令碼中。
* hello**擷取**關鍵字會從檔案讀取資料，並在讀取定義 hello 結構描述。 `Extractors.Tsv` 是內建的 U-SQL 擷取器，適用於以定位點分隔值的檔案。 您可以開發自訂擷取器。
* hello**輸出**資料寫入資料列集 tooa 檔案。 `Outputters.Csv()`是內建的 U-SQL outputter toocreate 逗點分隔值檔案。 您可以開發自訂輸出器。

### <a name="file-paths"></a>檔案路徑

hello 擷取和輸出的陳述式使用的檔案路徑。 檔案路徑可以是絕對或相對路徑：

此下列的絕對檔案路徑是指 tooa 檔案中名為 Data Lake Store `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

下面這個檔案路徑的開頭為 `"/"`。 它會參考 tooa hello 預設 Data Lake Store 帳戶中的檔案：

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>使用純量變數

您可以使用純量變數作為以及 toomake 指令碼維護更容易。 hello 先前 U-SQL 指令碼也可以寫成：

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

## <a name="transform-rowsets"></a>轉換資料列集

使用**選取**tootransform 資料列集：

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

hello WHERE 子句使用[C# 布林運算式](https://msdn.microsoft.com/library/6a71f45d.aspx)。 您可以使用 hello C# 運算式語言 toodo 您自己的運算式和函數。 您甚至可以將它們與邏輯結合 (AND) 和邏輯分離 (OR) 做結合，以執行更複雜的篩選。

hello 下列指令碼會使用 hello DateTime.Parse() 方法並搭配使用。

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
 >hello 第二個查詢正在對 hello hello 第一個資料列集，會建立複合 hello 的兩個篩選條件的結果。 您也可以重複使用的變數名稱，並 hello 名稱的語彙範圍。

## <a name="aggregate-rowsets"></a>彙總資料列集
U SQL 可讓您 hello 熟悉 ORDER BY、 GROUP BY 及彙總。

hello 下列查詢尋找 hello 總持續時間，每個區域，並顯示 hello 前五個持續時間順序。

U SQL 資料列集不會保留其 hello 下一個查詢的順序。 因此，tooorder 的輸出，您需要 tooadd ORDER BY toohello 輸出陳述式：

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

hello U-SQL ORDER BY 子句時，需要使用 hello FETCH 子句，SELECT 運算式中。

hello U-SQL HAVING 子句可以使用的 toorestrict hello 輸出 toogroups 滿足 hello HAVING 條件的：

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

進階的彙總的情況下，請參閱 hello hello U-SQL 參考文件[彙總、 分析，並參考函式](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>後續步驟
* [Microsoft Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
* [使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)
