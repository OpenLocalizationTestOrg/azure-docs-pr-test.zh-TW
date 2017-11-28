---
title: "aaaRecover 資料，從 Azure 備份伺服器 |Microsoft 文件"
description: "復原您所保護的 hello 資料 tooa 復原服務保存庫，從任何 Azure 備份伺服器已註冊的 toothat 保存庫。"
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
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a><span data-ttu-id="21d7d-103">從 Azure 備份伺服器復原資料</span><span class="sxs-lookup"><span data-stu-id="21d7d-103">Recover data from Azure Backup Server</span></span>
<span data-ttu-id="21d7d-104">您可以使用 Azure 備份伺服器 toorecover hello 資料，而您已備份的 tooa 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="21d7d-104">You can use Azure Backup Server toorecover hello data you've backed up tooa Recovery Services vault.</span></span> <span data-ttu-id="21d7d-105">hello 程序提供執行因此整合至 hello Azure 備份伺服器管理主控台中，並且其他 Azure 備份 」 元件類似 toohello 復原工作流程。</span><span class="sxs-lookup"><span data-stu-id="21d7d-105">hello process for doing so is integrated into hello Azure Backup Server management console, and is similar toohello recovery workflow for other Azure Backup components.</span></span>

> [!NOTE]
> <span data-ttu-id="21d7d-106">這篇文章僅適用於 [System Center Data Protection Manager 2012 R2 UR7 或更新版本] (https://support.microsoft.com/en-us/kb/3065246)，結合 hello[最新的 Azure 備份代理程式](http://aka.ms/azurebackup_agent)。</span><span class="sxs-lookup"><span data-stu-id="21d7d-106">This article is applicable for [System Center Data Protection Manager 2012 R2 with UR7 or later] (https://support.microsoft.com/en-us/kb/3065246), combined with hello [latest Azure Backup agent](http://aka.ms/azurebackup_agent).</span></span>
>
>

<span data-ttu-id="21d7d-107">toorecover 資料，從 Azure 備份伺服器：</span><span class="sxs-lookup"><span data-stu-id="21d7d-107">toorecover data from an Azure Backup Server:</span></span>

1. <span data-ttu-id="21d7d-108">從 hello**復原**索引標籤上的 hello Azure 備份伺服器管理主控台中，按一下**加入外部 DPM'** (在 hello 囉 」 畫面的左上角)。</span><span class="sxs-lookup"><span data-stu-id="21d7d-108">From hello **Recovery** tab of hello Azure Backup Server management console, click **'Add External DPM'** (at hello top left of hello screen).</span></span>   
    <span data-ttu-id="21d7d-109">![新增外部 DPM](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)</span><span class="sxs-lookup"><span data-stu-id="21d7d-109">![Add External DPM](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)</span></span>
2. <span data-ttu-id="21d7d-110">下載新**保存庫認證**hello hello 與相關聯的保存庫中**Azure 備份伺服器**其中要復原 hello 資料，從 Azure 備份伺服器 hello 清單中選擇 hello Azure 備份伺服器向 hello 復原服務保存庫，並提供 hello**加密複雜密碼**hello 伺服器要復原其資料相關聯。</span><span class="sxs-lookup"><span data-stu-id="21d7d-110">Download new **vault credentials** from hello vault associated with hello **Azure Backup Server** where hello data is being recovered, choose hello Azure Backup Server from hello list of Azure Backup Servers registered with hello Recovery Services vault, and provide hello **encryption passphrase** associated with hello server whose data is being recovered.</span></span>

    ![外部 DPM 認證](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > <span data-ttu-id="21d7d-112">僅 Azure 備份伺服器相關聯 hello 相同註冊保存庫可以復原彼此的資料。</span><span class="sxs-lookup"><span data-stu-id="21d7d-112">Only Azure Backup Servers associated with hello same registration vault can recover each other’s data.</span></span>
   >
   >

    <span data-ttu-id="21d7d-113">一旦 hello 外部的 Azure 備份伺服器成功加入，您可以瀏覽 hello 外部伺服器 hello 資料並 hello 本機的 Azure 備份伺服器，從 hello**復原** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="21d7d-113">Once hello External Azure Backup Server is successfully added, you can browse hello data of hello external server and hello local Azure Backup Server from hello **Recovery** tab.</span></span>
3. <span data-ttu-id="21d7d-114">瀏覽 hello 可用清單所保護的實際執行伺服器 hello 外部的 Azure 備份伺服器，並選取 hello 適當的資料來源。</span><span class="sxs-lookup"><span data-stu-id="21d7d-114">Browse hello available list of production servers protected by hello external Azure Backup Server and select hello appropriate data source.</span></span>

    ![瀏覽外部 DPM 伺服器](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. <span data-ttu-id="21d7d-116">選取**hello 的月份和年份**從 hello**復原點**下拉式清單選取所需的 hello**復原日期**的 hello 復原點時已建立，並選取 hello**復原時間**。</span><span class="sxs-lookup"><span data-stu-id="21d7d-116">Select **hello month and year** from hello **Recovery points** drop down, select hello required **Recovery date** for when hello recovery point was created, and select hello **Recovery time**.</span></span>

    <span data-ttu-id="21d7d-117">檔案和資料夾清單隨即出現在 hello 底部窗格中，可以瀏覽並復原 tooany 位置。</span><span class="sxs-lookup"><span data-stu-id="21d7d-117">A list of files and folders appears in hello bottom pane, which can be browsed and recovered tooany location.</span></span>

    ![外部 DPM 伺服器復原點](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. <span data-ttu-id="21d7d-119">以滑鼠右鍵按一下 hello 適當的項目，然後按一下**復原**。</span><span class="sxs-lookup"><span data-stu-id="21d7d-119">Right click hello appropriate item and click **Recover**.</span></span>

    ![外部 DPM 復原](./media/backup-azure-alternate-dpm-server/recover.png)
6. <span data-ttu-id="21d7d-121">檢閱 hello**復原選取項目**。</span><span class="sxs-lookup"><span data-stu-id="21d7d-121">Review hello **Recover Selection**.</span></span> <span data-ttu-id="21d7d-122">請確認 hello 資料和 hello 要復原的備份複本的時間以及 hello 來源從中建立 hello 備份複本。</span><span class="sxs-lookup"><span data-stu-id="21d7d-122">Verify hello data and time of hello backup copy being recovered, as well as hello source from which hello backup copy was created.</span></span> <span data-ttu-id="21d7d-123">如果 hello 選取範圍不正確，請按一下**取消**toonavigate 後 toorecovery 索引標籤 tooselect 適當的復原點。</span><span class="sxs-lookup"><span data-stu-id="21d7d-123">If hello selection is incorrect, click **Cancel** toonavigate back toorecovery tab tooselect appropriate recovery point.</span></span> <span data-ttu-id="21d7d-124">如果 hello 選擇正確時，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="21d7d-124">If hello selection is correct, click **Next**.</span></span>

    ![外部 DPM 復原摘要](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. <span data-ttu-id="21d7d-126">選取**復原 tooan 替代位置**。</span><span class="sxs-lookup"><span data-stu-id="21d7d-126">Select **Recover tooan alternate location**.</span></span> <span data-ttu-id="21d7d-127">**瀏覽**toohello hello 復原正確的位置。</span><span class="sxs-lookup"><span data-stu-id="21d7d-127">**Browse** toohello correct location for hello recovery.</span></span>

    ![外部 DPM 復原替代位置](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. <span data-ttu-id="21d7d-129">選擇相關太 hello 選項**建立複本**，**略過**，或**覆寫**。</span><span class="sxs-lookup"><span data-stu-id="21d7d-129">Choose hello option related too**create copy**, **Skip**, or **Overwrite**.</span></span>

   * <span data-ttu-id="21d7d-130">**建立複本**-建立 hello 檔案的副本，如果沒有名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="21d7d-130">**Create copy** - creates a copy of hello file if there is a name collision.</span></span>
   * <span data-ttu-id="21d7d-131">**略過**-如果有名稱衝突，這會將 hello 原始檔案 hello 檔案時無法復原。</span><span class="sxs-lookup"><span data-stu-id="21d7d-131">**Skip** - if there is a name collision, does not recover hello file which leaves hello original file.</span></span>
   * <span data-ttu-id="21d7d-132">**覆寫**-名稱衝突，是否會覆寫 hello 現有 hello 檔案副本。</span><span class="sxs-lookup"><span data-stu-id="21d7d-132">**Overwrite** - if there is a name collision, overwrites hello existing copy of hello file.</span></span>

     <span data-ttu-id="21d7d-133">選擇適當選項，hello 太**還原安全性**。</span><span class="sxs-lookup"><span data-stu-id="21d7d-133">Choose hello appropriate option too**Restore security**.</span></span> <span data-ttu-id="21d7d-134">您可以套用 hello 的 hello hello 資料要復原的目的地電腦的安全性設定或 hello 所適用的 tooproduct 次 hello hello 的復原點建立的安全性設定。</span><span class="sxs-lookup"><span data-stu-id="21d7d-134">You can apply hello security settings of hello destination computer where hello data is being recovered or hello security settings that were applicable tooproduct at hello time hello recovery point was created.</span></span>

     <span data-ttu-id="21d7d-135">識別是否**通知**傳送，一旦 hello 復原已成功完成。</span><span class="sxs-lookup"><span data-stu-id="21d7d-135">Identify whether a **Notification** is sent, once hello recovery successfully completes.</span></span>

     ![外部 DPM 復原通知](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. <span data-ttu-id="21d7d-137">hello**摘要**畫面會列出目前選擇的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="21d7d-137">hello **Summary** screen lists hello options chosen so far.</span></span> <span data-ttu-id="21d7d-138">一旦您按一下**「 復原 」**，hello 資料是復原的 toohello 適當的內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="21d7d-138">Once you click **‘Recover’**, hello data is recovered toohello appropriate on-premises location.</span></span>

    ![外部 DPM 復原選項摘要](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > <span data-ttu-id="21d7d-140">hello 復原工作可以監視在 hello**監視**hello Azure 備份伺服器 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="21d7d-140">hello recovery job can be monitored in hello **Monitoring** tab of hello Azure Backup Server.</span></span>
   >
   >

    ![監視復原](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. <span data-ttu-id="21d7d-142">您可以按一下**清除外部 DPM**上 hello**復原**hello hello 外部 DPM 伺服器的 DPM 伺服器 tooremove hello 檢視 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="21d7d-142">You can click **Clear External DPM** on hello **Recovery** tab of hello DPM server tooremove hello view of hello external DPM server.</span></span>

    ![清除外部 DPM](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a><span data-ttu-id="21d7d-144">疑難排解錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="21d7d-144">Troubleshooting Error Messages</span></span>
| <span data-ttu-id="21d7d-145">否。</span><span class="sxs-lookup"><span data-stu-id="21d7d-145">No.</span></span> | <span data-ttu-id="21d7d-146">錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="21d7d-146">Error Message</span></span> | <span data-ttu-id="21d7d-147">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="21d7d-147">Troubleshooting steps</span></span> |
|:---:|:--- |:--- |
| <span data-ttu-id="21d7d-148">1.</span><span class="sxs-lookup"><span data-stu-id="21d7d-148">1.</span></span> |<span data-ttu-id="21d7d-149">此伺服器未註冊的 toohello hello 保存庫認證所指定的保存庫。</span><span class="sxs-lookup"><span data-stu-id="21d7d-149">This server is not registered toohello vault specified by hello vault credential.</span></span> |<span data-ttu-id="21d7d-150">**原因：**會出現這個錯誤時 hello 保存庫認證檔案選取不屬於的 toohello 復原服務保存庫相關聯 Azure 備份伺服器的 hello 嘗試修復。</span><span class="sxs-lookup"><span data-stu-id="21d7d-150">**Cause:** This error appears when hello vault credential file selected does not belong toohello Recovery Services vault associated with Azure Backup Server on which hello recovery is attempted.</span></span> <br> <span data-ttu-id="21d7d-151">**解決方式：**下載 hello 保存庫認證檔案從 hello 復原服務保存庫 toowhich hello 註冊 Azure 備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="21d7d-151">**Resolution:** Download hello vault credential file from hello Recovery Services vault toowhich hello Azure Backup Server is registered.</span></span> |
| <span data-ttu-id="21d7d-152">2.</span><span class="sxs-lookup"><span data-stu-id="21d7d-152">2.</span></span> |<span data-ttu-id="21d7d-153">Hello 可復原的資料無法使用，或 hello 選取的伺服器不是 DPM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="21d7d-153">Either hello recoverable data is not available or hello selected server is not a DPM server.</span></span> |<span data-ttu-id="21d7d-154">**原因：**有沒有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，或伺服器 hello 您尚未尚未上傳 hello 中繼資料，或是 hello 選取的伺服器不是 Azure 備份伺服器 （也稱為 Windows Server 或 Windows 用戶端）。</span><span class="sxs-lookup"><span data-stu-id="21d7d-154">**Cause:** There are no other Azure Backup Servers registered toohello Recovery Services vault, or hello servers have not yet uploaded hello metadata, or hello selected server is not an Azure Backup Server (aka Windows Server or Windows Client).</span></span> <br> <span data-ttu-id="21d7d-155">**解決方式：**如果有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，請確定該 hello 最新 Azure 備份代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="21d7d-155">**Resolution:** If there are other Azure Backup Servers registered toohello Recovery Services vault, ensure that hello latest Azure Backup agent is installed.</span></span> <br><span data-ttu-id="21d7d-156">如果有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，請等候一天後安裝 toostart hello 復原程序。</span><span class="sxs-lookup"><span data-stu-id="21d7d-156">If there are other Azure Backup Servers registered toohello Recovery Services vault, wait for a day after installation toostart hello recovery process.</span></span> <span data-ttu-id="21d7d-157">hello 夜間工作都會將上傳所有受保護的 hello 備份 toocloud hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="21d7d-157">hello nightly job will upload hello metadata for all hello protected backups toocloud.</span></span> <span data-ttu-id="21d7d-158">hello 資料可供復原。</span><span class="sxs-lookup"><span data-stu-id="21d7d-158">hello data will be available for recovery.</span></span> |
| <span data-ttu-id="21d7d-159">3.</span><span class="sxs-lookup"><span data-stu-id="21d7d-159">3.</span></span> |<span data-ttu-id="21d7d-160">沒有其他 DPM 伺服器是已註冊的 toothis 保存庫。</span><span class="sxs-lookup"><span data-stu-id="21d7d-160">No other DPM server is registered toothis vault.</span></span> |<span data-ttu-id="21d7d-161">**原因：**沒有其他 Azure 備份伺服器的已註冊的 toohello 保存庫中的 hello 嘗試修復。</span><span class="sxs-lookup"><span data-stu-id="21d7d-161">**Cause:** There are no other Azure Backup Servers  that are registered toohello vault from which hello recovery is being attempted.</span></span><br><span data-ttu-id="21d7d-162">**解決方式：**如果有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，請確定該 hello 最新 Azure 備份代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="21d7d-162">**Resolution:** If there are other Azure Backup Servers registered toohello Recovery Services vault, ensure that hello latest Azure Backup agent is installed.</span></span><br><span data-ttu-id="21d7d-163">如果有其他 Azure 備份伺服器已註冊的 toohello 復原服務保存庫，請等候一天後安裝 toostart hello 復原程序。</span><span class="sxs-lookup"><span data-stu-id="21d7d-163">If there are other Azure Backup Servers registered toohello Recovery Services vault, wait for a day after installation toostart hello recovery process.</span></span> <span data-ttu-id="21d7d-164">hello 夜間工作會上傳所有受保護的備份 toocloud hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="21d7d-164">hello nightly job uploads hello metadata for all protected backups toocloud.</span></span> <span data-ttu-id="21d7d-165">hello 資料可供復原。</span><span class="sxs-lookup"><span data-stu-id="21d7d-165">hello data will be available for recovery.</span></span> |
| <span data-ttu-id="21d7d-166">4.</span><span class="sxs-lookup"><span data-stu-id="21d7d-166">4.</span></span> |<span data-ttu-id="21d7d-167">提供的 hello 加密複雜密碼不符合以 hello 下列伺服器關聯的複雜密碼：**<server name>**</span><span class="sxs-lookup"><span data-stu-id="21d7d-167">hello encryption passphrase provided does not match with passphrase associated with hello following server: **<server name>**</span></span> |<span data-ttu-id="21d7d-168">**原因：** hello hello 加密 hello hello Azure 備份伺服器的資料要復原資料的程序中使用的加密複雜密碼不符合提供的 hello 加密複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="21d7d-168">**Cause:** hello encryption passphrase used in hello process of encrypting hello data from hello Azure Backup Server’s data that is being recovered does not match hello encryption passphrase provided.</span></span> <span data-ttu-id="21d7d-169">hello 代理程式是無法 toodecrypt hello 資料。</span><span class="sxs-lookup"><span data-stu-id="21d7d-169">hello agent is unable toodecrypt hello data.</span></span> <span data-ttu-id="21d7d-170">因此 hello 復原會失敗。</span><span class="sxs-lookup"><span data-stu-id="21d7d-170">Hence hello recovery fails.</span></span><br><span data-ttu-id="21d7d-171">**解決方式：**請提供 hello 完全相同的加密複雜密碼與 hello 要復原其資料的 Azure 備份伺服器相關聯。</span><span class="sxs-lookup"><span data-stu-id="21d7d-171">**Resolution:** Please provide hello exact same encryption passphrase associated with hello Azure Backup Server whose data is being recovered.</span></span> |

## <a name="frequently-asked-questions"></a><span data-ttu-id="21d7d-172">常見問題集</span><span class="sxs-lookup"><span data-stu-id="21d7d-172">Frequently asked questions</span></span>

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a><span data-ttu-id="21d7d-173">為什麼不能在安裝 UR7 和最新的 Azure 備份代理程式之後，從另一部 DPM 伺服器新增外部 DPM 伺服器？</span><span class="sxs-lookup"><span data-stu-id="21d7d-173">Why can’t I add an external DPM server after installing UR7 and latest Azure Backup agent?</span></span>

<span data-ttu-id="21d7d-174">Hello 屬於資料來源的 DPM 伺服器受保護的雲端 toohello （透過早於更新彙總套件 7 使用更新彙總套件），您必須等待至少一天後安裝 hello UR7 和最新的 Azure Backup agent，toostart**加入外部 DPM 伺服器**.</span><span class="sxs-lookup"><span data-stu-id="21d7d-174">For hello DPM servers with data sources that are protected toohello cloud (by using an update rollup earlier than Update Rollup 7), you must wait at least one day after installing hello UR7 and latest Azure Backup agent, toostart **Add External DPM server**.</span></span> <span data-ttu-id="21d7d-175">hello 一天時間週期為 hello DPM 保護群組 tooAzure 需要的 tooupload hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="21d7d-175">hello one-day time period is needed tooupload hello metadata of hello DPM protection groups tooAzure.</span></span> <span data-ttu-id="21d7d-176">保護群組的中繼資料上傳 hello 透過夜間工作的第一次。</span><span class="sxs-lookup"><span data-stu-id="21d7d-176">Protection group metadata is uploaded hello first time through a nightly job.</span></span>

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a><span data-ttu-id="21d7d-177">Hello hello Microsoft Azure 復原服務代理程式所需的最小版本為何？</span><span class="sxs-lookup"><span data-stu-id="21d7d-177">What is hello minimum version of hello Microsoft Azure Recovery Services agent needed?</span></span>

<span data-ttu-id="21d7d-178">hello 最小版本 hello Microsoft Azure 復原服務代理程式或 Azure 備份代理程式，需要 tooenable 這項功能是 2.0.8719.0。</span><span class="sxs-lookup"><span data-stu-id="21d7d-178">hello minimum version of hello Microsoft Azure Recovery Services agent, or Azure Backup agent, required tooenable this feature is 2.0.8719.0.</span></span>  <span data-ttu-id="21d7d-179">tooview hello 代理程式的版本： 開啟 控制台 **>** 所有控制台項目 **>** 程式和功能 **>** Microsoft Azure Recovery Services Agent。</span><span class="sxs-lookup"><span data-stu-id="21d7d-179">tooview hello agent's version: open Control Panel **>** All Control Panel items **>** Programs and features **>** Microsoft Azure Recovery Services Agent.</span></span> <span data-ttu-id="21d7d-180">如果是小於 2.0.8719.0 hello 版，下載並安裝 hello[最新的 Azure 備份代理程式](https://go.microsoft.com/fwLink/?LinkID=288905)。</span><span class="sxs-lookup"><span data-stu-id="21d7d-180">If hello version is less than 2.0.8719.0, download and install hello [latest Azure Backup agent](https://go.microsoft.com/fwLink/?LinkID=288905).</span></span>

![清除外部 DPM](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a><span data-ttu-id="21d7d-182">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="21d7d-182">Next steps:</span></span>
<span data-ttu-id="21d7d-183">•    [Azure 備份常見問題集](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="21d7d-183">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
