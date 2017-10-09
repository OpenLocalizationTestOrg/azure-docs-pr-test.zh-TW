---
title: "aaa(deprecated) 二項式分佈套件-Azure |Microsoft 文件"
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
redirect_document_id: True
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="06cbd-103">(已過時) 二項分配套件</span><span class="sxs-lookup"><span data-stu-id="06cbd-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="06cbd-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="06cbd-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="06cbd-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="06cbd-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="06cbd-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="06cbd-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="06cbd-107">hello 二項式分佈套件是一組範例 web 服務 ([二項式產生器](https://datamarket.azure.com/dataset/aml_labs/bdg5)，[機率計算機](https://datamarket.azure.com/dataset/aml_labs/bdp4)，[分量計算機](https://datamarket.azure.com/dataset/aml_labs/bdq5))，協助產生和處理二項式分佈。</span><span class="sxs-lookup"><span data-stu-id="06cbd-107">hello Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="06cbd-108">hello 服務允許產生二項式分佈序列的長度，計算分位數超出從給定的分量提供機率和計算的機率。</span><span class="sxs-lookup"><span data-stu-id="06cbd-108">hello services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="06cbd-109">每個 hello 服務會發出不同的輸出選取的 hello 服務為基礎 （請參閱下方說明）。</span><span class="sxs-lookup"><span data-stu-id="06cbd-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="06cbd-110">hello 二項式分佈套件為基礎 hello R 函式 qbinom、 rbinom 和 pbinom，hello 統計資料的 R 封裝中所包含的。</span><span class="sxs-lookup"><span data-stu-id="06cbd-110">hello Binomial Distribution Suite is based on hello R functions qbinom, rbinom, and pbinom, which are included in hello R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="06cbd-111">這些 web 服務無法供使用者 – 可能直接在 hello marketplace，透過行動裝置應用程式，透過網站，或甚至本機電腦上，例如。</span><span class="sxs-lookup"><span data-stu-id="06cbd-111">These web services could be consumed by users – potentially directly on hello marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="06cbd-112">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="06cbd-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="06cbd-113">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="06cbd-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="06cbd-114">hello web 服務可以發行的 toohello Azure Marketplace，供使用者和裝置 hello world-跨 hello 作者 hello web 服務的任何基礎結構設定不需要。</span><span class="sxs-lookup"><span data-stu-id="06cbd-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world – no infrastructure setup by hello author of hello web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="06cbd-115">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="06cbd-115">Consumption of web service</span></span>
<span data-ttu-id="06cbd-116">hello 二項式分佈套件包含下列 3 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="06cbd-116">hello Binomial Distribution Suite includes hello following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="06cbd-117">二項分配分位數計算機</span><span class="sxs-lookup"><span data-stu-id="06cbd-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="06cbd-118">此服務會接受常態分佈的 4 個引數和計算相關聯的 hello 分量。</span><span class="sxs-lookup"><span data-stu-id="06cbd-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>
<span data-ttu-id="06cbd-119">hello 輸入引數為：</span><span class="sxs-lookup"><span data-stu-id="06cbd-119">hello input arguments are:</span></span>

* <span data-ttu-id="06cbd-120">p - 多個試験的單一彙總機率。</span><span class="sxs-lookup"><span data-stu-id="06cbd-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="06cbd-121">大小-hello 的次數。</span><span class="sxs-lookup"><span data-stu-id="06cbd-121">size - hello number of trials.</span></span>
* <span data-ttu-id="06cbd-122">問題-hello 試用的成功機率。</span><span class="sxs-lookup"><span data-stu-id="06cbd-122">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="06cbd-123">端-1l 下邊 hello 分佈，如 hello 上邊的 hello 發佈 U hello。</span><span class="sxs-lookup"><span data-stu-id="06cbd-123">Side - L for hello lower side of hello distribution, U for hello upper side of hello distribution.</span></span> 

<span data-ttu-id="06cbd-124">hello 輸出 hello 服務是以指定機率 hello 相關聯之計算的 hello 分量。</span><span class="sxs-lookup"><span data-stu-id="06cbd-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="06cbd-125">二項分配機率計算機</span><span class="sxs-lookup"><span data-stu-id="06cbd-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="06cbd-126">此服務會接受二項式分佈的 4 個引數，並可計算出 hello 相關聯的機率。</span><span class="sxs-lookup"><span data-stu-id="06cbd-126">This service accepts 4 arguments of a binomial distribution and calculates hello associated probability.</span></span>
<span data-ttu-id="06cbd-127">hello 輸入引數為：</span><span class="sxs-lookup"><span data-stu-id="06cbd-127">hello input arguments are:</span></span>

* <span data-ttu-id="06cbd-128">q - 二項分配事件的單一分位數。</span><span class="sxs-lookup"><span data-stu-id="06cbd-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="06cbd-129">大小-hello 的次數。</span><span class="sxs-lookup"><span data-stu-id="06cbd-129">size - hello number of trials.</span></span>
* <span data-ttu-id="06cbd-130">問題-hello 試用的成功機率。</span><span class="sxs-lookup"><span data-stu-id="06cbd-130">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="06cbd-131">端-1l hello 下邊的 hello 分佈，hello 上邊的 hello 發佈的 U 或 E 等於 tooa 成功次數的單一數字。</span><span class="sxs-lookup"><span data-stu-id="06cbd-131">side - L for hello lower side of hello distribution, U for hello upper side of hello distribution, or E that is equal tooa single number of successes.</span></span>

<span data-ttu-id="06cbd-132">hello 輸出 hello 服務是以指定分量的 hello 有關的 hello 計算機率。</span><span class="sxs-lookup"><span data-stu-id="06cbd-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="06cbd-133">二項分配產生器</span><span class="sxs-lookup"><span data-stu-id="06cbd-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="06cbd-134">這項服務可接受 3 個二項分配的引數，並產生已二項分配的隨機序號。</span><span class="sxs-lookup"><span data-stu-id="06cbd-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="06cbd-135">hello 下列引數應該提供 tooit 內 hello 要求：</span><span class="sxs-lookup"><span data-stu-id="06cbd-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="06cbd-136">n - 觀察的次數。</span><span class="sxs-lookup"><span data-stu-id="06cbd-136">n - Number of observations.</span></span> 
* <span data-ttu-id="06cbd-137">size - 試驗的次數。</span><span class="sxs-lookup"><span data-stu-id="06cbd-137">size - Number of trials.</span></span>
* <span data-ttu-id="06cbd-138">prob - 成功的機率。</span><span class="sxs-lookup"><span data-stu-id="06cbd-138">prob - Probability of success.</span></span>

<span data-ttu-id="06cbd-139">hello 服務的 hello 輸出是一串長度 n 二項式分佈根據 hello 大小和問題引數。</span><span class="sxs-lookup"><span data-stu-id="06cbd-139">hello output of hello service is a sequence of length n with a binomial distribution based on hello size and prob arguments.</span></span>

> <span data-ttu-id="06cbd-140">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="06cbd-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="06cbd-141">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式會在此處：[產生器](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx)，[機率計算機](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx)，[分量計算機](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator))。</span><span class="sxs-lookup"><span data-stu-id="06cbd-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="06cbd-142">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="06cbd-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="06cbd-143">二項分配分位數計算機</span><span class="sxs-lookup"><span data-stu-id="06cbd-143">Binomial Distribution Quantile Calculator</span></span>
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

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="06cbd-144">二項分配機率計算機</span><span class="sxs-lookup"><span data-stu-id="06cbd-144">Binomial Distribution Probability Calculator</span></span>
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


### <a name="binomial-distribution-generator"></a><span data-ttu-id="06cbd-145">二項分配產生器</span><span class="sxs-lookup"><span data-stu-id="06cbd-145">Binomial Distribution Generator</span></span>
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





## <a name="creation-of-web-service"></a><span data-ttu-id="06cbd-146">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="06cbd-146">Creation of web service</span></span>
> <span data-ttu-id="06cbd-147">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="06cbd-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="06cbd-148">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="06cbd-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="06cbd-149">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="06cbd-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="06cbd-150">二項分配分位數計算機</span><span class="sxs-lookup"><span data-stu-id="06cbd-150">Binomial Distribution Quantile Calculator</span></span>
![建立工作區][4]

#### <a name="module-1"></a><span data-ttu-id="06cbd-152">模組 1：</span><span class="sxs-lookup"><span data-stu-id="06cbd-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a><span data-ttu-id="06cbd-153">模組 2：</span><span class="sxs-lookup"><span data-stu-id="06cbd-153">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="06cbd-154">二項分配機率計算機</span><span class="sxs-lookup"><span data-stu-id="06cbd-154">Binomial Distribution Probability Calculator</span></span>
![建立工作區][5]

#### <a name="module-1"></a><span data-ttu-id="06cbd-156">模組 1：</span><span class="sxs-lookup"><span data-stu-id="06cbd-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a><span data-ttu-id="06cbd-157">模組 2：</span><span class="sxs-lookup"><span data-stu-id="06cbd-157">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="06cbd-158">二項分配產生器</span><span class="sxs-lookup"><span data-stu-id="06cbd-158">Binomial Distribution Generator</span></span>
![建立工作區][6]

#### <a name="module-1"></a><span data-ttu-id="06cbd-160">模組 1：</span><span class="sxs-lookup"><span data-stu-id="06cbd-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="06cbd-161">模組 2：</span><span class="sxs-lookup"><span data-stu-id="06cbd-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="06cbd-162">限制</span><span class="sxs-lookup"><span data-stu-id="06cbd-162">Limitations</span></span>
<span data-ttu-id="06cbd-163">這些是非常簡單的範例周圍 hello 二項式分佈。</span><span class="sxs-lookup"><span data-stu-id="06cbd-163">These are very simple examples surrounding hello binomial distribution.</span></span> <span data-ttu-id="06cbd-164">如下所示上述的 hello 範例程式碼，將實作小錯誤攔截。</span><span class="sxs-lookup"><span data-stu-id="06cbd-164">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="06cbd-165">常見問題集</span><span class="sxs-lookup"><span data-stu-id="06cbd-165">FAQ</span></span>
<span data-ttu-id="06cbd-166">常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="06cbd-166">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

