---
title: "aaaManage Azure 復原服務保存庫與伺服器 |Microsoft 文件"
description: "使用此教學課程 toolearn toomanage Azure 復原服務保存庫的方式和伺服器。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="09000-103">監視和管理 Windows 電腦的 Azure 復原服務保存庫和伺服器</span><span class="sxs-lookup"><span data-stu-id="09000-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09000-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="09000-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="09000-105">傳統</span><span class="sxs-lookup"><span data-stu-id="09000-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="09000-106">在本文中您會發現備份監視和管理工作可透過 Azure 入口網站和 hello Microsoft Azure 備份代理程式 hello hello 的概觀。</span><span class="sxs-lookup"><span data-stu-id="09000-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="09000-107">本文假設您已經有 Azure 訂用帳戶，並至少建立了一個復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="09000-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="09000-108">開啟復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="09000-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="09000-109">hello 復原服務保存庫儀表板會顯示 hello 詳細資料] 或 [復原服務保存庫的屬性。</span><span class="sxs-lookup"><span data-stu-id="09000-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="09000-110">登入 toohello [Azure 入口網站](https://portal.azure.com/)使用您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="09000-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="09000-111">在 hello 中樞功能表中，按一下 **更服務**。</span><span class="sxs-lookup"><span data-stu-id="09000-111">On hello Hub menu, click **More Services**.</span></span>

    ![開啟復原服務保存庫清單的步驟 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="09000-113">您想 tooopen 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="09000-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="09000-114">在 [hello] 對話方塊中，開始輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="09000-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="09000-115">當您開始輸入 hello 清單會篩選器根據您的輸入。</span><span class="sxs-lookup"><span data-stu-id="09000-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="09000-116">按一下**復原服務保存庫**toodisplay hello 清單的 復原服務保存庫中您訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="09000-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="09000-118">此時會開啟 復原服務保存庫的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="09000-118">hello list of Recovery Services vaults opens.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="09000-120">從保存庫的 hello 清單中，選取 hello hello 想 tooopen 復原服務保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="09000-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="09000-121">hello 復原服務保存庫儀表板 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="09000-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![復原服務保存庫儀表板](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="09000-123">既然您已開啟 hello 復原服務保存庫，再試一次任一 hello 監視或管理工作。</span><span class="sxs-lookup"><span data-stu-id="09000-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="09000-124">監視備份作業和警示</span><span class="sxs-lookup"><span data-stu-id="09000-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="09000-125">監視作業，並從 hello 警示復原服務保存庫儀表板，了解：</span><span class="sxs-lookup"><span data-stu-id="09000-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="09000-126">備份警示詳細資料</span><span class="sxs-lookup"><span data-stu-id="09000-126">Backup alerts details</span></span>
* <span data-ttu-id="09000-127">檔案和資料夾，以及 Azure hello 雲端中受保護的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="09000-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="09000-128">Azure 中已使用的儲存體總計</span><span class="sxs-lookup"><span data-stu-id="09000-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="09000-129">備份作業狀態</span><span class="sxs-lookup"><span data-stu-id="09000-129">Backup job status</span></span>

![備份儀表板工作](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="09000-131">按一下每個這些磚中的 hello 資訊會開啟 hello 關聯刀鋒視窗，讓您管理相關的工作。</span><span class="sxs-lookup"><span data-stu-id="09000-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="09000-132">從 hello hello 儀表板頂端：</span><span class="sxs-lookup"><span data-stu-id="09000-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="09000-133">[設定] 可供存取可用的備份工作。</span><span class="sxs-lookup"><span data-stu-id="09000-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="09000-134">備份-可協助您將新的檔案和資料夾 （或 Azure Vm） toohello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="09000-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="09000-135">不再使用 delete-如果復原服務保存庫，您可以將它刪除 toofree 出儲存空間。</span><span class="sxs-lookup"><span data-stu-id="09000-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="09000-136">Hello 保存庫中刪除所有受保護的伺服器之後，才會啟用刪除。</span><span class="sxs-lookup"><span data-stu-id="09000-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![備份儀表板工作](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="09000-138">針對使用 Azure 備份代理程式之備份的警示：</span><span class="sxs-lookup"><span data-stu-id="09000-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="09000-139">警示層級</span><span class="sxs-lookup"><span data-stu-id="09000-139">Alert Level</span></span> | <span data-ttu-id="09000-140">傳送的警示</span><span class="sxs-lookup"><span data-stu-id="09000-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="09000-141">重要</span><span class="sxs-lookup"><span data-stu-id="09000-141">Critical</span></span> |<span data-ttu-id="09000-142">備份失敗、復原失敗</span><span class="sxs-lookup"><span data-stu-id="09000-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="09000-143">警告</span><span class="sxs-lookup"><span data-stu-id="09000-143">Warning</span></span> |<span data-ttu-id="09000-144">備份 （當少於一百檔案則不會備份到期 toocorruption 問題，且超過 1 百萬個檔案已成功備份），已完成但出現警告</span><span class="sxs-lookup"><span data-stu-id="09000-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="09000-145">資訊</span><span class="sxs-lookup"><span data-stu-id="09000-145">Informational</span></span> |<span data-ttu-id="09000-146">None</span><span class="sxs-lookup"><span data-stu-id="09000-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="09000-147">管理備份警示</span><span class="sxs-lookup"><span data-stu-id="09000-147">Manage Backup alerts</span></span>
<span data-ttu-id="09000-148">按一下 hello**備份警示**磚 tooopen hello**備份警示**刀鋒視窗及管理警示。</span><span class="sxs-lookup"><span data-stu-id="09000-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![備份警示](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="09000-150">hello 備份警示磚顯示 hello 數目：</span><span class="sxs-lookup"><span data-stu-id="09000-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="09000-151">過去 24 小時內未解決的重大警示</span><span class="sxs-lookup"><span data-stu-id="09000-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="09000-152">過去 24 小時內未解決的警告警示</span><span class="sxs-lookup"><span data-stu-id="09000-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="09000-153">按一下這些連結會帶您 toohello**備份警示**刀鋒視窗的 篩選檢視的這些警示 （重大或警告）。</span><span class="sxs-lookup"><span data-stu-id="09000-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="09000-154">Hello 備份警示刀鋒視窗中，從您：</span><span class="sxs-lookup"><span data-stu-id="09000-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="09000-155">選擇將適當的資訊 tooinclude hello 與您的通知。</span><span class="sxs-lookup"><span data-stu-id="09000-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![選擇資料行](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="09000-157">針對嚴重性、狀態和開始/結束時間篩選警示。</span><span class="sxs-lookup"><span data-stu-id="09000-157">Filter alerts for severity, status and start/end times.</span></span>

    ![篩選警示](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="09000-159">針對嚴重性、頻率和接收者設定通知，以及開啟或關閉警示。</span><span class="sxs-lookup"><span data-stu-id="09000-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![篩選警示](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="09000-161">如果**每個警示**當做 hello**通知**不進行任何群組或減少電子郵件的頻率。</span><span class="sxs-lookup"><span data-stu-id="09000-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="09000-162">每個警示會產生 1 則通知。</span><span class="sxs-lookup"><span data-stu-id="09000-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="09000-163">這是 hello 預設設定，而且 hello 解析電子郵件也會立即送出。</span><span class="sxs-lookup"><span data-stu-id="09000-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="09000-164">如果**每小時摘要**當做 hello**通知**傳送 toohello 使用者告訴他們有一個電子郵件的頻率無法解析產生 hello 在過去一小時內的新警示。</span><span class="sxs-lookup"><span data-stu-id="09000-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="09000-165">解析電子郵件送出 hello hello 小時結尾處。</span><span class="sxs-lookup"><span data-stu-id="09000-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="09000-166">警示可以傳送 hello 下列嚴重性層級：</span><span class="sxs-lookup"><span data-stu-id="09000-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="09000-167">重要</span><span class="sxs-lookup"><span data-stu-id="09000-167">critical</span></span>
* <span data-ttu-id="09000-168">警告</span><span class="sxs-lookup"><span data-stu-id="09000-168">warning</span></span>
* <span data-ttu-id="09000-169">資訊</span><span class="sxs-lookup"><span data-stu-id="09000-169">information</span></span>

<span data-ttu-id="09000-170">以 hello hello 警示中停用**中停用**hello 工作詳細資料 刀鋒視窗中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="09000-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="09000-171">當您按一下 [停用] 時，您可以提供解決方式資訊。</span><span class="sxs-lookup"><span data-stu-id="09000-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="09000-172">您選擇 hello 資料行要作為組件以 hello hello 警示的 tooappear**選擇資料行** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="09000-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="09000-173">從 hello**設定**刀鋒視窗中，選取 管理備份警示**監視與報表 > 警示與事件 > 備份警示**，然後按一下**篩選**或**設定通知**。</span><span class="sxs-lookup"><span data-stu-id="09000-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="09000-174">管理備份項目</span><span class="sxs-lookup"><span data-stu-id="09000-174">Manage Backup items</span></span>
<span data-ttu-id="09000-175">管理內部部署備份現已推出 hello 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="09000-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="09000-176">在 hello 備份區段中的 hello 儀表板，hello**備份項目**磚會顯示受保護的備份項目的 hello 數目 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="09000-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="09000-177">按一下**檔案資料夾**hello 備份項目磚中。</span><span class="sxs-lookup"><span data-stu-id="09000-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![備份項目圖格](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="09000-179">刀鋒視窗會開啟以 hello hello 備份項目來篩選，您會看到每個項目列出的特定備份組 tooFile 資料夾。</span><span class="sxs-lookup"><span data-stu-id="09000-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![備份項目](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="09000-181">如果您從 hello 清單中選取特定的備份項目，您會看到該項目 hello 基本詳細資料。</span><span class="sxs-lookup"><span data-stu-id="09000-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="09000-182">從 hello**設定**刀鋒視窗中，您可以管理檔案和資料夾選取**受保護項目 > 備份項目**，然後選取 **檔案資料夾**hello 從下拉功能表。</span><span class="sxs-lookup"><span data-stu-id="09000-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![從設定備份項目](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="09000-184">管理備份作業</span><span class="sxs-lookup"><span data-stu-id="09000-184">Manage Backup jobs</span></span>
<span data-ttu-id="09000-185">在內部部署 （當 hello 在內部部署伺服器備份 tooAzure） 及 Azure 備份的備份工作會顯示 hello 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="09000-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="09000-186">Hello hello 儀表板的 備份 區段中，在 hello 備份工作 磚會顯示 hello 作業數目：</span><span class="sxs-lookup"><span data-stu-id="09000-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="09000-187">進行中</span><span class="sxs-lookup"><span data-stu-id="09000-187">in progress</span></span>
* <span data-ttu-id="09000-188">無法在 hello 過去 24 小時。</span><span class="sxs-lookup"><span data-stu-id="09000-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="09000-189">toomanage 的備份作業中，按一下 hello**備份工作**磚，以開啟刀鋒視窗中的備份工作 hello。</span><span class="sxs-lookup"><span data-stu-id="09000-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![從設定備份項目](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="09000-191">修改以 hello hello Backup 工作刀鋒視窗中可用的 hello 資訊**選擇資料行**hello hello 頁頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="09000-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="09000-192">使用 hello**篩選**按鈕 tooselect 之間的檔案和資料夾以及 Azure 虛擬機器備份。</span><span class="sxs-lookup"><span data-stu-id="09000-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="09000-193">如果您沒有看到您的備份檔案及資料夾，按一下**篩選**在 hello hello 頁面並選取最上方的按鈕**檔案和資料夾**功能表 hello 項目類型。</span><span class="sxs-lookup"><span data-stu-id="09000-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="09000-194">從 hello**設定**刀鋒視窗中，您選取 管理備份工作**監視與報表 > 作業 > 備份工作**，然後選取 **檔案資料夾**從 hello 拖放關閉功能表。</span><span class="sxs-lookup"><span data-stu-id="09000-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="09000-195">監視備份使用量</span><span class="sxs-lookup"><span data-stu-id="09000-195">Monitor Backup usage</span></span>
<span data-ttu-id="09000-196">Hello hello 儀表板的 [備份] 區段中，在 hello 備份 [使用量] 磚會顯示 hello Azure 中已使用的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="09000-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="09000-197">提供下列各項的儲存體使用量︰</span><span class="sxs-lookup"><span data-stu-id="09000-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="09000-198">Hello 保存庫相關聯的雲端 LRS 儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="09000-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="09000-199">雲端 GRS hello 保存庫相關聯的存放裝置使用量</span><span class="sxs-lookup"><span data-stu-id="09000-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="09000-200">管理您的生產伺服器</span><span class="sxs-lookup"><span data-stu-id="09000-200">Manage your production servers</span></span>
<span data-ttu-id="09000-201">您的實際執行伺服器，按一下 toomanage**設定**。</span><span class="sxs-lookup"><span data-stu-id="09000-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="09000-202">按一下 [管理] 之下的 [備份基礎結構] > [生產伺服器]。</span><span class="sxs-lookup"><span data-stu-id="09000-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="09000-203">hello 實際執行伺服器刀鋒視窗中列出的所有可用的實際執行伺服器。</span><span class="sxs-lookup"><span data-stu-id="09000-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="09000-204">按一下 在 hello 清單 tooopen hello 伺服器詳細資料的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="09000-204">Click on a server in hello list tooopen hello server details.</span></span>

![受保護項目](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="09000-206">開啟 hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="09000-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="09000-207">開啟 hello **Microsoft Azure 備份代理程式**(藉由搜尋電腦找到它*Microsoft Azure 備份*)。</span><span class="sxs-lookup"><span data-stu-id="09000-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Windows Server 備份排程](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="09000-209">從 hello**動作**位於 hello hello 備份代理程式 」 主控台的權限執行下列管理工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="09000-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="09000-210">註冊伺服器</span><span class="sxs-lookup"><span data-stu-id="09000-210">Register Server</span></span>
* <span data-ttu-id="09000-211">排程備份</span><span class="sxs-lookup"><span data-stu-id="09000-211">Schedule Backup</span></span>
* <span data-ttu-id="09000-212">立即備份</span><span class="sxs-lookup"><span data-stu-id="09000-212">Back Up now</span></span>
* <span data-ttu-id="09000-213">變更屬性</span><span class="sxs-lookup"><span data-stu-id="09000-213">Change Properties</span></span>

![Microsoft Azure 備份代理程式主控台動作](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="09000-215">太**復原資料**，請參閱[還原檔案 tooa Windows server 或 Windows 用戶端電腦](backup-azure-restore-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="09000-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="09000-216">修改備份排程，hello</span><span class="sxs-lookup"><span data-stu-id="09000-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="09000-217">Hello Microsoft Azure Backup agent 中按一下**排程備份**。</span><span class="sxs-lookup"><span data-stu-id="09000-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="09000-219">在 [hello**排程備份精靈**保留 hello**變更 toobackup 項目或時間**選取的選項，然後按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="09000-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="09000-221">如果您想 tooadd 或變更項目，在 hello**選取項目 tooBackup**畫面上，按一下**新增的項目**。</span><span class="sxs-lookup"><span data-stu-id="09000-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="09000-222">您也可以設定**排除設定**在 hello 精靈的這個頁面。</span><span class="sxs-lookup"><span data-stu-id="09000-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="09000-223">如果您想要 tooexclude 檔案或檔案類型讀取 hello 加入程序[排除設定](#manage-exclusion-settings)。</span><span class="sxs-lookup"><span data-stu-id="09000-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="09000-224">選取 hello 檔案和資料夾，您想 tooback 和按一下**好**。</span><span class="sxs-lookup"><span data-stu-id="09000-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="09000-226">指定 hello**備份排程**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="09000-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="09000-227">您可以排程每日 (一天最多 3 次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="09000-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Windows Server 備份項目](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="09000-229">指定 hello 備份排程中會詳細說明此[文章](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="09000-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="09000-230">選取 hello**保留原則**hello 備份複本，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="09000-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Windows Server 備份項目](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="09000-232">在 hello**確認**畫面檢閱 hello 資訊，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="09000-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="09000-233">一旦 hello 精靈可讓您完成建立 hello**備份排程**，按一下 **關閉**。</span><span class="sxs-lookup"><span data-stu-id="09000-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="09000-234">之後修改的保護，您可以確認備份正確的觸發移 toohello 由**作業** 索引標籤，並確認變更會反映在 hello 備份作業。</span><span class="sxs-lookup"><span data-stu-id="09000-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="09000-235">啟用網路節流</span><span class="sxs-lookup"><span data-stu-id="09000-235">Enable Network Throttling</span></span>

<span data-ttu-id="09000-236">hello Azure 備份代理程式提供節流索引標籤可讓您 toocontrol 資料傳輸期間的網路頻寬使用方式。</span><span class="sxs-lookup"><span data-stu-id="09000-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="09000-237">如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量，此控制項可以是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="09000-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="09000-238">節流的資料傳輸 tooback 套用設定，並還原活動。</span><span class="sxs-lookup"><span data-stu-id="09000-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="09000-239">tooenable 節流：</span><span class="sxs-lookup"><span data-stu-id="09000-239">tooenable throttling:</span></span>

1. <span data-ttu-id="09000-240">在 hello **Backup agent**，按一下 **變更屬性**。</span><span class="sxs-lookup"><span data-stu-id="09000-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="09000-241">在 [hello * * 節流] 索引標籤，選取**啟用網際網路頻寬使用節流設定的備份操作**。</span><span class="sxs-lookup"><span data-stu-id="09000-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![網路節流](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="09000-243">一旦您已啟用節流設定，指定允許頻寬的備份資料傳輸期間的 hello**上班**和**非工作小時**。</span><span class="sxs-lookup"><span data-stu-id="09000-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="09000-244">hello 頻寬值 512 kb/秒 (Kbps) 為開頭，而且可以向上 too1023 mb / 秒 (Mbps)。</span><span class="sxs-lookup"><span data-stu-id="09000-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="09000-245">您可以指定 hello 開始和完成**上班**，而 hello 一週的哪幾天會被視為工作天。</span><span class="sxs-lookup"><span data-stu-id="09000-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="09000-246">指定工作時數的 hello 之外的 hello 時間是視為的 toobe 非工作小時。</span><span class="sxs-lookup"><span data-stu-id="09000-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="09000-247">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="09000-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="09000-248">管理排除設定</span><span class="sxs-lookup"><span data-stu-id="09000-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="09000-249">開啟 hello **Microsoft Azure 備份代理程式**(您可以藉由搜尋電腦上找到它*Microsoft Azure 備份*)。</span><span class="sxs-lookup"><span data-stu-id="09000-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="09000-251">Hello Microsoft Azure Backup agent 中按一下**排程備份**。</span><span class="sxs-lookup"><span data-stu-id="09000-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="09000-253">在 排程備份精靈 hello 保留 hello**變更 toobackup 項目或時間**選取的選項，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="09000-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="09000-255">按一下 [排除設定] 。</span><span class="sxs-lookup"><span data-stu-id="09000-255">Click **Exclusions Settings**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="09000-257">按一下 [新增排除] 。</span><span class="sxs-lookup"><span data-stu-id="09000-257">Click **Add Exclusion**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="09000-259">選取 hello 位置，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="09000-259">Select hello location and then, click **OK**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="09000-261">Hello 檔案延伸模組增益集 hello**檔案類型**欄位。</span><span class="sxs-lookup"><span data-stu-id="09000-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="09000-263">新增 .mp3 副檔名</span><span class="sxs-lookup"><span data-stu-id="09000-263">Adding an .mp3 extension</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="09000-265">tooadd 另一個延伸模組中，按一下**新增排除**，然後輸入另一個檔案類型副檔名 （新增.jpeg 副檔名）。</span><span class="sxs-lookup"><span data-stu-id="09000-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="09000-267">當您新增所有 hello 擴充功能之後時，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="09000-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="09000-268">繼續透過 hello 排程備份精靈]，依序按一下**下一步**直到 hello**確認頁面**，然後按一下 [**完成**。</span><span class="sxs-lookup"><span data-stu-id="09000-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="09000-270">常見問題集</span><span class="sxs-lookup"><span data-stu-id="09000-270">Frequently asked questions</span></span>
<span data-ttu-id="09000-271">**Q1。hello 備份工作狀態會顯示為已完成在 hello Azure 備份代理程式為何不它取得會立即反映在入口網站？**</span><span class="sxs-lookup"><span data-stu-id="09000-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="09000-272">A1.</span><span class="sxs-lookup"><span data-stu-id="09000-272">A1.</span></span> <span data-ttu-id="09000-273">那里會在延遲時間上限為 15 分鐘之間 hello 備份作業的狀態反映在 hello Azure 備份代理程式 」 和 「 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="09000-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="09000-274">**Q.2 備份工作失敗時，時間長度花費 tooraise 警示？**</span><span class="sxs-lookup"><span data-stu-id="09000-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="09000-275">A.2 警示就會引發 hello Azure 備份失敗的 20 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="09000-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="09000-276">**Q3.是否會有已設定通知但不會傳送電子郵件的情況？**</span><span class="sxs-lookup"><span data-stu-id="09000-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="09000-277">A3.</span><span class="sxs-lookup"><span data-stu-id="09000-277">A3.</span></span> <span data-ttu-id="09000-278">不會傳送 hello 通知順序 tooreduce hello 警示的干擾中時，以下是 hello 案例：</span><span class="sxs-lookup"><span data-stu-id="09000-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="09000-279">如果每小時設定通知，並引發並 hello 一小時內已解決的警示</span><span class="sxs-lookup"><span data-stu-id="09000-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="09000-280">作業便會取消。</span><span class="sxs-lookup"><span data-stu-id="09000-280">Job is canceled.</span></span>
* <span data-ttu-id="09000-281">第二個備份作業會失敗，因為原始的備份作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="09000-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="09000-282">疑難排解監視問題</span><span class="sxs-lookup"><span data-stu-id="09000-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="09000-283">**問題：**作業和/或 hello Azure Backup agent 的警示不會出現在 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="09000-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="09000-284">**疑難排解步驟：** hello 程序， ```OBRecoveryServicesManagementAgent```，傳送 hello 作業和警示資料 toohello Azure 備份服務。</span><span class="sxs-lookup"><span data-stu-id="09000-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="09000-285">此程序可能偶爾會卡住或關閉。</span><span class="sxs-lookup"><span data-stu-id="09000-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="09000-286">tooverify hello 程序並未執行，請開啟**工作管理員**，檢查是否 hello```OBRecoveryServicesManagementAgent```處理序正在執行。</span><span class="sxs-lookup"><span data-stu-id="09000-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="09000-287">假設 hello 程序不在執行中，開啟**控制台**並瀏覽 hello 服務清單。</span><span class="sxs-lookup"><span data-stu-id="09000-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="09000-288">啟動或重新啟動 **Microsoft Azure 復原服務管理代理程式**。</span><span class="sxs-lookup"><span data-stu-id="09000-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="09000-289">如需詳細資訊，瀏覽 hello 記錄檔，位於：</span><span class="sxs-lookup"><span data-stu-id="09000-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="09000-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` 例如：</span><span class="sxs-lookup"><span data-stu-id="09000-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="09000-291">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09000-291">Next steps</span></span>
* [<span data-ttu-id="09000-292">從 Azure 還原 Windows Server 或 Windows 用戶端</span><span class="sxs-lookup"><span data-stu-id="09000-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="09000-293">toolearn 進一步了解 Azure 備份，請參閱[Azure 備份概觀](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="09000-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="09000-294">請瀏覽 hello [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="09000-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
