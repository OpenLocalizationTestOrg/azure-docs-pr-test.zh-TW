---
title: "初步了解：使用備份保存庫備份 Azure VM | Microsoft Docs"
description: "使用傳統入口網站將 Azure VM 備份至備份保存庫。 本教學課程說明包括建立備份保存庫、註冊 VM、建立備份原則和執行初始備份作業等所有階段。"
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
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="ea248-104">先睹為快：備份 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ea248-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea248-105">使用復原服務保存庫保護 VM</span><span class="sxs-lookup"><span data-stu-id="ea248-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="ea248-106">使用備份保存庫保護 Azure VM</span><span class="sxs-lookup"><span data-stu-id="ea248-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="ea248-107">本教學課程會帶領您逐步完成將 Azure 虛擬機器 (VM) 備份至 Azure 備份保存庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="ea248-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="ea248-108">這篇文章說明用來備份 VM 的傳統模型或 Service Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="ea248-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="ea248-109">下列步驟只適用於在傳統入口網站中建立的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="ea248-110">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="ea248-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="ea248-111">如果您有興趣將 VM 備份至屬於資源群組的復原服務保存庫，請參閱 [初步了解：使用復原服務保存庫保護 VM](backup-azure-vms-first-look-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="ea248-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="ea248-112">若要成功完成本教學課程，必須先滿足下列先決條件︰</span><span class="sxs-lookup"><span data-stu-id="ea248-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="ea248-113">您已在 Azure 訂用帳戶中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="ea248-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="ea248-114">VM 可連線到 Azure 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ea248-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="ea248-115">如需其他資訊，請參閱[網路連線](backup-azure-vms-prepare.md#network-connectivity)。</span><span class="sxs-lookup"><span data-stu-id="ea248-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="ea248-116">Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ea248-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ea248-117">本教學課程適用於在傳統入口網站中建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ea248-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="ea248-118">建立備份保存庫</span><span class="sxs-lookup"><span data-stu-id="ea248-118">Create a backup vault</span></span>
<span data-ttu-id="ea248-119">備份保存庫是一個實體，儲存隨著時間建立的所有備份和復原點。</span><span class="sxs-lookup"><span data-stu-id="ea248-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="ea248-120">備份保存庫也包含備份虛擬機器時將套用的備份原則。</span><span class="sxs-lookup"><span data-stu-id="ea248-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea248-121">從 2017 年 3 月開始，您無法再使用傳統入口網站來建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="ea248-122">您可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="ea248-123">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="ea248-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="ea248-124">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="ea248-125">在 2017 年 10 月 15 日之後，您就不能使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="ea248-126">**在 2017 年 11 月 1 日以前**：</span><span class="sxs-lookup"><span data-stu-id="ea248-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="ea248-127">所有其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="ea248-128">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="ea248-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="ea248-129">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="ea248-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="ea248-130">探索及註冊 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ea248-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="ea248-131">向保存庫註冊 VM 前，請執行探索程序以識別任何新的 VM。</span><span class="sxs-lookup"><span data-stu-id="ea248-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="ea248-132">這會傳回訂用帳戶中的虛擬機器清單以及其他資訊，例如雲端服務名稱和區域。</span><span class="sxs-lookup"><span data-stu-id="ea248-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="ea248-133">登入 [Azure 傳統入口網站](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="ea248-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="ea248-134">在 Azure 傳統入口網站中，按一下 [復原服務]  以開啟復原服務保存庫清單。</span><span class="sxs-lookup"><span data-stu-id="ea248-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="ea248-135">![選取工作負載](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="ea248-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="ea248-136">在保存庫清單中，選取要備份 VM 的保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="ea248-137">當您選取保存庫時，它會開啟在 [快速啟動]  頁面中</span><span class="sxs-lookup"><span data-stu-id="ea248-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="ea248-138">在保存庫功能表中，按一下 [已註冊的項目] 。</span><span class="sxs-lookup"><span data-stu-id="ea248-138">From the vault menu, click **Registered Items**.</span></span>

    ![選取工作負載](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="ea248-140">在 [類型] 功能表中選取 [Azure 虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="ea248-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![選取工作負載](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="ea248-142">按一下頁面底部的 [ **探索** ]。</span><span class="sxs-lookup"><span data-stu-id="ea248-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="ea248-143">![探索按鈕](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="ea248-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="ea248-144">在列表顯示虛擬機器時，探索程序可能需花費幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="ea248-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="ea248-145">畫面底部會有通知讓您知道程序正在執行中。</span><span class="sxs-lookup"><span data-stu-id="ea248-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![探索 VM](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="ea248-147">程序完成時，通知隨即變更。</span><span class="sxs-lookup"><span data-stu-id="ea248-147">The notification changes when the process is complete.</span></span>

    ![探索完成](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="ea248-149">按一下頁面底部的 [註冊]  。</span><span class="sxs-lookup"><span data-stu-id="ea248-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="ea248-150">![註冊按鈕](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="ea248-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="ea248-151">在 [註冊項目]  捷徑功能表中，選取您想要註冊的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ea248-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="ea248-152">您可以同時註冊多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ea248-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="ea248-153">系統會為您所選取的每個虛擬機器建立一個工作。</span><span class="sxs-lookup"><span data-stu-id="ea248-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="ea248-154">按一下通知中的 [檢視作業]，以移至 [作業] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ea248-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![註冊作業](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="ea248-156">虛擬機器也會連同註冊作業的狀態，出現在已註冊的項目清單中。</span><span class="sxs-lookup"><span data-stu-id="ea248-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![註冊狀態 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="ea248-158">作業完成時，狀態會改變以反映「已註冊」  狀態。</span><span class="sxs-lookup"><span data-stu-id="ea248-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![註冊狀態 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="ea248-160">在虛擬機器中安裝 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="ea248-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="ea248-161">Azure VM 代理程式必須安裝在 Azure 虛擬機器上，備份擴充功能才能運作。</span><span class="sxs-lookup"><span data-stu-id="ea248-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="ea248-162">如果 VM 是建立自 Azure 資源庫，則 VM 代理程式已存在於 VM；您可以跳到[保護您的 VM](backup-azure-vms-first-look.md#create-the-backup-policy)。</span><span class="sxs-lookup"><span data-stu-id="ea248-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="ea248-163">如果您的 VM 是從內部部署資料中心進行移轉，VM 可能還未安裝 VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="ea248-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="ea248-164">您必須先在虛擬機器上安裝 VM 代理程式，再繼續進行保護 VM。</span><span class="sxs-lookup"><span data-stu-id="ea248-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="ea248-165">如需安裝 VM 代理程式的詳細步驟，請參閱 [《備份 VM》文章的＜VM 代理程式＞一節](backup-azure-vms-prepare.md#vm-agent)。</span><span class="sxs-lookup"><span data-stu-id="ea248-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="ea248-166">建立備份原則</span><span class="sxs-lookup"><span data-stu-id="ea248-166">Create the backup policy</span></span>
<span data-ttu-id="ea248-167">觸發初始備份作業之前，請先設定備份快照擷取時間排程。</span><span class="sxs-lookup"><span data-stu-id="ea248-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="ea248-168">備份快照擷取時間排程以及快照保留時間長度是備份原則。</span><span class="sxs-lookup"><span data-stu-id="ea248-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="ea248-169">保留資訊是以 Grandfather-father-son 備份輪替配置為基礎。</span><span class="sxs-lookup"><span data-stu-id="ea248-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="ea248-170">在 Azure 傳統入口網站中，瀏覽至 [復原服務] 下的備份保存庫，然後按一下 [註冊的項目]。</span><span class="sxs-lookup"><span data-stu-id="ea248-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="ea248-171">從下拉式選單中選取 [Azure 虛擬機器]  。</span><span class="sxs-lookup"><span data-stu-id="ea248-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![在入口網站中選取工作負載](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="ea248-173">按一下頁面底部的 [保護]  。</span><span class="sxs-lookup"><span data-stu-id="ea248-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="ea248-174">![按一下 [保護]](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="ea248-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="ea248-175">[保護項目精靈] 隨即出現，並「只」列出已註冊但未受保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ea248-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![設定大規模保護](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="ea248-177">選取您要保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ea248-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="ea248-178">如果有兩個以上同名的虛擬機器，請使用雲端服務來區別虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ea248-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="ea248-179">在 [設定保護]  功能表上，選取現有原則或建立新原則，以保護您所識別的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ea248-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="ea248-180">新的備份保存庫擁有與保存庫相關聯的預設原則。</span><span class="sxs-lookup"><span data-stu-id="ea248-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="ea248-181">這項原則會在每晚擷取每日快照，並將每日快照保留 30 天。</span><span class="sxs-lookup"><span data-stu-id="ea248-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="ea248-182">每一個備份原則可以有多個相關聯的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ea248-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="ea248-183">但虛擬機器一次只能與一個原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="ea248-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![使用新的原則來保護](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="ea248-185">備份原則中包含排定備份的保留配置。</span><span class="sxs-lookup"><span data-stu-id="ea248-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="ea248-186">如果您選取現有的備份原則，將無法在下一個步驟中修改保留選項。</span><span class="sxs-lookup"><span data-stu-id="ea248-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="ea248-187">在 [保留範圍]  上，定義特定備份點的每日、每週、每月和每年範圍。</span><span class="sxs-lookup"><span data-stu-id="ea248-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="ea248-189">保留期原則會指定儲存備份的時間長度。</span><span class="sxs-lookup"><span data-stu-id="ea248-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="ea248-190">您可以根據進行備份的時間指定不同的保留原則。</span><span class="sxs-lookup"><span data-stu-id="ea248-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="ea248-191">按一下 [作業] 以檢視 [設定保護] 作業的清單。</span><span class="sxs-lookup"><span data-stu-id="ea248-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![設定保護工作](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="ea248-193">現在您已建立原則，接下來請移至下一個步驟，並執行初始備份。</span><span class="sxs-lookup"><span data-stu-id="ea248-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="ea248-194">初始備份</span><span class="sxs-lookup"><span data-stu-id="ea248-194">Initial backup</span></span>
<span data-ttu-id="ea248-195">在虛擬機器受到原則保護後，您可以在 [受保護項目]  索引標籤上檢視該關聯性。在執行初始備份前，[保護狀態] 會顯示為 [受保護 - (待執行初始備份)]。</span><span class="sxs-lookup"><span data-stu-id="ea248-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="ea248-196">根據預設，第一個排定的備份是 *初始備份*。</span><span class="sxs-lookup"><span data-stu-id="ea248-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![待備份](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="ea248-198">若要立即啟動初始備份︰</span><span class="sxs-lookup"><span data-stu-id="ea248-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="ea248-199">在 [受保護的項目] 頁面上，按一下頁面底部的 [立即備份]。</span><span class="sxs-lookup"><span data-stu-id="ea248-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="ea248-200">![[立即備份] 圖示](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="ea248-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="ea248-201">Azure 備份服務會初始備份作業建立備份工作。</span><span class="sxs-lookup"><span data-stu-id="ea248-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="ea248-202">按一下 [工作]  索引標籤來檢視工作清單。</span><span class="sxs-lookup"><span data-stu-id="ea248-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![備份進行中](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="ea248-204">初始備份完成後，[受保護的項目] 索引標籤中的虛擬機器狀態為 [受保護]。</span><span class="sxs-lookup"><span data-stu-id="ea248-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![搭配復原點備份虛擬機器](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="ea248-206">備份虛擬機器是本機的程序。</span><span class="sxs-lookup"><span data-stu-id="ea248-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="ea248-207">您無法將虛擬機器從一個區域備份到另一個區域中的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="ea248-208">因此，對於每一個有 VM 需要備份的 Azure 區域，必須在該區域中至少建立一個備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea248-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="ea248-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea248-209">Next steps</span></span>
<span data-ttu-id="ea248-210">現在您已成功備份 VM，接下來有幾個可能相關的步驟。</span><span class="sxs-lookup"><span data-stu-id="ea248-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="ea248-211">最合乎邏輯的步驟是讓自己熟悉如何將資料還原到 VM。</span><span class="sxs-lookup"><span data-stu-id="ea248-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="ea248-212">不過，也有能夠幫助您了解如何確保資料安全無虞以及將成本降至最低的管理工作。</span><span class="sxs-lookup"><span data-stu-id="ea248-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="ea248-213">管理和監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ea248-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="ea248-214">還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ea248-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="ea248-215">疑難排解指引</span><span class="sxs-lookup"><span data-stu-id="ea248-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="ea248-216">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="ea248-216">Questions?</span></span>
<span data-ttu-id="ea248-217">如果您有問題，或希望我們加入任何功能，請 [傳送意見反應給我們](http://aka.ms/azurebackup_feedback)。</span><span class="sxs-lookup"><span data-stu-id="ea248-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
