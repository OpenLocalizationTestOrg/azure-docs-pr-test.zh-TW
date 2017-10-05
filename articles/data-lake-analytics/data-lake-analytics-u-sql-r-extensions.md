---
title: "在 Azure Data Lake Analytics 中使用 R 擴充 U-SQL 指令碼 | Microsoft Docs"
description: "了解如何在 U-SQL 指令碼中執行 R 程式碼"
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
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="9775c-103">教學課程︰開始使用 R 擴充 U-SQL</span><span class="sxs-lookup"><span data-stu-id="9775c-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="9775c-104">以下範例說明部署 R 程式碼的基本步驟：</span><span class="sxs-lookup"><span data-stu-id="9775c-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="9775c-105">使用 `REFERENCE ASSEMBLY` 陳述式啟用 U-SQL 指令碼的 R 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9775c-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="9775c-106">使用 ` REDUCE` 作業分割索引鍵上的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="9775c-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="9775c-107">U-SQL 的 R 延伸模組有內建的歸納器 (`Extension.R.Reducer`)，會在指派給歸納器的每一個頂點上執行 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="9775c-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="9775c-108">專用具名資料框架的使用情況會相對應地呼叫 `inputFromUSQL` 和 `outputToUSQL ` 以在 USQL 和 R 之間傳遞資料。輸入和輸出資料框架識別碼名稱是固定的 (也就是使用者無法變更輸入和輸出資料框架識別碼的這些預先定義名稱)。</span><span class="sxs-lookup"><span data-stu-id="9775c-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="9775c-109">將 R 程式碼內嵌在 U-SQL 指令碼中</span><span class="sxs-lookup"><span data-stu-id="9775c-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="9775c-110">您可以使用 `Extension.R.Reducer` 的 command 參數，將 R 程式碼內嵌在 U-SQL 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="9775c-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="9775c-111">例如，您可以將 R 指令碼宣告為字串變數，再當作參數傳給歸納器。</span><span class="sxs-lookup"><span data-stu-id="9775c-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="9775c-112">將 R 程式碼保存在個別檔案中，然後在 U-SQL 指令碼中參考它</span><span class="sxs-lookup"><span data-stu-id="9775c-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="9775c-113">下列範例說明更複雜的使用方式。</span><span class="sxs-lookup"><span data-stu-id="9775c-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="9775c-114">在此案例中，R 程式碼會部署成「資源」(也就是 U-SQL 指令碼)。</span><span class="sxs-lookup"><span data-stu-id="9775c-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="9775c-115">將此 R 程式碼儲存為個別的檔案。</span><span class="sxs-lookup"><span data-stu-id="9775c-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="9775c-116">透過 DEPLOY RESOURCE 陳述式，使用 U-SQL 指令碼來部署該 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9775c-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="9775c-117">R 如何與 U-SQL 整合</span><span class="sxs-lookup"><span data-stu-id="9775c-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="9775c-118">資料類型</span><span class="sxs-lookup"><span data-stu-id="9775c-118">Datatypes</span></span>
* <span data-ttu-id="9775c-119">來自 U-SQL 的字串和數值資料行會在 R 資料框架和 U-SQL 之間以現狀進行轉換 [支援的類型：`double``string`、`bool`、`integer`、`byte`]。</span><span class="sxs-lookup"><span data-stu-id="9775c-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="9775c-120">U-SQL 不支援 `Factor` 資料類型。</span><span class="sxs-lookup"><span data-stu-id="9775c-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="9775c-121">`byte[]` 必須序列化為 base64 編碼的 `string`。</span><span class="sxs-lookup"><span data-stu-id="9775c-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="9775c-122">當 U-SQL 建立 R 輸入資料框架，或是設定歸納器參數 `stringsAsFactors: true` 之後，U-SQL 字串便可以轉換為 R 程式碼的因素。</span><span class="sxs-lookup"><span data-stu-id="9775c-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="9775c-123">結構描述</span><span class="sxs-lookup"><span data-stu-id="9775c-123">Schemas</span></span>
* <span data-ttu-id="9775c-124">U-SQL 資料集不能有重複的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="9775c-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="9775c-125">U-SQL 資料集的資料行名稱必須為字串。</span><span class="sxs-lookup"><span data-stu-id="9775c-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="9775c-126">資料行名稱在 U-SQL 和 R 指令碼中皆必須為相同。</span><span class="sxs-lookup"><span data-stu-id="9775c-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="9775c-127">唯讀資料行不能是輸出資料框架的一部分。</span><span class="sxs-lookup"><span data-stu-id="9775c-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="9775c-128">因為如果唯讀資料行是 UDO 輸出結構描述的一部分，便會自動插入回 U-SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="9775c-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="9775c-129">功能限制：</span><span class="sxs-lookup"><span data-stu-id="9775c-129">Functional limitations</span></span>
* <span data-ttu-id="9775c-130">R 引擎無法在相同的程序中具現化兩次。</span><span class="sxs-lookup"><span data-stu-id="9775c-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="9775c-131">目前，在以歸納器 UDO 所產生的分割模型進行預測時，U-SQL 不支援使用合併器 UDO。</span><span class="sxs-lookup"><span data-stu-id="9775c-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="9775c-132">使用者可以將分割的模型宣告為資源，然後用於 R 指令碼中 (請參閱範例程式碼 `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="9775c-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="9775c-133">R 版本</span><span class="sxs-lookup"><span data-stu-id="9775c-133">R Versions</span></span>
<span data-ttu-id="9775c-134">僅支援 R 3.2.2。</span><span class="sxs-lookup"><span data-stu-id="9775c-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="9775c-135">標準的 R 模組</span><span class="sxs-lookup"><span data-stu-id="9775c-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="9775c-136">輸入和輸出的大小限制</span><span class="sxs-lookup"><span data-stu-id="9775c-136">Input and Output size limitations</span></span>
<span data-ttu-id="9775c-137">指派給每個頂點的記憶體數量皆有上限。</span><span class="sxs-lookup"><span data-stu-id="9775c-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="9775c-138">因為輸入和輸出資料框架必須存在於 R 程式碼的記憶體中，輸入和輸出的大小總和不能超過 500 GB。</span><span class="sxs-lookup"><span data-stu-id="9775c-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="9775c-139">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="9775c-139">Sample Code</span></span>
<span data-ttu-id="9775c-140">安裝 U-SQL 進階分析擴充功能之後，您的 Data Lake Store 帳戶中會有更多範例程式碼可用。</span><span class="sxs-lookup"><span data-stu-id="9775c-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="9775c-141">其他範例程式碼的路徑如下：`<your_account_address>/usqlext/samples/R`。</span><span class="sxs-lookup"><span data-stu-id="9775c-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="9775c-142">使用 U-SQL 部署自訂 R 模組</span><span class="sxs-lookup"><span data-stu-id="9775c-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="9775c-143">首先，建立自訂 R 模組並壓縮它，然後將已壓縮的 R 自訂模組檔案上傳至您的 ADL 存放區。</span><span class="sxs-lookup"><span data-stu-id="9775c-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="9775c-144">在範例中，我們會將 magittr_1.5.zip 上傳至我們所使用之 ADLA 帳戶的預設 ADLA 帳戶根目錄。</span><span class="sxs-lookup"><span data-stu-id="9775c-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="9775c-145">將模組上傳至 ADL 存放區之後，將它宣告為使用 DEPLOY RESOURCE 以供您的 U-SQL 指令碼使用，然後呼叫 `install.packages` 來安裝它。</span><span class="sxs-lookup"><span data-stu-id="9775c-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
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

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="9775c-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9775c-146">Next Steps</span></span>
* [<span data-ttu-id="9775c-147">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="9775c-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="9775c-148">使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="9775c-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="9775c-149">針對 Azure 資料湖分析工作使用 U-SQL 視窗函式</span><span class="sxs-lookup"><span data-stu-id="9775c-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
