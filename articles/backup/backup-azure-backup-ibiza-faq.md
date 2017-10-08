---
title: "aaaRecovery 服務保存庫常見問題集 |Microsoft 文件"
description: "此版的 hello 常見問題集支援 hello 公用預覽版本 hello Azure 備份服務。 Hello 備份代理程式、 備份和保留、 復原、 安全性、 hello Azure 備份解決方案的其他常見問題的相關常見問題的解答 toofrequently。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份解決方案；備份服務"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a><span data-ttu-id="fba8a-105">復原服務保存庫 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="fba8a-105">Recovery Services vault - FAQ</span></span>
<span data-ttu-id="fba8a-106">這篇文章提供資訊特定 tooRecovery 服務保存庫，而且它補充 hello [Azure 備份常見問題集](backup-azure-backup-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="fba8a-106">This article provides information specific tooRecovery Services vault and it supplements hello [Azure Backup FAQ](backup-azure-backup-faq.md).</span></span> <span data-ttu-id="fba8a-107">hello Azure 備份常見問題集提供 hello 組完整的問與答 hello Azure 備份服務。</span><span class="sxs-lookup"><span data-stu-id="fba8a-107">hello Azure Backup FAQ provides hello full set of questions and answers about hello Azure Backup service.</span></span>  

<span data-ttu-id="fba8a-108">您可以詢問有關 Azure Backup 的問題 hello Disqus > 一節的這篇文章或相關文件中。</span><span class="sxs-lookup"><span data-stu-id="fba8a-108">You can ask questions about Azure Backup in hello Disqus section of this article or a related article.</span></span> <span data-ttu-id="fba8a-109">您也可以張貼疑問 hello Azure 備份服務在 hello[討論區論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)。</span><span class="sxs-lookup"><span data-stu-id="fba8a-109">You can also post questions about hello Azure Backup service in hello [discussion forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).</span></span>

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a><span data-ttu-id="fba8a-110">復原服務保存庫是以 Resource Manager 為基礎。</span><span class="sxs-lookup"><span data-stu-id="fba8a-110">Recovery Services vaults are Resource Manager based.</span></span> <span data-ttu-id="fba8a-111">備份保存庫 (傳統模式) 是否仍受支援？</span><span class="sxs-lookup"><span data-stu-id="fba8a-111">Are Backup vaults (classic mode) still supported?</span></span> <br/>
<span data-ttu-id="fba8a-112">是，仍然支援備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="fba8a-112">Yes, Backup vaults are still supported.</span></span> <span data-ttu-id="fba8a-113">建立備份保存庫中 hello[傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="fba8a-113">Create Backup vaults in hello [Classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="fba8a-114">建立復原服務保存庫中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="fba8a-114">Create Recovery Services vaults in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fba8a-115">但是我們強烈建議您 toocreate 復原服務保存庫做為所有未來的增強功能可只在復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="fba8a-115">However we strongly recommend you toocreate recovery services vault as all future enhancements will be available only in Recovery Services vault.</span></span>

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a><span data-ttu-id="fba8a-116">可以移轉備份保存庫 tooa 復原服務保存庫嗎？</span><span class="sxs-lookup"><span data-stu-id="fba8a-116">Can I migrate a Backup vault tooa Recovery Services vault?</span></span> <br/>
<span data-ttu-id="fba8a-117">不幸的是不可以，此時您無法移轉復原服務保存庫備份保存庫 tooa hello 內容。</span><span class="sxs-lookup"><span data-stu-id="fba8a-117">Unfortunately no, at this time you can't migrate hello contents of a Backup vault tooa Recovery Services vault.</span></span> <span data-ttu-id="fba8a-118">我們正著手新增這項功能，但公開預覽中並未提供。</span><span class="sxs-lookup"><span data-stu-id="fba8a-118">We are working on adding this functionality, but it is not available as part of Public Preview.</span></span>

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a><span data-ttu-id="fba8a-119">復原服務保存庫是否支援傳統 VM 或以 Resource Manager 為基礎的 VM？</span><span class="sxs-lookup"><span data-stu-id="fba8a-119">Do Recovery Services vaults support classic VMs or Resource Manager based VMs?</span></span> <br/>
<span data-ttu-id="fba8a-120">復原服務保存庫支援兩種模式。</span><span class="sxs-lookup"><span data-stu-id="fba8a-120">Recovery Services vaults support both models.</span></span>  <span data-ttu-id="fba8a-121">您可以備份在 hello 傳統入口網站 （此為傳統模式 Vm） 中建立的 VM，或在 hello Azure 入口網站 （此為基礎的資源管理員） 建立 VM tooa 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="fba8a-121">You can back up a VM created in hello Classic portal (which are classic mode VMs), or a VM created in hello Azure portal (which are Resource Manager based) tooa Recovery Services vault.</span></span>

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a><span data-ttu-id="fba8a-122">我已在備份保存庫中備份傳統 VM。</span><span class="sxs-lookup"><span data-stu-id="fba8a-122">I have backed up my classic VMs in backup vault.</span></span> <span data-ttu-id="fba8a-123">現在我想 toomigrate 我 Vm 從傳統模式 tooResource 管理員模式。</span><span class="sxs-lookup"><span data-stu-id="fba8a-123">Now I want toomigrate my VMs from classic mode tooResource Manager mode.</span></span>  <span data-ttu-id="fba8a-124">如何才能在復原服務保存庫中備份它們？</span><span class="sxs-lookup"><span data-stu-id="fba8a-124">How Can I backup them in recovery services vault?</span></span>
<span data-ttu-id="fba8a-125">備份的備份保存庫中的傳統 Vm 將不會移轉自動 toorecovery 服務保存庫傳統 tooResource 管理員模式下從移轉 hello Vm 時。</span><span class="sxs-lookup"><span data-stu-id="fba8a-125">Backups of classic VMs in backup vault won't migrate automatically toorecovery services vault when you migrate hello VMs from classic tooResource Manager mode.</span></span> <span data-ttu-id="fba8a-126">請遵循下列步驟進行 VM 備份的移轉︰</span><span class="sxs-lookup"><span data-stu-id="fba8a-126">Please follow these steps for migration of VM backups:</span></span>

1. <span data-ttu-id="fba8a-127">在備份保存庫，到太**受保護項目**索引標籤並選取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="fba8a-127">In backup vault, go too**Protected Items** tab and select hello VM.</span></span> <span data-ttu-id="fba8a-128">按一下 [停止保護](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="fba8a-128">Click on [Stop Protection](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines).</span></span> <span data-ttu-id="fba8a-129">讓 [刪除相關聯的備份資料] 選項保持 [未核取] 狀態。</span><span class="sxs-lookup"><span data-stu-id="fba8a-129">Leave *Delete associated backup data* option **unchecked**.</span></span>
2. <span data-ttu-id="fba8a-130">在 hello [Azure 入口網站](https://portal.azure.com)，go toohello**延伸**功能表 hello VM 和解除安裝 hello **VMSnapshot/VMSnapshotLinux**延伸模組。</span><span class="sxs-lookup"><span data-stu-id="fba8a-130">In hello [Azure portal](https://portal.azure.com), go toohello **Extensions** menu for hello VM and uninstall hello **VMSnapshot/VMSnapshotLinux** extension.</span></span>
3. <span data-ttu-id="fba8a-131">從傳統模式 tooResource 管理員模式移轉 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fba8a-131">Migrate hello virtual machine from classic mode tooResource Manager mode.</span></span> <span data-ttu-id="fba8a-132">請確定儲存體和網路對應 toovirtual 機器是讓同時移轉的 tooResource 管理員模式。</span><span class="sxs-lookup"><span data-stu-id="fba8a-132">Make sure that storage and network corresponding toovirtual machine are also migrated tooResource Manager mode.</span></span>
4. <span data-ttu-id="fba8a-133">建立復原服務保存庫和設定虛擬機器使用的備份在 hello 移轉**備份**在保存庫儀表板頂端的動作。</span><span class="sxs-lookup"><span data-stu-id="fba8a-133">Create a recovery services vault and configure backup on hello migrated virtual machine using **Backup** action on top of vault dashboard.</span></span> <span data-ttu-id="fba8a-134">進一步了解如何太[啟用復原服務保存庫中的備份](backup-azure-vms-first-look-arm.md)</span><span class="sxs-lookup"><span data-stu-id="fba8a-134">Learn More on how too[enable backup in recovery services vault](backup-azure-vms-first-look-arm.md)</span></span>
