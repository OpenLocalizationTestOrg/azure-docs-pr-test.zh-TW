---
title: "Azure Vm tooanother 與 Azure Site Recovery 的 Azure 區域的 aaaEnable 複寫 |Microsoft 文件"
description: "摘要說明您需要 tooenable 複寫 tooanother Azure 地區的 Azure Vm，使用 hello Azure Site Recovery 服務的 hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="27ffd-103">步驟 5：啟用 Azure VM 的複寫</span><span class="sxs-lookup"><span data-stu-id="27ffd-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="27ffd-104">設定好後[復原服務保存庫](azure-to-azure-walkthrough-vault.md)，搭配使用的虛擬機器 (Vm)，tooanother Azure 區域，此文章 tooenable 複寫[Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="27ffd-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="27ffd-105">tooenable 複寫，您設定來源和目標設定，確認 hello 複寫原則，，並選取您想要 tooreplicate 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="27ffd-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="27ffd-106">當您完成 hello 發行項，您的 Azure Vm 應該複寫 toohello 次要 Azure 地區。</span><span class="sxs-lookup"><span data-stu-id="27ffd-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="27ffd-107">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="27ffd-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="27ffd-108">Azure VM 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="27ffd-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="27ffd-109">選取 hello 來源</span><span class="sxs-lookup"><span data-stu-id="27ffd-109">Select hello source</span></span> 

1. <span data-ttu-id="27ffd-110">在 復原服務保存庫中，按一下 hello 保存庫名稱 > **+ 複寫**。</span><span class="sxs-lookup"><span data-stu-id="27ffd-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="27ffd-111">在 [來源] 中，選取 [Azure-PREVIEW]。</span><span class="sxs-lookup"><span data-stu-id="27ffd-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="27ffd-112">在**來源位置**，選取 hello 來源 Vm 目前的執行所在的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="27ffd-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="27ffd-113">選取 hello **Azure 虛擬機器部署模型**vm:**資源管理員**或**傳統**。</span><span class="sxs-lookup"><span data-stu-id="27ffd-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="27ffd-114">選取 hello**來源資源群組**對於資源管理員的 Vm，或**雲端服務**用於傳統的 Vm。</span><span class="sxs-lookup"><span data-stu-id="27ffd-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="27ffd-115">按一下**確定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="27ffd-115">Click **OK** toosave hello settings.</span></span>

    ![設定 hello 來源](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="27ffd-117">選取 hello Vm</span><span class="sxs-lookup"><span data-stu-id="27ffd-117">Select hello VMs</span></span>

<span data-ttu-id="27ffd-118">Site Recovery 擷取的 hello 與 hello 訂用帳戶和資源群組/雲端服務相關聯的 Vm 清單。</span><span class="sxs-lookup"><span data-stu-id="27ffd-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="27ffd-119">在**虛擬機器**，選取您想要 tooreplicate hello Vm。</span><span class="sxs-lookup"><span data-stu-id="27ffd-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="27ffd-120">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="27ffd-120">Click **OK**.</span></span>

    ![選取 VM](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="27ffd-122">配置設定</span><span class="sxs-lookup"><span data-stu-id="27ffd-122">Configure settings</span></span>

<span data-ttu-id="27ffd-123">Site Recovery 會佈建 hello 目標區域 （根據 hello 來源地區設定），預設設定和 hello 複寫原則：</span><span class="sxs-lookup"><span data-stu-id="27ffd-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="27ffd-124">**目標位置**: hello 想 toouse 災害復原的目標區域。</span><span class="sxs-lookup"><span data-stu-id="27ffd-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="27ffd-125">我們建議 hello 目標位置符合 hello hello Site Recovery 保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="27ffd-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="27ffd-126">**目標資源群組**： 容錯移轉之後將屬於的資源群組 toowhich hello 目標區域中的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="27ffd-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="27ffd-127">根據預設，站台復原會建立新的資源群組具有"asr"後置詞 hello 目標區域中。</span><span class="sxs-lookup"><span data-stu-id="27ffd-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="27ffd-128">**目標虛擬網路**: hello hello 中哪一個 Azure Vm 中目標區域即將放置在容錯移轉後的網路。</span><span class="sxs-lookup"><span data-stu-id="27ffd-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="27ffd-129">根據預設，站台復原會在"asr"尾碼的 hello 目標區域中建立新的虛擬網路 （和子網路）。</span><span class="sxs-lookup"><span data-stu-id="27ffd-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="27ffd-130">此網路是對應的 tooyour 來源網路。</span><span class="sxs-lookup"><span data-stu-id="27ffd-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="27ffd-131">請注意，您可以指派特定的 IP 位址在虛擬機器的容錯移轉之後，如果您需要 tooretain hello 相同的 IP 位址 hello 來源和目標位置。</span><span class="sxs-lookup"><span data-stu-id="27ffd-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="27ffd-132">**快取儲存體帳戶**： 站台復原 hello 來源範圍中使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="27ffd-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="27ffd-133">來源 Vm 上的變更會傳送 toothis 帳戶之前複寫 toohello 目標位置。</span><span class="sxs-lookup"><span data-stu-id="27ffd-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="27ffd-134">**目標儲存體帳戶**： 根據預設，站台復原會建立新的儲存體帳戶在 hello 目標區域中，toomirror hello 來源 VM 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="27ffd-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="27ffd-135">**目標可用性設定組**： 根據預設，站台復原會建立新的可用性設定組與 hello"asr"後置字元的 hello 目標區域中。</span><span class="sxs-lookup"><span data-stu-id="27ffd-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="27ffd-136">**複寫原則名稱**：原則名稱。</span><span class="sxs-lookup"><span data-stu-id="27ffd-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="27ffd-137">**復原點保留**：根據預設，Site Recovery 會保留復原點 24 小時。</span><span class="sxs-lookup"><span data-stu-id="27ffd-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="27ffd-138">您可以設定介於 1 與 72 小時之間的值。</span><span class="sxs-lookup"><span data-stu-id="27ffd-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="27ffd-139">**應用程式一致性快照的頻率**：根據預設，Site Recovery 會每隔 4 小時製作一份應用程式一致性快照集。</span><span class="sxs-lookup"><span data-stu-id="27ffd-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="27ffd-140">您可以設定介於 1 與 12 小時之間的任何值。</span><span class="sxs-lookup"><span data-stu-id="27ffd-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="27ffd-141">資料會持續複寫：</span><span class="sxs-lookup"><span data-stu-id="27ffd-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="27ffd-142">損毀一致性復原點會在建立時維持一致的資料寫入順序。</span><span class="sxs-lookup"><span data-stu-id="27ffd-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="27ffd-143">這種類型的復原點通常已足夠如果您的應用程式是從損毀不含資料不一致的設計的 toorecover</span><span class="sxs-lookup"><span data-stu-id="27ffd-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="27ffd-144">系統會每隔數分鐘產生損毀一致性復原點。</span><span class="sxs-lookup"><span data-stu-id="27ffd-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="27ffd-145">透過使用這些復原點 toofail 和復原您的 Vm 提供 hello 幾分鐘的復原點目標 (RPO)。</span><span class="sxs-lookup"><span data-stu-id="27ffd-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="27ffd-146">執行應用程式完成所有操作，而排清緩衝區 toodisk （應用程式停止），請確定 （在加法 toowrite 順序一致性） 的應用程式一致的復原點。</span><span class="sxs-lookup"><span data-stu-id="27ffd-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="27ffd-147">建議您對資料庫應用程式 (例如 SQL Server、Oracle 和 Exchange) 使用這些復原點。</span><span class="sxs-lookup"><span data-stu-id="27ffd-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="27ffd-149">修改設定</span><span class="sxs-lookup"><span data-stu-id="27ffd-149">Modify settings</span></span>

<span data-ttu-id="27ffd-150">如果您想 toomodify 目標與複寫原則設定時，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="27ffd-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="27ffd-151">tooview 或修改目標設定，請按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="27ffd-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="27ffd-152">toooverride hello 預設目標設定，請按一下**自訂**。</span><span class="sxs-lookup"><span data-stu-id="27ffd-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="27ffd-153">您可以指定目標資源群組、虛擬網路、可用性設定組和目標儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="27ffd-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="27ffd-154">如果 Vm 是 hello 來源範圍中的一組的一部分，您只可以加入可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="27ffd-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="27ffd-156">復原點和應用程式一致快照集，toooverride 複寫設定，請按一下**自訂**下一步太**複寫原則**。</span><span class="sxs-lookup"><span data-stu-id="27ffd-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="27ffd-158">按一下 佈建 hello 目標資源 toostart，**建立目標資源**。</span><span class="sxs-lookup"><span data-stu-id="27ffd-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="27ffd-159">佈建約需要一分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="27ffd-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="27ffd-160">不要關閉 hello 刀鋒視窗中，佈建，期間或您必須透過 toostart。</span><span class="sxs-lookup"><span data-stu-id="27ffd-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="27ffd-161">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="27ffd-161">Enable replication</span></span>

1. <span data-ttu-id="27ffd-162">在 [設定] 中，按一下 [啟用複寫]。</span><span class="sxs-lookup"><span data-stu-id="27ffd-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="27ffd-163">這可讓您選取的 Vm hello 的初始複寫。</span><span class="sxs-lookup"><span data-stu-id="27ffd-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="27ffd-164">初始複寫狀態可能需要一些時間 toorefresh。</span><span class="sxs-lookup"><span data-stu-id="27ffd-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="27ffd-165">按一下**重新整理**tooget hello 最新狀態。</span><span class="sxs-lookup"><span data-stu-id="27ffd-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="27ffd-166">您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**.</span><span class="sxs-lookup"><span data-stu-id="27ffd-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="27ffd-167">在**設定** > **複寫的項目**，您可以檢視 hello 狀態的 Vm 和 hello 初始複寫正在進行。</span><span class="sxs-lookup"><span data-stu-id="27ffd-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="27ffd-168">向下一直按 hello VM toodrill，其設定。</span><span class="sxs-lookup"><span data-stu-id="27ffd-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="27ffd-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27ffd-169">Next steps</span></span>

<span data-ttu-id="27ffd-170">跳過[步驟 6： 執行測試容錯移轉](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="27ffd-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
