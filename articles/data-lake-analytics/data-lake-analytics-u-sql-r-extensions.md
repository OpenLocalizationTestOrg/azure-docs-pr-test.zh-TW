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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="4e034-103">教學課程︰開始使用 R 擴充 U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e034-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="4e034-104">hello 下列範例將說明 hello 部署 R 程式碼的基本步驟：</span><span class="sxs-lookup"><span data-stu-id="4e034-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="4e034-105">使用 hello `REFERENCE ASSEMBLY` hello U-SQL 指令碼陳述式 tooenable R 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="4e034-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="4e034-106">使用` REDUCE`作業 toopartition hello 輸入在索引鍵的資料。</span><span class="sxs-lookup"><span data-stu-id="4e034-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="4e034-107">U-SQL hello R 擴充功能包含內建減壓器 (`Extension.R.Reducer`) 每個頂點指派 toohello 減壓器上執行的 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4e034-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="4e034-108">使用專用的具名資料框架稱為`inputFromUSQL`和`outputToUSQL `分別 toopass 資料 U SQL 與。 輸入和輸出之間的資料框架的識別項名稱固定 （亦即，使用者無法變更這些預先定義的名稱的輸入和輸出資料框架識別項）。</span><span class="sxs-lookup"><span data-stu-id="4e034-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="4e034-109">Hello U-SQL 指令碼中的內嵌 R 程式碼</span><span class="sxs-lookup"><span data-stu-id="4e034-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="4e034-110">您可以內嵌 hello R 程式碼 U-SQL 指令碼使用 hello 命令參數的 hello `Extension.R.Reducer`。</span><span class="sxs-lookup"><span data-stu-id="4e034-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="4e034-111">例如，您可以宣告 hello 做為字串變數的 R 指令碼，並將它傳遞為參數 toohello 減壓器。</span><span class="sxs-lookup"><span data-stu-id="4e034-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="4e034-112">在不同的檔案保持 hello R 程式碼，並參考該 hello U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="4e034-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="4e034-113">下列範例中的 hello 說明更複雜的使用方式。</span><span class="sxs-lookup"><span data-stu-id="4e034-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="4e034-114">在此情況下，hello R 程式碼會部署為 hello U-SQL 指令碼的資源。</span><span class="sxs-lookup"><span data-stu-id="4e034-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="4e034-115">將此 R 程式碼儲存為個別的檔案。</span><span class="sxs-lookup"><span data-stu-id="4e034-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="4e034-116">使用 R 指令碼 U-SQL 指令碼 toodeploy 以 hello 部署的資源陳述式。</span><span class="sxs-lookup"><span data-stu-id="4e034-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="4e034-117">R 如何與 U-SQL 整合</span><span class="sxs-lookup"><span data-stu-id="4e034-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="4e034-118">資料類型</span><span class="sxs-lookup"><span data-stu-id="4e034-118">Datatypes</span></span>
* <span data-ttu-id="4e034-119">來自 U-SQL 的字串和數值資料行會在 R 資料框架和 U-SQL 之間以現狀進行轉換 [支援的類型：`double``string`、`bool`、`integer`、`byte`]。</span><span class="sxs-lookup"><span data-stu-id="4e034-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="4e034-120">hello `Factor` U SQL 中不支援資料類型。</span><span class="sxs-lookup"><span data-stu-id="4e034-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="4e034-121">`byte[]` 必須序列化為 base64 編碼的 `string`。</span><span class="sxs-lookup"><span data-stu-id="4e034-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="4e034-122">U-SQL 字串可以轉換的 toofactors 在 R 程式碼中，一旦 U-SQL 建立 R 輸入資料框架，或由設定 hello 減壓器參數`stringsAsFactors: true`。</span><span class="sxs-lookup"><span data-stu-id="4e034-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="4e034-123">結構描述</span><span class="sxs-lookup"><span data-stu-id="4e034-123">Schemas</span></span>
* <span data-ttu-id="4e034-124">U-SQL 資料集不能有重複的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="4e034-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="4e034-125">U-SQL 資料集的資料行名稱必須為字串。</span><span class="sxs-lookup"><span data-stu-id="4e034-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="4e034-126">資料行名稱必須 hello 相同 U SQL 與 R 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="4e034-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="4e034-127">唯讀資料行不能 hello 輸出資料框架的一部分。</span><span class="sxs-lookup"><span data-stu-id="4e034-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="4e034-128">因為它屬於 UDO 的輸出結構描述，唯讀資料行自動插入 hello U-SQL 資料表中。</span><span class="sxs-lookup"><span data-stu-id="4e034-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="4e034-129">功能限制：</span><span class="sxs-lookup"><span data-stu-id="4e034-129">Functional limitations</span></span>
* <span data-ttu-id="4e034-130">hello R 引擎無法具現化兩次在 hello 相同的程序。</span><span class="sxs-lookup"><span data-stu-id="4e034-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="4e034-131">目前，在以歸納器 UDO 所產生的分割模型進行預測時，U-SQL 不支援使用合併器 UDO。</span><span class="sxs-lookup"><span data-stu-id="4e034-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="4e034-132">使用者可以宣告為資源的 hello 分割模型，並將其用於其 R 指令碼 (請參閱範例程式碼`ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="4e034-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="4e034-133">R 版本</span><span class="sxs-lookup"><span data-stu-id="4e034-133">R Versions</span></span>
<span data-ttu-id="4e034-134">僅支援 R 3.2.2。</span><span class="sxs-lookup"><span data-stu-id="4e034-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="4e034-135">標準的 R 模組</span><span class="sxs-lookup"><span data-stu-id="4e034-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="4e034-136">輸入和輸出的大小限制</span><span class="sxs-lookup"><span data-stu-id="4e034-136">Input and Output size limitations</span></span>
<span data-ttu-id="4e034-137">每個頂點都有指派 tooit 的記憶體數量有限。</span><span class="sxs-lookup"><span data-stu-id="4e034-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="4e034-138">Hello 輸入和輸出資料框架必須存在於記憶體中 hello R 程式碼，因為 hello hello 輸入和輸出大小總計不得超過 500 MB。</span><span class="sxs-lookup"><span data-stu-id="4e034-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="4e034-139">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="4e034-139">Sample Code</span></span>
<span data-ttu-id="4e034-140">您安裝 hello U-SQL 進階分析擴充功能之後，您 Data Lake Store 帳戶中所提供更多的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="4e034-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="4e034-141">hello 更多的範例程式碼路徑是： `<your_account_address>/usqlext/samples/R`。</span><span class="sxs-lookup"><span data-stu-id="4e034-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="4e034-142">使用 U-SQL 部署自訂 R 模組</span><span class="sxs-lookup"><span data-stu-id="4e034-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="4e034-143">首先，建立自訂 R 模組和 zip 它，然後上傳 hello zipped R 自訂模組檔案 tooyour ADL 存放區。</span><span class="sxs-lookup"><span data-stu-id="4e034-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="4e034-144">在 hello 範例中，我們將上傳 magittr_1.5.zip toohello 根 hello 預設 ADLS 帳戶的 hello ADLA 我們使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e034-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="4e034-145">一旦您上傳 hello 模組 tooADL 存放區，將它宣告為使用部署資源 toomake U-SQL 指令碼與呼叫中提供`install.packages`tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="4e034-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4e034-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e034-146">Next Steps</span></span>
* [<span data-ttu-id="4e034-147">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="4e034-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="4e034-148">使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="4e034-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="4e034-149">針對 Azure 資料湖分析工作使用 U-SQL 視窗函式</span><span class="sxs-lookup"><span data-stu-id="4e034-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
