---
title: "網路的實體伺服器複寫 tooAzure aaaPlan |Microsoft 文件"
description: "本文將討論 tooAzure 實體伺服器進行複寫時，需要網路規劃"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 71db2435-b5ce-4263-83f6-093d10d1d4e1
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e2ca2db2a1cb58ca5468d4ee2b0406f29ff09479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-physical-server-replication-tooazure"></a><span data-ttu-id="a9c51-103">步驟 4： 規劃實體伺服器複寫 tooAzure 的網路功能</span><span class="sxs-lookup"><span data-stu-id="a9c51-103">Step 4: Plan networking for physical server replication tooAzure</span></span>

<span data-ttu-id="a9c51-104">本文摘要說明網路規劃考量，當複寫在內部部署實體伺服器 tooAzure 使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="a9c51-104">This article summarizes network planning considerations when replicating on-premises physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="a9c51-105">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="a9c51-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connect-tooreplica-azure-vms"></a><span data-ttu-id="a9c51-106">連接 tooreplica Azure Vm</span><span class="sxs-lookup"><span data-stu-id="a9c51-106">Connect tooreplica Azure VMs</span></span>

<span data-ttu-id="a9c51-107">規劃您的複寫和容錯移轉策略 hello 重要的問題的其中一個時，如何在容錯移轉之後 tooconnect toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="a9c51-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="a9c51-108">設計複本 Azure VM 的網路策略時，有兩種選擇：</span><span class="sxs-lookup"><span data-stu-id="a9c51-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="a9c51-109">**使用不同的 IP 位址**： 您可以選取 toouse 不同的 IP 位址範圍的 hello 複寫 Azure VM 網路。</span><span class="sxs-lookup"><span data-stu-id="a9c51-109">**Use a different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="a9c51-110">在此案例中，hello 機器容錯移轉，以及 DNS 更新之後需要取得新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a9c51-110">In this scenario, hello machine gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="a9c51-111">**使用 hello 相同 IP 位址**： 您可能會想 toouse hello 相同的 IP 位址範圍，與您內部部署主要站台中，供 hello 容錯移轉後的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="a9c51-111">**Use hello same IP address**: You might want toouse hello same IP address range as that in your primary on-premises site, for hello Azure network after failover.</span></span> <span data-ttu-id="a9c51-112">可簡化相同的 IP 位址保持 hello hello 復原藉由減少容錯移轉之後網路相關的問題。</span><span class="sxs-lookup"><span data-stu-id="a9c51-112">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="a9c51-113">不過，當您要複寫 tooAzure，您必須 tooupdate hello 新位置的 hello IP 位址的路由在容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="a9c51-113">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span>

## <a name="retain-ip-addresses"></a><span data-ttu-id="a9c51-114">保留 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a9c51-114">Retain IP addresses</span></span>

<span data-ttu-id="a9c51-115">容錯移轉 tooAzure，具有子網路容錯移轉時，站台復原提供 hello 功能 tooretain 固定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a9c51-115">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>
<span data-ttu-id="a9c51-116">藉由子網路容錯移轉，特定的子網路會存在於站台 1 或站台 2 中，但絕不會同時存在於這兩個站台中。</span><span class="sxs-lookup"><span data-stu-id="a9c51-116">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="a9c51-117">順序 toomaintain hello IP 位址空間 hello 事件中的容錯移轉，在您以程式設計的方式排列 hello 路由器基礎結構 toomove hello 子網路從一個站台 tooanother。</span><span class="sxs-lookup"><span data-stu-id="a9c51-117">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="a9c51-118">容錯移轉期間，以 hello hello 子網路移動相關的受保護的 Vm。</span><span class="sxs-lookup"><span data-stu-id="a9c51-118">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="a9c51-119">hello 主要缺點是，在 hello 事件中的失敗，您必須 toomove hello 整個子網路。</span><span class="sxs-lookup"><span data-stu-id="a9c51-119">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>

### <a name="failover-example"></a><span data-ttu-id="a9c51-120">容錯移轉範例</span><span class="sxs-lookup"><span data-stu-id="a9c51-120">Failover example</span></span>

<span data-ttu-id="a9c51-121">讓我們看看 tooAzure 容錯移轉的範例。</span><span class="sxs-lookup"><span data-stu-id="a9c51-121">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="a9c51-122">Woodgrove Bank 是一家虛構的公司，擁有裝載其商務應用程式的內部部署基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a9c51-122">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="a9c51-123">它們的行動應用程式裝載在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="a9c51-123">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="a9c51-124">Woodgrove Bank Vm 在 Azure 和內部部署伺服器之間的連線是由站台對站台 (VPN) 連線 hello 在內部部署邊緣網路與 hello Azure 虛擬網路之間提供。</span><span class="sxs-lookup"><span data-stu-id="a9c51-124">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="a9c51-125">這個 hello 公司的 Azure 虛擬網路的 VPN 表示會顯示為其內部部署網路的延伸。</span><span class="sxs-lookup"><span data-stu-id="a9c51-125">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="a9c51-126">Woodgrove 想 toouse Site Recovery tooreplicate 內部工作負載 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a9c51-126">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="a9c51-127">Woodgrove 有 toodeal 應用程式與組態的硬式編碼的 IP 位址，而定，因此在容錯移轉 tooAzure 之後的應用程式需要 tooretain IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a9c51-127">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="a9c51-128">Woodgrove 已指派的 IP 位址範圍 172.16.1.0/24 從 172.16.2.0/24 tooits 資源在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="a9c51-128">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="a9c51-129">Woodgrove toobe 無法 tooreplicate 其伺服器 tooAzure 時保留 hello IP 位址，如以下是何種 hello 公司需要 toodo:</span><span class="sxs-lookup"><span data-stu-id="a9c51-129">For Woodgrove toobe able tooreplicate its servers tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="a9c51-130">建立 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="a9c51-130">Create an Azure virtual network.</span></span> <span data-ttu-id="a9c51-131">它應該 hello 的延伸模組為內部網路，使應用程式可以順暢地進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="a9c51-131">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="a9c51-132">Azure 可讓您 tooadd 站對站 VPN 連線能力，此外 toopoint 對站連線能力 toohello 虛擬網路在 Azure 中建立。</span><span class="sxs-lookup"><span data-stu-id="a9c51-132">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="a9c51-133">設定 hello 站對站連線，請在 hello Azure 網路，只有 hello IP 位址範圍是不同 hello 內部 IP 位址範圍內，您可以路由傳送流量 toohello 在內部部署位置 （區域網路）。</span><span class="sxs-lookup"><span data-stu-id="a9c51-133">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="a9c51-134">這是因為 Azure 不支援延伸的子網路。</span><span class="sxs-lookup"><span data-stu-id="a9c51-134">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="a9c51-135">因此如果您有子網路 192.168.1.0/24 內部部署，您無法加入本機網路 192.168.1.0/24 hello Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="a9c51-135">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="a9c51-136">這是預期行為，因為 Azure 不知道 hello 的子網路中沒有任何作用中的機器，並只災害復原正在建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="a9c51-136">This is expected because Azure doesn’t know that there are no active machines in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="a9c51-137">toobe toocorrectly 無法路由傳送網路流量超出 hello 網路和 hello 本機網路中的 Azure 網路 hello 子網路不得發生衝突。</span><span class="sxs-lookup"><span data-stu-id="a9c51-137">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![子網路容錯移轉之前](./media/physical-walkthrough-network/network-design7.png)

#### <a name="before-failover"></a><span data-ttu-id="a9c51-139">容錯移轉之前</span><span class="sxs-lookup"><span data-stu-id="a9c51-139">Before failover</span></span>

1. <span data-ttu-id="a9c51-140">建立額外的網路 (例如「復原網路」)。</span><span class="sxs-lookup"><span data-stu-id="a9c51-140">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="a9c51-141">這是 hello 網路中的容錯移轉的 Vm 會建立。</span><span class="sxs-lookup"><span data-stu-id="a9c51-141">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="a9c51-142">hello 機器的 IP 位址的 tooensure 會保留在容錯移轉之後，在 hello 機器內容 >**設定**，指定的 hello hello 伺服器的相同 IP 位址已在內部，，然後按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="a9c51-142">tooensure that hello IP address for a machine is retained after a failover, in hello machine properties > **Configure**, specify hello same IP address that hello server has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="a9c51-143">當 hello 機器容錯移轉時，Azure Site Recovery 會指派提供 IP 位址 tooit hello。</span><span class="sxs-lookup"><span data-stu-id="a9c51-143">When hello machine is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>
4. <span data-ttu-id="a9c51-144">容錯移轉觸發程序會觸發，並 hello Vm 在 Azure 中建立具有所需的 hello IP 位址之後，您可以連接 toohello 網路使用[Vnet tooVnet 連線](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="a9c51-144">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet connection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="a9c51-145">此動作可以編寫指令碼。</span><span class="sxs-lookup"><span data-stu-id="a9c51-145">This action can be scripted.</span></span>
5. <span data-ttu-id="a9c51-146">路由需要適當地修改，toobe tooreflect 該 192.168.1.0/24 現在已移 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a9c51-146">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![子網路容錯移轉之後](./media/physical-walkthrough-network/network-design9.png)

#### <a name="after-failover"></a><span data-ttu-id="a9c51-148">容錯移轉之後</span><span class="sxs-lookup"><span data-stu-id="a9c51-148">After failover</span></span>

<span data-ttu-id="a9c51-149">如果您沒有如以上所述的 Azure 網路，則可以在容錯移轉之後，在主要站台與 Azure 之間建立站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="a9c51-149">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failover.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="a9c51-150">變更 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a9c51-150">Change IP addresses</span></span>

<span data-ttu-id="a9c51-151">這[部落格文章](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)說明如何 tooset 向上 hello Azure 網路基礎結構時您不需要 tooretain IP 位址在容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="a9c51-151">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="a9c51-152">它會啟動應用程式描述、 查看如何 tooset 網路內部部署，以及在 Azure 中，並於結尾提供執行容錯移轉的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a9c51-152">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a9c51-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9c51-153">Next steps</span></span>

<span data-ttu-id="a9c51-154">跳過[步驟 5： 準備 Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="a9c51-154">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>
