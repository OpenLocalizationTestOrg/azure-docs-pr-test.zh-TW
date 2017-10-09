---
title: "aaa(deprecated) 求生分析與 Azure Machine Learning |Microsoft 文件"
description: "(已過時) 存活分析 - 事件發生機率"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="fc2d8-103">(已過時) 存活分析</span><span class="sxs-lookup"><span data-stu-id="fc2d8-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="fc2d8-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="fc2d8-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="fc2d8-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="fc2d8-107">在許多案例中，在評估的 hello 主要結果會是 hello 時間 tooan 感興趣的事件。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-107">Under many scenarios, hello main outcome under assessment is hello time tooan event of interest.</span></span> <span data-ttu-id="fc2d8-108">換句話說，hello 問題 」 時將會發生此事件？ 」</span><span class="sxs-lookup"><span data-stu-id="fc2d8-108">In other words, hello question “when this event will occur?”</span></span> <span data-ttu-id="fc2d8-109">。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-109">is asked.</span></span> <span data-ttu-id="fc2d8-110">做為範例，請考慮 hello 資料其中描述 hello 經過時間 （日、 年、 里程數等） 的情況下才 hello 疾病 relapse、 收到博士程度 （剎車組板失敗） 感興趣的事件，就會發生。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-110">As examples, consider situations where hello data describes hello elapsed time (days, years, mileage, etc.) until hello event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="fc2d8-111">Hello 資料中的每個執行個體代表特定的物件 （一位病患、 學生、 汽車等）。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-111">Each instance in hello data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="fc2d8-112">這[web 服務](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis)「 什麼是 hello 機率 hello 感興趣的事件，會發生時間 n 個物件 x？"hello 問題的答案</span><span class="sxs-lookup"><span data-stu-id="fc2d8-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers hello question “what is hello probability that hello event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="fc2d8-113">藉由提供求生分析模型，此 web 服務可讓使用者 toosupply 資料 tootrain hello 模型並進行測試。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-113">By providing a survival analysis model, this web service enables users toosupply data tootrain hello model and test it.</span></span> <span data-ttu-id="fc2d8-114">hello 主要佈景主題的 hello 實驗長度 toomodel hello hello 所經過時間的感興趣的 hello 事件發生之前。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-114">hello main theme of hello experiment is toomodel hello length of hello elapsed time until hello event of interest occurs.</span></span> 

> <span data-ttu-id="fc2d8-115">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="fc2d8-116">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="fc2d8-117">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="fc2d8-118">接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="fc2d8-119">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="fc2d8-119">Consumption of web service</span></span>
<span data-ttu-id="fc2d8-120">下表中的 hello 顯示 hello hello web 服務的輸入的資料結構描述。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-120">hello input data schema of hello web service is shown in hello following table.</span></span> <span data-ttu-id="fc2d8-121">做為 hello 輸入所需的六項資訊： 定型資料、 測試資料、 感興趣時間、 hello 的 「 時間 」 維度的索引、 hello 索引的 「 事件 」 維度和 hello 變數類型 (連續或係數)。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-121">Six pieces of information are needed as hello input: training data, testing data, time of interest, hello index of "time" dimension, hello index of "event" dimension, and hello variable types (continuous or factor).</span></span> <span data-ttu-id="fc2d8-122">hello 定型資料是使用其中 hello 資料列會以逗號分隔、 hello 資料行以分號分隔的字串表示。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-122">hello training data is represented with a string, where hello rows are separated by comma, and hello columns are separated by semicolon.</span></span> <span data-ttu-id="fc2d8-123">hello hello 資料的功能數目是有彈性。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-123">hello number of features of hello data is flexible.</span></span> <span data-ttu-id="fc2d8-124">Hello 輸入字串中的所有 hello 項目必須都是數字。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-124">All hello elements in hello input string must be numeric.</span></span> <span data-ttu-id="fc2d8-125">在 hello 定型資料，hello 「 時間 」 維度表示起點 hello hello 研究 （某個病患收到藥物處理程式、 學生起始博士研究、 啟動 toobe 一輛車後經過的時間單位 （日、 年、 里程數等） 的 hello 數驅動等）。直到 hello 發生的事件感興趣 （hello 病患傳回 toodrug 使用量、 hello 學生取得 hello 博士程度、 hello 汽車有剎車組板失敗等）。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-125">In hello training data, hello “time” dimension indicates hello number of time units (days, years, mileage, etc.) elapsed since hello starting point of hello study (a patient receiving drug treatment programs, a student starting PhD study, a car starting toobe driven, etc.) until hello event of interest (hello patient returning toodrug usage, hello student obtaining hello PhD degree, hello car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="fc2d8-126">hello 「 事件 」 維度表示 hello 感興趣的事件是否發生在 hello hello 研究的結尾。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-126">hello “event” dimension indicates whether hello event of interest occurs at hello end of hello study.</span></span> <span data-ttu-id="fc2d8-127">值為 「 事件 = 1"表示 hello 感興趣的事件發生於 hello 階段由 hello 「 時間 」 維度;「 事件 = 0"表示 hello 感興趣的事件尚未發生 hello hello 「 時間 」 維度所指定的時間。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-127">A value of “event=1” means that hello event of interest occurs at hello time indicated by hello “time” dimension; “event=0” means that hello event of interest has not occurred by hello time indicated by hello “time” dimension.</span></span>

* <span data-ttu-id="fc2d8-128">trainingdata - 字元字串。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-128">trainingdata - A character string.</span></span> <span data-ttu-id="fc2d8-129">資料列會以逗號分隔，而資料行會以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="fc2d8-130">每個資料列包含「時間」維度、「事件」維度和預測變數。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="fc2d8-131">testingdata - 包含特定物件之預測變數的一列資料。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="fc2d8-132">time_of_interest-感興趣 n hello 已耗用時間。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-132">time_of_interest - hello elapsed time of interest n.</span></span>
* <span data-ttu-id="fc2d8-133">index_time-hello hello （從 1 開始） 的 「 時間 」 維度的資料行索引。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-133">index_time - hello column index of hello “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="fc2d8-134">index_event-hello hello （從 1 開始） 的 「 事件 」 維度的資料行索引。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-134">index_event - hello column index of hello “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="fc2d8-135">variable_types - 以分號做為分隔符號的字元字串。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="fc2d8-136">0 表示連續變數，而 1 表示因子變數。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="fc2d8-137">hello 輸出是 hello 機率在特定時間發生的事件。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-137">hello output is hello probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="fc2d8-138">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-138">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="fc2d8-139">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx))。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-139">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="fc2d8-140">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="fc2d8-140">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




<span data-ttu-id="fc2d8-141">這項測試的 hello 解譯如下。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-141">hello interpretation of this test is as follows.</span></span> <span data-ttu-id="fc2d8-142">假設 hello 資料 hello 目標 toomodel hello 經過時間，直到 hello 傳回 toodrug 使用量，以供 hello 收到病患已收到 hello 兩個處理程式。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-142">Assuming hello goal of hello data is toomodel hello elapsed time until hello return toodrug usage for hello patients who received one of hello two treatment programs.</span></span> <span data-ttu-id="fc2d8-143">hello hello web 服務讀取的輸出： 的病患正在 35 歲，有先前藥品處理 2 次，接受 hello 住家長時間來處理程式，而且與 heroin 和 cocaine 使用量 hello 機率傳回 toohello 藥物使用量依 95.64%500 的日期。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-143">hello output of hello web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking hello long residential treatment program, and with both heroin and cocaine usage, hello probability of returning toohello drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="fc2d8-144">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="fc2d8-144">Creation of web service</span></span>
> <span data-ttu-id="fc2d8-145">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="fc2d8-146">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="fc2d8-147">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-147">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="fc2d8-148">在 Azure Machine Learning 中，新的空白實驗建立的來源和兩個[執行 R 指令碼][ execute-r-script]模組提取到 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="fc2d8-149">hello 資料結構描述以建立簡單[執行 R 指令碼][execute-r-script]，而後者可定義 hello hello web 服務的輸入的資料結構描述。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-149">hello data schema was created with a simple [Execute R Script][execute-r-script], which defines hello input data schema for hello web service.</span></span> <span data-ttu-id="fc2d8-150">此模組然後是第二個連結 toohello[執行 R 指令碼][ execute-r-script]模組呈現，而沒有主要工作。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-150">This module is then linked toohello second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="fc2d8-151">此模組會進行資料前處理、模型建立和預測。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="fc2d8-152">在 hello 資料前置處理步驟中，是轉換 hello 輸入長字串所表示的資料，並將其轉換至資料框架中。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-152">In hello data preprocessing step, hello input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="fc2d8-153">在 hello 模型建置步驟中，外部的 R 封裝 「 survival_2.37 7.zip"是第一次安裝進行求生分析。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-153">In hello model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="fc2d8-154">然後數列資料處理工作後執行 hello"coxph"函式。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-154">Then hello “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="fc2d8-155">hello 求生分析 hello"coxph"函式的詳細資料可讀取 hello R 文件。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-155">hello details of hello “coxph” function for survival analysis can be read from hello R documentation.</span></span> <span data-ttu-id="fc2d8-156">在 hello 預測步驟中，測試執行個體提供成 hello 定型的模型與 hello"surfit"函式，並 hello 存續曲線，這個測試的執行個體產生做為 「 曲線 」 變數。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-156">In hello prediction step, a testing instance is supplied into hello trained model with hello “surfit” function, and hello survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="fc2d8-157">最後，會取得 hello hello 時間感興趣的機率。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-157">Finally, hello probability of hello time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="fc2d8-158">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="fc2d8-158">Experiment flow:</span></span>
![實驗流程][1]

#### <a name="module-1"></a><span data-ttu-id="fc2d8-160">模組 1：</span><span class="sxs-lookup"><span data-stu-id="fc2d8-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="fc2d8-161">模組 2：</span><span class="sxs-lookup"><span data-stu-id="fc2d8-161">Module 2:</span></span>
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="fc2d8-162">限制</span><span class="sxs-lookup"><span data-stu-id="fc2d8-162">Limitations</span></span>
<span data-ttu-id="fc2d8-163">這項 Web 服務只能以數值做為特徵變數 (資料行)。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="fc2d8-164">hello 「 事件 」 資料行可能需要只值 0 或 1。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-164">hello “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="fc2d8-165">hello 「 時間 」 資料行必須 toobe 的正整數。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-165">hello “time” column needs toobe a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="fc2d8-166">常見問題集</span><span class="sxs-lookup"><span data-stu-id="fc2d8-166">FAQ</span></span>
<span data-ttu-id="fc2d8-167">常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="fc2d8-167">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

