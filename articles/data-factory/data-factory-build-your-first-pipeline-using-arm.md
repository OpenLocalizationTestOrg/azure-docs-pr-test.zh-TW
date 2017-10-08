---
title: "aaaBuild 您第一次的 data factory （Resource Manager 範本） |Microsoft 文件"
description: "在本教學課程中，您會使用 Azure Resource Manager 範本來建立範例 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>教學課程：使用 Azure Resource Manager 範本建置您的第一個 Azure Data Factory
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-build-your-first-pipeline.md)
> * [Azure 入口網站](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 範本](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

在本文中，您使用 Azure Resource Manager 範本 toocreate 第一個 Azure data factory。 toodo hello 教學課程中使用其他工具/Sdk，從 hello 下拉式清單選取其中一個 hello 選項。

在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。 此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。 hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。 

> [!NOTE]
> 在此教學課程中的 hello 資料管線轉換輸入的資料 tooproduce 輸出資料。 如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
> 
> 在此教學課程中的 hello 管線有一個活動的型別： HDInsightHive。 一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。 

## <a name="prerequisites"></a>必要條件
* 閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。
* 遵循指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)文章 tooinstall 最新版的 Azure PowerShell 在您的電腦上。
* 請參閱[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)toolearn 關於 Azure Resource Manager 範本。 

## <a name="in-this-tutorial"></a>本教學課程內容
| 實體 | 說明 |
| --- | --- |
| Azure 儲存體連結服務 |連結您的 Azure 儲存體帳戶 toohello data factory。 hello 保存 hello hello 管線，在此範例中的輸入和輸出資料的 Azure 儲存體帳戶。 |
| HDInsight 隨選連結服務 |指定 HDInsight 叢集 toohello 資料處理站的連結。 hello 叢集會自動為您 tooprocess 資料建立，而且 hello 處理完成之後刪除。 |
| Azure Blob 輸入資料集 |是指 toohello Azure 儲存體連結服務。 hello 連結的服務是指 tooan Azure 儲存體帳戶和 hello Azure Blob 資料集指定 hello 儲存體保存 hello 輸入的資料中的 hello 容器、 資料夾和檔案名稱。 |
| Azure Blob 輸出資料集 |是指 toohello Azure 儲存體連結服務。 hello 連結的服務是指 tooan Azure 儲存體帳戶和 hello Azure Blob 資料集指定保存 hello 輸出資料 hello 儲存體中的 hello 容器、 資料夾和檔案名稱。 |
| Data Pipeline |hello 管線有一個活動的型別 HDInsightHive，這會消耗 hello 輸入資料集並產生 hello 輸出資料集。 |

資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 兩種活動類型︰[資料移動活動](data-factory-data-movement-activities.md)和[資料轉換活動](data-factory-data-transformation-activities.md)。 在本教學課程中，您可以使用一個活動建立管線 (Hive 活動)。

hello 下節提供 hello 完成資源管理員範本，您可以快速地執行透過 hello 教學課程和測試 hello 範本定義 Data Factory 實體。 toounderstand 如何定義每個 Data Factory 實體，請參閱[hello 範本中的 Data Factory 實體](#data-factory-entities-in-the-template)> 一節。

## <a name="data-factory-json-template"></a>Data Factory JSON 範本
是用於定義 data factory hello 最上層資源管理員範本： 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
建立名為的 JSON 檔案**ADFTutorialARM.json**中**C:\ADFGetStarted**資料夾以 hello 下列內容：

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> 您可以找到另一個 Resource Manager 範本的範例，以在[教學課程︰使用 Azure Resource Manager 範本建立管線與複製活動](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)上建立 Azure Data Factory。  
> 
> 

## <a name="parameters-json"></a>參數 JSON
建立名為的 JSON 檔案**ADFTutorialARM Parameters.json**包含 hello Azure Resource Manager 範本的參數。  

> [!IMPORTANT]
> 指定 hello 名稱和您的 Azure 儲存體帳戶金鑰 hello **storageAccountName**和**storageAccountKey**此參數檔案中的參數。 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> 您可能需要進行開發，個別參數的 JSON 檔案測試，而且您可以搭配使用的實際執行環境的 hello 相同資料 Factory JSON 範本。 使用 Power Shell 指令碼，您可以在這些環境中自動部署 Data Factory 實體。 
> 
> 

## <a name="create-data-factory"></a>建立 Data Factory
1. 啟動**Azure PowerShell**和 hello 執行下列命令： 
   * 執行下列命令的 hello 並輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * 執行下列命令 tooview hello 這個帳戶的所有 hello 訂用帳戶。
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * 執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。 此訂用帳戶應 hello 與 hello hello Azure 入口網站中使用相同。
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. 執行下列命令使用您在步驟 1 中建立的 hello Resource Manager 範本的 toodeploy Data Factory 實體的 hello。 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>監視管線
1. 登入 toohello 之後[Azure 入口網站](https://portal.azure.com/)，按一下 **瀏覽**選取**Data factory**。
     ![瀏覽 Data Factory](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. 在 hello **Data Factory**刀鋒視窗中，按一下 hello 資料處理站 (**TutorialFactoryARM**) 所建立。    
3. 在 hello **Data Factory**按一下刀鋒視窗中針對您的 data factory**圖表**。

     ![圖表磚](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. 在 hello**圖表檢視**、 看見 hello 管線的概觀，以及資料集用在本教學課程。
   
   ![圖表檢視](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. 在 hello 圖表檢視中，按兩下 hello 資料集**AzureBlobOutput**。 您會看到目前正在處理該 hello 扇區。
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. 當處理完成時，請參閱中的 hello 扇區**準備**狀態。 建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。 因此，預期 hello 管線 tootake**大約 30 分鐘**tooprocess hello 配量。
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. 當 hello 配量處於**準備**狀態，請檢查 hello **partitioneddata**資料夾中 hello **adfgetstarted** hello 您 blob 儲存體容器中的輸出資料。  

請參閱[監視資料集和管線](data-factory-monitor-manage-pipelines.md)如需如何 toouse hello Azure 入口網站的刀鋒 toomonitor hello 管線和資料集您已建立本教學課程中的指示。

您也可以使用監視和管理應用程式 toomonitor 資料管線。 請參閱[監視和管理使用監視應用程式的 Azure Data Factory 管線](data-factory-monitor-manage-app.md)如需使用 hello 應用程式詳細資料。 

> [!IMPORTANT]
> 已成功處理 hello 配量時，取得刪除 hello 輸入的檔。 因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello hello adfgetstarted 容器的輸入的檔 (input.log) toohello inputdata 資料夾。
> 
> 

## <a name="data-factory-entities-in-hello-template"></a>Hello 範本中的 data Factory 實體
### <a name="define-data-factory"></a>定義資料處理站
Hello 下列範例所示，您可以定義在 hello Resource Manager 範本中的 data factory:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
hello dataFactoryName 定義為： 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
它是唯一的字串 hello 資源群組 id。  

### <a name="defining-data-factory-entities"></a>定義 Data Factory 實體
hello 下列 Data Factory 實體範本中所定義 hello JSON: 

* [Azure 儲存體連結服務](#azure-storage-linked-service)
* [HDInsight 隨選連結服務](#hdinsight-on-demand-linked-service)
* [Azure Blob 輸入資料集](#azure-blob-input-dataset)
* [Azure Blob 輸出資料集](#azure-blob-output-dataset)
* [具有複製活動的管線](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務
您可以在此區段中指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。 請參閱[Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性使用 toodefine Azure 儲存體連結服務。 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
hello **connectionString**使用 hello storageAccountName 及 storageAccountKey 參數。 hello 使用組態檔傳遞這些參數的值。 hello 定義也會使用變數： azureStroageLinkedService 和 dataFactoryName hello 範本中定義。 

#### <a name="hdinsight-on-demand-linked-service"></a>HDInsight 隨選連結服務
請參閱[計算連結的服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)文件如需詳細資訊 JSON 屬性使用 toodefine HDInsight 視連結的服務。  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
請注意下列點 hello: 

* hello Data Factory 建立**linux**上方 JSON hello 與您的 HDInsight 叢集。 如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。 
* 您可以使用 **自己的 HDInsight 叢集** ，不必使用隨選的 HDInsight 叢集。 如需詳細資訊，請參閱 [HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 。
* hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。 HDInsight 刪除 hello 叢集時，不會刪除此容器。 這是設計的行為。 HDInsight 叢集隨 HDInsight 連結服務，以建立每次配量需要處理現有的叢集即時除非 toobe (**timeToLive**) 和 hello 處理完成時刪除。
  
    隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。 如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。 這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。 使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。

如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。

#### <a name="azure-blob-input-dataset"></a>Azure Blob 輸入資料集
您指定 blob 容器、 資料夾和檔案，其中包含 hello 輸入的資料的 hello 的名稱。 請參閱[Azure Blob 資料集屬性](data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
這個定義會使用下列參數的範本中定義參數的 hello: blobContainer，inputBlobFolder，和 inputBlobName。 

#### <a name="azure-blob-output-dataset"></a>Azure Blob 輸出資料集
您指定 blob 容器和保存 hello 輸出資料之資料夾的 hello 的名稱。 請參閱[Azure Blob 資料集屬性](data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

這個定義會使用下列參數 hello 參數範本中定義的 hello: blobContainer 和 outputBlobFolder。 

#### <a name="data-pipeline"></a>Data Pipeline
您可以定義在隨選 Azure HDInsight 叢集上執行 Hive 指令碼以轉換資料的管線。 請參閱[管線 JSON](data-factory-create-pipelines.md#pipeline-json)如需 JSON 用項目 toodefine 管線，以在此範例的描述。 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a>重複使用 hello 範本
在 hello 教學課程中，您可以建立 Data Factory 實體和傳遞的參數值的範本定義的範本。 toouse hello 相同範本 toodeploy Data Factory 實體 toodifferent 環境，您建立參數檔案的每個環境，並部署 toothat 環境時，請使用它。     

範例：  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
請注意，第一個命令會使用參數的 hello hello 開發環境的 hello 測試環境中，第二個檔案，與 hello hello 的生產環境的第三個。  

您也可以重複使用 hello 範本 tooperform 重複的工作。 比方說，需要 toocreate 許多 data factory，其中包含一個或多個實作的管線 hello 相同邏輯，但每個資料處理站會使用不同 Azure 儲存體和 Azure SQL Database 帳戶。 在此案例中，您可以使用 hello 相同的範本在 hello 與不同的參數相同的環境 （開發、 測試或生產） 檔案 toocreate data factory。 

## <a name="resource-manager-template-for-creating-a-gateway"></a>可供建立閘道的 Resource Manager 範本
以下是範例資源管理員範本在 hello 回中建立邏輯的閘道。 在內部部署電腦或 Azure IaaS VM 上安裝閘道器並使用金鑰的 Data Factory 服務註冊 hello 閘道。 如需詳細資訊，請參閱 [在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
此範本會利用名為 GatewayUsingARM 的閘道建立名為 GatewayUsingArmDF 的 Data Factory。 

## <a name="see-also"></a>另請參閱
| 主題 | 說明 |
|:--- |:--- |
| [管線](data-factory-create-pipelines.md) |這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 端對端資料驅動型工作流程或商務案例。 |
| [資料集](data-factory-create-datasets.md) |本文協助您了解 Azure Data Factory 中的資料集。 |
| [排程和執行](data-factory-scheduling-and-execution.md) |本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。 |
| [使用監視應用程式來監視和管理管線](data-factory-monitor-manage-app.md) |本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。 |

