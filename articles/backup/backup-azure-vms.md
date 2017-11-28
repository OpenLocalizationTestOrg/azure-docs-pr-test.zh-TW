---
title: "傳統部署 Azure 虛擬機器 tooa 備份保存庫註冊 aaaBack |Microsoft 文件"
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
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="cfb50-104">備份 Azure 虛擬機器 (傳統入口網站)</span><span class="sxs-lookup"><span data-stu-id="cfb50-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cfb50-105">備份 Vm tooRecovery 服務保存庫</span><span class="sxs-lookup"><span data-stu-id="cfb50-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="cfb50-106">備份 Vm tooBackup 保存庫</span><span class="sxs-lookup"><span data-stu-id="cfb50-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="cfb50-107">本文章提供 hello 程序來備份傳統部署 Azure 虛擬機器 (VM) tooa 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="cfb50-108">有一些工作，您可以將 Azure 虛擬機器之前，需要 tootake 處置。</span><span class="sxs-lookup"><span data-stu-id="cfb50-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="cfb50-109">如果您尚未完成，同時 hello[必要條件](backup-azure-vms-prepare.md)tooprepare 環境以備份您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="cfb50-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="cfb50-110">如需詳細資訊，請參閱 hello 文件上[規劃 VM 備份基礎結構在 Azure 中的](backup-azure-vms-introduction.md)和[Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)。</span><span class="sxs-lookup"><span data-stu-id="cfb50-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="cfb50-111">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="cfb50-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cfb50-112">備份保存庫只能保護傳統部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="cfb50-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="cfb50-113">您無法使用備份保存庫保護 Resource Manager 部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="cfb50-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="cfb50-114">請參閱[備份 Vm tooRecovery 服務保存庫](backup-azure-arm-vms.md)如需詳細資訊，使用 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="cfb50-115">備份 Azure 虛擬機器需要三個主要步驟：</span><span class="sxs-lookup"><span data-stu-id="cfb50-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Azure IaaS vm 的三個步驟 tooback](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="cfb50-117">備份虛擬機器是本機的程序。</span><span class="sxs-lookup"><span data-stu-id="cfb50-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="cfb50-118">您無法備份一個區域 tooa 備份保存庫中另一個區域中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="cfb50-119">因此，您必須在每個 Azure 區域中建立備份保存庫，其中含有將備份的 VM。</span><span class="sxs-lookup"><span data-stu-id="cfb50-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="cfb50-120">從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="cfb50-121">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="cfb50-122">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="cfb50-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="cfb50-123">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="cfb50-124">2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="cfb50-125">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="cfb50-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="cfb50-126">所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="cfb50-127">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="cfb50-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="cfb50-128">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="cfb50-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="cfb50-129">步驟 1 - 探索 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cfb50-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="cfb50-130">tooensure 任何新虛擬機器 (Vm) 加入的 toohello 訂用帳戶後再註冊，識別執行 hello 探索程序。</span><span class="sxs-lookup"><span data-stu-id="cfb50-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="cfb50-131">hello 處理序會查詢 Azure hello hello 訂用帳戶，以及其他資訊中的虛擬機器清單，例如 hello 雲端服務名稱與 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="cfb50-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="cfb50-132">登入 toohello[傳統入口網站](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="cfb50-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="cfb50-133">在 hello 清單中的 Azure 服務，按一下 **復原服務**tooopen hello 份備份及 Site Recovery 保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="cfb50-134">![開啟保存庫清單](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="cfb50-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="cfb50-135">在備份保存庫的 hello 清單中，選取 hello 保存庫 tooback 將 vm。</span><span class="sxs-lookup"><span data-stu-id="cfb50-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="cfb50-136">如果這是新的保存庫 hello 入口網站開啟 toohello**快速入門**頁面。</span><span class="sxs-lookup"><span data-stu-id="cfb50-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![開啟已註冊的項目功能表](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="cfb50-138">如果先前已設定 hello 保存庫，hello 入口網站會開啟 toohello 最近使用的功能表。</span><span class="sxs-lookup"><span data-stu-id="cfb50-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="cfb50-139">從 hello （hello 頁面頂端的 hello） 的保存庫功能表上，按一下 **註冊的項目**。</span><span class="sxs-lookup"><span data-stu-id="cfb50-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![開啟已註冊的項目功能表](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="cfb50-141">從 hello**類型**功能表上，選取**Azure 虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="cfb50-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="cfb50-143">按一下**探索**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="cfb50-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="cfb50-144">![探索按鈕](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="cfb50-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="cfb50-145">hello 探索程序可能需要幾分鐘的時間 hello 虛擬機器會被製成資料表。</span><span class="sxs-lookup"><span data-stu-id="cfb50-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="cfb50-146">沒有在 hello 可讓您知道 hello 處理序正在執行的 hello 畫面下方的通知。</span><span class="sxs-lookup"><span data-stu-id="cfb50-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![探索 VM](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="cfb50-148">hello 程序完成時，就會變更 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="cfb50-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="cfb50-149">如果 hello 探索程序找不到 hello 虛擬機器，先確認 hello Vm 存在。</span><span class="sxs-lookup"><span data-stu-id="cfb50-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="cfb50-150">如果 hello Vm 存在，請確定 hello Vm 會在 hello 相同 hello 備份保存庫與區域。</span><span class="sxs-lookup"><span data-stu-id="cfb50-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="cfb50-151">如果 hello Vm 存在，而且是在 hello 相同的區域，請確定 hello Vm 還不是已註冊的 tooa 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="cfb50-152">如果 VM 是指派的 tooa 備份保存庫不是指派的可用 toobe tooother 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="cfb50-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![探索完成](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="cfb50-154">一旦您已經探索 hello 新項目，請移 tooStep 2，並註冊您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="cfb50-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="cfb50-155">步驟 2 - 註冊 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cfb50-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="cfb50-156">註冊 Azure 虛擬機器 tooassociate 它以 hello Azure 備份服務。</span><span class="sxs-lookup"><span data-stu-id="cfb50-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="cfb50-157">這通常是一次性活動。</span><span class="sxs-lookup"><span data-stu-id="cfb50-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="cfb50-158">瀏覽 toohello 下的備份保存庫**復原服務**在 hello Azure 入口網站，然後按一下**註冊的項目**。</span><span class="sxs-lookup"><span data-stu-id="cfb50-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="cfb50-159">選取**Azure 虛擬機器**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="cfb50-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="cfb50-161">按一下**註冊**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="cfb50-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="cfb50-162">![註冊按鈕](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="cfb50-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="cfb50-163">在 hello**登錄項目**快顯功能表中，您想 tooregister 選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="cfb50-164">如果有兩個或多個虛擬機器與 hello 相同名稱，請使用 hello 雲端服務 toodistinguish 兩者之間。</span><span class="sxs-lookup"><span data-stu-id="cfb50-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="cfb50-165">您可以同時註冊多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="cfb50-166">系統會為您所選取的每個虛擬機器建立一個工作。</span><span class="sxs-lookup"><span data-stu-id="cfb50-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="cfb50-167">按一下**檢視工作**在 hello 通知 toogo toohello**作業**頁面。</span><span class="sxs-lookup"><span data-stu-id="cfb50-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![註冊作業](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="cfb50-169">hello 虛擬機器也會出現在 hello 註冊項目清單，以及 hello 的 hello 註冊作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="cfb50-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![註冊狀態 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="cfb50-171">Hello 狀態 hello 作業完成時，變更 tooreflect hello*註冊*狀態。</span><span class="sxs-lookup"><span data-stu-id="cfb50-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![註冊狀態 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="cfb50-173">步驟 3 - 保護 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cfb50-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="cfb50-174">現在您可以設定 hello 虛擬機器的備份和保留原則。</span><span class="sxs-lookup"><span data-stu-id="cfb50-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="cfb50-175">使用單一保護動作可以保護多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="cfb50-176">隨附於 2015 年之後建立的 azure 備份保存庫 hello 保存庫內建的預設原則。</span><span class="sxs-lookup"><span data-stu-id="cfb50-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="cfb50-177">這項預設原則會隨附 30 天預設保留和每日一次的備份排程。</span><span class="sxs-lookup"><span data-stu-id="cfb50-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="cfb50-178">瀏覽 toohello 下的備份保存庫**復原服務**在 hello Azure 入口網站，然後按一下**註冊的項目**。</span><span class="sxs-lookup"><span data-stu-id="cfb50-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="cfb50-179">選取**Azure 虛擬機器**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="cfb50-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![在入口網站中選取工作負載](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="cfb50-181">按一下**保護**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="cfb50-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="cfb50-182">hello**保護的項目 」 精靈**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cfb50-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="cfb50-183">hello 精靈只列出註冊和未受保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="cfb50-184">選取您想 tooprotect hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="cfb50-185">如果有兩個或多個虛擬機器與 hello 相同名稱，請使用 hello 雲端服務 toodistinguish hello 的虛擬機器之間。</span><span class="sxs-lookup"><span data-stu-id="cfb50-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="cfb50-186">您可以同時保護多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![設定大規模保護](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="cfb50-188">選擇**備份排程**tooback hello 您所選取的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="cfb50-189">您可以從現有的一組原則中挑選，或定義新的原則。</span><span class="sxs-lookup"><span data-stu-id="cfb50-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="cfb50-190">每一個備份原則可以有多個相關聯的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="cfb50-191">不過，hello 虛擬機器只能與一個原則，在任何給定時間點相關聯的時間。</span><span class="sxs-lookup"><span data-stu-id="cfb50-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![使用新的原則來保護](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="cfb50-193">備份原則包括 hello 排程備份的保留配置。</span><span class="sxs-lookup"><span data-stu-id="cfb50-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="cfb50-194">如果您選取現有的備份原則，您無法修改 hello 下一個步驟中的 hello 保留選項。</span><span class="sxs-lookup"><span data-stu-id="cfb50-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="cfb50-195">選擇**保留範圍**tooassociate hello 備份。</span><span class="sxs-lookup"><span data-stu-id="cfb50-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![使用彈性保留來保護](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="cfb50-197">保留原則指定 hello 長度儲存備份的時間。</span><span class="sxs-lookup"><span data-stu-id="cfb50-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="cfb50-198">您可以指定 hello 備份時，根據不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="cfb50-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="cfb50-199">例如，每日取得的備份點 (可充當作業復原點) 可能會保留 90 天。</span><span class="sxs-lookup"><span data-stu-id="cfb50-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="cfb50-200">相較之下，在 hello （基於稽核目的） 每季結束時採取的備份點可能需要 toobe 保留多個月或年。</span><span class="sxs-lookup"><span data-stu-id="cfb50-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="cfb50-202">在此範例影像中：</span><span class="sxs-lookup"><span data-stu-id="cfb50-202">In this example image:</span></span>

   * <span data-ttu-id="cfb50-203">**每日的保留原則**：每日所進行的備份會儲存 30 天。</span><span class="sxs-lookup"><span data-stu-id="cfb50-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="cfb50-204">**每週的保留原則**：每個星期日所進行的備份會保留 104 週。</span><span class="sxs-lookup"><span data-stu-id="cfb50-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="cfb50-205">**每月保留原則**: hello 進行每個月的最後一個星期日的備份會保留 120 個月。</span><span class="sxs-lookup"><span data-stu-id="cfb50-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="cfb50-206">**每年保留原則**: hello 進行的每個月的第一個星期日的備份保留 99 年。</span><span class="sxs-lookup"><span data-stu-id="cfb50-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="cfb50-207">作業會建立 tooconfigure hello 保護原則，並將每個您所選取的虛擬機器的 hello 虛擬機器 toothat 原則產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cfb50-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="cfb50-208">tooview hello 清單**設定保護**工作，從 hello 保存庫功能表上，按一下**作業**選取**設定保護**從 hello**作業**篩選器。</span><span class="sxs-lookup"><span data-stu-id="cfb50-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![設定保護工作](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="cfb50-210">初始備份</span><span class="sxs-lookup"><span data-stu-id="cfb50-210">Initial backup</span></span>
<span data-ttu-id="cfb50-211">一旦原則受到 hello 虛擬機器，就會顯示在 [hello**受保護項目**hello 狀態] 索引標籤*（暫止的初始備份） 的受保護-*。</span><span class="sxs-lookup"><span data-stu-id="cfb50-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="cfb50-212">根據預設，hello 第一個排定的備份是 hello*初始備份*。</span><span class="sxs-lookup"><span data-stu-id="cfb50-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="cfb50-213">tootrigger hello 初始的備份設定保護之後，立即：</span><span class="sxs-lookup"><span data-stu-id="cfb50-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="cfb50-214">在 hello 底部 hello**受保護項目**頁面上，按一下**立即備份**。</span><span class="sxs-lookup"><span data-stu-id="cfb50-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="cfb50-215">hello Azure 備份服務會建立 hello 初始備份作業的備份工作。</span><span class="sxs-lookup"><span data-stu-id="cfb50-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="cfb50-216">按一下 hello**作業**工作 索引標籤 tooview hello 清單。</span><span class="sxs-lookup"><span data-stu-id="cfb50-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![備份進行中](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="cfb50-218">Hello 備份作業期間，hello Azure 備份服務發出的命令 toohello 備份擴充功能中每個虛擬機器 tooflush 所有寫入作業，並採取一致的快照集。</span><span class="sxs-lookup"><span data-stu-id="cfb50-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="cfb50-219">Hello 初始備份完成時，在 hello hello 虛擬機器 hello 狀態**受保護項目** 索引標籤是*保護*。</span><span class="sxs-lookup"><span data-stu-id="cfb50-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![搭配復原點備份虛擬機器](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="cfb50-221">檢視備份狀態和詳細資料</span><span class="sxs-lookup"><span data-stu-id="cfb50-221">Viewing backup status and details</span></span>
<span data-ttu-id="cfb50-222">受保護，一旦 hello 虛擬機器計數也會增加在 hello**儀表板**摘要頁面。</span><span class="sxs-lookup"><span data-stu-id="cfb50-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="cfb50-223">hello**儀表板**頁面也會顯示 hello 的 hello 過去 24 小時的作業數目*成功*，有*失敗*，而且*正在*.</span><span class="sxs-lookup"><span data-stu-id="cfb50-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="cfb50-224">在 hello**作業**頁面上，使用 hello**狀態**，**作業**，或**從**和**至**功能表 toofilterhello 作業。</span><span class="sxs-lookup"><span data-stu-id="cfb50-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![儀表板頁面中的備份狀態](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="cfb50-226">Hello 儀表板中的值，就會重新整理一次每隔 24 小時。</span><span class="sxs-lookup"><span data-stu-id="cfb50-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="cfb50-227">錯誤疑難排解</span><span class="sxs-lookup"><span data-stu-id="cfb50-227">Troubleshooting errors</span></span>
<span data-ttu-id="cfb50-228">如果您註冊您的虛擬機器執行備份時的問題，請查看 hello [VM 疑難排解文章](backup-azure-vms-troubleshoot.md)的說明。</span><span class="sxs-lookup"><span data-stu-id="cfb50-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfb50-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cfb50-229">Next steps</span></span>
* [<span data-ttu-id="cfb50-230">管理和監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cfb50-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="cfb50-231">還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cfb50-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
