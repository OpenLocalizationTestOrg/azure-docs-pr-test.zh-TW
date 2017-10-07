---
title: "aaaAzure PowerShell 指令碼範例-建立 web 應用程式和部署程式碼 tooa 預備環境 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-建立 web 應用程式和部署程式碼 tooa 預備環境"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="38b55-103">建立 web 應用程式和部署程式碼 tooa 預備環境</span><span class="sxs-lookup"><span data-stu-id="38b55-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="38b55-104">這個範例指令碼應用程式服務中建立 web 應用程式呼叫 「 預備 」，其他的部署位置與，然後部署範例應用程式 toohello 「 預備 」 位置。</span><span class="sxs-lookup"><span data-stu-id="38b55-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="38b55-105">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="38b55-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="38b55-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="38b55-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="38b55-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="38b55-107">Clean up deployment</span></span> 

<span data-ttu-id="38b55-108">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="38b55-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="38b55-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="38b55-109">Script explanation</span></span>

<span data-ttu-id="38b55-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="38b55-110">This script uses hello following commands.</span></span> <span data-ttu-id="38b55-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="38b55-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="38b55-112">命令</span><span class="sxs-lookup"><span data-stu-id="38b55-112">Command</span></span> | <span data-ttu-id="38b55-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="38b55-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="38b55-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="38b55-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="38b55-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="38b55-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="38b55-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="38b55-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="38b55-117">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="38b55-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="38b55-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="38b55-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="38b55-119">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="38b55-119">Creates a web app.</span></span> |
| [<span data-ttu-id="38b55-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="38b55-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="38b55-121">修改應用程式服務計劃 toochange 其定價層。</span><span class="sxs-lookup"><span data-stu-id="38b55-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="38b55-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="38b55-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="38b55-123">建立 Web 應用程式的部署位置。</span><span class="sxs-lookup"><span data-stu-id="38b55-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="38b55-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="38b55-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="38b55-125">修改資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="38b55-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="38b55-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="38b55-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="38b55-127">將 Web 應用程式的部署位置切換到生產環境。</span><span class="sxs-lookup"><span data-stu-id="38b55-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="38b55-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38b55-128">Next steps</span></span>

<span data-ttu-id="38b55-129">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="38b55-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="38b55-130">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="38b55-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
