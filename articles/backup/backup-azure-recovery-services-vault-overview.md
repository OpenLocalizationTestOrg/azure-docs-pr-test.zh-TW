---
title: "復原服務保存庫的 aaaOverview |Microsoft 文件"
description: "復原服務保存庫和 Azure 備份保存庫之間的概觀與比較。"
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a><span data-ttu-id="1b130-103">復原服務保存庫概觀</span><span class="sxs-lookup"><span data-stu-id="1b130-103">Recovery Services vaults overview</span></span>

<span data-ttu-id="1b130-104">本文說明復原服務保存庫的 hello 的功能。</span><span class="sxs-lookup"><span data-stu-id="1b130-104">This article describes hello features of a Recovery Services vault.</span></span> <span data-ttu-id="1b130-105">復原服務保存庫是 Azure 中裝載資料的儲存體實體。</span><span class="sxs-lookup"><span data-stu-id="1b130-105">A Recovery Services vault is a storage entity in Azure that houses data.</span></span> <span data-ttu-id="1b130-106">hello 資料通常是資料或虛擬機器 (Vm)、 工作負載、 伺服器或工作站的組態資訊的複本。</span><span class="sxs-lookup"><span data-stu-id="1b130-106">hello data is typically copies of data, or configuration information for virtual machines (VMs), workloads, servers, or workstations.</span></span> <span data-ttu-id="1b130-107">復原服務保存庫是備份保存庫 hello 資源管理員版本。</span><span class="sxs-lookup"><span data-stu-id="1b130-107">A Recovery Services vault is hello Resource Manager version of a Backup vault.</span></span> <span data-ttu-id="1b130-108">Microsoft 會鼓勵您 toouse 復原服務保存庫和 tooconvert 任何備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="1b130-108">Microsoft encourages you toouse Recovery Services vaults, and tooconvert any Backup vaults tooRecovery Services vaults.</span></span>

## <a name="what-is-a-recovery-services-vault"></a><span data-ttu-id="1b130-109">什麼是復原服務保存庫？</span><span class="sxs-lookup"><span data-stu-id="1b130-109">What is a Recovery Services vault?</span></span>

<span data-ttu-id="1b130-110">復原服務保存庫是在 Azure 中的線上存放區實體使用 toohold 資料，例如備份、 復原點，以及備份原則。</span><span class="sxs-lookup"><span data-stu-id="1b130-110">A Recovery Services vault is an online storage entity in Azure used toohold data such as backup copies, recovery points, and backup policies.</span></span> <span data-ttu-id="1b130-111">您可以使用 復原服務保存庫 toohold 備份資料的各種 Azure 服務，例如 IaaS Vm （Linux 或 Windows） 和 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="1b130-111">You can use Recovery Services vaults toohold backup data for various Azure services such as IaaS VMs (Linux or Windows) and Azure SQL databases.</span></span> <span data-ttu-id="1b130-112">復原服務保存庫支援 System Center DPM、Windows Server、Azure 備份伺服器等等。</span><span class="sxs-lookup"><span data-stu-id="1b130-112">Recovery Services vaults support System Center DPM, Windows Server, Azure Backup Server, and more.</span></span> <span data-ttu-id="1b130-113">復原服務保存庫讓您輕鬆 tooorganize 備份資料，可能降低管理負擔降到最低。</span><span class="sxs-lookup"><span data-stu-id="1b130-113">Recovery Services vaults make it easy tooorganize your backup data, while minimizing management overhead.</span></span>

<span data-ttu-id="1b130-114">您可以在訂用帳戶內建立所需數量的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="1b130-114">Within an Azure subscription, you can create as many Recovery Services vaults as you like.</span></span>

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a><span data-ttu-id="1b130-115">比較復原服務保存庫與備份保存庫</span><span class="sxs-lookup"><span data-stu-id="1b130-115">Comparing Recovery Services vaults and Backup vaults</span></span>

<span data-ttu-id="1b130-116">復原服務保存庫會 hello Azure Resource Manager 以模型為基礎的 Azure，而以 hello Azure Service Manager 模型為基礎的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="1b130-116">Recovery Services vaults are based on hello Azure Resource Manager model of Azure, whereas Backup vaults are based on hello Azure Service Manager model.</span></span> <span data-ttu-id="1b130-117">當您升級備份保存庫 tooa 復原服務保存庫時，hello 備份資料期間和之後 hello 升級程序會保持不變。</span><span class="sxs-lookup"><span data-stu-id="1b130-117">When you upgrade a Backup vault tooa Recovery Services vault, hello backup data remains intact during and after hello upgrade process.</span></span> <span data-ttu-id="1b130-118">復原服務保存庫可提供備份保存庫無法使用的功能，例如︰</span><span class="sxs-lookup"><span data-stu-id="1b130-118">Recovery Services vaults provide features not available for Backup vaults, such as:</span></span>

- <span data-ttu-id="1b130-119">**增強功能 toohelp 安全備份資料**： 與復原服務保存庫中，Azure 備份提供的安全性功能 tooprotect 雲端備份。</span><span class="sxs-lookup"><span data-stu-id="1b130-119">**Enhanced capabilities toohelp secure backup data**: With Recovery Services vaults, Azure Backup provides security capabilities tooprotect cloud backups.</span></span> <span data-ttu-id="1b130-120">這些安全性功能可確保您能保護您的備份，並安全地從雲端備份將資料復原，即使生產和備份伺服器遭到入侵也一樣。</span><span class="sxs-lookup"><span data-stu-id="1b130-120">These security features ensure that you can secure your backups, and safely recover data from cloud backups even if production and backup servers are compromised.</span></span> [<span data-ttu-id="1b130-121">深入了解</span><span class="sxs-lookup"><span data-stu-id="1b130-121">Learn more</span></span>](backup-azure-security-feature.md)

- <span data-ttu-id="1b130-122">**將您的混合式 IT 環境集中監視**︰透過復原服務保存庫，您不只可以監視 [Azure IaaS VM](backup-azure-manage-vms.md)，還可以從中央入口網站監視[內部部署資產](backup-azure-manage-windows-server.md#manage-backup-items)。</span><span class="sxs-lookup"><span data-stu-id="1b130-122">**Central monitoring for your hybrid IT environment**: With Recovery Services vaults, you can monitor not only your [Azure IaaS VMs](backup-azure-manage-vms.md) but also your [on-premises assets](backup-azure-manage-windows-server.md#manage-backup-items) from a central portal.</span></span> [<span data-ttu-id="1b130-123">深入了解</span><span class="sxs-lookup"><span data-stu-id="1b130-123">Learn more</span></span>](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- <span data-ttu-id="1b130-124">**角色型存取控制 (RBAC)**：RBAC 提供 Azure 中的更細緻存取權管理。</span><span class="sxs-lookup"><span data-stu-id="1b130-124">**Role-Based Access Control (RBAC)**: RBAC provides fine-grained access management control in Azure.</span></span> <span data-ttu-id="1b130-125">[Azure 提供的各種內建角色](../active-directory/role-based-access-built-in-roles.md)，且 Azure 備份具有三個[內建角色 toomanage 復原點](backup-rbac-rs-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="1b130-125">[Azure provides various built-in roles](../active-directory/role-based-access-built-in-roles.md), and Azure Backup has three [built-in roles toomanage recovery points](backup-rbac-rs-vault.md).</span></span> <span data-ttu-id="1b130-126">復原服務保存庫相容於 RBAC，限制備份和還原的使用者角色存取 toohello 定義集合。</span><span class="sxs-lookup"><span data-stu-id="1b130-126">Recovery Services vaults are compatible with RBAC, which restricts backup and restore access toohello defined set of user roles.</span></span> [<span data-ttu-id="1b130-127">深入了解</span><span class="sxs-lookup"><span data-stu-id="1b130-127">Learn more</span></span>](backup-rbac-rs-vault.md)

- <span data-ttu-id="1b130-128">**保護 Azure 虛擬機器的所有設定**︰復原服務保存庫會保護以 Resource Manager 為基礎的 VM，包括進階磁碟、受控磁碟及加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="1b130-128">**Protect all configurations of Azure Virtual Machines**: Recovery Services vaults protect Resource Manager-based VMs including Premium Disks, Managed Disks, and Encrypted VMs.</span></span> <span data-ttu-id="1b130-129">升級備份保存庫 tooa 復原服務保存庫可讓您的 Service Manager Vm tooResource Manager Vm hello 機會 tooupgrade。</span><span class="sxs-lookup"><span data-stu-id="1b130-129">Upgrading a Backup vault tooa Recovery Services vault gives you hello opportunity tooupgrade your Service Manager-based VMs tooResource Manager-based VMs.</span></span> <span data-ttu-id="1b130-130">升級 hello 保存庫，您可以保留您 Service Manager 架構的 VM 的復原點，並設定保護 hello 升級 （資源管理員已啟用） Vm。</span><span class="sxs-lookup"><span data-stu-id="1b130-130">While upgrading hello vault, you can retain your Service Manager-based VM recovery points and configure protection for hello upgraded (Resource Manager-enabled) VMs.</span></span> [<span data-ttu-id="1b130-131">深入了解</span><span class="sxs-lookup"><span data-stu-id="1b130-131">Learn more</span></span>](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- <span data-ttu-id="1b130-132">**IaaS Vm 的立即還原**： 使用 復原服務保存庫、 還原檔案和資料夾從 IaaS VM 而不還原 hello 整個 VM，可讓更快速的還原時間。</span><span class="sxs-lookup"><span data-stu-id="1b130-132">**Instant restore for IaaS VMs**: Using Recovery Services vaults, you can restore files and folders from an IaaS VM without restoring hello entire VM, which enables faster restore times.</span></span> <span data-ttu-id="1b130-133">IaaS VM 的立即還原適用於 Windows 和 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="1b130-133">Instant restore for IaaS VMs is available for both Windows and Linux VMs.</span></span> [<span data-ttu-id="1b130-134">深入了解</span><span class="sxs-lookup"><span data-stu-id="1b130-134">Learn more</span></span>](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a><span data-ttu-id="1b130-135">管理您的復原服務保存庫在 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="1b130-135">Managing your Recovery Services vaults in hello portal</span></span>
<span data-ttu-id="1b130-136">建立及管理在 hello Azure 入口網站中的 [復原服務保存庫的很簡單，因為 hello 備份服務已整合至 hello Azure 設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1b130-136">Creation and management of Recovery Services vaults in hello Azure portal is easy because hello Backup service is integrated into hello Azure Settings blade.</span></span> <span data-ttu-id="1b130-137">此整合意味著您可以建立或管理復原服務保存庫*hello hello 目標服務內容中*。</span><span class="sxs-lookup"><span data-stu-id="1b130-137">This integration means you can create or manage a Recovery Services vault *in hello context of hello target service*.</span></span> <span data-ttu-id="1b130-138">例如，tooview hello 復原點的 vm，加以選取，然後按一下**備份**hello 設定 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="1b130-138">For example, tooview hello recovery points for a VM, select it, and click **Backup** in hello Settings blade.</span></span> <span data-ttu-id="1b130-139">hello 備份資訊的特定 toothat VM 會出現。</span><span class="sxs-lookup"><span data-stu-id="1b130-139">hello backup information specific toothat VM appears.</span></span> <span data-ttu-id="1b130-140">在下列範例，hello **ContosoVM** hello hello 虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="1b130-140">In hello following example, **ContosoVM** is hello name of hello virtual machine.</span></span> <span data-ttu-id="1b130-141">**ContosoVM demovault** hello hello 復原服務保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="1b130-141">**ContosoVM-demovault** is hello name of hello Recovery Services vault.</span></span> <span data-ttu-id="1b130-142">您不需要 tooremember hello hello 復原服務保存庫名稱，儲存 hello 復原點，您可以從 hello 虛擬機器存取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="1b130-142">You don't need tooremember hello name of hello Recovery Services vault that stores hello recovery points, you can access this information from hello virtual machine.</span></span>  

![復原服務保存庫詳細資料 VM](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

<span data-ttu-id="1b130-144">如果使用 hello 保護多個伺服器相同的復原服務保存庫，它可能會在 hello 復原服務保存庫的多個邏輯 toolook。</span><span class="sxs-lookup"><span data-stu-id="1b130-144">If multiple servers are protected using hello same Recovery Services vault, it may be more logical toolook at hello Recovery Services vault.</span></span> <span data-ttu-id="1b130-145">您可以搜尋 hello 訂閱中的所有復原服務保存庫，並選擇 hello 清單其中一個。</span><span class="sxs-lookup"><span data-stu-id="1b130-145">You can search for all Recovery Services vaults in hello subscription, and choose one from hello list.</span></span>

<span data-ttu-id="1b130-146">hello 以下各節包含說明如何 toouse 復原服務保存庫中每一種活動的連結 tooarticles。</span><span class="sxs-lookup"><span data-stu-id="1b130-146">hello following sections contain links tooarticles that explain how toouse a Recovery Services vault in each type of activity.</span></span>

### <a name="back-up-data"></a><span data-ttu-id="1b130-147">備份資料</span><span class="sxs-lookup"><span data-stu-id="1b130-147">Back up data</span></span>
- [<span data-ttu-id="1b130-148">備份 Azure VM</span><span class="sxs-lookup"><span data-stu-id="1b130-148">Back up an Azure VM</span></span>](backup-azure-vms-first-look-arm.md)
- [<span data-ttu-id="1b130-149">備份 Windows Server 或 Windows 工作站</span><span class="sxs-lookup"><span data-stu-id="1b130-149">Back up Windows Server or Windows workstation</span></span>](backup-try-azure-backup-in-10-mins.md)
- [<span data-ttu-id="1b130-150">備份 DPM 工作負載 tooAzure</span><span class="sxs-lookup"><span data-stu-id="1b130-150">Back up DPM workloads tooAzure</span></span>](backup-azure-dpm-introduction.md)
- [<span data-ttu-id="1b130-151">準備使用 Azure 備份伺服器的工作負載備份 tooback</span><span class="sxs-lookup"><span data-stu-id="1b130-151">Prepare tooback up workloads using Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a><span data-ttu-id="1b130-152">管理復原點</span><span class="sxs-lookup"><span data-stu-id="1b130-152">Manage recovery points</span></span>
- [<span data-ttu-id="1b130-153">管理 Azure VM 備份</span><span class="sxs-lookup"><span data-stu-id="1b130-153">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
- [<span data-ttu-id="1b130-154">管理檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="1b130-154">Managing files and folders</span></span>](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a><span data-ttu-id="1b130-155">從 hello 保存庫還原資料</span><span class="sxs-lookup"><span data-stu-id="1b130-155">Restore data from hello vault</span></span>
- [<span data-ttu-id="1b130-156">復原 Azure VM 中的個別檔案</span><span class="sxs-lookup"><span data-stu-id="1b130-156">Recover individual files from an Azure VM</span></span>](backup-azure-restore-files-from-vm.md)
- [<span data-ttu-id="1b130-157">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="1b130-157">Restore an Azure VM</span></span>](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a><span data-ttu-id="1b130-158">安全 hello 保存庫</span><span class="sxs-lookup"><span data-stu-id="1b130-158">Secure hello vault</span></span>
- [<span data-ttu-id="1b130-159">保護復原服務保存庫中的雲端備份資料</span><span class="sxs-lookup"><span data-stu-id="1b130-159">Securing cloud backup data in Recovery Services vaults</span></span>](backup-azure-security-feature.md)



## <a name="next-steps"></a><span data-ttu-id="1b130-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b130-160">Next Steps</span></span>
<span data-ttu-id="1b130-161">使用下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b130-161">Use hello following article for:</span></span></br><span data-ttu-id="1b130-162">
[備份 IaaS VM](backup-azure-arm-vms-prepare.md)</span><span class="sxs-lookup"><span data-stu-id="1b130-162">
[Back up an IaaS VM](backup-azure-arm-vms-prepare.md)</span></span></br><span data-ttu-id="1b130-163">
[備份 Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="1b130-163">
[Back up an Azure Backup Server](backup-azure-microsoft-azure-backup.md)</span></span></br><span data-ttu-id="1b130-164">
[備份 Windows Server](backup-configure-vault.md)</span><span class="sxs-lookup"><span data-stu-id="1b130-164">
[Back up a Windows Server](backup-configure-vault.md)</span></span>
