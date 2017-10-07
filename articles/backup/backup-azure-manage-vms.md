---
title: "aaaManage 資源管理員部署虛擬機器備份 |Microsoft 文件"
description: "深入了解如何 toomanage 和監視資源管理員部署虛擬機器備份"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="8ed35-103">管理 Azure 虛擬機器備份</span><span class="sxs-lookup"><span data-stu-id="8ed35-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ed35-104">管理 Azure VM 備份</span><span class="sxs-lookup"><span data-stu-id="8ed35-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="8ed35-105">管理傳統 VM 備份</span><span class="sxs-lookup"><span data-stu-id="8ed35-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="8ed35-106">這篇文章提供有關管理 VM 備份的指引，並說明可用 hello 入口網站儀表板中的 hello 備份警示資訊。</span><span class="sxs-lookup"><span data-stu-id="8ed35-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="8ed35-107">這篇文章中的 hello 指導方針適用於向復原服務保存庫 toousing Vm。</span><span class="sxs-lookup"><span data-stu-id="8ed35-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="8ed35-108">這份文件未涵蓋 hello 建立的虛擬機器，或它不會說明如何 tooprotect 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ed35-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="8ed35-109">保護與復原服務保存庫在 Azure 中的 Azure Resource Manager 部署 Vm 的入門，請參閱[第一印象： 備份復原服務保存庫的 Vm tooa](backup-azure-vms-first-look-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="8ed35-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="8ed35-110">管理保存庫與受保護的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8ed35-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="8ed35-111">Hello Azure 入口網站，在 hello 復原服務保存庫儀表板會提供存取 tooinformation 有關 hello 保存庫包括：</span><span class="sxs-lookup"><span data-stu-id="8ed35-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="8ed35-112">hello 最新的備份快照集，這也是最新還原點 hello < b\></span><span class="sxs-lookup"><span data-stu-id="8ed35-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="8ed35-113">hello 備份原則 < b\></span><span class="sxs-lookup"><span data-stu-id="8ed35-113">hello backup policy <br\></span></span>
* <span data-ttu-id="8ed35-114">所有備份快照的大小總計 <br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="8ed35-115">hello 保存庫所保護的虛擬機器的數目 < b\></span><span class="sxs-lookup"><span data-stu-id="8ed35-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="8ed35-116">許多管理工作，與虛擬機器的備份開始與 hello 儀表板中開啟 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="8ed35-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="8ed35-117">不過，由於保存庫可能 tooview 詳細特定 VM 中，開啟多個項目 （或多個 Vm） 使用的 tooprotect hello 保存庫項目儀表板。</span><span class="sxs-lookup"><span data-stu-id="8ed35-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="8ed35-118">hello 下列程序為您示範如何 tooopen hello*保存庫儀表板*然後繼續 toohello*保存庫項目儀表板*。</span><span class="sxs-lookup"><span data-stu-id="8ed35-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="8ed35-119">指出如何 tooadd hello 保存庫和保存庫項目 toohello Azure 儀表板使用 hello 的 Pin toodashboard 命令兩個程序中有 「 提示 」。</span><span class="sxs-lookup"><span data-stu-id="8ed35-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="8ed35-120">Pin toodashboard 是一種建立快顯 toohello 保存庫或項目。</span><span class="sxs-lookup"><span data-stu-id="8ed35-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="8ed35-121">您也可以從 hello 捷徑執行常用命令。</span><span class="sxs-lookup"><span data-stu-id="8ed35-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="8ed35-122">如果您有多個儀表板並刀鋒視窗開啟時，使用 hello 深藍色滑動軸在 hello hello 視窗 tooslide hello 來回 Azure 儀表板底部。</span><span class="sxs-lookup"><span data-stu-id="8ed35-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![使用滑桿以完整檢視](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="8ed35-124">開啟 復原服務保存庫 hello 儀表板中：</span><span class="sxs-lookup"><span data-stu-id="8ed35-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="8ed35-125">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="8ed35-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8ed35-126">在 hello 中樞功能表中，按一下 **瀏覽**hello 清單中的資源，在輸入**復原服務**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="8ed35-127">當您開始輸入 hello 清單會篩選根據您的輸入。</span><span class="sxs-lookup"><span data-stu-id="8ed35-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="8ed35-128">按一下 [復原服務保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="8ed35-128">Click **Recovery Services vault**.</span></span>

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="8ed35-130">會顯示復原服務保存庫 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="8ed35-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="8ed35-131">復原服務保存庫清單</span><span class="sxs-lookup"><span data-stu-id="8ed35-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="8ed35-132">如果您釘選的保存庫 toohello Azure 儀表板，該保存庫時，立即存取開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8ed35-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="8ed35-133">toopin 保存庫 toohello 儀表板，在 hello 保存庫清單中，hello 保存庫，以滑鼠右鍵按一下並選取**Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="8ed35-134">從 hello 的保存庫的清單，請選取 hello 保存庫 tooopen 其儀表板。</span><span class="sxs-lookup"><span data-stu-id="8ed35-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="8ed35-135">當您選取 hello 保存庫、 hello 保存庫儀表板和 hello**設定**刀鋒視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="8ed35-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="8ed35-136">在下列映像的 hello，hello **Contoso 保存庫**儀表板會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="8ed35-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![開啟保存庫儀表板和設定刀鋒視窗](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="8ed35-138">開啟保存庫項目儀表板</span><span class="sxs-lookup"><span data-stu-id="8ed35-138">Open a vault item dashboard</span></span>
<span data-ttu-id="8ed35-139">Hello 前程序中，您會開啟 hello 保存庫儀表板。</span><span class="sxs-lookup"><span data-stu-id="8ed35-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="8ed35-140">tooopen hello 保存庫項目儀表板：</span><span class="sxs-lookup"><span data-stu-id="8ed35-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="8ed35-141">Hello 保存庫儀表板] 上 hello**備份項目**磚中，按一下 [ **Azure 虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![開啟備份項目備份圖格](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="8ed35-143">hello**備份項目**刀鋒視窗會列出 hello 最後一個備份作業每個項目。</span><span class="sxs-lookup"><span data-stu-id="8ed35-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="8ed35-144">在此範例中，有一個受此保存庫保護的虛擬機器：demovm markgal。</span><span class="sxs-lookup"><span data-stu-id="8ed35-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![備份項目圖格](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="8ed35-146">為了方便存取，您可以釘選的保存庫項目 toohello Azure 儀表板。</span><span class="sxs-lookup"><span data-stu-id="8ed35-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="8ed35-147">保存庫中的項目，hello 保存庫項目清單中，以滑鼠右鍵按一下 hello 項目並選取 toopin **Pin toodashboard**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="8ed35-148">在 hello**備份項目**刀鋒視窗中，按一下 hello 項目 tooopen hello 保存庫項目的儀表板。</span><span class="sxs-lookup"><span data-stu-id="8ed35-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![備份項目圖格](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="8ed35-150">hello 保存庫項目儀表板及其**設定**刀鋒視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="8ed35-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![搭配設定刀鋒視窗的備份項目儀表板](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="8ed35-152">從 hello 保存庫項目儀表板，您可以完成許多金鑰管理工作，例如：</span><span class="sxs-lookup"><span data-stu-id="8ed35-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="8ed35-153">變更原則或建立新的備份原則 <br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="8ed35-154">檢視還原點並查看其一致性狀態 <br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="8ed35-155">虛擬機器的隨選備份 <br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="8ed35-156">停止保護虛擬機器 <br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="8ed35-157">繼續保護虛擬機器 <br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="8ed35-158">刪除備份資料 (或復原點) <br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="8ed35-159">[還原備份磁碟](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="8ed35-160">下列程序的 hello，hello 開始點就是 hello 保存庫項目儀表板。</span><span class="sxs-lookup"><span data-stu-id="8ed35-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="8ed35-161">管理備份原則</span><span class="sxs-lookup"><span data-stu-id="8ed35-161">Manage backup policies</span></span>
1. <span data-ttu-id="8ed35-162">在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **所有設定**tooopen hello**設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8ed35-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![備份原則刀鋒視窗](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="8ed35-164">在 hello**設定**刀鋒視窗中，按一下 **備份原則**tooopen 該刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8ed35-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="8ed35-165">在 hello 刀鋒視窗中，會顯示 hello 備份頻率和保留範圍詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8ed35-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![備份原則刀鋒視窗](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="8ed35-167">從 hello**選擇備份原則**功能表：</span><span class="sxs-lookup"><span data-stu-id="8ed35-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="8ed35-168">toochange 原則中，選取不同的原則，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="8ed35-169">hello 新原則會立即套用的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="8ed35-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="8ed35-170"><br\></span><span class="sxs-lookup"><span data-stu-id="8ed35-170"><br\></span></span>
   * <span data-ttu-id="8ed35-171">toocreate 原則，選取**新建**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-171">toocreate a policy, select **Create New**.</span></span>

     ![虛擬機器備份](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="8ed35-173">如需建立備份原則的指示，請參閱 [定義備份原則](backup-azure-manage-vms.md#defining-a-backup-policy)。</span><span class="sxs-lookup"><span data-stu-id="8ed35-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="8ed35-174">管理備份原則，請確定 toofollow hello[最佳做法](backup-azure-vms-introduction.md#best-practices)的最佳化備份效能</span><span class="sxs-lookup"><span data-stu-id="8ed35-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="8ed35-175">虛擬機器的隨選備份</span><span class="sxs-lookup"><span data-stu-id="8ed35-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="8ed35-176">設定保護後，您可以執行虛擬機器的隨選備份。</span><span class="sxs-lookup"><span data-stu-id="8ed35-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="8ed35-177">Hello 初始備份暫止時，隨備份會建立的 hello 復原服務保存庫中的 hello 虛擬機器的完整複本。</span><span class="sxs-lookup"><span data-stu-id="8ed35-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="8ed35-178">如果 hello 初始備份完成時，隨備份才會傳送變更從 hello 上一個快照，toohello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8ed35-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="8ed35-179">亦即，後續備份一律是增量備份。</span><span class="sxs-lookup"><span data-stu-id="8ed35-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed35-180">指定備份的 hello 保留範圍是 hello hello 每日備份的點 hello 原則中所指定的保留值。</span><span class="sxs-lookup"><span data-stu-id="8ed35-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="8ed35-181">如果不選取任何每日備份點，則會使用 hello 每週備份點。</span><span class="sxs-lookup"><span data-stu-id="8ed35-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="8ed35-182">虛擬機器的 tootrigger 隨備份：</span><span class="sxs-lookup"><span data-stu-id="8ed35-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="8ed35-183">在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **備份現在**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![立即備份按鈕](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="8ed35-185">hello 入口網站可確保您想 toostart 視備份工作。</span><span class="sxs-lookup"><span data-stu-id="8ed35-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="8ed35-186">按一下**是**toostart hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="8ed35-186">Click **Yes** toostart hello backup job.</span></span>

    ![立即備份按鈕](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="8ed35-188">hello 備份建立復原點。</span><span class="sxs-lookup"><span data-stu-id="8ed35-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="8ed35-189">hello hello 復原點的保留範圍是 hello 與 hello hello 虛擬機器相關聯的原則中指定的保留範圍相同。</span><span class="sxs-lookup"><span data-stu-id="8ed35-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="8ed35-190">tootrack hello 進行 hello 保存庫儀表板中的 hello 工作按一下 hello **Backup 工作**磚。</span><span class="sxs-lookup"><span data-stu-id="8ed35-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="8ed35-191">停止保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8ed35-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="8ed35-192">如果您選擇 toostop 保護虛擬機器，您會問您是否 tooretain hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="8ed35-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="8ed35-193">有兩種方式 toostop 保護的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="8ed35-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="8ed35-194">停止所有未來的備份作業並刪除所有復原點，或</span><span class="sxs-lookup"><span data-stu-id="8ed35-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="8ed35-195">停止所有未來備份工作，但保留 hello 復原點</span><span class="sxs-lookup"><span data-stu-id="8ed35-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="8ed35-196">沒有儲存體中留下 hello 復原點的相關成本。</span><span class="sxs-lookup"><span data-stu-id="8ed35-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="8ed35-197">不過，復原點可能會留下 hello hello 好處是稍後，您可以還原 hello 虛擬機器有需要。</span><span class="sxs-lookup"><span data-stu-id="8ed35-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="8ed35-198">復原點可能會留下 hello hello 成本的相關資訊，請參閱 hello[定價詳細資料](https://azure.microsoft.com/pricing/details/backup/)。</span><span class="sxs-lookup"><span data-stu-id="8ed35-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="8ed35-199">如果您選擇 toodelete 所有復原點，您無法還原 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ed35-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="8ed35-200">toostop 虛擬機器的保護：</span><span class="sxs-lookup"><span data-stu-id="8ed35-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="8ed35-201">在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **停止備份**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![停止備份按鈕](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="8ed35-203">hello 停止備份 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="8ed35-203">hello Stop Backup blade opens.</span></span>

    ![停止備份刀鋒視窗](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="8ed35-205">在 hello**停止備份**刀鋒視窗中，選擇 tooretain 或 delete hello 備份資料。</span><span class="sxs-lookup"><span data-stu-id="8ed35-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="8ed35-206">hello 資訊 方塊會提供有關您所選擇的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8ed35-206">hello information box provides details about your choice.</span></span>

    ![停止保護](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="8ed35-208">如果您選擇 tooretain hello 備份資料，請略過 toostep 4。</span><span class="sxs-lookup"><span data-stu-id="8ed35-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="8ed35-209">如果您選擇 toodelete 備份資料，請確認您想 toostop hello 備份工作，並刪除 hello 的復原點類型 hello hello 項目名稱。</span><span class="sxs-lookup"><span data-stu-id="8ed35-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![停止驗證](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="8ed35-211">如果您不確定的 hello 項目名稱，將滑鼠停留在 hello 驚嘆號 tooview hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="8ed35-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="8ed35-212">此外，hello hello 項目名稱會低於**停止備份**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="8ed35-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="8ed35-213">選擇性地提供 [原因] 或 [註解]。</span><span class="sxs-lookup"><span data-stu-id="8ed35-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="8ed35-214">toostop hello 備份工作 hello 目前項目，請按一下![停止備份 按鈕](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="8ed35-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="8ed35-215">通知訊息，可讓您知道 hello 備份工作都已停止。</span><span class="sxs-lookup"><span data-stu-id="8ed35-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![確認停止保護](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="8ed35-217">繼續保護虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8ed35-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="8ed35-218">如果 hello**保留備份資料**選項選擇 hello 虛擬機器的保護已停止時，就可能 tooresume 保護。</span><span class="sxs-lookup"><span data-stu-id="8ed35-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="8ed35-219">如果 hello**刪除備份資料**選擇選項，則無法繼續 hello 虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="8ed35-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="8ed35-220">tooresume hello 虛擬機器的保護</span><span class="sxs-lookup"><span data-stu-id="8ed35-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="8ed35-221">在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **繼續備份**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![繼續保護](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="8ed35-223">hello 備份原則 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="8ed35-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8ed35-224">當重新保護 hello 虛擬機器時，您可以選擇不同的原則，小於 hello 原則與虛擬機器已受保護一開始。</span><span class="sxs-lookup"><span data-stu-id="8ed35-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="8ed35-225">中的 hello 步驟[管理備份原則](backup-azure-manage-vms.md#manage-backup-policies)tooassign hello 原則 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8ed35-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="8ed35-226">一旦 hello 備份原則套用的 toohello 虛擬機器，您會看到下列訊息的 hello。</span><span class="sxs-lookup"><span data-stu-id="8ed35-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![已成功保護 VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="8ed35-228">刪除備份資料</span><span class="sxs-lookup"><span data-stu-id="8ed35-228">Delete Backup data</span></span>
<span data-ttu-id="8ed35-229">您可以刪除 hello 期間 hello 與虛擬機器相關聯的備份資料**停止備份**作業，或每當 hello 之後備份工作已完成。</span><span class="sxs-lookup"><span data-stu-id="8ed35-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="8ed35-230">它甚至可能有幫助 toowait 天或週之前刪除 hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="8ed35-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="8ed35-231">不同於還原復原點，當您刪除備份資料時，您無法選擇特定的復原點 toodelete。</span><span class="sxs-lookup"><span data-stu-id="8ed35-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="8ed35-232">如果您選擇 toodelete 備份資料，您會刪除與 hello 項目相關聯的所有復原點。</span><span class="sxs-lookup"><span data-stu-id="8ed35-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="8ed35-233">hello 下列程序假設 hello hello 虛擬機器的備份工作已停止或停用。</span><span class="sxs-lookup"><span data-stu-id="8ed35-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="8ed35-234">一旦 hello 備份工作已停用，hello**繼續備份**和**刪除備份**hello 保存庫項目儀表板中可用選項。</span><span class="sxs-lookup"><span data-stu-id="8ed35-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![繼續和刪除按鈕](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="8ed35-236">toodelete hello 與虛擬機器上的備份資料*備份已停用*:</span><span class="sxs-lookup"><span data-stu-id="8ed35-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="8ed35-237">在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **刪除備份**。</span><span class="sxs-lookup"><span data-stu-id="8ed35-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="8ed35-239">hello**刪除備份資料**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="8ed35-239">hello **Delete Backup Data** blade opens.</span></span>

    ![VM 類型](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="8ed35-241">型別 hello 名稱要的 hello 項目 tooconfirm toodelete hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="8ed35-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![停止驗證](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="8ed35-243">如果您不確定的 hello 項目名稱，將滑鼠停留在 hello 驚嘆號 tooview hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="8ed35-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="8ed35-244">此外，hello hello 項目名稱會低於**刪除備份資料**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="8ed35-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="8ed35-245">選擇性地提供 [原因] 或 [註解]。</span><span class="sxs-lookup"><span data-stu-id="8ed35-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="8ed35-246">toodelete hello 備份資料 hello 目前項目，請按一下![停止備份 按鈕](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="8ed35-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="8ed35-247">通知訊息，可讓您知道 hello 備份資料都已刪除。</span><span class="sxs-lookup"><span data-stu-id="8ed35-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ed35-248">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ed35-248">Next steps</span></span>
<span data-ttu-id="8ed35-249">如需從復原點重新建立虛擬機器的詳細資訊，請參閱 [還原 Azure VM](backup-azure-restore-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="8ed35-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="8ed35-250">如果您需要保護虛擬機器的詳細資訊，請參閱[第一印象： 備份復原服務保存庫的 Vm tooa](backup-azure-vms-first-look-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="8ed35-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="8ed35-251">如需監視事件的相關資訊，請參閱 [監視 Azure 虛擬機器備份的警示](backup-azure-monitor-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="8ed35-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
