---
title: "PowerShell 指令碼範例-aaaAzure 手動調整 web 應用程式 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 手動調整 Web 應用程式"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="7a1c4-103">手動調整 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a1c4-103">Scale a web app manually</span></span>

<span data-ttu-id="7a1c4-104">在此案例中，您將學習 toocreate 資源群組、 應用程式服務方案和 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="7a1c4-105">然後，您會縮放 hello App Service 方案，從單一執行個體 toomultiple 執行個體。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="7a1c4-106">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7a1c4-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="7a1c4-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7a1c4-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="7a1c4-108">Clean up deployment</span></span> 

<span data-ttu-id="7a1c4-109">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7a1c4-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="7a1c4-110">Script explanation</span></span>

<span data-ttu-id="7a1c4-111">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-111">This script uses hello following commands.</span></span> <span data-ttu-id="7a1c4-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7a1c4-113">命令</span><span class="sxs-lookup"><span data-stu-id="7a1c4-113">Command</span></span> | <span data-ttu-id="7a1c4-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="7a1c4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a1c4-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7a1c4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7a1c4-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7a1c4-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7a1c4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7a1c4-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7a1c4-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7a1c4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7a1c4-120">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="7a1c4-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7a1c4-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="7a1c4-122">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a1c4-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a1c4-123">Next steps</span></span>

<span data-ttu-id="7a1c4-124">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7a1c4-125">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="7a1c4-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
