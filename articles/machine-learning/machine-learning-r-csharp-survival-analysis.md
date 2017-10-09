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
# <a name="deprecated-survival-analysis"></a>(已過時) 存活分析

> [!NOTE]
> 淘汰 hello Microsoft DataMarket 和這個 API 已被取代。 
> 
> 您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。 如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。

在許多案例中，在評估的 hello 主要結果會是 hello 時間 tooan 感興趣的事件。 換句話說，hello 問題 」 時將會發生此事件？ 」 。 做為範例，請考慮 hello 資料其中描述 hello 經過時間 （日、 年、 里程數等） 的情況下才 hello 疾病 relapse、 收到博士程度 （剎車組板失敗） 感興趣的事件，就會發生。 Hello 資料中的每個執行個體代表特定的物件 （一位病患、 學生、 汽車等）。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

這[web 服務](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis)「 什麼是 hello 機率 hello 感興趣的事件，會發生時間 n 個物件 x？"hello 問題的答案 藉由提供求生分析模型，此 web 服務可讓使用者 toosupply 資料 tootrain hello 模型並進行測試。 hello 主要佈景主題的 hello 實驗長度 toomodel hello hello 所經過時間的感興趣的 hello 事件發生之前。 

> 使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。 但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。 只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。 接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。  
> 
> 

## <a name="consumption-of-web-service"></a>使用 Web 服務
下表中的 hello 顯示 hello hello web 服務的輸入的資料結構描述。 做為 hello 輸入所需的六項資訊： 定型資料、 測試資料、 感興趣時間、 hello 的 「 時間 」 維度的索引、 hello 索引的 「 事件 」 維度和 hello 變數類型 (連續或係數)。 hello 定型資料是使用其中 hello 資料列會以逗號分隔、 hello 資料行以分號分隔的字串表示。 hello hello 資料的功能數目是有彈性。 Hello 輸入字串中的所有 hello 項目必須都是數字。 在 hello 定型資料，hello 「 時間 」 維度表示起點 hello hello 研究 （某個病患收到藥物處理程式、 學生起始博士研究、 啟動 toobe 一輛車後經過的時間單位 （日、 年、 里程數等） 的 hello 數驅動等）。直到 hello 發生的事件感興趣 （hello 病患傳回 toodrug 使用量、 hello 學生取得 hello 博士程度、 hello 汽車有剎車組板失敗等）。 hello 「 事件 」 維度表示 hello 感興趣的事件是否發生在 hello hello 研究的結尾。 值為 「 事件 = 1"表示 hello 感興趣的事件發生於 hello 階段由 hello 「 時間 」 維度;「 事件 = 0"表示 hello 感興趣的事件尚未發生 hello hello 「 時間 」 維度所指定的時間。

* trainingdata - 字元字串。 資料列會以逗號分隔，而資料行會以分號分隔。 每個資料列包含「時間」維度、「事件」維度和預測變數。
* testingdata - 包含特定物件之預測變數的一列資料。
* time_of_interest-感興趣 n hello 已耗用時間。
* index_time-hello hello （從 1 開始） 的 「 時間 」 維度的資料行索引。
* index_event-hello hello （從 1 開始） 的 「 事件 」 維度的資料行索引。
* variable_types - 以分號做為分隔符號的字元字串。 0 表示連續變數，而 1 表示因子變數。

hello 輸出是 hello 機率在特定時間發生的事件。 

> 這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。 
> 
> 

有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx))。 

### <a name="starting-c-code-for-web-service-consumption"></a>啟動 Web 服務使用的 C# 程式碼：
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




這項測試的 hello 解譯如下。 假設 hello 資料 hello 目標 toomodel hello 經過時間，直到 hello 傳回 toodrug 使用量，以供 hello 收到病患已收到 hello 兩個處理程式。 hello hello web 服務讀取的輸出： 的病患正在 35 歲，有先前藥品處理 2 次，接受 hello 住家長時間來處理程式，而且與 heroin 和 cocaine 使用量 hello 機率傳回 toohello 藥物使用量依 95.64%500 的日期。

## <a name="creation-of-web-service"></a>建立 Web 服務
> 這項 Web 服務是使用 Azure Machine Learning 所建立。 如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。 以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。
> 
> 

在 Azure Machine Learning 中，新的空白實驗建立的來源和兩個[執行 R 指令碼][ execute-r-script]模組提取到 hello 工作區。 hello 資料結構描述以建立簡單[執行 R 指令碼][execute-r-script]，而後者可定義 hello hello web 服務的輸入的資料結構描述。 此模組然後是第二個連結 toohello[執行 R 指令碼][ execute-r-script]模組呈現，而沒有主要工作。 此模組會進行資料前處理、模型建立和預測。 在 hello 資料前置處理步驟中，是轉換 hello 輸入長字串所表示的資料，並將其轉換至資料框架中。 在 hello 模型建置步驟中，外部的 R 封裝 「 survival_2.37 7.zip"是第一次安裝進行求生分析。 然後數列資料處理工作後執行 hello"coxph"函式。 hello 求生分析 hello"coxph"函式的詳細資料可讀取 hello R 文件。 在 hello 預測步驟中，測試執行個體提供成 hello 定型的模型與 hello"surfit"函式，並 hello 存續曲線，這個測試的執行個體產生做為 「 曲線 」 變數。 最後，會取得 hello hello 時間感興趣的機率。 

### <a name="experiment-flow"></a>實驗流程：
![實驗流程][1]

#### <a name="module-1"></a>模組 1：
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

#### <a name="module-2"></a>模組 2：
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




## <a name="limitations"></a>限制
這項 Web 服務只能以數值做為特徵變數 (資料行)。 hello 「 事件 」 資料行可能需要只值 0 或 1。 hello 「 時間 」 資料行必須 toobe 的正整數。

## <a name="faq"></a>常見問題集
常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

