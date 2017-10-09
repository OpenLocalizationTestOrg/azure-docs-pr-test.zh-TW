---
title: "aaa(deprecated) 多變量線性迴歸-Azure |Microsoft 文件"
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
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="bd295-103">(已過時) 多變量線性迴歸</span><span class="sxs-lookup"><span data-stu-id="bd295-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="bd295-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="bd295-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="bd295-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="bd295-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="bd295-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="bd295-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="bd295-107">假設您擁有的資料集就像 tooquickly 預測相依變數 (y) 根據獨立變數的每個個別 (i)。</span><span class="sxs-lookup"><span data-stu-id="bd295-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="bd295-108">線性迴歸是這類預測的常用統計技術。</span><span class="sxs-lookup"><span data-stu-id="bd295-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="bd295-109">這裡 hello 相依變數 y 假設 toobe 連續值。</span><span class="sxs-lookup"><span data-stu-id="bd295-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="bd295-110">簡單的案例可能是個人的 hello 研究者嘗試 toopredict hello 權數，其高度 (x) 為基礎 (y)。</span><span class="sxs-lookup"><span data-stu-id="bd295-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="bd295-111">Hello 研究者有 hello （例如 weight、 性別、 競爭） 個別的其他資訊的位置，並嘗試 toopredict hello 加權 hello 個別的可能是更進階的案例。</span><span class="sxs-lookup"><span data-stu-id="bd295-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="bd295-112">這[web 服務](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression)最適合 hello 線性迴歸模型 toohello 資料和輸出 hello hello 觀察 hello 資料中的每個預測的值 (y)。</span><span class="sxs-lookup"><span data-stu-id="bd295-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="bd295-113">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="bd295-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="bd295-114">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="bd295-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="bd295-115">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="bd295-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="bd295-116">接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="bd295-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="bd295-117">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="bd295-117">Consumption of web service</span></span>
<span data-ttu-id="bd295-118">此 web 服務可提供 hello 預測所有 hello 觀察 hello 獨立變數所都根據的 hello 相依變數的值。</span><span class="sxs-lookup"><span data-stu-id="bd295-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="bd295-119">hello web 服務預期 hello 終端使用者 tooinput 資料做為字串，其中會以逗號 （，） 分隔的資料列和資料行以分號 （;） 分隔。</span><span class="sxs-lookup"><span data-stu-id="bd295-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="bd295-120">hello web 服務需要 1 個資料列一次，並預期 hello 第一個資料行 toobe hello 相依變數。</span><span class="sxs-lookup"><span data-stu-id="bd295-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="bd295-121">範例資料集看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="bd295-121">An example dataset could look like this:</span></span>

![範例資料][1]

<span data-ttu-id="bd295-123">沒有相依變數的觀察應輸入 “NA” 做為 y。</span><span class="sxs-lookup"><span data-stu-id="bd295-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="bd295-124">hello 資料輸入資料集上方 hello 會 hello 遵循字串:"10 5; 2,18，則為 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12，則為 2; 1，NA、 3、 4"。</span><span class="sxs-lookup"><span data-stu-id="bd295-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="bd295-125">hello 輸出 hello hello 資料列的每個預測的值根據 hello 獨立變數。</span><span class="sxs-lookup"><span data-stu-id="bd295-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="bd295-126">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="bd295-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="bd295-127">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx))。</span><span class="sxs-lookup"><span data-stu-id="bd295-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="bd295-128">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="bd295-128">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="bd295-129">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="bd295-129">Creation of web service</span></span>
> <span data-ttu-id="bd295-130">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="bd295-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="bd295-131">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="bd295-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="bd295-132">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="bd295-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="bd295-133">在 Azure Machine Learning 中，新的空白實驗建立的來源和兩個[執行 R 指令碼][ execute-r-script]模組提取到 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="bd295-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="bd295-134">這項 Web 服務使用基礎 R 指令碼來執行 Azure Machine Learning 實驗。</span><span class="sxs-lookup"><span data-stu-id="bd295-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="bd295-135">有 2 組件 toothis 試驗： 結構描述定義，以及定型模型 + 計分。</span><span class="sxs-lookup"><span data-stu-id="bd295-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="bd295-136">hello 第一個模組定義 hello 預期結構 hello 輸入資料集，其中 hello 第一個變數是 hello 相依變數，而其餘的 hello 變數無關。</span><span class="sxs-lookup"><span data-stu-id="bd295-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="bd295-137">hello 第二個模組非常適合 hello 輸入資料的一般的線性迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="bd295-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![實驗流程][3]

#### <a name="module-1"></a><span data-ttu-id="bd295-139">模組 1：</span><span class="sxs-lookup"><span data-stu-id="bd295-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="bd295-140">結構描述定義</span><span class="sxs-lookup"><span data-stu-id="bd295-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="bd295-141">模組 2：</span><span class="sxs-lookup"><span data-stu-id="bd295-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="bd295-142">LM 模型</span><span class="sxs-lookup"><span data-stu-id="bd295-142">LM modeling</span></span>
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

## <a name="limitations"></a><span data-ttu-id="bd295-143">限制</span><span class="sxs-lookup"><span data-stu-id="bd295-143">Limitations</span></span>
<span data-ttu-id="bd295-144">這是一個非常簡單的多元線性迴歸 Web 服務案例。</span><span class="sxs-lookup"><span data-stu-id="bd295-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="bd295-145">可以從上述的 hello 範例程式碼看出，實作沒有錯誤攔截和 hello 服務承擔一切都是連續的變數 （沒有類別功能允許），當做 hello 服務只有輸入數字值時的這個 web 的 hello 建立 hello服務。</span><span class="sxs-lookup"><span data-stu-id="bd295-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="bd295-146">此外，hello 服務目前會處理有限的資料大小，因為 toohello 要求/回應性質 hello web 服務呼叫和 hello hello 模型的事實所適合每次呼叫 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="bd295-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="bd295-147">常見問題集</span><span class="sxs-lookup"><span data-stu-id="bd295-147">FAQ</span></span>
<span data-ttu-id="bd295-148">常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="bd295-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

