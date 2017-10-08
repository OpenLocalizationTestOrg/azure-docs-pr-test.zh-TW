---
title: "aaaDeploy Azure 資源 toomultiple 資源群組 |Microsoft 文件"
description: "顯示如何 tootarget 以上的一項 Azure 資源群組部署期間。"
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
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="2a2bc-103">部署 Azure 資源 toomore 比一個資源群組</span><span class="sxs-lookup"><span data-stu-id="2a2bc-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="2a2bc-104">一般而言，您可以部署所有 hello 資源範本 tooa 單一資源群組中。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="2a2bc-105">不過，有一些當您一起想 toodeploy 一組資源，但將它們放在不同的資源群組的案例。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="2a2bc-106">例如，您可能想 toodeploy hello 備份虛擬機器的 Azure Site Recovery tooa 個別資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="2a2bc-107">資源管理員可讓您 toouse 巢狀範本 tootarget 不同的資源群組與 hello hello 父樣板使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="2a2bc-108">hello 資源群組都 hello hello 應用程式生命週期容器和它的資源的集合。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="2a2bc-109">您建立 hello hello 範本以外的資源群組，並指定在部署期間的 hello 資源群組 tootarget。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="2a2bc-110">對於簡介 tooresource 的群組，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="2a2bc-111">範本範例</span><span class="sxs-lookup"><span data-stu-id="2a2bc-111">Example template</span></span>

<span data-ttu-id="2a2bc-112">tootarget 不同的資源，您必須在部署期間使用巢狀或連結的範本。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="2a2bc-113">hello`Microsoft.Resources/deployments`資源類型提供`resourceGroup`參數，可讓您 toospecify hello 的不同資源群組巢狀部署。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="2a2bc-114">執行 hello 部署之前，必須有所有的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="2a2bc-115">hello 下列範例會將部署兩個儲存體帳戶-指定在部署期間，hello 資源群組中，名為資源群組中的另一個`crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="2a2bc-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="2a2bc-116">如果您設定`resourceGroup`toohello 不存在的資源群組名稱，hello 部署失敗。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="2a2bc-117">如果您未提供的值`resourceGroup`，資源管理員會使用 hello 父資源群組。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="2a2bc-118">部署 hello 範本</span><span class="sxs-lookup"><span data-stu-id="2a2bc-118">Deploy hello template</span></span>

<span data-ttu-id="2a2bc-119">toodeploy hello 範例範本，您可以使用 hello 入口網站、 Azure PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="2a2bc-120">若是使用 Azure PowerShell 或 Azure CLI，您必須使用 2017年 5 月或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="2a2bc-121">hello 範例假設您已在本機儲存 hello 範本，檔案名稱為**crossrgdeployment.json**。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="2a2bc-122">對於 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="2a2bc-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="2a2bc-123">對於 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="2a2bc-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="2a2bc-124">部署完成後，您會看到兩個資源群組。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="2a2bc-125">每個資源群組都包含儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="2a2bc-126">使用 resourceGroup() 函數</span><span class="sxs-lookup"><span data-stu-id="2a2bc-126">Use resourceGroup() function</span></span>

<span data-ttu-id="2a2bc-127">針對交叉資源群組部署，hello [resouceGroup() 函式](resource-group-template-functions-resource.md#resourcegroup)解析以不同的方式會根據您指定 hello 巢狀的樣板的方式。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="2a2bc-128">如果您內嵌在另一個範本內的一個範本，resouceGroup() hello 巢狀範本中的會解析 toohello 父資源群組。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="2a2bc-129">內嵌的範本會使用下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a2bc-129">An embedded template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

<span data-ttu-id="2a2bc-130">如果您將連結 tooa 另一個範本，resouceGroup() hello 連結的範本中會解析 toohello 巢狀的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="2a2bc-131">連結的範本會使用下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a2bc-131">A linked template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2a2bc-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a2bc-132">Next steps</span></span>

* <span data-ttu-id="2a2bc-133">如何 toodefine 參數在範本中，請參閱的 toounderstand [hello 結構和語法的 Azure 資源管理員範本了解](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2a2bc-134">如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="2a2bc-135">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="2a2bc-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
