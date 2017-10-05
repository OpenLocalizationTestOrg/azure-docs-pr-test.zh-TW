---
title: "Azure PowerShell 指令碼範例 - 建立 Web 應用程式並從 GitHub 部署程式碼 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 建立 Web 應用程式並從 GitHub 部署程式碼"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1f7fc21dc12c334f5d347ae9918bd62945bede64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="6bcbe-103">建立 Web 應用程式並從 GitHub 部署程式碼</span><span class="sxs-lookup"><span data-stu-id="6bcbe-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="6bcbe-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後從公用 GitHub 存放庫部署 Web 應用程式程式碼 (不使用連續部署)。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="6bcbe-105">如需進行使用連續部署的 GitHub 部署，請參閱[建立可從 GitHub 連續部署的 Web 應用程式](app-service-powershell-continuous-deployment-github.md)。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="6bcbe-106">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="6bcbe-107">此外，您需要包含 Web 應用程式程式碼的 GitHub 儲存機制的連結。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-107">Also, you need a link to GitHub repository that contains the web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6bcbe-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="6bcbe-108">Sample script</span></span>

<span data-ttu-id="6bcbe-109">[!code-powershell[主要](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "建立 Web 應用程式並從 GitHub 部署程式碼")]</span><span class="sxs-lookup"><span data-stu-id="6bcbe-109">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6bcbe-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="6bcbe-110">Clean up deployment</span></span> 

<span data-ttu-id="6bcbe-111">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-111">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6bcbe-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="6bcbe-112">Script explanation</span></span>

<span data-ttu-id="6bcbe-113">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-113">This script uses the following commands.</span></span> <span data-ttu-id="6bcbe-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6bcbe-115">命令</span><span class="sxs-lookup"><span data-stu-id="6bcbe-115">Command</span></span> | <span data-ttu-id="6bcbe-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="6bcbe-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6bcbe-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6bcbe-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6bcbe-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6bcbe-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6bcbe-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6bcbe-120">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6bcbe-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6bcbe-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6bcbe-122">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-122">Creates a web app.</span></span> |
| [<span data-ttu-id="6bcbe-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="6bcbe-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="6bcbe-124">修改資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-124">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6bcbe-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bcbe-125">Next steps</span></span>

<span data-ttu-id="6bcbe-126">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6bcbe-127">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="6bcbe-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
