---
title: "使用 Azure 網路監看員下一個躍點來尋找下一個躍點 - PowerShell | Microsoft Docs"
description: "本文會說明如何使用 PowerShell，利用下一個躍點功能來得知下一個躍點類型和 IP 位址。"
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
ms.openlocfilehash: 00161e7c6fb4becdb7d8eab266fa27128e50f8ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="057a1-103">使用 PowerShell，利用 Azure 網路監看員的下一個躍點功能找出下一個躍點類型</span><span class="sxs-lookup"><span data-stu-id="057a1-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="057a1-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="057a1-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="057a1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="057a1-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="057a1-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="057a1-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="057a1-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="057a1-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="057a1-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="057a1-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="057a1-109">下一個躍點是網路監看員的一項功能，可根據指定的虛擬機器取得下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="057a1-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="057a1-110">這項功能可用於判斷離開虛擬機器的流量是否會周遊閘道、網際網路或虛擬網路，以抵達其目的地。</span><span class="sxs-lookup"><span data-stu-id="057a1-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="057a1-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="057a1-111">Before you begin</span></span>

<span data-ttu-id="057a1-112">在此案例中，您會使用 Azure 入口網站來尋找下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="057a1-112">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span></span>

<span data-ttu-id="057a1-113">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="057a1-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="057a1-114">此案例也假設已有具有有效虛擬機器的資源群組可供使用。</span><span class="sxs-lookup"><span data-stu-id="057a1-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="057a1-115">案例</span><span class="sxs-lookup"><span data-stu-id="057a1-115">Scenario</span></span>

<span data-ttu-id="057a1-116">本文涵蓋的案例會使用網路監看員的下一個躍點功能，以找出資源的下一個躍點類型和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="057a1-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="057a1-117">若要深入了解下一個躍點，請造訪[下一個躍點概觀](network-watcher-next-hop-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="057a1-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="057a1-118">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="057a1-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="057a1-119">第一步是擷取網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="057a1-119">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="057a1-120">`$networkWatcher` 變數會傳遞至下一個躍點驗證 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="057a1-120">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="057a1-121">取得虛擬機器</span><span class="sxs-lookup"><span data-stu-id="057a1-121">Get a virtual machine</span></span>

<span data-ttu-id="057a1-122">下一個躍點會從虛擬機器傳回下一個躍點和下一個躍點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="057a1-122">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span></span> <span data-ttu-id="057a1-123">Cmdlet 需要虛擬機器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="057a1-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="057a1-124">如果您已經知道要使用的虛擬機器識別碼，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="057a1-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="057a1-125">下一個躍點需要配置 VM 資源以供執行。</span><span class="sxs-lookup"><span data-stu-id="057a1-125">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="get-the-network-interfaces"></a><span data-ttu-id="057a1-126">取得網路介面</span><span class="sxs-lookup"><span data-stu-id="057a1-126">Get the network interfaces</span></span>

<span data-ttu-id="057a1-127">您需要虛擬機器上 NIC 的 IP 位址，在此範例中，我們會擷取虛擬機器上的 NIC。</span><span class="sxs-lookup"><span data-stu-id="057a1-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="057a1-128">如果您已經知道您想要在虛擬機器上測試的 IP 位址，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="057a1-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="057a1-129">取得下一個躍點</span><span class="sxs-lookup"><span data-stu-id="057a1-129">Get Next Hop</span></span>

<span data-ttu-id="057a1-130">現在我們呼叫 `Get-AzureRmNetworkWatcherNextHop` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="057a1-130">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="057a1-131">我們會將網路監看員、虛擬機器識別碼、來源 IP 位址和目的地 IP 位址傳遞給此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="057a1-131">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="057a1-132">在此範例中，目的地 IP 位址是在另一個虛擬網路的 VM。</span><span class="sxs-lookup"><span data-stu-id="057a1-132">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="057a1-133">兩個虛擬網路之間有虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="057a1-133">There is a virtual network gateway between the two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="057a1-134">檢閱結果</span><span class="sxs-lookup"><span data-stu-id="057a1-134">Review results</span></span>

<span data-ttu-id="057a1-135">完成時會提供結果。</span><span class="sxs-lookup"><span data-stu-id="057a1-135">When complete, the results are provided.</span></span> <span data-ttu-id="057a1-136">所傳回的有下一個躍點 IP 位址以及其所屬的資源類型。</span><span class="sxs-lookup"><span data-stu-id="057a1-136">The next hop IP address is returned as well as the type of resource it is.</span></span> <span data-ttu-id="057a1-137">在此案例中，它是虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="057a1-137">In this scenario, it is the public IP address of the virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="057a1-138">下列清單顯示目前可用的 NextHopType 值︰</span><span class="sxs-lookup"><span data-stu-id="057a1-138">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="057a1-139">**下一個躍點類型**</span><span class="sxs-lookup"><span data-stu-id="057a1-139">**Next Hop Type**</span></span>

* <span data-ttu-id="057a1-140">Internet</span><span class="sxs-lookup"><span data-stu-id="057a1-140">Internet</span></span>
* <span data-ttu-id="057a1-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="057a1-141">VirtualAppliance</span></span>
* <span data-ttu-id="057a1-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="057a1-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="057a1-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="057a1-143">VnetLocal</span></span>
* <span data-ttu-id="057a1-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="057a1-144">HyperNetGateway</span></span>
* <span data-ttu-id="057a1-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="057a1-145">VnetPeering</span></span>
* <span data-ttu-id="057a1-146">None</span><span class="sxs-lookup"><span data-stu-id="057a1-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="057a1-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="057a1-147">Next steps</span></span>

<span data-ttu-id="057a1-148">請造訪[使用網路監看員稽核 NSG](network-watcher-nsg-auditing-powershell.md)，以了解如何以程式設計方式檢閱網路安全性群組設定</span><span class="sxs-lookup"><span data-stu-id="057a1-148">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















