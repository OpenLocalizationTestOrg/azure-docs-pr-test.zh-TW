---
title: "復原服務保存庫常見問題集 | Microsoft Docs"
description: "此版本的常見問題集支援公開預覽版本的 Azure 備份服務。 關於備份代理程式、備份和保留、復原、安全性，以及 Azure 備份解決方案其他常見問題的常見問題集答案。"
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
ms.openlocfilehash: e5ef305d926a57e32cdebd44f3dbe2185c735dd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="recovery-services-vault---faq"></a><span data-ttu-id="4b1b2-105">復原服務保存庫 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="4b1b2-105">Recovery Services vault - FAQ</span></span>
<span data-ttu-id="4b1b2-106">本文提供復原服務保存庫特有資訊，並補充說明 [Azure 備份常見問題集](backup-azure-backup-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-106">This article provides information specific to Recovery Services vault and it supplements the [Azure Backup FAQ](backup-azure-backup-faq.md).</span></span> <span data-ttu-id="4b1b2-107">Azure 備份常見問題集提供一組關於 Azure 備份服務的完整問答。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-107">The Azure Backup FAQ provides the full set of questions and answers about the Azure Backup service.</span></span>  

<span data-ttu-id="4b1b2-108">您可以在本文件或相關文件的 Disqus 一節中詢問有關 Azure 備份的問題。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-108">You can ask questions about Azure Backup in the Disqus section of this article or a related article.</span></span> <span data-ttu-id="4b1b2-109">您也可以在 [論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)中張貼有關 Azure 備份服務的問題。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-109">You can also post questions about the Azure Backup service in the [discussion forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).</span></span>

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a><span data-ttu-id="4b1b2-110">復原服務保存庫是以 Resource Manager 為基礎。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-110">Recovery Services vaults are Resource Manager based.</span></span> <span data-ttu-id="4b1b2-111">備份保存庫 (傳統模式) 是否仍受支援？</span><span class="sxs-lookup"><span data-stu-id="4b1b2-111">Are Backup vaults (classic mode) still supported?</span></span> <br/>
<span data-ttu-id="4b1b2-112">是，仍然支援備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-112">Yes, Backup vaults are still supported.</span></span> <span data-ttu-id="4b1b2-113">在 [傳統入口網站](https://manage.windowsazure.com)中建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-113">Create Backup vaults in the [Classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="4b1b2-114">在 [Azure 入口網站](https://portal.azure.com)中建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-114">Create Recovery Services vaults in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4b1b2-115">不過，強烈建議您建立復原服務保存庫，因為所有未來的增強功能僅可用於復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-115">However we strongly recommend you to create recovery services vault as all future enhancements will be available only in Recovery Services vault.</span></span>

## <a name="can-i-migrate-a-backup-vault-to-a-recovery-services-vault-br"></a><span data-ttu-id="4b1b2-116">是否可以將備份保存庫移轉至復原服務保存庫？</span><span class="sxs-lookup"><span data-stu-id="4b1b2-116">Can I migrate a Backup vault to a Recovery Services vault?</span></span> <br/>
<span data-ttu-id="4b1b2-117">很遺憾，不行，目前無法將備份保存庫的內容移轉至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-117">Unfortunately no, at this time you can't migrate the contents of a Backup vault to a Recovery Services vault.</span></span> <span data-ttu-id="4b1b2-118">我們正著手新增這項功能，但公開預覽中並未提供。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-118">We are working on adding this functionality, but it is not available as part of Public Preview.</span></span>

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a><span data-ttu-id="4b1b2-119">復原服務保存庫是否支援傳統 VM 或以 Resource Manager 為基礎的 VM？</span><span class="sxs-lookup"><span data-stu-id="4b1b2-119">Do Recovery Services vaults support classic VMs or Resource Manager based VMs?</span></span> <br/>
<span data-ttu-id="4b1b2-120">復原服務保存庫支援兩種模式。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-120">Recovery Services vaults support both models.</span></span>  <span data-ttu-id="4b1b2-121">您可以將傳統入口網站中建立的 VM (傳統模式 VM) 或 Azure 入口網站中建立的 VM (以 Resource Manager 為基礎) 備份至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-121">You can back up a VM created in the Classic portal (which are classic mode VMs), or a VM created in the Azure portal (which are Resource Manager based) to a Recovery Services vault.</span></span>

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-to-migrate-my-vms-from-classic-mode-to-resource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a><span data-ttu-id="4b1b2-122">我已在備份保存庫中備份傳統 VM。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-122">I have backed up my classic VMs in backup vault.</span></span> <span data-ttu-id="4b1b2-123">我現在想要將 VM 從傳統模式移轉至 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-123">Now I want to migrate my VMs from classic mode to Resource Manager mode.</span></span>  <span data-ttu-id="4b1b2-124">如何才能在復原服務保存庫中備份它們？</span><span class="sxs-lookup"><span data-stu-id="4b1b2-124">How Can I backup them in recovery services vault?</span></span>
<span data-ttu-id="4b1b2-125">當您將 VM 從傳統移轉至 Resource Manager 模式，備份保存庫中傳統 VM 的備份將不會自動移轉至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-125">Backups of classic VMs in backup vault won't migrate automatically to recovery services vault when you migrate the VMs from classic to Resource Manager mode.</span></span> <span data-ttu-id="4b1b2-126">請遵循下列步驟進行 VM 備份的移轉︰</span><span class="sxs-lookup"><span data-stu-id="4b1b2-126">Please follow these steps for migration of VM backups:</span></span>

1. <span data-ttu-id="4b1b2-127">在備份保存庫中，請移至 [受保護的項目]  索引標籤並選取 VM。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-127">In backup vault, go to **Protected Items** tab and select the VM.</span></span> <span data-ttu-id="4b1b2-128">按一下 [停止保護](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-128">Click on [Stop Protection](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines).</span></span> <span data-ttu-id="4b1b2-129">讓 [刪除相關聯的備份資料] 選項保持 [未核取] 狀態。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-129">Leave *Delete associated backup data* option **unchecked**.</span></span>
2. <span data-ttu-id="4b1b2-130">在 [Azure 入口網站](https://portal.azure.com)中，移至 VM 的[擴充] 功能表並將 **VMSnapshot/VMSnapshotLinux** 擴充功能解除安裝。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-130">In the [Azure portal](https://portal.azure.com), go to the **Extensions** menu for the VM and uninstall the **VMSnapshot/VMSnapshotLinux** extension.</span></span>
3. <span data-ttu-id="4b1b2-131">將虛擬機器從傳統模式移轉至 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-131">Migrate the virtual machine from classic mode to Resource Manager mode.</span></span> <span data-ttu-id="4b1b2-132">確定虛擬機器對應的儲存體和網路也會移轉至 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-132">Make sure that storage and network corresponding to virtual machine are also migrated to Resource Manager mode.</span></span>
4. <span data-ttu-id="4b1b2-133">建立復原服務保存庫，並利用保存庫儀表板上的 [備份]  動作，在移轉的虛擬機器上設定備份。</span><span class="sxs-lookup"><span data-stu-id="4b1b2-133">Create a recovery services vault and configure backup on the migrated virtual machine using **Backup** action on top of vault dashboard.</span></span> <span data-ttu-id="4b1b2-134">深入了解如何 [在復原服務保存庫中啟用備份](backup-azure-vms-first-look-arm.md)</span><span class="sxs-lookup"><span data-stu-id="4b1b2-134">Learn More on how to [enable backup in recovery services vault](backup-azure-vms-first-look-arm.md)</span></span>
