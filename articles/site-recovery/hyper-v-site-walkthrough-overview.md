---
title: "使用 Azure Site Recovery 將 Hyper-V VM 複寫至 Azure | Microsoft Docs"
description: "說明如何將內部部署 Hyper-V VM 針對 Azure 進行協調複寫、容錯移轉及復原"
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
ms.openlocfilehash: da10b213bc2543942b5ac77cf5c5d8547c00220c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure"></a><span data-ttu-id="6f21b-103">將 Hyper-V 虛擬機器 (不含 VMM) 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="6f21b-103">Replicate Hyper-V virtual machines (without VMM) to Azure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f21b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6f21b-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="6f21b-105">Azure 傳統型</span><span class="sxs-lookup"><span data-stu-id="6f21b-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="6f21b-106">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="6f21b-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="6f21b-107">本文概述在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md)，將內部部署 Hyper-V 虛擬機器複寫至 Azure 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="6f21b-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="6f21b-108">在此部署中，Hyper-V VM 並非由 System Center Virtual Machine Manager (VMM) 所管理。</span><span class="sxs-lookup"><span data-stu-id="6f21b-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="6f21b-109">閱讀本文之後，在本文下方張貼意見，或在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="6f21b-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="6f21b-110">步驟 1：檢閱架構和必要條件</span><span class="sxs-lookup"><span data-stu-id="6f21b-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="6f21b-111">在開始部署之前，請檢閱案例架構，並確定您了解部署所需的一切元件</span><span class="sxs-lookup"><span data-stu-id="6f21b-111">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="6f21b-112">移至[步驟 1：檢閱架構](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-112">Go to [Step 1: Review the architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="6f21b-113">步驟 2：檢閱必要條件</span><span class="sxs-lookup"><span data-stu-id="6f21b-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="6f21b-114">請確定您已備妥每個部署元件的必要條件：</span><span class="sxs-lookup"><span data-stu-id="6f21b-114">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="6f21b-115">**Azure 必要條件**您需要 Microsoft Azure 帳戶、Azure 網路和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f21b-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="6f21b-116">**內部部署 Hyper-V 必要條件**：請確定備妥 Hyper-V 主機可進行 Site Recovery 部署。</span><span class="sxs-lookup"><span data-stu-id="6f21b-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="6f21b-117">**複寫 VM**：您想要複寫的 VM 必須符合 Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="6f21b-117">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements.</span></span>

<span data-ttu-id="6f21b-118">移至[步驟 2：確認必要條件和限制](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-118">Go to [Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="6f21b-119">步驟 3：規劃產能</span><span class="sxs-lookup"><span data-stu-id="6f21b-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="6f21b-120">如果您要執行完整部署，就必須了解需要哪些複寫資源。</span><span class="sxs-lookup"><span data-stu-id="6f21b-120">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="6f21b-121">有幾個工具可幫助您執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="6f21b-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="6f21b-122">移至步驟 2。</span><span class="sxs-lookup"><span data-stu-id="6f21b-122">Go to Step 2.</span></span> <span data-ttu-id="6f21b-123">如果您要進行快速設定來測試環境，則可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="6f21b-123">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="6f21b-124">移至[步驟 3：規劃容量](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-124">Go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="6f21b-125">步驟 4：規劃網路</span><span class="sxs-lookup"><span data-stu-id="6f21b-125">Step 4: Plan networking</span></span>

<span data-ttu-id="6f21b-126">您必須進行一些網路規劃，以確保 Azure VM 在發生容錯移轉之後會連線到網路，並且它們具有正確的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6f21b-126">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="6f21b-127">移至[步驟 4：規劃網路](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-127">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="6f21b-128">步驟 5：準備 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="6f21b-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="6f21b-129">在開始之前，請先設定 Azure 網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="6f21b-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="6f21b-130">您可以在部署期間執行這項操作，但建議您在開始之前進行。</span><span class="sxs-lookup"><span data-stu-id="6f21b-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="6f21b-131">移至[步驟 5：準備 Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-131">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="6f21b-132">步驟 6：準備 Hyper-V</span><span class="sxs-lookup"><span data-stu-id="6f21b-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="6f21b-133">請確定 Hyper-V 伺服器符合 Site Recovery 部署需求。</span><span class="sxs-lookup"><span data-stu-id="6f21b-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="6f21b-134">移至[步驟 6：準備 Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-134">Go to [Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="6f21b-135">步驟 7：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="6f21b-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="6f21b-136">您必須設定「復原服務」保存庫，才能協調和管理複寫。</span><span class="sxs-lookup"><span data-stu-id="6f21b-136">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="6f21b-137">當您設定保存庫時，請指定您想要複寫的項目，以及您要複寫它的位置。</span><span class="sxs-lookup"><span data-stu-id="6f21b-137">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="6f21b-138">移至[步驟 7：建立保存庫](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-138">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="6f21b-139">步驟 8：設定來源與目標設定</span><span class="sxs-lookup"><span data-stu-id="6f21b-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="6f21b-140">設定可用於複寫的來源和目標。</span><span class="sxs-lookup"><span data-stu-id="6f21b-140">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="6f21b-141">設定來源設定包括將 Hyper-V 主機新增至 Hyper-V 站台、在每個 Hyper-V 主機上安裝 Site Recovery 提供者和復原服務代理程式，以及在復原服務保存庫中註冊站台。</span><span class="sxs-lookup"><span data-stu-id="6f21b-141">Setting up source settings includes adding Hyper-V hosts to a Hyper-V site, installing the Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering the site in the Recovery Services vault.</span></span>

<span data-ttu-id="6f21b-142">移至[步驟 8：設定來源和目標](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-142">Go to [Step 8: Set up the source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="6f21b-143">步驟 9：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="6f21b-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="6f21b-144">若要在保存庫中指定 Hyper-V VM 的複寫設定，您就要設定原則。</span><span class="sxs-lookup"><span data-stu-id="6f21b-144">You set up a policy to specify replication settings for Hyper-V VMs in the vault.</span></span>

<span data-ttu-id="6f21b-145">移至[步驟 9：設定複寫原則](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-145">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="6f21b-146">步驟 10：啟用複寫</span><span class="sxs-lookup"><span data-stu-id="6f21b-146">Step 10: Enable replication</span></span>

<span data-ttu-id="6f21b-147">您備妥複寫原則之後，在啟用後就會發生初始複寫 VM。</span><span class="sxs-lookup"><span data-stu-id="6f21b-147">After you have a replication policy in place,  After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="6f21b-148">移至[步驟 10：啟用複寫](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-148">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="6f21b-149">步驟 11：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="6f21b-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="6f21b-150">初始複寫完成，且差異複寫執行之後，您可以執行測試容錯移轉，以確定一切如預期運作。</span><span class="sxs-lookup"><span data-stu-id="6f21b-150">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="6f21b-151">移至[步驟 11：執行測試容錯移轉](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="6f21b-151">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
