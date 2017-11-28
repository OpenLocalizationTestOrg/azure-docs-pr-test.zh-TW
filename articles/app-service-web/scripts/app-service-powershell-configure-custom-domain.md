---
title: "PowerShell 指令碼範例-aaaAzure 指派自訂網域 tooa web 應用程式 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例將自訂網域 tooa web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="50c0c-103">指定自訂網域 tooa web 應用程式</span><span class="sxs-lookup"><span data-stu-id="50c0c-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="50c0c-104">這個範例指令碼應用程式服務中建立 web 應用程式及其相關的資源，然後對應`www.<yourdomain>`tooit。</span><span class="sxs-lookup"><span data-stu-id="50c0c-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="50c0c-105">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="50c0c-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="50c0c-106">此外，您需要 toohave 存取 tooyour 網域註冊機構的 DNS 設定 頁面。</span><span class="sxs-lookup"><span data-stu-id="50c0c-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="50c0c-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="50c0c-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="50c0c-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="50c0c-108">Clean up deployment</span></span> 

<span data-ttu-id="50c0c-109">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="50c0c-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="50c0c-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="50c0c-110">Script explanation</span></span>

<span data-ttu-id="50c0c-111">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="50c0c-111">This script uses hello following commands.</span></span> <span data-ttu-id="50c0c-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="50c0c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="50c0c-113">命令</span><span class="sxs-lookup"><span data-stu-id="50c0c-113">Command</span></span> | <span data-ttu-id="50c0c-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="50c0c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="50c0c-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="50c0c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="50c0c-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="50c0c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="50c0c-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="50c0c-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="50c0c-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="50c0c-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="50c0c-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="50c0c-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="50c0c-120">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="50c0c-120">Creates a web app.</span></span> |
| [<span data-ttu-id="50c0c-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="50c0c-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="50c0c-122">修改應用程式服務計劃 toochange 其定價層。</span><span class="sxs-lookup"><span data-stu-id="50c0c-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="50c0c-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="50c0c-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="50c0c-124">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="50c0c-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50c0c-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50c0c-125">Next steps</span></span>

<span data-ttu-id="50c0c-126">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="50c0c-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="50c0c-127">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="50c0c-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
