---
title: "初步了解：使用備份保存庫備份 Azure VM | Microsoft Docs"
description: "使用 hello 傳統入口網站的 tooback Azure Vm tooa 備份保存庫註冊。 本教學課程說明包括建立 hello 備份保存庫、 註冊 hello Vm、 建立備份原則，以及執行 hello 初始備份作業的所有階段。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="33983-104">先睹為快：備份 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="33983-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33983-105">使用復原服務保存庫保護 VM</span><span class="sxs-lookup"><span data-stu-id="33983-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="33983-106">使用備份保存庫保護 Azure VM</span><span class="sxs-lookup"><span data-stu-id="33983-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="33983-107">本教學課程會帶領您完成備份 Azure 虛擬機器 (VM) tooa 備份保存庫在 Azure 中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="33983-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="33983-108">本文說明 hello 傳統模型或 Service Manager 部署模型，來備份 Vm。</span><span class="sxs-lookup"><span data-stu-id="33983-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="33983-109">hello 下列步驟適用於只能在 hello 傳統入口網站中建立的 tooBackup 保存庫。</span><span class="sxs-lookup"><span data-stu-id="33983-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="33983-110">Microsoft 建議針對新部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="33983-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="33983-111">如果您有興趣 VM tooa 復原服務保存庫所屬 tooa 資源群組的備份，請參閱[第一印象： 保護與復原服務保存庫的 Vm](backup-azure-vms-first-look-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="33983-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="33983-112">toosuccessfully 完成 hello 下列教學課程中，必須具有下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="33983-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="33983-113">您已在 Azure 訂用帳戶中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="33983-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="33983-114">hello VM 有連線能力 tooAzure 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="33983-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="33983-115">如需其他資訊，請參閱[網路連線](backup-azure-vms-prepare.md#network-connectivity)。</span><span class="sxs-lookup"><span data-stu-id="33983-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="33983-116">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="33983-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="33983-117">本教學課程適用於與 hello 傳統入口網站中建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33983-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="33983-118">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="33983-118">Create a backup vault</span></span>
<span data-ttu-id="33983-119">備份保存庫是儲存所有的 hello 備份和復原點已建立一段時間的實體。</span><span class="sxs-lookup"><span data-stu-id="33983-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="33983-120">hello 備份保存庫也包含 hello 套用的 toohello 虛擬機器進行備份的備份原則。</span><span class="sxs-lookup"><span data-stu-id="33983-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33983-121">從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="33983-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="33983-122">您可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="33983-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="33983-123">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="33983-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="33983-124">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="33983-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="33983-125">2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="33983-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="33983-126">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="33983-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="33983-127">所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="33983-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="33983-128">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="33983-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="33983-129">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="33983-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="33983-130">探索及註冊 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="33983-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="33983-131">向保存庫中的 hello VM，在執行之前 hello 探索程序 tooidentify 任何新的 Vm。</span><span class="sxs-lookup"><span data-stu-id="33983-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="33983-132">這會傳回 hello 訂用帳戶，以及其他資訊，例如 hello 雲端服務名稱和 hello 區域中的虛擬機器的清單。</span><span class="sxs-lookup"><span data-stu-id="33983-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="33983-133">登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="33983-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="33983-134">在 hello Azure 傳統入口網站，按一下 **復原服務**tooopen hello 清單的 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="33983-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="33983-135">![選取工作負載](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="33983-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="33983-136">從保存庫的 hello 清單中選取 hello 保存庫 tooback 將 vm。</span><span class="sxs-lookup"><span data-stu-id="33983-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="33983-137">當您選取您的保存庫時，會開啟 hello**快速入門**頁面</span><span class="sxs-lookup"><span data-stu-id="33983-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="33983-138">從 hello 保存庫功能表上，按一下 **註冊的項目**。</span><span class="sxs-lookup"><span data-stu-id="33983-138">From hello vault menu, click **Registered Items**.</span></span>

    ![選取工作負載](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="33983-140">從 hello**類型**功能表上，選取**Azure 虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="33983-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="33983-142">按一下**探索**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="33983-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="33983-143">![探索按鈕](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="33983-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="33983-144">hello 探索程序可能需要幾分鐘的時間 hello 虛擬機器會被製成資料表。</span><span class="sxs-lookup"><span data-stu-id="33983-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="33983-145">沒有在 hello 可讓您知道 hello 處理序正在執行的 hello 畫面下方的通知。</span><span class="sxs-lookup"><span data-stu-id="33983-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![探索 VM](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="33983-147">hello 程序完成時，就會變更 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="33983-147">hello notification changes when hello process is complete.</span></span>

    ![探索完成](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="33983-149">按一下**註冊**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="33983-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="33983-150">![註冊按鈕](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="33983-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="33983-151">在 hello**登錄項目**快顯功能表中，您想 tooregister 選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33983-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="33983-152">您可以同時註冊多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33983-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="33983-153">系統會為您所選取的每個虛擬機器建立一個工作。</span><span class="sxs-lookup"><span data-stu-id="33983-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="33983-154">按一下**檢視工作**在 hello 通知 toogo toohello**作業**頁面。</span><span class="sxs-lookup"><span data-stu-id="33983-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![註冊作業](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="33983-156">hello 虛擬機器也會出現在 hello 註冊項目清單，以及 hello 的 hello 註冊作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="33983-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![註冊狀態 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="33983-158">Hello 狀態 hello 作業完成時，變更 tooreflect hello*註冊*狀態。</span><span class="sxs-lookup"><span data-stu-id="33983-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![註冊狀態 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="33983-160">Hello 虛擬機器上安裝 VM 代理程式 hello</span><span class="sxs-lookup"><span data-stu-id="33983-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="33983-161">hello Azure VM 代理程式必須安裝在 Azure 虛擬機器以 hello 備份副檔名 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="33983-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="33983-162">如果您的 VM 建立從 hello Azure 組件庫，hello VM 代理程式已經存在於 hello VM;您可以再跳過[保護您的 Vm](backup-azure-vms-first-look.md#create-the-backup-policy)。</span><span class="sxs-lookup"><span data-stu-id="33983-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="33983-163">如果您的 VM 從內部部署資料中心，移轉 hello VM 可能沒有安裝 VM 代理程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="33983-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="33983-164">您必須安裝 VM 代理程式 hello hello 之前繼續 tooprotect hello VM 的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="33983-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="33983-165">如需安裝的詳細的步驟 hello VM 代理程式，請參閱 < hello [hello 備份 Vm 文章的 「 VM 代理程式 」 一節](backup-azure-vms-prepare.md#vm-agent)。</span><span class="sxs-lookup"><span data-stu-id="33983-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="33983-166">建立 hello 備份原則</span><span class="sxs-lookup"><span data-stu-id="33983-166">Create hello backup policy</span></span>
<span data-ttu-id="33983-167">產生備份快照集時，觸發 hello 初始備份作業之前，設定 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="33983-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="33983-168">hello 排程備份快照集所使用，以及這些快照集 hello 的時間長度會保留下來，為 hello 備份原則。</span><span class="sxs-lookup"><span data-stu-id="33983-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="33983-169">hello 保留資訊會取決於祖父-父親-son 備份旋轉配置。</span><span class="sxs-lookup"><span data-stu-id="33983-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="33983-170">瀏覽 toohello 下的備份保存庫**復原服務**在 hello Azure 傳統入口網站，然後按一下**註冊的項目**。</span><span class="sxs-lookup"><span data-stu-id="33983-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="33983-171">選取**Azure 虛擬機器**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="33983-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![在入口網站中選取工作負載](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="33983-173">按一下**保護**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="33983-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="33983-174">![按一下 [保護]](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="33983-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="33983-175">hello**保護的項目 」 精靈**隨即出現，並列出*只*註冊和未受保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33983-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![設定大規模保護](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="33983-177">選取您想 tooprotect hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33983-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="33983-178">如果有兩個或多個虛擬機器以 hello 相同名稱、 使用 hello 雲端服務 toodistinguish hello 的虛擬機器之間。</span><span class="sxs-lookup"><span data-stu-id="33983-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="33983-179">在 hello**設定保護**功能表選取現有的原則，或建立新的原則 tooprotect hello 虛擬機器，您所識別。</span><span class="sxs-lookup"><span data-stu-id="33983-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="33983-180">新的備份保存庫具有與 hello 保存庫相關聯的預設原則。</span><span class="sxs-lookup"><span data-stu-id="33983-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="33983-181">這項原則會每日快照集每個晚上，並會保留 30 天 hello 每日快照集。</span><span class="sxs-lookup"><span data-stu-id="33983-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="33983-182">每一個備份原則可以有多個相關聯的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="33983-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="33983-183">不過，hello 虛擬機器只能與一個原則相關聯一次。</span><span class="sxs-lookup"><span data-stu-id="33983-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![使用新的原則來保護](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="33983-185">備份原則包括 hello 排程備份的保留配置。</span><span class="sxs-lookup"><span data-stu-id="33983-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="33983-186">如果您選取現有的備份原則，您會無法 toomodify hello 保留選項 hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="33983-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="33983-187">在**保留範圍**定義 hello hello 特定備份點的每日、 每週、 每月和每年的範圍。</span><span class="sxs-lookup"><span data-stu-id="33983-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="33983-189">保留原則指定 hello 長度儲存備份的時間。</span><span class="sxs-lookup"><span data-stu-id="33983-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="33983-190">您可以指定 hello 備份時，根據不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="33983-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="33983-191">按一下**作業**tooview hello 清單**設定保護**作業。</span><span class="sxs-lookup"><span data-stu-id="33983-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![設定保護工作](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="33983-193">現在，您已建立 hello 原則，請移 toohello 下一個步驟，並執行 hello 初始備份。</span><span class="sxs-lookup"><span data-stu-id="33983-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="33983-194">初始備份</span><span class="sxs-lookup"><span data-stu-id="33983-194">Initial backup</span></span>
<span data-ttu-id="33983-195">一旦將虛擬機器已受保護原則，您可以檢視該關聯性上 hello**受保護項目** 索引標籤。Hello 初始備份發生之前，hello**保護狀態**顯示為**（暫止的初始備份） 的受保護-**。</span><span class="sxs-lookup"><span data-stu-id="33983-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="33983-196">根據預設，hello 第一個排定的備份是 hello*初始備份*。</span><span class="sxs-lookup"><span data-stu-id="33983-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![待備份](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="33983-198">toostart hello 初始備份現在：</span><span class="sxs-lookup"><span data-stu-id="33983-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="33983-199">在 hello**受保護項目**頁面上，按一下**立即備份**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="33983-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="33983-200">![[立即備份] 圖示](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="33983-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="33983-201">hello Azure 備份服務會建立 hello 初始備份作業的備份工作。</span><span class="sxs-lookup"><span data-stu-id="33983-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="33983-202">按一下 hello**作業**工作 索引標籤 tooview hello 清單。</span><span class="sxs-lookup"><span data-stu-id="33983-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![備份進行中](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="33983-204">當初始備份完成時，hello 虛擬機器在 hello hello 狀態**受保護項目** 索引標籤是*保護*。</span><span class="sxs-lookup"><span data-stu-id="33983-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="33983-206">備份虛擬機器是本機的程序。</span><span class="sxs-lookup"><span data-stu-id="33983-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="33983-207">您無法備份虛擬機器從一個區域 tooa 備份保存庫中另一個區域。</span><span class="sxs-lookup"><span data-stu-id="33983-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="33983-208">因此，為具有 Vm 需要 toobe 備份的每個 Azure 區域，必須建立至少一個備份保存庫在該區域中。</span><span class="sxs-lookup"><span data-stu-id="33983-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="33983-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33983-209">Next steps</span></span>
<span data-ttu-id="33983-210">現在您已成功備份 VM，接下來有幾個可能相關的步驟。</span><span class="sxs-lookup"><span data-stu-id="33983-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="33983-211">hello 最具邏輯步驟是 toofamiliarize 自行還原資料 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="33983-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="33983-212">不過，有管理工作，協助您了解如何 tookeep 安全資料和降低成本。</span><span class="sxs-lookup"><span data-stu-id="33983-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="33983-213">管理和監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="33983-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="33983-214">還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="33983-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="33983-215">疑難排解指引</span><span class="sxs-lookup"><span data-stu-id="33983-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="33983-216">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="33983-216">Questions?</span></span>
<span data-ttu-id="33983-217">如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="33983-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
