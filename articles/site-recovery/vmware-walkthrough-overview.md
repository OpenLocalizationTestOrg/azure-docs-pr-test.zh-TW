---
title: "使用 Azure Site Recovery aaaReplicate VMware Vm tooAzure |Microsoft 文件"
description: "提供用來複寫 tooAzure VMware Vm 上執行工作負載的 hello 步驟的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="34959-103">複寫與站台復原的 VMware Vm tooAzure</span><span class="sxs-lookup"><span data-stu-id="34959-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="34959-104">本文概述 hello 步驟需要的 tooreplicate 在內部部署 VMware 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="34959-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![部署程序](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="34959-106">**圖 1：部署程序摘要**</span><span class="sxs-lookup"><span data-stu-id="34959-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="34959-107">步驟 1：檢閱架構和必要條件</span><span class="sxs-lookup"><span data-stu-id="34959-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="34959-108">在開始部署之前，檢閱 hello 案例架構，並確定您了解您需要 toodeploy 所有 hello 元件</span><span class="sxs-lookup"><span data-stu-id="34959-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="34959-109">跳過[步驟 1： 檢閱 hello 架構](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="34959-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="34959-110">步驟 2：檢閱必要條件</span><span class="sxs-lookup"><span data-stu-id="34959-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="34959-111">請確定您具備 hello 必要條件以便於部署的每個元件：</span><span class="sxs-lookup"><span data-stu-id="34959-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="34959-112">**Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="34959-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="34959-113">**內部部署 Site Recovery 元件**：您需要有一部執行內部部署 Site Recovery 元件的機器。</span><span class="sxs-lookup"><span data-stu-id="34959-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="34959-114">**在內部部署 VMware 必要條件**： 您需要 tooset 帳戶以便 VMware 伺服器和 Vm，可以存取站台復原。</span><span class="sxs-lookup"><span data-stu-id="34959-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="34959-115">**複寫 Vm**: Vm tooreplicate 需要 toocomply Azure 需求，並安裝 hello 行動服務元件。</span><span class="sxs-lookup"><span data-stu-id="34959-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="34959-116">跳過[步驟 2： 檢閱必要條件和限制](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="34959-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="34959-117">步驟 3：規劃容量</span><span class="sxs-lookup"><span data-stu-id="34959-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="34959-118">如果您進行完整部署需要 toofigure 出您需要哪些複寫資源。</span><span class="sxs-lookup"><span data-stu-id="34959-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="34959-119">有幾個的工具可用 toohelp 這麼做。</span><span class="sxs-lookup"><span data-stu-id="34959-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="34959-120">移 tooStep 2。</span><span class="sxs-lookup"><span data-stu-id="34959-120">Go tooStep 2.</span></span> <span data-ttu-id="34959-121">如果您進行快速設定 tootest hello 環境可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="34959-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="34959-122">跳過[步驟 3： 規劃容量](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="34959-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="34959-123">步驟 4：規劃網路</span><span class="sxs-lookup"><span data-stu-id="34959-123">Step 4: Plan networking</span></span>

<span data-ttu-id="34959-124">您需要 toodo 規劃 tooensure Azure Vm 就會發生容錯移轉之後連接的 toonetworks 和確認他們已擁有 hello 正確 IP 位址，某些網路。</span><span class="sxs-lookup"><span data-stu-id="34959-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="34959-125">跳過[步驟 4： 規劃的網路功能](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="34959-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="34959-126">步驟 5：準備 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="34959-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="34959-127">在開始之前，請先設定 Azure 網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="34959-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="34959-128">您可以在部署期間執行這項操作，但建議您在開始之前進行。</span><span class="sxs-lookup"><span data-stu-id="34959-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="34959-129">跳過[步驟 5： 準備 Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="34959-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="34959-130">步驟 6：準備 VMware</span><span class="sxs-lookup"><span data-stu-id="34959-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="34959-131">您需要 tooset 帳戶將用於站台復原：</span><span class="sxs-lookup"><span data-stu-id="34959-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="34959-132">存取 VMware 虛擬化伺服器 tooautomatically 偵測到 Vm。</span><span class="sxs-lookup"><span data-stu-id="34959-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="34959-133">存取 Vm tooinstall hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="34959-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="34959-134">每個的 VM，您想要 tooreplicate 必須擁有 hello 行動服務代理程式安裝之前，您可以啟用複寫功能。</span><span class="sxs-lookup"><span data-stu-id="34959-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="34959-135">跳過[步驟 6： 準備 VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="34959-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="34959-136">步驟 7：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="34959-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="34959-137">您需要註冊復原服務保存庫 tooorchestrate tooset 和管理複寫。</span><span class="sxs-lookup"><span data-stu-id="34959-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="34959-138">當您設定 hello 保存庫時，指定您想要 tooreplicate，以及您希望 tooreplicate 它。</span><span class="sxs-lookup"><span data-stu-id="34959-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="34959-139">跳過[步驟 7： 設定保存庫](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="34959-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="34959-140">步驟 8：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="34959-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="34959-141">設定 hello 來源和目標使用，可用於複寫。</span><span class="sxs-lookup"><span data-stu-id="34959-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="34959-142">來源設定的設定包含執行整合安裝 tooinstall hello 在內部部署站台復原元件。</span><span class="sxs-lookup"><span data-stu-id="34959-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="34959-143">跳過[步驟 8: hello 來源和目標設定](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="34959-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="34959-144">步驟 9：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="34959-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="34959-145">您設定原則 toospecify 複寫設定 VMware vm hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="34959-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="34959-146">跳過[步驟 9： 設定複寫原則](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="34959-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="34959-147">步驟 10： 安裝 hello 行動服務</span><span class="sxs-lookup"><span data-stu-id="34959-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="34959-148">必須安裝行動服務的 hello 想在每個 VM 上 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="34959-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="34959-149">有幾個方式 tooset hello 與發送或提取安裝的服務。</span><span class="sxs-lookup"><span data-stu-id="34959-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="34959-150">跳過[步驟 10： 安裝 hello 行動服務](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="34959-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="34959-151">步驟 11：啟用複寫</span><span class="sxs-lookup"><span data-stu-id="34959-151">Step 11: Enable replication</span></span>

<span data-ttu-id="34959-152">Hello 行動服務在 VM 上執行之後，您可以啟用複寫功能。</span><span class="sxs-lookup"><span data-stu-id="34959-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="34959-153">啟用之後，就會發生 hello VM 的初始複寫。</span><span class="sxs-lookup"><span data-stu-id="34959-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="34959-154">跳過[步驟 11： 啟用複寫](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="34959-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="34959-155">步驟 12：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="34959-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="34959-156">初始複寫完成，並執行差異複寫之後，您可以執行測試容錯移轉 toomake 確定一切如預期運作。</span><span class="sxs-lookup"><span data-stu-id="34959-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="34959-157">跳過[步驟 12： 執行測試容錯移轉](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="34959-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
