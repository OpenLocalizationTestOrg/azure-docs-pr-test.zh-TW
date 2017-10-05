---
title: "備份 Azure VM | Microsoft Docs"
description: "探索、註冊及備份 Azure 虛擬機器到復原服務保存庫。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "虛擬機器備份; 備份虛擬機器; 備份和災害復原; arm vm 備份"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="e0ae2-104">將 Azure 虛擬機器備份到復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="e0ae2-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0ae2-105">將 VM 備份到復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="e0ae2-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="e0ae2-106">將 VM 備份到備份保存庫</span><span class="sxs-lookup"><span data-stu-id="e0ae2-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="e0ae2-107">本文將詳細說明如何將 Azure VM (包括以 Resource Manager 部署和傳統部署的 VM) 備份至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="e0ae2-108">備份 VM 的工作多數是準備。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="e0ae2-109">在備份或保護 VM 之前，您必須完成 [必要條件](backup-azure-arm-vms-prepare.md) 來備妥 VM 的保護環境。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="e0ae2-110">完成必要條件後，您就能初始備份作業來製作 VM 的快照集。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="e0ae2-111">如需詳細資訊，請參閱[在 Azure 中規劃 VM 備份基礎結構](backup-azure-vms-introduction.md)和 [Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)的文章。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="e0ae2-112">觸發備份作業</span><span class="sxs-lookup"><span data-stu-id="e0ae2-112">Triggering the backup job</span></span>
<span data-ttu-id="e0ae2-113">與復原服務保存庫相關聯的備份原則會定義備份作業的執行頻率和時間。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="e0ae2-114">根據預設，第一個排定的備份是初始備份。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="e0ae2-115">在執行初始備份之前，[備份作業] 刀鋒視窗上的 [上次備份狀態] 會顯示為 [警告 (待執行初始備份)]。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![待備份](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="e0ae2-117">除非您的初始備份預計會馬上開始，否則建議您執行 [立即備份] 。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="e0ae2-118">以下程序從保存庫儀表板開始。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="e0ae2-119">當您完成所有必要條件後，此程序可用來執行初始備份作業。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="e0ae2-120">如果您已執行過初始備份作業，此程序便不適用。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="e0ae2-121">相關聯的備份原則決定後續的備份作業。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="e0ae2-122">若要執行初始備份作業：</span><span class="sxs-lookup"><span data-stu-id="e0ae2-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="e0ae2-123">在保存庫儀表板中，按一下 [備份項目] 下的數字，或按一下 [備份項目] 圖格。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="e0ae2-124">
  ![設定圖示](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="e0ae2-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="e0ae2-125">[備份項目]  刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-125">The **Backup Items** blade opens.</span></span>

  ![備份項目](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="e0ae2-127">在 [備份項目] 刀鋒視窗中，選取該項目。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-127">On the **Backup Items** blade, select the item.</span></span>

  ![設定圖示](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="e0ae2-129">[備份項目] 清單隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-129">The **Backup Items** list opens.</span></span> <br/>

  ![備份作業已觸發](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="e0ae2-131">在 [備份項目] 清單上，按一下省略符號 **...** 以開啟操作功能表。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="e0ae2-133">操作功能表隨即出現。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-133">The Context menu appears.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="e0ae2-135">在操作功能表上，按一下 [立即備份]。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-135">On the Context menu, click **Backup now**.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="e0ae2-137">[立即備份] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-137">The Backup Now blade opens.</span></span>

  ![顯示 [立即備份] 刀鋒視窗](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="e0ae2-139">在 [立即備份] 刀鋒視窗上，按一下日曆圖示，使用日曆控制項選取此復原點保留的最後一天，然後按一下 [備份]。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![設定 [立即備份] 復原點保留的最後一天](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="e0ae2-141">部署通知可讓您知道已觸發備份工作，而且您可以在 [備份工作] 頁面上監視作業的進度。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="e0ae2-142">根據您的 VM 大小，建立初始備份可能需要花一點時間。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="e0ae2-143">若要在保存庫儀表板上檢視或追蹤初始備份的狀態，請在 [備份工作] 圖格上，按一下 [進行中]。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="e0ae2-145">[備份工作] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-145">The Backup Jobs blade opens.</span></span>

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="e0ae2-147">在 [備份作業]  刀鋒視窗中，您可以看到所有作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="e0ae2-148">檢查您 VM 的備份作業是否仍在進行中或已經完成。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="e0ae2-149">當備份工作完成時，狀態會是「完成」 。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e0ae2-150">在備份工作進行時，Azure 備份服務會對每個 VM 中的備份擴充功能發出命令，以排清所有寫入並取得一致的快照。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="e0ae2-151">錯誤疑難排解</span><span class="sxs-lookup"><span data-stu-id="e0ae2-151">Troubleshooting errors</span></span>
<span data-ttu-id="e0ae2-152">如果您在備份虛擬機器時遇到問題，請參閱 [VM 疑難排解文章](backup-azure-vms-troubleshoot.md)以取得說明。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0ae2-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0ae2-153">Next steps</span></span>
<span data-ttu-id="e0ae2-154">現在您已能保護您的 VM，請參閱下列文章，以了解 VM 管理工作及如何還原 VM。</span><span class="sxs-lookup"><span data-stu-id="e0ae2-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="e0ae2-155">管理和監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e0ae2-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="e0ae2-156">還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e0ae2-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
