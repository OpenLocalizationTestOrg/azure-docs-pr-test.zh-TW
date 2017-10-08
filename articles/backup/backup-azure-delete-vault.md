---
title: " 刪除 Azure 中的復原服務保存庫 | Microsoft Docs "
description: "如何 toodelete Azure 備份和復原服務保存庫。 備份保存庫可稱為 Azure 雲端保存庫，或 Azure 復原保存庫。 當您無法刪除備份保存庫中 hello 傳統入口網站或 Azure 入口網站時，請疑難排解問題。"
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a><span data-ttu-id="2f477-105">刪除復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="2f477-105">Delete a Recovery Services vault</span></span>
<span data-ttu-id="2f477-106">hello Azure 備份服務有兩種類型的保存庫-hello 備份保存庫及 hello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-106">hello Azure Backup service has two types of vaults - hello Backup vault and hello Recovery Services vault.</span></span> <span data-ttu-id="2f477-107">hello 備份保存庫來自第一個項目。</span><span class="sxs-lookup"><span data-stu-id="2f477-107">hello Backup vault came first.</span></span> <span data-ttu-id="2f477-108">然後復原服務保存庫的 hello 以往 toosupport hello 展開資源管理員部署。</span><span class="sxs-lookup"><span data-stu-id="2f477-108">Then hello Recovery Services vault came along toosupport hello expanded Resource Manager deployments.</span></span> <span data-ttu-id="2f477-109">因為 hello 擴充的功能和必須儲存在 hello 保存庫刪除備份或復原服務保存庫中的 hello 資訊相依性可能會造成混淆。</span><span class="sxs-lookup"><span data-stu-id="2f477-109">Because of hello expanded capabilities and hello information dependencies that must be stored in hello vault, deleting a Backup or Recovery Services vault can be confusing.</span></span> <span data-ttu-id="2f477-110">本文說明 toodelete hello hello 傳統入口網站和 hello Azure 入口網站中的保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-110">This article explains how toodelete hello vaults in hello classic portal and hello Azure portal.</span></span>  

| <span data-ttu-id="2f477-111">**部署類型**</span><span class="sxs-lookup"><span data-stu-id="2f477-111">**Deployment Type**</span></span> | <span data-ttu-id="2f477-112">**入口網站**</span><span class="sxs-lookup"><span data-stu-id="2f477-112">**Portal**</span></span> | <span data-ttu-id="2f477-113">**保存庫名稱**</span><span class="sxs-lookup"><span data-stu-id="2f477-113">**Vault name**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f477-114">傳統</span><span class="sxs-lookup"><span data-stu-id="2f477-114">Classic</span></span> |<span data-ttu-id="2f477-115">傳統</span><span class="sxs-lookup"><span data-stu-id="2f477-115">Classic</span></span> |<span data-ttu-id="2f477-116">備份保存庫</span><span class="sxs-lookup"><span data-stu-id="2f477-116">Backup vault</span></span> |
| <span data-ttu-id="2f477-117">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2f477-117">Resource Manager</span></span> |<span data-ttu-id="2f477-118">Azure</span><span class="sxs-lookup"><span data-stu-id="2f477-118">Azure</span></span> |<span data-ttu-id="2f477-119">復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="2f477-119">Recovery Services vault</span></span> |

> [!NOTE]
> <span data-ttu-id="2f477-120">備份保存庫無法保護 Resource Manager 部署的解決方案。</span><span class="sxs-lookup"><span data-stu-id="2f477-120">Backup vaults cannot protect Resource Manager-deployed solutions.</span></span> <span data-ttu-id="2f477-121">不過，您可以使用 復原服務保存庫 tooprotect 原本部署伺服器和 Vm。</span><span class="sxs-lookup"><span data-stu-id="2f477-121">However, you can use a Recovery Services vault tooprotect classically deployed servers and VMs.</span></span>  
>

> [!IMPORTANT]
> <span data-ttu-id="2f477-122">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-122">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="2f477-123">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="2f477-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="2f477-124">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="2f477-125">**2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-125">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="2f477-126">**自 2017 年 11 月 1 日起**：</span><span class="sxs-lookup"><span data-stu-id="2f477-126">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="2f477-127">任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-127">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="2f477-128">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="2f477-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="2f477-129">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="2f477-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="2f477-130">在本文中，我們將使用 hello 詞彙、 保存庫、 toorefer toohello 一般表單的 hello 備份保存庫或復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-130">In this article, we use hello term, vault, toorefer toohello generic form of hello Backup vault or Recovery Services vault.</span></span> <span data-ttu-id="2f477-131">我們使用 hello 正式名稱、 備份保存庫或復原服務保存庫時，它需要 toodistinguish hello 保存庫之間。</span><span class="sxs-lookup"><span data-stu-id="2f477-131">We use hello formal name, Backup vault, or Recovery Services vault, when it is necessary toodistinguish between hello vaults.</span></span>

## <a name="deleting-a-recovery-services-vault"></a><span data-ttu-id="2f477-132">刪除復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="2f477-132">Deleting a Recovery Services vault</span></span>
<span data-ttu-id="2f477-133">刪除復原服務保存庫是一步驟的程序- *hello 保存庫不包含任何資源提供*。</span><span class="sxs-lookup"><span data-stu-id="2f477-133">Deleting a Recovery Services vault is a one-step process - *provided hello vault doesn't contain any resources*.</span></span> <span data-ttu-id="2f477-134">您可以刪除復原服務保存庫之前，您必須移除或刪除 hello 保存庫中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="2f477-134">Before you can delete a Recovery Services vault, you must remove or delete all resources in hello vault.</span></span> <span data-ttu-id="2f477-135">如果您嘗試 toodelete 包含資源的保存庫，您會取得下列映像的 hello 類似錯誤：</span><span class="sxs-lookup"><span data-stu-id="2f477-135">If you attempt toodelete a vault that contains resources, you get an error like hello following image:</span></span>

![保存庫刪除錯誤](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

<span data-ttu-id="2f477-137">您已經清除 hello hello 保存庫中的資源，直到按一下**重試**產生 hello 相同的錯誤。</span><span class="sxs-lookup"><span data-stu-id="2f477-137">Until you have cleared hello resources from hello vault, clicking **Retry** produces hello same error.</span></span> <span data-ttu-id="2f477-138">如果您正在卡錯誤訊息，請按一下**取消**和使用 hello 下列步驟 toodelete hello 保存庫中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="2f477-138">If you're stuck on this error message, click **Cancel** and use hello following steps toodelete hello resources in hello vault.</span></span>

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a><span data-ttu-id="2f477-139">移除保護 VM 的保存庫中的 hello 項目</span><span class="sxs-lookup"><span data-stu-id="2f477-139">Removing hello items from a vault protecting a VM</span></span>
<span data-ttu-id="2f477-140">如果您已經有 hello 復原服務保存庫開啟時，略過 toohello 第二個步驟。</span><span class="sxs-lookup"><span data-stu-id="2f477-140">If you already have hello Recovery Services vault open, skip toohello second step.</span></span>

1. <span data-ttu-id="2f477-141">開啟 hello Azure 入口網站，然後 hello 儀表板開啟您想要 toodelete hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-141">Open hello Azure portal, and from hello Dashboard open hello vault you want toodelete.</span></span>

   <span data-ttu-id="2f477-142">如果您沒有復原服務保存庫的 hello 釘選 toohello 儀表板，在 [hello 中樞功能表上的，按一下**更服務**hello] 清單中的資源，在輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="2f477-142">If you don't have hello Recovery Services vault pinned toohello Dashboard, on hello Hub menu, click **More Services** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="2f477-143">當您開始輸入 hello 清單會篩選根據您的輸入。</span><span class="sxs-lookup"><span data-stu-id="2f477-143">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="2f477-144">按一下 [復原服務保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="2f477-144">Click **Recovery Services vaults**.</span></span>

   ![建立復原服務保存庫的步驟 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   <span data-ttu-id="2f477-146">復原服務保存庫的 hello 清單隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="2f477-146">hello list of Recovery Services vaults is displayed.</span></span> <span data-ttu-id="2f477-147">從 hello 清單中，選取您想要 toodelete hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-147">From hello list, select hello vault you want toodelete.</span></span>

   ![從清單中選擇保存庫](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. <span data-ttu-id="2f477-149">在 [hello 保存庫] 檢視中，查看在 hello **Essentials**窗格。</span><span class="sxs-lookup"><span data-stu-id="2f477-149">In hello vault view, look at hello **Essentials** pane.</span></span> <span data-ttu-id="2f477-150">toodelete 保存庫中，不能有任何受保護的項目。</span><span class="sxs-lookup"><span data-stu-id="2f477-150">toodelete a vault, there cannot be any protected items.</span></span> <span data-ttu-id="2f477-151">如果您看到的數字非零，之下**備份項目**或**備份管理伺服器**，才能刪除 hello 保存庫，您必須移除這些項目。</span><span class="sxs-lookup"><span data-stu-id="2f477-151">If you see a number other than zero, under either **Backup Items** or **Backup management servers**, you must remove those items before you can delete hello vault.</span></span>

    ![在基本窗格中查看受保護的項目](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    <span data-ttu-id="2f477-153">Vm 和檔案/資料夾會被視為備份的項目，而且會列在 hello**備份項目**hello Essentials 窗格的區域。</span><span class="sxs-lookup"><span data-stu-id="2f477-153">VMs and Files/Folders are considered Backup Items, and are listed in hello **Backup Items** area of hello Essentials pane.</span></span> <span data-ttu-id="2f477-154">DPM 伺服器會列在 [hello**備份管理伺服器**hello Essentials] 窗格的區域。</span><span class="sxs-lookup"><span data-stu-id="2f477-154">A DPM server is listed in hello **Backup Management Server** area of hello Essentials pane.</span></span> <span data-ttu-id="2f477-155">**複製項目**相關 toohello Azure Site Recovery 服務。</span><span class="sxs-lookup"><span data-stu-id="2f477-155">**Replicated Items** pertain toohello Azure Site Recovery service.</span></span>
3. <span data-ttu-id="2f477-156">從 hello 保存庫中，尋找 hello 保存庫中的 hello 項目移除 hello toobegin 受保護的項目。</span><span class="sxs-lookup"><span data-stu-id="2f477-156">toobegin removing hello protected items from hello vault, find hello items in hello vault.</span></span> <span data-ttu-id="2f477-157">Hello 保存庫儀表板中按一下**設定**，然後按一下**備份項目**tooopen 該刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2f477-157">In hello vault dashboard click **Settings**, and then click **Backup items** tooopen that blade.</span></span>

    ![從清單中選擇保存庫](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    <span data-ttu-id="2f477-159">hello**備份項目**分頁有個別的清單，根據 hello 項目類型： Azure 虛擬機器或檔案資料夾 （請參閱映像）。</span><span class="sxs-lookup"><span data-stu-id="2f477-159">hello **Backup Items** blade has separate lists, based on hello Item Type: Azure Virtual Machines or File-Folders (see image).</span></span> <span data-ttu-id="2f477-160">hello 預設項目類型清單中所示為 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2f477-160">hello default Item Type list shown is Azure Virtual Machines.</span></span> <span data-ttu-id="2f477-161">檔案資料夾中的項目 hello 保存庫中，選取 tooview hello 清單**檔案資料夾**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="2f477-161">tooview hello list of File-Folders items in hello vault, select **File-Folders** from hello drop-down menu.</span></span>
4. <span data-ttu-id="2f477-162">您可以保護 VM 的 hello 保存庫中刪除項目之前，您必須停止 hello 項目的備份工作，並刪除 hello 復原點的資料。</span><span class="sxs-lookup"><span data-stu-id="2f477-162">Before you can delete an item from hello vault protecting a VM, you must stop hello item's backup job and delete hello recovery point data.</span></span> <span data-ttu-id="2f477-163">Hello 保存庫中的每個項目，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2f477-163">For each item in hello vault, follow these steps:</span></span>

    <span data-ttu-id="2f477-164">a.</span><span class="sxs-lookup"><span data-stu-id="2f477-164">a.</span></span> <span data-ttu-id="2f477-165">在 hello**備份項目**刀鋒視窗中，以滑鼠右鍵按一下 hello 項目，並從 hello 內容功能表中，選取**停止備份**。</span><span class="sxs-lookup"><span data-stu-id="2f477-165">On hello **Backup Items** blade, right-click hello item, and from hello context menu, select **Stop backup**.</span></span>

    ![停止 hello 備份工作](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    <span data-ttu-id="2f477-167">hello 停止備份 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2f477-167">hello Stop Backup blade opens.</span></span>

    <span data-ttu-id="2f477-168">b.</span><span class="sxs-lookup"><span data-stu-id="2f477-168">b.</span></span> <span data-ttu-id="2f477-169">在 hello**停止備份**刀鋒視窗中的，從 hello**選擇選項**功能表上，選取**刪除備份資料**> hello 項目的型別 hello 名稱 > 按一下**停止備份**。</span><span class="sxs-lookup"><span data-stu-id="2f477-169">On hello **Stop Backup** blade, from hello **Choose an option** menu, select **Delete Backup Data** > type hello name of hello item > and click **Stop backup**.</span></span>

    <span data-ttu-id="2f477-170">型別 hello 名稱 hello 項目，您想要 toodelete tooverify 它。</span><span class="sxs-lookup"><span data-stu-id="2f477-170">Type hello name of hello item, tooverify you want toodelete it.</span></span> <span data-ttu-id="2f477-171">hello**停止備份**確認 hello 項目之後，就會啟動按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f477-171">hello **Stop Backup** button activates once you verify hello item.</span></span> <span data-ttu-id="2f477-172">如果看不到 hello 對話方塊方塊 tootype hello hello 備份項目名稱，您會選擇 hello**保留備份資料**選項。</span><span class="sxs-lookup"><span data-stu-id="2f477-172">If you do not see hello dialog box tootype hello name of hello backup item, you chose hello **Retain Backup Data** option.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    <span data-ttu-id="2f477-174">（選擇性） 您可以提供的原因為何會刪除 hello 資料，並加入註解。</span><span class="sxs-lookup"><span data-stu-id="2f477-174">Optionally, you can provide a reason why you are deleting hello data, and add comments.</span></span> <span data-ttu-id="2f477-175">按一下 之後**停止備份**，然後再嘗試 toodelete hello 保存庫允許 hello delete 作業 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="2f477-175">After you click **Stop Backup**, allow hello delete job toocomplete before attempting toodelete hello vault.</span></span> <span data-ttu-id="2f477-176">tooverify 的 hello 作業已完成，請檢查 hello Azure 訊息![刪除備份資料](./media/backup-azure-delete-vault/messages.png)。</span><span class="sxs-lookup"><span data-stu-id="2f477-176">tooverify that hello job has completed, check hello Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span></span> <br/>
    <span data-ttu-id="2f477-177">Hello 作業完成之後，您會收到訊息，表示 hello 備份程序已停止且 hello 備份資料，該項目，已刪除。</span><span class="sxs-lookup"><span data-stu-id="2f477-177">Once hello job is complete, you receive a message stating hello backup process was stopped and hello backup data, for that item, was deleted.</span></span>

    <span data-ttu-id="2f477-178">c.</span><span class="sxs-lookup"><span data-stu-id="2f477-178">c.</span></span> <span data-ttu-id="2f477-179">刪除在 hello hello 清單中的項目之後**備份項目**功能表上，按一下 **重新整理**toosee hello 剩餘 hello 保存庫中的項目。</span><span class="sxs-lookup"><span data-stu-id="2f477-179">After deleting an item in hello list, on hello **Backup Items** menu, click **Refresh** toosee hello remaining items in hello vault.</span></span>

      ![刪除備份資料](./media/backup-azure-delete-vault/empty-items-list.png)

      <span data-ttu-id="2f477-181">當 hello 清單中有任何項目時，捲動 toohello **Essentials** hello 備份保存庫刀鋒視窗中的窗格。</span><span class="sxs-lookup"><span data-stu-id="2f477-181">When there are no items in hello list, scroll toohello **Essentials** pane in hello Backup vault blade.</span></span> <span data-ttu-id="2f477-182">清單中不應該有任何 [備份項目]、[備份管理伺服器] 或 [複寫的項目]。</span><span class="sxs-lookup"><span data-stu-id="2f477-182">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span></span> <span data-ttu-id="2f477-183">如果項目仍然顯示 hello 保存庫中，傳回 toostep 三，然後選擇另一個項目型別清單。</span><span class="sxs-lookup"><span data-stu-id="2f477-183">If items still appear in hello vault, return toostep three and choose a different item type list.</span></span>  
5. <span data-ttu-id="2f477-184">當 hello 保存庫工具列中沒有項目，請按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-184">When there are no more items in hello vault toolbar, click **Delete**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-vault.png)
6. <span data-ttu-id="2f477-186">按一下您想 toodelete hello 保存庫，tooverify**是**。</span><span class="sxs-lookup"><span data-stu-id="2f477-186">tooverify that you want toodelete hello vault, click **Yes**.</span></span>

    <span data-ttu-id="2f477-187">就 hello 保存庫刪除並 hello 入口網站傳回 toohello**新增**服務功能表。</span><span class="sxs-lookup"><span data-stu-id="2f477-187">hello vault is deleted and hello portal returns toohello **New** service menu.</span></span>

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a><span data-ttu-id="2f477-188">如果停止 hello 備份程序，而保留的 hello 資料，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="2f477-188">What if I stopped hello backup process but retained hello data?</span></span>
<span data-ttu-id="2f477-189">如果您停止 hello 備份程序，但是不小心*保留*hello 資料，您必須刪除 hello 備份資料，才能刪除 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-189">If you stopped hello backup process but accidentally *retained* hello data, you must delete hello backup data before you can delete hello vault.</span></span> <span data-ttu-id="2f477-190">toodelete hello 備份資料：</span><span class="sxs-lookup"><span data-stu-id="2f477-190">toodelete hello backup data:</span></span>

1. <span data-ttu-id="2f477-191">在 hello**備份項目**刀鋒視窗中，以滑鼠右鍵按一下 hello 項目，並且 hello 操作功能表上按一下**刪除備份資料**。</span><span class="sxs-lookup"><span data-stu-id="2f477-191">On hello **Backup Items** blade, right-click hello item, and on hello context menu click **Delete backup data**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    <span data-ttu-id="2f477-193">hello**刪除備份資料**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2f477-193">hello **Delete Backup Data** blade opens.</span></span>
2. <span data-ttu-id="2f477-194">在 hello**刪除備份資料**刀鋒視窗中，輸入 hello 名稱 hello 項目，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-194">On hello **Delete Backup Data** blade, type hello name of hello item, and click **Delete**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-retained-vault.png)

    <span data-ttu-id="2f477-196">一旦您已刪除 hello 資料，傳回 toostep 4c 並繼續執行 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="2f477-196">Once you have deleted hello data, return toostep 4c and continue with hello process.</span></span>

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a><span data-ttu-id="2f477-197">刪除保存庫使用 tooprotect DPM 伺服器</span><span class="sxs-lookup"><span data-stu-id="2f477-197">Delete a vault used tooprotect a DPM server</span></span>
<span data-ttu-id="2f477-198">您可以刪除保存庫使用 tooprotect DPM 伺服器之前，您必須清除任何已建立的復原點，然後取消註冊 hello hello 保存庫中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="2f477-198">Before you can delete a vault used tooprotect a DPM server, you must clear any recovery points that have been created, and then unregister hello server from hello vault.</span></span>

<span data-ttu-id="2f477-199">保護群組相關聯的 toodelete hello 資料：</span><span class="sxs-lookup"><span data-stu-id="2f477-199">toodelete hello data associated with a protection group:</span></span>

1. <span data-ttu-id="2f477-200">在 hello DPM 系統管理員主控台中，按一下 **保護**> 選取保護群組 > 選取 hello 保護群組成員 > 在 hello 工具功能區中，按一下**移除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-200">In hello DPM Administrator Console, click **Protection** > select a protection group > select hello Protection Group Member > and in hello tool ribbon, click **Remove**.</span></span>

  <span data-ttu-id="2f477-201">選取 hello 保護群組成員 tooactivate hello**移除**hello 工具功能區中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f477-201">Select hello Protection Group Member tooactivate hello **Remove** button in hello tool ribbon.</span></span> <span data-ttu-id="2f477-202">Hello 成員是在 hello 範例**dummyvm9**。</span><span class="sxs-lookup"><span data-stu-id="2f477-202">In hello example, hello member is **dummyvm9**.</span></span> <span data-ttu-id="2f477-203">tooselect hello 保護群組中的多個成員按住 hello Ctrl 鍵同時按一下 hello 成員上。</span><span class="sxs-lookup"><span data-stu-id="2f477-203">tooselect multiple members in hello protection group, hold down hello Ctrl key while clicking on hello members.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    <span data-ttu-id="2f477-205">hello**停止保護** 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2f477-205">hello **Stop Protection** dialog opens.</span></span>
2. <span data-ttu-id="2f477-206">在 hello**停止保護**對話方塊中，選取**刪除受保護的資料**，然後按一下**停止保護**。</span><span class="sxs-lookup"><span data-stu-id="2f477-206">In hello **Stop Protection** dialog, select **Delete protected data**, and click **Stop Protection**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    <span data-ttu-id="2f477-208">toodelete 保存庫，您必須清除，或刪除，hello 保存庫的受保護的資料。</span><span class="sxs-lookup"><span data-stu-id="2f477-208">toodelete a vault, you must clear, or delete, hello vault of protected data.</span></span> <span data-ttu-id="2f477-209">根據 hello 復原點數目以及 hello 保護群組中的資料，它可能需要幾秒 tooseveral 分鐘 toodelete hello 資料。</span><span class="sxs-lookup"><span data-stu-id="2f477-209">Depending on hello number of recovery points and data in hello protection group, it may take anywhere from a few seconds tooseveral minutes toodelete hello data.</span></span> <span data-ttu-id="2f477-210">hello**停止保護**hello 作業完成時，對話方塊會顯示 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="2f477-210">hello **Stop Protection** dialog shows hello status when hello job has completed.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. <span data-ttu-id="2f477-212">對所有保護群組中的所有成員執行此程序。</span><span class="sxs-lookup"><span data-stu-id="2f477-212">Continue this process for all members in all protection groups.</span></span>

    <span data-ttu-id="2f477-213">移除所有受保護的資料與保護群組。</span><span class="sxs-lookup"><span data-stu-id="2f477-213">Remove all protected data and protection groups.</span></span>
4. <span data-ttu-id="2f477-214">刪除所有成員從 hello 保護群組之後, 切換 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2f477-214">After deleting all members from hello protection group, switch toohello Azure portal.</span></span> <span data-ttu-id="2f477-215">開啟 hello 保存庫儀表板，並確定沒有任何**備份項目**，**備份管理伺服器**，或**複寫項目**。</span><span class="sxs-lookup"><span data-stu-id="2f477-215">Open hello vault dashboard, and make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="2f477-216">Hello 保存庫在工具列上，按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-216">On hello vault toolbar, click **Delete**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-vault.png)

    <span data-ttu-id="2f477-218">如果沒有備份管理伺服器登錄 toohello 保存庫，您無法刪除 hello 保存庫，即使在 hello 保存庫中沒有資料。</span><span class="sxs-lookup"><span data-stu-id="2f477-218">If there are Backup management servers registered toohello vault, you can't delete hello vault even if there is no data in hello vault.</span></span> <span data-ttu-id="2f477-219">如果您刪除 hello 與 hello 保存庫相關聯的備份管理伺服器，但沒有所列的 hello 伺服器**Essentials**  窗格中，請參閱[尋找 hello 備份管理伺服器已註冊的 toohello 保存庫](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault).</span><span class="sxs-lookup"><span data-stu-id="2f477-219">If you deleted hello Backup management servers associated with hello vault, but there are servers listed in hello **Essentials** pane, see [Find hello Backup management servers registered toohello vault](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault).</span></span>
5. <span data-ttu-id="2f477-220">按一下您想 toodelete hello 保存庫，tooverify**是**。</span><span class="sxs-lookup"><span data-stu-id="2f477-220">tooverify that you want toodelete hello vault, click **Yes**.</span></span>

    <span data-ttu-id="2f477-221">就 hello 保存庫刪除並 hello 入口網站傳回 toohello**新增**服務功能表。</span><span class="sxs-lookup"><span data-stu-id="2f477-221">hello vault is deleted and hello portal returns toohello **New** service menu.</span></span>

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a><span data-ttu-id="2f477-222">刪除保存庫使用 tooprotect 實際執行伺服器</span><span class="sxs-lookup"><span data-stu-id="2f477-222">Delete a vault used tooprotect a Production server</span></span>
<span data-ttu-id="2f477-223">您可以刪除保存庫使用 tooprotect 實際執行伺服器之前，您必須先刪除或 hello 保存庫中的 hello 伺服器取消登錄。</span><span class="sxs-lookup"><span data-stu-id="2f477-223">Before you can delete a vault used tooprotect a Production server, you must delete or unregister hello server from hello vault.</span></span>

<span data-ttu-id="2f477-224">toodelete hello 的實際執行伺服器 hello 保存庫相關聯：</span><span class="sxs-lookup"><span data-stu-id="2f477-224">toodelete hello Production server associated with hello vault:</span></span>

1. <span data-ttu-id="2f477-225">在 hello Azure 入口網站，開啟 hello 保存庫儀表板，然後按一下**設定** > **備份基礎結構** > **實際執行伺服器**。</span><span class="sxs-lookup"><span data-stu-id="2f477-225">In hello Azure portal, open hello vault dashboard and click **Settings** > **Backup Infrastructure** > **Production Servers**.</span></span>

    ![開啟生產伺服器刀鋒視窗](./media/backup-azure-delete-vault/delete-production-server.png)

    <span data-ttu-id="2f477-227">hello**實際執行伺服器**刀鋒視窗會開啟，並列出所有的實際執行伺服器 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="2f477-227">hello **Production Servers** blade opens and lists all Production servers in hello vault.</span></span>

    ![生產伺服器的清單](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. <span data-ttu-id="2f477-229">在 hello**實際執行伺服器**刀鋒視窗中，以滑鼠右鍵按一下 hello 伺服器上，按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-229">On hello **Production Servers** blade, right-click on hello server, and click **Delete**.</span></span>

    ![<span data-ttu-id="2f477-230">刪除生產伺服器</span><span class="sxs-lookup"><span data-stu-id="2f477-230">delete production server</span></span> ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    <span data-ttu-id="2f477-231">hello**刪除**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2f477-231">hello **Delete** blade opens.</span></span>

    ![<span data-ttu-id="2f477-232">刪除生產伺服器</span><span class="sxs-lookup"><span data-stu-id="2f477-232">delete production server</span></span> ](./media/backup-azure-delete-vault/delete-blade.png)
3. <span data-ttu-id="2f477-233">在 hello**刪除**刀鋒視窗中，確認 hello 伺服器名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-233">On hello **Delete** blade, confirm hello server name, and click **Delete**.</span></span> <span data-ttu-id="2f477-234">您必須正確命名 hello server，tooactivate hello**刪除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f477-234">You must correctly name hello server, tooactivate hello **Delete** button.</span></span>

    <span data-ttu-id="2f477-235">一旦刪除 hello 保存庫時，您會收到訊息，指出已刪除 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-235">Once hello vault is deleted, you receive a message stating hello vault has been deleted.</span></span> <span data-ttu-id="2f477-236">刪除 hello 保存庫中的所有伺服器之後, 捲動後 toohello Essentials 窗格 hello 保存庫儀表板中。</span><span class="sxs-lookup"><span data-stu-id="2f477-236">After deleting all servers in hello vault, scroll back toohello Essentials pane in hello vault dashboard.</span></span>
4. <span data-ttu-id="2f477-237">在 hello 保存庫儀表板，請確認沒有任何**備份項目**，**備份管理伺服器**，或**複寫項目**。</span><span class="sxs-lookup"><span data-stu-id="2f477-237">In hello vault dashboard, make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="2f477-238">Hello 保存庫在工具列上，按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-238">On hello vault toolbar, click **Delete**.</span></span>
5. <span data-ttu-id="2f477-239">按一下您想 toodelete hello 保存庫，tooverify**是**。</span><span class="sxs-lookup"><span data-stu-id="2f477-239">tooverify that you want toodelete hello vault, click **Yes**.</span></span>

    <span data-ttu-id="2f477-240">就 hello 保存庫刪除並 hello 入口網站傳回 toohello**新增**服務功能表。</span><span class="sxs-lookup"><span data-stu-id="2f477-240">hello vault is deleted and hello portal returns toohello **New** service menu.</span></span>

## <a name="delete-a-backup-vault-in-classic-portal"></a><span data-ttu-id="2f477-241">刪除傳統入口網站中的備份保存庫</span><span class="sxs-lookup"><span data-stu-id="2f477-241">Delete a backup vault in classic portal</span></span>
<span data-ttu-id="2f477-242">hello 以下指示會刪除備份保存庫 hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="2f477-242">hello following instructions are for deleting a Backup vault in hello classic portal.</span></span> <span data-ttu-id="2f477-243">您可以刪除 hello 備份保存庫之前，您必須刪除 hello 的復原點，或備份的項目，然後移除 hello 註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="2f477-243">Before you can delete hello Backup vault, you must delete hello recovery points, or backed up items, and remove hello registered servers.</span></span> <span data-ttu-id="2f477-244">hello 已註冊的伺服器為 hello Windows 伺服器、 工作站上或已註冊的 toohello 保存庫的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2f477-244">hello registered servers are hello Windows Server, workstation, or virtual machines that were registered toohello vault.</span></span>

1. <span data-ttu-id="2f477-245">開啟 hello[傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="2f477-245">Open hello [Classic portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="2f477-246">從 hello 清單中的備份保存庫，選取您想要 toodelete hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-246">From hello list of backup vaults, select hello vault you want toodelete.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    <span data-ttu-id="2f477-248">hello 保存庫儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2f477-248">hello vault dashboard opens.</span></span> <span data-ttu-id="2f477-249">查看 hello 與 hello 保存庫相關聯的 Windows 伺服器及/或 Azure 的虛擬機器的數目。</span><span class="sxs-lookup"><span data-stu-id="2f477-249">Look at hello number of Windows Servers and/or Azure virtual machines associated with hello vault.</span></span> <span data-ttu-id="2f477-250">此外，看看 hello Azure 中已使用的總儲存體。</span><span class="sxs-lookup"><span data-stu-id="2f477-250">Also, look at hello total storage consumed in Azure.</span></span> <span data-ttu-id="2f477-251">停止所有的備份工作，並刪除所有資料，然後再刪除 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-251">Stop all backup jobs and delete all data before deleting hello vault.</span></span>

3. <span data-ttu-id="2f477-252">按一下 hello**受保護項目**索引標籤，然後再按一下**停止保護**</span><span class="sxs-lookup"><span data-stu-id="2f477-252">Click hello **Protected Items** tab, and then click **Stop Protection**</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    <span data-ttu-id="2f477-254">hello**停止保護 '您的保存庫'**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="2f477-254">hello **Stop protection of 'your vault'** dialog appears.</span></span>
4. <span data-ttu-id="2f477-255">在 hello**停止保護 '您的保存庫'**  對話方塊中，核取**刪除相關聯的備份資料**按一下![核取記號](./media/backup-azure-delete-vault/checkmark.png)。</span><span class="sxs-lookup"><span data-stu-id="2f477-255">In hello **Stop protection of 'your vault'** dialog, check **Delete associated backup data** and click ![checkmark](./media/backup-azure-delete-vault/checkmark.png).</span></span> <br/>
    <span data-ttu-id="2f477-256">或者，您可以選擇停止保護的原因，並提供註解。</span><span class="sxs-lookup"><span data-stu-id="2f477-256">Optionally, you can choose a reason for stopping protection, and provide a comment.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    <span data-ttu-id="2f477-258">在刪除之後 hello hello 保存庫中的項目，hello 保存庫是空的。</span><span class="sxs-lookup"><span data-stu-id="2f477-258">After deleting hello items in hello vault, hello vault will be empty.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. <span data-ttu-id="2f477-260">在 hello 索引標籤的清單中，按一下 **註冊的項目**。</span><span class="sxs-lookup"><span data-stu-id="2f477-260">In hello list of tabs, click **Registered Items**.</span></span> <span data-ttu-id="2f477-261">hello**類型**下拉式選單，可讓您 toochoose hello 類型的已註冊的伺服器 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-261">hello **Type** drop-down menu, enables you toochoose hello type of server registered toohello vault.</span></span> <span data-ttu-id="2f477-262">hello 類型可以是 Windows Server 或 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2f477-262">hello type can be Windows Server or Azure Virtual Machine.</span></span> <span data-ttu-id="2f477-263">在下列範例的 hello，選取 hello 虛擬機器已註冊的 toohello 保存庫，然後按一下**取消註冊**。</span><span class="sxs-lookup"><span data-stu-id="2f477-263">In hello following example, select hello virtual machine registered toohello vault, and click **Unregister**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  <span data-ttu-id="2f477-265">如果您想 toodelete hello 註冊的 Windows 伺服器，從 hello**類型**下拉式選單中，選取**Windows Server**，按一下 ![核取記號](./media/backup-azure-delete-vault/checkmark.png)toorefresh 囉 」 畫面，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-265">If you want toodelete hello registration for a Windows Server, from hello **Type** drop-down menu, select **Windows Server**, click ![checkmark](./media/backup-azure-delete-vault/checkmark.png) toorefresh hello screen, and then click **Delete**.</span></span> <br/>

  ![選取 Windows Server](./media/backup-azure-delete-vault/select-windows-server.png)

6. <span data-ttu-id="2f477-267">在 hello 索引標籤的清單中，按一下 **儀表板**tooopen 的索引標籤。請確認沒有任何已註冊的伺服器或 Azure hello 雲端中受保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2f477-267">In hello list of tabs, click **Dashboard** tooopen that tab. Verify there are no registered servers or Azure virtual machines protected in hello cloud.</span></span> <span data-ttu-id="2f477-268">此外，也確認儲存體中沒有資料。</span><span class="sxs-lookup"><span data-stu-id="2f477-268">Also, verify there is no data in storage.</span></span> <span data-ttu-id="2f477-269">按一下**刪除**toodelete hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f477-269">Click **Delete** toodelete hello vault.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    <span data-ttu-id="2f477-271">hello 刪除備份保存庫確認畫面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2f477-271">hello Delete Backup vault confirmation screen opens.</span></span> <span data-ttu-id="2f477-272">選取的選項為何，您要刪除 hello 保存庫，然後按一下</span><span class="sxs-lookup"><span data-stu-id="2f477-272">Select an option why you're deleting hello vault, and click</span></span> ![勾選記號](./media/backup-azure-delete-vault/checkmark.png)<span data-ttu-id="2f477-274">。</span><span class="sxs-lookup"><span data-stu-id="2f477-274">.</span></span> <br/>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    <span data-ttu-id="2f477-276">就 hello 保存庫刪除，並傳回 toohello 傳統的入口網站儀表板。</span><span class="sxs-lookup"><span data-stu-id="2f477-276">hello vault is deleted, and you return toohello classic portal dashboard.</span></span>

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a><span data-ttu-id="2f477-277">尋找 hello 備份管理伺服器已註冊的 toohello 保存庫</span><span class="sxs-lookup"><span data-stu-id="2f477-277">Find hello Backup Management servers registered toohello vault</span></span>
<span data-ttu-id="2f477-278">如果您有多個已註冊的伺服器 tooa 保存庫時，可能很難 tooremember 它們。</span><span class="sxs-lookup"><span data-stu-id="2f477-278">If you have multiple servers registered tooa vault, it can be difficult tooremember them.</span></span> <span data-ttu-id="2f477-279">toosee hello 伺服器註冊 toohello 保存庫，並加以刪除：</span><span class="sxs-lookup"><span data-stu-id="2f477-279">toosee hello servers registered toohello vault, and delete them:</span></span>

1. <span data-ttu-id="2f477-280">開啟 hello 保存庫儀表板。</span><span class="sxs-lookup"><span data-stu-id="2f477-280">Open hello vault dashboard.</span></span>
2. <span data-ttu-id="2f477-281">在 hello **Essentials**  窗格中，按一下 **設定**tooopen 該刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2f477-281">In hello **Essentials** pane, click **Settings** tooopen that blade.</span></span>

    ![開啟設定刀鋒視窗](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. <span data-ttu-id="2f477-283">在 hello**設定 刀鋒視窗**，按一下 **備份基礎結構**。</span><span class="sxs-lookup"><span data-stu-id="2f477-283">On hello **Settings blade**, click **Backup Infrastructure**.</span></span>
4. <span data-ttu-id="2f477-284">在 hello**備份基礎結構**刀鋒視窗中，按一下 **備份管理伺服器**。</span><span class="sxs-lookup"><span data-stu-id="2f477-284">On hello **Backup Infrastructure** blade, click **Backup Management Servers**.</span></span> <span data-ttu-id="2f477-285">hello 備份管理伺服器刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2f477-285">hello Backup Management Servers blade opens.</span></span>

    ![備份管理伺服器的清單](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. <span data-ttu-id="2f477-287">toodelete hello 清單中，從伺服器 hello hello 伺服器名稱上按一下滑鼠右鍵，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="2f477-287">toodelete a server from hello list, right-click hello name of hello server and then click **Delete**.</span></span>
    <span data-ttu-id="2f477-288">hello**刪除**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2f477-288">hello **Delete** blade opens.</span></span>
6. <span data-ttu-id="2f477-289">在 hello**刪除**刀鋒視窗中，提供 hello hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="2f477-289">On hello **Delete** blade, provide hello name of hello server.</span></span> <span data-ttu-id="2f477-290">如果是完整名稱，您可以複製並貼上 hello 備份管理伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="2f477-290">If it is a long name, you can copy and paste it from hello list of Backup Management Servers.</span></span> <span data-ttu-id="2f477-291">然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="2f477-291">Then click **Delete**.</span></span>  
