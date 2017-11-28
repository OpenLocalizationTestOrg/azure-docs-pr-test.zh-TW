---
title: "aaaManage 和監視 Azure 虛擬機器備份 |Microsoft 文件"
description: "了解如何 toomanage 和監視 Azure 虛擬機器的備份"
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
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="a4910-103">管理一般的 Azure 備份作業與 hello 傳統入口網站中的觸發程序警示</span><span class="sxs-lookup"><span data-stu-id="a4910-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4910-104">管理 Azure VM 備份</span><span class="sxs-lookup"><span data-stu-id="a4910-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="a4910-105">管理傳統 VM 備份</span><span class="sxs-lookup"><span data-stu-id="a4910-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="a4910-106">本文針對 Azure 中受保護的傳統模型虛擬機器，提供一般管理和監視工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a4910-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="a4910-107">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a4910-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a4910-108">請參閱[準備 Azure 虛擬機器註冊您的環境 tooback](backup-azure-vms-prepare.md)如需詳細資訊，使用傳統部署模型的 Vm。</span><span class="sxs-lookup"><span data-stu-id="a4910-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="a4910-109">從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="a4910-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="a4910-110">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a4910-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="a4910-111">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="a4910-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="a4910-112">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a4910-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="a4910-113">2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="a4910-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="a4910-114">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="a4910-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="a4910-115">所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a4910-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="a4910-116">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="a4910-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="a4910-117">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="a4910-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="a4910-118">管理受保護的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a4910-118">Manage protected virtual machines</span></span>
<span data-ttu-id="a4910-119">toomanage 受保護的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="a4910-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="a4910-120">tooview 及管理備份設定，如虛擬機器按一下 [hello**受保護項目**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a4910-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="a4910-121">按一下 受保護項目的 toosee hello hello 名稱**備份詳細資料**索引標籤上，它會顯示 hello 上次備份的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a4910-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![虛擬機器備份](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="a4910-123">tooview 和管理備份原則設定，如虛擬機器按一下 [hello**原則**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a4910-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![虛擬機器原則](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="a4910-125">hello**備份原則**索引標籤上顯示 hello 現有的原則。</span><span class="sxs-lookup"><span data-stu-id="a4910-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="a4910-126">您可以視需要修改。</span><span class="sxs-lookup"><span data-stu-id="a4910-126">You can modify as needed.</span></span> <span data-ttu-id="a4910-127">如果您需要新的原則 toocreate 按一下**建立**上 hello**原則**頁面。</span><span class="sxs-lookup"><span data-stu-id="a4910-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="a4910-128">請注意，如果您想 tooremove 原則它不應該與它相關聯的任何虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a4910-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![虛擬機器原則](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="a4910-130">取得 hello 上的虛擬機器的動作或狀態的相關資訊**作業**頁面。</span><span class="sxs-lookup"><span data-stu-id="a4910-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="a4910-131">更多詳細資料或篩選的工作特定的虛擬機器，請按一下 hello 清單 tooget 中的工作。</span><span class="sxs-lookup"><span data-stu-id="a4910-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![工作](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="a4910-133">虛擬機器的隨選備份</span><span class="sxs-lookup"><span data-stu-id="a4910-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="a4910-134">設定保護後，您可以執行虛擬機器的隨選備份。</span><span class="sxs-lookup"><span data-stu-id="a4910-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="a4910-135">如果暫止 hello 初始備份 hello 虛擬機器，隨備份將會在 Azure 備份保存庫中建立 hello 虛擬機器的完整複本。</span><span class="sxs-lookup"><span data-stu-id="a4910-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="a4910-136">如果第一次備份完成時，備份將會隨僅傳送變更，從上一次備份 tooAzure 備份保存庫也就是它一律為增量。</span><span class="sxs-lookup"><span data-stu-id="a4910-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="a4910-137">視備份的保留範圍設定為指定的備份原則對應 toohello VM 中的每日保留期 tooretention 值。</span><span class="sxs-lookup"><span data-stu-id="a4910-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="a4910-138">虛擬機器的 tootake 隨備份：</span><span class="sxs-lookup"><span data-stu-id="a4910-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="a4910-139">瀏覽 toohello**受保護項目**頁面，然後選取**Azure 虛擬機器**為**類型**（如果尚未選取），然後按一下 [**選取**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4910-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="a4910-141">選取 hello 虛擬機器的方法，您可以想 tootake 隨備份，然後按一下**立即備份**在 hello hello 頁面底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4910-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![立即備份](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="a4910-143">這會在 hello 選取虛擬機器上建立備份作業。</span><span class="sxs-lookup"><span data-stu-id="a4910-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="a4910-144">透過這項作業所建立的復原點的保留範圍將會與 hello hello 虛擬機器相關聯的原則中指定相同的。</span><span class="sxs-lookup"><span data-stu-id="a4910-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![建立備份作業](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="a4910-146">tooview hello 原則相關聯的虛擬機器，向下切入向下 hello 中的虛擬機器到**受保護項目**頁面和移 toobackup 原則 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a4910-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="a4910-147">Hello 工作建立之後，您可以按一下**檢視工作**中列 toosee hello 相對應的工作 hello 作業 頁面中的 hello 快顯的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4910-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![建立的備份作業](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="a4910-149">Hello 工作順利完成之後, 建立復原點將會是您可以使用 toorestore hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a4910-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="a4910-150">這也會增加 hello 復原點的資料行值中的 1**受保護項目**頁面。</span><span class="sxs-lookup"><span data-stu-id="a4910-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="a4910-151">停止保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a4910-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="a4910-152">您可以選擇 toostop hello 未來備份的虛擬機器，以 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="a4910-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="a4910-153">保留 Azure 備份保存庫中與虛擬機器相關聯的備份資料</span><span class="sxs-lookup"><span data-stu-id="a4910-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="a4910-154">刪除與虛擬機器相關聯的備份資料</span><span class="sxs-lookup"><span data-stu-id="a4910-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="a4910-155">如果您已經選取 tooretain 備份虛擬機器相關聯的資料，您可以使用 hello 備份資料 toorestore hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a4910-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="a4910-156">如需這類虛擬機器的定價詳細資訊，請按一下 [這裡](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="a4910-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="a4910-157">tooStop 虛擬機器的保護：</span><span class="sxs-lookup"><span data-stu-id="a4910-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="a4910-158">瀏覽過**受保護項目**頁面，然後選取**Azure 虛擬機器**當做 hello 篩選類型 （如果尚未選取），並按一下**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4910-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="a4910-160">選取 hello 虛擬機器，然後按一下 **停止保護**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="a4910-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![停止保護](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="a4910-162">根據預設，Azure Backup 不會刪除 hello hello 虛擬機器相關聯的備份資料。</span><span class="sxs-lookup"><span data-stu-id="a4910-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![確認停止保護](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="a4910-164">如果您想 toodelete 備份資料，請選取 [hello] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a4910-164">If you want toodelete backup data, select hello check box.</span></span>

    ![核取方塊](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="a4910-166">請選擇停止 hello 備份的原因。</span><span class="sxs-lookup"><span data-stu-id="a4910-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="a4910-167">雖然這是選擇性的則提供原因將會協助 Azure Backup toowork hello 的意見反應並優先處理 hello 客戶案例。</span><span class="sxs-lookup"><span data-stu-id="a4910-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="a4910-168">按一下**送出**按鈕 toosubmit hello**停止保護**作業。</span><span class="sxs-lookup"><span data-stu-id="a4910-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="a4910-169">按一下**檢視工作**toosee hello 中相對應的 hello 工作**作業**頁面。</span><span class="sxs-lookup"><span data-stu-id="a4910-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![停止保護](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="a4910-171">如果您沒有選取**刪除相關聯的備份資料**選項期間**停止保護**精靈，然後 post 作業完成時，保護狀態會變更太**停止保護**.</span><span class="sxs-lookup"><span data-stu-id="a4910-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="a4910-172">hello 資料維持向 Azure 備份，直到明確刪除。</span><span class="sxs-lookup"><span data-stu-id="a4910-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="a4910-173">您隨時都可以刪除 hello 資料選取 hello 虛擬機器在 hello**受保護項目**頁面，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="a4910-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![已停止保護](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="a4910-175">如果您已選取 hello**刪除相關聯的備份資料**選項，hello 虛擬機器將不會屬於 hello**受保護項目**頁面。</span><span class="sxs-lookup"><span data-stu-id="a4910-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="a4910-176">重新保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a4910-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="a4910-177">如果您沒有選取 hello**刪除關聯的備份資料**選項**停止保護**，之後，您可以重新保護 hello 虛擬機器組成 hello 步驟類似 toobacking 註冊虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a4910-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="a4910-178">受保護，此虛擬機器會具有保留的備份資料先前 toostop 保護並且之後建立復原點之後重新保護。</span><span class="sxs-lookup"><span data-stu-id="a4910-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="a4910-179">之後再重新執行保護，hello 虛擬機器的保護狀態就會變更太**保護**如果太前一個復原點**停止保護**。</span><span class="sxs-lookup"><span data-stu-id="a4910-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![重新保護的 VM](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="a4910-181">當重新保護 hello 虛擬機器時，您可以選擇不同的原則，小於 hello 原則與虛擬機器已受保護一開始。</span><span class="sxs-lookup"><span data-stu-id="a4910-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="a4910-182">取消註冊虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a4910-182">Unregister virtual machines</span></span>
<span data-ttu-id="a4910-183">若要從備份保存庫 hello tooremove hello 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="a4910-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="a4910-184">按一下 hello**取消註冊**在 hello hello 頁面底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4910-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![停用保護](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="a4910-186">快顯通知會出現在 hello 要求確認囉 」 畫面底部。</span><span class="sxs-lookup"><span data-stu-id="a4910-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="a4910-187">按一下**是**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="a4910-187">Click **YES** toocontinue.</span></span>

    ![停用保護](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="a4910-189">刪除備份資料</span><span class="sxs-lookup"><span data-stu-id="a4910-189">Delete Backup data</span></span>
<span data-ttu-id="a4910-190">您可以刪除 hello 與虛擬機器，可能是相關聯的備份資料：</span><span class="sxs-lookup"><span data-stu-id="a4910-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="a4910-191">在停止保護作業期間</span><span class="sxs-lookup"><span data-stu-id="a4910-191">During Stop Protection Job</span></span>
* <span data-ttu-id="a4910-192">在虛擬機器上完成停止保護作業之後</span><span class="sxs-lookup"><span data-stu-id="a4910-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="a4910-193">toodelete hello 中的虛擬機器的備份資料*停止保護*狀態張貼成功完成**停止備份**作業：</span><span class="sxs-lookup"><span data-stu-id="a4910-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="a4910-194">瀏覽 toohello**受保護項目**頁面，然後選取**Azure 虛擬機器**為*類型*按一下 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4910-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="a4910-196">選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a4910-196">Select hello virtual machine.</span></span> <span data-ttu-id="a4910-197">hello 虛擬機器會處於**停止保護**狀態。</span><span class="sxs-lookup"><span data-stu-id="a4910-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![已停止保護](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="a4910-199">按一下 hello**刪除**在 hello hello 頁面底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4910-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![刪除備份](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="a4910-201">在 [hello**刪除備份資料**精靈] 中，選取刪除 （強烈建議） 備份資料的原因，然後按一下**送出**。</span><span class="sxs-lookup"><span data-stu-id="a4910-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![刪除備份資料](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="a4910-203">這會建立選取的虛擬機器作業 toodelete 備份資料。</span><span class="sxs-lookup"><span data-stu-id="a4910-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="a4910-204">按一下**檢視工作**toosee 作業 頁面中相對應的工作。</span><span class="sxs-lookup"><span data-stu-id="a4910-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![成功刪除資料](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="a4910-206">Hello 作業完成後，hello 對應 toohello 虛擬機器會移除的項目**受保護項目**頁面。</span><span class="sxs-lookup"><span data-stu-id="a4910-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="a4910-207">儀表板</span><span class="sxs-lookup"><span data-stu-id="a4910-207">Dashboard</span></span>
<span data-ttu-id="a4910-208">在 hello**儀表板**頁面上，您可以檢閱 Azure 虛擬機器、 儲存和與其相關聯 hello 在過去 24 小時內的工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a4910-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="a4910-209">您可以檢視備份狀態和任何相關聯的備份錯誤。</span><span class="sxs-lookup"><span data-stu-id="a4910-209">You can view backup status and any associated backup errors.</span></span>

![儀表板](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="a4910-211">Hello 儀表板中的值，就會重新整理一次每隔 24 小時。</span><span class="sxs-lookup"><span data-stu-id="a4910-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="a4910-212">稽核作業</span><span class="sxs-lookup"><span data-stu-id="a4910-212">Auditing Operations</span></span>
<span data-ttu-id="a4910-213">Azure 備份提供 hello"作業記錄 」 備份作業的 hello 客戶，讓您輕鬆 toosee hello 備份保存庫執行完全管理作業所觸發的檢閱。</span><span class="sxs-lookup"><span data-stu-id="a4910-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="a4910-214">作業記錄檔啟用絕佳的檢討，和稽核 hello 備份作業的支援。</span><span class="sxs-lookup"><span data-stu-id="a4910-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="a4910-215">下列作業的 hello 會記錄在作業記錄：</span><span class="sxs-lookup"><span data-stu-id="a4910-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="a4910-216">註冊</span><span class="sxs-lookup"><span data-stu-id="a4910-216">Register</span></span>
* <span data-ttu-id="a4910-217">Unregister </span><span class="sxs-lookup"><span data-stu-id="a4910-217">Unregister</span></span>
* <span data-ttu-id="a4910-218">設定保護</span><span class="sxs-lookup"><span data-stu-id="a4910-218">Configure protection</span></span>
* <span data-ttu-id="a4910-219">備份 (同時透過 BackupNow 進行排程以及隨選備份)</span><span class="sxs-lookup"><span data-stu-id="a4910-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="a4910-220">還原</span><span class="sxs-lookup"><span data-stu-id="a4910-220">Restore</span></span>
* <span data-ttu-id="a4910-221">停止保護</span><span class="sxs-lookup"><span data-stu-id="a4910-221">Stop protection</span></span>
* <span data-ttu-id="a4910-222">刪除備份資料</span><span class="sxs-lookup"><span data-stu-id="a4910-222">Delete backup data</span></span>
* <span data-ttu-id="a4910-223">Add policy</span><span class="sxs-lookup"><span data-stu-id="a4910-223">Add policy</span></span>
* <span data-ttu-id="a4910-224">刪除原則</span><span class="sxs-lookup"><span data-stu-id="a4910-224">Delete policy</span></span>
* <span data-ttu-id="a4910-225">更新原則</span><span class="sxs-lookup"><span data-stu-id="a4910-225">Update policy</span></span>
* <span data-ttu-id="a4910-226">取消工作</span><span class="sxs-lookup"><span data-stu-id="a4910-226">Cancel job</span></span>

<span data-ttu-id="a4910-227">tooview 作業記錄檔對應 tooa 備份保存庫：</span><span class="sxs-lookup"><span data-stu-id="a4910-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="a4910-228">瀏覽過**管理服務**在 Azure 入口網站，然後按一下hello**作業記錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a4910-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![作業記錄](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="a4910-230">在 hello 篩選條件中，選取**備份**為*類型*hello 備份保存庫中指定名稱和*服務名稱*，然後按一下 **送出**。</span><span class="sxs-lookup"><span data-stu-id="a4910-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![作業記錄檔篩選器](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="a4910-232">Hello 作業記錄檔、 選取任何作業，然後按一下**詳細資料**toosee 詳細說明對應 tooan 作業。</span><span class="sxs-lookup"><span data-stu-id="a4910-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![作業記錄檔擷取詳細資料](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="a4910-234">hello**明細 精靈中**包含 hello 作業觸發，作業識別碼，資源的這項作業會觸發並 hello 作業的開始時間的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a4910-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![Operation Details](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="a4910-236">警示通知</span><span class="sxs-lookup"><span data-stu-id="a4910-236">Alert notifications</span></span>
<span data-ttu-id="a4910-237">您可以在入口網站取得 hello 工作的自訂警示通知。</span><span class="sxs-lookup"><span data-stu-id="a4910-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="a4910-238">這是藉由在作業記錄檔事件中定義以 PowerShell 為基礎的警示規則來達成。</span><span class="sxs-lookup"><span data-stu-id="a4910-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="a4910-239">我們建議使用「PowerShell 1.3.0 版或更新版本」 。</span><span class="sxs-lookup"><span data-stu-id="a4910-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="a4910-240">toodefine 備份失敗的自訂通知 tooalert，範例命令看起來像：</span><span class="sxs-lookup"><span data-stu-id="a4910-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="a4910-241">**ResourceId**：您可從以上章節所述的 [作業記錄檔] 快顯視窗中取得。</span><span class="sxs-lookup"><span data-stu-id="a4910-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="a4910-242">作業的詳細資料快顯視窗中的 ResourceUri 是 hello ResourceId toobe 提供給這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="a4910-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="a4910-243">**OperationName**： 這會是 hello 格式的"Microsoft.Backup/backupvault/<EventName>"其中 EventName 是其中一個暫存器、 取消註冊、 ConfigureProtection、 備份、 還原、 StopProtection、 DeleteBackupData，CreateProtectionPolicy，DeleteProtectionPolicy，UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="a4910-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="a4910-244">**狀態**：支援的值為 - 已開始、成功和失敗。</span><span class="sxs-lookup"><span data-stu-id="a4910-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="a4910-245">**ResourceGroup**: hello 資源在其觸發作業的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a4910-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="a4910-246">您可以從 ResourceId 值加以取得。</span><span class="sxs-lookup"><span data-stu-id="a4910-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="a4910-247">值，欄位之間*/resourceGroups/*和*/providers/* ResourceId 中值為 hello ResourceGroup 值。</span><span class="sxs-lookup"><span data-stu-id="a4910-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="a4910-248">**名稱**: hello 警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="a4910-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="a4910-249">**CustomEmail**： 指定您想要 toosend 警示通知的 hello 自訂電子郵件地址 toowhich</span><span class="sxs-lookup"><span data-stu-id="a4910-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="a4910-250">**SendToServiceOwners**： 這個選項會傳送警示通知 tooall 系統管理員和共同管理員的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4910-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="a4910-251">它可以用於 **New-AzureRmAlertRuleEmail** Cmdlet 中</span><span class="sxs-lookup"><span data-stu-id="a4910-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="a4910-252">警示的限制</span><span class="sxs-lookup"><span data-stu-id="a4910-252">Limitations on Alerts</span></span>
<span data-ttu-id="a4910-253">以事件為基礎的警示會受到 toohello 下列限制：</span><span class="sxs-lookup"><span data-stu-id="a4910-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="a4910-254">Hello 備份保存庫中的所有虛擬機器上便會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="a4910-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="a4910-255">您無法自訂 tooget 組特定的備份保存庫中的虛擬機器的警示。</span><span class="sxs-lookup"><span data-stu-id="a4910-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="a4910-256">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="a4910-256">This feature is in Preview.</span></span> [<span data-ttu-id="a4910-257">深入了解</span><span class="sxs-lookup"><span data-stu-id="a4910-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="a4910-258">您將會收到來自 "alerts-noreply@mail.windowsazure.com" 的警示。</span><span class="sxs-lookup"><span data-stu-id="a4910-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="a4910-259">目前您無法修改 hello 電子郵件寄件者。</span><span class="sxs-lookup"><span data-stu-id="a4910-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4910-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4910-260">Next steps</span></span>
* [<span data-ttu-id="a4910-261">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="a4910-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
