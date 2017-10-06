---
title: "aaaAzure PowerShell 指令碼範例-調整 web 應用程式與高可用性架構全球 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 透過高可用性架構將 Web 應用程式調整為全球可用"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="272ef-103">透過高可用性架構將 Web 應用程式調整為全球可用</span><span class="sxs-lookup"><span data-stu-id="272ef-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="272ef-104">在此案例中，您會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。</span><span class="sxs-lookup"><span data-stu-id="272ef-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="272ef-105">一旦完成 hello 練習會有高可用性的架構可讓提供全域 hello 最低的網路延遲為基礎的 web 應用程式的可用性。</span><span class="sxs-lookup"><span data-stu-id="272ef-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="272ef-106">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="272ef-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="272ef-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="272ef-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="272ef-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="272ef-108">Clean up deployment</span></span> 

<span data-ttu-id="272ef-109">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="272ef-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="272ef-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="272ef-110">Script explanation</span></span>

<span data-ttu-id="272ef-111">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="272ef-111">This script uses hello following commands.</span></span> <span data-ttu-id="272ef-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="272ef-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="272ef-113">命令</span><span class="sxs-lookup"><span data-stu-id="272ef-113">Command</span></span> | <span data-ttu-id="272ef-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="272ef-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="272ef-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="272ef-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="272ef-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="272ef-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="272ef-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="272ef-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="272ef-118">建立流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="272ef-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="272ef-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="272ef-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="272ef-120">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="272ef-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="272ef-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="272ef-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="272ef-122">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="272ef-122">Creates a web app.</span></span> |
| [<span data-ttu-id="272ef-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="272ef-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="272ef-124">在流量管理員設定檔中建立端點。</span><span class="sxs-lookup"><span data-stu-id="272ef-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="272ef-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="272ef-125">Next steps</span></span>

<span data-ttu-id="272ef-126">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="272ef-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="272ef-127">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="272ef-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
