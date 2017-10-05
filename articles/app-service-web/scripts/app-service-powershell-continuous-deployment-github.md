---
title: "Azure PowerShell 指令碼範例 - 建立可從 GitHub 連續部署的 Web 應用程式 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 建立可從 GitHub 連續部署的 Web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="4f826-103">建立可從 GitHub 連續部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4f826-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="4f826-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後設定從 GitHub 存放庫進行的連續部署。</span><span class="sxs-lookup"><span data-stu-id="4f826-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="4f826-105">如需進行沒有連續部署的 GitHub 部署，請參閱[建立 Web 應用程式並從 GitHub 部署程式碼](app-service-powershell-deploy-github.md)。</span><span class="sxs-lookup"><span data-stu-id="4f826-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="4f826-106">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4f826-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="4f826-107">此外，請確定：</span><span class="sxs-lookup"><span data-stu-id="4f826-107">Also, ensure that:</span></span>

- <span data-ttu-id="4f826-108">已使用 `az login` 命令建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="4f826-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="4f826-109">應用程式的程式碼位於您擁有的公用或私人 GitHub 存放庫。</span><span class="sxs-lookup"><span data-stu-id="4f826-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="4f826-110">您已[在 GitHub 帳戶中建立存取權杖](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)。</span><span class="sxs-lookup"><span data-stu-id="4f826-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="4f826-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4f826-111">Sample script</span></span>

<span data-ttu-id="4f826-112">[!code-powershell[主要](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "建立可從 GitHub 連續部署的 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="4f826-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4f826-113">清除部署</span><span class="sxs-lookup"><span data-stu-id="4f826-113">Clean up deployment</span></span> 

<span data-ttu-id="4f826-114">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="4f826-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4f826-115">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="4f826-115">Script explanation</span></span>

<span data-ttu-id="4f826-116">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="4f826-116">This script uses the following commands.</span></span> <span data-ttu-id="4f826-117">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="4f826-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4f826-118">命令</span><span class="sxs-lookup"><span data-stu-id="4f826-118">Command</span></span> | <span data-ttu-id="4f826-119">注意事項</span><span class="sxs-lookup"><span data-stu-id="4f826-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4f826-120">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4f826-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4f826-121">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4f826-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4f826-122">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4f826-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4f826-123">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4f826-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4f826-124">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4f826-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4f826-125">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4f826-125">Creates a web app.</span></span> |
| [<span data-ttu-id="4f826-126">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4f826-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="4f826-127">修改資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="4f826-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4f826-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f826-128">Next steps</span></span>

<span data-ttu-id="4f826-129">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4f826-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4f826-130">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="4f826-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
