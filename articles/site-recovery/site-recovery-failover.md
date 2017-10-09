---
title: "在站台復原 aaaFailover |Microsoft 文件"
description: "Azure Site Recovery 會協調 hello 複寫、 容錯移轉和復原的虛擬機器和實體伺服器。 深入了解容錯移轉 tooAzure 或次要資料中心。"
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
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a><span data-ttu-id="67ed7-104">Site Recovery 中的容錯移轉</span><span class="sxs-lookup"><span data-stu-id="67ed7-104">Failover in Site Recovery</span></span>
<span data-ttu-id="67ed7-105">本文說明如何 toofailover 虛擬機器和實體伺服器受 Site Recovery 保護。</span><span class="sxs-lookup"><span data-stu-id="67ed7-105">This article describes how toofailover virtual machines and physical servers protected by Site Recovery.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67ed7-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="67ed7-106">Prerequisites</span></span>
1. <span data-ttu-id="67ed7-107">執行容錯移轉之前，請執行[測試容錯移轉](site-recovery-test-failover-to-azure.md)tooensure 的一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="67ed7-107">Before you do a failover, do a [test failover](site-recovery-test-failover-to-azure.md) tooensure that everything is working as expected.</span></span>
1. <span data-ttu-id="67ed7-108">[準備 hello 網路](site-recovery-network-design.md)在目標位置，然後再進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="67ed7-108">[Prepare hello network](site-recovery-network-design.md) at target location before you do a failover.</span></span>  


## <a name="run-a-failover"></a><span data-ttu-id="67ed7-109">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="67ed7-109">Run a failover</span></span>
<span data-ttu-id="67ed7-110">此程序描述如何容錯移轉的 toorun[復原計劃](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="67ed7-110">This procedure describes how toorun a failover for a [recovery plan](site-recovery-create-recovery-plans.md).</span></span> <span data-ttu-id="67ed7-111">或者您可以執行單一虛擬機器或實體伺服器 hello 容錯移轉從 hello**複寫項目**頁面</span><span class="sxs-lookup"><span data-stu-id="67ed7-111">Alternatively you can run hello failover for a single virtual machine or physical server from hello **Replicated items** page</span></span>


![容錯移轉](./media/site-recovery-failover/Failover.png)

1. <span data-ttu-id="67ed7-113">選取 [復原方案]  >  *recoveryplan_name*。</span><span class="sxs-lookup"><span data-stu-id="67ed7-113">Select **Recovery Plans** > *recoveryplan_name*.</span></span> <span data-ttu-id="67ed7-114">按一下 [容錯移轉]</span><span class="sxs-lookup"><span data-stu-id="67ed7-114">Click **Failover**</span></span>
2. <span data-ttu-id="67ed7-115">在 hello**容錯移轉**畫面上，選取**復原點**toofailover 至。</span><span class="sxs-lookup"><span data-stu-id="67ed7-115">On hello **Failover** screen, select a **Recovery Point** toofailover to.</span></span> <span data-ttu-id="67ed7-116">您可以使用其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="67ed7-116">You can use one of hello following options:</span></span>
    1.  <span data-ttu-id="67ed7-117">**最新**（預設值）： 此選項會先處理所有 hello 資料它們容錯移轉 tooit 之前已傳送的 tooSite 復原服務 toocreate 每部虛擬機器的復原點。</span><span class="sxs-lookup"><span data-stu-id="67ed7-117">**Latest** (default): This option first processes all hello data that has been sent tooSite Recovery service toocreate a recovery point for each virtual machine before failing them over tooit.</span></span> <span data-ttu-id="67ed7-118">此選項提供 hello 觸發 hello 容錯移轉時，最低的 RPO （復原點目標） hello 建立虛擬機器容錯移轉擁有 hello 的所有資料後，已為複寫 tooSite 復原服務。</span><span class="sxs-lookup"><span data-stu-id="67ed7-118">This option provides hello lowest RPO (Recovery Point Objective) as hello virtual machine created after failover has all hello data that has been replicated tooSite Recovery service when hello failover was triggered.</span></span>
    1.  <span data-ttu-id="67ed7-119">**最新版處理**: hello 復原計劃 toohello 最新復原點的站台復原服務已經處理的所有虛擬機器都容錯移轉這個選項。</span><span class="sxs-lookup"><span data-stu-id="67ed7-119">**Latest processed**: This option fails over all virtual machines of hello recovery plan toohello latest recovery point that has already been processed by Site Recovery service.</span></span> <span data-ttu-id="67ed7-120">當您在進行測試容錯移轉的虛擬機器時，也會顯示 hello 最新的已處理的復原點的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="67ed7-120">When you are doing test failover of a virtual machine, time stamp of hello latest processed recovery point is also shown.</span></span> <span data-ttu-id="67ed7-121">如果您要復原計劃的容錯移轉，您可以移 tooindividual 虛擬機器，並查看**最新復原點**磚 tooget 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="67ed7-121">If you are doing failover of a recovery plan, you can go tooindividual virtual machine and look at **Latest Recovery Points** tile tooget this information.</span></span> <span data-ttu-id="67ed7-122">當沒有時間 tooprocess hello 未處理的資料時，此選項提供低 RTO （復原時間目標） 容錯移轉選項。</span><span class="sxs-lookup"><span data-stu-id="67ed7-122">As no time is spent tooprocess hello unprocessed data, this option provides a low RTO (Recovery Time Objective) failover option.</span></span>
    1.  <span data-ttu-id="67ed7-123">**最新的應用程式一致**: hello 復原計劃 toohello 最新應用程式一致復原點的站台復原服務已經處理的所有虛擬機器都容錯移轉這個選項。</span><span class="sxs-lookup"><span data-stu-id="67ed7-123">**Latest app-consistent**: This option fails over all virtual machines of hello recovery plan toohello latest application consistent recovery point that has already been processed by Site Recovery service.</span></span> <span data-ttu-id="67ed7-124">當您在進行測試容錯移轉的虛擬機器時，也會顯示 hello 最新的應用程式一致復原點的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="67ed7-124">When you are doing test failover of a virtual machine, time stamp of hello latest app-consistent recovery point is also shown.</span></span> <span data-ttu-id="67ed7-125">如果您要復原計劃的容錯移轉，您可以移 tooindividual 虛擬機器，並查看**最新復原點**磚 tooget 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="67ed7-125">If you are doing failover of a recovery plan, you can go tooindividual virtual machine and look at **Latest Recovery Points** tile tooget this information.</span></span>
    1.  <span data-ttu-id="67ed7-126">**已處理最近的多部虛擬機器**：此選項僅適用於至少一部虛擬機器已啟動多部虛擬機器一致性的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="67ed7-126">**Latest multi-VM processed**: This option is only available for recovery plans that have at least one virtual machine with multi-VM consistency ON.</span></span> <span data-ttu-id="67ed7-127">虛擬機器屬於複寫群組容錯移轉 toohello 最新通用多重 VM 一致性復原點。</span><span class="sxs-lookup"><span data-stu-id="67ed7-127">Virtual machines that are part of a replication group failover toohello latest common multi-VM consistent recovery point.</span></span> <span data-ttu-id="67ed7-128">其他虛擬機器容錯移轉 tootheir 最近處理過的復原點。</span><span class="sxs-lookup"><span data-stu-id="67ed7-128">Other virtual machines failover tootheir latest processed recovery point.</span></span>  
    1.  <span data-ttu-id="67ed7-129">**最近的多部虛擬機器應用程式一致**：此選項僅適用於至少一部虛擬機器已啟動多部虛擬機器一致性的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="67ed7-129">**Latest multi-VM app-consistent**: This option is only available for recovery plans that have at least one virtual machine with multi-VM consistency ON.</span></span> <span data-ttu-id="67ed7-130">虛擬機器屬於複寫群組容錯移轉 toohello 最新通用多部 VM 應用程式一致復原點。</span><span class="sxs-lookup"><span data-stu-id="67ed7-130">Virtual machines that are part of a replication group failover toohello latest common multi-VM application-consistent recovery point.</span></span> <span data-ttu-id="67ed7-131">其他虛擬機器容錯移轉 tootheir 最新應用程式一致復原點。</span><span class="sxs-lookup"><span data-stu-id="67ed7-131">Other virtual machines failover tootheir latest application-consistent recovery point.</span></span>
    1.  <span data-ttu-id="67ed7-132">**自訂**： 如果您在進行測試容錯移轉的虛擬機器，則您可以使用此選項 toofailover tooa 特定的復原點。</span><span class="sxs-lookup"><span data-stu-id="67ed7-132">**Custom**: If you are doing test failover of a virtual machine, then you can use this option toofailover tooa particular recovery point.</span></span>

    > [!NOTE]
    > <span data-ttu-id="67ed7-133">當您容錯移轉 tooAzure hello 選項 toochoose 復原點才可用。</span><span class="sxs-lookup"><span data-stu-id="67ed7-133">hello option toochoose a recovery point is only available when you are failing over tooAzure.</span></span>
    >
    >


1. <span data-ttu-id="67ed7-134">如果某些 hello hello 復原計劃中的虛擬機器已在先前執行容錯移轉，而且現在 hello 虛擬機器正在作用中來源和目標位置上，您可以使用**變更方向**選項 toodecide hello 方向應該會 hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="67ed7-134">If some of hello virtual machines in hello recovery plan were failed over in a previous run and now hello virtual machines are active on both source and target location, you can use **Change direction** option toodecide hello direction in which hello failover should happen.</span></span>
1. <span data-ttu-id="67ed7-135">如果您要容錯移轉 tooAzure 與 hello （只有在您保護 hyper-v 虛擬機器從 VMM 伺服器時，才適用） 的雲端啟用資料加密，請在**加密金鑰**選取 hello 已發行憑證，當您啟用在 hello VMM 伺服器上的安裝期間的資料加密。</span><span class="sxs-lookup"><span data-stu-id="67ed7-135">If you're failing over tooAzure and data encryption is enabled for hello cloud (applies only when you have protected Hyper-v virtual machines from a VMM Server), in **Encryption Key** select hello certificate that was issued when you enabled data encryption during setup on hello VMM server.</span></span>
1. <span data-ttu-id="67ed7-136">選取**機器關機再開始容錯移轉**關機之前觸發的來源虛擬機器的 Site Recovery tooattempt toodo 只要 hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="67ed7-136">Select **Shut down machine before beginning failover** if you want Site Recovery tooattempt toodo a shutdown of source virtual machines before triggering hello failover.</span></span> <span data-ttu-id="67ed7-137">即使關機失敗，仍會繼續容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="67ed7-137">Failover continues even if shutdown fails.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="67ed7-138">如果 hyper-v 虛擬機器，此選項也會嘗試不尚未傳送 toohello 服務觸發 hello 容錯移轉之前的 toosynchronize hello 在內部部署資料。</span><span class="sxs-lookup"><span data-stu-id="67ed7-138">In case of Hyper-v virtual machines, this option also tries toosynchronize hello on-premises data that has not yet been sent toohello service before triggering hello failover.</span></span>
    >
    >

1. <span data-ttu-id="67ed7-139">您可以依照 hello hello 容錯移轉的進度**作業**頁面。</span><span class="sxs-lookup"><span data-stu-id="67ed7-139">You can follow hello failover progress on hello **Jobs** page.</span></span> <span data-ttu-id="67ed7-140">即使未規劃的容錯移轉期間發生錯誤，hello 復原方案執行，直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="67ed7-140">Even if errors occur during an unplanned failover, hello recovery plan runs until it is complete.</span></span>
1. <span data-ttu-id="67ed7-141">Hello 容錯移轉之後，請登入以 tooit 驗證 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="67ed7-141">After hello failover, validate hello virtual machine by logging in tooit.</span></span> <span data-ttu-id="67ed7-142">如果您想要 toogo 另一個復原點 hello 虛擬機器，然後您可以使用**變更復原點**選項。</span><span class="sxs-lookup"><span data-stu-id="67ed7-142">If you want toogo another recovery point for hello virtual machine, then you can use **Change recovery point** option.</span></span>
1. <span data-ttu-id="67ed7-143">一旦您滿意 hello 容錯移轉虛擬機器時，您可以**認可**hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="67ed7-143">Once you are satisfied with hello failed over virtual machine, you can **Commit** hello failover.</span></span> <span data-ttu-id="67ed7-144">這會刪除所有 hello 可用復原點與 hello 服務和**變更復原點**選項將無法再使用。</span><span class="sxs-lookup"><span data-stu-id="67ed7-144">This deletes all hello recovery points available with hello service and **Change recovery point** option will no longer be available.</span></span>

## <a name="planned-failover"></a><span data-ttu-id="67ed7-145">計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="67ed7-145">Planned failover</span></span>
<span data-ttu-id="67ed7-146">除了容錯移轉，使用 Site Recovery 保護的 Hyper-V 虛擬機器也支援**計劃性容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="67ed7-146">Apart from, Failover, Hyper-V virtual machines protected using Site Recovery also support **Planned failover**.</span></span> <span data-ttu-id="67ed7-147">這是完全不會遺失資料的容錯移轉選項。</span><span class="sxs-lookup"><span data-stu-id="67ed7-147">This is a zero data loss failover option.</span></span> <span data-ttu-id="67ed7-148">觸發已規劃的容錯移轉時，第一次 hello 虛擬機器已關閉，hello 資料尚未同步處理的 toobe 已同步處理，則會觸發容錯移轉的來源。</span><span class="sxs-lookup"><span data-stu-id="67ed7-148">When a planned failover is triggered, first hello source virtual machines are shut down, hello data yet toobe synchronized is synchronized and then a failover is triggered.</span></span>

> [!NOTE]
> <span data-ttu-id="67ed7-149">當您容錯移轉的 hyper-v 虛擬機器從一個內部部署站台 tooanother 在內部部署站台，toocome 後 toohello 內部主要站台有 toofirst**反向複寫**hello 虛擬機器回復 tooprimary 站台和然後觸發容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="67ed7-149">When you failover Hyper-v virtual machines from one on-premises site tooanother on-premises site, toocome back toohello primary on-premises site you have toofirst **reverse replicate** hello virtual machine back tooprimary site and then trigger a failover.</span></span> <span data-ttu-id="67ed7-150">如果主要虛擬機器 hello 就無法使用，然後之前啟動太**反向複寫**您有從備份 toorestore hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="67ed7-150">If hello primary virtual machine is not available, then before starting too**reverse replicate** you have toorestore hello virtual machine from a backup.</span></span>   
>
>

## <a name="failover-job"></a><span data-ttu-id="67ed7-151">容錯移轉作業</span><span class="sxs-lookup"><span data-stu-id="67ed7-151">Failover job</span></span>

![容錯移轉](./media/site-recovery-failover/FailoverJob.png)

<span data-ttu-id="67ed7-153">觸發容錯移轉時會執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="67ed7-153">When a  failover is triggered, it involves following steps:</span></span>

1. <span data-ttu-id="67ed7-154">先決條件檢查︰這個步驟可確保符合容錯移轉所需的所有條件</span><span class="sxs-lookup"><span data-stu-id="67ed7-154">Prerequisites check: This step ensures that all conditions required for failover are met</span></span>
1. <span data-ttu-id="67ed7-155">容錯移轉： 此步驟中處理 hello 資料，並讓它準備好，以便可以建立 Azure 虛擬機器，不使用。</span><span class="sxs-lookup"><span data-stu-id="67ed7-155">Failover: This step processes hello data and makes it ready so that an Azure virtual machine can be created out of it.</span></span> <span data-ttu-id="67ed7-156">如果您已選擇**最新**復原點，此步驟中建立的復原點從 toohello 服務已傳送的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="67ed7-156">If you have chosen **Latest** recovery point, this step creates a recovery point from hello data that has been sent toohello service.</span></span>
1. <span data-ttu-id="67ed7-157">開始： 此步驟中建立 Azure 虛擬機器使用 hello hello 上一個步驟中處理的資料。</span><span class="sxs-lookup"><span data-stu-id="67ed7-157">Start: This step creates an Azure virtual machine using hello data processed in hello previous step.</span></span>

> [!WARNING]
> <span data-ttu-id="67ed7-158">**不會取消正在進行中容錯移轉**： 在啟動容錯移轉之前，已停止的 hello 虛擬機器複寫。</span><span class="sxs-lookup"><span data-stu-id="67ed7-158">**Don't Cancel an in progress failover**: Before failover is started, replication for hello virtual machine is stopped.</span></span> <span data-ttu-id="67ed7-159">如果您**取消**進度作業中容錯移轉會停止，但 hello 虛擬機器將不會啟動 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="67ed7-159">If you **Cancel** an in progress job, failover stops but hello virtual machine will not start tooreplicate.</span></span> <span data-ttu-id="67ed7-160">無法重新開始複寫。</span><span class="sxs-lookup"><span data-stu-id="67ed7-160">Replication cannot be started again.</span></span>
>
>

## <a name="time-taken-for-failover-tooazure"></a><span data-ttu-id="67ed7-161">容錯移轉 tooAzure 的時間</span><span class="sxs-lookup"><span data-stu-id="67ed7-161">Time taken for failover tooAzure</span></span>

<span data-ttu-id="67ed7-162">在某些情況下，虛擬機器的容錯移轉需要其他中繼步驟的程序通常需要約 8 too10 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="67ed7-162">In certain cases, failover of virtual machines requires an extra intermediate step that usually takes around 8  too10 minutes toocomplete.</span></span> <span data-ttu-id="67ed7-163">這些情況如下所示︰</span><span class="sxs-lookup"><span data-stu-id="67ed7-163">These cases are as following:</span></span>

* <span data-ttu-id="67ed7-164">VMware 虛擬機器使用的行動服務版本早於 9.8 版</span><span class="sxs-lookup"><span data-stu-id="67ed7-164">VMware virtual machines using mobility service of version older than 9.8</span></span>
* <span data-ttu-id="67ed7-165">實體伺服器</span><span class="sxs-lookup"><span data-stu-id="67ed7-165">Physical servers</span></span> 
* <span data-ttu-id="67ed7-166">VMware Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="67ed7-166">VMware Linux virtual machines</span></span>
* <span data-ttu-id="67ed7-167">如同實體伺服器般受到保護的 Hyper-V 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="67ed7-167">Hyper-V virtual machines protected as physical servers</span></span>
* <span data-ttu-id="67ed7-168">沒有以下驅動程式作為開機驅動程式的 VMware 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="67ed7-168">VMware virtual machines where following drivers are not present as boot drivers</span></span> 
    * <span data-ttu-id="67ed7-169">storvsc</span><span class="sxs-lookup"><span data-stu-id="67ed7-169">storvsc</span></span> 
    * <span data-ttu-id="67ed7-170">vmbus</span><span class="sxs-lookup"><span data-stu-id="67ed7-170">vmbus</span></span> 
    * <span data-ttu-id="67ed7-171">storflt</span><span class="sxs-lookup"><span data-stu-id="67ed7-171">storflt</span></span> 
    * <span data-ttu-id="67ed7-172">intelide</span><span class="sxs-lookup"><span data-stu-id="67ed7-172">intelide</span></span> 
    * <span data-ttu-id="67ed7-173">atapi</span><span class="sxs-lookup"><span data-stu-id="67ed7-173">atapi</span></span>
* <span data-ttu-id="67ed7-174">沒有啟用 DHCP 服務的 VMware 虛擬機器，無論其是否正在使用 DHCP 或靜態 IP 位址</span><span class="sxs-lookup"><span data-stu-id="67ed7-174">VMware virtual machines that don't have DHCP service enabled irrespective of whether they are using DHCP or static IP addresses</span></span>

<span data-ttu-id="67ed7-175">在所有 hello 其他情況下此中繼步驟並不需要與 hello hello 容錯移轉所花費的時間會顯著降低。</span><span class="sxs-lookup"><span data-stu-id="67ed7-175">In all hello other cases this intermediate step is not required and hello time taken for hello failover is significantly lower.</span></span> 





## <a name="using-scripts-in-failover"></a><span data-ttu-id="67ed7-176">在容錯移轉中使用指令碼</span><span class="sxs-lookup"><span data-stu-id="67ed7-176">Using scripts in Failover</span></span>
<span data-ttu-id="67ed7-177">您可能想要 tooautomate 特定動作時執行的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="67ed7-177">You might want tooautomate certain actions while doing a failover.</span></span> <span data-ttu-id="67ed7-178">您可以使用指令碼或[Azure 自動化 runbook](site-recovery-runbook-automation.md)中[復原計劃](site-recovery-create-recovery-plans.md)toodo 的。</span><span class="sxs-lookup"><span data-stu-id="67ed7-178">You can use scripts or [Azure automation runbooks](site-recovery-runbook-automation.md) in [recovery plans](site-recovery-create-recovery-plans.md) toodo that.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="67ed7-179">其他考量</span><span class="sxs-lookup"><span data-stu-id="67ed7-179">Other considerations</span></span>
* <span data-ttu-id="67ed7-180">**磁碟機代號**— tooretain hello 磁碟機代號在容錯移轉後的虛擬機器上，您可以設定 hello **SAN 原則**hello 虛擬機器太**OnlineAll**。</span><span class="sxs-lookup"><span data-stu-id="67ed7-180">**Drive letter** — tooretain hello drive letter on virtual machines after failover you can set hello **SAN Policy** for hello virtual machine too**OnlineAll**.</span></span> <span data-ttu-id="67ed7-181">[閱讀更多資訊](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure)。</span><span class="sxs-lookup"><span data-stu-id="67ed7-181">[Read more](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).</span></span>



## <a name="next-steps"></a><span data-ttu-id="67ed7-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67ed7-182">Next steps</span></span>
<span data-ttu-id="67ed7-183">一旦您已容錯移轉虛擬機器，而 hello 在內部部署資料中心，您應該[**重新保護**](site-recovery-how-to-reprotect.md) VMware 虛擬機器備份 toohello 在內部部署資料中心。</span><span class="sxs-lookup"><span data-stu-id="67ed7-183">Once you have failed over virtual machines and hello on-premises data center is available, you should [**Re-protect**](site-recovery-how-to-reprotect.md) VMware virtual machines back toohello on-premises data center.</span></span>

<span data-ttu-id="67ed7-184">使用[**規劃的容錯移轉**](site-recovery-failback-from-azure-to-hyper-v.md)太選項**容錯回復**hyper-v 虛擬機器從 Azure 備份 tooon 內部部署。</span><span class="sxs-lookup"><span data-stu-id="67ed7-184">Use [**Planned failover**](site-recovery-failback-from-azure-to-hyper-v.md) option too**Failback** Hyper-v virtual machines back tooon-premises from Azure.</span></span>

<span data-ttu-id="67ed7-185">如果您無法透過 hyper-v 虛擬機器 tooanother 在內部部署資料中心受 VMM 伺服器與 hello 主要資料中心使用，然後使用**反轉複寫**選項 toostart hello 複寫後 toohello主要資料中心。</span><span class="sxs-lookup"><span data-stu-id="67ed7-185">If you have failed over a Hyper-v virtual machine tooanother on-premises data center managed by a VMM server and hello primary data center is available, then use **Reverse replicate** option toostart hello replication back toohello primary data center.</span></span>
