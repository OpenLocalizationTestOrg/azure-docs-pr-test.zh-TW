---
title: "Azure Site Recovery 中的兩個 Azure 區域之間的 aaaNetwork 對應 |Microsoft 文件"
description: "Azure Site Recovery 會協調 hello 複寫、 容錯移轉和復原的虛擬機器和實體伺服器。 深入了解容錯移轉 tooAzure 或次要資料中心。"
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
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="b2e8e-104">兩個 Azure 區域間的網路對應</span><span class="sxs-lookup"><span data-stu-id="b2e8e-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="b2e8e-105">本文說明如何 toomap Azure 虛擬網路的兩個彼此的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="b2e8e-106">網路對應可確保當 hello 目標 Azure 區域中建立複寫的虛擬機器時，它會建立 hello 是對應的 toovirtual hello 來源虛擬機器網路的虛擬網路上。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="b2e8e-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="b2e8e-107">Prerequisites</span></span>
<span data-ttu-id="b2e8e-108">對應網路之前，請確定您已在來源和目標 Azure 區域中建立 [Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="b2e8e-109">對應網路</span><span class="sxs-lookup"><span data-stu-id="b2e8e-109">Map networks</span></span>

<span data-ttu-id="b2e8e-110">toomap 一個 Azure 區域 tooanother 虛擬網路在其他區域中，移 tooSite Recovery 基礎結構中的 Azure 虛擬網路]-> [網路對應 （適用於 Azure 虛擬機器），並建立網路對應。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="b2e8e-112">在 hello 例會我的虛擬機器在東亞地區執行，而且正在複寫 tooSoutheast 亞洲。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="b2e8e-113">選取 hello 來源和目標網路，然後按一下確定 toocreate 東亞 tooSoutheast 亞洲的網路對應。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="b2e8e-115">請勿 hello 同一件事 toocreate 東南亞 tooEast 亞洲的網路對應。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="b2e8e-117">啟用複寫時對應網路</span><span class="sxs-lookup"><span data-stu-id="b2e8e-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="b2e8e-118">如果您要將虛擬機器的 hello 第一次表單一個 Azure 區域 tooanother 複寫時未完成網路對應，然後您可以選擇目標網路一部分 hello 相同的程序。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="b2e8e-119">站台復原會在從來源區域 tootarget 地區和這個選取的目標地區 toosource 區域建立網路對應。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="b2e8e-121">根據預設，站台復原會建立網路是相同的 toohello 來源網路的 hello 目標區域中，並加上 '-asr' 後置詞 toohello hello 來源網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="b2e8e-122">您可以按一下 [自訂] 選擇已建立的網路。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-122">You can choose an already created network by clicking Customize.</span></span>

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="b2e8e-124">如果已完成 hello 網路對應，您無法啟用複寫時變更 hello 目標虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="b2e8e-125">toochange，修改現有的網路對應。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-125">toochange it, modify existing network mapping.</span></span>  

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![網路對應](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="b2e8e-128">如果您修改區域 1 tooregion-2 的網路對應，請確定您修改區域 2 tooregion-1 以及從 hello 網路對應。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="b2e8e-129">子網路選取項目</span><span class="sxs-lookup"><span data-stu-id="b2e8e-129">Subnet selection</span></span>
<span data-ttu-id="b2e8e-130">Hello 目標虛擬機器的子網路，選取上 hello hello hello 來源虛擬機器的子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="b2e8e-131">Hello 的子網路是否名稱相同的 hello hello 目標網路，在可用的來源虛擬機器則可替 hello 目標虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="b2e8e-132">如果沒有 hello 的子網路名稱相同 hello 目標網路，然後選擇依字母順序的第一個子網路是因為 hello 目標子網路。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="b2e8e-133">您可以修改此子網路移 tooCompute 和 hello 虛擬機器的網路設定。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![修改子網路](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="b2e8e-135">IP 位址</span><span class="sxs-lookup"><span data-stu-id="b2e8e-135">IP address</span></span>

<span data-ttu-id="b2e8e-136">選擇每個 hello hello 目標虛擬機器網路介面的 IP 位址，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2e8e-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="b2e8e-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="b2e8e-137">DHCP</span></span>
<span data-ttu-id="b2e8e-138">如果 hello hello 來源虛擬機器網路介面使用 DHCP，然後 hello 目標虛擬機器的網路介面也會設為 DHCP。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="b2e8e-139">靜態 IP</span><span class="sxs-lookup"><span data-stu-id="b2e8e-139">Static IP</span></span>
<span data-ttu-id="b2e8e-140">如果 hello 網路介面的 hello 來源虛擬機器使用靜態 IP，然後 hello 目標虛擬機器的網路介面也會設 toouse 靜態 IP。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="b2e8e-141">選擇靜態 IP 的方式如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2e8e-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="b2e8e-142">相同的位址空間</span><span class="sxs-lookup"><span data-stu-id="b2e8e-142">Same address space</span></span>

<span data-ttu-id="b2e8e-143">如果 hello 來源子網路和 hello 目標子網路有 hello 相同，則目標 IP 已設定相同的 hello hello 來源虛擬機器網路介面的 hello IP 位址空間。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="b2e8e-144">如果找不到相同的 IP，然後其他可用的 IP 會設定為 hello 目標 IP。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="b2e8e-145">不同的位址空間</span><span class="sxs-lookup"><span data-stu-id="b2e8e-145">Different address space</span></span>

<span data-ttu-id="b2e8e-146">如果 hello 來源的子網路和 hello 目標子網路具有不同的位址空間，做為 hello 目標子網路中任何可用的 IP 設定目標 IP。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="b2e8e-147">您可以修改每個網路介面上的 hello 目標 IP 移 tooCompute 和 hello 虛擬機器的網路設定。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2e8e-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2e8e-148">Next steps</span></span>

- <span data-ttu-id="b2e8e-149">深入了解[複寫 Azure VM 的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="b2e8e-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
