---
title: "機器學習 API：文字分析 | Microsoft Docs"
description: "Microsoft 的機器學習文字分析應用程式開發介面可以是使用的 tooanalyze 情緒分析、 關鍵片語擷取、 語言偵測和主題偵測非結構化的文字。"
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>機器學習 API：情感文字分析、關鍵片語擷取、語言偵測及主題偵測
> [!NOTE]
> 此指南適用於第 1 版的 hello 應用程式開發介面。 第 2 版，如[ **toothis 文件，請參閱**](../cognitive-services/cognitive-services-text-analytics-quick-start.md)。 第 2 版現在是此 API hello 慣用的版本。
> 
> 

## <a name="overview"></a>概觀
hello 文字分析 API 是一套的文字分析[web 服務](https://datamarket.azure.com/dataset/amla/text-analytics)使用 Azure Machine Learning 建立。 hello 應用程式開發介面可以是使用的 tooanalyze 進行工作，例如情緒分析、 關鍵片語擷取、 語言偵測和主題偵測非結構化的文字。 沒有資料的定型所需 toouse 這個 API： 只將文字資料。 這個 API 會使用進階的自然語言處理技術 toodeliver 最佳預測。

您可以看到在動作中的文字分析上我們[示範網站](https://text-analytics-demo.azurewebsites.net/)，其中您也可以找到[範例](https://text-analytics-demo.azurewebsites.net/Home/SampleCode)如何在 C# 和 Python tooimplement 文字分析。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>情感分析
hello API 傳回的數值分數 0 與 1 之間。 分數關閉 too1 表示正面的人氣，而分數關閉 too0 表示負數的人氣。 情感分數使用分類技術產生。 hello 的輸入的特徵 toohello 分類包含 n 字母組，從組件的語音標記和 word 內嵌產生的功能。 目前，英文是 hello 只支援的語言。

## <a name="key-phrase-extraction"></a>關鍵片語擷取
hello API 傳回此項表示應 hello 討論中的重點 hello 輸入文字的字串清單。 我們採用的技術來自 Microsoft Office 複雜的自然語言處理工具組。 目前，英文是 hello 只支援的語言。

## <a name="language-detection"></a>語言偵測
hello API 傳回 hello 偵測到語言和數字的分數，介於 0 與 1 之間。 分數關閉 too1 表示 100%確定性 hello 識別語言為 true。 總共支援 120 種語言。

## <a name="topic-detection"></a>主題偵測
這是新發行的 API 會傳回 hello 上偵測到的主題送出的文字記錄的清單。 主題是以關鍵片語識別，可以是一或多個相關文字。 這個 API 需要至少 100 文字記錄 toobe 提交，但整個數百是設計的 toodetect 主題 toothousands 的記錄。 請注意，每提交 1 筆文字記錄，此 API 就會以 1 筆交易計費。 hello 應用程式開發介面是設計的 toowork 適合短時，人們寫入文字，例如檢閱和使用者意見反應。

- - -
## <a name="api-definition"></a>API 定義
### <a name="headers"></a>headers
請確定 hello 正確的標頭併入您的要求，應，如下所示：

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

您可以從您的帳戶在 hello 來找到您的帳戶金鑰[Azure Datamarket](https://datamarket.azure.com/account/keys)。 請注意，目前只接受 JSON 做為輸入和輸出格式。 不支援 XML。

- - -
## <a name="single-response-apis"></a>單一回應 API
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**範例要求**

在下列呼叫 hello，我們正在要求 hello 片語"Hello World"情緒分析：

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

這會傳回如下的回應：

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**範例要求**

在下列呼叫 hello，我們正在要求 hello 關鍵片語 hello 在文字中找到 「 棒的旅館 toostay，與唯一裝潢及易記的人員 」:

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

這會傳回如下的回應：

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**範例要求**

在 hello GET 呼叫下方，我們所要求的 hello 文字中的 hello 關鍵片語的 hello 人氣*Hello World*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

這會傳回如下的回應：

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**選擇性參數**

`NumberOfLanguagesToDetect` 是選擇性參數。 hello 預設值為 1。

- - -
## <a name="batch-apis"></a>Batch API
hello 文字分析服務可讓您 toodo 人氣與 key 片語擷取批次模式。 請注意每 hello 筆記錄當做一筆交易計分計數。 例如，如果您在單一呼叫中要求 1000 筆記錄的情緒，則會扣除 1000 個交易。

請注意，hello 識別碼輸入 hello 系統是 hello hello 系統所傳回的識別碼。 hello web 服務不會檢查這些 Id 是唯一。 它負責 hello hello 呼叫端 tooverify 唯一性。 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**範例要求**

在 hello POST 呼叫下，我們會要求的 hello 片語"Hello World"、"Foo Hello World"和 hello hello 要求主體中的"Hello 我 World"hello sentiments:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

要求本文：

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

在以下 hello 回應，您會取得 hello 清單的文字識別碼相關聯的分數：

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**範例要求**

在此範例中，我們正在要求 sentiments hello hello 下列文字中的關鍵片語的 hello 清單： 

* 「 棒的旅館 toostay，與唯一裝潢及易記的人員 」
* "It was an amazing build conference, with very interesting talks"
* "hello 流量是恐怖，我花費三小時一次將 toohello 機場"

此要求是由為 POST 呼叫 toohello 端點：

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

要求本文：

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

以下回應 hello，取得與文字識別碼相關聯的主要片語的 hello 清單：

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a>GetLanguageBatch

在 hello POST 呼叫下方，我們正在要求兩個文字輸入語言的偵測：

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

要求本文：

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

這會傳回下列回應，其中英文中偵測到的第一個輸入 hello 和法文 hello 第二個輸入中的 hello:

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a>主題偵測 API
這是新發行的 API 會傳回 hello 上偵測到的主題送出的文字記錄的清單。 主題是以關鍵片語識別，可以是一或多個相關文字。 請注意，每提交 1 筆文字記錄，此 API 就會以 1 筆交易計費。

這個 API 需要至少 100 文字記錄 toobe 提交，但整個數百是設計的 toodetect 主題 toothousands 的記錄。

### <a name="topics--submit-job"></a>主題 – 提交作業
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**範例要求**

在 hello POST 呼叫下方，我們會要求 100 的發行項，其中 hello 第一次與上一次輸入文件，也會顯示，而兩個 StopPhrases 包含一組主題。

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

要求本文：

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

在以下的 hello 回應，除可獲得 hello JobId hello 送出的工作：

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

不應當做主題傳回的單字或多字片語的清單。 可以使用的 toofilter 出相當廣泛的主題。 例如，在飯店業評論的相關資料集中，"hotel" 和 "hostel" 可能是合理的停止片語。  

### <a name="topics--poll-for-job-results"></a>主題 – 輪詢作業結果
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**範例要求**

傳遞的 hello hello '送出工作' 步驟 toofetch hello 就會從傳回的作業識別碼。 我們建議您呼叫此端點每隔一分鐘，直到狀態 = hello 回應中的 「 完成 」。 這需要大約 10 分鐘，工作 toocomplete，或具有數千個記錄之作業更久。

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


當它正在處理時，hello 回應會顯示如下：

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


hello API hello 遵循格式中的 JSON 格式傳回的輸出：

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


每個部分的 hello 回應 hello 屬性如下所示：

**TopicInfo 屬性**

| 金鑰 | 說明 |
|:--- |:--- |
| TopicId |每個主題的唯一識別碼。 |
| 分數 |記錄的計數會指派 tootopic。 |
| KeyPhrase |實體單字或片語 hello 主題。 可以是 1 個字或多個字。 |

**TopicAssignment 屬性**

| 金鑰 | 說明 |
|:--- |:--- |
| 識別碼 |Hello 記錄的識別碼。 相當於 toohello hello 輸入中包含的識別碼。 |
| TopicId |已指派給哪個 hello 記錄 hello 主題識別碼。 |
| Distance |Hello 資料錄的信心所屬 toohello 主題。 距離近 toozero 表示較高信心。 |

