---
title: "aaaAzure PowerShell 指令碼範例-建立 web 應用程式和部署程式碼從 GitHub |Microsoft 文件"
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
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="9c642-103">建立 Web 應用程式並從 GitHub 部署程式碼</span><span class="sxs-lookup"><span data-stu-id="9c642-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="9c642-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後從公用 GitHub 存放庫部署 Web 應用程式程式碼 (不使用連續部署)。</span><span class="sxs-lookup"><span data-stu-id="9c642-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="9c642-105">如需進行使用連續部署的 GitHub 部署，請參閱[建立可從 GitHub 連續部署的 Web 應用程式](app-service-powershell-continuous-deployment-github.md)。</span><span class="sxs-lookup"><span data-stu-id="9c642-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="9c642-106">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9c642-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="9c642-107">此外，您需要包含 hello web 應用程式程式碼的連結 tooGitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9c642-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="9c642-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="9c642-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9c642-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="9c642-109">Clean up deployment</span></span> 

<span data-ttu-id="9c642-110">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="9c642-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="9c642-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="9c642-111">Script explanation</span></span>

<span data-ttu-id="9c642-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="9c642-112">This script uses hello following commands.</span></span> <span data-ttu-id="9c642-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="9c642-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9c642-114">命令</span><span class="sxs-lookup"><span data-stu-id="9c642-114">Command</span></span> | <span data-ttu-id="9c642-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="9c642-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9c642-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9c642-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9c642-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9c642-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9c642-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="9c642-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="9c642-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="9c642-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9c642-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="9c642-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="9c642-121">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c642-121">Creates a web app.</span></span> |
| [<span data-ttu-id="9c642-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="9c642-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="9c642-123">修改資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="9c642-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c642-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c642-124">Next steps</span></span>

<span data-ttu-id="9c642-125">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9c642-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9c642-126">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="9c642-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
