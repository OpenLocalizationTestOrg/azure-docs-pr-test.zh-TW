---
title: "使用 Azure 網路監看員的「下一個躍點」功能來尋找下一個躍點 - Azure CLI 2.0 | Microsoft Docs"
description: "本文會說明如何使用 Azure CLI，利用下一個躍點功能來得知下一個躍點類型和 IP 位址。"
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
ms.openlocfilehash: d1ee6870ba0188ff2c473e4cca12a5bdc1f97d3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="2ec05-103">使用採用 Azure CLI 2.0 之 Azure 網路監看員的「下一個躍點」功能，得知下一個躍點類型</span><span class="sxs-lookup"><span data-stu-id="2ec05-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2ec05-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2ec05-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="2ec05-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ec05-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="2ec05-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2ec05-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="2ec05-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2ec05-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="2ec05-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="2ec05-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="2ec05-109">下一個躍點是網路監看員的一項功能，可根據指定的虛擬機器取得下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2ec05-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="2ec05-110">這項功能可用於判斷離開虛擬機器的流量是否會周遊閘道、網際網路或虛擬網路，以抵達其目的地。</span><span class="sxs-lookup"><span data-stu-id="2ec05-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="2ec05-111">本文使用資源管理部署模型的新一代 CLI：Azure CLI 2.0，它適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="2ec05-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="2ec05-112">若要執行本文的步驟，您需要[安裝適用於 Mac、Linux 和 Windows 的 Azure 命令列介面 (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="2ec05-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2ec05-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="2ec05-113">Before you begin</span></span>

<span data-ttu-id="2ec05-114">在此案例中，您會使用 Azure CLI 來尋找下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2ec05-114">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="2ec05-115">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="2ec05-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="2ec05-116">此案例也假設已有具有有效虛擬機器的資源群組可供使用。</span><span class="sxs-lookup"><span data-stu-id="2ec05-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2ec05-117">案例</span><span class="sxs-lookup"><span data-stu-id="2ec05-117">Scenario</span></span>

<span data-ttu-id="2ec05-118">本文涵蓋的案例會使用網路監看員的下一個躍點功能，以找出資源的下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2ec05-118">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="2ec05-119">若要深入了解下一個躍點，請造訪[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2ec05-119">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="2ec05-120">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="2ec05-120">Get Next Hop</span></span>

<span data-ttu-id="2ec05-121">若要取得下一個躍點，我們可呼叫 `az network watcher show-next-hop` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2ec05-121">To get the next hop we call the `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="2ec05-122">我們會將網路監看員資源群組 NetworkWatcher、虛擬機器識別碼、來源 IP 位址和目的地 IP 位址傳遞給此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2ec05-122">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="2ec05-123">在此範例中，目的地 IP 位址是在另一個虛擬網路的 VM。</span><span class="sxs-lookup"><span data-stu-id="2ec05-123">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="2ec05-124">兩個虛擬網路之間有虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="2ec05-124">There is a virtual network gateway between the two virtual networks.</span></span>

<span data-ttu-id="2ec05-125">安裝及設定最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) (若您尚未這麼做)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ec05-125">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="2ec05-126">然後，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="2ec05-126">Then run the following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="2ec05-127">如果 VM 具有多個 NIC，而且任一 NIC 啟用了 IP 轉送，則必須指定 NIC 參數 (-i nic-id)。</span><span class="sxs-lookup"><span data-stu-id="2ec05-127">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="2ec05-128">否則為選擇性。</span><span class="sxs-lookup"><span data-stu-id="2ec05-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="2ec05-129">檢閱結果</span><span class="sxs-lookup"><span data-stu-id="2ec05-129">Review results</span></span>

<span data-ttu-id="2ec05-130">完成時會提供結果。</span><span class="sxs-lookup"><span data-stu-id="2ec05-130">When complete, the results are provided.</span></span> <span data-ttu-id="2ec05-131">所傳回的有下一個躍點 IP 位址以及其所屬的資源類型。</span><span class="sxs-lookup"><span data-stu-id="2ec05-131">The next hop IP address is returned as well as the type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="2ec05-132">下列清單顯示目前可用的 NextHopType 值︰</span><span class="sxs-lookup"><span data-stu-id="2ec05-132">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="2ec05-133">**下一個躍點類型**</span><span class="sxs-lookup"><span data-stu-id="2ec05-133">**Next Hop Type**</span></span>

* <span data-ttu-id="2ec05-134">Internet</span><span class="sxs-lookup"><span data-stu-id="2ec05-134">Internet</span></span>
* <span data-ttu-id="2ec05-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="2ec05-135">VirtualAppliance</span></span>
* <span data-ttu-id="2ec05-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="2ec05-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="2ec05-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="2ec05-137">VnetLocal</span></span>
* <span data-ttu-id="2ec05-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="2ec05-138">HyperNetGateway</span></span>
* <span data-ttu-id="2ec05-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="2ec05-139">VnetPeering</span></span>
* <span data-ttu-id="2ec05-140">None</span><span class="sxs-lookup"><span data-stu-id="2ec05-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ec05-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ec05-141">Next steps</span></span>

<span data-ttu-id="2ec05-142">請造訪[使用網路監看員稽核 NSG](network-watcher-nsg-auditing-powershell.md)，以了解如何以程式設計方式檢閱網路安全性群組設定</span><span class="sxs-lookup"><span data-stu-id="2ec05-142">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
