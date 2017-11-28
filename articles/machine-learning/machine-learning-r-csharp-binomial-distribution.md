---
title: "(已過時) 二項分配套件 - Azure | Microsoft Docs"
description: "(已過時) 二項分配套件"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 6f0a6d06e7401c8360a92a707a0552f41ff3657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="ca81b-103">(已過時) 二項分配套件</span><span class="sxs-lookup"><span data-stu-id="ca81b-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="ca81b-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="ca81b-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="ca81b-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="ca81b-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="ca81b-106">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="ca81b-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="ca81b-107">二項分配套件是一組範例 Web 服務 ([二項產生器](https://datamarket.azure.com/dataset/aml_labs/bdg5)、[機率計算機](https://datamarket.azure.com/dataset/aml_labs/bdp4)、[分位數計算機](https://datamarket.azure.com/dataset/aml_labs/bdq5))，可協助產生和處理二項分配。</span><span class="sxs-lookup"><span data-stu-id="ca81b-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="ca81b-108">這些服務允許產生任何長度的二項分配序列、算出指定機率的分位數，以及計算指定分位數的機率。</span><span class="sxs-lookup"><span data-stu-id="ca81b-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="ca81b-109">每個服務會根據所選取的服務發出不同的輸出 (請參閱下列說明)。</span><span class="sxs-lookup"><span data-stu-id="ca81b-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="ca81b-110">二項分配套件會以 R 統計封裝中所包含的 R 函數 qbinom、rbinom 和 pbinom 為基礎。</span><span class="sxs-lookup"><span data-stu-id="ca81b-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="ca81b-111">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，直接在 Marketplace 上取用這些 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="ca81b-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="ca81b-112">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="ca81b-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="ca81b-113">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="ca81b-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="ca81b-114">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ca81b-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="ca81b-115">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="ca81b-115">Consumption of web service</span></span>
<span data-ttu-id="ca81b-116">二項分配套件包括下列 3 個服務。</span><span class="sxs-lookup"><span data-stu-id="ca81b-116">The Binomial Distribution Suite includes the following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="ca81b-117">二項分配分位數計算機</span><span class="sxs-lookup"><span data-stu-id="ca81b-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="ca81b-118">這項服務可接受 4 個常態分配的引數，並計算相關聯的分位數。</span><span class="sxs-lookup"><span data-stu-id="ca81b-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>
<span data-ttu-id="ca81b-119">輸入引數包括：</span><span class="sxs-lookup"><span data-stu-id="ca81b-119">The input arguments are:</span></span>

* <span data-ttu-id="ca81b-120">p - 多個試験的單一彙總機率。</span><span class="sxs-lookup"><span data-stu-id="ca81b-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="ca81b-121">size - 試驗的次數。</span><span class="sxs-lookup"><span data-stu-id="ca81b-121">size - The number of trials.</span></span>
* <span data-ttu-id="ca81b-122">prob - 試驗中的成功機率。</span><span class="sxs-lookup"><span data-stu-id="ca81b-122">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="ca81b-123">Side - L 代表分配的下限，U 代表分配的上限。</span><span class="sxs-lookup"><span data-stu-id="ca81b-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span></span> 

<span data-ttu-id="ca81b-124">服務的輸出是計算與指定機率相關聯的分位數。</span><span class="sxs-lookup"><span data-stu-id="ca81b-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="ca81b-125">二項分配機率計算機</span><span class="sxs-lookup"><span data-stu-id="ca81b-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="ca81b-126">這項服務可接受 4 個二項分配的引數，並計算相關聯的機率。</span><span class="sxs-lookup"><span data-stu-id="ca81b-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span></span>
<span data-ttu-id="ca81b-127">輸入引數包括：</span><span class="sxs-lookup"><span data-stu-id="ca81b-127">The input arguments are:</span></span>

* <span data-ttu-id="ca81b-128">q - 二項分配事件的單一分位數。</span><span class="sxs-lookup"><span data-stu-id="ca81b-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="ca81b-129">size - 試驗的次數。</span><span class="sxs-lookup"><span data-stu-id="ca81b-129">size - The number of trials.</span></span>
* <span data-ttu-id="ca81b-130">prob - 試驗中的成功機率。</span><span class="sxs-lookup"><span data-stu-id="ca81b-130">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="ca81b-131">side - L 代表分配的下限，U 代表分配的上限，或 E 等於成功的單一數目。</span><span class="sxs-lookup"><span data-stu-id="ca81b-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span></span>

<span data-ttu-id="ca81b-132">服務的輸出是計算與指定分位數相關聯的機率。</span><span class="sxs-lookup"><span data-stu-id="ca81b-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="ca81b-133">二項分配產生器</span><span class="sxs-lookup"><span data-stu-id="ca81b-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="ca81b-134">這項服務可接受 3 個二項分配的引數，並產生已二項分配的隨機序號。</span><span class="sxs-lookup"><span data-stu-id="ca81b-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="ca81b-135">要求中應提供下列引數：</span><span class="sxs-lookup"><span data-stu-id="ca81b-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="ca81b-136">n - 觀察的次數。</span><span class="sxs-lookup"><span data-stu-id="ca81b-136">n - Number of observations.</span></span> 
* <span data-ttu-id="ca81b-137">size - 試驗的次數。</span><span class="sxs-lookup"><span data-stu-id="ca81b-137">size - Number of trials.</span></span>
* <span data-ttu-id="ca81b-138">prob - 成功的機率。</span><span class="sxs-lookup"><span data-stu-id="ca81b-138">prob - Probability of success.</span></span>

<span data-ttu-id="ca81b-139">服務的輸出是一系列長度 n 和根據 size 和 prob 引數的二項分配。</span><span class="sxs-lookup"><span data-stu-id="ca81b-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span></span>

> <span data-ttu-id="ca81b-140">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="ca81b-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="ca81b-141">以自動化方式取用服務的方法有很多種 (範例應用程式如下：[產生器](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx)、[機率計算機](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx)、[分位數計算機](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator))。</span><span class="sxs-lookup"><span data-stu-id="ca81b-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="ca81b-142">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="ca81b-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="ca81b-143">二項分配分位數計算機</span><span class="sxs-lookup"><span data-stu-id="ca81b-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="ca81b-144">二項分配機率計算機</span><span class="sxs-lookup"><span data-stu-id="ca81b-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="ca81b-145">二項分配產生器</span><span class="sxs-lookup"><span data-stu-id="ca81b-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="ca81b-146">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="ca81b-146">Creation of web service</span></span>
> <span data-ttu-id="ca81b-147">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="ca81b-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="ca81b-148">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="ca81b-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="ca81b-149">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca81b-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="ca81b-150">二項分配分位數計算機</span><span class="sxs-lookup"><span data-stu-id="ca81b-150">Binomial Distribution Quantile Calculator</span></span>
![建立工作區][4]

#### <a name="module-1"></a><span data-ttu-id="ca81b-152">模組 1：</span><span class="sxs-lookup"><span data-stu-id="ca81b-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a><span data-ttu-id="ca81b-153">模組 2：</span><span class="sxs-lookup"><span data-stu-id="ca81b-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="ca81b-154">二項分配機率計算機</span><span class="sxs-lookup"><span data-stu-id="ca81b-154">Binomial Distribution Probability Calculator</span></span>
![建立工作區][5]

#### <a name="module-1"></a><span data-ttu-id="ca81b-156">模組 1：</span><span class="sxs-lookup"><span data-stu-id="ca81b-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a><span data-ttu-id="ca81b-157">模組 2：</span><span class="sxs-lookup"><span data-stu-id="ca81b-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="ca81b-158">二項分配產生器</span><span class="sxs-lookup"><span data-stu-id="ca81b-158">Binomial Distribution Generator</span></span>
![建立工作區][6]

#### <a name="module-1"></a><span data-ttu-id="ca81b-160">模組 1：</span><span class="sxs-lookup"><span data-stu-id="ca81b-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="ca81b-161">模組 2：</span><span class="sxs-lookup"><span data-stu-id="ca81b-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="ca81b-162">限制</span><span class="sxs-lookup"><span data-stu-id="ca81b-162">Limitations</span></span>
<span data-ttu-id="ca81b-163">這些是二項分配的相關簡單範例。</span><span class="sxs-lookup"><span data-stu-id="ca81b-163">These are very simple examples surrounding the binomial distribution.</span></span> <span data-ttu-id="ca81b-164">從上面的範例程式碼可以看出，已實作小小的錯誤攔截。</span><span class="sxs-lookup"><span data-stu-id="ca81b-164">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="ca81b-165">常見問題集</span><span class="sxs-lookup"><span data-stu-id="ca81b-165">FAQ</span></span>
<span data-ttu-id="ca81b-166">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="ca81b-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

