---
title: "複寫 Azure 區域之間的 Azure Vm 的災害復原需求： Azure tooAzure |Microsoft 文件"
description: "摘要說明您需要 tooreplicate Azure Vm 與嚴重損壞修復所需的 hello Azure Site Recovery 服務的 Azure 區域 (Azure-Azure) 之間的 hello 步驟。"
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
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="8af70-103">使用 Azure Site Recovery 在區域之間椱寫 Azure VM</span><span class="sxs-lookup"><span data-stu-id="8af70-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="8af70-104">Azure 虛擬機器 (VM) 的 Azure Site Recovery 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="8af70-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="8af70-105">本文說明如何使用 Azure 的區域之間的 Azure Vm tooreplicate hello [Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="8af70-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="8af70-106">在這份文件或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="8af70-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="8af70-107">Azure 的災害復原</span><span class="sxs-lookup"><span data-stu-id="8af70-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="8af70-108">內建的 Azure 基礎結構的功能和功能都在 Azure Vm 執行的工作負載的 tooa 健全且彈性的可用性策略。</span><span class="sxs-lookup"><span data-stu-id="8af70-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="8af70-109">不過，有許多為什麼您需要 tooplan 之間的 Azure 地區的災害復原自己的原因：</span><span class="sxs-lookup"><span data-stu-id="8af70-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="8af70-110">您需要特定的應用程式和工作負載所需的業務續航力和災害復原 (BCDR) 策略 toomeet 規範指導方針。</span><span class="sxs-lookup"><span data-stu-id="8af70-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="8af70-111">您想 hello 能力 tooprotect 並復原 Azure Vm，根據您的商務決策而不只根據內建的 Azure 功能。</span><span class="sxs-lookup"><span data-stu-id="8af70-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="8af70-112">根據您的商務與相容性需求，而不會影響生產環境中需要 tootest 容錯移轉和復原。</span><span class="sxs-lookup"><span data-stu-id="8af70-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="8af70-113">您需要 toofail toohello hello 災害事件中的復原區域，並順暢地容錯回復 toohello 原始的來源地區。</span><span class="sxs-lookup"><span data-stu-id="8af70-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="8af70-114">使用站台復原您的 Azure-Azure VM 複寫 toohelp 所有這些工作。</span><span class="sxs-lookup"><span data-stu-id="8af70-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="8af70-115">為什麼要使用 Site Recovery？</span><span class="sxs-lookup"><span data-stu-id="8af70-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="8af70-116">站台復原提供簡單的方式 tooreplicate Azure Vm 之間的區域：</span><span class="sxs-lookup"><span data-stu-id="8af70-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="8af70-117">**自動部署**。</span><span class="sxs-lookup"><span data-stu-id="8af70-117">**Automatic deployment**.</span></span> <span data-ttu-id="8af70-118">不是主動-主動複寫模型，像沒有需要高而且非常複雜的基礎結構 hello 次要區域中。</span><span class="sxs-lookup"><span data-stu-id="8af70-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="8af70-119">當您啟用複寫時，站台復原會自動建立所需的 hello 資源在 hello 目標區域中，取決於來源地區設定。</span><span class="sxs-lookup"><span data-stu-id="8af70-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="8af70-120">**控制區域**。</span><span class="sxs-lookup"><span data-stu-id="8af70-120">**Control regions**.</span></span> <span data-ttu-id="8af70-121">使用站台復原，也可以從中的任何區域 tooany 區域大陸複寫。</span><span class="sxs-lookup"><span data-stu-id="8af70-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="8af70-122">使用讀取權限異地備援儲存體 (僅以非同步方式在標準[配對區域](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)之間複寫) 比較此項。</span><span class="sxs-lookup"><span data-stu-id="8af70-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="8af70-123">讀取權限的地理備援儲存體提供唯讀存取 toohello 資料在 hello 目標區域中。</span><span class="sxs-lookup"><span data-stu-id="8af70-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="8af70-124">**自動化複寫**。</span><span class="sxs-lookup"><span data-stu-id="8af70-124">**Automated replication**.</span></span> <span data-ttu-id="8af70-125">Site Recovery 提供自動化連續複寫。</span><span class="sxs-lookup"><span data-stu-id="8af70-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="8af70-126">按一下即可觸發容錯移轉和容錯回復。</span><span class="sxs-lookup"><span data-stu-id="8af70-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="8af70-127">**RTO 和 RPO**。</span><span class="sxs-lookup"><span data-stu-id="8af70-127">**RTO and RPO**.</span></span> <span data-ttu-id="8af70-128">站台復原會利用連接區域 tookeep hello Azure 網路基礎結構 RTO 和 RPO 非常低。</span><span class="sxs-lookup"><span data-stu-id="8af70-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="8af70-129">**測試**。</span><span class="sxs-lookup"><span data-stu-id="8af70-129">**Testing**.</span></span> <span data-ttu-id="8af70-130">您可藉由隨選測試容錯移轉視需要執行災害復原演練，完全不影響生產工作負載或進行中的複寫。</span><span class="sxs-lookup"><span data-stu-id="8af70-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="8af70-131">**復原計劃**。</span><span class="sxs-lookup"><span data-stu-id="8af70-131">**Recovery plans**.</span></span> <span data-ttu-id="8af70-132">您可以使用復原計劃 tooorchestrate 容錯移轉和容錯回復 hello 整個應用程式在多個 Vm 上執行。</span><span class="sxs-lookup"><span data-stu-id="8af70-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="8af70-133">hello 復原計劃功能具有豐富的第一級整合與 Azure 自動化 runbook。</span><span class="sxs-lookup"><span data-stu-id="8af70-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="8af70-134">部署摘要</span><span class="sxs-lookup"><span data-stu-id="8af70-134">Deployment summary</span></span>

<span data-ttu-id="8af70-135">以下是所需的摘要 toodo tooset Vm 的 Azure 區域之間的複寫設定：</span><span class="sxs-lookup"><span data-stu-id="8af70-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="8af70-136">建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8af70-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="8af70-137">hello 保存庫包含組態設定，並且會協調複寫。</span><span class="sxs-lookup"><span data-stu-id="8af70-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="8af70-138">啟用複寫 hello Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="8af70-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="8af70-139">執行測試容錯移轉 toomake 確定所有內容都如預期運作。</span><span class="sxs-lookup"><span data-stu-id="8af70-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="8af70-140">您可以檢查 hello[支援比對 Azure VM 複寫](./site-recovery-support-matrix-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="8af70-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="8af70-141">如需如何 tooconfigure hello 複寫所需輸出的網路連線的 Azure Vm 的站台復原資訊，請參閱 hello[網路指引文件](./site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="8af70-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="8af70-142">開始之前</span><span class="sxs-lookup"><span data-stu-id="8af70-142">Before you start</span></span>

* <span data-ttu-id="8af70-143">您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)tooenable 的 Azure 虛擬機器的複寫。</span><span class="sxs-lookup"><span data-stu-id="8af70-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="8af70-144">您的 Azure 訂用帳戶應啟用的 toocreate Vm，您想為 hello 災害復原區域 toouse hello 目標位置中。</span><span class="sxs-lookup"><span data-stu-id="8af70-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="8af70-145">請連絡客戶支援 tooenable hello 必要的配額。</span><span class="sxs-lookup"><span data-stu-id="8af70-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8af70-146">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="8af70-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="8af70-147">我們建議您在您想要 Vm tooreplicate hello 位置建立 hello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8af70-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="8af70-148">例如，如果您的目標位置是 hello 中央而我們，建立 hello 保存庫中的**美國中部**。</span><span class="sxs-lookup"><span data-stu-id="8af70-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="8af70-149">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="8af70-149">Enable replication</span></span>

<span data-ttu-id="8af70-150">在**復原服務保存庫**，按一下 hello 保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="8af70-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="8af70-151">在 hello 保存庫中，按一下 hello **+ 複寫** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8af70-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="8af70-152">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="8af70-152">Step 1.</span></span> <span data-ttu-id="8af70-153">設定 hello 來源</span><span class="sxs-lookup"><span data-stu-id="8af70-153">Configure hello source</span></span>
1. <span data-ttu-id="8af70-154">在 [來源] 中，選取 [Azure-PREVIEW]。</span><span class="sxs-lookup"><span data-stu-id="8af70-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="8af70-155">在**來源位置**，選取 hello 來源 Vm 目前的執行所在的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="8af70-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="8af70-156">選取 hello 的 Vm 的部署模型：**資源管理員**或**傳統**。</span><span class="sxs-lookup"><span data-stu-id="8af70-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="8af70-157">選取 hello**來源資源群組**資源管理員 vm 或**雲端服務**用於傳統的 Vm。</span><span class="sxs-lookup"><span data-stu-id="8af70-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![設定 hello 來源](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="8af70-159">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="8af70-159">Step 2.</span></span> <span data-ttu-id="8af70-160">選取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8af70-160">Select virtual machines</span></span>

* <span data-ttu-id="8af70-161">選取您想 tooreplicate，然後再按一下 hello Vm**確定**。</span><span class="sxs-lookup"><span data-stu-id="8af70-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![選取 VM](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="8af70-163">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="8af70-163">Step 3.</span></span> <span data-ttu-id="8af70-164">配置設定</span><span class="sxs-lookup"><span data-stu-id="8af70-164">Configure settings</span></span>

1. <span data-ttu-id="8af70-165">toooverride hello 預設設定為目標，並指定 hello 設定您的選擇，按一下**自訂**。</span><span class="sxs-lookup"><span data-stu-id="8af70-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="8af70-166">如需詳細資訊，請參閱[自訂目標資源](site-recovery-replicate-azure-to-azure.md##customize-target-resources)。</span><span class="sxs-lookup"><span data-stu-id="8af70-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![配置設定](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="8af70-168">根據預設，Site Recovery 會建立複寫原則，每隔 4 小時會製作應用程式一致快照，並將復原點保留 24 小時。</span><span class="sxs-lookup"><span data-stu-id="8af70-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="8af70-169">按一下 toocreate 具有不同的設定原則**自訂**下一步太**複寫原則**。</span><span class="sxs-lookup"><span data-stu-id="8af70-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![自訂原則](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="8af70-171">按一下 佈建 hello 目標資源 toostart，**建立目標資源**。</span><span class="sxs-lookup"><span data-stu-id="8af70-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="8af70-172">佈建約需要一分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="8af70-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="8af70-173">不要關閉 hello 刀鋒視窗中，佈建，期間或您需要 toostart 比。</span><span class="sxs-lookup"><span data-stu-id="8af70-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="8af70-174">hello tootrigger 複寫選取 VM，請按一下**啟用複寫**。</span><span class="sxs-lookup"><span data-stu-id="8af70-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="8af70-175">您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**.</span><span class="sxs-lookup"><span data-stu-id="8af70-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="8af70-176">在**設定** > **複寫的項目**，您可以檢視 hello 狀態的 Vm 和 hello 初始複寫正在進行。</span><span class="sxs-lookup"><span data-stu-id="8af70-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="8af70-177">向下一直按 hello VM toodrill，其設定。</span><span class="sxs-lookup"><span data-stu-id="8af70-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="8af70-178">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="8af70-178">Run a test failover</span></span>

<span data-ttu-id="8af70-179">您設定的所有項目之後，執行測試容錯移轉 toomake 確定一切如預期般運作：</span><span class="sxs-lookup"><span data-stu-id="8af70-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="8af70-180">透過單一電腦、 toofail 中**設定** > **複寫的項目**，按一下 hello VM **+ 測試容錯移轉**圖示。</span><span class="sxs-lookup"><span data-stu-id="8af70-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="8af70-181">toofail 透過復原計劃，在**設定** > **復原計劃**，以滑鼠右鍵按一下 hello 計劃**測試容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="8af70-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="8af70-182">復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="8af70-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="8af70-183">在**測試容錯移轉**，選取 hello 容錯移轉發生後連接 hello 目標 Azure 虛擬網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="8af70-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="8af70-184">toostart hello 容錯移轉，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="8af70-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="8af70-185">tootrack 進度，請按一下 hello VM tooopen 其屬性。</span><span class="sxs-lookup"><span data-stu-id="8af70-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="8af70-186">或者您可以按一下 hello**測試容錯移轉**作業在 hello 保存庫名稱 >**設定** > **作業** > **的站台復原工作**.</span><span class="sxs-lookup"><span data-stu-id="8af70-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="8af70-187">Hello 之後容錯移轉完成時，hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="8af70-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="8af70-188">請確定該 hello VM hello 適當的大小，它已連接 toohello 適當的網路，而且它正在執行。</span><span class="sxs-lookup"><span data-stu-id="8af70-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="8af70-189">按一下 toodelete hello hello 測試容錯移轉期間所建立的 Vm**清除測試容錯移轉**hello 上複寫項目或 hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="8af70-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="8af70-190">在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="8af70-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="8af70-191">[深入了解](site-recovery-test-failover-to-azure.md)測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="8af70-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8af70-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8af70-192">Next steps</span></span>

<span data-ttu-id="8af70-193">之後，您會測試 hello 部署：</span><span class="sxs-lookup"><span data-stu-id="8af70-193">After you test hello deployment:</span></span>

- <span data-ttu-id="8af70-194">[進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉以及 toorun 它們。</span><span class="sxs-lookup"><span data-stu-id="8af70-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="8af70-195">深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)tooreduce RTO。</span><span class="sxs-lookup"><span data-stu-id="8af70-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
