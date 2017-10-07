---
title: "(已過時) 預測：自動迴歸整合式移動平均 (ARIMA) - Azure | Microsoft Docs"
description: "(已過時) 預測 - 自動迴歸整合式移動平均 (ARIMA)"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: 1e0d525f-8a9e-4b42-87e0-c9423f059f8c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 4f3af41fd8873fdf75c6426fd395351cb41db190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a><span data-ttu-id="d184a-103">(已過時) 預測 - 自動迴歸整合式移動平均 (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="d184a-103">(deprecated) Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>

> [!NOTE]
> <span data-ttu-id="d184a-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="d184a-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="d184a-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="d184a-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="d184a-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="d184a-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>


<span data-ttu-id="d184a-107">這[服務](https://datamarket.azure.com/dataset/aml_labs/arima)實作根據 hello hello 使用者所提供的歷程記錄資料的自動迴歸整合式移動平均 (ARIMA) tooproduce 預測。</span><span class="sxs-lookup"><span data-stu-id="d184a-107">This [service](https://datamarket.azure.com/dataset/aml_labs/arima) implements Autoregressive Integrated Moving Average (ARIMA) tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="d184a-108">將 hello 加大本年度的特定產品的需求？</span><span class="sxs-lookup"><span data-stu-id="d184a-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="d184a-109">可以我預測 hello 產品銷售聖誕季節，讓我可以有效地計劃我清查？</span><span class="sxs-lookup"><span data-stu-id="d184a-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="d184a-110">預測模型是 apt tooaddress 這類問題。</span><span class="sxs-lookup"><span data-stu-id="d184a-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="d184a-111">指定 hello 過去的資料，這些模型會檢查隱藏的趨勢和季節性 toopredict 未來的趨勢。</span><span class="sxs-lookup"><span data-stu-id="d184a-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="d184a-112">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="d184a-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="d184a-113">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="d184a-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="d184a-114">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="d184a-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="d184a-115">接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="d184a-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="d184a-116">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="d184a-116">Consumption of web service</span></span>
<span data-ttu-id="d184a-117">此服務會接受 4 個引數，並計算 hello ARIMA 預測。</span><span class="sxs-lookup"><span data-stu-id="d184a-117">This service accepts 4 arguments and calculates hello ARIMA forecasts.</span></span>
<span data-ttu-id="d184a-118">hello 輸入引數為：</span><span class="sxs-lookup"><span data-stu-id="d184a-118">hello input arguments are:</span></span>

* <span data-ttu-id="d184a-119">頻率-表示 hello 頻率的 hello 未經處理資料 （每日/週/月/每季/安排每年）。</span><span class="sxs-lookup"><span data-stu-id="d184a-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="d184a-120">水平 - 未來預測時間範圍。</span><span class="sxs-lookup"><span data-stu-id="d184a-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="d184a-121">日期-加入 hello 新時間序列中資料的時間。</span><span class="sxs-lookup"><span data-stu-id="d184a-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="d184a-122">值-新增 hello 新時間序列的資料值。</span><span class="sxs-lookup"><span data-stu-id="d184a-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="d184a-123">hello 服務的 hello 輸出是 hello 計算預測的值。</span><span class="sxs-lookup"><span data-stu-id="d184a-123">hello output of hello service is hello calculated forecast values.</span></span> 

<span data-ttu-id="d184a-124">可能的範例輸入如下：</span><span class="sxs-lookup"><span data-stu-id="d184a-124">Sample input could be:</span></span> 

* <span data-ttu-id="d184a-125">頻率 - 12</span><span class="sxs-lookup"><span data-stu-id="d184a-125">Frequency - 12</span></span>
* <span data-ttu-id="d184a-126">水平 - 12</span><span class="sxs-lookup"><span data-stu-id="d184a-126">Horizon - 12</span></span>
* <span data-ttu-id="d184a-127">日期 - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="d184a-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="d184a-128">值 - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="d184a-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="d184a-129">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="d184a-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="d184a-130">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx))。</span><span class="sxs-lookup"><span data-stu-id="d184a-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="d184a-131">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="d184a-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
        public string frequency;
        public string horizon;
        public string date;
        public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
         byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
         return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }


    void Main()
    {
          var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri =  "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";

          var httpClient = new HttpClient();
           httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere","ChangeToAPIKey");
           httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
          var query = httpClient.PostAsync(acitionUri,new StringContent(json));
          var result = query.Result.Content;
          var scoreResult = result.ReadAsStringAsync().Result;
      }

## <a name="creation-of-web-service"></a><span data-ttu-id="d184a-132">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="d184a-132">Creation of web service</span></span>
> <span data-ttu-id="d184a-133">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="d184a-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="d184a-134">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="d184a-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="d184a-135">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="d184a-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="d184a-136">Azure Machine Learning 中已建立新的空白實驗，</span><span class="sxs-lookup"><span data-stu-id="d184a-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="d184a-137">並已使用預先定義的資料結構描述上傳範例輸入資料。</span><span class="sxs-lookup"><span data-stu-id="d184a-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="d184a-138">連結的 toohello 資料結構描述是[執行 R 指令碼][ execute-r-script]模組，使用 'auto.arima' 和 '趨勢預測' 函式，從 r 所產生 hello ARIMA 預測模型</span><span class="sxs-lookup"><span data-stu-id="d184a-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module, which generates hello ARIMA forecasting model by using ‘auto.arima’ and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="d184a-139">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="d184a-139">Experiment flow:</span></span>
![建立工作區][2]

#### <a name="module-1"></a><span data-ttu-id="d184a-141">模組 1：</span><span class="sxs-lookup"><span data-stu-id="d184a-141">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![建立工作區][3]    

#### <a name="module-2"></a><span data-ttu-id="d184a-143">模組 2：</span><span class="sxs-lookup"><span data-stu-id="d184a-143">Module 2:</span></span>
    # data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- auto.arima(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # produce forecasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="d184a-144">限制</span><span class="sxs-lookup"><span data-stu-id="d184a-144">Limitations</span></span>
<span data-ttu-id="d184a-145">這是一個非常簡單的 ARIMA 預測範例。</span><span class="sxs-lookup"><span data-stu-id="d184a-145">This is a very simple example for ARIMA forecasting.</span></span> <span data-ttu-id="d184a-146">從上述的 hello 範例程式碼可以看到，不實作攔截任何錯誤時，以及 hello 服務會假設所有 hello 變數都是連續/positive 值而 hello 頻率應大於 1 的整數。</span><span class="sxs-lookup"><span data-stu-id="d184a-146">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="d184a-147">hello hello 的日期和值的向量長度應該 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="d184a-147">hello length of hello date and value vectors should be hello same.</span></span> <span data-ttu-id="d184a-148">hello 日期變數應該遵守 toohello ' mm/dd/yyyy 格式 '。</span><span class="sxs-lookup"><span data-stu-id="d184a-148">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="d184a-149">常見問題集</span><span class="sxs-lookup"><span data-stu-id="d184a-149">FAQ</span></span>
<span data-ttu-id="d184a-150">常見問題集 hello web 服務或發行 toomarketplace 耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="d184a-150">For frequently asked questions on consumption of hello web service or publishing toomarketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

