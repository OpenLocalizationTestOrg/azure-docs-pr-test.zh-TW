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
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>使用更新資源活動更新 Azure Machine Learning 模型

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 活動](data-factory-hive-activity.md) 
> * [Pig 活動](data-factory-pig-activity.md)
> * [MapReduce 活動](data-factory-map-reduce.md)
> * [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
> * [Spark 活動](data-factory-spark.md)
> * [Machine Learning Batch 執行活動](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 更新資源活動](data-factory-azure-ml-update-resource-activity.md)
> * [預存程序活動](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)
> * [.NET 自訂活動](data-factory-use-custom-activities.md)

本文補充 hello 主要 Azure Data Factory-Azure Machine Learning 整合文件：[建立預測管線使用 Azure Machine Learning 和 Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md)。 如果您尚未這樣做，請檢閱 hello 主要文件，再閱讀這篇文章。 

## <a name="overview"></a>概觀
經過一段時間，在 hello Azure ML 計分實驗中的 hello 預測模型需要 toobe 原樣使用新的輸入資料集。 您完成定型之後，您會想要計分 web 服務以 hello tooupdate hello 重新定型 ML 模型。 hello 的一般步驟 tooenable 重新訓練及更新透過 web 服務的 Azure ML 模型如下：

1. 在 [Azure ML Studio](https://studio.azureml.net)中建立實驗。
2. 當您滿意 hello 模型時，請使用 Azure ML Studio toopublish web 服務，這兩個 hello**定型實驗**和計分 /**預測實驗**。

hello 下表說明此範例中使用的 hello web 服務。  如需詳細資訊，請參閱 [以程式設計方式重新定型機器學習服務模型](../machine-learning/machine-learning-retrain-models-programmatically.md) 。

- **訓練 Web 服務** - 接收訓練資料並產生已訓練的模型。 hello 輸出 hello 重新訓練是 Azure Blob 儲存體.ilearner 檔案。 hello**預設端點**為您當您發行 hello 訓練試驗為 web 服務會自動建立。 您可以建立多個端點，但是 hello 範例使用 hello 預設端點。
- **評分 Web 服務** - 接收未標記的資料範例並進行預測。 hello 輸出的預測可能會有各種形式，例如.csv 檔案或 Azure SQL database，依據 hello 實驗 hello 設定中的資料列。 當您發佈為 web 服務的 hello 預測實驗 hello 預設端點將自動為您中建立。 

hello 圖描述 hello 定型和計分在 Azure ML 中端點之間的關聯性。

![Web 服務](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

您可以叫用 hello**定型 web 服務**使用 hello **Azure ML 批次執行活動**。 叫用訓練 Web 服務與叫用 Azure ML Web 服務 (評分 Web 服務) 以便進行資料評分相同。 hello 先前各節封面 tooinvoke Azure ML web 服務，從 Azure Data Factory 管線詳細的方式。 

您可以叫用 hello**計分 web 服務**使用 hello **Azure ML 更新資源活動**tooupdate hello web 服務與 hello 定型新模型。 下列範例中的 hello 提供連結的服務定義： 

## <a name="scoring-web-service-is-a-classic-web-service"></a>評分 Web 服務是傳統的 Web 服務
如果計分 web 服務的 hello**傳統 web 服務**，第二個建立 hello**非預設和更新端點**使用 hello [Azure 入口網站](https://manage.windowsazure.com)。 如需相關步驟，請參閱[建立端點](../machine-learning/machine-learning-create-endpoint.md)一文。 建立 hello 非預設更新端點之後，請勿 hello 下列步驟：

* 按一下**批次執行**tooget hello URI 值為 hello **mlEndpoint** JSON 屬性。
* 按一下**更新資源**連結 tooget hello URI 值為 hello **updateResourceEndpoint** JSON 屬性。 hello API 金鑰是本身 hello 端點頁面上 （在 hello 右下角）。

![可更新端點](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

下列範例中的 hello 提供 hello AzureML 連結服務的範例 JSON 定義。 hello 連結的服務會使用 hello apiKey 進行驗證。  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>評分 Web 服務是 Azure Resource Manager Web 服務 
如果 hello web 服務會公開的 Azure 資源管理員端點的 web 服務的 hello 新類型，您不需要 tooadd hello 第二個**非預設**端點。 hello **updateResourceEndpoint** hello 中連結的服務是 hello 格式： 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

您可以為預留位置 hello URL 中取得值，查詢在 hello hello web 服務時[Azure 機器學習 Web 服務網站](https://services.azureml.net/)。 hello 新的更新資源端點類型需要 AAD (Azure Active Directory) 權杖。 在 AzureML 連結服務中指定 **servicePrincipalId** 和 **servicePrincipalKey**。 請參閱[toocreate 服務主體的方式，並指派權限 toomanage Azure 資源](../azure-resource-manager/resource-group-create-service-principal-portal.md)。 以下是 AzureML 連結服務定義範例︰ 

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

hello 下列案例提供更多詳細資料。 其中包含從 Azure Data Factory 管線重新訓練和更新 Azure ML 模型的範例。

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>案例：重新訓練和更新 Azure ML 模型
本節提供使用 hello 範例管線**Azure ML 批次執行活動**tooretrain 模型。 hello 管線也會使用 hello **Azure ML 更新資源活動**tooupdate hello 計分 web 服務中的 hello 模型。 hello 章節也會提供所有的 JSON 片段 hello 連結的服務、 資料集，以及在 hello 範例中的管線。

以下是 hello 範例管線的 hello 圖表檢視。 如您所見，hello Azure ML 批次執行活動就會接受 hello 訓練輸入，並且會產生定型輸出 （iLearner 檔案）。 hello Azure ML 更新資源活動會採用此定型輸出，並更新 hello hello 計分 web 服務端點中的模型。 hello 更新資源活動不會產生任何輸出。 hello placeholderBlob 是所需的 hello Azure Data Factory 服務 toorun hello 管線只要 dummy 輸出資料集。

![管線圖](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Azure Blob 儲存體連結服務：
hello Azure 儲存體保存 hello 下列資料：

* 訓練資料。 hello hello Azure ML 訓練 web 服務的輸入的資料。  
* iLearner 檔案。 hello 來自 hello Azure ML 訓練 web 服務的輸出。 這個檔案也是 hello 輸入的 toohello 更新資源活動。  

以下是 hello 連結服務的 hello 範例 JSON 定義：

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

### <a name="training-input-dataset"></a>訓練輸入資料集：
hello 下列資料集代表 hello Azure ML 訓練 web 服務的 hello 輸入的定型資料。 hello Azure ML 批次執行的活動會使用此資料集做為輸入。

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

### <a name="training-output-dataset"></a>訓練輸出資料集：
hello 下列資料集代表 hello 輸出 iLearner 檔案從 hello Azure ML 訓練 web 服務。 hello Azure ML 批次執行的活動會產生此資料集。 此資料集也是 hello 輸入的 toohello Azure ML 更新資源活動。

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Azure ML 訓練端點的連結服務
下列 JSON 片段 hello 定義點 toohello hello 訓練 web 服務的預設端點的 Azure Machine Learning 連結服務。

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

在**Azure ML Studio**，執行下列 tooget 值為 hello **mlEndpoint**和**apiKey**:

1. 按一下**WEB 服務**hello 左側功能表上。
2. 按一下 hello**定型 web 服務**hello 的 web 服務的清單中。
3. 按一下 [複製] 下一步太**API 金鑰**文字方塊。 在 hello 剪貼簿貼入 hello 資料 Factory JSON 編輯器 hello 索引鍵。
4. 在 hello **Azure ML studio**，按一下 **批次執行**連結。
5. 複製 hello**要求 URI**從 hello**要求**區段，並將它貼到 hello 資料 Factory JSON 編輯器。   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Azure ML 可更新評分端點的連結服務：
下列 JSON 片段 hello 定義點 toohello hello 計分 web 服務的非預設更新端點的 Azure Machine Learning 連結服務。  

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

### <a name="placeholder-output-dataset"></a>預留位置輸出資料集：
hello Azure ML 更新資源活動不會產生任何輸出。 不過，Azure Data Factory 需要管線的輸出資料集 toodrive hello 排程。 因此，我們在此範例中使用虛擬/預留位置資料集。  

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

### <a name="pipeline"></a>管線
hello 管線有兩個活動： **AzureMLBatchExecution**和**AzureMLUpdateResource**。 hello Azure ML 批次執行的活動會接受做為輸入的 hello 定型資料，並產生 ilearner 做為檔案，做為輸出。 hello 活動與 hello 輸入培訓資料叫用 hello 訓練 web 服務 （定型實驗公開為 web 服務），並從 hello webservice 接收 hello ilearner 做為檔。 hello placeholderBlob 是所需的 hello Azure Data Factory 服務 toorun hello 管線只要 dummy 輸出資料集。

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
