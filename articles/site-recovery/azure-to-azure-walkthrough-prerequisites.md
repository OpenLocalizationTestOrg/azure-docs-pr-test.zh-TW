---
title: "啟動複寫的 Azure Vm tooanother 區域 aaaBefore |Microsoft 文件 '"
description: "摘要說明您之前使用 hello Azure Site Recovery 服務的 Azure 地區之間複寫 Azure Vm 需要 tootake hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a><span data-ttu-id="cd64f-103">步驟 2：開始之前</span><span class="sxs-lookup"><span data-stu-id="cd64f-103">Step 2: Before you start</span></span>

<span data-ttu-id="cd64f-104">您已檢閱過 hello 之後[架構](azure-to-azure-walkthrough-architecture.md)之間使用的 Azure 地區複寫 Azure 虛擬機器 (Vm) [Azure Site Recovery](site-recovery-overview.md)，使用此發行項 tooverify 必要條件。</span><span class="sxs-lookup"><span data-stu-id="cd64f-104">After you've reviewed hello [architecture](azure-to-azure-walkthrough-architecture.md) for replicating Azure virtual machines (VMs) between Azure regions with [Azure Site Recovery](site-recovery-overview.md), use this article tooverify prerequisites.</span></span> 

- <span data-ttu-id="cd64f-105">當您完成 hello 發行項時，您應該有明確的了解需要 toomake hello 部署什麼運作，而且已完成 hello 先決條件步驟。</span><span class="sxs-lookup"><span data-stu-id="cd64f-105">When you finish hello article, you should have a clear understanding of what's needed toomake hello deployment work, and have completed hello prerequisite steps.</span></span>
- <span data-ttu-id="cd64f-106">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="cd64f-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
>
> <span data-ttu-id="cd64f-107">Azure VM 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="cd64f-107">Azure VM replication is currently in preview.</span></span>



## <a name="support-recommendations"></a><span data-ttu-id="cd64f-108">支援建議</span><span class="sxs-lookup"><span data-stu-id="cd64f-108">Support recommendations</span></span>

<span data-ttu-id="cd64f-109">檢閱 hello 資料表下方。</span><span class="sxs-lookup"><span data-stu-id="cd64f-109">Review hello table below.</span></span>

<span data-ttu-id="cd64f-110">**元件**</span><span class="sxs-lookup"><span data-stu-id="cd64f-110">**Component**</span></span> | <span data-ttu-id="cd64f-111">**需求**</span><span class="sxs-lookup"><span data-stu-id="cd64f-111">**Requirement**</span></span>
--- | ---
<span data-ttu-id="cd64f-112">**復原服務保存庫**</span><span class="sxs-lookup"><span data-stu-id="cd64f-112">**Recovery Services vault**</span></span> | <span data-ttu-id="cd64f-113">我們建議您在 hello 目標的 toouse 災害的 Azure 區域中建立的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="cd64f-113">We recommend that you create a Recovery Services vault in hello target Azure region that you want toouse for disaster recovery.</span></span> <span data-ttu-id="cd64f-114">例如，如果您想在美國東部 tooCentral 美國 tooreplicate 來源 Vm，美國中部建立 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="cd64f-114">For example, if you want tooreplicate source VMs in East US tooCentral US, create hello vault in Central US.</span></span>
<span data-ttu-id="cd64f-115">**Azure 訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="cd64f-115">**Azure subscription**</span></span> | <span data-ttu-id="cd64f-116">您的 Azure 訂用帳戶應啟用的 toocreate Vm，您想為 hello 災害復原區域 toouse hello 目標位置中。</span><span class="sxs-lookup"><span data-stu-id="cd64f-116">Your Azure subscription should be enabled toocreate VMs, in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="cd64f-117">請連絡客戶支援 tooenable hello 必要的配額。</span><span class="sxs-lookup"><span data-stu-id="cd64f-117">Contact support tooenable hello required quota.</span></span>
<span data-ttu-id="cd64f-118">**目標區域產能**</span><span class="sxs-lookup"><span data-stu-id="cd64f-118">**Target region capacity**</span></span> | <span data-ttu-id="cd64f-119">Hello 目標 Azure 地區，hello 訂用帳戶必須具備足夠的容量以 Vm、 儲存體帳戶和網路元件。</span><span class="sxs-lookup"><span data-stu-id="cd64f-119">In hello target Azure region, hello subscription should have enough capacity for VMs, storage accounts, and network components.</span></span>
<span data-ttu-id="cd64f-120">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="cd64f-120">**Storage**</span></span> | <span data-ttu-id="cd64f-121">使用 hello[儲存體指引](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)為您的 Azure Vm，tooavoid 效能問題的來源。</span><span class="sxs-lookup"><span data-stu-id="cd64f-121">Use hello [storage guidance](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) for your source Azure VMs, tooavoid performance issues.</span></span><br/><br/> <span data-ttu-id="cd64f-122">儲存體帳戶必須在 hello 與 hello 保存庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="cd64f-122">Storage accounts must be in hello same region as hello vault.</span></span><br/><br/> <span data-ttu-id="cd64f-123">您無法複寫在中部和印度南部及印度 toopremium 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cd64f-123">You can't replicate toopremium accounts in Central and South India.</span></span><br/><br/> <span data-ttu-id="cd64f-124">如果您部署與 hello 預設設定進行複寫時，站台復原就會建立所需的 hello hello 來源設定為基礎的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cd64f-124">If you deploy replication with hello default settings, Site Recovery creates hello required storage accounts based on hello source configuration.</span></span> <span data-ttu-id="cd64f-125">如果您自訂設定，請遵循 hello [VM 磁碟的延展性目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)。</span><span class="sxs-lookup"><span data-stu-id="cd64f-125">If you customize settings, follow hello [scalability targets for VM disks](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).</span></span>
<span data-ttu-id="cd64f-126">**網路功能**</span><span class="sxs-lookup"><span data-stu-id="cd64f-126">**Networking**</span></span> | <span data-ttu-id="cd64f-127">您需要 tooallow 從 Azure Vm 的輸出連線的特定 Url/IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="cd64f-127">You need tooallow outbound connectivity from Azure VMs, for specific URLs/IP ranges.</span></span><br/><br/> <span data-ttu-id="cd64f-128">網路帳戶必須在 hello 與 hello 保存庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="cd64f-128">Network accounts must be in hello same region as hello vault.</span></span> 
<span data-ttu-id="cd64f-129">**Azure VM**</span><span class="sxs-lookup"><span data-stu-id="cd64f-129">**Azure VM**</span></span> | <span data-ttu-id="cd64f-130">請確定所有最新的根憑證 hello hello Windows/Linux 的 Azure VM 上。</span><span class="sxs-lookup"><span data-stu-id="cd64f-130">Make sure all of hello latest root certificates are on hello Windows/Linux Azure VM.</span></span> <span data-ttu-id="cd64f-131">如果他們不這樣做，您必須能夠 tooregister hello Site Recovery 中的 VM 由於安全性限制。</span><span class="sxs-lookup"><span data-stu-id="cd64f-131">If they're not, you won't be able tooregister hello VM in Site Recovery, because of security constraints.</span></span>
<span data-ttu-id="cd64f-132">**Azure 使用者帳戶**</span><span class="sxs-lookup"><span data-stu-id="cd64f-132">**Azure user account**</span></span> | <span data-ttu-id="cd64f-133">您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)tooenable 的 Azure 虛擬機器的複寫。</span><span class="sxs-lookup"><span data-stu-id="cd64f-133">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

<span data-ttu-id="cd64f-134">取得支援需求的完整清單，在 hello[支援矩陣](site-recovery-support-matrix-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="cd64f-134">Get a full list of support requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md)</span></span>


## <a name="set-permissions-on-hello-account"></a><span data-ttu-id="cd64f-135">Hello 帳戶上設定權限</span><span class="sxs-lookup"><span data-stu-id="cd64f-135">Set permissions on hello account</span></span>

1. <span data-ttu-id="cd64f-136">閱讀有關 hello[權限](site-recovery-role-based-linked-access-control.md)您需要進行複寫。</span><span class="sxs-lookup"><span data-stu-id="cd64f-136">Read about hello [permissions](site-recovery-role-based-linked-access-control.md) you need for replication.</span></span>
2. <span data-ttu-id="cd64f-137">請遵循這些[指示](../active-directory/role-based-access-control-configure.md#add-access)tooadd 權限。</span><span class="sxs-lookup"><span data-stu-id="cd64f-137">Follow these [instructions](../active-directory/role-based-access-control-configure.md#add-access) tooadd permissions.</span></span>


## <a name="verify-target-resources"></a><span data-ttu-id="cd64f-138">驗證目標資源</span><span class="sxs-lookup"><span data-stu-id="cd64f-138">Verify target resources</span></span>

1. <span data-ttu-id="cd64f-139">啟用您的 Azure 訂用帳戶 tooallow toocreate Vm 在 hello 目標想要為 hello 災害復原區域 toouse 嚴重損壞修復 toouse 地區。</span><span class="sxs-lookup"><span data-stu-id="cd64f-139">Enable your Azure subscription tooallow you toocreate VMs in hello target region you want toouse for disaster recovery that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="cd64f-140">請連絡客戶支援 tooenable hello 必要的配額。</span><span class="sxs-lookup"><span data-stu-id="cd64f-140">Contact support tooenable hello required quota.</span></span>
2. <span data-ttu-id="cd64f-141">請確定您的訂用帳戶有足夠的資源 tooenable Vm，以符合您的來源 Vm 的大小。</span><span class="sxs-lookup"><span data-stu-id="cd64f-141">Make sure your subscription has enough resources tooenable VMs with sizes that match your source VMs.</span></span> <span data-ttu-id="cd64f-142">根據預設，當設定複寫、 站台復原來挑選 hello 相同大小的 hello 目標 VM，或 hello 最可能的大小。</span><span class="sxs-lookup"><span data-stu-id="cd64f-142">By default, when set up replication, Site Recovery picks hello same size for hello target VM, or hello closest possible size.</span></span> <span data-ttu-id="cd64f-143">深入了解針對目標資源進行[疑難排解](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097)。</span><span class="sxs-lookup"><span data-stu-id="cd64f-143">Learn more about [troubleshooting](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) target resources.</span></span>

## <a name="verify-azure-vm-certificates"></a><span data-ttu-id="cd64f-144">驗證 Azure VM 憑證</span><span class="sxs-lookup"><span data-stu-id="cd64f-144">Verify Azure VM certificates</span></span>

1. <span data-ttu-id="cd64f-145">檢查 hello Windows 或您想要 tooreplicate Linux Vm 上的所有 hello 最新的根憑證都存在。</span><span class="sxs-lookup"><span data-stu-id="cd64f-145">Check that all hello latest root certificates are present on hello Windows or Linux VMs you want tooreplicate.</span></span> <span data-ttu-id="cd64f-146">如果 hello 最新的根憑證不存在，hello VM 不能註冊的 tooSite 復原，因為 toosecurity 條件約束。</span><span class="sxs-lookup"><span data-stu-id="cd64f-146">If hello latest root certificates are not present, hello VM cannot be registered tooSite Recovery due toosecurity constraints.</span></span>
2. <span data-ttu-id="cd64f-147">適用於 Windows Vm hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="cd64f-147">For Windows VMs, do hello following:</span></span>

    - <span data-ttu-id="cd64f-148">Hello VM 上安裝所有 hello 最新 Windows 更新，使所有 hello 受信任的根憑證都位於 hello 的電腦上。</span><span class="sxs-lookup"><span data-stu-id="cd64f-148">Install all hello latest Windows updates on hello VM so that all hello trusted root certificates are on hello machine.</span></span>
    - <span data-ttu-id="cd64f-149">在中斷連線的環境，請遵循 hello 標準 Windows Update 處理程序/憑證更新程序中組織、 tooget hello 最新的根憑證和更新的 CRL，hello Vm 上。</span><span class="sxs-lookup"><span data-stu-id="cd64f-149">In a disconnected environment, follow hello standard Windows Update process/certificate update process in your organization, tooget hello latest root certificates, and updated CRL, on hello VMs.</span></span>
3. <span data-ttu-id="cd64f-150">適用於 Linux Vm，請遵循您的 Linux 散發者 tooget hello 最受信任的根憑證與 hello 最新憑證撤銷清單 hello VM 上的所提供的 hello 指引。</span><span class="sxs-lookup"><span data-stu-id="cd64f-150">For Linux VMs, follow hello guidance provided by your Linux distributor tooget hello latest trusted root certificates and hello latest certificate revocation list on hello VM.</span></span> <span data-ttu-id="cd64f-151">深入了解針對受信任根發行進行[疑難排解](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066)。</span><span class="sxs-lookup"><span data-stu-id="cd64f-151">Learn more about [troubleshooting](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) trusted root issues.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cd64f-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cd64f-152">Next steps</span></span>

<span data-ttu-id="cd64f-153">跳過[步驟 3： 規劃網路](azure-to-azure-walkthrough-network.md)tooset 上的傳出連線。</span><span class="sxs-lookup"><span data-stu-id="cd64f-153">Go too[Step 3: Plan networking](azure-to-azure-walkthrough-network.md) tooset up outbound connectivity.</span></span>
