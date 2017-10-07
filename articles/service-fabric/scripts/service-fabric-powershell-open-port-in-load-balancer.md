---
title: "PowerShell 指令碼範例在負載平衡器中開啟應用程式連接埠 aaaAzure |Microsoft 文件"
description: "Azure 的 PowerShell 指令碼範例-開啟 hello Azure 負載平衡器 Service Fabric 應用程式中的連接埠。"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a><span data-ttu-id="f89b6-103">在 hello Azure 負載平衡器中開啟應用程式連接埠</span><span class="sxs-lookup"><span data-stu-id="f89b6-103">Open an application port in hello Azure load balancer</span></span>

<span data-ttu-id="f89b6-104">在 Azure 中執行的 Service Fabric 應用程式位於 hello Azure 負載平衡器後方。</span><span class="sxs-lookup"><span data-stu-id="f89b6-104">A Service Fabric application running in Azure sits behind hello Azure load balancer.</span></span> <span data-ttu-id="f89b6-105">這個範例指令碼會在 Azure Load Balancer 中開啟連接埠，以便 Service Fabric 應用程式可以與外部用戶端通訊。</span><span class="sxs-lookup"><span data-stu-id="f89b6-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="f89b6-106">視需要自訂 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="f89b6-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="f89b6-107">如有需要安裝 hello Service Fabric PowerShell 模組以 hello [Service Fabric SDK](../service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f89b6-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f89b6-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="f89b6-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a><span data-ttu-id="f89b6-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="f89b6-109">Script explanation</span></span>

<span data-ttu-id="f89b6-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="f89b6-110">This script uses hello following commands.</span></span> <span data-ttu-id="f89b6-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="f89b6-111">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="f89b6-112">命令</span><span class="sxs-lookup"><span data-stu-id="f89b6-112">Command</span></span> | <span data-ttu-id="f89b6-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="f89b6-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f89b6-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="f89b6-114">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="f89b6-115">取得 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f89b6-115">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="f89b6-116">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="f89b6-116">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="f89b6-117">取得 hello Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f89b6-117">Gets hello Azure load balancer.</span></span> |
| [<span data-ttu-id="f89b6-118">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="f89b6-118">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="f89b6-119">加入探查設定 tooa 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f89b6-119">Adds a probe configuration tooa load balancer.</span></span>|
| [<span data-ttu-id="f89b6-120">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="f89b6-120">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="f89b6-121">取得負載平衡器的探查組態。</span><span class="sxs-lookup"><span data-stu-id="f89b6-121">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="f89b6-122">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="f89b6-122">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="f89b6-123">加入規則組態 tooa 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="f89b6-123">Adds a rule configuration tooa load balancer.</span></span> |
| [<span data-ttu-id="f89b6-124">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="f89b6-124">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="f89b6-125">設定 hello 負載平衡器的目標狀態。</span><span class="sxs-lookup"><span data-stu-id="f89b6-125">Sets hello goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f89b6-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f89b6-126">Next steps</span></span>

<span data-ttu-id="f89b6-127">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f89b6-127">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f89b6-128">可以在 hello 中找到其他的 Powershell 範例，讓 Azure Service Fabric [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="f89b6-128">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
