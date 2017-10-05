---
title: "(已過時) 預測 - ETS + STL - Azure  | Microsoft Docs"
description: "(已過時) 預測 - ETS + STL"
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a575af931a41b7a55eb2102f3553640a16099146
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---ets--stl"></a><span data-ttu-id="74a1e-103">(已過時) 預測 - ETS + STL</span><span class="sxs-lookup"><span data-stu-id="74a1e-103">(deprecated) Forecasting - ETS + STL</span></span>

> [!NOTE]
> <span data-ttu-id="74a1e-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="74a1e-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="74a1e-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="74a1e-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="74a1e-106">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="74a1e-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="74a1e-107">這項 [Web 服務](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) 會實作季節性趨勢分解法 (STL) 和指數平滑法 (ETS) 模型，以根據使用者所提供的歷程記錄資料產生預測。</span><span class="sxs-lookup"><span data-stu-id="74a1e-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implements Seasonal Trend Decomposition (STL) and Exponential Smoothing (ETS) models to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="74a1e-108">今年的特定產品需求會增加嗎？</span><span class="sxs-lookup"><span data-stu-id="74a1e-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="74a1e-109">為方便有效地規劃庫存，我可以預測聖誕節的產品銷售嗎？</span><span class="sxs-lookup"><span data-stu-id="74a1e-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="74a1e-110">預測模型專門處理此類問題。</span><span class="sxs-lookup"><span data-stu-id="74a1e-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="74a1e-111">有了過去的資料，這些模型可以檢查隱藏的趨勢和季節性來預測未來的趨勢。</span><span class="sxs-lookup"><span data-stu-id="74a1e-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="74a1e-112">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="74a1e-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="74a1e-113">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="74a1e-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="74a1e-114">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="74a1e-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="74a1e-115">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="74a1e-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="74a1e-116">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="74a1e-116">Consumption of web service</span></span>
<span data-ttu-id="74a1e-117">這項服務可接受 4 個引數，並計算預測。</span><span class="sxs-lookup"><span data-stu-id="74a1e-117">This service accepts 4 arguments and calculates the forecasts.</span></span>
<span data-ttu-id="74a1e-118">輸入引數包括：</span><span class="sxs-lookup"><span data-stu-id="74a1e-118">The input arguments are:</span></span>

* <span data-ttu-id="74a1e-119">頻率 - 表示原始資料的頻率 (每日/每週/每月/每季/每年一次)。</span><span class="sxs-lookup"><span data-stu-id="74a1e-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="74a1e-120">水平 - 未來預測時間範圍。</span><span class="sxs-lookup"><span data-stu-id="74a1e-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="74a1e-121">日期 - 加入時間的新時間序列資料。</span><span class="sxs-lookup"><span data-stu-id="74a1e-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="74a1e-122">值 - 加入新的時間序列資料值。</span><span class="sxs-lookup"><span data-stu-id="74a1e-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="74a1e-123">服務的輸出會是已經計算的預測值。</span><span class="sxs-lookup"><span data-stu-id="74a1e-123">The output of the service is the calculated forecast values.</span></span>

<span data-ttu-id="74a1e-124">可能的範例輸入如下：</span><span class="sxs-lookup"><span data-stu-id="74a1e-124">Sample input could be:</span></span> 

* <span data-ttu-id="74a1e-125">頻率 - 12</span><span class="sxs-lookup"><span data-stu-id="74a1e-125">Frequency - 12</span></span>
* <span data-ttu-id="74a1e-126">水平 - 12</span><span class="sxs-lookup"><span data-stu-id="74a1e-126">Horizon - 12</span></span>
* <span data-ttu-id="74a1e-127">日期 - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="74a1e-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="74a1e-128">值 - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="74a1e-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="74a1e-129">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="74a1e-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="74a1e-130">以自動化方式取用服務的方法有很多種 ([這裡](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)提供一個範例應用程式)。</span><span class="sxs-lookup"><span data-stu-id="74a1e-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="74a1e-131">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="74a1e-131">Starting C# code for web service consumption:</span></span>
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
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="74a1e-132">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="74a1e-132">Creation of web service</span></span>
> <span data-ttu-id="74a1e-133">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="74a1e-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="74a1e-134">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="74a1e-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="74a1e-135">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="74a1e-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="74a1e-136">Azure Machine Learning 中已建立新的空白實驗，</span><span class="sxs-lookup"><span data-stu-id="74a1e-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="74a1e-137">並已使用預先定義的資料結構描述上傳範例輸入資料。</span><span class="sxs-lookup"><span data-stu-id="74a1e-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="74a1e-138">連結至資料結構描述的[執行 R 指令碼][execute-r-script]模組會使用 R 的 ‘stl’、‘ets’ 和 ‘forecast’ 函式，以產生 STL 和 ETS 預測模型。</span><span class="sxs-lookup"><span data-stu-id="74a1e-138">Linked to the data schema is an [Execute R Script][execute-r-script] module, which generates STL and ETS forecasting models by using ‘stl’, ‘ets’, and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="74a1e-139">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="74a1e-139">Experiment flow:</span></span>
![實驗流程][2]

#### <a name="module-1"></a><span data-ttu-id="74a1e-141">模組 1：</span><span class="sxs-lookup"><span data-stu-id="74a1e-141">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![範例資料][3]    

#### <a name="module-2"></a><span data-ttu-id="74a1e-143">模組 2：</span><span class="sxs-lookup"><span data-stu-id="74a1e-143">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a><span data-ttu-id="74a1e-144">限制</span><span class="sxs-lookup"><span data-stu-id="74a1e-144">Limitations</span></span>
<span data-ttu-id="74a1e-145">這是一個非常簡單的 ETS + STL 預測範例。</span><span class="sxs-lookup"><span data-stu-id="74a1e-145">This is a very simple example for ETS + STL forecasting.</span></span> <span data-ttu-id="74a1e-146">從上面的範例程式碼可以看出，未實作錯誤攔截，且這項服務假設所有變數都是連續/正值，而頻率應該是大於 1 的整數。</span><span class="sxs-lookup"><span data-stu-id="74a1e-146">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="74a1e-147">日期和值向量的長度應該相同，且時間序列的長度應該大於 2 倍頻率。</span><span class="sxs-lookup"><span data-stu-id="74a1e-147">The length of the date and value vectors should be the same, and the length of the time series should be greater than 2*frequency.</span></span> <span data-ttu-id="74a1e-148">日期變數應遵守 ‘mm/dd/yyyy’ 格式。</span><span class="sxs-lookup"><span data-stu-id="74a1e-148">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="74a1e-149">常見問題集</span><span class="sxs-lookup"><span data-stu-id="74a1e-149">FAQ</span></span>
<span data-ttu-id="74a1e-150">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="74a1e-150">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

