---
title: "使用 PowerShell 建立具有多個 NIC 的 VM (傳統) | Microsoft Docs"
description: "深入了解如何使用 PowerShell 建立與設定具有多個 NIC 的 VM。"
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 68ccc1cac22e593b099729fe68c6bee63df44d9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="1ed85-103">建立具有多個 NIC 的 VM (傳統)</span><span class="sxs-lookup"><span data-stu-id="1ed85-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="1ed85-104">您可以在 Azure 中建立虛擬機器 (VM) 並將多個網路介面 (NIC) 連接至每個 VM。</span><span class="sxs-lookup"><span data-stu-id="1ed85-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="1ed85-105">多個 NIC 是許多網路虛擬應用裝置的需求，例如應用程式傳遞和 WAN 最佳化解決方案。</span><span class="sxs-lookup"><span data-stu-id="1ed85-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="1ed85-106">多個 NIC 也能隔離 NIC 之間的流量。</span><span class="sxs-lookup"><span data-stu-id="1ed85-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![適用於 VM 的多個 NIC](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="1ed85-108">圖中顯示具有三個 NIC 的 VM，每個都連接到不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="1ed85-108">The figure shows a VM with three NICs, each connected to a different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ed85-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1ed85-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1ed85-110">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="1ed85-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="1ed85-111">Microsoft 建議大部分的新部署使用 Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="1ed85-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="1ed85-112">只有「預設」NIC 上才支援網際網路對向的 VIP (傳統部署)。</span><span class="sxs-lookup"><span data-stu-id="1ed85-112">Internet-facing VIP (classic deployments) is only supported on the "default" NIC.</span></span> <span data-ttu-id="1ed85-113">只有一個  VIP 可以連接到預設 NIC 的 IP。</span><span class="sxs-lookup"><span data-stu-id="1ed85-113">There is only one VIP to the IP of the default NIC.</span></span>
* <span data-ttu-id="1ed85-114">執行個體層級公用 IP (LPIP) 位址 (傳統部署) 目前不支援多個 NIC 的 VM。</span><span class="sxs-lookup"><span data-stu-id="1ed85-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="1ed85-115">VM 內部的 NIC 順序是隨機的，而且也可透過 Azure 基礎結構更新來變更。</span><span class="sxs-lookup"><span data-stu-id="1ed85-115">The order of the NICs from inside the VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="1ed85-116">不過，IP 位址及對應的乙太網路 MAC 位址會維持不變。</span><span class="sxs-lookup"><span data-stu-id="1ed85-116">However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same.</span></span> <span data-ttu-id="1ed85-117">例如，假設 **Eth1** 具有 IP 位址 10.1.0.100 和 MAC 位址 00-0D-3A-B0-39-0D；在 Azure 基礎結構更新並重新開機之後，就無法變更為 **Eth2**，但是 IP 和 MAC 配對會保持相同。</span><span class="sxs-lookup"><span data-stu-id="1ed85-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed to **Eth2**, but the IP and MAC pairing will remain the same.</span></span> <span data-ttu-id="1ed85-118">當客戶起始重新啟動時，NIC 順序會保持相同。</span><span class="sxs-lookup"><span data-stu-id="1ed85-118">When a restart is customer-initiated, the NIC order will remain the same.</span></span>
* <span data-ttu-id="1ed85-119">每個 VM 上的每個 NIC 位址都必須位於子網路中，單一 VM 上的多個 NIC 每個都可以指派位於相同子網路的位址。</span><span class="sxs-lookup"><span data-stu-id="1ed85-119">The address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in the same subnet.</span></span>
* <span data-ttu-id="1ed85-120">VM 大小會決定您可以為 VM 建立的 NIC 數目。</span><span class="sxs-lookup"><span data-stu-id="1ed85-120">The VM size determines the number of NICS that you can create for a VM.</span></span> <span data-ttu-id="1ed85-121">請參考 [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 和 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 的VM 大小文章，以確定每個 VM 大小支援的 NIC 數目。</span><span class="sxs-lookup"><span data-stu-id="1ed85-121">Reference the [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles to determine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="1ed85-122">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="1ed85-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="1ed85-123">在資源管理員部署中，VM 上的任何 NIC 可能會關聯至網路安全性群組 (NSG)，包括已啟用多個 NIC 功能的 VM 上的任何 NIC。</span><span class="sxs-lookup"><span data-stu-id="1ed85-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="1ed85-124">如果已為 NIC 指派子網路 (該子網路會關聯至 NSG) 內的位址，則子網路 NSG 中的規則也適用於該 NIC。</span><span class="sxs-lookup"><span data-stu-id="1ed85-124">If a NIC is assigned an address within a subnet where the subnet is associated with an NSG, then the rules in the subnet’s NSG also apply to that NIC.</span></span> <span data-ttu-id="1ed85-125">除了將子網路關聯至 NSG，您也可以將 NIC 關聯至 NSG。</span><span class="sxs-lookup"><span data-stu-id="1ed85-125">In addition to associating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="1ed85-126">如果將子網路關聯至 NSG，而且該子網路內的 NIC 會個別關聯至 NSG，則相關聯的 NSG 規則會根據傳入或傳出 NIC 的流量方向套用 **流程順序** ：</span><span class="sxs-lookup"><span data-stu-id="1ed85-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, the associated NSG rules are applied in **flow order** according to the direction of the traffic being passed into or out of the NIC:</span></span>

* <span data-ttu-id="1ed85-127">**連入流量** 的目的地是上述流量中的 NIC，首先會通過子網路，並在傳入 NIC 前觸發子網路的 NSG 規則，然後再觸發 NIC 的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="1ed85-127">**Incoming traffic** whose destination is the NIC in question flows first through the subnet, triggering the subnet’s NSG rules, before passing into the NIC, then triggering the NIC’s NSG rules.</span></span>
* <span data-ttu-id="1ed85-128">**連出流量** 的來源是有問題的流量中第一次從 NIC 流出的 NIC，會在流經子網路之前觸發 NIC 的 NSG 規則，然後觸發子網路的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="1ed85-128">**Outgoing traffic** whose source is the NIC in question flows first out from the NIC, triggering the NIC’s NSG rules, before passing through the subnet, then triggering the subnet’s NSG rules.</span></span>

<span data-ttu-id="1ed85-129">深入了解 [網路安全性群組](virtual-networks-nsg.md) 和其如何根據與子網路、VM 和 NIC 之關聯而套用。</span><span class="sxs-lookup"><span data-stu-id="1ed85-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations to subnets, VMs, and NICs..</span></span>

## <a name="how-to-configure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="1ed85-130">如何在傳統部署中設定有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="1ed85-130">How to Configure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="1ed85-131">下列指示將協助您建立多個 NIC 的 VM，其中包含 3 個 NIC：一個預設的 NIC 和兩個額外的 NIC。</span><span class="sxs-lookup"><span data-stu-id="1ed85-131">The instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="1ed85-132">組態步驟將建立 VM，此 VM 將根據下列服務組態檔片段來設定：</span><span class="sxs-lookup"><span data-stu-id="1ed85-132">The configuration steps will create a VM that will be configured according to the service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over the remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="1ed85-133">嘗試執行此範例的 PowerShell 命令之前，您需要具備下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="1ed85-133">You need the following prerequisites before trying to run the PowerShell commands in the example.</span></span>

* <span data-ttu-id="1ed85-134">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ed85-134">An Azure subscription.</span></span>
* <span data-ttu-id="1ed85-135">已設定的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1ed85-135">A configured virtual network.</span></span> <span data-ttu-id="1ed85-136">如需 VNet 的詳細資訊，請參閱 [虛擬網路概觀](virtual-networks-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="1ed85-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="1ed85-137">已下載並安裝最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1ed85-137">The latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="1ed85-138">請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="1ed85-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="1ed85-139">若要建立具有多個 NIC 的 VM，請完成下列步驟，在單一 PowerShell 工作階段中輸入每個命令︰</span><span class="sxs-lookup"><span data-stu-id="1ed85-139">To create a VM with multiple NICs, complete the following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="1ed85-140">從 Azure VM 映像庫中選取 VM 映像</span><span class="sxs-lookup"><span data-stu-id="1ed85-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="1ed85-141">請注意，映像經常變更且可依區域取得。</span><span class="sxs-lookup"><span data-stu-id="1ed85-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="1ed85-142">以下範例中指定的映像可能會變更，或者可能不在您的區域中，因此，請務必指定您需要的映像。</span><span class="sxs-lookup"><span data-stu-id="1ed85-142">The image specified in the example below may change or might not be in your region, so be sure to specify the image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="1ed85-143">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="1ed85-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="1ed85-144">建立預設的系統管理員登入。</span><span class="sxs-lookup"><span data-stu-id="1ed85-144">Create the default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="1ed85-145">在 VM 組態中加入其他 NIC。</span><span class="sxs-lookup"><span data-stu-id="1ed85-145">Add additional NICs to the VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="1ed85-146">指定預設 NIC 的子網路和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1ed85-146">Specify the subnet and IP address for the default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="1ed85-147">在虛擬網路中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="1ed85-147">Create the VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="1ed85-148">您在此處指定的 VNet 必須已經存在 (如必要條件中所提及)。</span><span class="sxs-lookup"><span data-stu-id="1ed85-148">The VNet that you specify here must already exist (as mentioned in the prerequisites).</span></span> <span data-ttu-id="1ed85-149">下面範例指定名稱為 **MultiNIC-VNet**的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1ed85-149">The example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="1ed85-150">限制</span><span class="sxs-lookup"><span data-stu-id="1ed85-150">Limitations</span></span>
<span data-ttu-id="1ed85-151">使用多個 NIC 功能時有下列限制︰</span><span class="sxs-lookup"><span data-stu-id="1ed85-151">The following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="1ed85-152">具多個 NIC 的 VM 必須建立在 Azure 虛擬網路 (VNet) 中。</span><span class="sxs-lookup"><span data-stu-id="1ed85-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="1ed85-153">非 VNet 的 VM 無法設定為具有多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="1ed85-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="1ed85-154">可用性設定組中的所有 VM 都必須使用多個 NIC 或單一 NIC。</span><span class="sxs-lookup"><span data-stu-id="1ed85-154">All VMs in an availability set need to use either multiple NICs or a single NIC.</span></span> <span data-ttu-id="1ed85-155">在可用性設定組內無法混用多個 NIC VM 和單一 NIC VM。</span><span class="sxs-lookup"><span data-stu-id="1ed85-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="1ed85-156">雲端服務中的 VM 適用相同規則。</span><span class="sxs-lookup"><span data-stu-id="1ed85-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="1ed85-157">具多個 NIC 的 VM 不需要有相同數目的 NIC，只要它們各自都有至少兩個即可。</span><span class="sxs-lookup"><span data-stu-id="1ed85-157">For multiple NIC VMs, they aren't required to have the same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="1ed85-158">一旦部署 VM 之後，如果沒有刪除後再重新建立，則無法使用多個 NIC 設定包含單一 NIC 的 VM (反之亦然)。</span><span class="sxs-lookup"><span data-stu-id="1ed85-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-to-other-subnets"></a><span data-ttu-id="1ed85-159">其他子網路的次要 NIC 存取</span><span class="sxs-lookup"><span data-stu-id="1ed85-159">Secondary NICs access to other subnets</span></span>
<span data-ttu-id="1ed85-160">根據預設，將不會使用預設閘道設定次要 NIC，因為次要 NIC 上的流量將會限制在相同的子網路內。</span><span class="sxs-lookup"><span data-stu-id="1ed85-160">By default secondary NICs will not be configured with a default gateway, due to which the traffic flow on the secondary NICs will be limited to be within the same subnet.</span></span> <span data-ttu-id="1ed85-161">如果使用者想要啟用次要 NIC 在其子網路外部通訊，他們必須在路由表中新增項目以設定閘道，如下所述。</span><span class="sxs-lookup"><span data-stu-id="1ed85-161">If the users want to enable secondary NICs to talk outside their own subnet, they will need to add an entry in the routing table to configure the gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="1ed85-162">在 2015 年 7 月之前建立的 VM 可能已經為所有 NIC 設定預設閘道。</span><span class="sxs-lookup"><span data-stu-id="1ed85-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="1ed85-163">在這些 VM 重新開機之前，將不會移除次要 NIC 的預設閘道。</span><span class="sxs-lookup"><span data-stu-id="1ed85-163">The default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="1ed85-164">在使用弱式主機路由模型的作業系統 (例如 Linux) 中，如果輸入和輸出流量使用不同的 NIC，網際網路連線可能會中斷。</span><span class="sxs-lookup"><span data-stu-id="1ed85-164">In Operating systems that use the weak host routing model, such as Linux, Internet connectivity can break if the ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="1ed85-165">設定 Windows VM</span><span class="sxs-lookup"><span data-stu-id="1ed85-165">Configure Windows VMs</span></span>
<span data-ttu-id="1ed85-166">假設您有包含兩個 NIC 的 Windows VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ed85-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="1ed85-167">主要 NIC IP 位址：192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="1ed85-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="1ed85-168">次要 NIC IP 位址：192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="1ed85-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="1ed85-169">此 VM 的 IPv4 路由表看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="1ed85-169">The IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="1ed85-170">請注意，預設路由 (0.0.0.0) 僅提供主要 NIC 使用。</span><span class="sxs-lookup"><span data-stu-id="1ed85-170">Notice that the default route (0.0.0.0) is only available to the primary NIC.</span></span> <span data-ttu-id="1ed85-171">您將無法存取次要 NIC 子網路外部的資源，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ed85-171">You will not be able to access resources outside the subnet for the secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="1ed85-172">若要在次要 NIC 上新增預設路由，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1ed85-172">To add a default route on the secondary NIC, follow the steps below:</span></span>

1. <span data-ttu-id="1ed85-173">從命令提示字元執行下列命令來識別次要 NIC 的索引編號：</span><span class="sxs-lookup"><span data-stu-id="1ed85-173">From a command prompt, run the command below to identify the index number for the secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="1ed85-174">請注意資料表中的第二個項目，索引為 27 (此範例中)。</span><span class="sxs-lookup"><span data-stu-id="1ed85-174">Notice the second entry in the table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="1ed85-175">透過下列方式，經由命令提示字元執行 **route add** 命令。</span><span class="sxs-lookup"><span data-stu-id="1ed85-175">From the command prompt, run the **route add** command as shown below.</span></span> <span data-ttu-id="1ed85-176">在此範例中，您指定 192.168.2.1 做為次要 NIC 的預設閘道：</span><span class="sxs-lookup"><span data-stu-id="1ed85-176">In this example, you are specifying 192.168.2.1 as the default gateway for the secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="1ed85-177">若要測試連線，請移至命令提示字元並嘗試 ping 不同的次要 NIC 子網路，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="1ed85-177">To test connectivity, go back to the command prompt and try to ping a different subnet from the secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="1ed85-178">您也可以檢查您的路由表，來檢查新加入的路由，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ed85-178">You can also check your route table to check the newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="1ed85-179">設定 Linux VM</span><span class="sxs-lookup"><span data-stu-id="1ed85-179">Configure Linux VMs</span></span>
<span data-ttu-id="1ed85-180">若是 Linux VM，因為預設行為是使用弱式主機路由，建議您將次要 NIC 的流量限制在相同的子網路中。</span><span class="sxs-lookup"><span data-stu-id="1ed85-180">For Linux VMs, since the default behavior uses weak host routing, we recommend that the secondary NICs are restricted to traffic flows only within the same subnet.</span></span> <span data-ttu-id="1ed85-181">不過，如果某些情況要求子網路外部的連線，使用者應該根據路由啟用原則，以確保輸入和輸出流量都使用相同的 NIC。</span><span class="sxs-lookup"><span data-stu-id="1ed85-181">However if certain scenarios demand connectivity outside the subnet, users should enable policy based routing to ensure that the ingress and egress traffic uses the same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ed85-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ed85-182">Next steps</span></span>
* <span data-ttu-id="1ed85-183">部署 [在資源管理員部署中的 2 層應用程式案例之多個 NIC VM](virtual-network-deploy-multinic-arm-template.md)。</span><span class="sxs-lookup"><span data-stu-id="1ed85-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="1ed85-184">部署 [在傳統部署中的 2 層應用程式案例之多個 NIC VM](virtual-network-deploy-multinic-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="1ed85-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

