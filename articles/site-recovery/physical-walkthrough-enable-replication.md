---
title: "使用 Azure Site Recovery 來啟用將實體伺服器複寫至 Azure 的複寫功能 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 服務來啟用將實體伺服器複寫至 Azure 的複寫功能時所需的步驟"
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
ms.openlocfilehash: 42f35c53eec06a346281fd90c97aecfd2269307d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-physical-servers-to-azure"></a><span data-ttu-id="112dc-103">步驟 10：啟用將實體伺服器複寫至 Azure 的複寫功能</span><span class="sxs-lookup"><span data-stu-id="112dc-103">Step 10: Enable replication for physical servers to Azure</span></span>


<span data-ttu-id="112dc-104">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務，來啟用將內部部署 Windows/Linux 實體伺服器複寫至 Azure 的複寫功能。</span><span class="sxs-lookup"><span data-stu-id="112dc-104">This article describes how to enable replication for on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="112dc-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="112dc-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="112dc-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="112dc-106">Before you start</span></span>

- <span data-ttu-id="112dc-107">伺服器必須[已安裝行動服務元件](physical-walkthrough-install-mobility.md)。</span><span class="sxs-lookup"><span data-stu-id="112dc-107">Servers must have the [Mobility service component installed](physical-walkthrough-install-mobility.md).</span></span>
- <span data-ttu-id="112dc-108">如果已準備好 VM 進行推入安裝，當您啟用複寫時，處理序伺服器會自動安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="112dc-108">If a VM is prepared for push installation, the process server automatically installs the Mobility service when you enable replication.</span></span>
- <span data-ttu-id="112dc-109">啟用機器的複寫功能時，您的 Azure 使用者帳戶必須具有特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)，以確保您能夠使用 Azure 儲存體及建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="112dc-109">When you enable a machine for replication, your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to ensure you're able to use Azure storage, and create Azure VMs.</span></span>
- <span data-ttu-id="112dc-110">當您新增或修改伺服器的 IP 位址時，可能需要 15 分鐘或更久，變更才會生效，也才會出現在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="112dc-110">When you add or modify IP addresses for servers, it can take up to 15 minutes or longer for changes to take effect, and for them to appear in the portal.</span></span>


## <a name="exclude-disks-from-replication"></a><span data-ttu-id="112dc-111">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="112dc-111">Exclude disks from replication</span></span>

<span data-ttu-id="112dc-112">依預設會複寫電腦上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="112dc-112">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="112dc-113">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="112dc-113">You can exclude disks from replication.</span></span> <span data-ttu-id="112dc-114">例如，您可能不想要複寫具有暫存資料的磁碟，或是每次機器或應用程式重新啟動時便重新整理的資料 (例如 pagefile.sys 或 SQL Server tempdb)。</span><span class="sxs-lookup"><span data-stu-id="112dc-114">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="112dc-115">深入了解</span><span class="sxs-lookup"><span data-stu-id="112dc-115">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a><span data-ttu-id="112dc-116">複寫伺服器</span><span class="sxs-lookup"><span data-stu-id="112dc-116">Replicate servers</span></span>

1. <span data-ttu-id="112dc-117">按一下 [步驟 2: 複寫應用程式]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="112dc-117">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="112dc-118">在 [來源] 中，選取設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="112dc-118">In **Source**, select the configuration server.</span></span>
3. <span data-ttu-id="112dc-119">在 [機器類型] 中，選取 [實體機器]。</span><span class="sxs-lookup"><span data-stu-id="112dc-119">In **Machine type**, select **Physical Machines**.</span></span>
4. <span data-ttu-id="112dc-120">選取處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="112dc-120">Select the process server.</span></span> <span data-ttu-id="112dc-121">如果您尚未建立任何額外的處理序伺服器，則這會成為設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="112dc-121">If you haven't created any additional process servers this will be the configuration server.</span></span> <span data-ttu-id="112dc-122">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="112dc-122">Then click **OK**.</span></span>
5. <span data-ttu-id="112dc-123">在 [目標] 中，選取您想要在其中建立容錯移轉 VM 的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="112dc-123">In **Target**, select the subscription and the resource group in which you want to create the failed over VMs.</span></span> <span data-ttu-id="112dc-124">選擇您想要在 Azure (傳統或資源管理) 中，針對容錯移轉 VM 使用的部署模型。</span><span class="sxs-lookup"><span data-stu-id="112dc-124">Choose the deployment model that you want to use in Azure (classic or resource management), for the failed over VMs.</span></span>
6. <span data-ttu-id="112dc-125">選取您要用來複寫資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="112dc-125">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="112dc-126">如果您不想要使用已設定的帳戶，您可以建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="112dc-126">If you don't want to use an account you've already set up, you can create a new one.</span></span>
7. <span data-ttu-id="112dc-127">選取 Azure VM 在容錯移轉後所要連線的 **Azure 網路**和**子網路**。</span><span class="sxs-lookup"><span data-stu-id="112dc-127">Select the **Azure network** and **Subnet** to which Azure VMs connect after failover.</span></span> <span data-ttu-id="112dc-128">選取 [立即設定選取的機器]，將網路設定套用至您選取要進行保護的所有機器。</span><span class="sxs-lookup"><span data-stu-id="112dc-128">Select **Configure now for selected machines** to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="112dc-129">選取 [稍後設定] 以選取每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="112dc-129">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="112dc-130">如果您不想使用現有的網路，您可以建立網路。</span><span class="sxs-lookup"><span data-stu-id="112dc-130">If you don't want to use an existing network, you can create one.</span></span>

    ![啟用複寫](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. <span data-ttu-id="112dc-132">在**實體機器**中，按一下 [+實體機器]，然後輸入**名稱**和 **IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="112dc-132">In **Physical machines**, click **+Physical machine** and enter the **Name** and **IP address**.</span></span> <span data-ttu-id="112dc-133">選擇您想要複寫之電腦的作業系統。</span><span class="sxs-lookup"><span data-stu-id="112dc-133">Choose the operating system of the machine you want to replicate.</span></span> <span data-ttu-id="112dc-134">需要花費數分鐘的時間，才能探索到電腦並加以顯示於清單中。</span><span class="sxs-lookup"><span data-stu-id="112dc-134">It takes a few minutes until machines are discovered and shown in the list.</span></span>
9. <span data-ttu-id="112dc-135">在 [名稱]  > 中，選取處理序伺服器將用來在機器上自動安裝行動服務的帳戶。</span><span class="sxs-lookup"><span data-stu-id="112dc-135">In **Properties** > **Configure properties**, select the account that will be used by the process server to automatically install the Mobility service on the machine.</span></span>
10. <span data-ttu-id="112dc-136">依預設會複寫所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="112dc-136">By default all disks are replicated.</span></span> <span data-ttu-id="112dc-137">按一下 [所有磁碟]  ，然後將任何您不想要複寫的磁碟取消選取。</span><span class="sxs-lookup"><span data-stu-id="112dc-137">Click **All Disks** and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="112dc-138">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="112dc-138">Then click **OK**.</span></span> <span data-ttu-id="112dc-139">您可以稍後再設定其他 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="112dc-139">You can set additional VM properties later.</span></span>

    ![啟用複寫](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="112dc-141">在 [複寫設定] > [設定複寫設定] 中，確認已選取正確的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="112dc-141">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="112dc-142">如果您修改原則，變更會套用至複寫電腦及新的電腦。</span><span class="sxs-lookup"><span data-stu-id="112dc-142">If you modify a policy, changes will be applied to replicating machine, and to new machines.</span></span>
12. <span data-ttu-id="112dc-143">如果您想要將機器聚集成一個複寫群組，請啟用 [多部 VM 一致性]  ，並指定群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="112dc-143">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="112dc-144">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="112dc-144">Then click **OK**.</span></span> <span data-ttu-id="112dc-145">請注意：</span><span class="sxs-lookup"><span data-stu-id="112dc-145">Note that:</span></span>

    * <span data-ttu-id="112dc-146">複寫群組中的電腦會一起複寫，並且在容錯移轉時會有共用的損毀一致和應用程式一致的復原點。</span><span class="sxs-lookup"><span data-stu-id="112dc-146">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="112dc-147">建議您將實體伺服器收集在一起，以便它們能夠反映您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="112dc-147">We recommend that you gather physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="112dc-148">啟用多部 VM 一致性可能會影響工作負載的效能，應該只用於機器正在執行相同工作負載，且您需要一致性的情況。</span><span class="sxs-lookup"><span data-stu-id="112dc-148">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running the same workload and you need consistency.</span></span>

13. <span data-ttu-id="112dc-149">按一下 [啟用複寫] 。</span><span class="sxs-lookup"><span data-stu-id="112dc-149">Click **Enable Replication**.</span></span> <span data-ttu-id="112dc-150">您可以在 [設定]  >  [作業]  >  [Site Recovery 作業] 中，追蹤 [啟用保護] 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="112dc-150">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="112dc-151">執行 [完成保護]  作業之後，機器即準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="112dc-151">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="112dc-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="112dc-152">Next steps</span></span>

<span data-ttu-id="112dc-153">移至[步驟 11：執行測試容錯移轉](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="112dc-153">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>
