---
title: "(已過時) 叢集模型 - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7cbbbd6d4236dab638eb3051595a584557480841
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="9f31c-103">(已過時) 叢集模型</span><span class="sxs-lookup"><span data-stu-id="9f31c-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="9f31c-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="9f31c-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="9f31c-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="9f31c-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9f31c-106">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="9f31c-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="9f31c-107">我們可以如何預測多組的信用卡持卡人行為，以降低信用卡發卡機構的壞帳風險？</span><span class="sxs-lookup"><span data-stu-id="9f31c-107">How can we predict groups of credit cardholders’ behaviors in order to reduce the charge-off risk of credit card issuers?</span></span> <span data-ttu-id="9f31c-108">我們可以如何定義多組員工的人格特質，以提高員工工作效能？</span><span class="sxs-lookup"><span data-stu-id="9f31c-108">How can we define groups of personality traits of employees in order to improve their performance at work?</span></span> <span data-ttu-id="9f31c-109">醫生可以如何根據疾病特性來將病人分類？</span><span class="sxs-lookup"><span data-stu-id="9f31c-109">How can doctors classify patients into groups based on the characteristics of their diseases?</span></span> <span data-ttu-id="9f31c-110">基本上，叢集分析可以回答所有這些問題。</span><span class="sxs-lookup"><span data-stu-id="9f31c-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9f31c-111">叢集分析會根據變數的組合，將一組觀察分成兩個或多個互斥的未知群組。</span><span class="sxs-lookup"><span data-stu-id="9f31c-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="9f31c-112">叢集分析的目的是要找出將觀察 (通常是人員或其特性) 分組的系統，其中群組成員會共用共同的屬性。</span><span class="sxs-lookup"><span data-stu-id="9f31c-112">The purpose of cluster analysis is to discover a system of organizing observations, usually people or their characteristics, into groups, where members of the groups share properties in common.</span></span> <span data-ttu-id="9f31c-113">這項 [服務](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) 使用 K-Means 方法 (常用的叢集技術) 來群集任意資料。</span><span class="sxs-lookup"><span data-stu-id="9f31c-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses the K-Means methodology, a commonly used clustering technique, to cluster arbitrary data into groups.</span></span> <span data-ttu-id="9f31c-114">這項 Web 服務會接受資料和 k 個叢集做為輸入，並產生有關每個觀察屬於哪個 k 群組的預測。</span><span class="sxs-lookup"><span data-stu-id="9f31c-114">This web service takes the data and the number of k clusters as input, and produces predictions of which of the k groups to which each observations belongs.</span></span> 

> <span data-ttu-id="9f31c-115">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9f31c-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="9f31c-116">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9f31c-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="9f31c-117">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9f31c-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="9f31c-118">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="9f31c-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="9f31c-119">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="9f31c-119">Consumption of web service</span></span>
<span data-ttu-id="9f31c-120">此 Web 服務會將資料分成一組 k 群組，並輸出每個資料列的群組指派。</span><span class="sxs-lookup"><span data-stu-id="9f31c-120">This web service groups the data into a set of k groups and outputs the group assignment for each row.</span></span> <span data-ttu-id="9f31c-121">Web 服務需要使用者以字串形式輸入資料，其中資料列會以逗號 (,) 分隔，而資料行會以分號 (;) 分隔。</span><span class="sxs-lookup"><span data-stu-id="9f31c-121">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="9f31c-122">Web 服務一次需要 1 個資料列。</span><span class="sxs-lookup"><span data-stu-id="9f31c-122">The web service expects 1 row at a time.</span></span> <span data-ttu-id="9f31c-123">範例資料集看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="9f31c-123">An example dataset could look like this:</span></span>

![範例資料][1]

<span data-ttu-id="9f31c-125">假設使用者想要將資料分成三個互斥的群組。</span><span class="sxs-lookup"><span data-stu-id="9f31c-125">Suppose the user wanted to separate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="9f31c-126">上述資料集的輸入資料應如下所示：值 = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”；k=”3”。</span><span class="sxs-lookup"><span data-stu-id="9f31c-126">The data input for the above dataset would be the following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="9f31c-127">輸出會是每個資料列的預測群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="9f31c-127">The output is the predicted group membership for each of the rows.</span></span>

> <span data-ttu-id="9f31c-128">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="9f31c-128">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="9f31c-129">以自動化方式取用服務的方法有很多種 ([這裡](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)提供一個範例應用程式)。</span><span class="sxs-lookup"><span data-stu-id="9f31c-129">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="9f31c-130">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="9f31c-130">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="9f31c-131">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="9f31c-131">Creation of web service</span></span>
> <span data-ttu-id="9f31c-132">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="9f31c-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="9f31c-133">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="9f31c-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="9f31c-134">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="9f31c-134">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="9f31c-135">從 Azure Machine Learning 中，已建立一個新的空白實驗，並將兩個[執行 R 指令碼][execute-r-script]模組提取到工作區。</span><span class="sxs-lookup"><span data-stu-id="9f31c-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="9f31c-136">資料結構描述是以簡單的[執行 R 指令碼][execute-r-script]建立的。</span><span class="sxs-lookup"><span data-stu-id="9f31c-136">The data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="9f31c-137">接著，資料結構描述被連結到叢集模型區段，此區段同樣也是以[執行 R 指令碼][execute-r-script]建立的。</span><span class="sxs-lookup"><span data-stu-id="9f31c-137">Then, the data schema was linked to the cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="9f31c-138">在用於叢集模型的[執行 R 指令碼][execute-r-script]中，Web 服務會接著使用 “k-means” 函數 (已預先建置到 Azure Machine Learning 的[執行 R 指令碼][execute-r-script]中)。</span><span class="sxs-lookup"><span data-stu-id="9f31c-138">In the [Execute R Script][execute-r-script] used for the cluster model, the web service then utilizes the “k-means” function, which is prebuilt into the [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![實驗流程][3]

#### <a name="module-1"></a><span data-ttu-id="9f31c-140">模組 1：</span><span class="sxs-lookup"><span data-stu-id="9f31c-140">Module 1:</span></span>
    #Enter the input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="9f31c-141">模組 2：</span><span class="sxs-lookup"><span data-stu-id="9f31c-141">Module 2:</span></span>
    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="9f31c-142">限制</span><span class="sxs-lookup"><span data-stu-id="9f31c-142">Limitations</span></span>
<span data-ttu-id="9f31c-143">這是一個非常簡單的群集 Web 服務範例。</span><span class="sxs-lookup"><span data-stu-id="9f31c-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="9f31c-144">從上面的範例程式碼可以看出，未實作錯誤攔截，且由於建立這項 Web 服務時，服務只輸入數值，因此服務會假設所有項目都是連續變數 (不允許類別功能)。</span><span class="sxs-lookup"><span data-stu-id="9f31c-144">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="9f31c-145">此外，由於 Web 服務呼叫的要求/回應本質，以及每次呼叫 Web 服務時就會調整模型的事實，該項服務目前只能處理有限的資料大小。</span><span class="sxs-lookup"><span data-stu-id="9f31c-145">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="9f31c-146">常見問題集</span><span class="sxs-lookup"><span data-stu-id="9f31c-146">FAQ</span></span>
<span data-ttu-id="9f31c-147">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="9f31c-147">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

