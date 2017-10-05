---
title: "使用 Azure Site Recovery 將實體內部部署伺服器複寫至 Azure | Microsoft Docs"
description: "簡述使用 Azure Site Recovery 服務將在內部部署 Windows/Linux 實體伺服器上執行的工作負載複寫至 Azure 所需的步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 0a09b35e98dc0b2f5283c2a707a3a2b8ac9a39f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-physical-servers-to-azure-with-site-recovery"></a><span data-ttu-id="93649-103">使用 Site Recovery 將實體伺服器複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="93649-103">Replicate physical servers to Azure with Site Recovery</span></span>

<span data-ttu-id="93649-104">本文概述在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署 Windows/Linux 實體伺服器複寫至 Azure 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="93649-104">This article provides an overview of the steps required to replicate on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="93649-105">步驟 1：檢閱架構和必要條件</span><span class="sxs-lookup"><span data-stu-id="93649-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="93649-106">在開始部署之前，請檢閱案例架構，並確定您了解設定部署所需的一切元件。</span><span class="sxs-lookup"><span data-stu-id="93649-106">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to set up the deployment.</span></span>

<span data-ttu-id="93649-107">移至[步驟 1：檢閱架構](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="93649-107">Go to [Step 1: Review the architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="93649-108">步驟 2：檢閱必要條件</span><span class="sxs-lookup"><span data-stu-id="93649-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="93649-109">請確定您已備妥每個部署元件的必要條件：</span><span class="sxs-lookup"><span data-stu-id="93649-109">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="93649-110">**Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="93649-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="93649-111">**內部部署 Site Recovery 元件**：您需要有一部執行內部部署 Site Recovery 元件的機器。</span><span class="sxs-lookup"><span data-stu-id="93649-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="93649-112">**複寫的機器**：您想要複寫的伺服器必須符合內部部署環境與 Azure 的需求。</span><span class="sxs-lookup"><span data-stu-id="93649-112">**Replicated machines**: Servers you want to replicate need to comply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="93649-113">移至[步驟 2：檢閱必要條件和限制](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="93649-113">Go to [Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="93649-114">步驟 3：規劃容量</span><span class="sxs-lookup"><span data-stu-id="93649-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="93649-115">如果您要執行完整部署，就必須了解需要哪些複寫資源。</span><span class="sxs-lookup"><span data-stu-id="93649-115">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="93649-116">如果您要進行快速設定來測試環境，則可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="93649-116">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="93649-117">移至[步驟 3：規劃容量](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="93649-117">Go to [Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="93649-118">步驟 4：規劃網路</span><span class="sxs-lookup"><span data-stu-id="93649-118">Step 4: Plan networking</span></span>

<span data-ttu-id="93649-119">您必須進行一些網路規劃，以確保 Azure VM 在發生容錯移轉之後會連線到網路，並且它們具有正確的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93649-119">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="93649-120">移至[步驟 4：規劃網路](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="93649-120">Go to [Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="93649-121">步驟 5：準備 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="93649-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="93649-122">在開始之前，請先設定 Azure 網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="93649-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="93649-123">移至[步驟 5：準備 Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="93649-123">Go to [Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="93649-124">步驟 6：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="93649-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="93649-125">您需設定「復原服務」保存庫來協調和管理複寫。</span><span class="sxs-lookup"><span data-stu-id="93649-125">You set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="93649-126">當您設定保存庫時，請指定您想要複寫的項目，以及要將它複寫到何處。</span><span class="sxs-lookup"><span data-stu-id="93649-126">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="93649-127">移至[步驟 6：設定保存庫](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="93649-127">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="93649-128">步驟 7：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="93649-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="93649-129">設定來源和目標 (Azure) 站台的設定。</span><span class="sxs-lookup"><span data-stu-id="93649-129">Configure settings for the source and target (Azure) site.</span></span> <span data-ttu-id="93649-130">來源設定包括執行「整合安裝」來安裝內部部署 Site Recovery 元件。</span><span class="sxs-lookup"><span data-stu-id="93649-130">Source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="93649-131">移至[步驟 7：設定來源和目標](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="93649-131">Go to [Step 7: Set up the source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="93649-132">步驟 8：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="93649-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="93649-133">您需設定原則來指定實體伺服器應該如何進行複寫。</span><span class="sxs-lookup"><span data-stu-id="93649-133">You set up a policy to specify how physical servers should replicate.</span></span>

<span data-ttu-id="93649-134">移至[步驟 8：設定複寫原則](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="93649-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="93649-135">步驟 9：安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="93649-135">Step 9: Install the Mobility service</span></span>

<span data-ttu-id="93649-136">行動服務必須安裝在您要複寫的每部伺服器上。</span><span class="sxs-lookup"><span data-stu-id="93649-136">The Mobility service must be installed on each server you want to replicate.</span></span> <span data-ttu-id="93649-137">有幾個方法可藉由推入或提取安裝來安裝服務。</span><span class="sxs-lookup"><span data-stu-id="93649-137">There are a few ways to set up the service, with push or pull installation.</span></span>

<span data-ttu-id="93649-138">移至[步驟 9：安裝行動服務](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="93649-138">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="93649-139">步驟 10：啟用複寫</span><span class="sxs-lookup"><span data-stu-id="93649-139">Step 10: Enable replication</span></span>

<span data-ttu-id="93649-140">在行動服務於伺服器上執行之後，您便可以為其啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="93649-140">After the Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="93649-141">啟用複寫之後，就會進行初始 VM 複寫。</span><span class="sxs-lookup"><span data-stu-id="93649-141">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="93649-142">移至[步驟 10：啟用複寫](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="93649-142">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="93649-143">步驟 11：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="93649-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="93649-144">在初始複寫完成且差異複寫執行之後，您可以執行測試容錯移轉，以確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="93649-144">After initial replication finishes and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="93649-145">移至[步驟 11：執行測試容錯移轉](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="93649-145">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

