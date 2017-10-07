---
title: "aaaFind 下一個躍點與 Azure 網路監看員下一個躍點-PowerShell |Microsoft 文件"
description: "本文將說明如何尋找哪些 hello 下個躍點類型會與 ip 位址使用下個躍點使用 PowerShell。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="a4698-103">找出 hello 下一個躍點類型會使用 Azure 網路監看員使用 PowerShell 中的 hello 下一個躍點功能</span><span class="sxs-lookup"><span data-stu-id="a4698-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a4698-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a4698-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="a4698-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4698-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="a4698-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a4698-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="a4698-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a4698-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="a4698-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="a4698-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="a4698-109">下一個躍點是網路監看員提供 hello 功能的一項功能取得下一個躍點類型 hello 和根據指定的虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a4698-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="a4698-110">這項功能可用於判斷如果離開虛擬機器的流量會周遊閘道、 網際網路或虛擬網路 tooget tooits 目的地。</span><span class="sxs-lookup"><span data-stu-id="a4698-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a4698-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="a4698-111">Before you begin</span></span>

<span data-ttu-id="a4698-112">在此案例中，您將使用 hello Azure 入口網站 toofind hello 下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a4698-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="a4698-113">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="a4698-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="a4698-114">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="a4698-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a4698-115">案例</span><span class="sxs-lookup"><span data-stu-id="a4698-115">Scenario</span></span>

<span data-ttu-id="a4698-116">在此文章所涵蓋的 hello 案例使用下一個躍點，會找出 hello 下一個躍點類型和資源的 IP 位址的網路監看員的一項功能。</span><span class="sxs-lookup"><span data-stu-id="a4698-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="a4698-117">toolearn 深入了解下個躍點，請瀏覽[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a4698-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="a4698-118">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="a4698-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="a4698-119">hello 第一個步驟是 tooretrieve hello 網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="a4698-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="a4698-120">hello`$networkWatcher`變數傳遞 toohello 下一個躍點驗證 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a4698-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="a4698-121">取得虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a4698-121">Get a virtual machine</span></span>

<span data-ttu-id="a4698-122">下一個躍點傳回 hello 下一個躍點和 hello hello 下一個躍點 IP 位址，從虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a4698-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="a4698-123">Hello cmdlet 需要虛擬機器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a4698-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="a4698-124">如果您已經知道 hello 虛擬機器 toouse hello 識別碼，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="a4698-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="a4698-125">下一個躍點需要 hello VM 資源配置 toorun。</span><span class="sxs-lookup"><span data-stu-id="a4698-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="a4698-126">取得 hello 網路介面</span><span class="sxs-lookup"><span data-stu-id="a4698-126">Get hello network interfaces</span></span>

<span data-ttu-id="a4698-127">需要 hello 的 hello 虛擬機器上的 NIC 的 IP 位址，在此範例中我們擷取 hello Nic 的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="a4698-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="a4698-128">如果您已經知道 hello IP 位址，您會想 tootest hello 虛擬機器上，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="a4698-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="a4698-129">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="a4698-129">Get Next Hop</span></span>

<span data-ttu-id="a4698-130">現在，我們會呼叫 hello `Get-AzureRmNetworkWatcherNextHop` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a4698-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="a4698-131">我們傳遞 hello cmdlet hello 網路監看員，虛擬機器識別碼時，來源 IP 位址和目的地 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a4698-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="a4698-132">在此範例中，hello 目的地 IP 位址會是 tooa VM，另一個虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="a4698-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="a4698-133">Hello 兩個虛擬網路之間沒有虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="a4698-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="a4698-134">檢閱結果</span><span class="sxs-lookup"><span data-stu-id="a4698-134">Review results</span></span>

<span data-ttu-id="a4698-135">完成時，會提供 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="a4698-135">When complete, hello results are provided.</span></span> <span data-ttu-id="a4698-136">它是的資源 hello 類型以及傳回 hello 下一個躍點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a4698-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="a4698-137">在此案例中，它是 hello 虛擬網路閘道的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a4698-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="a4698-138">hello 下列清單顯示目前可用 NextHopType 值 hello:</span><span class="sxs-lookup"><span data-stu-id="a4698-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="a4698-139">**下一個躍點類型**</span><span class="sxs-lookup"><span data-stu-id="a4698-139">**Next Hop Type**</span></span>

* <span data-ttu-id="a4698-140">Internet</span><span class="sxs-lookup"><span data-stu-id="a4698-140">Internet</span></span>
* <span data-ttu-id="a4698-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="a4698-141">VirtualAppliance</span></span>
* <span data-ttu-id="a4698-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="a4698-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="a4698-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="a4698-143">VnetLocal</span></span>
* <span data-ttu-id="a4698-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="a4698-144">HyperNetGateway</span></span>
* <span data-ttu-id="a4698-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="a4698-145">VnetPeering</span></span>
* <span data-ttu-id="a4698-146">None</span><span class="sxs-lookup"><span data-stu-id="a4698-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4698-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4698-147">Next steps</span></span>

<span data-ttu-id="a4698-148">深入了解如何 tooreview 您的網路安全性群組設定，以程式設計方式造訪[NSG 稽核與網路監看員](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a4698-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















