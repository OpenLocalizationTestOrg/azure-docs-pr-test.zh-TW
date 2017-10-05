---
title: "使用 Azure 備份代理程式來備份檔案和資料夾 | Microsoft Docs"
description: "使用 Microsoft Azure 備份代理程式，可將 Windows 檔案和資料夾備份至 Azure。 建立復原服務保存庫、安裝備份代理程式、定義備份原則，並對檔案和資料夾執行初始備份。"
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="6cba8-105">使用資源管理員部署模型將 Windows Server 或用戶端備份至 Azure</span><span class="sxs-lookup"><span data-stu-id="6cba8-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6cba8-106">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6cba8-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="6cba8-107">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="6cba8-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="6cba8-108">本文說明如何 Resource Manager 部署模型將 Windows Server (或 Windows 用戶端) 檔案和資料夾備份至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6cba8-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![備份程序步驟](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="6cba8-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="6cba8-110">Before you start</span></span>
<span data-ttu-id="6cba8-111">若要將伺服器或用戶端備份至 Azure，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cba8-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="6cba8-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="6cba8-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6cba8-113">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="6cba8-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="6cba8-114">復原服務保存庫是一個實體，會儲存歷來建立的所有備份和復原點。</span><span class="sxs-lookup"><span data-stu-id="6cba8-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="6cba8-115">復原服務保存庫也包含套用至受保護檔案和資料夾的備份原則。</span><span class="sxs-lookup"><span data-stu-id="6cba8-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="6cba8-116">當您建立復原服務保存庫時，也應該選取適當的儲存體備援選項。</span><span class="sxs-lookup"><span data-stu-id="6cba8-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="6cba8-117">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="6cba8-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="6cba8-118">如果您尚未這麼做，請使用 Azure 訂用帳戶登入 [Azure 入口網站](https://portal.azure.com/) 。</span><span class="sxs-lookup"><span data-stu-id="6cba8-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="6cba8-119">在 [中樞] 功能表上按一下 [更多服務]，在資源清單中輸入**復原服務**，然後按一下 [復原服務保存庫]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="6cba8-121">如果訂用帳戶中有復原服務保存庫，則會列出保存庫。</span><span class="sxs-lookup"><span data-stu-id="6cba8-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="6cba8-122">在 [復原服務保存庫] 功能表上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![建立復原服務保存庫的步驟 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="6cba8-124">[復原服務保存庫] 刀鋒視窗隨即開啟，並提示您提供 [名稱]、[訂用帳戶]、[資源群組] 和 [位置]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![建立復原服務保存庫的步驟 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="6cba8-126">在 [名稱] 中，輸入易記名稱來識別保存庫。</span><span class="sxs-lookup"><span data-stu-id="6cba8-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="6cba8-127">必須是 Azure 訂用帳戶中唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="6cba8-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="6cba8-128">輸入包含 2 到 50 個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="6cba8-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="6cba8-129">該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="6cba8-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="6cba8-130">在 [訂用帳戶] 區段中，使用下拉式功能表來選擇 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cba8-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="6cba8-131">如果您只使用一個訂用帳戶，該訂用帳戶會出現，您可以跳到下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="6cba8-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="6cba8-132">如果您不確定要使用哪個訂用帳戶，請使用預設 (或建議) 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6cba8-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="6cba8-133">只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。</span><span class="sxs-lookup"><span data-stu-id="6cba8-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="6cba8-134">在 [資源群組] 區段中︰</span><span class="sxs-lookup"><span data-stu-id="6cba8-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="6cba8-135">如果您想建立新的資源群組，請選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="6cba8-136">或</span><span class="sxs-lookup"><span data-stu-id="6cba8-136">Or</span></span>
    * <span data-ttu-id="6cba8-137">選取 [使用現有的]﹐然後按一下下拉式功能表，以查看可用的資源群組清單。</span><span class="sxs-lookup"><span data-stu-id="6cba8-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="6cba8-138">如需資源群組的完整資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6cba8-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="6cba8-139">按一下 [位置]  以選取保存庫的地理區域。</span><span class="sxs-lookup"><span data-stu-id="6cba8-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="6cba8-140">此選項會決定您的備份資料要傳送到哪個地理區域。</span><span class="sxs-lookup"><span data-stu-id="6cba8-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="6cba8-141">按一下 [復原服務保存庫] 刀鋒視窗底部的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="6cba8-142">建立復原服務保存庫可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="6cba8-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="6cba8-143">請監視入口網站右上方區域中的狀態通知。</span><span class="sxs-lookup"><span data-stu-id="6cba8-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="6cba8-144">保存庫一旦建立好，就會出現在 [復原服務保存庫] 的清單中。</span><span class="sxs-lookup"><span data-stu-id="6cba8-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="6cba8-145">在數分鐘之後﹐如果您沒有看到您的保存庫，請按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![按一下 [重新整理] 按鈕。](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="6cba8-147">一旦在復原服務保存庫清單中看到您的保存庫，您即可開始設定儲存體備援。</span><span class="sxs-lookup"><span data-stu-id="6cba8-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="6cba8-148">設定儲存體備援</span><span class="sxs-lookup"><span data-stu-id="6cba8-148">Set storage redundancy</span></span>
<span data-ttu-id="6cba8-149">首次建立復原服務保存庫時會決定儲存體的複寫方式。</span><span class="sxs-lookup"><span data-stu-id="6cba8-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="6cba8-150">從 [復原服務保存庫] 刀鋒視窗，按一下 [新增保存庫]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![從復原服務保存庫清單中選取新的保存庫](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="6cba8-152">當您選取保存庫時，[復原服務保存庫] 刀鋒視窗會縮小﹐而 [設定] 刀鋒視窗 (頂端有保存庫名稱) 和 [保存庫詳細資料] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6cba8-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![檢視新保存庫的儲存體組態](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="6cba8-154">在新保存庫的 [設定] 刀鋒視窗中，使用垂直滑桿捲動至 [管理] 區段，然後按一下 [備份基礎結構]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="6cba8-155">[備份基礎結構] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6cba8-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="6cba8-156">在 [備份基礎結構] 刀鋒視窗中，按一下 [備份設定]開啟 [備份設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6cba8-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![為新保存庫設定儲存體組態](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="6cba8-158">為保存庫選擇適當的儲存體複寫選項。</span><span class="sxs-lookup"><span data-stu-id="6cba8-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![儲存體組態選項](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="6cba8-160">根據預設，保存庫具有異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="6cba8-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="6cba8-161">如果您使用 Azure 做為主要的備份儲存體端點，請繼續使用 [異地備援]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="6cba8-162">如果您未使用 Azure 做為主要的備份儲存體端點，則選擇 [本地備援]，以減少 Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="6cba8-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="6cba8-163">在此[儲存體備援概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。</span><span class="sxs-lookup"><span data-stu-id="6cba8-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="6cba8-164">現在您已建立保存庫，接下來請下載及安裝 Microsoft Azure 復原服務代理程式、下載保存庫認證，以及使用這些認證向保存庫註冊代理程式，讓基礎結構做好備份檔案和資料夾的準備。</span><span class="sxs-lookup"><span data-stu-id="6cba8-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="6cba8-165">設定保存庫</span><span class="sxs-lookup"><span data-stu-id="6cba8-165">Configure the vault</span></span>

1. <span data-ttu-id="6cba8-166">在 [復原服務保存庫] 刀鋒視窗上 (針對剛建立的保存庫)，在 [開始使用] 區段中按一下 [備份]，然後在 [開始使用備份功能] 刀鋒視窗上，選取 [備份目標]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="6cba8-168">[備份目標] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6cba8-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="6cba8-169">如果先前已設定過復原服務保存庫，當您按一下 [復原服務保存庫] 刀鋒視窗上的 [備份] 時，便會開啟 [備份目標] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6cba8-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="6cba8-171">從 [您的工作負載在何處執行?] 下拉式功能表中，選取 [內部部署]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="6cba8-172">因為您的 Windows Server 或 Windows 電腦是不在 Azure 中的實體電腦，所以您選擇 [內部部署]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="6cba8-173">從 [您要備份什麼?] 功能表中，選取 [檔案和資料夾]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![設定檔案和資料夾](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="6cba8-175">按一下 [確定] 後，[備份目標] 旁會出現勾選記號，且 [準備基礎結構] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6cba8-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![已設定備份目標，接下來是準備基礎結構](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="6cba8-177">在 [準備基礎結構] 刀鋒視窗上，按 [下載 Windows Server 或 Windows Client 的代理程式]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="6cba8-179">如果您使用 Windows Server Essential，請選擇下載 Windows Server Essential 的代理程式。</span><span class="sxs-lookup"><span data-stu-id="6cba8-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="6cba8-180">快顯功能表會提示您執行或儲存 MARSAgentInstaller.exe。</span><span class="sxs-lookup"><span data-stu-id="6cba8-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![MARSAgentInstaller dialog](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="6cba8-182">在下載快顯功能表中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="6cba8-183">根據預設，**MARSagentinstaller.exe** 檔案會儲存至 [下載] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cba8-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="6cba8-184">安裝程式完成時，您會看到快顯視窗，詢問您是否要執行安裝程式，或開啟資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cba8-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="6cba8-186">您還不需要安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="6cba8-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="6cba8-187">您可以在下載保存庫認證之後﹐安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="6cba8-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="6cba8-188">在 [準備基礎結構] 刀鋒視窗上，按 [下載]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![下載保存庫認證](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="6cba8-190">保存庫認證會下載至「下載」資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cba8-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="6cba8-191">保存庫認證下載完成之後，您會看到快顯視窗，詢問您是否要開啟或儲存認證。</span><span class="sxs-lookup"><span data-stu-id="6cba8-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="6cba8-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6cba8-192">Click **Save**.</span></span> <span data-ttu-id="6cba8-193">如果您不小心按到 [開啟]，請讓嘗試開啟保存庫認證的對話方塊失敗。</span><span class="sxs-lookup"><span data-stu-id="6cba8-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="6cba8-194">您無法開啟保存庫認證。</span><span class="sxs-lookup"><span data-stu-id="6cba8-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="6cba8-195">請繼續進行下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="6cba8-195">Proceed to the next step.</span></span> <span data-ttu-id="6cba8-196">保存庫認證位於 [下載] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6cba8-196">The vault credentials are in the Downloads folder.</span></span>   

  ![保存庫認證下載完成](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="6cba8-198">安裝和註冊代理程式</span><span class="sxs-lookup"><span data-stu-id="6cba8-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="6cba8-199">透過 Azure 入口網站啟用備份的功能尚未推出。</span><span class="sxs-lookup"><span data-stu-id="6cba8-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="6cba8-200">使用 Microsoft Azure 復原服務代理程式來備份檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="6cba8-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="6cba8-201">在 [下載] 資料夾 (或其他儲存位置) 中找到 **MARSagentinstaller.exe** 並對其按兩下。</span><span class="sxs-lookup"><span data-stu-id="6cba8-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="6cba8-202">安裝程式在擷取、安裝和註冊復原服務代理程式時會提供一系列訊息。</span><span class="sxs-lookup"><span data-stu-id="6cba8-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![執行復原服務代理安裝程式的認證](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="6cba8-204">完成 Microsoft Azure 復原服務代理程式安裝精靈。</span><span class="sxs-lookup"><span data-stu-id="6cba8-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="6cba8-205">若要完成精靈，您需要︰</span><span class="sxs-lookup"><span data-stu-id="6cba8-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="6cba8-206">選擇安裝和快取資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="6cba8-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="6cba8-207">如果您使用 Proxy 伺服器來連線到網際網路，請提供您的 Proxy 伺服器資訊。</span><span class="sxs-lookup"><span data-stu-id="6cba8-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="6cba8-208">如果您使用已驗證的 Proxy，請提供您的使用者名稱和密碼詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6cba8-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="6cba8-209">提供下載的保存庫認證</span><span class="sxs-lookup"><span data-stu-id="6cba8-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="6cba8-210">將加密複雜密碼存放在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="6cba8-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6cba8-211">如果遺失或忘記複雜密碼，Microsoft 將無法協助您復原備份資料。</span><span class="sxs-lookup"><span data-stu-id="6cba8-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="6cba8-212">將檔案存放在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="6cba8-212">Save the file in a secure location.</span></span> <span data-ttu-id="6cba8-213">必須有此檔案才能還原備份。</span><span class="sxs-lookup"><span data-stu-id="6cba8-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="6cba8-214">現已安裝代理程式，且已向保存庫註冊您的電腦。</span><span class="sxs-lookup"><span data-stu-id="6cba8-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="6cba8-215">您已準備好可以設定及排程備份。</span><span class="sxs-lookup"><span data-stu-id="6cba8-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="6cba8-216">網路和連線性需求</span><span class="sxs-lookup"><span data-stu-id="6cba8-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="6cba8-217">如果您的電腦/Proxy 具有受限的網際網路存取，請確保將電腦/Proxy 上的防火牆設定，設定為允許下列 URL：</span><span class="sxs-lookup"><span data-stu-id="6cba8-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="6cba8-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="6cba8-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="6cba8-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6cba8-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="6cba8-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="6cba8-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="6cba8-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6cba8-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="6cba8-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="6cba8-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="6cba8-223">建立備份原則</span><span class="sxs-lookup"><span data-stu-id="6cba8-223">Create the backup policy</span></span>
<span data-ttu-id="6cba8-224">備份原則就是復原點擷取排程以及復原點保留時間長度。</span><span class="sxs-lookup"><span data-stu-id="6cba8-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="6cba8-225">請使用 Microsoft Azure 備份代理程式來為檔案和資料夾建立備份原則。</span><span class="sxs-lookup"><span data-stu-id="6cba8-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="6cba8-226">建立備份排程</span><span class="sxs-lookup"><span data-stu-id="6cba8-226">To create a backup schedule</span></span>
1. <span data-ttu-id="6cba8-227">開啟 Microsoft Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="6cba8-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="6cba8-228">您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。</span><span class="sxs-lookup"><span data-stu-id="6cba8-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![啟動 Azure 備份代理程式](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="6cba8-230">在備份代理程式的 [動作] 窗格中，按一下 [排程備份] 以啟動「排程備份精靈」。</span><span class="sxs-lookup"><span data-stu-id="6cba8-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Windows Server 備份排程](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="6cba8-232">在排程備份精靈的 [開始使用] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="6cba8-233">在 [選取要備份的項目] 頁面上，按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="6cba8-234">[選取項目] 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6cba8-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="6cba8-235">選取您要保護的檔案和資料夾，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="6cba8-236">在 [選取要備份的項目] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="6cba8-237">在 [指定備份排程] 頁面上，指定備份排程並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="6cba8-238">您可以排程每日 (一天最多三次) 或每週備份。</span><span class="sxs-lookup"><span data-stu-id="6cba8-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Windows Server 備份項目](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="6cba8-240">如需如何指定備份排程的相關詳細資訊，請參閱 [使用 Azure 備份來取代您的磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)一文。</span><span class="sxs-lookup"><span data-stu-id="6cba8-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="6cba8-241">在 [選取保留原則] 頁面上，選擇用於備份複本的特定保留原則，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="6cba8-242">保留原則會指定備份的儲存持續期間。</span><span class="sxs-lookup"><span data-stu-id="6cba8-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="6cba8-243">除了僅針對所有備份點指定「一般原則」之外，您可以指定在進行備份時根據不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="6cba8-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="6cba8-244">您可以修改每日、每週、每月和每年保留原則，以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="6cba8-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="6cba8-245">在 [選擇初始備份類型] 頁面上，選擇初始備份類型。</span><span class="sxs-lookup"><span data-stu-id="6cba8-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="6cba8-246">讓 [自動透過網路] 選項保持已選取狀態，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="6cba8-247">您可以透過網路自動備份，也可以離線備份。</span><span class="sxs-lookup"><span data-stu-id="6cba8-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="6cba8-248">這篇文章的其餘部分說明自動備份的程序。</span><span class="sxs-lookup"><span data-stu-id="6cba8-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="6cba8-249">如果您想要執行離線備份，請檢閱 [在 Azure Backup 中離線備份工作流程](backup-azure-backup-import-export.md) 一文以了解其他資訊。</span><span class="sxs-lookup"><span data-stu-id="6cba8-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="6cba8-250">在 [確認] 頁面上檢閱資訊，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="6cba8-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="6cba8-251">當精靈建立好備份排程時，請按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="6cba8-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="6cba8-252">啟用網路節流</span><span class="sxs-lookup"><span data-stu-id="6cba8-252">Enable network throttling</span></span>
<span data-ttu-id="6cba8-253">Microsoft Azure 備份代理程式提供網路節流。</span><span class="sxs-lookup"><span data-stu-id="6cba8-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="6cba8-254">節流會控制資料傳輸期間的網路頻寬使用方式。</span><span class="sxs-lookup"><span data-stu-id="6cba8-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="6cba8-255">如果您需要在上班時間內備份資料，但不希望備份程序干擾其他網際網路流量，這樣的控制會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="6cba8-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="6cba8-256">節流適用於備份和還原活動。</span><span class="sxs-lookup"><span data-stu-id="6cba8-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="6cba8-257">網路節流不適用於 Windows Server 2008 R2 SP1、Windows Server 2008 SP2 或 Windows 7 (含 service pack)。</span><span class="sxs-lookup"><span data-stu-id="6cba8-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="6cba8-258">Azure 備份網路節流功能可保證本機作業系統上的服務品質 (QoS)。</span><span class="sxs-lookup"><span data-stu-id="6cba8-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="6cba8-259">雖然 Azure 備份可保護這些作業系統，但這些平台上可用的 QoS 版本無法與 Azure 備份網路節流搭配使用。</span><span class="sxs-lookup"><span data-stu-id="6cba8-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="6cba8-260">網路節流可使用於所有其他 [支援的作業系統](backup-azure-backup-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="6cba8-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="6cba8-261">**啟用網路節流**</span><span class="sxs-lookup"><span data-stu-id="6cba8-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="6cba8-262">在 Microsoft Azure 備份代理程式中，按一下 [變更屬性]。</span><span class="sxs-lookup"><span data-stu-id="6cba8-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![變更屬性](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="6cba8-264">在 [節流] 索引標籤上，選取 [啟用備份作業的網際網路頻寬使用節流功能] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6cba8-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![網路節流](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="6cba8-266">在您啟用節流之後，請指定允許的頻寬進行 [工作時間] 和 [非工作時間] 期間的備份資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="6cba8-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="6cba8-267">頻寬值從每秒 512 KB (Kbps) 開始，並可高達每秒 1023 MB (Mbps)。</span><span class="sxs-lookup"><span data-stu-id="6cba8-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="6cba8-268">您也可以指定 [工作時間] 的開始和完成時間，以及一週中有哪幾天視為工作天。</span><span class="sxs-lookup"><span data-stu-id="6cba8-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="6cba8-269">指定之工作時間以外的時間則視為非工作時間。</span><span class="sxs-lookup"><span data-stu-id="6cba8-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="6cba8-270">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="6cba8-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="6cba8-271">第一次備份檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="6cba8-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="6cba8-272">在備份代理程式中，按一下 [立即備份]  ，以透過網路完成初始植入。</span><span class="sxs-lookup"><span data-stu-id="6cba8-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Windows Server 立即備份](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="6cba8-274">在 [確認] 頁面上，檢閱立即備份精靈將用於備份電腦的設定。</span><span class="sxs-lookup"><span data-stu-id="6cba8-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="6cba8-275">然後按一下 [備份] 。</span><span class="sxs-lookup"><span data-stu-id="6cba8-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="6cba8-276">按一下 [關閉]  即可關閉精靈。</span><span class="sxs-lookup"><span data-stu-id="6cba8-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="6cba8-277">如果您在備份程序完成之前關閉精靈，精靈會繼續在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="6cba8-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="6cba8-278">完成初始備份之後，備份主控台中會顯示 [作業已完成]  狀態。</span><span class="sxs-lookup"><span data-stu-id="6cba8-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR 已完成](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="6cba8-280">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="6cba8-280">Questions?</span></span>
<span data-ttu-id="6cba8-281">如果您有問題，或希望我們加入任何功能，請 [傳送意見反應給我們](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="6cba8-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cba8-282">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cba8-282">Next steps</span></span>
<span data-ttu-id="6cba8-283">如需備份 VM 或其他工作負載的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="6cba8-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="6cba8-284">現在您已備份好檔案和資料夾，接下來您可以 [管理您的保存庫和伺服器](backup-azure-manage-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="6cba8-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="6cba8-285">如果您需要還原備份，請使用本文來 [還原檔案到 Windows 電腦](backup-azure-restore-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="6cba8-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
