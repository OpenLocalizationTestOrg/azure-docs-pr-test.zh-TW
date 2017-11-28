---
title: "設定 Windows 系統狀態 tooAzure aaaBack |Microsoft 文件"
description: "了解 tooback 的 Windows Server 和/或 Windows 電腦 tooAzure hello 系統狀態。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "如何 toobackup;如何設定; tooback備份檔案和資料夾"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="f344f-104">在 Resource Manager 部署中備份 Windows 系統狀態</span><span class="sxs-lookup"><span data-stu-id="f344f-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="f344f-105">本文說明如何 tooback 您 Windows Server 的系統狀態 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="f344f-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="f344f-106">它是教學課程的預定的 toowalk 您透過 hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="f344f-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="f344f-107">如果您想 tooknow 深入了解 Azure 備份，請閱讀本[概觀](backup-introduction-to-azure-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="f344f-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="f344f-108">如果您沒有 Azure 訂用帳戶，請建立 [免費帳戶](https://azure.microsoft.com/free/) ，以便存取任何 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="f344f-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f344f-109">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="f344f-109">Create a recovery services vault</span></span>
<span data-ttu-id="f344f-110">您的檔案及資料夾 tooback，您需要 toocreate hello toostore hello 資料所在的區域中的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="f344f-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="f344f-111">您也需要的 toodetermine 方式複寫儲存體。</span><span class="sxs-lookup"><span data-stu-id="f344f-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="f344f-112">toocreate 復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="f344f-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="f344f-113">如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)使用您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f344f-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="f344f-114">在 hello 中樞功能表中，按一下 [**更多服務**hello] 清單中的資源，在輸入**復原服務**按一下**復原服務保存庫**。</span><span class="sxs-lookup"><span data-stu-id="f344f-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="f344f-116">如果 hello 訂用帳戶中沒有復原服務保存庫，則會列出 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="f344f-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="f344f-117">在 hello**復原服務保存庫**功能表上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="f344f-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![建立復原服務保存庫的步驟 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="f344f-119">hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。</span><span class="sxs-lookup"><span data-stu-id="f344f-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![建立復原服務保存庫的步驟 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="f344f-121">如**名稱**，輸入好記名稱 tooidentify hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="f344f-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="f344f-122">hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f344f-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="f344f-123">輸入包含 2 到 50 個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="f344f-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="f344f-124">該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="f344f-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="f344f-125">在 hello**訂用帳戶**區段中，使用 hello 下拉式功能表 toochoose hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f344f-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="f344f-126">如果您使用只有一個訂用帳戶時，會出現該訂用帳戶，所以您可以跳 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f344f-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="f344f-127">如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f344f-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="f344f-128">只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。</span><span class="sxs-lookup"><span data-stu-id="f344f-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="f344f-129">在 hello**資源群組**> 一節：</span><span class="sxs-lookup"><span data-stu-id="f344f-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="f344f-130">選取**建立新**如果您想 toocreate 資源群組。</span><span class="sxs-lookup"><span data-stu-id="f344f-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="f344f-131">或</span><span class="sxs-lookup"><span data-stu-id="f344f-131">Or</span></span>
    * <span data-ttu-id="f344f-132">選取**使用現有**按一下 hello 下拉式功能表 toosee hello 可用的資源群組清單。</span><span class="sxs-lookup"><span data-stu-id="f344f-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="f344f-133">完整資源群組的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f344f-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="f344f-134">按一下**位置**hello 保存庫的 tooselect hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="f344f-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="f344f-135">這個選擇會決定您的備份資料的傳送目標的 hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="f344f-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="f344f-136">在 hello hello 復原服務保存庫刀鋒視窗底部，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="f344f-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="f344f-137">可能需要幾分鐘的時間復原服務保存庫建立 toobe hello。</span><span class="sxs-lookup"><span data-stu-id="f344f-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="f344f-138">監視 hello 上方右側的區域中的 hello 入口網站的 hello 狀態通知。</span><span class="sxs-lookup"><span data-stu-id="f344f-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="f344f-139">一旦建立您的保存庫，它會出現在 hello 清單復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="f344f-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="f344f-140">在數分鐘之後﹐如果您沒有看到您的保存庫，請按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="f344f-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![按一下 [重新整理] 按鈕。](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="f344f-142">一旦您看到您的保存庫中的 復原服務保存庫的 hello 清單，您就準備好 tooset hello 儲存體備援。</span><span class="sxs-lookup"><span data-stu-id="f344f-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="f344f-143">設定儲存體備援 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="f344f-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="f344f-144">當您建立的復原服務保存庫時，請確定儲存體備援設定的 hello 您想要的方式。</span><span class="sxs-lookup"><span data-stu-id="f344f-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="f344f-145">從 hello**復原服務保存庫**刀鋒視窗中，按一下 hello 新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="f344f-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![從 hello 復原服務保存庫清單中選取 hello 新的保存庫](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="f344f-147">當您選取 hello 保存庫時，hello**復原服務保存庫**刀鋒視窗縮小及 hello 設定 刀鋒視窗 (*hello 頂端具有 hello hello 保存庫名稱*) 和 hello 保存庫詳細資料 刀鋒視窗開啟。</span><span class="sxs-lookup"><span data-stu-id="f344f-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![檢視新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="f344f-149">在 hello 新的保存庫的設定 刀鋒視窗中，使用 hello 垂直投影片 tooscroll toohello 管理 區段中，關閉，然後按一下**備份基礎結構**。</span><span class="sxs-lookup"><span data-stu-id="f344f-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="f344f-150">hello 備份基礎結構刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f344f-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="f344f-151">在 hello 備份基礎結構刀鋒視窗中，按一下 **備份設定**tooopen hello**備份設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f344f-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![設定新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="f344f-153">選擇您的保存庫的 hello 適當的儲存體複寫選項。</span><span class="sxs-lookup"><span data-stu-id="f344f-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![儲存體組態選項](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="f344f-155">根據預設，保存庫具有異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="f344f-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="f344f-156">如果您使用 Azure 做為備份的主要儲存體端點時，繼續 toouse**異地備援**。</span><span class="sxs-lookup"><span data-stu-id="f344f-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="f344f-157">如果您不使用 Azure 做為備份的主要儲存體端點，然後選擇 **本機備援**，進而降低 hello Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="f344f-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="f344f-158">在此[儲存體備援概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="f344f-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="f344f-159">您已建立了保存庫，接著請設定它來備份 Windows 系統狀態。</span><span class="sxs-lookup"><span data-stu-id="f344f-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="f344f-160">設定 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="f344f-160">Configure hello vault</span></span>
1. <span data-ttu-id="f344f-161">在復原服務保存庫刀鋒視窗 （適用於 hello 保存庫中您剛建立），hello hello 開始使用 > 一節中，按一下**備份**，然後在 hello**開始使用備份**刀鋒視窗中，選取**備份目標**。</span><span class="sxs-lookup"><span data-stu-id="f344f-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="f344f-163">hello**備份目標**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f344f-163">hello **Backup Goal** blade opens.</span></span>

    ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="f344f-165">從 hello**其中執行您的工作負載？**下拉式選單中，選取**內部**。</span><span class="sxs-lookup"><span data-stu-id="f344f-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="f344f-166">因為您的 Windows Server 或 Windows 電腦是不在 Azure 中的實體電腦，所以您選擇 [內部部署]。</span><span class="sxs-lookup"><span data-stu-id="f344f-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="f344f-167">從 hello**怎麼辦想 toobackup？**功能表上，選取**系統狀態**，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f344f-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![設定檔案和資料夾](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="f344f-169">之後按一下 確定 核取記號會出現 下一步太**備份目標**，和 hello**準備基礎結構**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f344f-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![已設定備份目標，接下來是準備基礎結構](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="f344f-171">在 hello**準備基礎結構**刀鋒視窗中，按一下 **下載適用於 Windows Server 的代理程式或 Windows 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="f344f-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="f344f-173">如果您使用 Windows Server 基本項目，然後選擇 toodownload hello 代理程式的 Windows Server 不可或缺。</span><span class="sxs-lookup"><span data-stu-id="f344f-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="f344f-174">快顯功能表會提示您 toorun 或儲存 MARSAgentInstaller.exe。</span><span class="sxs-lookup"><span data-stu-id="f344f-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![MARSAgentInstaller dialog](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="f344f-176">在 hello 下載快顯功能表上，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="f344f-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="f344f-177">根據預設，hello **MARSagentinstaller.exe** tooyour Downloads 資料夾儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f344f-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="f344f-178">Hello 安裝程式完成時，您會看到快顯視窗，詢問您想 toorun hello 安裝程式，或開啟 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f344f-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="f344f-180">您無須 tooinstall hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f344f-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="f344f-181">您已下載 hello 保存庫認證之後，您可以安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="f344f-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="f344f-182">在 hello**準備基礎結構**刀鋒視窗中，按一下 **下載**。</span><span class="sxs-lookup"><span data-stu-id="f344f-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![下載保存庫認證](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="f344f-184">hello 保存庫認證下載 tooyour 下載 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f344f-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="f344f-185">Hello 保存庫認證完成下載之後，您會看到快顯視窗，詢問您想 tooopen 或儲存 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="f344f-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="f344f-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f344f-186">Click **Save**.</span></span> <span data-ttu-id="f344f-187">如果您不小心按**開啟**、 讓 hello 對話方塊中嘗試 tooopen hello 保存庫認證失敗。</span><span class="sxs-lookup"><span data-stu-id="f344f-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="f344f-188">您無法開啟 hello 保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="f344f-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="f344f-189">繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f344f-189">Proceed toohello next step.</span></span> <span data-ttu-id="f344f-190">hello 保存庫認證是在 hello 下載 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f344f-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![保存庫認證下載完成](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="f344f-192">安裝並註冊 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="f344f-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="f344f-193">透過 hello Azure 入口網站啟用備份尚無法使用。</span><span class="sxs-lookup"><span data-stu-id="f344f-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="f344f-194">使用 hello Microsoft Azure Recovery Services Agent tooback Windows 伺服器系統狀態。</span><span class="sxs-lookup"><span data-stu-id="f344f-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="f344f-195">找出並按兩下 hello **MARSagentinstaller.exe** hello 下載資料夾 （或其他已儲存的位置）。</span><span class="sxs-lookup"><span data-stu-id="f344f-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="f344f-196">hello 安裝程式會提供一系列的訊息，擷取安裝，並註冊 hello 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="f344f-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![執行復原服務代理安裝程式的認證](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="f344f-198">完成 hello Microsoft Azure Recovery Services Agent 安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="f344f-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="f344f-199">您需要 toocomplete hello 精靈:</span><span class="sxs-lookup"><span data-stu-id="f344f-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="f344f-200">選擇 hello 安裝和快取資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="f344f-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="f344f-201">提供 proxy 伺服器資訊，如果您使用 proxy 伺服器 tooconnect toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="f344f-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="f344f-202">如果您使用已驗證的 Proxy，請提供您的使用者名稱和密碼詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f344f-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="f344f-203">提供 hello 下載保存庫認證</span><span class="sxs-lookup"><span data-stu-id="f344f-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="f344f-204">將 hello 加密複雜密碼儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="f344f-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f344f-205">如果您遺失或忘記 hello 複雜密碼時，Microsoft 無法協助復原 hello 備份資料。</span><span class="sxs-lookup"><span data-stu-id="f344f-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="f344f-206">將 hello 檔案儲存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="f344f-206">Save hello file in a secure location.</span></span> <span data-ttu-id="f344f-207">它是必要的 toorestore 備份。</span><span class="sxs-lookup"><span data-stu-id="f344f-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="f344f-208">hello 代理程式現在已安裝，且您的電腦已註冊的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="f344f-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="f344f-209">正在準備 tooconfigure，並將備份排程。</span><span class="sxs-lookup"><span data-stu-id="f344f-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="f344f-210">備份 Windows Server 系統狀態 (預覽)</span><span class="sxs-lookup"><span data-stu-id="f344f-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="f344f-211">hello 初始備份包含三個工作：</span><span class="sxs-lookup"><span data-stu-id="f344f-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="f344f-212">啟用系統狀態備份使用 hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="f344f-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="f344f-213">Hello 備份排程</span><span class="sxs-lookup"><span data-stu-id="f344f-213">Schedule hello backup</span></span>
* <span data-ttu-id="f344f-214">備份檔案和資料夾進行 hello 第一次</span><span class="sxs-lookup"><span data-stu-id="f344f-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="f344f-215">toocomplete hello 初始備份、 使用 hello Microsoft Azure 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="f344f-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="f344f-216">使用 hello Azure Backup agent tooenable 系統狀態備份</span><span class="sxs-lookup"><span data-stu-id="f344f-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="f344f-217">PowerShell 工作階段中執行下列命令 toostop hello Azure 備份引擎 hello。</span><span class="sxs-lookup"><span data-stu-id="f344f-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="f344f-218">開啟 Windows 登錄 hello。</span><span class="sxs-lookup"><span data-stu-id="f344f-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="f344f-219">加入下列登錄機碼以 hello hello 指定 DWord 值。</span><span class="sxs-lookup"><span data-stu-id="f344f-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="f344f-220">登錄路徑</span><span class="sxs-lookup"><span data-stu-id="f344f-220">Registry path</span></span> | <span data-ttu-id="f344f-221">登錄機碼</span><span class="sxs-lookup"><span data-stu-id="f344f-221">Registry key</span></span> | <span data-ttu-id="f344f-222">DWord 值</span><span class="sxs-lookup"><span data-stu-id="f344f-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="f344f-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="f344f-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="f344f-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="f344f-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="f344f-225">2</span><span class="sxs-lookup"><span data-stu-id="f344f-225">2</span></span> |

4. <span data-ttu-id="f344f-226">藉由執行下列命令，在提升權限的命令提示字元中的 hello，重新啟動 hello 備份引擎。</span><span class="sxs-lookup"><span data-stu-id="f344f-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="f344f-227">tooschedule hello 備份工作</span><span class="sxs-lookup"><span data-stu-id="f344f-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="f344f-228">開啟 hello Microsoft Azure Recovery Services agent。</span><span class="sxs-lookup"><span data-stu-id="f344f-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="f344f-229">您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。</span><span class="sxs-lookup"><span data-stu-id="f344f-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![啟動 hello Azure 復原服務代理程式](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="f344f-231">在 hello 復原服務代理程式，按一下 **排程備份**。</span><span class="sxs-lookup"><span data-stu-id="f344f-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Windows Server 備份排程](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="f344f-233">在 [hello 上開始使用 hello 排程備份精靈] 頁面中，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="f344f-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="f344f-234">在 hello 選取項目 tooBackup 頁面上，按一下 **新增的項目**。</span><span class="sxs-lookup"><span data-stu-id="f344f-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="f344f-235">選取 系統狀態，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="f344f-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="f344f-236">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f344f-236">Click **Next**.</span></span>

7. <span data-ttu-id="f344f-237">hello 系統狀態備份和保留排程會自動設定 tooback 總每個星期天下午 9:00 的當地時間，並 hello 保留週期設 too60 天。</span><span class="sxs-lookup"><span data-stu-id="f344f-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f344f-238">系統會自動設定系統狀態的備份和保留原則。</span><span class="sxs-lookup"><span data-stu-id="f344f-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="f344f-239">如果您將備份檔案和資料夾此外 toohello Windows 伺服器系統狀態，指定唯一的檔案備份，從 hello 精靈的 hello 備份和保留原則。</span><span class="sxs-lookup"><span data-stu-id="f344f-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="f344f-240">在 hello 確認頁面上，檢閱 hello 資訊，然後再按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="f344f-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="f344f-241">Hello 精靈可讓您完成建立 hello 備份排程後，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="f344f-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="f344f-242">Windows 伺服器系統狀態的 tooback hello 第一次</span><span class="sxs-lookup"><span data-stu-id="f344f-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="f344f-243">確定 Windows Server 沒有需要重新啟動的擱置中更新。</span><span class="sxs-lookup"><span data-stu-id="f344f-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="f344f-244">在 hello 復原服務代理程式，按一下 **立即備份**toocomplete hello 初始植入 hello 網路上。</span><span class="sxs-lookup"><span data-stu-id="f344f-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![立即備份 Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="f344f-246">在 hello 確認頁面上，檢閱 hello 立即備份精靈的 hello 設定會使用 tooback hello 機器。</span><span class="sxs-lookup"><span data-stu-id="f344f-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="f344f-247">然後按一下 [備份] 。</span><span class="sxs-lookup"><span data-stu-id="f344f-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="f344f-248">按一下**關閉**tooclose hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="f344f-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="f344f-249">如果您在 hello 備份程序完成之前關閉 hello 精靈，hello 精靈會繼續 toorun hello 背景。</span><span class="sxs-lookup"><span data-stu-id="f344f-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="f344f-250">如果您將備份檔案和資料夾在伺服器上另外 toohello Windows 伺服器系統狀態，hello 立即備份精靈會只備份檔案。</span><span class="sxs-lookup"><span data-stu-id="f344f-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="f344f-251">tooperform 臨機操作的系統狀態備份，請使用下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f344f-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="f344f-252">Hello 初始備份完成後，hello**作業已完成**hello Backup 主控台中顯示的狀態。</span><span class="sxs-lookup"><span data-stu-id="f344f-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![IR 已完成](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="f344f-254">常見問題集</span><span class="sxs-lookup"><span data-stu-id="f344f-254">Frequently asked questions</span></span>

<span data-ttu-id="f344f-255">hello 以下問題和解答提供補充資訊。</span><span class="sxs-lookup"><span data-stu-id="f344f-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="f344f-256">什麼是 hello 暫存磁碟區？</span><span class="sxs-lookup"><span data-stu-id="f344f-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="f344f-257">hello 暫存磁碟區表示 hello hello 原生功能，Windows Server Backup 要分階段 hello 系統狀態備份的中間位置。</span><span class="sxs-lookup"><span data-stu-id="f344f-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="f344f-258">Azure 備份代理程式則會壓縮及加密此中繼備份並將它透過安全的 HTTPS 通訊協定 toohello 設定復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="f344f-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="f344f-259">**我們強烈建議您在非 Windows 作業系統磁碟區建立 hello 暫存磁碟區。如果您觀察系統狀態備份發生問題時，檢查您的暫存磁碟區的 hello 位置是 hello 的第一個疑難排解步驟。**</span><span class="sxs-lookup"><span data-stu-id="f344f-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="f344f-260">如何變更 hello hello Azure Backup agent 中指定的暫存磁碟區路徑？</span><span class="sxs-lookup"><span data-stu-id="f344f-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="f344f-261">根據預設 hello 暫存磁碟區位於 hello 快取資料夾。</span><span class="sxs-lookup"><span data-stu-id="f344f-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="f344f-262">toochange 這個位置，使用下列命令 （在提升權限的命令提示字元） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="f344f-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="f344f-263">然後更新 hello 遵循 hello 路徑 toohello 新暫存磁碟區的資料夾與登錄項目。</span><span class="sxs-lookup"><span data-stu-id="f344f-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="f344f-264">登錄路徑</span><span class="sxs-lookup"><span data-stu-id="f344f-264">Registry path</span></span>|<span data-ttu-id="f344f-265">登錄機碼</span><span class="sxs-lookup"><span data-stu-id="f344f-265">Registry key</span></span>|<span data-ttu-id="f344f-266">值</span><span class="sxs-lookup"><span data-stu-id="f344f-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="f344f-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="f344f-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="f344f-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="f344f-268">SSBStagingPath</span></span> | <span data-ttu-id="f344f-269">新的暫存磁碟區位置</span><span class="sxs-lookup"><span data-stu-id="f344f-269">new staging volume location</span></span> |

<span data-ttu-id="f344f-270">hello 臨時區域路徑會區分大小寫，而且必須是 hello 完全相同的大小寫為項目存在 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="f344f-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="f344f-271">一旦變更 hello 暫存磁碟區路徑，請重新啟動 hello 備份引擎：</span><span class="sxs-lookup"><span data-stu-id="f344f-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="f344f-272">toopick 出 hello 變更路徑，請開啟 hello Microsoft Azure 復原服務代理程式觸發程序的系統狀態的臨機操作備份。</span><span class="sxs-lookup"><span data-stu-id="f344f-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="f344f-273">為什麼會預設保留設定 too60 天 hello 系統狀態？</span><span class="sxs-lookup"><span data-stu-id="f344f-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="f344f-274">系統狀態備份的 hello 有用的生命週期是 hello 與 hello 」 標記存留時間 」 設定 hello Windows Server Active Directory 角色相同。</span><span class="sxs-lookup"><span data-stu-id="f344f-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="f344f-275">hello 標記存留期項目的 hello 預設值是 60 天。</span><span class="sxs-lookup"><span data-stu-id="f344f-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="f344f-276">這個值可以在 hello 目錄服務 (NTDS) 組態物件上設定。</span><span class="sxs-lookup"><span data-stu-id="f344f-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="f344f-277">如何變更 hello 預設備份和系統狀態的保留原則？</span><span class="sxs-lookup"><span data-stu-id="f344f-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="f344f-278">toochange hello 預設備份和保留原則對於系統狀態：</span><span class="sxs-lookup"><span data-stu-id="f344f-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="f344f-279">停止 hello 備份引擎。</span><span class="sxs-lookup"><span data-stu-id="f344f-279">Stop hello Backup engine.</span></span> <span data-ttu-id="f344f-280">執行下列命令，從提升權限的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="f344f-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="f344f-281">加入或更新 hello 遵循 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider 中登錄索引鍵的項目。</span><span class="sxs-lookup"><span data-stu-id="f344f-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="f344f-282">登錄名稱</span><span class="sxs-lookup"><span data-stu-id="f344f-282">Registry Name</span></span>|<span data-ttu-id="f344f-283">說明</span><span class="sxs-lookup"><span data-stu-id="f344f-283">Description</span></span>|<span data-ttu-id="f344f-284">值</span><span class="sxs-lookup"><span data-stu-id="f344f-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="f344f-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="f344f-285">SSBScheduleTime</span></span>|<span data-ttu-id="f344f-286">使用的 tooconfigure hello hello 備份時間。</span><span class="sxs-lookup"><span data-stu-id="f344f-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="f344f-287">預設值為當地時間下午 9 點。</span><span class="sxs-lookup"><span data-stu-id="f344f-287">Default is 9PM local time.</span></span>|<span data-ttu-id="f344f-288">DWord：格式為 HHMM (十進位)，例如用 2130 代表當地時間下午 9:30</span><span class="sxs-lookup"><span data-stu-id="f344f-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="f344f-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="f344f-289">SSBScheduleDays</span></span>|<span data-ttu-id="f344f-290">使用的 tooconfigure hello 天系統狀態備份時必須在 hello 執行指定的時間。</span><span class="sxs-lookup"><span data-stu-id="f344f-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="f344f-291">獨立的數字指定 hello 一週天數。</span><span class="sxs-lookup"><span data-stu-id="f344f-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="f344f-292">0 代表星期日、1 代表星期一，依此類推。</span><span class="sxs-lookup"><span data-stu-id="f344f-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="f344f-293">預設的備份日是星期日。</span><span class="sxs-lookup"><span data-stu-id="f344f-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="f344f-294">Hello 週 toorun 備份 1230年例如排定備份在上星期一、 星期二、 星期三與星期日 （十進位） 的 DWord： 天數。</span><span class="sxs-lookup"><span data-stu-id="f344f-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="f344f-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="f344f-295">SSBRetentionDays</span></span>|<span data-ttu-id="f344f-296">使用的 tooconfigure hello 天 tooretain 備份。</span><span class="sxs-lookup"><span data-stu-id="f344f-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="f344f-297">預設值為 60。</span><span class="sxs-lookup"><span data-stu-id="f344f-297">Default value is 60.</span></span> <span data-ttu-id="f344f-298">允許的最大值為 180。</span><span class="sxs-lookup"><span data-stu-id="f344f-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="f344f-299">DWord： 天 tooretain 備份 （十進位）。</span><span class="sxs-lookup"><span data-stu-id="f344f-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="f344f-300">使用下列命令 toorestart hello 備份引擎 hello。</span><span class="sxs-lookup"><span data-stu-id="f344f-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="f344f-301">開啟 hello Microsoft 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="f344f-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="f344f-302">按一下**排程備份**，然後按一下**下一步**直至您看見 hello 反映的變更。</span><span class="sxs-lookup"><span data-stu-id="f344f-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="f344f-303">按一下**完成**tooapply hello 變更。</span><span class="sxs-lookup"><span data-stu-id="f344f-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="f344f-304">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="f344f-304">Questions?</span></span>
<span data-ttu-id="f344f-305">如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="f344f-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f344f-306">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f344f-306">Next steps</span></span>
* <span data-ttu-id="f344f-307">詳細了解如何 [備份 Windows 電腦](backup-configure-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="f344f-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="f344f-308">現在您已備份好檔案和資料夾，接下來您可以 [管理您的保存庫和伺服器](backup-azure-manage-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="f344f-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="f344f-309">如果您需要 toorestore 備份，請使用本文章太[還原檔案 tooa Windows 機器](backup-azure-restore-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="f344f-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
