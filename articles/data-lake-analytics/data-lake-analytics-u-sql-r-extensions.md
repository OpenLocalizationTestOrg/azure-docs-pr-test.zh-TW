---
title: "aaaExtend U-SQL 指令碼以在 Azure Data Lake Analytics R |Microsoft 文件"
description: "了解 toorun R U-SQL 指令碼中的程式碼"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>教學課程︰開始使用 R 擴充 U-SQL

hello 下列範例將說明 hello 部署 R 程式碼的基本步驟：
* 使用 hello `REFERENCE ASSEMBLY` hello U-SQL 指令碼陳述式 tooenable R 擴充功能。
* 使用` REDUCE`作業 toopartition hello 輸入在索引鍵的資料。
* U-SQL hello R 擴充功能包含內建減壓器 (`Extension.R.Reducer`) 每個頂點指派 toohello 減壓器上執行的 R 程式碼。 
* 使用專用的具名資料框架稱為`inputFromUSQL`和`outputToUSQL `分別 toopass 資料 U SQL 與。 輸入和輸出之間的資料框架的識別項名稱固定 （亦即，使用者無法變更這些預先定義的名稱的輸入和輸出資料框架識別項）。

## <a name="embedding-r-code-in-hello-u-sql-script"></a>Hello U-SQL 指令碼中的內嵌 R 程式碼

您可以內嵌 hello R 程式碼 U-SQL 指令碼使用 hello 命令參數的 hello `Extension.R.Reducer`。 例如，您可以宣告 hello 做為字串變數的 R 指令碼，並將它傳遞為參數 toohello 減壓器。


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>在不同的檔案保持 hello R 程式碼，並參考該 hello U-SQL 指令碼

下列範例中的 hello 說明更複雜的使用方式。 在此情況下，hello R 程式碼會部署為 hello U-SQL 指令碼的資源。

將此 R 程式碼儲存為個別的檔案。

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

使用 R 指令碼 U-SQL 指令碼 toodeploy 以 hello 部署的資源陳述式。

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a>R 如何與 U-SQL 整合

### <a name="datatypes"></a>資料類型
* 來自 U-SQL 的字串和數值資料行會在 R 資料框架和 U-SQL 之間以現狀進行轉換 [支援的類型：`double``string`、`bool`、`integer`、`byte`]。
* hello `Factor` U SQL 中不支援資料類型。
* `byte[]` 必須序列化為 base64 編碼的 `string`。
* U-SQL 字串可以轉換的 toofactors 在 R 程式碼中，一旦 U-SQL 建立 R 輸入資料框架，或由設定 hello 減壓器參數`stringsAsFactors: true`。

### <a name="schemas"></a>結構描述
* U-SQL 資料集不能有重複的資料行名稱。
* U-SQL 資料集的資料行名稱必須為字串。
* 資料行名稱必須 hello 相同 U SQL 與 R 指令碼中。
* 唯讀資料行不能 hello 輸出資料框架的一部分。 因為它屬於 UDO 的輸出結構描述，唯讀資料行自動插入 hello U-SQL 資料表中。

### <a name="functional-limitations"></a>功能限制：
* hello R 引擎無法具現化兩次在 hello 相同的程序。 
* 目前，在以歸納器 UDO 所產生的分割模型進行預測時，U-SQL 不支援使用合併器 UDO。 使用者可以宣告為資源的 hello 分割模型，並將其用於其 R 指令碼 (請參閱範例程式碼`ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>R 版本
僅支援 R 3.2.2。

### <a name="standard-r-modules"></a>標準的 R 模組

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a>輸入和輸出的大小限制
每個頂點都有指派 tooit 的記憶體數量有限。 Hello 輸入和輸出資料框架必須存在於記憶體中 hello R 程式碼，因為 hello hello 輸入和輸出大小總計不得超過 500 MB。

### <a name="sample-code"></a>範例程式碼
您安裝 hello U-SQL 進階分析擴充功能之後，您 Data Lake Store 帳戶中所提供更多的範例程式碼。 hello 更多的範例程式碼路徑是： `<your_account_address>/usqlext/samples/R`。 

## <a name="deploying-custom-r-modules-with-u-sql"></a>使用 U-SQL 部署自訂 R 模組

首先，建立自訂 R 模組和 zip 它，然後上傳 hello zipped R 自訂模組檔案 tooyour ADL 存放區。 在 hello 範例中，我們將上傳 magittr_1.5.zip toohello 根 hello 預設 ADLS 帳戶的 hello ADLA 我們使用的帳戶。 一旦您上傳 hello 模組 tooADL 存放區，將它宣告為使用部署資源 toomake U-SQL 指令碼與呼叫中提供`install.packages`tooinstall 它。

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a>後續步驟
* [Microsoft Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
* [使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)
* [針對 Azure 資料湖分析工作使用 U-SQL 視窗函式](data-lake-analytics-use-window-functions.md)
