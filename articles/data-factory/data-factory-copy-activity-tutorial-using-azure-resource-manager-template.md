---
title: "教學課程：使用 Resource Manager 範本建立管線 | Microsoft Docs"
description: "在本教學課程中，您會使用 Azure Resource Manager 範本建立 Azure Data Factory 管線。 此管線會將資料從 Azure Blob 儲存體複製到 Azure SQL Database。"
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
ms.openlocfilehash: 8a155213ed17e516a5c46abbe3d8a2bcc52268ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="b8a14-104">本教學課程︰使用 Azure Resource Manager 範本建立 Data Factory 管線來複製資料</span><span class="sxs-lookup"><span data-stu-id="b8a14-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8a14-105">概觀和必要條件</span><span class="sxs-lookup"><span data-stu-id="b8a14-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="b8a14-106">複製精靈</span><span class="sxs-lookup"><span data-stu-id="b8a14-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="b8a14-107">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b8a14-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="b8a14-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8a14-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="b8a14-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8a14-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="b8a14-110">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="b8a14-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="b8a14-111">REST API</span><span class="sxs-lookup"><span data-stu-id="b8a14-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="b8a14-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="b8a14-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="b8a14-113">本教學課程示範如何使用 Azure Resource Manager 範本建立 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b8a14-113">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="b8a14-114">本教學課程中的資料管線會將資料從來源資料存放區，複製到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b8a14-114">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="b8a14-115">它不會轉換輸入資料來產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="b8a14-115">It does not transform input data to produce output data.</span></span> <span data-ttu-id="b8a14-116">如需如何使用 Azure Data Factory 轉換資料的教學課程，請參閱[教學課程︰使用 Hadoop 叢集建置管線來轉換資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-116">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="b8a14-117">在本教學課程中，您可以建立包含一個活動的管線：複製活動。</span><span class="sxs-lookup"><span data-stu-id="b8a14-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="b8a14-118">複製活動會將資料從支援的資料存放區複製到支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b8a14-118">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="b8a14-119">如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b8a14-120">此活動是由全域可用的服務所提供，可以使用安全、可靠及可調整的方式，在各種不同的資料存放區之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="b8a14-120">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="b8a14-121">如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-121">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="b8a14-122">一個管線中可以有多個活動。</span><span class="sxs-lookup"><span data-stu-id="b8a14-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="b8a14-123">您可以將一個活動的輸出資料集設為另一個活動的輸入資料集，藉此鏈結兩個活動 (讓一個活動接著另一個活動執行)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-123">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="b8a14-124">如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="b8a14-125">本教學課程中的資料管線會將資料從來源資料存放區，複製到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b8a14-125">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="b8a14-126">如需如何使用 Azure Data Factory 轉換資料的教學課程，請參閱[教學課程︰使用 Hadoop 叢集建置管線來轉換資料](data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-126">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b8a14-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="b8a14-127">Prerequisites</span></span>
* <span data-ttu-id="b8a14-128">請檢閱[教學課程概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)並完成**必要**步驟。</span><span class="sxs-lookup"><span data-stu-id="b8a14-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="b8a14-129">按照 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 一文中的指示，在您的電腦上安裝最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b8a14-129">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="b8a14-130">在本教學課程中，您可以使用 PowerShell 來部署 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="b8a14-130">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="b8a14-131">(選擇性) 若要了解 Azure Resource Manager 範本，請參閱 [撰寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md) 。</span><span class="sxs-lookup"><span data-stu-id="b8a14-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="b8a14-132">本教學課程內容</span><span class="sxs-lookup"><span data-stu-id="b8a14-132">In this tutorial</span></span>
<span data-ttu-id="b8a14-133">在本教學課程中，您可以利用下列 Data Factory 實體建立資料處理站︰</span><span class="sxs-lookup"><span data-stu-id="b8a14-133">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="b8a14-134">實體</span><span class="sxs-lookup"><span data-stu-id="b8a14-134">Entity</span></span> | <span data-ttu-id="b8a14-135">說明</span><span class="sxs-lookup"><span data-stu-id="b8a14-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b8a14-136">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="b8a14-136">Azure Storage linked service</span></span> |<span data-ttu-id="b8a14-137">將您的 Azure 儲存體帳戶連結至 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b8a14-137">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="b8a14-138">Azure 儲存體是來源資料存放區，而 Azure SQL Database 是教學課程中複製活動的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b8a14-138">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="b8a14-139">它會指定包含複製活動之輸入資料的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8a14-139">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="b8a14-140">Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="b8a14-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="b8a14-141">將您的 Azure SQL Database 連結至 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b8a14-141">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="b8a14-142">它會指定包含複製活動之輸出資料的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="b8a14-142">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="b8a14-143">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="b8a14-143">Azure Blob input dataset</span></span> |<span data-ttu-id="b8a14-144">是指 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="b8a14-144">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="b8a14-145">連結的服務是指 Azure 儲存體帳戶，而 Azure Blob 資料集則會指定保留輸入資料儲存體中的容器、資料夾和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="b8a14-145">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="b8a14-146">Azure SQL 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="b8a14-146">Azure SQL output dataset</span></span> |<span data-ttu-id="b8a14-147">是指 Azure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="b8a14-147">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="b8a14-148">Azure SQL 連結服務是指 Azure SQL Server，而 Azure SQL 資料集會指定包含輸出資料的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="b8a14-148">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="b8a14-149">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="b8a14-149">Data pipeline</span></span> |<span data-ttu-id="b8a14-150">管線有一個類型 Copy 的活動，會採用 Azure blob 資料集做為輸入和 Azure SQL 資料集做為輸出。</span><span class="sxs-lookup"><span data-stu-id="b8a14-150">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="b8a14-151">Copy 活動會將資料從 Azure Blob 複製到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="b8a14-151">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="b8a14-152">資料處理站可以有一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="b8a14-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="b8a14-153">其中的管線可以有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="b8a14-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="b8a14-154">兩種活動類型︰[資料移動活動](data-factory-data-movement-activities.md)和[資料轉換活動](data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="b8a14-155">在本教學課程中，您可以使用一個活動建立管線 (複製活動)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![將 Azure Blob 複製到 Azure SQL Database](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="b8a14-157">下節會提供完整的 Resource Manager 範本來定義 Data Factory 實體，如此您可以快速執行教學課程並測試範本。</span><span class="sxs-lookup"><span data-stu-id="b8a14-157">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="b8a14-158">若要了解每個 Data Factory 實體的定義方式，請參閱[範本中的 Data Factory 實體](#data-factory-entities-in-the-template)一節。</span><span class="sxs-lookup"><span data-stu-id="b8a14-158">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="b8a14-159">Data Factory JSON 範本</span><span class="sxs-lookup"><span data-stu-id="b8a14-159">Data Factory JSON template</span></span>
<span data-ttu-id="b8a14-160">用於定義資料處理站的最上層 Resource Manager 範本是︰</span><span class="sxs-lookup"><span data-stu-id="b8a14-160">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="b8a14-161">在 **C:\ADFGetStarted** 資料夾中，使用下列內容建立名為 **ADFCopyTutorialARM.json** 的 JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="b8a14-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
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
                  "description": "Copy data frm Azure blob to Azure SQL",
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

## <a name="parameters-json"></a><span data-ttu-id="b8a14-162">參數 JSON</span><span class="sxs-lookup"><span data-stu-id="b8a14-162">Parameters JSON</span></span>
<span data-ttu-id="b8a14-163">建立名為 **ADFCopyTutorialARM-Parameters.json** 的 JSON 檔案，其中包含 Azure Resource Manager 範本的參數。</span><span class="sxs-lookup"><span data-stu-id="b8a14-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b8a14-164">針對此參數檔案中的 storageAccountName 和 storageAccountKey 參數指定您 Azure 儲存體帳戶的名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="b8a14-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="b8a14-165">針對 sqlServerName、databaseName、sqlServerUserName 和 sqlServerPassword 參數指定 Azure SQL 伺服器、資料庫、使用者和密碼。</span><span class="sxs-lookup"><span data-stu-id="b8a14-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="b8a14-166">您可能需要不同的參數 JSON 檔案，以供可與相同 Data Factory JSON 範本共同使用的開發、測試和生產環境使用。</span><span class="sxs-lookup"><span data-stu-id="b8a14-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="b8a14-167">使用 Power Shell 指令碼，您可以在這些環境中自動部署 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="b8a14-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="b8a14-168">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="b8a14-168">Create data factory</span></span>
1. <span data-ttu-id="b8a14-169">啟動 **Azure PowerShell** 並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b8a14-169">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="b8a14-170">執行下列命令並輸入您用來登入 Azure 入口網站的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b8a14-170">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="b8a14-171">執行下列命令以檢視此帳戶的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8a14-171">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="b8a14-172">執行下列命令以選取您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8a14-172">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="b8a14-173">執行下列命令，使用您在步驟 1 中建立的 Resource Manager 範本來部署 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="b8a14-173">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="b8a14-174">監視管線</span><span class="sxs-lookup"><span data-stu-id="b8a14-174">Monitor pipeline</span></span>

1. <span data-ttu-id="b8a14-175">使用您的 Azure 帳戶登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-175">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="b8a14-176">按一下左功能表的 [Data Factory] \(或) 按一下 [更多服務] 然後按一下 [智慧 + 分析] 類別下的 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="b8a14-176">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Data Factory 功能表](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="b8a14-178">在 [資料處理站] 頁面上，搜尋並尋找您的資料處理站 (AzureBlobToAzureSQLDatabaseDF)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-178">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![搜尋 Data Factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="b8a14-180">按一下您的 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b8a14-180">Click your Azure data factory.</span></span> <span data-ttu-id="b8a14-181">您會看到 Data Factory 的首頁。</span><span class="sxs-lookup"><span data-stu-id="b8a14-181">You see the home page for the data factory.</span></span>
   
    ![Data Factory 首頁](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="b8a14-183">請遵循[監視資料集和管線](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline)中的指示，監視您在本教學課程中建立的管線和資料集。</span><span class="sxs-lookup"><span data-stu-id="b8a14-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="b8a14-184">Visual Studio 目前不支援監視 Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="b8a14-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="b8a14-185">當配量處於 [就緒] 狀態時，請確認資料已複製到 Azure SQL Database 中的 **emp** 資料表。</span><span class="sxs-lookup"><span data-stu-id="b8a14-185">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="b8a14-186">如需有關如何使用 Azure 入口網站刀鋒視窗來監視您在本教學課程中建立的管線和資料集的詳細資訊，請參閱 [監視資料集和管線](data-factory-monitor-manage-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-186">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="b8a14-187">如需有關如何使用監視及管理應用程式來監視資料管線的詳細資訊，請參閱[使用監視應用程式來監視和管理 Azure Data Factory 管線](data-factory-monitor-manage-app.md)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-187">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="b8a14-188">範本中的 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="b8a14-188">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="b8a14-189">定義資料處理站</span><span class="sxs-lookup"><span data-stu-id="b8a14-189">Define data factory</span></span>
<span data-ttu-id="b8a14-190">您可以在 Resource Manager 範本中定義資料處理站，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="b8a14-190">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="b8a14-191">dataFactoryName 定義為：</span><span class="sxs-lookup"><span data-stu-id="b8a14-191">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="b8a14-192">根據資源群組識別碼，它是唯一的字串。</span><span class="sxs-lookup"><span data-stu-id="b8a14-192">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="b8a14-193">定義 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="b8a14-193">Defining Data Factory entities</span></span>
<span data-ttu-id="b8a14-194">下列的 Data Factory 實體定義於 JSON 範本中︰</span><span class="sxs-lookup"><span data-stu-id="b8a14-194">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="b8a14-195">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="b8a14-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="b8a14-196">Azure SQL 連結服務</span><span class="sxs-lookup"><span data-stu-id="b8a14-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="b8a14-197">Azure blob 資料集</span><span class="sxs-lookup"><span data-stu-id="b8a14-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="b8a14-198">Azure SQL 資料集</span><span class="sxs-lookup"><span data-stu-id="b8a14-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="b8a14-199">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="b8a14-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="b8a14-200">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="b8a14-200">Azure Storage linked service</span></span>
<span data-ttu-id="b8a14-201">AzureStorageLinkedService 會將 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="b8a14-201">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="b8a14-202">您已建立容器並將資料上傳到此儲存體帳戶，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="b8a14-202">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="b8a14-203">在此區段中指定您 Azure 儲存體帳戶的名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="b8a14-203">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="b8a14-204">如需用來定義 Azure 儲存體連結服務之 JSON 屬性的詳細資料，請參閱 [Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="b8a14-205">connectionString 會使用 storageAccountName 和 storageAccountKey 參數。</span><span class="sxs-lookup"><span data-stu-id="b8a14-205">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="b8a14-206">使用組態檔傳遞這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="b8a14-206">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="b8a14-207">定義也會使用在範本中定義的變數︰azureStroageLinkedService 和 dataFactoryName。</span><span class="sxs-lookup"><span data-stu-id="b8a14-207">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="b8a14-208">Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="b8a14-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="b8a14-209">AzureSqlLinkedService 會將 Azure SQL Database 連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="b8a14-209">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="b8a14-210">從 Blob 儲存體複製的資料會儲存在此資料庫中。</span><span class="sxs-lookup"><span data-stu-id="b8a14-210">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="b8a14-211">您在此資料庫中建立了 emp 資料表，作為[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="b8a14-211">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="b8a14-212">在此區段中指定 Azure SQL 伺服器名稱、資料庫名稱、使用者名稱和使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="b8a14-212">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="b8a14-213">如需用來定義 Azure SQL 連結服務之 JSON 屬性的詳細資料，請參閱 [Azure SQL 連結服務](data-factory-azure-sql-connector.md#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="b8a14-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="b8a14-214">connectionString 會使用 sqlServerName、databaseName、sqlServerUserName 和 sqlServerPassword 參數，其值會使用組態檔傳遞。</span><span class="sxs-lookup"><span data-stu-id="b8a14-214">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="b8a14-215">定義也會使用下列來自範本的參數：azureSqlLinkedServiceName、dataFactoryName。</span><span class="sxs-lookup"><span data-stu-id="b8a14-215">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="b8a14-216">Azure Blob 資料集</span><span class="sxs-lookup"><span data-stu-id="b8a14-216">Azure blob dataset</span></span>
<span data-ttu-id="b8a14-217">Azure 儲存體連結服務會指定 Data Factory 服務在執行階段用來連線到 Azure 儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="b8a14-217">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="b8a14-218">在 Azure Blob 資料集定義中，您可指定 Blob 容器、資料夾和包含輸入資料之檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="b8a14-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="b8a14-219">請參閱 [Azure Blob 資料集屬性](data-factory-azure-blob-connector.md#dataset-properties)，以取得用來定義 Azure Blob 資料集之 JSON 屬性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b8a14-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="b8a14-220">Azure SQL 資料集</span><span class="sxs-lookup"><span data-stu-id="b8a14-220">Azure SQL dataset</span></span>
<span data-ttu-id="b8a14-221">指定存放來自 Azure Blob 儲存體之複製資料的 Azure SQL Database 中的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="b8a14-221">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="b8a14-222">請參閱 [Azure SQL 資料集屬性](data-factory-azure-sql-connector.md#dataset-properties)，以取得用來定義 Azure SQL 資料集之 JSON 屬性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b8a14-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

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

#### <a name="data-pipeline"></a><span data-ttu-id="b8a14-223">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="b8a14-223">Data pipeline</span></span>
<span data-ttu-id="b8a14-224">定義將資料從 Azure blob 資料集複製到 Azure SQL 資料集的管線。</span><span class="sxs-lookup"><span data-stu-id="b8a14-224">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="b8a14-225">請參閱[管線 JSON](data-factory-create-pipelines.md#pipeline-json)，以取得用來在此範例中定義管線的 JSON 元素之描述。</span><span class="sxs-lookup"><span data-stu-id="b8a14-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

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
              "description": "Copy data frm Azure blob to Azure SQL",
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

## <a name="reuse-the-template"></a><span data-ttu-id="b8a14-226">重複使用範本</span><span class="sxs-lookup"><span data-stu-id="b8a14-226">Reuse the template</span></span>
<span data-ttu-id="b8a14-227">在教學課程中，您可以建立定義 Data Factory 實體的範本和傳遞參數值的範本。</span><span class="sxs-lookup"><span data-stu-id="b8a14-227">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="b8a14-228">管線會將資料從 Azure 儲存體帳戶複製到透過參數指定的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="b8a14-228">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="b8a14-229">若要使用相同的範本將 Data Factory 實體部署至不同的環境，您可以針對每個環境建立參數檔案，並在部署到該環境時使用它。</span><span class="sxs-lookup"><span data-stu-id="b8a14-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="b8a14-230">範例：</span><span class="sxs-lookup"><span data-stu-id="b8a14-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="b8a14-231">請注意，第一個命令會使用開發環境的參數檔案，第二個會使用測試環境的參數檔案，而第三個會使用生產環境的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="b8a14-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="b8a14-232">您也可以重複使用範本來執行重複的工作。</span><span class="sxs-lookup"><span data-stu-id="b8a14-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="b8a14-233">例如，您需要使用一個或多個管線建立許多資料處理站，這些管線會實作相同的邏輯，但每個資料處理站會使用不同的儲存體和 SQL Database 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8a14-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="b8a14-234">在此案例中，您會在具有不同參數檔案的相同環境中 (開發、測試或生產) 使用相同的範本來建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="b8a14-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="b8a14-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8a14-235">Next steps</span></span>
<span data-ttu-id="b8a14-236">在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b8a14-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="b8a14-237">下表提供複製活動所支援作為來源或目的地的資料存放區清單：</span><span class="sxs-lookup"><span data-stu-id="b8a14-237">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="b8a14-238">若要深入了解如何從資料存放區雙向複製資料，請按一下資料表中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="b8a14-238">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
