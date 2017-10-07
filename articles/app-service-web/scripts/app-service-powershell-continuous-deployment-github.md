---
title: "aaaAzure PowerShell 指令碼範例-使用來自 GitHub 的連續部署建立 web 應用程式 |Microsoft 文件"
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
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="4ba5e-103">建立可從 GitHub 連續部署的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4ba5e-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="4ba5e-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後設定從 GitHub 存放庫進行的連續部署。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="4ba5e-105">如需進行沒有連續部署的 GitHub 部署，請參閱[建立 Web 應用程式並從 GitHub 部署程式碼](app-service-powershell-deploy-github.md)。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="4ba5e-106">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="4ba5e-107">此外，請確定：</span><span class="sxs-lookup"><span data-stu-id="4ba5e-107">Also, ensure that:</span></span>

- <span data-ttu-id="4ba5e-108">已建立與 Azure 的連線使用 hello`az login`命令。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="4ba5e-109">hello 應用程式程式碼是您所擁有的公用或私用 GitHub 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="4ba5e-110">您已[在 GitHub 帳戶中建立存取權杖](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="4ba5e-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4ba5e-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4ba5e-112">清除部署</span><span class="sxs-lookup"><span data-stu-id="4ba5e-112">Clean up deployment</span></span> 

<span data-ttu-id="4ba5e-113">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4ba5e-114">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="4ba5e-114">Script explanation</span></span>

<span data-ttu-id="4ba5e-115">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-115">This script uses hello following commands.</span></span> <span data-ttu-id="4ba5e-116">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4ba5e-117">命令</span><span class="sxs-lookup"><span data-stu-id="4ba5e-117">Command</span></span> | <span data-ttu-id="4ba5e-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="4ba5e-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4ba5e-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4ba5e-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4ba5e-120">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4ba5e-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4ba5e-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4ba5e-122">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4ba5e-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4ba5e-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4ba5e-124">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-124">Creates a web app.</span></span> |
| [<span data-ttu-id="4ba5e-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4ba5e-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="4ba5e-126">修改資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4ba5e-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ba5e-127">Next steps</span></span>

<span data-ttu-id="4ba5e-128">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4ba5e-129">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="4ba5e-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
