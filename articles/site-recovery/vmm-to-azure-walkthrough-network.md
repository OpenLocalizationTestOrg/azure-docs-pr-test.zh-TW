---
title: "網路與 Azure Site Recovery 的 HYPER-V (withSystem Center VMM) tooAzure 複寫 aaaPlan |Microsoft 文件"
description: "本文將討論網路計劃所需的複寫 （使用 VMM) 的 HYPER-V Vm tooAzure 時"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 51ca8b939b6f96880f83599ea8009eb0bfa5b957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-with-vmm-tooazure-replication"></a><span data-ttu-id="4f2e5-103">步驟 4： 規劃 （使用 VMM) 的 HYPER-V tooAzure 複寫的網路功能</span><span class="sxs-lookup"><span data-stu-id="4f2e5-103">Step 4: Plan networking for Hyper-V (with VMM) tooAzure replication</span></span>

<span data-ttu-id="4f2e5-104">在執行之後[容量規劃](vmm-to-azure-walkthrough-capacity.md)（如果您進行完整部署），閱讀有關網路複寫在內部部署 HYPER-V Vm 中 System Center Virtual Machine Manager (VMM) 時的規劃考量此發行項 toolearn雲端 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-104">After performing [capacity planning](vmm-to-azure-walkthrough-capacity.md) (if you're doing a full deployment), read this article toolearn about network planning considerations when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="4f2e5-105">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="network-mapping-for-replication-tooazure"></a><span data-ttu-id="4f2e5-106">複寫 tooAzure 網路對應</span><span class="sxs-lookup"><span data-stu-id="4f2e5-106">Network mapping for replication tooAzure</span></span>

<span data-ttu-id="4f2e5-107">當複寫 （在 VMM 中管理） 的 HYPER-V Vm tooAzure 時，會使用網路對應。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) tooAzure.</span></span> <span data-ttu-id="4f2e5-108">網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-108">Network mapping maps between VM networks on a source VMM server, and target Azure networks.</span></span> <span data-ttu-id="4f2e5-109">對應未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="4f2e5-109">Mapping does hello following:</span></span>

- <span data-ttu-id="4f2e5-110">**網路連線**— 容錯移轉之後，所有複寫的 Azure Vm 就會連接的 toohello 對應的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-110">**Network connection**—After failover, all replicated Azure VMs are connected toohello mapped Azure network.</span></span> <span data-ttu-id="4f2e5-111">容錯移轉 hello 相同的所有機器網路可以連接 tooeach 其他，即使它們在不同的復原計劃中容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-111">All machines which fail over on hello same network can connect tooeach other, even if they failed over in different recovery plans.</span></span>
- <span data-ttu-id="4f2e5-112">**網路閘道**-Vm 網路閘道已設定 hello 目標 Azure 網路上，如果可以 tooother 在內部部署內部 hello 對應中的虛擬機器網路連線。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-112">**Network gateway**—If a network gateway is set up on hello target Azure network, VMs can connect tooother on-premises virtual machines in hello mapped on-premised network.</span></span>

### <a name="prepare-vmm-for-network-mapping"></a><span data-ttu-id="4f2e5-113">準備 VMM 以進行網路對應</span><span class="sxs-lookup"><span data-stu-id="4f2e5-113">Prepare VMM for network mapping</span></span>

<span data-ttu-id="4f2e5-114">準備 VMM 以進行網路對應，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4f2e5-114">Prepare VMM for network mapping as follows:</span></span>

1. <span data-ttu-id="4f2e5-115">如果您沒有的話，請準備[VMM 邏輯網路](https://docs.microsoft.com/system-center/vmm/network-logical)hello 雲端中的 hello HYPER-V 主機位於與關聯。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-115">If you don't have one, prepare a [VMM logical network](https://docs.microsoft.com/system-center/vmm/network-logical) that's associated with hello cloud in which hello Hyper-V hosts are located.</span></span>
2. <span data-ttu-id="4f2e5-116">如果您沒有的話，請建立[VM 網路](https://docs.microsoft.com/system-center/vmm/network-virtual)連結的 toohello 您備妥以上的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-116">If you don't have one, created a [VM network](https://docs.microsoft.com/system-center/vmm/network-virtual) linked toohello logical network you prepared above.</span></span>
3. <span data-ttu-id="4f2e5-117">連接 Vm 上 hello HYPER-V 主機伺服器/叢集 hello VMM 雲端，toohello VM 網路中。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-117">Connect VMs on hello Hyper-V host server/cluster in hello VMM cloud, toohello VM network.</span></span>

 
<span data-ttu-id="4f2e5-118">請注意：</span><span class="sxs-lookup"><span data-stu-id="4f2e5-118">Note that:</span></span> 
- <span data-ttu-id="4f2e5-119">新的 Vm 新增 toohello 來源 VM 網路連線發生複寫時，toohello 對應 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-119">New VMs are added toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
- <span data-ttu-id="4f2e5-120">如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器在容錯移轉之後連接 toothat 目標子網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-120">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
- <span data-ttu-id="4f2e5-121">如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器所連接 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-121">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>
- <span data-ttu-id="4f2e5-122">您準備 Azure 網路，並設定網路對應，為您部署的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-122">You prepare an Azure network, and set up network mappings, as you deploy hello scenario.</span></span>

## <a name="connecting-tooazure-vms-after-failover"></a><span data-ttu-id="4f2e5-123">在容錯移轉之後連接 tooAzure Vm</span><span class="sxs-lookup"><span data-stu-id="4f2e5-123">Connecting tooAzure VMs after failover</span></span>

<span data-ttu-id="4f2e5-124">規劃您的複寫和容錯移轉策略 hello 重要的問題的其中一個時，如何在容錯移轉之後 tooconnect toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-124">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="4f2e5-125">設計複本 Azure VM 的網路策略時，有兩種選擇：</span><span class="sxs-lookup"><span data-stu-id="4f2e5-125">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="4f2e5-126">**使用不同的 IP 位址**： 您可以選取 toouse 不同的 IP 位址範圍的 hello 複寫 Azure VM 網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-126">**Use a different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="4f2e5-127">在此案例 hello VM 容錯移轉之後，取得新的 IP 位址，DNS 更新為必要項。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-127">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="4f2e5-128">**保留相同的 IP 位址的 hello**： 您可能會想 toouse hello 相同 IP 位址範圍，在主要在內部網路，如 hello Azure 網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-128">**Retain hello same IP address**: You might want toouse hello same IP address range as that in your primary on-premises network, for hello Azure network after failover.</span></span>  <span data-ttu-id="4f2e5-129">可簡化相同的 IP 位址保持 hello hello 復原藉由減少容錯移轉之後網路相關的問題。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-129">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="4f2e5-130">不過，當您要複寫 tooAzure，您必須 tooupdate hello 新位置的 hello IP 位址的路由在容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-130">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="4f2e5-131">保留 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4f2e5-131">Retain IP addresses</span></span>

<span data-ttu-id="4f2e5-132">容錯移轉 tooAzure，具有子網路容錯移轉時，站台復原提供 hello 功能 tooretain 固定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-132">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="4f2e5-133">藉由子網路容錯移轉，特定的子網路會存在於站台 1 或站台 2 中，但絕不會同時存在於這兩個站台中。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-133">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="4f2e5-134">順序 toomaintain hello IP 位址空間 hello 事件中的容錯移轉，在您以程式設計的方式排列 hello 路由器基礎結構 toomove hello 子網路從一個站台 tooanother。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-134">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="4f2e5-135">容錯移轉期間，以 hello hello 子網路移動相關的受保護的 Vm。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-135">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="4f2e5-136">hello 主要缺點是，在 hello 事件中的失敗，您必須 toomove hello 整個子網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-136">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>



### <a name="failover-example"></a><span data-ttu-id="4f2e5-137">容錯移轉範例</span><span class="sxs-lookup"><span data-stu-id="4f2e5-137">Failover example</span></span>

<span data-ttu-id="4f2e5-138">讓我們看看 tooAzure 容錯移轉的範例。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-138">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="4f2e5-139">Woodgrove Bank 是一家虛構的公司，擁有裝載其商務應用程式的內部部署基礎結構。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-139">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="4f2e5-140">它們的行動應用程式裝載在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-140">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="4f2e5-141">Woodgrove Bank Vm 在 Azure 和內部部署伺服器之間的連線是由站台對站台 (VPN) 連線 hello 在內部部署邊緣網路與 hello Azure 虛擬網路之間提供。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-141">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="4f2e5-142">這個 hello 公司的 Azure 虛擬網路的 VPN 表示會顯示為其內部部署網路的延伸。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-142">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="4f2e5-143">Woodgrove 想 toouse Site Recovery tooreplicate 內部工作負載 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-143">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="4f2e5-144">Woodgrove 有 toodeal 應用程式與組態的硬式編碼的 IP 位址，而定，因此在容錯移轉 tooAzure 之後的應用程式需要 tooretain IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-144">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="4f2e5-145">Woodgrove 已指派的 IP 位址範圍 172.16.1.0/24 從 172.16.2.0/24 tooits 資源在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-145">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="4f2e5-146">Woodgrove toobe 無法 tooreplicate 其 Vm tooAzure 時保留 hello IP 位址，如以下是何種 hello 公司需要 toodo:</span><span class="sxs-lookup"><span data-stu-id="4f2e5-146">For Woodgrove toobe able tooreplicate its VMs tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="4f2e5-147">建立 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-147">Create an Azure virtual network.</span></span> <span data-ttu-id="4f2e5-148">它應該 hello 的延伸模組為內部網路，使應用程式可以順暢地進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-148">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="4f2e5-149">Azure 可讓您 tooadd 站對站 VPN 連線能力，此外 toopoint 對站連線能力 toohello 虛擬網路在 Azure 中建立。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-149">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="4f2e5-150">設定 hello 站對站連線，請在 hello Azure 網路，只有 hello IP 位址範圍是不同 hello 內部 IP 位址範圍內，您可以路由傳送流量 toohello 在內部部署位置 （區域網路）。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-150">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="4f2e5-151">這是因為 Azure 不支援延伸的子網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-151">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="4f2e5-152">因此如果您有子網路 192.168.1.0/24 內部部署，您無法加入本機網路 192.168.1.0/24 hello Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-152">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="4f2e5-153">這是預期行為，因為 Azure 不知道 hello 的子網路中有沒有作用中的 Vm，並只災害復原正在建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-153">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="4f2e5-154">toobe toocorrectly 無法路由傳送網路流量超出 hello 網路和 hello 本機網路中的 Azure 網路 hello 子網路不得發生衝突。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-154">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![子網路容錯移轉之前](./media/vmm-to-azure-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="4f2e5-156">容錯移轉之前</span><span class="sxs-lookup"><span data-stu-id="4f2e5-156">Before failover</span></span>

1. <span data-ttu-id="4f2e5-157">建立額外的網路 (例如「復原網路」)。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-157">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="4f2e5-158">這是 hello 網路中的容錯移轉的 Vm 會建立。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-158">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="4f2e5-159">容錯移轉之後，在 hello VM 屬性仍會保留 hello vm 的 IP 位址的 tooensure >**設定**，指定相同的 IP 位址 VM 內部，並按一下該 hello hello**儲存**。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-159">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="4f2e5-160">當 hello VM 容錯移轉時，Azure Site Recovery 會指派提供 IP 位址 tooit hello。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-160">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![網路屬性](./media/vmm-to-azure-walkthrough-network/network-design8.png)

4. <span data-ttu-id="4f2e5-162">容錯移轉觸發程序會觸發，並 hello Vm 在 Azure 中建立具有所需的 hello IP 位址之後，您可以連接 toohello 網路使用[Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-162">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="4f2e5-163">此動作可以編寫指令碼。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-163">This action can be scripted.</span></span>
5. <span data-ttu-id="4f2e5-164">路由需要適當地修改，toobe tooreflect 該 192.168.1.0/24 現在已移 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-164">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![子網路容錯移轉之後](./media/vmm-to-azure-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="4f2e5-166">容錯移轉之後</span><span class="sxs-lookup"><span data-stu-id="4f2e5-166">After failover</span></span>

<span data-ttu-id="4f2e5-167">如果您還沒有如上所示的 Azure 網路，可以在容錯移轉之後，建立主要站台與 Azure 之間的站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-167">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="4f2e5-168">變更 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4f2e5-168">Change IP addresses</span></span>

<span data-ttu-id="4f2e5-169">這[部落格文章](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)說明如何 tooset 向上 hello Azure 網路基礎結構時您不需要 tooretain IP 位址在容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-169">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="4f2e5-170">它會啟動應用程式描述、 查看如何 tooset 網路內部部署，以及在 Azure 中，並於結尾提供執行容錯移轉的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4f2e5-170">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4f2e5-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f2e5-171">Next steps</span></span>

<span data-ttu-id="4f2e5-172">跳過[步驟 5： 準備 Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="4f2e5-172">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>
