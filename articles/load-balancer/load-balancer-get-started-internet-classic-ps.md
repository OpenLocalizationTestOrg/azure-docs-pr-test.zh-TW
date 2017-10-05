---
title: "建立網際網路對向負載平衡器 - Azure PowerShell 傳統 | Microsoft Docs"
description: "了解如何使用 PowerShell 在傳統模式中建立網際網路面向的負載平衡器"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1a41f3ba199fb692c111ea6a40ddb09605f91da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="56aa4-103">開始在 PowerShell 中建立網際網路面向的負載平衡器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="56aa4-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="56aa4-104">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="56aa4-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="56aa4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56aa4-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="56aa4-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="56aa4-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="56aa4-107">Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="56aa4-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="56aa4-108">使用 Azure 資源之前，請務必了解 Azure 目前有 Azure Resource Manager 和「傳統」兩種部署模型。</span><span class="sxs-lookup"><span data-stu-id="56aa4-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="56aa4-109">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。</span><span class="sxs-lookup"><span data-stu-id="56aa4-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="56aa4-110">您可以按一下本文頂端的索引標籤，檢視不同工具的文件。</span><span class="sxs-lookup"><span data-stu-id="56aa4-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="56aa4-111">本文涵蓋之內容包括傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="56aa4-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="56aa4-112">您也可以 [了解如何使用 Azure 資源管理員建立網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="56aa4-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="56aa4-113">使用 PowerShell 設定負載平衡器</span><span class="sxs-lookup"><span data-stu-id="56aa4-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="56aa4-114">若要使用 PowerShell 設定負載平衡器，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="56aa4-114">To set up a load balancer using powershell, follow the steps below:</span></span>

1. <span data-ttu-id="56aa4-115">如果您從未用過 Azure PowerShell，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) ，並遵循其中的所有指示登入 Azure，然後選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="56aa4-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="56aa4-116">建立虛擬機器之後，您可以使用 PowerShell cmdlet，將負載平衡器新增至相同雲端服務內的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="56aa4-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="56aa4-117">在下列範例中，您會將稱為 "webfarm" 的負載平衡器集新增至雲端服務 "mytestcloud" (或 myctestcloud.cloudapp.net)，並將負載平衡器的端點新增至名為 "web1" 和 "web2" 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="56aa4-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span></span> <span data-ttu-id="56aa4-118">負載平衡器會接收連接埠 80 的流量，並使用 TCP 負載平衡本機端點 (在此案例中為連接埠 80) 所定義之虛擬機器之間的流量。</span><span class="sxs-lookup"><span data-stu-id="56aa4-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="56aa4-119">步驟 1</span><span class="sxs-lookup"><span data-stu-id="56aa4-119">Step 1</span></span>

<span data-ttu-id="56aa4-120">為第一部 VM "web1" 建立負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="56aa4-120">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="56aa4-121">步驟 2</span><span class="sxs-lookup"><span data-stu-id="56aa4-121">Step 2</span></span>

<span data-ttu-id="56aa4-122">使用相同的負載平衡器集名稱，為第二部 VM "web2" 建立另一個端點</span><span class="sxs-lookup"><span data-stu-id="56aa4-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="56aa4-123">從負載平衡器移除虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56aa4-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="56aa4-124">您可以使用 Remove-AzureEndpoint 從負載平衡器移除虛擬機器端點</span><span class="sxs-lookup"><span data-stu-id="56aa4-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="56aa4-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56aa4-125">Next steps</span></span>

<span data-ttu-id="56aa4-126">您也可以[開始建立內部負載平衡器](load-balancer-get-started-ilb-classic-ps.md)，以及為特定負載平衡器的網路流量行為設定何種[分配模式](load-balancer-distribution-mode.md)。</span><span class="sxs-lookup"><span data-stu-id="56aa4-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="56aa4-127">如果您的應用程式需要讓負載平衡器後方的伺服器保持連接狀態，您可以深入了解 [負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)。</span><span class="sxs-lookup"><span data-stu-id="56aa4-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="56aa4-128">當您使用 Azure 負載平衡器時，該文章可幫助您了解閒置連接行為。</span><span class="sxs-lookup"><span data-stu-id="56aa4-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
