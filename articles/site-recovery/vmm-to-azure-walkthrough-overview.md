---
title: "aaaReplicate 在 VMM 中的 HYPER-V Vm 雲端與 Azure Site Recovery tooAzure |Microsoft 文件"
description: "提供用來複寫 VMM 雲端 tooAzure 使用 hello Azure Site Recovery 服務中的 HYPER-V Vm 的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="0939a-103">複寫 HYPER-V 虛擬機器在 VMM 雲端 tooAzure hello Azure 入口網站中使用站台復原中</span><span class="sxs-lookup"><span data-stu-id="0939a-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0939a-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0939a-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="0939a-105">Azure 傳統型</span><span class="sxs-lookup"><span data-stu-id="0939a-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="0939a-106">PowerShell Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0939a-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="0939a-107">PowerShell 傳統</span><span class="sxs-lookup"><span data-stu-id="0939a-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="0939a-108">本文章提供概觀 hello 步驟需要 tooreplicate 內部部署 HYPER-V 虛擬機器 (Vm) 管理 System Center Virtual Machine Manager (VMM) 雲端 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md)服務hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0939a-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="0939a-109">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="0939a-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="0939a-110">步驟 1： 檢閱 hello 案例架構</span><span class="sxs-lookup"><span data-stu-id="0939a-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="0939a-111">您開始部署，檢閱 hello 案例架構，並確定您了解所有 hello 元件必須先 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="0939a-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="0939a-112">跳過[步驟 1： 檢閱 hello 架構](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="0939a-113">步驟 2：檢閱必要條件和限制</span><span class="sxs-lookup"><span data-stu-id="0939a-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="0939a-114">請確定您已了解 hello 部署必要條件和限制。</span><span class="sxs-lookup"><span data-stu-id="0939a-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="0939a-115">**Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0939a-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="0939a-116">**內部部署 VMM 伺服器和 Hyper-V 主機**：請確定 VMM 伺服器和 Hyper-V 主機符合 Site Recovery 部署的必要條件並已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="0939a-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="0939a-117">**複寫 Vm**： 核取您想要 tooreplicate Vm 符合 Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="0939a-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="0939a-118">跳過[步驟 2： 確認必要條件和限制](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="0939a-119">步驟 3：規劃容量</span><span class="sxs-lookup"><span data-stu-id="0939a-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="0939a-120">如果您進行完整部署，您會需要 toofigure 出您需要哪些複寫資源。</span><span class="sxs-lookup"><span data-stu-id="0939a-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="0939a-121">有幾個的工具可用 toohelp 這麼做。</span><span class="sxs-lookup"><span data-stu-id="0939a-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="0939a-122">如果您進行快速設定 tootest hello 環境，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="0939a-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="0939a-123">跳過[步驟 3： 規劃容量](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="0939a-124">步驟 4：規劃網路</span><span class="sxs-lookup"><span data-stu-id="0939a-124">Step 4: Plan networking</span></span>

<span data-ttu-id="0939a-125">您需要 toodo 某些網路規劃 tooensure，您可以設定網路對應，當您部署的 hello 案例中，Azure Vm 將會連接的 tooAzure 虛擬網路之後發生容錯移轉，以及它們要指派適當的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0939a-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="0939a-126">跳過[步驟 4： 規劃的網路功能](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="0939a-127">步驟 5：準備 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="0939a-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="0939a-128">設定 Azure 帳戶、網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="0939a-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="0939a-129">您可以在部署期間執行這項操作，但建議您在開始之前進行。</span><span class="sxs-lookup"><span data-stu-id="0939a-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="0939a-130">跳過[步驟 5： 準備 Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="0939a-131">步驟 6：準備 VMM 和 Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0939a-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="0939a-132">準備站台復原 」 部署的 hello 在內部部署 VMM 伺服器和 HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="0939a-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="0939a-133">跳過[步驟 6： 準備內部部署伺服器](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="0939a-134">步驟 7：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="0939a-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="0939a-135">設定復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="0939a-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="0939a-136">hello 保存庫包含組態設定，並且會協調複寫。</span><span class="sxs-lookup"><span data-stu-id="0939a-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="0939a-137">步驟 7：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="0939a-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="0939a-138">步驟 8：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="0939a-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="0939a-139">設定 hello 來源和目標複寫的位置。</span><span class="sxs-lookup"><span data-stu-id="0939a-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="0939a-140">新增 hello VMM 伺服器 toohello 保存庫，並下載 Site Recovery 元件的 hello 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="0939a-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="0939a-141">Hello VMM 伺服器上執行 Azure Site Recovery Provider 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="0939a-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="0939a-142">安裝程式會在 hello VMM 伺服器上，安裝 hello 提供者，並登錄 hello 伺服器 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="0939a-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="0939a-143">您每個 HYPER-V 主機上安裝 hello Microsoft 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="0939a-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="0939a-144">跳過[步驟 8： 來源和目標設定](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="0939a-145">步驟 9：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="0939a-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="0939a-146">對應內部部署 VMM VM 網路 tooAzure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0939a-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="0939a-147">容錯移轉之後，Azure Vm 中建立 hello 對應 toohello 在內部部署的 VM 網路中的 hello 來源 HYPER-V 所在的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="0939a-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="0939a-148">跳過[步驟 9： 設定網路對應](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="0939a-149">步驟 10：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="0939a-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="0939a-150">指定如何在內部部署 Vm 會複寫的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="0939a-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="0939a-151">跳過[步驟 10： 設定複寫原則](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="0939a-152">步驟 11：啟用 VM 複寫</span><span class="sxs-lookup"><span data-stu-id="0939a-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="0939a-153">選取您想要 tooreplicate hello Vm。</span><span class="sxs-lookup"><span data-stu-id="0939a-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="0939a-154">啟用複寫觸發程序 hello 初始複寫 tooAzure 的 VM，後面接著進行中的差異複寫。</span><span class="sxs-lookup"><span data-stu-id="0939a-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="0939a-155">跳過[步驟 11： 啟用複寫](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="0939a-156">步驟 12：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="0939a-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="0939a-157">執行測試容錯移轉 toomake 確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="0939a-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="0939a-158">跳過[步驟 12： 執行測試容錯移轉](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="0939a-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


