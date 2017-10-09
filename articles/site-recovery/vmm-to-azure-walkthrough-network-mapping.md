---
title: "aaaConfigure 網路對應，複寫在 VMM 中的 HYPER-V Vm 雲端與 Azure Site Recovery tooAzure |Microsoft 文件"
description: "描述如何在 VMM 中的 HYPER-V Vm 進行複寫時，tooconfigure 網路對應雲端 tooAzure 與 Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="c8bf8-103">步驟 9： 設定 HYPER-V 複寫 （VMM) tooAzure 網路對應</span><span class="sxs-lookup"><span data-stu-id="c8bf8-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="c8bf8-104">設定 hello 之後[來源和目標的複寫設定](vmm-to-azure-walkthrough-source-target.md)，使用此發行項 tooconfigure 網路對應 toomap 在內部部署 VMM VM 網路與 Azure 網路之間。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="c8bf8-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c8bf8-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="c8bf8-106">Before you start</span></span>

- <span data-ttu-id="c8bf8-107">深入了解[網路對應](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="c8bf8-108">[準備 VMM 以進行網路對應](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping)。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="c8bf8-109">請確認 hello VMM 伺服器上的虛擬機器連線的 tooa VM 網路，而且您已建立至少一個 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="c8bf8-110">多個 VM 網路可以是對應的 tooa 單一 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="c8bf8-111">設定對應</span><span class="sxs-lookup"><span data-stu-id="c8bf8-111">Configure mapping</span></span>

<span data-ttu-id="c8bf8-112">設定對應，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="c8bf8-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="c8bf8-113">在**Site Recovery 基礎結構** > **網路對應** > **網路對應**，按一下 hello **+ 的網路對應**圖示。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![網路對應](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="c8bf8-115">在**加入網路對應**，選取 hello 來源 VMM 伺服器，和**Azure**為 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="c8bf8-116">在容錯移轉之後，請確認 hello 訂用帳戶和 hello 部署模型。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="c8bf8-117">在**來源網路**，選取您想要從 hello VMM 伺服器相關聯的 hello 清單 toomap hello 來源內部部署 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="c8bf8-118">在**目標網路**，選取 hello 複本 Azure 的 Vm 會位於位置在建立時即 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="c8bf8-119">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-119">Then click **OK**.</span></span>

    ![網路對應](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="c8bf8-121">以下是網路對應開始時發生的事情︰</span><span class="sxs-lookup"><span data-stu-id="c8bf8-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="c8bf8-122">Hello 來源 VM 網路上的現有 Vm 時開始對應連接的 toohello 目標網路。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="c8bf8-123">新的 Vm 連接的 toohello 來源 VM 網路連線發生複寫時，toohello 對應 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="c8bf8-124">如果您修改現有的網路對應，複本虛擬機器會連接使用 hello 新設定。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="c8bf8-125">如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器在容錯移轉之後連接 toothat 目標子網路。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="c8bf8-126">如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器所連接 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="c8bf8-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c8bf8-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8bf8-127">Next steps</span></span>

<span data-ttu-id="c8bf8-128">跳過[步驟 10： 建立複寫原則](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c8bf8-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
