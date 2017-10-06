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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(已過時) 語彙型情感分析

> [!NOTE]
> 淘汰 hello Microsoft DataMarket 和這個 API 已被取代。 
> 
> 您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。 如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。

如何測量使用者在線上社交網路中 (例如 Facebook 文章、推文、評論等)，針對品牌或主題的意見和態度？ 情感分析提供分析這類問題的方法。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

情感分析通常有兩個方法。 其中一個使用監督式的學習演算法，和其他 hello 可被視為不受監督的學習。 監督式學習演算法通常會在大型註解主體上建置分類模型。 其正確性主要是根據 hello 註釋，hello 品質和 hello 定型程序通常需要一些時間。 除此之外，當我們套用 hello 演算法 tooanother 網域，hello 結果通常是不好。 比較 toosupervised 學習 」 中，以字典為基礎不受監督的學習使用人氣字典，不需要儲存大型資料主體和定型集可加快許多 hello 整個程序。 

我們[服務](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis)建置在 hello MPQA 主觀性 Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/)，也就是其中一個最常用的 hello 主觀性 lexicon 除外。 MPQA 中有 5,097 個否定字和 2,533 個肯定字。 而且所有這些字都會加上強極性或弱極性的註解。 hello 整個主體低於 GNU 通用公共授權。 hello web 服務可以套用的 tooany 簡短句子，例如推文和 Facebook 文章。 

> 使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。 但是 hello 目的 hello web 服務也是 tooserve 作為範例，Azure Machine Learning 可以列印文件的是，請使用的 toocreate 之上的 R 程式碼的 web 服務。 只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。 接著可以發行的 toohello Azure Marketplace 和跨使用者和裝置 hello world hello 作者 hello web 服務的任何基礎結構設定與 hello web 服務。
> 
> 

## <a name="consumption-of-web-service"></a>使用 Web 服務
hello 輸入的資料可以是任何文字，但 hello web 服務較適用於短的句子。 hello 輸出是介於-1 和 1 之間的數值。 任何超過 0 的值代表 hello 的 hello 文字的人氣為負數;正 0 以上。 hello 結果 hello 絕對值表示相關聯的 hello 人氣 hello 強度。 

> 這項服務，如 hello Azure Marketplace 上裝載是 OData 服務。無法呼叫透過 POST 或 GET 的方法。 
> 
> 

有多種方式來使用 hello 服務，以自動化方式 (範例應用程式是[這裡](http://microsoftazuremachinelearning.azurewebsites.net/))。

### <a name="starting-c-code-for-web-service-consumption"></a>啟動 Web 服務使用的 C# 程式碼：
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



hello 輸入是現今完全正確。 」 hello 輸出是"1"，這表示正面的人氣 hello 輸入句子與相關聯。 

## <a name="creation-of-web-service"></a>建立 Web 服務
> 這項 Web 服務是使用 Azure Machine Learning 所建立。 如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。 以下是 hello 實驗中的 hello 模組的每個建立 hello web 服務和範例程式碼的 hello 實驗的螢幕擷取畫面。
> 
> 

Azure Machine Learning 中已建立新的空白實驗， hello 下圖顯示以字典為基礎的舉動分析 hello 實驗流程。 hello"sent_dict.csv 」 檔案是 hello MPQA 主觀性詞典 」，並已設定為 hello 輸入的其中一種[執行 R 指令碼][execute-r-script]。 另一個輸入是從測試中，我們執行選取項目，修改資料行名稱，並分割作業的 hello Amazon 檢閱資料集取樣的檢閱。 我們使用雜湊封裝 toostore hello 主觀性 lexicon hello 記憶體中，以加速 hello 分數的計算程序。 將"tm 」 封裝會依 token hello 整個文字，並將其相較於 hello 人氣字典中的 hello 文字。 最後，分數會計算中的 hello 文字加入 hello 的主觀的每個單字的加權。 

### <a name="experiment-flow"></a>實驗流程：
![實驗流程][2]

#### <a name="module-1"></a>模組 1：
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>安裝雜湊套件
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



## <a name="limitations"></a>限制
演算法的觀點而言，以字典為基礎的舉動分析是一般人氣分析工具，而可能無法執行效能優於特定欄位的 hello 分類方法。 hello 否定問題也不處理使用。 我們在程式中硬式編碼了幾個否定字，但使用否定字典並建置一些規則會是更好的方法。 hello web 服務更好短而簡單的句子，例如推文和 Facebook 文章上比在長且複雜的句子，例如 Amazon 評論。 

## <a name="faq"></a>常見問題集
常見問題集 hello web 服務或發行 toohello Azure Marketplace 的耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


