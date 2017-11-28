---
title: "aaaManage Azure 備份保存庫與伺服器 Azure 使用 hello 傳統部署模型 |Microsoft 文件"
description: "使用此教學課程 toolearn toomanage Azure Backup 的保存庫和伺服器。"
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
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="604fd-103">管理 Azure 備份保存庫使用和伺服器 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="604fd-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="604fd-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="604fd-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="604fd-105">傳統</span><span class="sxs-lookup"><span data-stu-id="604fd-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="604fd-106">在本文中，您會發現 hello 備份管理工作可透過 hello Azure 傳統入口網站和 hello Microsoft Azure 備份代理程式的概觀。</span><span class="sxs-lookup"><span data-stu-id="604fd-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="604fd-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="604fd-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="604fd-108">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="604fd-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="604fd-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="604fd-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="604fd-110">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="604fd-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="604fd-111">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="604fd-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="604fd-112">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="604fd-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="604fd-113">2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="604fd-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="604fd-114">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="604fd-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="604fd-115">所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="604fd-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="604fd-116">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="604fd-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="604fd-117">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="604fd-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="604fd-118">管理入口網站工作</span><span class="sxs-lookup"><span data-stu-id="604fd-118">Management portal tasks</span></span>
1. <span data-ttu-id="604fd-119">登入 toohello[管理入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="604fd-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="604fd-120">按一下**復原服務**，然後按一下 [備份保存庫 tooview hello 快速入門] 頁面的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="604fd-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![復原服務](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="604fd-122">藉由選取 hello 選項在 hello hello 快速入門 頁面的頂端，您可以看到 hello 可用的管理工作。</span><span class="sxs-lookup"><span data-stu-id="604fd-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![管理索引標籤](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="604fd-124">儀表板</span><span class="sxs-lookup"><span data-stu-id="604fd-124">Dashboard</span></span>
<span data-ttu-id="604fd-125">選取**儀表板**hello 伺服器 toosee hello 使用量概觀。</span><span class="sxs-lookup"><span data-stu-id="604fd-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="604fd-126">hello**使用量概觀**包括：</span><span class="sxs-lookup"><span data-stu-id="604fd-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="604fd-127">已登錄的 Windows 伺服器的 hello 數 toocloud</span><span class="sxs-lookup"><span data-stu-id="604fd-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="604fd-128">Azure 雲端中受保護的虛擬機器的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="604fd-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="604fd-129">hello Azure 中已使用的總儲存體</span><span class="sxs-lookup"><span data-stu-id="604fd-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="604fd-130">hello 的最近工作的狀態</span><span class="sxs-lookup"><span data-stu-id="604fd-130">hello status of recent jobs</span></span>

<span data-ttu-id="604fd-131">在 hello hello 儀表板底部，您可以執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="604fd-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="604fd-132">**管理憑證**-如果憑證是使用的 tooregister hello 伺服器，請使用此 tooupdate hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="604fd-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="604fd-133">如果使用保存庫認證，則請勿使用 [管理憑證] 。</span><span class="sxs-lookup"><span data-stu-id="604fd-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="604fd-134">**刪除**-刪除 hello 目前備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="604fd-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="604fd-135">如果不再使用備份保存庫，您可以刪除它 toofree 出儲存空間。</span><span class="sxs-lookup"><span data-stu-id="604fd-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="604fd-136">**刪除**hello 保存庫中刪除所有已註冊的伺服器之後，才會啟用。</span><span class="sxs-lookup"><span data-stu-id="604fd-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![備份儀表板工作](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="604fd-138">已註冊的項目</span><span class="sxs-lookup"><span data-stu-id="604fd-138">Registered items</span></span>
<span data-ttu-id="604fd-139">選取**註冊的項目**tooview hello hello 的伺服器名稱註冊 toothis 保存庫。</span><span class="sxs-lookup"><span data-stu-id="604fd-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![已註冊的項目](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="604fd-141">hello**類型**篩選器預設 tooAzure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="604fd-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="604fd-142">tooview hello 名稱 hello 伺服器的已註冊的 toothis 保存庫中，選取**Windows server** hello 從下拉功能表。</span><span class="sxs-lookup"><span data-stu-id="604fd-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="604fd-143">從這裡您可以執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="604fd-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="604fd-144">**允許重新註冊**-時選取此選項的伺服器，您可以使用 hello**登錄精靈**hello 在內部部署 Microsoft Azure 備份代理程式 tooregister hello 伺服器 hello 備份保存庫第二個階段中.</span><span class="sxs-lookup"><span data-stu-id="604fd-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="604fd-145">您可能需要由於 hello 憑證或伺服器是否有 toobe 重建 tooan 錯誤 toore 暫存器。</span><span class="sxs-lookup"><span data-stu-id="604fd-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="604fd-146">**刪除**-從 hello 備份保存庫刪除伺服器。</span><span class="sxs-lookup"><span data-stu-id="604fd-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="604fd-147">所有儲存的 hello hello 伺服器相關聯的資料會立即刪除。</span><span class="sxs-lookup"><span data-stu-id="604fd-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![已註冊的項目工作](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="604fd-149">受保護項目</span><span class="sxs-lookup"><span data-stu-id="604fd-149">Protected items</span></span>
<span data-ttu-id="604fd-150">選取**受保護項目**tooview hello 項目從 hello 伺服器備份。</span><span class="sxs-lookup"><span data-stu-id="604fd-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![受保護項目](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="604fd-152">設定</span><span class="sxs-lookup"><span data-stu-id="604fd-152">Configure</span></span>
<span data-ttu-id="604fd-153">從 hello**設定** 索引標籤，您可以選取 hello 適當的儲存體備援選項。</span><span class="sxs-lookup"><span data-stu-id="604fd-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="604fd-154">建立保存庫之後，權限，而之前的任何機器註冊的 tooit hello 最佳時間 tooselect hello 儲存體備援選項。</span><span class="sxs-lookup"><span data-stu-id="604fd-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="604fd-155">一旦項目已註冊的 toohello 保存庫，hello 儲存體備援選項已鎖定且無法修改。</span><span class="sxs-lookup"><span data-stu-id="604fd-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![設定](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="604fd-157">如需 [儲存體備援](../storage/common/storage-redundancy.md)的詳細資訊，請參閱這篇文章。</span><span class="sxs-lookup"><span data-stu-id="604fd-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="604fd-158">Microsoft Azure 備份代理程式工作</span><span class="sxs-lookup"><span data-stu-id="604fd-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="604fd-159">主控台</span><span class="sxs-lookup"><span data-stu-id="604fd-159">Console</span></span>
<span data-ttu-id="604fd-160">開啟 hello **Microsoft Azure 備份代理程式**(您可以藉由搜尋電腦上找到它*Microsoft Azure 備份*)。</span><span class="sxs-lookup"><span data-stu-id="604fd-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![備份代理程式](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="604fd-162">從 hello**動作**位於 hello hello 備份代理程式 」 主控台的權限可以執行下列管理工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="604fd-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="604fd-163">註冊伺服器</span><span class="sxs-lookup"><span data-stu-id="604fd-163">Register Server</span></span>
* <span data-ttu-id="604fd-164">排程備份</span><span class="sxs-lookup"><span data-stu-id="604fd-164">Schedule Backup</span></span>
* <span data-ttu-id="604fd-165">立即備份</span><span class="sxs-lookup"><span data-stu-id="604fd-165">Back Up now</span></span>
* <span data-ttu-id="604fd-166">變更屬性</span><span class="sxs-lookup"><span data-stu-id="604fd-166">Change Properties</span></span>

![代理程式主控台動作](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="604fd-168">太**復原資料**，請參閱[還原檔案 tooa Windows server 或 Windows 用戶端電腦](backup-azure-restore-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="604fd-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="604fd-169">修改現有備份</span><span class="sxs-lookup"><span data-stu-id="604fd-169">Modify an existing backup</span></span>
1. <span data-ttu-id="604fd-170">Hello Microsoft Azure Backup agent 中按一下**排程備份**。</span><span class="sxs-lookup"><span data-stu-id="604fd-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="604fd-172">在 [hello**排程備份精靈**保留 hello**變更 toobackup 項目或時間**選取的選項，然後按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="604fd-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![修改排定的備份](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="604fd-174">如果您想 tooadd 或變更項目，在 hello**選取項目 tooBackup**畫面上，按一下**新增的項目**。</span><span class="sxs-lookup"><span data-stu-id="604fd-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="604fd-175">您也可以設定**排除設定**在 hello 精靈的這個頁面。</span><span class="sxs-lookup"><span data-stu-id="604fd-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="604fd-176">如果您想要 tooexclude 檔案或檔案類型讀取 hello 加入程序[排除設定](#exclusion-settings)。</span><span class="sxs-lookup"><span data-stu-id="604fd-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="604fd-177">選取 hello 檔案和資料夾，您想 tooback 和按一下**好**。</span><span class="sxs-lookup"><span data-stu-id="604fd-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![新增項目](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="604fd-179">指定 hello**備份排程**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="604fd-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="604fd-180">您可以排程每日 (一天最多 3 次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="604fd-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![指定備份排程](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="604fd-182">指定 hello 備份排程中會詳細說明此[文章](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="604fd-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="604fd-183">選取 hello**保留原則**hello 備份複本，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="604fd-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![選取保留原則](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="604fd-185">在 hello**確認**畫面檢閱 hello 資訊，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="604fd-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="604fd-186">一旦 hello 精靈可讓您完成建立 hello**備份排程**，按一下 **關閉**。</span><span class="sxs-lookup"><span data-stu-id="604fd-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="604fd-187">之後修改的保護，您可以確認備份正確的觸發移 toohello 由**作業** 索引標籤，並確認變更會反映在 hello 備份作業。</span><span class="sxs-lookup"><span data-stu-id="604fd-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="604fd-188">啟用網路節流</span><span class="sxs-lookup"><span data-stu-id="604fd-188">Enable Network Throttling</span></span>
<span data-ttu-id="604fd-189">hello Azure 備份代理程式提供節流索引標籤可讓您 toocontrol 資料傳輸期間的網路頻寬使用方式。</span><span class="sxs-lookup"><span data-stu-id="604fd-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="604fd-190">如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量，此控制項可以是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="604fd-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="604fd-191">節流的資料傳輸 tooback 套用設定，並還原活動。</span><span class="sxs-lookup"><span data-stu-id="604fd-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="604fd-192">tooenable 節流：</span><span class="sxs-lookup"><span data-stu-id="604fd-192">tooenable throttling:</span></span>

1. <span data-ttu-id="604fd-193">在 hello **Backup agent**，按一下 **變更屬性**。</span><span class="sxs-lookup"><span data-stu-id="604fd-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="604fd-194">選取 hello**啟用網際網路頻寬使用節流設定的備份操作**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="604fd-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![網路節流](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="604fd-196">一旦您已啟用節流設定，指定允許頻寬的備份資料傳輸期間的 hello**上班**和**非工作小時**。</span><span class="sxs-lookup"><span data-stu-id="604fd-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="604fd-197">hello 頻寬值 512 kb/秒 (Kbps) 為開頭，而且可以向上 too1023 mb / 秒 (Mbps)。</span><span class="sxs-lookup"><span data-stu-id="604fd-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="604fd-198">您可以指定 hello 開始和完成**上班**，而 hello 一週的哪幾天會被視為工作天。</span><span class="sxs-lookup"><span data-stu-id="604fd-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="604fd-199">指定工作時數的 hello 之外的 hello 時間是視為的 toobe 非工作小時。</span><span class="sxs-lookup"><span data-stu-id="604fd-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="604fd-200">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="604fd-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="604fd-201">排除設定</span><span class="sxs-lookup"><span data-stu-id="604fd-201">Exclusion settings</span></span>
1. <span data-ttu-id="604fd-202">開啟 hello **Microsoft Azure 備份代理程式**(您可以藉由搜尋電腦上找到它*Microsoft Azure 備份*)。</span><span class="sxs-lookup"><span data-stu-id="604fd-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![開啟備份代理程式](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="604fd-204">Hello Microsoft Azure Backup agent 中按一下**排程備份**。</span><span class="sxs-lookup"><span data-stu-id="604fd-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="604fd-206">在 排程備份精靈 hello 保留 hello**變更 toobackup 項目或時間**選取的選項，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="604fd-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![修改排程](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="604fd-208">按一下 [排除設定] 。</span><span class="sxs-lookup"><span data-stu-id="604fd-208">Click **Exclusions Settings**.</span></span>

    ![選取項目 tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="604fd-210">按一下 [新增排除] 。</span><span class="sxs-lookup"><span data-stu-id="604fd-210">Click **Add Exclusion**.</span></span>

    ![新增排除項目](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="604fd-212">選取 hello 位置，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="604fd-212">Select hello location and then, click **OK**.</span></span>

    ![選取要排除的位置](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="604fd-214">Hello 檔案延伸模組增益集 hello**檔案類型**欄位。</span><span class="sxs-lookup"><span data-stu-id="604fd-214">Add hello file extension in hello **File Type** field.</span></span>

    ![依檔案類型排除](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="604fd-216">新增 .mp3 副檔名</span><span class="sxs-lookup"><span data-stu-id="604fd-216">Adding an .mp3 extension</span></span>

    ![檔案類型範例](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="604fd-218">tooadd 另一個延伸模組中，按一下**新增排除**，然後輸入另一個檔案類型副檔名 （新增.jpeg 副檔名）。</span><span class="sxs-lookup"><span data-stu-id="604fd-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![另一個檔案類型範例](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="604fd-220">當您新增所有 hello 擴充功能之後時，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="604fd-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="604fd-221">繼續透過 hello 排程備份精靈]，依序按一下**下一步**直到 hello**確認頁面**，然後按一下 [**完成**。</span><span class="sxs-lookup"><span data-stu-id="604fd-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![排除確認](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="604fd-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="604fd-223">Next steps</span></span>
* [<span data-ttu-id="604fd-224">從 Azure 還原 Windows Server 或 Windows 用戶端</span><span class="sxs-lookup"><span data-stu-id="604fd-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="604fd-225">toolearn 進一步了解 Azure 備份，請參閱[Azure 備份概觀](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="604fd-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="604fd-226">請瀏覽 hello [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="604fd-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
