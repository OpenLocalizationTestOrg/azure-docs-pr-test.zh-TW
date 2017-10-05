---
title: "(已過時) 比例差異測試 - Azure | Microsoft Docs"
description: "(已過時) 比例差異測試"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a08f91ca76eef2562caeb9eb64cec5e549ed2f5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="e6cdf-103">(已過時) 比例差異測試</span><span class="sxs-lookup"><span data-stu-id="e6cdf-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="e6cdf-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="e6cdf-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="e6cdf-106">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="e6cdf-107">兩個比例有統計上的差異嗎？</span><span class="sxs-lookup"><span data-stu-id="e6cdf-107">Are two proportions statistically different?</span></span> <span data-ttu-id="e6cdf-108">假設使用者想要比較兩部電影，以判斷其中一部電影與另一部電影比較起來是否有明顯較高比例的「讚」。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-108">Suppose a user wants to compare two movies to determine if one movie has a significantly higher proportion of ‘likes’ when compared to the other.</span></span> <span data-ttu-id="e6cdf-109">在大型樣本中，在 0.50 和 0.51 比例之間可能會有統計上的顯著差異；</span><span class="sxs-lookup"><span data-stu-id="e6cdf-109">With a large sample, there could be a statistically significant difference between the proportions 0.50 and 0.51.</span></span> <span data-ttu-id="e6cdf-110">但在小型樣本中，可能沒有足夠的資料可以判斷這些比例是否真有差異。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-110">With a small sample, there may not be enough data to determine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e6cdf-111">這項 [Web 服務](https://datamarket.azure.com/dataset/aml_labs/prop_test) 會根據使用者針對 2 個比較群組輸入的的成功次數和總試驗次數，來進行兩個比例的差異假設測試。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of the difference in two proportions based on user input of the number of successes and the total number of trials for the 2 comparison groups.</span></span> <span data-ttu-id="e6cdf-112">一個可能的案例是從電影比較應用程式內部呼叫這項 Web 服務，根據電影分級讓使用者知道其中一部電影是否比另一部電影受到更多人的喜愛。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-112">In one possible scenario, this web service could be called from within a movie comparison app, telling the user whether one of the movies is really ‘liked’ more often than the other, based on movie ratings.</span></span>

> <span data-ttu-id="e6cdf-113">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="e6cdf-114">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="e6cdf-115">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="e6cdf-116">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="e6cdf-117">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e6cdf-117">Consumption of web service</span></span>
<span data-ttu-id="e6cdf-118">這項服務可接受 4 個引數，並執行比例的假設測試。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="e6cdf-119">輸入引數包括：</span><span class="sxs-lookup"><span data-stu-id="e6cdf-119">The input arguments are:</span></span>

* <span data-ttu-id="e6cdf-120">Successes1 - 樣本 1 中的成功事件數目。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="e6cdf-121">Successes2 - 樣本 2 中的成功事件數目。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="e6cdf-122">Total1 - 樣本 1 的大小。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="e6cdf-123">Total2 - 樣本 2 的大小。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="e6cdf-124">服務的輸出是假設測試的結果，並加上卡方統計資料、df、p 值，以及樣本 1/2 中的比例和信賴區間界限。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-124">The output of the service is the result of the hypothesis test along with the chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="e6cdf-125">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-125">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="e6cdf-126">以自動化方式取用服務的方法有很多種 ([這裡](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)提供一個範例應用程式)。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-126">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="e6cdf-127">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="e6cdf-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="e6cdf-128">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e6cdf-128">Creation of web service</span></span>
> <span data-ttu-id="e6cdf-129">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="e6cdf-130">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="e6cdf-131">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-131">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="e6cdf-132">Azure Machine Learning 中已建立具有兩個[執行 R 指令碼][execute-r-script]模組的新空白實驗。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="e6cdf-133">第一個模組會定義資料結構描述，而第二個模組則會使用 R 內的 prop.test 命令來執行 2 個比例的假設測試。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-133">In the first module the data schema is defined, while the second module uses the prop.test command within R to perform the hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="e6cdf-134">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="e6cdf-134">Experiment flow:</span></span>
![實驗流程][2]

#### <a name="module-1"></a><span data-ttu-id="e6cdf-136">模組 1：</span><span class="sxs-lookup"><span data-stu-id="e6cdf-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data to output port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="e6cdf-137">模組 2：</span><span class="sxs-lookup"><span data-stu-id="e6cdf-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"The proportions are different!",
    "The proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="e6cdf-138">限制</span><span class="sxs-lookup"><span data-stu-id="e6cdf-138">Limitations</span></span>
<span data-ttu-id="e6cdf-139">這是一個非常簡單的測試範例，可測試 2 個比例中的差異。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="e6cdf-140">從上面的範例程式碼可以看出，未實作錯誤攔截，且服務會假設所有變數都是連續的。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-140">As can be seen from the example code above, no error catching is implemented and the service assumes that all the variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="e6cdf-141">常見問題集</span><span class="sxs-lookup"><span data-stu-id="e6cdf-141">FAQ</span></span>
<span data-ttu-id="e6cdf-142">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="e6cdf-142">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

