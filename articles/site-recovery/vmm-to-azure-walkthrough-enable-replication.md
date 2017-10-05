---
title: "使用 Azure Site Recovery 將 VMM 雲端中的 Hyper-V VM 複寫至 Azure | Microsoft Docs"
description: "說明如何使用 Azure Site Recovery 服務將 VMM 雲端中的 Hyper-V VM 複寫至 Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 96a817e43a830e836f2faa4603fc88ed9c0b1828
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="step-11-enable-replication-to-azure-for-hyper-v-vms-in-vmm-clouds"></a><span data-ttu-id="34039-103">步驟 11：啟用將 Hyper-V VM (位於 VMM 雲端中) 複寫至 Azure 的複寫功能</span><span class="sxs-lookup"><span data-stu-id="34039-103">Step 11: Enable replication to Azure for Hyper-V VMs in VMM clouds</span></span>

<span data-ttu-id="34039-104">設定複寫原則後，請使用本文來啟用複寫功能，以使用 Azure 入口網站中的 [Azure Site Recovery](site-recovery-overview.md) 服務將 System Center Virtual Machine Manager (VMM) 雲端中管理的內部部署 Hyper-V 虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="34039-104">After you've set up a replication policy, use this article to enable replication for on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds), to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="34039-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="34039-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="34039-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="34039-106">Before you start</span></span>

<span data-ttu-id="34039-107">請確定您的 Azure 帳戶有適當的[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)可建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="34039-107">Make sure your Azure account has the correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)to create Azure VMs.</span></span> <span data-ttu-id="34039-108">[深入了解](../active-directory/role-based-access-built-in-roles.md) Azure 角色型存取控制。</span><span class="sxs-lookup"><span data-stu-id="34039-108">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="34039-109">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="34039-109">Exclude disks from replication</span></span>

<span data-ttu-id="34039-110">依預設會複寫電腦上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-110">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="34039-111">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-111">You can exclude disks from replication.</span></span> <span data-ttu-id="34039-112">例如，您可能不想要複寫具有暫存資料的磁碟，或是每次機器或應用程式重新啟動時便重新整理的資料 (例如 pagefile.sys 或 SQL Server tempdb)。</span><span class="sxs-lookup"><span data-stu-id="34039-112">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="34039-113">深入了解</span><span class="sxs-lookup"><span data-stu-id="34039-113">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="34039-114">複寫 VM</span><span class="sxs-lookup"><span data-stu-id="34039-114">Replicate VMs</span></span>

<span data-ttu-id="34039-115">啟用 VM 複寫，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="34039-115">Enable replication for VMs as follows:</span></span>  

1. <span data-ttu-id="34039-116">按一下 [步驟 2: 複寫應用程式]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="34039-116">Click **Step 2: Replicate application** > **Source**.</span></span> <span data-ttu-id="34039-117">第一次啟用複寫之後，請按一下保存庫中的 [+複寫]，以對其他機器啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="34039-117">After you've enabled replication for the first time, click **+Replicate** in the vault to enable replication for additional machines.</span></span>

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. <span data-ttu-id="34039-119">在 [來源] 刀鋒視窗中，選取 VMM 伺服器和 Hyper-V 主機所在的雲端。</span><span class="sxs-lookup"><span data-stu-id="34039-119">In the **Source** blade, select the VMM server, and the cloud in which the Hyper-V hosts are located.</span></span> <span data-ttu-id="34039-120">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="34039-120">Then click **OK**.</span></span>

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. <span data-ttu-id="34039-122">在 [目標] 中，選取訂用帳戶、容錯移轉後的部署模型，以及您用於複寫資料的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="34039-122">In **Target**, select the subscription, post-failover deployment model, and the storage account you're using for replicated data.</span></span>

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. <span data-ttu-id="34039-124">選取您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="34039-124">Select the storage account you want to use.</span></span> <span data-ttu-id="34039-125">如果您想使用與現有不同的儲存體帳戶，您可以[建立一個](#set-up-an-azure-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="34039-125">If you want to use a different storage account than those you have, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="34039-126">如果您將進階儲存體帳戶使用於複寫的資料，則必須選取其他標準儲存體帳戶來儲存複寫記錄，而這類記錄會擷取內部部署資料的進行中變更。若要使用 Resource Manager 模型建立儲存體帳戶，按一下 [新建]。</span><span class="sxs-lookup"><span data-stu-id="34039-126">If you’re using a premium storage account for replicated data, you need to select  an additional standard storage account to store replication logs that capture ongoing changes to on-premises data.To create a storage account using the Resource Manager model click **Create new**.</span></span> <span data-ttu-id="34039-127">如果您想要使用傳統模型建立儲存體帳戶，請[在 Azure 入口網站中](../storage/common/storage-create-storage-account.md)執行該作業。</span><span class="sxs-lookup"><span data-stu-id="34039-127">If you want to create a storage account using the classic model, do that [in the Azure portal](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="34039-128">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="34039-128">Then click **OK**.</span></span>
5. <span data-ttu-id="34039-129">選取 Azure VM 在容錯移轉後啟動時所要建立的 Azure 網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="34039-129">Select the Azure network and subnet to which Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="34039-130">選取 [立即設定選取的機器]，將網路設定套用至您選取要進行保護的所有機器。</span><span class="sxs-lookup"><span data-stu-id="34039-130">Select **Configure now for selected machines**, to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="34039-131">選取 [稍後設定] 以選取每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="34039-131">Select **Configure later**, to select the Azure network per machine.</span></span> <span data-ttu-id="34039-132">如果您想使用與現有不同的網路，您可以[建立一個](#set-up-an-azure-network)。</span><span class="sxs-lookup"><span data-stu-id="34039-132">If you want to use a different network from those you have, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="34039-133">若要使用 Resource Manager 模型來建立網路，請按一下 [新建]。</span><span class="sxs-lookup"><span data-stu-id="34039-133">To create a network using the Resource Manager model click **Create new**.</span></span> <span data-ttu-id="34039-134">如果您想要使用傳統模型建立網路，請[在 Azure 入口網站中](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)執行該作業。</span><span class="sxs-lookup"><span data-stu-id="34039-134">If you want to create a network using the classic model, do that [in the Azure portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> <span data-ttu-id="34039-135">選取適用的子網路。</span><span class="sxs-lookup"><span data-stu-id="34039-135">Select a subnet if applicable.</span></span> <span data-ttu-id="34039-136">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="34039-136">Then click **OK**.</span></span>
6. <span data-ttu-id="34039-137">在 [虛擬機器] > [選取虛擬機器] 中，按一下並選取您要複寫的每部機器。</span><span class="sxs-lookup"><span data-stu-id="34039-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="34039-138">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="34039-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="34039-139">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="34039-139">Then click **OK**.</span></span>

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. <span data-ttu-id="34039-141">在 [名稱]  > 中，為選取的 VM 選取作業系統，以及 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-141">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>

    - <span data-ttu-id="34039-142">確認 Azure VM 名稱 (目標名稱) 符合 [Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="34039-142">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>   
    - <span data-ttu-id="34039-143">依預設會選取 VM 的所有磁碟以進行複寫，但您可以將磁碟清除以排除它們。</span><span class="sxs-lookup"><span data-stu-id="34039-143">By default all the disks of the VM are selected for replication, but you can clear disks to exclude them.</span></span>

        - <span data-ttu-id="34039-144">您可能想要排除磁碟來減少複寫頻寬。</span><span class="sxs-lookup"><span data-stu-id="34039-144">You might want to exclude disks to reduce replication bandwidth.</span></span> <span data-ttu-id="34039-145">例如，您可能不想要複寫具有暫存資料的磁碟，或是每次電腦或應用程式重新啟動時便重新整理的資料 (例如 pagefile.sys 或 Microsoft SQL Server tempdb)。</span><span class="sxs-lookup"><span data-stu-id="34039-145">For example, you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or apps restarts (such as pagefile.sys or Microsoft SQL Server tempdb).</span></span> <span data-ttu-id="34039-146">您可以取消選取磁碟以將磁碟排除複寫。</span><span class="sxs-lookup"><span data-stu-id="34039-146">You can exclude the disk from replication by unselecting the disk.</span></span>
        - <span data-ttu-id="34039-147">只有基本磁碟可以排除。</span><span class="sxs-lookup"><span data-stu-id="34039-147">Only basic disks can be exclude.</span></span> <span data-ttu-id="34039-148">您無法排除作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-148">You can't exclude OS disks.</span></span>
        - <span data-ttu-id="34039-149">我們建議不要排除動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-149">We recommend that you don't exclude dynamic disks.</span></span> <span data-ttu-id="34039-150">Site Recovery 無法識別客體 VM 內的虛擬硬碟為基本還是動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-150">Site Recovery can't identify whether a virtual hard disk inside a guest VM is basic or dynamic.</span></span> <span data-ttu-id="34039-151">如果未排除所有的相依動態磁碟區磁碟，受保護的動態磁碟會在 VM 容錯移轉時顯示為失敗的磁碟，且該磁碟上的資料無法存取。</span><span class="sxs-lookup"><span data-stu-id="34039-151">If all dependent dynamic volume disks aren't excluded, the protected dynamic disk will show as a failed disk when the VM fails over, and the data on that disk won't be accessible.</span></span>
        - <span data-ttu-id="34039-152">啟用複寫後，您無法加入或移除複寫的磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-152">After replication is enabled, you can't add or remove disks for replication.</span></span> <span data-ttu-id="34039-153">如果您想要新增或排除磁碟，必須停用 VM 的保護，然後重新啟用它。</span><span class="sxs-lookup"><span data-stu-id="34039-153">If you want to add or exclude a disk, you need to disable protection for the VM, and then re-enable it.</span></span>
        - <span data-ttu-id="34039-154">您以手動方式在 Azure 中建立的磁碟將不會容錯回復。</span><span class="sxs-lookup"><span data-stu-id="34039-154">Disks you create manually in Azure aren't failed back.</span></span> <span data-ttu-id="34039-155">例如，如果您容錯移轉三個磁碟，並直接在 Azure VM 中建立兩個磁碟，則只有那三個容錯移轉的磁碟會從 Azure 容錯回復至 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="34039-155">For example, if you fail over three disks, and create two directly in Azure VM, only the three disks which were failed over will be failed back from Azure to Hyper-V.</span></span> <span data-ttu-id="34039-156">您無法在容錯回復，或是從 Hyper-V 至 Azure 的反向複寫中包含手動建立的磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-156">You can't include disks created manually in failback, or in reverse replication from Hyper-V to Azure.</span></span>
        - <span data-ttu-id="34039-157">如果您排除應用程式運作所需的磁碟，在容錯移轉至 Azure 之後，您必須在 Azure 中手動建立它，複寫的應用程式才能執行。</span><span class="sxs-lookup"><span data-stu-id="34039-157">If you exclude a disk that's needed for an application to operate, after failover to Azure you need to create it manually in Azure, so that the replicated application can run.</span></span> <span data-ttu-id="34039-158">或者，您可以將 Azure 自動化整合至復原計畫，在電腦容錯移轉期間建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="34039-158">Alternatively, you could integrate Azure automation into a recovery plan, to create the disk during failover of the machine.</span></span>

    <span data-ttu-id="34039-159">按一下 [確定] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="34039-159">Click **OK** to save changes.</span></span> <span data-ttu-id="34039-160">您可以稍後再設定其他屬性。</span><span class="sxs-lookup"><span data-stu-id="34039-160">You can set additional properties later.</span></span>

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. <span data-ttu-id="34039-162">在 [複寫設定]  >  [進行複寫設定] 中，選取您要套用於受保護 VM 的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="34039-162">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="34039-163">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="34039-163">Then click **OK**.</span></span> <span data-ttu-id="34039-164">您可以在 > [複寫原則] > 原則名稱 > [編輯設定] 中，修改複寫原則。</span><span class="sxs-lookup"><span data-stu-id="34039-164">You can modify the replication policy in **Replication policies** > policy name > **Edit Settings**.</span></span> <span data-ttu-id="34039-165">您套用的變更用於已在複寫的機器和新的機器。</span><span class="sxs-lookup"><span data-stu-id="34039-165">Changes you apply are used for machines that are already replicating, and new machines.</span></span>

   ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="34039-167">您可以在 [作業] >  [Site Recovery 作業] 中，追蹤 [啟用保護] 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="34039-167">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="34039-168">執行 [完成保護] 作業之後，機器即準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="34039-168">After the **Finalize Protection** job runs, the machine is ready for failover.</span></span>



## <a name="next-steps"></a><span data-ttu-id="34039-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34039-169">Next steps</span></span>

<span data-ttu-id="34039-170">移至[步驟 12：執行測試容錯移轉](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="34039-170">Go to [Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>
