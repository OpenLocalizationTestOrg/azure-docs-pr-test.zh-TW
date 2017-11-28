---
title: "aaaReplicate 實體內部部署伺服器與 Azure Site Recovery 的 tooAzure |Microsoft 文件"
description: "複寫在內部部署 Windows/Linux 實體伺服器 tooAzure 以 hello Azure Site Recovery 服務上執行工作負載提供 hello 步驟的概觀。"
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
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="3d947-103">複寫與站台復原的實體伺服器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="3d947-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="3d947-104">本文概述 hello 步驟需要的 tooreplicate 在內部部署 Windows/Linux 實體伺服器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="3d947-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="3d947-105">步驟 1：檢閱架構和必要條件</span><span class="sxs-lookup"><span data-stu-id="3d947-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="3d947-106">在開始部署之前，檢閱 hello 案例架構，並確定您了解所有您需要 tooset hello 部署的 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="3d947-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="3d947-107">跳過[步驟 1： 檢閱 hello 架構](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="3d947-108">步驟 2：檢閱必要條件</span><span class="sxs-lookup"><span data-stu-id="3d947-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="3d947-109">請確定您具備 hello 必要條件以便於部署的每個元件：</span><span class="sxs-lookup"><span data-stu-id="3d947-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="3d947-110">**Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d947-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="3d947-111">**內部部署 Site Recovery 元件**：您需要有一部執行內部部署 Site Recovery 元件的機器。</span><span class="sxs-lookup"><span data-stu-id="3d947-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="3d947-112">**複寫機器**： 您想 tooreplicate 伺服器需要 toocomply 在內部部署與 Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="3d947-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="3d947-113">跳過[步驟 2： 檢閱必要條件和限制](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="3d947-114">步驟 3：規劃容量</span><span class="sxs-lookup"><span data-stu-id="3d947-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="3d947-115">如果您進行完整部署需要 toofigure 出您需要哪些複寫資源。</span><span class="sxs-lookup"><span data-stu-id="3d947-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="3d947-116">如果您進行快速設定 tootest hello 環境，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="3d947-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="3d947-117">跳過[步驟 3： 規劃容量](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="3d947-118">步驟 4：規劃網路</span><span class="sxs-lookup"><span data-stu-id="3d947-118">Step 4: Plan networking</span></span>

<span data-ttu-id="3d947-119">您需要 toodo 規劃 tooensure Azure Vm 就會發生容錯移轉之後連接的 toonetworks 和確認他們已擁有 hello 正確 IP 位址，某些網路。</span><span class="sxs-lookup"><span data-stu-id="3d947-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="3d947-120">跳過[步驟 4： 規劃的網路功能](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="3d947-121">步驟 5：準備 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="3d947-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="3d947-122">在開始之前，請先設定 Azure 網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="3d947-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="3d947-123">跳過[步驟 5： 準備 Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="3d947-124">步驟 6：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="3d947-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="3d947-125">您可以設定 復原服務保存庫 tooorchestrate 和管理複寫。</span><span class="sxs-lookup"><span data-stu-id="3d947-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="3d947-126">當您設定 hello 保存庫時，指定您想要 tooreplicate，以及您希望 tooreplicate 它。</span><span class="sxs-lookup"><span data-stu-id="3d947-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="3d947-127">跳過[步驟 6： 設定保存庫](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="3d947-128">步驟 7：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="3d947-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="3d947-129">設定 hello 來源和目標 (Azure) 的站台。</span><span class="sxs-lookup"><span data-stu-id="3d947-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="3d947-130">來源設定包含執行整合安裝 tooinstall hello 在內部部署站台復原元件。</span><span class="sxs-lookup"><span data-stu-id="3d947-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="3d947-131">跳過[步驟 7： 設定 hello 來源和目標](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="3d947-132">步驟 8：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="3d947-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="3d947-133">您設定原則 toospecify 如何實體伺服器應該將複寫。</span><span class="sxs-lookup"><span data-stu-id="3d947-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="3d947-134">跳過[步驟 8： 設定複寫原則](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="3d947-135">步驟 9： 安裝 hello 行動服務</span><span class="sxs-lookup"><span data-stu-id="3d947-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="3d947-136">必須安裝行動服務的 hello 想 tooreplicate 在每一部伺服器上。</span><span class="sxs-lookup"><span data-stu-id="3d947-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="3d947-137">有幾個方式 tooset hello 服務，與發送或提取的安裝。</span><span class="sxs-lookup"><span data-stu-id="3d947-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="3d947-138">跳過[步驟 9： 安裝 hello 行動服務](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="3d947-139">步驟 10：啟用複寫</span><span class="sxs-lookup"><span data-stu-id="3d947-139">Step 10: Enable replication</span></span>

<span data-ttu-id="3d947-140">Hello 行動服務正在伺服器上執行之後，您可以啟用複寫功能。</span><span class="sxs-lookup"><span data-stu-id="3d947-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="3d947-141">啟用之後，就會發生 hello VM 的初始複寫。</span><span class="sxs-lookup"><span data-stu-id="3d947-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="3d947-142">跳過[步驟 10： 啟用複寫](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="3d947-143">步驟 11：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="3d947-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="3d947-144">初始複寫完成，並執行差異複寫之後，您可以執行測試容錯移轉 toomake 確定一切如預期運作。</span><span class="sxs-lookup"><span data-stu-id="3d947-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="3d947-145">跳過[步驟 11： 執行測試容錯移轉](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="3d947-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

