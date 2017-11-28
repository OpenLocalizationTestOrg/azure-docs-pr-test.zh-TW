---
title: "使用 Azure Site Recovery 將 Hyper-V VM 複寫至次要 VMM 站台 | Microsoft Docs"
description: "提供使用 Azure 入口網站將 Hyper-V VM 複寫至次要 VMM 站台的概觀。"
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
ms.openlocfilehash: b422dd2cf23426de2f154a553b38509082536309
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a><span data-ttu-id="7ac14-103">將位於 VMM 雲端中的 Hyper-V 虛擬機器複寫至次要 VMM 站台</span><span class="sxs-lookup"><span data-stu-id="7ac14-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ac14-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7ac14-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="7ac14-105">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="7ac14-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="7ac14-106">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="7ac14-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="7ac14-107">本文提供的步驟概觀，是關於如何使用 Azure 入口網站中的 [Azure Site Recovery](site-recovery-overview.md)，將 System Center Virtual Machine Manager (VMM) 雲端中管理的內部部署 Hyper-V 虛擬機器 (VM) 複寫至次要 VMM 位置。</span><span class="sxs-lookup"><span data-stu-id="7ac14-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span>

<span data-ttu-id="7ac14-108">在閱讀本文之後，請在下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中張貼任何意見。</span><span class="sxs-lookup"><span data-stu-id="7ac14-108">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="7ac14-109">步驟 1：檢閱案例架構</span><span class="sxs-lookup"><span data-stu-id="7ac14-109">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="7ac14-110">在開始部署之前，請檢閱案例架構，並確定您了解部署所需的一切元件。</span><span class="sxs-lookup"><span data-stu-id="7ac14-110">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="7ac14-111">移至[步驟 1：檢閱架構](vmm-to-vmm-walkthrough-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-111">Go to [Step 1: Review the architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="7ac14-112">步驟 2：檢閱必要條件和限制</span><span class="sxs-lookup"><span data-stu-id="7ac14-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="7ac14-113">請確定您了解部署的必要條件和限制。</span><span class="sxs-lookup"><span data-stu-id="7ac14-113">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="7ac14-114">**Azure 必要條件**：您需要 Microsoft Azure 訂用帳戶和 Azure 復原服務保存庫，以協調和管理複寫。</span><span class="sxs-lookup"><span data-stu-id="7ac14-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, to orchestrate and manage replication.</span></span>
<span data-ttu-id="7ac14-115">**內部部署 VMM 伺服器和 Hyper-V 主機**：請確定 VMM 伺服器和 Hyper-V 主機符合 Site Recovery 部署的必要條件並已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="7ac14-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="7ac14-116">移至[步驟 2：確認必要條件和限制](vmm-to-vmm-walkthrough-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-116">Go to [Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="7ac14-117">步驟 3：規劃網路服務</span><span class="sxs-lookup"><span data-stu-id="7ac14-117">Step 3: Plan networking</span></span>

<span data-ttu-id="7ac14-118">您必須進行一些網路規劃，以確保部署案例時可以在 VMM VM 網路之間設定網路對應。</span><span class="sxs-lookup"><span data-stu-id="7ac14-118">You need to do some network planning to ensure that you can configure network mapping between VMM VM networks when you deploy the scenario.</span></span>

<span data-ttu-id="7ac14-119">移至[步驟 3：規劃網路服務](vmm-to-vmm-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-119">Go to [Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="7ac14-120">步驟 4：準備 VMM 和 Hyper-V</span><span class="sxs-lookup"><span data-stu-id="7ac14-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="7ac14-121">準備 Site Recovery 部署所需的 VMM 伺服器和 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="7ac14-121">Prepare the VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="7ac14-122">移至[步驟 4：準備內部部署伺服器](vmm-to-vmm-walkthrough-vmm-hyper-v.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-122">Go to [Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="7ac14-123">步驟 5：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="7ac14-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="7ac14-124">設定復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="7ac14-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="7ac14-125">保存庫包含組態設定，並協調複寫。</span><span class="sxs-lookup"><span data-stu-id="7ac14-125">The vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="7ac14-126">[步驟 5：設定保存庫](vmm-to-vmm-walkthrough-create-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="7ac14-127">步驟 6：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="7ac14-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="7ac14-128">設定來源和目標複寫 VMM 位置。</span><span class="sxs-lookup"><span data-stu-id="7ac14-128">Set up the source and target replication VMM locations.</span></span> <span data-ttu-id="7ac14-129">將 VMM 伺服器加入至保存庫，並下載 Site Recovery 元件的安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="7ac14-129">Add the VMM servers to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="7ac14-130">在 VMM 伺服器上執行 Azure Site Recovery Provider 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="7ac14-130">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="7ac14-131">安裝程式會在 VMM 伺服器上安裝 Provider，並在保存庫中註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="7ac14-131">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="7ac14-132">在每部 Hyper-V 主機上安裝 Microsoft 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="7ac14-132">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="7ac14-133">移至[步驟 6：設定來源和目標設定](vmm-to-vmm-walkthrough-source-target.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-133">Go to [Step 6: Set up the source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="7ac14-134">步驟 7：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="7ac14-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="7ac14-135">對應來源和目標位置中的 VMM VM 網路。</span><span class="sxs-lookup"><span data-stu-id="7ac14-135">Map VMM VM networks in the source and target locations.</span></span> <span data-ttu-id="7ac14-136">在容錯移轉後，會在與來源 Hyper-V VM 所在的來源 VM 網路對應的目標網路中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="7ac14-136">After failover, VMs are created in the target network that maps to the source VM network in which the source Hyper-V VM is located.</span></span>

<span data-ttu-id="7ac14-137">移至[步驟 7：設定網路對應](vmm-to-vmm-walkthrough-network-mapping.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-137">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="7ac14-138">步驟 8：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="7ac14-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="7ac14-139">指定 VM 在 VMM 位置之間的複寫方式。</span><span class="sxs-lookup"><span data-stu-id="7ac14-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="7ac14-140">移至[步驟 8：設定複寫原則](vmm-to-vmm-walkthrough-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-140">Go to [Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="7ac14-141">步驟 9：啟用 VM 複寫</span><span class="sxs-lookup"><span data-stu-id="7ac14-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="7ac14-142">選取您要複寫的 VM。</span><span class="sxs-lookup"><span data-stu-id="7ac14-142">Select the VMs you want to replicate.</span></span> <span data-ttu-id="7ac14-143">啟用 VM 複寫首先會複寫至次要站台，接著持續進行差異複寫。</span><span class="sxs-lookup"><span data-stu-id="7ac14-143">Enabling a VM for replication triggers the initial replication to the secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="7ac14-144">移至[步驟 9：啟用複寫](vmm-to-vmm-walkthrough-enable-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-144">Go to [Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="7ac14-145">步驟 10：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="7ac14-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="7ac14-146">執行測試容錯移轉，確定一切都沒問題。</span><span class="sxs-lookup"><span data-stu-id="7ac14-146">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="7ac14-147">移至[步驟 10：執行測試容錯移轉](vmm-to-vmm-walkthrough-test-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac14-147">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
