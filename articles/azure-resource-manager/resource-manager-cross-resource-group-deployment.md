---
title: "將 Azure 資源部署至多個資源群組 | Microsoft Docs"
description: "示範如何在部署期間將目標放在多個 Azure 資源群組。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="3376a-103">將 Azure 資源部署至多個資源群組</span><span class="sxs-lookup"><span data-stu-id="3376a-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="3376a-104">一般而言，您要將範本中的所有資源部署至單一資源群組。</span><span class="sxs-lookup"><span data-stu-id="3376a-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="3376a-105">不過，在某些情況下，您要將一組資源部署在一起，但將它們放在不同的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="3376a-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="3376a-106">例如，建議您將 Azure Site Recovery 的備份虛擬機器部署至不同的資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="3376a-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="3376a-107">Resource Manager 可讓您使用巢狀的範本，將目標放在與父系範本所使用之資源群組不同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3376a-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="3376a-108">資源群組是應用程式及其資源集合的生命週期容器。</span><span class="sxs-lookup"><span data-stu-id="3376a-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="3376a-109">您要建立樣板之外的資源群組，並指定要在部署期間作為目標的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3376a-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="3376a-110">如需資源群組的簡介，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3376a-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="3376a-111">範本範例</span><span class="sxs-lookup"><span data-stu-id="3376a-111">Example template</span></span>

<span data-ttu-id="3376a-112">若要將目標放在不同的資源，您必須在部署期間使用巢狀或連結的範本。</span><span class="sxs-lookup"><span data-stu-id="3376a-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="3376a-113">`Microsoft.Resources/deployments` 資源類型會提供`resourceGroup` 參數，可讓您為巢狀部署指定不同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3376a-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="3376a-114">執行部署之前，所有資源群組都必須存在。</span><span class="sxs-lookup"><span data-stu-id="3376a-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="3376a-115">下列範例會部署兩個儲存體帳戶 - 一個是在部署期間指定的資源群組中，另一個是在名為 `crossResourceGroupDeployment` 的資源群組中：</span><span class="sxs-lookup"><span data-stu-id="3376a-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

<span data-ttu-id="3376a-116">如果您將 `resourceGroup` 設定為不存在的資源群組名稱，部署就會失敗。</span><span class="sxs-lookup"><span data-stu-id="3376a-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="3376a-117">如果您未提供 `resourceGroup` 的值，Resource Manager 就會使用父系資源群組。</span><span class="sxs-lookup"><span data-stu-id="3376a-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="3376a-118">部署範本</span><span class="sxs-lookup"><span data-stu-id="3376a-118">Deploy the template</span></span>

<span data-ttu-id="3376a-119">若要部署範例範本，您可以使用入口網站、Azure PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="3376a-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="3376a-120">若是使用 Azure PowerShell 或 Azure CLI，您必須使用 2017年 5 月或更新版本。</span><span class="sxs-lookup"><span data-stu-id="3376a-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="3376a-121">這些範例會假設您已在本機將範本儲存為名為 **crossrgdeployment.json** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="3376a-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="3376a-122">對於 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="3376a-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="3376a-123">對於 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="3376a-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="3376a-124">部署完成後，您會看到兩個資源群組。</span><span class="sxs-lookup"><span data-stu-id="3376a-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="3376a-125">每個資源群組都包含儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3376a-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="3376a-126">使用 resourceGroup() 函數</span><span class="sxs-lookup"><span data-stu-id="3376a-126">Use resourceGroup() function</span></span>

<span data-ttu-id="3376a-127">對於跨資源群組部署，[resouceGroup() 函數](resource-group-template-functions-resource.md#resourcegroup)會根據您指定巢狀範本的方式，以不同的方式進行解析。</span><span class="sxs-lookup"><span data-stu-id="3376a-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="3376a-128">如果您將某個範本內嵌於另一個範本內，巢狀範本中的 resouceGroup() 會解析至父資源群組。</span><span class="sxs-lookup"><span data-stu-id="3376a-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="3376a-129">內嵌範本會使用下列格式：</span><span class="sxs-lookup"><span data-stu-id="3376a-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="3376a-130">如果您連結至個別範本，連結範本中的 resouceGroup() 會解析至巢狀資源群組。</span><span class="sxs-lookup"><span data-stu-id="3376a-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="3376a-131">連結範本會使用下列格式：</span><span class="sxs-lookup"><span data-stu-id="3376a-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="3376a-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3376a-132">Next steps</span></span>

* <span data-ttu-id="3376a-133">若要了解如何在您的範本中定義參數，請參閱[了解 Azure Resource Manager 範本的結構和語法](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="3376a-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3376a-134">如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="3376a-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="3376a-135">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="3376a-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
