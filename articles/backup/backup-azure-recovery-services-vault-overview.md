---
title: "復原服務保存庫概觀 | Microsoft Docs"
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
ms.openlocfilehash: 19e2aafe3de106be32f3d90c63c0ea03c626f272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="recovery-services-vaults-overview"></a><span data-ttu-id="9dbfc-103">復原服務保存庫概觀</span><span class="sxs-lookup"><span data-stu-id="9dbfc-103">Recovery Services vaults overview</span></span>

<span data-ttu-id="9dbfc-104">本文說明復原服務保存庫的功能。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-104">This article describes the features of a Recovery Services vault.</span></span> <span data-ttu-id="9dbfc-105">復原服務保存庫是 Azure 中裝載資料的儲存體實體。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-105">A Recovery Services vault is a storage entity in Azure that houses data.</span></span> <span data-ttu-id="9dbfc-106">資料通常是資料的副本，或是虛擬機器 (VM)、工作負載、伺服器或工作站的設定資訊。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-106">The data is typically copies of data, or configuration information for virtual machines (VMs), workloads, servers, or workstations.</span></span> <span data-ttu-id="9dbfc-107">復原服務保存庫是 Resource Manager 版本的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-107">A Recovery Services vault is the Resource Manager version of a Backup vault.</span></span> <span data-ttu-id="9dbfc-108">Microsoft 鼓勵您使用復原服務保存庫，並將任何備份保存庫轉換成復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-108">Microsoft encourages you to use Recovery Services vaults, and to convert any Backup vaults to Recovery Services vaults.</span></span>

## <a name="what-is-a-recovery-services-vault"></a><span data-ttu-id="9dbfc-109">什麼是復原服務保存庫？</span><span class="sxs-lookup"><span data-stu-id="9dbfc-109">What is a Recovery Services vault?</span></span>

<span data-ttu-id="9dbfc-110">復原服務保存庫是 Azure 中的線上儲存實體，用來保存備份副本、復原點及備份原則等資料。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-110">A Recovery Services vault is an online storage entity in Azure used to hold data such as backup copies, recovery points, and backup policies.</span></span> <span data-ttu-id="9dbfc-111">您可以使用復原服務保存庫來保存各種 Azure 服務 (例如 IaaS VM (Linux 或 Windows) 和 Azure SQL Database) 的備份資料。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-111">You can use Recovery Services vaults to hold backup data for various Azure services such as IaaS VMs (Linux or Windows) and Azure SQL databases.</span></span> <span data-ttu-id="9dbfc-112">復原服務保存庫支援 System Center DPM、Windows Server、Azure 備份伺服器等等。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-112">Recovery Services vaults support System Center DPM, Windows Server, Azure Backup Server, and more.</span></span> <span data-ttu-id="9dbfc-113">復原服務保存庫可輕鬆地組織您的備份資料，同時可減輕管理負擔。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-113">Recovery Services vaults make it easy to organize your backup data, while minimizing management overhead.</span></span>

<span data-ttu-id="9dbfc-114">您可以在訂用帳戶內建立所需數量的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-114">Within an Azure subscription, you can create as many Recovery Services vaults as you like.</span></span>

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a><span data-ttu-id="9dbfc-115">比較復原服務保存庫與備份保存庫</span><span class="sxs-lookup"><span data-stu-id="9dbfc-115">Comparing Recovery Services vaults and Backup vaults</span></span>

<span data-ttu-id="9dbfc-116">復原服務保存庫是以 Azure 的 Azure Resource Manager 模型作為基礎，而備份保存庫則是以 Azure Service Manager 模型為作為基礎。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-116">Recovery Services vaults are based on the Azure Resource Manager model of Azure, whereas Backup vaults are based on the Azure Service Manager model.</span></span> <span data-ttu-id="9dbfc-117">當您將備份保存庫升級至復原服務保存庫時，備份資料在升級程序期間及升級程序之後都會維持不變。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-117">When you upgrade a Backup vault to a Recovery Services vault, the backup data remains intact during and after the upgrade process.</span></span> <span data-ttu-id="9dbfc-118">復原服務保存庫可提供備份保存庫無法使用的功能，例如︰</span><span class="sxs-lookup"><span data-stu-id="9dbfc-118">Recovery Services vaults provide features not available for Backup vaults, such as:</span></span>

- <span data-ttu-id="9dbfc-119">**可協助保護備份資料安全的增強功能**︰透過復原服務保存庫，Azure 備份能提供安全性功能來保護雲端備份。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-119">**Enhanced capabilities to help secure backup data**: With Recovery Services vaults, Azure Backup provides security capabilities to protect cloud backups.</span></span> <span data-ttu-id="9dbfc-120">這些安全性功能可確保您能保護您的備份，並安全地從雲端備份將資料復原，即使生產和備份伺服器遭到入侵也一樣。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-120">These security features ensure that you can secure your backups, and safely recover data from cloud backups even if production and backup servers are compromised.</span></span> [<span data-ttu-id="9dbfc-121">深入了解</span><span class="sxs-lookup"><span data-stu-id="9dbfc-121">Learn more</span></span>](backup-azure-security-feature.md)

- <span data-ttu-id="9dbfc-122">**將您的混合式 IT 環境集中監視**︰透過復原服務保存庫，您不只可以監視 [Azure IaaS VM](backup-azure-manage-vms.md)，還可以從中央入口網站監視[內部部署資產](backup-azure-manage-windows-server.md#manage-backup-items)。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-122">**Central monitoring for your hybrid IT environment**: With Recovery Services vaults, you can monitor not only your [Azure IaaS VMs](backup-azure-manage-vms.md) but also your [on-premises assets](backup-azure-manage-windows-server.md#manage-backup-items) from a central portal.</span></span> [<span data-ttu-id="9dbfc-123">深入了解</span><span class="sxs-lookup"><span data-stu-id="9dbfc-123">Learn more</span></span>](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- <span data-ttu-id="9dbfc-124">**角色型存取控制 (RBAC)**：RBAC 提供 Azure 中的更細緻存取權管理。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-124">**Role-Based Access Control (RBAC)**: RBAC provides fine-grained access management control in Azure.</span></span> <span data-ttu-id="9dbfc-125">[Azure 提供各種內建角色](../active-directory/role-based-access-built-in-roles.md)，且 Azure Backup 有三個[內建的角色可用來管理復原點](backup-rbac-rs-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-125">[Azure provides various built-in roles](../active-directory/role-based-access-built-in-roles.md), and Azure Backup has three [built-in roles to manage recovery points](backup-rbac-rs-vault.md).</span></span> <span data-ttu-id="9dbfc-126">復原服務保存庫與 RBAC 相容，且會對一組定義之使用者角色的備份和還原存取權限加以限制。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-126">Recovery Services vaults are compatible with RBAC, which restricts backup and restore access to the defined set of user roles.</span></span> [<span data-ttu-id="9dbfc-127">深入了解</span><span class="sxs-lookup"><span data-stu-id="9dbfc-127">Learn more</span></span>](backup-rbac-rs-vault.md)

- <span data-ttu-id="9dbfc-128">**保護 Azure 虛擬機器的所有設定**︰復原服務保存庫會保護以 Resource Manager 為基礎的 VM，包括進階磁碟、受控磁碟及加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-128">**Protect all configurations of Azure Virtual Machines**: Recovery Services vaults protect Resource Manager-based VMs including Premium Disks, Managed Disks, and Encrypted VMs.</span></span> <span data-ttu-id="9dbfc-129">將備份保存庫升級至復原服務保存庫，讓您有機會可將以 Service Manager 為基礎的 VM 升級至以 Resource Manager 為基礎的 VM。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-129">Upgrading a Backup vault to a Recovery Services vault gives you the opportunity to upgrade your Service Manager-based VMs to Resource Manager-based VMs.</span></span> <span data-ttu-id="9dbfc-130">在升級保存庫時，您可以保留以 Service Manager 為基礎的 VM 復原點，並設定已升級 (已啟用 Resource Manager) 的 VM 保護。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-130">While upgrading the vault, you can retain your Service Manager-based VM recovery points and configure protection for the upgraded (Resource Manager-enabled) VMs.</span></span> [<span data-ttu-id="9dbfc-131">深入了解</span><span class="sxs-lookup"><span data-stu-id="9dbfc-131">Learn more</span></span>](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- <span data-ttu-id="9dbfc-132">**IaaS VM 的立即還原**︰您可以使用復原服務保存庫，從 IaaS VM 還原檔案和資料夾，而非還原整個 VM，這樣可加速還原時間。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-132">**Instant restore for IaaS VMs**: Using Recovery Services vaults, you can restore files and folders from an IaaS VM without restoring the entire VM, which enables faster restore times.</span></span> <span data-ttu-id="9dbfc-133">IaaS VM 的立即還原適用於 Windows 和 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-133">Instant restore for IaaS VMs is available for both Windows and Linux VMs.</span></span> [<span data-ttu-id="9dbfc-134">深入了解</span><span class="sxs-lookup"><span data-stu-id="9dbfc-134">Learn more</span></span>](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-the-portal"></a><span data-ttu-id="9dbfc-135">在入口網站中管理復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="9dbfc-135">Managing your Recovery Services vaults in the portal</span></span>
<span data-ttu-id="9dbfc-136">建立和管理 Azure 入口網站中的復原服務保存庫很輕鬆，因為備份服務已整合至 [Azure 設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-136">Creation and management of Recovery Services vaults in the Azure portal is easy because the Backup service is integrated into the Azure Settings blade.</span></span> <span data-ttu-id="9dbfc-137">這項整合代表您可以在目標服務的內容中，建立或管理復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-137">This integration means you can create or manage a Recovery Services vault *in the context of the target service*.</span></span> <span data-ttu-id="9dbfc-138">例如，若要檢視 VM 的復原點，請加以選取，然後按一下 [設定] 刀鋒視窗中的 [備份]。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-138">For example, to view the recovery points for a VM, select it, and click **Backup** in the Settings blade.</span></span> <span data-ttu-id="9dbfc-139">隨即出現該 VM 特定的備份資訊。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-139">The backup information specific to that VM appears.</span></span> <span data-ttu-id="9dbfc-140">在下列範例中，**ContosoVM** 是虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-140">In the following example, **ContosoVM** is the name of the virtual machine.</span></span> <span data-ttu-id="9dbfc-141">**ContosoVM demovault** 是復原服務保存庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-141">**ContosoVM-demovault** is the name of the Recovery Services vault.</span></span> <span data-ttu-id="9dbfc-142">您不需要記住儲存復原點的復原服務保存庫名稱，您可以從虛擬機器存取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-142">You don't need to remember the name of the Recovery Services vault that stores the recovery points, you can access this information from the virtual machine.</span></span>  

![復原服務保存庫詳細資料 VM](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

<span data-ttu-id="9dbfc-144">如果使用相同的復原服務保存庫來保護多部伺服器，則查看復原服務保存庫可能更具邏輯。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-144">If multiple servers are protected using the same Recovery Services vault, it may be more logical to look at the Recovery Services vault.</span></span> <span data-ttu-id="9dbfc-145">您可以搜尋訂用帳戶中所有的復原服務保存庫，並從清單中選擇一個。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-145">You can search for all Recovery Services vaults in the subscription, and choose one from the list.</span></span>

<span data-ttu-id="9dbfc-146">下列各節所包含的文章連結，說明如何在每一個活動類型中使用復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="9dbfc-146">The following sections contain links to articles that explain how to use a Recovery Services vault in each type of activity.</span></span>

### <a name="back-up-data"></a><span data-ttu-id="9dbfc-147">備份資料</span><span class="sxs-lookup"><span data-stu-id="9dbfc-147">Back up data</span></span>
- [<span data-ttu-id="9dbfc-148">備份 Azure VM</span><span class="sxs-lookup"><span data-stu-id="9dbfc-148">Back up an Azure VM</span></span>](backup-azure-vms-first-look-arm.md)
- [<span data-ttu-id="9dbfc-149">備份 Windows Server 或 Windows 工作站</span><span class="sxs-lookup"><span data-stu-id="9dbfc-149">Back up Windows Server or Windows workstation</span></span>](backup-try-azure-backup-in-10-mins.md)
- [<span data-ttu-id="9dbfc-150">將 DPM 工作負載備份到 Azure</span><span class="sxs-lookup"><span data-stu-id="9dbfc-150">Back up DPM workloads to Azure</span></span>](backup-azure-dpm-introduction.md)
- [<span data-ttu-id="9dbfc-151">準備使用 Azure 備份伺服器來備份工作負載</span><span class="sxs-lookup"><span data-stu-id="9dbfc-151">Prepare to back up workloads using Azure Backup Server</span></span>](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a><span data-ttu-id="9dbfc-152">管理復原點</span><span class="sxs-lookup"><span data-stu-id="9dbfc-152">Manage recovery points</span></span>
- [<span data-ttu-id="9dbfc-153">管理 Azure VM 備份</span><span class="sxs-lookup"><span data-stu-id="9dbfc-153">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
- [<span data-ttu-id="9dbfc-154">管理檔案和資料夾</span><span class="sxs-lookup"><span data-stu-id="9dbfc-154">Managing files and folders</span></span>](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-the-vault"></a><span data-ttu-id="9dbfc-155">從保存庫還原資料</span><span class="sxs-lookup"><span data-stu-id="9dbfc-155">Restore data from the vault</span></span>
- [<span data-ttu-id="9dbfc-156">復原 Azure VM 中的個別檔案</span><span class="sxs-lookup"><span data-stu-id="9dbfc-156">Recover individual files from an Azure VM</span></span>](backup-azure-restore-files-from-vm.md)
- [<span data-ttu-id="9dbfc-157">還原 Azure VM</span><span class="sxs-lookup"><span data-stu-id="9dbfc-157">Restore an Azure VM</span></span>](backup-azure-arm-restore-vms.md)

### <a name="secure-the-vault"></a><span data-ttu-id="9dbfc-158">保護保存庫</span><span class="sxs-lookup"><span data-stu-id="9dbfc-158">Secure the vault</span></span>
- [<span data-ttu-id="9dbfc-159">保護復原服務保存庫中的雲端備份資料</span><span class="sxs-lookup"><span data-stu-id="9dbfc-159">Securing cloud backup data in Recovery Services vaults</span></span>](backup-azure-security-feature.md)



## <a name="next-steps"></a><span data-ttu-id="9dbfc-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9dbfc-160">Next Steps</span></span>
<span data-ttu-id="9dbfc-161">使用下列文章︰</span><span class="sxs-lookup"><span data-stu-id="9dbfc-161">Use the following article for:</span></span></br><span data-ttu-id="9dbfc-162">
[備份 IaaS VM](backup-azure-arm-vms-prepare.md)</span><span class="sxs-lookup"><span data-stu-id="9dbfc-162">
[Back up an IaaS VM](backup-azure-arm-vms-prepare.md)</span></span></br><span data-ttu-id="9dbfc-163">
[備份 Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="9dbfc-163">
[Back up an Azure Backup Server](backup-azure-microsoft-azure-backup.md)</span></span></br><span data-ttu-id="9dbfc-164">
[備份 Windows Server](backup-configure-vault.md)</span><span class="sxs-lookup"><span data-stu-id="9dbfc-164">
[Back up a Windows Server](backup-configure-vault.md)</span></span>
