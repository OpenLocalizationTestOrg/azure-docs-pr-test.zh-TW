---
title: "使用 Azure Data Factory 更新 Machine Learning 模型 | Microsoft Docs"
description: "說明如何使用 Azure Data Factory 和 Azure Machine Learning 建立預測管線"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: e31a7a59d14de4382190b39bd70f3ddf6cf673ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="9e3cb-103">使用更新資源活動更新 Azure Machine Learning 模型</span><span class="sxs-lookup"><span data-stu-id="9e3cb-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9e3cb-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="9e3cb-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9e3cb-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9e3cb-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9e3cb-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9e3cb-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9e3cb-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9e3cb-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9e3cb-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9e3cb-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="9e3cb-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="9e3cb-114">本文補充主要 Azure Data Factory - Azure Machine Learning 整合文件︰[使用 Azure Machine Learning 和 Azure Data Factory 建立預測管線](data-factory-azure-ml-batch-execution-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="9e3cb-115">如果您尚未檢閱主要文件，請在閱讀這篇文章之前先這麼做。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="9e3cb-116">概觀</span><span class="sxs-lookup"><span data-stu-id="9e3cb-116">Overview</span></span>
<span data-ttu-id="9e3cb-117">經過一段時間，必須使用新的輸入資料集重新訓練 Azure ML 評分實驗中的預測模型。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="9e3cb-118">完成重新訓練之後，您想要使用已重新訓練的 ML 模型來更新評分 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="9e3cb-119">透過 Web 服務啟用重新訓練和更新 Azure ML 模型的一般步驟如下：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="9e3cb-120">在 [Azure ML Studio](https://studio.azureml.net)中建立實驗。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="9e3cb-121">當您對模型感到滿意時，請使用 Azure ML Studio 對**訓練實驗**和評分/**預測實驗**發佈 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="9e3cb-122">下表說明本範例中使用的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="9e3cb-123">如需詳細資訊，請參閱 [以程式設計方式重新定型機器學習服務模型](../machine-learning/machine-learning-retrain-models-programmatically.md) 。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="9e3cb-124">**訓練 Web 服務** - 接收訓練資料並產生已訓練的模型。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="9e3cb-125">重新訓練的輸出是 Azure Blob 儲存體中的 .ilearner 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="9e3cb-126">當您將訓練實驗發佈為 Web 服務時，系統會自動為您建立 **預設端點** 。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="9e3cb-127">您可以建立多個端點，但此範例僅使用預設端點。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="9e3cb-128">**評分 Web 服務** - 接收未標記的資料範例並進行預測。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="9e3cb-129">預測的輸出可能有各種形式，例如 .csv 檔案或 Azure SQL Database 中的資料列 (視實驗的組態而定)。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="9e3cb-130">當您將預測實驗發佈為 Web 服務時，系統會自動為您建立預設端點。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="9e3cb-131">下圖描述 Azure ML 中訓練與評分端點之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![Web 服務](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="9e3cb-133">您可以使用 [AzureML Batch 執行活動] 來叫用**訓練 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="9e3cb-134">叫用訓練 Web 服務與叫用 Azure ML Web 服務 (評分 Web 服務) 以便進行資料評分相同。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="9e3cb-135">上述各節詳細說明如何從 Azure Data Factory 管線叫用 Azure ML Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="9e3cb-136">您可以使用 [Azure ML 更新資源活動] 來叫用**評分 Web 服務**，進而以新訓練的模型更新 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="9e3cb-137">下列範例提供連結的服務定義︰</span><span class="sxs-lookup"><span data-stu-id="9e3cb-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="9e3cb-138">評分 Web 服務是傳統的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="9e3cb-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="9e3cb-139">如果評分 Web 服務是「傳統 Web 服務」，請使用 [Azure 入口網站](https://manage.windowsazure.com)，建立第二個「非預設且可更新的端點」。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="9e3cb-140">如需相關步驟，請參閱[建立端點](../machine-learning/machine-learning-create-endpoint.md)一文。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="9e3cb-141">建立非預設的可更新端點之後，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="9e3cb-142">按一下 [批次執行] 以取得 **mlEndpoint** JSON 屬性的 URI 值。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="9e3cb-143">按一下 [更新資源] 連結以取得 **updateResourceEndpoint** JSON 屬性的 URI 值。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="9e3cb-144">API 金鑰本身位於端點頁面 (位於右下角)。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![可更新端點](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="9e3cb-146">下列範例提供 AzureML 連結服務的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="9e3cb-147">連結服務使用 apiKey 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-147">The linked service uses the apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="9e3cb-148">評分 Web 服務是 Azure Resource Manager Web 服務</span><span class="sxs-lookup"><span data-stu-id="9e3cb-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="9e3cb-149">如果 Web 服務是會公開 Azure Resource Manager 端點的新 Web 服務類型，您不需要新增第二個「非預設」端點。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="9e3cb-150">連結服務中 **updateResourceEndpoint** 的格式如下︰</span><span class="sxs-lookup"><span data-stu-id="9e3cb-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="9e3cb-151">在 [Azure Machine Learning Web 服務入口網站](https://services.azureml.net/)上查詢 Web 服務時，您可以取得 URL 中預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="9e3cb-152">新的更新資源端點類型需要 AAD (Azure Active Directory) 權杖。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="9e3cb-153">在 AzureML 連結服務中指定 **servicePrincipalId** 和 **servicePrincipalKey**。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="9e3cb-154">請參閱[如何建立服務主體及指派權限來管理 Azure 資源](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="9e3cb-155">以下是 AzureML 連結服務定義範例︰</span><span class="sxs-lookup"><span data-stu-id="9e3cb-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="9e3cb-156">下列案例提供更多詳細資料，</span><span class="sxs-lookup"><span data-stu-id="9e3cb-156">The following scenario provides more details.</span></span> <span data-ttu-id="9e3cb-157">其中包含從 Azure Data Factory 管線重新訓練和更新 Azure ML 模型的範例。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="9e3cb-158">案例：重新訓練和更新 Azure ML 模型</span><span class="sxs-lookup"><span data-stu-id="9e3cb-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="9e3cb-159">本節提供使用 **Azure ML 批次執行活動** 來重新訓練模型的範例管線。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="9e3cb-160">管線也會使用 **Azure ML 更新資源活動** 來更新評分 Web 服務中的模型。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="9e3cb-161">本節還會提供範例中所有連結服務、資料集和管線的 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="9e3cb-162">以下是範例管線的圖表檢視。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="9e3cb-163">如您所見，Azure ML 批次執行活動會採用訓練輸入並產生訓練輸出 (iLearner 檔案)。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="9e3cb-164">Azure ML 更新資源活動會採用此訓練輸出，並更新評分 Web 服務端點中的模型。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="9e3cb-165">更新資源活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="9e3cb-166">PlaceholderBlob 只是 Azure Data Factory 服務執行管線所需的虛擬輸出資料集而已。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![管線圖](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="9e3cb-168">Azure Blob 儲存體連結服務：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="9e3cb-169">Azure 儲存體會保留下列資料：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="9e3cb-170">訓練資料。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-170">training data.</span></span> <span data-ttu-id="9e3cb-171">Azure ML 訓練 Web 服務的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="9e3cb-172">iLearner 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-172">iLearner file.</span></span> <span data-ttu-id="9e3cb-173">Azure ML 訓練 Web 服務的輸出。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="9e3cb-174">此檔案也是更新資源活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="9e3cb-175">以下是連結服務的範例 JSON 定義：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-175">Here is the sample JSON definition of the linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="9e3cb-176">訓練輸入資料集：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-176">Training input dataset:</span></span>
<span data-ttu-id="9e3cb-177">下列資料集代表 Azure ML 訓練 Web 服務的輸入訓練資料。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="9e3cb-178">Azure ML 批次執行活動會以此資料集做為輸入。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a><span data-ttu-id="9e3cb-179">訓練輸出資料集：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-179">Training output dataset:</span></span>
<span data-ttu-id="9e3cb-180">下列資料集代表 Azure ML 訓練 Web 服務的輸出入 iLearner 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="9e3cb-181">Azure ML 批次執行活動會產生此資料集。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="9e3cb-182">此資料集同時也是 Azure ML 更新資源活動的輸入。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="9e3cb-183">Azure ML 訓練端點的連結服務</span><span class="sxs-lookup"><span data-stu-id="9e3cb-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="9e3cb-184">下列 JSON 程式碼片段定義的 Azure 機器學習連結服務可指向訓練 Web 服務的預設端點。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="9e3cb-185">在 [Azure ML Studio] 中，依下列方式取得 **mlEndpoint** 和 **apiKey** 的值：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="9e3cb-186">按一下左功能表中的 [ **Web 服務** ]。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="9e3cb-187">按一下 Web 服務清單中的 **訓練 Web 服務** 。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="9e3cb-188">按一下 [API 金鑰]  文字方塊旁的 [複製]。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="9e3cb-189">將剪貼簿中的金鑰貼到 Data Factory JSON 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="9e3cb-190">在 **Azure ML Studio** 中按一下 [批次執行] 連結。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="9e3cb-191">從 [要求] 區段複製 [要求 URI] 並將它貼到 Data Factory JSON 編輯器中。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="9e3cb-192">Azure ML 可更新評分端點的連結服務：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="9e3cb-193">下列 JSON 程式碼片段定義的 Azure 機器學習連結服務可指向評分 Web 服務的非預設可更新端點。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="9e3cb-194">預留位置輸出資料集：</span><span class="sxs-lookup"><span data-stu-id="9e3cb-194">Placeholder output dataset:</span></span>
<span data-ttu-id="9e3cb-195">Azure ML 更新資源活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="9e3cb-196">不過，Azure Data Factory 需要輸出資料集來驅動管線的排程。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="9e3cb-197">因此，我們在此範例中使用虛擬/預留位置資料集。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="9e3cb-198">管線</span><span class="sxs-lookup"><span data-stu-id="9e3cb-198">Pipeline</span></span>
<span data-ttu-id="9e3cb-199">管線有兩個活動：**AzureMLBatchExecution** 和 **AzureMLUpdateResource**。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="9e3cb-200">Azure ML 批次執行活動會以訓練資料做為輸入並產生 iLearner 檔案做為輸出。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="9e3cb-201">此活動會使用輸入訓練資料叫用訓練 Web 服務 (公開為 Web 服務的訓練實驗)，並從 Web 服務接收 iLearner 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="9e3cb-202">PlaceholderBlob 只是 Azure Data Factory 服務執行管線所需的虛擬輸出資料集而已。</span><span class="sxs-lookup"><span data-stu-id="9e3cb-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![管線圖](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
