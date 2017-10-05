---
title: "Site Recovery 中的容錯移轉 | Microsoft Docs"
description: "Azure Site Recovery 可協調虛擬機器和實體伺服器的複寫、容錯移轉及復原作業。 了解如何容錯移轉到 Azure 或次要資料中心。"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: ef586191f0b89dca89810644d45503fe42538635
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="failover-in-site-recovery"></a><span data-ttu-id="ff66d-104">Site Recovery 中的容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ff66d-104">Failover in Site Recovery</span></span>
<span data-ttu-id="ff66d-105">本文說明如何容錯移轉 Site Recovery 所保護的虛擬機器和實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff66d-105">This article describes how to failover virtual machines and physical servers protected by Site Recovery.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff66d-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff66d-106">Prerequisites</span></span>
1. <span data-ttu-id="ff66d-107">執行容錯移轉之前，請執行[測試容錯移轉](site-recovery-test-failover-to-azure.md)，以確保一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="ff66d-107">Before you do a failover, do a [test failover](site-recovery-test-failover-to-azure.md) to ensure that everything is working as expected.</span></span>
1. <span data-ttu-id="ff66d-108">執行容錯移轉之前，在目標位置[準備網路](site-recovery-network-design.md)。</span><span class="sxs-lookup"><span data-stu-id="ff66d-108">[Prepare the network](site-recovery-network-design.md) at target location before you do a failover.</span></span>  


## <a name="run-a-failover"></a><span data-ttu-id="ff66d-109">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ff66d-109">Run a failover</span></span>
<span data-ttu-id="ff66d-110">此程序說明如何針對[復原方案](site-recovery-create-recovery-plans.md)執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-110">This procedure describes how to run a failover for a [recovery plan](site-recovery-create-recovery-plans.md).</span></span> <span data-ttu-id="ff66d-111">或者，您可以從 [複寫的項目] 頁面，針對單一虛擬機器或實體伺服器執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-111">Alternatively you can run the failover for a single virtual machine or physical server from the **Replicated items** page</span></span>


![容錯移轉](./media/site-recovery-failover/Failover.png)

1. <span data-ttu-id="ff66d-113">選取 [復原方案]  >  *recoveryplan_name*。</span><span class="sxs-lookup"><span data-stu-id="ff66d-113">Select **Recovery Plans** > *recoveryplan_name*.</span></span> <span data-ttu-id="ff66d-114">按一下 [容錯移轉]</span><span class="sxs-lookup"><span data-stu-id="ff66d-114">Click **Failover**</span></span>
2. <span data-ttu-id="ff66d-115">在 [容錯移轉]畫面上，選取要容錯移轉到的 [復原點]。</span><span class="sxs-lookup"><span data-stu-id="ff66d-115">On the **Failover** screen, select a **Recovery Point** to failover to.</span></span> <span data-ttu-id="ff66d-116">您可以使用下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="ff66d-116">You can use one of the following options:</span></span>
    1.  <span data-ttu-id="ff66d-117">**最新** (預設值)︰此選項會先處理已傳送到 Site Recovery 服務的所有資料，先為每個虛擬機器建立復原點後再進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-117">**Latest** (default): This option first processes all the data that has been sent to Site Recovery service to create a recovery point for each virtual machine before failing them over to it.</span></span> <span data-ttu-id="ff66d-118">此選項提供最低的 RPO (復原點目標)，因為在容錯移轉後建立的虛擬機器會具有觸發容錯移轉時已複寫到 Site Recovery 服務的所有資料。</span><span class="sxs-lookup"><span data-stu-id="ff66d-118">This option provides the lowest RPO (Recovery Point Objective) as the virtual machine created after failover has all the data that has been replicated to Site Recovery service when the failover was triggered.</span></span>
    1.  <span data-ttu-id="ff66d-119">**最新處理**︰這個選項會將復原方案的所有虛擬機器容錯移轉至 Site Recovery 服務已處理的最新復原點。</span><span class="sxs-lookup"><span data-stu-id="ff66d-119">**Latest processed**: This option fails over all virtual machines of the recovery plan to the latest recovery point that has already been processed by Site Recovery service.</span></span> <span data-ttu-id="ff66d-120">當您進行虛擬機器的測試容錯移轉時，也會顯示最新處理復原點的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ff66d-120">When you are doing test failover of a virtual machine, time stamp of the latest processed recovery point is also shown.</span></span> <span data-ttu-id="ff66d-121">如果您正在執行某個復原方案的容錯移轉，您可以移至個別的虛擬機器，並查看 [最新復原點] 圖格以取得此資訊。</span><span class="sxs-lookup"><span data-stu-id="ff66d-121">If you are doing failover of a recovery plan, you can go to individual virtual machine and look at **Latest Recovery Points** tile to get this information.</span></span> <span data-ttu-id="ff66d-122">因為沒有花時間處理未處理的資料，此選項提供低 RTO (復原時間目標) 容錯移轉選項。</span><span class="sxs-lookup"><span data-stu-id="ff66d-122">As no time is spent to process the unprocessed data, this option provides a low RTO (Recovery Time Objective) failover option.</span></span>
    1.  <span data-ttu-id="ff66d-123">**最新的應用程式一致**︰這個選項會將復原方案的所有虛擬機器容錯移轉至 Site Recovery 服務已處理的最新應用程式一致復原點。</span><span class="sxs-lookup"><span data-stu-id="ff66d-123">**Latest app-consistent**: This option fails over all virtual machines of the recovery plan to the latest application consistent recovery point that has already been processed by Site Recovery service.</span></span> <span data-ttu-id="ff66d-124">當您進行虛擬機器的測試容錯移轉時，也會顯示最新應用程式一致復原點的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ff66d-124">When you are doing test failover of a virtual machine, time stamp of the latest app-consistent recovery point is also shown.</span></span> <span data-ttu-id="ff66d-125">如果您正在執行某個復原方案的容錯移轉，您可以移至個別的虛擬機器，並查看 [最新復原點] 圖格以取得此資訊。</span><span class="sxs-lookup"><span data-stu-id="ff66d-125">If you are doing failover of a recovery plan, you can go to individual virtual machine and look at **Latest Recovery Points** tile to get this information.</span></span>
    1.  <span data-ttu-id="ff66d-126">**已處理最近的多部虛擬機器**：此選項僅適用於至少一部虛擬機器已啟動多部虛擬機器一致性的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="ff66d-126">**Latest multi-VM processed**: This option is only available for recovery plans that have at least one virtual machine with multi-VM consistency ON.</span></span> <span data-ttu-id="ff66d-127">屬於最近一般多部虛擬機器一致復原點的複寫群組容錯移轉一部份的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ff66d-127">Virtual machines that are part of a replication group failover to the latest common multi-VM consistent recovery point.</span></span> <span data-ttu-id="ff66d-128">對於最近處理的復原點進行的其他虛擬機器容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-128">Other virtual machines failover to their latest processed recovery point.</span></span>  
    1.  <span data-ttu-id="ff66d-129">**最近的多部虛擬機器應用程式一致**：此選項僅適用於至少一部虛擬機器已啟動多部虛擬機器一致性的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="ff66d-129">**Latest multi-VM app-consistent**: This option is only available for recovery plans that have at least one virtual machine with multi-VM consistency ON.</span></span> <span data-ttu-id="ff66d-130">屬於最近一般多部虛擬機器應用程式一致復原點的複寫群組容錯移轉一部份的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ff66d-130">Virtual machines that are part of a replication group failover to the latest common multi-VM application-consistent recovery point.</span></span> <span data-ttu-id="ff66d-131">對於最近的應用程式一致復原點進行的其他虛擬機器容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-131">Other virtual machines failover to their latest application-consistent recovery point.</span></span>
    1.  <span data-ttu-id="ff66d-132">**自訂**︰如果您要執行虛擬機器的測試容錯移轉，您可以使用此選項以容錯移轉至特定復原點。</span><span class="sxs-lookup"><span data-stu-id="ff66d-132">**Custom**: If you are doing test failover of a virtual machine, then you can use this option to failover to a particular recovery point.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff66d-133">只有在容錯移轉至 Azure 時，才有選項讓您選擇復原點。</span><span class="sxs-lookup"><span data-stu-id="ff66d-133">The option to choose a recovery point is only available when you are failing over to Azure.</span></span>
    >
    >


1. <span data-ttu-id="ff66d-134">如果復原方案中有部分虛擬機器在前次執行時已容錯移轉，而現在這些虛擬機器在來源和目標位置上都在使用中，您可以使用 [變更方向] 選項，決定容錯移轉進行的方向。</span><span class="sxs-lookup"><span data-stu-id="ff66d-134">If some of the virtual machines in the recovery plan were failed over in a previous run and now the virtual machines are active on both source and target location, you can use **Change direction** option to decide the direction in which the failover should happen.</span></span>
1. <span data-ttu-id="ff66d-135">如果您要容錯移轉至 Azure，且已針對雲端啟用資料加密 (只有在您已從 VMM 伺服器保護 Hyper-v 虛擬機器時才適用)，請在 [加密金鑰] 中，選取您在 VMM 伺服器上安裝期間啟用資料加密時所發出的憑證。</span><span class="sxs-lookup"><span data-stu-id="ff66d-135">If you're failing over to Azure and data encryption is enabled for the cloud (applies only when you have protected Hyper-v virtual machines from a VMM Server), in **Encryption Key** select the certificate that was issued when you enabled data encryption during setup on the VMM server.</span></span>
1. <span data-ttu-id="ff66d-136">如果想在觸發容錯移轉之前，讓 Site Recovery 嘗試將來源虛擬機器關機，請選取 [先將機器關機再開始容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="ff66d-136">Select **Shut down machine before beginning failover** if you want Site Recovery to attempt to do a shutdown of source virtual machines before triggering the failover.</span></span> <span data-ttu-id="ff66d-137">即使關機失敗，仍會繼續容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-137">Failover continues even if shutdown fails.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="ff66d-138">對於 Hyper-v 虛擬機器，此選項也會在觸發容錯移轉之前，嘗試同步處理尚未傳送至服務的內部部署資料。</span><span class="sxs-lookup"><span data-stu-id="ff66d-138">In case of Hyper-v virtual machines, this option also tries to synchronize the on-premises data that has not yet been sent to the service before triggering the failover.</span></span>
    >
    >

1. <span data-ttu-id="ff66d-139">您可以 [作業] 頁面上追蹤容錯移轉進度。</span><span class="sxs-lookup"><span data-stu-id="ff66d-139">You can follow the failover progress on the **Jobs** page.</span></span> <span data-ttu-id="ff66d-140">即使在非計劃性容錯移轉期間發生錯誤，復原方案還是會執行到完成為止。</span><span class="sxs-lookup"><span data-stu-id="ff66d-140">Even if errors occur during an unplanned failover, the recovery plan runs until it is complete.</span></span>
1. <span data-ttu-id="ff66d-141">容錯移轉之後，登入虛擬機器進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ff66d-141">After the failover, validate the virtual machine by logging in to it.</span></span> <span data-ttu-id="ff66d-142">如果您想要前往虛擬機器的另一個復原點，您可以使用 [變更復原點] 選項。</span><span class="sxs-lookup"><span data-stu-id="ff66d-142">If you want to go another recovery point for the virtual machine, then you can use **Change recovery point** option.</span></span>
1. <span data-ttu-id="ff66d-143">一旦您滿意容錯移轉的虛擬機器，您可以 [認可] 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-143">Once you are satisfied with the failed over virtual machine, you can **Commit** the failover.</span></span> <span data-ttu-id="ff66d-144">這會刪除服務可用的所有復原點，而且無法再使用 [變更復原點] 選項。</span><span class="sxs-lookup"><span data-stu-id="ff66d-144">This deletes all the recovery points available with the service and **Change recovery point** option will no longer be available.</span></span>

## <a name="planned-failover"></a><span data-ttu-id="ff66d-145">計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="ff66d-145">Planned failover</span></span>
<span data-ttu-id="ff66d-146">除了容錯移轉，使用 Site Recovery 保護的 Hyper-V 虛擬機器也支援**計劃性容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="ff66d-146">Apart from, Failover, Hyper-V virtual machines protected using Site Recovery also support **Planned failover**.</span></span> <span data-ttu-id="ff66d-147">這是完全不會遺失資料的容錯移轉選項。</span><span class="sxs-lookup"><span data-stu-id="ff66d-147">This is a zero data loss failover option.</span></span> <span data-ttu-id="ff66d-148">觸發計劃性容錯移轉時，首先，來源虛擬機器會關機，尚未同步處理的資料會同步處理，然後觸發容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-148">When a planned failover is triggered, first the source virtual machines are shut down, the data yet to be synchronized is synchronized and then a failover is triggered.</span></span>

> [!NOTE]
> <span data-ttu-id="ff66d-149">當您在兩個內部部署網站之間容錯移轉 Hyper-v 虛擬機器時，若要回到主要內部部署網站，您必須先將虛擬機器**反向複寫**回主要網站，然後再觸發容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ff66d-149">When you failover Hyper-v virtual machines from one on-premises site to another on-premises site, to come back to the primary on-premises site you have to first **reverse replicate** the virtual machine back to primary site and then trigger a failover.</span></span> <span data-ttu-id="ff66d-150">如果主要虛擬機器無法使用，則開始**反向複寫**之前，您必須從備份還原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ff66d-150">If the primary virtual machine is not available, then before starting to **reverse replicate** you have to restore the virtual machine from a backup.</span></span>   
>
>

## <a name="failover-job"></a><span data-ttu-id="ff66d-151">容錯移轉作業</span><span class="sxs-lookup"><span data-stu-id="ff66d-151">Failover job</span></span>

![容錯移轉](./media/site-recovery-failover/FailoverJob.png)

<span data-ttu-id="ff66d-153">觸發容錯移轉時會執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ff66d-153">When a  failover is triggered, it involves following steps:</span></span>

1. <span data-ttu-id="ff66d-154">先決條件檢查︰這個步驟可確保符合容錯移轉所需的所有條件</span><span class="sxs-lookup"><span data-stu-id="ff66d-154">Prerequisites check: This step ensures that all conditions required for failover are met</span></span>
1. <span data-ttu-id="ff66d-155">容錯移轉︰這個步驟會處理並備妥資料，以用來建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ff66d-155">Failover: This step processes the data and makes it ready so that an Azure virtual machine can be created out of it.</span></span> <span data-ttu-id="ff66d-156">如果您已選擇 [最新] 復原點，此步驟會從已傳送至服務的資料建立復原點。</span><span class="sxs-lookup"><span data-stu-id="ff66d-156">If you have chosen **Latest** recovery point, this step creates a recovery point from the data that has been sent to the service.</span></span>
1. <span data-ttu-id="ff66d-157">開始︰這個步驟會使用上一個步驟中所處理的資料建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ff66d-157">Start: This step creates an Azure virtual machine using the data processed in the previous step.</span></span>

> [!WARNING]
> <span data-ttu-id="ff66d-158">**不要取消進行中的容錯移轉**︰容錯移轉開始之前，虛擬機器的複寫會停止。</span><span class="sxs-lookup"><span data-stu-id="ff66d-158">**Don't Cancel an in progress failover**: Before failover is started, replication for the virtual machine is stopped.</span></span> <span data-ttu-id="ff66d-159">如果您**取消**進行中的作業，容錯移轉會停止，但虛擬機器不會開始複寫。</span><span class="sxs-lookup"><span data-stu-id="ff66d-159">If you **Cancel** an in progress job, failover stops but the virtual machine will not start to replicate.</span></span> <span data-ttu-id="ff66d-160">無法重新開始複寫。</span><span class="sxs-lookup"><span data-stu-id="ff66d-160">Replication cannot be started again.</span></span>
>
>

## <a name="time-taken-for-failover-to-azure"></a><span data-ttu-id="ff66d-161">容錯移轉至 Azure 所花費的時間</span><span class="sxs-lookup"><span data-stu-id="ff66d-161">Time taken for failover to Azure</span></span>

<span data-ttu-id="ff66d-162">在某些情況下，虛擬機器的容錯移轉會需要其他中繼步驟，通常會費時大約 8 到 10 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="ff66d-162">In certain cases, failover of virtual machines requires an extra intermediate step that usually takes around 8  to 10 minutes to complete.</span></span> <span data-ttu-id="ff66d-163">這些情況如下所示︰</span><span class="sxs-lookup"><span data-stu-id="ff66d-163">These cases are as following:</span></span>

* <span data-ttu-id="ff66d-164">VMware 虛擬機器使用的行動服務版本早於 9.8 版</span><span class="sxs-lookup"><span data-stu-id="ff66d-164">VMware virtual machines using mobility service of version older than 9.8</span></span>
* <span data-ttu-id="ff66d-165">實體伺服器</span><span class="sxs-lookup"><span data-stu-id="ff66d-165">Physical servers</span></span> 
* <span data-ttu-id="ff66d-166">VMware Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ff66d-166">VMware Linux virtual machines</span></span>
* <span data-ttu-id="ff66d-167">如同實體伺服器般受到保護的 Hyper-V 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ff66d-167">Hyper-V virtual machines protected as physical servers</span></span>
* <span data-ttu-id="ff66d-168">沒有以下驅動程式作為開機驅動程式的 VMware 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ff66d-168">VMware virtual machines where following drivers are not present as boot drivers</span></span> 
    * <span data-ttu-id="ff66d-169">storvsc</span><span class="sxs-lookup"><span data-stu-id="ff66d-169">storvsc</span></span> 
    * <span data-ttu-id="ff66d-170">vmbus</span><span class="sxs-lookup"><span data-stu-id="ff66d-170">vmbus</span></span> 
    * <span data-ttu-id="ff66d-171">storflt</span><span class="sxs-lookup"><span data-stu-id="ff66d-171">storflt</span></span> 
    * <span data-ttu-id="ff66d-172">intelide</span><span class="sxs-lookup"><span data-stu-id="ff66d-172">intelide</span></span> 
    * <span data-ttu-id="ff66d-173">atapi</span><span class="sxs-lookup"><span data-stu-id="ff66d-173">atapi</span></span>
* <span data-ttu-id="ff66d-174">沒有啟用 DHCP 服務的 VMware 虛擬機器，無論其是否正在使用 DHCP 或靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="ff66d-174">VMware virtual machines that don't have DHCP service enabled irrespective of whether they are using DHCP or static IP addresses</span></span>

<span data-ttu-id="ff66d-175">在其他所有情況下則不需要此中繼步驟，且容錯移轉所花費的時間非常少。</span><span class="sxs-lookup"><span data-stu-id="ff66d-175">In all the other cases this intermediate step is not required and the time taken for the failover is significantly lower.</span></span> 





## <a name="using-scripts-in-failover"></a><span data-ttu-id="ff66d-176">在容錯移轉中使用指令碼</span><span class="sxs-lookup"><span data-stu-id="ff66d-176">Using scripts in Failover</span></span>
<span data-ttu-id="ff66d-177">您可能想要在容錯移轉時自動執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="ff66d-177">You might want to automate certain actions while doing a failover.</span></span> <span data-ttu-id="ff66d-178">若要這樣做，您可以在[復原方案](site-recovery-create-recovery-plans.md)中使用指令碼或 [Azure 自動化 Runbook](site-recovery-runbook-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="ff66d-178">You can use scripts or [Azure automation runbooks](site-recovery-runbook-automation.md) in [recovery plans](site-recovery-create-recovery-plans.md) to do that.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="ff66d-179">其他考量</span><span class="sxs-lookup"><span data-stu-id="ff66d-179">Other considerations</span></span>
* <span data-ttu-id="ff66d-180">**磁碟機代號** - 若要在容錯移轉後保留虛擬機器上的磁碟機代號，您可以將虛擬機器的 [SAN 原則] 設定為 [OnlineAll]。</span><span class="sxs-lookup"><span data-stu-id="ff66d-180">**Drive letter** — To retain the drive letter on virtual machines after failover you can set the **SAN Policy** for the virtual machine to **OnlineAll**.</span></span> <span data-ttu-id="ff66d-181">[閱讀更多資訊](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure)。</span><span class="sxs-lookup"><span data-stu-id="ff66d-181">[Read more](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).</span></span>



## <a name="next-steps"></a><span data-ttu-id="ff66d-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff66d-182">Next steps</span></span>
<span data-ttu-id="ff66d-183">當您容錯移轉虛擬機器之後，而且內部部署資料中心可用時，您應該將 VMware 虛擬機器移回內部部署資料中心來[**重新保護**](site-recovery-how-to-reprotect.md)。</span><span class="sxs-lookup"><span data-stu-id="ff66d-183">Once you have failed over virtual machines and the on-premises data center is available, you should [**Re-protect**](site-recovery-how-to-reprotect.md) VMware virtual machines back to the on-premises data center.</span></span>

<span data-ttu-id="ff66d-184">使用[**計劃性容錯移轉**](site-recovery-failback-from-azure-to-hyper-v.md)選項，將 Hyper-v 虛擬機器從 Azure **容錯回復**回到內部部署。</span><span class="sxs-lookup"><span data-stu-id="ff66d-184">Use [**Planned failover**](site-recovery-failback-from-azure-to-hyper-v.md) option to **Failback** Hyper-v virtual machines back to on-premises from Azure.</span></span>

<span data-ttu-id="ff66d-185">如果您已將 Hyper-v 虛擬機器容錯回復至 VMM 伺服器所管理的另一個內部部署資料中心，而且主要資料中心可用，請使用 [反向複寫] 選項，開始複寫回到主要資料中心。</span><span class="sxs-lookup"><span data-stu-id="ff66d-185">If you have failed over a Hyper-v virtual machine to another on-premises data center managed by a VMM server and the primary data center is available, then use **Reverse replicate** option to start the replication back to the primary data center.</span></span>
