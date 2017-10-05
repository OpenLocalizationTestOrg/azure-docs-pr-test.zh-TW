---
title: "(已過時) 使用 Azure Machine Learning 進行存活分析 | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="d61ab-103">(已過時) 存活分析</span><span class="sxs-lookup"><span data-stu-id="d61ab-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="d61ab-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="d61ab-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="d61ab-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="d61ab-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="d61ab-106">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="d61ab-107">在許多情況下，主要評估結果會是感興趣事件的時間。</span><span class="sxs-lookup"><span data-stu-id="d61ab-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="d61ab-108">換句話說，詢問的問題會是「何時將發生這個事件」</span><span class="sxs-lookup"><span data-stu-id="d61ab-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="d61ab-109">。</span><span class="sxs-lookup"><span data-stu-id="d61ab-109">is asked.</span></span> <span data-ttu-id="d61ab-110">例如，請考慮資料描述感興趣的事件 (疾病復發、取得博士學位、煞車來令片故障) 發生前所經過之時間 (天、年、里程數等) 的案例。</span><span class="sxs-lookup"><span data-stu-id="d61ab-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="d61ab-111">資料中的每個執行個體代表特定物件 (病患、學生、汽車等)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="d61ab-112">這項 [Web 服務](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis)回答了「物件 x 在時間 n 前發生感興趣事件的機率為何？」這個問題。</span><span class="sxs-lookup"><span data-stu-id="d61ab-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="d61ab-113">藉由提供存活分析模型，這項 Web 服務可讓使用者提供資料來定型模型並加以測試。</span><span class="sxs-lookup"><span data-stu-id="d61ab-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="d61ab-114">此實驗的主旨是要在感興趣的事件發生之前建立經過時間長度的模型。</span><span class="sxs-lookup"><span data-stu-id="d61ab-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="d61ab-115">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="d61ab-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="d61ab-116">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="d61ab-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="d61ab-117">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="d61ab-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="d61ab-118">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="d61ab-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="d61ab-119">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="d61ab-119">Consumption of web service</span></span>
<span data-ttu-id="d61ab-120">下表中顯示 Web 服務的輸入資料結構描述。</span><span class="sxs-lookup"><span data-stu-id="d61ab-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="d61ab-121">必須輸入六項資訊：定型資料、測試資料、感興趣的時間、「時間」維度的索引、「事件」維度的索引和變數類型 (連續或因素)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="d61ab-122">訓練資料是以字串表示，其中的資料列是以逗號分隔，而資料行是以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="d61ab-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="d61ab-123">資料的特徵數目是彈性的。</span><span class="sxs-lookup"><span data-stu-id="d61ab-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="d61ab-124">輸入字串中的所有元素都必須為數值。</span><span class="sxs-lookup"><span data-stu-id="d61ab-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="d61ab-125">在定型資料中，「時間」維度表示自研究的起點 (病患收到藥物治療方案、學生開始博士研究、汽車開始發動等)，到發生感興趣的事件 (病患再度吸食毒品、學生取得博士學位、汽車的煞車來令片故障等) 所經過的時間單位數 (日、年、里程數等)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="d61ab-126">「事件」維度指出感興趣的事件是否發生在研究結束時。</span><span class="sxs-lookup"><span data-stu-id="d61ab-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="d61ab-127">「事件 = 1」的值表示感興趣的事件發生於「時間」維度所指出的時間；而「事件 = 0」表示到「時間」維度所指定的時間為止都未發生感興趣的事件。</span><span class="sxs-lookup"><span data-stu-id="d61ab-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="d61ab-128">trainingdata - 字元字串。</span><span class="sxs-lookup"><span data-stu-id="d61ab-128">trainingdata - A character string.</span></span> <span data-ttu-id="d61ab-129">資料列會以逗號分隔，而資料行會以分號分隔。</span><span class="sxs-lookup"><span data-stu-id="d61ab-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="d61ab-130">每個資料列包含「時間」維度、「事件」維度和預測變數。</span><span class="sxs-lookup"><span data-stu-id="d61ab-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="d61ab-131">testingdata - 包含特定物件之預測變數的一列資料。</span><span class="sxs-lookup"><span data-stu-id="d61ab-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="d61ab-132">time_of_interest - 興趣 n 的經過時間。</span><span class="sxs-lookup"><span data-stu-id="d61ab-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="d61ab-133">index_time -「時間」維度的資料行索引 (從 1 開始)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="d61ab-134">index_event -「事件」維度的資料行索引 (從 1 開始)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="d61ab-135">variable_types - 以分號做為分隔符號的字元字串。</span><span class="sxs-lookup"><span data-stu-id="d61ab-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="d61ab-136">0 表示連續變數，而 1 表示因子變數。</span><span class="sxs-lookup"><span data-stu-id="d61ab-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="d61ab-137">輸出是在特定時間前發生事件的機率。</span><span class="sxs-lookup"><span data-stu-id="d61ab-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="d61ab-138">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="d61ab-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="d61ab-139">以自動化方式取用服務的方法有很多種 ([這裡](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)提供一個範例應用程式)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="d61ab-140">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="d61ab-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="d61ab-141">這項測試的解譯如下。</span><span class="sxs-lookup"><span data-stu-id="d61ab-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="d61ab-142">假設資料的目標是要建立在收到兩種治療方案之一的病患再次吸食毒品的經過時間模型。</span><span class="sxs-lookup"><span data-stu-id="d61ab-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="d61ab-143">Web 服務的輸出如下所示：病患目前 35 歲，先前藥物治療 2 次，採用長期居家治療方案，吸食海洛因和古柯鹼，在第 500 天前再度吸食毒品的機率是 95.64%。</span><span class="sxs-lookup"><span data-stu-id="d61ab-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="d61ab-144">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="d61ab-144">Creation of web service</span></span>
> <span data-ttu-id="d61ab-145">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="d61ab-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="d61ab-146">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="d61ab-147">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="d61ab-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="d61ab-148">Azure Machine Learning 中已建立新的空白實驗，並將兩個[執行 R 指令碼][execute-r-script]模組提取到工作區。</span><span class="sxs-lookup"><span data-stu-id="d61ab-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="d61ab-149">已使用簡單的[執行 R 指令碼][execute-r-script]建立資料結構描述，其中定義 Web 服務的輸入資料結構描述。</span><span class="sxs-lookup"><span data-stu-id="d61ab-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="d61ab-150">這個模組會接著連結至執行主要工作的第二個[執行 R 指令碼][execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="d61ab-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="d61ab-151">此模組會進行資料前處理、模型建立和預測。</span><span class="sxs-lookup"><span data-stu-id="d61ab-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="d61ab-152">在資料前處理步驟中，長字串所表示的輸入資料會轉換成資料框架。</span><span class="sxs-lookup"><span data-stu-id="d61ab-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="d61ab-153">在模型建立步驟中，首次安裝外部 R 套件 "survival_2.37-7.zip" 以進行存活分析。</span><span class="sxs-lookup"><span data-stu-id="d61ab-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="d61ab-154">然後會在序列資料處理工作之後執行 "coxph" 函數。</span><span class="sxs-lookup"><span data-stu-id="d61ab-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="d61ab-155">在 R 文件中可以讀取存活分析的 "coxph" 函數詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d61ab-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="d61ab-156">在預測步驟中，會利用 "surfit" 函數在定型模型中提供測試執行個體，而且此測試執行個體的存活曲線會產生成為 “curve” 變數。</span><span class="sxs-lookup"><span data-stu-id="d61ab-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="d61ab-157">最後會取得感興趣時間的機率。</span><span class="sxs-lookup"><span data-stu-id="d61ab-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="d61ab-158">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="d61ab-158">Experiment flow:</span></span>
![實驗流程][1]

#### <a name="module-1"></a><span data-ttu-id="d61ab-160">模組 1：</span><span class="sxs-lookup"><span data-stu-id="d61ab-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="d61ab-161">模組 2：</span><span class="sxs-lookup"><span data-stu-id="d61ab-161">Module 2:</span></span>
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

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
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

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
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

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="d61ab-162">限制</span><span class="sxs-lookup"><span data-stu-id="d61ab-162">Limitations</span></span>
<span data-ttu-id="d61ab-163">這項 Web 服務只能以數值做為特徵變數 (資料行)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="d61ab-164">[事件] 資料行只能接受 0 或 1 的值。</span><span class="sxs-lookup"><span data-stu-id="d61ab-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="d61ab-165">[時間] 資料行必須是正整數。</span><span class="sxs-lookup"><span data-stu-id="d61ab-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="d61ab-166">常見問題集</span><span class="sxs-lookup"><span data-stu-id="d61ab-166">FAQ</span></span>
<span data-ttu-id="d61ab-167">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="d61ab-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

