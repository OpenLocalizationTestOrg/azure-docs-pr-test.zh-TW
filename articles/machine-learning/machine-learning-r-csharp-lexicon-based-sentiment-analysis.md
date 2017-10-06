---
title: "aaa(deprecated) Lexicon 基礎情緒分析-Azure |Microsoft 文件"
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
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="fed86-103">(已過時) 語彙型情感分析</span><span class="sxs-lookup"><span data-stu-id="fed86-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="fed86-104">淘汰 hello Microsoft DataMarket 和這個 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="fed86-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="fed86-105">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="fed86-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="fed86-106">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="fed86-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="fed86-107">如何測量使用者在線上社交網路中 (例如 Facebook 文章、推文、評論等)，針對品牌或主題的意見和態度？</span><span class="sxs-lookup"><span data-stu-id="fed86-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="fed86-108">情感分析提供分析這類問題的方法。</span><span class="sxs-lookup"><span data-stu-id="fed86-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="fed86-109">情感分析通常有兩個方法。</span><span class="sxs-lookup"><span data-stu-id="fed86-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="fed86-110">其中一個使用監督式的學習演算法，和其他 hello 可被視為不受監督的學習。</span><span class="sxs-lookup"><span data-stu-id="fed86-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="fed86-111">監督式學習演算法通常會在大型註解主體上建置分類模型。</span><span class="sxs-lookup"><span data-stu-id="fed86-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="fed86-112">其正確性主要是根據 hello 註釋，hello 品質和 hello 定型程序通常需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="fed86-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="fed86-113">除此之外，當我們套用 hello 演算法 tooanother 網域，hello 結果通常是不好。</span><span class="sxs-lookup"><span data-stu-id="fed86-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="fed86-114">比較 toosupervised 學習 」 中，以字典為基礎不受監督的學習使用人氣字典，不需要儲存大型資料主體和定型集可加快許多 hello 整個程序。</span><span class="sxs-lookup"><span data-stu-id="fed86-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="fed86-115">我們[服務](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis)建置在 hello MPQA 主觀性 Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/)，也就是其中一個最常用的 hello 主觀性 lexicon 除外。</span><span class="sxs-lookup"><span data-stu-id="fed86-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="fed86-116">MPQA 中有 5,097 個否定字和 2,533 個肯定字。</span><span class="sxs-lookup"><span data-stu-id="fed86-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="fed86-117">而且所有這些字都會加上強極性或弱極性的註解。</span><span class="sxs-lookup"><span data-stu-id="fed86-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="fed86-118">hello 整個主體低於 GNU 通用公共授權。</span><span class="sxs-lookup"><span data-stu-id="fed86-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="fed86-119">hello web 服務可以套用的 tooany 簡短句子，例如推文和 Facebook 文章。</span><span class="sxs-lookup"><span data-stu-id="fed86-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="fed86-120">使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fed86-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="fed86-121">但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="fed86-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="fed86-122">只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="fed86-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="fed86-123">接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="fed86-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="fed86-124">使用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="fed86-124">Consumption of web service</span></span>
<span data-ttu-id="fed86-125">hello 輸入的資料可以是任何文字，但 hello web 服務較適用於短的句子。</span><span class="sxs-lookup"><span data-stu-id="fed86-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="fed86-126">hello 輸出是介於-1 和 1 之間的數值。</span><span class="sxs-lookup"><span data-stu-id="fed86-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="fed86-127">任何超過 0 的值代表 hello 的 hello 文字的人氣為負數;正 0 以上。</span><span class="sxs-lookup"><span data-stu-id="fed86-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="fed86-128">hello 結果 hello 絕對值表示相關聯的 hello 人氣 hello 強度。</span><span class="sxs-lookup"><span data-stu-id="fed86-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="fed86-129">這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。</span><span class="sxs-lookup"><span data-stu-id="fed86-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="fed86-130">有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/))。</span><span class="sxs-lookup"><span data-stu-id="fed86-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="fed86-131">啟動 Web 服務使用的 C# 程式碼：</span><span class="sxs-lookup"><span data-stu-id="fed86-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="fed86-132">hello 輸入是現今完全正確。 」</span><span class="sxs-lookup"><span data-stu-id="fed86-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="fed86-133">hello 輸出是"1"，這表示正面的人氣 hello 輸入句子與相關聯。</span><span class="sxs-lookup"><span data-stu-id="fed86-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="fed86-134">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="fed86-134">Creation of web service</span></span>
> <span data-ttu-id="fed86-135">這項 Web 服務是使用 Azure Machine Learning 所建立。</span><span class="sxs-lookup"><span data-stu-id="fed86-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="fed86-136">如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。</span><span class="sxs-lookup"><span data-stu-id="fed86-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="fed86-137">以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="fed86-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="fed86-138">Azure Machine Learning 中已建立新的空白實驗，</span><span class="sxs-lookup"><span data-stu-id="fed86-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="fed86-139">hello 下圖顯示以字典為基礎的舉動分析 hello 實驗流程。</span><span class="sxs-lookup"><span data-stu-id="fed86-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="fed86-140">hello"sent_dict.csv 」 檔案是 hello MPQA 主觀性詞典 」，並已設定為 hello 輸入的其中一種[執行 R 指令碼][execute-r-script]。</span><span class="sxs-lookup"><span data-stu-id="fed86-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="fed86-141">另一個輸入是從測試中，我們執行選取項目，修改資料行名稱，並分割作業的 hello Amazon 檢閱資料集取樣的檢閱。</span><span class="sxs-lookup"><span data-stu-id="fed86-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="fed86-142">我們使用雜湊封裝 toostore hello 主觀性 lexicon hello 記憶體中，以加速 hello 分數的計算程序。</span><span class="sxs-lookup"><span data-stu-id="fed86-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="fed86-143">將"tm 」 封裝會依 token hello 整個文字，並將其相較於 hello 人氣字典中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="fed86-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="fed86-144">最後，分數會計算中的 hello 文字加入 hello 的主觀的每個單字的加權。</span><span class="sxs-lookup"><span data-stu-id="fed86-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="fed86-145">實驗流程：</span><span class="sxs-lookup"><span data-stu-id="fed86-145">Experiment flow:</span></span>
![實驗流程][2]

#### <a name="module-1"></a><span data-ttu-id="fed86-147">模組 1：</span><span class="sxs-lookup"><span data-stu-id="fed86-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="fed86-148">安裝雜湊套件</span><span class="sxs-lookup"><span data-stu-id="fed86-148">Install hash package</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a><span data-ttu-id="fed86-149">限制</span><span class="sxs-lookup"><span data-stu-id="fed86-149">Limitations</span></span>
<span data-ttu-id="fed86-150">演算法的觀點而言，以字典為基礎的舉動分析是一般人氣分析工具，而可能無法執行效能優於特定欄位的 hello 分類方法。</span><span class="sxs-lookup"><span data-stu-id="fed86-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="fed86-151">hello 否定問題也不處理使用。</span><span class="sxs-lookup"><span data-stu-id="fed86-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="fed86-152">我們在程式中硬式編碼了幾個否定字，但使用否定字典並建置一些規則會是更好的方法。</span><span class="sxs-lookup"><span data-stu-id="fed86-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="fed86-153">hello web 服務更好短而簡單的句子，例如推文和 Facebook 文章上比在長且複雜的句子，例如 Amazon 評論。</span><span class="sxs-lookup"><span data-stu-id="fed86-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="fed86-154">常見問題集</span><span class="sxs-lookup"><span data-stu-id="fed86-154">FAQ</span></span>
<span data-ttu-id="fed86-155">常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="fed86-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


