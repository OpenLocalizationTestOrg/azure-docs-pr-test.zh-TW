---
title: "使用 Azure Site Recovery aaaReplicate HYPER-V Vm tooAzure |Microsoft 文件"
description: "描述如何 tooorchestrate 複寫、 容錯移轉和復原的內部部署 Hyper-v-V Vm tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="5c581-103">複寫 HYPER-V 虛擬機器 （無 VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="5c581-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c581-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5c581-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="5c581-105">Azure 傳統型</span><span class="sxs-lookup"><span data-stu-id="5c581-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="5c581-106">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="5c581-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="5c581-107">本文概述 hello 所需步驟 tooreplicate 在內部部署 HYPER-V 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5c581-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="5c581-108">在此部署中，Hyper-V VM 並非由 System Center Virtual Machine Manager (VMM) 所管理。</span><span class="sxs-lookup"><span data-stu-id="5c581-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="5c581-109">閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="5c581-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="5c581-110">步驟 1：檢閱架構和必要條件</span><span class="sxs-lookup"><span data-stu-id="5c581-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="5c581-111">在開始部署之前，檢閱 hello 案例架構，並確定您了解您需要 toodeploy 所有 hello 元件</span><span class="sxs-lookup"><span data-stu-id="5c581-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="5c581-112">跳過[步驟 1： 檢閱 hello 架構](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="5c581-113">步驟 2：檢閱必要條件</span><span class="sxs-lookup"><span data-stu-id="5c581-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="5c581-114">請確定您具備 hello 必要條件以便於部署的每個元件：</span><span class="sxs-lookup"><span data-stu-id="5c581-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="5c581-115">**Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c581-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="5c581-116">**內部部署 Hyper-V 必要條件**：請確定備妥 Hyper-V 主機可進行 Site Recovery 部署。</span><span class="sxs-lookup"><span data-stu-id="5c581-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="5c581-117">**複寫 Vm**： 您想要 tooreplicate 需要 toocomply Azure 需求的 Vm。</span><span class="sxs-lookup"><span data-stu-id="5c581-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="5c581-118">跳過[步驟 2： 確認必要條件和限制](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="5c581-119">步驟 3：規劃容量</span><span class="sxs-lookup"><span data-stu-id="5c581-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="5c581-120">如果您進行完整部署需要 toofigure 出您需要哪些複寫資源。</span><span class="sxs-lookup"><span data-stu-id="5c581-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="5c581-121">有幾個的工具可用 toohelp 這麼做。</span><span class="sxs-lookup"><span data-stu-id="5c581-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="5c581-122">移 tooStep 2。</span><span class="sxs-lookup"><span data-stu-id="5c581-122">Go tooStep 2.</span></span> <span data-ttu-id="5c581-123">如果您進行快速設定 tootest hello 環境可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="5c581-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="5c581-124">跳過[步驟 3： 規劃容量](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="5c581-125">步驟 4：規劃網路</span><span class="sxs-lookup"><span data-stu-id="5c581-125">Step 4: Plan networking</span></span>

<span data-ttu-id="5c581-126">您需要 toodo 規劃 tooensure Azure Vm 就會發生容錯移轉之後連接的 toonetworks 和確認他們已擁有 hello 正確 IP 位址，某些網路。</span><span class="sxs-lookup"><span data-stu-id="5c581-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="5c581-127">跳過[步驟 4： 規劃的網路功能](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="5c581-128">步驟 5：準備 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="5c581-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="5c581-129">在開始之前，請先設定 Azure 網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="5c581-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="5c581-130">您可以在部署期間執行這項操作，但建議您在開始之前進行。</span><span class="sxs-lookup"><span data-stu-id="5c581-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="5c581-131">跳過[步驟 5： 準備 Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="5c581-132">步驟 6：準備 Hyper-V</span><span class="sxs-lookup"><span data-stu-id="5c581-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="5c581-133">請確定 Hyper-V 伺服器符合 Site Recovery 部署需求。</span><span class="sxs-lookup"><span data-stu-id="5c581-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="5c581-134">跳過[步驟 6： 準備 HYPER-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="5c581-135">步驟 7：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="5c581-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="5c581-136">您需要註冊復原服務保存庫 tooorchestrate tooset 和管理複寫。</span><span class="sxs-lookup"><span data-stu-id="5c581-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="5c581-137">當您設定 hello 保存庫時，指定您想要 tooreplicate，以及您希望 tooreplicate 它。</span><span class="sxs-lookup"><span data-stu-id="5c581-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="5c581-138">跳過[步驟 7： 建立保存庫](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="5c581-139">步驟 8：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="5c581-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="5c581-140">設定 hello 來源和目標使用，可用於複寫。</span><span class="sxs-lookup"><span data-stu-id="5c581-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="5c581-141">設定來源設定，包括新增 HYPER-V 主機 tooa HYPER-V 網站時，每個 HYPER-V 主機上，安裝 hello Site Recovery 提供者和復原服務代理程式和 hello 復原服務保存庫中註冊 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="5c581-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="5c581-142">跳過[步驟 8: hello 來源和目標設定](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="5c581-143">步驟 9：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="5c581-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="5c581-144">您設定原則 toospecify 複寫設定的 HYPER-V Vm hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="5c581-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="5c581-145">跳過[步驟 9： 設定複寫原則](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="5c581-146">步驟 10：啟用複寫</span><span class="sxs-lookup"><span data-stu-id="5c581-146">Step 10: Enable replication</span></span>

<span data-ttu-id="5c581-147">您已備妥，複寫原則之後啟用之後，就會發生 hello VM 的初始複寫。</span><span class="sxs-lookup"><span data-stu-id="5c581-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="5c581-148">跳過[步驟 10： 啟用複寫](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="5c581-149">步驟 11：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="5c581-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="5c581-150">初始複寫完成，並執行差異複寫之後，您可以執行測試容錯移轉 toomake 確定一切如預期運作。</span><span class="sxs-lookup"><span data-stu-id="5c581-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="5c581-151">跳過[步驟 11： 執行測試容錯移轉](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="5c581-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
