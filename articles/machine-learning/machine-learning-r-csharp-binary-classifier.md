---
title: "aaa(deprecated) 二元分類器-Azure |Microsoft 文件"
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
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="3434c-103">(已過時) 二元分類器</span><span class="sxs-lookup"><span data-stu-id="3434c-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="3434c-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="3434c-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="3434c-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="3434c-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3434c-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="3434c-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="3434c-107">假設您擁有的資料集，並希望 toopredict hello 獨立變數所根據的二進位相依變數。</span><span class="sxs-lookup"><span data-stu-id="3434c-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="3434c-108">「羅吉斯迴歸」是適用於此類預測的普遍統計技術。</span><span class="sxs-lookup"><span data-stu-id="3434c-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="3434c-109">這裡 hello 相依變數是二進位或二分，而 p hello 與否 hello 特性感興趣的機率。</span><span class="sxs-lookup"><span data-stu-id="3434c-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="3434c-110">簡單的案例可能是其中研究人員正嘗試 toopredict 潛在學生是否可能 tooaccept 根據的資訊 （GPA 高中、 家庭收入、 內建的狀態，性別） 許可提供 tooa 大學。</span><span class="sxs-lookup"><span data-stu-id="3434c-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="3434c-111">hello 預測的結果都接受 hello 許可提供 hello 潛在學生 hello 可能性。</span><span class="sxs-lookup"><span data-stu-id="3434c-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="3434c-112">這[web 服務](https://datamarket.azure.com/dataset/aml_labs/log_regression)最適合 hello 羅吉斯迴歸模型 toohello 資料和輸出 hello hello 觀察 hello 資料中的每個機率值 (y)。</span><span class="sxs-lookup"><span data-stu-id="3434c-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="3434c-113">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="3434c-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="3434c-114">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="3434c-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="3434c-115">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="3434c-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="3434c-116">接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="3434c-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="3434c-117">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="3434c-117">Consumption of web service</span></span>
<span data-ttu-id="3434c-118">此 web 服務可提供 hello 預測所有 hello 觀察 hello 獨立變數所都根據的 hello 相依變數的值。</span><span class="sxs-lookup"><span data-stu-id="3434c-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="3434c-119">hello web 服務預期 hello 終端使用者 tooinput 資料做為字串，其中資料列會以逗號 （，） 分隔，並以分號 （;） 分隔資料行。</span><span class="sxs-lookup"><span data-stu-id="3434c-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="3434c-120">hello web 服務需要 1 個資料列一次，並預期 hello 第一個資料行 toobe hello 相依變數。</span><span class="sxs-lookup"><span data-stu-id="3434c-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="3434c-121">範例資料集看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="3434c-121">An example dataset could look like this:</span></span>

![範例資料][1]

<span data-ttu-id="3434c-123">沒有相依變數的觀察應輸入 “NA” 做為 y。</span><span class="sxs-lookup"><span data-stu-id="3434c-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="3434c-124">hello 資料輸入資料集上方 hello 會 hello 遵循字串:"1; 5; 2,1; 1; 6，0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2，則為 1，NA; 3; 4"。</span><span class="sxs-lookup"><span data-stu-id="3434c-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="3434c-125">hello 輸出 hello hello 資料列的每個預測的值根據 hello 獨立變數。</span><span class="sxs-lookup"><span data-stu-id="3434c-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="3434c-126">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="3434c-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="3434c-127">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx))。</span><span class="sxs-lookup"><span data-stu-id="3434c-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="3434c-128">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="3434c-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="3434c-129">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="3434c-129">Creation of web service</span></span>
> <span data-ttu-id="3434c-130">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="3434c-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="3434c-131">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="3434c-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="3434c-132">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="3434c-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="3434c-133">在 Azure Machine Learning 中，新的空白實驗建立的來源和兩個[執行 R 指令碼][ execute-r-script]模組提取到 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="3434c-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="3434c-134">這項 Web 服務使用基礎 R 指令碼來執行 Azure Machine Learning 實驗。</span><span class="sxs-lookup"><span data-stu-id="3434c-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="3434c-135">有 2 組件 toothis 試驗： 結構描述定義，以及定型模型 + 計分。</span><span class="sxs-lookup"><span data-stu-id="3434c-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="3434c-136">hello 第一個模組定義 hello 預期結構 hello 輸入資料集，其中 hello 第一個變數是 hello 相依變數，而其餘的 hello 變數無關。</span><span class="sxs-lookup"><span data-stu-id="3434c-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="3434c-137">hello 第二個模組非常適合 hello 輸入資料的一般羅吉斯迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="3434c-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![實驗流程][2]

#### <a name="module-1"></a><span data-ttu-id="3434c-139">模組 1：</span><span class="sxs-lookup"><span data-stu-id="3434c-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="3434c-140">模組 2：</span><span class="sxs-lookup"><span data-stu-id="3434c-140">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="3434c-141">限制</span><span class="sxs-lookup"><span data-stu-id="3434c-141">Limitations</span></span>
<span data-ttu-id="3434c-142">這是一個非常簡單的二元分類 Web 服務範例。</span><span class="sxs-lookup"><span data-stu-id="3434c-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="3434c-143">可以從上述的 hello 範例程式碼看出，實作沒有錯誤攔截和 hello 服務承擔一切都是連續的二進位檔/變數 （沒有類別功能允許），當做 hello 服務只有輸入數字值時的 hello 建立 helloweb 服務。</span><span class="sxs-lookup"><span data-stu-id="3434c-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="3434c-144">此外，hello 服務目前會處理有限的資料大小，因為 toohello 要求/回應性質 hello web 服務呼叫和 hello hello 模型的事實所適合每次呼叫 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="3434c-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="3434c-145">常見問題集</span><span class="sxs-lookup"><span data-stu-id="3434c-145">FAQ</span></span>
<span data-ttu-id="3434c-146">常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="3434c-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

