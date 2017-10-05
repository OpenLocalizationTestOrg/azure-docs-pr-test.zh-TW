---
title: "(已過時) 二元分類器 - Azure | Microsoft Docs"
description: "(已過時) 二元分類器"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
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
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="4fb4c-103">(已過時) 二元分類器</span><span class="sxs-lookup"><span data-stu-id="4fb4c-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="4fb4c-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4fb4c-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4fb4c-106">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4fb4c-107">假設您有一個資料集，並想要根據獨立變更來預測二元相依變數。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="4fb4c-108">「羅吉斯迴歸」是適用於此類預測的普遍統計技術。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="4fb4c-109">這裡的相依變數是二元或二分類變數，而 p 是感興趣特性的存在機率。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="4fb4c-110">一個簡單的案例是研究人員嘗試根據資訊 (高中的 GPA、家庭收入、居住地、性別)，來預測未來學生是否有可能接受大學的入學許可。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="4fb4c-111">預測的結果是未來學生接受入學許可的機率。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="4fb4c-112">這項 [Web 服務](https://datamarket.azure.com/dataset/aml_labs/log_regression) 會將資料套入羅吉斯迴歸模型，並為資料中的每個觀察輸出機率值 (y)。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="4fb4c-113">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="4fb4c-114">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="4fb4c-115">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4fb4c-116">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4fb4c-117">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="4fb4c-117">Consumption of web service</span></span>
<span data-ttu-id="4fb4c-118">此 web 服務會根據所有觀察的獨立變數來提供相依變數的預測值。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="4fb4c-119">Web 服務需要使用者以字串形式輸入資料，其中資料列會以逗號 (,) 分隔，而資料行會以分號 (;) 分隔。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="4fb4c-120">Web 服務一次可輸入一個資料列，而且第一個資料行必須是相依變數。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="4fb4c-121">範例資料集看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="4fb4c-121">An example dataset could look like this:</span></span>

![範例資料][1]

<span data-ttu-id="4fb4c-123">沒有相依變數的觀察應輸入 “NA” 做為 y。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="4fb4c-124">上述資料集的資料輸入字串如下：“1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="4fb4c-125">輸出會是根據獨立變數的每個資料列預估值。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="4fb4c-126">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4fb4c-127">以自動化方式取用服務的方法有很多種 ([這裡](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)提供一個範例應用程式)。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4fb4c-128">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="4fb4c-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="4fb4c-129">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="4fb4c-129">Creation of web service</span></span>
> <span data-ttu-id="4fb4c-130">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4fb4c-131">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="4fb4c-132">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="4fb4c-133">從 Azure Machine Learning 中，已建立一個新的空白實驗，並將兩個[執行 R 指令碼][execute-r-script]模組提取到工作區。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="4fb4c-134">這項 Web 服務使用基礎 R 指令碼來執行 Azure Machine Learning 實驗。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="4fb4c-135">這項實驗有兩個部分：結構描述定義，以及定型模型 + 計分。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="4fb4c-136">第一個模組會定義輸入資料集的預期結構，其中第一個變數是相依變數，而其餘變數是獨立變數。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="4fb4c-137">第二個模組會將輸入資料套入一般羅吉斯迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![實驗流程][2]

#### <a name="module-1"></a><span data-ttu-id="4fb4c-139">模組 1：</span><span class="sxs-lookup"><span data-stu-id="4fb4c-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="4fb4c-140">模組 2：</span><span class="sxs-lookup"><span data-stu-id="4fb4c-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="4fb4c-141">限制</span><span class="sxs-lookup"><span data-stu-id="4fb4c-141">Limitations</span></span>
<span data-ttu-id="4fb4c-142">這是一個非常簡單的二元分類 Web 服務範例。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="4fb4c-143">從上面的範例程式碼可以看出，未實作錯誤攔截，且由於建立這項 Web 服務時，服務只輸入數值，因此服務會假設所有項目都是二元/連續變數 (不允許類別功能)。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="4fb4c-144">此外，由於 Web 服務呼叫的要求/回應本質，以及每次呼叫 Web 服務時就會調整模型的事實，該項服務目前只能處理有限的資料大小。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="4fb4c-145">常見問題集</span><span class="sxs-lookup"><span data-stu-id="4fb4c-145">FAQ</span></span>
<span data-ttu-id="4fb4c-146">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="4fb4c-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

