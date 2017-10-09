---
title: "在 Stream Analytics aaaUse Azure Machine Learning 端點 |Microsoft 文件"
description: "串流分析中的機器語言使用者定義函式"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="f06d0-103">在串流分析中整合機器學習服務</span><span class="sxs-lookup"><span data-stu-id="f06d0-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="f06d0-104">串流分析支援呼叫 tooAzure 機器學習端點的使用者定義函數。</span><span class="sxs-lookup"><span data-stu-id="f06d0-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="f06d0-105">這項功能的 REST API 支援會詳細說明 hello[資料流分析 REST API 文件庫](https://msdn.microsoft.com/library/azure/dn835031.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f06d0-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="f06d0-106">本文提供要在串流分析中成功實作這項功能所需的補充資訊。</span><span class="sxs-lookup"><span data-stu-id="f06d0-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="f06d0-107">您也可以在 [這裡](stream-analytics-machine-learning-integration-tutorial.md)取得已發佈的教學課程。</span><span class="sxs-lookup"><span data-stu-id="f06d0-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="f06d0-108">概觀：Azure Machine Learning 術語</span><span class="sxs-lookup"><span data-stu-id="f06d0-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="f06d0-109">Microsoft Azure Machine Learning 提供共同作業、 拖放的工具，您可以使用 toobuild、 測試及部署您的資料的預測分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="f06d0-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="f06d0-110">此工具會呼叫 hello *Azure Machine Learning Studio*。</span><span class="sxs-lookup"><span data-stu-id="f06d0-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="f06d0-111">hello studio 是以 hello 使用的 toointeract 機器學習資源和輕鬆建置、 測試及逐一查看設計。</span><span class="sxs-lookup"><span data-stu-id="f06d0-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="f06d0-112">這些資源和其定義如下。</span><span class="sxs-lookup"><span data-stu-id="f06d0-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="f06d0-113">**工作區**: hello*工作區*會保留所有其他機器學習資源集中管理及控制容器的容器。</span><span class="sxs-lookup"><span data-stu-id="f06d0-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="f06d0-114">**實驗**:*實驗*資料科學家 tooutilize 資料集所建立並定型的機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="f06d0-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="f06d0-115">**端點**:*端點*會做為輸入 hello Azure 機器學習使用物件 tootake 功能、 適用於指定的機器學習模型，再傳回評分的輸出。</span><span class="sxs-lookup"><span data-stu-id="f06d0-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="f06d0-116">**評分 Web 服務**： *評分 Web 服務* 是上述端點的集合。</span><span class="sxs-lookup"><span data-stu-id="f06d0-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="f06d0-117">每個端點都有適用於批次執行和同步執行的 API。</span><span class="sxs-lookup"><span data-stu-id="f06d0-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="f06d0-118">串流分析使用同步執行。</span><span class="sxs-lookup"><span data-stu-id="f06d0-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="f06d0-119">hello 特定服務的名稱為[要求/回應服務](../machine-learning/machine-learning-consume-web-services.md)AzureML studio 中。</span><span class="sxs-lookup"><span data-stu-id="f06d0-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="f06d0-120">串流分析作業所需的機器學習服務資源</span><span class="sxs-lookup"><span data-stu-id="f06d0-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="f06d0-121">基於 hello 資料流分析作業正在處理的要求/回應端點， [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md)，而且 swagger 定義所有必要才能成功執行。</span><span class="sxs-lookup"><span data-stu-id="f06d0-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="f06d0-122">資料流分析已建構 hello swagger 端點 url、 查詢 hello 介面並傳回預設 UDF 定義 toohello 使用者的其他端點。</span><span class="sxs-lookup"><span data-stu-id="f06d0-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="f06d0-123">透過 REST API 設定串流分析和機器學習服務 UDF</span><span class="sxs-lookup"><span data-stu-id="f06d0-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="f06d0-124">使用 REST Api，您可以設定工作 toocall Azure 機器語言函式。</span><span class="sxs-lookup"><span data-stu-id="f06d0-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="f06d0-125">hello 步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="f06d0-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="f06d0-126">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="f06d0-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="f06d0-127">定義輸入</span><span class="sxs-lookup"><span data-stu-id="f06d0-127">Define an input</span></span>
3. <span data-ttu-id="f06d0-128">定義輸出</span><span class="sxs-lookup"><span data-stu-id="f06d0-128">Define an output</span></span>
4. <span data-ttu-id="f06d0-129">建立使用者定義函式 (UDF)</span><span class="sxs-lookup"><span data-stu-id="f06d0-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="f06d0-130">寫入資料流分析轉換呼叫 hello UDF</span><span class="sxs-lookup"><span data-stu-id="f06d0-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="f06d0-131">啟動 hello 工作</span><span class="sxs-lookup"><span data-stu-id="f06d0-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="f06d0-132">使用基本屬性建立 UDF</span><span class="sxs-lookup"><span data-stu-id="f06d0-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="f06d0-133">例如，下列範例程式碼的 hello 建立名為的純量 UDF *newudf* tooan Azure Machine Learning 端點繫結。</span><span class="sxs-lookup"><span data-stu-id="f06d0-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="f06d0-134">請注意該 hello*端點*（服務 URI） 可以選擇服務和 hello hello hello API 說明頁面上找到*apiKey* hello 服務主頁面上可以找到。</span><span class="sxs-lookup"><span data-stu-id="f06d0-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="f06d0-135">要求本文範例：</span><span class="sxs-lookup"><span data-stu-id="f06d0-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="f06d0-136">呼叫預設 UDF 的 RetrieveDefaultDefinition 端點</span><span class="sxs-lookup"><span data-stu-id="f06d0-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="f06d0-137">一次 hello hello hello UDF 需要完整定義會建立 UDF 的基本架構。</span><span class="sxs-lookup"><span data-stu-id="f06d0-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="f06d0-138">hello RetreiveDefaultDefinition 端點可協助您取得繫結的 tooan Azure Machine Learning 端點的純量函式的 hello default 定義。</span><span class="sxs-lookup"><span data-stu-id="f06d0-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="f06d0-139">hello 裝載下列需要您 tooget hello 預設 UDF 定義繫結的 tooan Azure Machine Learning 端點的純量函式。</span><span class="sxs-lookup"><span data-stu-id="f06d0-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="f06d0-140">它不會指定 hello 實際的端點，因為它已經提供在 PUT 要求。</span><span class="sxs-lookup"><span data-stu-id="f06d0-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="f06d0-141">資料流分析呼叫 hello hello 要求中提供，如果提供明確的端點。</span><span class="sxs-lookup"><span data-stu-id="f06d0-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="f06d0-142">否則它會使用原本所參考的其中一個 hello。</span><span class="sxs-lookup"><span data-stu-id="f06d0-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="f06d0-143">這裡 hello UDF 會接受單一字串參數 （句子），並傳回表示該句子 hello 「 情緒"標籤字串類型的單一輸出。</span><span class="sxs-lookup"><span data-stu-id="f06d0-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="f06d0-144">要求本文範例：</span><span class="sxs-lookup"><span data-stu-id="f06d0-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="f06d0-145">此項目的範例輸出會看起來像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="f06d0-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="f06d0-146">修補程式 UDF hello 回應</span><span class="sxs-lookup"><span data-stu-id="f06d0-146">Patch UDF with hello response</span></span>
<span data-ttu-id="f06d0-147">現在 hello UDF 必須先安裝修補與前一個回應 hello，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f06d0-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="f06d0-148">要求本文 (RetrieveDefaultDefinition 的輸出)：</span><span class="sxs-lookup"><span data-stu-id="f06d0-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="f06d0-149">實作資料流分析轉換 toocall hello UDF</span><span class="sxs-lookup"><span data-stu-id="f06d0-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="f06d0-150">現在每個輸入的事件查詢 hello UDF （以下稱為 scoreTweet），以及撰寫該事件 tooan 輸出的回應。</span><span class="sxs-lookup"><span data-stu-id="f06d0-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="f06d0-151">取得說明</span><span class="sxs-lookup"><span data-stu-id="f06d0-151">Get help</span></span>
<span data-ttu-id="f06d0-152">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f06d0-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f06d0-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f06d0-153">Next steps</span></span>
* [<span data-ttu-id="f06d0-154">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="f06d0-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f06d0-155">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f06d0-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f06d0-156">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="f06d0-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f06d0-157">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="f06d0-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f06d0-158">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="f06d0-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
