---
title: "使用 Azure Site Recovery 將 VMware VM 複寫至 Azure | Microsoft Docs"
description: "概述將 VMware VM 上執行的工作負載複寫至 Azure 所需的步驟"
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
ms.openlocfilehash: db6f5f95929503e82a529dba26b56af1edb0767f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-vms-to-azure-with-site-recovery"></a><span data-ttu-id="6a647-103">使用 Site Recovery 將 VMWare VM 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="6a647-103">Replicate VMware VMs to Azure with Site Recovery</span></span>

<span data-ttu-id="6a647-104">本文概述在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署 VMware 虛擬機器複寫至 Azure 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="6a647-104">This article provides an overview of the steps required to replicate on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


![部署程序](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="6a647-106">**圖 1：部署程序摘要**</span><span class="sxs-lookup"><span data-stu-id="6a647-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="6a647-107">步驟 1：檢閱架構和必要條件</span><span class="sxs-lookup"><span data-stu-id="6a647-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="6a647-108">在開始部署之前，請檢閱案例架構，並確定您了解部署所需的一切元件</span><span class="sxs-lookup"><span data-stu-id="6a647-108">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="6a647-109">移至[步驟 1：檢閱架構](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-109">Go to [Step 1: Review the architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="6a647-110">步驟 2：檢閱必要條件</span><span class="sxs-lookup"><span data-stu-id="6a647-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="6a647-111">請確定您已備妥每個部署元件的必要條件：</span><span class="sxs-lookup"><span data-stu-id="6a647-111">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="6a647-112">**Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a647-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="6a647-113">**內部部署 Site Recovery 元件**：您需要有一部執行內部部署 Site Recovery 元件的機器。</span><span class="sxs-lookup"><span data-stu-id="6a647-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="6a647-114">**內部部署 VMware 必要條件**：您需要設定帳戶，以便讓 Site Recovery 能夠存取 VMware 伺服器和 VM。</span><span class="sxs-lookup"><span data-stu-id="6a647-114">**On-premises VMware prerequisites**: You need to set up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="6a647-115">**複寫的 VM**：您想要複寫的 VM 必須符合 Azure 需求，並且已安裝行動服務元件。</span><span class="sxs-lookup"><span data-stu-id="6a647-115">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements, and have the Mobility service component installed.</span></span>

<span data-ttu-id="6a647-116">移至[步驟 2：檢閱必要條件和限制](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-116">Go to [Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="6a647-117">步驟 3：規劃容量</span><span class="sxs-lookup"><span data-stu-id="6a647-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="6a647-118">如果您要執行完整部署，就必須了解需要哪些複寫資源。</span><span class="sxs-lookup"><span data-stu-id="6a647-118">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="6a647-119">有幾個工具可幫助您執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="6a647-119">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="6a647-120">移至步驟 2。</span><span class="sxs-lookup"><span data-stu-id="6a647-120">Go to Step 2.</span></span> <span data-ttu-id="6a647-121">如果您要進行快速設定來測試環境，則可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="6a647-121">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="6a647-122">移至[步驟 3：規劃容量](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-122">Go to [Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="6a647-123">步驟 4：規劃網路</span><span class="sxs-lookup"><span data-stu-id="6a647-123">Step 4: Plan networking</span></span>

<span data-ttu-id="6a647-124">您必須進行一些網路規劃，以確保 Azure VM 在發生容錯移轉之後會連線到網路，並且它們具有正確的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6a647-124">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="6a647-125">移至[步驟 4：規劃網路](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-125">Go to [Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="6a647-126">步驟 5：準備 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="6a647-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="6a647-127">在開始之前，請先設定 Azure 網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="6a647-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="6a647-128">您可以在部署期間執行這項操作，但建議您在開始之前進行。</span><span class="sxs-lookup"><span data-stu-id="6a647-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="6a647-129">移至[步驟 5：準備 Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-129">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="6a647-130">步驟 6：準備 VMware</span><span class="sxs-lookup"><span data-stu-id="6a647-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="6a647-131">您必須設定 Site Recovery 將用來執行下列操作的帳戶：</span><span class="sxs-lookup"><span data-stu-id="6a647-131">You need to set up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="6a647-132">存取 VMware 虛擬化伺服器以自動偵測 VM。</span><span class="sxs-lookup"><span data-stu-id="6a647-132">Access VMware virtualization servers to automatically detect VMs.</span></span>
- <span data-ttu-id="6a647-133">存取 VM 以安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="6a647-133">Access VMs to install the Mobility service.</span></span> <span data-ttu-id="6a647-134">您想要複寫的每個 VM 都必須先安裝行動服務代理程式，您才能為其啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="6a647-134">Each VM you want to replicate must have the Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="6a647-135">移至[步驟 6：準備 VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-135">Go to [Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="6a647-136">步驟 7：設定保存庫</span><span class="sxs-lookup"><span data-stu-id="6a647-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="6a647-137">您必須設定「復原服務」保存庫，才能協調和管理複寫。</span><span class="sxs-lookup"><span data-stu-id="6a647-137">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="6a647-138">當您設定保存庫時，請指定您想要複寫的項目，以及要將它複寫到何處。</span><span class="sxs-lookup"><span data-stu-id="6a647-138">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="6a647-139">移至[步驟 7：設定保存庫](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-139">Go to [Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="6a647-140">步驟 8：設定來源和目標設定</span><span class="sxs-lookup"><span data-stu-id="6a647-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="6a647-141">設定用於複寫的來源和目標。</span><span class="sxs-lookup"><span data-stu-id="6a647-141">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="6a647-142">設定來源設定包括執行「整合安裝」來安裝內部部署 Site Recovery 元件。</span><span class="sxs-lookup"><span data-stu-id="6a647-142">Setting up source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="6a647-143">移至[步驟 8：設定來源和目標](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-143">Go to [Step 8: Set up the source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="6a647-144">步驟 9：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="6a647-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="6a647-145">您需設定原則來為保存庫中的 VMware VM 指定複寫設定。</span><span class="sxs-lookup"><span data-stu-id="6a647-145">You set up a policy to specify replication settings for VMware VMs in the vault.</span></span>

<span data-ttu-id="6a647-146">移至[步驟 9：設定複寫原則](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-146">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="6a647-147">步驟 10：安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="6a647-147">Step 10: Install the Mobility service</span></span>

<span data-ttu-id="6a647-148">行動服務必須安裝在您要複寫的每個 VM 上。</span><span class="sxs-lookup"><span data-stu-id="6a647-148">The Mobility service must be installed on each VM you want to replicate.</span></span> <span data-ttu-id="6a647-149">有幾個方法可藉由推入或提取安裝來安裝服務。</span><span class="sxs-lookup"><span data-stu-id="6a647-149">There are a few ways to set up the service with push or pull installation.</span></span>

<span data-ttu-id="6a647-150">移至[步驟 10：安裝行動服務](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-150">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="6a647-151">步驟 11：啟用複寫</span><span class="sxs-lookup"><span data-stu-id="6a647-151">Step 11: Enable replication</span></span>

<span data-ttu-id="6a647-152">在行動服務於 VM 上執行之後，您便可以為其啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="6a647-152">After the Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="6a647-153">啟用複寫之後，就會進行初始 VM 複寫。</span><span class="sxs-lookup"><span data-stu-id="6a647-153">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="6a647-154">移至[步驟 11：啟用複寫](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-154">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="6a647-155">步驟 12：執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="6a647-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="6a647-156">在初始複寫完成且差異複寫執行之後，您可以執行測試容錯移轉，以確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="6a647-156">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="6a647-157">移至[步驟 12：執行測試容錯移轉](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="6a647-157">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
