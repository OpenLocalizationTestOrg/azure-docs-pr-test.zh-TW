---
title: "Azure Analysis Services 備份與還原 | Microsoft Docs"
description: "說明如何備份和還原 Azure Analysis Services 資料庫。"
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
ms.openlocfilehash: bffa481a498b130ef1f2388a5ba856da5d164ee0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="85708-103">備份與還原</span><span class="sxs-lookup"><span data-stu-id="85708-103">Backup and restore</span></span>

<span data-ttu-id="85708-104">在 Azure Analysis Services 中備份表格式模型資料庫與內部部署的 Analysis Services 情況非常類似。</span><span class="sxs-lookup"><span data-stu-id="85708-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="85708-105">主要的差異在於備份檔案的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="85708-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="85708-106">備份檔案必須儲存至 [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的容器。</span><span class="sxs-lookup"><span data-stu-id="85708-106">Backup files must be saved to a container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="85708-107">您可以使用您已經有的儲存體帳戶和容器，或是在為您的伺服器設定儲存體設定時再建立帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="85708-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="85708-108">建立儲存體帳戶會導致產生新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="85708-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="85708-109">若要深入了解，請參閱 [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/blobs/)。</span><span class="sxs-lookup"><span data-stu-id="85708-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="85708-110">備份會以 .abf 副檔名儲存。</span><span class="sxs-lookup"><span data-stu-id="85708-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="85708-111">針對記憶體內表格式模型，會同時儲存模型資料和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="85708-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="85708-112">針對 DirectQuery 表格式模型，則只會儲存模型中繼資料。</span><span class="sxs-lookup"><span data-stu-id="85708-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="85708-113">視您選擇的選項而定，可以將備份壓縮和加密。</span><span class="sxs-lookup"><span data-stu-id="85708-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="85708-114">設定儲存體設定</span><span class="sxs-lookup"><span data-stu-id="85708-114">Configure storage settings</span></span>
<span data-ttu-id="85708-115">進行備份之前，您必須為伺服器設定儲存體設定。</span><span class="sxs-lookup"><span data-stu-id="85708-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="85708-116">設定儲存體設定</span><span class="sxs-lookup"><span data-stu-id="85708-116">To configure storage settings</span></span>
1.  <span data-ttu-id="85708-117">在 Azure 入口網站 > [設定] 中，按一下 [備份]。</span><span class="sxs-lookup"><span data-stu-id="85708-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![[設定] 中的 [備份]](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="85708-119">按一下 [已啟用]，然後按一下 [儲存體設定]。</span><span class="sxs-lookup"><span data-stu-id="85708-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![啟用](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="85708-121">選取您的儲存體帳戶，或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="85708-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="85708-122">選取容器，或建立新容器。</span><span class="sxs-lookup"><span data-stu-id="85708-122">Select a container or create a new one.</span></span>

    ![選取容器](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="85708-124">儲存您的備份設定。</span><span class="sxs-lookup"><span data-stu-id="85708-124">Save your backup settings.</span></span>

    ![儲存備份設定](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="85708-126">備份</span><span class="sxs-lookup"><span data-stu-id="85708-126">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="85708-127">使用 SSMS 來進行備份</span><span class="sxs-lookup"><span data-stu-id="85708-127">To backup by using SSMS</span></span>

1. <span data-ttu-id="85708-128">在 SSMS 中，於資料庫上按一下滑鼠右鍵 > [備份]。</span><span class="sxs-lookup"><span data-stu-id="85708-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="85708-129">在 [備份資料庫] > [備份檔案] 中，按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="85708-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="85708-130">在 [另存新檔] 對話方塊中，確認資料夾路徑，然後輸入備份檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="85708-130">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> 

4. <span data-ttu-id="85708-131">在 [備份資料庫] 對話方塊中，選取選項。</span><span class="sxs-lookup"><span data-stu-id="85708-131">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="85708-132">**允許檔案覆寫** - 若要覆寫同名的備份檔案，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="85708-132">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="85708-133">如果未選取此選項，您要儲存的檔案就不能與相同位置中已經存在的檔案同名。</span><span class="sxs-lookup"><span data-stu-id="85708-133">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="85708-134">**套用壓縮** - 若要壓縮備份檔案，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="85708-134">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="85708-135">壓縮過的備份檔案可節省磁碟空間，但需要使用稍微多一點的 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="85708-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="85708-136">**加密備份檔案** - 若要將備份檔案加密，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="85708-136">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="85708-137">此選項需要有使用者提供的密碼來保護備份檔案。</span><span class="sxs-lookup"><span data-stu-id="85708-137">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="85708-138">此密碼可防止以還原作業以外的任何其他方式讀取備份資料。</span><span class="sxs-lookup"><span data-stu-id="85708-138">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="85708-139">如果您選擇將備份加密，請將密碼儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="85708-139">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="85708-140">按一下 [確定] 以建立並儲存備份檔案。</span><span class="sxs-lookup"><span data-stu-id="85708-140">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="85708-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85708-141">PowerShell</span></span>
<span data-ttu-id="85708-142">使用 [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="85708-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="85708-143">還原</span><span class="sxs-lookup"><span data-stu-id="85708-143">Restore</span></span>
<span data-ttu-id="85708-144">在還原時，您的備份檔案必須位於您為伺服器所設定的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="85708-144">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="85708-145">如果您需要將備份檔案從內部部署位置移至儲存體帳戶，請使用 [Microsoft Azure 儲存體總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)或 [AzCopy](../storage/common/storage-use-azcopy.md) 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="85708-145">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="85708-146">如果您要從內部部署伺服器進行還原，則必須先從該模型的角色中移除所有網域使用者，再將他們新增回角色中成為 Azure Active Directory 使用者。</span><span class="sxs-lookup"><span data-stu-id="85708-146">If you're restoring from an on-premises server, you must remove all the domain users from the model's roles and add them back to the roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="85708-147">使用 SSMS 來進行還原</span><span class="sxs-lookup"><span data-stu-id="85708-147">To restore by using SSMS</span></span>

1. <span data-ttu-id="85708-148">在 SSMS 中，於資料庫上按一下滑鼠右鍵 > [還原]。</span><span class="sxs-lookup"><span data-stu-id="85708-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="85708-149">在 [備份資料庫] 對話方塊的 [備份檔案] 中，按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="85708-149">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="85708-150">在 [尋找資料庫檔案] 對話方塊中，選取您想要還原的檔案。</span><span class="sxs-lookup"><span data-stu-id="85708-150">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="85708-151">在 [還原資料庫] 中，選取資料庫。</span><span class="sxs-lookup"><span data-stu-id="85708-151">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="85708-152">指定選項。</span><span class="sxs-lookup"><span data-stu-id="85708-152">Specify options.</span></span> <span data-ttu-id="85708-153">安全性選項必須與您備份時所使用的備份選項相符。</span><span class="sxs-lookup"><span data-stu-id="85708-153">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="85708-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85708-154">PowerShell</span></span>

<span data-ttu-id="85708-155">使用 [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="85708-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="85708-156">相關資訊</span><span class="sxs-lookup"><span data-stu-id="85708-156">Related information</span></span>

[<span data-ttu-id="85708-157">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="85708-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="85708-158">[高可用性](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="85708-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="85708-159">管理 Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="85708-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
