---
title: "使用 Azure Data Factory aaaCreate 預測的資料管線 |Microsoft 文件"
description: "描述如何 toocreate 建立預測管線使用 Azure Data Factory 和 Azure Machine Learning"
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
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="8536f-103">使用 Azure Machine Learning 和 Azure Data Factory 來建立預測管線</span><span class="sxs-lookup"><span data-stu-id="8536f-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="8536f-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="8536f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="8536f-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="8536f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="8536f-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="8536f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="8536f-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="8536f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="8536f-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="8536f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="8536f-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="8536f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="8536f-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="8536f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="8536f-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="8536f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="8536f-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="8536f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="8536f-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="8536f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="8536f-114">簡介</span><span class="sxs-lookup"><span data-stu-id="8536f-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="8536f-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8536f-115">Azure Machine Learning</span></span>
<span data-ttu-id="8536f-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)可讓您 toobuild 測試和部署的預測分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="8536f-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="8536f-117">從高階觀點而言，由下列三個步驟完成這個動作：</span><span class="sxs-lookup"><span data-stu-id="8536f-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="8536f-118">**建立訓練實驗**。</span><span class="sxs-lookup"><span data-stu-id="8536f-118">**Create a training experiment**.</span></span> <span data-ttu-id="8536f-119">您可以使用 hello Azure ML Studio，以進行此步驟。</span><span class="sxs-lookup"><span data-stu-id="8536f-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="8536f-120">hello ML studio 是共同作業視覺式開發環境，您使用 tootrain 和測試模型使用定型資料的預測分析。</span><span class="sxs-lookup"><span data-stu-id="8536f-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="8536f-121">**將它轉換 tooa 預測實驗**。</span><span class="sxs-lookup"><span data-stu-id="8536f-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="8536f-122">一旦您的模型已定型使用現有的資料，而且您準備好 toouse 它 tooscore 新資料準備，並簡化計分實驗。</span><span class="sxs-lookup"><span data-stu-id="8536f-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="8536f-123">**將其部署為 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="8536f-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="8536f-124">只要按一下，您就可以將評分實驗當做 Azure Web 服務發佈。</span><span class="sxs-lookup"><span data-stu-id="8536f-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="8536f-125">您可以傳送資料 tooyour 模型，透過此 web 服務端點，並接收從 hello 模型結果的預測。</span><span class="sxs-lookup"><span data-stu-id="8536f-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="8536f-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8536f-126">Azure Data Factory</span></span>
<span data-ttu-id="8536f-127">Data Factory 是以雲端為基礎的資料整合服務會協調及自動 hello**移動**和**轉換**的資料。</span><span class="sxs-lookup"><span data-stu-id="8536f-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="8536f-128">您可以建立資料整合方案使用 Azure Data Factory 可以擷取從各種資料存放區的資料，轉換/處理序 hello 資料，並將發行 hello 結果資料 toohello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="8536f-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="8536f-129">資料處理站服務 toocreate 資料管線，而移動和轉換資料，可讓您，然後再執行指定的排程 （每小時、 每天、 每週等等） 上的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="8536f-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="8536f-130">它也提供豐富的視覺效果 toodisplay hello 歷程和您的資料管線之間的相依性監視所有您在資料管線，從單一統一的檢視 tooeasily 找出問題並設定監視警示。</span><span class="sxs-lookup"><span data-stu-id="8536f-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="8536f-131">請參閱[簡介 tooAzure Data Factory](data-factory-introduction.md)和[建置您的第一個管線](data-factory-build-your-first-pipeline.md)文章 tooquickly 開始 hello Azure Data Factory 服務使用。</span><span class="sxs-lookup"><span data-stu-id="8536f-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="8536f-132">Data Factory 和 Machine Learning 一起合作</span><span class="sxs-lookup"><span data-stu-id="8536f-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="8536f-133">Azure Data Factory 可讓您 tooeasily 建立使用已發行的管線[Azure Machine Learning] [ azure-machine-learning] web 服務的預測分析。</span><span class="sxs-lookup"><span data-stu-id="8536f-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="8536f-134">使用 hello**批次執行活動**在 Azure Data Factory 管線中，您可以叫用 Azure ML web 服務 toomake 預測 hello 批次中的資料。</span><span class="sxs-lookup"><span data-stu-id="8536f-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="8536f-135">請參閱[叫用 Azure ML web 服務使用 hello 批次執行活動](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8536f-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="8536f-136">經過一段時間，在 hello Azure ML 計分實驗中的 hello 預測模型需要 toobe 原樣使用新的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="8536f-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="8536f-137">您可以執行下列步驟的 hello 重新訓練從 Data Factory 管線的 Azure ML 模型：</span><span class="sxs-lookup"><span data-stu-id="8536f-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="8536f-138">將 hello 定型實驗 （不預測實驗） 發佈為 web 服務。</span><span class="sxs-lookup"><span data-stu-id="8536f-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="8536f-139">您可以如同 tooexpose 預測實驗為 web 服務在 hello 前一個案例中，您 hello Azure ML Studio 中的這個步驟。</span><span class="sxs-lookup"><span data-stu-id="8536f-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="8536f-140">使用 hello Azure ML 批次執行活動 tooinvoke hello web 服務的 hello 定型實驗。</span><span class="sxs-lookup"><span data-stu-id="8536f-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="8536f-141">基本上，您可以使用 hello Azure ML 批次執行活動 tooinvoke web 服務的定型和計分 web 服務。</span><span class="sxs-lookup"><span data-stu-id="8536f-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="8536f-142">您完成定型之後，更新 hello 計分 web 服務 （預測實驗公開為 web 服務） 與 hello 定型新模型，使用 hello **Azure ML 更新資源活動**。</span><span class="sxs-lookup"><span data-stu-id="8536f-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="8536f-143">如需詳細資料，請參閱[使用更新資源活動更新模型](data-factory-azure-ml-update-resource-activity.md)一文。</span><span class="sxs-lookup"><span data-stu-id="8536f-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="8536f-144">使用批次執行活動來叫用 Web 服務</span><span class="sxs-lookup"><span data-stu-id="8536f-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="8536f-145">您使用 Azure Data Factory tooorchestrate 資料移動和處理，並執行使用 Azure Machine Learning 批次執行。</span><span class="sxs-lookup"><span data-stu-id="8536f-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="8536f-146">Hello 最上層步驟如下：</span><span class="sxs-lookup"><span data-stu-id="8536f-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="8536f-147">建立 Azure Machine Learning 連結服務。</span><span class="sxs-lookup"><span data-stu-id="8536f-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="8536f-148">您需要下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="8536f-148">You need hello following values:</span></span>

   1. <span data-ttu-id="8536f-149">**要求 URI** hello 批次執行應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="8536f-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="8536f-150">您可以找到要求的 URI hello 按一下 hello**批次執行**hello web 服務 頁面中的連結。</span><span class="sxs-lookup"><span data-stu-id="8536f-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="8536f-151">**API 金鑰**hello 已發行的 Azure Machine Learning web 服務。</span><span class="sxs-lookup"><span data-stu-id="8536f-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="8536f-152">您可以按一下 hello 已發行的 web 服務，以尋找 hello API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="8536f-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="8536f-153">使用 hello **AzureMLBatchExecution**活動。</span><span class="sxs-lookup"><span data-stu-id="8536f-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![機器學習服務儀表板](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![批次 URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="8536f-156">案例： 實驗使用 Web 服務輸入/輸出參考 Azure Blob 儲存體 toodata</span><span class="sxs-lookup"><span data-stu-id="8536f-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="8536f-157">在此案例中，hello Azure 機器學習 Web 服務會使用 Azure blob 儲存體中的檔案中的資料做出預測，並將 hello blob 儲存體中的 hello 預測結果。</span><span class="sxs-lookup"><span data-stu-id="8536f-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="8536f-158">hello 下列 JSON 定義與 AzureMLBatchExecution 活動的 Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="8536f-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="8536f-159">hello 活動有 hello 集**DecisionTreeInputBlob**做為輸入和**DecisionTreeResultBlob**做為 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="8536f-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="8536f-160">hello **DecisionTreeInputBlob**被當做輸入的 toohello web 服務，方法是使用 hello **webServiceInput** JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="8536f-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="8536f-161">hello **DecisionTreeResultBlob**被當做輸出 toohello Web 服務，方法是使用 hello **webServiceOutputs** JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="8536f-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="8536f-162">如果 hello web 服務接受多個輸入，使用 hello **webServiceInputs**屬性，而不要使用**webServiceInput**。</span><span class="sxs-lookup"><span data-stu-id="8536f-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="8536f-163">請參閱 hello [Web 服務需要多個輸入](#web-service-requires-multiple-inputs)> 一節使用 hello webServiceInputs 屬性的範例。</span><span class="sxs-lookup"><span data-stu-id="8536f-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="8536f-164">資料集所參考的 hello **webServiceInput**/**webServiceInputs**和**webServiceOutputs**屬性 (在**typeProperties**) 也必須包含在 hello 活動**輸入**和**輸出**。</span><span class="sxs-lookup"><span data-stu-id="8536f-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="8536f-165">在您的 Azure ML 實驗中，Web 服務輸入和輸出連接埠及全域參數有您可以自訂的預設名稱 ("input1"、"input2")。</span><span class="sxs-lookup"><span data-stu-id="8536f-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="8536f-166">您使用 webServiceInputs、 webServiceOutputs，和 globalParameters 設定 hello 名稱必須完全符合 hello 實驗中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="8536f-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="8536f-167">您可以在 Azure ML 端點 tooverify hello 預期對應 hello 批次執行說明頁面上檢視 hello 範例要求裝載。</span><span class="sxs-lookup"><span data-stu-id="8536f-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
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
> <span data-ttu-id="8536f-168">只有輸入及輸出的 hello AzureMLBatchExecution 活動可以傳遞為參數 toohello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8536f-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="8536f-169">例如，在 JSON 片段上方 hello，DecisionTreeInputBlob 是輸入的 toohello AzureMLBatchExecution 活動，以透過 webServiceInput 參數當做輸入的 toohello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="8536f-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="8536f-170">範例</span><span class="sxs-lookup"><span data-stu-id="8536f-170">Example</span></span>
<span data-ttu-id="8536f-171">這個範例會使用 Azure 儲存體 toohold 兩者 hello 輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="8536f-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="8536f-172">我們建議您通過 hello[建置您的第一個管線，使用 Data Factory] [ adf-build-1st-pipeline]再通過此範例中，教學課程。</span><span class="sxs-lookup"><span data-stu-id="8536f-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="8536f-173">在此範例中使用 hello Data Factory 編輯器 toocreate Data Factory 成品連結的服務、 資料集 （管線）。</span><span class="sxs-lookup"><span data-stu-id="8536f-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="8536f-174">為您的 **Azure 儲存體**建立**連結服務**。</span><span class="sxs-lookup"><span data-stu-id="8536f-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="8536f-175">如果 hello 輸入和輸出檔案位於不同的儲存體帳戶，您需要兩個連結的服務。</span><span class="sxs-lookup"><span data-stu-id="8536f-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="8536f-176">以下是 JSON 範例：</span><span class="sxs-lookup"><span data-stu-id="8536f-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="8536f-177">建立 hello**輸入**Azure Data Factory**資料集**。</span><span class="sxs-lookup"><span data-stu-id="8536f-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="8536f-178">與某些其他 Data Factory 資料集不同的是，這些資料集必須同時包含 **folderPath** 和 **fileName** 值。</span><span class="sxs-lookup"><span data-stu-id="8536f-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="8536f-179">您可以使用資料分割 toocause 每個批次執行 （每一個資料配量） tooprocess 或產生唯一的輸入和輸出檔。</span><span class="sxs-lookup"><span data-stu-id="8536f-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="8536f-180">您可能需要的 tooinclude 某些上游活動 tootransform hello 輸入 hello CSV 檔案格式，並將它放在每個配量的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8536f-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="8536f-181">在此情況下，您不會加入 hello**外部**和**externalData**顯示 hello 下列在範例中和您 DecisionTreeInputBlob 會 hello 的不同活動的輸出資料集設定。</span><span class="sxs-lookup"><span data-stu-id="8536f-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="8536f-182">您輸入的 csv 檔案必須有 hello 欄標題列。</span><span class="sxs-lookup"><span data-stu-id="8536f-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="8536f-183">如果您使用 hello**複製活動**toocreate/移動到 hello blob 儲存體 hello csv，您應該設定 hello 接收屬性**blobWriterAddHeader**太**true**。</span><span class="sxs-lookup"><span data-stu-id="8536f-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="8536f-184">例如：</span><span class="sxs-lookup"><span data-stu-id="8536f-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="8536f-185">如果 hello csv 檔案並沒有 hello 標頭資料列，您可能會看到下列錯誤 hello:**活動中的錯誤： 讀取字串時發生錯誤。非預期的權杖：StartObject。路徑 ''、行 1、位置 1**。</span><span class="sxs-lookup"><span data-stu-id="8536f-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="8536f-186">建立 hello**輸出**Azure Data Factory**資料集**。</span><span class="sxs-lookup"><span data-stu-id="8536f-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="8536f-187">這個範例會使用每個配量執行分割 toocreate 唯一的輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="8536f-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="8536f-188">沒有資料分割的 hello，hello 活動會覆寫 hello 檔。</span><span class="sxs-lookup"><span data-stu-id="8536f-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

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
4. <span data-ttu-id="8536f-189">建立**連結服務**的型別： **AzureMLLinkedService**、 提供 hello API 金鑰，以及模型批次執行 URL。</span><span class="sxs-lookup"><span data-stu-id="8536f-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="8536f-190">最後，撰寫一個包含 **AzureMLBatchExecution** 活動的管線。</span><span class="sxs-lookup"><span data-stu-id="8536f-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="8536f-191">在執行階段，管線會執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8536f-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="8536f-192">從您的輸入資料集取得 hello hello 輸入檔的位置。</span><span class="sxs-lookup"><span data-stu-id="8536f-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="8536f-193">叫用 hello Azure Machine Learning 批次執行應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="8536f-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="8536f-194">複製 hello 在輸出資料集中指定的批次執行輸出 toohello blob。</span><span class="sxs-lookup"><span data-stu-id="8536f-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8536f-195">AzureMLBatchExecution 活動可以有零個或多個輸入，以及一個或多個輸出。</span><span class="sxs-lookup"><span data-stu-id="8536f-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="8536f-196">**開始**和**結束**日期時間必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="8536f-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="8536f-197">例如：2014-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="8536f-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="8536f-198">hello**結束**次為選擇性。</span><span class="sxs-lookup"><span data-stu-id="8536f-198">hello **end** time is optional.</span></span> <span data-ttu-id="8536f-199">如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時。**"</span><span class="sxs-lookup"><span data-stu-id="8536f-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="8536f-200">無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。</span><span class="sxs-lookup"><span data-stu-id="8536f-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="8536f-201">如需 JSON 屬性的詳細資料，請參閱 [JSON 指令碼參考](https://msdn.microsoft.com/library/dn835050.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8536f-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="8536f-202">指定 hello AzureMLBatchExecution 活動的輸入是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="8536f-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="8536f-203">案例： 實驗不同的儲存體中使用讀取器/寫入器模組 toorefer toodata</span><span class="sxs-lookup"><span data-stu-id="8536f-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="8536f-204">建立 Azure ML 實驗時的另一個常見案例是 toouse 讀取器和寫入器模組。</span><span class="sxs-lookup"><span data-stu-id="8536f-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="8536f-205">hello 讀取器模組是使用的 tooload 實驗資料而 hello 編寫器模組 toosave 將實驗中的資料。</span><span class="sxs-lookup"><span data-stu-id="8536f-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="8536f-206">如需讀取器和寫入器模組的詳細資料，請參閱 MSDN Library 上的[讀取器](https://msdn.microsoft.com/library/azure/dn905997.aspx)和[寫入器](https://msdn.microsoft.com/library/azure/dn905984.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="8536f-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="8536f-207">使用時 hello 讀取器和寫入器模組，它是很好的作法 toouse 這些讀取器/寫入器模組的每一個屬性的 Web 服務參數。</span><span class="sxs-lookup"><span data-stu-id="8536f-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="8536f-208">這些 web 參數可讓您 tooconfigure hello 值在執行階段。</span><span class="sxs-lookup"><span data-stu-id="8536f-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="8536f-209">例如，建立實驗時，您可以利用讀取器模組使用 Azure SQL Database：XXX.database.windows.net。</span><span class="sxs-lookup"><span data-stu-id="8536f-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="8536f-210">Hello web 服務完成部署之後，您要的 hello web 服務 toospecify tooenable hello 取用者呼叫 YYY.database.windows.net 另一個 Azure SQL Server。</span><span class="sxs-lookup"><span data-stu-id="8536f-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="8536f-211">您可以使用 Web 服務參數 tooallow 設定此值 toobe。</span><span class="sxs-lookup"><span data-stu-id="8536f-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="8536f-212">Web 服務的輸入和輸出與 Web 服務參數不同。</span><span class="sxs-lookup"><span data-stu-id="8536f-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="8536f-213">在 hello 第一個案例中，您已經知道如何為 Azure ML Web 服務指定為輸入及輸出。</span><span class="sxs-lookup"><span data-stu-id="8536f-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="8536f-214">在此案例中，您可以將 Web 服務對應 tooproperties 的讀取器/寫入器模組的參數來傳遞。</span><span class="sxs-lookup"><span data-stu-id="8536f-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="8536f-215">讓我們看看使用 Web 服務參數的案例。</span><span class="sxs-lookup"><span data-stu-id="8536f-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="8536f-216">您有已部署的 Azure Machine Learning web 服務使用其中一個支援的 Azure Machine Learning hello 資料來源的讀取器模組 tooread 資料 (例如： Azure SQL Database)。</span><span class="sxs-lookup"><span data-stu-id="8536f-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="8536f-217">執行 hello 批次執行之後，hello 結果會寫入使用 (Azure SQL Database) 寫入器模組。</span><span class="sxs-lookup"><span data-stu-id="8536f-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="8536f-218">Hello 實驗中定義任何 web 服務輸入及輸出。</span><span class="sxs-lookup"><span data-stu-id="8536f-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="8536f-219">在此情況下，我們建議您設定 hello 讀取器和寫入器模組的相關 web 服務參數。</span><span class="sxs-lookup"><span data-stu-id="8536f-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="8536f-220">此設定可讓使用 hello AzureMLBatchExecution 活動時，設定模組 toobe hello 讀取器/寫入器。</span><span class="sxs-lookup"><span data-stu-id="8536f-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="8536f-221">您指定 Web 服務參數在 hello **globalParameters**區段 hello 活動 JSON 中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8536f-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="8536f-222">您也可以使用[Data Factory 函數](data-factory-functions-variables.md)傳遞值 hello Web 服務參數 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8536f-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="8536f-223">hello Web 服務參數會區分大小寫，因此請確定您指定在 hello 活動中的 hello 名稱 JSON 符合 hello hello Web 服務所公開的。</span><span class="sxs-lookup"><span data-stu-id="8536f-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="8536f-224">使用讀取器模組 tooread 資料從 Azure Blob 中的多個檔案</span><span class="sxs-lookup"><span data-stu-id="8536f-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="8536f-225">具有 Pig 和 Hive 等活動的巨量資料管線可以產生沒有副檔名的一個或多個輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="8536f-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="8536f-226">例如，當您指定外部的 Hive 資料表，hello hello 外部的 Hive 資料表的資料可以儲存在 Azure blob 儲存體以下列名稱 000000_0 hello。</span><span class="sxs-lookup"><span data-stu-id="8536f-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="8536f-227">您可以使用在實驗 tooread hello 讀取器模組的多個檔案，並用於預測。</span><span class="sxs-lookup"><span data-stu-id="8536f-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="8536f-228">當使用 hello 讀取器模組在 Azure 機器學習實驗中，您可以指定 Azure Blob 做為輸入。</span><span class="sxs-lookup"><span data-stu-id="8536f-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="8536f-229">hello Azure blob 儲存體中的 hello 檔案可以是 hello 輸出檔案 (範例： 000000_0)，在 HDInsight 上執行 Pig 和 Hive 指令碼所產生。</span><span class="sxs-lookup"><span data-stu-id="8536f-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="8536f-230">hello 讀取器模組可讓您 tooread 副檔名的檔案 （無） 藉由設定 hello**路徑 toocontainer、 目錄/blob**。</span><span class="sxs-lookup"><span data-stu-id="8536f-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="8536f-231">hello**路徑 toocontainer**點 toohello 容器和**目錄/blob**點 toofolder hello 檔案所在 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="8536f-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="8536f-232">也就是星號 hello \*)**指定所有 hello hello 容器/資料夾中的檔案 (也就是資料/aggregateddata/年 = 6-2014年/月 /\*)** hello 實驗中讀取。</span><span class="sxs-lookup"><span data-stu-id="8536f-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Azure Blob 屬性](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="8536f-234">範例</span><span class="sxs-lookup"><span data-stu-id="8536f-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="8536f-235">AzureMLBatchExecution 活動使用 Web 服務參數的管線</span><span class="sxs-lookup"><span data-stu-id="8536f-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="8536f-236">在上述範例 JSON hello:</span><span class="sxs-lookup"><span data-stu-id="8536f-236">In hello above JSON example:</span></span>

* <span data-ttu-id="8536f-237">hello 部署 Azure 機器學習 Web 服務會使用讀取器和寫入器模組 tooread/寫入資料，從 / tooan Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="8536f-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="8536f-238">此 Web 服務會公開下列四個參數的 hello： 資料庫伺服器名稱、 資料庫名稱、 伺服器使用者帳戶名稱，以及伺服器的使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="8536f-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="8536f-239">**開始**和**結束**日期時間必須是 [ISO 格式](http://en.wikipedia.org/wiki/ISO_8601)。</span><span class="sxs-lookup"><span data-stu-id="8536f-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="8536f-240">例如：2014-10-14T16:32:41Z。</span><span class="sxs-lookup"><span data-stu-id="8536f-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="8536f-241">hello**結束**次為選擇性。</span><span class="sxs-lookup"><span data-stu-id="8536f-241">hello **end** time is optional.</span></span> <span data-ttu-id="8536f-242">如果您未指定值為 hello**結束**屬性，它會計算為"**start + 48 小時。**"</span><span class="sxs-lookup"><span data-stu-id="8536f-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="8536f-243">無限期地指定 toorun hello 管線**9999-09-09**為 hello hello 值**結束**屬性。</span><span class="sxs-lookup"><span data-stu-id="8536f-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="8536f-244">如需 JSON 屬性的詳細資料，請參閱 [JSON 指令碼參考](https://msdn.microsoft.com/library/dn835050.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8536f-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="8536f-245">其他案例</span><span class="sxs-lookup"><span data-stu-id="8536f-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="8536f-246">Web 服務需要多個輸入</span><span class="sxs-lookup"><span data-stu-id="8536f-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="8536f-247">如果 hello web 服務接受多個輸入，使用 hello **webServiceInputs**屬性，而不要使用**webServiceInput**。</span><span class="sxs-lookup"><span data-stu-id="8536f-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="8536f-248">資料集所參考的 hello **webServiceInputs**也必須包含在 hello 活動**輸入**。</span><span class="sxs-lookup"><span data-stu-id="8536f-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="8536f-249">在您的 Azure ML 實驗中，Web 服務輸入和輸出連接埠及全域參數有您可以自訂的預設名稱 ("input1"、"input2")。</span><span class="sxs-lookup"><span data-stu-id="8536f-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="8536f-250">您使用 webServiceInputs、 webServiceOutputs，和 globalParameters 設定 hello 名稱必須完全符合 hello 實驗中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="8536f-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="8536f-251">您可以在 Azure ML 端點 tooverify hello 預期對應 hello 批次執行說明頁面上檢視 hello 範例要求裝載。</span><span class="sxs-lookup"><span data-stu-id="8536f-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="8536f-252">Web 服務不需要輸入</span><span class="sxs-lookup"><span data-stu-id="8536f-252">Web Service does not require an input</span></span>
<span data-ttu-id="8536f-253">Azure ML 批次執行 web 服務可以是任何工作流程使用的 toorun，例如 R 或 Python 指令碼，可能不需要任何輸入。</span><span class="sxs-lookup"><span data-stu-id="8536f-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="8536f-254">或者，hello 實驗可能不會公開任何 GlobalParameters 讀取器模組以進行設定。</span><span class="sxs-lookup"><span data-stu-id="8536f-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="8536f-255">在此情況下，hello AzureMLBatchExecution 活動會設定如下：</span><span class="sxs-lookup"><span data-stu-id="8536f-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="8536f-256">Web 服務不需要輸入/輸出</span><span class="sxs-lookup"><span data-stu-id="8536f-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="8536f-257">hello Azure ML 批次執行 web 服務可能沒有設定任何 Web 服務輸出。</span><span class="sxs-lookup"><span data-stu-id="8536f-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="8536f-258">在此範例中，沒有任何 Web 服務輸入或輸出，也不會設定任何 GlobalParameters。</span><span class="sxs-lookup"><span data-stu-id="8536f-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="8536f-259">仍有本身，hello 活動上設定的輸出，但它不指定為 webServiceOutput。</span><span class="sxs-lookup"><span data-stu-id="8536f-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="8536f-260">Web 服務會使用讀取器和寫入器，和其他活動成功時，才 hello 活動執行</span><span class="sxs-lookup"><span data-stu-id="8536f-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="8536f-261">hello Azure ML web 服務讀取器和寫入器模組可能會設定的 toorun，不論任何 GlobalParameters。</span><span class="sxs-lookup"><span data-stu-id="8536f-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="8536f-262">不過，您可能想 tooembed 服務呼叫某些上游處理完成時，才會使用資料集相依性 tooinvoke hello 服務在管線中。</span><span class="sxs-lookup"><span data-stu-id="8536f-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="8536f-263">使用這種方式完成 hello 批次執行之後，您也可以觸發某些其他動作。</span><span class="sxs-lookup"><span data-stu-id="8536f-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="8536f-264">在此情況下，你可以使用活動輸入及輸出，但不命名它們其中任何一個為 Web 服務輸入或輸出的 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="8536f-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="8536f-265">hello**心得**是：</span><span class="sxs-lookup"><span data-stu-id="8536f-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="8536f-266">如果您的實驗端點使用 webServiceInput： 它由 blob 資料集，並納入 hello 活動輸入] 和 [hello webServiceInput 屬性。</span><span class="sxs-lookup"><span data-stu-id="8536f-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="8536f-267">否則，會省略 hello webServiceInput 屬性。</span><span class="sxs-lookup"><span data-stu-id="8536f-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="8536f-268">如果您的實驗端點使用 webServiceOutput(s)： 它們由 blob 資料集，且會包含在 hello 活動輸出以及 hello webServiceOutputs 屬性中。</span><span class="sxs-lookup"><span data-stu-id="8536f-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="8536f-269">hello 活動會輸出和 webServiceOutputs hello hello 實驗中的每個輸出名稱對應。</span><span class="sxs-lookup"><span data-stu-id="8536f-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="8536f-270">否則，會省略 hello webServiceOutputs 屬性。</span><span class="sxs-lookup"><span data-stu-id="8536f-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="8536f-271">如果您的實驗端點公開 globalParameter(s)，會收到 hello 活動 globalParameters 屬性中做為索引鍵的值組。</span><span class="sxs-lookup"><span data-stu-id="8536f-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="8536f-272">否則，會省略 hello globalParameters 屬性。</span><span class="sxs-lookup"><span data-stu-id="8536f-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="8536f-273">hello 索引鍵是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8536f-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="8536f-274">[Azure Data Factory 函數](data-factory-functions-variables.md)可能用於 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8536f-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="8536f-275">額外的資料集可能包含在 hello 活動輸入及輸出屬性，不含 hello 活動 typeProperties 中所參考。</span><span class="sxs-lookup"><span data-stu-id="8536f-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="8536f-276">這些資料集控管使用配量相依性的執行，但 hello AzureMLBatchExecution 活動會加以忽略。</span><span class="sxs-lookup"><span data-stu-id="8536f-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="8536f-277">使用更新資源活動來更新模型</span><span class="sxs-lookup"><span data-stu-id="8536f-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="8536f-278">您完成定型之後，更新 hello 計分 web 服務 （預測實驗公開為 web 服務） 與 hello 定型新模型，使用 hello **Azure ML 更新資源活動**。</span><span class="sxs-lookup"><span data-stu-id="8536f-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="8536f-279">如需詳細資料，請參閱[使用更新資源活動更新模型](data-factory-azure-ml-update-resource-activity.md)一文。</span><span class="sxs-lookup"><span data-stu-id="8536f-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="8536f-280">讀取器和寫入器模組</span><span class="sxs-lookup"><span data-stu-id="8536f-280">Reader and Writer Modules</span></span>
<span data-ttu-id="8536f-281">使用 Web 服務參數的常見案例是 hello 使用 Azure SQL 讀取器和寫入器。</span><span class="sxs-lookup"><span data-stu-id="8536f-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="8536f-282">hello 讀取器模組已從 Azure Machine Learning Studio 以外的資料管理服務的實驗使用的 tooload 資料。</span><span class="sxs-lookup"><span data-stu-id="8536f-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="8536f-283">hello 寫入器模組是 toosave 資料到 Azure Machine Learning Studio 以外的資料管理服務將實驗中。</span><span class="sxs-lookup"><span data-stu-id="8536f-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="8536f-284">如需 Azure Blob/Azure SQL 讀取器/寫入器的詳細資料，請參閱 MSDN Library 上的[讀取器](https://msdn.microsoft.com/library/azure/dn905997.aspx)和[寫入器](https://msdn.microsoft.com/library/azure/dn905984.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="8536f-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="8536f-285">hello 前一節中的 hello 範例使用 hello Azure Blob 讀取器和 Azure Blob 的寫入器。</span><span class="sxs-lookup"><span data-stu-id="8536f-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="8536f-286">本節討論如何使用 Azure SQL 讀取器和 Azure SQL 寫入器。</span><span class="sxs-lookup"><span data-stu-id="8536f-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="8536f-287">常見問題集</span><span class="sxs-lookup"><span data-stu-id="8536f-287">Frequently asked questions</span></span>
<span data-ttu-id="8536f-288">**問：** 我擁有巨量資料管線所產生的多個檔案。</span><span class="sxs-lookup"><span data-stu-id="8536f-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="8536f-289">可以使用 hello AzureMLBatchExecution 活動 toowork 所有 hello 檔案嗎？</span><span class="sxs-lookup"><span data-stu-id="8536f-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="8536f-290">**答：** 是。</span><span class="sxs-lookup"><span data-stu-id="8536f-290">**A:** Yes.</span></span> <span data-ttu-id="8536f-291">請參閱 hello**使用讀取器模組 tooread 資料從 Azure Blob 中的多個檔案**如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8536f-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="8536f-292">AzureML 批次計分活動</span><span class="sxs-lookup"><span data-stu-id="8536f-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="8536f-293">如果您使用 hello **AzureMLBatchScoring**活動 toointegrate 與 Azure Machine Learning 中的，我們建議您使用 hello 最新**AzureMLBatchExecution**活動。</span><span class="sxs-lookup"><span data-stu-id="8536f-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="8536f-294">hello AzureMLBatchExecution 活動 hello 2015 年 8 月發行的 Azure SDK 和 Azure PowerShell 中引進。</span><span class="sxs-lookup"><span data-stu-id="8536f-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="8536f-295">如果您想 toocontinue 使用 hello AzureMLBatchScoring 活動，請繼續閱讀本節。</span><span class="sxs-lookup"><span data-stu-id="8536f-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="8536f-296">使用 Azure 儲存體進行輸入/輸出的 AzureML 批次計分活動</span><span class="sxs-lookup"><span data-stu-id="8536f-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="8536f-297">Web 服務參數</span><span class="sxs-lookup"><span data-stu-id="8536f-297">Web Service Parameters</span></span>
<span data-ttu-id="8536f-298">新增 Web 服務參數，toospecify 值**typeProperties**區段 toohello **AzureMLBatchScoringActivty** > 一節中 hello 管線 JSON hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8536f-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="8536f-299">您也可以使用[Data Factory 函數](data-factory-functions-variables.md)傳遞值 hello Web 服務參數 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8536f-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="8536f-300">hello Web 服務參數會區分大小寫，因此請確定您指定在 hello 活動中的 hello 名稱 JSON 符合 hello hello Web 服務所公開的。</span><span class="sxs-lookup"><span data-stu-id="8536f-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="8536f-301">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8536f-301">See Also</span></span>
* [<span data-ttu-id="8536f-302">Azure 部落格文章：開始使用 Azure Data Factory 和 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8536f-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
