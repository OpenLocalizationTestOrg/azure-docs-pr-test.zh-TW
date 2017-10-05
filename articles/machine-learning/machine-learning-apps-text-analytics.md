---
title: "機器學習 API：文字分析 | Microsoft Docs"
description: "Microsoft 的機器學習文字分析 API 可用來分析非結構化文字，例如情感分析、關鍵片語擷取、語言偵測及主題偵測。"
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
redirect_document_id: TRUE
ms.openlocfilehash: 10eae2ff5624dcb57de1cf72b326147f35bc2a0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="b627f-103">機器學習 API：情感文字分析、關鍵片語擷取、語言偵測及主題偵測</span><span class="sxs-lookup"><span data-stu-id="b627f-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="b627f-104">本指南適用於第 1 版的 API。</span><span class="sxs-lookup"><span data-stu-id="b627f-104">This guide is for version 1 of the API.</span></span> <span data-ttu-id="b627f-105">關於第 2 版，[**請參閱本文件**](../cognitive-services/cognitive-services-text-analytics-quick-start.md)。</span><span class="sxs-lookup"><span data-stu-id="b627f-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="b627f-106">現在建議使用此 API 的第 2 版。</span><span class="sxs-lookup"><span data-stu-id="b627f-106">Version 2 is now the preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="b627f-107">Overview</span><span class="sxs-lookup"><span data-stu-id="b627f-107">Overview</span></span>
<span data-ttu-id="b627f-108">文字分析 API 是一套以 Azure Machine Learning 服務建置的文字分析 [Web 服務](https://datamarket.azure.com/dataset/amla/text-analytics) 。</span><span class="sxs-lookup"><span data-stu-id="b627f-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="b627f-109">此 API 可用來分析工作的非結構化文字，例如情感分析、關鍵片語擷取、語言偵測及主題偵測。</span><span class="sxs-lookup"><span data-stu-id="b627f-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="b627f-110">使用此 API 不需要任何訓練資料，只要將文字資料帶入即可。</span><span class="sxs-lookup"><span data-stu-id="b627f-110">No training data is needed to use this API: just bring your text data.</span></span> <span data-ttu-id="b627f-111">此 API 使用進階的自然語言處理技術來提供最佳預測。</span><span class="sxs-lookup"><span data-stu-id="b627f-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span></span>

<span data-ttu-id="b627f-112">您可以在我們的[示範網站](https://text-analytics-demo.azurewebsites.net/)看到文字分析的運作，其中您也可以找到如何以 C# 和 Python 實作文字分析的[範例](https://text-analytics-demo.azurewebsites.net/Home/SampleCode)。</span><span class="sxs-lookup"><span data-stu-id="b627f-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="b627f-113">情感分析</span><span class="sxs-lookup"><span data-stu-id="b627f-113">Sentiment analysis</span></span>
<span data-ttu-id="b627f-114">API 會傳回一個 0 到 1 之間的分數。</span><span class="sxs-lookup"><span data-stu-id="b627f-114">The API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="b627f-115">接近 1 的分數表示正面的情感，而接近 0 的分數則表示負面的情感。</span><span class="sxs-lookup"><span data-stu-id="b627f-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="b627f-116">情感分數使用分類技術產生。</span><span class="sxs-lookup"><span data-stu-id="b627f-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="b627f-117">輸入分類器的特徵包括 n-grams、從 part-of-speech 標記產生的特徵以及字詞內嵌。</span><span class="sxs-lookup"><span data-stu-id="b627f-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="b627f-118">目前，英文是唯一支援的語言。</span><span class="sxs-lookup"><span data-stu-id="b627f-118">Currently, English is the only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="b627f-119">關鍵片語擷取</span><span class="sxs-lookup"><span data-stu-id="b627f-119">Key phrase extraction</span></span>
<span data-ttu-id="b627f-120">API 會傳回輸入文字中代表說話重點的字串清單。</span><span class="sxs-lookup"><span data-stu-id="b627f-120">The API returns a list of strings denoting the key talking points in the input text.</span></span> <span data-ttu-id="b627f-121">我們採用的技術來自 Microsoft Office 複雜的自然語言處理工具組。</span><span class="sxs-lookup"><span data-stu-id="b627f-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="b627f-122">目前，英文是唯一支援的語言。</span><span class="sxs-lookup"><span data-stu-id="b627f-122">Currently, English is the only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="b627f-123">語言偵測</span><span class="sxs-lookup"><span data-stu-id="b627f-123">Language detection</span></span>
<span data-ttu-id="b627f-124">此 API 會傳回偵測到的語言和 0 到 1 之間的分數。</span><span class="sxs-lookup"><span data-stu-id="b627f-124">The API returns the detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="b627f-125">接近 1 的分數表示 100% 確定已識別的語言為真實。</span><span class="sxs-lookup"><span data-stu-id="b627f-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span></span> <span data-ttu-id="b627f-126">總共支援 120 種語言。</span><span class="sxs-lookup"><span data-stu-id="b627f-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="b627f-127">主題偵測</span><span class="sxs-lookup"><span data-stu-id="b627f-127">Topic detection</span></span>
<span data-ttu-id="b627f-128">這是新發行的 API，可針對已提交的文字記錄清單傳回前幾個偵測到的主題。</span><span class="sxs-lookup"><span data-stu-id="b627f-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="b627f-129">主題是以關鍵片語識別，可以是一或多個相關文字。</span><span class="sxs-lookup"><span data-stu-id="b627f-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="b627f-130">這個 API 至少需要提交 100 筆文字記錄，但其設計可偵測數百至數千筆記錄的主題。</span><span class="sxs-lookup"><span data-stu-id="b627f-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="b627f-131">請注意，每提交 1 筆文字記錄，此 API 就會以 1 筆交易計費。</span><span class="sxs-lookup"><span data-stu-id="b627f-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="b627f-132">此 API 的設計適用於簡短的人工書寫文字，例如評論和使用者意見反應。</span><span class="sxs-lookup"><span data-stu-id="b627f-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="b627f-133">API 定義</span><span class="sxs-lookup"><span data-stu-id="b627f-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="b627f-134">標頭</span><span class="sxs-lookup"><span data-stu-id="b627f-134">Headers</span></span>
<span data-ttu-id="b627f-135">請確定要求中包含正確的標頭，應該如下：</span><span class="sxs-lookup"><span data-stu-id="b627f-135">Ensure that you include the correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="b627f-136">您可以在 [Azure 資料市場](https://datamarket.azure.com/account/keys)中找到您帳戶中的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b627f-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="b627f-137">請注意，目前只接受 JSON 做為輸入和輸出格式。</span><span class="sxs-lookup"><span data-stu-id="b627f-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="b627f-138">不支援 XML。</span><span class="sxs-lookup"><span data-stu-id="b627f-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="b627f-139">單一回應 API</span><span class="sxs-lookup"><span data-stu-id="b627f-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="b627f-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="b627f-140">GetSentiment</span></span>
<span data-ttu-id="b627f-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="b627f-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="b627f-142">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="b627f-142">**Example request**</span></span>

<span data-ttu-id="b627f-143">在下面的呼叫中，我們要求片語 "Hello World" 的情緒分析：</span><span class="sxs-lookup"><span data-stu-id="b627f-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="b627f-144">這會傳回如下的回應：</span><span class="sxs-lookup"><span data-stu-id="b627f-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="b627f-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="b627f-145">GetKeyPhrases</span></span>
<span data-ttu-id="b627f-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="b627f-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="b627f-147">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="b627f-147">**Example request**</span></span>

<span data-ttu-id="b627f-148">在下面的呼叫中，我們要求 "It was a wonderful hotel to stay at, with unique decor and friendly staff" 這段文字中找到的關鍵片語：</span><span class="sxs-lookup"><span data-stu-id="b627f-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="b627f-149">這會傳回如下的回應：</span><span class="sxs-lookup"><span data-stu-id="b627f-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="b627f-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="b627f-150">GetLanguage</span></span>
<span data-ttu-id="b627f-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="b627f-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="b627f-152">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="b627f-152">**Example request**</span></span>

<span data-ttu-id="b627f-153">在下面的 GET 呼叫中，我們要求 *Hello World*</span><span class="sxs-lookup"><span data-stu-id="b627f-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="b627f-154">這會傳回如下的回應：</span><span class="sxs-lookup"><span data-stu-id="b627f-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="b627f-155">**選擇性參數**</span><span class="sxs-lookup"><span data-stu-id="b627f-155">**Optional parameters**</span></span>

<span data-ttu-id="b627f-156">`NumberOfLanguagesToDetect` 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="b627f-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="b627f-157">預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="b627f-157">The default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="b627f-158">Batch API</span><span class="sxs-lookup"><span data-stu-id="b627f-158">Batch APIs</span></span>
<span data-ttu-id="b627f-159">文字分析服務可讓您以 Batch 模式執行情感和關鍵片語的擷取。</span><span class="sxs-lookup"><span data-stu-id="b627f-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="b627f-160">請注意，每一筆評分記錄都是一個交易。</span><span class="sxs-lookup"><span data-stu-id="b627f-160">Note that each of the records scored counts as one transaction.</span></span> <span data-ttu-id="b627f-161">例如，如果您在單一呼叫中要求 1000 筆記錄的情緒，則會扣除 1000 個交易。</span><span class="sxs-lookup"><span data-stu-id="b627f-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="b627f-162">請注意，在系統中輸入的識別碼是由系統傳回的識別碼。</span><span class="sxs-lookup"><span data-stu-id="b627f-162">Note that the IDs entered into the system are the IDs returned by the system.</span></span> <span data-ttu-id="b627f-163">Web 服務不會檢查這些是否為唯一的識別碼。</span><span class="sxs-lookup"><span data-stu-id="b627f-163">The web service does not check that these IDs are unique.</span></span> <span data-ttu-id="b627f-164">呼叫端必須負責驗證唯一性。</span><span class="sxs-lookup"><span data-stu-id="b627f-164">It is the responsibility of the caller to verify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="b627f-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="b627f-165">GetSentimentBatch</span></span>
<span data-ttu-id="b627f-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="b627f-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="b627f-167">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="b627f-167">**Example request**</span></span>

<span data-ttu-id="b627f-168">在下面的 POST 呼叫中，我們在要求本文中要求 "Hello World"、"Hello Foo World" 和 "Hello My World" 這些片語的情緒：</span><span class="sxs-lookup"><span data-stu-id="b627f-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="b627f-169">要求本文：</span><span class="sxs-lookup"><span data-stu-id="b627f-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="b627f-170">在以下回應中，您會取得與文字識別碼相關聯的分數的清單：</span><span class="sxs-lookup"><span data-stu-id="b627f-170">In the response below, you get the list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="b627f-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="b627f-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="b627f-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="b627f-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="b627f-173">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="b627f-173">**Example request**</span></span>

<span data-ttu-id="b627f-174">在此範例，我們要求下列文字中關鍵片語的情緒清單：</span><span class="sxs-lookup"><span data-stu-id="b627f-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span></span> 

* <span data-ttu-id="b627f-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span><span class="sxs-lookup"><span data-stu-id="b627f-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="b627f-176">"It was an amazing build conference, with very interesting talks"</span><span class="sxs-lookup"><span data-stu-id="b627f-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="b627f-177">"The traffic was terrible, I spent three hours going to the airport"</span><span class="sxs-lookup"><span data-stu-id="b627f-177">"The traffic was terrible, I spent three hours going to the airport"</span></span>

<span data-ttu-id="b627f-178">此要求是對端點的 POST 呼叫：</span><span class="sxs-lookup"><span data-stu-id="b627f-178">This request is made as a POST call to the endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="b627f-179">要求本文：</span><span class="sxs-lookup"><span data-stu-id="b627f-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

<span data-ttu-id="b627f-180">在以下回應中，您會取得與文字識別碼相關聯的片語的清單：</span><span class="sxs-lookup"><span data-stu-id="b627f-180">In the response below, you get the list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="b627f-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="b627f-181">GetLanguageBatch</span></span>

<span data-ttu-id="b627f-182">在下面的 POST 呼叫中，我們要求兩個文字輸入的語言偵測：</span><span class="sxs-lookup"><span data-stu-id="b627f-182">In the POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="b627f-183">要求本文：</span><span class="sxs-lookup"><span data-stu-id="b627f-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="b627f-184">這會傳回下列回應，在第一個輸入中偵測到英文，在第二個輸入中偵測到法文：</span><span class="sxs-lookup"><span data-stu-id="b627f-184">This returns the following response, where English is detected in the first input and French in the second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="b627f-185">主題偵測 API</span><span class="sxs-lookup"><span data-stu-id="b627f-185">Topic Detection APIs</span></span>
<span data-ttu-id="b627f-186">這是新發行的 API，可針對已提交的文字記錄清單傳回前幾個偵測到的主題。</span><span class="sxs-lookup"><span data-stu-id="b627f-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="b627f-187">主題是以關鍵片語識別，可以是一或多個相關文字。</span><span class="sxs-lookup"><span data-stu-id="b627f-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="b627f-188">請注意，每提交 1 筆文字記錄，此 API 就會以 1 筆交易計費。</span><span class="sxs-lookup"><span data-stu-id="b627f-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="b627f-189">這個 API 至少需要提交 100 筆文字記錄，但其設計可偵測數百至數千筆記錄的主題。</span><span class="sxs-lookup"><span data-stu-id="b627f-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="b627f-190">主題 – 提交作業</span><span class="sxs-lookup"><span data-stu-id="b627f-190">Topics – Submit job</span></span>
<span data-ttu-id="b627f-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="b627f-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="b627f-192">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="b627f-192">**Example request**</span></span>

<span data-ttu-id="b627f-193">在以下的 POST 呼叫中，我們要求一組 100 篇文章的主題，其中會顯示第一篇和最後一篇輸入文章，並包含兩個 StopPhrases。</span><span class="sxs-lookup"><span data-stu-id="b627f-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="b627f-194">要求本文：</span><span class="sxs-lookup"><span data-stu-id="b627f-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="b627f-195">在以下回應中，您可以取得已提交工作的 JobId：</span><span class="sxs-lookup"><span data-stu-id="b627f-195">In the response below, you get the JobId for the submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="b627f-196">不應當做主題傳回的單字或多字片語的清單。</span><span class="sxs-lookup"><span data-stu-id="b627f-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="b627f-197">可用來篩選出相當廣泛的主題。</span><span class="sxs-lookup"><span data-stu-id="b627f-197">Can be used to filter out very generic topics.</span></span> <span data-ttu-id="b627f-198">例如，在飯店業評論的相關資料集中，"hotel" 和 "hostel" 可能是合理的停止片語。</span><span class="sxs-lookup"><span data-stu-id="b627f-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="b627f-199">主題 – 輪詢作業結果</span><span class="sxs-lookup"><span data-stu-id="b627f-199">Topics – Poll for job results</span></span>
<span data-ttu-id="b627f-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="b627f-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="b627f-201">**範例要求**</span><span class="sxs-lookup"><span data-stu-id="b627f-201">**Example request**</span></span>

<span data-ttu-id="b627f-202">傳遞從「提交工作」步驟傳回的 JobId，以擷取結果。</span><span class="sxs-lookup"><span data-stu-id="b627f-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span></span> <span data-ttu-id="b627f-203">建議您每分鐘呼叫此端點一次，直到回應中出現「狀態 =「完成」」為止。</span><span class="sxs-lookup"><span data-stu-id="b627f-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span></span> <span data-ttu-id="b627f-204">完成一個工作大約需要 10 分鐘，完成包含數千筆記錄的工作則需要更久時間。</span><span class="sxs-lookup"><span data-stu-id="b627f-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="b627f-205">工作正在處理時，回應將會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="b627f-205">While it is processing, the response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="b627f-206">API 會以下列格式傳回 JSON 格式的輸出：</span><span class="sxs-lookup"><span data-stu-id="b627f-206">The API returns output in JSON format in the following format:</span></span>

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


<span data-ttu-id="b627f-207">回應每個部分的屬性如下所示：</span><span class="sxs-lookup"><span data-stu-id="b627f-207">The properties for each part of the response are as follows:</span></span>

<span data-ttu-id="b627f-208">**TopicInfo 屬性**</span><span class="sxs-lookup"><span data-stu-id="b627f-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="b627f-209">金鑰</span><span class="sxs-lookup"><span data-stu-id="b627f-209">Key</span></span> | <span data-ttu-id="b627f-210">說明</span><span class="sxs-lookup"><span data-stu-id="b627f-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b627f-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="b627f-211">TopicId</span></span> |<span data-ttu-id="b627f-212">每個主題的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="b627f-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="b627f-213">分數</span><span class="sxs-lookup"><span data-stu-id="b627f-213">Score</span></span> |<span data-ttu-id="b627f-214">指派給主題的記錄數。</span><span class="sxs-lookup"><span data-stu-id="b627f-214">Count of records assigned to topic.</span></span> |
| <span data-ttu-id="b627f-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="b627f-215">KeyPhrase</span></span> |<span data-ttu-id="b627f-216">主題彙總的單字或片語。</span><span class="sxs-lookup"><span data-stu-id="b627f-216">A summarizing word or phrase for the topic.</span></span> <span data-ttu-id="b627f-217">可以是 1 個字或多個字。</span><span class="sxs-lookup"><span data-stu-id="b627f-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="b627f-218">**TopicAssignment 屬性**</span><span class="sxs-lookup"><span data-stu-id="b627f-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="b627f-219">金鑰</span><span class="sxs-lookup"><span data-stu-id="b627f-219">Key</span></span> | <span data-ttu-id="b627f-220">說明</span><span class="sxs-lookup"><span data-stu-id="b627f-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b627f-221">識別碼</span><span class="sxs-lookup"><span data-stu-id="b627f-221">Id</span></span> |<span data-ttu-id="b627f-222">記錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="b627f-222">Identifier for the record.</span></span> <span data-ttu-id="b627f-223">等於輸入中包含的識別碼。</span><span class="sxs-lookup"><span data-stu-id="b627f-223">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="b627f-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="b627f-224">TopicId</span></span> |<span data-ttu-id="b627f-225">已獲指派記錄的主題識別碼。</span><span class="sxs-lookup"><span data-stu-id="b627f-225">The topic ID which the record has been assigned to.</span></span> |
| <span data-ttu-id="b627f-226">Distance</span><span class="sxs-lookup"><span data-stu-id="b627f-226">Distance</span></span> |<span data-ttu-id="b627f-227">記錄屬於主題的信賴度。</span><span class="sxs-lookup"><span data-stu-id="b627f-227">Confidence that the record belongs to the topic.</span></span> <span data-ttu-id="b627f-228">Distance 越接近零，表示信賴度越高。</span><span class="sxs-lookup"><span data-stu-id="b627f-228">Distance closer to zero indicates higher confidence.</span></span> |

