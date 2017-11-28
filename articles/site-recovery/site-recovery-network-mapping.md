---
title: "HYPER-V 虛擬機器複寫與站台復原的 aaaPlan 網路對應 |Microsoft 文件"
description: "設定 HYPER-V 虛擬機器的複寫從內部部署資料中心 tooAzure 或 tooa 次要站台的網路對應。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a><span data-ttu-id="796d2-103">使用 Site Recovery 規劃 Hyper-V VM 複寫的網路對應</span><span class="sxs-lookup"><span data-stu-id="796d2-103">Plan network mapping for Hyper-V VM replication with Site Recovery</span></span>



<span data-ttu-id="796d2-104">這篇文章可協助您 toounderstand 和規劃的網路對應的 HYPER-V Vm tooAzure 或 tooa 次要站台的複寫期間，使用 hello [Azure Site Recovery 服務](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="796d2-104">This article helps you toounderstand and plan for network mapping during replication of Hyper-V VMs tooAzure, or tooa secondary site, using hello [Azure Site Recovery service](site-recovery-overview.md).</span></span>

<span data-ttu-id="796d2-105">在讀取後這份文件張貼在 hello 下方的本文中，任何註解或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="796d2-105">After reading this article post any comments at hello bottom of this article, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="network-mapping-for-replication-tooazure"></a><span data-ttu-id="796d2-106">複寫 tooAzure 網路對應</span><span class="sxs-lookup"><span data-stu-id="796d2-106">Network mapping for replication tooAzure</span></span>

<span data-ttu-id="796d2-107">當複寫 （在 VMM 中管理） 的 HYPER-V Vm tooAzure 時，會使用網路對應。</span><span class="sxs-lookup"><span data-stu-id="796d2-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) tooAzure.</span></span> <span data-ttu-id="796d2-108">網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-108">Network mapping maps between VM networks on a source VMM server, and target Azure networks.</span></span> <span data-ttu-id="796d2-109">對應未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="796d2-109">Mapping does hello following:</span></span>

- <span data-ttu-id="796d2-110">**網路連線**— 可確保複寫的 Azure Vm 連接的 toohello 對應的網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-110">**Network connection**—Ensures that replicated Azure VMs are connected toohello mapped network.</span></span> <span data-ttu-id="796d2-111">容錯移轉 hello 相同的所有機器網路可以連接 tooeach 其他，即使它們在不同的復原計劃中容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="796d2-111">All machines which fail over on hello same network can connect tooeach other, even if they failed over in different recovery plans.</span></span>
- <span data-ttu-id="796d2-112">**網路閘道**-Vm 網路閘道已設定 hello 目標 Azure 網路上，如果可以連線 tooother 在內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="796d2-112">**Network gateway**—If a network gateway is set up on hello target Azure network, VMs can connect tooother on-premises virtual machines.</span></span>

<span data-ttu-id="796d2-113">請注意：</span><span class="sxs-lookup"><span data-stu-id="796d2-113">Note that:</span></span>

- <span data-ttu-id="796d2-114">您將對應的來源 VMM VM 網路 tooan Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-114">You map a source VMM VM network tooan Azure virtual network.</span></span>
- <span data-ttu-id="796d2-115">在容錯移轉 Azure Vm 中 hello 之後來源網路就會連接的 toohello 對應的目標虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-115">After failover Azure VMs in hello source network will be connected toohello mapped target virtual network.</span></span>
- <span data-ttu-id="796d2-116">新的 Vm 加入 toohello 來源 VM 網路連線發生複寫時，toohello 對應 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-116">New VMs added toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
- <span data-ttu-id="796d2-117">如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器在容錯移轉之後連接 toothat 目標子網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-117">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
- <span data-ttu-id="796d2-118">如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器所連接 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-118">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a><span data-ttu-id="796d2-119">複寫 tooa 次要資料中心的網路對應</span><span class="sxs-lookup"><span data-stu-id="796d2-119">Network mapping for replication tooa secondary datacenter</span></span>

<span data-ttu-id="796d2-120">當複寫 (managed 在 System Center Virtual Machine Manager (VMM)) 的 HYPER-V Vm tooa 次要資料中心時，會使用網路對應。</span><span class="sxs-lookup"><span data-stu-id="796d2-120">Network mapping is used when replicating Hyper-V VMs (managed in System Center Virtual Machine Manager (VMM)) tooa secondary datacenter.</span></span> <span data-ttu-id="796d2-121">網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 VMM 伺服器上的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-121">Network mapping maps between VM networks on a source VMM server, and VM networks on a target VMM server.</span></span> <span data-ttu-id="796d2-122">對應未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="796d2-122">Mapping does hello following:</span></span>

- <span data-ttu-id="796d2-123">**網路連線**— 容錯移轉之後連接 Vm tooappropriate 網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-123">**Network connection**—Connects VMs tooappropriate networks after failover.</span></span> <span data-ttu-id="796d2-124">hello 複本 VM 將會是對應的 toohello 來源網路的連線的 toohello 目標網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-124">hello replica VM will be connected toohello target network that's mapped toohello source network.</span></span>
- <span data-ttu-id="796d2-125">**最佳的放置**— 數位 hello HYPER-V 主機伺服器上的複本 Vm 的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="796d2-125">**Optimal placement**—Optimally places hello replica VMs on Hyper-V host servers.</span></span> <span data-ttu-id="796d2-126">複本 Vm 會放置在主機上，可以存取 hello 對應 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-126">Replica VMs are placed on hosts that can access hello mapped VM networks.</span></span>
- <span data-ttu-id="796d2-127">**任何網路對應**— 如果您未設定網路對應，複本 Vm 容錯移轉之後將無法連接的 tooany VM 網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-127">**No network mapping**—If you don’t configure network mapping, replica VMs won’t be connected tooany VM networks after failover.</span></span>

<span data-ttu-id="796d2-128">請注意：</span><span class="sxs-lookup"><span data-stu-id="796d2-128">Note that:</span></span>

- <span data-ttu-id="796d2-129">網路對應可以設定兩部 VMM 伺服器上的 VM 網路之間或單一 VMM 伺服器上如果兩個站台由管理 hello 相同伺服器。</span><span class="sxs-lookup"><span data-stu-id="796d2-129">Network mapping can be configured between VM networks on two VMM servers, or on a single VMM server if two sites are managed by hello same server.</span></span>
- <span data-ttu-id="796d2-130">當正確設定對應和已啟用複寫，hello 主要位置的 VM 將會連接的 tooa 網路而它在 hello 目標位置的複本將會連接 tooits 對應網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-130">When mapping is configured correctly and replication is enabled, a VM at hello primary location will be connected tooa network, and its replica at hello target location will be connected tooits mapped network.</span></span>
-
- <span data-ttu-id="796d2-131">如果網路有已正確設定在 VMM 中，當您在網路對應期間選取目標 VM 網路時，使用 hello 來源 VM 網路的 hello VMM 來源雲端將會顯示，以及用於 hello 目標雲端上的 hello 可用目標 VM 網路保護。</span><span class="sxs-lookup"><span data-stu-id="796d2-131">If networks have been set up correctly in VMM, when you select a target VM network during network mapping, hello VMM source clouds that use hello source VM network will be displayed, along with hello available target VM networks on hello target clouds that are used for protection.</span></span>
- <span data-ttu-id="796d2-132">如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="796d2-132">If hello target network has multiple subnets and one of those subnets has hello same name as hello subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="796d2-133">如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-133">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



### <a name="example"></a><span data-ttu-id="796d2-134">範例</span><span class="sxs-lookup"><span data-stu-id="796d2-134">Example</span></span>

<span data-ttu-id="796d2-135">以下是範例 tooillustrate 這項機制。</span><span class="sxs-lookup"><span data-stu-id="796d2-135">Here’s an example tooillustrate this mechanism.</span></span> <span data-ttu-id="796d2-136">讓我們以具有兩個位置 (紐約和芝加哥) 的組織為例。</span><span class="sxs-lookup"><span data-stu-id="796d2-136">Let’s take an organization with two locations in New York and Chicago.</span></span>

<span data-ttu-id="796d2-137">**位置**</span><span class="sxs-lookup"><span data-stu-id="796d2-137">**Location**</span></span> | <span data-ttu-id="796d2-138">**VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="796d2-138">**VMM server**</span></span> | <span data-ttu-id="796d2-139">**VM 網路**</span><span class="sxs-lookup"><span data-stu-id="796d2-139">**VM networks**</span></span> | <span data-ttu-id="796d2-140">**對應至**</span><span class="sxs-lookup"><span data-stu-id="796d2-140">**Mapped to**</span></span>
---|---|---|---
<span data-ttu-id="796d2-141">紐約</span><span class="sxs-lookup"><span data-stu-id="796d2-141">New York</span></span> | <span data-ttu-id="796d2-142">VMM-NewYork</span><span class="sxs-lookup"><span data-stu-id="796d2-142">VMM-NewYork</span></span>| <span data-ttu-id="796d2-143">VMNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="796d2-143">VMNetwork1-NewYork</span></span> | <span data-ttu-id="796d2-144">對應的 tooVMNetwork1 芝加哥</span><span class="sxs-lookup"><span data-stu-id="796d2-144">Mapped tooVMNetwork1-Chicago</span></span>
 |  | <span data-ttu-id="796d2-145">VMNetwork2-NewYork</span><span class="sxs-lookup"><span data-stu-id="796d2-145">VMNetwork2-NewYork</span></span> | <span data-ttu-id="796d2-146">未對應</span><span class="sxs-lookup"><span data-stu-id="796d2-146">Not mapped</span></span>
<span data-ttu-id="796d2-147">芝加哥</span><span class="sxs-lookup"><span data-stu-id="796d2-147">Chicago</span></span> | <span data-ttu-id="796d2-148">VMM-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-148">VMM-Chicago</span></span>| <span data-ttu-id="796d2-149">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-149">VMNetwork1-Chicago</span></span> | <span data-ttu-id="796d2-150">對應的 tooVMNetwork1 紐約</span><span class="sxs-lookup"><span data-stu-id="796d2-150">Mapped tooVMNetwork1-NewYork</span></span>
 | | <span data-ttu-id="796d2-151">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-151">VMNetwork1-Chicago</span></span> | <span data-ttu-id="796d2-152">未對應</span><span class="sxs-lookup"><span data-stu-id="796d2-152">Not mapped</span></span>

<span data-ttu-id="796d2-153">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="796d2-153">In this example:</span></span>

- <span data-ttu-id="796d2-154">針對已連線的 tooVMNetwork1 紐約任何虛擬機器建立複本虛擬機器時，就會連接的 tooVMNetwork1 芝加哥。</span><span class="sxs-lookup"><span data-stu-id="796d2-154">When a replica virtual machine is created for any virtual machine that is connected tooVMNetwork1-NewYork, it will be connected tooVMNetwork1-Chicago.</span></span>
- <span data-ttu-id="796d2-155">VMNetwork2 紐約或 VMNetwork2 芝加哥建立複本虛擬機器時，它將無法連接的 tooany 網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-155">When a replica virtual machine is created for VMNetwork2-NewYork or VMNetwork2-Chicago, it will not be connected tooany network.</span></span>

<span data-ttu-id="796d2-156">以下是如何在我們的範例組織中，與 hello 與 hello 雲端相關聯的邏輯網路中設定 VMM 雲端。</span><span class="sxs-lookup"><span data-stu-id="796d2-156">Here's how VMM clouds are set up in our example organization, and hello logical networks associated with hello clouds.</span></span>

#### <a name="cloud-protection-settings"></a><span data-ttu-id="796d2-157">雲端保護設定</span><span class="sxs-lookup"><span data-stu-id="796d2-157">Cloud protection settings</span></span>

<span data-ttu-id="796d2-158">**受保護的雲端**</span><span class="sxs-lookup"><span data-stu-id="796d2-158">**Protected cloud**</span></span> | <span data-ttu-id="796d2-159">**保護雲端**</span><span class="sxs-lookup"><span data-stu-id="796d2-159">**Protecting cloud**</span></span> | <span data-ttu-id="796d2-160">**邏輯網路 (紐約)**</span><span class="sxs-lookup"><span data-stu-id="796d2-160">**Logical network (New York)**</span></span>  
---|---|---
<span data-ttu-id="796d2-161">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="796d2-161">GoldCloud1</span></span> | <span data-ttu-id="796d2-162">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="796d2-162">GoldCloud2</span></span> |
<span data-ttu-id="796d2-163">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="796d2-163">SilverCloud1</span></span>| <span data-ttu-id="796d2-164">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="796d2-164">SilverCloud2</span></span> |
<span data-ttu-id="796d2-165">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="796d2-165">GoldCloud2</span></span> | <p><span data-ttu-id="796d2-166">NA</span><span class="sxs-lookup"><span data-stu-id="796d2-166">NA</span></span></p><p></p> | <p><span data-ttu-id="796d2-167">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="796d2-167">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="796d2-168">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-168">LogicalNetwork1-Chicago</span></span></p>
<span data-ttu-id="796d2-169">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="796d2-169">SilverCloud2</span></span> | <p><span data-ttu-id="796d2-170">NA</span><span class="sxs-lookup"><span data-stu-id="796d2-170">NA</span></span></p><p></p> | <p><span data-ttu-id="796d2-171">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="796d2-171">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="796d2-172">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-172">LogicalNetwork1-Chicago</span></span></p>

#### <a name="logical-and-vm-network-settings"></a><span data-ttu-id="796d2-173">邏輯和 VM 網路設定</span><span class="sxs-lookup"><span data-stu-id="796d2-173">Logical and VM network settings</span></span>

<span data-ttu-id="796d2-174">**位置**</span><span class="sxs-lookup"><span data-stu-id="796d2-174">**Location**</span></span> | <span data-ttu-id="796d2-175">**邏輯網路**</span><span class="sxs-lookup"><span data-stu-id="796d2-175">**Logical network**</span></span> | <span data-ttu-id="796d2-176">**相關聯的 VM 網路**</span><span class="sxs-lookup"><span data-stu-id="796d2-176">**Associated VM network**</span></span>
---|---|---
<span data-ttu-id="796d2-177">紐約</span><span class="sxs-lookup"><span data-stu-id="796d2-177">New York</span></span> | <span data-ttu-id="796d2-178">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="796d2-178">LogicalNetwork1-NewYork</span></span> | <span data-ttu-id="796d2-179">VMNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="796d2-179">VMNetwork1-NewYork</span></span>
<span data-ttu-id="796d2-180">芝加哥</span><span class="sxs-lookup"><span data-stu-id="796d2-180">Chicago</span></span> | <span data-ttu-id="796d2-181">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-181">LogicalNetwork1-Chicago</span></span> | <span data-ttu-id="796d2-182">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-182">VMNetwork1-Chicago</span></span>
 | <span data-ttu-id="796d2-183">LogicalNetwork2Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-183">LogicalNetwork2Chicago</span></span> | <span data-ttu-id="796d2-184">VMNetwork2-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-184">VMNetwork2-Chicago</span></span>

#### <a name="target-network-settings"></a><span data-ttu-id="796d2-185">目標網路設定</span><span class="sxs-lookup"><span data-stu-id="796d2-185">Target network settings</span></span>

<span data-ttu-id="796d2-186">根據這些設定，當您選取 hello 目標 VM 網路，hello 下表顯示的 hello 選項可供使用。</span><span class="sxs-lookup"><span data-stu-id="796d2-186">Based on these settings, when you select hello target VM network, hello following table shows hello choices that will be available.</span></span>

<span data-ttu-id="796d2-187">**選取**</span><span class="sxs-lookup"><span data-stu-id="796d2-187">**Select**</span></span> | <span data-ttu-id="796d2-188">**受保護的雲端**</span><span class="sxs-lookup"><span data-stu-id="796d2-188">**Protected cloud**</span></span> | <span data-ttu-id="796d2-189">**保護雲端**</span><span class="sxs-lookup"><span data-stu-id="796d2-189">**Protecting cloud**</span></span> | <span data-ttu-id="796d2-190">**可用的目標網路**</span><span class="sxs-lookup"><span data-stu-id="796d2-190">**Target network available**</span></span>
---|---|---|---
<span data-ttu-id="796d2-191">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-191">VMNetwork1-Chicago</span></span> | <span data-ttu-id="796d2-192">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="796d2-192">SilverCloud1</span></span> | <span data-ttu-id="796d2-193">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="796d2-193">SilverCloud2</span></span> | <span data-ttu-id="796d2-194">可用</span><span class="sxs-lookup"><span data-stu-id="796d2-194">Available</span></span>
 | <span data-ttu-id="796d2-195">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="796d2-195">GoldCloud1</span></span> | <span data-ttu-id="796d2-196">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="796d2-196">GoldCloud2</span></span> | <span data-ttu-id="796d2-197">可用</span><span class="sxs-lookup"><span data-stu-id="796d2-197">Available</span></span>
<span data-ttu-id="796d2-198">VMNetwork2-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-198">VMNetwork2-Chicago</span></span> | <span data-ttu-id="796d2-199">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="796d2-199">SilverCloud1</span></span> | <span data-ttu-id="796d2-200">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="796d2-200">SilverCloud2</span></span> | <span data-ttu-id="796d2-201">尚未提供</span><span class="sxs-lookup"><span data-stu-id="796d2-201">Not available</span></span>
 | <span data-ttu-id="796d2-202">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="796d2-202">GoldCloud1</span></span> | <span data-ttu-id="796d2-203">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="796d2-203">GoldCloud2</span></span> | <span data-ttu-id="796d2-204">可用</span><span class="sxs-lookup"><span data-stu-id="796d2-204">Available</span></span>


<span data-ttu-id="796d2-205">如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="796d2-205">If hello target network has multiple subnets and one of those subnets has hello same name as hello subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="796d2-206">如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-206">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>


#### <a name="failback-behavior"></a><span data-ttu-id="796d2-207">容錯回復行為</span><span class="sxs-lookup"><span data-stu-id="796d2-207">Failback behavior</span></span>

<span data-ttu-id="796d2-208">toosee 怎樣 hello 案例容錯回復 （反向複寫），讓我們假設 VMNetwork1 紐約對應的 tooVMNetwork1-芝加哥，以下列設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="796d2-208">toosee what happens in hello case of failback (reverse replication), let’s assume that VMNetwork1-NewYork is mapped tooVMNetwork1-Chicago, with hello following settings.</span></span>


<span data-ttu-id="796d2-209">**虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="796d2-209">**Virtual machine**</span></span> | <span data-ttu-id="796d2-210">**連接的 tooVM 網路**</span><span class="sxs-lookup"><span data-stu-id="796d2-210">**Connected tooVM network**</span></span>
---|---
<span data-ttu-id="796d2-211">VM1</span><span class="sxs-lookup"><span data-stu-id="796d2-211">VM1</span></span> | <span data-ttu-id="796d2-212">VMNetwork1-Network</span><span class="sxs-lookup"><span data-stu-id="796d2-212">VMNetwork1-Network</span></span>
<span data-ttu-id="796d2-213">VM2 (VM1 的複本)</span><span class="sxs-lookup"><span data-stu-id="796d2-213">VM2 (replica of VM1)</span></span> | <span data-ttu-id="796d2-214">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="796d2-214">VMNetwork1-Chicago</span></span>

<span data-ttu-id="796d2-215">讓我們使用這些設定，檢閱幾個可能的案例中發生的情況。</span><span class="sxs-lookup"><span data-stu-id="796d2-215">With these settings, let's review what happens in a couple of possible scenarios.</span></span>

<span data-ttu-id="796d2-216">**案例**</span><span class="sxs-lookup"><span data-stu-id="796d2-216">**Scenario**</span></span> | <span data-ttu-id="796d2-217">**結果**</span><span class="sxs-lookup"><span data-stu-id="796d2-217">**Outcome**</span></span>
---|---
<span data-ttu-id="796d2-218">Vm-2 的容錯移轉之後的 hello 網路屬性沒有變更。</span><span class="sxs-lookup"><span data-stu-id="796d2-218">No change in hello network properties of VM-2 after failover.</span></span> | <span data-ttu-id="796d2-219">Vm-1 依然連接的 toohello 來源網路。</span><span class="sxs-lookup"><span data-stu-id="796d2-219">VM-1 remains connected toohello source network.</span></span>
<span data-ttu-id="796d2-220">在容錯移轉並中斷連線之後，VM-2 的網路屬性有所變更。</span><span class="sxs-lookup"><span data-stu-id="796d2-220">Network properties of VM-2 are changed after failover and is disconnected.</span></span> | <span data-ttu-id="796d2-221">VM-1 已中斷連線。</span><span class="sxs-lookup"><span data-stu-id="796d2-221">VM-1 is disconnected.</span></span>
<span data-ttu-id="796d2-222">Vm-2 的網路屬性會變更容錯移轉之後，並且已連線的 tooVMNetwork2 芝加哥。</span><span class="sxs-lookup"><span data-stu-id="796d2-222">Network properties of VM-2 are changed after failover and is connected tooVMNetwork2-Chicago.</span></span> | <span data-ttu-id="796d2-223">如果未對應 VMNetwork2-Chicago，將會中斷 VM-1 連線。</span><span class="sxs-lookup"><span data-stu-id="796d2-223">If VMNetwork2-Chicago isn’t mapped, VM-1 will be disconnected.</span></span>
<span data-ttu-id="796d2-224">VMNetwork1-Chicago 的網路對應已變更。</span><span class="sxs-lookup"><span data-stu-id="796d2-224">Network mapping of VMNetwork1-Chicago is changed.</span></span> | <span data-ttu-id="796d2-225">Vm-1 將會連接的 toohello 現在對應的網路 tooVMNetwork1 芝加哥。</span><span class="sxs-lookup"><span data-stu-id="796d2-225">VM-1 will be connected toohello network now mapped tooVMNetwork1-Chicago.</span></span>



## <a name="next-steps"></a><span data-ttu-id="796d2-226">後續步驟</span><span class="sxs-lookup"><span data-stu-id="796d2-226">Next steps</span></span>

<span data-ttu-id="796d2-227">深入了解[規劃 hello 網路基礎結構](site-recovery-network-design.md)。</span><span class="sxs-lookup"><span data-stu-id="796d2-227">Learn about [planning hello network infrastructure](site-recovery-network-design.md).</span></span>
