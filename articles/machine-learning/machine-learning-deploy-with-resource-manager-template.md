---
title: "使用 Azure Resource Manager 部署 Machine Learning 工作區 | Microsoft Docs"
description: "如何使用 Azure Resource Manager 範本部署 Azure Machine Learning 的工作區"
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
ms.openlocfilehash: 9e37780428b0867da63987ec4f7f843a8abeb907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="72663-103">使用 Azure Resource Manager 部署 Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="72663-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="72663-104">簡介</span><span class="sxs-lookup"><span data-stu-id="72663-104">Introduction</span></span>
<span data-ttu-id="72663-105">使用 Azure Resource Manager 部署範本提供了可擴充的方式來部署具有驗證和重試機制的互連元件，為您節省時間。</span><span class="sxs-lookup"><span data-stu-id="72663-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="72663-106">若要設定 Azure Machine Learning 工作區，例如，您需要先設定 Azure 儲存體帳戶，然後再部署您的工作區。</span><span class="sxs-lookup"><span data-stu-id="72663-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="72663-107">假想您要對數百個工作區手動進行此動作。</span><span class="sxs-lookup"><span data-stu-id="72663-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="72663-108">簡單的替代方法是使用 Azure Resource Manager 範本來部署 Azure Machine Learning 工作區和所有相依性。</span><span class="sxs-lookup"><span data-stu-id="72663-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="72663-109">這篇文章會帶領您逐步完成此程序。</span><span class="sxs-lookup"><span data-stu-id="72663-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="72663-110">如需 Azure Resource Manager 的詳細概觀，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="72663-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="72663-111">逐步說明：建立 Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="72663-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="72663-112">我們將建立 Azure 資源群組，然後使用 Resource Manager 範本部署新的 Azure 儲存體帳戶和新的 Azure Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="72663-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="72663-113">部署完成之後，我們會印出所建立的工作區的重要資訊 (主索引鍵、工作區識別碼和工作區的 URL)。</span><span class="sxs-lookup"><span data-stu-id="72663-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="72663-114">建立 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="72663-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="72663-115">Machine Learning 工作區需有 Azure 儲存體帳戶來儲存連結到它的資料集。</span><span class="sxs-lookup"><span data-stu-id="72663-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span></span>
<span data-ttu-id="72663-116">以下範本會使用資源群組的名稱來產生儲存體帳戶名稱和工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="72663-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span></span>  <span data-ttu-id="72663-117">建立工作區時，它也會使用儲存體帳戶名稱做為屬性。</span><span class="sxs-lookup"><span data-stu-id="72663-117">It also uses the storage account name as a property when creating the workspace.</span></span>

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
<span data-ttu-id="72663-118">將此範本在 c:\temp\ 下儲存為 mlworkspace.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="72663-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-the-resource-group-based-on-the-template"></a><span data-ttu-id="72663-119">依據範本部署資源群組</span><span class="sxs-lookup"><span data-stu-id="72663-119">Deploy the resource group, based on the template</span></span>
* <span data-ttu-id="72663-120">開啟 PowerShell</span><span class="sxs-lookup"><span data-stu-id="72663-120">Open PowerShell</span></span>
* <span data-ttu-id="72663-121">安裝 Azure Resource Manager 和 Azure 服務管理的模組</span><span class="sxs-lookup"><span data-stu-id="72663-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install the Azure Resource Manager modules from the PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install the Azure Service Management modules from the PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="72663-122">下列步驟會下載並安裝完成剩餘步驟所需的模組。</span><span class="sxs-lookup"><span data-stu-id="72663-122">These steps download and install the modules necessary to complete the remaining steps.</span></span> <span data-ttu-id="72663-123">這只需要在您執行 PowerShell 命令的環境中執行一次。</span><span class="sxs-lookup"><span data-stu-id="72663-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span></span>   

* <span data-ttu-id="72663-124">向 Azure 驗證</span><span class="sxs-lookup"><span data-stu-id="72663-124">Authenticate to Azure</span></span>  

```
# Authenticate (enter your credentials in the pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="72663-125">需要為每個工作階段重複執行這個步驟。</span><span class="sxs-lookup"><span data-stu-id="72663-125">This step needs to be repeated for each session.</span></span> <span data-ttu-id="72663-126">驗證之後，應該會顯示您的訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="72663-126">Once authenticated, your subscription information should be displayed.</span></span>

![Azure 帳戶][1]

<span data-ttu-id="72663-128">現在，我們已經可以存取 Azure，便可以建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="72663-128">Now that we have access to Azure, we can create the resource group.</span></span>

* <span data-ttu-id="72663-129">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="72663-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="72663-130">請確認資源群組已正確佈建。</span><span class="sxs-lookup"><span data-stu-id="72663-130">Verify that the resource group is correctly provisioned.</span></span> <span data-ttu-id="72663-131">**ProvisioningState** 應該是 “Succeeded”。</span><span class="sxs-lookup"><span data-stu-id="72663-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="72663-132">範本會使用資源群組名稱來產生儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="72663-132">The resource group name is used by the template to generate the storage account name.</span></span> <span data-ttu-id="72663-133">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能使用數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="72663-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![資源群組][2]

* <span data-ttu-id="72663-135">使用資源群組部署，部署新的 Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="72663-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is the location of the JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="72663-136">一旦完成部署之後，就可以直接存取您所部署的工作區的屬性。</span><span class="sxs-lookup"><span data-stu-id="72663-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span></span> <span data-ttu-id="72663-137">例如，您可以存取主要金鑰權杖。</span><span class="sxs-lookup"><span data-stu-id="72663-137">For example, you can access the Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="72663-138">另一種擷取現有工作區權杖的方式是使用 Invoke-AzureRmResourceAction 命令。</span><span class="sxs-lookup"><span data-stu-id="72663-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="72663-139">例如，您可以列出所有工作區的主要和次要權杖。</span><span class="sxs-lookup"><span data-stu-id="72663-139">For example, you can list the primary and secondary tokens of all workspaces.</span></span>

```  
# List the primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="72663-140">佈建工作區之後，您也可以使用 [適用於 Azure Machine Learning 的 PowerShell 模組](http://aka.ms/amlps)將許多 Azure Machine Learning Studio 工作自動化。</span><span class="sxs-lookup"><span data-stu-id="72663-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72663-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72663-141">Next Steps</span></span>
* <span data-ttu-id="72663-142">深入了解 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="72663-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="72663-143">看看 [Azure 快速入門範本儲存機制](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="72663-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="72663-144">觀看這段 [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39)影片。</span><span class="sxs-lookup"><span data-stu-id="72663-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
