---
title: "HYPER-V 複寫 tooa 次要 VMM 站台與 Azure Site Recovery 的網路功能的 aaaPlan |Microsoft 文件"
description: "本文將討論網路時複寫 HYPER-V Vm tooa 次要 System Center VMM 站台與 Azure Site Recovery 的規劃。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a><span data-ttu-id="15fb7-103">步驟 3： 規劃 HYPER-V 虛擬機器複寫 tooa 次要 VMM 站台的網路功能</span><span class="sxs-lookup"><span data-stu-id="15fb7-103">Step 3: Plan networking for Hyper-V VM replication tooa secondary VMM site</span></span>

<span data-ttu-id="15fb7-104">檢閱部署必要條件，讀取網路複寫管理 System Center Virtual Machine Manager (VMM) 雲端中 HYPER-V 虛擬機器 (Vm) 時這個發行項 tooplan 之後 tooa 次要站台使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="15fb7-104">After reviewing deployment prerequisites, read this article tooplan networking when replicating Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary site using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> 

<span data-ttu-id="15fb7-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="15fb7-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="network-mapping-overview"></a><span data-ttu-id="15fb7-106">網路對應概觀</span><span class="sxs-lookup"><span data-stu-id="15fb7-106">Network mapping overview</span></span>

<span data-ttu-id="15fb7-107">當複寫 （在 VMM 中管理） 的 HYPER-V Vm tooa 次要資料中心時，會使用網路對應。</span><span class="sxs-lookup"><span data-stu-id="15fb7-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) tooa secondary datacenter.</span></span> <span data-ttu-id="15fb7-108">網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 VMM 伺服器上的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-108">Network mapping maps between VM networks on a source VMM server, and VM networks on a target VMM server.</span></span> <span data-ttu-id="15fb7-109">對應未 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="15fb7-109">Mapping does hello following:</span></span>

- <span data-ttu-id="15fb7-110">**網路連線**— 容錯移轉之後連接 Vm tooappropriate 網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-110">**Network connection**—Connects VMs tooappropriate networks after failover.</span></span> <span data-ttu-id="15fb7-111">hello 複本 VM 將會是對應的 toohello 來源網路的連線的 toohello 目標網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-111">hello replica VM will be connected toohello target network that's mapped toohello source network.</span></span>
- <span data-ttu-id="15fb7-112">**最佳的放置**— 數位 hello HYPER-V 主機伺服器上的複本 Vm 的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="15fb7-112">**Optimal placement**—Optimally places hello replica VMs on Hyper-V host servers.</span></span> <span data-ttu-id="15fb7-113">複本 Vm 會放置在主機上，可以存取 hello 對應 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-113">Replica VMs are placed on hosts that can access hello mapped VM networks.</span></span>
- <span data-ttu-id="15fb7-114">**任何網路對應**— 如果您未設定網路對應，複本 Vm 容錯移轉之後將無法連接的 tooany VM 網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-114">**No network mapping**—If you don’t configure network mapping, replica VMs won’t be connected tooany VM networks after failover.</span></span>


### <a name="example"></a><span data-ttu-id="15fb7-115">範例</span><span class="sxs-lookup"><span data-stu-id="15fb7-115">Example</span></span>

<span data-ttu-id="15fb7-116">以下是範例 tooillustrate 這項機制。</span><span class="sxs-lookup"><span data-stu-id="15fb7-116">Here’s an example tooillustrate this mechanism.</span></span> <span data-ttu-id="15fb7-117">讓我們以具有兩個位置 (紐約和芝加哥) 的組織為例。</span><span class="sxs-lookup"><span data-stu-id="15fb7-117">Let’s take an organization with two locations in New York and Chicago.</span></span>

<span data-ttu-id="15fb7-118">**位置**</span><span class="sxs-lookup"><span data-stu-id="15fb7-118">**Location**</span></span> | <span data-ttu-id="15fb7-119">**VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="15fb7-119">**VMM server**</span></span> | <span data-ttu-id="15fb7-120">**VM 網路**</span><span class="sxs-lookup"><span data-stu-id="15fb7-120">**VM networks**</span></span> | <span data-ttu-id="15fb7-121">**對應至**</span><span class="sxs-lookup"><span data-stu-id="15fb7-121">**Mapped to**</span></span>
---|---|---|---
<span data-ttu-id="15fb7-122">紐約</span><span class="sxs-lookup"><span data-stu-id="15fb7-122">New York</span></span> | <span data-ttu-id="15fb7-123">VMM-NewYork</span><span class="sxs-lookup"><span data-stu-id="15fb7-123">VMM-NewYork</span></span>| <span data-ttu-id="15fb7-124">VMNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="15fb7-124">VMNetwork1-NewYork</span></span> | <span data-ttu-id="15fb7-125">對應的 tooVMNetwork1 芝加哥</span><span class="sxs-lookup"><span data-stu-id="15fb7-125">Mapped tooVMNetwork1-Chicago</span></span>
 |  | <span data-ttu-id="15fb7-126">VMNetwork2-NewYork</span><span class="sxs-lookup"><span data-stu-id="15fb7-126">VMNetwork2-NewYork</span></span> | <span data-ttu-id="15fb7-127">未對應</span><span class="sxs-lookup"><span data-stu-id="15fb7-127">Not mapped</span></span>
<span data-ttu-id="15fb7-128">芝加哥</span><span class="sxs-lookup"><span data-stu-id="15fb7-128">Chicago</span></span> | <span data-ttu-id="15fb7-129">VMM-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-129">VMM-Chicago</span></span>| <span data-ttu-id="15fb7-130">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-130">VMNetwork1-Chicago</span></span> | <span data-ttu-id="15fb7-131">對應的 tooVMNetwork1 紐約</span><span class="sxs-lookup"><span data-stu-id="15fb7-131">Mapped tooVMNetwork1-NewYork</span></span>
 | | <span data-ttu-id="15fb7-132">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-132">VMNetwork1-Chicago</span></span> | <span data-ttu-id="15fb7-133">未對應</span><span class="sxs-lookup"><span data-stu-id="15fb7-133">Not mapped</span></span>

<span data-ttu-id="15fb7-134">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="15fb7-134">In this example:</span></span>

- <span data-ttu-id="15fb7-135">針對已連線的 tooVMNetwork1 紐約任何虛擬機器建立複本虛擬機器時，就會連接的 tooVMNetwork1 芝加哥。</span><span class="sxs-lookup"><span data-stu-id="15fb7-135">When a replica virtual machine is created for any virtual machine that is connected tooVMNetwork1-NewYork, it will be connected tooVMNetwork1-Chicago.</span></span>
- <span data-ttu-id="15fb7-136">VMNetwork2 紐約或 VMNetwork2 芝加哥建立複本虛擬機器時，它將無法連接的 tooany 網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-136">When a replica virtual machine is created for VMNetwork2-NewYork or VMNetwork2-Chicago, it will not be connected tooany network.</span></span>

<span data-ttu-id="15fb7-137">以下是如何在我們的範例組織中，與 hello 與 hello 雲端相關聯的邏輯網路中設定 VMM 雲端。</span><span class="sxs-lookup"><span data-stu-id="15fb7-137">Here's how VMM clouds are set up in our example organization, and hello logical networks associated with hello clouds.</span></span>

#### <a name="cloud-protection-settings"></a><span data-ttu-id="15fb7-138">雲端保護設定</span><span class="sxs-lookup"><span data-stu-id="15fb7-138">Cloud protection settings</span></span>

<span data-ttu-id="15fb7-139">**受保護的雲端**</span><span class="sxs-lookup"><span data-stu-id="15fb7-139">**Protected cloud**</span></span> | <span data-ttu-id="15fb7-140">**保護雲端**</span><span class="sxs-lookup"><span data-stu-id="15fb7-140">**Protecting cloud**</span></span> | <span data-ttu-id="15fb7-141">**邏輯網路 (紐約)**</span><span class="sxs-lookup"><span data-stu-id="15fb7-141">**Logical network (New York)**</span></span>  
---|---|---
<span data-ttu-id="15fb7-142">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="15fb7-142">GoldCloud1</span></span> | <span data-ttu-id="15fb7-143">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="15fb7-143">GoldCloud2</span></span> |
<span data-ttu-id="15fb7-144">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="15fb7-144">SilverCloud1</span></span>| <span data-ttu-id="15fb7-145">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="15fb7-145">SilverCloud2</span></span> |
<span data-ttu-id="15fb7-146">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="15fb7-146">GoldCloud2</span></span> | <p><span data-ttu-id="15fb7-147">NA</span><span class="sxs-lookup"><span data-stu-id="15fb7-147">NA</span></span></p><p></p> | <p><span data-ttu-id="15fb7-148">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="15fb7-148">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="15fb7-149">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-149">LogicalNetwork1-Chicago</span></span></p>
<span data-ttu-id="15fb7-150">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="15fb7-150">SilverCloud2</span></span> | <p><span data-ttu-id="15fb7-151">NA</span><span class="sxs-lookup"><span data-stu-id="15fb7-151">NA</span></span></p><p></p> | <p><span data-ttu-id="15fb7-152">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="15fb7-152">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="15fb7-153">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-153">LogicalNetwork1-Chicago</span></span></p>

#### <a name="logical-and-vm-network-settings"></a><span data-ttu-id="15fb7-154">邏輯和 VM 網路設定</span><span class="sxs-lookup"><span data-stu-id="15fb7-154">Logical and VM network settings</span></span>

<span data-ttu-id="15fb7-155">**位置**</span><span class="sxs-lookup"><span data-stu-id="15fb7-155">**Location**</span></span> | <span data-ttu-id="15fb7-156">**邏輯網路**</span><span class="sxs-lookup"><span data-stu-id="15fb7-156">**Logical network**</span></span> | <span data-ttu-id="15fb7-157">**相關聯的 VM 網路**</span><span class="sxs-lookup"><span data-stu-id="15fb7-157">**Associated VM network**</span></span>
---|---|---
<span data-ttu-id="15fb7-158">紐約</span><span class="sxs-lookup"><span data-stu-id="15fb7-158">New York</span></span> | <span data-ttu-id="15fb7-159">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="15fb7-159">LogicalNetwork1-NewYork</span></span> | <span data-ttu-id="15fb7-160">VMNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="15fb7-160">VMNetwork1-NewYork</span></span>
<span data-ttu-id="15fb7-161">芝加哥</span><span class="sxs-lookup"><span data-stu-id="15fb7-161">Chicago</span></span> | <span data-ttu-id="15fb7-162">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-162">LogicalNetwork1-Chicago</span></span> | <span data-ttu-id="15fb7-163">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-163">VMNetwork1-Chicago</span></span>
 | <span data-ttu-id="15fb7-164">LogicalNetwork2Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-164">LogicalNetwork2Chicago</span></span> | <span data-ttu-id="15fb7-165">VMNetwork2-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-165">VMNetwork2-Chicago</span></span>

#### <a name="target-network-settings"></a><span data-ttu-id="15fb7-166">目標網路設定</span><span class="sxs-lookup"><span data-stu-id="15fb7-166">Target network settings</span></span>

<span data-ttu-id="15fb7-167">根據這些設定，當您選取 hello 目標 VM 網路，hello 下表顯示的 hello 選項可供使用。</span><span class="sxs-lookup"><span data-stu-id="15fb7-167">Based on these settings, when you select hello target VM network, hello following table shows hello choices that will be available.</span></span>

<span data-ttu-id="15fb7-168">**選取**</span><span class="sxs-lookup"><span data-stu-id="15fb7-168">**Select**</span></span> | <span data-ttu-id="15fb7-169">**受保護的雲端**</span><span class="sxs-lookup"><span data-stu-id="15fb7-169">**Protected cloud**</span></span> | <span data-ttu-id="15fb7-170">**保護雲端**</span><span class="sxs-lookup"><span data-stu-id="15fb7-170">**Protecting cloud**</span></span> | <span data-ttu-id="15fb7-171">**可用的目標網路**</span><span class="sxs-lookup"><span data-stu-id="15fb7-171">**Target network available**</span></span>
---|---|---|---
<span data-ttu-id="15fb7-172">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-172">VMNetwork1-Chicago</span></span> | <span data-ttu-id="15fb7-173">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="15fb7-173">SilverCloud1</span></span> | <span data-ttu-id="15fb7-174">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="15fb7-174">SilverCloud2</span></span> | <span data-ttu-id="15fb7-175">可用</span><span class="sxs-lookup"><span data-stu-id="15fb7-175">Available</span></span>
 | <span data-ttu-id="15fb7-176">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="15fb7-176">GoldCloud1</span></span> | <span data-ttu-id="15fb7-177">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="15fb7-177">GoldCloud2</span></span> | <span data-ttu-id="15fb7-178">可用</span><span class="sxs-lookup"><span data-stu-id="15fb7-178">Available</span></span>
<span data-ttu-id="15fb7-179">VMNetwork2-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-179">VMNetwork2-Chicago</span></span> | <span data-ttu-id="15fb7-180">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="15fb7-180">SilverCloud1</span></span> | <span data-ttu-id="15fb7-181">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="15fb7-181">SilverCloud2</span></span> | <span data-ttu-id="15fb7-182">尚未提供</span><span class="sxs-lookup"><span data-stu-id="15fb7-182">Not available</span></span>
 | <span data-ttu-id="15fb7-183">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="15fb7-183">GoldCloud1</span></span> | <span data-ttu-id="15fb7-184">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="15fb7-184">GoldCloud2</span></span> | <span data-ttu-id="15fb7-185">可用</span><span class="sxs-lookup"><span data-stu-id="15fb7-185">Available</span></span>


<span data-ttu-id="15fb7-186">如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="15fb7-186">If hello target network has multiple subnets and one of those subnets has hello same name as hello subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="15fb7-187">如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-187">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>


#### <a name="failback-behavior"></a><span data-ttu-id="15fb7-188">容錯回復行為</span><span class="sxs-lookup"><span data-stu-id="15fb7-188">Failback behavior</span></span>

<span data-ttu-id="15fb7-189">toosee 怎樣 hello 案例容錯回復 （反向複寫），讓我們假設 VMNetwork1 紐約對應的 tooVMNetwork1-芝加哥，以下列設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="15fb7-189">toosee what happens in hello case of failback (reverse replication), let’s assume that VMNetwork1-NewYork is mapped tooVMNetwork1-Chicago, with hello following settings.</span></span>


<span data-ttu-id="15fb7-190">**虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="15fb7-190">**Virtual machine**</span></span> | <span data-ttu-id="15fb7-191">**連接的 tooVM 網路**</span><span class="sxs-lookup"><span data-stu-id="15fb7-191">**Connected tooVM network**</span></span>
---|---
<span data-ttu-id="15fb7-192">VM1</span><span class="sxs-lookup"><span data-stu-id="15fb7-192">VM1</span></span> | <span data-ttu-id="15fb7-193">VMNetwork1-Network</span><span class="sxs-lookup"><span data-stu-id="15fb7-193">VMNetwork1-Network</span></span>
<span data-ttu-id="15fb7-194">VM2 (VM1 的複本)</span><span class="sxs-lookup"><span data-stu-id="15fb7-194">VM2 (replica of VM1)</span></span> | <span data-ttu-id="15fb7-195">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="15fb7-195">VMNetwork1-Chicago</span></span>

<span data-ttu-id="15fb7-196">讓我們使用這些設定，檢閱幾個可能的案例中發生的情況。</span><span class="sxs-lookup"><span data-stu-id="15fb7-196">With these settings, let's review what happens in a couple of possible scenarios.</span></span>

<span data-ttu-id="15fb7-197">**案例**</span><span class="sxs-lookup"><span data-stu-id="15fb7-197">**Scenario**</span></span> | <span data-ttu-id="15fb7-198">**結果**</span><span class="sxs-lookup"><span data-stu-id="15fb7-198">**Outcome**</span></span>
---|---
<span data-ttu-id="15fb7-199">Vm-2 的容錯移轉之後的 hello 網路屬性沒有變更。</span><span class="sxs-lookup"><span data-stu-id="15fb7-199">No change in hello network properties of VM-2 after failover.</span></span> | <span data-ttu-id="15fb7-200">Vm-1 依然連接的 toohello 來源網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-200">VM-1 remains connected toohello source network.</span></span>
<span data-ttu-id="15fb7-201">在容錯移轉並中斷連線之後，VM-2 的網路屬性有所變更。</span><span class="sxs-lookup"><span data-stu-id="15fb7-201">Network properties of VM-2 are changed after failover and is disconnected.</span></span> | <span data-ttu-id="15fb7-202">VM-1 已中斷連線。</span><span class="sxs-lookup"><span data-stu-id="15fb7-202">VM-1 is disconnected.</span></span>
<span data-ttu-id="15fb7-203">Vm-2 的網路屬性會變更容錯移轉之後，並且已連線的 tooVMNetwork2 芝加哥。</span><span class="sxs-lookup"><span data-stu-id="15fb7-203">Network properties of VM-2 are changed after failover and is connected tooVMNetwork2-Chicago.</span></span> | <span data-ttu-id="15fb7-204">如果未對應 VMNetwork2-Chicago，將會中斷 VM-1 連線。</span><span class="sxs-lookup"><span data-stu-id="15fb7-204">If VMNetwork2-Chicago isn’t mapped, VM-1 will be disconnected.</span></span>
<span data-ttu-id="15fb7-205">VMNetwork1-Chicago 的網路對應已變更。</span><span class="sxs-lookup"><span data-stu-id="15fb7-205">Network mapping of VMNetwork1-Chicago is changed.</span></span> | <span data-ttu-id="15fb7-206">Vm-1 將會連接的 toohello 現在對應的網路 tooVMNetwork1 芝加哥。</span><span class="sxs-lookup"><span data-stu-id="15fb7-206">VM-1 will be connected toohello network now mapped tooVMNetwork1-Chicago.</span></span>



## <a name="prepare-for-network-mapping"></a><span data-ttu-id="15fb7-207">準備網路對應</span><span class="sxs-lookup"><span data-stu-id="15fb7-207">Prepare for network mapping</span></span>

1. <span data-ttu-id="15fb7-208">Hello 來源和目標 VMM 伺服器上，您應該與 hello 來源與目標雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-208">On hello source and target VMM servers, you should have a logical network associated with hello source and target clouds.</span></span> 
2. <span data-ttu-id="15fb7-209">Hello 來源和目標伺服器，您必須具備的 VM 網路連結的 toohello 邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-209">In hello source and target servers, you should have a VM network linked toohello logical network.</span></span>
3. <span data-ttu-id="15fb7-210">在 hello 來源位置中的 HYPER-V 主機上的 Vm 應該連結的 toohello 來源 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-210">VMs on Hyper-V hosts in hello source location should be linked toohello source VM network.</span></span> <span data-ttu-id="15fb7-211">如果您只使用單一 VMM 伺服器，您可以設定之間的對應 hello 上的 VM 網路相同伺服器。</span><span class="sxs-lookup"><span data-stu-id="15fb7-211">If you're only using a single VMM server, you can configure mapping between VM networks on hello same server.</span></span>

<span data-ttu-id="15fb7-212">在 Site Recovery 部署期間設定網路對應時，會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="15fb7-212">Here's what happens when you set up network mapping during Site Recovery deployment:</span></span>

- <span data-ttu-id="15fb7-213">當您設定網路對應，並選取目標 VM 網路時，使用 hello 來源 VM 網路的 hello VMM 來源雲端將會顯示，以及在 hello 目標雲端上的 hello 可用目標 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-213">When you set up network mapping and select a target VM network, hello VMM source clouds that use hello source VM network will be displayed, along with hello available target VM networks on hello target clouds.</span></span>
- - <span data-ttu-id="15fb7-214">當對應已正確設定和啟用複寫時，來源 VM 將會連接的 tooits 來源 VM 網路，而它在 hello 目標位置的複本將會連接 tooits 對應 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-214">When mapping is configured correctly and replication is enabled, a source VM will be connected tooits source VM network, and its replica at hello target location will be connected tooits mapped VM network.</span></span>
- <span data-ttu-id="15fb7-215">如果 hello 目標網路有多個子網路，且其中一個子網路具有相同的名稱為 hello 子網路的 hello 來源虛擬機器所在，然後 hello 的 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="15fb7-215">If hello target network has multiple subnets, and one of those subnets has hello same name as hello subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="15fb7-216">如果不沒有具有相符名稱的任何目標子網路，hello VM 將會連接的 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-216">If there’s no target subnet with a matching name, hello VM will be connected toohello first subnet in hello network.</span></span>

## <a name="connect-toovms-after-failover"></a><span data-ttu-id="15fb7-217">容錯移轉之後連接 tooVMs</span><span class="sxs-lookup"><span data-stu-id="15fb7-217">Connect tooVMs after failover</span></span>

<span data-ttu-id="15fb7-218">規劃您的複寫和容錯移轉策略 hello 重要的問題的其中一個時，如何在容錯移轉之後 tooconnect toohello 複本。</span><span class="sxs-lookup"><span data-stu-id="15fb7-218">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello replica after failover.</span></span> <span data-ttu-id="15fb7-219">其中有幾個選項：</span><span class="sxs-lookup"><span data-stu-id="15fb7-219">There are a couple of choices:</span></span> 

- <span data-ttu-id="15fb7-220">**使用不同的 IP 位址**： 您可以選取 toouse 不同的 IP 位址的 hello 複寫 VM。</span><span class="sxs-lookup"><span data-stu-id="15fb7-220">**Use a different IP address**: You can select toouse a different IP address for hello replicated VM.</span></span> <span data-ttu-id="15fb7-221">在此案例 hello VM 容錯移轉之後，取得新的 IP 位址，DNS 更新為必要項。</span><span class="sxs-lookup"><span data-stu-id="15fb7-221">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="15fb7-222">**保留相同的 IP 位址的 hello**： 您可能會想 toouse hello hello 複本 VM 相同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15fb7-222">**Retain hello same IP address**: You might want toouse hello same IP address for hello replica VM.</span></span> <span data-ttu-id="15fb7-223">可簡化相同的 IP 位址保持 hello hello 復原藉由減少容錯移轉之後網路相關的問題。</span><span class="sxs-lookup"><span data-stu-id="15fb7-223">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> 

## <a name="retain-ip-addresses"></a><span data-ttu-id="15fb7-224">保留 IP 位址</span><span class="sxs-lookup"><span data-stu-id="15fb7-224">Retain IP addresses</span></span>

<span data-ttu-id="15fb7-225">如果您想 tooretain hello IP 位址從 hello 主要站台容錯移轉 toohello 次要站台之後，您可以執行完整的子網路容錯移轉，，並更新 hello IP 位址的路由 tooindicate hello 新位置或替代方案部署的延展的子網路之間 hello主要和 hello 復原站台。</span><span class="sxs-lookup"><span data-stu-id="15fb7-225">If you want tooretain hello IP addresses from hello primary site after failover toohello secondary site, you can do a full subnet failover, and update routes tooindicate hello new location of hello IP addresses, or alternative deploy a stretched subnet between hello primary and hello recovery sites.</span></span>

### <a name="stretched-subnet"></a><span data-ttu-id="15fb7-226">延伸的子網路</span><span class="sxs-lookup"><span data-stu-id="15fb7-226">Stretched subnet</span></span>

<span data-ttu-id="15fb7-227">在延展的子網路，hello 子網路，同時在 hello 主要和次要站台。</span><span class="sxs-lookup"><span data-stu-id="15fb7-227">In a stretched subnet, hello subnet is available simultaneously in both hello primary and secondary site.</span></span> <span data-ttu-id="15fb7-228">如果您移動伺服器和其 IP (第 3 層) 組態 toohello 次要站台，hello 網路就會自動路由 hello 流量 toohello 新位置。</span><span class="sxs-lookup"><span data-stu-id="15fb7-228">If you move a server and its IP (Layer 3) configuration toohello secondary site, hello network will route hello traffic toohello new location automatically.</span></span> 

<span data-ttu-id="15fb7-229">從第 2 層 (資料連結層) 的觀點而言，您需要可以管理延伸的 VLAN 的網路設備。</span><span class="sxs-lookup"><span data-stu-id="15fb7-229">From a Layer 2 (data link layer) perspective, you need networking equipment that can manage a stretched VLAN.</span></span> <span data-ttu-id="15fb7-230">此外，由延伸 hello VLAN，hello 潛在容錯網域延伸 tooboth 站台，基本上成為單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="15fb7-230">In addition, by stretching hello VLAN, hello potential fault domain extends tooboth sites, essentially becoming a single point of failure.</span></span> <span data-ttu-id="15fb7-231">雖然機率不高，但有可能發生廣播風暴，而且無法隔離。</span><span class="sxs-lookup"><span data-stu-id="15fb7-231">While this is an unlikely, it could happen that a broadcast storm started and cannot be isolated.</span></span> 


### <a name="subnet-failover"></a><span data-ttu-id="15fb7-232">子網路容錯移轉</span><span class="sxs-lookup"><span data-stu-id="15fb7-232">Subnet failover</span></span>

<span data-ttu-id="15fb7-233">您可以執行的子網路容錯移轉 tooobtain hello hello 延展的子網路的優點，而不實際自動縮放。</span><span class="sxs-lookup"><span data-stu-id="15fb7-233">You can run a subnet failover tooobtain hello benefits of hello stretched subnet, without actually stretching it.</span></span> <span data-ttu-id="15fb7-234">在此解決方案中，子網路將可在 hello 來源或目標站台中，但不是能在兩者同時。</span><span class="sxs-lookup"><span data-stu-id="15fb7-234">In this solution, a subnet will be available in hello source or target site, but not at both simultaneously.</span></span> <span data-ttu-id="15fb7-235">toomaintain hello IP 位址空間 hello 事件中的容錯移轉，您可以透過程式設計方式排列 hello 路由器基礎結構 toomove hello 子網路從一個站台 tooanother。</span><span class="sxs-lookup"><span data-stu-id="15fb7-235">toomaintain hello IP address space in hello event of a failover, you can programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="15fb7-236">子網路容錯移轉發生時，都會隨之移動後 hello 相關聯的 Vm。</span><span class="sxs-lookup"><span data-stu-id="15fb7-236">After when failover occurs, subnets would move with hello associated VMs.</span></span> <span data-ttu-id="15fb7-237">hello 主要缺點是，在 hello 事件中的失敗，您必須 toomove hello 整個子網路。</span><span class="sxs-lookup"><span data-stu-id="15fb7-237">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>

### <a name="example"></a><span data-ttu-id="15fb7-238">範例</span><span class="sxs-lookup"><span data-stu-id="15fb7-238">Example</span></span>

<span data-ttu-id="15fb7-239">以下是完整的子網路容錯移轉範例。</span><span class="sxs-lookup"><span data-stu-id="15fb7-239">Here's an example of complete subnet failover.</span></span> <span data-ttu-id="15fb7-240">hello 主要站台的子網路 192.168.1.0/24 中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="15fb7-240">hello primary site has applications running in subnet 192.168.1.0/24.</span></span> <span data-ttu-id="15fb7-241">在容錯移轉時，此子網路中的所有 hello Vm 已容錯移轉 toohello 次要站台，而會保留其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15fb7-241">At failover, all hello VMs in this subnet are failed over toohello secondary site, and retain their IP addresses.</span></span> <span data-ttu-id="15fb7-242">路由需要 toobe 修改 tooreflect hello 事實的所有 hello VM 虛擬機器屬於 toosubnet 192.168.1.0/24 現在已經都移動 toohello 次要站台。</span><span class="sxs-lookup"><span data-stu-id="15fb7-242">Routes need toobe modified tooreflect hello fact that all hello VM virtual machines belonging toosubnet 192.168.1.0/24 have now moved toohello secondary site.</span></span>

<span data-ttu-id="15fb7-243">hello 下列圖形顯示 hello 子網路容錯移轉的前後：</span><span class="sxs-lookup"><span data-stu-id="15fb7-243">hello following graphics show hello subnets before and after failover:</span></span>

- <span data-ttu-id="15fb7-244">容錯移轉之前，子網路 192.168.0.1/24 而作用於 hello 來源站台，成為作用中 hello 次要站台容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="15fb7-244">Before failover, subnet 192.168.0.1/24 is active on hello source site, become active on hello secondary site after failover.</span></span>
- <span data-ttu-id="15fb7-245">主要站台和復原站台、 第三個網站和主要站台之間路由傳送的 hello，而第三個網站和復原站台 toobe 適當修改。</span><span class="sxs-lookup"><span data-stu-id="15fb7-245">hello routes between primary site and recovery site, third site and primary site, and third site and recovery site will have toobe appropriately modified.</span></span>

<span data-ttu-id="15fb7-246">**容錯移轉之前**</span><span class="sxs-lookup"><span data-stu-id="15fb7-246">**Before failover**</span></span>

![容錯移轉之前](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

<span data-ttu-id="15fb7-248">**容錯移轉之後**</span><span class="sxs-lookup"><span data-stu-id="15fb7-248">**After failover**</span></span>

![容錯移轉之後](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

<span data-ttu-id="15fb7-250">容錯移轉之後，會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="15fb7-250">After failover, here's what happens:</span></span>

- <span data-ttu-id="15fb7-251">Site Recovery 從 hello 靜態 IP 位址集區 hello 相關網路，每個 VMM 執行個體中每個網路介面上 hello VM，配置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15fb7-251">Site Recovery allocates an IP address for each network interface on hello VM, from hello static IP address pool in hello relevant network, for each VMM instance.</span></span>
- <span data-ttu-id="15fb7-252">如果 hello IP 位址集區中 hello 次要站台是相同的 hello 來源站台，站台復原上配置的 hello hello 相同的 IP 位址 （hello 來源 VM） toohello 複本 VM。</span><span class="sxs-lookup"><span data-stu-id="15fb7-252">If hello IP address pool in hello secondary site is hello same as that on hello source site, Site Recovery allocates hello same IP address (of hello source VM) toohello replica VM.</span></span> <span data-ttu-id="15fb7-253">hello IP 位址已保留在 VMM 中，但未設定為 hello 容錯移轉 IP 位址 hello HYPER-V 主機上。</span><span class="sxs-lookup"><span data-stu-id="15fb7-253">hello IP address is reserved in VMM, but it isn't set as hello failover IP address on hello Hyper-V host.</span></span> <span data-ttu-id="15fb7-254">hello 容錯移轉 IP 位址的 hyper-v 主機上設定之前 hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="15fb7-254">hello failover IP address on a Hyper-v host is set just before hello failover.</span></span>
- <span data-ttu-id="15fb7-255">如果 hello 相同的 IP 位址無法使用，Site Recovery 會從 hello 集區配置另一個可用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15fb7-255">If hello same IP address isn't available, Site Recovery allocates another available IP address from hello pool.</span></span>
- <span data-ttu-id="15fb7-256">如果 Vm 使用 DHCP，Site Recovery 並不管理 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15fb7-256">If VMs use DHCP, Site Recovery doesn't manage hello IP addresses.</span></span> <span data-ttu-id="15fb7-257">您需要 hello DHCP 的 toocheck hello 次要站台上的伺服器可以從 hello 做 hello 來源站台相同的範圍配置位址。</span><span class="sxs-lookup"><span data-stu-id="15fb7-257">You need toocheck that hello DHCP server on hello secondary site can allocate address from hello same range as hello source site.</span></span>

### <a name="validate-hello-ip-address"></a><span data-ttu-id="15fb7-258">驗證 hello IP 位址</span><span class="sxs-lookup"><span data-stu-id="15fb7-258">Validate hello IP address</span></span>

<span data-ttu-id="15fb7-259">啟用 vm 保護之後，您可以使用下列範例指令碼 tooverify hello 指派位址 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="15fb7-259">After you enable protection for a VM, you can use following sample script tooverify hello address assigned toohello VM.</span></span> <span data-ttu-id="15fb7-260">相同的 IP 位址會設定為 hello 容錯移轉 IP 位址，並在 hello 容錯移轉期間指派 toohello VM hello:</span><span class="sxs-lookup"><span data-stu-id="15fb7-260">hello same IP address will be set as hello failover IP address, and assigned toohello VM at hello time of failover:</span></span>

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a><span data-ttu-id="15fb7-261">變更 IP 位址</span><span class="sxs-lookup"><span data-stu-id="15fb7-261">Changing IP addresses</span></span>

<span data-ttu-id="15fb7-262">在此案例中，會變更 hello 的容錯移轉的 Vm 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15fb7-262">In this scenario, hello IP addresses of VMs that fail over are changed.</span></span> <span data-ttu-id="15fb7-263">此解決方案的 hello 缺點是需要 hello 維護動作。</span><span class="sxs-lookup"><span data-stu-id="15fb7-263">hello drawback of this solution is hello maintenance required.</span></span> <span data-ttu-id="15fb7-264">通常在複本 VM 啟動後會更新 DNS。</span><span class="sxs-lookup"><span data-stu-id="15fb7-264">Typically, DNS will be updated after replica VMs start.</span></span> <span data-ttu-id="15fb7-265">DNS 項目，可能需要變更 toobe 或 fluster thenetwork 和更新的快取項目中。</span><span class="sxs-lookup"><span data-stu-id="15fb7-265">DNS entries might need toobe changed or fluster in thenetwork, and cached entries updated.</span></span> <span data-ttu-id="15fb7-266">這可能會導致停機時間。</span><span class="sxs-lookup"><span data-stu-id="15fb7-266">This can result in downtime.</span></span> <span data-ttu-id="15fb7-267">透過下列方式可以避免停機時間：</span><span class="sxs-lookup"><span data-stu-id="15fb7-267">Downtime can be mitigated as follows:</span></span>

- <span data-ttu-id="15fb7-268">對內部網路應用程式使用低 TTL 值。</span><span class="sxs-lookup"><span data-stu-id="15fb7-268">Use low TTL values for intranet applications.</span></span>
- <span data-ttu-id="15fb7-269">使用下列指令碼的站台復原復原方案，tooupdate hello DNS 伺服器 tooensure 及時更新中的 hello。</span><span class="sxs-lookup"><span data-stu-id="15fb7-269">Use hello following script in a Site Recovery recovery plan, tooupdate hello DNS server tooensure a timely update.</span></span> <span data-ttu-id="15fb7-270">如果您使用動態 DNS 登錄，您不需要 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="15fb7-270">You don't need hello script if you use dynamic DNS registration.</span></span>

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a><span data-ttu-id="15fb7-271">範例</span><span class="sxs-lookup"><span data-stu-id="15fb7-271">Example</span></span> 

<span data-ttu-id="15fb7-272">讓我們看看計劃跨 hello 主要 toouse 不同 IP 位址和 hello 復原站台的案例。在此範例中有不同的 IP 位址在主要和次要站台之間，而且那里; s 協力廠商網站，從 hello 主要或復原站台上裝載的應用程式可以存取。</span><span class="sxs-lookup"><span data-stu-id="15fb7-272">Let's look at a scenario in which you're planning toouse different IP addresses across hello primary and hello recovery sites.In this example we have different IP addresses across primary and secondary sites, and there;s a third site from which applications hosted on hello primary or recovery site can be accessed.</span></span>

- <span data-ttu-id="15fb7-273">容錯移轉之前，應用程式是託管的子網路 192.168.1.0/24 hello 主要站台上，設定在 hello 次要站台上的子網路 172.16.1.0/24 toobe 容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="15fb7-273">Before failover, apps are hosted subnet 192.168.1.0/24 on hello primary site, and are configured toobe in subnet 172.16.1.0/24 on hello secondary site after a failover.</span></span>
- <span data-ttu-id="15fb7-274">已適當地設定 VPN 連線/網路路由，讓所有的三個站台可以互相存取。</span><span class="sxs-lookup"><span data-stu-id="15fb7-274">VPN connections/network routes have been configured appropriately so that all three sites can access each other.</span></span>
- <span data-ttu-id="15fb7-275">容錯移轉之後，應用程式將會還原 hello 復原子網路中。</span><span class="sxs-lookup"><span data-stu-id="15fb7-275">After failover, apps will be restored in hello recovery subnet.</span></span> <span data-ttu-id="15fb7-276">在此案例中有任何需要 toofail 透過 hello 整個子網路，且不不需要的 tooreconfigure VPN 或網路路由的任何變更。</span><span class="sxs-lookup"><span data-stu-id="15fb7-276">In this scenario there's no need toofail over hello entire subnet, and no changes are needed tooreconfigure VPN or network routes.</span></span> <span data-ttu-id="15fb7-277">hello 容錯移轉和某些 DNS 更新，請確定應用程式仍然可以存取。</span><span class="sxs-lookup"><span data-stu-id="15fb7-277">hello failover, and some DNS updates, ensure that applications remain accessible.</span></span>
- <span data-ttu-id="15fb7-278">若 DNS 設定的 tooallow 動態更新，然後 hello Vm 會自行註冊方式容錯移轉後啟動時使用 hello 新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15fb7-278">If DNS is configured tooallow dynamic updates, then hello VMs will register themselves using hello new IP address, when they start after failover.</span></span>

<span data-ttu-id="15fb7-279">**容錯移轉之前**</span><span class="sxs-lookup"><span data-stu-id="15fb7-279">**Before failover**</span></span>

![不同的 IP - 容錯移轉之前](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

<span data-ttu-id="15fb7-281">**容錯移轉之後**</span><span class="sxs-lookup"><span data-stu-id="15fb7-281">**After failover**</span></span>

![不同的 IP - 容錯移轉之後](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a><span data-ttu-id="15fb7-283">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15fb7-283">Next steps</span></span>

<span data-ttu-id="15fb7-284">跳過[步驟 4： 準備 VMM 和 HYPER-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md)。</span><span class="sxs-lookup"><span data-stu-id="15fb7-284">Go too[Step 4: Prepare VMM and Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>


