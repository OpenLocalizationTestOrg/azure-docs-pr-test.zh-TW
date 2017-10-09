---
title: "aaaReplicate HYPER-V Vm tooa 次要 VMM 站台與 Azure Site Recovery |Microsoft 文件"
description: "用來複寫 HYPER-V Vm tooa 次要 VMM 站台使用 hello Azure 入口網站提供的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="fb6fc-103">將 HYPER-V 虛擬機器在 VMM 雲端 tooa 次要 VMM 站台複寫</span><span class="sxs-lookup"><span data-stu-id="fb6fc-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb6fc-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fb6fc-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="fb6fc-105">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="fb6fc-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="fb6fc-106">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="fb6fc-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="fb6fc-107">本文概述的 hello 需要 tooreplicate 內部管理次要 VMM 位置 tooa，System Center Virtual Machine Manager (VMM) 雲端中 HYPER-V 虛擬機器 (Vm) 的步驟，使用[Azure Site Recovery](site-recovery-overview.md)hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="fb6fc-108">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="fb6fc-109">步驟 1： 檢閱 hello 案例架構</span><span class="sxs-lookup"><span data-stu-id="fb6fc-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="fb6fc-110">您開始部署，檢閱 hello 案例架構，並確定您了解所有 hello 元件必須先 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="fb6fc-111">跳過[步驟 1： 檢閱 hello 架構](vmm-to-vmm-walkthrough-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="fb6fc-112">步驟 2：檢閱必要條件和限制</span><span class="sxs-lookup"><span data-stu-id="fb6fc-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="fb6fc-113">請確定您已了解 hello 部署必要條件和限制。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="fb6fc-114">**Azure 的必要條件**： 您需要 Microsoft Azure 訂用帳戶和 Azure 復原服務保存庫 tooorchestrate 和管理複寫。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="fb6fc-115">**內部部署 VMM 伺服器和 Hyper-V 主機**：請確定 VMM 伺服器和 Hyper-V 主機符合 Site Recovery 部署的必要條件並已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="fb6fc-116">跳過[步驟 2： 確認必要條件和限制](vmm-to-vmm-walkthrough-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="fb6fc-117">步驟 3：規劃網路服務</span><span class="sxs-lookup"><span data-stu-id="fb6fc-117">Step 3: Plan networking</span></span>

<span data-ttu-id="fb6fc-118">您需要 toodo 規劃，您可以設定網路對應，當您部署的 hello 案例時，VMM VM 網路間的 tooensure 部分網路。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="fb6fc-119">跳過[步驟 3： 規劃網路](vmm-to-vmm-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="fb6fc-120">步驟 4：準備 VMM 和 Hyper-V</span><span class="sxs-lookup"><span data-stu-id="fb6fc-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="fb6fc-121">準備站台復原 」 部署的 hello VMM 伺服器和 HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="fb6fc-122">跳過[步驟 4： 準備內部部署伺服器](vmm-to-vmm-walkthrough-vmm-hyper-v.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="fb6fc-123">步驟 5：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="fb6fc-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="fb6fc-124">設定復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="fb6fc-125">hello 保存庫包含組態設定，並且會協調複寫。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="fb6fc-126">[步驟 5：設定保存庫](vmm-to-vmm-walkthrough-create-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="fb6fc-127">步驟 6：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="fb6fc-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="fb6fc-128">設定 hello 來源和目標複寫 VMM 位置。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="fb6fc-129">新增 hello VMM 伺服器 toohello 保存庫，並下載 Site Recovery 元件的 hello 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="fb6fc-130">Hello VMM 伺服器上執行 Azure Site Recovery Provider 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="fb6fc-131">安裝程式會在 hello VMM 伺服器上，安裝 hello 提供者，並登錄 hello 伺服器 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="fb6fc-132">您每個 HYPER-V 主機上安裝 hello Microsoft 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="fb6fc-133">跳過[步驟 6： 設定 hello 來源和目標設定](vmm-to-vmm-walkthrough-source-target.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="fb6fc-134">步驟 7：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="fb6fc-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="fb6fc-135">VMM 的 VM 網路對應 hello 來源和目標位置中。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="fb6fc-136">容錯移轉之後，Vm 會在建立 hello 目標網路中的 hello 來源 HYPER-V 虛擬機器位於該對應 toohello 來源 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="fb6fc-137">跳過[步驟 7： 設定網路對應](vmm-to-vmm-walkthrough-network-mapping.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="fb6fc-138">步驟 8：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="fb6fc-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="fb6fc-139">指定 VM 在 VMM 位置之間的複寫方式。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="fb6fc-140">跳過[步驟 8： 設定複寫原則](vmm-to-vmm-walkthrough-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="fb6fc-141">步驟 9：啟用 VM 複寫</span><span class="sxs-lookup"><span data-stu-id="fb6fc-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="fb6fc-142">選取您想要 tooreplicate hello Vm。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="fb6fc-143">啟用複寫觸發程序 hello 初始複寫 toohello 次要站台的 VM，後面接著進行中的差異複寫。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="fb6fc-144">跳過[步驟 9： 啟用複寫](vmm-to-vmm-walkthrough-enable-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="fb6fc-145">步驟 10：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="fb6fc-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="fb6fc-146">執行測試容錯移轉 toomake 確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="fb6fc-147">跳過[步驟 10： 執行測試容錯移轉](vmm-to-vmm-walkthrough-test-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="fb6fc-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
