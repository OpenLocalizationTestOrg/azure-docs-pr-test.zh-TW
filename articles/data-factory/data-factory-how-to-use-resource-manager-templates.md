---
title: "在 Data Factory 中使用 Resource Manager 範本 | Microsoft Docs"
description: "了解如何建立及使用 Azure Resource Manager 範本來建立 Data Factory 實體。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="f6f3b-103">使用範本來建立 Azure Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="f6f3b-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="f6f3b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f6f3b-104">Overview</span></span>
<span data-ttu-id="f6f3b-105">基於資料整合需求使用 Azure Data Factory 時，您可能會發現自己跨不同環境重複使用相同的模式，或在相同的解決方案內反覆地實作相同的工作。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="f6f3b-106">範本可協助您輕鬆地實作和管理這些案例。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="f6f3b-107">Azure Data Factory 中的範本最適用於涉及重複使用和重複時。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="f6f3b-108">假設某個組織在全球各地有 10 個製造工廠。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="f6f3b-109">每個工廠中的記錄都會儲存在不同的內部部署 SQL Server 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="f6f3b-110">公司想要在雲端中建置單一資料倉儲，以進行臨機操作分析。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="f6f3b-111">它也想要具有相同的邏輯，但開發、測試和生產環境的組態不同。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="f6f3b-112">在此情況下，必須在相同的環境內重複執行工作，但每個製造工廠的 10 個資料處理站各有不同的值。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="f6f3b-113">實際上，具有**重複**情況。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="f6f3b-114">範本化允許任意使用這個泛形流程 (即在每個資料處理站中具有相同活動的管線)，但會針對每個製造工廠使用不同的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="f6f3b-115">此外，組織想要跨不同環境部署這 10 個資料處理站多次時，範本可以針對開發、測試和生產環境使用不同的參數檔案，來使用這個**重複使用性**。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="f6f3b-116">使用 Azure Resource Manager 範本化</span><span class="sxs-lookup"><span data-stu-id="f6f3b-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="f6f3b-117">[Azure Resource Manager 範本](../azure-resource-manager/resource-group-overview.md#template-deployment)是達成 Azure Data Factory 中範本化的不錯方式。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="f6f3b-118">Resource Manager 範本透過 JSON 檔案來定義 Azure 解決方案的基礎結構和組態。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="f6f3b-119">因為 Azure Resource Manager 範本是與所有/大部分 Azure 服務搭配運作，所以可以廣泛用來輕鬆地管理 Azure 資產的所有資源。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="f6f3b-120">若要深入了解 Resource Manager 範本的一般資訊，請參閱[撰寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md) 。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="f6f3b-121">教學課程</span><span class="sxs-lookup"><span data-stu-id="f6f3b-121">Tutorials</span></span>
<span data-ttu-id="f6f3b-122">如需使用 Resource Manager 範本建立 Data Factory 實體的逐步指示，請參閱下列教學課程︰</span><span class="sxs-lookup"><span data-stu-id="f6f3b-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="f6f3b-123">教學課程：使用 Azure Resource Manager 範本建立管線以複製資料</span><span class="sxs-lookup"><span data-stu-id="f6f3b-123">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="f6f3b-124">教學課程：使用 Azure Resource Manager 範本建立管線以處理資料</span><span class="sxs-lookup"><span data-stu-id="f6f3b-124">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="f6f3b-125">GitHub 上的 Data Factory 範本</span><span class="sxs-lookup"><span data-stu-id="f6f3b-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="f6f3b-126">請參考 GitHub 上的下列 Azure 快速入門範本：</span><span class="sxs-lookup"><span data-stu-id="f6f3b-126">Check out the following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="f6f3b-127">建立 Data Factory 以將資料從 Azure Blob 儲存體複製到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f6f3b-127">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="f6f3b-128">在 Azure HDInsight 叢集上使用 Hive 活動建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="f6f3b-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="f6f3b-129">建立 Data Factory 以將資料從 Salesforce 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="f6f3b-129">Create a Data factory to copy data from Salesforce to Azure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="f6f3b-130">建立 Data factory 以鏈結活動︰將資料從 FTP 伺服器複製到 Azure Blob、叫用隨選 HDInsight 叢集上的 hive 指令碼來轉換資料，並將結果複製到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f6f3b-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="f6f3b-131">在 [Azure 快速啟動](https://azure.microsoft.com/documentation/templates/)上自由共用 Azure Data Factory 範本。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="f6f3b-132">開發可透過這個存放庫共用的範本時，請參閱[參與指南](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE)。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="f6f3b-133">下列各節提供在 Resource Manager 範本中定義 Data Factory 資源的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="f6f3b-134">在範本中定義 Data Factory 資源</span><span class="sxs-lookup"><span data-stu-id="f6f3b-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="f6f3b-135">用於定義資料處理站的最上層範本是︰</span><span class="sxs-lookup"><span data-stu-id="f6f3b-135">The top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="f6f3b-136">定義資料處理站</span><span class="sxs-lookup"><span data-stu-id="f6f3b-136">Define data factory</span></span>
<span data-ttu-id="f6f3b-137">您可以在 Resource Manager 範本中定義資料處理站，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="f6f3b-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="f6f3b-138">dataFactoryName 在 “variables” 中定義為：</span><span class="sxs-lookup"><span data-stu-id="f6f3b-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="f6f3b-139">定義連結服務</span><span class="sxs-lookup"><span data-stu-id="f6f3b-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="f6f3b-140">如需所要部署之特定連結服務的 JSON 屬性詳細資料，請參閱[儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)或[算連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="f6f3b-141">“dependsOn” 參數指定對應資料處理站的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="f6f3b-142">下列 JSON 定義中會顯示針對 Azure 儲存體定義連結服務的範例：</span><span class="sxs-lookup"><span data-stu-id="f6f3b-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="f6f3b-143">定義資料集</span><span class="sxs-lookup"><span data-stu-id="f6f3b-143">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="f6f3b-144">如需您想要部署之特定資料集類型的 JSON 屬性詳細資料，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="f6f3b-145">請注意，“dependsOn” 參數指定對應資料處理站和儲存體連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="f6f3b-146">下列 JSON 定義中會顯示針對 Azure Blob 儲存體定義資料集類型的範例：</span><span class="sxs-lookup"><span data-stu-id="f6f3b-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="f6f3b-147">定義管線</span><span class="sxs-lookup"><span data-stu-id="f6f3b-147">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="f6f3b-148">如需定義您想要部署之特定管線和活動的 JSON 屬性詳細資料，請參閱[定義管線](data-factory-create-pipelines.md#pipeline-json)。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="f6f3b-149">請注意，“dependsOn” 參數指定資料處理站的名稱，以及任何對應連結服務或資料集。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="f6f3b-150">下列 JSON 片段顯示將資料從 Azure Blob 儲存體複製至 Azure SQL Database 的管線範例：</span><span class="sxs-lookup"><span data-stu-id="f6f3b-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="f6f3b-151">參數化 Data Factory 範本</span><span class="sxs-lookup"><span data-stu-id="f6f3b-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="f6f3b-152">如需參數化的最佳作法，請參閱[建立 Azure Resource Manager 範本的最佳作法](../azure-resource-manager/resource-manager-template-best-practices.md#parameters)一文。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="f6f3b-153">一般而言，參數的使用應該降到最低，特別是改為使用變數時。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="f6f3b-154">在下列情況中，僅提供參數：</span><span class="sxs-lookup"><span data-stu-id="f6f3b-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="f6f3b-155">設定會因環境 (範例︰開發、測試和生產) 而不同</span><span class="sxs-lookup"><span data-stu-id="f6f3b-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="f6f3b-156">機密資料 (例如密碼)</span><span class="sxs-lookup"><span data-stu-id="f6f3b-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="f6f3b-157">如果您在使用範本部署 Azure Data Factory 實體時需要從 [Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)提取密碼，請指定 **金鑰保存庫**和**密碼名稱**，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="f6f3b-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="f6f3b-158">雖然目前尚未支援匯出現有資料處理站的範本，但是目前正在努力中。</span><span class="sxs-lookup"><span data-stu-id="f6f3b-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
