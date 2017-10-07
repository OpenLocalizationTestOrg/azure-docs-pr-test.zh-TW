---
title: "實體伺服器複寫 tooAzure 與 Azure Site Recovery 的 aaaEnable 複寫 |Microsoft 文件"
description: "摘要說明您需要 tooenable 複寫 tooAzure 對於實體伺服器，請使用 hello Azure Site Recovery 服務的 hello 步驟"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a><span data-ttu-id="3bfa5-103">步驟 10： 啟用複寫功能的實體伺服器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="3bfa5-103">Step 10: Enable replication for physical servers tooAzure</span></span>


<span data-ttu-id="3bfa5-104">本文說明如何針對 tooenable 複寫在內部部署 Windows/Linux 實體伺服器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-104">This article describes how tooenable replication for on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="3bfa5-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="3bfa5-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="3bfa5-106">Before you start</span></span>

- <span data-ttu-id="3bfa5-107">伺服器必須擁有 hello[安裝行動服務元件](physical-walkthrough-install-mobility.md)。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-107">Servers must have hello [Mobility service component installed](physical-walkthrough-install-mobility.md).</span></span>
- <span data-ttu-id="3bfa5-108">如果 VM 備妥推入安裝，hello 處理序伺服器在啟用複寫時自動安裝 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-108">If a VM is prepared for push installation, hello process server automatically installs hello Mobility service when you enable replication.</span></span>
- <span data-ttu-id="3bfa5-109">當您啟用來複寫的電腦時，您的 Azure 使用者帳戶需要特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)tooensure 你可以 toouse Azure 儲存體，但建立 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-109">When you enable a machine for replication, your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure you're able toouse Azure storage, and create Azure VMs.</span></span>
- <span data-ttu-id="3bfa5-110">當您新增或修改伺服器的 IP 位址時，可能需要向上 too15 分鐘或更久變更 tootake 效果，以及它們 tooappear hello 入口網站中的。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-110">When you add or modify IP addresses for servers, it can take up too15 minutes or longer for changes tootake effect, and for them tooappear in hello portal.</span></span>


## <a name="exclude-disks-from-replication"></a><span data-ttu-id="3bfa5-111">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="3bfa5-111">Exclude disks from replication</span></span>

<span data-ttu-id="3bfa5-112">依預設會複寫電腦上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-112">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="3bfa5-113">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-113">You can exclude disks from replication.</span></span> <span data-ttu-id="3bfa5-114">例如您可能不想 tooreplicate 磁碟具有暫存資料或重新整理每次在電腦的資料或應用程式重新啟動 （例如 pagefile.sys 或 SQL Server tempdb）。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-114">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="3bfa5-115">深入了解</span><span class="sxs-lookup"><span data-stu-id="3bfa5-115">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a><span data-ttu-id="3bfa5-116">複寫伺服器</span><span class="sxs-lookup"><span data-stu-id="3bfa5-116">Replicate servers</span></span>

1. <span data-ttu-id="3bfa5-117">按一下 [步驟 2: 複寫應用程式]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-117">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="3bfa5-118">在**來源**，選取 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-118">In **Source**, select hello configuration server.</span></span>
3. <span data-ttu-id="3bfa5-119">在 [機器類型] 中，選取 [實體機器]。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-119">In **Machine type**, select **Physical Machines**.</span></span>
4. <span data-ttu-id="3bfa5-120">選取 hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-120">Select hello process server.</span></span> <span data-ttu-id="3bfa5-121">如果您尚未建立任何額外的處理序伺服器，這會是 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-121">If you haven't created any additional process servers this will be hello configuration server.</span></span> <span data-ttu-id="3bfa5-122">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-122">Then click **OK**.</span></span>
5. <span data-ttu-id="3bfa5-123">在**目標**選取 hello 訂用帳戶，hello 想 toocreate hello 容錯移轉 Vm 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-123">In **Target**, select hello subscription and hello resource group in which you want toocreate hello failed over VMs.</span></span> <span data-ttu-id="3bfa5-124">選擇要容錯移轉 Vm hello toouse （classic 或資源管理），Azure 中的 hello 部署模型。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-124">Choose hello deployment model that you want toouse in Azure (classic or resource management), for hello failed over VMs.</span></span>
6. <span data-ttu-id="3bfa5-125">選取要用於複寫資料 toouse hello Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-125">Select hello Azure storage account you want toouse for replicating data.</span></span> <span data-ttu-id="3bfa5-126">如果您不想 toouse 您已經設定的帳戶，您可以建立一個新。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-126">If you don't want toouse an account you've already set up, you can create a new one.</span></span>
7. <span data-ttu-id="3bfa5-127">選取 hello **Azure 網路**和**子網路**toowhich Azure Vm 容錯移轉之後連接。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-127">Select hello **Azure network** and **Subnet** toowhich Azure VMs connect after failover.</span></span> <span data-ttu-id="3bfa5-128">選取**現在選取的機器設定**tooapply hello 網路設定 tooall 您選取的機器進行保護。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-128">Select **Configure now for selected machines** tooapply hello network setting tooall machines you select for protection.</span></span> <span data-ttu-id="3bfa5-129">選取**稍後設定**tooselect hello 每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-129">Select **Configure later** tooselect hello Azure network per machine.</span></span> <span data-ttu-id="3bfa5-130">如果您不想 toouse 現有網路，您可以建立一個。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-130">If you don't want toouse an existing network, you can create one.</span></span>

    ![啟用複寫](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. <span data-ttu-id="3bfa5-132">在**實體機器**，按一下  **+ 實體機器**，然後輸入 hello**名稱**和**IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-132">In **Physical machines**, click **+Physical machine** and enter hello **Name** and **IP address**.</span></span> <span data-ttu-id="3bfa5-133">選擇 hello 作業系統要 tooreplicate 的 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-133">Choose hello operating system of hello machine you want tooreplicate.</span></span> <span data-ttu-id="3bfa5-134">花幾分鐘的時間之前的電腦系統會探索並 hello 清單所示。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-134">It takes a few minutes until machines are discovered and shown in hello list.</span></span>
9. <span data-ttu-id="3bfa5-135">在**屬性** > **設定屬性**，選取將由 hello 處理序伺服器 tooautomatically 的 hello 帳戶 hello 機器上安裝 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-135">In **Properties** > **Configure properties**, select hello account that will be used by hello process server tooautomatically install hello Mobility service on hello machine.</span></span>
10. <span data-ttu-id="3bfa5-136">依預設會複寫所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-136">By default all disks are replicated.</span></span> <span data-ttu-id="3bfa5-137">按一下**所有磁碟**並清除您不想 tooreplicate 任何磁碟。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-137">Click **All Disks** and clear any disks you don't want tooreplicate.</span></span> <span data-ttu-id="3bfa5-138">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-138">Then click **OK**.</span></span> <span data-ttu-id="3bfa5-139">您可以稍後再設定其他 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-139">You can set additional VM properties later.</span></span>

    ![啟用複寫](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="3bfa5-141">在**複寫設定** > **設定複寫設定**，確認該 hello 正確選取複寫原則。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-141">In **Replication settings** > **Configure replication settings**, verify that hello correct replication policy is selected.</span></span> <span data-ttu-id="3bfa5-142">如果您修改原則時，將變更套用的 tooreplicating 機器和 toonew 機器。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-142">If you modify a policy, changes will be applied tooreplicating machine, and toonew machines.</span></span>
12. <span data-ttu-id="3bfa5-143">啟用**多重 VM 一致性**如果 toogather 機器的複寫群組，並指定 hello 群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-143">Enable **Multi-VM consistency** if you want toogather machines into a replication group, and specify a name for hello group.</span></span> <span data-ttu-id="3bfa5-144">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-144">Then click **OK**.</span></span> <span data-ttu-id="3bfa5-145">請注意：</span><span class="sxs-lookup"><span data-stu-id="3bfa5-145">Note that:</span></span>

    * <span data-ttu-id="3bfa5-146">複寫群組中的電腦會一起複寫，並且在容錯移轉時會有共用的損毀一致和應用程式一致的復原點。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-146">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="3bfa5-147">建議您將實體伺服器收集在一起，以便它們能夠反映您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-147">We recommend that you gather physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="3bfa5-148">啟用多重 VM 一致性可能會影響工作負載的效能，應該只用於如果機器 hello 執行相同的工作負載，且需要一致性。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-148">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running hello same workload and you need consistency.</span></span>

13. <span data-ttu-id="3bfa5-149">按一下 [啟用複寫] 。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-149">Click **Enable Replication**.</span></span> <span data-ttu-id="3bfa5-150">您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**.</span><span class="sxs-lookup"><span data-stu-id="3bfa5-150">You can track progress of hello **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="3bfa5-151">之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="3bfa5-151">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bfa5-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bfa5-152">Next steps</span></span>

<span data-ttu-id="3bfa5-153">跳過[步驟 11： 執行測試容錯移轉](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="3bfa5-153">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>
