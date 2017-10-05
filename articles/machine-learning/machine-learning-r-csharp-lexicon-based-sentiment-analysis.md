---
title: "(已過時) 語彙型情感分析 - Azure | Microsoft Docs"
description: "(已過時) 語彙型情感分析"
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 7bc80a1e1067296528eca1a843ea30b0c27af616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="2fc6a-103">(已過時) 語彙型情感分析</span><span class="sxs-lookup"><span data-stu-id="2fc6a-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="2fc6a-104">Microsoft DataMarket 已進入淘汰階段，而此 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="2fc6a-105">您可以在 [Cortana Intelligence 資源庫 (英文)](http://gallery.cortanaintelligence.com) 中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="2fc6a-106">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="2fc6a-107">如何測量使用者在線上社交網路中 (例如 Facebook 文章、推文、評論等)，針對品牌或主題的意見和態度？</span><span class="sxs-lookup"><span data-stu-id="2fc6a-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="2fc6a-108">情感分析提供分析這類問題的方法。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2fc6a-109">情感分析通常有兩個方法。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="2fc6a-110">其中一個方法使用監督式學習演算法，而另一個方法可視為非監督式學習。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-110">One is using a supervised learning algorithm, and the other can be treated as unsupervised learning.</span></span> <span data-ttu-id="2fc6a-111">監督式學習演算法通常會在大型註解主體上建置分類模型。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="2fc6a-112">其精確度主要會視註解的品質而定，且定型程序通常需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-112">Its accuracy is mainly based on the quality of the annotation, and usually the training process will take a long time.</span></span> <span data-ttu-id="2fc6a-113">除此之外，當我們將演算法套用到另一個網域時，效果通常不是很好。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-113">Besides that, when we apply the algorithm to another domain, the result is usually not good.</span></span> <span data-ttu-id="2fc6a-114">相較於監督式學習，語彙型非監督式學習使用情感字典，由於不需要儲存大型資料主體和定型，因此可加快整個程序的速度。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-114">Compared to supervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes the whole process much faster.</span></span> 

<span data-ttu-id="2fc6a-115">我們的[服務](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis)以 MPQA 主觀性詞典 (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/) 為建置基礎，這是最常用的主觀性詞典之一。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on the MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of the most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="2fc6a-116">MPQA 中有 5,097 個否定字和 2,533 個肯定字。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="2fc6a-117">而且所有這些字都會加上強極性或弱極性的註解。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="2fc6a-118">整個主體會位於 [GNU 通用公共授權] 下方。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-118">The whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="2fc6a-119">Web 服務可以套用至任何簡短的句子，例如推文和 Facebook 文章。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-119">The web service can be applied to any short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="2fc6a-120">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="2fc6a-121">不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-121">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="2fc6a-122">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="2fc6a-123">接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-123">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="2fc6a-124">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2fc6a-124">Consumption of web service</span></span>
<span data-ttu-id="2fc6a-125">輸入資料可以是任何文字，但 Web 服務最適合用在簡短的句子。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-125">The input data can be any text, but the web service works better with short sentences.</span></span> <span data-ttu-id="2fc6a-126">輸出可以是 -1 和 1 之間的數值。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-126">The output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="2fc6a-127">任何小於 0 的值表示文字的情感是負面的；如果大於 0，則表示情感是正面的。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-127">Any value below 0 denotes that the sentiment of the text is negative; positive if above 0.</span></span> <span data-ttu-id="2fc6a-128">結果的絕對值表示相關聯情感的強度。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-128">The absolute value of the result denotes the strength of the associated sentiment.</span></span> 

> <span data-ttu-id="2fc6a-129">在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="2fc6a-130">以自動化方式取用服務的方法有很多種 ([這裡](http://microsoftazuremachinelearning.azurewebsites.net/)提供一個範例應用程式)。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="2fc6a-131">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="2fc6a-131">Starting C# code for web service consumption:</span></span>
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



<span data-ttu-id="2fc6a-132">輸入是「今天是美好的一天」。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-132">The input is “Today is a good day.”</span></span> <span data-ttu-id="2fc6a-133">輸出是 "1"，表示與輸入句子相關聯的正面情感。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-133">The output is “1”, which indicates a positive sentiment associated with the input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="2fc6a-134">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2fc6a-134">Creation of web service</span></span>
> <span data-ttu-id="2fc6a-135">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="2fc6a-136">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="2fc6a-137">以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-137">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="2fc6a-138">Azure Machine Learning 中已建立新的空白實驗。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="2fc6a-139">下圖說明語彙型情感分析的實驗流程。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-139">The figure below shows the experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="2fc6a-140">“sent_dict.csv” 檔案是 MPQA 主觀性詞典，已設定為[執行 R 指令碼][execute-r-script]的其中一個輸入。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-140">The “sent_dict.csv” file is the MPQA subjectivity lexicon, and is set as one of the inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="2fc6a-141">另一個輸入是來自 Amazon 評論測試資料集的取樣評論，我們在這個資料集中執行範圍選取、資料行名稱修改和分割作業。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-141">Another input is a sampled review from the Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="2fc6a-142">我們使用雜湊封裝將主觀性詞典儲存在記憶體中，以加快計分程序的速度。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-142">We use a hash package to store the subjectivity lexicon in the memory and accelerate the score computation process.</span></span> <span data-ttu-id="2fc6a-143">“tm” 封裝會將整個文字語彙基元化，並與情感字典中的單字進行比較。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-143">The whole text will be tokenized by “tm” package and compared with the word in the sentiment dictionary.</span></span> <span data-ttu-id="2fc6a-144">最後，分數的計算方式是在文字中加上每個主觀字的加權。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-144">Finally, a score will be calculated by adding the weight of each subjective word in the text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="2fc6a-145">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="2fc6a-145">Experiment flow:</span></span>
![實驗流程][2]

#### <a name="module-1"></a><span data-ttu-id="2fc6a-147">模組 1：</span><span class="sxs-lookup"><span data-stu-id="2fc6a-147">Module 1:</span></span>
    # Map 1-based optional input ports to variables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="2fc6a-148">安裝雜湊套件</span><span class="sxs-lookup"><span data-stu-id="2fc6a-148">Install hash package</span></span>
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="2fc6a-149">限制</span><span class="sxs-lookup"><span data-stu-id="2fc6a-149">Limitations</span></span>
<span data-ttu-id="2fc6a-150">從演算法的觀點來看，語彙型情感分析是一般情感分析工具，在某些領域中，這項工具的執行效果可能沒有分類方法來得出色。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than the classification method for specific fields.</span></span> <span data-ttu-id="2fc6a-151">否定問題不是很好處理。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-151">The negation problem is not well dealt with.</span></span> <span data-ttu-id="2fc6a-152">我們在程式中硬式編碼了幾個否定字，但使用否定字典並建置一些規則會是更好的方法。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="2fc6a-153">相較於又長又複雜的句子 (例如 Amazon 評論)，在簡短的句子 (例如推文和 Facebook 文章) 上執行 Web 服務會有較佳的效果。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-153">The web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="2fc6a-154">常見問題集</span><span class="sxs-lookup"><span data-stu-id="2fc6a-154">FAQ</span></span>
<span data-ttu-id="2fc6a-155">如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="2fc6a-155">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


