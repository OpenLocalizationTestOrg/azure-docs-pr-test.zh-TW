---
title: "PowerShell 指令碼範例-aaaAzure 部署範本 |Microsoft 文件"
description: "部署 Azure Resource Manager 範本的範例指令碼。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="21d31-103">Azure Resource Manager 範本部署 - PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="21d31-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="21d31-104">此指令碼會將部署您的訂用帳戶中資源管理員範本 tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="21d31-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="21d31-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="21d31-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="21d31-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="21d31-106">Clean up deployment</span></span> 

<span data-ttu-id="21d31-107">Hello 執行的下列命令 tooremove hello 資源群組和其所有資源。</span><span class="sxs-lookup"><span data-stu-id="21d31-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="21d31-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="21d31-108">Script explanation</span></span>

<span data-ttu-id="21d31-109">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="21d31-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="21d31-110">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="21d31-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="21d31-111">命令</span><span class="sxs-lookup"><span data-stu-id="21d31-111">Command</span></span> | <span data-ttu-id="21d31-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="21d31-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="21d31-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="21d31-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="21d31-114">因此其資源類型可以是已部署的 tooyour 訂用帳戶註冊資源提供者。</span><span class="sxs-lookup"><span data-stu-id="21d31-114">Registers a resource provider so its resource types can be deployed tooyour subscription.</span></span>  |
| [<span data-ttu-id="21d31-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="21d31-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="21d31-116">取得資源群組。</span><span class="sxs-lookup"><span data-stu-id="21d31-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="21d31-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="21d31-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="21d31-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="21d31-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="21d31-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="21d31-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="21d31-120">新增 Azure 部署 tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="21d31-120">Adds an Azure deployment tooa resource group.</span></span>  |
| [<span data-ttu-id="21d31-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="21d31-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="21d31-122">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="21d31-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="21d31-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21d31-123">Next steps</span></span>
* <span data-ttu-id="21d31-124">如簡介 toodeploying 範本，請參閱[部署資源與資源管理員範本和 Azure PowerShell](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="21d31-124">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="21d31-125">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="21d31-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="21d31-126">toodefine 參數在範本中，請參閱[撰寫樣板](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="21d31-126">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="21d31-127">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="21d31-127">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

