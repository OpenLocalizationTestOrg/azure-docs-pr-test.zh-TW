---
title: "網路與 Azure Site Recovery （不含 System Center VMM) 的 HYPER-V tooAzure 複寫 aaaPlan |Microsoft 文件"
description: "本文將討論網路計劃所需的複寫 （無 VMM) 的 HYPER-V Vm tooAzure 時"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a><span data-ttu-id="53f89-103">步驟 4： 規劃 HYPER-V tooAzure 複寫的網路功能</span><span class="sxs-lookup"><span data-stu-id="53f89-103">Step 4: Plan networking for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="53f89-104">本文摘要說明網路規劃考量，當複寫在內部使用 hello （不含 System Center VMM) 的 HYPER-V Vm tooAzure [Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="53f89-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="53f89-105">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="53f89-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-tooreplica-vms-after-failover"></a><span data-ttu-id="53f89-106">在容錯移轉之後連接 tooreplica Vm</span><span class="sxs-lookup"><span data-stu-id="53f89-106">Connecting tooreplica VMs after failover</span></span>

<span data-ttu-id="53f89-107">規劃您的複寫和容錯移轉策略 hello 重要的問題的其中一個時，如何在容錯移轉之後 tooconnect toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="53f89-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="53f89-108">設計複本 Azure VM 的網路策略時，有兩種選擇：</span><span class="sxs-lookup"><span data-stu-id="53f89-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="53f89-109">**不同的 IP 位址**： 您可以選取 toouse 不同的 IP 位址範圍的 hello 複寫 Azure VM 網路。</span><span class="sxs-lookup"><span data-stu-id="53f89-109">**Different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="53f89-110">在此案例 hello VM 容錯移轉之後，取得新的 IP 位址，DNS 更新為必要項。</span><span class="sxs-lookup"><span data-stu-id="53f89-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="53f89-111">深入了解</span><span class="sxs-lookup"><span data-stu-id="53f89-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="53f89-112">**相同的 IP 位址**： 您可以在主要在內部網路，如 hello Azure 網路容錯移轉之後，toouse hello 相同 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="53f89-112">**Same IP address**: You might want toouse hello same IP address range as that in your primary on-premises network, for hello Azure network after failover.</span></span>  <span data-ttu-id="53f89-113">可簡化相同的 IP 位址保持 hello hello 復原藉由減少容錯移轉之後網路相關的問題。</span><span class="sxs-lookup"><span data-stu-id="53f89-113">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="53f89-114">不過，當您要複寫 tooAzure，您必須 tooupdate hello 新位置的 hello IP 位址的路由在容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="53f89-114">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="53f89-115">保留 IP 位址</span><span class="sxs-lookup"><span data-stu-id="53f89-115">Retain IP addresses</span></span>

<span data-ttu-id="53f89-116">容錯移轉 tooAzure，具有子網路容錯移轉時，站台復原提供 hello 功能 tooretain 固定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="53f89-116">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="53f89-117">藉由子網路容錯移轉，特定的子網路會存在於站台 1 或站台 2 中，但絕不會同時存在於這兩個站台中。</span><span class="sxs-lookup"><span data-stu-id="53f89-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="53f89-118">順序 toomaintain hello IP 位址空間 hello 事件中的容錯移轉，在您以程式設計的方式排列 hello 路由器基礎結構 toomove hello 子網路從一個站台 tooanother。</span><span class="sxs-lookup"><span data-stu-id="53f89-118">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="53f89-119">容錯移轉期間，以 hello hello 子網路移動相關的受保護的 Vm。</span><span class="sxs-lookup"><span data-stu-id="53f89-119">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="53f89-120">hello 主要缺點是，在 hello 事件中的失敗，您必須 toomove hello 整個子網路。</span><span class="sxs-lookup"><span data-stu-id="53f89-120">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="53f89-121">容錯移轉範例</span><span class="sxs-lookup"><span data-stu-id="53f89-121">Failover example</span></span>

<span data-ttu-id="53f89-122">讓我們看看 tooAzure 容錯移轉的範例。</span><span class="sxs-lookup"><span data-stu-id="53f89-122">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="53f89-123">Woodgrove Bank 是一家虛構的公司，擁有裝載其商務應用程式的內部部署基礎結構。</span><span class="sxs-lookup"><span data-stu-id="53f89-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="53f89-124">它們的行動應用程式裝載在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="53f89-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="53f89-125">Woodgrove Bank Vm 在 Azure 和內部部署伺服器之間的連線是由站台對站台 (VPN) 連線 hello 在內部部署邊緣網路與 hello Azure 虛擬網路之間提供。</span><span class="sxs-lookup"><span data-stu-id="53f89-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="53f89-126">這個 hello 公司的 Azure 虛擬網路的 VPN 表示會顯示為其內部部署網路的延伸。</span><span class="sxs-lookup"><span data-stu-id="53f89-126">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="53f89-127">Woodgrove 想 toouse Site Recovery tooreplicate 內部工作負載 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="53f89-127">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="53f89-128">Woodgrove 有 toodeal 應用程式與組態的硬式編碼的 IP 位址，而定，因此在容錯移轉 tooAzure 之後的應用程式需要 tooretain IP 位址。</span><span class="sxs-lookup"><span data-stu-id="53f89-128">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="53f89-129">Woodgrove 已指派的 IP 位址範圍 172.16.1.0/24 從 172.16.2.0/24 tooits 資源在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="53f89-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="53f89-130">Woodgrove toobe 無法 tooreplicate 其 Vm tooAzure 時保留 hello IP 位址，如以下是何種 hello 公司需要 toodo:</span><span class="sxs-lookup"><span data-stu-id="53f89-130">For Woodgrove toobe able tooreplicate its VMs tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="53f89-131">建立 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="53f89-131">Create an Azure virtual network.</span></span> <span data-ttu-id="53f89-132">它應該 hello 的延伸模組為內部網路，使應用程式可以順暢地進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="53f89-132">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="53f89-133">Azure 可讓您 tooadd 站對站 VPN 連線能力，此外 toopoint 對站連線能力 toohello 虛擬網路在 Azure 中建立。</span><span class="sxs-lookup"><span data-stu-id="53f89-133">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="53f89-134">設定 hello 站對站連線，請在 hello Azure 網路，只有 hello IP 位址範圍是不同 hello 內部 IP 位址範圍內，您可以路由傳送流量 toohello 在內部部署位置 （區域網路）。</span><span class="sxs-lookup"><span data-stu-id="53f89-134">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="53f89-135">這是因為 Azure 不支援延伸的子網路。</span><span class="sxs-lookup"><span data-stu-id="53f89-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="53f89-136">因此如果您有子網路 192.168.1.0/24 內部部署，您無法加入本機網路 192.168.1.0/24 hello Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="53f89-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="53f89-137">這是預期行為，因為 Azure 不知道 hello 的子網路中有沒有作用中的 Vm，並只災害復原正在建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="53f89-137">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="53f89-138">toobe toocorrectly 無法路由傳送網路流量超出 hello 網路和 hello 本機網路中的 Azure 網路 hello 子網路不得發生衝突。</span><span class="sxs-lookup"><span data-stu-id="53f89-138">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![子網路容錯移轉之前](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="53f89-140">容錯移轉之前</span><span class="sxs-lookup"><span data-stu-id="53f89-140">Before failover</span></span>

1. <span data-ttu-id="53f89-141">建立額外的網路 (例如「復原網路」)。</span><span class="sxs-lookup"><span data-stu-id="53f89-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="53f89-142">這是 hello 網路中的容錯移轉的 Vm 會建立。</span><span class="sxs-lookup"><span data-stu-id="53f89-142">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="53f89-143">容錯移轉之後，在 hello VM 屬性仍會保留 hello vm 的 IP 位址的 tooensure >**設定**，指定相同的 IP 位址 VM 內部，並按一下該 hello hello**儲存**。</span><span class="sxs-lookup"><span data-stu-id="53f89-143">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="53f89-144">當 hello VM 容錯移轉時，Azure Site Recovery 會指派提供 IP 位址 tooit hello。</span><span class="sxs-lookup"><span data-stu-id="53f89-144">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![網路屬性](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="53f89-146">容錯移轉觸發程序會觸發，並 hello Vm 在 Azure 中建立具有所需的 hello IP 位址之後，您可以連接 toohello 網路使用[Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="53f89-146">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="53f89-147">此動作可以編寫指令碼。</span><span class="sxs-lookup"><span data-stu-id="53f89-147">This action can be scripted.</span></span>
5. <span data-ttu-id="53f89-148">路由需要適當地修改，toobe tooreflect 該 192.168.1.0/24 現在已移 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="53f89-148">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![子網路容錯移轉之後](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="53f89-150">容錯移轉之後</span><span class="sxs-lookup"><span data-stu-id="53f89-150">After failover</span></span>

<span data-ttu-id="53f89-151">如果您還沒有如上所示的 Azure 網路，可以在容錯移轉之後，建立主要站台與 Azure 之間的站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="53f89-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="53f89-152">變更 IP 位址</span><span class="sxs-lookup"><span data-stu-id="53f89-152">Change IP addresses</span></span>

<span data-ttu-id="53f89-153">這[部落格文章](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)說明如何 tooset 向上 hello Azure 網路基礎結構時您不需要 tooretain IP 位址在容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="53f89-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="53f89-154">它會啟動應用程式描述、 查看如何 tooset 網路內部部署，以及在 Azure 中，並於結尾提供執行容錯移轉的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="53f89-154">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="53f89-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53f89-155">Next steps</span></span>

<span data-ttu-id="53f89-156">跳過[步驟 5： 準備 Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="53f89-156">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>
