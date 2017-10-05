---
title: "使用 Azure Site Recovery 來啟用將 Azure VM 複寫至其他 Azure 區域的複寫功能 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 服務來啟用將 VMware VM 複寫至 Azure 的複寫功能時所需的步驟"
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
ms.openlocfilehash: f426ba4341e61d3c7da820d7d5097b217e94ca0e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="d6585-103">步驟 5：啟用 Azure VM 的複寫</span><span class="sxs-lookup"><span data-stu-id="d6585-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="d6585-104">設定[復原服務保存庫](azure-to-azure-walkthrough-vault.md)之後，使用本文來啟用虛擬機器 (VM) 的複寫，以透過 [Azure Site Recovery](site-recovery-overview.md) 複寫到另一個 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="d6585-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article to enable replication of virtual machines (VMs), to another Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="d6585-105">若要啟用複寫，請設定來源和目標設定、驗證複寫原則，並選取您想要複寫的 VM。</span><span class="sxs-lookup"><span data-stu-id="d6585-105">To enable replication, you set up source and target settings, verify the replication policy, and select VMs you want to replicate.</span></span>

- <span data-ttu-id="d6585-106">當您完成本文時，Azure VM 應會複寫到次要 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="d6585-106">When you finish the article, your Azure VMs should be replicating to the secondary Azure region.</span></span>
- <span data-ttu-id="d6585-107">請在本文下方張貼意見，或在 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中提出問題</span><span class="sxs-lookup"><span data-stu-id="d6585-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="d6585-108">Azure VM 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="d6585-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-the-source"></a><span data-ttu-id="d6585-109">選取來源</span><span class="sxs-lookup"><span data-stu-id="d6585-109">Select the source</span></span> 

1. <span data-ttu-id="d6585-110">在復原服務保存庫中，按一下 [+複寫]。</span><span class="sxs-lookup"><span data-stu-id="d6585-110">In Recovery Services vaults, click the vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="d6585-111">在 [來源] 中，選取 [Azure-PREVIEW]。</span><span class="sxs-lookup"><span data-stu-id="d6585-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="d6585-112">在 [來源位置] 中，選取 VM 目前執行所在的來源 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="d6585-112">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="d6585-113">選取 VM 的 **Azure 虛擬機器部署模型**：[Resource Manager] 或 [傳統]。</span><span class="sxs-lookup"><span data-stu-id="d6585-113">Select the **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="d6585-114">對於 Resource Manager VM 選取**來源資源群組**，或對於傳統 VM 選取**雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="d6585-114">Select the **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="d6585-115">按一下 [確定]  來儲存設定。</span><span class="sxs-lookup"><span data-stu-id="d6585-115">Click **OK** to save the settings.</span></span>

    ![設定來源](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-the-vms"></a><span data-ttu-id="d6585-117">選取 VM</span><span class="sxs-lookup"><span data-stu-id="d6585-117">Select the VMs</span></span>

<span data-ttu-id="d6585-118">Site Recovery 會擷取與訂用帳戶和資源群組/雲端服務相關聯的 VM 清單。</span><span class="sxs-lookup"><span data-stu-id="d6585-118">Site Recovery retrieves a list of the VMs associated with the subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="d6585-119">在 [虛擬機器] 中，選取您要複寫的 VM。</span><span class="sxs-lookup"><span data-stu-id="d6585-119">In **Virtual Machines**, select the VMs you want to replicate.</span></span>
2. <span data-ttu-id="d6585-120">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="d6585-120">Click **OK**.</span></span>

    ![選取 VM](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="d6585-122">配置設定</span><span class="sxs-lookup"><span data-stu-id="d6585-122">Configure settings</span></span>

<span data-ttu-id="d6585-123">Site Recovery 會佈建目標區域 (根據來源區域設定) 及複寫原則的預設設定：</span><span class="sxs-lookup"><span data-stu-id="d6585-123">Site Recovery provisions default settings for the target region (based on the source region settings), and the replication policy:</span></span>

   - <span data-ttu-id="d6585-124">**目標位置**：您想要用於災害復原的目標區域。</span><span class="sxs-lookup"><span data-stu-id="d6585-124">**Target location**: The target region you want to use for disaster recovery.</span></span> <span data-ttu-id="d6585-125">我們建議目標位置符合 Site Recovery 保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="d6585-125">We recommend that the target location matches the location of the Site Recovery vault.</span></span>
   - <span data-ttu-id="d6585-126">**目標資源群組**：目標區域中的 Azure VM 在容錯移轉後所屬的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d6585-126">**Target resource group**: Resource group to which Azure VMs in the target region will belong after failover.</span></span> <span data-ttu-id="d6585-127">根據預設，Site Recovery 會在目標區域中建立具有 "asr" 尾碼的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="d6585-127">By default, Site Recovery creates a new resource group in the target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="d6585-128">**目標虛擬網路**：目標區域中的 Azure VM 在容錯移轉後所在的網路。</span><span class="sxs-lookup"><span data-stu-id="d6585-128">**Target virtual network**: The network in which Azure VMs in the target region will be located after failover.</span></span> <span data-ttu-id="d6585-129">根據預設，Site Recovery 會在目標區域中建立具有 "asr" 尾碼的新虛擬網路 (和子網路)。</span><span class="sxs-lookup"><span data-stu-id="d6585-129">By default, Site Recovery creates a new virtual network (and subnets) in the target region with an "asr" suffix.</span></span> <span data-ttu-id="d6585-130">此網路會對應至您的來源網路。</span><span class="sxs-lookup"><span data-stu-id="d6585-130">This network is mapped to your source network.</span></span> <span data-ttu-id="d6585-131">請注意，如果您需要在來源和目標位置保留相同的 IP 位址，請可以在 VM 的容錯移轉之後，指派特定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d6585-131">Note that you can assign a specific IP address after failover of a VM, if you need to retain the same IP address in the source and target locations.</span></span> 
   - <span data-ttu-id="d6585-132">**快取儲存體帳戶**：Site Recovery 會使用來源區域中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6585-132">**Cache storage accounts**: Site Recovery uses a storage account in the source region.</span></span> <span data-ttu-id="d6585-133">來源 VM 上的變更會在複寫到目標位置之前，先傳送到此帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6585-133">Changes on source VMs are sent to this account, before replication to the target location.</span></span> 
   - <span data-ttu-id="d6585-134">**目標儲存體帳戶**：根據預設，Site Recovery 會在目標區域中建立新的儲存體帳戶，以反映來源 VM 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6585-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in the target region, to mirror the source VM storage account.</span></span>
   -  <span data-ttu-id="d6585-135">**目標可用性設定組**：根據預設，Site Recovery 會在目標區域中建立具有 "asr" 尾碼的新可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="d6585-135">**Target availability sets**: By default, Site Recovery creates a new availability set in the target region, with the "asr" suffix.</span></span> 
   - <span data-ttu-id="d6585-136">**複寫原則名稱**：原則名稱。</span><span class="sxs-lookup"><span data-stu-id="d6585-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="d6585-137">**復原點保留**：根據預設，Site Recovery 會保留復原點 24 小時。</span><span class="sxs-lookup"><span data-stu-id="d6585-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="d6585-138">您可以設定介於 1 與 72 小時之間的值。</span><span class="sxs-lookup"><span data-stu-id="d6585-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="d6585-139">**應用程式一致性快照的頻率**：根據預設，Site Recovery 會每隔 4 小時製作一份應用程式一致性快照集。</span><span class="sxs-lookup"><span data-stu-id="d6585-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="d6585-140">您可以設定介於 1 與 12 小時之間的任何值。</span><span class="sxs-lookup"><span data-stu-id="d6585-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="d6585-141">資料會持續複寫：</span><span class="sxs-lookup"><span data-stu-id="d6585-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="d6585-142">損毀一致性復原點會在建立時維持一致的資料寫入順序。</span><span class="sxs-lookup"><span data-stu-id="d6585-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="d6585-143">如果您的應用程式設計成從損毀復原，但沒有資料不一致的情形，這類型的復原點通常就已足夠。</span><span class="sxs-lookup"><span data-stu-id="d6585-143">This type of recovery point is usually sufficient if your app is designed to recover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="d6585-144">系統會每隔數分鐘產生損毀一致性復原點。</span><span class="sxs-lookup"><span data-stu-id="d6585-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="d6585-145">使用這些復原點來容錯移轉和復原您的 VM，可依照分鐘的順序提供復原點目標 (RPO)。</span><span class="sxs-lookup"><span data-stu-id="d6585-145">Using these recovery points to fail over and recover your VMs provides a Recovery Point Objective (RPO) in the order of minutes.</span></span>
    - <span data-ttu-id="d6585-146">應用程式一致性復原點 (除了寫入順序一致性以外) 可確保執行中的應用程式會完成所有作業，並將緩衝區排清到磁碟 (應用程式靜止)。</span><span class="sxs-lookup"><span data-stu-id="d6585-146">App-consistent recovery points (in addition to write-order consistency) ensure that running apps complete all operations and flush buffers to disk (application quiescing).</span></span> <span data-ttu-id="d6585-147">建議您對資料庫應用程式 (例如 SQL Server、Oracle 和 Exchange) 使用這些復原點。</span><span class="sxs-lookup"><span data-stu-id="d6585-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="d6585-149">修改設定</span><span class="sxs-lookup"><span data-stu-id="d6585-149">Modify settings</span></span>

<span data-ttu-id="d6585-150">如果您想要修改目標與複寫原則設定，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d6585-150">If you want to modify target and replication policy settings, do the following:</span></span>

1. <span data-ttu-id="d6585-151">若要檢視或修改目標設定，請按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="d6585-151">To view or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="d6585-152">若要覆寫預設目標設定，請按一下 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="d6585-152">To override the default target settings, click **Customize**.</span></span> <span data-ttu-id="d6585-153">您可以指定目標資源群組、虛擬網路、可用性設定組和目標儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6585-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="d6585-154">只有在 VM 是來源範圍中某個設定組的一部分，您才能新增可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="d6585-154">You can only add availability sets if VMs are part of a set in the source region.</span></span>

    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="d6585-156">若要覆寫復原點和應用程式一致性快照集的複寫設定，請按一下[複寫原則] 旁邊的 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="d6585-156">To override replication settings for recovery points and app-consistent snapshots, click **Customize** next to **Replication Policy**.</span></span>
 
    ![配置設定](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="d6585-158">若要開始佈建目標資源，請按一下 [建立目標資源]。</span><span class="sxs-lookup"><span data-stu-id="d6585-158">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="d6585-159">佈建約需要一分鐘左右。</span><span class="sxs-lookup"><span data-stu-id="d6585-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="d6585-160">請勿在佈建期間關閉刀鋒視窗，否則需要從頭開始。</span><span class="sxs-lookup"><span data-stu-id="d6585-160">Don't close the blade during provisioning, or you'll have to start over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="d6585-161">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="d6585-161">Enable replication</span></span>

1. <span data-ttu-id="d6585-162">在 [設定] 中，按一下 [啟用複寫]。</span><span class="sxs-lookup"><span data-stu-id="d6585-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="d6585-163">這可進行您所選 VM 的初始複寫。</span><span class="sxs-lookup"><span data-stu-id="d6585-163">This enables initial replication of the VMs you selected.</span></span> <span data-ttu-id="d6585-164">初始複寫狀態可能需要一些時間才會重新整理。</span><span class="sxs-lookup"><span data-stu-id="d6585-164">Initial replication status might take some time to refresh.</span></span> <span data-ttu-id="d6585-165">按一下 [重新整理] 以取得最新狀態。</span><span class="sxs-lookup"><span data-stu-id="d6585-165">Click **Refresh** to get the latest status.</span></span>

2. <span data-ttu-id="d6585-166">您可以在 [設定]  >  [作業]  >  [Site Recovery 作業] 中，追蹤 [啟用保護] 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="d6585-166">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="d6585-167">在 [設定] > [複寫的項目] 中，您可以檢視 VM 的狀態和初始複寫進度。</span><span class="sxs-lookup"><span data-stu-id="d6585-167">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="d6585-168">按一下 VM 可向下鑽研其設定。</span><span class="sxs-lookup"><span data-stu-id="d6585-168">Click the VM to drill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="d6585-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6585-169">Next steps</span></span>

<span data-ttu-id="d6585-170">移至[步驟 6：執行測試容錯移轉](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="d6585-170">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
