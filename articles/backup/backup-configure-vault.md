---
title: "檔案及資料夾 aaaUse Azure 備份代理程式 tooback |Microsoft 文件"
description: "使用 Windows 檔案和資料夾 tooAzure 向上 hello Microsoft Azure 備份代理程式 tooback。 建立復原服務保存庫、 安裝 hello 備份代理程式、 定義 hello 備份原則，並執行 hello 初始備份 hello 檔案及資料夾。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份保存庫；備份 Windows Server；備份Windows；"
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="eb639-105">備份 Windows Server 或用戶端 tooAzure，使用 hello Resource Manager 部署模型</span><span class="sxs-lookup"><span data-stu-id="eb639-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb639-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eb639-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="eb639-107">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="eb639-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="eb639-108">本文說明如何使用 Azure 備份您的 Windows Server （或 Windows 用戶端） tooback 檔案和資料夾 tooAzure hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="eb639-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![備份程序步驟](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="eb639-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="eb639-110">Before you start</span></span>
<span data-ttu-id="eb639-111">伺服器或用戶端 tooAzure tooback，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb639-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="eb639-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="eb639-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="eb639-113">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="eb639-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="eb639-114">復原服務保存庫是儲存所有的 hello 備份和復原點建立一段時間的實體。</span><span class="sxs-lookup"><span data-stu-id="eb639-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="eb639-115">hello 復原服務保存庫也包含 hello 套用的備份原則 toohello 受保護檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="eb639-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="eb639-116">當您建立的復原服務保存庫時，您應該也選取 hello 適當的儲存體備援選項。</span><span class="sxs-lookup"><span data-stu-id="eb639-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="eb639-117">toocreate 復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="eb639-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="eb639-118">如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)使用您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb639-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="eb639-119">在 hello 中樞功能表中，按一下 [**更多服務**hello] 清單中的資源，在輸入**復原服務**按一下**復原服務保存庫**。</span><span class="sxs-lookup"><span data-stu-id="eb639-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="eb639-121">如果 hello 訂用帳戶中沒有復原服務保存庫，則會列出 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="eb639-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="eb639-122">在 hello**復原服務保存庫**功能表上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="eb639-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![建立復原服務保存庫的步驟 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="eb639-124">hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。</span><span class="sxs-lookup"><span data-stu-id="eb639-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![建立復原服務保存庫的步驟 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="eb639-126">如**名稱**，輸入好記名稱 tooidentify hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="eb639-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="eb639-127">hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb639-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="eb639-128">輸入包含 2 到 50 個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="eb639-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="eb639-129">該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="eb639-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="eb639-130">在 hello**訂用帳戶**區段中，使用 hello 下拉式功能表 toochoose hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb639-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="eb639-131">如果您使用只有一個訂用帳戶時，會出現該訂用帳戶，所以您可以跳 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="eb639-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="eb639-132">如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb639-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="eb639-133">只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。</span><span class="sxs-lookup"><span data-stu-id="eb639-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="eb639-134">在 hello**資源群組**> 一節：</span><span class="sxs-lookup"><span data-stu-id="eb639-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="eb639-135">選取**建立新**如果您想 toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="eb639-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="eb639-136">或</span><span class="sxs-lookup"><span data-stu-id="eb639-136">Or</span></span>
    * <span data-ttu-id="eb639-137">選取**使用現有**按一下 hello 下拉式功能表 toosee hello 可用的資源群組清單。</span><span class="sxs-lookup"><span data-stu-id="eb639-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="eb639-138">完整資源群組的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="eb639-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="eb639-139">按一下**位置**hello 保存庫的 tooselect hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="eb639-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="eb639-140">這個選擇會決定您的備份資料的傳送目標的 hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="eb639-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="eb639-141">在 hello hello 復原服務保存庫刀鋒視窗底部，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="eb639-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="eb639-142">可能需要幾分鐘的時間復原服務保存庫建立 toobe hello。</span><span class="sxs-lookup"><span data-stu-id="eb639-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="eb639-143">監視 hello 上方右側的區域中的 hello 入口網站的 hello 狀態通知。</span><span class="sxs-lookup"><span data-stu-id="eb639-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="eb639-144">一旦建立您的保存庫，它會出現在 hello 清單復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="eb639-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="eb639-145">在數分鐘之後﹐如果您沒有看到您的保存庫，請按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="eb639-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![按一下 [重新整理] 按鈕。](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="eb639-147">一旦您看到您的保存庫中的 復原服務保存庫的 hello 清單，您就準備好 tooset hello 儲存體備援。</span><span class="sxs-lookup"><span data-stu-id="eb639-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="eb639-148">設定儲存體備援</span><span class="sxs-lookup"><span data-stu-id="eb639-148">Set storage redundancy</span></span>
<span data-ttu-id="eb639-149">首次建立復原服務保存庫時會決定儲存體的複寫方式。</span><span class="sxs-lookup"><span data-stu-id="eb639-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="eb639-150">從 hello**復原服務保存庫**刀鋒視窗中，按一下 hello 新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="eb639-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![從 hello 復原服務保存庫清單中選取 hello 新的保存庫](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="eb639-152">當您選取 hello 保存庫時，hello**復原服務保存庫**刀鋒視窗縮小及 hello 設定 刀鋒視窗 (*hello 頂端具有 hello hello 保存庫名稱*) 和 hello 保存庫詳細資料 刀鋒視窗開啟。</span><span class="sxs-lookup"><span data-stu-id="eb639-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![檢視新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="eb639-154">在 hello 新的保存庫的設定 刀鋒視窗中，使用 hello 垂直投影片 tooscroll toohello 管理 區段中，關閉，然後按一下**備份基礎結構**。</span><span class="sxs-lookup"><span data-stu-id="eb639-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="eb639-155">hello 備份基礎結構刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="eb639-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="eb639-156">在 hello 備份基礎結構刀鋒視窗中，按一下 **備份設定**tooopen hello**備份設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="eb639-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![設定新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="eb639-158">選擇您的保存庫的 hello 適當的儲存體複寫選項。</span><span class="sxs-lookup"><span data-stu-id="eb639-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![儲存體組態選項](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="eb639-160">根據預設，保存庫具有異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="eb639-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="eb639-161">如果您使用 Azure 做為備份的主要儲存體端點時，繼續 toouse**異地備援**。</span><span class="sxs-lookup"><span data-stu-id="eb639-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="eb639-162">如果您不使用 Azure 做為備份的主要儲存體端點，然後選擇 **本機備援**，進而降低 hello Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="eb639-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="eb639-163">在此[儲存體備援概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="eb639-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="eb639-164">既然您已建立保存庫，請下載和安裝 hello Microsoft Azure 復原服務代理程式、 下載保存庫認證，然後使用這些認證 tooregister hello 代理程式與準備您的基礎結構 tooback 檔案及資料夾hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="eb639-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="eb639-165">設定 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="eb639-165">Configure hello vault</span></span>

1. <span data-ttu-id="eb639-166">在復原服務保存庫刀鋒視窗 （適用於 hello 保存庫中您剛建立），hello hello 開始使用 > 一節中，按一下**備份**，然後在 hello**開始使用備份**刀鋒視窗中，選取**備份目標**。</span><span class="sxs-lookup"><span data-stu-id="eb639-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="eb639-168">hello**備份目標**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="eb639-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="eb639-169">如果之前已經設定的 hello 復原服務保存庫，然後 hello**備份目標**刀鋒視窗隨即開啟，當您按一下**備份**hello 復原服務保存庫刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="eb639-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="eb639-171">從 hello**其中執行您的工作負載？**下拉式選單中，選取**內部**。</span><span class="sxs-lookup"><span data-stu-id="eb639-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="eb639-172">因為您的 Windows Server 或 Windows 電腦是不在 Azure 中的實體電腦，所以您選擇 [內部部署]。</span><span class="sxs-lookup"><span data-stu-id="eb639-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="eb639-173">從 hello**怎麼辦想 toobackup？**功能表上，選取**檔案和資料夾**，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="eb639-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![設定檔案和資料夾](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="eb639-175">之後按一下 確定 核取記號會出現 下一步太**備份目標**，和 hello**準備基礎結構**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="eb639-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![已設定備份目標，接下來是準備基礎結構](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="eb639-177">在 hello**準備基礎結構**刀鋒視窗中，按一下 **下載適用於 Windows Server 的代理程式或 Windows 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="eb639-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="eb639-179">如果您使用 Windows Server 基本項目，然後選擇 toodownload hello 代理程式的 Windows Server 不可或缺。</span><span class="sxs-lookup"><span data-stu-id="eb639-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="eb639-180">快顯功能表會提示您 toorun 或儲存 MARSAgentInstaller.exe。</span><span class="sxs-lookup"><span data-stu-id="eb639-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![MARSAgentInstaller dialog](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="eb639-182">在 hello 下載快顯功能表上，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="eb639-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="eb639-183">根據預設，hello **MARSagentinstaller.exe** tooyour Downloads 資料夾儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="eb639-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="eb639-184">Hello 安裝程式完成時，您會看到快顯視窗，詢問您想 toorun hello 安裝程式，或開啟 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="eb639-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="eb639-186">您無須 tooinstall hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="eb639-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="eb639-187">您已下載 hello 保存庫認證之後，您可以安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="eb639-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="eb639-188">在 hello**準備基礎結構**刀鋒視窗中，按一下 **下載**。</span><span class="sxs-lookup"><span data-stu-id="eb639-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![下載保存庫認證](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="eb639-190">hello 保存庫認證下載 tooyour 下載 資料夾。</span><span class="sxs-lookup"><span data-stu-id="eb639-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="eb639-191">Hello 保存庫認證完成下載之後，您會看到快顯視窗，詢問您想 tooopen 或儲存 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="eb639-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="eb639-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="eb639-192">Click **Save**.</span></span> <span data-ttu-id="eb639-193">如果您不小心按**開啟**、 讓 hello 對話方塊中嘗試 tooopen hello 保存庫認證失敗。</span><span class="sxs-lookup"><span data-stu-id="eb639-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="eb639-194">您無法開啟 hello 保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="eb639-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="eb639-195">繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="eb639-195">Proceed toohello next step.</span></span> <span data-ttu-id="eb639-196">hello 保存庫認證是在 hello 下載 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="eb639-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![保存庫認證下載完成](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="eb639-198">安裝並註冊 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="eb639-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="eb639-199">透過 hello Azure 入口網站啟用備份尚無法使用。</span><span class="sxs-lookup"><span data-stu-id="eb639-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="eb639-200">使用您的檔案及資料夾的 hello Microsoft Azure Recovery Services Agent tooback。</span><span class="sxs-lookup"><span data-stu-id="eb639-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="eb639-201">找出並按兩下 hello **MARSagentinstaller.exe** hello 下載資料夾 （或其他已儲存的位置）。</span><span class="sxs-lookup"><span data-stu-id="eb639-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="eb639-202">hello 安裝程式會提供一系列的訊息，擷取安裝，並註冊 hello 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="eb639-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![執行復原服務代理安裝程式的認證](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="eb639-204">完成 hello Microsoft Azure Recovery Services Agent 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="eb639-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="eb639-205">您需要 toocomplete hello 精靈:</span><span class="sxs-lookup"><span data-stu-id="eb639-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="eb639-206">選擇 hello 安裝和快取資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="eb639-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="eb639-207">提供 proxy 伺服器資訊，如果您使用 proxy 伺服器 tooconnect toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="eb639-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="eb639-208">如果您使用已驗證的 Proxy，請提供您的使用者名稱和密碼詳細資料。</span><span class="sxs-lookup"><span data-stu-id="eb639-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="eb639-209">提供 hello 下載保存庫認證</span><span class="sxs-lookup"><span data-stu-id="eb639-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="eb639-210">將 hello 加密複雜密碼儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="eb639-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="eb639-211">如果您遺失或忘記 hello 複雜密碼時，Microsoft 無法協助復原 hello 備份資料。</span><span class="sxs-lookup"><span data-stu-id="eb639-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="eb639-212">將 hello 檔案儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="eb639-212">Save hello file in a secure location.</span></span> <span data-ttu-id="eb639-213">它是必要的 toorestore 備份。</span><span class="sxs-lookup"><span data-stu-id="eb639-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="eb639-214">hello 代理程式現在已安裝，且您的電腦已註冊的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="eb639-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="eb639-215">正在準備 tooconfigure，並將備份排程。</span><span class="sxs-lookup"><span data-stu-id="eb639-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="eb639-216">網路和連線需求</span><span class="sxs-lookup"><span data-stu-id="eb639-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="eb639-217">如果您的電腦/proxy 具有有限的網際網路存取，請確定 hello 機器/proxy 上的防火牆設定已設定的 tooallow hello 下列 Url:</span><span class="sxs-lookup"><span data-stu-id="eb639-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="eb639-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="eb639-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="eb639-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="eb639-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="eb639-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="eb639-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="eb639-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="eb639-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="eb639-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="eb639-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="eb639-223">建立 hello 備份原則</span><span class="sxs-lookup"><span data-stu-id="eb639-223">Create hello backup policy</span></span>
<span data-ttu-id="eb639-224">hello 備份原則時，hello 排程復原點會採取與 hello 的 hello 復原點，就會保留的時間長度。</span><span class="sxs-lookup"><span data-stu-id="eb639-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="eb639-225">使用檔案和資料夾的 hello Microsoft Azure 備份代理程式 toocreate hello 備份原則。</span><span class="sxs-lookup"><span data-stu-id="eb639-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="eb639-226">toocreate 備份排程</span><span class="sxs-lookup"><span data-stu-id="eb639-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="eb639-227">開啟 hello Microsoft Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="eb639-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="eb639-228">您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。</span><span class="sxs-lookup"><span data-stu-id="eb639-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![啟動 hello Azure 備份代理程式](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="eb639-230">在 [hello 備份代理程式的**動作**] 窗格中，按一下 [**排程備份**toolaunch hello 排程備份精靈]。</span><span class="sxs-lookup"><span data-stu-id="eb639-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Windows Server 備份排程](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="eb639-232">在 hello**入門**的 hello 排程備份精靈 頁面上按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eb639-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="eb639-233">在 hello**選取項目 tooBackup**頁面上，按一下**新增的項目**。</span><span class="sxs-lookup"><span data-stu-id="eb639-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="eb639-234">hello 選取項目 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="eb639-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="eb639-235">選取 hello 檔案和資料夾，您想 tooprotect，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="eb639-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="eb639-236">在 hello**選取項目 tooBackup**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eb639-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="eb639-237">在 hello**指定備份排程**頁面上，指定 hello 備份排程，以及按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eb639-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="eb639-238">您可以排程每日 (一天最多三次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="eb639-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 備份項目](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="eb639-240">如需有關如何 toospecify hello 備份排程的詳細資訊，請參閱 hello 文章[使用 Azure Backup tooreplace 磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)。</span><span class="sxs-lookup"><span data-stu-id="eb639-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="eb639-241">在 hello**選取保留原則**頁面上，選擇 hello 特定的保留原則 hello 為 hello 備份副本，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eb639-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="eb639-242">hello 保留原則指定 hello 持續時間的 hello 備份會儲存。</span><span class="sxs-lookup"><span data-stu-id="eb639-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="eb639-243">而不是只指定 「 一般原則 」 的所有備份的點，您可以指定不同的保留原則根據 hello 備份發生時。</span><span class="sxs-lookup"><span data-stu-id="eb639-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="eb639-244">您可以修改 hello 每日、 每週、 每月和每年保留原則 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="eb639-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="eb639-245">在 [hello 選擇初始備份類型] 頁面上，選擇 hello 初始備份類型。</span><span class="sxs-lookup"><span data-stu-id="eb639-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="eb639-246">保留 hello 選項**自動透過網路 hello**選取，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eb639-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="eb639-247">您可以備份自動 hello 網路上或您可以離線備份。</span><span class="sxs-lookup"><span data-stu-id="eb639-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="eb639-248">hello 本文其餘部分說明 hello 程序會自動備份。</span><span class="sxs-lookup"><span data-stu-id="eb639-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="eb639-249">如果您偏好 toodo 離線備份，請檢閱 hello 文件[Azure Backup 中的離線備份工作流程](backup-azure-backup-import-export.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="eb639-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="eb639-250">在 hello 確認頁面上，檢閱 hello 資訊，然後再按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="eb639-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="eb639-251">Hello 精靈可讓您完成建立 hello 備份排程後，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="eb639-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="eb639-252">啟用網路節流</span><span class="sxs-lookup"><span data-stu-id="eb639-252">Enable network throttling</span></span>
<span data-ttu-id="eb639-253">hello Microsoft Azure 備份代理程式會提供網路節流設定。</span><span class="sxs-lookup"><span data-stu-id="eb639-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="eb639-254">節流會控制資料傳輸期間的網路頻寬使用方式。</span><span class="sxs-lookup"><span data-stu-id="eb639-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="eb639-255">如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量，此控制項可以是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="eb639-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="eb639-256">節流設定會套用 tooback 和還原活動。</span><span class="sxs-lookup"><span data-stu-id="eb639-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="eb639-257">網路節流不適用於 Windows Server 2008 R2 SP1、Windows Server 2008 SP2 或 Windows 7 (含 service pack)。</span><span class="sxs-lookup"><span data-stu-id="eb639-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="eb639-258">hello Azure Backup 網路節流功能會 hello 本機作業系統上的服務品質 (QoS)。</span><span class="sxs-lookup"><span data-stu-id="eb639-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="eb639-259">Azure 備份可保護這些作業系統，但不適用於 Azure Backup 網路節流設定 hello QoS 適用於這些平台版本。</span><span class="sxs-lookup"><span data-stu-id="eb639-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="eb639-260">網路節流可使用於所有其他 [支援的作業系統](backup-azure-backup-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="eb639-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="eb639-261">**tooenable 網路節流設定**</span><span class="sxs-lookup"><span data-stu-id="eb639-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="eb639-262">在 hello Microsoft Azure 備份代理程式，按一下 **變更屬性**。</span><span class="sxs-lookup"><span data-stu-id="eb639-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![變更屬性](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="eb639-264">在 hello**節流**索引標籤，選取 hello**啟用網際網路頻寬使用節流設定的備份操作**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="eb639-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![網路節流](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="eb639-266">啟用節流設定後，指定允許的頻寬的備份資料傳輸期間的 hello**上班**和**非工作小時**。</span><span class="sxs-lookup"><span data-stu-id="eb639-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="eb639-267">hello 頻寬值開始每秒 (Kbps) 為 512 kb，最高 too1，023 mb / 秒 (MBps)。</span><span class="sxs-lookup"><span data-stu-id="eb639-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="eb639-268">也可以指定 hello 開始和完成**上班**，和 hello 一週的哪幾天都視為的工作日。</span><span class="sxs-lookup"><span data-stu-id="eb639-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="eb639-269">指定之工作時間以外的時間則視為非工作時間。</span><span class="sxs-lookup"><span data-stu-id="eb639-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="eb639-270">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eb639-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="eb639-271">tooback 檔案及資料夾的 hello 第一次</span><span class="sxs-lookup"><span data-stu-id="eb639-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="eb639-272">在 hello 備份代理程式，按一下 **立即備份**toocomplete hello 初始植入 hello 網路上。</span><span class="sxs-lookup"><span data-stu-id="eb639-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Windows Server 立即備份](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="eb639-274">在 hello 確認頁面上，檢閱 hello 立即備份精靈的 hello 設定會使用 tooback hello 機器。</span><span class="sxs-lookup"><span data-stu-id="eb639-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="eb639-275">然後按一下 [備份] 。</span><span class="sxs-lookup"><span data-stu-id="eb639-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="eb639-276">按一下**關閉**tooclose hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="eb639-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="eb639-277">如果 hello 備份程序完成之前，您可以這樣做，hello 精靈會繼續 toorun hello 背景。</span><span class="sxs-lookup"><span data-stu-id="eb639-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="eb639-278">Hello 初始備份完成後，hello**作業已完成**hello Backup 主控台中顯示的狀態。</span><span class="sxs-lookup"><span data-stu-id="eb639-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR 已完成](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="eb639-280">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="eb639-280">Questions?</span></span>
<span data-ttu-id="eb639-281">如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="eb639-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb639-282">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb639-282">Next steps</span></span>
<span data-ttu-id="eb639-283">如需備份 VM 或其他工作負載的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="eb639-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="eb639-284">現在您已備份好檔案和資料夾，接下來您可以 [管理您的保存庫和伺服器](backup-azure-manage-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="eb639-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="eb639-285">如果您需要 toorestore 備份，請使用本文章太[還原檔案 tooa Windows 機器](backup-azure-restore-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="eb639-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
