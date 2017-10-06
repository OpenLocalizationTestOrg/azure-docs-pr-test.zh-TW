---
title: "aaa(deprecated) 常態分佈 Web 服務套件-Azure |Microsoft 文件"
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
redirect_document_id: True
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="86b3d-103">(已過時) 常態分佈套件</span><span class="sxs-lookup"><span data-stu-id="86b3d-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="86b3d-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="86b3d-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="86b3d-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="86b3d-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="86b3d-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="86b3d-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="86b3d-107">hello 常態分佈套件是一組範例 web 服務 ([產生器](https://datamarket.azure.com/dataset/aml_labs/ndg7)，[分量計算機](https://datamarket.azure.com/dataset/aml_labs/ndq5)，[機率計算機](https://datamarket.azure.com/dataset/aml_labs/ndp5))，協助在產生和處理常態分佈。</span><span class="sxs-lookup"><span data-stu-id="86b3d-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="86b3d-108">hello 服務可讓產生常態分佈序列的長度，計算從指定的機率，分量，計算從指定的分量的機率。</span><span class="sxs-lookup"><span data-stu-id="86b3d-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="86b3d-109">每個 hello 服務會發出不同的輸出選取的 hello 服務為基礎 （請參閱下方說明）。</span><span class="sxs-lookup"><span data-stu-id="86b3d-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="86b3d-110">hello 常態分佈套件為基礎 hello R 函式 qnorm、 rnorm 和 pnorm，它們包含在統計資料的 R 封裝。</span><span class="sxs-lookup"><span data-stu-id="86b3d-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="86b3d-111">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="86b3d-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="86b3d-112">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="86b3d-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="86b3d-113">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="86b3d-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="86b3d-114">接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="86b3d-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="86b3d-115">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="86b3d-115">Consumption of web service</span></span>
<span data-ttu-id="86b3d-116">hello 常態分佈套件包含下列 3 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="86b3d-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="86b3d-117">常態分佈分位數計算機</span><span class="sxs-lookup"><span data-stu-id="86b3d-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="86b3d-118">此服務會接受常態分佈的 4 個引數和計算相關聯的 hello 分量。</span><span class="sxs-lookup"><span data-stu-id="86b3d-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="86b3d-119">hello 輸入引數為：</span><span class="sxs-lookup"><span data-stu-id="86b3d-119">hello input arguments are:</span></span>

* <span data-ttu-id="86b3d-120">p - 常態分佈事件的單一機率。</span><span class="sxs-lookup"><span data-stu-id="86b3d-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="86b3d-121">表示-hello 常態分佈平均值。</span><span class="sxs-lookup"><span data-stu-id="86b3d-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="86b3d-122">SD-hello 常態分佈的標準差。</span><span class="sxs-lookup"><span data-stu-id="86b3d-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="86b3d-123">側邊-1l 下邊 hello 發佈 hello 和上邊 hello 發佈 hello 的 U。</span><span class="sxs-lookup"><span data-stu-id="86b3d-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="86b3d-124">hello 輸出 hello 服務是以指定機率 hello 相關聯之計算的 hello 分量。</span><span class="sxs-lookup"><span data-stu-id="86b3d-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="86b3d-125">常態分佈機率計算機</span><span class="sxs-lookup"><span data-stu-id="86b3d-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="86b3d-126">此服務會接受常態分佈的 4 個引數，並可計算出 hello 相關聯的機率。</span><span class="sxs-lookup"><span data-stu-id="86b3d-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="86b3d-127">hello 輸入引數為：</span><span class="sxs-lookup"><span data-stu-id="86b3d-127">hello input arguments are:</span></span>

* <span data-ttu-id="86b3d-128">q - 常態分佈事件的單一分位數。</span><span class="sxs-lookup"><span data-stu-id="86b3d-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="86b3d-129">表示-hello 常態分佈平均值。</span><span class="sxs-lookup"><span data-stu-id="86b3d-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="86b3d-130">SD-hello 常態分佈的標準差。</span><span class="sxs-lookup"><span data-stu-id="86b3d-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="86b3d-131">側邊-1l 下邊 hello 發佈 hello 和上邊 hello 發佈 hello 的 U。</span><span class="sxs-lookup"><span data-stu-id="86b3d-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="86b3d-132">hello 輸出 hello 服務是以指定分量的 hello 有關的 hello 計算機率。</span><span class="sxs-lookup"><span data-stu-id="86b3d-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="86b3d-133">常態分佈產生器</span><span class="sxs-lookup"><span data-stu-id="86b3d-133">Normal Distribution Generator</span></span>
<span data-ttu-id="86b3d-134">這項服務可接受 3 個常態分佈的引數，並產生已常態分佈的隨機序號。</span><span class="sxs-lookup"><span data-stu-id="86b3d-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="86b3d-135">hello 下列引數應該提供 tooit 內 hello 要求：</span><span class="sxs-lookup"><span data-stu-id="86b3d-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="86b3d-136">n 層 hello 觀測值數目。</span><span class="sxs-lookup"><span data-stu-id="86b3d-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="86b3d-137">表示-hello 常態分佈平均值。</span><span class="sxs-lookup"><span data-stu-id="86b3d-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="86b3d-138">sd-hello 常態分佈的標準差。</span><span class="sxs-lookup"><span data-stu-id="86b3d-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="86b3d-139">hello 服務的 hello 輸出是含有一般分佈根據 hello 平均值和 sd 引數的長度 n 的序列。</span><span class="sxs-lookup"><span data-stu-id="86b3d-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="86b3d-140">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="86b3d-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="86b3d-141">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式會在此處：[產生器](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx)，[機率計算機](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx)，[分量計算機](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx))。</span><span class="sxs-lookup"><span data-stu-id="86b3d-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="86b3d-142">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="86b3d-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="86b3d-143">常態分佈分位數計算機</span><span class="sxs-lookup"><span data-stu-id="86b3d-143">Normal Distribution Quantile Calculator</span></span>
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


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="86b3d-144">常態分佈機率計算機</span><span class="sxs-lookup"><span data-stu-id="86b3d-144">Normal Distribution Probability Calculator</span></span>
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

### <a name="normal-distribution-generator"></a><span data-ttu-id="86b3d-145">常態分佈產生器</span><span class="sxs-lookup"><span data-stu-id="86b3d-145">Normal Distribution Generator</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="86b3d-146">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="86b3d-146">Creation of web service</span></span>
> <span data-ttu-id="86b3d-147">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="86b3d-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="86b3d-148">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="86b3d-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="86b3d-149">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="86b3d-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="86b3d-150">常態分佈分位數計算機</span><span class="sxs-lookup"><span data-stu-id="86b3d-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="86b3d-151">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="86b3d-151">Experiment flow:</span></span>

![實驗流程][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="86b3d-153">常態分佈機率計算機</span><span class="sxs-lookup"><span data-stu-id="86b3d-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="86b3d-154">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="86b3d-154">Experiment flow:</span></span>

![實驗流程][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="86b3d-156">常態分佈產生器</span><span class="sxs-lookup"><span data-stu-id="86b3d-156">Normal Distribution Generator</span></span>
<span data-ttu-id="86b3d-157">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="86b3d-157">Experiment flow:</span></span>

![實驗流程][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="86b3d-159">限制</span><span class="sxs-lookup"><span data-stu-id="86b3d-159">Limitations</span></span>
<span data-ttu-id="86b3d-160">這些是非常簡單的範例周圍 hello 常態分佈。</span><span class="sxs-lookup"><span data-stu-id="86b3d-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="86b3d-161">如下所示上述的 hello 範例程式碼，將實作小錯誤攔截。</span><span class="sxs-lookup"><span data-stu-id="86b3d-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="86b3d-162">常見問題集</span><span class="sxs-lookup"><span data-stu-id="86b3d-162">FAQ</span></span>
<span data-ttu-id="86b3d-163">常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="86b3d-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

