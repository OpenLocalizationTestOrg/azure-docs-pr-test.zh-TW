---
title: "Azure Site Recovery 之中兩個 Azure 區域間的網路對應 | Microsoft Docs"
description: "Azure Site Recovery 可協調虛擬機器和實體伺服器的複寫、容錯移轉及復原作業。 了解如何容錯移轉到 Azure 或次要資料中心。"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="d25d9-104">兩個 Azure 區域間的網路對應</span><span class="sxs-lookup"><span data-stu-id="d25d9-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="d25d9-105">本文說明如何彼此對應兩個 Azure 區域的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d25d9-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="d25d9-106">網路對應可確保在目標 Azure 區域中建立複寫的虛擬機器時，將在與來源虛擬機器之虛擬網路對應的虛擬網路上建立。</span><span class="sxs-lookup"><span data-stu-id="d25d9-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="d25d9-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="d25d9-107">Prerequisites</span></span>
<span data-ttu-id="d25d9-108">對應網路之前，請確定您已在來源和目標 Azure 區域中建立 [Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d25d9-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="d25d9-109">對應網路</span><span class="sxs-lookup"><span data-stu-id="d25d9-109">Map networks</span></span>

<span data-ttu-id="d25d9-110">若要將一個 Azure 區域中的 Azure 虛擬網路對應至另一個地區中的另一個虛擬網路，請移至 [Site Recovery 基礎結構] -> [網路對應] \(適用於 Azure 虛擬機器)，並建立網路對應。</span><span class="sxs-lookup"><span data-stu-id="d25d9-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="d25d9-112">在下列範例中，我的虛擬機器在東亞地區執行，而且正在複寫至東南亞。</span><span class="sxs-lookup"><span data-stu-id="d25d9-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="d25d9-113">選取來源和目標網路，然後按一下 [確定] 建立從東亞到東南亞的網路對應。</span><span class="sxs-lookup"><span data-stu-id="d25d9-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="d25d9-115">以同樣的方式建議從東南亞到東亞的網路對應。</span><span class="sxs-lookup"><span data-stu-id="d25d9-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="d25d9-117">啟用複寫時對應網路</span><span class="sxs-lookup"><span data-stu-id="d25d9-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="d25d9-118">第一次從一個 Azure 區域將虛擬機器複寫到另一個區域時，如果未完成網路對應，您可以在同一個程序中選擇目標網路。</span><span class="sxs-lookup"><span data-stu-id="d25d9-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="d25d9-119">Site Recovery 會根據此選項，建立從來源地區到目標區域以及從目標區域到目標區域的網路對應。</span><span class="sxs-lookup"><span data-stu-id="d25d9-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="d25d9-121">根據預設，Site Recovery 會在目標區域中建立與來源網路相同的網路，並在來源網路的名稱後面加上「-asr」的尾碼。</span><span class="sxs-lookup"><span data-stu-id="d25d9-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="d25d9-122">您可以按一下 [自訂] 選擇已建立的網路。</span><span class="sxs-lookup"><span data-stu-id="d25d9-122">You can choose an already created network by clicking Customize.</span></span>

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="d25d9-124">如果已完成網路對應，您無法在啟用複寫時變更目標虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d25d9-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="d25d9-125">若要變更，請修改現有的網路對應。</span><span class="sxs-lookup"><span data-stu-id="d25d9-125">To change it, modify existing network mapping.</span></span>  

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="d25d9-128">如果將網路對應從 region-1 修改為 region-2，請確定網路對應也從 region-2 修改為 region-1。</span><span class="sxs-lookup"><span data-stu-id="d25d9-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="d25d9-129">子網路選取項目</span><span class="sxs-lookup"><span data-stu-id="d25d9-129">Subnet selection</span></span>
<span data-ttu-id="d25d9-130">目標虛擬機器的子網路，是根據來源虛擬機器的子網路名稱來選取。</span><span class="sxs-lookup"><span data-stu-id="d25d9-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="d25d9-131">如果目標網路中可用的來源虛擬機器有相同名稱的子網路，則會對於目標虛擬機器選擇該子網路。</span><span class="sxs-lookup"><span data-stu-id="d25d9-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="d25d9-132">如果目標網路沒有相同名稱的子網路，則會依字母順序選擇第一個子網路做為目標子網路。</span><span class="sxs-lookup"><span data-stu-id="d25d9-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="d25d9-133">您可以移至虛擬機器的 [計算和網路設定] 修改此子網路。</span><span class="sxs-lookup"><span data-stu-id="d25d9-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![修改子網路](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="d25d9-135">IP 位址</span><span class="sxs-lookup"><span data-stu-id="d25d9-135">IP address</span></span>

<span data-ttu-id="d25d9-136">對於目標虛擬機器的每個網路介面，均按照下列方式選擇 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="d25d9-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="d25d9-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="d25d9-137">DHCP</span></span>
<span data-ttu-id="d25d9-138">如果來源虛擬機器的網路介面使用 DHCP，則也會將目標虛擬機器的網路介面設定為 DHCP。</span><span class="sxs-lookup"><span data-stu-id="d25d9-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="d25d9-139">靜態 IP</span><span class="sxs-lookup"><span data-stu-id="d25d9-139">Static IP</span></span>
<span data-ttu-id="d25d9-140">如果來源虛擬機器的網路介面使用靜態 IP，則也會將目標虛擬機器的網路介面設定為使用靜態 IP。</span><span class="sxs-lookup"><span data-stu-id="d25d9-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="d25d9-141">選擇靜態 IP 的方式如下所示：</span><span class="sxs-lookup"><span data-stu-id="d25d9-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="d25d9-142">相同的位址空間</span><span class="sxs-lookup"><span data-stu-id="d25d9-142">Same address space</span></span>

<span data-ttu-id="d25d9-143">如果來源的子網路和目標子網路具有相同的位址空間，則目標 IP 會設定為與來源虛擬機器的網路介面的 IP 相同。</span><span class="sxs-lookup"><span data-stu-id="d25d9-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="d25d9-144">如果找不到相同的 IP，則將設定其他可用的 IP 做為目標 IP。</span><span class="sxs-lookup"><span data-stu-id="d25d9-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="d25d9-145">不同的位址空間</span><span class="sxs-lookup"><span data-stu-id="d25d9-145">Different address space</span></span>

<span data-ttu-id="d25d9-146">如果來源子網路和目標子網路具有不同的位址空間，則目標 IP 會設定為與目標子網路中的任何可用 IP 相同。</span><span class="sxs-lookup"><span data-stu-id="d25d9-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="d25d9-147">您可以移至虛擬機器的 [計算和網路設定] 修改各個網路介面上的目標 IP。</span><span class="sxs-lookup"><span data-stu-id="d25d9-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d25d9-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d25d9-148">Next steps</span></span>

- <span data-ttu-id="d25d9-149">深入了解[複寫 Azure VM 的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="d25d9-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
