---
title: "管理和監視 Azure 虛擬機器備份 | Microsoft Docs"
description: "了解如何管理和監視 Azure 虛擬機器備份"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d876bb1759600fa29a26730bfa8b4ec19db1e442
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-the-classic-portal"></a><span data-ttu-id="527fa-103">在傳統入口網站中管理一般的 Azure 備份作業和觸發警示</span><span class="sxs-lookup"><span data-stu-id="527fa-103">Manage common Azure Backup jobs and trigger alerts in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="527fa-104">管理 Azure VM 備份</span><span class="sxs-lookup"><span data-stu-id="527fa-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="527fa-105">管理傳統 VM 備份</span><span class="sxs-lookup"><span data-stu-id="527fa-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="527fa-106">本文針對 Azure 中受保護的傳統模型虛擬機器，提供一般管理和監視工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="527fa-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="527fa-107">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="527fa-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="527fa-108">如需使用傳統部署模型 VM 的詳細資料，請參閱 [準備環境以備份 Azure 虛擬機器](backup-azure-vms-prepare.md) 。</span><span class="sxs-lookup"><span data-stu-id="527fa-108">See [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="527fa-109">從 2017 年 3 月開始，您無法再使用傳統入口網站來建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="527fa-109">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
>
> <span data-ttu-id="527fa-110">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="527fa-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="527fa-111">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="527fa-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="527fa-112">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="527fa-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="527fa-113">在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="527fa-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="527fa-114">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="527fa-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="527fa-115">所有其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="527fa-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="527fa-116">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="527fa-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="527fa-117">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="527fa-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="527fa-118">管理受保護的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="527fa-118">Manage protected virtual machines</span></span>
<span data-ttu-id="527fa-119">管理受保護的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="527fa-119">To manage protected virtual machines:</span></span>

1. <span data-ttu-id="527fa-120">若要檢視和管理虛擬機器的備份設定，按一下 [ **受保護項目** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="527fa-120">To view and manage backup settings for a virtual machine click the **Protected Items** tab.</span></span>
2. <span data-ttu-id="527fa-121">按一下受保護項目的名稱以查看 [ **備份詳細資料** ] 索引標籤，上面會顯示上次備份的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="527fa-121">Click on the name of a protected item to see the **Backup Details** tab, which shows you information about the last backup.</span></span>

    ![虛擬機器備份](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="527fa-123">若要檢視和管理虛擬機器的備份原則設定，按一下 [ **原則** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="527fa-123">To view and manage backup policy settings for a virtual machine click the **Policies** tab.</span></span>

    ![虛擬機器原則](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="527fa-125">[ **備份原則** ] 索引標籤將顯示現有的原則。</span><span class="sxs-lookup"><span data-stu-id="527fa-125">The **Backup Policies** tab shows you the existing policy.</span></span> <span data-ttu-id="527fa-126">您可以視需要修改。</span><span class="sxs-lookup"><span data-stu-id="527fa-126">You can modify as needed.</span></span> <span data-ttu-id="527fa-127">如果您需要建立新的原則，按一下 [原則] 頁面中的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="527fa-127">If you need to create a new policy click **Create** on the **Policies** page.</span></span> <span data-ttu-id="527fa-128">請注意，如果您想要移除一個原則，該原則就不能與任何虛擬機器相關聯。</span><span class="sxs-lookup"><span data-stu-id="527fa-128">Note that if you want to remove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![虛擬機器原則](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="527fa-130">您可以在 [ **工作** ] 頁面取得更多虛擬機器動作或狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="527fa-130">You can get more information about actions or status for a virtual machine on the **Jobs** page.</span></span> <span data-ttu-id="527fa-131">按一下清單中的工作以取得詳細資訊，或為特定虛擬機器篩選工作。</span><span class="sxs-lookup"><span data-stu-id="527fa-131">Click a job in the list to get more details, or filter jobs for a specific virtual machine.</span></span>

    ![工作](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="527fa-133">虛擬機器的隨選備份</span><span class="sxs-lookup"><span data-stu-id="527fa-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="527fa-134">設定保護後，您可以執行虛擬機器的隨選備份。</span><span class="sxs-lookup"><span data-stu-id="527fa-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="527fa-135">如果虛擬機器的初始備份已暫止，則隨選備份會在 Azure 備份保存庫中建立虛擬機器的完整複本。</span><span class="sxs-lookup"><span data-stu-id="527fa-135">If the initial backup is pending for the virtual machine, on-demand backup will create a full copy of the virtual machine in Azure backup vault.</span></span> <span data-ttu-id="527fa-136">如果已完成第一個備份，隨選備份只會將先前備份的變更傳送到 Azure 備份保存庫 (亦即一律是增量備份)。</span><span class="sxs-lookup"><span data-stu-id="527fa-136">If first backup is completed, on-demand backup will only send changes from previous backup to Azure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="527fa-137">隨選備份的保留範圍，已設定為在與 VM 對應之備份原則中針對每日保留指定的保留值。</span><span class="sxs-lookup"><span data-stu-id="527fa-137">Retention range of an on-demand backup is set to retention value specified for Daily retention in backup policy corresponding to the VM.</span></span>  
>
>

<span data-ttu-id="527fa-138">若要進行虛擬機器的隨選備份：</span><span class="sxs-lookup"><span data-stu-id="527fa-138">To take an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="527fa-139">瀏覽至 [受保護的項目] 頁面，並選取 [Azure 虛擬機器] 做為 [類型] \(若尚未選取)，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527fa-139">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="527fa-141">選取您要進行隨選備份的虛擬機器，然後按一下頁面底部的 [ **立即備份** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527fa-141">Select the virtual machine on which you want to take an on-demand backup and click on **Backup Now** button at the bottom of the page.</span></span>

    ![立即備份](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="527fa-143">這會在所選的虛擬機器上建立備份作業。</span><span class="sxs-lookup"><span data-stu-id="527fa-143">This will create a backup job on the selected virtual machine.</span></span> <span data-ttu-id="527fa-144">透過這項作業建立的復原點保留範圍，將會與在虛擬機器相關原則中指定的保留範圍相同。</span><span class="sxs-lookup"><span data-stu-id="527fa-144">Retention range of recovery point created through this job will be same as that specified in the policy associated with the virtual machine.</span></span>

    ![建立備份作業](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="527fa-146">若要檢視與虛擬機器相關聯的原則，請向下切入到 [ **受保護項目** ] 頁面中的虛擬機器，並移至 [備份原則] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="527fa-146">To view the policy associated with a virtual machine, drill down into virtual machine in the **Protected Items** page and go to backup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="527fa-147">建立作業之後，您可以按一下快顯通知列中的 [ **檢視作業** ]，以在 [作業] 頁面中查看對應的作業。</span><span class="sxs-lookup"><span data-stu-id="527fa-147">Once the job is created, you can click on **View job** button in the toast bar to see the corresponding job in the jobs page.</span></span>

    ![建立的備份作業](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="527fa-149">順利完成作業之後，將會建立可供您還原虛擬機器的復原點。</span><span class="sxs-lookup"><span data-stu-id="527fa-149">After successful completion of the job, a recovery point will be created which you can use to restore the virtual machine.</span></span> <span data-ttu-id="527fa-150">這也會使 [ **受保護項目** ] 頁面中 的復原點資料行值遞增 1。</span><span class="sxs-lookup"><span data-stu-id="527fa-150">This will also increment the recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="527fa-151">停止保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="527fa-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="527fa-152">您可以透過下列選項，選擇停止虛擬機器的未來備份：</span><span class="sxs-lookup"><span data-stu-id="527fa-152">You can choose to stop the future backups of a virtual machine with the following options:</span></span>

* <span data-ttu-id="527fa-153">保留 Azure 備份保存庫中與虛擬機器相關聯的備份資料</span><span class="sxs-lookup"><span data-stu-id="527fa-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="527fa-154">刪除與虛擬機器相關聯的備份資料</span><span class="sxs-lookup"><span data-stu-id="527fa-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="527fa-155">如果您選取保留與虛擬機器相關聯的備份資料，您可以使用備份資料還原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="527fa-155">If you have selected to retain backup data associated with virtual machine, you can use the backup data to restore the virtual machine.</span></span> <span data-ttu-id="527fa-156">如需這類虛擬機器的定價詳細資訊，請按一下 [這裡](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="527fa-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="527fa-157">若要停止虛擬機器的保護：</span><span class="sxs-lookup"><span data-stu-id="527fa-157">To Stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="527fa-158">瀏瀏覽至 [受保護的項目] 頁面，並選取 [Azure 虛擬機器] 作為篩選類型 (若尚未選取)，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527fa-158">Navigate to **Protected Items** page and select **Azure virtual machine** as the filter type (if not already selected) and click on **Select** button.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="527fa-160">選取虛擬機器，然後按一下頁面底部的 [ **停止保護** ]。</span><span class="sxs-lookup"><span data-stu-id="527fa-160">Select the virtual machine and click on **Stop Protection** at the bottom of the page.</span></span>

    ![停止保護](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="527fa-162">根據預設，Azure 備份不會刪除與虛擬機器相關聯的備份資料。</span><span class="sxs-lookup"><span data-stu-id="527fa-162">By default, Azure Backup doesn’t delete the backup data associated with the virtual machine.</span></span>

    ![確認停止保護](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="527fa-164">如果您要刪除備份資料，請選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="527fa-164">If you want to delete backup data, select the check box.</span></span>

    ![核取方塊](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="527fa-166">請選取停止備份的原因。</span><span class="sxs-lookup"><span data-stu-id="527fa-166">Please select a reason for stopping the backup.</span></span> <span data-ttu-id="527fa-167">雖然這是選擇性動作，但提供原因可幫助 Azure 備份處理意見反應，並設定客戶案例的優先順序。</span><span class="sxs-lookup"><span data-stu-id="527fa-167">While this is optional, providing a reason will help Azure Backup to work on the feedback and prioritize the customer scenarios.</span></span>
4. <span data-ttu-id="527fa-168">按一下 [提交] 按鈕以提交 [停止保護] 作業。</span><span class="sxs-lookup"><span data-stu-id="527fa-168">Click on **Submit** button to submit the **Stop protection** job.</span></span> <span data-ttu-id="527fa-169">按一下 [檢視作業] 以在 [作業] 頁面中查看對應作業。</span><span class="sxs-lookup"><span data-stu-id="527fa-169">Click on **View Job** to see the corresponding the job in **Jobs** page.</span></span>

    ![停止保護](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="527fa-171">如果您未在 [停止保護] 精靈中選取 [刪除相關聯的備份資料] 選項，然後在作業完成後，保護狀態會變更為 [已停止保護]。</span><span class="sxs-lookup"><span data-stu-id="527fa-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes to **Protection Stopped**.</span></span> <span data-ttu-id="527fa-172">資料將會使用 Azure 備份保留，直到被明確刪除為止。</span><span class="sxs-lookup"><span data-stu-id="527fa-172">The data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="527fa-173">您隨時都可藉由在 [受保護的項目] 頁面中選取虛擬機器，然後按一下 [刪除] 來刪除資料。</span><span class="sxs-lookup"><span data-stu-id="527fa-173">You can always delete the data by selecting the virtual machine in the **Protected Items** page and clicking **Delete**.</span></span>

    ![已停止保護](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="527fa-175">若您已選取 [刪除相關聯的備份資料] 選項，則虛擬機器將不會出現在 [受保護的項目] 頁面中。</span><span class="sxs-lookup"><span data-stu-id="527fa-175">If you have selected the **Delete associated backup data** option, the virtual machine won’t be part of the **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="527fa-176">重新保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="527fa-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="527fa-177">如果您未選取 [停止保護] 中的 [刪除相關聯的備份資料] 選項，您可以遵循類似於備份已註冊虛擬機器的步驟，重新保護虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="527fa-177">If you have not selected the **Delete associate backup data** option in **Stop Protection**, you can re-protect the virtual machine by following the steps similar to backing up registered virtual machines.</span></span> <span data-ttu-id="527fa-178">一旦受保護，此虛擬機器會在停止保護之前保留備份資料，而在重新保護之後建立復原點。</span><span class="sxs-lookup"><span data-stu-id="527fa-178">Once protected, this virtual machine will have backup data retained prior to stop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="527fa-179">重新保護之後，如果有 [停止保護] 之前的復原點，則虛擬機器的保護狀態會變更為 [受保護]。</span><span class="sxs-lookup"><span data-stu-id="527fa-179">After re-protect, the virtual machine’s protection status will be changed to **Protected** if there are recovery points prior to **Stop Protection**.</span></span>

  ![重新保護的 VM](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="527fa-181">重新保護虛擬機器時，您可以選擇與最初用於保護虛擬機器不同的原則。</span><span class="sxs-lookup"><span data-stu-id="527fa-181">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="527fa-182">取消註冊虛擬機器</span><span class="sxs-lookup"><span data-stu-id="527fa-182">Unregister virtual machines</span></span>
<span data-ttu-id="527fa-183">如果您想要從備份保存庫移除虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="527fa-183">If you want to remove the virtual machine from the backup vault:</span></span>

1. <span data-ttu-id="527fa-184">按一下頁面底部的 [ **取消註冊** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527fa-184">Click on the **UNREGISTER** button at the bottom of the page.</span></span>

    ![停用保護](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="527fa-186">快顯通知會出現在畫面底部要求確認。</span><span class="sxs-lookup"><span data-stu-id="527fa-186">A toast notification will appear at the bottom of the screen requesting confirmation.</span></span> <span data-ttu-id="527fa-187">按一下 [ **是** ] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="527fa-187">Click **YES** to continue.</span></span>

    ![停用保護](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="527fa-189">刪除備份資料</span><span class="sxs-lookup"><span data-stu-id="527fa-189">Delete Backup data</span></span>
<span data-ttu-id="527fa-190">您可以刪除與虛擬機器相關聯的備份資料：</span><span class="sxs-lookup"><span data-stu-id="527fa-190">You can delete the backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="527fa-191">在停止保護作業期間</span><span class="sxs-lookup"><span data-stu-id="527fa-191">During Stop Protection Job</span></span>
* <span data-ttu-id="527fa-192">在虛擬機器上完成停止保護作業之後</span><span class="sxs-lookup"><span data-stu-id="527fa-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="527fa-193">針對在順利完成 [停止備份] 作業後處於 [已停止保護] 狀態的虛擬機器，若要刪除其中的備份資料：</span><span class="sxs-lookup"><span data-stu-id="527fa-193">To delete backup data on a virtual machine, which is in the *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="527fa-194">瀏覽至 [受保護的項目] 頁面，並選取 [Azure 虛擬機器] 做為*類型*，然後按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="527fa-194">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as *type* and click the **Select** button.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="527fa-196">選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="527fa-196">Select the virtual machine.</span></span> <span data-ttu-id="527fa-197">虛擬機器會處於 [ **已停止保護** ] 狀態。</span><span class="sxs-lookup"><span data-stu-id="527fa-197">The virtual machine will be in **Protection Stopped** state.</span></span>

    ![已停止保護](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="527fa-199">按一下頁面底部的 [刪除]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="527fa-199">Click the **DELETE** button at the bottom of the page.</span></span>

    ![刪除備份](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="527fa-201">在 [刪除備份資料] 精靈中，選取刪除備份資料的原因 (強烈建議)，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="527fa-201">In the **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![刪除備份資料](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="527fa-203">這會建立一項作業以刪除所選虛擬機器的備份資料。</span><span class="sxs-lookup"><span data-stu-id="527fa-203">This will create a job to delete backup data of selected virtual machine.</span></span> <span data-ttu-id="527fa-204">按一下 [檢視作業]  以在 [作業] 頁面中查看對應作業。</span><span class="sxs-lookup"><span data-stu-id="527fa-204">Click **View job** to see corresponding job in Jobs page.</span></span>

    ![成功刪除資料](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="527fa-206">完成此作業後，將從 [受保護項目]  頁面中移除虛擬機器的對應項目。</span><span class="sxs-lookup"><span data-stu-id="527fa-206">Once the job is completed, the entry corresponding to the virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="527fa-207">儀表板</span><span class="sxs-lookup"><span data-stu-id="527fa-207">Dashboard</span></span>
<span data-ttu-id="527fa-208">在 [ **儀表板** ] 頁面中，您可以檢閱有關 Azure 虛擬機器、其儲存體和過去 24 小時內相關聯作業的資訊。</span><span class="sxs-lookup"><span data-stu-id="527fa-208">On the **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in the last 24 hours.</span></span> <span data-ttu-id="527fa-209">您可以檢視備份狀態和任何相關聯的備份錯誤。</span><span class="sxs-lookup"><span data-stu-id="527fa-209">You can view backup status and any associated backup errors.</span></span>

![儀表板](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="527fa-211">儀表板中的值會每隔 24 小時重新整理一次。</span><span class="sxs-lookup"><span data-stu-id="527fa-211">Values in the dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="527fa-212">稽核作業</span><span class="sxs-lookup"><span data-stu-id="527fa-212">Auditing Operations</span></span>
<span data-ttu-id="527fa-213">Azure 備份提供由客戶觸發之備份作業的「作業記錄檔」檢閱，可輕鬆查看備份保存庫上執行了哪些管理作業。</span><span class="sxs-lookup"><span data-stu-id="527fa-213">Azure backup provides review of the "operation logs" of backup operations triggered by the customer making it easy to see exactly what management operations were performed on the backup vault.</span></span> <span data-ttu-id="527fa-214">作業記錄檔會啟用備份作業的絕佳事後剖析和稽核支援。</span><span class="sxs-lookup"><span data-stu-id="527fa-214">Operations logs enable great post-mortem and audit support for the backup operations.</span></span>

<span data-ttu-id="527fa-215">作業記錄檔中會記錄下列作業：</span><span class="sxs-lookup"><span data-stu-id="527fa-215">The following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="527fa-216">註冊</span><span class="sxs-lookup"><span data-stu-id="527fa-216">Register</span></span>
* <span data-ttu-id="527fa-217">Unregister </span><span class="sxs-lookup"><span data-stu-id="527fa-217">Unregister</span></span>
* <span data-ttu-id="527fa-218">設定保護</span><span class="sxs-lookup"><span data-stu-id="527fa-218">Configure protection</span></span>
* <span data-ttu-id="527fa-219">備份 (同時透過 BackupNow 進行排程以及隨選備份)</span><span class="sxs-lookup"><span data-stu-id="527fa-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="527fa-220">還原</span><span class="sxs-lookup"><span data-stu-id="527fa-220">Restore</span></span>
* <span data-ttu-id="527fa-221">停止保護</span><span class="sxs-lookup"><span data-stu-id="527fa-221">Stop protection</span></span>
* <span data-ttu-id="527fa-222">刪除備份資料</span><span class="sxs-lookup"><span data-stu-id="527fa-222">Delete backup data</span></span>
* <span data-ttu-id="527fa-223">Add policy</span><span class="sxs-lookup"><span data-stu-id="527fa-223">Add policy</span></span>
* <span data-ttu-id="527fa-224">刪除原則</span><span class="sxs-lookup"><span data-stu-id="527fa-224">Delete policy</span></span>
* <span data-ttu-id="527fa-225">更新原則</span><span class="sxs-lookup"><span data-stu-id="527fa-225">Update policy</span></span>
* <span data-ttu-id="527fa-226">取消工作</span><span class="sxs-lookup"><span data-stu-id="527fa-226">Cancel job</span></span>

<span data-ttu-id="527fa-227">檢視對應到備份保存庫的作業記錄檔：</span><span class="sxs-lookup"><span data-stu-id="527fa-227">To view operation logs corresponding to a backup vault:</span></span>

1. <span data-ttu-id="527fa-228">瀏覽至 Azure 入口網站中的 [管理服務]，然後按一下 [作業記錄檔] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="527fa-228">Navigate to **Management services** in Azure portal, and then click the **Operation Logs** tab.</span></span>

    ![作業記錄](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="527fa-230">在篩選器中，選取 [備份] 做為*類型*，指定*服務名稱*中的備份保存庫名稱，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="527fa-230">In the filters, select **Backup** as *Type* and specify the backup vault name in *service name* and click on **Submit**.</span></span>

    ![作業記錄檔篩選器](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="527fa-232">在作業記錄檔中選取任一作業，然後按一下 [詳細資料] 以查看對應至作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="527fa-232">In the operations logs, select any operation and click  **Details** to see details corresponding to an operation.</span></span>

    ![作業記錄檔擷取詳細資料](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="527fa-234">**詳細資料精靈** 包含觸發的作業、工作識別碼、觸發作業所在的資源，以及作業的開始時間等相關資訊。</span><span class="sxs-lookup"><span data-stu-id="527fa-234">The **Details wizard** contains information about the operation triggered, job Id, resource on which this operation is triggered, and start time of the operation.</span></span>

    ![Operation Details](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="527fa-236">警示通知</span><span class="sxs-lookup"><span data-stu-id="527fa-236">Alert notifications</span></span>
<span data-ttu-id="527fa-237">您可以在入口網站取得工作的自訂警示通知。</span><span class="sxs-lookup"><span data-stu-id="527fa-237">You can get custom alert notifications for the jobs in portal.</span></span> <span data-ttu-id="527fa-238">這是藉由在作業記錄檔事件中定義以 PowerShell 為基礎的警示規則來達成。</span><span class="sxs-lookup"><span data-stu-id="527fa-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="527fa-239">我們建議使用「PowerShell 1.3.0 版或更新版本」 。</span><span class="sxs-lookup"><span data-stu-id="527fa-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="527fa-240">若要定義自訂通知以警示備份失敗，範例命令看起來像：</span><span class="sxs-lookup"><span data-stu-id="527fa-240">To define a custom notification to alert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="527fa-241">**ResourceId**：您可從以上章節所述的 [作業記錄檔] 快顯視窗中取得。</span><span class="sxs-lookup"><span data-stu-id="527fa-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="527fa-242">作業之詳細資料快顯視窗中的 ResourceUri 是要提供給此 Cmdlet 的 ResourceId。</span><span class="sxs-lookup"><span data-stu-id="527fa-242">ResourceUri in details popup window of an operation is the ResourceId to be supplied for this cmdlet.</span></span>

<span data-ttu-id="527fa-243">**OperationName**：其格式將會是 "Microsoft.Backup/backupvault/<EventName>"，其中 EventName 為以下任一值：Register、Unregister、ConfigureProtection、Backup、Restore、StopProtection、DeleteBackupData、CreateProtectionPolicy、DeleteProtectionPolicy、UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="527fa-243">**OperationName**: This will be of the format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="527fa-244">**狀態**：支援的值為 - 已開始、成功和失敗。</span><span class="sxs-lookup"><span data-stu-id="527fa-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="527fa-245">**ResourceGroup**：觸發作業所在的資源 ResourceGroup。</span><span class="sxs-lookup"><span data-stu-id="527fa-245">**ResourceGroup**:ResourceGroup of the resource on which operation is triggered.</span></span> <span data-ttu-id="527fa-246">您可以從 ResourceId 值加以取得。</span><span class="sxs-lookup"><span data-stu-id="527fa-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="527fa-247">在 ResourceId 值中，介於欄位 */resourceGroups/* 和 */providers/* 之間的值即為 ResourceGroup 的值。</span><span class="sxs-lookup"><span data-stu-id="527fa-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is the value for ResourceGroup.</span></span>

<span data-ttu-id="527fa-248">**名稱**：警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="527fa-248">**Name**: Name of the Alert Rule.</span></span>

<span data-ttu-id="527fa-249">**CustomEmail**：指定您要傳送警示通知的自訂電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="527fa-249">**CustomEmail**: Specify the custom email address to which you want to send alert notification</span></span>

<span data-ttu-id="527fa-250">**SendToServiceOwners**：此選項會將警示通知傳送給訂用帳戶的所有系統管理員和共同管理員。</span><span class="sxs-lookup"><span data-stu-id="527fa-250">**SendToServiceOwners**: This option sends alert notification to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="527fa-251">它可以用於 **New-AzureRmAlertRuleEmail** Cmdlet 中</span><span class="sxs-lookup"><span data-stu-id="527fa-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="527fa-252">警示的限制</span><span class="sxs-lookup"><span data-stu-id="527fa-252">Limitations on Alerts</span></span>
<span data-ttu-id="527fa-253">以事件為基礎的警示受到下列限制：</span><span class="sxs-lookup"><span data-stu-id="527fa-253">Event-based alerts are subjected to the following limitations:</span></span>

1. <span data-ttu-id="527fa-254">在備份保存庫中的所有虛擬機器上觸發警示。</span><span class="sxs-lookup"><span data-stu-id="527fa-254">Alerts are triggered on all virtual machines in the backup vault.</span></span> <span data-ttu-id="527fa-255">您無法自訂它以取得備份保存庫中特定一組虛擬機器的警示。</span><span class="sxs-lookup"><span data-stu-id="527fa-255">You cannot customize it to get alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="527fa-256">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="527fa-256">This feature is in Preview.</span></span> [<span data-ttu-id="527fa-257">深入了解</span><span class="sxs-lookup"><span data-stu-id="527fa-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="527fa-258">您將會收到來自 "alerts-noreply@mail.windowsazure.com" 的警示。</span><span class="sxs-lookup"><span data-stu-id="527fa-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="527fa-259">目前您無法修改電子郵件寄件者。</span><span class="sxs-lookup"><span data-stu-id="527fa-259">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="527fa-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="527fa-260">Next steps</span></span>
* [<span data-ttu-id="527fa-261">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="527fa-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
