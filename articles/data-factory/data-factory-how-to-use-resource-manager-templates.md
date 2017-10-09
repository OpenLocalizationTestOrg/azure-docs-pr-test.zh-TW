---
title: "aaaUse Data Factory 中的資源管理員範本 |Microsoft 文件"
description: "深入了解如何 toocreate 和使用 Azure Resource Manager 範本 toocreate Data Factory 實體。"
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
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="0d978-103">使用範本 toocreate Azure Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="0d978-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="0d978-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0d978-104">Overview</span></span>
<span data-ttu-id="0d978-105">使用 Azure Data Factory 的資料整合需求，您可能會發現自己時重複使用不同環境下 hello 相同的模式，或實作 hello 相同工作回應 hello 內相同的方案。</span><span class="sxs-lookup"><span data-stu-id="0d978-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="0d978-106">範本可協助您輕鬆地實作和管理這些案例。</span><span class="sxs-lookup"><span data-stu-id="0d978-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="0d978-107">Azure Data Factory 中的範本最適用於涉及重複使用和重複時。</span><span class="sxs-lookup"><span data-stu-id="0d978-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="0d978-108">請考慮組織其中有 10 個製造廠 hello 世界各地的 hello 情況。</span><span class="sxs-lookup"><span data-stu-id="0d978-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="0d978-109">從每個工廠 hello 記錄檔會儲存在不同的內部部署 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0d978-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="0d978-110">hello 公司想 toobuild hello 雲端中的單一資料倉儲進行臨機操作分析。</span><span class="sxs-lookup"><span data-stu-id="0d978-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="0d978-111">它也會想 toohave hello 相同邏輯，但不同的組態，用於開發、 測試和實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0d978-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="0d978-112">在此情況下，工作都必須重複 toobe 內 hello 相同環境中，但具有不同的值跨 hello 的每個製造工廠的 10 個 data factory。</span><span class="sxs-lookup"><span data-stu-id="0d978-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="0d978-113">實際上，具有**重複**情況。</span><span class="sxs-lookup"><span data-stu-id="0d978-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="0d978-114">樣板化可讓此泛型流程 hello 抽象 （也就是管線有 hello 每個 data factory 中的相同活動），但是會使用每個製造工廠個別參數檔案。</span><span class="sxs-lookup"><span data-stu-id="0d978-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="0d978-115">此外，如 hello 的組織想 toodeploy 這些 10 的 data factory 多次不同環境下，範本可以使用這個**重複使用性**藉由使用不同的參數檔案進行開發，測試，和實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0d978-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="0d978-116">使用 Azure Resource Manager 範本化</span><span class="sxs-lookup"><span data-stu-id="0d978-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="0d978-117">[Azure 資源管理員範本](../azure-resource-manager/resource-group-overview.md#template-deployment)是 Azure Data Factory 中的絕佳方式，tooachieve 樣板化。</span><span class="sxs-lookup"><span data-stu-id="0d978-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="0d978-118">資源管理員範本定義 hello 基礎結構和 Azure 方案的組態，透過 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d978-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="0d978-119">因為 Azure 資源管理員範本不適用於所有/大部分 Azure 服務，它可以廣泛用於 tooeasily 管理您的 Azure 資產的所有資源。</span><span class="sxs-lookup"><span data-stu-id="0d978-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="0d978-120">請參閱[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)toolearn 深入了解一般 hello 資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="0d978-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="0d978-121">教學課程</span><span class="sxs-lookup"><span data-stu-id="0d978-121">Tutorials</span></span>
<span data-ttu-id="0d978-122">Hello 遵循逐步指示 toocreate Data Factory 實體的教學課程使用的資源管理員範本，請參閱：</span><span class="sxs-lookup"><span data-stu-id="0d978-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="0d978-123">教學課程： 使用 Azure Resource Manager 範本來建立管線 toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="0d978-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="0d978-124">教學課程： 使用 Azure Resource Manager 範本來建立管線 tooprocess 資料</span><span class="sxs-lookup"><span data-stu-id="0d978-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="0d978-125">GitHub 上的 Data Factory 範本</span><span class="sxs-lookup"><span data-stu-id="0d978-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="0d978-126">請參閱下列 Azure 快速入門範本 GitHub 上的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d978-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="0d978-127">從 Azure Blob 儲存體 tooAzure SQL 資料庫建立資料處理站 toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="0d978-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="0d978-128">在 Azure HDInsight 叢集上使用 Hive 活動建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="0d978-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="0d978-129">建立資料處理站 toocopy 資料從 Salesforce tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="0d978-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="0d978-130">建立鏈結活動的 Data factory： 將資料從 FTP 伺服器複製 tooAzure Blob 叫用 hive 指令碼-隨選 HDInsight 叢集 tootransform hello 資料，並將結果複製到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0d978-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="0d978-131">感覺可用 tooshare 您 Azure Data Factory 的範本在[Azure 快速入門](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="0d978-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="0d978-132">請參閱 toohello[參與指南](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE)開發的範本，可以透過這個儲存機制共用時。</span><span class="sxs-lookup"><span data-stu-id="0d978-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="0d978-133">hello 下列各節提供有關資源管理員範本中定義 Data Factory 的資源的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0d978-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="0d978-134">在範本中定義 Data Factory 資源</span><span class="sxs-lookup"><span data-stu-id="0d978-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="0d978-135">hello 定義的資料處理站的最上層範本是：</span><span class="sxs-lookup"><span data-stu-id="0d978-135">hello top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="0d978-136">定義資料處理站</span><span class="sxs-lookup"><span data-stu-id="0d978-136">Define data factory</span></span>
<span data-ttu-id="0d978-137">Hello 下列範例所示，您可以定義在 hello Resource Manager 範本中的 data factory:</span><span class="sxs-lookup"><span data-stu-id="0d978-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="0d978-138">hello dataFactoryName 「 變數 」 中定義為：</span><span class="sxs-lookup"><span data-stu-id="0d978-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="0d978-139">定義連結服務</span><span class="sxs-lookup"><span data-stu-id="0d978-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="0d978-140">請參閱[儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)或[計算連結服務](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)想 toodeploy hello hello 特定連結服務的 JSON 屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0d978-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="0d978-141">hello"dependsOn"參數指定 hello 對應的 data factory 的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d978-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="0d978-142">定義 Azure 儲存體連結的服務的範例所示 hello 下列 JSON 定義：</span><span class="sxs-lookup"><span data-stu-id="0d978-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="0d978-143">定義資料集</span><span class="sxs-lookup"><span data-stu-id="0d978-143">Define datasets</span></span>

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
<span data-ttu-id="0d978-144">請參閱太[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)想 toodeploy hello hello 特定的資料集類型的 JSON 屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0d978-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="0d978-145">注意 hello"dependsOn"參數指定名稱的 hello 相對應的資料處理站和儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="0d978-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="0d978-146">Hello 下列 JSON 定義中顯示的 Azure blob 儲存體的資料集型別定義範例：</span><span class="sxs-lookup"><span data-stu-id="0d978-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="0d978-147">定義管線</span><span class="sxs-lookup"><span data-stu-id="0d978-147">Define pipelines</span></span>

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

<span data-ttu-id="0d978-148">請參閱太[定義管線](data-factory-create-pipelines.md#pipeline-json)hello 用於定義的 JSON 屬性的詳細 hello 特定管線和活動為您想 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="0d978-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="0d978-149">請注意 hello"dependsOn 」 參數會指定 hello data factory，名稱和任何對應的連結的服務或資料集。</span><span class="sxs-lookup"><span data-stu-id="0d978-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="0d978-150">將資料從 Azure Blob 儲存體 tooAzure SQL 資料庫複製 」 管線的範例所示 hello 下列 JSON 片段：</span><span class="sxs-lookup"><span data-stu-id="0d978-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="0d978-151">參數化 Data Factory 範本</span><span class="sxs-lookup"><span data-stu-id="0d978-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="0d978-152">如需參數化的最佳作法，請參閱[建立 Azure Resource Manager 範本的最佳作法](../azure-resource-manager/resource-manager-template-best-practices.md#parameters)一文。</span><span class="sxs-lookup"><span data-stu-id="0d978-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="0d978-153">一般而言，參數的使用應該降到最低，特別是改為使用變數時。</span><span class="sxs-lookup"><span data-stu-id="0d978-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="0d978-154">只提供 hello 下列案例中的參數：</span><span class="sxs-lookup"><span data-stu-id="0d978-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="0d978-155">設定會因環境 (範例︰開發、測試和生產) 而不同</span><span class="sxs-lookup"><span data-stu-id="0d978-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="0d978-156">機密資料 (例如密碼)</span><span class="sxs-lookup"><span data-stu-id="0d978-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="0d978-157">如果您需要從 toopull 密碼[Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)部署時使用範本的 Azure Data Factory 實體，指定 hello**金鑰保存庫**和**秘密名稱**中所示下列範例的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d978-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

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
> <span data-ttu-id="0d978-158">雖然匯出範本，現有的 data factory 的目前尚未支援，則為 hello 運作。</span><span class="sxs-lookup"><span data-stu-id="0d978-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
