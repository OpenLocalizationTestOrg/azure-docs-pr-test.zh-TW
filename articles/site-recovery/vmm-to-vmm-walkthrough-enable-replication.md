---
title: "aaaEnable HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery |Microsoft 文件"
description: "描述如何針對 HYPER-V Vm 複寫 tooa tooenable 複寫次要 System Center VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="851c2-103">步驟 9： 啟用複寫 tooa 次要站台的 HYPER-V Vm</span><span class="sxs-lookup"><span data-stu-id="851c2-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="851c2-104">設定好的複寫原則之後，使用此發行項 tooenable 複寫 tooa 次要 System Center Virtual Machine Manager (VMM) 站台的內部部署 HYPER-V 虛擬機器 (VM)，使用[Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="851c2-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="851c2-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="851c2-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="851c2-106">選取 Vm tooreplicate</span><span class="sxs-lookup"><span data-stu-id="851c2-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="851c2-107">按一下 [步驟 2: 複寫應用程式]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="851c2-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![啟用複寫](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="851c2-109">在**來源**、 選取 hello VMM 伺服器，和 hello 中的 hello 想 tooreplicate 的 HYPER-V 主機位於的雲端。</span><span class="sxs-lookup"><span data-stu-id="851c2-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="851c2-110">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="851c2-110">Then click **OK**.</span></span>

    ![啟用複寫](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="851c2-112">在**目標**，確認 hello 次要 VMM 伺服器和雲端。</span><span class="sxs-lookup"><span data-stu-id="851c2-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="851c2-113">在**虛擬機器**，選取您想要從 hello 清單 tooprotect hello Vm。</span><span class="sxs-lookup"><span data-stu-id="851c2-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![啟用虛擬機器保護](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="851c2-115">您可以追蹤進度的 hello**啟用保護**中的動作**作業** > **站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="851c2-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="851c2-116">之後 hello**完成保護**作業完成、 hello 初始複寫完成，且 hello 虛擬機器是否已做好容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="851c2-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="851c2-117">請注意：</span><span class="sxs-lookup"><span data-stu-id="851c2-117">Note that:</span></span>

- <span data-ttu-id="851c2-118">您也可以啟用 hello VMM 主控台中的虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="851c2-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="851c2-119">按一下**啟用保護**hello 虛擬機器內容中的 hello 工具列上 > **Azure Site Recovery**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="851c2-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="851c2-120">啟用複寫之後，您可以檢視內容 hello VM 中**複寫的項目**。</span><span class="sxs-lookup"><span data-stu-id="851c2-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="851c2-121">在 hello **Essentials**儀表板，您可以看到 hello hello VM 和其狀態的複寫原則的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="851c2-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="851c2-122">如需詳細資訊，請按一下 [屬性]  。</span><span class="sxs-lookup"><span data-stu-id="851c2-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="851c2-123">加入現有的 VM</span><span class="sxs-lookup"><span data-stu-id="851c2-123">Onboard existing VMs</span></span>

<span data-ttu-id="851c2-124">如果 VMM 中目前已經有使用 Hyper-V 複本複寫的虛擬機器，您可以使用下列方式加入它們以提供 Azure Site Recovery 複寫：</span><span class="sxs-lookup"><span data-stu-id="851c2-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="851c2-125">請確認裝載現有 VM 的 hello hello HYPER-V 伺服器位於 hello 主要雲端，然後裝載 hello 複本虛擬機器的 hello HYPER-V 伺服器位於 hello 次要雲端。</span><span class="sxs-lookup"><span data-stu-id="851c2-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="851c2-126">請確定 hello 主要 VMM 雲端所設定的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="851c2-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="851c2-127">啟用 hello 主要虛擬機器的複寫。</span><span class="sxs-lookup"><span data-stu-id="851c2-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="851c2-128">Azure Site Recovery 和 VMM 確定 hello 相同的複本主機和虛擬機器偵測到，，和 Azure Site Recovery 會重複使用，並重新建立複寫使用 hello 指定設定。</span><span class="sxs-lookup"><span data-stu-id="851c2-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="851c2-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="851c2-129">Next steps</span></span>

<span data-ttu-id="851c2-130">跳過[步驟 10： 執行測試容錯移轉](vmm-to-vmm-walkthrough-test-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="851c2-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
