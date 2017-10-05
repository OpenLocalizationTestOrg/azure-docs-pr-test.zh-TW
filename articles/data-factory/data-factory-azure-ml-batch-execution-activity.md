---
title: "使用 Azure Data Factory 建立預測資料管線 | Microsoft Docs"
description: "說明如何使用 Azure Data Factory 和 Azure Machine Learning 建立預測管線"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="262f6-103">使用 Azure Machine Learning 和 Azure Data Factory 來建立預測管線</span><span class="sxs-lookup"><span data-stu-id="262f6-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="262f6-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="262f6-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="262f6-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="262f6-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="262f6-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="262f6-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="262f6-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="262f6-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="262f6-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="262f6-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="262f6-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="262f6-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="262f6-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="262f6-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="262f6-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="262f6-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="262f6-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="262f6-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="262f6-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="262f6-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="262f6-114">簡介</span><span class="sxs-lookup"><span data-stu-id="262f6-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="262f6-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="262f6-115">Azure Machine Learning</span></span>
<span data-ttu-id="262f6-116">[Azure 機器學習服務](https://azure.microsoft.com/documentation/services/machine-learning/) 可讓您建置、測試以及部署預測性分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="262f6-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="262f6-117">從高階觀點而言，由下列三個步驟完成這個動作：</span><span class="sxs-lookup"><span data-stu-id="262f6-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="262f6-118">**建立訓練實驗**。</span><span class="sxs-lookup"><span data-stu-id="262f6-118">**Create a training experiment**.</span></span> <span data-ttu-id="262f6-119">您可以使用 Azure ML Studio 來進行此步驟。</span><span class="sxs-lookup"><span data-stu-id="262f6-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="262f6-120">ML Studio 是共同作業的視覺化開發環境，可供您使用訓練資料來訓練和測試預測性分析模型。</span><span class="sxs-lookup"><span data-stu-id="262f6-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="262f6-121">**將其轉換為評分實驗**。</span><span class="sxs-lookup"><span data-stu-id="262f6-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="262f6-122">一旦您的模型已使用現有資料訓練，並做好使用該模型為新資料評分的準備之後，您準備並簡化用於評分實驗。</span><span class="sxs-lookup"><span data-stu-id="262f6-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="262f6-123">**將其部署為 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="262f6-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="262f6-124">只要按一下，您就可以將評分實驗當做 Azure Web 服務發佈。</span><span class="sxs-lookup"><span data-stu-id="262f6-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="262f6-125">您可以透過此 Web 服務端點將資料傳送給您的模型，並從模型接收結果預測。</span><span class="sxs-lookup"><span data-stu-id="262f6-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="262f6-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="262f6-126">Azure Data Factory</span></span>
<span data-ttu-id="262f6-127">Data Factory 是雲端架構資料整合服務，用來協調以及自動**移動**和**轉換**資料。</span><span class="sxs-lookup"><span data-stu-id="262f6-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="262f6-128">您可以使用 Azure Data Factory 建立資料整合方案，以從各種資料存放區內嵌資料、轉換/處理資料，並將結果資料發佈至資料存放區。</span><span class="sxs-lookup"><span data-stu-id="262f6-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="262f6-129">Data Factory 服務可讓您建立資料管線，以移動和轉換資料，然後依指定的排程 (每小時、每天、每週等) 執行管線。</span><span class="sxs-lookup"><span data-stu-id="262f6-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="262f6-130">它也提供豐富的視覺效果來顯示資料管線之間的歷程和相依性，並可透過單一整合檢視監視您所有的資料管線，以輕鬆地找出問題並設定監視警示。</span><span class="sxs-lookup"><span data-stu-id="262f6-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="262f6-131">請參閱 [Azure Data Factory 簡介](data-factory-introduction.md)和[建置您的第一個管線](data-factory-build-your-first-pipeline.md)文章，快速地開始使用 Azure Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="262f6-132">Data Factory 和 Machine Learning 一起合作</span><span class="sxs-lookup"><span data-stu-id="262f6-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="262f6-133">Azure Data Factory 可讓您輕鬆地建立管線，使用已發佈的 [Azure Machine Learning][azure-machine-learning] Web 服務進行預測性分析。</span><span class="sxs-lookup"><span data-stu-id="262f6-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="262f6-134">在 Azure Data Factory 管線中使用 [批次執行活動]  ，您可以叫用 Azure ML Web 服務以對批次中的資料進行預測。</span><span class="sxs-lookup"><span data-stu-id="262f6-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="262f6-135">如需詳細資訊，請參閱 [使用批次執行活動叫用 Azure ML Web 服務](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) 一節。</span><span class="sxs-lookup"><span data-stu-id="262f6-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="262f6-136">經過一段時間，必須使用新的輸入資料集重新訓練 Azure ML 評分實驗中的預測模型。</span><span class="sxs-lookup"><span data-stu-id="262f6-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="262f6-137">您可以執行下列步驟，從 Data Factory 管線重新訓練 Azure ML 模型：</span><span class="sxs-lookup"><span data-stu-id="262f6-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="262f6-138">將訓練實驗 (而非預設實驗) 發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="262f6-139">在 Azure ML Studio 中進行此步驟的方法，和先前案例中將預測實驗公開為 Web 服務的方法一樣。</span><span class="sxs-lookup"><span data-stu-id="262f6-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="262f6-140">使用 Azure ML 批次執行活動，對訓練實驗叫用 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="262f6-141">基本上，您可以使用 Azure ML 批次執行活動來叫用訓練 Web 服務和評分 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="262f6-142">完成重新訓練之後，您可以使用「Azure ML 更新資源活動」，使用新訓練的模型來更新評分 Web 服務 (以 Web 服務公開的預測實驗)。</span><span class="sxs-lookup"><span data-stu-id="262f6-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="262f6-143">如需詳細資料，請參閱[使用更新資源活動更新模型](data-factory-azure-ml-update-resource-activity.md)一文。</span><span class="sxs-lookup"><span data-stu-id="262f6-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="262f6-144">使用批次執行活動來叫用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="262f6-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="262f6-145">您可以使用 Azure Data Factory 協調資料的移動和處理作業，然後使用 Azure Machine Learning 批次執行。</span><span class="sxs-lookup"><span data-stu-id="262f6-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="262f6-146">以下是最上層的步驟︰</span><span class="sxs-lookup"><span data-stu-id="262f6-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="262f6-147">建立 Azure Machine Learning 連結服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="262f6-148">您需要下列值︰</span><span class="sxs-lookup"><span data-stu-id="262f6-148">You need the following values:</span></span>

   1. <span data-ttu-id="262f6-149">**要求 URI** 。</span><span class="sxs-lookup"><span data-stu-id="262f6-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="262f6-150">您可以按一下 Web 服務頁面中的 **批次執行** 連結，即可找到要求 URI。</span><span class="sxs-lookup"><span data-stu-id="262f6-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="262f6-151">**API 金鑰** 。</span><span class="sxs-lookup"><span data-stu-id="262f6-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="262f6-152">按一下已發佈的 Web 服務，即可找到 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="262f6-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="262f6-153">使用 **AzureMLBatchExecution** 活動。</span><span class="sxs-lookup"><span data-stu-id="262f6-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![機器學習服務儀表板](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![批次 URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="262f6-156">案例：使用 Web 服務輸入/輸出 (參考 Azure Blob 儲存體中的資料) 的實驗</span><span class="sxs-lookup"><span data-stu-id="262f6-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="262f6-157">在此案例中，Azure Machine Learning Web 服務會使用 Azure Blob 儲存體中的檔案資料執行預測，並將預測結果儲存在 Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="262f6-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="262f6-158">下列 JSON 使用 AzureMLBatchExecution 活動定義 Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="262f6-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="262f6-159">此活動以 **DecisionTreeInputBlob** 資料集做為輸入，以 **DecisionTreeResultBlob** 資料集做為輸出。</span><span class="sxs-lookup"><span data-stu-id="262f6-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="262f6-160">**DecisionTreeInputBlob** 會做為輸入以使用 **webServiceInput** JSON 屬性傳遞至 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="262f6-161">**DecisionTreeResultBlob** 會做為輸出以使用 **webServiceOutputs** JSON 屬性傳遞至 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="262f6-162">如果 Web 服務接受多個輸入，請使用 **webServiceInputs** 屬性，而不要使用 **webServiceInput**。</span><span class="sxs-lookup"><span data-stu-id="262f6-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="262f6-163">如需如何使用 webServiceInputs 屬性的範例，請參閱 [Web 服務需要多個輸入](#web-service-requires-multiple-inputs) 一節。</span><span class="sxs-lookup"><span data-stu-id="262f6-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="262f6-164">**webServiceInput**/**webServiceInputs** 和 **webServiceOutputs** 屬性 (位於 **typeProperties** 中) 所參考的資料集必須也包含在活動的 **inputs** 和 **outputs** 中。</span><span class="sxs-lookup"><span data-stu-id="262f6-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="262f6-165">在您的 Azure ML 實驗中，Web 服務輸入和輸出連接埠及全域參數有您可以自訂的預設名稱 ("input1"、"input2")。</span><span class="sxs-lookup"><span data-stu-id="262f6-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="262f6-166">您用於 webServiceInputs、webServiceOutputs 及 globalParameters 設定的名稱必須與實驗中的名稱完全相同。</span><span class="sxs-lookup"><span data-stu-id="262f6-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="262f6-167">您可以檢視您 Azure ML 端點之 [批次執行說明] 頁面上的範例要求承載，來確認預期的對應。</span><span class="sxs-lookup"><span data-stu-id="262f6-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="262f6-168">只有當輸入及輸出屬於 AzureMLBatchExecution 活動時，才可以當做參數傳遞至 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="262f6-169">例如，在上面的 JSON 片段中，DecisionTreeInputBlob 是 AzureMLBatchExecution 活動的輸入，其透過 webServiceInput 參數傳遞至 Web 服務做為輸入。</span><span class="sxs-lookup"><span data-stu-id="262f6-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="262f6-170">範例</span><span class="sxs-lookup"><span data-stu-id="262f6-170">Example</span></span>
<span data-ttu-id="262f6-171">此範例使用 Azure 儲存體來存放輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="262f6-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="262f6-172">建議您在瀏覽此範例之前，先瀏覽[透過 Data Factory 建立第一個管線][adf-build-1st-pipeline]教學課程。</span><span class="sxs-lookup"><span data-stu-id="262f6-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="262f6-173">在此範例中使用 Data Factory 編輯器來建立 Data Factory 構件 (連結服務、資料集、管線)。</span><span class="sxs-lookup"><span data-stu-id="262f6-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="262f6-174">為您的 **Azure 儲存體**建立**連結服務**。</span><span class="sxs-lookup"><span data-stu-id="262f6-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="262f6-175">如果輸入和輸出檔案在不同的儲存體帳戶中，您就需要兩個連結服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="262f6-176">以下是 JSON 範例：</span><span class="sxs-lookup"><span data-stu-id="262f6-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="262f6-177">建立**輸入** Azure Data Factory **資料集**。</span><span class="sxs-lookup"><span data-stu-id="262f6-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="262f6-178">與某些其他 Data Factory 資料集不同的是，這些資料集必須同時包含 **folderPath** 和 **fileName** 值。</span><span class="sxs-lookup"><span data-stu-id="262f6-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="262f6-179">您可以使用資料分割，讓每個批次執行 (每一個資料配量) 處理或產生唯一的輸入和輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="262f6-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="262f6-180">您可能需要包含某個上游活動，以將輸入轉換成 CSV 檔案格式，並將它放在每個配量的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="262f6-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="262f6-181">在此情況下，您不需包含下列範例所示的 **external** 及 **externalData** 設定，而您的 DecisionTreeInputBlob 會是不同活動的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="262f6-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    <span data-ttu-id="262f6-182">您的輸入 csv 檔案必須要有資料行標題資料列。</span><span class="sxs-lookup"><span data-stu-id="262f6-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="262f6-183">如果使用 [複製活動] 建立 csv 或將其移至 Blob 儲存體，則接收屬性 **blobWriterAddHeader** 應該設為 **true**。</span><span class="sxs-lookup"><span data-stu-id="262f6-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="262f6-184">例如：</span><span class="sxs-lookup"><span data-stu-id="262f6-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="262f6-185">如果 csv 檔案沒有標頭資料列，您可能會看到下列錯誤：**活動中的錯誤：讀取字串時發生錯誤。非預期的權杖：StartObject。路徑 ''、行 1、位置 1**。</span><span class="sxs-lookup"><span data-stu-id="262f6-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="262f6-186">建立**輸出** Azure Data Factory **資料集**。</span><span class="sxs-lookup"><span data-stu-id="262f6-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="262f6-187">此範例使用資料分割來為每一個配量執行建立一個唯一輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="262f6-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="262f6-188">如果沒有資料分割，活動就會覆寫檔案。</span><span class="sxs-lookup"><span data-stu-id="262f6-188">Without the partitioning, the activity would overwrite the file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="262f6-189">建立 **AzureMLLinkedService** 類型的**連結服務**，並提供 API 金鑰和模型批次執行 URL。</span><span class="sxs-lookup"><span data-stu-id="262f6-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="262f6-190">最後，撰寫一個包含 **AzureMLBatchExecution** 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="262f6-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="262f6-191">在執行階段，管線會執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="262f6-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="262f6-192">從輸入資料集取得輸入檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="262f6-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="262f6-193">叫用 Azure Machine Learning 批次執行 API</span><span class="sxs-lookup"><span data-stu-id="262f6-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="262f6-194">將批次執行輸出複製到輸出資料集中指定的 Blob。</span><span class="sxs-lookup"><span data-stu-id="262f6-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="262f6-195">AzureMLBatchExecution 活動可以有零個或多個輸入，以及一個或多個輸出。</span><span class="sxs-lookup"><span data-stu-id="262f6-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="262f6-196">**開始**和**結束**日期時間必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="262f6-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="262f6-197">例如：2014-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="262f6-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="262f6-198">**結束**時間是選用項目。</span><span class="sxs-lookup"><span data-stu-id="262f6-198">The **end** time is optional.</span></span> <span data-ttu-id="262f6-199">如果您未指定 **end** 屬性的值，則會以「**start + 48 小時**」計算。</span><span class="sxs-lookup"><span data-stu-id="262f6-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="262f6-200">若要無限期地執行管線，請指定 **9999-09-09** 做為 **end** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="262f6-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="262f6-201">如需 JSON 屬性的詳細資料，請參閱 [JSON 指令碼參考](https://msdn.microsoft.com/library/dn835050.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="262f6-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="262f6-202">您可自行選擇是否指定 AzureMLBatchExecution 活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="262f6-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="262f6-203">案例：使用讀取器/寫入器模組參考各種儲存體資料的實驗</span><span class="sxs-lookup"><span data-stu-id="262f6-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="262f6-204">建立 Azure ML 實驗時的另一個常見案例，是使用讀取器和寫入器模組。</span><span class="sxs-lookup"><span data-stu-id="262f6-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="262f6-205">讀取器模組是用來將資料載入實驗，而寫入器模組則是用於儲存您的實驗資料。</span><span class="sxs-lookup"><span data-stu-id="262f6-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="262f6-206">如需讀取器和寫入器模組的詳細資料，請參閱 MSDN Library 上的[讀取器](https://msdn.microsoft.com/library/azure/dn905997.aspx)和[寫入器](https://msdn.microsoft.com/library/azure/dn905984.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="262f6-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="262f6-207">使用讀取器和寫入器模組時，較好的做法是針對這些讀取器/寫入器模組的每一個屬性，使用 Web 服務參數。</span><span class="sxs-lookup"><span data-stu-id="262f6-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="262f6-208">這些 Web 參數可讓您在執行階段設定值。</span><span class="sxs-lookup"><span data-stu-id="262f6-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="262f6-209">例如，建立實驗時，您可以利用讀取器模組使用 Azure SQL Database：XXX.database.windows.net。</span><span class="sxs-lookup"><span data-stu-id="262f6-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="262f6-210">部署 Web 服務之後，您需要啟用 Web 服務的取用者，藉此指定另一個稱為 YYY.database.windows.net 的 Azure SQL Server。</span><span class="sxs-lookup"><span data-stu-id="262f6-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="262f6-211">您可以使用 Web 服務參數來設定此值。</span><span class="sxs-lookup"><span data-stu-id="262f6-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="262f6-212">Web 服務的輸入和輸出與 Web 服務參數不同。</span><span class="sxs-lookup"><span data-stu-id="262f6-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="262f6-213">在第一個案例中，您已了解如何為 Azure ML Web 服務指定輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="262f6-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="262f6-214">在此案例中，您會傳遞 Web 服務的參數，以對應至讀取器/寫入器模組的屬性。</span><span class="sxs-lookup"><span data-stu-id="262f6-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="262f6-215">讓我們看看使用 Web 服務參數的案例。</span><span class="sxs-lookup"><span data-stu-id="262f6-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="262f6-216">您已部署 Azure Machine Learning Web 服務，其使用讀取器模組所讀取的資料，是來自其中一個受 Azure Machine Learning 支援的資料來源 (例如：Azure SQL Database)。</span><span class="sxs-lookup"><span data-stu-id="262f6-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="262f6-217">批次執行之後，會使用寫入器模組寫入結果 (Azure SQL Database)。</span><span class="sxs-lookup"><span data-stu-id="262f6-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="262f6-218">實驗中沒有定義任何 Web 服務的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="262f6-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="262f6-219">在此情況下，我們建議您為讀取器和寫入器模組設定相關 Web 服務參數。</span><span class="sxs-lookup"><span data-stu-id="262f6-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="262f6-220">此組態允許在使用 AzureMLBatchExecution 活動時設定讀取器/寫入器模組。</span><span class="sxs-lookup"><span data-stu-id="262f6-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="262f6-221">如以下活動 JSON 所示，在 **globalParameters** 區段中指定 Web 服務參數。</span><span class="sxs-lookup"><span data-stu-id="262f6-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="262f6-222">您也可以使用 [Data Factory 函式](data-factory-functions-variables.md) 傳遞 Web 服務參數的值，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="262f6-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="262f6-223">Web 服務參數區分大小寫，因此，請確定您在活動 JSON 中所指定的名稱符合 Web 服務所公開的名稱。</span><span class="sxs-lookup"><span data-stu-id="262f6-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="262f6-224">使用讀取器模組讀取 Azure Blob 中多個檔案的資料</span><span class="sxs-lookup"><span data-stu-id="262f6-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="262f6-225">具有 Pig 和 Hive 等活動的巨量資料管線可以產生沒有副檔名的一個或多個輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="262f6-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="262f6-226">例如，當您指定外部 Hive 資料表時，外部 Hive 資料表的資料可以儲存在 Azure Blob 儲存體中，並命名為：000000_0。</span><span class="sxs-lookup"><span data-stu-id="262f6-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="262f6-227">您可以在實驗中使用讀取器模組讀取多個檔案，並將該模組用於預測。</span><span class="sxs-lookup"><span data-stu-id="262f6-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="262f6-228">在 Azure Machine Learning 實驗中使用讀取器模組時，您可以指定 Azure Blob 做為輸入。</span><span class="sxs-lookup"><span data-stu-id="262f6-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="262f6-229">Azure Blob 儲存體中的檔案可以是在 HDInsight 上執行的 Pig 和 Hive 指令碼所產生的輸出檔 (範例：000000_0)。</span><span class="sxs-lookup"><span data-stu-id="262f6-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="262f6-230">讀取器模組可讓您藉由設定 **容器、目錄或 Blob 的路徑**來讀取檔案 (沒有副檔名)。</span><span class="sxs-lookup"><span data-stu-id="262f6-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="262f6-231">**容器路徑**指向容器，**目錄/Blob** 則指向包含檔案的資料夾，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="262f6-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="262f6-232">星號 (也就是 \*) **會指定容器/資料夾中的所有檔案 (也就是 data/aggregateddata/year=2014/month-6/\*)** 將讀取為實驗的一部分。</span><span class="sxs-lookup"><span data-stu-id="262f6-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Azure Blob 屬性](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="262f6-234">範例</span><span class="sxs-lookup"><span data-stu-id="262f6-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="262f6-235">AzureMLBatchExecution 活動使用 Web 服務參數的管線</span><span class="sxs-lookup"><span data-stu-id="262f6-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="262f6-236">在上述 JSON 範例中：</span><span class="sxs-lookup"><span data-stu-id="262f6-236">In the above JSON example:</span></span>

* <span data-ttu-id="262f6-237">已部署的 Azure Machine Learning Web 服務使用讀取器和寫入器模組，讀取 Azure SQL Database 的資料，或將資料寫入其中。</span><span class="sxs-lookup"><span data-stu-id="262f6-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="262f6-238">此 Web 服務會公開下列 4 個參數：資料庫伺服器名稱、資料庫名稱、伺服器使用者帳戶名稱和伺服器使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="262f6-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="262f6-239">**開始**和**結束**日期時間必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="262f6-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="262f6-240">例如：2014-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="262f6-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="262f6-241">**結束**時間是選用項目。</span><span class="sxs-lookup"><span data-stu-id="262f6-241">The **end** time is optional.</span></span> <span data-ttu-id="262f6-242">如果您未指定 **end** 屬性的值，則會以「**start + 48 小時**」計算。</span><span class="sxs-lookup"><span data-stu-id="262f6-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="262f6-243">若要無限期地執行管線，請指定 **9999-09-09** 做為 **end** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="262f6-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="262f6-244">如需 JSON 屬性的詳細資料，請參閱 [JSON 指令碼參考](https://msdn.microsoft.com/library/dn835050.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="262f6-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="262f6-245">其他案例</span><span class="sxs-lookup"><span data-stu-id="262f6-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="262f6-246">Web 服務需要多個輸入</span><span class="sxs-lookup"><span data-stu-id="262f6-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="262f6-247">如果 Web 服務接受多個輸入，請使用 **webServiceInputs** 屬性，而不要使用 **webServiceInput**。</span><span class="sxs-lookup"><span data-stu-id="262f6-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="262f6-248">**webServiceInputs** 所參考的資料集也必須包含在活動的 **inputs** 中。</span><span class="sxs-lookup"><span data-stu-id="262f6-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="262f6-249">在您的 Azure ML 實驗中，Web 服務輸入和輸出連接埠及全域參數有您可以自訂的預設名稱 ("input1"、"input2")。</span><span class="sxs-lookup"><span data-stu-id="262f6-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="262f6-250">您用於 webServiceInputs、webServiceOutputs 及 globalParameters 設定的名稱必須與實驗中的名稱完全相同。</span><span class="sxs-lookup"><span data-stu-id="262f6-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="262f6-251">您可以檢視您 Azure ML 端點之 [批次執行說明] 頁面上的範例要求承載，來確認預期的對應。</span><span class="sxs-lookup"><span data-stu-id="262f6-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="262f6-252">Web 服務不需要輸入</span><span class="sxs-lookup"><span data-stu-id="262f6-252">Web Service does not require an input</span></span>
<span data-ttu-id="262f6-253">Azure ML 批次執行 Web 服務可用來執行任何可能不需要任何輸入的工作流程，例如 R 或 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="262f6-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="262f6-254">或者，您也可以使用不會公開任何 GlobalParameters 的讀取器模組來設定實驗。</span><span class="sxs-lookup"><span data-stu-id="262f6-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="262f6-255">在此情況下，AzureMLBatchExecution 活動的設定如下：</span><span class="sxs-lookup"><span data-stu-id="262f6-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="262f6-256">Web 服務不需要輸入/輸出</span><span class="sxs-lookup"><span data-stu-id="262f6-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="262f6-257">Azure ML 批次執行 Web 服務可能未設定任何 Web 服務輸出。</span><span class="sxs-lookup"><span data-stu-id="262f6-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="262f6-258">在此範例中，沒有任何 Web 服務輸入或輸出，也不會設定任何 GlobalParameters。</span><span class="sxs-lookup"><span data-stu-id="262f6-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="262f6-259">仍會在活動本身設定輸出，但不會將它指定為 webServiceOutput。</span><span class="sxs-lookup"><span data-stu-id="262f6-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="262f6-260">Web 服務會使用讀取器和寫入器，而且只有在其他活動皆成功時，才會執行活動</span><span class="sxs-lookup"><span data-stu-id="262f6-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="262f6-261">Azure ML Web 服務的讀取器和寫入器模組可能會設定為不一定要利用任何 GlobalParameters 來執行。</span><span class="sxs-lookup"><span data-stu-id="262f6-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="262f6-262">但是，您可能想要在管線中內嵌服務呼叫來使用資料集相依性，只有在完成一些上游處理之後，才會叫用該服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="262f6-263">您也可以在使用此方法完成批次執行之後觸發一些其他動作。</span><span class="sxs-lookup"><span data-stu-id="262f6-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="262f6-264">在此情況下，您可以使用活動輸入和輸出來表達相依性，而不需將它們任一個命名為 Web 服務輸入或輸出。</span><span class="sxs-lookup"><span data-stu-id="262f6-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="262f6-265">**心得** 如下︰</span><span class="sxs-lookup"><span data-stu-id="262f6-265">The **takeaways** are:</span></span>

* <span data-ttu-id="262f6-266">如果您的實驗端點使用 webServiceInput：它可透過 Blob 資料集來表示，並且會包含於活動輸入以及 webServiceInput 屬性中。</span><span class="sxs-lookup"><span data-stu-id="262f6-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="262f6-267">否則，即會省略 webServiceInput 屬性。</span><span class="sxs-lookup"><span data-stu-id="262f6-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="262f6-268">如果您的實驗端點使用 webServiceOutput：它們可透過 Blob 資料集來表示，並且會包含於活動輸出以及 webServicepOutputs 屬性中。</span><span class="sxs-lookup"><span data-stu-id="262f6-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="262f6-269">活動輸出和 webServiceOutputs 會以此實驗中的每個輸出名稱來對應。</span><span class="sxs-lookup"><span data-stu-id="262f6-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="262f6-270">否則，即會省略 webServiceOutputs 屬性。</span><span class="sxs-lookup"><span data-stu-id="262f6-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="262f6-271">如果您的實驗端點會公開 globalParameter，則會在活動 globalParameters 屬性中提供它們以做為金鑰值組。</span><span class="sxs-lookup"><span data-stu-id="262f6-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="262f6-272">否則，即會省略 globalParameters 屬性。</span><span class="sxs-lookup"><span data-stu-id="262f6-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="262f6-273">金鑰會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="262f6-273">The keys are case-sensitive.</span></span> <span data-ttu-id="262f6-274">[Azure Data Factory 函式](data-factory-functions-variables.md) 可能會在值中使用。</span><span class="sxs-lookup"><span data-stu-id="262f6-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="262f6-275">您可以將額外的資料集包含於活動輸入和輸出屬性中，而不需在活動的 typeProperties 中加以參考。</span><span class="sxs-lookup"><span data-stu-id="262f6-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="262f6-276">這些資料集會使用配量相依性來管理執行，但其他的則會被 AzureMLBatchExecution 活動所忽略。</span><span class="sxs-lookup"><span data-stu-id="262f6-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="262f6-277">使用更新資源活動來更新模型</span><span class="sxs-lookup"><span data-stu-id="262f6-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="262f6-278">完成重新訓練之後，您可以使用「Azure ML 更新資源活動」，使用新訓練的模型來更新評分 Web 服務 (以 Web 服務公開的預測實驗)。</span><span class="sxs-lookup"><span data-stu-id="262f6-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="262f6-279">如需詳細資料，請參閱[使用更新資源活動更新模型](data-factory-azure-ml-update-resource-activity.md)一文。</span><span class="sxs-lookup"><span data-stu-id="262f6-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="262f6-280">讀取器和寫入器模組</span><span class="sxs-lookup"><span data-stu-id="262f6-280">Reader and Writer Modules</span></span>
<span data-ttu-id="262f6-281">使用 Azure SQL 讀取器和寫入器，是常見的 Web 服務參數使用案例。</span><span class="sxs-lookup"><span data-stu-id="262f6-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="262f6-282">讀取器模組可用來將資料從 Azure Machine Learning Studio 外部的資料管理服務載入至實驗。</span><span class="sxs-lookup"><span data-stu-id="262f6-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="262f6-283">寫入器模組則用來將資料從實驗儲存至 Azure Machine Learning Studio 外部的資料管理服務。</span><span class="sxs-lookup"><span data-stu-id="262f6-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="262f6-284">如需 Azure Blob/Azure SQL 讀取器/寫入器的詳細資料，請參閱 MSDN Library 上的[讀取器](https://msdn.microsoft.com/library/azure/dn905997.aspx)和[寫入器](https://msdn.microsoft.com/library/azure/dn905984.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="262f6-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="262f6-285">上一節中的範例已使用 Azure Blob 讀取器與 Azure Blob 寫入器。</span><span class="sxs-lookup"><span data-stu-id="262f6-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="262f6-286">本節討論如何使用 Azure SQL 讀取器和 Azure SQL 寫入器。</span><span class="sxs-lookup"><span data-stu-id="262f6-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="262f6-287">常見問題集</span><span class="sxs-lookup"><span data-stu-id="262f6-287">Frequently asked questions</span></span>
<span data-ttu-id="262f6-288">**問：** 我擁有巨量資料管線所產生的多個檔案。</span><span class="sxs-lookup"><span data-stu-id="262f6-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="262f6-289">我可以使用 AzureMLBatchExecution 活動來處理所有檔案嗎？</span><span class="sxs-lookup"><span data-stu-id="262f6-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="262f6-290">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="262f6-290">**A:** Yes.</span></span> <span data-ttu-id="262f6-291">如需詳細資料，請參閱 **使用讀取器模組讀取 Azure Blob 中多個檔案的資料** 一節。</span><span class="sxs-lookup"><span data-stu-id="262f6-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="262f6-292">AzureML 批次計分活動</span><span class="sxs-lookup"><span data-stu-id="262f6-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="262f6-293">如果您使用 **AzureMLBatchScoring** 活動來與 Azure Machine Learning 整合，建議您使用最新的 **AzureMLBatchExecution** 活動。</span><span class="sxs-lookup"><span data-stu-id="262f6-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="262f6-294">2015 年 8 月發行的 Azure SDK 和 Azure PowerShell 中導入了 AzureMLBatchExecution 活動。</span><span class="sxs-lookup"><span data-stu-id="262f6-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="262f6-295">如果您想要繼續使用 AzureMLBatchScoring 活動，請繼續閱讀本節。</span><span class="sxs-lookup"><span data-stu-id="262f6-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="262f6-296">使用 Azure 儲存體進行輸入/輸出的 AzureML 批次計分活動</span><span class="sxs-lookup"><span data-stu-id="262f6-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="262f6-297">Web 服務參數</span><span class="sxs-lookup"><span data-stu-id="262f6-297">Web Service Parameters</span></span>
<span data-ttu-id="262f6-298">若要指定 Web 服務參數的值，請將 **typeProperties** 區段新增至管線 JSON 中的 **AzureMLBatchScoringActivty** 區段，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="262f6-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="262f6-299">您也可以使用 [Data Factory 函式](data-factory-functions-variables.md) 傳遞 Web 服務參數的值，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="262f6-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="262f6-300">Web 服務參數區分大小寫，因此，請確定您在活動 JSON 中所指定的名稱符合 Web 服務所公開的名稱。</span><span class="sxs-lookup"><span data-stu-id="262f6-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="262f6-301">另請參閱</span><span class="sxs-lookup"><span data-stu-id="262f6-301">See Also</span></span>
* [<span data-ttu-id="262f6-302">Azure 部落格文章：開始使用 Azure Data Factory 和 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="262f6-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
