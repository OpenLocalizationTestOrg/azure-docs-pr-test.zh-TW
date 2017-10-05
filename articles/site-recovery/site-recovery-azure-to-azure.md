---
title: "對於災害復原需求，複寫 Azure 區域之間的 Azure VM：Azure 至 Azure |Microsoft Docs"
description: "摘要說明對於災害復原需求，使用 Azure Site Recovery 服務在 Azure 區域 (Azure 至 Azure) 之間複寫 Azure VM 所需的步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: 9ca33057f6030fdcc233f6053fdc392d62f8f9f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="972ed-103">使用 Azure Site Recovery 在區域之間椱寫 Azure VM</span><span class="sxs-lookup"><span data-stu-id="972ed-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="972ed-104">Azure 虛擬機器 (VM) 的 Azure Site Recovery 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="972ed-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="972ed-105">本文說明如何在 Azure 入口網站中使用 [Site Recovery](site-recovery-overview.md) 服務，在 Azure 區域之間複寫 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="972ed-105">This article describes how to replicate Azure VMs between Azure regions by using the [Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="972ed-106">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) (英文) 上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="972ed-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="972ed-107">Azure 的災害復原</span><span class="sxs-lookup"><span data-stu-id="972ed-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="972ed-108">對於在 Azure VM 上執行的工作負載而言，內建的 Azure 基礎結構功用和功能提供強固且彈性的可用性策略。</span><span class="sxs-lookup"><span data-stu-id="972ed-108">Built-in Azure infrastructure capabilities and features contribute to a robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="972ed-109">不過，您經常需要自行規劃 Azure 區域之間的災害復原：</span><span class="sxs-lookup"><span data-stu-id="972ed-109">However, there are many reasons why you need to plan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="972ed-110">對於需要業務續航力和災害復原 (BCDR) 策略的特定應用程式和工作負載，您必須符合合規性指導方針。</span><span class="sxs-lookup"><span data-stu-id="972ed-110">You need to meet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="972ed-111">您想要能夠根據您的商務決策保護和復原 Azure VM，而不只根據內建的 Azure 功能。</span><span class="sxs-lookup"><span data-stu-id="972ed-111">You want the ability to protect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="972ed-112">您需要根據商務與合規性需求測試容錯移轉和復原，而不影響生產環境。</span><span class="sxs-lookup"><span data-stu-id="972ed-112">You need to test failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="972ed-113">您需要在發生災害時容錯移轉到復原區域，並順暢地容錯回復到原始的來源地區。</span><span class="sxs-lookup"><span data-stu-id="972ed-113">You need to fail over to the recovery region in the event of a disaster and fail back to the original source region seamlessly.</span></span>

<span data-ttu-id="972ed-114">使用 Azure-Azure VM 複寫的 Site Recovery 可協助您執行所有這些工作。</span><span class="sxs-lookup"><span data-stu-id="972ed-114">Use Site Recovery for Azure-to-Azure VM replication to help you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="972ed-115">為什麼要使用 Site Recovery？</span><span class="sxs-lookup"><span data-stu-id="972ed-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="972ed-116">Site Recovery 提供在區域之間複寫 Azure VM 的簡易方式：</span><span class="sxs-lookup"><span data-stu-id="972ed-116">Site Recovery provides a simple way to replicate Azure VMs between regions:</span></span>

- <span data-ttu-id="972ed-117">**自動部署**。</span><span class="sxs-lookup"><span data-stu-id="972ed-117">**Automatic deployment**.</span></span> <span data-ttu-id="972ed-118">不同於主動-主動複寫模型，次要地區不需要昂貴且複雜的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="972ed-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in the secondary region.</span></span> <span data-ttu-id="972ed-119">您啟用複寫時，Site Recovery 會根據來源地區設定，在目標區域中自動建立所需的資源。</span><span class="sxs-lookup"><span data-stu-id="972ed-119">When you enable replication, Site Recovery automatically creates the required resources in the target region, based on source region settings.</span></span>
- <span data-ttu-id="972ed-120">**控制區域**。</span><span class="sxs-lookup"><span data-stu-id="972ed-120">**Control regions**.</span></span> <span data-ttu-id="972ed-121">使用 Site Recovery，即可從同一洲的任何地區複寫到任何地區。</span><span class="sxs-lookup"><span data-stu-id="972ed-121">With Site Recovery, you can replicate from any region to any region within a continent.</span></span> <span data-ttu-id="972ed-122">使用讀取權限異地備援儲存體 (僅以非同步方式在標準[配對區域](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)之間複寫) 比較此項。</span><span class="sxs-lookup"><span data-stu-id="972ed-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="972ed-123">讀取權限異地備援儲存體提供目標區域資料的唯讀存取權限。</span><span class="sxs-lookup"><span data-stu-id="972ed-123">Read-access geo-redundant storage provides read-only access to the data in the target region.</span></span>
- <span data-ttu-id="972ed-124">**自動化複寫**。</span><span class="sxs-lookup"><span data-stu-id="972ed-124">**Automated replication**.</span></span> <span data-ttu-id="972ed-125">Site Recovery 提供自動化連續複寫。</span><span class="sxs-lookup"><span data-stu-id="972ed-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="972ed-126">按一下即可觸發容錯移轉和容錯回復。</span><span class="sxs-lookup"><span data-stu-id="972ed-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="972ed-127">**RTO 和 RPO**。</span><span class="sxs-lookup"><span data-stu-id="972ed-127">**RTO and RPO**.</span></span> <span data-ttu-id="972ed-128">Site Recovery 會利用連線區域的 Azure 網路基礎結構，維持相當低的 RTO 和 RPO。</span><span class="sxs-lookup"><span data-stu-id="972ed-128">Site Recovery takes advantage of the Azure network infrastructure that connects regions to keep RTO and RPO very low.</span></span>
- <span data-ttu-id="972ed-129">**測試**。</span><span class="sxs-lookup"><span data-stu-id="972ed-129">**Testing**.</span></span> <span data-ttu-id="972ed-130">您可藉由隨選測試容錯移轉視需要執行災害復原演練，完全不影響生產工作負載或進行中的複寫。</span><span class="sxs-lookup"><span data-stu-id="972ed-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="972ed-131">**復原計劃**。</span><span class="sxs-lookup"><span data-stu-id="972ed-131">**Recovery plans**.</span></span> <span data-ttu-id="972ed-132">您可以使用復原計劃，對於在多個 VM 上執行的整個應用程式協調容錯移轉和容錯回復。</span><span class="sxs-lookup"><span data-stu-id="972ed-132">You can use recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="972ed-133">復原計劃功能已與 Azure 自動化 Runbook 達到絕佳的一流整合。</span><span class="sxs-lookup"><span data-stu-id="972ed-133">The recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="972ed-134">部署摘要</span><span class="sxs-lookup"><span data-stu-id="972ed-134">Deployment summary</span></span>

<span data-ttu-id="972ed-135">以下摘要說明設定在 Azure 區域之間執行 VM 複寫所需的步驟：</span><span class="sxs-lookup"><span data-stu-id="972ed-135">Here's a summary of what you need to do to set up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="972ed-136">建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="972ed-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="972ed-137">保存庫包含組態設定，並會協調複寫。</span><span class="sxs-lookup"><span data-stu-id="972ed-137">The vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="972ed-138">啟用 Azure VM 的複寫。</span><span class="sxs-lookup"><span data-stu-id="972ed-138">Enable replication for the Azure VMs.</span></span>
3. <span data-ttu-id="972ed-139">執行測試容錯移轉，確定一切都沒問題。</span><span class="sxs-lookup"><span data-stu-id="972ed-139">Run a test failover to make sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="972ed-140">您可以檢查 [Azure VM 複寫的支援矩陣](./site-recovery-support-matrix-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="972ed-140">You can check the [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="972ed-141">如需如何對於 Azure VM 設定所需網路輸出連線能力進行 Site Recovery 複寫的資訊，請參閱[網路指引文件](./site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="972ed-141">For information on how to configure the required network outbound connectivity for Azure VMs for Site Recovery replication, see the [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="972ed-142">開始之前</span><span class="sxs-lookup"><span data-stu-id="972ed-142">Before you start</span></span>

* <span data-ttu-id="972ed-143">您的 Azure 使用者帳戶必須具有特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)，才能啟用 Azure 虛擬機器的複寫功能。</span><span class="sxs-lookup"><span data-stu-id="972ed-143">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="972ed-144">必須啟用您的 Azure 訂用帳戶，才能在要做為災害復原區域的目標位置中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="972ed-144">Your Azure subscription should be enabled to create VMs in the target location that you want to use as the disaster recovery region.</span></span> <span data-ttu-id="972ed-145">請連絡支援人員啟用所需的配額。</span><span class="sxs-lookup"><span data-stu-id="972ed-145">Contact support to enable the required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="972ed-146">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="972ed-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="972ed-147">建議您在要 VM 複寫的位置中，建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="972ed-147">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="972ed-148">例如，如果您的目標位置是美國中部、請在**美國中部**建立保存庫。</span><span class="sxs-lookup"><span data-stu-id="972ed-148">For example, if your target location is the central US, create the vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="972ed-149">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="972ed-149">Enable replication</span></span>

<span data-ttu-id="972ed-150">在 [復原服務保存庫] 中，按一下保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="972ed-150">In **Recovery Services vaults**, click the vault name.</span></span> <span data-ttu-id="972ed-151">在保存庫中，按一下 [+ 複寫] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="972ed-151">In the vault, click the **+Replicate** button.</span></span>

### <a name="step-1-configure-the-source"></a><span data-ttu-id="972ed-152">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="972ed-152">Step 1.</span></span> <span data-ttu-id="972ed-153">設定來源</span><span class="sxs-lookup"><span data-stu-id="972ed-153">Configure the source</span></span>
1. <span data-ttu-id="972ed-154">在 [來源] 中，選取 [Azure-PREVIEW]。</span><span class="sxs-lookup"><span data-stu-id="972ed-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="972ed-155">在 [來源位置] 中，選取 VM 目前執行所在的來源 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="972ed-155">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="972ed-156">選取 VM 的部署模型：[資源管理員] 或 [傳統]。</span><span class="sxs-lookup"><span data-stu-id="972ed-156">Select the deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="972ed-157">對於資源管理員 VM 選取**來源資源群組**，或對於傳統 VM 選取**雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="972ed-157">Select the **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![設定來源](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="972ed-159">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="972ed-159">Step 2.</span></span> <span data-ttu-id="972ed-160">選取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="972ed-160">Select virtual machines</span></span>

* <span data-ttu-id="972ed-161">選取要複寫的 VM，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="972ed-161">Select the VMs you want to replicate, and then click **OK**.</span></span>

    ![選取 VM](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="972ed-163">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="972ed-163">Step 3.</span></span> <span data-ttu-id="972ed-164">配置設定</span><span class="sxs-lookup"><span data-stu-id="972ed-164">Configure settings</span></span>

1. <span data-ttu-id="972ed-165">若要覆寫預設的目標設定，並指定您選擇的設定，請按一下 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="972ed-165">To override the default target settings and specify the settings of your choice, click **Customize**.</span></span> <span data-ttu-id="972ed-166">如需詳細資訊，請參閱[自訂目標資源](site-recovery-replicate-azure-to-azure.md##customize-target-resources)。</span><span class="sxs-lookup"><span data-stu-id="972ed-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![配置設定](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="972ed-168">根據預設，Site Recovery 會建立複寫原則，每隔 4 小時會製作應用程式一致快照，並將復原點保留 24 小時。</span><span class="sxs-lookup"><span data-stu-id="972ed-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="972ed-169">若要使用不同的設定建立原則，請按一下 [複寫原則] 旁的 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="972ed-169">To create a policy with different settings, click **Customize** next to **Replication Policy**.</span></span>

    ![自訂原則](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="972ed-171">若要開始佈建目標資源，請按一下 [建立目標資源]。</span><span class="sxs-lookup"><span data-stu-id="972ed-171">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="972ed-172">佈建約需要一分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="972ed-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="972ed-173">請勿在佈建期間關閉刀鋒視窗，否則需要從頭開始。</span><span class="sxs-lookup"><span data-stu-id="972ed-173">Don't close the blade during provisioning, or you need to start over.</span></span>

4. <span data-ttu-id="972ed-174">若要觸發所選 VM 的複寫，請按一下 [啟用複寫]。</span><span class="sxs-lookup"><span data-stu-id="972ed-174">To trigger replication of the selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="972ed-175">您可以在 [設定]  >  [作業]  >  [Site Recovery 作業] 中，追蹤 [啟用保護] 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="972ed-175">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="972ed-176">在 [設定] > [複寫的項目] 中，您可以檢視 VM 的狀態和初始複寫進度。</span><span class="sxs-lookup"><span data-stu-id="972ed-176">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="972ed-177">按一下 VM 可向下鑽研其設定。</span><span class="sxs-lookup"><span data-stu-id="972ed-177">Click the VM to drill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="972ed-178">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="972ed-178">Run a test failover</span></span>

<span data-ttu-id="972ed-179">一切就緒後，執行測試容錯移轉，確定一切如預期般運作：</span><span class="sxs-lookup"><span data-stu-id="972ed-179">After you set up everything, run a test failover to make sure everything's working as expected:</span></span>

1. <span data-ttu-id="972ed-180">若要容錯移轉單一機器，請在 [設定]  >  [複寫的項目] 中，按一下 VM [+測試容錯移轉] 圖示。</span><span class="sxs-lookup"><span data-stu-id="972ed-180">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="972ed-181">若要容錯移轉復原方案，請在 [設定]  >  [復原方案] 中，以滑鼠右鍵按一下方案 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="972ed-181">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan **Test Failover**.</span></span> <span data-ttu-id="972ed-182">若要建立復原方案，請[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="972ed-182">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="972ed-183">在 [測試容錯移轉] 中，選取 Azure VM 在容錯移轉之後所要連線的目標 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="972ed-183">In **Test Failover**, select the target Azure virtual network to which Azure VMs are connected after the failover occurs.</span></span>

4. <span data-ttu-id="972ed-184">若要開始容錯移轉，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="972ed-184">To start the failover, click **OK**.</span></span> <span data-ttu-id="972ed-185">若要追蹤進度，請按一下 VM 開啟其內容。</span><span class="sxs-lookup"><span data-stu-id="972ed-185">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="972ed-186">您也可以按一下保存庫名稱中的 [測試容錯移轉]作業 > [設定] > [作業] > [Site Recovery 作業]。</span><span class="sxs-lookup"><span data-stu-id="972ed-186">Or you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="972ed-187">容錯移轉完成之後，複本 Azure 電腦會出現在 Azure 入口網站> [虛擬機器] 中。</span><span class="sxs-lookup"><span data-stu-id="972ed-187">After the failover finishes, the replica Azure machine appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="972ed-188">請確定 VM 為適當的大小、已連線到適當的網路，而且正在執行中。</span><span class="sxs-lookup"><span data-stu-id="972ed-188">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="972ed-189">若要刪除測試容錯移轉期間建立的 VM，請按一下複寫的項目或復原計劃上的 [清除測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="972ed-189">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="972ed-190">在 [記事] 中，記錄並儲存關於測試容錯移轉的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="972ed-190">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="972ed-191">[深入了解](site-recovery-test-failover-to-azure.md)測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="972ed-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="972ed-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="972ed-192">Next steps</span></span>

<span data-ttu-id="972ed-193">測試部署後：</span><span class="sxs-lookup"><span data-stu-id="972ed-193">After you test the deployment:</span></span>

- <span data-ttu-id="972ed-194">[深入了解](site-recovery-failover.md)不同類型的容錯移轉及執行方法。</span><span class="sxs-lookup"><span data-stu-id="972ed-194">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="972ed-195">深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)降低 RTO。</span><span class="sxs-lookup"><span data-stu-id="972ed-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
