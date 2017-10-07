---
title: "aaaAzure PowerShell 指令碼範例-建立 web 應用程式和部署程式碼從本機 Git 儲存機制 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 建立 Web 應用程式並從本機 Git 存放庫部署程式碼"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="50957-103">建立 Web 應用程式並從本機 Git 存放庫部署程式碼</span><span class="sxs-lookup"><span data-stu-id="50957-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="50957-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後在本機 Git 存放庫中部署 Web 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="50957-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="50957-105">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="50957-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="50957-106">此外，應用程式程式碼必須 toobe 認可到本機的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="50957-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="50957-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="50957-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="50957-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="50957-108">Clean up deployment</span></span> 

<span data-ttu-id="50957-109">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="50957-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="50957-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="50957-110">Script explanation</span></span>

<span data-ttu-id="50957-111">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="50957-111">This script uses hello following commands.</span></span> <span data-ttu-id="50957-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="50957-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="50957-113">命令</span><span class="sxs-lookup"><span data-stu-id="50957-113">Command</span></span> | <span data-ttu-id="50957-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="50957-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="50957-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="50957-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="50957-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="50957-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="50957-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="50957-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="50957-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="50957-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="50957-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="50957-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="50957-120">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="50957-120">Creates a web app.</span></span> |
| [<span data-ttu-id="50957-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="50957-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="50957-122">修改資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="50957-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="50957-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="50957-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="50957-124">取得 Web 應用程式的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="50957-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50957-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50957-125">Next steps</span></span>

<span data-ttu-id="50957-126">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="50957-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="50957-127">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="50957-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
