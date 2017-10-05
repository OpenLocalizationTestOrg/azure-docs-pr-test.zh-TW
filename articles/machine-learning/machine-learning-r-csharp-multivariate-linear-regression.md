---
title: "(已過時) 多變量線性迴歸 - Azure | Microsoft Docs"
description: "(已過時) 多變量線性迴歸"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 65a8005139e920cd19593e954fc1bf836354bdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="9882b-103">(已過時) 多變量線性迴歸</span><span class="sxs-lookup"><span data-stu-id="9882b-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="9882b-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="9882b-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="9882b-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="9882b-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9882b-106">如需此資源庫的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="9882b-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="9882b-107">假設您有一個資料集，並想要根據獨立變數，快速地預測每個項目 (i) 的相依變數 (y)。</span><span class="sxs-lookup"><span data-stu-id="9882b-107">Suppose you have a dataset and would like to quickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="9882b-108">線性迴歸是這類預測的常用統計技術。</span><span class="sxs-lookup"><span data-stu-id="9882b-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="9882b-109">這裡假設相依變數 y 是連續值。</span><span class="sxs-lookup"><span data-stu-id="9882b-109">Here the dependent variable y is assumed to be a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9882b-110">一個簡單的案例是研究人員嘗試根據身高 (x) 來預測某人 (y) 的體重。</span><span class="sxs-lookup"><span data-stu-id="9882b-110">A simple scenario could be where the researcher is trying to predict the weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="9882b-111">一個較為進階的案例是研究人員擁有個別的額外資訊 (例如體重、性別、種族)，並嘗試預測某人的體重。</span><span class="sxs-lookup"><span data-stu-id="9882b-111">A more advanced scenario could be where the researcher has additional information for the individual (such as weight, gender, race) and attempts to predict the weight of the individual.</span></span> <span data-ttu-id="9882b-112">這項 [Web 服務](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) 會將資料套入線性迴歸模型，並為資料中的每個觀察輸出預測值 (y)。</span><span class="sxs-lookup"><span data-stu-id="9882b-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits the linear regression model to the data and outputs the predicted value (y) for each of the observations in the data.</span></span>

> <span data-ttu-id="9882b-113">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9882b-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="9882b-114">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9882b-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="9882b-115">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9882b-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="9882b-116">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="9882b-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="9882b-117">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="9882b-117">Consumption of web service</span></span>
<span data-ttu-id="9882b-118">此 web 服務會根據所有觀察的獨立變數來提供相依變數的預測值。</span><span class="sxs-lookup"><span data-stu-id="9882b-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="9882b-119">Web 服務需要使用者以字串形式輸入資料，其中資料列會以逗號 (,) 分隔，而資料行會以分號 (;) 分隔。</span><span class="sxs-lookup"><span data-stu-id="9882b-119">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="9882b-120">Web 服務一次可輸入一個資料列，而且第一個資料行必須是相依變數。</span><span class="sxs-lookup"><span data-stu-id="9882b-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="9882b-121">範例資料集看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="9882b-121">An example dataset could look like this:</span></span>

![範例資料][1]

<span data-ttu-id="9882b-123">沒有相依變數的觀察應輸入 “NA” 做為 y。</span><span class="sxs-lookup"><span data-stu-id="9882b-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="9882b-124">上述資料集的資料輸入字串如下：“10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”。</span><span class="sxs-lookup"><span data-stu-id="9882b-124">The data input for the above dataset would be the following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="9882b-125">輸出會是根據獨立變數的每個資料列預估值。</span><span class="sxs-lookup"><span data-stu-id="9882b-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="9882b-126">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="9882b-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="9882b-127">以自動化方式取用服務的方法有很多種 ([這裡](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)提供一個範例應用程式)。</span><span class="sxs-lookup"><span data-stu-id="9882b-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="9882b-128">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="9882b-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="9882b-129">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="9882b-129">Creation of web service</span></span>
> <span data-ttu-id="9882b-130">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="9882b-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="9882b-131">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="9882b-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="9882b-132">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="9882b-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="9882b-133">Azure Machine Learning 中已建立新的空白實驗，並將兩個[執行 R 指令碼][execute-r-script]模組提取到工作區。</span><span class="sxs-lookup"><span data-stu-id="9882b-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="9882b-134">這項 Web 服務使用基礎 R 指令碼來執行 Azure Machine Learning 實驗。</span><span class="sxs-lookup"><span data-stu-id="9882b-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="9882b-135">這項實驗有兩個部分：結構描述定義，以及定型模型 + 計分。</span><span class="sxs-lookup"><span data-stu-id="9882b-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="9882b-136">第一個模組會定義輸入資料集的預期結構，其中第一個變數是相依變數，而其餘變數是獨立變數。</span><span class="sxs-lookup"><span data-stu-id="9882b-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="9882b-137">第二個模組會將輸入資料套入一般線性迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="9882b-137">The second module fits a generic linear regression model for the input data.</span></span>  

![實驗流程][3]

#### <a name="module-1"></a><span data-ttu-id="9882b-139">模組 1：</span><span class="sxs-lookup"><span data-stu-id="9882b-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="9882b-140">結構描述定義</span><span class="sxs-lookup"><span data-stu-id="9882b-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="9882b-141">模組 2：</span><span class="sxs-lookup"><span data-stu-id="9882b-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="9882b-142">LM 模型</span><span class="sxs-lookup"><span data-stu-id="9882b-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="9882b-143">限制</span><span class="sxs-lookup"><span data-stu-id="9882b-143">Limitations</span></span>
<span data-ttu-id="9882b-144">這是一個非常簡單的多元線性迴歸 Web 服務案例。</span><span class="sxs-lookup"><span data-stu-id="9882b-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="9882b-145">從上面的範例程式碼可以看出，未實作錯誤攔截，且由於建立這項 Web 服務時，服務只輸入數值，因此服務會假設所有項目都是連續變數 (不允許類別功能)。</span><span class="sxs-lookup"><span data-stu-id="9882b-145">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="9882b-146">此外，由於 Web 服務呼叫的要求/回應本質，以及每次呼叫 Web 服務時就會調整模型的事實，該項服務目前只能處理有限的資料大小。</span><span class="sxs-lookup"><span data-stu-id="9882b-146">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="9882b-147">常見問題集</span><span class="sxs-lookup"><span data-stu-id="9882b-147">FAQ</span></span>
<span data-ttu-id="9882b-148">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="9882b-148">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

