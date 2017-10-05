---
title: "使用 Azure 網路監看員下一個躍點來尋找下一個躍點 - Azure 入口網站 | Microsoft Docs"
description: "本文會說明如何使用 Azure 入口網站，利用下一個躍點功能來得知下一個躍點類型和 IP 位址"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="2cdd7-103">使用入口網站，利用 Azure 網路監看員的下一個躍點功能找出下一個躍點類型</span><span class="sxs-lookup"><span data-stu-id="2cdd7-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2cdd7-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2cdd7-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="2cdd7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cdd7-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="2cdd7-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2cdd7-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="2cdd7-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2cdd7-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="2cdd7-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="2cdd7-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="2cdd7-109">下一個躍點是網路監看員的一項功能，可根據指定的虛擬機器取得下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="2cdd7-110">這項功能可用於判斷離開虛擬機器的流量是否會周遊閘道、網際網路或虛擬網路，以抵達其目的地。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2cdd7-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="2cdd7-111">Before you begin</span></span>

<span data-ttu-id="2cdd7-112">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="2cdd7-113">此案例也假設已有具有有效虛擬機器的資源群組可供使用。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2cdd7-114">案例</span><span class="sxs-lookup"><span data-stu-id="2cdd7-114">Scenario</span></span>

<span data-ttu-id="2cdd7-115">本文涵蓋的案例會使用下一個躍點，以找出資源的下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="2cdd7-116">若要深入了解下一個躍點，請造訪[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="2cdd7-117">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="2cdd7-117">In this scenario, you will:</span></span>

* <span data-ttu-id="2cdd7-118">從虛擬機器中擷取下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="2cdd7-119">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="2cdd7-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="2cdd7-120">步驟 1</span><span class="sxs-lookup"><span data-stu-id="2cdd7-120">Step 1</span></span>

<span data-ttu-id="2cdd7-121">在 Azure 入口網站中瀏覽至您的網路監看員資源。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="2cdd7-122">步驟 2</span><span class="sxs-lookup"><span data-stu-id="2cdd7-122">Step 2</span></span>

<span data-ttu-id="2cdd7-123">按一下瀏覽窗格中的 [下一個躍點]、選取虛擬機器和網路介面、填寫來源和目的地 IP，然後按 [下一個躍點] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="2cdd7-124">下一個躍點需要配置 VM 資源以供執行。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-124">Next hop requires that the VM resource is allocated to run.</span></span>

![取得下一個躍點概觀][1]

### <a name="step-3"></a><span data-ttu-id="2cdd7-126">步驟 3</span><span class="sxs-lookup"><span data-stu-id="2cdd7-126">Step 3</span></span>

<span data-ttu-id="2cdd7-127">一旦工作完成後，會提供結果。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="2cdd7-128">會顯示 IP 位址和下一個躍點的裝置類型。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="2cdd7-129">下表會在入口網站中顯示可用的傳回值。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="2cdd7-130">**下一個躍點類型**</span><span class="sxs-lookup"><span data-stu-id="2cdd7-130">**Next Hop Type**</span></span>

* <span data-ttu-id="2cdd7-131">Internet</span><span class="sxs-lookup"><span data-stu-id="2cdd7-131">Internet</span></span>
* <span data-ttu-id="2cdd7-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="2cdd7-132">VirtualAppliance</span></span>
* <span data-ttu-id="2cdd7-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="2cdd7-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="2cdd7-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="2cdd7-134">VnetLocal</span></span>
* <span data-ttu-id="2cdd7-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="2cdd7-135">HyperNetGateway</span></span>
* <span data-ttu-id="2cdd7-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="2cdd7-136">VnetPeering</span></span>
* <span data-ttu-id="2cdd7-137">None</span><span class="sxs-lookup"><span data-stu-id="2cdd7-137">None</span></span>

<span data-ttu-id="2cdd7-138">如果自訂路由用來路由傳送此流量，則使用者定義的路由 (UDR) 也會與結果顯示。</span><span class="sxs-lookup"><span data-stu-id="2cdd7-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![取得下一個躍點結果][2]

## <a name="next-steps"></a><span data-ttu-id="2cdd7-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2cdd7-140">Next steps</span></span>

<span data-ttu-id="2cdd7-141">請造訪[使用網路監看員稽核 NSG](network-watcher-nsg-auditing-powershell.md)，以了解如何以程式設計方式檢閱網路安全性群組設定</span><span class="sxs-lookup"><span data-stu-id="2cdd7-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














