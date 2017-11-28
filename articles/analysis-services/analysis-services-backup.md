---
title: "aaaAzure Analysis Services 資料庫備份和還原 |Microsoft 文件"
description: "描述如何 toobackup 和還原 Azure Analysis Services 資料庫。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="17577-103">備份與還原</span><span class="sxs-lookup"><span data-stu-id="17577-103">Backup and restore</span></span>

<span data-ttu-id="17577-104">備份 Azure Analysis Services 中的表格式模型資料庫是大部分相同 hello 與內部部署 Analysis Services。</span><span class="sxs-lookup"><span data-stu-id="17577-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="17577-105">hello 的主要差異是您用來儲存備份檔案。</span><span class="sxs-lookup"><span data-stu-id="17577-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="17577-106">備份檔案必須儲存在 tooa 容器[Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="17577-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="17577-107">您可以使用您已經有的儲存體帳戶和容器，或是在為您的伺服器設定儲存體設定時再建立帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="17577-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="17577-108">建立儲存體帳戶會導致產生新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="17577-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="17577-109">詳細資訊，請參閱 toolearn [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/blobs/)。</span><span class="sxs-lookup"><span data-stu-id="17577-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="17577-110">備份會以 .abf 副檔名儲存。</span><span class="sxs-lookup"><span data-stu-id="17577-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="17577-111">針對記憶體內表格式模型，會同時儲存模型資料和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="17577-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="17577-112">針對 DirectQuery 表格式模型，則只會儲存模型中繼資料。</span><span class="sxs-lookup"><span data-stu-id="17577-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="17577-113">備份可以壓縮和加密，依據您選擇的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="17577-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="17577-114">設定儲存體設定</span><span class="sxs-lookup"><span data-stu-id="17577-114">Configure storage settings</span></span>
<span data-ttu-id="17577-115">之前備份，您會需要 tooconfigure 存放裝置設定為您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="17577-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="17577-116">tooconfigure 存放裝置設定</span><span class="sxs-lookup"><span data-stu-id="17577-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="17577-117">在 Azure 入口網站 > [設定] 中，按一下 [備份]。</span><span class="sxs-lookup"><span data-stu-id="17577-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![[設定] 中的 [備份]](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="17577-119">按一下 [已啟用]，然後按一下 [儲存體設定]。</span><span class="sxs-lookup"><span data-stu-id="17577-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![啟用](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="17577-121">選取您的儲存體帳戶，或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="17577-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="17577-122">選取容器，或建立新容器。</span><span class="sxs-lookup"><span data-stu-id="17577-122">Select a container or create a new one.</span></span>

    ![選取容器](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="17577-124">儲存您的備份設定。</span><span class="sxs-lookup"><span data-stu-id="17577-124">Save your backup settings.</span></span>

    ![儲存備份設定](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="17577-126">備份</span><span class="sxs-lookup"><span data-stu-id="17577-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="17577-127">使用 SSMS toobackup</span><span class="sxs-lookup"><span data-stu-id="17577-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="17577-128">在 SSMS 中，於資料庫上按一下滑鼠右鍵 > [備份]。</span><span class="sxs-lookup"><span data-stu-id="17577-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="17577-129">在 [備份資料庫] > [備份檔案] 中，按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="17577-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="17577-130">在 [hello**另存新檔**] 對話方塊中，確認 hello 資料夾路徑，，，然後輸入 hello 備份檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="17577-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="17577-131">在 hello **Backup Database**對話方塊中，選取選項。</span><span class="sxs-lookup"><span data-stu-id="17577-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="17577-132">**允許檔案覆寫**-選取 hello 這個選項 toooverwrite 備份檔案相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="17577-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="17577-133">如果未選取此選項，您所儲存的 hello 檔案不能有名稱相同的 hello 做為檔案已存在於 hello 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="17577-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="17577-134">**套用壓縮**-選取這個選項 toocompress hello 備份檔案。</span><span class="sxs-lookup"><span data-stu-id="17577-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="17577-135">壓縮過的備份檔案可節省磁碟空間，但需要使用稍微多一點的 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="17577-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="17577-136">**加密備份檔案**-選取這個選項 tooencrypt hello 備份檔案。</span><span class="sxs-lookup"><span data-stu-id="17577-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="17577-137">此選項需要使用者提供的密碼 toosecure hello 備份檔案。</span><span class="sxs-lookup"><span data-stu-id="17577-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="17577-138">hello 密碼可防止讀取 hello 備份資料的還原作業以外的任何其他方式。</span><span class="sxs-lookup"><span data-stu-id="17577-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="17577-139">如果您選擇 tooencrypt 備份，請將 hello 密碼儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="17577-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="17577-140">按一下**確定**toocreate 儲存 hello 備份檔案。</span><span class="sxs-lookup"><span data-stu-id="17577-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="17577-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="17577-141">PowerShell</span></span>
<span data-ttu-id="17577-142">使用 [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17577-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="17577-143">還原</span><span class="sxs-lookup"><span data-stu-id="17577-143">Restore</span></span>
<span data-ttu-id="17577-144">還原時，您的備份檔案必須是您已設定為您的伺服器 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="17577-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="17577-145">如果您需要 toomove 備份檔案從內部部署位置 tooyour 儲存體帳戶，請使用[Microsoft Azure 儲存體總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)或 hello [AzCopy](../storage/common/storage-use-azcopy.md)命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="17577-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="17577-146">如果您正在從內部部署伺服器中還原，您必須從 hello 模型的角色中移除所有的 hello 網域使用者，並將其加入回 toohello 角色做為 Azure Active Directory 的使用者。</span><span class="sxs-lookup"><span data-stu-id="17577-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="17577-147">使用 SSMS toorestore</span><span class="sxs-lookup"><span data-stu-id="17577-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="17577-148">在 SSMS 中，於資料庫上按一下滑鼠右鍵 > [還原]。</span><span class="sxs-lookup"><span data-stu-id="17577-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="17577-149">在 hello **Backup Database**對話方塊，請在**備份檔案**，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="17577-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="17577-150">在 hello**尋找資料庫檔案**對話方塊中，您想要 toorestore 選取 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="17577-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="17577-151">在**還原資料庫**，選取 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="17577-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="17577-152">指定選項。</span><span class="sxs-lookup"><span data-stu-id="17577-152">Specify options.</span></span> <span data-ttu-id="17577-153">安全性選項必須符合 hello 備份時所使用的備份選項。</span><span class="sxs-lookup"><span data-stu-id="17577-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="17577-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="17577-154">PowerShell</span></span>

<span data-ttu-id="17577-155">使用 [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17577-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="17577-156">相關資訊</span><span class="sxs-lookup"><span data-stu-id="17577-156">Related information</span></span>

[<span data-ttu-id="17577-157">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="17577-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="17577-158">[高可用性](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="17577-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="17577-159">管理 Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="17577-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
