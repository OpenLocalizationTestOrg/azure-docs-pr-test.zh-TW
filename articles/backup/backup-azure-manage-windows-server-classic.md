---
title: "使用傳統部署模型管理 Azure 備份保存庫與 Azure 伺服器 | Microsoft Azure"
description: "使用本教學課程了解如何管理 Azure 備份保存庫與伺服器。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 91451b2cdc42ed05ef7c1ba9c66ad5b4b45dd788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="d5817-103">使用傳統部署模型管理 Azure 備份保存庫與伺服器</span><span class="sxs-lookup"><span data-stu-id="d5817-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5817-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="d5817-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="d5817-105">傳統</span><span class="sxs-lookup"><span data-stu-id="d5817-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="d5817-106">在本文中，您將了解透過 Azure 傳統入口網站和 Microsoft Azure 備份代理程式提供之備份管理工作的概觀。</span><span class="sxs-lookup"><span data-stu-id="d5817-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5817-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d5817-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d5817-108">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="d5817-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d5817-109">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="d5817-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5817-110">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="d5817-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="d5817-111">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="d5817-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="d5817-112">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="d5817-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="d5817-113">在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="d5817-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="d5817-114">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="d5817-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="d5817-115">所有其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="d5817-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="d5817-116">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="d5817-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="d5817-117">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="d5817-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="d5817-118">管理入口網站工作</span><span class="sxs-lookup"><span data-stu-id="d5817-118">Management portal tasks</span></span>
1. <span data-ttu-id="d5817-119">登入 [管理入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="d5817-119">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d5817-120">按一下 [復原服務] ，然後按一下備份保存庫的名稱以檢視 [快速啟動] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d5817-120">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![復原服務](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="d5817-122">藉由選取 [快速啟動] 頁面頂端的選項，您可以看到可用的管理工作。</span><span class="sxs-lookup"><span data-stu-id="d5817-122">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![管理索引標籤](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="d5817-124">儀表板</span><span class="sxs-lookup"><span data-stu-id="d5817-124">Dashboard</span></span>
<span data-ttu-id="d5817-125">選取 [儀表板] 以查看伺服器的使用量概觀。</span><span class="sxs-lookup"><span data-stu-id="d5817-125">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="d5817-126">**使用量概觀**包括︰</span><span class="sxs-lookup"><span data-stu-id="d5817-126">The **usage overview** includes:</span></span>

* <span data-ttu-id="d5817-127">已向雲端註冊的 Windows Server 數目</span><span class="sxs-lookup"><span data-stu-id="d5817-127">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="d5817-128">雲端中受保護的 Azure 虛擬機器數目</span><span class="sxs-lookup"><span data-stu-id="d5817-128">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="d5817-129">Azure 中已使用的儲存體總計</span><span class="sxs-lookup"><span data-stu-id="d5817-129">The total storage consumed in Azure</span></span>
* <span data-ttu-id="d5817-130">最近的工作狀態</span><span class="sxs-lookup"><span data-stu-id="d5817-130">The status of recent jobs</span></span>

<span data-ttu-id="d5817-131">您可以在儀表板下方執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="d5817-131">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="d5817-132">**管理憑證** - 如果已使用憑證註冊伺服器，則可使用這個選項來更新憑證。</span><span class="sxs-lookup"><span data-stu-id="d5817-132">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="d5817-133">如果使用保存庫認證，則請勿使用 [管理憑證] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="d5817-134">**刪除** - 刪除目前的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="d5817-134">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="d5817-135">如果您有不再使用的備份保存庫，可將之刪除來釋出儲存空間。</span><span class="sxs-lookup"><span data-stu-id="d5817-135">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="d5817-136">**刪除** 才會啟用。</span><span class="sxs-lookup"><span data-stu-id="d5817-136">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![備份儀表板工作](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="d5817-138">已註冊的項目</span><span class="sxs-lookup"><span data-stu-id="d5817-138">Registered items</span></span>
<span data-ttu-id="d5817-139">選取 [已註冊的項目]  ，以檢視已註冊至此保存庫的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="d5817-139">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![已註冊的項目](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="d5817-141">**類型** 篩選預設為 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d5817-141">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="d5817-142">若要檢視已註冊至此保存庫的伺服器名稱，可從下拉式功能表中選取 [Windows Server]  。</span><span class="sxs-lookup"><span data-stu-id="d5817-142">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="d5817-143">您可以在其中執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="d5817-143">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="d5817-144">**允許重新註冊** - 為伺服器選取此選項時，您可以使用內部部署 Microsoft Azure 備份代理程式中的**註冊精靈**，再次向備份保存庫註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="d5817-144">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="d5817-145">如果憑證中有錯誤，或必須重建伺服器，您可能需要重新註冊。</span><span class="sxs-lookup"><span data-stu-id="d5817-145">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="d5817-146">**刪除** - 從備份保存庫中刪除伺服器。</span><span class="sxs-lookup"><span data-stu-id="d5817-146">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="d5817-147">所有與該伺服器相關聯的已儲存資料都將立即刪除。</span><span class="sxs-lookup"><span data-stu-id="d5817-147">All of the stored data associated with the server is deleted immediately.</span></span>

    ![已註冊的項目工作](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="d5817-149">受保護項目</span><span class="sxs-lookup"><span data-stu-id="d5817-149">Protected items</span></span>
<span data-ttu-id="d5817-150">選取 [受保護項目]  ，以檢視已從伺服器備份的項目。</span><span class="sxs-lookup"><span data-stu-id="d5817-150">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![受保護項目](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="d5817-152">設定</span><span class="sxs-lookup"><span data-stu-id="d5817-152">Configure</span></span>
<span data-ttu-id="d5817-153">從 [設定]  索引標籤，您可以選取適當的儲存體備援選項。</span><span class="sxs-lookup"><span data-stu-id="d5817-153">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="d5817-154">選取儲存體備援選項的最佳時機，就在建立保存庫之後，以及任何電腦註冊至保存庫之前。</span><span class="sxs-lookup"><span data-stu-id="d5817-154">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> <span data-ttu-id="d5817-155">一旦項目已註冊至保存庫，儲存體備援選項即遭到鎖定且無法修改。</span><span class="sxs-lookup"><span data-stu-id="d5817-155">Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.</span></span>
>
>

![設定](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="d5817-157">如需 [儲存體備援](../storage/common/storage-redundancy.md)的詳細資訊，請參閱這篇文章。</span><span class="sxs-lookup"><span data-stu-id="d5817-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="d5817-158">Microsoft Azure 備份代理程式工作</span><span class="sxs-lookup"><span data-stu-id="d5817-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="d5817-159">主控台</span><span class="sxs-lookup"><span data-stu-id="d5817-159">Console</span></span>
<span data-ttu-id="d5817-160">開啟 **Microsoft Azure 備份代理程式** (透過在電腦中搜尋「Microsoft Azure 備份」即可找到)。</span><span class="sxs-lookup"><span data-stu-id="d5817-160">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![備份代理程式](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="d5817-162">從可在備份代理程式主控台右側取得的 [動作]  ，您可以執行下列管理工作︰</span><span class="sxs-lookup"><span data-stu-id="d5817-162">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="d5817-163">註冊伺服器</span><span class="sxs-lookup"><span data-stu-id="d5817-163">Register Server</span></span>
* <span data-ttu-id="d5817-164">排程備份</span><span class="sxs-lookup"><span data-stu-id="d5817-164">Schedule Backup</span></span>
* <span data-ttu-id="d5817-165">立即備份</span><span class="sxs-lookup"><span data-stu-id="d5817-165">Back Up now</span></span>
* <span data-ttu-id="d5817-166">變更屬性</span><span class="sxs-lookup"><span data-stu-id="d5817-166">Change Properties</span></span>

![代理程式主控台動作](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="d5817-168">若要 **復原資料**，請參閱 [將檔案還原到 Windows Server 或 Windows 用戶端電腦](backup-azure-restore-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="d5817-168">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="d5817-169">修改現有備份</span><span class="sxs-lookup"><span data-stu-id="d5817-169">Modify an existing backup</span></span>
1. <span data-ttu-id="d5817-170">在 Microsoft Azure 備份代理程式中，按一下 [排程備份] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-170">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="d5817-172">在**排程備份精靈**中，讓 [變更備份項目或時間] 選項保留選取狀態，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d5817-172">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![修改排定的備份](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="d5817-174">如果您想要新增或變更項目，在 [選取要備份的項目] 畫面中按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="d5817-174">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="d5817-175">您也可以在這個精靈頁面中設定 [排除設定]  。</span><span class="sxs-lookup"><span data-stu-id="d5817-175">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="d5817-176">如果您想要排除檔案或檔案類型，請參閱新增 [排除設定](#exclusion-settings)的程序。</span><span class="sxs-lookup"><span data-stu-id="d5817-176">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="d5817-177">選取要備份的檔案和資料夾，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-177">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![新增項目](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="d5817-179">指定 [備份排程]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d5817-179">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="d5817-180">您可以排程每日 (一天最多 3 次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="d5817-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![指定備份排程](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="d5817-182">這篇 [文章](backup-azure-backup-cloud-as-tape.md)中會詳細說明指定備份排程。</span><span class="sxs-lookup"><span data-stu-id="d5817-182">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="d5817-183">選取備份複本的 [保留原則]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d5817-183">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![選取保留原則](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="d5817-185">在 [確認] 畫面上檢閱資訊，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d5817-185">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="d5817-186">當精靈完成 [備份排程] 的建立之後，按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="d5817-186">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="d5817-187">修改保護之後，您可以藉由移至 [工作]  索引標籤並確認變更反映於備份工作中，來確定可正確觸發備份。</span><span class="sxs-lookup"><span data-stu-id="d5817-187">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="d5817-188">啟用網路節流</span><span class="sxs-lookup"><span data-stu-id="d5817-188">Enable Network Throttling</span></span>
<span data-ttu-id="d5817-189">Azure 備份代理程式提供 [節流] 索引標籤，可讓您控制在資料傳輸期間使用網路頻寬的方式。</span><span class="sxs-lookup"><span data-stu-id="d5817-189">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="d5817-190">如果您需要在上班時間內備份資料，但不希望備份程序干擾其他網際網路流量，這樣的控制會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="d5817-190">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="d5817-191">資料傳輸的節流適用於備份和還原活動。</span><span class="sxs-lookup"><span data-stu-id="d5817-191">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="d5817-192">啟用節流︰</span><span class="sxs-lookup"><span data-stu-id="d5817-192">To enable throttling:</span></span>

1. <span data-ttu-id="d5817-193">在**備份代理程式**中，按一下 [變更屬性]。</span><span class="sxs-lookup"><span data-stu-id="d5817-193">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="d5817-194">選取 [啟用備份作業的網際網路頻寬使用節流功能]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d5817-194">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![網路節流](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="d5817-196">一旦啟用節流之後，請指定允許在 [工作時間] 和 [非工作時間] 進行備份資料傳輸的頻寬。</span><span class="sxs-lookup"><span data-stu-id="d5817-196">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="d5817-197">頻寬值從每秒 512 KB (Kbps) 開始，並可高達每秒 1023 MB (Mbps)。</span><span class="sxs-lookup"><span data-stu-id="d5817-197">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="d5817-198">您也可以指定 [工作時間] 的開始和完成時間，以及一週中有哪幾天視為工作天。</span><span class="sxs-lookup"><span data-stu-id="d5817-198">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="d5817-199">指定工作時間以外的時間會視為非工作時間。</span><span class="sxs-lookup"><span data-stu-id="d5817-199">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="d5817-200">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="d5817-201">排除設定</span><span class="sxs-lookup"><span data-stu-id="d5817-201">Exclusion settings</span></span>
1. <span data-ttu-id="d5817-202">開啟 **Microsoft Azure 備份代理程式** (透過在電腦中搜尋「Microsoft Azure 備份」即可找到)。</span><span class="sxs-lookup"><span data-stu-id="d5817-202">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![開啟備份代理程式](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="d5817-204">在 Microsoft Azure 備份代理程式中，按一下 [排程備份] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-204">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="d5817-206">在排程備份精靈中，讓 [變更備份項目或時間] 選項保留選取狀態，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d5817-206">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![修改排程](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="d5817-208">按一下 [排除設定] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-208">Click **Exclusions Settings**.</span></span>

    ![選取要排除的項目](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="d5817-210">按一下 [新增排除] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-210">Click **Add Exclusion**.</span></span>

    ![新增排除項目](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="d5817-212">選取位置，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-212">Select the location and then, click **OK**.</span></span>

    ![選取要排除的位置](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="d5817-214">在 [檔案類型]  欄位中新增副檔名。</span><span class="sxs-lookup"><span data-stu-id="d5817-214">Add the file extension in the **File Type** field.</span></span>

    ![依檔案類型排除](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="d5817-216">新增 .mp3 副檔名</span><span class="sxs-lookup"><span data-stu-id="d5817-216">Adding an .mp3 extension</span></span>

    ![檔案類型範例](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="d5817-218">若要新增其他副檔名，可按一下 [新增排除]  ，然後輸入另一個副檔名 (新增 .jpeg 副檔名)。</span><span class="sxs-lookup"><span data-stu-id="d5817-218">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![另一個檔案類型範例](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="d5817-220">當您已新增所有副檔名之後，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d5817-220">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="d5817-221">按 [下一步] 繼續執行排程備份精靈， 直到出現 [確認] 頁面，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d5817-221">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![排除確認](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="d5817-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5817-223">Next steps</span></span>
* [<span data-ttu-id="d5817-224">從 Azure 還原 Windows Server 或 Windows 用戶端</span><span class="sxs-lookup"><span data-stu-id="d5817-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="d5817-225">若要深入了解 Azure 備份，請參閱 [Azure 備份概觀](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="d5817-225">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="d5817-226">瀏覽 [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="d5817-226">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
