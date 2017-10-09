---
title: "aaaAzure VM 備份常見問題集 |Microsoft 文件"
description: "關於回答 toocommon 問題： 如何與 Azure VM 備份的運作方式、 限制和功能會變更 toopolicy 發生的時機"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "azure vm 備份, azure vm 還原, 備份原則"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a><span data-ttu-id="5389f-104">Hello Azure VM 備份服務有關的問題</span><span class="sxs-lookup"><span data-stu-id="5389f-104">Questions about hello Azure VM Backup service</span></span>
<span data-ttu-id="5389f-105">這篇文章有解答 toocommon 問題 toohelp 快速了解 hello Azure VM 備份的元件。</span><span class="sxs-lookup"><span data-stu-id="5389f-105">This article has answers toocommon questions toohelp you quickly understand hello Azure VM Backup components.</span></span> <span data-ttu-id="5389f-106">在某些 hello 解答，會有連結 toohello 文件具有完整的資訊。</span><span class="sxs-lookup"><span data-stu-id="5389f-106">In some of hello answers, there are links toohello articles that have comprehensive information.</span></span> <span data-ttu-id="5389f-107">您也可以張貼疑問 hello Azure 備份服務在 hello[討論區論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)。</span><span class="sxs-lookup"><span data-stu-id="5389f-107">You can also post questions about hello Azure Backup service in hello [discussion forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).</span></span>

## <a name="configure-backup"></a><span data-ttu-id="5389f-108">設定備份</span><span class="sxs-lookup"><span data-stu-id="5389f-108">Configure backup</span></span>
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a><span data-ttu-id="5389f-109">復原服務保存庫是否支援傳統 VM 或以 Resource Manager 為基礎的 VM？</span><span class="sxs-lookup"><span data-stu-id="5389f-109">Do Recovery Services vaults support classic VMs or Resource Manager based VMs?</span></span> <br/>
<span data-ttu-id="5389f-110">復原服務保存庫支援兩種模式。</span><span class="sxs-lookup"><span data-stu-id="5389f-110">Recovery Services vaults support both models.</span></span>  <span data-ttu-id="5389f-111">您可以備份傳統 VM （hello 傳統入口網站中建立） 或 （在 hello Azure 入口網站中建立） 的資源管理員 VM tooa 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="5389f-111">You can back up a classic VM (created in hello Classic portal), or a Resource Manager VM (created in hello Azure portal) tooa Recovery Services vault.</span></span>

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a><span data-ttu-id="5389f-112">Azure VM 備份不支援哪些組態？</span><span class="sxs-lookup"><span data-stu-id="5389f-112">What configurations are not supported by Azure VM backup ?</span></span>
<span data-ttu-id="5389f-113">請瀏覽[支援的作業系統](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup)和 [VM 備份的限制](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)</span><span class="sxs-lookup"><span data-stu-id="5389f-113">Please go through [Supported operating systems](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) and [Limitations of VM backup](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)</span></span>

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a><span data-ttu-id="5389f-114">在設定備份精靈中為何看不到我的 VM？</span><span class="sxs-lookup"><span data-stu-id="5389f-114">Why can't I see my VM in configure backup wizard?</span></span>
<span data-ttu-id="5389f-115">在「設定備份精靈」中，Azure 備份只會列出下列 VM：</span><span class="sxs-lookup"><span data-stu-id="5389f-115">In Configure backup wizard, Azure Backup only lists VMs which are:</span></span>
* <span data-ttu-id="5389f-116">尚未保護-您可以確認 hello 的 VM 的備份狀態移 tooVM 刀鋒視窗，然後檢查備份狀態設定 功能表中的 hello 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="5389f-116">Not already protected - You can verify hello backup status of a VM by going tooVM blade and checking on Backup status from Settings Menu of hello blade.</span></span> <span data-ttu-id="5389f-117">進一步了解如何太[檢查 VM 的備份狀態](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)</span><span class="sxs-lookup"><span data-stu-id="5389f-117">Learn more on how too[Check backup status of a VM](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)</span></span>
* <span data-ttu-id="5389f-118">作為 VM 所屬 toosame 區域</span><span class="sxs-lookup"><span data-stu-id="5389f-118">Belongs toosame region as VM</span></span>

## <a name="backup"></a><span data-ttu-id="5389f-119">備份</span><span class="sxs-lookup"><span data-stu-id="5389f-119">Backup</span></span>
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a><span data-ttu-id="5389f-120">隨選備份作業是否會遵循與排定備份相同的保留排程？</span><span class="sxs-lookup"><span data-stu-id="5389f-120">Will on-demand backup job follow same retention schedule as scheduled backups?</span></span>
<span data-ttu-id="5389f-121">否。</span><span class="sxs-lookup"><span data-stu-id="5389f-121">No.</span></span> <span data-ttu-id="5389f-122">視備份作業需要 toospecify hello 保留範圍。</span><span class="sxs-lookup"><span data-stu-id="5389f-122">You need toospecify hello retention range for an on-demand backup job.</span></span> <span data-ttu-id="5389f-123">根據預設，若從入口網站觸發，將會保留 30 天。</span><span class="sxs-lookup"><span data-stu-id="5389f-123">By default, it will be retained for 30 days when triggered from portal.</span></span> 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a><span data-ttu-id="5389f-124">我在最近一些 VM 上啟用了 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="5389f-124">I recently enabled Azure Disk Encryption on some VMs.</span></span> <span data-ttu-id="5389f-125">我的備份將會繼續 toowork 嗎？</span><span class="sxs-lookup"><span data-stu-id="5389f-125">Will my backups continue toowork?</span></span>
<span data-ttu-id="5389f-126">您需要 toogive 權限的 Azure 備份服務 tooaccess 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="5389f-126">You need toogive permissions for Azure Backup service tooaccess Key Vault.</span></span> <span data-ttu-id="5389f-127">您可以使用 [PowerShell](backup-azure-vms-automation.md) 文件的「啟用備份」一節中所述的步驟，在 PowerShell 中提供這些權限。</span><span class="sxs-lookup"><span data-stu-id="5389f-127">You can provide these permissions in PowerShell using steps mentioned in *Enable Backup* section of [PowerShell](backup-azure-vms-automation.md) documentation.</span></span>

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a><span data-ttu-id="5389f-128">我移轉 VM toomanaged 磁碟的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5389f-128">I migrated disks of a VM toomanaged disks.</span></span> <span data-ttu-id="5389f-129">我的備份將會繼續 toowork 嗎？</span><span class="sxs-lookup"><span data-stu-id="5389f-129">Will my backups continue toowork?</span></span>
<span data-ttu-id="5389f-130">[是]，備份一起順暢運作時並不需要 toore-設定備份。</span><span class="sxs-lookup"><span data-stu-id="5389f-130">Yes, backups work seamlessly and no need toore-configure backup.</span></span> 

## <a name="restore"></a><span data-ttu-id="5389f-131">還原</span><span class="sxs-lookup"><span data-stu-id="5389f-131">Restore</span></span>
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a><span data-ttu-id="5389f-132">如何在還原磁碟與完整 VM 還原之間做決定？</span><span class="sxs-lookup"><span data-stu-id="5389f-132">How do I decide between restoring disks versus full VM restore?</span></span>
<span data-ttu-id="5389f-133">將 Azure VM 完整還原視為快速建立已還原 VM 的一個選項。</span><span class="sxs-lookup"><span data-stu-id="5389f-133">Think of Azure full VM restore as a way of quick create option for restored VM.</span></span> <span data-ttu-id="5389f-134">VM 復原選項會變更 hello 名稱的磁碟、 磁碟、 公用 IP 位址、 網路介面來使用容器名稱的唯一性取得 VM 建立時建立的資源。它也不會加入 hello VM tooavailability 集合。</span><span class="sxs-lookup"><span data-stu-id="5389f-134">Restore VM option will change hello names of disks, containers used by disks,public IP addresses, network interface names for uniqueness of resources getting created as part of VM creation.It will also not add hello VM tooavailability set.</span></span> 

<span data-ttu-id="5389f-135">使用還原磁碟：</span><span class="sxs-lookup"><span data-stu-id="5389f-135">Use restore disks to:</span></span>
* <span data-ttu-id="5389f-136">自訂 hello 階段組態，例如變更 hello 大小從備份設定中的點，便會建立的 VM</span><span class="sxs-lookup"><span data-stu-id="5389f-136">Customize hello VM that gets created from point in time configuration like changing hello size from backup configuration</span></span>
* <span data-ttu-id="5389f-137">加入不存在於 hello 備份時的組態</span><span class="sxs-lookup"><span data-stu-id="5389f-137">Add configurations which are not present at hello time of backup</span></span> 
* <span data-ttu-id="5389f-138">取得建立資源的控制 hello 命名慣例</span><span class="sxs-lookup"><span data-stu-id="5389f-138">Control hello naming convention for resources getting created</span></span>
* <span data-ttu-id="5389f-139">新增 VM tooavailability 組</span><span class="sxs-lookup"><span data-stu-id="5389f-139">Add VM tooavailability set</span></span>
* <span data-ttu-id="5389f-140">您擁有只使用 PowerShell/宣告式範本定義即可達成的組態</span><span class="sxs-lookup"><span data-stu-id="5389f-140">You have any configuration which can be achieved only using PowerShell/a declarative template definition</span></span>

## <a name="manage-vm-backups"></a><span data-ttu-id="5389f-141">管理 VM 備份</span><span class="sxs-lookup"><span data-stu-id="5389f-141">Manage VM backups</span></span>
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a><span data-ttu-id="5389f-142">變更 VM 的備份原則時會發生什麼狀況？</span><span class="sxs-lookup"><span data-stu-id="5389f-142">What happens when I change a backup policy on VM(s)?</span></span>
<span data-ttu-id="5389f-143">在 VM 上套用新原則時，將遵守排程和保留 hello 新原則。</span><span class="sxs-lookup"><span data-stu-id="5389f-143">When a new policy is applied on VM(s), schedule and retention of hello new policy will be followed.</span></span> <span data-ttu-id="5389f-144">現有的復原點如果保留擴充，將會標示 tookeep 它們依據新的原則。</span><span class="sxs-lookup"><span data-stu-id="5389f-144">If retention is extended, existing recovery points will be marked tookeep them as per new policy.</span></span> <span data-ttu-id="5389f-145">保留會降低，如果它們標示為清除在 hello 下次執行清理工作，並將被刪除。</span><span class="sxs-lookup"><span data-stu-id="5389f-145">If retention is reduced, they are marked for pruning in hello next cleanup job and will be deleted.</span></span> 
