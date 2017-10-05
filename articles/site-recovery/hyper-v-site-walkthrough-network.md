---
title: "使用 Azure Site Recovery 規劃 Hyper-V (不含 System Center VMM) 至 Azure 複寫的網路服務 | Microsoft Docs"
description: "本文討論將 Hyper-V VM (不含 VMM) 複寫至 Azure 時所需的網路規劃"
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
ms.openlocfilehash: 100b9d8a55c2c163e7a04680f0f7d7963315ee73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-plan-networking-for-hyper-v-to-azure-replication"></a><span data-ttu-id="9b84e-103">步驟 4：為 Hyper-V 至 Azure 複寫規劃網路服務</span><span class="sxs-lookup"><span data-stu-id="9b84e-103">Step 4: Plan networking for Hyper-V to Azure replication</span></span>

<span data-ttu-id="9b84e-104">本文摘要說明使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署 Hyper-V VM (不含 System Center VMM) 複寫至 Azure 時的網路規劃考量。</span><span class="sxs-lookup"><span data-stu-id="9b84e-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="9b84e-105">請在本文下方張貼意見，或在 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中提出問題。</span><span class="sxs-lookup"><span data-stu-id="9b84e-105">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-to-replica-vms-after-failover"></a><span data-ttu-id="9b84e-106">在容錯移轉之後連線到複本 VM</span><span class="sxs-lookup"><span data-stu-id="9b84e-106">Connecting to replica VMs after failover</span></span>

<span data-ttu-id="9b84e-107">規劃您的複寫和容錯移轉策略時，其中一項重要的問題，是如何在容錯移轉之後連線至 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="9b84e-107">When planning your replication and failover strategy, one of the key questions is how to connect to the Azure VM after failover.</span></span> <span data-ttu-id="9b84e-108">設計複本 Azure VM 的網路策略時，有兩種選擇：</span><span class="sxs-lookup"><span data-stu-id="9b84e-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="9b84e-109">**不同的 IP 位址**：您可以選取針對複寫的 Azure VM 網路使用不同的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="9b84e-109">**Different IP address**: You can select to use a different IP address range for the replicated Azure VM network.</span></span> <span data-ttu-id="9b84e-110">在此情節中，VM 會在容錯移轉之後取得新的 IP 位址，因此需要 DNS 更新。</span><span class="sxs-lookup"><span data-stu-id="9b84e-110">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="9b84e-111">深入了解</span><span class="sxs-lookup"><span data-stu-id="9b84e-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="9b84e-112">**相同的 IP 位址**：您可能會想要在容錯移轉之後，將與您主要內部部署網路中相同的 IP 位址範圍用於 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="9b84e-112">**Same IP address**: You might want to use the same IP address range as that in your primary on-premises network, for the Azure network after failover.</span></span>  <span data-ttu-id="9b84e-113">保留相同的 IP 位址可在容錯移轉之後減少網路相關問題，藉以簡化復原。</span><span class="sxs-lookup"><span data-stu-id="9b84e-113">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="9b84e-114">不過，當您複寫到 Azure 時，將需要在容錯移轉後，以新的 IP 位址位置更新路由。</span><span class="sxs-lookup"><span data-stu-id="9b84e-114">However, when you're replicating to Azure, you will need to update routes with the new location of the IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="9b84e-115">保留 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9b84e-115">Retain IP addresses</span></span>

<span data-ttu-id="9b84e-116">Site Recovery 提供可在容錯移轉至 Azure (藉由子網路容錯移轉) 時保留固定 IP 位址的功能。</span><span class="sxs-lookup"><span data-stu-id="9b84e-116">Site Recovery provides the capability to retain fixed IP addresses when failing over to Azure, with a subnet failover.</span></span>

<span data-ttu-id="9b84e-117">藉由子網路容錯移轉，特定的子網路會存在於站台 1 或站台 2 中，但絕不會同時存在於這兩個站台中。</span><span class="sxs-lookup"><span data-stu-id="9b84e-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="9b84e-118">為了在發生容錯移轉時維持 IP 位址空間，您需以程式設計方式為路由器基礎結構進行安排，將子網路從一個站台移到另一個站台。</span><span class="sxs-lookup"><span data-stu-id="9b84e-118">In order to maintain the IP address space in the event of a failover, you programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="9b84e-119">在容錯移轉期間，子網路會隨著關聯的受保護 VM 一起移動。</span><span class="sxs-lookup"><span data-stu-id="9b84e-119">During failover, the subnets move with the associated protected VMs.</span></span> <span data-ttu-id="9b84e-120">主要的缺點在於，當發生失敗時，您必須移動整個子網路。</span><span class="sxs-lookup"><span data-stu-id="9b84e-120">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="9b84e-121">容錯移轉範例</span><span class="sxs-lookup"><span data-stu-id="9b84e-121">Failover example</span></span>

<span data-ttu-id="9b84e-122">讓我們看看容錯移轉至 Azure 的範例。</span><span class="sxs-lookup"><span data-stu-id="9b84e-122">Let's look at an example for failover to Azure.</span></span>

- <span data-ttu-id="9b84e-123">Woodgrove Bank 是一家虛構的公司，擁有裝載其商務應用程式的內部部署基礎結構。</span><span class="sxs-lookup"><span data-stu-id="9b84e-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="9b84e-124">它們的行動應用程式裝載在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="9b84e-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="9b84e-125">Azure 中 Woodgrove Bank VM 與內部部署伺服器之間的連線，是由內部部署邊緣網路與 Azure 虛擬網路之間的站對站 (VPN) 連線所提供的。</span><span class="sxs-lookup"><span data-stu-id="9b84e-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between the on-premises edge network and the Azure virtual network.</span></span>
- <span data-ttu-id="9b84e-126">此 VPN 意謂著此公司在 Azure 中的虛擬網路會顯示為其內部部署網路的延伸。</span><span class="sxs-lookup"><span data-stu-id="9b84e-126">This VPN means that the company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="9b84e-127">Woodgrove 想要使用 Site Recovery 將內部部署工作負載複寫到 Azure。</span><span class="sxs-lookup"><span data-stu-id="9b84e-127">Woodgrove wants to use Site Recovery to replicate on-premises workloads to Azure.</span></span>
 - <span data-ttu-id="9b84e-128">Woodgrove 必須處理依存於硬式編碼 IP 位址的應用程式和組態，因此必須在容錯移轉至 Azure 之後，保留其應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9b84e-128">Woodgrove has to deal with applications and configurations which depend on hard-coded IP addresses, and thus need to retain IP addresses for their applications after failover to Azure.</span></span>
 - <span data-ttu-id="9b84e-129">Woodgrove 已將來自範圍 172.16.1.0/24、172.16.2.0/24 的 IP 位址指派給其在 Azure 中執行的資源。</span><span class="sxs-lookup"><span data-stu-id="9b84e-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 to its resources running in Azure.</span></span>


<span data-ttu-id="9b84e-130">Woodgrove 若要既能將其 VM 複寫至 Azure，同時又保留 IP 位址，就必須執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="9b84e-130">For Woodgrove to be able to replicate its VMs to Azure while retaining the IP addresses, here's what the company needs to do:</span></span>

1. <span data-ttu-id="9b84e-131">建立 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9b84e-131">Create an Azure virtual network.</span></span> <span data-ttu-id="9b84e-132">這應該為內部部署網路的延伸，以便讓應用程式可以順暢地容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="9b84e-132">It should be an extension of the on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="9b84e-133">除了點對站連線能力之外，Azure 還可讓您將站對站 VPN 連線能力新增到 Azure 中建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9b84e-133">Azure allows you to add site-to-site VPN connectivity, in addition to point-to-site connectivity to the virtual networks created in Azure.</span></span>
3. <span data-ttu-id="9b84e-134">當設定站對站連線時，在 Azure 網路中，只有當 IP 位址範圍不同於內部部署 IP 位址範圍時，您才能將流量路由傳送到內部部署位置 (本機網路)。</span><span class="sxs-lookup"><span data-stu-id="9b84e-134">When setting up the site-to-site connection, in the Azure network, you can route traffic to the on-premises location (local-network) only if the IP address range is different from the on-premises IP address range.</span></span>
    - <span data-ttu-id="9b84e-135">這是因為 Azure 不支援延伸的子網路。</span><span class="sxs-lookup"><span data-stu-id="9b84e-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="9b84e-136">因此，如果您的內部部署環境中有子網路 192.168.1.0/24，您便無法在 Azure 網路中新增本機網路 192.168.1.0/24。</span><span class="sxs-lookup"><span data-stu-id="9b84e-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in the Azure network.</span></span>
    - <span data-ttu-id="9b84e-137">這是預期行為，因為 Azure 並不知道子網路中沒有任何作用中的 VM，也不知道子網路是僅針對災害復原而建立的。</span><span class="sxs-lookup"><span data-stu-id="9b84e-137">This is expected because Azure doesn’t know that there are no active VMs in the subnet, and that the subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="9b84e-138">若要能夠從 Azure 網路正確地路由傳送網路流量，網路和本機網路中的子網路便不得發生衝突。</span><span class="sxs-lookup"><span data-stu-id="9b84e-138">To be able to correctly route network traffic out of an Azure network the subnets in the network and the local-network mustn't conflict.</span></span>

![子網路容錯移轉之前](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="9b84e-140">容錯移轉之前</span><span class="sxs-lookup"><span data-stu-id="9b84e-140">Before failover</span></span>

1. <span data-ttu-id="9b84e-141">建立額外的網路 (例如「復原網路」)。</span><span class="sxs-lookup"><span data-stu-id="9b84e-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="9b84e-142">這是要作為容錯移轉 VM 建立位置的網路。</span><span class="sxs-lookup"><span data-stu-id="9b84e-142">This is the network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="9b84e-143">為了確保在容錯移轉後會保留 VM 的 IP 位址，請在 VM 屬性 > [設定] 中，指定與 VM 在內部部署環境中所用相同的 IP 位址，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9b84e-143">To ensure that the IP address for a VM is retained after a failover, in the VM properties > **Configure**, specify the same IP address that the VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="9b84e-144">當 VM 容錯移轉時，Azure Site Recovery 會將提供的 IP 位址指派給它。</span><span class="sxs-lookup"><span data-stu-id="9b84e-144">When the VM is failed over, Azure Site Recovery will assign the provided IP address to it.</span></span>

    ![網路屬性](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="9b84e-146">容錯移轉觸發，並使用必要的 IP 位址在 Azure 中建立 VM 之後，您可以使用 [Vnet 對 Vnet 連線](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)來連線到網路。</span><span class="sxs-lookup"><span data-stu-id="9b84e-146">After failover is trigger is triggered, and the VMs are created in Azure with the required IP address, you can connect to the network using a [Vnet to Vnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="9b84e-147">此動作可以編寫指令碼。</span><span class="sxs-lookup"><span data-stu-id="9b84e-147">This action can be scripted.</span></span>
5. <span data-ttu-id="9b84e-148">路由需要經過適當地修改，以反映 192.168.1.0/24 現已移至 Azure。</span><span class="sxs-lookup"><span data-stu-id="9b84e-148">Routes need to be appropriately modified, to reflect that 192.168.1.0/24 has now moved to Azure.</span></span>

    ![子網路容錯移轉之後](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="9b84e-150">容錯移轉之後</span><span class="sxs-lookup"><span data-stu-id="9b84e-150">After failover</span></span>

<span data-ttu-id="9b84e-151">如果您還沒有如上所示的 Azure 網路，可以在容錯移轉之後，建立主要站台與 Azure 之間的站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="9b84e-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="9b84e-152">變更 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9b84e-152">Change IP addresses</span></span>

<span data-ttu-id="9b84e-153">這篇[部落格文章](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)說明當您不需要在容錯移轉之後保留 IP 位址時，如何設定 Azure 網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="9b84e-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how to set up the Azure networking infrastructure when you don't need to retain IP addresses after failover.</span></span> <span data-ttu-id="9b84e-154">它是以應用程式描述作為開頭、研究如何在內部部署環境及 Azure 中設定網路，然後以關於執行容錯移轉的資訊作為總結。</span><span class="sxs-lookup"><span data-stu-id="9b84e-154">It starts with an application description, looks at how to set up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="9b84e-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b84e-155">Next steps</span></span>

<span data-ttu-id="9b84e-156">移至[步驟 5：準備 Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="9b84e-156">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>
