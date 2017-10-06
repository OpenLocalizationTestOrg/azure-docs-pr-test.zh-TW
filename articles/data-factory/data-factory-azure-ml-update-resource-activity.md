---
title: "使用 Azure Data Factory aaaUpdate 機器學習模型 |Microsoft 文件"
description: "描述如何 toocreate 建立預測管線使用 Azure Data Factory 和 Azure Machine Learning"
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
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="ccfc3-103">使用更新資源活動更新 Azure Machine Learning 模型</span><span class="sxs-lookup"><span data-stu-id="ccfc3-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ccfc3-104">Hive 活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="ccfc3-105">Pig 活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ccfc3-106">MapReduce 活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ccfc3-107">Hadoop 串流活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ccfc3-108">Spark 活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ccfc3-109">Machine Learning Batch 執行活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ccfc3-110">Machine Learning 更新資源活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ccfc3-111">預存程序活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ccfc3-112">Data Lake Analytics U-SQL 活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ccfc3-113">.NET 自訂活動</span><span class="sxs-lookup"><span data-stu-id="ccfc3-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="ccfc3-114">本文補充 hello 主要 Azure Data Factory-Azure Machine Learning 整合文件：[建立預測管線使用 Azure Machine Learning 和 Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="ccfc3-115">如果您尚未這樣做，請檢閱 hello 主要文件，再閱讀這篇文章。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="ccfc3-116">概觀</span><span class="sxs-lookup"><span data-stu-id="ccfc3-116">Overview</span></span>
<span data-ttu-id="ccfc3-117">經過一段時間，在 hello Azure ML 計分實驗中的 hello 預測模型需要 toobe 原樣使用新的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="ccfc3-118">您完成定型之後，您會想要計分 web 服務以 hello tooupdate hello 重新定型 ML 模型。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="ccfc3-119">hello 的一般步驟 tooenable 重新訓練及更新透過 web 服務的 Azure ML 模型如下：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="ccfc3-120">在 [Azure ML Studio](https://studio.azureml.net)中建立實驗。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="ccfc3-121">當您滿意 hello 模型時，請使用 Azure ML Studio toopublish web 服務，這兩個 hello**定型實驗**和計分 /**預測實驗**。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="ccfc3-122">hello 下表說明此範例中使用的 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="ccfc3-123">如需詳細資訊，請參閱 [以程式設計方式重新定型機器學習服務模型](../machine-learning/machine-learning-retrain-models-programmatically.md) 。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="ccfc3-124">**訓練 Web 服務** - 接收訓練資料並產生已訓練的模型。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="ccfc3-125">hello 輸出 hello 重新訓練是 Azure Blob 儲存體.ilearner 檔案。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="ccfc3-126">hello**預設端點**為您當您發行 hello 訓練試驗為 web 服務會自動建立。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="ccfc3-127">您可以建立多個端點，但是 hello 範例使用 hello 預設端點。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="ccfc3-128">**評分 Web 服務** - 接收未標記的資料範例並進行預測。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="ccfc3-129">hello 輸出的預測可能會有各種形式，例如.csv 檔案或 Azure SQL database，依據 hello 實驗 hello 設定中的資料列。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="ccfc3-130">當您發佈為 web 服務的 hello 預測實驗 hello 預設端點將自動為您中建立。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="ccfc3-131">hello 圖描述 hello 定型和計分在 Azure ML 中端點之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![Web 服務](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="ccfc3-133">您可以叫用 hello**定型 web 服務**使用 hello **Azure ML 批次執行活動**。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="ccfc3-134">叫用訓練 Web 服務與叫用 Azure ML Web 服務 (評分 Web 服務) 以便進行資料評分相同。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="ccfc3-135">hello 先前各節封面 tooinvoke Azure ML web 服務，從 Azure Data Factory 管線詳細的方式。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="ccfc3-136">您可以叫用 hello**計分 web 服務**使用 hello **Azure ML 更新資源活動**tooupdate hello web 服務與 hello 定型新模型。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="ccfc3-137">下列範例中的 hello 提供連結的服務定義：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="ccfc3-138">評分 Web 服務是傳統的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="ccfc3-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="ccfc3-139">如果計分 web 服務的 hello**傳統 web 服務**，第二個建立 hello**非預設和更新端點**使用 hello [Azure 入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ccfc3-140">如需相關步驟，請參閱[建立端點](../machine-learning/machine-learning-create-endpoint.md)一文。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="ccfc3-141">建立 hello 非預設更新端點之後，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="ccfc3-142">按一下**批次執行**tooget hello URI 值為 hello **mlEndpoint** JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="ccfc3-143">按一下**更新資源**連結 tooget hello URI 值為 hello **updateResourceEndpoint** JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="ccfc3-144">hello API 金鑰是本身 hello 端點頁面上 （在 hello 右下角）。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![可更新端點](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="ccfc3-146">下列範例中的 hello 提供 hello AzureML 連結服務的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="ccfc3-147">hello 連結的服務會使用 hello apiKey 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-147">hello linked service uses hello apiKey for authentication.</span></span>  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="ccfc3-148">評分 Web 服務是 Azure Resource Manager Web 服務</span><span class="sxs-lookup"><span data-stu-id="ccfc3-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="ccfc3-149">如果 hello web 服務會公開的 Azure 資源管理員端點的 web 服務的 hello 新類型，您不需要 tooadd hello 第二個**非預設**端點。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="ccfc3-150">hello **updateResourceEndpoint** hello 中連結的服務是 hello 格式：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="ccfc3-151">您可以為預留位置 hello URL 中取得值，查詢在 hello hello web 服務時[Azure 機器學習 Web 服務網站](https://services.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="ccfc3-152">hello 新的更新資源端點類型需要 AAD (Azure Active Directory) 權杖。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="ccfc3-153">在 AzureML 連結服務中指定 **servicePrincipalId** 和 **servicePrincipalKey**。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="ccfc3-154">請參閱[toocreate 服務主體的方式，並指派權限 toomanage Azure 資源](../azure-resource-manager/resource-group-create-service-principal-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="ccfc3-155">以下是 AzureML 連結服務定義範例︰</span><span class="sxs-lookup"><span data-stu-id="ccfc3-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
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

<span data-ttu-id="ccfc3-156">hello 下列案例提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-156">hello following scenario provides more details.</span></span> <span data-ttu-id="ccfc3-157">其中包含從 Azure Data Factory 管線重新訓練和更新 Azure ML 模型的範例。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="ccfc3-158">案例：重新訓練和更新 Azure ML 模型</span><span class="sxs-lookup"><span data-stu-id="ccfc3-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="ccfc3-159">本節提供使用 hello 範例管線**Azure ML 批次執行活動**tooretrain 模型。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="ccfc3-160">hello 管線也會使用 hello **Azure ML 更新資源活動**tooupdate hello 計分 web 服務中的 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="ccfc3-161">hello 章節也會提供所有的 JSON 片段 hello 連結的服務、 資料集，以及在 hello 範例中的管線。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="ccfc3-162">以下是 hello 範例管線的 hello 圖表檢視。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="ccfc3-163">如您所見，hello Azure ML 批次執行活動就會接受 hello 訓練輸入，並且會產生定型輸出 （iLearner 檔案）。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="ccfc3-164">hello Azure ML 更新資源活動會採用此定型輸出，並更新 hello hello 計分 web 服務端點中的模型。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="ccfc3-165">hello 更新資源活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="ccfc3-166">hello placeholderBlob 是所需的 hello Azure Data Factory 服務 toorun hello 管線只要 dummy 輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![管線圖](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="ccfc3-168">Azure Blob 儲存體連結服務：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="ccfc3-169">hello Azure 儲存體保存 hello 下列資料：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="ccfc3-170">訓練資料。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-170">training data.</span></span> <span data-ttu-id="ccfc3-171">hello hello Azure ML 訓練 web 服務的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="ccfc3-172">iLearner 檔案。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-172">iLearner file.</span></span> <span data-ttu-id="ccfc3-173">hello 來自 hello Azure ML 訓練 web 服務的輸出。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="ccfc3-174">這個檔案也是 hello 輸入的 toohello 更新資源活動。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="ccfc3-175">以下是 hello 連結服務的 hello 範例 JSON 定義：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-175">Here is hello sample JSON definition of hello linked service:</span></span>

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

### <a name="training-input-dataset"></a><span data-ttu-id="ccfc3-176">訓練輸入資料集：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-176">Training input dataset:</span></span>
<span data-ttu-id="ccfc3-177">hello 下列資料集代表 hello Azure ML 訓練 web 服務的 hello 輸入的定型資料。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="ccfc3-178">hello Azure ML 批次執行的活動會使用此資料集做為輸入。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

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

### <a name="training-output-dataset"></a><span data-ttu-id="ccfc3-179">訓練輸出資料集：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-179">Training output dataset:</span></span>
<span data-ttu-id="ccfc3-180">hello 下列資料集代表 hello 輸出 iLearner 檔案從 hello Azure ML 訓練 web 服務。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="ccfc3-181">hello Azure ML 批次執行的活動會產生此資料集。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="ccfc3-182">此資料集也是 hello 輸入的 toohello Azure ML 更新資源活動。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="ccfc3-183">Azure ML 訓練端點的連結服務</span><span class="sxs-lookup"><span data-stu-id="ccfc3-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="ccfc3-184">下列 JSON 片段 hello 定義點 toohello hello 訓練 web 服務的預設端點的 Azure Machine Learning 連結服務。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

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

<span data-ttu-id="ccfc3-185">在**Azure ML Studio**，執行下列 tooget 值為 hello **mlEndpoint**和**apiKey**:</span><span class="sxs-lookup"><span data-stu-id="ccfc3-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="ccfc3-186">按一下**WEB 服務**hello 左側功能表上。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="ccfc3-187">按一下 hello**定型 web 服務**hello 的 web 服務的清單中。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="ccfc3-188">按一下 [複製] 下一步太**API 金鑰**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="ccfc3-189">在 hello 剪貼簿貼入 hello 資料 Factory JSON 編輯器 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="ccfc3-190">在 hello **Azure ML studio**，按一下 **批次執行**連結。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="ccfc3-191">複製 hello**要求 URI**從 hello**要求**區段，並將它貼到 hello 資料 Factory JSON 編輯器。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="ccfc3-192">Azure ML 可更新評分端點的連結服務：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="ccfc3-193">下列 JSON 片段 hello 定義點 toohello hello 計分 web 服務的非預設更新端點的 Azure Machine Learning 連結服務。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

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

### <a name="placeholder-output-dataset"></a><span data-ttu-id="ccfc3-194">預留位置輸出資料集：</span><span class="sxs-lookup"><span data-stu-id="ccfc3-194">Placeholder output dataset:</span></span>
<span data-ttu-id="ccfc3-195">hello Azure ML 更新資源活動不會產生任何輸出。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="ccfc3-196">不過，Azure Data Factory 需要管線的輸出資料集 toodrive hello 排程。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="ccfc3-197">因此，我們在此範例中使用虛擬/預留位置資料集。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="ccfc3-198">管線</span><span class="sxs-lookup"><span data-stu-id="ccfc3-198">Pipeline</span></span>
<span data-ttu-id="ccfc3-199">hello 管線有兩個活動： **AzureMLBatchExecution**和**AzureMLUpdateResource**。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="ccfc3-200">hello Azure ML 批次執行的活動會接受做為輸入的 hello 定型資料，並產生 ilearner 做為檔案，做為輸出。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="ccfc3-201">hello 活動與 hello 輸入培訓資料叫用 hello 訓練 web 服務 （定型實驗公開為 web 服務），並從 hello webservice 接收 hello ilearner 做為檔。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="ccfc3-202">hello placeholderBlob 是所需的 hello Azure Data Factory 服務 toorun hello 管線只要 dummy 輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="ccfc3-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

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
