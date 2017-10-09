---
title: "aaaCreate 具有使用 PowerShell 將多個 Nic 的 VM （傳統） |Microsoft 文件"
description: "深入了解如何 toocreate，並設定使用 PowerShell 將多個 Nic Vm。"
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
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="1c967-103">建立具有多個 NIC 的 VM (傳統)</span><span class="sxs-lookup"><span data-stu-id="1c967-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="1c967-104">您可以在 Azure 中建立虛擬機器 (Vm)，並附加多個網路介面 (Nic) tooeach 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="1c967-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="1c967-105">多個 NIC 是許多網路虛擬應用裝置的需求，例如應用程式傳遞和 WAN 最佳化解決方案。</span><span class="sxs-lookup"><span data-stu-id="1c967-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="1c967-106">多個 NIC 也能隔離 NIC 之間的流量。</span><span class="sxs-lookup"><span data-stu-id="1c967-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![適用於 VM 的多個 NIC](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="1c967-108">hello 圖便會顯示具有三個 Nic VM，每個連線 tooa 不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="1c967-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c967-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1c967-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1c967-110">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="1c967-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="1c967-111">Microsoft 建議大部分的新部署使用 Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="1c967-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="1c967-112">Hello 「 預設 」 NIC 上才支援網際網路對向的 VIP （傳統部署）</span><span class="sxs-lookup"><span data-stu-id="1c967-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="1c967-113">沒有只有一個 VIP toohello IP 的 hello 預設 nic。</span><span class="sxs-lookup"><span data-stu-id="1c967-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="1c967-114">執行個體層級公用 IP (LPIP) 位址 (傳統部署) 目前不支援多個 NIC 的 VM。</span><span class="sxs-lookup"><span data-stu-id="1c967-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="1c967-115">hello 的 hello Nic 順序內 hello VM 會隨機的而且也可以變更各個 Azure 基礎結構更新。</span><span class="sxs-lookup"><span data-stu-id="1c967-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="1c967-116">不過，hello IP 位址，而且 hello 對應的乙太網路 MAC 位址會保留 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="1c967-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="1c967-117">例如，假設**Eth1**具有 IP 位址是 10.1.0.100 和 00-0D-3A-B0-39-0D 的 MAC 位址，則為 Azure 基礎結構更新並重新開機之後, 就無法變更太**Eth2**，但 hello IP 和 MAC 配對會保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="1c967-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="1c967-118">當客戶啟動重新啟動，NIC 順序 hello 仍 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="1c967-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="1c967-119">hello 每個 VM 上的每個 NIC 的位址必須位於子網路、 在單一上的多個 Nic VM 可以每個指派位址 hello 相同子網路。</span><span class="sxs-lookup"><span data-stu-id="1c967-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="1c967-120">hello VM 大小會決定您可以建立適用於 VM 的 NIC 的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="1c967-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="1c967-121">參考 hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM 大小的發行項 toodetermine 多少 NIC 支援每個 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="1c967-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="1c967-122">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="1c967-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="1c967-123">在資源管理員部署中，VM 上的任何 NIC 可能會關聯至網路安全性群組 (NSG)，包括已啟用多個 NIC 功能的 VM 上的任何 NIC。</span><span class="sxs-lookup"><span data-stu-id="1c967-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="1c967-124">如果 NIC 指派其中 hello 子網路是與 NSG 相關聯的子網路內的位址，然後 hello hello 子網路的 NSG 中的規則也適用於 toothat nic。</span><span class="sxs-lookup"><span data-stu-id="1c967-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="1c967-125">在與 Nsg 加法 tooassociating 子網路，可以也 NIC 關聯 NSG。</span><span class="sxs-lookup"><span data-stu-id="1c967-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="1c967-126">如果子網路是 NSG 和內的 NIC 相關聯的子網路個別與 NSG 相關聯，hello 關聯 NSG 規則會套用**流程順序**根據 toohello hello 流量進入或離開傳遞方向hello NIC:</span><span class="sxs-lookup"><span data-stu-id="1c967-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="1c967-127">**連入流量**其目的地是有問題的 hello NIC 流經先 hello 子網路，觸發 hello 子網路的 NSG 規則，然後再將傳入 hello NIC，然後觸發 hello NIC 的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="1c967-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="1c967-128">**連出流量**其來源為 hello 有問題的 NIC 流程從 hello NIC，觸發 hello NIC 的 NSG 規則通過 hello 的子網路，然後觸發 hello 子網路的 NSG 規則之前先出。</span><span class="sxs-lookup"><span data-stu-id="1c967-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="1c967-129">深入了解[網路安全性群組](virtual-networks-nsg.md)和套用方式根據關聯 toosubnets、 Vm 和 Nic...</span><span class="sxs-lookup"><span data-stu-id="1c967-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="1c967-130">如何 tooConfigure 傳統部署在多重 NIC VM</span><span class="sxs-lookup"><span data-stu-id="1c967-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="1c967-131">下列的 hello 指示將協助您建立多重 NIC VM 包含 3 個 Nic： 預設 NIC 和兩個其他 Nic。</span><span class="sxs-lookup"><span data-stu-id="1c967-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="1c967-132">hello 組態步驟將建立的 VM，將會根據 toohello 服務組態檔片段以下設定：</span><span class="sxs-lookup"><span data-stu-id="1c967-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

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
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="1c967-133">您需要下列必要條件，然後再嘗試 toorun hello hello 範例中的 PowerShell 命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="1c967-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="1c967-134">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c967-134">An Azure subscription.</span></span>
* <span data-ttu-id="1c967-135">已設定的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1c967-135">A configured virtual network.</span></span> <span data-ttu-id="1c967-136">如需 VNet 的詳細資訊，請參閱 [虛擬網路概觀](virtual-networks-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="1c967-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="1c967-137">hello 最新版本的 Azure PowerShell 下載及安裝。</span><span class="sxs-lookup"><span data-stu-id="1c967-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="1c967-138">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="1c967-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="1c967-139">toocreate 具有多個 Nic，完成下列步驟，在單一 PowerShell 工作階段中輸入每個命令的 hello 的 VM:</span><span class="sxs-lookup"><span data-stu-id="1c967-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="1c967-140">從 Azure VM 映像庫中選取 VM 映像</span><span class="sxs-lookup"><span data-stu-id="1c967-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="1c967-141">請注意，映像經常變更且可依區域取得。</span><span class="sxs-lookup"><span data-stu-id="1c967-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="1c967-142">hello hello 下面範例中所指定的映像可能會變更或可能不會在您的地區，因此請確定您需要 toospecify hello 映像。</span><span class="sxs-lookup"><span data-stu-id="1c967-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="1c967-143">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="1c967-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="1c967-144">建立 hello 預設系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="1c967-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="1c967-145">新增其他 Nic toohello VM 組態。</span><span class="sxs-lookup"><span data-stu-id="1c967-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="1c967-146">指定 hello 預設 NIC 的 hello 子網路和 IP 位址</span><span class="sxs-lookup"><span data-stu-id="1c967-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="1c967-147">建立虛擬網路中的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1c967-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="1c967-148">hello 您在此處指定的 VNet 必須已存在 （如 hello 必要條件中所述）。</span><span class="sxs-lookup"><span data-stu-id="1c967-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="1c967-149">下列的 hello 範例會指定虛擬網路，名為**MultiNIC VNet**。</span><span class="sxs-lookup"><span data-stu-id="1c967-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="1c967-150">限制</span><span class="sxs-lookup"><span data-stu-id="1c967-150">Limitations</span></span>
<span data-ttu-id="1c967-151">使用多個 Nic 時，會適用下列限制的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c967-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="1c967-152">具多個 NIC 的 VM 必須建立在 Azure 虛擬網路 (VNet) 中。</span><span class="sxs-lookup"><span data-stu-id="1c967-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="1c967-153">非 VNet 的 VM 無法設定為具有多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="1c967-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="1c967-154">所有 Vm 的可用性中都設定需要 toouse，多個 Nic 或單一 nic。</span><span class="sxs-lookup"><span data-stu-id="1c967-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="1c967-155">在可用性設定組內無法混用多個 NIC VM 和單一 NIC VM。</span><span class="sxs-lookup"><span data-stu-id="1c967-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="1c967-156">雲端服務中的 VM 適用相同規則。</span><span class="sxs-lookup"><span data-stu-id="1c967-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="1c967-157">對於多個 NIC Vm，它們不需要 toohave hello 的 Nic 數目相同，只要它們都各自具有至少兩個。</span><span class="sxs-lookup"><span data-stu-id="1c967-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="1c967-158">一旦部署 VM 之後，如果沒有刪除後再重新建立，則無法使用多個 NIC 設定包含單一 NIC 的 VM (反之亦然)。</span><span class="sxs-lookup"><span data-stu-id="1c967-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="1c967-159">次要 Nic 存取 tooother 子網路</span><span class="sxs-lookup"><span data-stu-id="1c967-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="1c967-160">依預設不會與預設閘道設定次要 Nic，因為 toowhich hello 流量流程在 hello 次要 Nic 會是有限的 toobe hello 內相同的子網路。</span><span class="sxs-lookup"><span data-stu-id="1c967-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="1c967-161">如果 hello 使用者想 tooenable 次要 Nic tootalk 自己的子網路之外，他們必須的 tooadd hello 路由表 tooconfigure hello 閘道做為中的項目如下所述。</span><span class="sxs-lookup"><span data-stu-id="1c967-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="1c967-162">在 2015 年 7 月之前建立的 VM 可能已經為所有 NIC 設定預設閘道。</span><span class="sxs-lookup"><span data-stu-id="1c967-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="1c967-163">這些 Vm 生效，不會移除次要 Nic 的 hello 預設閘道。</span><span class="sxs-lookup"><span data-stu-id="1c967-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="1c967-164">作業系統中，使用 hello 弱式主機路由模型，例如 Linux、 如果 hello 輸入和輸出流量都使用不同的 Nic，可以中斷網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="1c967-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="1c967-165">設定 Windows VM</span><span class="sxs-lookup"><span data-stu-id="1c967-165">Configure Windows VMs</span></span>
<span data-ttu-id="1c967-166">假設您有包含兩個 NIC 的 Windows VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c967-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="1c967-167">主要 NIC IP 位址：192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="1c967-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="1c967-168">次要 NIC IP 位址：192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="1c967-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="1c967-169">此 VM 的 hello IPv4 路由表看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="1c967-169">hello IPv4 route table for this VM would look like this:</span></span>

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

<span data-ttu-id="1c967-170">請注意該 hello 預設路由 (0.0.0.0) 是可用 toohello 主要 NIC</span><span class="sxs-lookup"><span data-stu-id="1c967-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="1c967-171">您將不會外 hello 次要的 hello 子網路的資源，能 tooaccess NIC，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c967-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="1c967-172">的預設路由的 tooadd hello 次要 NIC，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="1c967-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="1c967-173">從命令提示字元執行以下 hello tooidentify hello 索引編號的 hello 命令次要 NIC:</span><span class="sxs-lookup"><span data-stu-id="1c967-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="1c967-174">請注意 hello hello 資料表、 索引為 27 （在此範例中） 中的第二個項目。</span><span class="sxs-lookup"><span data-stu-id="1c967-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="1c967-175">Hello 命令提示字元中執行 hello**路由新增**命令如下所示。</span><span class="sxs-lookup"><span data-stu-id="1c967-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="1c967-176">在此範例中，您要為 hello hello 預設閘道指定 192.168.2.1 次要 NIC:</span><span class="sxs-lookup"><span data-stu-id="1c967-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="1c967-177">tootest 連線返回 toohello 命令提示字元，並再試一次的 tooping 從不同的子網路 hello 次要 NIC 為顯示整數 eh 下面範例：</span><span class="sxs-lookup"><span data-stu-id="1c967-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="1c967-178">您也可以檢查您的路由表 toocheck hello 新加入的路由，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c967-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="1c967-179">設定 Linux VM</span><span class="sxs-lookup"><span data-stu-id="1c967-179">Configure Linux VMs</span></span>
<span data-ttu-id="1c967-180">適用於 Linux Vm，因為 hello 預設行為會使用弱式主機路由，我們建議您該 hello 次要 Nic tootraffic 限制流量只在 hello 內相同的子網路。</span><span class="sxs-lookup"><span data-stu-id="1c967-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="1c967-181">不過如果某些情況下需要 hello 子網路外部連線，使用者應該啟用原則型路由 tooensure hello 輸入，輸出流量使用 hello 相同的 nic。</span><span class="sxs-lookup"><span data-stu-id="1c967-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c967-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c967-182">Next steps</span></span>
* <span data-ttu-id="1c967-183">部署 [在資源管理員部署中的 2 層應用程式案例之多個 NIC VM](virtual-network-deploy-multinic-arm-template.md)。</span><span class="sxs-lookup"><span data-stu-id="1c967-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="1c967-184">部署 [在傳統部署中的 2 層應用程式案例之多個 NIC VM](virtual-network-deploy-multinic-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="1c967-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

