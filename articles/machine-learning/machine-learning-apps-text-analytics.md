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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="a88b1-103">機器學習 API：情感文字分析、關鍵片語擷取、語言偵測及主題偵測</span><span class="sxs-lookup"><span data-stu-id="a88b1-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="a88b1-104">此指南適用於第 1 版的 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="a88b1-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="a88b1-105">第 2 版，如[ **toothis 文件，請參閱**](../cognitive-services/cognitive-services-text-analytics-quick-start.md)。</span><span class="sxs-lookup"><span data-stu-id="a88b1-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="a88b1-106">第 2 版現在是此 API hello 慣用的版本。</span><span class="sxs-lookup"><span data-stu-id="a88b1-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="a88b1-107">概觀</span><span class="sxs-lookup"><span data-stu-id="a88b1-107">Overview</span></span>
<span data-ttu-id="a88b1-108">hello 文字分析 API 是一套的文字分析[web 服務](https://datamarket.azure.com/dataset/amla/text-analytics)使用 Azure Machine Learning 建立。</span><span class="sxs-lookup"><span data-stu-id="a88b1-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="a88b1-109">hello 應用程式開發介面可以是使用的 tooanalyze 進行工作，例如情緒分析、 關鍵片語擷取、 語言偵測和主題偵測非結構化的文字。</span><span class="sxs-lookup"><span data-stu-id="a88b1-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="a88b1-110">沒有資料的定型所需 toouse 這個 API： 只將文字資料。</span><span class="sxs-lookup"><span data-stu-id="a88b1-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="a88b1-111">這個 API 會使用進階的自然語言處理技術 toodeliver 最佳預測。</span><span class="sxs-lookup"><span data-stu-id="a88b1-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="a88b1-112">您可以看到在動作中的文字分析上我們[示範網站](https://text-analytics-demo.azurewebsites.net/)，其中您也可以找到[範例](https://text-analytics-demo.azurewebsites.net/Home/SampleCode)如何在 C# 和 Python tooimplement 文字分析。</span><span class="sxs-lookup"><span data-stu-id="a88b1-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="a88b1-113">情感分析</span><span class="sxs-lookup"><span data-stu-id="a88b1-113">Sentiment analysis</span></span>
<span data-ttu-id="a88b1-114">hello API 傳回的數值分數 0 與 1 之間。</span><span class="sxs-lookup"><span data-stu-id="a88b1-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="a88b1-115">分數關閉 too1 表示正面的人氣，而分數關閉 too0 表示負數的人氣。</span><span class="sxs-lookup"><span data-stu-id="a88b1-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="a88b1-116">情感分數使用分類技術產生。</span><span class="sxs-lookup"><span data-stu-id="a88b1-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="a88b1-117">hello 的輸入的特徵 toohello 分類包含 n 字母組，從組件的語音標記和 word 內嵌產生的功能。</span><span class="sxs-lookup"><span data-stu-id="a88b1-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="a88b1-118">目前，英文是 hello 只支援的語言。</span><span class="sxs-lookup"><span data-stu-id="a88b1-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="a88b1-119">關鍵片語擷取</span><span class="sxs-lookup"><span data-stu-id="a88b1-119">Key phrase extraction</span></span>
<span data-ttu-id="a88b1-120">hello API 傳回此項表示應 hello 討論中的重點 hello 輸入文字的字串清單。</span><span class="sxs-lookup"><span data-stu-id="a88b1-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="a88b1-121">我們採用的技術來自 Microsoft Office 複雜的自然語言處理工具組。</span><span class="sxs-lookup"><span data-stu-id="a88b1-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="a88b1-122">目前，英文是 hello 只支援的語言。</span><span class="sxs-lookup"><span data-stu-id="a88b1-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="a88b1-123">語言偵測</span><span class="sxs-lookup"><span data-stu-id="a88b1-123">Language detection</span></span>
<span data-ttu-id="a88b1-124">hello API 傳回 hello 偵測到語言和數字的分數，介於 0 與 1 之間。</span><span class="sxs-lookup"><span data-stu-id="a88b1-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="a88b1-125">分數關閉 too1 表示 100%確定性 hello 識別語言為 true。</span><span class="sxs-lookup"><span data-stu-id="a88b1-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="a88b1-126">總共支援 120 種語言。</span><span class="sxs-lookup"><span data-stu-id="a88b1-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="a88b1-127">主題偵測</span><span class="sxs-lookup"><span data-stu-id="a88b1-127">Topic detection</span></span>
<span data-ttu-id="a88b1-128">這是新發行的 API 會傳回 hello 上偵測到的主題送出的文字記錄的清單。</span><span class="sxs-lookup"><span data-stu-id="a88b1-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="a88b1-129">主題是以關鍵片語識別，可以是一或多個相關文字。</span><span class="sxs-lookup"><span data-stu-id="a88b1-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="a88b1-130">這個 API 需要至少 100 文字記錄 toobe 提交，但整個數百是設計的 toodetect 主題 toothousands 的記錄。</span><span class="sxs-lookup"><span data-stu-id="a88b1-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="a88b1-131">請注意，每提交 1 筆文字記錄，此 API 就會以 1 筆交易計費。</span><span class="sxs-lookup"><span data-stu-id="a88b1-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="a88b1-132">hello 應用程式開發介面是設計的 toowork 適合短時，人們寫入文字，例如檢閱和使用者意見反應。</span><span class="sxs-lookup"><span data-stu-id="a88b1-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="a88b1-133">API 定義</span><span class="sxs-lookup"><span data-stu-id="a88b1-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="a88b1-134">headers</span><span class="sxs-lookup"><span data-stu-id="a88b1-134">Headers</span></span>
<span data-ttu-id="a88b1-135">請確定 hello 正確的標頭併入您的要求，應，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a88b1-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="a88b1-136">您可以從您的帳戶在 hello 來找到您的帳戶金鑰[Azure Datamarket](https://datamarket.azure.com/account/keys)。</span><span class="sxs-lookup"><span data-stu-id="a88b1-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="a88b1-137">請注意，目前只接受 JSON 做為輸入和輸出格式。</span><span class="sxs-lookup"><span data-stu-id="a88b1-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="a88b1-138">不支援 XML。</span><span class="sxs-lookup"><span data-stu-id="a88b1-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="a88b1-139">單一回應 API</span><span class="sxs-lookup"><span data-stu-id="a88b1-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="a88b1-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="a88b1-140">GetSentiment</span></span>
<span data-ttu-id="a88b1-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="a88b1-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="a88b1-142">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="a88b1-142">**Example request**</span></span>

<span data-ttu-id="a88b1-143">在下列呼叫 hello，我們正在要求 hello 片語"Hello World"情緒分析：</span><span class="sxs-lookup"><span data-stu-id="a88b1-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="a88b1-144">這會傳回如下的回應：</span><span class="sxs-lookup"><span data-stu-id="a88b1-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="a88b1-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="a88b1-145">GetKeyPhrases</span></span>
<span data-ttu-id="a88b1-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="a88b1-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="a88b1-147">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="a88b1-147">**Example request**</span></span>

<span data-ttu-id="a88b1-148">在下列呼叫 hello，我們正在要求 hello 關鍵片語 hello 在文字中找到 「 棒的旅館 toostay，與唯一裝潢及易記的人員 」:</span><span class="sxs-lookup"><span data-stu-id="a88b1-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="a88b1-149">這會傳回如下的回應：</span><span class="sxs-lookup"><span data-stu-id="a88b1-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="a88b1-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="a88b1-150">GetLanguage</span></span>
<span data-ttu-id="a88b1-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="a88b1-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="a88b1-152">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="a88b1-152">**Example request**</span></span>

<span data-ttu-id="a88b1-153">在 hello GET 呼叫下方，我們所要求的 hello 文字中的 hello 關鍵片語的 hello 人氣*Hello World*</span><span class="sxs-lookup"><span data-stu-id="a88b1-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="a88b1-154">這會傳回如下的回應：</span><span class="sxs-lookup"><span data-stu-id="a88b1-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="a88b1-155">**選擇性參數**</span><span class="sxs-lookup"><span data-stu-id="a88b1-155">**Optional parameters**</span></span>

<span data-ttu-id="a88b1-156">`NumberOfLanguagesToDetect` 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="a88b1-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="a88b1-157">hello 預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="a88b1-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="a88b1-158">Batch API</span><span class="sxs-lookup"><span data-stu-id="a88b1-158">Batch APIs</span></span>
<span data-ttu-id="a88b1-159">hello 文字分析服務可讓您 toodo 人氣與 key 片語擷取批次模式。</span><span class="sxs-lookup"><span data-stu-id="a88b1-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="a88b1-160">請注意每 hello 筆記錄當做一筆交易計分計數。</span><span class="sxs-lookup"><span data-stu-id="a88b1-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="a88b1-161">例如，如果您在單一呼叫中要求 1000 筆記錄的情緒，則會扣除 1000 個交易。</span><span class="sxs-lookup"><span data-stu-id="a88b1-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="a88b1-162">請注意，hello 識別碼輸入 hello 系統是 hello hello 系統所傳回的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a88b1-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="a88b1-163">hello web 服務不會檢查這些 Id 是唯一。</span><span class="sxs-lookup"><span data-stu-id="a88b1-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="a88b1-164">它負責 hello hello 呼叫端 tooverify 唯一性。</span><span class="sxs-lookup"><span data-stu-id="a88b1-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="a88b1-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="a88b1-165">GetSentimentBatch</span></span>
<span data-ttu-id="a88b1-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="a88b1-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="a88b1-167">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="a88b1-167">**Example request**</span></span>

<span data-ttu-id="a88b1-168">在 hello POST 呼叫下，我們會要求的 hello 片語"Hello World"、"Foo Hello World"和 hello hello 要求主體中的"Hello 我 World"hello sentiments:</span><span class="sxs-lookup"><span data-stu-id="a88b1-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="a88b1-169">要求本文：</span><span class="sxs-lookup"><span data-stu-id="a88b1-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="a88b1-170">在以下 hello 回應，您會取得 hello 清單的文字識別碼相關聯的分數：</span><span class="sxs-lookup"><span data-stu-id="a88b1-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="a88b1-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="a88b1-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="a88b1-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="a88b1-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="a88b1-173">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="a88b1-173">**Example request**</span></span>

<span data-ttu-id="a88b1-174">在此範例中，我們正在要求 sentiments hello hello 下列文字中的關鍵片語的 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="a88b1-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="a88b1-175">「 棒的旅館 toostay，與唯一裝潢及易記的人員 」</span><span class="sxs-lookup"><span data-stu-id="a88b1-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="a88b1-176">"It was an amazing build conference, with very interesting talks"</span><span class="sxs-lookup"><span data-stu-id="a88b1-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="a88b1-177">"hello 流量是恐怖，我花費三小時一次將 toohello 機場"</span><span class="sxs-lookup"><span data-stu-id="a88b1-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="a88b1-178">此要求是由為 POST 呼叫 toohello 端點：</span><span class="sxs-lookup"><span data-stu-id="a88b1-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="a88b1-179">要求本文：</span><span class="sxs-lookup"><span data-stu-id="a88b1-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="a88b1-180">以下回應 hello，取得與文字識別碼相關聯的主要片語的 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="a88b1-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="a88b1-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="a88b1-181">GetLanguageBatch</span></span>

<span data-ttu-id="a88b1-182">在 hello POST 呼叫下方，我們正在要求兩個文字輸入語言的偵測：</span><span class="sxs-lookup"><span data-stu-id="a88b1-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="a88b1-183">要求本文：</span><span class="sxs-lookup"><span data-stu-id="a88b1-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="a88b1-184">這會傳回下列回應，其中英文中偵測到的第一個輸入 hello 和法文 hello 第二個輸入中的 hello:</span><span class="sxs-lookup"><span data-stu-id="a88b1-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="a88b1-185">主題偵測 API</span><span class="sxs-lookup"><span data-stu-id="a88b1-185">Topic Detection APIs</span></span>
<span data-ttu-id="a88b1-186">這是新發行的 API 會傳回 hello 上偵測到的主題送出的文字記錄的清單。</span><span class="sxs-lookup"><span data-stu-id="a88b1-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="a88b1-187">主題是以關鍵片語識別，可以是一或多個相關文字。</span><span class="sxs-lookup"><span data-stu-id="a88b1-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="a88b1-188">請注意，每提交 1 筆文字記錄，此 API 就會以 1 筆交易計費。</span><span class="sxs-lookup"><span data-stu-id="a88b1-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="a88b1-189">這個 API 需要至少 100 文字記錄 toobe 提交，但整個數百是設計的 toodetect 主題 toothousands 的記錄。</span><span class="sxs-lookup"><span data-stu-id="a88b1-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="a88b1-190">主題 – 提交作業</span><span class="sxs-lookup"><span data-stu-id="a88b1-190">Topics – Submit job</span></span>
<span data-ttu-id="a88b1-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="a88b1-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="a88b1-192">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="a88b1-192">**Example request**</span></span>

<span data-ttu-id="a88b1-193">在 hello POST 呼叫下方，我們會要求 100 的發行項，其中 hello 第一次與上一次輸入文件，也會顯示，而兩個 StopPhrases 包含一組主題。</span><span class="sxs-lookup"><span data-stu-id="a88b1-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="a88b1-194">要求本文：</span><span class="sxs-lookup"><span data-stu-id="a88b1-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="a88b1-195">在以下的 hello 回應，除可獲得 hello JobId hello 送出的工作：</span><span class="sxs-lookup"><span data-stu-id="a88b1-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="a88b1-196">不應當做主題傳回的單字或多字片語的清單。</span><span class="sxs-lookup"><span data-stu-id="a88b1-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="a88b1-197">可以使用的 toofilter 出相當廣泛的主題。</span><span class="sxs-lookup"><span data-stu-id="a88b1-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="a88b1-198">例如，在飯店業評論的相關資料集中，"hotel" 和 "hostel" 可能是合理的停止片語。</span><span class="sxs-lookup"><span data-stu-id="a88b1-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="a88b1-199">主題 – 輪詢作業結果</span><span class="sxs-lookup"><span data-stu-id="a88b1-199">Topics – Poll for job results</span></span>
<span data-ttu-id="a88b1-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="a88b1-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="a88b1-201">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="a88b1-201">**Example request**</span></span>

<span data-ttu-id="a88b1-202">傳遞的 hello hello '送出工作' 步驟 toofetch hello 就會從傳回的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="a88b1-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="a88b1-203">我們建議您呼叫此端點每隔一分鐘，直到狀態 = hello 回應中的 「 完成 」。</span><span class="sxs-lookup"><span data-stu-id="a88b1-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="a88b1-204">這需要大約 10 分鐘，工作 toocomplete，或具有數千個記錄之作業更久。</span><span class="sxs-lookup"><span data-stu-id="a88b1-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="a88b1-205">當它正在處理時，hello 回應會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="a88b1-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="a88b1-206">hello API hello 遵循格式中的 JSON 格式傳回的輸出：</span><span class="sxs-lookup"><span data-stu-id="a88b1-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="a88b1-207">每個部分的 hello 回應 hello 屬性如下所示：</span><span class="sxs-lookup"><span data-stu-id="a88b1-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="a88b1-208">**TopicInfo 屬性**</span><span class="sxs-lookup"><span data-stu-id="a88b1-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="a88b1-209">金鑰</span><span class="sxs-lookup"><span data-stu-id="a88b1-209">Key</span></span> | <span data-ttu-id="a88b1-210">說明</span><span class="sxs-lookup"><span data-stu-id="a88b1-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a88b1-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="a88b1-211">TopicId</span></span> |<span data-ttu-id="a88b1-212">每個主題的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a88b1-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="a88b1-213">分數</span><span class="sxs-lookup"><span data-stu-id="a88b1-213">Score</span></span> |<span data-ttu-id="a88b1-214">記錄的計數會指派 tootopic。</span><span class="sxs-lookup"><span data-stu-id="a88b1-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="a88b1-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="a88b1-215">KeyPhrase</span></span> |<span data-ttu-id="a88b1-216">實體單字或片語 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="a88b1-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="a88b1-217">可以是 1 個字或多個字。</span><span class="sxs-lookup"><span data-stu-id="a88b1-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="a88b1-218">**TopicAssignment 屬性**</span><span class="sxs-lookup"><span data-stu-id="a88b1-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="a88b1-219">金鑰</span><span class="sxs-lookup"><span data-stu-id="a88b1-219">Key</span></span> | <span data-ttu-id="a88b1-220">說明</span><span class="sxs-lookup"><span data-stu-id="a88b1-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a88b1-221">識別碼</span><span class="sxs-lookup"><span data-stu-id="a88b1-221">Id</span></span> |<span data-ttu-id="a88b1-222">Hello 記錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a88b1-222">Identifier for hello record.</span></span> <span data-ttu-id="a88b1-223">相當於 toohello hello 輸入中包含的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a88b1-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="a88b1-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="a88b1-224">TopicId</span></span> |<span data-ttu-id="a88b1-225">已指派給哪個 hello 記錄 hello 主題識別碼。</span><span class="sxs-lookup"><span data-stu-id="a88b1-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="a88b1-226">Distance</span><span class="sxs-lookup"><span data-stu-id="a88b1-226">Distance</span></span> |<span data-ttu-id="a88b1-227">Hello 資料錄的信心所屬 toohello 主題。</span><span class="sxs-lookup"><span data-stu-id="a88b1-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="a88b1-228">距離近 toozero 表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="a88b1-228">Distance closer toozero indicates higher confidence.</span></span> |

