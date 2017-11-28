---
title: "啟動 Azure Vm aaaBack |Microsoft 文件"
description: "探索、 註冊及備份 Azure 虛擬機器 tooa 復原服務保存庫。"
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
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="ce60f-104">備份 Azure 虛擬機器 tooa 復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="ce60f-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce60f-105">備份 Vm tooRecovery 服務保存庫</span><span class="sxs-lookup"><span data-stu-id="ce60f-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="ce60f-106">備份 Vm tooBackup 保存庫</span><span class="sxs-lookup"><span data-stu-id="ce60f-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="ce60f-107">這篇文章說明如何 tooback 向上 （資源管理員部署和傳統部署） 的 Azure Vm tooa 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="ce60f-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="ce60f-108">大部分的 hello 工作來備份 Vm 是 hello 準備。</span><span class="sxs-lookup"><span data-stu-id="ce60f-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="ce60f-109">您可以備份或保護的 VM，您必須先完成 hello[必要條件](backup-azure-arm-vms-prepare.md)tooprepare 環境以保護您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ce60f-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="ce60f-110">當您完成 hello 必要條件時，您可以起始 hello VM 的備份作業 tootake 快照集。</span><span class="sxs-lookup"><span data-stu-id="ce60f-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="ce60f-111">如需詳細資訊，請參閱 hello 文件上[規劃 VM 備份基礎結構在 Azure 中的](backup-azure-vms-introduction.md)和[Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)。</span><span class="sxs-lookup"><span data-stu-id="ce60f-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="ce60f-112">觸發 hello 備份工作</span><span class="sxs-lookup"><span data-stu-id="ce60f-112">Triggering hello backup job</span></span>
<span data-ttu-id="ce60f-113">hello 與 hello 復原服務保存庫相關聯的備份原則會定義 hello 備份作業的執行頻率和時間。</span><span class="sxs-lookup"><span data-stu-id="ce60f-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="ce60f-114">根據預設，hello 第一個排定的備份是 hello 初始備份。</span><span class="sxs-lookup"><span data-stu-id="ce60f-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="ce60f-115">Hello 初始備份，就會發生，直到 hello 上次備份的狀態上 hello**備份工作**刀鋒視窗中顯示為**警告 （已暫止的初始備份）**。</span><span class="sxs-lookup"><span data-stu-id="ce60f-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![待備份](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="ce60f-117">除非您初始的備份是到期 toobegin 過期，建議您執行**立即備份**。</span><span class="sxs-lookup"><span data-stu-id="ce60f-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="ce60f-118">hello hello 保存庫儀表板中的下列程序啟動。</span><span class="sxs-lookup"><span data-stu-id="ce60f-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="ce60f-119">此程序可在完成所有必要條件之後，執行 hello 初始備份工作。</span><span class="sxs-lookup"><span data-stu-id="ce60f-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="ce60f-120">如果尚未執行 hello 初始備份工作，就無法使用此程序。</span><span class="sxs-lookup"><span data-stu-id="ce60f-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="ce60f-121">hello 相關聯的備份原則會決定 hello 的下一個備份工作。</span><span class="sxs-lookup"><span data-stu-id="ce60f-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="ce60f-122">toorun hello 初始備份作業：</span><span class="sxs-lookup"><span data-stu-id="ce60f-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="ce60f-123">Hello 保存庫儀表板上按一下下的 hello 號碼**備份項目**，或按一下 hello**備份項目**磚。</span><span class="sxs-lookup"><span data-stu-id="ce60f-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="ce60f-124">
  ![設定圖示](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="ce60f-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="ce60f-125">hello**備份項目**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ce60f-125">hello **Backup Items** blade opens.</span></span>

  ![備份項目](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="ce60f-127">在 hello**備份項目**刀鋒視窗中，選取 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="ce60f-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![設定圖示](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="ce60f-129">hello**備份項目**清單隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ce60f-129">hello **Backup Items** list opens.</span></span> <br/>

  ![備份作業已觸發](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="ce60f-131">在 hello**備份項目**清單中，按一下 hello 省略符號**...** tooopen hello 操作功能表。</span><span class="sxs-lookup"><span data-stu-id="ce60f-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="ce60f-133">hello 操作功能表隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ce60f-133">hello Context menu appears.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="ce60f-135">Hello 操作功能表上，按一下 **備份現在**。</span><span class="sxs-lookup"><span data-stu-id="ce60f-135">On hello Context menu, click **Backup now**.</span></span>

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="ce60f-137">hello 立即備份 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ce60f-137">hello Backup Now blade opens.</span></span>

  ![顯示 hello 立即備份 刀鋒視窗](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="ce60f-139">Hello 立即備份刀鋒視窗上，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="ce60f-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![設定 hello 最後一天 hello 備份現在會保留復原點](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="ce60f-141">部署通知可讓您知道已觸發 hello 備份工作，而且您可以監視 hello hello 備份工作 頁面上的 hello 作業進度。</span><span class="sxs-lookup"><span data-stu-id="ce60f-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="ce60f-142">根據您的 VM hello 大小，建立 hello 初始備份可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="ce60f-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="ce60f-143">hello 初始備份，hello 保存庫儀表板上，在 hello tooview 或追蹤 hello 狀態**備份工作**磚按一下**正在**。</span><span class="sxs-lookup"><span data-stu-id="ce60f-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="ce60f-145">hello 備份作業 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ce60f-145">hello Backup Jobs blade opens.</span></span>

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="ce60f-147">在 hello**備份作業**刀鋒視窗中，您可以查看所有工作的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="ce60f-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="ce60f-148">請檢查 VM 的 hello 備份工作是否仍在進行中，或若它已完成。</span><span class="sxs-lookup"><span data-stu-id="ce60f-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="ce60f-149">Hello 狀態的備份工作完成時，是*已完成*。</span><span class="sxs-lookup"><span data-stu-id="ce60f-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ce60f-150">Hello 備份作業的一部分 hello Azure 備份服務發出的命令 toohello 備份擴充功能中每個 VM tooflush 所有寫入，並採取一致的快照集。</span><span class="sxs-lookup"><span data-stu-id="ce60f-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="ce60f-151">錯誤疑難排解</span><span class="sxs-lookup"><span data-stu-id="ce60f-151">Troubleshooting errors</span></span>
<span data-ttu-id="ce60f-152">如果您註冊您的虛擬機器執行備份時的問題，請參閱 hello [VM 疑難排解文章](backup-azure-vms-troubleshoot.md)的說明。</span><span class="sxs-lookup"><span data-stu-id="ce60f-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce60f-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce60f-153">Next steps</span></span>
<span data-ttu-id="ce60f-154">既然您已保護您的 VM，請參閱下列文章 toolearn 有關 VM 管理工作，hello 和如何 toorestore Vm。</span><span class="sxs-lookup"><span data-stu-id="ce60f-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="ce60f-155">管理和監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ce60f-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="ce60f-156">還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ce60f-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
