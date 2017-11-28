---
title: "設定 Windows 檔案和資料夾 tooAzure （資源管理員） aaaBack |Microsoft 文件"
description: "了解註冊資源管理員部署中的 Windows 檔案和資料夾 tooAzure tooback。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "如何 toobackup;如何設定; tooback備份檔案和資料夾"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="87794-104">初步了解：在 Resource Manager 部署中備份檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="87794-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="87794-105">這篇文章說明如何使用資源管理員部署您的 Windows Server （或 Windows 電腦） tooback 檔案和資料夾 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="87794-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="87794-106">它是教學課程的預定的 toowalk 您透過 hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="87794-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="87794-107">如果您想 tooget 開始使用 Azure Backup，您在 hello 正確的位置。</span><span class="sxs-lookup"><span data-stu-id="87794-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="87794-108">如果您想 tooknow 深入了解 Azure 備份，請閱讀本[概觀](backup-introduction-to-azure-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="87794-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="87794-109">如果您沒有 Azure 訂用帳戶，請建立 [免費帳戶](https://azure.microsoft.com/free/) ，以便存取任何 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="87794-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="87794-110">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="87794-110">Create a recovery services vault</span></span>
<span data-ttu-id="87794-111">您的檔案及資料夾 tooback，您需要 toocreate hello toostore hello 資料所在的區域中的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="87794-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="87794-112">您也需要的 toodetermine 方式複寫儲存體。</span><span class="sxs-lookup"><span data-stu-id="87794-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="87794-113">toocreate 復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="87794-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="87794-114">如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)使用您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="87794-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="87794-115">在 hello 中樞功能表中，按一下 [**更多服務**hello] 清單中的資源，在輸入**復原服務**按一下**復原服務保存庫**。</span><span class="sxs-lookup"><span data-stu-id="87794-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="87794-117">如果 hello 訂用帳戶中沒有復原服務保存庫，則會列出 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="87794-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="87794-118">在 hello**復原服務保存庫**功能表上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="87794-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![建立復原服務保存庫的步驟 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="87794-120">hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。</span><span class="sxs-lookup"><span data-stu-id="87794-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![建立復原服務保存庫的步驟 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="87794-122">如**名稱**，輸入好記名稱 tooidentify hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="87794-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="87794-123">hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="87794-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="87794-124">輸入包含 2 到 50 個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="87794-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="87794-125">該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="87794-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="87794-126">在 hello**訂用帳戶**區段中，使用 hello 下拉式功能表 toochoose hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="87794-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="87794-127">如果您使用只有一個訂用帳戶時，會出現該訂用帳戶，所以您可以跳 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="87794-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="87794-128">如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="87794-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="87794-129">只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。</span><span class="sxs-lookup"><span data-stu-id="87794-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="87794-130">在 hello**資源群組**> 一節：</span><span class="sxs-lookup"><span data-stu-id="87794-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="87794-131">選取**建立新**如果您想 toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="87794-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="87794-132">或</span><span class="sxs-lookup"><span data-stu-id="87794-132">Or</span></span>
    * <span data-ttu-id="87794-133">選取**使用現有**按一下 hello 下拉式功能表 toosee hello 可用的資源群組清單。</span><span class="sxs-lookup"><span data-stu-id="87794-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="87794-134">完整資源群組的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="87794-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="87794-135">按一下**位置**hello 保存庫的 tooselect hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="87794-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="87794-136">這個選擇會決定您的備份資料的傳送目標的 hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="87794-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="87794-137">在 hello hello 復原服務保存庫刀鋒視窗底部，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="87794-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="87794-138">可能需要幾分鐘的時間復原服務保存庫建立 toobe hello。</span><span class="sxs-lookup"><span data-stu-id="87794-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="87794-139">監視 hello 上方右側的區域中的 hello 入口網站的 hello 狀態通知。</span><span class="sxs-lookup"><span data-stu-id="87794-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="87794-140">一旦建立您的保存庫，它會出現在 hello 清單復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="87794-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="87794-141">在數分鐘之後﹐如果您沒有看到您的保存庫，請按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="87794-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![按一下 [重新整理] 按鈕。](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="87794-143">一旦您看到您的保存庫中的 復原服務保存庫的 hello 清單，您就準備好 tooset hello 儲存體備援。</span><span class="sxs-lookup"><span data-stu-id="87794-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="87794-144">設定儲存體備援 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="87794-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="87794-145">當您建立的復原服務保存庫時，請確定儲存體備援設定的 hello 您想要的方式。</span><span class="sxs-lookup"><span data-stu-id="87794-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="87794-146">從 hello**復原服務保存庫**刀鋒視窗中，按一下 hello 新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="87794-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![從 hello 復原服務保存庫清單中選取 hello 新的保存庫](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="87794-148">當您選取 hello 保存庫時，hello**復原服務保存庫**刀鋒視窗縮小及 hello 設定 刀鋒視窗 (*hello 頂端具有 hello hello 保存庫名稱*) 和 hello 保存庫詳細資料 刀鋒視窗開啟。</span><span class="sxs-lookup"><span data-stu-id="87794-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![檢視新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="87794-150">在 hello 新的保存庫的設定 刀鋒視窗中，使用 hello 垂直投影片 tooscroll toohello 管理 區段中，關閉，然後按一下**備份基礎結構**。</span><span class="sxs-lookup"><span data-stu-id="87794-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="87794-151">hello 備份基礎結構刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="87794-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="87794-152">在 hello 備份基礎結構刀鋒視窗中，按一下 **備份設定**tooopen hello**備份設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87794-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![設定新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="87794-154">選擇您的保存庫的 hello 適當的儲存體複寫選項。</span><span class="sxs-lookup"><span data-stu-id="87794-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![儲存體組態選項](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="87794-156">根據預設，保存庫具有異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="87794-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="87794-157">如果您使用 Azure 做為備份的主要儲存體端點時，繼續 toouse**異地備援**。</span><span class="sxs-lookup"><span data-stu-id="87794-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="87794-158">如果您不使用 Azure 做為備份的主要儲存體端點，然後選擇 **本機備援**，進而降低 hello Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="87794-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="87794-159">在此[儲存體備援概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="87794-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="87794-160">現在您已建立保存庫，請設定它來備份檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="87794-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="87794-161">設定 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="87794-161">Configure hello vault</span></span>
1. <span data-ttu-id="87794-162">在復原服務保存庫刀鋒視窗 （適用於 hello 保存庫中您剛建立），hello hello 開始使用 > 一節中，按一下**備份**，然後在 hello**開始使用備份**刀鋒視窗中，選取**備份目標**。</span><span class="sxs-lookup"><span data-stu-id="87794-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="87794-164">hello**備份目標**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="87794-164">hello **Backup Goal** blade opens.</span></span>

    ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="87794-166">從 hello**其中執行您的工作負載？**下拉式選單中，選取**內部**。</span><span class="sxs-lookup"><span data-stu-id="87794-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="87794-167">因為您的 Windows Server 或 Windows 電腦是不在 Azure 中的實體電腦，所以您選擇 [內部部署]。</span><span class="sxs-lookup"><span data-stu-id="87794-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="87794-168">從 hello**怎麼辦想 toobackup？**功能表上，選取**檔案和資料夾**，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="87794-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![設定檔案和資料夾](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="87794-170">之後按一下 確定 核取記號會出現 下一步太**備份目標**，和 hello**準備基礎結構**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="87794-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![已設定備份目標，接下來是準備基礎結構](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="87794-172">在 hello**準備基礎結構**刀鋒視窗中，按一下 **下載適用於 Windows Server 的代理程式或 Windows 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="87794-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="87794-174">如果您使用 Windows Server 基本項目，然後選擇 toodownload hello 代理程式的 Windows Server 不可或缺。</span><span class="sxs-lookup"><span data-stu-id="87794-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="87794-175">快顯功能表會提示您 toorun 或儲存 MARSAgentInstaller.exe。</span><span class="sxs-lookup"><span data-stu-id="87794-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller dialog](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="87794-177">在 hello 下載快顯功能表上，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="87794-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="87794-178">根據預設，hello **MARSagentinstaller.exe** tooyour Downloads 資料夾儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="87794-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="87794-179">Hello 安裝程式完成時，您會看到快顯視窗，詢問您想 toorun hello 安裝程式，或開啟 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="87794-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="87794-181">您無須 tooinstall hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="87794-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="87794-182">您已下載 hello 保存庫認證之後，您可以安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="87794-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="87794-183">在 hello**準備基礎結構**刀鋒視窗中，按一下 **下載**。</span><span class="sxs-lookup"><span data-stu-id="87794-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![下載保存庫認證](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="87794-185">hello 保存庫認證下載 tooyour 下載 資料夾。</span><span class="sxs-lookup"><span data-stu-id="87794-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="87794-186">Hello 保存庫認證完成下載之後，您會看到快顯視窗，詢問您想 tooopen 或儲存 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="87794-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="87794-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="87794-187">Click **Save**.</span></span> <span data-ttu-id="87794-188">如果您不小心按**開啟**、 讓 hello 對話方塊中嘗試 tooopen hello 保存庫認證失敗。</span><span class="sxs-lookup"><span data-stu-id="87794-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="87794-189">您無法開啟 hello 保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="87794-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="87794-190">繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="87794-190">Proceed toohello next step.</span></span> <span data-ttu-id="87794-191">hello 保存庫認證是在 hello 下載 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="87794-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![保存庫認證下載完成](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="87794-193">安裝並註冊 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="87794-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="87794-194">透過 hello Azure 入口網站啟用備份尚無法使用。</span><span class="sxs-lookup"><span data-stu-id="87794-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="87794-195">使用您的檔案及資料夾的 hello Microsoft Azure Recovery Services Agent tooback。</span><span class="sxs-lookup"><span data-stu-id="87794-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="87794-196">找出並按兩下 hello **MARSagentinstaller.exe** hello 下載資料夾 （或其他已儲存的位置）。</span><span class="sxs-lookup"><span data-stu-id="87794-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="87794-197">hello 安裝程式會提供一系列的訊息，擷取安裝，並註冊 hello 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="87794-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![執行復原服務代理安裝程式的認證](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="87794-199">完成 hello Microsoft Azure Recovery Services Agent 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="87794-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="87794-200">您需要 toocomplete hello 精靈:</span><span class="sxs-lookup"><span data-stu-id="87794-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="87794-201">選擇 hello 安裝和快取資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="87794-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="87794-202">提供 proxy 伺服器資訊，如果您使用 proxy 伺服器 tooconnect toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="87794-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="87794-203">如果您使用已驗證的 Proxy，請提供您的使用者名稱和密碼詳細資料。</span><span class="sxs-lookup"><span data-stu-id="87794-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="87794-204">提供 hello 下載保存庫認證</span><span class="sxs-lookup"><span data-stu-id="87794-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="87794-205">將 hello 加密複雜密碼儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="87794-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="87794-206">如果您遺失或忘記 hello 複雜密碼時，Microsoft 無法協助復原 hello 備份資料。</span><span class="sxs-lookup"><span data-stu-id="87794-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="87794-207">將 hello 檔案儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="87794-207">Save hello file in a secure location.</span></span> <span data-ttu-id="87794-208">它是必要的 toorestore 備份。</span><span class="sxs-lookup"><span data-stu-id="87794-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="87794-209">hello 代理程式現在已安裝，且您的電腦已註冊的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="87794-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="87794-210">正在準備 tooconfigure，並將備份排程。</span><span class="sxs-lookup"><span data-stu-id="87794-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="87794-211">網路和連線需求</span><span class="sxs-lookup"><span data-stu-id="87794-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="87794-212">如果您的電腦/proxy 具有有限的網際網路存取，請確定 hello mcahine/proxy 上的防火牆設定會設定的 tooallow hello 下列 Url:</span><span class="sxs-lookup"><span data-stu-id="87794-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="87794-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="87794-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="87794-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="87794-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="87794-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="87794-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="87794-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="87794-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="87794-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="87794-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="87794-218">備份檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="87794-218">Back up your files and folders</span></span>
<span data-ttu-id="87794-219">hello 初始備份包含兩個主要工作：</span><span class="sxs-lookup"><span data-stu-id="87794-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="87794-220">Hello 備份排程</span><span class="sxs-lookup"><span data-stu-id="87794-220">Schedule hello backup</span></span>
* <span data-ttu-id="87794-221">備份檔案和資料夾進行 hello 第一次</span><span class="sxs-lookup"><span data-stu-id="87794-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="87794-222">toocomplete hello 初始備份、 使用 hello Microsoft Azure 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="87794-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="87794-223">tooschedule hello 備份工作</span><span class="sxs-lookup"><span data-stu-id="87794-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="87794-224">開啟 hello Microsoft Azure Recovery Services agent。</span><span class="sxs-lookup"><span data-stu-id="87794-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="87794-225">您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。</span><span class="sxs-lookup"><span data-stu-id="87794-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![啟動 hello Azure 復原服務代理程式](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="87794-227">在 hello 復原服務代理程式，按一下 **排程備份**。</span><span class="sxs-lookup"><span data-stu-id="87794-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="87794-229">在 [hello 上開始使用 hello 排程備份精靈] 頁面中，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="87794-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="87794-230">在 hello 選取項目 tooBackup 頁面上，按一下 **新增的項目**。</span><span class="sxs-lookup"><span data-stu-id="87794-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="87794-231">選取 hello 檔案和資料夾，您想 tooback、，然後按一下**好**。</span><span class="sxs-lookup"><span data-stu-id="87794-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="87794-232">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="87794-232">Click **Next**.</span></span>
7. <span data-ttu-id="87794-233">在 hello**指定備份排程**頁面上，指定 hello**備份排程**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="87794-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="87794-234">您可以排程每日 (一天最多三次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="87794-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 備份項目](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="87794-236">如需有關如何 toospecify hello 備份排程的詳細資訊，請參閱 hello 文章[使用 Azure Backup tooreplace 磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="87794-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="87794-237">在 hello**選取保留原則**頁面上，選取 hello**保留原則**為 hello 備份副本。</span><span class="sxs-lookup"><span data-stu-id="87794-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="87794-238">hello 保留原則會指定儲存 hello 備份資料的時間長度。</span><span class="sxs-lookup"><span data-stu-id="87794-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="87794-239">而不要指定 「 一般原則 」 的所有備份的點，您可以指定不同的保留原則根據 hello 備份發生時。</span><span class="sxs-lookup"><span data-stu-id="87794-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="87794-240">您可以修改 hello 每日、 每週、 每月和每年保留原則 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="87794-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="87794-241">在 [hello 選擇初始備份類型] 頁面上，選擇 hello 初始備份類型。</span><span class="sxs-lookup"><span data-stu-id="87794-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="87794-242">保留 hello 選項**自動透過網路 hello**選取，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="87794-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="87794-243">您可以備份自動 hello 網路上或您可以離線備份。</span><span class="sxs-lookup"><span data-stu-id="87794-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="87794-244">hello 本文其餘部分說明 hello 程序會自動備份。</span><span class="sxs-lookup"><span data-stu-id="87794-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="87794-245">如果您偏好 toodo 離線備份，請檢閱 hello 文件[Azure Backup 中的離線備份工作流程](backup-azure-backup-import-export.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="87794-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="87794-246">在 hello 確認頁面上，檢閱 hello 資訊，然後再按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="87794-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="87794-247">Hello 精靈可讓您完成建立 hello 備份排程後，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="87794-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="87794-248">tooback 檔案及資料夾的 hello 第一次</span><span class="sxs-lookup"><span data-stu-id="87794-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="87794-249">在 hello 復原服務代理程式，按一下 **立即備份**toocomplete hello 初始植入 hello 網路上。</span><span class="sxs-lookup"><span data-stu-id="87794-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![立即備份 Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="87794-251">在 hello 確認頁面上，檢閱 hello 立即備份精靈的 hello 設定會使用 tooback hello 機器。</span><span class="sxs-lookup"><span data-stu-id="87794-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="87794-252">然後按一下 [備份] 。</span><span class="sxs-lookup"><span data-stu-id="87794-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="87794-253">按一下**關閉**tooclose hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="87794-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="87794-254">如果您在 hello 備份程序完成之前關閉 hello 精靈，hello 精靈會繼續 toorun hello 背景。</span><span class="sxs-lookup"><span data-stu-id="87794-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="87794-255">Hello 初始備份完成後，hello**作業已完成**hello Backup 主控台中顯示的狀態。</span><span class="sxs-lookup"><span data-stu-id="87794-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR 已完成](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="87794-257">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="87794-257">Questions?</span></span>
<span data-ttu-id="87794-258">如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="87794-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87794-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87794-259">Next steps</span></span>
* <span data-ttu-id="87794-260">詳細了解如何 [備份 Windows 電腦](backup-configure-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="87794-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="87794-261">現在您已備份好檔案和資料夾，接下來您可以 [管理您的保存庫和伺服器](backup-azure-manage-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="87794-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="87794-262">如果您需要 toorestore 備份，請使用本文章太[還原檔案 tooa Windows 機器](backup-azure-restore-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="87794-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
