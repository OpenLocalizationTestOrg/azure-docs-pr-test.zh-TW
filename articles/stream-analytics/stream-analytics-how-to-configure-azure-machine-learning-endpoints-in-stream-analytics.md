---
title: "在串流分析中使用 Azure Machine Learning 端點 | Microsoft Docs"
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
ms.openlocfilehash: d3a46190dd802bf31ea03ef38304d58e6e63b66d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="53539-103">在串流分析中整合機器學習服務</span><span class="sxs-lookup"><span data-stu-id="53539-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="53539-104">串流分析支援對外呼叫 Azure Machine Learning 端點的使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="53539-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span></span> <span data-ttu-id="53539-105">[串流分析 REST API 程式庫](https://msdn.microsoft.com/library/azure/dn835031.aspx)中會詳細說明此功能的 REST API 支援。</span><span class="sxs-lookup"><span data-stu-id="53539-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="53539-106">本文提供要在串流分析中成功實作這項功能所需的補充資訊。</span><span class="sxs-lookup"><span data-stu-id="53539-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="53539-107">您也可以在 [這裡](stream-analytics-machine-learning-integration-tutorial.md)取得已發佈的教學課程。</span><span class="sxs-lookup"><span data-stu-id="53539-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="53539-108">概觀：Azure Machine Learning 術語</span><span class="sxs-lookup"><span data-stu-id="53539-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="53539-109">Microsoft Azure Machine Learning 提供可共同作業的拖放工具，供您依據資料來建置、測試及部署預測性分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="53539-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="53539-110">此工具稱為 *Azure Machine Learning Studio*。</span><span class="sxs-lookup"><span data-stu-id="53539-110">This tool is called the *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="53539-111">您可以利用此 Studio 來與機器學習服務資源互動，並輕鬆地建置、測試和反覆調整設計。</span><span class="sxs-lookup"><span data-stu-id="53539-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="53539-112">這些資源和其定義如下。</span><span class="sxs-lookup"><span data-stu-id="53539-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="53539-113">**工作區**： *工作區* 這個容器中會保有其他所有機器學習服務資源，以便集中管理和控制。</span><span class="sxs-lookup"><span data-stu-id="53539-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="53539-114">**實驗**：資料科學家會建立 *實驗* 來利用資料集和訓練機器學習服務模型。</span><span class="sxs-lookup"><span data-stu-id="53539-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="53539-115">**端點**： *端點* 是 Azure Machine Learning 物件，可供用來將功能做為輸入、套用指定的機器學習服務模型，並傳回經過評分的輸出。</span><span class="sxs-lookup"><span data-stu-id="53539-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="53539-116">**評分 Web 服務**： *評分 Web 服務* 是上述端點的集合。</span><span class="sxs-lookup"><span data-stu-id="53539-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="53539-117">每個端點都有適用於批次執行和同步執行的 API。</span><span class="sxs-lookup"><span data-stu-id="53539-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="53539-118">串流分析使用同步執行。</span><span class="sxs-lookup"><span data-stu-id="53539-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="53539-119">該特定服務在 AzureML Studio 中的名稱為 [要求/回應服務](../machine-learning/machine-learning-consume-web-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="53539-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="53539-120">串流分析作業所需的機器學習服務資源</span><span class="sxs-lookup"><span data-stu-id="53539-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="53539-121">為了處理串流分析作業，必須要有要求/回應端點、 [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md)和 swagger 定義才能順利執行。</span><span class="sxs-lookup"><span data-stu-id="53539-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="53539-122">串流分析有其他端點可建構 swagger 端點的 URL、查閱介面，以及將預設 UDF 定義傳回給使用者。</span><span class="sxs-lookup"><span data-stu-id="53539-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="53539-123">透過 REST API 設定串流分析和機器學習服務 UDF</span><span class="sxs-lookup"><span data-stu-id="53539-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="53539-124">透過使用 REST API，您可以設定作業來呼叫 Azure 機器語言函式。</span><span class="sxs-lookup"><span data-stu-id="53539-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span></span> <span data-ttu-id="53539-125">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="53539-125">The steps are as follows:</span></span>

1. <span data-ttu-id="53539-126">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="53539-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="53539-127">定義輸入</span><span class="sxs-lookup"><span data-stu-id="53539-127">Define an input</span></span>
3. <span data-ttu-id="53539-128">定義輸出</span><span class="sxs-lookup"><span data-stu-id="53539-128">Define an output</span></span>
4. <span data-ttu-id="53539-129">建立使用者定義函式 (UDF)</span><span class="sxs-lookup"><span data-stu-id="53539-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="53539-130">撰寫呼叫 UDF 的串流分析轉換</span><span class="sxs-lookup"><span data-stu-id="53539-130">Write a Stream Analytics transformation that calls the UDF</span></span>
6. <span data-ttu-id="53539-131">啟動工作</span><span class="sxs-lookup"><span data-stu-id="53539-131">Start the job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="53539-132">使用基本屬性建立 UDF</span><span class="sxs-lookup"><span data-stu-id="53539-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="53539-133">下列範例程式碼會建立名為 *newudf* 且繫結至 Azure Machine Learning 端點的純量 UDF，來做為示範。</span><span class="sxs-lookup"><span data-stu-id="53539-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="53539-134">請注意，您可以在 API 說明頁面中找到所選服務的*端點* (服務 URI)，以及在 [服務] 主頁面中找到 *apiKey*。</span><span class="sxs-lookup"><span data-stu-id="53539-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="53539-135">要求本文範例：</span><span class="sxs-lookup"><span data-stu-id="53539-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="53539-136">呼叫預設 UDF 的 RetrieveDefaultDefinition 端點</span><span class="sxs-lookup"><span data-stu-id="53539-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="53539-137">一旦建立好基本架構 UDF，就需要 UDF 的完整定義。</span><span class="sxs-lookup"><span data-stu-id="53539-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span></span> <span data-ttu-id="53539-138">RetreiveDefaultDefinition 端點可協助您取得繫結至 Azure Machine Learning 端點之純量函式的預設定義。</span><span class="sxs-lookup"><span data-stu-id="53539-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="53539-139">下列內容會要求您取得繫結至 Azure Machine Learning 端點之純量函式的預設 UDF 定義。</span><span class="sxs-lookup"><span data-stu-id="53539-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="53539-140">因為已在 PUT 要求期間提供，因此它不會指定實際的端點。</span><span class="sxs-lookup"><span data-stu-id="53539-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="53539-141">串流分析會呼叫要求中提供的端點 (如果已明確提供)。</span><span class="sxs-lookup"><span data-stu-id="53539-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span></span> <span data-ttu-id="53539-142">否則，它會使用原本參考的端點。</span><span class="sxs-lookup"><span data-stu-id="53539-142">Otherwise it uses the one originally referenced.</span></span> <span data-ttu-id="53539-143">UDF 在這邊會採用單一字串參數 (一個句子)，並傳回指出該句子的「情緒」標籤的單一類型字串輸出。</span><span class="sxs-lookup"><span data-stu-id="53539-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="53539-144">要求本文範例：</span><span class="sxs-lookup"><span data-stu-id="53539-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="53539-145">此項目的範例輸出會看起來像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="53539-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-the-response"></a><span data-ttu-id="53539-146">使用回應修補 UDF</span><span class="sxs-lookup"><span data-stu-id="53539-146">Patch UDF with the response</span></span>
<span data-ttu-id="53539-147">現在必須使用先前的回應修補 UDF，如下所示。</span><span class="sxs-lookup"><span data-stu-id="53539-147">Now the UDF must be patched with the previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="53539-148">要求本文 (RetrieveDefaultDefinition 的輸出)：</span><span class="sxs-lookup"><span data-stu-id="53539-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-to-call-the-udf"></a><span data-ttu-id="53539-149">實作串流分析轉換來呼叫 UDF</span><span class="sxs-lookup"><span data-stu-id="53539-149">Implement Stream Analytics transformation to call the UDF</span></span>
<span data-ttu-id="53539-150">現在要查詢每一個輸入事件的 UDF (這裡稱為 scoreTweet)，並將該事件的回應寫入至輸出。</span><span class="sxs-lookup"><span data-stu-id="53539-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="53539-151">取得說明</span><span class="sxs-lookup"><span data-stu-id="53539-151">Get help</span></span>
<span data-ttu-id="53539-152">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="53539-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="53539-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53539-153">Next steps</span></span>
* [<span data-ttu-id="53539-154">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="53539-154">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="53539-155">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="53539-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="53539-156">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="53539-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="53539-157">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="53539-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="53539-158">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="53539-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
