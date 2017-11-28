---
title: "使用 Azure Site Recovery 將 Hyper-V VM 複寫至 Azure (不含 System Center VMM) | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 啟用將 Hyper-V VM 複寫至 Azure 的複寫功能時所需的步驟"
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
ms.openlocfilehash: aabe99dbd375b80e4a87ca7a067927008672b4ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-to-azure"></a><span data-ttu-id="e05a1-103">步驟 10：啟用將 Hyper-V VM 複寫至 Azure 的複寫功能</span><span class="sxs-lookup"><span data-stu-id="e05a1-103">Step 10: Enable replication for Hyper-V VMs replicating to Azure</span></span>


<span data-ttu-id="e05a1-104">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務，啟用將內部部署 Hyper-V 虛擬機器 (非 System Center VMM 所管理) 複寫至 Azure 的複寫功能。</span><span class="sxs-lookup"><span data-stu-id="e05a1-104">This article describes how to enable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="e05a1-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="e05a1-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="e05a1-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="e05a1-106">Before you start</span></span>

<span data-ttu-id="e05a1-107">在開始之前，請確定您的 Azure 使用者帳戶具有必要的[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)，才能將新的虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="e05a1-107">Before you start, ensure that your Azure user account has the required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="e05a1-108">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="e05a1-108">Exclude disks from replication</span></span>

<span data-ttu-id="e05a1-109">依預設會複寫電腦上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="e05a1-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="e05a1-110">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="e05a1-110">You can exclude disks from replication.</span></span> <span data-ttu-id="e05a1-111">例如，您可能不想要複寫具有暫存資料的磁碟，或是每次機器或應用程式重新啟動時便重新整理的資料 (例如 pagefile.sys 或 SQL Server tempdb)。</span><span class="sxs-lookup"><span data-stu-id="e05a1-111">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="e05a1-112">深入了解</span><span class="sxs-lookup"><span data-stu-id="e05a1-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="e05a1-113">複寫 VM</span><span class="sxs-lookup"><span data-stu-id="e05a1-113">Replicate VMs</span></span>

<span data-ttu-id="e05a1-114">啟用 VM 複寫，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e05a1-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="e05a1-115">按一下 [複寫應用程式] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="e05a1-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="e05a1-116">第一次設定複寫之後，您可以按一下 [+複寫]，以對其他電腦啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="e05a1-116">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="e05a1-118">在 [來源] 中，選取 Hyper-V 網站。</span><span class="sxs-lookup"><span data-stu-id="e05a1-118">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="e05a1-119">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e05a1-119">Then click **OK**.</span></span>
3. <span data-ttu-id="e05a1-120">在 [目標] 中，選取保存庫訂用帳戶，以及您想要在容錯移轉後於 Azure 中使用的容錯移轉模型 (傳統或資源管理)。</span><span class="sxs-lookup"><span data-stu-id="e05a1-120">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="e05a1-121">選取您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e05a1-121">Select the storage account you want to use.</span></span> <span data-ttu-id="e05a1-122">如果您沒有想要使用的帳戶，您可以[建立一個](#set-up-an-azure-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="e05a1-122">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="e05a1-123">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e05a1-123">Then click **OK**.</span></span>
5. <span data-ttu-id="e05a1-124">選取 Azure VM 在容錯移轉後啟動時所要連線的 Azure 網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="e05a1-124">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="e05a1-125">若要將網路設定套用至您啟用要進行複寫的所有電腦，請選取 [立即設定選取的機器]。</span><span class="sxs-lookup"><span data-stu-id="e05a1-125">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="e05a1-126">選取 [稍後設定] 以選取每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="e05a1-126">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="e05a1-127">如果您沒有想要使用的網路，您可以[建立一個](#set-up-an-azure-network)。</span><span class="sxs-lookup"><span data-stu-id="e05a1-127">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="e05a1-128">選取適用的子網路。</span><span class="sxs-lookup"><span data-stu-id="e05a1-128">Select a subnet if applicable.</span></span> <span data-ttu-id="e05a1-129">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e05a1-129">Then click **OK**.</span></span>

   ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="e05a1-131">在 [虛擬機器] > [選取虛擬機器] 中，按一下並選取您要複寫的每部機器。</span><span class="sxs-lookup"><span data-stu-id="e05a1-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="e05a1-132">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="e05a1-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="e05a1-133">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e05a1-133">Then click **OK**.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="e05a1-135">在 [名稱]  > 中，為選取的 VM 選取作業系統，以及 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="e05a1-135">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="e05a1-136">確認 Azure VM 名稱 (目標名稱) 符合 [Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="e05a1-136">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="e05a1-137">依預設會選取 VM 的所有磁碟以進行複寫。</span><span class="sxs-lookup"><span data-stu-id="e05a1-137">By default all the disks of the VM are selected for replication.</span></span> <span data-ttu-id="e05a1-138">清除磁碟以將它們排除。</span><span class="sxs-lookup"><span data-stu-id="e05a1-138">Clear disks to exclude them.</span></span>
10. <span data-ttu-id="e05a1-139">按一下 [確定] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="e05a1-139">Click **OK** to save changes.</span></span> <span data-ttu-id="e05a1-140">您可以稍後再設定其他屬性。</span><span class="sxs-lookup"><span data-stu-id="e05a1-140">You can set additional properties later.</span></span>

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="e05a1-142">在 [複寫設定]  >  [進行複寫設定] 中，選取您要套用於受保護 VM 的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="e05a1-142">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="e05a1-143">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e05a1-143">Then click **OK**.</span></span> <span data-ttu-id="e05a1-144">您可以在 [複寫原則] > 原則名稱 > [編輯設定] 中，修改複寫原則。</span><span class="sxs-lookup"><span data-stu-id="e05a1-144">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="e05a1-145">您套用的變更將用於已在複寫的機器和新的機器。</span><span class="sxs-lookup"><span data-stu-id="e05a1-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="e05a1-147">您可以在 [作業] >  [Site Recovery 作業] 中，追蹤 [啟用保護] 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="e05a1-147">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="e05a1-148">執行 [完成保護]  作業之後，機器即準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="e05a1-148">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e05a1-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e05a1-149">Next steps</span></span>


<span data-ttu-id="e05a1-150">移至[步驟 11：執行測試容錯移轉](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="e05a1-150">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
