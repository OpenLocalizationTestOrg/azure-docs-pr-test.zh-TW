---
title: "aaaFind 下一個躍點與 Azure 網路監看員下一個躍點-Azure 入口網站 |Microsoft 文件"
description: "本文將說明如何尋找哪些 hello 下個躍點類型，且使用下一個躍點使用的 ip 位址 hello Azure 入口網站"
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
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="e2010-103">找出 hello 下一個躍點類型會使用 Azure 網路監看員使用 hello 入口網站中的 hello 下一個躍點功能</span><span class="sxs-lookup"><span data-stu-id="e2010-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e2010-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e2010-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="e2010-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2010-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="e2010-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e2010-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="e2010-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e2010-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="e2010-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="e2010-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="e2010-109">下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e2010-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="e2010-110">這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。</span><span class="sxs-lookup"><span data-stu-id="e2010-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e2010-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="e2010-111">Before you begin</span></span>

<span data-ttu-id="e2010-112">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="e2010-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="e2010-113">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="e2010-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="e2010-114">案例</span><span class="sxs-lookup"><span data-stu-id="e2010-114">Scenario</span></span>

<span data-ttu-id="e2010-115">涵蓋在本文中的 hello 案例會使用下一個躍點 toofind 出 hello 下一個躍點類型和 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="e2010-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="e2010-116">toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e2010-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="e2010-117">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="e2010-117">In this scenario, you will:</span></span>

* <span data-ttu-id="e2010-118">從虛擬機器擷取 hello 下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="e2010-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="e2010-119">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="e2010-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="e2010-120">步驟 1</span><span class="sxs-lookup"><span data-stu-id="e2010-120">Step 1</span></span>

<span data-ttu-id="e2010-121">瀏覽 tooyour 網路監看員資源 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="e2010-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="e2010-122">步驟 2</span><span class="sxs-lookup"><span data-stu-id="e2010-122">Step 2</span></span>

<span data-ttu-id="e2010-123">按一下**下個躍點**hello 瀏覽窗格中，選取 hello 虛擬機器網路介面，填寫 hello 來源和目的地 IP，然後按一下 hello**下個躍點**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e2010-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="e2010-124">下一個躍點需要 hello VM 資源配置 toorun。</span><span class="sxs-lookup"><span data-stu-id="e2010-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![取得下一個躍點概觀][1]

### <a name="step-3"></a><span data-ttu-id="e2010-126">步驟 3</span><span class="sxs-lookup"><span data-stu-id="e2010-126">Step 3</span></span>

<span data-ttu-id="e2010-127">Hello 工作完成之後，會提供 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="e2010-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="e2010-128">hello IP 位址和裝置 hello 下一個躍點的類型時，就會顯示。</span><span class="sxs-lookup"><span data-stu-id="e2010-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="e2010-129">hello 下表顯示可用的傳回的值 hello hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="e2010-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="e2010-130">**下一個躍點類型**</span><span class="sxs-lookup"><span data-stu-id="e2010-130">**Next Hop Type**</span></span>

* <span data-ttu-id="e2010-131">Internet</span><span class="sxs-lookup"><span data-stu-id="e2010-131">Internet</span></span>
* <span data-ttu-id="e2010-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="e2010-132">VirtualAppliance</span></span>
* <span data-ttu-id="e2010-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="e2010-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="e2010-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="e2010-134">VnetLocal</span></span>
* <span data-ttu-id="e2010-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="e2010-135">HyperNetGateway</span></span>
* <span data-ttu-id="e2010-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="e2010-136">VnetPeering</span></span>
* <span data-ttu-id="e2010-137">None</span><span class="sxs-lookup"><span data-stu-id="e2010-137">None</span></span>

<span data-ttu-id="e2010-138">如果自訂的路由使用的 tooroute 這個流量，hello 使用者定義的路由 (UDR) 也會顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="e2010-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![取得下一個躍點結果][2]

## <a name="next-steps"></a><span data-ttu-id="e2010-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2010-140">Next steps</span></span>

<span data-ttu-id="e2010-141">深入了解如何 tooreview 您的網路安全性群組設定，以程式設計方式造訪[NSG 稽核與網路監看員](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e2010-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














