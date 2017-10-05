---
title: "從 Azure 備份伺服器復原資料 | Microsoft Docs"
description: "從登錄至復原服務保存庫的任何 Azure 備份伺服器，復原該保存庫中保護的資料。"
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 688d155b68bc2d76d53f78d251bc2f659582845f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="recover-data-from-azure-backup-server"></a><span data-ttu-id="130df-103">從 Azure 備份伺服器復原資料</span><span class="sxs-lookup"><span data-stu-id="130df-103">Recover data from Azure Backup Server</span></span>
<span data-ttu-id="130df-104">您可以使用 Azure 備份伺服器，將您已備份到復原服務保存庫的資料復原。</span><span class="sxs-lookup"><span data-stu-id="130df-104">You can use Azure Backup Server to recover the data you've backed up to a Recovery Services vault.</span></span> <span data-ttu-id="130df-105">要這麼做的程序就是整合到 Azure 備份伺服器管理主控台，且類似於其他 Azure 備份元件的復原工作流程。</span><span class="sxs-lookup"><span data-stu-id="130df-105">The process for doing so is integrated into the Azure Backup Server management console, and is similar to the recovery workflow for other Azure Backup components.</span></span>

> [!NOTE]
> <span data-ttu-id="130df-106">本文適用於 [System Center Data Protection Manager 2012 R2 with UR7 或更新版本] (https://support.microsoft.com/en-us/kb/3065246)，結合[最新版的 Azure 備份代理程式](http://aka.ms/azurebackup_agent)。</span><span class="sxs-lookup"><span data-stu-id="130df-106">This article is applicable for [System Center Data Protection Manager 2012 R2 with UR7 or later] (https://support.microsoft.com/en-us/kb/3065246), combined with the [latest Azure Backup agent](http://aka.ms/azurebackup_agent).</span></span>
>
>

<span data-ttu-id="130df-107">若要從 Azure 備份伺服器復原資料：</span><span class="sxs-lookup"><span data-stu-id="130df-107">To recover data from an Azure Backup Server:</span></span>

1. <span data-ttu-id="130df-108">在 Azure 備份伺服器管理主控台的 [復原] 索引標籤中，按一下 [新增外部 DPM] \(在畫面左上方)。</span><span class="sxs-lookup"><span data-stu-id="130df-108">From the **Recovery** tab of the Azure Backup Server management console, click **'Add External DPM'** (at the top left of the screen).</span></span>   
    <span data-ttu-id="130df-109">![新增外部 DPM](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)</span><span class="sxs-lookup"><span data-stu-id="130df-109">![Add External DPM](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)</span></span>
2. <span data-ttu-id="130df-110">從與要復原資料的 **Azure 備份伺服器**關聯的保存庫下載新的**保存庫認證**、從已向復原服務保存庫登錄的 Azure 備份伺服器清單中選擇 Azure 備份伺服器，並提供與要復原資料的伺服器關聯的**加密複雜密碼**。</span><span class="sxs-lookup"><span data-stu-id="130df-110">Download new **vault credentials** from the vault associated with the **Azure Backup Server** where the data is being recovered, choose the Azure Backup Server from the list of Azure Backup Servers registered with the Recovery Services vault, and provide the **encryption passphrase** associated with the server whose data is being recovered.</span></span>

    ![外部 DPM 認證](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > <span data-ttu-id="130df-112">只有與相同登錄保存庫相關聯的 Azure 備份伺服器，才可以復原彼此的資料。</span><span class="sxs-lookup"><span data-stu-id="130df-112">Only Azure Backup Servers associated with the same registration vault can recover each other’s data.</span></span>
   >
   >

    <span data-ttu-id="130df-113">順利新增外部 Azure 備份伺服器之後，您就可以從 [復原] 索引標籤瀏覽外部伺服器和本機 Azure 備份伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="130df-113">Once the External Azure Backup Server is successfully added, you can browse the data of the external server and the local Azure Backup Server from the **Recovery** tab.</span></span>
3. <span data-ttu-id="130df-114">瀏覽由外部 Azure 備份伺服器保護的實際執行伺服器可用清單，並選取適當的資料來源。</span><span class="sxs-lookup"><span data-stu-id="130df-114">Browse the available list of production servers protected by the external Azure Backup Server and select the appropriate data source.</span></span>

    ![瀏覽外部 DPM 伺服器](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. <span data-ttu-id="130df-116">從 [復原點] 下拉式清單中選取「月份和年份」，選取代表復原點何時建立的必要 [復原日期]，並選取 [復原時間]。</span><span class="sxs-lookup"><span data-stu-id="130df-116">Select **the month and year** from the **Recovery points** drop down, select the required **Recovery date** for when the recovery point was created, and select the **Recovery time**.</span></span>

    <span data-ttu-id="130df-117">檔案和資料夾清單會出現在底部窗格中，方便您瀏覽並復原到任何位置。</span><span class="sxs-lookup"><span data-stu-id="130df-117">A list of files and folders appears in the bottom pane, which can be browsed and recovered to any location.</span></span>

    ![外部 DPM 伺服器復原點](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. <span data-ttu-id="130df-119">在適當的項目上按一下滑鼠右鍵，然後按一下 [復原] 。</span><span class="sxs-lookup"><span data-stu-id="130df-119">Right click the appropriate item and click **Recover**.</span></span>

    ![外部 DPM 復原](./media/backup-azure-alternate-dpm-server/recover.png)
6. <span data-ttu-id="130df-121">檢閱「復原選取項目」 。</span><span class="sxs-lookup"><span data-stu-id="130df-121">Review the **Recover Selection**.</span></span> <span data-ttu-id="130df-122">請確認要復原之備份複本的資料和時間，以及建立備份複本的來源。</span><span class="sxs-lookup"><span data-stu-id="130df-122">Verify the data and time of the backup copy being recovered, as well as the source from which the backup copy was created.</span></span> <span data-ttu-id="130df-123">如果選取項目不正確，請按一下 [取消]  ，往回瀏覽至 [復原] 索引標籤，以選取適當的復原點。</span><span class="sxs-lookup"><span data-stu-id="130df-123">If the selection is incorrect, click **Cancel** to navigate back to recovery tab to select appropriate recovery point.</span></span> <span data-ttu-id="130df-124">如果選取項目正確，請按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="130df-124">If the selection is correct, click **Next**.</span></span>

    ![外部 DPM 復原摘要](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. <span data-ttu-id="130df-126">選取 [復原到替代位置] 。</span><span class="sxs-lookup"><span data-stu-id="130df-126">Select **Recover to an alternate location**.</span></span> <span data-ttu-id="130df-127"> 到正確的復原位置。</span><span class="sxs-lookup"><span data-stu-id="130df-127">**Browse** to the correct location for the recovery.</span></span>

    ![外部 DPM 復原替代位置](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. <span data-ttu-id="130df-129">選擇與 [建立複本]、[略過] 或 [覆寫] 相關的選項。</span><span class="sxs-lookup"><span data-stu-id="130df-129">Choose the option related to **create copy**, **Skip**, or **Overwrite**.</span></span>

   * <span data-ttu-id="130df-130">**建立複本** - 會在名稱有衝突時，建立一份檔案的複本。</span><span class="sxs-lookup"><span data-stu-id="130df-130">**Create copy** - creates a copy of the file if there is a name collision.</span></span>
   * <span data-ttu-id="130df-131">**跳過** - 如果名稱有衝突，就不會復原離開原始檔的檔案。</span><span class="sxs-lookup"><span data-stu-id="130df-131">**Skip** - if there is a name collision, does not recover the file which leaves the original file.</span></span>
   * <span data-ttu-id="130df-132">**覆寫** - 如果名稱有衝突，就會覆寫檔案的現有副本。</span><span class="sxs-lookup"><span data-stu-id="130df-132">**Overwrite** - if there is a name collision, overwrites the existing copy of the file.</span></span>

     <span data-ttu-id="130df-133">請選擇適當的選項來「還原安全性」 。</span><span class="sxs-lookup"><span data-stu-id="130df-133">Choose the appropriate option to **Restore security**.</span></span> <span data-ttu-id="130df-134">您可以在建立復原點時，針對將資料復原至其中的目的地電腦，套用其安全性設定，或是套用適用於產品的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="130df-134">You can apply the security settings of the destination computer where the data is being recovered or the security settings that were applicable to product at the time the recovery point was created.</span></span>

     <span data-ttu-id="130df-135">確認是否要在復原成功完成後，傳送「通知」。</span><span class="sxs-lookup"><span data-stu-id="130df-135">Identify whether a **Notification** is sent, once the recovery successfully completes.</span></span>

     ![外部 DPM 復原通知](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. <span data-ttu-id="130df-137">[摘要]  畫面會列出到目前為止已選擇的選項。</span><span class="sxs-lookup"><span data-stu-id="130df-137">The **Summary** screen lists the options chosen so far.</span></span> <span data-ttu-id="130df-138">按一下 [復原] 之後，資料就會復原到適當的內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="130df-138">Once you click **‘Recover’**, the data is recovered to the appropriate on-premises location.</span></span>

    ![外部 DPM 復原選項摘要](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > <span data-ttu-id="130df-140">您可以在 Azure 備份伺服器的 [監視] 索引標籤中監視復原作業。</span><span class="sxs-lookup"><span data-stu-id="130df-140">The recovery job can be monitored in the **Monitoring** tab of the Azure Backup Server.</span></span>
   >
   >

    ![監視復原](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. <span data-ttu-id="130df-142">您可以在 DPM 伺服器的 [復原] 索引標籤上，按一下 [清除外部 DPM]，以移除外部 DPM 伺服器的檢視。</span><span class="sxs-lookup"><span data-stu-id="130df-142">You can click **Clear External DPM** on the **Recovery** tab of the DPM server to remove the view of the external DPM server.</span></span>

    ![清除外部 DPM](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a><span data-ttu-id="130df-144">疑難排解錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="130df-144">Troubleshooting Error Messages</span></span>
| <span data-ttu-id="130df-145">否。</span><span class="sxs-lookup"><span data-stu-id="130df-145">No.</span></span> | <span data-ttu-id="130df-146">錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="130df-146">Error Message</span></span> | <span data-ttu-id="130df-147">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="130df-147">Troubleshooting steps</span></span> |
|:---:|:--- |:--- |
| <span data-ttu-id="130df-148">1.</span><span class="sxs-lookup"><span data-stu-id="130df-148">1.</span></span> |<span data-ttu-id="130df-149">保存庫認證所指定的保存庫中未登錄此伺服器。</span><span class="sxs-lookup"><span data-stu-id="130df-149">This server is not registered to the vault specified by the vault credential.</span></span> |<span data-ttu-id="130df-150">**原因：**如果選取的保存庫認證檔案不屬於與所嘗試復原之 Azure 備份伺服器關聯的復原服務保存庫，就會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="130df-150">**Cause:** This error appears when the vault credential file selected does not belong to the Recovery Services vault associated with Azure Backup Server on which the recovery is attempted.</span></span> <br> <span data-ttu-id="130df-151">**解決方法：**從已登錄 Azure 備份伺服器的復原服務保存庫下載保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="130df-151">**Resolution:** Download the vault credential file from the Recovery Services vault to which the Azure Backup Server is registered.</span></span> |
| <span data-ttu-id="130df-152">2.</span><span class="sxs-lookup"><span data-stu-id="130df-152">2.</span></span> |<span data-ttu-id="130df-153">可復原資料無法使用，或選取的伺服器不是 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="130df-153">Either the recoverable data is not available or the selected server is not a DPM server.</span></span> |<span data-ttu-id="130df-154">**原因：**沒有任何其他 Azure 備份伺服器已向復原服務保存庫登錄，或伺服器尚未上傳中繼資料，或選取的伺服器不是 Azure 備份伺服器 (也稱為 Windows Server 或 Windows 用戶端)。</span><span class="sxs-lookup"><span data-stu-id="130df-154">**Cause:** There are no other Azure Backup Servers registered to the Recovery Services vault, or the servers have not yet uploaded the metadata, or the selected server is not an Azure Backup Server (aka Windows Server or Windows Client).</span></span> <br> <span data-ttu-id="130df-155">**解決方法：**如果有其他已向復原服務保存庫登錄的 Azure 備份伺服器，請確定已安裝最新的 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="130df-155">**Resolution:** If there are other Azure Backup Servers registered to the Recovery Services vault, ensure that the latest Azure Backup agent is installed.</span></span> <br><span data-ttu-id="130df-156">如果有其他 Azure 備份伺服器已向復原服務保存庫登錄，請在安裝後等候一天，再開始復原程序。</span><span class="sxs-lookup"><span data-stu-id="130df-156">If there are other Azure Backup Servers registered to the Recovery Services vault, wait for a day after installation to start the recovery process.</span></span> <span data-ttu-id="130df-157">夜間作業會針對所有受保護的備份，將中繼資料上傳至雲端。</span><span class="sxs-lookup"><span data-stu-id="130df-157">The nightly job will upload the metadata for all the protected backups to cloud.</span></span> <span data-ttu-id="130df-158">資料將可供復原。</span><span class="sxs-lookup"><span data-stu-id="130df-158">The data will be available for recovery.</span></span> |
| <span data-ttu-id="130df-159">3.</span><span class="sxs-lookup"><span data-stu-id="130df-159">3.</span></span> |<span data-ttu-id="130df-160">此保存庫未登錄其他 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="130df-160">No other DPM server is registered to this vault.</span></span> |<span data-ttu-id="130df-161">**原因︰**沒有任何其他 Azure 備份伺服器已向嘗試復原的保存庫登錄。</span><span class="sxs-lookup"><span data-stu-id="130df-161">**Cause:** There are no other Azure Backup Servers  that are registered to the vault from which the recovery is being attempted.</span></span><br><span data-ttu-id="130df-162">**解決方法：**如果有其他已向復原服務保存庫登錄的 Azure 備份伺服器，請確定已安裝最新的 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="130df-162">**Resolution:** If there are other Azure Backup Servers registered to the Recovery Services vault, ensure that the latest Azure Backup agent is installed.</span></span><br><span data-ttu-id="130df-163">如果有其他 Azure 備份伺服器已向復原服務保存庫登錄，請在安裝後等候一天，再開始復原程序。</span><span class="sxs-lookup"><span data-stu-id="130df-163">If there are other Azure Backup Servers registered to the Recovery Services vault, wait for a day after installation to start the recovery process.</span></span> <span data-ttu-id="130df-164">夜間作業會針對所有受保護的備份，將中繼資料上傳至雲端。</span><span class="sxs-lookup"><span data-stu-id="130df-164">The nightly job uploads the metadata for all protected backups to cloud.</span></span> <span data-ttu-id="130df-165">資料將可供復原。</span><span class="sxs-lookup"><span data-stu-id="130df-165">The data will be available for recovery.</span></span> |
| <span data-ttu-id="130df-166">4.</span><span class="sxs-lookup"><span data-stu-id="130df-166">4.</span></span> |<span data-ttu-id="130df-167">提供的加密複雜密碼與下列伺服器關聯的複雜密碼不相符： **<server name>**</span><span class="sxs-lookup"><span data-stu-id="130df-167">The encryption passphrase provided does not match with passphrase associated with the following server: **<server name>**</span></span> |<span data-ttu-id="130df-168">**原因：**在加密來自要復原之 Azure 備份伺服器的資料過程中使用的加密複雜密碼，與所提供的加密複雜密碼不符。</span><span class="sxs-lookup"><span data-stu-id="130df-168">**Cause:** The encryption passphrase used in the process of encrypting the data from the Azure Backup Server’s data that is being recovered does not match the encryption passphrase provided.</span></span> <span data-ttu-id="130df-169">代理程式無法解密資料。</span><span class="sxs-lookup"><span data-stu-id="130df-169">The agent is unable to decrypt the data.</span></span> <span data-ttu-id="130df-170">因此復原失敗。</span><span class="sxs-lookup"><span data-stu-id="130df-170">Hence the recovery fails.</span></span><br><span data-ttu-id="130df-171">**解決方法：**請提供與要復原資料的 Azure 備份伺服器關聯且完全相同的加密複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="130df-171">**Resolution:** Please provide the exact same encryption passphrase associated with the Azure Backup Server whose data is being recovered.</span></span> |

## <a name="frequently-asked-questions"></a><span data-ttu-id="130df-172">常見問題集</span><span class="sxs-lookup"><span data-stu-id="130df-172">Frequently asked questions</span></span>

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a><span data-ttu-id="130df-173">為什麼不能在安裝 UR7 和最新的 Azure 備份代理程式之後，從另一部 DPM 伺服器新增外部 DPM 伺服器？</span><span class="sxs-lookup"><span data-stu-id="130df-173">Why can’t I add an external DPM server after installing UR7 and latest Azure Backup agent?</span></span>

<span data-ttu-id="130df-174">針對資料來源已在雲端受保護 (藉由使用比「更新彙總套件 7」舊的更新彙總套件進行保護) 的 DPM 伺服器，您必須在安裝 UR7 和最新的 Azure 備份代理程式之後至少等候一天，再開始「新增外部 DPM 伺服器」。</span><span class="sxs-lookup"><span data-stu-id="130df-174">For the DPM servers with data sources that are protected to the cloud (by using an update rollup earlier than Update Rollup 7), you must wait at least one day after installing the UR7 and latest Azure Backup agent, to start **Add External DPM server**.</span></span> <span data-ttu-id="130df-175">需要一天的時間才能將 DPM 保護群組的中繼資料上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="130df-175">The one-day time period is needed to upload the metadata of the DPM protection groups to Azure.</span></span> <span data-ttu-id="130df-176">保護群組中繼資料第一次會透過夜間作業上傳。</span><span class="sxs-lookup"><span data-stu-id="130df-176">Protection group metadata is uploaded the first time through a nightly job.</span></span>

### <a name="what-is-the-minimum-version-of-the-microsoft-azure-recovery-services-agent-needed"></a><span data-ttu-id="130df-177">Microsoft Azure 復原服務代理程式所需的最低版本是什麼？</span><span class="sxs-lookup"><span data-stu-id="130df-177">What is the minimum version of the Microsoft Azure Recovery Services agent needed?</span></span>

<span data-ttu-id="130df-178">啟用這項功能所需的 Microsoft Azure 復原服務代理程式或 Azure 備份代理程式的最低版本是 2.0.8719.0。</span><span class="sxs-lookup"><span data-stu-id="130df-178">The minimum version of the Microsoft Azure Recovery Services agent, or Azure Backup agent, required to enable this feature is 2.0.8719.0.</span></span>  <span data-ttu-id="130df-179">若要檢視代理程式的版本：開啟 [控制台]**>**[所有控制台項目]**>**[程式和功能]**>**[Microsoft Azure 復原服務代理程式]。</span><span class="sxs-lookup"><span data-stu-id="130df-179">To view the agent's version: open Control Panel **>** All Control Panel items **>** Programs and features **>** Microsoft Azure Recovery Services Agent.</span></span> <span data-ttu-id="130df-180">如果版本低於 2.0.8719.0，請下載及安裝[最新的 Azure 備份代理程式](https://go.microsoft.com/fwLink/?LinkID=288905)。</span><span class="sxs-lookup"><span data-stu-id="130df-180">If the version is less than 2.0.8719.0, download and install the [latest Azure Backup agent](https://go.microsoft.com/fwLink/?LinkID=288905).</span></span>

![清除外部 DPM](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a><span data-ttu-id="130df-182">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="130df-182">Next steps:</span></span>
<span data-ttu-id="130df-183">•    [Azure 備份常見問題集](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="130df-183">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
