---
title: "Azure PowerShell 指令碼範例 - 部署範本 | Microsoft Docs"
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
ms.openlocfilehash: b7a7dda1da653d084e02e6724d2f0cb5aa76807a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="f9871-103">Azure Resource Manager 範本部署 - PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="f9871-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="f9871-104">此指令碼會將 Resource Manager 範本部署到您的訂用帳戶中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f9871-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f9871-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="f9871-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template to Azure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #The subscription id where the template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #The resource group where the template will be deployed. Can be the name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try to create a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #The deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path to the template file. Defaults to template.json.
    [string]$TemplateFilePath = "template.json",  

    #Path to the parameters file. Defaults to parameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login to Azure and select subscription
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

# Start the deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="f9871-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="f9871-106">Clean up deployment</span></span> 

<span data-ttu-id="f9871-107">執行下列命令來移除資源群組和其所有資源。</span><span class="sxs-lookup"><span data-stu-id="f9871-107">Run the following command to remove the resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f9871-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="f9871-108">Script explanation</span></span>

<span data-ttu-id="f9871-109">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="f9871-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="f9871-110">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="f9871-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f9871-111">命令</span><span class="sxs-lookup"><span data-stu-id="f9871-111">Command</span></span> | <span data-ttu-id="f9871-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="f9871-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f9871-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="f9871-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="f9871-114">註冊資源提供者，使其資源類型可以部署到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f9871-114">Registers a resource provider so its resource types can be deployed to your subscription.</span></span>  |
| [<span data-ttu-id="f9871-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f9871-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="f9871-116">取得資源群組。</span><span class="sxs-lookup"><span data-stu-id="f9871-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="f9871-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f9871-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f9871-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f9871-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f9871-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="f9871-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="f9871-120">將 Azure 部署加入資源群組。</span><span class="sxs-lookup"><span data-stu-id="f9871-120">Adds an Azure deployment to a resource group.</span></span>  |
| [<span data-ttu-id="f9871-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f9871-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f9871-122">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="f9871-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="f9871-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9871-123">Next steps</span></span>
* <span data-ttu-id="f9871-124">如需部署範本的簡介，請參閱[使用 Resource Manager 範本與 Azure PowerShell 來部署資源](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="f9871-124">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="f9871-125">如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。</span><span class="sxs-lookup"><span data-stu-id="f9871-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="f9871-126">若要在範本中定義參數，請參閱 [編寫範本](resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="f9871-126">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="f9871-127">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="f9871-127">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

