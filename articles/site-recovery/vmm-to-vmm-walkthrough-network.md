---
title: "規劃使用 Azure Site Recovery 將 Hyper-V 複寫至次要 VMM 站台的網路服務 | Microsoft Docs"
description: "本文討論使用 Azure Site Recovery 將 Hyper-V VM 複寫至次要的 System Center VMM 站台的網路服務規劃。"
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
ms.openlocfilehash: a1f3f6e6cba074647195e2b0cbcdc7b4f3dec475
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-to-a-secondary-vmm-site"></a><span data-ttu-id="b42f5-103">步驟 3：規劃將 Hyper-V VM 複寫至次要 VMM 站台的網路服務</span><span class="sxs-lookup"><span data-stu-id="b42f5-103">Step 3: Plan networking for Hyper-V VM replication to a secondary VMM site</span></span>

<span data-ttu-id="b42f5-104">檢閱部署的必要條件後，請閱讀本文以規劃在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 將 System Center Virtual Machine Manager (VMM) 雲端中管理的 Hyper-V 虛擬機器 (VM) 複寫至次要站台的網路服務。</span><span class="sxs-lookup"><span data-stu-id="b42f5-104">After reviewing deployment prerequisites, read this article to plan networking when replicating Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary site using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> 

<span data-ttu-id="b42f5-105">在閱讀本文之後，請在下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中張貼任何意見。</span><span class="sxs-lookup"><span data-stu-id="b42f5-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="network-mapping-overview"></a><span data-ttu-id="b42f5-106">網路對應概觀</span><span class="sxs-lookup"><span data-stu-id="b42f5-106">Network mapping overview</span></span>

<span data-ttu-id="b42f5-107">將 Hyper-V VM (在 VMM 中管理) 複寫到次要資料中心時，將使用網路對應。</span><span class="sxs-lookup"><span data-stu-id="b42f5-107">Network mapping is used when replicating Hyper-V VMs (managed in VMM) to a secondary datacenter.</span></span> <span data-ttu-id="b42f5-108">網路對應會對應來源 VMM 伺服器上的 VM 網路與目標 VMM 伺服器上的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-108">Network mapping maps between VM networks on a source VMM server, and VM networks on a target VMM server.</span></span> <span data-ttu-id="b42f5-109">對應具有下列功能：</span><span class="sxs-lookup"><span data-stu-id="b42f5-109">Mapping does the following:</span></span>

- <span data-ttu-id="b42f5-110">**網路連線**—在容錯移轉之後，將 VM 連線至適當的網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-110">**Network connection**—Connects VMs to appropriate networks after failover.</span></span> <span data-ttu-id="b42f5-111">複本 VM 將會連線至對應到來源網路的目標網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-111">The replica VM will be connected to the target network that's mapped to the source network.</span></span>
- <span data-ttu-id="b42f5-112">**最佳放置**—以最佳方式將複本 VM 放置在 Hyper-V 主機伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b42f5-112">**Optimal placement**—Optimally places the replica VMs on Hyper-V host servers.</span></span> <span data-ttu-id="b42f5-113">複本 VM 會放在可以存取對應的 VM 網路的主機上。</span><span class="sxs-lookup"><span data-stu-id="b42f5-113">Replica VMs are placed on hosts that can access the mapped VM networks.</span></span>
- <span data-ttu-id="b42f5-114">**無網路對應**— 如果您沒有設定網路對應，複本 VM 將不會在容錯移轉後連線至 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-114">**No network mapping**—If you don’t configure network mapping, replica VMs won’t be connected to any VM networks after failover.</span></span>


### <a name="example"></a><span data-ttu-id="b42f5-115">範例</span><span class="sxs-lookup"><span data-stu-id="b42f5-115">Example</span></span>

<span data-ttu-id="b42f5-116">以下是說明這項機制的範例。</span><span class="sxs-lookup"><span data-stu-id="b42f5-116">Here’s an example to illustrate this mechanism.</span></span> <span data-ttu-id="b42f5-117">讓我們以具有兩個位置 (紐約和芝加哥) 的組織為例。</span><span class="sxs-lookup"><span data-stu-id="b42f5-117">Let’s take an organization with two locations in New York and Chicago.</span></span>

<span data-ttu-id="b42f5-118">**位置**</span><span class="sxs-lookup"><span data-stu-id="b42f5-118">**Location**</span></span> | <span data-ttu-id="b42f5-119">**VMM 伺服器**</span><span class="sxs-lookup"><span data-stu-id="b42f5-119">**VMM server**</span></span> | <span data-ttu-id="b42f5-120">**VM 網路**</span><span class="sxs-lookup"><span data-stu-id="b42f5-120">**VM networks**</span></span> | <span data-ttu-id="b42f5-121">**對應至**</span><span class="sxs-lookup"><span data-stu-id="b42f5-121">**Mapped to**</span></span>
---|---|---|---
<span data-ttu-id="b42f5-122">紐約</span><span class="sxs-lookup"><span data-stu-id="b42f5-122">New York</span></span> | <span data-ttu-id="b42f5-123">VMM-NewYork</span><span class="sxs-lookup"><span data-stu-id="b42f5-123">VMM-NewYork</span></span>| <span data-ttu-id="b42f5-124">VMNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="b42f5-124">VMNetwork1-NewYork</span></span> | <span data-ttu-id="b42f5-125">對應至 VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-125">Mapped to VMNetwork1-Chicago</span></span>
 |  | <span data-ttu-id="b42f5-126">VMNetwork2-NewYork</span><span class="sxs-lookup"><span data-stu-id="b42f5-126">VMNetwork2-NewYork</span></span> | <span data-ttu-id="b42f5-127">未對應</span><span class="sxs-lookup"><span data-stu-id="b42f5-127">Not mapped</span></span>
<span data-ttu-id="b42f5-128">芝加哥</span><span class="sxs-lookup"><span data-stu-id="b42f5-128">Chicago</span></span> | <span data-ttu-id="b42f5-129">VMM-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-129">VMM-Chicago</span></span>| <span data-ttu-id="b42f5-130">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-130">VMNetwork1-Chicago</span></span> | <span data-ttu-id="b42f5-131">對應至 VMNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="b42f5-131">Mapped to VMNetwork1-NewYork</span></span>
 | | <span data-ttu-id="b42f5-132">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-132">VMNetwork1-Chicago</span></span> | <span data-ttu-id="b42f5-133">未對應</span><span class="sxs-lookup"><span data-stu-id="b42f5-133">Not mapped</span></span>

<span data-ttu-id="b42f5-134">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="b42f5-134">In this example:</span></span>

- <span data-ttu-id="b42f5-135">為連線至 VMNetwork1-NewYork 的任何虛擬機器建立複本虛擬機器時，它將會連線至 VMNetwork1-Chicago。</span><span class="sxs-lookup"><span data-stu-id="b42f5-135">When a replica virtual machine is created for any virtual machine that is connected to VMNetwork1-NewYork, it will be connected to VMNetwork1-Chicago.</span></span>
- <span data-ttu-id="b42f5-136">為 VMNetwork2-NewYork 或 VMNetwork2-Chicago 建立複本虛擬機器時，它將不會連線至任何網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-136">When a replica virtual machine is created for VMNetwork2-NewYork or VMNetwork2-Chicago, it will not be connected to any network.</span></span>

<span data-ttu-id="b42f5-137">以下是如何在我們的範例組織中設定 VMM 雲端，以及與雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-137">Here's how VMM clouds are set up in our example organization, and the logical networks associated with the clouds.</span></span>

#### <a name="cloud-protection-settings"></a><span data-ttu-id="b42f5-138">雲端保護設定</span><span class="sxs-lookup"><span data-stu-id="b42f5-138">Cloud protection settings</span></span>

<span data-ttu-id="b42f5-139">**受保護的雲端**</span><span class="sxs-lookup"><span data-stu-id="b42f5-139">**Protected cloud**</span></span> | <span data-ttu-id="b42f5-140">**保護雲端**</span><span class="sxs-lookup"><span data-stu-id="b42f5-140">**Protecting cloud**</span></span> | <span data-ttu-id="b42f5-141">**邏輯網路 (紐約)**</span><span class="sxs-lookup"><span data-stu-id="b42f5-141">**Logical network (New York)**</span></span>  
---|---|---
<span data-ttu-id="b42f5-142">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="b42f5-142">GoldCloud1</span></span> | <span data-ttu-id="b42f5-143">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="b42f5-143">GoldCloud2</span></span> |
<span data-ttu-id="b42f5-144">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="b42f5-144">SilverCloud1</span></span>| <span data-ttu-id="b42f5-145">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="b42f5-145">SilverCloud2</span></span> |
<span data-ttu-id="b42f5-146">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="b42f5-146">GoldCloud2</span></span> | <p><span data-ttu-id="b42f5-147">NA</span><span class="sxs-lookup"><span data-stu-id="b42f5-147">NA</span></span></p><p></p> | <p><span data-ttu-id="b42f5-148">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="b42f5-148">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="b42f5-149">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-149">LogicalNetwork1-Chicago</span></span></p>
<span data-ttu-id="b42f5-150">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="b42f5-150">SilverCloud2</span></span> | <p><span data-ttu-id="b42f5-151">NA</span><span class="sxs-lookup"><span data-stu-id="b42f5-151">NA</span></span></p><p></p> | <p><span data-ttu-id="b42f5-152">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="b42f5-152">LogicalNetwork1-NewYork</span></span></p><p><span data-ttu-id="b42f5-153">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-153">LogicalNetwork1-Chicago</span></span></p>

#### <a name="logical-and-vm-network-settings"></a><span data-ttu-id="b42f5-154">邏輯和 VM 網路設定</span><span class="sxs-lookup"><span data-stu-id="b42f5-154">Logical and VM network settings</span></span>

<span data-ttu-id="b42f5-155">**位置**</span><span class="sxs-lookup"><span data-stu-id="b42f5-155">**Location**</span></span> | <span data-ttu-id="b42f5-156">**邏輯網路**</span><span class="sxs-lookup"><span data-stu-id="b42f5-156">**Logical network**</span></span> | <span data-ttu-id="b42f5-157">**相關聯的 VM 網路**</span><span class="sxs-lookup"><span data-stu-id="b42f5-157">**Associated VM network**</span></span>
---|---|---
<span data-ttu-id="b42f5-158">紐約</span><span class="sxs-lookup"><span data-stu-id="b42f5-158">New York</span></span> | <span data-ttu-id="b42f5-159">LogicalNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="b42f5-159">LogicalNetwork1-NewYork</span></span> | <span data-ttu-id="b42f5-160">VMNetwork1-NewYork</span><span class="sxs-lookup"><span data-stu-id="b42f5-160">VMNetwork1-NewYork</span></span>
<span data-ttu-id="b42f5-161">芝加哥</span><span class="sxs-lookup"><span data-stu-id="b42f5-161">Chicago</span></span> | <span data-ttu-id="b42f5-162">LogicalNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-162">LogicalNetwork1-Chicago</span></span> | <span data-ttu-id="b42f5-163">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-163">VMNetwork1-Chicago</span></span>
 | <span data-ttu-id="b42f5-164">LogicalNetwork2Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-164">LogicalNetwork2Chicago</span></span> | <span data-ttu-id="b42f5-165">VMNetwork2-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-165">VMNetwork2-Chicago</span></span>

#### <a name="target-network-settings"></a><span data-ttu-id="b42f5-166">目標網路設定</span><span class="sxs-lookup"><span data-stu-id="b42f5-166">Target network settings</span></span>

<span data-ttu-id="b42f5-167">根據這些設定，當您選取目標 VM 網路時，下表會顯示可用的選擇。</span><span class="sxs-lookup"><span data-stu-id="b42f5-167">Based on these settings, when you select the target VM network, the following table shows the choices that will be available.</span></span>

<span data-ttu-id="b42f5-168">**選取**</span><span class="sxs-lookup"><span data-stu-id="b42f5-168">**Select**</span></span> | <span data-ttu-id="b42f5-169">**受保護的雲端**</span><span class="sxs-lookup"><span data-stu-id="b42f5-169">**Protected cloud**</span></span> | <span data-ttu-id="b42f5-170">**保護雲端**</span><span class="sxs-lookup"><span data-stu-id="b42f5-170">**Protecting cloud**</span></span> | <span data-ttu-id="b42f5-171">**可用的目標網路**</span><span class="sxs-lookup"><span data-stu-id="b42f5-171">**Target network available**</span></span>
---|---|---|---
<span data-ttu-id="b42f5-172">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-172">VMNetwork1-Chicago</span></span> | <span data-ttu-id="b42f5-173">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="b42f5-173">SilverCloud1</span></span> | <span data-ttu-id="b42f5-174">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="b42f5-174">SilverCloud2</span></span> | <span data-ttu-id="b42f5-175">可用</span><span class="sxs-lookup"><span data-stu-id="b42f5-175">Available</span></span>
 | <span data-ttu-id="b42f5-176">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="b42f5-176">GoldCloud1</span></span> | <span data-ttu-id="b42f5-177">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="b42f5-177">GoldCloud2</span></span> | <span data-ttu-id="b42f5-178">可用</span><span class="sxs-lookup"><span data-stu-id="b42f5-178">Available</span></span>
<span data-ttu-id="b42f5-179">VMNetwork2-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-179">VMNetwork2-Chicago</span></span> | <span data-ttu-id="b42f5-180">SilverCloud1</span><span class="sxs-lookup"><span data-stu-id="b42f5-180">SilverCloud1</span></span> | <span data-ttu-id="b42f5-181">SilverCloud2</span><span class="sxs-lookup"><span data-stu-id="b42f5-181">SilverCloud2</span></span> | <span data-ttu-id="b42f5-182">尚未提供</span><span class="sxs-lookup"><span data-stu-id="b42f5-182">Not available</span></span>
 | <span data-ttu-id="b42f5-183">GoldCloud1</span><span class="sxs-lookup"><span data-stu-id="b42f5-183">GoldCloud1</span></span> | <span data-ttu-id="b42f5-184">GoldCloud2</span><span class="sxs-lookup"><span data-stu-id="b42f5-184">GoldCloud2</span></span> | <span data-ttu-id="b42f5-185">可用</span><span class="sxs-lookup"><span data-stu-id="b42f5-185">Available</span></span>


<span data-ttu-id="b42f5-186">如果目標網路具有多個子網路，且其中一個子網路的名稱和來源虛擬機器所在的子網路名稱相同，則複本虛擬機器將會在容錯移轉之後連線到該目標子網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-186">If the target network has multiple subnets and one of those subnets has the same name as the subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="b42f5-187">如果沒有目標子網路具有相符的名稱，虛擬機器將會連線到網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-187">If there’s no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>


#### <a name="failback-behavior"></a><span data-ttu-id="b42f5-188">容錯回復行為</span><span class="sxs-lookup"><span data-stu-id="b42f5-188">Failback behavior</span></span>

<span data-ttu-id="b42f5-189">若要了解容錯回復 (反向複寫) 時發生的狀況，讓我們假設 VMNetwork1-NewYork 對應到 VMNetwork1-Chicago，並包含下列設定。</span><span class="sxs-lookup"><span data-stu-id="b42f5-189">To see what happens in the case of failback (reverse replication), let’s assume that VMNetwork1-NewYork is mapped to VMNetwork1-Chicago, with the following settings.</span></span>


<span data-ttu-id="b42f5-190">**虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="b42f5-190">**Virtual machine**</span></span> | <span data-ttu-id="b42f5-191">**已連線至 VM 網路**</span><span class="sxs-lookup"><span data-stu-id="b42f5-191">**Connected to VM network**</span></span>
---|---
<span data-ttu-id="b42f5-192">VM1</span><span class="sxs-lookup"><span data-stu-id="b42f5-192">VM1</span></span> | <span data-ttu-id="b42f5-193">VMNetwork1-Network</span><span class="sxs-lookup"><span data-stu-id="b42f5-193">VMNetwork1-Network</span></span>
<span data-ttu-id="b42f5-194">VM2 (VM1 的複本)</span><span class="sxs-lookup"><span data-stu-id="b42f5-194">VM2 (replica of VM1)</span></span> | <span data-ttu-id="b42f5-195">VMNetwork1-Chicago</span><span class="sxs-lookup"><span data-stu-id="b42f5-195">VMNetwork1-Chicago</span></span>

<span data-ttu-id="b42f5-196">讓我們使用這些設定，檢閱幾個可能的案例中發生的情況。</span><span class="sxs-lookup"><span data-stu-id="b42f5-196">With these settings, let's review what happens in a couple of possible scenarios.</span></span>

<span data-ttu-id="b42f5-197">**案例**</span><span class="sxs-lookup"><span data-stu-id="b42f5-197">**Scenario**</span></span> | <span data-ttu-id="b42f5-198">**結果**</span><span class="sxs-lookup"><span data-stu-id="b42f5-198">**Outcome**</span></span>
---|---
<span data-ttu-id="b42f5-199">在容錯移轉之後，VM-2 的網路屬性沒有變更。</span><span class="sxs-lookup"><span data-stu-id="b42f5-199">No change in the network properties of VM-2 after failover.</span></span> | <span data-ttu-id="b42f5-200">VM 1 仍然連線至來源網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-200">VM-1 remains connected to the source network.</span></span>
<span data-ttu-id="b42f5-201">在容錯移轉並中斷連線之後，VM-2 的網路屬性有所變更。</span><span class="sxs-lookup"><span data-stu-id="b42f5-201">Network properties of VM-2 are changed after failover and is disconnected.</span></span> | <span data-ttu-id="b42f5-202">VM-1 已中斷連線。</span><span class="sxs-lookup"><span data-stu-id="b42f5-202">VM-1 is disconnected.</span></span>
<span data-ttu-id="b42f5-203">在容錯移轉並連線至 VMNetwork2-Chicago 之後，VM-2 的網路屬性有所變更。</span><span class="sxs-lookup"><span data-stu-id="b42f5-203">Network properties of VM-2 are changed after failover and is connected to VMNetwork2-Chicago.</span></span> | <span data-ttu-id="b42f5-204">如果未對應 VMNetwork2-Chicago，將會中斷 VM-1 連線。</span><span class="sxs-lookup"><span data-stu-id="b42f5-204">If VMNetwork2-Chicago isn’t mapped, VM-1 will be disconnected.</span></span>
<span data-ttu-id="b42f5-205">VMNetwork1-Chicago 的網路對應已變更。</span><span class="sxs-lookup"><span data-stu-id="b42f5-205">Network mapping of VMNetwork1-Chicago is changed.</span></span> | <span data-ttu-id="b42f5-206">VM-1 現在會連線到對應至 VMNetwork1-Chicago 的網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-206">VM-1 will be connected to the network now mapped to VMNetwork1-Chicago.</span></span>



## <a name="prepare-for-network-mapping"></a><span data-ttu-id="b42f5-207">準備網路對應</span><span class="sxs-lookup"><span data-stu-id="b42f5-207">Prepare for network mapping</span></span>

1. <span data-ttu-id="b42f5-208">在來源和目標 VMM 伺服器上，應具備與來源和目標雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-208">On the source and target VMM servers, you should have a logical network associated with the source and target clouds.</span></span> 
2. <span data-ttu-id="b42f5-209">在來源和目標伺服器上，應具備連結至邏輯網路的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-209">In the source and target servers, you should have a VM network linked to the logical network.</span></span>
3. <span data-ttu-id="b42f5-210">來源位置中 Hyper-V 主機上的 VM 應連結至來源 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-210">VMs on Hyper-V hosts in the source location should be linked to the source VM network.</span></span> <span data-ttu-id="b42f5-211">如果您只有單一 VMM 伺服器，則可以在同一部伺服器上的 VM 網路之間設定對應。</span><span class="sxs-lookup"><span data-stu-id="b42f5-211">If you're only using a single VMM server, you can configure mapping between VM networks on the same server.</span></span>

<span data-ttu-id="b42f5-212">在 Site Recovery 部署期間設定網路對應時，會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="b42f5-212">Here's what happens when you set up network mapping during Site Recovery deployment:</span></span>

- <span data-ttu-id="b42f5-213">當您設定網路對應並選取目標 VM 網路後，將會顯示使用來源 VM 網路的 VMM 來源雲端，以及目標雲端上可用的目標 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-213">When you set up network mapping and select a target VM network, the VMM source clouds that use the source VM network will be displayed, along with the available target VM networks on the target clouds.</span></span>
- - <span data-ttu-id="b42f5-214">正確設定對應並啟用複寫後，來源 VM 將連接至其來源 VM 網路，且其位於目標位置的複本將連接至其對應的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-214">When mapping is configured correctly and replication is enabled, a source VM will be connected to its source VM network, and its replica at the target location will be connected to its mapped VM network.</span></span>
- <span data-ttu-id="b42f5-215">如果目標網路具有多個子網路，且其中一個子網路的名稱和來源虛擬機器所在的子網路名稱相同，則複本虛擬機器將會在容錯移轉之後連線到該目標子網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-215">If the target network has multiple subnets, and one of those subnets has the same name as the subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="b42f5-216">如果沒有名稱相符的目標子網路，VM 將會連線到網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-216">If there’s no target subnet with a matching name, the VM will be connected to the first subnet in the network.</span></span>

## <a name="connect-to-vms-after-failover"></a><span data-ttu-id="b42f5-217">容錯移轉後連線到 VM</span><span class="sxs-lookup"><span data-stu-id="b42f5-217">Connect to VMs after failover</span></span>

<span data-ttu-id="b42f5-218">規劃您的複寫和容錯移轉策略時，其中一個重要的問題，就是如何在容錯移轉之後連線至複本。</span><span class="sxs-lookup"><span data-stu-id="b42f5-218">When planning your replication and failover strategy, one of the key questions is how to connect to the replica after failover.</span></span> <span data-ttu-id="b42f5-219">其中有幾個選項：</span><span class="sxs-lookup"><span data-stu-id="b42f5-219">There are a couple of choices:</span></span> 

- <span data-ttu-id="b42f5-220">**使用不同的 IP 位址**：您可以選擇讓複寫的 VM 使用不同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b42f5-220">**Use a different IP address**: You can select to use a different IP address for the replicated VM.</span></span> <span data-ttu-id="b42f5-221">在此情況下，VM 會在容錯移轉之後取得新的 IP 位址，因此需要更新 DNS。</span><span class="sxs-lookup"><span data-stu-id="b42f5-221">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="b42f5-222">**保留相同的 IP 位址**：您可能想讓複本 VM 使用相同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b42f5-222">**Retain the same IP address**: You might want to use the same IP address for the replica VM.</span></span> <span data-ttu-id="b42f5-223">保留相同的 IP 位址可在容錯移轉之後減少網路相關問題，藉以簡化復原。</span><span class="sxs-lookup"><span data-stu-id="b42f5-223">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> 

## <a name="retain-ip-addresses"></a><span data-ttu-id="b42f5-224">保留 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b42f5-224">Retain IP addresses</span></span>

<span data-ttu-id="b42f5-225">如果您想在容錯移轉至次要站台後保留主要站台的 IP 位址，可以執行完整的子網路容錯移轉，並更新路由以指示 IP 位址的新位置，或在主要和復原站台之間部署延伸的子網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-225">If you want to retain the IP addresses from the primary site after failover to the secondary site, you can do a full subnet failover, and update routes to indicate the new location of the IP addresses, or alternative deploy a stretched subnet between the primary and the recovery sites.</span></span>

### <a name="stretched-subnet"></a><span data-ttu-id="b42f5-226">延伸的子網路</span><span class="sxs-lookup"><span data-stu-id="b42f5-226">Stretched subnet</span></span>

<span data-ttu-id="b42f5-227">在延伸的子網路中，主要站台和次要站台可同時使用子網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-227">In a stretched subnet, the subnet is available simultaneously in both the primary and secondary site.</span></span> <span data-ttu-id="b42f5-228">如果您將伺服器和其 IP (第 3 層) 組態移至次要站台，網路會自動將流量路由傳送至新位置。</span><span class="sxs-lookup"><span data-stu-id="b42f5-228">If you move a server and its IP (Layer 3) configuration to the secondary site, the network will route the traffic to the new location automatically.</span></span> 

<span data-ttu-id="b42f5-229">從第 2 層 (資料連結層) 的觀點而言，您需要可以管理延伸的 VLAN 的網路設備。</span><span class="sxs-lookup"><span data-stu-id="b42f5-229">From a Layer 2 (data link layer) perspective, you need networking equipment that can manage a stretched VLAN.</span></span> <span data-ttu-id="b42f5-230">另外，透過延伸 VLAN，潛在的容錯網域會延伸到兩個站台，基本上成為單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="b42f5-230">In addition, by stretching the VLAN, the potential fault domain extends to both sites, essentially becoming a single point of failure.</span></span> <span data-ttu-id="b42f5-231">雖然機率不高，但有可能發生廣播風暴，而且無法隔離。</span><span class="sxs-lookup"><span data-stu-id="b42f5-231">While this is an unlikely, it could happen that a broadcast storm started and cannot be isolated.</span></span> 


### <a name="subnet-failover"></a><span data-ttu-id="b42f5-232">子網路容錯移轉</span><span class="sxs-lookup"><span data-stu-id="b42f5-232">Subnet failover</span></span>

<span data-ttu-id="b42f5-233">您可以執行子網路容錯移轉，以獲得延伸子網路的好處，而不用實際延伸。</span><span class="sxs-lookup"><span data-stu-id="b42f5-233">You can run a subnet failover to obtain the benefits of the stretched subnet, without actually stretching it.</span></span> <span data-ttu-id="b42f5-234">在此解決方案中，子網路將可用於來源或目標站台，但不能同時使用於兩者。</span><span class="sxs-lookup"><span data-stu-id="b42f5-234">In this solution, a subnet will be available in the source or target site, but not at both simultaneously.</span></span> <span data-ttu-id="b42f5-235">若要在發生容錯移轉時維持 IP 位址空間，您可以程式設計方式排列路由器基礎結構，將子網路從某個站台移到另一個站台。</span><span class="sxs-lookup"><span data-stu-id="b42f5-235">To maintain the IP address space in the event of a failover, you can programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="b42f5-236">之後，當發生容錯移轉時，子網路會連同相關聯的 VM 一起移動。</span><span class="sxs-lookup"><span data-stu-id="b42f5-236">After when failover occurs, subnets would move with the associated VMs.</span></span> <span data-ttu-id="b42f5-237">主要的缺點在於，當發生失敗時，您必須移動整個子網路。</span><span class="sxs-lookup"><span data-stu-id="b42f5-237">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>

### <a name="example"></a><span data-ttu-id="b42f5-238">範例</span><span class="sxs-lookup"><span data-stu-id="b42f5-238">Example</span></span>

<span data-ttu-id="b42f5-239">以下是完整的子網路容錯移轉範例。</span><span class="sxs-lookup"><span data-stu-id="b42f5-239">Here's an example of complete subnet failover.</span></span> <span data-ttu-id="b42f5-240">主要站台有在子網路 192.168.1.0/24 中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b42f5-240">The primary site has applications running in subnet 192.168.1.0/24.</span></span> <span data-ttu-id="b42f5-241">在容錯移轉時，這個子網路中的所有 VM 會容錯移轉至次要網站，並保留其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b42f5-241">At failover, all the VMs in this subnet are failed over to the secondary site, and retain their IP addresses.</span></span> <span data-ttu-id="b42f5-242">您必須修改路由，以反映屬於子網路 192.168.1.0/24 的所有 VM 現在都已移至復原站台的事實。</span><span class="sxs-lookup"><span data-stu-id="b42f5-242">Routes need to be modified to reflect the fact that all the VM virtual machines belonging to subnet 192.168.1.0/24 have now moved to the secondary site.</span></span>

<span data-ttu-id="b42f5-243">下圖顯示容錯移轉前後的子網路：</span><span class="sxs-lookup"><span data-stu-id="b42f5-243">The following graphics show the subnets before and after failover:</span></span>

- <span data-ttu-id="b42f5-244">在容錯移轉之前，子網路 192.168.0.1/24 的作用中環境是來源站台，在容錯移轉之後則變成次要站台。</span><span class="sxs-lookup"><span data-stu-id="b42f5-244">Before failover, subnet 192.168.0.1/24 is active on the source site, become active on the secondary site after failover.</span></span>
- <span data-ttu-id="b42f5-245">主要站台和復原站台、第三個站台和主要站台、以及第三個站台和復原站台之間的路由都必須適當地修改。</span><span class="sxs-lookup"><span data-stu-id="b42f5-245">The routes between primary site and recovery site, third site and primary site, and third site and recovery site will have to be appropriately modified.</span></span>

<span data-ttu-id="b42f5-246">**容錯移轉之前**</span><span class="sxs-lookup"><span data-stu-id="b42f5-246">**Before failover**</span></span>

![容錯移轉之前](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

<span data-ttu-id="b42f5-248">**容錯移轉之後**</span><span class="sxs-lookup"><span data-stu-id="b42f5-248">**After failover**</span></span>

![容錯移轉之後](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

<span data-ttu-id="b42f5-250">容錯移轉之後，會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="b42f5-250">After failover, here's what happens:</span></span>

- <span data-ttu-id="b42f5-251">針對每個 VMM 執行個體，Site Recovery 會為 VM 上的每個網路介面配置 IP 位址 (從相關網路中的靜態 IP 位址集區)。</span><span class="sxs-lookup"><span data-stu-id="b42f5-251">Site Recovery allocates an IP address for each network interface on the VM, from the static IP address pool in the relevant network, for each VMM instance.</span></span>
- <span data-ttu-id="b42f5-252">如果次要站台中的 IP 位址集區與來源站台中的相同，Site Recovery 會配置同一個 IP 位址 (來源 VM 的 IP 位址) 給複本 VM。</span><span class="sxs-lookup"><span data-stu-id="b42f5-252">If the IP address pool in the secondary site is the same as that on the source site, Site Recovery allocates the same IP address (of the source VM) to the replica VM.</span></span> <span data-ttu-id="b42f5-253">IP 位址會保留在 VMM 中，但不會設為 Hyper-V 主機上的容錯移轉 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b42f5-253">The IP address is reserved in VMM, but it isn't set as the failover IP address on the Hyper-V host.</span></span> <span data-ttu-id="b42f5-254">Hyper-V 主機上的容錯移轉 IP 位址會在容錯移轉之前設定。</span><span class="sxs-lookup"><span data-stu-id="b42f5-254">The failover IP address on a Hyper-v host is set just before the failover.</span></span>
- <span data-ttu-id="b42f5-255">如果同一個 IP 位址無法使用，Site Recovery 會從集區配置另一個可用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b42f5-255">If the same IP address isn't available, Site Recovery allocates another available IP address from the pool.</span></span>
- <span data-ttu-id="b42f5-256">如果 VM 使用 DHCP，Site Recovery 無法管理 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b42f5-256">If VMs use DHCP, Site Recovery doesn't manage the IP addresses.</span></span> <span data-ttu-id="b42f5-257">您必須確定次要站台上的 DHCP 伺服器可以從與來源站台相同的範圍配置位址。</span><span class="sxs-lookup"><span data-stu-id="b42f5-257">You need to check that the DHCP server on the secondary site can allocate address from the same range as the source site.</span></span>

### <a name="validate-the-ip-address"></a><span data-ttu-id="b42f5-258">驗證 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b42f5-258">Validate the IP address</span></span>

<span data-ttu-id="b42f5-259">啟用 VM 保護之後，您可以使用下列範例指令碼來驗證指派給 VM 的位址。</span><span class="sxs-lookup"><span data-stu-id="b42f5-259">After you enable protection for a VM, you can use following sample script to verify the address assigned to the VM.</span></span> <span data-ttu-id="b42f5-260">這個 IP 位址會設定為容錯移轉 IP 位址，並在容錯移轉時指派給 VM：</span><span class="sxs-lookup"><span data-stu-id="b42f5-260">The same IP address will be set as the failover IP address, and assigned to the VM at the time of failover:</span></span>

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a><span data-ttu-id="b42f5-261">變更 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b42f5-261">Changing IP addresses</span></span>

<span data-ttu-id="b42f5-262">在此案例中，容錯移轉之 VM 的 IP 位址會變更。</span><span class="sxs-lookup"><span data-stu-id="b42f5-262">In this scenario, the IP addresses of VMs that fail over are changed.</span></span> <span data-ttu-id="b42f5-263">此解決方案的缺點是需要維護。</span><span class="sxs-lookup"><span data-stu-id="b42f5-263">The drawback of this solution is the maintenance required.</span></span> <span data-ttu-id="b42f5-264">通常在複本 VM 啟動後會更新 DNS。</span><span class="sxs-lookup"><span data-stu-id="b42f5-264">Typically, DNS will be updated after replica VMs start.</span></span> <span data-ttu-id="b42f5-265">DNS 項目可能需要變更，否則在網路中會造成混亂，而快取的項目已更新。</span><span class="sxs-lookup"><span data-stu-id="b42f5-265">DNS entries might need to be changed or fluster in thenetwork, and cached entries updated.</span></span> <span data-ttu-id="b42f5-266">這可能會導致停機時間。</span><span class="sxs-lookup"><span data-stu-id="b42f5-266">This can result in downtime.</span></span> <span data-ttu-id="b42f5-267">透過下列方式可以避免停機時間：</span><span class="sxs-lookup"><span data-stu-id="b42f5-267">Downtime can be mitigated as follows:</span></span>

- <span data-ttu-id="b42f5-268">對內部網路應用程式使用低 TTL 值。</span><span class="sxs-lookup"><span data-stu-id="b42f5-268">Use low TTL values for intranet applications.</span></span>
- <span data-ttu-id="b42f5-269">在 Site Recovery 復原計畫中使用下列指令碼來更新 DNS 伺服器，以確保及時更新。</span><span class="sxs-lookup"><span data-stu-id="b42f5-269">Use the following script in a Site Recovery recovery plan, to update the DNS server to ensure a timely update.</span></span> <span data-ttu-id="b42f5-270">如果您使用動態 DNS 登錄，則不需要這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="b42f5-270">You don't need the script if you use dynamic DNS registration.</span></span>

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
    
### <a name="example"></a><span data-ttu-id="b42f5-271">範例</span><span class="sxs-lookup"><span data-stu-id="b42f5-271">Example</span></span> 

<span data-ttu-id="b42f5-272">來看看您計劃在主要和復原站台使用不同 IP 位址的案例。在此範例中，主要和次要站台有不同的 IP 位址，而且有第三個站台，可以從中存取裝載於主要或復原站台上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b42f5-272">Let's look at a scenario in which you're planning to use different IP addresses across the primary and the recovery sites.In this example we have different IP addresses across primary and secondary sites, and there;s a third site from which applications hosted on the primary or recovery site can be accessed.</span></span>

- <span data-ttu-id="b42f5-273">在容錯移轉之前，應用程式是裝載於主要站台上的子網路 192.168.1.0/24，在容錯移轉之後則會設為次要站台上的子網路 172.16.1.0/24。</span><span class="sxs-lookup"><span data-stu-id="b42f5-273">Before failover, apps are hosted subnet 192.168.1.0/24 on the primary site, and are configured to be in subnet 172.16.1.0/24 on the secondary site after a failover.</span></span>
- <span data-ttu-id="b42f5-274">已適當地設定 VPN 連線/網路路由，讓所有的三個站台可以互相存取。</span><span class="sxs-lookup"><span data-stu-id="b42f5-274">VPN connections/network routes have been configured appropriately so that all three sites can access each other.</span></span>
- <span data-ttu-id="b42f5-275">在容錯移轉之後，應用程式將於復原子網路中還原。</span><span class="sxs-lookup"><span data-stu-id="b42f5-275">After failover, apps will be restored in the recovery subnet.</span></span> <span data-ttu-id="b42f5-276">在此案例中，不需要容錯移轉整個子網路，而且不需任何變更，即可重新設定 VPN 或網路路由。</span><span class="sxs-lookup"><span data-stu-id="b42f5-276">In this scenario there's no need to fail over the entire subnet, and no changes are needed to reconfigure VPN or network routes.</span></span> <span data-ttu-id="b42f5-277">容錯移轉和某些 DNS 更新可確保應用程式可供存取。</span><span class="sxs-lookup"><span data-stu-id="b42f5-277">The failover, and some DNS updates, ensure that applications remain accessible.</span></span>
- <span data-ttu-id="b42f5-278">如果 DNS 設定為允許動態更新，則 VM 在容錯移轉後啟動時，就會使用新的 IP 位址自行註冊。</span><span class="sxs-lookup"><span data-stu-id="b42f5-278">If DNS is configured to allow dynamic updates, then the VMs will register themselves using the new IP address, when they start after failover.</span></span>

<span data-ttu-id="b42f5-279">**容錯移轉之前**</span><span class="sxs-lookup"><span data-stu-id="b42f5-279">**Before failover**</span></span>

![不同的 IP - 容錯移轉之前](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

<span data-ttu-id="b42f5-281">**容錯移轉之後**</span><span class="sxs-lookup"><span data-stu-id="b42f5-281">**After failover**</span></span>

![不同的 IP - 容錯移轉之後](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a><span data-ttu-id="b42f5-283">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b42f5-283">Next steps</span></span>

<span data-ttu-id="b42f5-284">移至[步驟 4：準備 VMM 和 Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md)。</span><span class="sxs-lookup"><span data-stu-id="b42f5-284">Go to [Step 4: Prepare VMM and Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>


