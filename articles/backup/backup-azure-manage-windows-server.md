---
title: "管理 Azure 復原服務保存庫與伺服器 | Microsoft Docs"
description: "使用本教學課程了解如何管理 Azure 復原服務保存庫與伺服器。"
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
ms.openlocfilehash: 5922e308f5c205a07bd329c28322ae82cea0e1fa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="91b4e-103">監視和管理 Windows 電腦的 Azure 復原服務保存庫和伺服器</span><span class="sxs-lookup"><span data-stu-id="91b4e-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91b4e-104">資源管理員</span><span class="sxs-lookup"><span data-stu-id="91b4e-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="91b4e-105">傳統</span><span class="sxs-lookup"><span data-stu-id="91b4e-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="91b4e-106">在本文中，您將了解透過 Azure 入口網站和 Microsoft Azure 備份代理程式提供之備份監視和管理工作的概觀。</span><span class="sxs-lookup"><span data-stu-id="91b4e-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="91b4e-107">本文假設您已經有 Azure 訂用帳戶，並至少建立了一個復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="91b4e-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="91b4e-108">開啟復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="91b4e-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="91b4e-109">復原服務保存庫儀表板會顯示復原服務保存庫的詳細資料或屬性。</span><span class="sxs-lookup"><span data-stu-id="91b4e-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="91b4e-110">使用 Azure 訂用帳戶登入 [Azure 入口網站](https://portal.azure.com/) 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="91b4e-111">在 [中樞] 功能表上，按一下 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-111">On the Hub menu, click **More Services**.</span></span>

    ![開啟復原服務保存庫清單的步驟 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="91b4e-113">您想要開啟復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="91b4e-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="91b4e-114">在對話方塊中，開始輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="91b4e-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="91b4e-115">當您開始輸入時，清單將會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="91b4e-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="91b4e-116">按一下 [復原服務保存庫]，以顯示您訂用帳戶中的復原服務保存庫清單。</span><span class="sxs-lookup"><span data-stu-id="91b4e-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="91b4e-118">復原服務保存庫清單隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="91b4e-118">The list of Recovery Services vaults opens.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="91b4e-120">從保存庫清單中，選取您想要開啟的復原服務保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="91b4e-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="91b4e-121">[復原服務保存庫儀表板] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="91b4e-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![復原服務保存庫儀表板](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="91b4e-123">現在您已開啟復原服務保存庫，請試著使用任何監視或管理工作。</span><span class="sxs-lookup"><span data-stu-id="91b4e-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="91b4e-124">監視備份作業和警示</span><span class="sxs-lookup"><span data-stu-id="91b4e-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="91b4e-125">您可以從復原服務保存庫儀表板監視作業和警示，您可以看到︰</span><span class="sxs-lookup"><span data-stu-id="91b4e-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="91b4e-126">備份警示詳細資料</span><span class="sxs-lookup"><span data-stu-id="91b4e-126">Backup alerts details</span></span>
* <span data-ttu-id="91b4e-127">檔案和資料夾，以及雲端中受保護的 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="91b4e-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="91b4e-128">Azure 中已使用的儲存體總計</span><span class="sxs-lookup"><span data-stu-id="91b4e-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="91b4e-129">備份作業狀態</span><span class="sxs-lookup"><span data-stu-id="91b4e-129">Backup job status</span></span>

![備份儀表板工作](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="91b4e-131">按一下上述每個圖格中的資訊，將會開啟相關聯的刀鋒視窗以便管理相關工作。</span><span class="sxs-lookup"><span data-stu-id="91b4e-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="91b4e-132">在儀表板的頂端：</span><span class="sxs-lookup"><span data-stu-id="91b4e-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="91b4e-133">[設定] 可供存取可用的備份工作。</span><span class="sxs-lookup"><span data-stu-id="91b4e-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="91b4e-134">備份 - 協助您將新的檔案和資料夾 (或 Azure VM) 備份至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="91b4e-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="91b4e-135">刪除 - 如果不再使用復原服務保存庫，您可予以刪除來釋出儲存空間。</span><span class="sxs-lookup"><span data-stu-id="91b4e-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="91b4e-136">只有在從保存庫中刪除了所有受保護的伺服器之後，[刪除] 才會啟用。</span><span class="sxs-lookup"><span data-stu-id="91b4e-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![備份儀表板工作](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="91b4e-138">針對使用 Azure 備份代理程式之備份的警示：</span><span class="sxs-lookup"><span data-stu-id="91b4e-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="91b4e-139">警示層級</span><span class="sxs-lookup"><span data-stu-id="91b4e-139">Alert Level</span></span> | <span data-ttu-id="91b4e-140">傳送的警示</span><span class="sxs-lookup"><span data-stu-id="91b4e-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="91b4e-141">重要</span><span class="sxs-lookup"><span data-stu-id="91b4e-141">Critical</span></span> |<span data-ttu-id="91b4e-142">備份失敗、復原失敗</span><span class="sxs-lookup"><span data-stu-id="91b4e-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="91b4e-143">警告</span><span class="sxs-lookup"><span data-stu-id="91b4e-143">Warning</span></span> |<span data-ttu-id="91b4e-144">備份完成，但有警告 (當不到一百個檔案因為損毀問題而未備份，以及超過一百萬個檔案成功備份時)</span><span class="sxs-lookup"><span data-stu-id="91b4e-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="91b4e-145">資訊</span><span class="sxs-lookup"><span data-stu-id="91b4e-145">Informational</span></span> |<span data-ttu-id="91b4e-146">None</span><span class="sxs-lookup"><span data-stu-id="91b4e-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="91b4e-147">管理備份警示</span><span class="sxs-lookup"><span data-stu-id="91b4e-147">Manage Backup alerts</span></span>
<span data-ttu-id="91b4e-148">按一下 [備份警示] 圖格以開啟 [備份警示] 刀鋒視窗及管理警示。</span><span class="sxs-lookup"><span data-stu-id="91b4e-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![備份警示](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="91b4e-150">[備份警示] 圖格會顯示下列各項的數目︰</span><span class="sxs-lookup"><span data-stu-id="91b4e-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="91b4e-151">過去 24 小時內未解決的重大警示</span><span class="sxs-lookup"><span data-stu-id="91b4e-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="91b4e-152">過去 24 小時內未解決的警告警示</span><span class="sxs-lookup"><span data-stu-id="91b4e-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="91b4e-153">按一下每個連結會帶您前往 [備份警示]  刀鋒視窗，其中包含這些警示 (重大或警告) 的篩選檢視。</span><span class="sxs-lookup"><span data-stu-id="91b4e-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="91b4e-154">在 [備份警示] 刀鋒視窗中，您可︰</span><span class="sxs-lookup"><span data-stu-id="91b4e-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="91b4e-155">選擇要與您的警示一起納入的適當資訊。</span><span class="sxs-lookup"><span data-stu-id="91b4e-155">Choose the appropriate information to include with your alerts.</span></span>

    ![選擇資料行](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="91b4e-157">針對嚴重性、狀態和開始/結束時間篩選警示。</span><span class="sxs-lookup"><span data-stu-id="91b4e-157">Filter alerts for severity, status and start/end times.</span></span>

    ![篩選警示](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="91b4e-159">針對嚴重性、頻率和接收者設定通知，以及開啟或關閉警示。</span><span class="sxs-lookup"><span data-stu-id="91b4e-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![篩選警示](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="91b4e-161">如果選取 [每個警示] 做為 [通知] 頻率，則電子郵件不會分組或減少。</span><span class="sxs-lookup"><span data-stu-id="91b4e-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="91b4e-162">每個警示會產生 1 則通知。</span><span class="sxs-lookup"><span data-stu-id="91b4e-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="91b4e-163">這是預設設定，而且也會立即送出解決方式電子郵件。</span><span class="sxs-lookup"><span data-stu-id="91b4e-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="91b4e-164">如果選取 [每小時摘要] 做為 [通知] 頻率，則會傳送一封電子郵件給使用者，告知過去一小時有未解決的新警示產生。</span><span class="sxs-lookup"><span data-stu-id="91b4e-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="91b4e-165">解決方式電子郵件會在每小時結束時送出。</span><span class="sxs-lookup"><span data-stu-id="91b4e-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="91b4e-166">可以針對下列嚴重性等級傳送警示︰</span><span class="sxs-lookup"><span data-stu-id="91b4e-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="91b4e-167">重要</span><span class="sxs-lookup"><span data-stu-id="91b4e-167">critical</span></span>
* <span data-ttu-id="91b4e-168">警告</span><span class="sxs-lookup"><span data-stu-id="91b4e-168">warning</span></span>
* <span data-ttu-id="91b4e-169">資訊</span><span class="sxs-lookup"><span data-stu-id="91b4e-169">information</span></span>

<span data-ttu-id="91b4e-170">您可使用 [作業詳細資料] 刀鋒視窗中的 [停用]  按鈕來停用警示。</span><span class="sxs-lookup"><span data-stu-id="91b4e-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="91b4e-171">當您按一下 [停用] 時，您可以提供解決方式資訊。</span><span class="sxs-lookup"><span data-stu-id="91b4e-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="91b4e-172">您可以使用 [選擇資料行]  按鈕，選擇您要顯示在警示中的資料行。</span><span class="sxs-lookup"><span data-stu-id="91b4e-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="91b4e-173">在 [設定] 刀鋒視窗中，選取 [監視和報告] > [警示和事件] > [備份警示]，然後按一下 [篩選] 或 [設定通知]，以管理備份警示。</span><span class="sxs-lookup"><span data-stu-id="91b4e-173">From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="91b4e-174">管理備份項目</span><span class="sxs-lookup"><span data-stu-id="91b4e-174">Manage Backup items</span></span>
<span data-ttu-id="91b4e-175">管理內部部署備份現在已可在管理入口網站中使用。</span><span class="sxs-lookup"><span data-stu-id="91b4e-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="91b4e-176">在儀表板的 [備份] 區段中，[備份項目]  圖格會顯示保存庫中受保護的備份項目數。</span><span class="sxs-lookup"><span data-stu-id="91b4e-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="91b4e-177">按一下 [備份項目] 圖格中的 [檔案-資料夾]  。</span><span class="sxs-lookup"><span data-stu-id="91b4e-177">Click **File-Folders** in the Backup Items tile.</span></span>

![備份項目圖格](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="91b4e-179">隨即開啟篩選器設定為 [檔案-資料夾] 的 [備份項目] 刀鋒視窗，其中列出每個特定備份項目。</span><span class="sxs-lookup"><span data-stu-id="91b4e-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![備份項目](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="91b4e-181">如果您選取清單中的特定備份項目，您會看到該項目的基本詳細資料。</span><span class="sxs-lookup"><span data-stu-id="91b4e-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="91b4e-182">在 [設定] 刀鋒視窗中，您可選取 [受保護項目] > [備份項目]，然後從下拉式功能表中選取 [檔案-資料夾]，以管理檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="91b4e-182">From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

![從設定備份項目](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="91b4e-184">管理備份作業</span><span class="sxs-lookup"><span data-stu-id="91b4e-184">Manage Backup jobs</span></span>
<span data-ttu-id="91b4e-185">內部部署 (當內部部署伺服器備份至 Azure 時) 和 Azure 備份的備份作業均會顯示在儀表板中。</span><span class="sxs-lookup"><span data-stu-id="91b4e-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="91b4e-186">在儀表板的 [備份] 區段中，[備份作業] 圖格會顯示作業數目：</span><span class="sxs-lookup"><span data-stu-id="91b4e-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="91b4e-187">進行中</span><span class="sxs-lookup"><span data-stu-id="91b4e-187">in progress</span></span>
* <span data-ttu-id="91b4e-188">過去 24 小時內失敗。</span><span class="sxs-lookup"><span data-stu-id="91b4e-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="91b4e-189">若要管理您的備份作業，請按一下 [備份作業]  圖格，即會開啟 [備份作業] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="91b4e-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![從設定備份項目](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="91b4e-191">您可使用頁面頂端的 [選擇資料行]  按鈕，修改 [備份作業] 刀鋒視窗中可用的資訊。</span><span class="sxs-lookup"><span data-stu-id="91b4e-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="91b4e-192">使用 [篩選]  按鈕來選取檔案和資料夾以及 Azure 虛擬機器備份。</span><span class="sxs-lookup"><span data-stu-id="91b4e-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="91b4e-193">如果您未看到已備份的檔案和資料夾，按一下頁面頂端的 [篩選] 按鈕，然後從 [項目類型] 功能表中選取 [檔案和資料夾]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="91b4e-194">在 [設定] 刀鋒視窗中，您可選取 [監視和報告] > [作業] > [備份作業]，然後從下拉式功能表中選取 [檔案-資料夾]，以管理備份作業。</span><span class="sxs-lookup"><span data-stu-id="91b4e-194">From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="91b4e-195">監視備份使用量</span><span class="sxs-lookup"><span data-stu-id="91b4e-195">Monitor Backup usage</span></span>
<span data-ttu-id="91b4e-196">在儀表板的 [備份] 區段中，[備份使用量] 圖格會顯示 Azure 中已取用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="91b4e-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="91b4e-197">提供下列各項的儲存體使用量︰</span><span class="sxs-lookup"><span data-stu-id="91b4e-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="91b4e-198">與保存庫相關聯的雲端 LRS 儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="91b4e-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="91b4e-199">與保存庫相關聯的雲端 GRS 儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="91b4e-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="91b4e-200">管理您的生產伺服器</span><span class="sxs-lookup"><span data-stu-id="91b4e-200">Manage your production servers</span></span>
<span data-ttu-id="91b4e-201">若要管理您的生產伺服器，請按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="91b4e-202">按一下 [管理] 之下的 [備份基礎結構] > [生產伺服器]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="91b4e-203">[生產伺服器] 刀鋒視窗會列出所有可用的生產伺服器。</span><span class="sxs-lookup"><span data-stu-id="91b4e-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="91b4e-204">按一下清單中的伺服器以開啟伺服器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="91b4e-204">Click on a server in the list to open the server details.</span></span>

![受保護項目](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="91b4e-206">開啟 Azure 備份代理程式</span><span class="sxs-lookup"><span data-stu-id="91b4e-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="91b4e-207">開啟 **Microsoft Azure 備份**代理程式 (透過在電腦中搜尋「Microsoft Azure 備份」即可找到)。</span><span class="sxs-lookup"><span data-stu-id="91b4e-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Windows Server 備份排程](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="91b4e-209">從備份代理程式主控台右側可用的 [動作]  ，您可執行下列管理工作︰</span><span class="sxs-lookup"><span data-stu-id="91b4e-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="91b4e-210">註冊伺服器</span><span class="sxs-lookup"><span data-stu-id="91b4e-210">Register Server</span></span>
* <span data-ttu-id="91b4e-211">排程備份</span><span class="sxs-lookup"><span data-stu-id="91b4e-211">Schedule Backup</span></span>
* <span data-ttu-id="91b4e-212">立即備份</span><span class="sxs-lookup"><span data-stu-id="91b4e-212">Back Up now</span></span>
* <span data-ttu-id="91b4e-213">變更屬性</span><span class="sxs-lookup"><span data-stu-id="91b4e-213">Change Properties</span></span>

![Microsoft Azure 備份代理程式主控台動作](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="91b4e-215">若要 **復原資料**，請參閱 [將檔案還原到 Windows Server 或 Windows 用戶端電腦](backup-azure-restore-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="91b4e-215">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="91b4e-216">修改備份排程</span><span class="sxs-lookup"><span data-stu-id="91b4e-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="91b4e-217">在 Microsoft Azure 備份代理程式中，按一下 [排程備份] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="91b4e-219">在**排程備份精靈**中，讓 [變更備份項目或時間] 選項保留選取狀態，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="91b4e-221">如果您想要新增或變更項目，在 [選取要備份的項目] 畫面中按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="91b4e-222">您也可以在這個精靈頁面中設定 [排除設定]  。</span><span class="sxs-lookup"><span data-stu-id="91b4e-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="91b4e-223">如果您想要排除檔案或檔案類型，請參閱新增 [排除設定](#manage-exclusion-settings)的程序。</span><span class="sxs-lookup"><span data-stu-id="91b4e-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="91b4e-224">選取要備份的檔案和資料夾，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="91b4e-226">指定 [備份排程]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="91b4e-227">您可以排程每日 (一天最多 3 次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="91b4e-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Windows Server 備份項目](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="91b4e-229">這篇 [文章](backup-azure-backup-cloud-as-tape.md)中會詳細說明指定備份排程。</span><span class="sxs-lookup"><span data-stu-id="91b4e-229">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="91b4e-230">選取備份複本的 [保留原則]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Windows Server 備份項目](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="91b4e-232">在 [確認] 畫面上檢閱資訊，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="91b4e-233">當精靈完成 [備份排程] 的建立之後，按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="91b4e-234">修改保護之後，您可以藉由移至 [工作]  索引標籤並確認變更反映於備份工作中，來確定可正確觸發備份。</span><span class="sxs-lookup"><span data-stu-id="91b4e-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="91b4e-235">啟用網路節流</span><span class="sxs-lookup"><span data-stu-id="91b4e-235">Enable Network Throttling</span></span>

<span data-ttu-id="91b4e-236">Azure 備份代理程式提供 [節流] 索引標籤，可讓您控制在資料傳輸期間使用網路頻寬的方式。</span><span class="sxs-lookup"><span data-stu-id="91b4e-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="91b4e-237">如果您需要在上班時間內備份資料，但不希望備份程序干擾其他網際網路流量，這樣的控制會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="91b4e-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="91b4e-238">資料傳輸的節流適用於備份和還原活動。</span><span class="sxs-lookup"><span data-stu-id="91b4e-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="91b4e-239">啟用節流︰</span><span class="sxs-lookup"><span data-stu-id="91b4e-239">To enable throttling:</span></span>

1. <span data-ttu-id="91b4e-240">在**備份代理程式**中，按一下 [變更屬性]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="91b4e-241">在 [節流] 索引標籤上，選取 [啟用備份作業的網際網路頻寬使用節流功能]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-241">On the **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![網路節流](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="91b4e-243">一旦啟用節流之後，請指定允許在 [工作時間] 和 [非工作時間] 進行備份資料傳輸的頻寬。</span><span class="sxs-lookup"><span data-stu-id="91b4e-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="91b4e-244">頻寬值從每秒 512 KB (Kbps) 開始，並可高達每秒 1023 MB (Mbps)。</span><span class="sxs-lookup"><span data-stu-id="91b4e-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="91b4e-245">您也可以指定 [工作時間] 的開始和完成時間，以及一週中有哪幾天視為工作天。</span><span class="sxs-lookup"><span data-stu-id="91b4e-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="91b4e-246">指定工作時間以外的時間會視為非工作時間。</span><span class="sxs-lookup"><span data-stu-id="91b4e-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="91b4e-247">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="91b4e-248">管理排除設定</span><span class="sxs-lookup"><span data-stu-id="91b4e-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="91b4e-249">開啟 **Microsoft Azure 備份代理程式** (透過在電腦中搜尋「Microsoft Azure 備份」即可找到)。</span><span class="sxs-lookup"><span data-stu-id="91b4e-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="91b4e-251">在 Microsoft Azure 備份代理程式中，按一下 [排程備份] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="91b4e-253">在排程備份精靈中，讓 [變更備份項目或時間] 選項保留選取狀態，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="91b4e-255">按一下 [排除設定] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-255">Click **Exclusions Settings**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="91b4e-257">按一下 [新增排除] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-257">Click **Add Exclusion**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="91b4e-259">選取位置，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-259">Select the location and then, click **OK**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="91b4e-261">在 [檔案類型]  欄位中新增副檔名。</span><span class="sxs-lookup"><span data-stu-id="91b4e-261">Add the file extension in the **File Type** field.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="91b4e-263">新增 .mp3 副檔名</span><span class="sxs-lookup"><span data-stu-id="91b4e-263">Adding an .mp3 extension</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="91b4e-265">若要新增其他副檔名，可按一下 [新增排除]  ，然後輸入另一個副檔名 (新增 .jpeg 副檔名)。</span><span class="sxs-lookup"><span data-stu-id="91b4e-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="91b4e-267">當您已新增所有副檔名之後，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="91b4e-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="91b4e-268">按 [下一步] 繼續執行排程備份精靈， 直到出現 [確認] 頁面，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="91b4e-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="91b4e-270">常見問題集</span><span class="sxs-lookup"><span data-stu-id="91b4e-270">Frequently asked questions</span></span>
<span data-ttu-id="91b4e-271">**Q1.備份作業狀態在 Azure 備份代理程式中顯示為已完成，但為何不會立即反映在入口網站中？**</span><span class="sxs-lookup"><span data-stu-id="91b4e-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="91b4e-272">A1.</span><span class="sxs-lookup"><span data-stu-id="91b4e-272">A1.</span></span> <span data-ttu-id="91b4e-273">Azure 備份代理程式與 Azure 入口網站中反映的備份作業狀態之間最多有 15 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="91b4e-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="91b4e-274">**Q.2 當備份作業失敗時，需要多久的時間才會引發警示？**</span><span class="sxs-lookup"><span data-stu-id="91b4e-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="91b4e-275">A.2 在 Azure 備份失敗的 20 分鐘內就會引發警示。</span><span class="sxs-lookup"><span data-stu-id="91b4e-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="91b4e-276">**Q3.是否會有已設定通知但不會傳送電子郵件的情況？**</span><span class="sxs-lookup"><span data-stu-id="91b4e-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="91b4e-277">A3.</span><span class="sxs-lookup"><span data-stu-id="91b4e-277">A3.</span></span> <span data-ttu-id="91b4e-278">以下是不傳送通知以便減少警示雜訊的案例︰</span><span class="sxs-lookup"><span data-stu-id="91b4e-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="91b4e-279">如果通知設為每小時，而且在一小時內引發警示並加以解決，</span><span class="sxs-lookup"><span data-stu-id="91b4e-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="91b4e-280">作業便會取消。</span><span class="sxs-lookup"><span data-stu-id="91b4e-280">Job is canceled.</span></span>
* <span data-ttu-id="91b4e-281">第二個備份作業會失敗，因為原始的備份作業正在進行中。</span><span class="sxs-lookup"><span data-stu-id="91b4e-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="91b4e-282">疑難排解監視問題</span><span class="sxs-lookup"><span data-stu-id="91b4e-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="91b4e-283">**問題︰**來自 Azure 備份代理程式的作業與警示未出現在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="91b4e-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="91b4e-284">**疑難排解步驟︰**```OBRecoveryServicesManagementAgent``` 程序會將作業和警示資料傳送至 Azure 備份服務。</span><span class="sxs-lookup"><span data-stu-id="91b4e-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="91b4e-285">此程序可能偶爾會卡住或關閉。</span><span class="sxs-lookup"><span data-stu-id="91b4e-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="91b4e-286">若要確認此程序不在執行中，請開啟 [工作管理員] 並檢查 ```OBRecoveryServicesManagementAgent``` 程序是否正在執行中。</span><span class="sxs-lookup"><span data-stu-id="91b4e-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="91b4e-287">假設此程序不在執行中，請開啟 [控制台] 並瀏覽服務清單。</span><span class="sxs-lookup"><span data-stu-id="91b4e-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="91b4e-288">啟動或重新啟動 **Microsoft Azure 復原服務管理代理程式**。</span><span class="sxs-lookup"><span data-stu-id="91b4e-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="91b4e-289">如需進一步資訊，請瀏覽以下位置的記錄檔：</span><span class="sxs-lookup"><span data-stu-id="91b4e-289">For further information, browse the logs at:</span></span><br/><span data-ttu-id="91b4e-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` 例如：</span><span class="sxs-lookup"><span data-stu-id="91b4e-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="91b4e-291">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91b4e-291">Next steps</span></span>
* [<span data-ttu-id="91b4e-292">從 Azure 還原 Windows Server 或 Windows 用戶端</span><span class="sxs-lookup"><span data-stu-id="91b4e-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="91b4e-293">若要深入了解 Azure 備份，請參閱 [Azure 備份概觀](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="91b4e-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="91b4e-294">瀏覽 [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="91b4e-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
