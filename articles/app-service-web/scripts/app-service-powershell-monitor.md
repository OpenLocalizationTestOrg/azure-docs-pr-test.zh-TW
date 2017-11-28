---
title: "PowerShell 指令碼範例-aaaAzure 監視 web 應用程式與 web 伺服器記錄檔 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 使用 Web 伺服器記錄監視 Web 應用程式"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="4e64f-103">使用 Web 伺服器記錄監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e64f-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="4e64f-104">在此案例中，您會建立資源群組、 應用程式服務方案、 web 應用程式和設定 hello web 應用程式 tooenable web 伺服器記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4e64f-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="4e64f-105">接著，您將下載 hello 檢閱記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4e64f-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="4e64f-106">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="4e64f-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="4e64f-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4e64f-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4e64f-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="4e64f-108">Clean up deployment</span></span> 

<span data-ttu-id="4e64f-109">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="4e64f-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4e64f-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="4e64f-110">Script explanation</span></span>

<span data-ttu-id="4e64f-111">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e64f-111">This script uses hello following commands.</span></span> <span data-ttu-id="4e64f-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="4e64f-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4e64f-113">命令</span><span class="sxs-lookup"><span data-stu-id="4e64f-113">Command</span></span> | <span data-ttu-id="4e64f-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="4e64f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4e64f-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4e64f-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4e64f-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4e64f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4e64f-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4e64f-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4e64f-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4e64f-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4e64f-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4e64f-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4e64f-120">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e64f-120">Creates a web app.</span></span> |
| [<span data-ttu-id="4e64f-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4e64f-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="4e64f-122">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="4e64f-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="4e64f-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="4e64f-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="4e64f-124">取得 Web 應用程式的計量。</span><span class="sxs-lookup"><span data-stu-id="4e64f-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4e64f-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e64f-125">Next steps</span></span>

<span data-ttu-id="4e64f-126">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4e64f-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4e64f-127">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="4e64f-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
