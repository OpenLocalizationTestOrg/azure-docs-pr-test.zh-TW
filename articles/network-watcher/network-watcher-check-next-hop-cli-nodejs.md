---
title: "aaaFind 與 Azure 網路監看員下一個躍點-Azure CLI 1.0 的下一個躍點 |Microsoft 文件"
description: "本文將說明如何尋找哪些 hello 下個躍點類型會與 ip 位址使用下個躍點使用 Azure CLI。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="0e4ad-103">找出 hello 下一個躍點類型會使用 Azure 網路監看員使用 Azure CLI 1.0 中的 hello 下一個躍點功能</span><span class="sxs-lookup"><span data-stu-id="0e4ad-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0e4ad-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0e4ad-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="0e4ad-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e4ad-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="0e4ad-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0e4ad-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="0e4ad-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0e4ad-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="0e4ad-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="0e4ad-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="0e4ad-109">下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="0e4ad-110">這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="0e4ad-111">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0e4ad-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="0e4ad-112">Before you begin</span></span>

<span data-ttu-id="0e4ad-113">在此案例中，您將使用 hello Azure CLI toofind hello 下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-113">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="0e4ad-114">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="0e4ad-115">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="0e4ad-116">案例</span><span class="sxs-lookup"><span data-stu-id="0e4ad-116">Scenario</span></span>

<span data-ttu-id="0e4ad-117">在此文章所涵蓋的 hello 案例使用下一個躍點，會找出 hello 下一個躍點類型和資源的 IP 位址的網路監看員的一項功能。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-117">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="0e4ad-118">toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-118">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="0e4ad-119">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="0e4ad-119">Get Next Hop</span></span>

<span data-ttu-id="0e4ad-120">tooget hello 下一個躍點，我們會呼叫 hello `azure netowrk watcher next-hop` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-120">tooget hello next hop we call hello `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="0e4ad-121">我們會傳送 hello cmdlet hello 網路監看員資源群組、 hello NetworkWatcher、 虛擬機器識別碼、 來源 IP 位址和目的地 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-121">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="0e4ad-122">在此範例中，hello 目的地 IP 位址會是 tooa VM，另一個虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-122">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="0e4ad-123">Hello 兩個虛擬網路之間沒有虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-123">There is a virtual network gateway between hello two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="0e4ad-124">如果 hello VM 有多個 Nic 和任何 hello Nic 上啟用 IP 轉送，然後 hello NIC 參數 (-我 nic 識別碼)，必須指定。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-124">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="0e4ad-125">否則為選擇性。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="0e4ad-126">檢閱結果</span><span class="sxs-lookup"><span data-stu-id="0e4ad-126">Review results</span></span>

<span data-ttu-id="0e4ad-127">完成時，會提供 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-127">When complete, hello results are provided.</span></span> <span data-ttu-id="0e4ad-128">它是的資源 hello 類型以及傳回 hello 下一個躍點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0e4ad-128">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="0e4ad-129">hello 下列清單顯示目前可用 NextHopType 值 hello:</span><span class="sxs-lookup"><span data-stu-id="0e4ad-129">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="0e4ad-130">**下一個躍點類型**</span><span class="sxs-lookup"><span data-stu-id="0e4ad-130">**Next Hop Type**</span></span>

* <span data-ttu-id="0e4ad-131">Internet</span><span class="sxs-lookup"><span data-stu-id="0e4ad-131">Internet</span></span>
* <span data-ttu-id="0e4ad-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="0e4ad-132">VirtualAppliance</span></span>
* <span data-ttu-id="0e4ad-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="0e4ad-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="0e4ad-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="0e4ad-134">VnetLocal</span></span>
* <span data-ttu-id="0e4ad-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="0e4ad-135">HyperNetGateway</span></span>
* <span data-ttu-id="0e4ad-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="0e4ad-136">VnetPeering</span></span>
* <span data-ttu-id="0e4ad-137">None</span><span class="sxs-lookup"><span data-stu-id="0e4ad-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e4ad-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e4ad-138">Next steps</span></span>

<span data-ttu-id="0e4ad-139">深入了解如何 tooreview 您的網路安全性群組設定，以程式設計方式造訪[NSG 稽核與網路監看員](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="0e4ad-139">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
