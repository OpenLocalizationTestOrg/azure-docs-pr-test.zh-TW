---
title: "aaa(deprecated) 叢集模型-Azure |Microsoft 文件"
description: "(已過時) 叢集模型"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="bcc48-103">(已過時) 叢集模型</span><span class="sxs-lookup"><span data-stu-id="bcc48-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="bcc48-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="bcc48-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="bcc48-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="bcc48-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="bcc48-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="bcc48-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="bcc48-107">我們可以預測的順序 tooreduce hello 電量關閉風險的信用卡簽發者的信用額度 cardholders 行為的群組？</span><span class="sxs-lookup"><span data-stu-id="bcc48-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="bcc48-108">我們如何可以定義群組的特質特性的員工順序 tooimprove 其工作的效能？</span><span class="sxs-lookup"><span data-stu-id="bcc48-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="bcc48-109">如何可以醫生分類病人分組根據其疾病 hello 特性？</span><span class="sxs-lookup"><span data-stu-id="bcc48-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="bcc48-110">基本上，叢集分析可以回答所有這些問題。</span><span class="sxs-lookup"><span data-stu-id="bcc48-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="bcc48-111">叢集分析會根據變數的組合，將一組觀察分成兩個或多個互斥的未知群組。</span><span class="sxs-lookup"><span data-stu-id="bcc48-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="bcc48-112">hello 叢集分析的目的是 toodiscover 系統的組織成群組的觀察值，通常是人員或它們的特性，其中 hello 群組的成員共用屬性在一般。</span><span class="sxs-lookup"><span data-stu-id="bcc48-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="bcc48-113">這[服務](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model)使用 hello K-means 方法，一個常用的群集技巧，toocluster 任意資料分組。</span><span class="sxs-lookup"><span data-stu-id="bcc48-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="bcc48-114">此 web 服務會接受 hello 資料並 hello 數目 k 叢集做為輸入，並產生其中的每個觀察值所屬的 hello k 群組 toowhich 預測。</span><span class="sxs-lookup"><span data-stu-id="bcc48-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="bcc48-115">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="bcc48-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="bcc48-116">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="bcc48-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="bcc48-117">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="bcc48-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="bcc48-118">接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="bcc48-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="bcc48-119">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="bcc48-119">Consumption of web service</span></span>
<span data-ttu-id="bcc48-120">此 web 服務會將 hello 資料分組的每個資料列的 k 群組和輸出 hello 群組指派一組。</span><span class="sxs-lookup"><span data-stu-id="bcc48-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="bcc48-121">hello web 服務預期 hello 終端使用者 tooinput 資料做為字串，其中會以逗號 （，） 分隔的資料列和資料行以分號 （;） 分隔。</span><span class="sxs-lookup"><span data-stu-id="bcc48-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="bcc48-122">hello web 服務中，必須要有 1 個資料列一次。</span><span class="sxs-lookup"><span data-stu-id="bcc48-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="bcc48-123">範例資料集看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="bcc48-123">An example dataset could look like this:</span></span>

![範例資料][1]

<span data-ttu-id="bcc48-125">假設此資料 hello 使用者希望 tooseparate 3 互斥分組。</span><span class="sxs-lookup"><span data-stu-id="bcc48-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="bcc48-126">hello 輸入的資料集上方 hello hello 下列資料： 值 ="10 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12，則為 2; 1,10; 3; 4";k ="3"。</span><span class="sxs-lookup"><span data-stu-id="bcc48-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="bcc48-127">hello 輸出是 hello 資料列的每個 hello 預測的群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="bcc48-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="bcc48-128">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="bcc48-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="bcc48-129">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx))。</span><span class="sxs-lookup"><span data-stu-id="bcc48-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="bcc48-130">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="bcc48-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="bcc48-131">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="bcc48-131">Creation of web service</span></span>
> <span data-ttu-id="bcc48-132">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="bcc48-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="bcc48-133">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="bcc48-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="bcc48-134">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="bcc48-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="bcc48-135">在 Azure Machine Learning 中，新的空白實驗建立的來源和兩個[執行 R 指令碼][ execute-r-script]模組提取到 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="bcc48-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="bcc48-136">建立 hello 資料結構描述使用簡單[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="bcc48-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="bcc48-137">然後，hello 資料結構描述已連結的 toohello 叢集模型 > 一節，以重新建立[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="bcc48-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="bcc48-138">在 hello[執行 R 指令碼][ execute-r-script]用於 hello 群集模型，hello web 服務然後會利用 hello"的 k-means"函式，也就是預先建置到 hello[執行 R 指令碼][ execute-r-script] Azure 機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="bcc48-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![實驗流程][3]

#### <a name="module-1"></a><span data-ttu-id="bcc48-140">模組 1：</span><span class="sxs-lookup"><span data-stu-id="bcc48-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="bcc48-141">模組 2：</span><span class="sxs-lookup"><span data-stu-id="bcc48-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="bcc48-142">限制</span><span class="sxs-lookup"><span data-stu-id="bcc48-142">Limitations</span></span>
<span data-ttu-id="bcc48-143">這是一個非常簡單的群集 Web 服務範例。</span><span class="sxs-lookup"><span data-stu-id="bcc48-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="bcc48-144">可以從上述的 hello 範例程式碼看出，實作沒有錯誤攔截和 hello 服務承擔一切都是連續的變數 （沒有類別功能允許），當做 hello 服務只有輸入數字值時的這個 web 的 hello 建立 hello服務。</span><span class="sxs-lookup"><span data-stu-id="bcc48-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="bcc48-145">此外，hello 服務目前會處理有限的資料大小，因為 toohello 要求/回應性質 hello web 服務呼叫和 hello hello 模型的事實所適合每次呼叫 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="bcc48-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="bcc48-146">常見問題集</span><span class="sxs-lookup"><span data-stu-id="bcc48-146">FAQ</span></span>
<span data-ttu-id="bcc48-147">常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="bcc48-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

