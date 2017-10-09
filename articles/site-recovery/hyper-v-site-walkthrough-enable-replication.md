---
title: "HYPER-V Vm 複寫 tooAzure （不含 System Center VMM) 與 Azure Site Recovery 的 aaaEnable 複寫 |Microsoft 文件"
description: "摘要說明您需要使用 hello Azure Site Recovery 服務的 HYPER-V Vm tooenable 複寫 tooAzure hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="d6c08-103">步驟 10： 啟用複寫功能複寫 tooAzure HYPER-V Vm</span><span class="sxs-lookup"><span data-stu-id="d6c08-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="d6c08-104">本文說明如何 tooenable 複寫在內部部署 HYPER-V 虛擬機器 （不受 System Center VMM） tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="d6c08-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="d6c08-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="d6c08-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="d6c08-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="d6c08-106">Before you start</span></span>

<span data-ttu-id="d6c08-107">在開始之前，請確定您的 Azure 使用者帳戶具有所需的 hello[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。</span><span class="sxs-lookup"><span data-stu-id="d6c08-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="d6c08-108">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="d6c08-108">Exclude disks from replication</span></span>

<span data-ttu-id="d6c08-109">依預設會複寫電腦上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6c08-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="d6c08-110">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6c08-110">You can exclude disks from replication.</span></span> <span data-ttu-id="d6c08-111">例如您可能不想 tooreplicate 磁碟具有暫存資料或重新整理每次在電腦的資料或應用程式重新啟動 （例如 pagefile.sys 或 SQL Server tempdb）。</span><span class="sxs-lookup"><span data-stu-id="d6c08-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="d6c08-112">深入了解</span><span class="sxs-lookup"><span data-stu-id="d6c08-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="d6c08-113">複寫 VM</span><span class="sxs-lookup"><span data-stu-id="d6c08-113">Replicate VMs</span></span>

<span data-ttu-id="d6c08-114">啟用 VM 複寫，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="d6c08-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="d6c08-115">按一下 [複寫應用程式] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="d6c08-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="d6c08-116">您已設定第一次的 hello 複寫之後，您可以按一下**+ 複寫**tooenable 其他機器複寫。</span><span class="sxs-lookup"><span data-stu-id="d6c08-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="d6c08-118">在**來源**，選取 hello HYPER-V 站台。</span><span class="sxs-lookup"><span data-stu-id="d6c08-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="d6c08-119">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d6c08-119">Then click **OK**.</span></span>
3. <span data-ttu-id="d6c08-120">在**目標**選取 hello 保存庫訂用帳戶，hello 想在容錯移轉之後 toouse Azure （classic 或資源管理） 中的容錯移轉模式。</span><span class="sxs-lookup"><span data-stu-id="d6c08-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="d6c08-121">選取您想 toouse hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6c08-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="d6c08-122">如果您沒有您想要讓 toouse 帳戶，您可以[建立一個](#set-up-an-azure-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="d6c08-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="d6c08-123">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d6c08-123">Then click **OK**.</span></span>
5. <span data-ttu-id="d6c08-124">正在建立容錯移轉時，將會連接選取 hello Azure 網路和子網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="d6c08-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="d6c08-125">選取 tooapply hello 網路設定 tooall 機器啟用複寫，**現在選取的機器設定**。</span><span class="sxs-lookup"><span data-stu-id="d6c08-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="d6c08-126">選取**稍後設定**tooselect hello 每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="d6c08-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="d6c08-127">如果您沒有您想 toouse 網路，您可以[建立一個](#set-up-an-azure-network)。</span><span class="sxs-lookup"><span data-stu-id="d6c08-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="d6c08-128">選取適用的子網路。</span><span class="sxs-lookup"><span data-stu-id="d6c08-128">Select a subnet if applicable.</span></span> <span data-ttu-id="d6c08-129">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d6c08-129">Then click **OK**.</span></span>

   ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="d6c08-131">在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。</span><span class="sxs-lookup"><span data-stu-id="d6c08-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="d6c08-132">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="d6c08-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="d6c08-133">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d6c08-133">Then click **OK**.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="d6c08-135">在**屬性** > **設定屬性**hello 作業系統選取的 hello 選取 Vm，hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="d6c08-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="d6c08-136">確認該 hello Azure VM 名稱 （目標） 符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="d6c08-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="d6c08-137">依預設會選取所有 hello 磁碟的 hello VM，複寫。</span><span class="sxs-lookup"><span data-stu-id="d6c08-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="d6c08-138">清除磁碟 tooexclude 它們。</span><span class="sxs-lookup"><span data-stu-id="d6c08-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="d6c08-139">按一下**確定**toosave 變更。</span><span class="sxs-lookup"><span data-stu-id="d6c08-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="d6c08-140">您可以稍後再設定其他屬性。</span><span class="sxs-lookup"><span data-stu-id="d6c08-140">You can set additional properties later.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="d6c08-142">在**複寫設定** > **設定複寫設定**，選取您想 tooapply hello 受保護 Vm 的 hello 複寫原則。</span><span class="sxs-lookup"><span data-stu-id="d6c08-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="d6c08-143">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d6c08-143">Then click **OK**.</span></span> <span data-ttu-id="d6c08-144">您可以修改中的 hello 複寫原則**複寫原則**> 原則名稱 >**編輯設定**。</span><span class="sxs-lookup"><span data-stu-id="d6c08-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="d6c08-145">您套用的變更將用於已在複寫的機器和新的機器。</span><span class="sxs-lookup"><span data-stu-id="d6c08-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="d6c08-147">您可以追蹤進度的 hello**啟用保護**作業中**作業** > **站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="d6c08-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="d6c08-148">之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d6c08-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d6c08-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6c08-149">Next steps</span></span>


<span data-ttu-id="d6c08-150">跳過[步驟 11： 執行測試容錯移轉](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="d6c08-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
