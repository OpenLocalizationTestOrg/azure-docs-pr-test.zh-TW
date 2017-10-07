---
title: "aaaDeploy Machine Learning 工作區與 Azure Resource Manager |Microsoft 文件"
description: "如何 toodeploy Azure Machine Learning 使用 Azure Resource Manager 範本的工作區"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="cc5f0-103">使用 Azure Resource Manager 部署 Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="cc5f0-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="cc5f0-104">簡介</span><span class="sxs-lookup"><span data-stu-id="cc5f0-104">Introduction</span></span>
<span data-ttu-id="cc5f0-105">使用 Azure 資源管理員部署範本為您節省時間，提供可擴充的方式 toodeploy 相互連接與驗證和重試機制元件。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="cc5f0-106">tooset 向上 Azure 機器學習服務工作區，例如，您需要 toofirst 設定 Azure 儲存體帳戶，然後再部署您的工作區。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="cc5f0-107">假想您要對數百個工作區手動進行此動作。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="cc5f0-108">簡單的替代方式是 toouse Azure Resource Manager 範本 toodeploy Azure 機器學習服務工作區和所有相依性。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="cc5f0-109">這篇文章會帶領您逐步完成此程序。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="cc5f0-110">如需 Azure Resource Manager 的詳細概觀，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="cc5f0-111">逐步說明：建立 Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="cc5f0-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="cc5f0-112">我們將建立 Azure 資源群組，然後使用 Resource Manager 範本部署新的 Azure 儲存體帳戶和新的 Azure Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="cc5f0-113">Hello 部署完成之後，我們會印出 hello （hello 主索引鍵、 hello 工作區識別碼和工作區中的 URL toohello hello） 所建立的工作區的相關重要資訊。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="cc5f0-114">建立 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="cc5f0-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="cc5f0-115">機器學習服務工作區需要 Azure 儲存體帳戶 toostore hello 連結的資料集 tooit。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="cc5f0-116">hello 下列範本會使用 hello 名稱 hello 資源群組 toogenerate hello 儲存體帳戶名稱和 hello 工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="cc5f0-117">它也會使用 hello 儲存體帳戶名稱做為屬性建立 hello 工作區時。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
<span data-ttu-id="cc5f0-118">將此範本在 c:\temp\ 下儲存為 mlworkspace.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="cc5f0-119">部署 hello 範本為基礎的 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="cc5f0-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="cc5f0-120">開啟 PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc5f0-120">Open PowerShell</span></span>
* <span data-ttu-id="cc5f0-121">安裝 Azure Resource Manager 和 Azure 服務管理的模組</span><span class="sxs-lookup"><span data-stu-id="cc5f0-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="cc5f0-122">下列步驟下載並安裝 hello 模組需要 toocomplete hello 其餘步驟。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="cc5f0-123">這個動作只需要 toobe hello 執行 hello PowerShell 命令所在的環境中，執行一次。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="cc5f0-124">驗證 tooAzure</span><span class="sxs-lookup"><span data-stu-id="cc5f0-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="cc5f0-125">此步驟需要 toobe 重複每個工作階段。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="cc5f0-126">驗證之後，應該會顯示您的訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-126">Once authenticated, your subscription information should be displayed.</span></span>

![Azure 帳戶][1]

<span data-ttu-id="cc5f0-128">既然我們已經有存取 tooAzure，我們可以建立 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="cc5f0-129">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="cc5f0-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="cc5f0-130">請確認已正確佈建 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="cc5f0-131">**ProvisioningState** 應該是 “Succeeded”。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="cc5f0-132">hello 資源群組名稱會使用 hello 範本 toogenerate hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="cc5f0-133">hello 儲存體帳戶名稱必須介於 3 到 24 個字元的長度，並使用數字和小寫的字母。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![資源群組][2]

* <span data-ttu-id="cc5f0-135">使用 hello 資源群組部署，部署新的機器學習服務工作區。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="cc5f0-136">一旦 hello 部署完成之後，就是您部署的 hello] 工作區的直接 tooaccess 屬性。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="cc5f0-137">例如，您可以存取 hello 主要金鑰語彙基元。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="cc5f0-138">現有的工作區的另一個方式 tooretrieve 語彙基元為 toouse hello Invoke AzureRmResourceAction 命令。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="cc5f0-139">例如，您可以列出所有工作區的 hello 主要和次要的權杖。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="cc5f0-140">Hello 工作區中佈建之後，您也可以自動化許多 Azure Machine Learning Studio 工作使用 hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps)。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc5f0-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc5f0-141">Next Steps</span></span>
* <span data-ttu-id="cc5f0-142">深入了解 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="cc5f0-143">看看 hello [Azure 快速入門範本儲存機制](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="cc5f0-144">觀看這段 [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39)影片。</span><span class="sxs-lookup"><span data-stu-id="cc5f0-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
