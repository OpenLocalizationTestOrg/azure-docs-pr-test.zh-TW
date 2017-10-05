---
title: "將傳統型部署的 Azure 虛擬機器備份到備份保存庫| Microsoft Docs"
description: "利用 Azure 虛擬機器備份的這些程序來探索、註冊及備份您的虛擬機器。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "虛擬機器備份; 備份虛擬機器; 備份和災害復原; vm 備份"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: e1da8bce96078a43c656f84005cefc8bbe81c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="464f8-104">備份 Azure 虛擬機器 (傳統入口網站)</span><span class="sxs-lookup"><span data-stu-id="464f8-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="464f8-105">將 VM 備份到復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="464f8-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="464f8-106">將 VM 備份到備份保存庫</span><span class="sxs-lookup"><span data-stu-id="464f8-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="464f8-107">本文提供將傳統部署的 Azure 虛擬機器 (VM) 備份到備份保存庫的程序。</span><span class="sxs-lookup"><span data-stu-id="464f8-107">This article provides the procedures for backing up a Classic-deployed Azure virtual machine (VM) to a Backup vault.</span></span> <span data-ttu-id="464f8-108">您必須先處理幾件工作，才能備份 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-108">There are a few tasks you need to take care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="464f8-109">如果您尚未這樣做，請完成 [必要條件](backup-azure-vms-prepare.md) ，讓您的環境準備好進行備份 VM 的工作。</span><span class="sxs-lookup"><span data-stu-id="464f8-109">If you haven't already done so, complete the [prerequisites](backup-azure-vms-prepare.md) to prepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="464f8-110">如需詳細資訊，請參閱[在 Azure 中規劃 VM 備份基礎結構](backup-azure-vms-introduction.md)和 [Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)的文件。</span><span class="sxs-lookup"><span data-stu-id="464f8-110">For additional information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="464f8-111">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="464f8-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="464f8-112">備份保存庫只能保護傳統部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="464f8-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="464f8-113">您無法使用備份保存庫保護 Resource Manager 部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="464f8-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="464f8-114">如需使用復原服務保存庫的詳細資訊，請參閱 [將 VM 備份到復原服務保存庫](backup-azure-arm-vms.md) 。</span><span class="sxs-lookup"><span data-stu-id="464f8-114">See [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="464f8-115">備份 Azure 虛擬機器需要三個主要步驟：</span><span class="sxs-lookup"><span data-stu-id="464f8-115">Backing up Azure virtual machines involves three key steps:</span></span>

![備份 Azure IaaS VM 的三個步驟](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="464f8-117">備份虛擬機器是本機的程序。</span><span class="sxs-lookup"><span data-stu-id="464f8-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="464f8-118">您無法將某一個區域中的虛擬機器備份到另一個區域中的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-118">You cannot back up virtual machines in one region to a backup vault in another region.</span></span> <span data-ttu-id="464f8-119">因此，您必須在每個 Azure 區域中建立備份保存庫，其中含有將備份的 VM。</span><span class="sxs-lookup"><span data-stu-id="464f8-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="464f8-120">從 2017 年 3 月開始，您無法再使用傳統入口網站來建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-120">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="464f8-121">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-121">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="464f8-122">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="464f8-122">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="464f8-123">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-123">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="464f8-124">在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-124">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="464f8-125">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="464f8-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="464f8-126">所有其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-126">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="464f8-127">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="464f8-127">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="464f8-128">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="464f8-128">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="464f8-129">步驟 1 - 探索 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="464f8-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="464f8-130">若要在註冊前確保能夠識別任何已加入至訂用帳戶的新虛擬機器 (VM)，請執行探索程序。</span><span class="sxs-lookup"><span data-stu-id="464f8-130">To ensure any new virtual machines (VMs) added to the subscription are identified before registering, run the discovery process.</span></span> <span data-ttu-id="464f8-131">此程序會在 Azure 中查詢訂用帳戶中的虛擬機器清單，以及其他資訊，例如雲端服務名稱、區域等。</span><span class="sxs-lookup"><span data-stu-id="464f8-131">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="464f8-132">登入 [傳統入口網站](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="464f8-132">Sign in to the [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="464f8-133">在 Azure 傳統服務清單中，按一下 [復原服務]  以開啟備份和 Site Recovery 保存庫清單。</span><span class="sxs-lookup"><span data-stu-id="464f8-133">In the list of Azure services, click **Recovery Services** to open the list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="464f8-134">![開啟保存庫清單](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="464f8-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="464f8-135">在備份保存庫清單中，選取要備份 VM 的保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-135">In the list of Backup vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="464f8-136">如果這是新的保存庫，則入口網站會開啟至 [快速啟動]  頁面。</span><span class="sxs-lookup"><span data-stu-id="464f8-136">If this is a new vault the portal opens to the **Quick Start** page.</span></span>

    ![開啟已註冊的項目功能表](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="464f8-138">如果先前已設定此保存庫，則入口網站會開啟至最近使用的功能表。</span><span class="sxs-lookup"><span data-stu-id="464f8-138">If the vault has previously been configured, the portal opens to the most recently used menu.</span></span>
4. <span data-ttu-id="464f8-139">在保存庫功能表 (位於頁面頂端) 中，按一下 [已註冊的項目] 。</span><span class="sxs-lookup"><span data-stu-id="464f8-139">From the vault menu (at the top of the page), click **Registered Items**.</span></span>

    ![開啟已註冊的項目功能表](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="464f8-141">在 [類型] 功能表中選取 [Azure 虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="464f8-141">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="464f8-143">按一下頁面底部的 [ **探索** ]。</span><span class="sxs-lookup"><span data-stu-id="464f8-143">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="464f8-144">![探索按鈕](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="464f8-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="464f8-145">在列表顯示虛擬機器時，探索程序可能需花費幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="464f8-145">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="464f8-146">畫面底部會有通知讓您知道程序正在執行中。</span><span class="sxs-lookup"><span data-stu-id="464f8-146">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![探索 VM](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="464f8-148">程序完成時，通知隨即變更。</span><span class="sxs-lookup"><span data-stu-id="464f8-148">The notification changes when the process is complete.</span></span> <span data-ttu-id="464f8-149">如果探索程序找不到虛擬機器，請先確定 VM 存在。</span><span class="sxs-lookup"><span data-stu-id="464f8-149">If the discovery process did not find the virtual machines, first ensure the VMs exist.</span></span> <span data-ttu-id="464f8-150">如果 VM 存在，請確定 VM 位於與備份保存庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="464f8-150">If the VMs exist, ensure the VMs are in the same region as the backup vault.</span></span> <span data-ttu-id="464f8-151">如果 VM 存在且位於相同區域中，請確定 VM 尚未註冊到備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-151">If the VMs exist and are in the same region, ensure the VMs are not already registered to a backup vault.</span></span> <span data-ttu-id="464f8-152">如果 VM 已指派給備份保存庫，便無法指派給其他備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="464f8-152">If a VM is assigned to a backup vault it is not available to be assigned to other backup vaults.</span></span>

    ![探索完成](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="464f8-154">一旦找到新的項目，請移至步驟 2 並註冊您的 VM。</span><span class="sxs-lookup"><span data-stu-id="464f8-154">Once you have discovered the new items, go to Step 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="464f8-155">步驟 2 - 註冊 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="464f8-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="464f8-156">您必須註冊 Azure 虛擬機器，使其與 Azure 備份服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="464f8-156">You register an Azure virtual machine to associate it with the Azure Backup service.</span></span> <span data-ttu-id="464f8-157">這通常是一次性活動。</span><span class="sxs-lookup"><span data-stu-id="464f8-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="464f8-158">在 Azure 入口網站中，瀏覽至 [復原服務] 下的備份保存庫，然後按一下 [註冊的項目]。</span><span class="sxs-lookup"><span data-stu-id="464f8-158">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="464f8-159">從下拉式選單中選取 [Azure 虛擬機器]  。</span><span class="sxs-lookup"><span data-stu-id="464f8-159">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="464f8-161">按一下頁面底部的 [註冊]  。</span><span class="sxs-lookup"><span data-stu-id="464f8-161">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="464f8-162">![註冊按鈕](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="464f8-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="464f8-163">在 [註冊項目]  捷徑功能表中，選取您想要註冊的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-163">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span> <span data-ttu-id="464f8-164">如果有兩個以上同名的虛擬機器，請使用雲端服務加以區別。</span><span class="sxs-lookup"><span data-stu-id="464f8-164">If there are two or more virtual machines with the same name, use the cloud service to distinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="464f8-165">您可以同時註冊多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="464f8-166">系統會為您所選取的每個虛擬機器建立一個工作。</span><span class="sxs-lookup"><span data-stu-id="464f8-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="464f8-167">按一下通知中的 [檢視作業]，以移至 [作業] 頁面。</span><span class="sxs-lookup"><span data-stu-id="464f8-167">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![註冊作業](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="464f8-169">虛擬機器也會連同註冊作業的狀態，出現在已註冊的項目清單中。</span><span class="sxs-lookup"><span data-stu-id="464f8-169">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![註冊狀態 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="464f8-171">作業完成時，狀態會改變以反映「已註冊」  狀態。</span><span class="sxs-lookup"><span data-stu-id="464f8-171">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![註冊狀態 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="464f8-173">步驟 3 - 保護 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="464f8-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="464f8-174">現在，您可以設定虛擬機器的備份和保留原則。</span><span class="sxs-lookup"><span data-stu-id="464f8-174">Now you can set up a backup and retention policy for the virtual machine.</span></span> <span data-ttu-id="464f8-175">使用單一保護動作可以保護多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="464f8-176">2015 年 5 月之後建立的 Azure 備份保存庫，會隨附內建於保存庫的預設原則。</span><span class="sxs-lookup"><span data-stu-id="464f8-176">Azure Backup vaults created after May 2015 come with a default policy built into the vault.</span></span> <span data-ttu-id="464f8-177">這項預設原則會隨附 30 天預設保留和每日一次的備份排程。</span><span class="sxs-lookup"><span data-stu-id="464f8-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="464f8-178">在 Azure 入口網站中，瀏覽至 [復原服務] 下的備份保存庫，然後按一下 [註冊的項目]。</span><span class="sxs-lookup"><span data-stu-id="464f8-178">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="464f8-179">從下拉式選單中選取 [Azure 虛擬機器]  。</span><span class="sxs-lookup"><span data-stu-id="464f8-179">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![在入口網站中選取工作負載](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="464f8-181">按一下頁面底部的 [保護]  。</span><span class="sxs-lookup"><span data-stu-id="464f8-181">Click **PROTECT** at the bottom of the page.</span></span>

    <span data-ttu-id="464f8-182">[保護項目]  精靈隨即出現。</span><span class="sxs-lookup"><span data-stu-id="464f8-182">The **Protect Items wizard** appears.</span></span> <span data-ttu-id="464f8-183">此精靈只會列出已註冊且不受保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-183">The wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="464f8-184">選取您要保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-184">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="464f8-185">如果有兩個以上同名的虛擬機器，請使用雲端服務來區別虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-185">If there are two or more virtual machines with the same name, use the cloud service to distinguish between the virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="464f8-186">您可以同時保護多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![設定大規模保護](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="464f8-188">選擇 [備份排程]  ，以備份您所選取的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-188">Choose a **backup schedule** to back up the virtual machines that you've selected.</span></span> <span data-ttu-id="464f8-189">您可以從現有的一組原則中挑選，或定義新的原則。</span><span class="sxs-lookup"><span data-stu-id="464f8-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="464f8-190">每一個備份原則可以有多個相關聯的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="464f8-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="464f8-191">但無論何時，虛擬機器只能與一個原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="464f8-191">However, the virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![使用新的原則來保護](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="464f8-193">備份原則中包含排定備份的保留配置。</span><span class="sxs-lookup"><span data-stu-id="464f8-193">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="464f8-194">如果您選取現有的備份原則，就無法在下一個步驟中修改保留選項。</span><span class="sxs-lookup"><span data-stu-id="464f8-194">If you select an existing backup policy, you cannot modify the retention options in the next step.</span></span>
   >
   >

5. <span data-ttu-id="464f8-195">選擇要與備份相關聯的 [保留範圍]  。</span><span class="sxs-lookup"><span data-stu-id="464f8-195">Choose a **retention range** to associate with the backups.</span></span>

    ![使用彈性保留來保護](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="464f8-197">保留期原則會指定儲存備份的時間長度。</span><span class="sxs-lookup"><span data-stu-id="464f8-197">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="464f8-198">您可以根據進行備份的時間指定不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="464f8-198">You can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="464f8-199">例如，每日取得的備份點 (可充當作業復原點) 可能會保留 90 天。</span><span class="sxs-lookup"><span data-stu-id="464f8-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="464f8-200">相較之下，在每一季結尾所取得的備份點 (供稽核之用) 可能需要保留數個月或數年。</span><span class="sxs-lookup"><span data-stu-id="464f8-200">In comparison, a backup point taken at the end of each quarter (for audit purposes) may need to be preserved for many months or years.</span></span>

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="464f8-202">在此範例影像中：</span><span class="sxs-lookup"><span data-stu-id="464f8-202">In this example image:</span></span>

   * <span data-ttu-id="464f8-203">**每日的保留原則**：每日所進行的備份會儲存 30 天。</span><span class="sxs-lookup"><span data-stu-id="464f8-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="464f8-204">**每週的保留原則**：每個星期日所進行的備份會保留 104 週。</span><span class="sxs-lookup"><span data-stu-id="464f8-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="464f8-205">**每月的保留原則**：每月最後一個星期日所進行的備份會保留 120 個月。</span><span class="sxs-lookup"><span data-stu-id="464f8-205">**Monthly retention policy**: Backups taken on the last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="464f8-206">**每年的保留原則**：每年一月第一個星期日所進行的備份會保留 99 年。</span><span class="sxs-lookup"><span data-stu-id="464f8-206">**Yearly retention policy**: Backups taken on the first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="464f8-207">建立的工作可設定保護原則，並將虛擬機器與您所選取的每個虛擬機器的該項原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="464f8-207">A job is created to configure the protection policy and associate the virtual machines to that policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="464f8-208">若要檢視 [設定保護] 作業的清單，可按一下保存庫功能表中的 [作業]，然後從 [作業] 篩選器選取 [設定保護]。</span><span class="sxs-lookup"><span data-stu-id="464f8-208">To view the list of **Configure Protection** jobs, from the vaults menu, click **Jobs** and select **Configure Protection** from the **Operation** filter.</span></span>

    ![設定保護工作](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="464f8-210">初始備份</span><span class="sxs-lookup"><span data-stu-id="464f8-210">Initial backup</span></span>
<span data-ttu-id="464f8-211">虛擬機器受到原則保護之後，就會出現在 [受保護的項目] 索引標籤下，狀態為 [受保護 - (擱置中的初始備份)]。</span><span class="sxs-lookup"><span data-stu-id="464f8-211">Once the virtual machine is protected with a policy, it shows up under the **Protected Items** tab with the status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="464f8-212">根據預設，第一個排定的備份是 *初始備份*。</span><span class="sxs-lookup"><span data-stu-id="464f8-212">By default, the first scheduled backup is the *initial backup*.</span></span>

<span data-ttu-id="464f8-213">若要在設定保護之後立即觸發初始備份：</span><span class="sxs-lookup"><span data-stu-id="464f8-213">To trigger the initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="464f8-214">在 [受保護的項目] 頁面底部，按一下 [立即備份]。</span><span class="sxs-lookup"><span data-stu-id="464f8-214">At the bottom of the **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="464f8-215">Azure 備份服務會初始備份作業建立備份工作。</span><span class="sxs-lookup"><span data-stu-id="464f8-215">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="464f8-216">按一下 [工作]  索引標籤來檢視工作清單。</span><span class="sxs-lookup"><span data-stu-id="464f8-216">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![備份進行中](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="464f8-218">在備份作業期間，Azure 備份服務會發出命令給每個虛擬機器中的備份擴充功能，以排清所有寫入工作並取得一致的快照。</span><span class="sxs-lookup"><span data-stu-id="464f8-218">During the backup operation, the Azure Backup service issues a command to the backup extension in each virtual machine to flush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="464f8-219">初始備份完成後，[受保護的項目] 索引標籤中的虛擬機器狀態會顯示為 [受保護]。</span><span class="sxs-lookup"><span data-stu-id="464f8-219">When the initial backup finishes, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

![搭配復原點備份虛擬機器](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="464f8-221">檢視備份狀態和詳細資料</span><span class="sxs-lookup"><span data-stu-id="464f8-221">Viewing backup status and details</span></span>
<span data-ttu-id="464f8-222">虛擬機器受到保護後，[ **儀表板** ] 頁面摘要中的虛擬機器計數也會遞增。</span><span class="sxs-lookup"><span data-stu-id="464f8-222">Once protected, the virtual machine count also increases in the **Dashboard** page summary.</span></span> <span data-ttu-id="464f8-223">[儀表板] 頁面也會顯示過去 24 小時內「成功」、「失敗」及「進行中」的作業數目。</span><span class="sxs-lookup"><span data-stu-id="464f8-223">The **Dashboard** page also shows the number of jobs from the last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="464f8-224">在 [作業] 頁面上，使用 [狀態]、[作業]，或 [從] 和 [至] 功能表來篩選作業。</span><span class="sxs-lookup"><span data-stu-id="464f8-224">On the **Jobs** page, use the **Status**, **Operation**, or **From** and **To** menus to filter the jobs.</span></span>

![儀表板頁面中的備份狀態](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="464f8-226">儀表板中的值會每隔 24 小時重新整理一次。</span><span class="sxs-lookup"><span data-stu-id="464f8-226">Values in the dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="464f8-227">錯誤疑難排解</span><span class="sxs-lookup"><span data-stu-id="464f8-227">Troubleshooting errors</span></span>
<span data-ttu-id="464f8-228">如果您在備份虛擬機器時遇到問題，請參閱 [VM 疑難排解文章](backup-azure-vms-troubleshoot.md) 以取得說明。</span><span class="sxs-lookup"><span data-stu-id="464f8-228">If you run into issues while backing up your virtual machine, look at the [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="464f8-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="464f8-229">Next steps</span></span>
* [<span data-ttu-id="464f8-230">管理和監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="464f8-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="464f8-231">還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="464f8-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
