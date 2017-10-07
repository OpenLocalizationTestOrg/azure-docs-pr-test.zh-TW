---
title: "HYPER-V 虛擬機器複寫 tooa 次要站台與 Azure Site Recovery 的 aaaMap 網路 |Microsoft 文件"
description: "描述如何 toomap 網路複寫 HYPER-V Vm tooa 次要 VMM 站台與 Azure Site Recovery 時。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="0d769-103">步驟 7： 對應網路的 HYPER-V 虛擬機器複寫 tooa 次要站台</span><span class="sxs-lookup"><span data-stu-id="0d769-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="0d769-104">設定好後[來源和目標設定](vmm-to-vmm-walkthrough-source-target.md)複寫 HYPER-V 虛擬機器 (Vm) tooa 次要 System Center Virtual Machine Manager (VMM) 站台，使用 HYPER-V 虛擬此發行項 tooconfigure 網路對應機器 (VM) 複寫 tooa 次要站台，使用[Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0d769-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="0d769-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="0d769-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="0d769-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="0d769-106">Before you start</span></span>

- <span data-ttu-id="0d769-107">開始之前，深入了解[網路對應](vmm-to-vmm-walkthrough-network.md#network-mapping-overview)。</span><span class="sxs-lookup"><span data-stu-id="0d769-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="0d769-108">請確認 VMM 伺服器上的虛擬機器會連接的 tooa VM 網路。</span><span class="sxs-lookup"><span data-stu-id="0d769-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="0d769-109">設定網路對應</span><span class="sxs-lookup"><span data-stu-id="0d769-109">Configure network mapping</span></span>

1. <span data-ttu-id="0d769-110">在 [網路對應] > [網路對應]，按一下 [+網路對應]。</span><span class="sxs-lookup"><span data-stu-id="0d769-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="0d769-111">在**加入網路對應**索引標籤上，選取 hello 來源與目標 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0d769-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="0d769-112">擷取 hello 與 hello VMM 伺服器相關聯的 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="0d769-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="0d769-113">在**來源網路**，選取您想 toouse hello 清單中的 hello 主要 VMM 伺服器相關聯的 VM 網路的 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="0d769-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="0d769-114">在**目標網路**，選取您想 toouse hello 次要 VMM 伺服器上的 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="0d769-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="0d769-115">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0d769-115">Then click **OK**.</span></span>

    ![網路對應](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="0d769-117">以下是網路對應開始時發生的事情︰</span><span class="sxs-lookup"><span data-stu-id="0d769-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="0d769-118">對應 toohello 來源 VM 網路的任何現有複本虛擬機器會連接的 toohello 目標 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="0d769-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="0d769-119">新的虛擬機器所連接的 toohello 來源 VM 網路在複寫之後會連接的 toohello 目標對應的網路。</span><span class="sxs-lookup"><span data-stu-id="0d769-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="0d769-120">如果您修改現有的對應與新的網路，複本虛擬機器將使用 hello 新設定連接。</span><span class="sxs-lookup"><span data-stu-id="0d769-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="0d769-121">如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="0d769-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="0d769-122">如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="0d769-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0d769-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d769-123">Next steps</span></span>

<span data-ttu-id="0d769-124">跳過[步驟 8： 設定複寫原則](vmm-to-vmm-walkthrough-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="0d769-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
