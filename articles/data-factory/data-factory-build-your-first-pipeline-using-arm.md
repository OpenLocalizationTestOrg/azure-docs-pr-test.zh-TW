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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="13ef3-103">教學課程：使用 Azure Resource Manager 範本建置您的第一個 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="13ef3-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13ef3-104">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="13ef3-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="13ef3-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="13ef3-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="13ef3-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13ef3-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="13ef3-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13ef3-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="13ef3-108">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="13ef3-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="13ef3-109">REST API</span><span class="sxs-lookup"><span data-stu-id="13ef3-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="13ef3-110">在本文中，您使用 Azure Resource Manager 範本 toocreate 第一個 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="13ef3-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="13ef3-111">toodo hello 教學課程中使用其他工具/Sdk，從 hello 下拉式清單選取其中一個 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="13ef3-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="13ef3-112">在此教學課程中的 hello 管線有一個活動： **HDInsight Hive 活動**。</span><span class="sxs-lookup"><span data-stu-id="13ef3-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="13ef3-113">此活動會在轉換輸入資料 tooproduce 輸出資料的 Azure HDInsight 叢集上執行 hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="13ef3-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="13ef3-114">hello 管線是排程的 toorun，每個月之間 hello 指定開始和結束時間之後。</span><span class="sxs-lookup"><span data-stu-id="13ef3-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="13ef3-115">在此教學課程中的 hello 資料管線轉換輸入的資料 tooproduce 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="13ef3-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="13ef3-116">如需如何使用 Azure Data Factory，toocopy 資料，請參閱[教學課程： 將資料從 Blob 儲存體 tooSQL 資料庫複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="13ef3-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="13ef3-117">在此教學課程中的 hello 管線有一個活動的型別： HDInsightHive。</span><span class="sxs-lookup"><span data-stu-id="13ef3-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="13ef3-118">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="13ef3-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="13ef3-119">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="13ef3-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="13ef3-120">如需詳細資訊，請參閱 [Data Factory 排程和執行](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="13ef3-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="13ef3-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="13ef3-121">Prerequisites</span></span>
* <span data-ttu-id="13ef3-122">閱讀[教學課程概觀](data-factory-build-your-first-pipeline.md)文件，以及完成 hello**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="13ef3-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="13ef3-123">遵循指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)文章 tooinstall 最新版的 Azure PowerShell 在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="13ef3-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="13ef3-124">請參閱[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)toolearn 關於 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="13ef3-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="13ef3-125">本教學課程內容</span><span class="sxs-lookup"><span data-stu-id="13ef3-125">In this tutorial</span></span>
| <span data-ttu-id="13ef3-126">實體</span><span class="sxs-lookup"><span data-stu-id="13ef3-126">Entity</span></span> | <span data-ttu-id="13ef3-127">說明</span><span class="sxs-lookup"><span data-stu-id="13ef3-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="13ef3-128">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="13ef3-128">Azure Storage linked service</span></span> |<span data-ttu-id="13ef3-129">連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="13ef3-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="13ef3-130">hello 保存 hello hello 管線，在此範例中的輸入和輸出資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="13ef3-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="13ef3-131">HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="13ef3-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="13ef3-132">指定 HDInsight 叢集 toohello 資料處理站的連結。</span><span class="sxs-lookup"><span data-stu-id="13ef3-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="13ef3-133">hello 叢集會自動為您 tooprocess 資料建立，而且 hello 處理完成之後刪除。</span><span class="sxs-lookup"><span data-stu-id="13ef3-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="13ef3-134">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="13ef3-134">Azure Blob input dataset</span></span> |<span data-ttu-id="13ef3-135">是指 toohello Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="13ef3-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="13ef3-136">hello 連結的服務是指 tooan Azure 儲存體帳戶和 hello Azure Blob 資料集指定 hello 儲存體保存 hello 輸入的資料中的 hello 容器、 資料夾和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="13ef3-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="13ef3-137">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="13ef3-137">Azure Blob output dataset</span></span> |<span data-ttu-id="13ef3-138">是指 toohello Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="13ef3-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="13ef3-139">hello 連結的服務是指 tooan Azure 儲存體帳戶和 hello Azure Blob 資料集指定保存 hello 輸出資料 hello 儲存體中的 hello 容器、 資料夾和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="13ef3-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="13ef3-140">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="13ef3-140">Data pipeline</span></span> |<span data-ttu-id="13ef3-141">hello 管線有一個活動的型別 HDInsightHive，這會消耗 hello 輸入資料集並產生 hello 輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="13ef3-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="13ef3-142">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="13ef3-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="13ef3-143">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="13ef3-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="13ef3-144">兩種活動類型︰[資料移動活動](data-factory-data-movement-activities.md)和[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="13ef3-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="13ef3-145">在本教學課程中，您可以使用一個活動建立管線 (Hive 活動)。</span><span class="sxs-lookup"><span data-stu-id="13ef3-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="13ef3-146">hello 下節提供 hello 完成資源管理員範本，您可以快速地執行透過 hello 教學課程和測試 hello 範本定義 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="13ef3-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="13ef3-147">toounderstand 如何定義每個 Data Factory 實體，請參閱[hello 範本中的 Data Factory 實體](#data-factory-entities-in-the-template)> 一節。</span><span class="sxs-lookup"><span data-stu-id="13ef3-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="13ef3-148">Data Factory JSON 範本</span><span class="sxs-lookup"><span data-stu-id="13ef3-148">Data Factory JSON template</span></span>
<span data-ttu-id="13ef3-149">是用於定義 data factory hello 最上層資源管理員範本：</span><span class="sxs-lookup"><span data-stu-id="13ef3-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="13ef3-150">建立名為的 JSON 檔案**ADFTutorialARM.json**中**C:\ADFGetStarted**資料夾以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="13ef3-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

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
> <span data-ttu-id="13ef3-151">您可以找到另一個 Resource Manager 範本的範例，以在[教學課程︰使用 Azure Resource Manager 範本建立管線與複製活動](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)上建立 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="13ef3-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="13ef3-152">參數 JSON</span><span class="sxs-lookup"><span data-stu-id="13ef3-152">Parameters JSON</span></span>
<span data-ttu-id="13ef3-153">建立名為的 JSON 檔案**ADFTutorialARM Parameters.json**包含 hello Azure Resource Manager 範本的參數。</span><span class="sxs-lookup"><span data-stu-id="13ef3-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="13ef3-154">指定 hello 名稱和您的 Azure 儲存體帳戶金鑰 hello **storageAccountName**和**storageAccountKey**此參數檔案中的參數。</span><span class="sxs-lookup"><span data-stu-id="13ef3-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="13ef3-155">您可能需要進行開發，個別參數的 JSON 檔案測試，而且您可以搭配使用的實際執行環境的 hello 相同資料 Factory JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="13ef3-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="13ef3-156">使用 Power Shell 指令碼，您可以在這些環境中自動部署 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="13ef3-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="13ef3-157">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="13ef3-157">Create data factory</span></span>
1. <span data-ttu-id="13ef3-158">啟動**Azure PowerShell**和 hello 執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="13ef3-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="13ef3-159">執行下列命令的 hello 並輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="13ef3-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="13ef3-160">執行下列命令 tooview hello 這個帳戶的所有 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="13ef3-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="13ef3-161">執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="13ef3-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="13ef3-162">此訂用帳戶應 hello 與 hello hello Azure 入口網站中使用相同。</span><span class="sxs-lookup"><span data-stu-id="13ef3-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="13ef3-163">執行下列命令使用您在步驟 1 中建立的 hello Resource Manager 範本的 toodeploy Data Factory 實體的 hello。</span><span class="sxs-lookup"><span data-stu-id="13ef3-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="13ef3-164">監視管線</span><span class="sxs-lookup"><span data-stu-id="13ef3-164">Monitor pipeline</span></span>
1. <span data-ttu-id="13ef3-165">登入 toohello 之後[Azure 入口網站](https://portal.azure.com/)，按一下 **瀏覽**選取**Data factory**。</span><span class="sxs-lookup"><span data-stu-id="13ef3-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="13ef3-166">![瀏覽 Data Factory](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="13ef3-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="13ef3-167">在 hello **Data Factory**刀鋒視窗中，按一下 hello 資料處理站 (**TutorialFactoryARM**) 所建立。</span><span class="sxs-lookup"><span data-stu-id="13ef3-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="13ef3-168">在 hello **Data Factory**按一下刀鋒視窗中針對您的 data factory**圖表**。</span><span class="sxs-lookup"><span data-stu-id="13ef3-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![圖表磚](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="13ef3-170">在 hello**圖表檢視**、 看見 hello 管線的概觀，以及資料集用在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="13ef3-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![圖表檢視](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="13ef3-172">在 hello 圖表檢視中，按兩下 hello 資料集**AzureBlobOutput**。</span><span class="sxs-lookup"><span data-stu-id="13ef3-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="13ef3-173">您會看到目前正在處理該 hello 扇區。</span><span class="sxs-lookup"><span data-stu-id="13ef3-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="13ef3-175">當處理完成時，請參閱中的 hello 扇區**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="13ef3-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="13ef3-176">建立隨選 HDInsight 叢集通常需要一些時間 (大約 20 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="13ef3-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="13ef3-177">因此，預期 hello 管線 tootake**大約 30 分鐘**tooprocess hello 配量。</span><span class="sxs-lookup"><span data-stu-id="13ef3-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Dataset](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="13ef3-179">當 hello 配量處於**準備**狀態，請檢查 hello **partitioneddata**資料夾中 hello **adfgetstarted** hello 您 blob 儲存體容器中的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="13ef3-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="13ef3-180">請參閱[監視資料集和管線](data-factory-monitor-manage-pipelines.md)如需如何 toouse hello Azure 入口網站的刀鋒 toomonitor hello 管線和資料集您已建立本教學課程中的指示。</span><span class="sxs-lookup"><span data-stu-id="13ef3-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="13ef3-181">您也可以使用監視和管理應用程式 toomonitor 資料管線。</span><span class="sxs-lookup"><span data-stu-id="13ef3-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="13ef3-182">請參閱[監視和管理使用監視應用程式的 Azure Data Factory 管線](data-factory-monitor-manage-app.md)如需使用 hello 應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="13ef3-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="13ef3-183">已成功處理 hello 配量時，取得刪除 hello 輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="13ef3-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="13ef3-184">因此，如果您想 toorerun hello 配量，或不要 hello 教學課程中上, 傳 hello hello adfgetstarted 容器的輸入的檔 (input.log) toohello inputdata 資料夾。</span><span class="sxs-lookup"><span data-stu-id="13ef3-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="13ef3-185">Hello 範本中的 data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="13ef3-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="13ef3-186">定義資料處理站</span><span class="sxs-lookup"><span data-stu-id="13ef3-186">Define data factory</span></span>
<span data-ttu-id="13ef3-187">Hello 下列範例所示，您可以定義在 hello Resource Manager 範本中的 data factory:</span><span class="sxs-lookup"><span data-stu-id="13ef3-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="13ef3-188">hello dataFactoryName 定義為：</span><span class="sxs-lookup"><span data-stu-id="13ef3-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="13ef3-189">它是唯一的字串 hello 資源群組 id。</span><span class="sxs-lookup"><span data-stu-id="13ef3-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="13ef3-190">定義 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="13ef3-190">Defining Data Factory entities</span></span>
<span data-ttu-id="13ef3-191">hello 下列 Data Factory 實體範本中所定義 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="13ef3-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="13ef3-192">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="13ef3-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="13ef3-193">HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="13ef3-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="13ef3-194">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="13ef3-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="13ef3-195">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="13ef3-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="13ef3-196">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="13ef3-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="13ef3-197">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="13ef3-197">Azure Storage linked service</span></span>
<span data-ttu-id="13ef3-198">您可以在此區段中指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="13ef3-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="13ef3-199">請參閱[Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性使用 toodefine Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="13ef3-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="13ef3-200">hello **connectionString**使用 hello storageAccountName 及 storageAccountKey 參數。</span><span class="sxs-lookup"><span data-stu-id="13ef3-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="13ef3-201">hello 使用組態檔傳遞這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="13ef3-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="13ef3-202">hello 定義也會使用變數： azureStroageLinkedService 和 dataFactoryName hello 範本中定義。</span><span class="sxs-lookup"><span data-stu-id="13ef3-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="13ef3-203">HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="13ef3-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="13ef3-204">請參閱[計算連結的服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)文件如需詳細資訊 JSON 屬性使用 toodefine HDInsight 視連結的服務。</span><span class="sxs-lookup"><span data-stu-id="13ef3-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="13ef3-205">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="13ef3-205">Note hello following points:</span></span> 

* <span data-ttu-id="13ef3-206">hello Data Factory 建立**linux**上方 JSON hello 與您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="13ef3-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="13ef3-207">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="13ef3-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="13ef3-208">您可以使用 **自己的 HDInsight 叢集** ，不必使用隨選的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="13ef3-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="13ef3-209">如需詳細資訊，請參閱 [HDInsight 連結服務](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="13ef3-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="13ef3-210">hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。</span><span class="sxs-lookup"><span data-stu-id="13ef3-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="13ef3-211">HDInsight 刪除 hello 叢集時，不會刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="13ef3-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="13ef3-212">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="13ef3-212">This behavior is by design.</span></span> <span data-ttu-id="13ef3-213">HDInsight 叢集隨 HDInsight 連結服務，以建立每次配量需要處理現有的叢集即時除非 toobe (**timeToLive**) 和 hello 處理完成時刪除。</span><span class="sxs-lookup"><span data-stu-id="13ef3-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="13ef3-214">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="13ef3-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="13ef3-215">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="13ef3-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="13ef3-216">這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。</span><span class="sxs-lookup"><span data-stu-id="13ef3-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="13ef3-217">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="13ef3-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="13ef3-218">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="13ef3-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="13ef3-219">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="13ef3-219">Azure blob input dataset</span></span>
<span data-ttu-id="13ef3-220">您指定 blob 容器、 資料夾和檔案，其中包含 hello 輸入的資料的 hello 的名稱。</span><span class="sxs-lookup"><span data-stu-id="13ef3-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="13ef3-221">請參閱[Azure Blob 資料集屬性](data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="13ef3-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="13ef3-222">這個定義會使用下列參數的範本中定義參數的 hello: blobContainer，inputBlobFolder，和 inputBlobName。</span><span class="sxs-lookup"><span data-stu-id="13ef3-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="13ef3-223">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="13ef3-223">Azure Blob output dataset</span></span>
<span data-ttu-id="13ef3-224">您指定 blob 容器和保存 hello 輸出資料之資料夾的 hello 的名稱。</span><span class="sxs-lookup"><span data-stu-id="13ef3-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="13ef3-225">請參閱[Azure Blob 資料集屬性](data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="13ef3-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="13ef3-226">這個定義會使用下列參數 hello 參數範本中定義的 hello: blobContainer 和 outputBlobFolder。</span><span class="sxs-lookup"><span data-stu-id="13ef3-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="13ef3-227">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="13ef3-227">Data pipeline</span></span>
<span data-ttu-id="13ef3-228">您可以定義在隨選 Azure HDInsight 叢集上執行 Hive 指令碼以轉換資料的管線。</span><span class="sxs-lookup"><span data-stu-id="13ef3-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="13ef3-229">請參閱[管線 JSON](data-factory-create-pipelines.md#pipeline-json)如需 JSON 用項目 toodefine 管線，以在此範例的描述。</span><span class="sxs-lookup"><span data-stu-id="13ef3-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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

## <a name="reuse-hello-template"></a><span data-ttu-id="13ef3-230">重複使用 hello 範本</span><span class="sxs-lookup"><span data-stu-id="13ef3-230">Reuse hello template</span></span>
<span data-ttu-id="13ef3-231">在 hello 教學課程中，您可以建立 Data Factory 實體和傳遞的參數值的範本定義的範本。</span><span class="sxs-lookup"><span data-stu-id="13ef3-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="13ef3-232">toouse hello 相同範本 toodeploy Data Factory 實體 toodifferent 環境，您建立參數檔案的每個環境，並部署 toothat 環境時，請使用它。</span><span class="sxs-lookup"><span data-stu-id="13ef3-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="13ef3-233">範例：</span><span class="sxs-lookup"><span data-stu-id="13ef3-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="13ef3-234">請注意，第一個命令會使用參數的 hello hello 開發環境的 hello 測試環境中，第二個檔案，與 hello hello 的生產環境的第三個。</span><span class="sxs-lookup"><span data-stu-id="13ef3-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="13ef3-235">您也可以重複使用 hello 範本 tooperform 重複的工作。</span><span class="sxs-lookup"><span data-stu-id="13ef3-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="13ef3-236">比方說，需要 toocreate 許多 data factory，其中包含一個或多個實作的管線 hello 相同邏輯，但每個資料處理站會使用不同 Azure 儲存體和 Azure SQL Database 帳戶。</span><span class="sxs-lookup"><span data-stu-id="13ef3-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="13ef3-237">在此案例中，您可以使用 hello 相同的範本在 hello 與不同的參數相同的環境 （開發、 測試或生產） 檔案 toocreate data factory。</span><span class="sxs-lookup"><span data-stu-id="13ef3-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="13ef3-238">可供建立閘道的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="13ef3-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="13ef3-239">以下是範例資源管理員範本在 hello 回中建立邏輯的閘道。</span><span class="sxs-lookup"><span data-stu-id="13ef3-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="13ef3-240">在內部部署電腦或 Azure IaaS VM 上安裝閘道器並使用金鑰的 Data Factory 服務註冊 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="13ef3-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="13ef3-241">如需詳細資訊，請參閱 [在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="13ef3-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="13ef3-242">此範本會利用名為 GatewayUsingARM 的閘道建立名為 GatewayUsingArmDF 的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="13ef3-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="13ef3-243">另請參閱</span><span class="sxs-lookup"><span data-stu-id="13ef3-243">See Also</span></span>
| <span data-ttu-id="13ef3-244">主題</span><span class="sxs-lookup"><span data-stu-id="13ef3-244">Topic</span></span> | <span data-ttu-id="13ef3-245">說明</span><span class="sxs-lookup"><span data-stu-id="13ef3-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="13ef3-246">管線</span><span class="sxs-lookup"><span data-stu-id="13ef3-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="13ef3-247">這篇文章可協助您了解管線和 Azure Data Factory 中的活動以及 toouse 它們 tooconstruct 端對端資料驅動型工作流程或商務案例。</span><span class="sxs-lookup"><span data-stu-id="13ef3-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="13ef3-248">資料集</span><span class="sxs-lookup"><span data-stu-id="13ef3-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="13ef3-249">本文協助您了解 Azure Data Factory 中的資料集。</span><span class="sxs-lookup"><span data-stu-id="13ef3-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="13ef3-250">排程和執行</span><span class="sxs-lookup"><span data-stu-id="13ef3-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="13ef3-251">本文說明 Azure Data Factory 應用程式模型的 hello 排程和執行的層面。</span><span class="sxs-lookup"><span data-stu-id="13ef3-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="13ef3-252">使用監視應用程式來監視和管理管線</span><span class="sxs-lookup"><span data-stu-id="13ef3-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="13ef3-253">本文說明如何 toomonitor，管理和偵錯管線使用 hello 監視和管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="13ef3-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

