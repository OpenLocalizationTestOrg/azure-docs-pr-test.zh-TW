---
title: "使用 Azure Site Recovery 將 VMM 雲端中的 Hyper-V VM 複寫至 Azure | Microsoft Docs"
description: "提供使用 Azure Site Recovery 服務將 VMM 雲端中的 Hyper-V VM 複寫至 Azure 的概觀"
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
ms.openlocfilehash: af68d21184c137b2b0f1bb4c1afb9bf507e8332d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a><span data-ttu-id="f0c26-103">使用 Azure 入口網站中的 Site Recovery 將 Hyper-V 虛擬機器 (位於 VMM 雲端中) 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="f0c26-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0c26-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f0c26-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="f0c26-105">Azure 傳統型</span><span class="sxs-lookup"><span data-stu-id="f0c26-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="f0c26-106">PowerShell Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f0c26-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="f0c26-107">PowerShell 傳統</span><span class="sxs-lookup"><span data-stu-id="f0c26-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="f0c26-108">本文提供的步驟概觀，是關於使用 Azure 入口網站中的 [Azure Site Recovery](site-recovery-overview.md) 服務，將 System Center Virtual Machine Manager (VMM) 雲端中管理的內部部署 Hyper-V 虛擬機器 (VM) 複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f0c26-108">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="f0c26-109">在閱讀本文之後，請在下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中張貼任何意見。</span><span class="sxs-lookup"><span data-stu-id="f0c26-109">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="f0c26-110">步驟 1：檢閱案例架構</span><span class="sxs-lookup"><span data-stu-id="f0c26-110">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="f0c26-111">在開始部署之前，請檢閱案例架構，並確定您了解部署所需的一切元件。</span><span class="sxs-lookup"><span data-stu-id="f0c26-111">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="f0c26-112">移至[步驟 1：檢閱架構](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-112">Go to [Step 1: Review the architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="f0c26-113">步驟 2：檢閱必要條件和限制</span><span class="sxs-lookup"><span data-stu-id="f0c26-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="f0c26-114">請確定您了解部署的必要條件和限制。</span><span class="sxs-lookup"><span data-stu-id="f0c26-114">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="f0c26-115">**Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0c26-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="f0c26-116">**內部部署 VMM 伺服器和 Hyper-V 主機**：請確定 VMM 伺服器和 Hyper-V 主機符合 Site Recovery 部署的必要條件並已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="f0c26-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="f0c26-117">**複寫 VM**：請確定您想要複寫的 VM 符合 Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="f0c26-117">**Replicated VMs**: Check that VMs you want to replicate comply with Azure requirements.</span></span>

<span data-ttu-id="f0c26-118">移至[步驟 2：確認必要條件和限制](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-118">Go to [Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="f0c26-119">步驟 3：規劃容量</span><span class="sxs-lookup"><span data-stu-id="f0c26-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="f0c26-120">如果您要執行完整部署，就必須了解需要哪些複寫資源。</span><span class="sxs-lookup"><span data-stu-id="f0c26-120">If you're doing a full deployment, you need to figure out what replication resources you need.</span></span> <span data-ttu-id="f0c26-121">有幾個工具可幫助您執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="f0c26-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="f0c26-122">如果您要進行快速設定來測試環境，則可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="f0c26-122">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="f0c26-123">移至[步驟 3：規劃容量](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-123">Go to [Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="f0c26-124">步驟 4：規劃網路</span><span class="sxs-lookup"><span data-stu-id="f0c26-124">Step 4: Plan networking</span></span>

<span data-ttu-id="f0c26-125">您必須進行一些網路規劃，以確保部署案例時可以設定網路對應、Azure VM 在容錯移轉發生後將連線到 Azure 虛擬網路，以及為它們指派適當的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0c26-125">You need to do some network planning to ensure that you can configure network mapping when you deploy the scenario, that Azure VMs will be connected to Azure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="f0c26-126">移至[步驟 4：規劃網路](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-126">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="f0c26-127">步驟 5：準備 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="f0c26-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="f0c26-128">設定 Azure 帳戶、網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="f0c26-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="f0c26-129">您可以在部署期間執行這項操作，但建議您在開始之前進行。</span><span class="sxs-lookup"><span data-stu-id="f0c26-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="f0c26-130">移至[步驟 5：準備 Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-130">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="f0c26-131">步驟 6：準備 VMM 和 Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f0c26-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="f0c26-132">準備 Site Recovery 部署所需的內部部署 VMM 伺服器和 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="f0c26-132">Prepare the on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="f0c26-133">移至[步驟 6：準備內部部署伺服器](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-133">Go to [Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="f0c26-134">步驟 7：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="f0c26-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="f0c26-135">設定復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="f0c26-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="f0c26-136">保存庫包含組態設定，並協調複寫。</span><span class="sxs-lookup"><span data-stu-id="f0c26-136">The vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="f0c26-137">步驟 7：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="f0c26-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="f0c26-138">步驟 8：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="f0c26-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="f0c26-139">設定來源和目標複寫位置。</span><span class="sxs-lookup"><span data-stu-id="f0c26-139">Set up the source and target replication locations.</span></span> <span data-ttu-id="f0c26-140">將 VMM 伺服器加入至保存庫，並下載 Site Recovery 元件的安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="f0c26-140">Add the VMM server to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="f0c26-141">在 VMM 伺服器上執行 Azure Site Recovery Provider 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="f0c26-141">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="f0c26-142">安裝程式會在 VMM 伺服器上安裝 Provider，並在保存庫中註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="f0c26-142">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="f0c26-143">在每部 Hyper-V 主機上安裝 Microsoft 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="f0c26-143">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="f0c26-144">移至[步驟 8：設定來源和目標設定](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-144">Go to [Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="f0c26-145">步驟 9：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="f0c26-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="f0c26-146">對應內部部署 VMM VM 網路和 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f0c26-146">Map on-premises VMM VM networks to Azure virtual networks.</span></span> <span data-ttu-id="f0c26-147">在容錯移轉後，會在與來源 Hyper-V 所在的內部部署 VM 網路對應的 Azure 網路中建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="f0c26-147">After failover, Azure VMs are created in the Azure network that maps to the on-premises VM network in which the source Hyper-V is located.</span></span>

<span data-ttu-id="f0c26-148">移至[步驟 9：設定網路對應](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-148">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="f0c26-149">步驟 10：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="f0c26-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="f0c26-150">指定內部部署 VM 複寫至 Azure 的方式。</span><span class="sxs-lookup"><span data-stu-id="f0c26-150">Specify how on-premises VMs will be replicated to Azure.</span></span>

<span data-ttu-id="f0c26-151">移至[步驟 10：設定複寫原則](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-151">Go to [Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="f0c26-152">步驟 11：啟用 VM 複寫</span><span class="sxs-lookup"><span data-stu-id="f0c26-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="f0c26-153">選取您要複寫的 VM。</span><span class="sxs-lookup"><span data-stu-id="f0c26-153">Select the VMs you want to replicate.</span></span> <span data-ttu-id="f0c26-154">啟用 VM 複寫首先會複寫至 Azure，接著持續進行差異複寫。</span><span class="sxs-lookup"><span data-stu-id="f0c26-154">ENabling a VM for replication triggers the initial replication to Azure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="f0c26-155">移至[步驟 11：啟用複寫](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-155">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="f0c26-156">步驟 12：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f0c26-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="f0c26-157">執行測試容錯移轉，確定一切都沒問題。</span><span class="sxs-lookup"><span data-stu-id="f0c26-157">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="f0c26-158">移至[步驟 12：執行測試容錯移轉](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="f0c26-158">Go to [Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


