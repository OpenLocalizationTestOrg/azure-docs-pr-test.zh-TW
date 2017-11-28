---
title: "教學課程：使用 Resource Manager 範本建立管線 | Microsoft Docs"
description: "在本教學課程中，您會使用 Azure Resource Manager 範本建立 Azure Data Factory 管線。 這個管線會將資料從 Azure blob 儲存體 tooan Azure SQL database。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="2d692-104">教學課程： 使用 Azure Resource Manager 範本 toocreate Data Factory 管線 toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="2d692-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d692-105">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="2d692-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="2d692-106">複製精靈</span><span class="sxs-lookup"><span data-stu-id="2d692-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="2d692-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2d692-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="2d692-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2d692-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="2d692-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d692-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="2d692-110">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="2d692-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="2d692-111">REST API</span><span class="sxs-lookup"><span data-stu-id="2d692-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="2d692-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="2d692-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="2d692-113">本教學課程示範如何 toouse Azure Resource Manager 範本 toocreate Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="2d692-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="2d692-114">在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2d692-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="2d692-115">它不會轉換輸入的資料 tooproduce 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="2d692-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="2d692-116">如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="2d692-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="2d692-117">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="2d692-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="2d692-118">hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2d692-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="2d692-119">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="2d692-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2d692-120">hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。</span><span class="sxs-lookup"><span data-stu-id="2d692-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="2d692-121">如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="2d692-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="2d692-122">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="2d692-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="2d692-123">此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。</span><span class="sxs-lookup"><span data-stu-id="2d692-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="2d692-124">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="2d692-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="2d692-125">在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2d692-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="2d692-126">如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="2d692-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2d692-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="2d692-127">Prerequisites</span></span>
* <span data-ttu-id="2d692-128">透過移[教學課程的概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)和完整 hello**必要條件**步驟。</span><span class="sxs-lookup"><span data-stu-id="2d692-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="2d692-129">遵循指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)文章 tooinstall 最新版的 Azure PowerShell 在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="2d692-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="2d692-130">在本教學課程中，您可以使用 PowerShell toodeploy Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="2d692-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="2d692-131">（選擇性）請參閱[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)toolearn 關於 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="2d692-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="2d692-132">本教學課程內容</span><span class="sxs-lookup"><span data-stu-id="2d692-132">In this tutorial</span></span>
<span data-ttu-id="2d692-133">在本教學課程中，您可以建立 data factory 以下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="2d692-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="2d692-134">實體</span><span class="sxs-lookup"><span data-stu-id="2d692-134">Entity</span></span> | <span data-ttu-id="2d692-135">說明</span><span class="sxs-lookup"><span data-stu-id="2d692-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d692-136">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="2d692-136">Azure Storage linked service</span></span> |<span data-ttu-id="2d692-137">連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="2d692-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="2d692-138">Azure 儲存體是 hello 來源資料存放區和 Azure SQL database 是 hello 教學課程中的 hello 複製活動的 hello 接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2d692-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="2d692-139">它會指定包含 hello hello 複製活動的輸入的資料的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d692-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="2d692-140">Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="2d692-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="2d692-141">連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="2d692-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="2d692-142">它會指定保留 hello hello 複製活動的輸出資料的 hello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="2d692-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="2d692-143">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="2d692-143">Azure Blob input dataset</span></span> |<span data-ttu-id="2d692-144">是指 toohello Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="2d692-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="2d692-145">hello 連結的服務是指 tooan Azure 儲存體帳戶和 hello Azure Blob 資料集指定 hello 儲存體保存 hello 輸入的資料中的 hello 容器、 資料夾和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="2d692-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="2d692-146">Azure SQL 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="2d692-146">Azure SQL output dataset</span></span> |<span data-ttu-id="2d692-147">是指 toohello Azure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="2d692-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="2d692-148">hello Azure SQL 連結服務參考 tooan Azure SQL server 和 hello Azure SQL 資料集會指定 hello 保存 hello 輸出資料的 hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="2d692-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="2d692-149">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="2d692-149">Data pipeline</span></span> |<span data-ttu-id="2d692-150">hello 管線有一個活動的輸入會做為輸入 hello Azure blob 資料集的複本與 hello Azure SQL 資料集做為輸出。</span><span class="sxs-lookup"><span data-stu-id="2d692-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="2d692-151">hello 複製活動會從 Azure blob tooa hello Azure SQL database 中的資料表複製資料。</span><span class="sxs-lookup"><span data-stu-id="2d692-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="2d692-152">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="2d692-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="2d692-153">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="2d692-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="2d692-154">兩種活動類型︰[資料移動活動](data-factory-data-movement-activities.md)和[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="2d692-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="2d692-155">在本教學課程中，您可以使用一個活動建立管線 (複製活動)。</span><span class="sxs-lookup"><span data-stu-id="2d692-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![複製 Azure Blob tooAzure SQL 資料庫](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="2d692-157">hello 下節提供 hello 完成資源管理員範本，您可以快速地執行透過 hello 教學課程和測試 hello 範本定義 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="2d692-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="2d692-158">toounderstand 如何定義每個 Data Factory 實體，請參閱[hello 範本中的 Data Factory 實體](#data-factory-entities-in-the-template)> 一節。</span><span class="sxs-lookup"><span data-stu-id="2d692-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="2d692-159">Data Factory JSON 範本</span><span class="sxs-lookup"><span data-stu-id="2d692-159">Data Factory JSON template</span></span>
<span data-ttu-id="2d692-160">是用於定義 data factory hello 最上層資源管理員範本：</span><span class="sxs-lookup"><span data-stu-id="2d692-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="2d692-161">建立名為的 JSON 檔案**ADFCopyTutorialARM.json**中**C:\ADFGetStarted**資料夾以 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="2d692-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
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
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
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
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
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
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob tooAzure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="2d692-162">參數 JSON</span><span class="sxs-lookup"><span data-stu-id="2d692-162">Parameters JSON</span></span>
<span data-ttu-id="2d692-163">建立名為的 JSON 檔案**ADFCopyTutorialARM Parameters.json**包含 hello Azure Resource Manager 範本的參數。</span><span class="sxs-lookup"><span data-stu-id="2d692-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2d692-164">針對此參數檔案中的 storageAccountName 和 storageAccountKey 參數指定您 Azure 儲存體帳戶的名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="2d692-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="2d692-165">針對 sqlServerName、databaseName、sqlServerUserName 和 sqlServerPassword 參數指定 Azure SQL 伺服器、資料庫、使用者和密碼。</span><span class="sxs-lookup"><span data-stu-id="2d692-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="2d692-166">您可能需要進行開發，個別參數的 JSON 檔案測試，而且您可以搭配使用的實際執行環境的 hello 相同資料 Factory JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="2d692-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="2d692-167">使用 Power Shell 指令碼，您可以在這些環境中自動部署 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="2d692-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="2d692-168">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="2d692-168">Create data factory</span></span>
1. <span data-ttu-id="2d692-169">啟動**Azure PowerShell**和 hello 執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="2d692-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="2d692-170">執行下列命令的 hello 並輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="2d692-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="2d692-171">執行下列命令 tooview hello 這個帳戶的所有 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d692-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="2d692-172">執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="2d692-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="2d692-173">執行下列命令使用您在步驟 1 中建立的 hello Resource Manager 範本的 toodeploy Data Factory 實體的 hello。</span><span class="sxs-lookup"><span data-stu-id="2d692-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="2d692-174">監視管線</span><span class="sxs-lookup"><span data-stu-id="2d692-174">Monitor pipeline</span></span>

1. <span data-ttu-id="2d692-175">登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d692-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="2d692-176">按一下**Data factory** hello 左邊功能表 （或） 上按一下**更多服務**按一下**Data factory**下**智慧 + 分析**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="2d692-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Data Factory 功能表](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="2d692-178">在 hello **Data factory**頁面、 搜尋和尋找您的 data factory (AzureBlobToAzureSQLDatabaseDF)。</span><span class="sxs-lookup"><span data-stu-id="2d692-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![搜尋 Data Factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="2d692-180">按一下您的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="2d692-180">Click your Azure data factory.</span></span> <span data-ttu-id="2d692-181">您看到 hello 首頁 hello data factory。</span><span class="sxs-lookup"><span data-stu-id="2d692-181">You see hello home page for hello data factory.</span></span>
   
    ![Data Factory 首頁](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="2d692-183">請依照下列指示從[監視資料集和管線](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline)toomonitor hello 管線和資料集已建立本教學課程中。</span><span class="sxs-lookup"><span data-stu-id="2d692-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="2d692-184">Visual Studio 目前不支援監視 Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="2d692-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="2d692-185">配量處於 hello**準備**狀態，請確認 hello 資料複製的 toohello **emp** hello Azure SQL database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="2d692-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="2d692-186">如需有關如何 toouse Azure 入口網站的刀鋒 toomonitor 管線和資料集您已建立本教學課程中的詳細資訊，請參閱[監視資料集和管線](data-factory-monitor-manage-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="2d692-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="2d692-187">如需有關如何 toouse hello 監視和管理應用程式 toomonitor 資料管線的詳細資訊，請參閱[監視和管理使用監視應用程式的 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="2d692-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="2d692-188">Hello 範本中的 data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="2d692-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="2d692-189">定義資料處理站</span><span class="sxs-lookup"><span data-stu-id="2d692-189">Define data factory</span></span>
<span data-ttu-id="2d692-190">Hello 下列範例所示，您可以定義在 hello Resource Manager 範本中的 data factory:</span><span class="sxs-lookup"><span data-stu-id="2d692-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="2d692-191">hello dataFactoryName 定義為：</span><span class="sxs-lookup"><span data-stu-id="2d692-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="2d692-192">它是唯一的字串 hello 資源群組 id。</span><span class="sxs-lookup"><span data-stu-id="2d692-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="2d692-193">定義 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="2d692-193">Defining Data Factory entities</span></span>
<span data-ttu-id="2d692-194">hello 下列 Data Factory 實體範本中所定義 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="2d692-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="2d692-195">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="2d692-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="2d692-196">Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="2d692-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="2d692-197">Azure blob 資料集</span><span class="sxs-lookup"><span data-stu-id="2d692-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="2d692-198">Azure SQL 資料集</span><span class="sxs-lookup"><span data-stu-id="2d692-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="2d692-199">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="2d692-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="2d692-200">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="2d692-200">Azure Storage linked service</span></span>
<span data-ttu-id="2d692-201">hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="2d692-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="2d692-202">您在建立容器，並在上傳資料 toothis 儲存體帳戶的[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="2d692-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="2d692-203">您可以在此區段中指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="2d692-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="2d692-204">請參閱[Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性使用 toodefine Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="2d692-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="2d692-205">hello connectionString 使用 hello storageAccountName 及 storageAccountKey 參數。</span><span class="sxs-lookup"><span data-stu-id="2d692-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="2d692-206">hello 使用組態檔傳遞這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="2d692-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="2d692-207">hello 定義也會使用變數： azureStroageLinkedService 和 dataFactoryName hello 範本中定義。</span><span class="sxs-lookup"><span data-stu-id="2d692-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="2d692-208">Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="2d692-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="2d692-209">AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="2d692-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="2d692-210">複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="2d692-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="2d692-211">在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="2d692-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="2d692-212">您可以在此區段中指定 hello Azure SQL server 名稱、 資料庫名稱、 使用者名稱和使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="2d692-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="2d692-213">請參閱[Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="2d692-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="2d692-214">hello connectionString 使用 sqlServerName、 databaseName、 sqlServerUserName 和其值使用組態檔傳遞 sqlServerPassword 參數。</span><span class="sxs-lookup"><span data-stu-id="2d692-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="2d692-215">hello 定義也會使用 hello hello 範本中的下列變數： azureSqlLinkedServiceName，dataFactoryName。</span><span class="sxs-lookup"><span data-stu-id="2d692-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="2d692-216">Azure Blob 資料集</span><span class="sxs-lookup"><span data-stu-id="2d692-216">Azure blob dataset</span></span>
<span data-ttu-id="2d692-217">hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="2d692-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="2d692-218">在 Azure blob 資料集定義中，您可以指定 blob 容器、 資料夾和檔案，其中包含 hello 輸入的資料的名稱。</span><span class="sxs-lookup"><span data-stu-id="2d692-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="2d692-219">請參閱[Azure Blob 資料集屬性](data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="2d692-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="2d692-220">Azure SQL 資料集</span><span class="sxs-lookup"><span data-stu-id="2d692-220">Azure SQL dataset</span></span>
<span data-ttu-id="2d692-221">您擁有 hello Azure Blob 儲存體的 hello 複製資料的 hello Azure SQL database 中指定 hello hello 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="2d692-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="2d692-222">請參閱[Azure SQL 資料集屬性](data-factory-azure-sql-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure SQL 資料集。</span><span class="sxs-lookup"><span data-stu-id="2d692-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="2d692-223">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="2d692-223">Data pipeline</span></span>
<span data-ttu-id="2d692-224">您定義將資料從 hello Azure blob 資料集 toohello Azure SQL 資料集的管線。</span><span class="sxs-lookup"><span data-stu-id="2d692-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="2d692-225">請參閱[管線 JSON](data-factory-create-pipelines.md#pipeline-json)如需 JSON 用項目 toodefine 管線，以在此範例的描述。</span><span class="sxs-lookup"><span data-stu-id="2d692-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob tooAzure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-hello-template"></a><span data-ttu-id="2d692-226">重複使用 hello 範本</span><span class="sxs-lookup"><span data-stu-id="2d692-226">Reuse hello template</span></span>
<span data-ttu-id="2d692-227">在 hello 教學課程中，您可以建立 Data Factory 實體和傳遞的參數值的範本定義的範本。</span><span class="sxs-lookup"><span data-stu-id="2d692-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="2d692-228">hello 管線會將資料從 Azure 儲存體帳戶 tooan Azure SQL database 透過參數所指定。</span><span class="sxs-lookup"><span data-stu-id="2d692-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="2d692-229">toouse hello 相同範本 toodeploy Data Factory 實體 toodifferent 環境，您建立參數檔案的每個環境，並部署 toothat 環境時，請使用它。</span><span class="sxs-lookup"><span data-stu-id="2d692-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="2d692-230">範例：</span><span class="sxs-lookup"><span data-stu-id="2d692-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="2d692-231">請注意，第一個命令會使用參數的 hello hello 開發環境的 hello 測試環境中，第二個檔案，與 hello hello 的生產環境的第三個。</span><span class="sxs-lookup"><span data-stu-id="2d692-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="2d692-232">您也可以重複使用 hello 範本 tooperform 重複的工作。</span><span class="sxs-lookup"><span data-stu-id="2d692-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="2d692-233">比方說，您需要 toocreate 許多 data factory，其中包含一個或多個實作的管線 hello 相同邏輯，但每個 data factory 會使用不同的 SQL 資料庫和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d692-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="2d692-234">在此案例中，您可以使用 hello 相同的範本在 hello 與不同的參數相同的環境 （開發、 測試或生產） 檔案 toocreate data factory。</span><span class="sxs-lookup"><span data-stu-id="2d692-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="2d692-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d692-235">Next steps</span></span>
<span data-ttu-id="2d692-236">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2d692-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="2d692-237">hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單：</span><span class="sxs-lookup"><span data-stu-id="2d692-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="2d692-238">關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2d692-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
