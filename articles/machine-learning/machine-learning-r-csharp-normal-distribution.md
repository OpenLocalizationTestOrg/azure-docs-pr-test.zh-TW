---
title: "(已過時) 常態分佈 Web 服務套件 - Azure | Microsoft Docs"
description: "(已過時) 常態分佈 Web 服務套件"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
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
ms.openlocfilehash: 79d1621330ad56b0c62ca46cfac424c2306e371f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="68fde-103">(已過時) 常態分佈套件</span><span class="sxs-lookup"><span data-stu-id="68fde-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="68fde-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="68fde-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="68fde-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="68fde-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="68fde-106">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="68fde-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="68fde-107">常態分佈套件是一組範例 Web 服務 ([產生器](https://datamarket.azure.com/dataset/aml_labs/ndg7)、[分位數計算機](https://datamarket.azure.com/dataset/aml_labs/ndq5)、[機率計算機](https://datamarket.azure.com/dataset/aml_labs/ndp5))，可協助產生和處理常態分佈。</span><span class="sxs-lookup"><span data-stu-id="68fde-107">The Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="68fde-108">這些服務允許產生任何長度的常態分佈序列、計算指定機率的分位數，以及計算指定分位數的機率。</span><span class="sxs-lookup"><span data-stu-id="68fde-108">The services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="68fde-109">每個服務會根據所選取的服務發出不同的輸出 (請參閱下列說明)。</span><span class="sxs-lookup"><span data-stu-id="68fde-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="68fde-110">常態分佈套件會以 R 統計封裝中所包含的 R 函數 qnorm、rnorm 和 pnorm 為基礎。</span><span class="sxs-lookup"><span data-stu-id="68fde-110">The Normal Distribution Suite is based on the R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="68fde-111">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="68fde-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="68fde-112">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="68fde-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="68fde-113">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="68fde-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="68fde-114">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="68fde-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="68fde-115">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="68fde-115">Consumption of web service</span></span>
<span data-ttu-id="68fde-116">常態分佈套件包括下列 3 個服務。</span><span class="sxs-lookup"><span data-stu-id="68fde-116">The Normal Distribution Suite includes the following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="68fde-117">常態分佈分位數計算機</span><span class="sxs-lookup"><span data-stu-id="68fde-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="68fde-118">這項服務可接受 4 個常態分配的引數，並計算相關聯的分位數。</span><span class="sxs-lookup"><span data-stu-id="68fde-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>

<span data-ttu-id="68fde-119">輸入引數包括：</span><span class="sxs-lookup"><span data-stu-id="68fde-119">The input arguments are:</span></span>

* <span data-ttu-id="68fde-120">p - 常態分佈事件的單一機率。</span><span class="sxs-lookup"><span data-stu-id="68fde-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="68fde-121">Mean - 常態分佈平均值。</span><span class="sxs-lookup"><span data-stu-id="68fde-121">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="68fde-122">SD - 常態分佈標準差。</span><span class="sxs-lookup"><span data-stu-id="68fde-122">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="68fde-123">Side - L 代表分佈的下限，而 U 代表分佈的上限。</span><span class="sxs-lookup"><span data-stu-id="68fde-123">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="68fde-124">服務的輸出是計算與指定機率相關聯的分位數。</span><span class="sxs-lookup"><span data-stu-id="68fde-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="68fde-125">常態分佈機率計算機</span><span class="sxs-lookup"><span data-stu-id="68fde-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="68fde-126">這項服務可接受 4 個常態分佈的引數，並計算相關聯的機率。</span><span class="sxs-lookup"><span data-stu-id="68fde-126">This service accepts 4 arguments of a normal distribution and calculates the associated probability.</span></span>

<span data-ttu-id="68fde-127">輸入引數包括：</span><span class="sxs-lookup"><span data-stu-id="68fde-127">The input arguments are:</span></span>

* <span data-ttu-id="68fde-128">q - 常態分佈事件的單一分位數。</span><span class="sxs-lookup"><span data-stu-id="68fde-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="68fde-129">Mean - 常態分佈平均值。</span><span class="sxs-lookup"><span data-stu-id="68fde-129">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="68fde-130">SD - 常態分佈標準差。</span><span class="sxs-lookup"><span data-stu-id="68fde-130">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="68fde-131">Side - L 代表分佈的下限，而 U 代表分佈的上限。</span><span class="sxs-lookup"><span data-stu-id="68fde-131">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="68fde-132">服務的輸出是計算與指定分位數相關聯的機率。</span><span class="sxs-lookup"><span data-stu-id="68fde-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="68fde-133">常態分佈產生器</span><span class="sxs-lookup"><span data-stu-id="68fde-133">Normal Distribution Generator</span></span>
<span data-ttu-id="68fde-134">這項服務可接受 3 個常態分佈的引數，並產生已常態分佈的隨機序號。</span><span class="sxs-lookup"><span data-stu-id="68fde-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="68fde-135">要求中應提供下列引數：</span><span class="sxs-lookup"><span data-stu-id="68fde-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="68fde-136">n - 觀察的次數。</span><span class="sxs-lookup"><span data-stu-id="68fde-136">n - The number of observations.</span></span> 
* <span data-ttu-id="68fde-137">Mean - 常態分佈平均值。</span><span class="sxs-lookup"><span data-stu-id="68fde-137">mean - The normal distribution mean.</span></span>
* <span data-ttu-id="68fde-138">SD - 常態分佈標準差。</span><span class="sxs-lookup"><span data-stu-id="68fde-138">sd - The normal distribution standard deviation.</span></span> 

<span data-ttu-id="68fde-139">服務的輸出是一系列長度 n 和根據 mean 和 sd 引數的常態分佈。</span><span class="sxs-lookup"><span data-stu-id="68fde-139">The output of the service is a sequence of length n with a normal distribution based on the mean and sd arguments.</span></span>

> <span data-ttu-id="68fde-140">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="68fde-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="68fde-141">以自動化方式取用服務的方法有很多種 (範例應用程式如下：[產生器](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx)、[機率計算機](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx)、[分位數計算機](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx))。</span><span class="sxs-lookup"><span data-stu-id="68fde-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="68fde-142">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="68fde-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="68fde-143">常態分佈分位數計算機</span><span class="sxs-lookup"><span data-stu-id="68fde-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="68fde-144">常態分佈機率計算機</span><span class="sxs-lookup"><span data-stu-id="68fde-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="68fde-145">常態分佈產生器</span><span class="sxs-lookup"><span data-stu-id="68fde-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="68fde-146">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="68fde-146">Creation of web service</span></span>
> <span data-ttu-id="68fde-147">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="68fde-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="68fde-148">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="68fde-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="68fde-149">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="68fde-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="68fde-150">常態分佈分位數計算機</span><span class="sxs-lookup"><span data-stu-id="68fde-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="68fde-151">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="68fde-151">Experiment flow:</span></span>

![實驗流程][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="68fde-153">常態分佈機率計算機</span><span class="sxs-lookup"><span data-stu-id="68fde-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="68fde-154">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="68fde-154">Experiment flow:</span></span>

![實驗流程][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="68fde-156">常態分佈產生器</span><span class="sxs-lookup"><span data-stu-id="68fde-156">Normal Distribution Generator</span></span>
<span data-ttu-id="68fde-157">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="68fde-157">Experiment flow:</span></span>

![實驗流程][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="68fde-159">限制</span><span class="sxs-lookup"><span data-stu-id="68fde-159">Limitations</span></span>
<span data-ttu-id="68fde-160">這些是常態分佈的相關簡單範例。</span><span class="sxs-lookup"><span data-stu-id="68fde-160">These are very simple examples surrounding the normal distribution.</span></span> <span data-ttu-id="68fde-161">從上面的範例程式碼可以看出，已實作小小的錯誤攔截。</span><span class="sxs-lookup"><span data-stu-id="68fde-161">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="68fde-162">常見問題集</span><span class="sxs-lookup"><span data-stu-id="68fde-162">FAQ</span></span>
<span data-ttu-id="68fde-163">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="68fde-163">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

