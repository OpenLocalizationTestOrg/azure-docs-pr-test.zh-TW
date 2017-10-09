---
title: "aaaFind 下一個躍點與 Azure 網路監看員下一個躍點-Azure CLI 2.0 |Microsoft 文件"
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
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="622a1-103">找出 hello 下一個躍點類型會使用 Azure 網路監看員使用 Azure CLI 2.0 中的 hello 下一個躍點功能</span><span class="sxs-lookup"><span data-stu-id="622a1-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="622a1-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="622a1-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="622a1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="622a1-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="622a1-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="622a1-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="622a1-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="622a1-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="622a1-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="622a1-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="622a1-109">下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="622a1-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="622a1-110">這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。</span><span class="sxs-lookup"><span data-stu-id="622a1-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="622a1-111">本文使用我們的下一個層代 CLI hello 資源管理部署模型，Azure CLI 2.0 中，這是適用於 Windows、 Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="622a1-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="622a1-112">tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="622a1-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="622a1-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="622a1-113">Before you begin</span></span>

<span data-ttu-id="622a1-114">在此案例中，您將使用 hello Azure CLI toofind hello 下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="622a1-114">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="622a1-115">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="622a1-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="622a1-116">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="622a1-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="622a1-117">案例</span><span class="sxs-lookup"><span data-stu-id="622a1-117">Scenario</span></span>

<span data-ttu-id="622a1-118">在此文章所涵蓋的 hello 案例使用下一個躍點，會找出 hello 下一個躍點類型和資源的 IP 位址的網路監看員的一項功能。</span><span class="sxs-lookup"><span data-stu-id="622a1-118">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="622a1-119">toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="622a1-119">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="622a1-120">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="622a1-120">Get Next Hop</span></span>

<span data-ttu-id="622a1-121">tooget hello 下一個躍點，我們會呼叫 hello `az network watcher show-next-hop` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="622a1-121">tooget hello next hop we call hello `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="622a1-122">我們會傳送 hello cmdlet hello 網路監看員資源群組、 hello NetworkWatcher、 虛擬機器識別碼、 來源 IP 位址和目的地 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="622a1-122">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="622a1-123">在此範例中，hello 目的地 IP 位址會是 tooa VM，另一個虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="622a1-123">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="622a1-124">Hello 兩個虛擬網路之間沒有虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="622a1-124">There is a virtual network gateway between hello two virtual networks.</span></span>

<span data-ttu-id="622a1-125">如果您尚未，安裝並設定最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="622a1-125">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="622a1-126">然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="622a1-126">Then run hello following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="622a1-127">如果 hello VM 有多個 Nic 和任何 hello Nic 上啟用 IP 轉送，然後 hello NIC 參數 (-我 nic 識別碼)，必須指定。</span><span class="sxs-lookup"><span data-stu-id="622a1-127">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="622a1-128">否則為選擇性。</span><span class="sxs-lookup"><span data-stu-id="622a1-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="622a1-129">檢閱結果</span><span class="sxs-lookup"><span data-stu-id="622a1-129">Review results</span></span>

<span data-ttu-id="622a1-130">完成時，會提供 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="622a1-130">When complete, hello results are provided.</span></span> <span data-ttu-id="622a1-131">它是的資源 hello 類型以及傳回 hello 下一個躍點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="622a1-131">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="622a1-132">hello 下列清單顯示目前可用 NextHopType 值 hello:</span><span class="sxs-lookup"><span data-stu-id="622a1-132">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="622a1-133">**下一個躍點類型**</span><span class="sxs-lookup"><span data-stu-id="622a1-133">**Next Hop Type**</span></span>

* <span data-ttu-id="622a1-134">Internet</span><span class="sxs-lookup"><span data-stu-id="622a1-134">Internet</span></span>
* <span data-ttu-id="622a1-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="622a1-135">VirtualAppliance</span></span>
* <span data-ttu-id="622a1-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="622a1-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="622a1-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="622a1-137">VnetLocal</span></span>
* <span data-ttu-id="622a1-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="622a1-138">HyperNetGateway</span></span>
* <span data-ttu-id="622a1-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="622a1-139">VnetPeering</span></span>
* <span data-ttu-id="622a1-140">None</span><span class="sxs-lookup"><span data-stu-id="622a1-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="622a1-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="622a1-141">Next steps</span></span>

<span data-ttu-id="622a1-142">深入了解如何 tooreview 您的網路安全性群組設定，以程式設計方式造訪[NSG 稽核與網路監看員](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="622a1-142">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
