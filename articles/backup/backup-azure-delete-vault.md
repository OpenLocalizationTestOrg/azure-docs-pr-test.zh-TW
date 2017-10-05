---
title: " 刪除 Azure 中的復原服務保存庫 | Microsoft Docs "
description: "如何刪除 Azure 備份與復原服務保存庫。 備份保存庫可稱為 Azure 雲端保存庫，或 Azure 復原保存庫。 當您無法在傳統入口網站或 Azure 入口網站中刪除備份保存庫時，請針對問題進行疑難排解。"
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
ms.openlocfilehash: ae4a73d12898c62fe2c5cf3683bc7c1c8c845fdf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-recovery-services-vault"></a><span data-ttu-id="96241-105">刪除復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="96241-105">Delete a Recovery Services vault</span></span>
<span data-ttu-id="96241-106">Azure 備份服務有兩種類型的保存庫：備份保存庫和復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-106">The Azure Backup service has two types of vaults - the Backup vault and the Recovery Services vault.</span></span> <span data-ttu-id="96241-107">先是備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-107">The Backup vault came first.</span></span> <span data-ttu-id="96241-108">然後是復原服務保存庫，以支援擴充的 Resource Manager 部署。</span><span class="sxs-lookup"><span data-stu-id="96241-108">Then the Recovery Services vault came along to support the expanded Resource Manager deployments.</span></span> <span data-ttu-id="96241-109">由於擴充的功能和資訊相依性必須儲存在保存庫中，刪除備份或復原服務保存庫可能會造成混淆。</span><span class="sxs-lookup"><span data-stu-id="96241-109">Because of the expanded capabilities and the information dependencies that must be stored in the vault, deleting a Backup or Recovery Services vault can be confusing.</span></span> <span data-ttu-id="96241-110">此文章說明如何在傳統入口網站和 Azure 入口網站中刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-110">This article explains how to delete the vaults in the classic portal and the Azure portal.</span></span>  

| <span data-ttu-id="96241-111">**部署類型**</span><span class="sxs-lookup"><span data-stu-id="96241-111">**Deployment Type**</span></span> | <span data-ttu-id="96241-112">**入口網站**</span><span class="sxs-lookup"><span data-stu-id="96241-112">**Portal**</span></span> | <span data-ttu-id="96241-113">**保存庫名稱**</span><span class="sxs-lookup"><span data-stu-id="96241-113">**Vault name**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96241-114">傳統</span><span class="sxs-lookup"><span data-stu-id="96241-114">Classic</span></span> |<span data-ttu-id="96241-115">傳統</span><span class="sxs-lookup"><span data-stu-id="96241-115">Classic</span></span> |<span data-ttu-id="96241-116">備份保存庫</span><span class="sxs-lookup"><span data-stu-id="96241-116">Backup vault</span></span> |
| <span data-ttu-id="96241-117">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96241-117">Resource Manager</span></span> |<span data-ttu-id="96241-118">Azure</span><span class="sxs-lookup"><span data-stu-id="96241-118">Azure</span></span> |<span data-ttu-id="96241-119">復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="96241-119">Recovery Services vault</span></span> |

> [!NOTE]
> <span data-ttu-id="96241-120">備份保存庫無法保護 Resource Manager 部署的解決方案。</span><span class="sxs-lookup"><span data-stu-id="96241-120">Backup vaults cannot protect Resource Manager-deployed solutions.</span></span> <span data-ttu-id="96241-121">不過，您可以使用復原服務保存庫來保護傳統方式部署的伺服器和 VM。</span><span class="sxs-lookup"><span data-stu-id="96241-121">However, you can use a Recovery Services vault to protect classically deployed servers and VMs.</span></span>  
>

> [!IMPORTANT]
> <span data-ttu-id="96241-122">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-122">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="96241-123">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="96241-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="96241-124">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="96241-125">在 **2017 年 10 月 15 日**之後，您就無法使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-125">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="96241-126">**自 2017 年 11 月 1 日起**：</span><span class="sxs-lookup"><span data-stu-id="96241-126">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="96241-127">任何其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-127">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="96241-128">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="96241-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="96241-129">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="96241-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="96241-130">本文中使用「保存庫」一詞來泛指備份保存庫或復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-130">In this article, we use the term, vault, to refer to the generic form of the Backup vault or Recovery Services vault.</span></span> <span data-ttu-id="96241-131">需要區別保存庫時，則使用正式名稱「備份保存庫」或「復原服務保存庫」。</span><span class="sxs-lookup"><span data-stu-id="96241-131">We use the formal name, Backup vault, or Recovery Services vault, when it is necessary to distinguish between the vaults.</span></span>

## <a name="deleting-a-recovery-services-vault"></a><span data-ttu-id="96241-132">刪除復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="96241-132">Deleting a Recovery Services vault</span></span>
<span data-ttu-id="96241-133">刪除復原服務保存庫是單一步驟的程序 - 前提是保存庫不包含任何資源 。</span><span class="sxs-lookup"><span data-stu-id="96241-133">Deleting a Recovery Services vault is a one-step process - *provided the vault doesn't contain any resources*.</span></span> <span data-ttu-id="96241-134">您必須先移除或刪除復原服務保存庫中的所有資源，才可以刪除復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-134">Before you can delete a Recovery Services vault, you must remove or delete all resources in the vault.</span></span> <span data-ttu-id="96241-135">如果您嘗試刪除包含資源的保存庫，會收到類似下圖的錯誤：</span><span class="sxs-lookup"><span data-stu-id="96241-135">If you attempt to delete a vault that contains resources, you get an error like the following image:</span></span>

![保存庫刪除錯誤](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

<span data-ttu-id="96241-137">按 [重試]  會再產生相同的錯誤，直到您清除保存庫中的資源為止。</span><span class="sxs-lookup"><span data-stu-id="96241-137">Until you have cleared the resources from the vault, clicking **Retry** produces the same error.</span></span> <span data-ttu-id="96241-138">如果您被卡在這則錯誤訊息，請按一下 [取消]，並使用下列步驟刪除保存庫中的資源。</span><span class="sxs-lookup"><span data-stu-id="96241-138">If you're stuck on this error message, click **Cancel** and use the following steps to delete the resources in the vault.</span></span>

### <a name="removing-the-items-from-a-vault-protecting-a-vm"></a><span data-ttu-id="96241-139">移除保護 VM 之保存庫中的項目</span><span class="sxs-lookup"><span data-stu-id="96241-139">Removing the items from a vault protecting a VM</span></span>
<span data-ttu-id="96241-140">如果您已開啟復原服務保存庫，請跳至第 2 步驟。</span><span class="sxs-lookup"><span data-stu-id="96241-140">If you already have the Recovery Services vault open, skip to the second step.</span></span>

1. <span data-ttu-id="96241-141">開啟 Azure 入口網站，從儀表板中開啟您要刪除的保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-141">Open the Azure portal, and from the Dashboard open the vault you want to delete.</span></span>

   <span data-ttu-id="96241-142">如果儀表板中尚未釘選復原服務保存庫，請按一下 [中樞] 功能表上的 [更多服務]，然後在資源清單中輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="96241-142">If you don't have the Recovery Services vault pinned to the Dashboard, on the Hub menu, click **More Services** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="96241-143">當您開始輸入時，清單會根據您輸入的文字進行篩選。</span><span class="sxs-lookup"><span data-stu-id="96241-143">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="96241-144">按一下 [復原服務保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="96241-144">Click **Recovery Services vaults**.</span></span>

   ![建立復原服務保存庫的步驟 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   <span data-ttu-id="96241-146">隨即會顯示 [復原服務保存庫] 清單。</span><span class="sxs-lookup"><span data-stu-id="96241-146">The list of Recovery Services vaults is displayed.</span></span> <span data-ttu-id="96241-147">從清單中，選取您要刪除的保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-147">From the list, select the vault you want to delete.</span></span>

   ![從清單中選擇保存庫](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. <span data-ttu-id="96241-149">在保存庫檢視中，找到 [基本]  窗格。</span><span class="sxs-lookup"><span data-stu-id="96241-149">In the vault view, look at the **Essentials** pane.</span></span> <span data-ttu-id="96241-150">若要刪除保存庫，不能有任何受保護的項目。</span><span class="sxs-lookup"><span data-stu-id="96241-150">To delete a vault, there cannot be any protected items.</span></span> <span data-ttu-id="96241-151">如果您在 [備份項目] 或 [備份管理伺服器] 下看到零以外的數字，必須先移除這些項目，才能刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-151">If you see a number other than zero, under either **Backup Items** or **Backup management servers**, you must remove those items before you can delete the vault.</span></span>

    ![在基本窗格中查看受保護的項目](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    <span data-ttu-id="96241-153">VM 和檔案/資料夾會被視為備份項目，列在 [基本] 窗格的 [備份項目]  區域中。</span><span class="sxs-lookup"><span data-stu-id="96241-153">VMs and Files/Folders are considered Backup Items, and are listed in the **Backup Items** area of the Essentials pane.</span></span> <span data-ttu-id="96241-154">DPM 伺服器會列在 [基本] 窗格的 [備份管理伺服器]  區域中。</span><span class="sxs-lookup"><span data-stu-id="96241-154">A DPM server is listed in the **Backup Management Server** area of the Essentials pane.</span></span> <span data-ttu-id="96241-155"> 屬於 Azure Site Recovery 服務。</span><span class="sxs-lookup"><span data-stu-id="96241-155">**Replicated Items** pertain to the Azure Site Recovery service.</span></span>
3. <span data-ttu-id="96241-156">若要開始從保存庫移除受保護的項目，請在保存庫中找到這些項目。</span><span class="sxs-lookup"><span data-stu-id="96241-156">To begin removing the protected items from the vault, find the items in the vault.</span></span> <span data-ttu-id="96241-157">在保存庫儀表板中，按一下 [設定]，然後按一下 [備份項目] 開啟其刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="96241-157">In the vault dashboard click **Settings**, and then click **Backup items** to open that blade.</span></span>

    ![從清單中選擇保存庫](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    <span data-ttu-id="96241-159">[備份項目]  刀鋒視窗中有不同的清單，取決於項目類型︰Azure 虛擬機器或檔案-資料夾 (請參閱圖片)。</span><span class="sxs-lookup"><span data-stu-id="96241-159">The **Backup Items** blade has separate lists, based on the Item Type: Azure Virtual Machines or File-Folders (see image).</span></span> <span data-ttu-id="96241-160">顯示的預設項目清單類型是 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="96241-160">The default Item Type list shown is Azure Virtual Machines.</span></span> <span data-ttu-id="96241-161">若要檢視保存庫中的檔案資料夾項目清單，請從下拉式選單中選取 [檔案-資料夾]  。</span><span class="sxs-lookup"><span data-stu-id="96241-161">To view the list of File-Folders items in the vault, select **File-Folders** from the drop-down menu.</span></span>
4. <span data-ttu-id="96241-162">您可以從保護 VM 的保存庫中刪除項目之前，必須先停止該項目的備份作業，並刪除復原點資料。</span><span class="sxs-lookup"><span data-stu-id="96241-162">Before you can delete an item from the vault protecting a VM, you must stop the item's backup job and delete the recovery point data.</span></span> <span data-ttu-id="96241-163">針對保存庫中的每個項目，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="96241-163">For each item in the vault, follow these steps:</span></span>

    <span data-ttu-id="96241-164">a.</span><span class="sxs-lookup"><span data-stu-id="96241-164">a.</span></span> <span data-ttu-id="96241-165">在 [備份項目] 刀鋒視窗中，以滑鼠右鍵按一下項目，然後從內容功能表中選取 [停止備份]。</span><span class="sxs-lookup"><span data-stu-id="96241-165">On the **Backup Items** blade, right-click the item, and from the context menu, select **Stop backup**.</span></span>

    ![停止備份作業](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    <span data-ttu-id="96241-167">[停止備份] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="96241-167">The Stop Backup blade opens.</span></span>

    <span data-ttu-id="96241-168">b.</span><span class="sxs-lookup"><span data-stu-id="96241-168">b.</span></span> <span data-ttu-id="96241-169">在 [停止備份] 刀鋒視窗中，從 [選擇選項] 功能表中選取 [刪除備份資料]，輸入項目的名稱，然後按一下 [停止備份]。</span><span class="sxs-lookup"><span data-stu-id="96241-169">On the **Stop Backup** blade, from the **Choose an option** menu, select **Delete Backup Data** > type the name of the item > and click **Stop backup**.</span></span>

    <span data-ttu-id="96241-170">輸入項目的名稱，以確認您想要刪除它。</span><span class="sxs-lookup"><span data-stu-id="96241-170">Type the name of the item, to verify you want to delete it.</span></span> <span data-ttu-id="96241-171">一旦您確認項目之後，[停止備份] 按鈕會生效。</span><span class="sxs-lookup"><span data-stu-id="96241-171">The **Stop Backup** button activates once you verify the item.</span></span> <span data-ttu-id="96241-172">如果看不到可輸入備份項目名稱的對話方塊，表示您選擇了 [保留備份資料] 選項。</span><span class="sxs-lookup"><span data-stu-id="96241-172">If you do not see the dialog box to type the name of the backup item, you chose the **Retain Backup Data** option.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    <span data-ttu-id="96241-174">或者，您可以提供您為什麼要刪除資料的原因，並加入註解。</span><span class="sxs-lookup"><span data-stu-id="96241-174">Optionally, you can provide a reason why you are deleting the data, and add comments.</span></span> <span data-ttu-id="96241-175">按一下 [停止備份] 之後，允許刪除作業完成，然後再嘗試刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-175">After you click **Stop Backup**, allow the delete job to complete before attempting to delete the vault.</span></span> <span data-ttu-id="96241-176">若要確認作業已完成，請檢查 Azure 訊息 ![delete backup data](./media/backup-azure-delete-vault/messages.png)。</span><span class="sxs-lookup"><span data-stu-id="96241-176">To verify that the job has completed, check the Azure Messages ![delete backup data](./media/backup-azure-delete-vault/messages.png).</span></span> <br/>
    <span data-ttu-id="96241-177">作業完成之後，您會看到一則訊息，指出備份流程已停止，且已刪除該項目的備份資料。</span><span class="sxs-lookup"><span data-stu-id="96241-177">Once the job is complete, you receive a message stating the backup process was stopped and the backup data, for that item, was deleted.</span></span>

    <span data-ttu-id="96241-178">c.</span><span class="sxs-lookup"><span data-stu-id="96241-178">c.</span></span> <span data-ttu-id="96241-179">刪除清單中的項目後，在 [備份項目] 功能表上按一下 [重新整理]，以查看保存庫中的其餘項目。</span><span class="sxs-lookup"><span data-stu-id="96241-179">After deleting an item in the list, on the **Backup Items** menu, click **Refresh** to see the remaining items in the vault.</span></span>

      ![刪除備份資料](./media/backup-azure-delete-vault/empty-items-list.png)

      <span data-ttu-id="96241-181">當清單中沒有任何項目時，捲動到備份保存庫刀鋒視窗的 [基本]  窗格。</span><span class="sxs-lookup"><span data-stu-id="96241-181">When there are no items in the list, scroll to the **Essentials** pane in the Backup vault blade.</span></span> <span data-ttu-id="96241-182">清單中不應該有任何 [備份項目]、[備份管理伺服器] 或 [複寫的項目]。</span><span class="sxs-lookup"><span data-stu-id="96241-182">There shouldn't be any **Backup items**, **Backup management servers**, or **Replicated items** listed.</span></span> <span data-ttu-id="96241-183">如果保存庫中仍有項目，請返回步驟三，並選擇其他項目類型清單。</span><span class="sxs-lookup"><span data-stu-id="96241-183">If items still appear in the vault, return to step three and choose a different item type list.</span></span>  
5. <span data-ttu-id="96241-184">當保存庫工具列中沒有其他項目，按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="96241-184">When there are no more items in the vault toolbar, click **Delete**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-vault.png)
6. <span data-ttu-id="96241-186">若要確認您想要刪除保存庫，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="96241-186">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="96241-187">保存庫便會被刪除，入口網站會回到 [新增]  服務功能表。</span><span class="sxs-lookup"><span data-stu-id="96241-187">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="what-if-i-stopped-the-backup-process-but-retained-the-data"></a><span data-ttu-id="96241-188">如果我停止備份程序但卻保留了資料，會怎麼樣？</span><span class="sxs-lookup"><span data-stu-id="96241-188">What if I stopped the backup process but retained the data?</span></span>
<span data-ttu-id="96241-189">如果您停止備份程序，但是不小心「保留」  資料，您必須先刪除備份資料，才能刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-189">If you stopped the backup process but accidentally *retained* the data, you must delete the backup data before you can delete the vault.</span></span> <span data-ttu-id="96241-190">刪除備份資料：</span><span class="sxs-lookup"><span data-stu-id="96241-190">To delete the backup data:</span></span>

1. <span data-ttu-id="96241-191">在 [備份項目] 刀鋒視窗中，以滑鼠右鍵按一下項目，然後在內容功能表中按一下 [刪除備份資料]。</span><span class="sxs-lookup"><span data-stu-id="96241-191">On the **Backup Items** blade, right-click the item, and on the context menu click **Delete backup data**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    <span data-ttu-id="96241-193">[刪除備份資料]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="96241-193">The **Delete Backup Data** blade opens.</span></span>
2. <span data-ttu-id="96241-194">在 [刪除備份資料] 刀鋒視窗中，輸入項目的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="96241-194">On the **Delete Backup Data** blade, type the name of the item, and click **Delete**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-retained-vault.png)

    <span data-ttu-id="96241-196">刪除資料之後，請返回步驟 4c，並繼續進行程序。</span><span class="sxs-lookup"><span data-stu-id="96241-196">Once you have deleted the data, return to step 4c and continue with the process.</span></span>

## <a name="delete-a-vault-used-to-protect-a-dpm-server"></a><span data-ttu-id="96241-197">刪除用來保護 DPM 伺服器的保存庫</span><span class="sxs-lookup"><span data-stu-id="96241-197">Delete a vault used to protect a DPM server</span></span>
<span data-ttu-id="96241-198">在刪除用來保護 DPM 伺服器的保存庫之前，您必須先清除所有已建立的復原點，然後從保存庫取消註冊該伺服器。</span><span class="sxs-lookup"><span data-stu-id="96241-198">Before you can delete a vault used to protect a DPM server, you must clear any recovery points that have been created, and then unregister the server from the vault.</span></span>

<span data-ttu-id="96241-199">刪除與保護群組相關聯的資料︰</span><span class="sxs-lookup"><span data-stu-id="96241-199">To delete the data associated with a protection group:</span></span>

1. <span data-ttu-id="96241-200">在 DPM 管理主控台中，按一下 [保護] > 選取保護群組 > 選取 [保護群組成員]，然後按一下工具功能區中的 [移除]。</span><span class="sxs-lookup"><span data-stu-id="96241-200">In the DPM Administrator Console, click **Protection** > select a protection group > select the Protection Group Member > and in the tool ribbon, click **Remove**.</span></span>

  <span data-ttu-id="96241-201">選取 [保護群組成員]，以啟用工具功能區中的 [移除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="96241-201">Select the Protection Group Member to activate the **Remove** button in the tool ribbon.</span></span> <span data-ttu-id="96241-202">在範例中，成員是 **dummyvm9**。</span><span class="sxs-lookup"><span data-stu-id="96241-202">In the example, the member is **dummyvm9**.</span></span> <span data-ttu-id="96241-203">若要選取保護群組中的多個成員，請按住 Ctrl 鍵並在成員上按一下。</span><span class="sxs-lookup"><span data-stu-id="96241-203">To select multiple members in the protection group, hold down the Ctrl key while clicking on the members.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    <span data-ttu-id="96241-205">[停止保護]  對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="96241-205">The **Stop Protection** dialog opens.</span></span>
2. <span data-ttu-id="96241-206">在 [停止保護] 對話方塊中，選取 [刪除受保護的資料]，然後按一下 [停止保護]。</span><span class="sxs-lookup"><span data-stu-id="96241-206">In the **Stop Protection** dialog, select **Delete protected data**, and click **Stop Protection**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    <span data-ttu-id="96241-208">若要刪除保存庫，您必須清除 (或刪除) 受保護資料的保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-208">To delete a vault, you must clear, or delete, the vault of protected data.</span></span> <span data-ttu-id="96241-209">刪除資料可能需要幾秒鐘至幾分鐘的時間，依保護群組中的復原點和資料數目而定。</span><span class="sxs-lookup"><span data-stu-id="96241-209">Depending on the number of recovery points and data in the protection group, it may take anywhere from a few seconds to several minutes to delete the data.</span></span> <span data-ttu-id="96241-210">作業完成時 [停止保護]  對話方塊會顯示狀態。</span><span class="sxs-lookup"><span data-stu-id="96241-210">The **Stop Protection** dialog shows the status when the job has completed.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. <span data-ttu-id="96241-212">對所有保護群組中的所有成員執行此程序。</span><span class="sxs-lookup"><span data-stu-id="96241-212">Continue this process for all members in all protection groups.</span></span>

    <span data-ttu-id="96241-213">移除所有受保護的資料與保護群組。</span><span class="sxs-lookup"><span data-stu-id="96241-213">Remove all protected data and protection groups.</span></span>
4. <span data-ttu-id="96241-214">刪除保護群組中的所有成員後，移至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="96241-214">After deleting all members from the protection group, switch to the Azure portal.</span></span> <span data-ttu-id="96241-215">開啟保存庫儀表板，確認已沒有任何 [備份項目]、[備份管理伺服器] 或 [複寫的項目]。</span><span class="sxs-lookup"><span data-stu-id="96241-215">Open the vault dashboard, and make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="96241-216">在保存庫工具列上，按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="96241-216">On the vault toolbar, click **Delete**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-vault.png)

    <span data-ttu-id="96241-218">如果有備份管理伺服器註冊到保存庫，您將無法刪除該保存庫，即使保存庫中沒有資料也一樣。</span><span class="sxs-lookup"><span data-stu-id="96241-218">If there are Backup management servers registered to the vault, you can't delete the vault even if there is no data in the vault.</span></span> <span data-ttu-id="96241-219">如果您已經刪除與保存庫相關聯的備份管理伺服器，但 [基本] 窗格中仍列出伺服器，請參閱[尋找註冊到保存庫的備份管理伺服器](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault)。</span><span class="sxs-lookup"><span data-stu-id="96241-219">If you deleted the Backup management servers associated with the vault, but there are servers listed in the **Essentials** pane, see [Find the Backup management servers registered to the vault](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault).</span></span>
5. <span data-ttu-id="96241-220">若要確認您想要刪除保存庫，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="96241-220">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="96241-221">保存庫便會被刪除，入口網站會回到 [新增]  服務功能表。</span><span class="sxs-lookup"><span data-stu-id="96241-221">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="delete-a-vault-used-to-protect-a-production-server"></a><span data-ttu-id="96241-222">刪除用來保護生產伺服器的保存庫</span><span class="sxs-lookup"><span data-stu-id="96241-222">Delete a vault used to protect a Production server</span></span>
<span data-ttu-id="96241-223">在刪除用來保護生產伺服器的保存庫之前，您必須先刪除或取消註冊保存庫中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="96241-223">Before you can delete a vault used to protect a Production server, you must delete or unregister the server from the vault.</span></span>

<span data-ttu-id="96241-224">刪除與保存庫相關聯的生產伺服器︰</span><span class="sxs-lookup"><span data-stu-id="96241-224">To delete the Production server associated with the vault:</span></span>

1. <span data-ttu-id="96241-225">在 Azure 入口網站中，開啟保存庫儀表板，然後按一下 [設定]  >  > 。</span><span class="sxs-lookup"><span data-stu-id="96241-225">In the Azure portal, open the vault dashboard and click **Settings** > **Backup Infrastructure** > **Production Servers**.</span></span>

    ![開啟生產伺服器刀鋒視窗](./media/backup-azure-delete-vault/delete-production-server.png)

    <span data-ttu-id="96241-227">[生產伺服器]  刀鋒視窗隨即開啟，並列出保存庫中所有的生產伺服器。</span><span class="sxs-lookup"><span data-stu-id="96241-227">The **Production Servers** blade opens and lists all Production servers in the vault.</span></span>

    ![生產伺服器的清單](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. <span data-ttu-id="96241-229">在 [生產伺服器] 刀鋒視窗中，以滑鼠右鍵按一下伺服器，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="96241-229">On the **Production Servers** blade, right-click on the server, and click **Delete**.</span></span>

    ![<span data-ttu-id="96241-230">刪除生產伺服器</span><span class="sxs-lookup"><span data-stu-id="96241-230">delete production server</span></span> ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    <span data-ttu-id="96241-231">[刪除]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="96241-231">The **Delete** blade opens.</span></span>

    ![<span data-ttu-id="96241-232">刪除生產伺服器</span><span class="sxs-lookup"><span data-stu-id="96241-232">delete production server</span></span> ](./media/backup-azure-delete-vault/delete-blade.png)
3. <span data-ttu-id="96241-233">在 [刪除] 刀鋒視窗上，確認伺服器名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="96241-233">On the **Delete** blade, confirm the server name, and click **Delete**.</span></span> <span data-ttu-id="96241-234">您必須正確命名伺服器，[刪除] 按鈕才能生效。</span><span class="sxs-lookup"><span data-stu-id="96241-234">You must correctly name the server, to activate the **Delete** button.</span></span>

    <span data-ttu-id="96241-235">一旦刪除保存庫，您會收到訊息，指出已刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-235">Once the vault is deleted, you receive a message stating the vault has been deleted.</span></span> <span data-ttu-id="96241-236">刪除保存庫中的所有伺服器之後，往回捲動至保存庫儀表板中的 [基本] 窗格。</span><span class="sxs-lookup"><span data-stu-id="96241-236">After deleting all servers in the vault, scroll back to the Essentials pane in the vault dashboard.</span></span>
4. <span data-ttu-id="96241-237">在保存庫儀表板中，確認已沒有任何 [備份項目]、[備份管理伺服器] 或 [複寫的項目]。</span><span class="sxs-lookup"><span data-stu-id="96241-237">In the vault dashboard, make sure there are no **Backup Items**, **Backup management servers**, or **Replicated items**.</span></span> <span data-ttu-id="96241-238">在保存庫工具列上，按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="96241-238">On the vault toolbar, click **Delete**.</span></span>
5. <span data-ttu-id="96241-239">若要確認您想要刪除保存庫，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="96241-239">To verify that you want to delete the vault, click **Yes**.</span></span>

    <span data-ttu-id="96241-240">保存庫便會被刪除，入口網站會回到 [新增]  服務功能表。</span><span class="sxs-lookup"><span data-stu-id="96241-240">The vault is deleted and the portal returns to the **New** service menu.</span></span>

## <a name="delete-a-backup-vault-in-classic-portal"></a><span data-ttu-id="96241-241">刪除傳統入口網站中的備份保存庫</span><span class="sxs-lookup"><span data-stu-id="96241-241">Delete a backup vault in classic portal</span></span>
<span data-ttu-id="96241-242">下列指示適用於在傳統入口網站中刪除備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-242">The following instructions are for deleting a Backup vault in the classic portal.</span></span> <span data-ttu-id="96241-243">在您可以刪除備份保存庫之前，您必須刪除復原點或備份的項目，並移除已註冊的伺服器。</span><span class="sxs-lookup"><span data-stu-id="96241-243">Before you can delete the Backup vault, you must delete the recovery points, or backed up items, and remove the registered servers.</span></span> <span data-ttu-id="96241-244">已註冊的伺服器為已註冊到保存庫的 Windows Server、工作站或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="96241-244">The registered servers are the Windows Server, workstation, or virtual machines that were registered to the vault.</span></span>

1. <span data-ttu-id="96241-245">開啟[傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="96241-245">Open the [Classic portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="96241-246">在備份保存庫清單中，選取要刪除的保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-246">From the list of backup vaults, select the vault you want to delete.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    <span data-ttu-id="96241-248">保存庫儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="96241-248">The vault dashboard opens.</span></span> <span data-ttu-id="96241-249">查看與保存庫相關聯的 Windows 伺服器和/或 Azure 虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="96241-249">Look at the number of Windows Servers and/or Azure virtual machines associated with the vault.</span></span> <span data-ttu-id="96241-250">並查看 Azure 中已使用的儲存體總計。</span><span class="sxs-lookup"><span data-stu-id="96241-250">Also, look at the total storage consumed in Azure.</span></span> <span data-ttu-id="96241-251">在刪除保存庫之前，請停止所有備份作業並刪除所有資料。</span><span class="sxs-lookup"><span data-stu-id="96241-251">Stop all backup jobs and delete all data before deleting the vault.</span></span>

3. <span data-ttu-id="96241-252">按一下 [受保護的項目] 索引標籤，然後按一下 [停止保護]。</span><span class="sxs-lookup"><span data-stu-id="96241-252">Click the **Protected Items** tab, and then click **Stop Protection**</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    <span data-ttu-id="96241-254">[停止保護您的保存庫]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="96241-254">The **Stop protection of 'your vault'** dialog appears.</span></span>
4. <span data-ttu-id="96241-255">在 [停止對 '您的保存庫' 的保護] 對話方塊中，勾選 [刪除相關聯的備份資料]，然後按一下![勾號](./media/backup-azure-delete-vault/checkmark.png)。</span><span class="sxs-lookup"><span data-stu-id="96241-255">In the **Stop protection of 'your vault'** dialog, check **Delete associated backup data** and click ![checkmark](./media/backup-azure-delete-vault/checkmark.png).</span></span> <br/>
    <span data-ttu-id="96241-256">或者，您可以選擇停止保護的原因，並提供註解。</span><span class="sxs-lookup"><span data-stu-id="96241-256">Optionally, you can choose a reason for stopping protection, and provide a comment.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    <span data-ttu-id="96241-258">刪除保存庫中的項目之後，保存庫是空的。</span><span class="sxs-lookup"><span data-stu-id="96241-258">After deleting the items in the vault, the vault will be empty.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. <span data-ttu-id="96241-260">在索引標籤的清單中，按一下 [已註冊的項目] 。</span><span class="sxs-lookup"><span data-stu-id="96241-260">In the list of tabs, click **Registered Items**.</span></span> <span data-ttu-id="96241-261">[類型] 下拉式功能表可讓您選擇註冊到保存庫的伺服器類型。</span><span class="sxs-lookup"><span data-stu-id="96241-261">The **Type** drop-down menu, enables you to choose the type of server registered to the vault.</span></span> <span data-ttu-id="96241-262">類型可以是 Windows Server 或 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="96241-262">The type can be Windows Server or Azure Virtual Machine.</span></span> <span data-ttu-id="96241-263">在下列範例中，選取已註冊到保存庫的虛擬機器，並按一下 [取消註冊]。</span><span class="sxs-lookup"><span data-stu-id="96241-263">In the following example, select the virtual machine registered to the vault, and click **Unregister**.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  <span data-ttu-id="96241-265">如果您想要刪除 Windows Server 的註冊，請從 [類型] 下拉式功能表中選取 [Windows Server]，按一下![核取記號](./media/backup-azure-delete-vault/checkmark.png)以重新整理畫面，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="96241-265">If you want to delete the registration for a Windows Server, from the **Type** drop-down menu, select **Windows Server**, click ![checkmark](./media/backup-azure-delete-vault/checkmark.png) to refresh the screen, and then click **Delete**.</span></span> <br/>

  ![選取 Windows Server](./media/backup-azure-delete-vault/select-windows-server.png)

6. <span data-ttu-id="96241-267">在索引標籤清單中，按一下 [儀表板]  以開啟該索引標籤。請確認沒有任何已註冊的伺服器或雲端中受保護的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="96241-267">In the list of tabs, click **Dashboard** to open that tab. Verify there are no registered servers or Azure virtual machines protected in the cloud.</span></span> <span data-ttu-id="96241-268">此外，也確認儲存體中沒有資料。</span><span class="sxs-lookup"><span data-stu-id="96241-268">Also, verify there is no data in storage.</span></span> <span data-ttu-id="96241-269">按一下 [刪除]  來刪除保存庫。</span><span class="sxs-lookup"><span data-stu-id="96241-269">Click **Delete** to delete the vault.</span></span>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    <span data-ttu-id="96241-271">[刪除備份保存庫] 確認畫面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="96241-271">The Delete Backup vault confirmation screen opens.</span></span> <span data-ttu-id="96241-272">選取為何要刪除保存庫的選項，按一下 </span><span class="sxs-lookup"><span data-stu-id="96241-272">Select an option why you're deleting the vault, and click</span></span> ![勾選記號](./media/backup-azure-delete-vault/checkmark.png)<span data-ttu-id="96241-274">。</span><span class="sxs-lookup"><span data-stu-id="96241-274">.</span></span> <br/>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    <span data-ttu-id="96241-276">保存庫便會被刪除，且您將返回傳統入口網站的儀表板。</span><span class="sxs-lookup"><span data-stu-id="96241-276">The vault is deleted, and you return to the classic portal dashboard.</span></span>

### <a name="find-the-backup-management-servers-registered-to-the-vault"></a><span data-ttu-id="96241-277">尋找註冊到保存庫的備份管理伺服器</span><span class="sxs-lookup"><span data-stu-id="96241-277">Find the Backup Management servers registered to the vault</span></span>
<span data-ttu-id="96241-278">如果您註冊多部伺服器至保存庫，可能很難全部記住。</span><span class="sxs-lookup"><span data-stu-id="96241-278">If you have multiple servers registered to a vault, it can be difficult to remember them.</span></span> <span data-ttu-id="96241-279">查看您註冊至保存庫的伺服器，並加以刪除︰</span><span class="sxs-lookup"><span data-stu-id="96241-279">To see the servers registered to the vault, and delete them:</span></span>

1. <span data-ttu-id="96241-280">開啟保存庫儀表板。</span><span class="sxs-lookup"><span data-stu-id="96241-280">Open the vault dashboard.</span></span>
2. <span data-ttu-id="96241-281">在 [基本] 窗格中，按一下 [設定] 以開啟此刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="96241-281">In the **Essentials** pane, click **Settings** to open that blade.</span></span>

    ![開啟設定刀鋒視窗](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. <span data-ttu-id="96241-283">在 [設定] 刀鋒視窗上，按一下 [備份基礎結構]。</span><span class="sxs-lookup"><span data-stu-id="96241-283">On the **Settings blade**, click **Backup Infrastructure**.</span></span>
4. <span data-ttu-id="96241-284">在 [備份基礎結構] 刀鋒視窗中，按一下 [備份管理伺服器]。</span><span class="sxs-lookup"><span data-stu-id="96241-284">On the **Backup Infrastructure** blade, click **Backup Management Servers**.</span></span> <span data-ttu-id="96241-285">[備份管理伺服器] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="96241-285">The Backup Management Servers blade opens.</span></span>

    ![備份管理伺服器的清單](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. <span data-ttu-id="96241-287">若要刪除清單中的伺服器，以滑鼠右鍵按一下伺服器的名稱，然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="96241-287">To delete a server from the list, right-click the name of the server and then click **Delete**.</span></span>
    <span data-ttu-id="96241-288">[刪除]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="96241-288">The **Delete** blade opens.</span></span>
6. <span data-ttu-id="96241-289">在 [刪除]  刀鋒視窗中，提供伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="96241-289">On the **Delete** blade, provide the name of the server.</span></span> <span data-ttu-id="96241-290">如果名稱很長，您可以從的備份管理伺服器的清單中複製並貼上。</span><span class="sxs-lookup"><span data-stu-id="96241-290">If it is a long name, you can copy and paste it from the list of Backup Management Servers.</span></span> <span data-ttu-id="96241-291">然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="96241-291">Then click **Delete**.</span></span>  
