---
title: "aaa(deprecated) 比例測試-Azure 中，差異 |Microsoft 文件"
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
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="976ca-103">(已過時) 比例差異測試</span><span class="sxs-lookup"><span data-stu-id="976ca-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="976ca-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="976ca-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="976ca-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="976ca-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="976ca-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="976ca-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="976ca-107">兩個比例有統計上的差異嗎？</span><span class="sxs-lookup"><span data-stu-id="976ca-107">Are two proportions statistically different?</span></span> <span data-ttu-id="976ca-108">假設使用者需要 toocompare 兩個影片 toodetermine 必須有一部電影的明顯更高比例 '喜歡' 當比較 toohello 其他。</span><span class="sxs-lookup"><span data-stu-id="976ca-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="976ca-109">使用大型的範例中，可能是 hello 比例 0.50 和 0.51 統計上明顯的差異。</span><span class="sxs-lookup"><span data-stu-id="976ca-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="976ca-110">使用一小部分的範例中，有可能無法足夠資料 toodetermine 如果這些比例實際不同。</span><span class="sxs-lookup"><span data-stu-id="976ca-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="976ca-111">這[web 服務](https://datamarket.azure.com/dataset/aml_labs/prop_test)進行兩個根據使用者輸入 hello 次數和試用 hello 2 比較群組的 hello 總數的比例 hello 差異檢定。</span><span class="sxs-lookup"><span data-stu-id="976ca-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="976ca-112">在一個可能的情況下，此 web 服務呼叫從影片比較應用程式，告知 hello 使用者是否 hello 影片的其中一個 '喜歡' 頻率遠高於其他 hello 根據電影分級中。</span><span class="sxs-lookup"><span data-stu-id="976ca-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="976ca-113">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="976ca-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="976ca-114">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="976ca-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="976ca-115">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="976ca-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="976ca-116">接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="976ca-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="976ca-117">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="976ca-117">Consumption of web service</span></span>
<span data-ttu-id="976ca-118">這項服務可接受 4 個引數，並執行比例的假設測試。</span><span class="sxs-lookup"><span data-stu-id="976ca-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="976ca-119">hello 輸入引數為：</span><span class="sxs-lookup"><span data-stu-id="976ca-119">hello input arguments are:</span></span>

* <span data-ttu-id="976ca-120">Successes1 - 樣本 1 中的成功事件數目。</span><span class="sxs-lookup"><span data-stu-id="976ca-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="976ca-121">Successes2 - 樣本 2 中的成功事件數目。</span><span class="sxs-lookup"><span data-stu-id="976ca-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="976ca-122">Total1 - 樣本 1 的大小。</span><span class="sxs-lookup"><span data-stu-id="976ca-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="976ca-123">Total2 - 樣本 2 的大小。</span><span class="sxs-lookup"><span data-stu-id="976ca-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="976ca-124">hello 服務的 hello 輸出是 hello 假設 hello 結果 hello chi-square 統計資料，df，p 值，以及測試，並在範例 1/2 和信賴區間界限內的比例。</span><span class="sxs-lookup"><span data-stu-id="976ca-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="976ca-125">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="976ca-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="976ca-126">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx))。</span><span class="sxs-lookup"><span data-stu-id="976ca-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="976ca-127">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="976ca-127">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="976ca-128">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="976ca-128">Creation of web service</span></span>
> <span data-ttu-id="976ca-129">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="976ca-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="976ca-130">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="976ca-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="976ca-131">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="976ca-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="976ca-132">Azure Machine Learning 中已建立具有兩個[執行 R 指令碼][execute-r-script]模組的新空白實驗。</span><span class="sxs-lookup"><span data-stu-id="976ca-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="976ca-133">Hello 第一個模組中 hello 資料結構描述定義，但 hello 第二個模組使用 R tooperform hello 假設測試中的 hello prop.test 命令進行 2 的比例。</span><span class="sxs-lookup"><span data-stu-id="976ca-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="976ca-134">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="976ca-134">Experiment flow:</span></span>
![實驗流程][2]

#### <a name="module-1"></a><span data-ttu-id="976ca-136">模組 1：</span><span class="sxs-lookup"><span data-stu-id="976ca-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="976ca-137">模組 2：</span><span class="sxs-lookup"><span data-stu-id="976ca-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="976ca-138">限制</span><span class="sxs-lookup"><span data-stu-id="976ca-138">Limitations</span></span>
<span data-ttu-id="976ca-139">這是一個非常簡單的測試範例，可測試 2 個比例中的差異。</span><span class="sxs-lookup"><span data-stu-id="976ca-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="976ca-140">可以從上述的 hello 範例程式碼看出，實作沒有錯誤攔截和 hello 服務承擔所有的 hello 變數是連續。</span><span class="sxs-lookup"><span data-stu-id="976ca-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="976ca-141">常見問題集</span><span class="sxs-lookup"><span data-stu-id="976ca-141">FAQ</span></span>
<span data-ttu-id="976ca-142">常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="976ca-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

