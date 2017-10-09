---
title: "適用於 Windows Vm 在 Azure 中的 aaaImpactful 維護 |Microsoft 文件"
description: "Windows 虛擬機器具影響力的維護。"
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 98afaea0fdca796177e075b33615b03f1e7a0fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a><span data-ttu-id="298c8-103">虛擬機器具影響力的維護</span><span class="sxs-lookup"><span data-stu-id="298c8-103">Impactful maintenance for virtual machines</span></span>

<span data-ttu-id="298c8-104">有少數的情況下因為 tooplanned 維護 toohello 基礎基礎結構重新啟動 Vm。</span><span class="sxs-lookup"><span data-stu-id="298c8-104">There are few cases where your VMs are rebooted due tooplanned maintenance toohello underlying infrastructure.</span></span> <span data-ttu-id="298c8-105">在裝載於 Azure Vm 的影響 toothe 可用性，hello 下列現在均可供您 toouse:</span><span class="sxs-lookup"><span data-stu-id="298c8-105">Being impactful toothe availability of your VMs hosted in Azure, hello following are now available for you toouse:</span></span>

-   <span data-ttu-id="298c8-106">通知會傳送 hello 影響前至少 30 天。</span><span class="sxs-lookup"><span data-stu-id="298c8-106">Notification sent at least 30 days before hello impact.</span></span>

-   <span data-ttu-id="298c8-107">每個每個 VM 的可見性 toohello 維護期間。</span><span class="sxs-lookup"><span data-stu-id="298c8-107">Visibility toohello maintenance windows per each VM.</span></span>

-   <span data-ttu-id="298c8-108">設定 hello 精確的時間進行維護，以影響您的 Vm 中的控制和彈性。</span><span class="sxs-lookup"><span data-stu-id="298c8-108">Flexibility and control in setting hello exact time for maintenance to impact your VMs.</span></span>

<span data-ttu-id="298c8-109">Microsoft Azure 中的維護會以反覆項目排程。</span><span class="sxs-lookup"><span data-stu-id="298c8-109">Maintenance in Microsoft Azure is scheduled in iterations.</span></span> <span data-ttu-id="298c8-110">初始反覆項目具有較小的範圍中順序 tooreduce hello 風險參與推出新的修正程式和功能。</span><span class="sxs-lookup"><span data-stu-id="298c8-110">Initial iterations have smaller scope in order tooreduce hello risk involved in rolling out new fixes and capabilities.</span></span> <span data-ttu-id="298c8-111">稍後反覆項目可能會跨越多個區域 (hello 絕不會從相同的區域組)。</span><span class="sxs-lookup"><span data-stu-id="298c8-111">Later iterations may span multiple regions (never from hello same region pair).</span></span> <span data-ttu-id="298c8-112">VM 包含在單一維護反覆項目。</span><span class="sxs-lookup"><span data-stu-id="298c8-112">A VM is included in a single maintenance iteration.</span></span> <span data-ttu-id="298c8-113">如果反覆項目已中止，剩餘的 VM 會包含在其他日後的反覆項目中。</span><span class="sxs-lookup"><span data-stu-id="298c8-113">If an iteration is aborted, remaining VMs are included in another, future, iteration.</span></span>

<span data-ttu-id="298c8-114">hello 計劃性的維護反覆項目有兩個階段： Pre-emptive 的維護期間和已排程維護視窗。</span><span class="sxs-lookup"><span data-stu-id="298c8-114">hello planned maintenance iteration has two phases: Pre-emptive Maintenance Window and a Scheduled-Maintenance Window.</span></span>

<span data-ttu-id="298c8-115">hello **Pre-emptive 維護視窗**hello 彈性 tooinitiate hello 維護您的 Vm 上為您提供。</span><span class="sxs-lookup"><span data-stu-id="298c8-115">hello **Pre-emptive Maintenance Window** provides you with hello flexibility tooinitiate hello maintenance on your VMs.</span></span> <span data-ttu-id="298c8-116">如此一來，您可以判斷您的 Vm 會受到影響，hello hello 更新和維護每個 VM 之間的 hello 時間序列。</span><span class="sxs-lookup"><span data-stu-id="298c8-116">By doing so, you can determine when your VMs are impacted, hello sequence of hello update, and hello time between each VM being maintained.</span></span> <span data-ttu-id="298c8-117">您可以查詢每個 VM toosee，是否已規劃的維護，並檢查您的最後一個發出的維護要求 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="298c8-117">You can query each VM toosee whether it is planned for maintenance and check hello result of your last initiated maintenance request.</span></span>

<span data-ttu-id="298c8-118">hello**排程的維護視窗**時，Azure 已排程進行 hello 維護您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="298c8-118">hello **Scheduled Maintenance Window** is when Azure has scheduled your VMs for hello maintenance.</span></span> <span data-ttu-id="298c8-119">這段期間，會遵循先佔式維護期間，您可以仍然 hello 維護視窗，請查詢，但不再是無法 tooorchestrate hello 維護。</span><span class="sxs-lookup"><span data-stu-id="298c8-119">During this time window, which follows the pre-emptive maintenance window, you can still query for hello maintenance window, but no longer be able tooorchestrate hello maintenance.</span></span>

## <a name="availability-considerations-during-planned-maintenance"></a><span data-ttu-id="298c8-120">規劃維護期間的可用性考量</span><span class="sxs-lookup"><span data-stu-id="298c8-120">Availability Considerations during Planned Maintenance</span></span> 

### <a name="paired-regions"></a><span data-ttu-id="298c8-121">配對的區域</span><span class="sxs-lookup"><span data-stu-id="298c8-121">Paired Regions</span></span>

<span data-ttu-id="298c8-122">每個 Azure 區域搭配另一個地區內 hello 一起進行地區組的相同地理位置。</span><span class="sxs-lookup"><span data-stu-id="298c8-122">Each Azure region is paired with another region within hello same geography, together making a regional pair.</span></span> <span data-ttu-id="298c8-123">當執行維護，Azure 只會更新 hello 虛擬機器執行個體在單一區域中的其配對。</span><span class="sxs-lookup"><span data-stu-id="298c8-123">When executing maintenance, Azure will only update hello Virtual Machine instances in a single region of its pair.</span></span> <span data-ttu-id="298c8-124">例如，在更新 hello 美國中北部的虛擬機器時，Azure 不會更新在美國中南部任何虛擬機器在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="298c8-124">For example, when updating hello Virtual Machines in North Central US, Azure will not update any Virtual Machines in South Central US at hello same time.</span></span> <span data-ttu-id="298c8-125">這兩次更新作業會分別排定在不同的時間，以啟用區域之間的容錯移轉或負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="298c8-125">This will be scheduled at a separate time, enabling failover or load balancing between regions.</span></span> <span data-ttu-id="298c8-126">不過，其他地區為北歐可以進行維護在 hello 相同時間為美國東部。</span><span class="sxs-lookup"><span data-stu-id="298c8-126">However, other regions such as North Europe can be under maintenance at hello same time as East US.</span></span>
<span data-ttu-id="298c8-127">深入了解 [Azure 區域配對](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)。</span><span class="sxs-lookup"><span data-stu-id="298c8-127">Read more about [Azure region pairs](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span></span>

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a><span data-ttu-id="298c8-128">單一執行個體 VM 與可用性設定組或 VM 擴展集</span><span class="sxs-lookup"><span data-stu-id="298c8-128">Single Instance VMs vs. Availability Set or VM scale set</span></span>

<span data-ttu-id="298c8-129">在部署在 Azure 中使用虛擬機器工作負載時，您可以建立 hello Vm 內的可用性設定組中訂單 tooprovide 高可用性 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="298c8-129">When deploying a workload using virtual machines in Azure, you can create hello VMs within an availability set in order tooprovide high availability tooyour application.</span></span> <span data-ttu-id="298c8-130">這項組態可以確保在中斷或維護事件期間，至少有一部虛擬機器可供使用。</span><span class="sxs-lookup"><span data-stu-id="298c8-130">This configuration ensures that during either an outage or maintenance events, at least one virtual machine is available.</span></span>

<span data-ttu-id="298c8-131">在可用性設定組，個別的 Vm 會散佈 too20 更新網域設定。</span><span class="sxs-lookup"><span data-stu-id="298c8-131">Within an availability set, individual VMs are spread across up too20 update domains.</span></span> <span data-ttu-id="298c8-132">在規劃維護期間，在任何指定時間只有單一更新網域受影響。</span><span class="sxs-lookup"><span data-stu-id="298c8-132">During planned maintenance, only a single update domain is impacted at any given time.</span></span> <span data-ttu-id="298c8-133">hello 順序受到影響的更新網域可能不會繼續循序計劃性維護期間。</span><span class="sxs-lookup"><span data-stu-id="298c8-133">hello order of update domains being impacted may not proceed sequentially during planned maintenance.</span></span> <span data-ttu-id="298c8-134">單一執行個體 Vm （不屬於可用性設定組），沒有任何方式 toopredict 或決定哪些，以及多少 Vm 會一起受到影響。</span><span class="sxs-lookup"><span data-stu-id="298c8-134">For single instance VMs (not part of availability set), there is no way toopredict or determine which and how many VMs are impacted together.</span></span>

<span data-ttu-id="298c8-135">虛擬機器擴展集都可讓您的 Azure 計算資源 toodeploy 和管理一組相同的 Vm 為單一資源。</span><span class="sxs-lookup"><span data-stu-id="298c8-135">Virtual machine scale sets are an Azure compute resource that enables you toodeploy and manage a set of identical VMs as a single resource.</span></span>
<span data-ttu-id="298c8-136">hello 規模集提供類似的保證 tooan 可用性設定組更新網域的形式。</span><span class="sxs-lookup"><span data-stu-id="298c8-136">hello scale set provides similar guarantees tooan availability set in the form of update domains.</span></span> 

<span data-ttu-id="298c8-137">如需有關如何設定您的虛擬機器的高可用性的詳細資訊，請參閱[*管理 Windows 虛擬機器的 hello 可用性*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="298c8-137">For more information about configuring your virtual machines for high availability, see [*Manage hello availability of your Windows virtual machines*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="scheduled-events"></a><span data-ttu-id="298c8-138">排程的事件</span><span class="sxs-lookup"><span data-stu-id="298c8-138">Scheduled Events</span></span>

<span data-ttu-id="298c8-139">Azure 的中繼資料服務可讓您 toodiscover 您在 Azure 中裝載的虛擬機器資訊。</span><span class="sxs-lookup"><span data-stu-id="298c8-139">Azure Metadata Service enables you toodiscover information about your Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="298c8-140">排程的事件，其中一個 hello 公開類別、 介面有關即將發生的事件 （例如，在重新開機），才能為其準備您的應用程式，以及限制中斷。</span><span class="sxs-lookup"><span data-stu-id="298c8-140">Scheduled Events, one of hello exposed categories, surfaces information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span>

<span data-ttu-id="298c8-141">如需排程的事件的詳細資訊，請參閱太[Azure 中繼資料服務-排程的事件](../virtual-machines-scheduled-events.md)。</span><span class="sxs-lookup"><span data-stu-id="298c8-141">For more information about scheduled events, refer too[Azure Metadata Service - Scheduled Events](../virtual-machines-scheduled-events.md).</span></span>

## <a name="maintenance-discovery-and-notifications"></a><span data-ttu-id="298c8-142">維護探索和通知</span><span class="sxs-lookup"><span data-stu-id="298c8-142">Maintenance Discovery and Notifications</span></span>

<span data-ttu-id="298c8-143">維護排程是在 hello 個別 Vm 層的可見 toocustomers。</span><span class="sxs-lookup"><span data-stu-id="298c8-143">Maintenance schedule is visible toocustomers at hello level of individual VMs.</span></span> <span data-ttu-id="298c8-144">您可以使用 Azure 入口網站、 API、 PowerShell 或 CLI tooquery 的先佔式與排程的維護期間。</span><span class="sxs-lookup"><span data-stu-id="298c8-144">You can use Azure portal, API, PowerShell, or CLI tooquery for the pre-emptive and scheduled maintenance windows.</span></span> <span data-ttu-id="298c8-145">此外，應該會收到通知 （電子郵件） hello 萬一其中一個 （或多個） 您的 Vm 會影響 hello 程序期間。</span><span class="sxs-lookup"><span data-stu-id="298c8-145">In addition, expect to receive a notification (email) in hello case where one (or more) of your VMs are impacted during hello process.</span></span>

<span data-ttu-id="298c8-146">先佔式維護和排程維護階段開始時會發出通知。</span><span class="sxs-lookup"><span data-stu-id="298c8-146">Both pre-emptive maintenance and scheduled maintenance phases begin with a notification.</span></span> <span data-ttu-id="298c8-147">預期 tooreceive 單一通知每個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="298c8-147">Expect tooreceive a single notification per Azure subscription.</span></span> <span data-ttu-id="298c8-148">hello 通知會傳送預設 toohello 訂用帳戶的系統管理員和共同管理員。</span><span class="sxs-lookup"><span data-stu-id="298c8-148">hello notification is sent toohello subscription’s admin and co-admin by default.</span></span> <span data-ttu-id="298c8-149">您也可以設定 hello 維護通知的對象。</span><span class="sxs-lookup"><span data-stu-id="298c8-149">You can also configure hello audience for the maintenance notification.</span></span>

### <a name="view-hello-maintenance-window-in-hello-portal"></a><span data-ttu-id="298c8-150">Hello 入口網站中檢視 hello 維護視窗</span><span class="sxs-lookup"><span data-stu-id="298c8-150">View hello Maintenance Window in hello portal</span></span> 

<span data-ttu-id="298c8-151">您可以使用 hello Azure 入口網站，並尋找排程維護的 Vm。</span><span class="sxs-lookup"><span data-stu-id="298c8-151">You can use hello Azure portal and look for VMs scheduled for maintenance.</span></span>

1.  <span data-ttu-id="298c8-152">登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="298c8-152">Sign in toohello Azure portal.</span></span>

2.  <span data-ttu-id="298c8-153">按一下，然後開啟 hello**虛擬機器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="298c8-153">Click and open hello **Virtual Machines** blade.</span></span>

3.  <span data-ttu-id="298c8-154">按一下 hello**資料行**從可用的資料行 toochoose 按鈕 tooopen hello 清單</span><span class="sxs-lookup"><span data-stu-id="298c8-154">Click hello **Columns** button tooopen hello list of available columns toochoose from</span></span>

4.  <span data-ttu-id="298c8-155">選取並加入 hello**維護視窗**資料行。</span><span class="sxs-lookup"><span data-stu-id="298c8-155">Select and add hello **Maintenance Window** columns.</span></span> <span data-ttu-id="298c8-156">已排程維護的 Vm 有顯示 hello 維護期間。</span><span class="sxs-lookup"><span data-stu-id="298c8-156">VMs that are scheduled for maintenance have hello maintenance windows surfaced.</span></span> <span data-ttu-id="298c8-157">一旦維護完成或中止，則維護期間將不再顯示。</span><span class="sxs-lookup"><span data-stu-id="298c8-157">Once maintenance is completed or aborted for a, the maintenance window is no longer be presented.</span></span>

### <a name="query-maintenance-details-using-hello-azure-api"></a><span data-ttu-id="298c8-158">查詢使用 hello Azure 應用程式開發介面的維護詳細資料</span><span class="sxs-lookup"><span data-stu-id="298c8-158">Query maintenance details using hello Azure API</span></span>

<span data-ttu-id="298c8-159">使用 hello[取得 VM 資訊 API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get)並尋找 hello 執行個體檢視 toodiscover hello 維護詳細資料的個別 VM 上。</span><span class="sxs-lookup"><span data-stu-id="298c8-159">Use hello [get VM information API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) and look for hello instance view toodiscover hello maintenance details on an individual VM.</span></span> <span data-ttu-id="298c8-160">hello 回應包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="298c8-160">hello response includes hello following elements:</span></span>

  - <span data-ttu-id="298c8-161">isCustomerInitiatedMaintenanceAllowed： 指出是否可以立即起始 hello VM 上的先佔式重新部署。</span><span class="sxs-lookup"><span data-stu-id="298c8-161">isCustomerInitiatedMaintenanceAllowed: Indicates whether you can now initiate pre-emptive redeploy on hello VM.</span></span>

  - <span data-ttu-id="298c8-162">preMaintenanceWindowStartTime: hello hello 先佔式維護期間的開始時間。</span><span class="sxs-lookup"><span data-stu-id="298c8-162">preMaintenanceWindowStartTime: hello start time of hello pre-emptive maintenance window.</span></span>

  - <span data-ttu-id="298c8-163">preMaintenanceWindowEndTime: hello hello 先佔式維護視窗結束時間。</span><span class="sxs-lookup"><span data-stu-id="298c8-163">preMaintenanceWindowEndTime: hello end time of hello pre-emptive maintenance window.</span></span> <span data-ttu-id="298c8-164">在此時間之後, 您將不再能夠 tooinitiate 維護此 VM 上。</span><span class="sxs-lookup"><span data-stu-id="298c8-164">After this time, you will no longer be able tooinitiate maintenance on this VM.</span></span>
    
  - <span data-ttu-id="298c8-165">maintenanceWindowStartTime: hello 的開始時間 hello 排程的維護期間時 VM 會受到影響。</span><span class="sxs-lookup"><span data-stu-id="298c8-165">maintenanceWindowStartTime: hello start time of hello scheduled maintenance window when your VM are impacted.</span></span>

  - <span data-ttu-id="298c8-166">maintenanceWindowEndTime: hello hello 排程的維護期間的結束時間。</span><span class="sxs-lookup"><span data-stu-id="298c8-166">maintenanceWindowEndTime: hello end time of hello scheduled maintenance window.</span></span>
  
  - <span data-ttu-id="298c8-167">lastOperationResultCode: hello 最後的維護重新部署作業的結果。</span><span class="sxs-lookup"><span data-stu-id="298c8-167">lastOperationResultCode: hello result of your last Maintenance-Redeploy operation.</span></span>
 
  - <span data-ttu-id="298c8-168">lastOperationMessage： 訊息的最後一個維護重新部署作業的描述 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="298c8-168">lastOperationMessage:  Message describing hello result of your last Maintenance-Redeploy operation.</span></span>

## <a name="pre-emptive-redeploy"></a><span data-ttu-id="298c8-169">先佔式重新部署</span><span class="sxs-lookup"><span data-stu-id="298c8-169">Pre-emptive Redeploy</span></span>

<span data-ttu-id="298c8-170">先佔式重新部署動作提供維護時套用的 tooyour Vm 在 Azure 中的 hello 彈性 toocontrol hello 時間。</span><span class="sxs-lookup"><span data-stu-id="298c8-170">Pre-emptive redeploy action provides hello flexibility toocontrol hello time when maintenance is applied tooyour VMs in Azure.</span></span> <span data-ttu-id="298c8-171">計劃性的維護的開頭的先佔式的維護期間，您可以決定為每個重新啟動您的 Vm toobe hello 確切時間。</span><span class="sxs-lookup"><span data-stu-id="298c8-171">Planned maintenance begins with a pre-emptive maintenance window where you can decide on hello exact time for each of your VMs toobe rebooted.</span></span> <span data-ttu-id="298c8-172">以下是這類功能很實用的使用案例：</span><span class="sxs-lookup"><span data-stu-id="298c8-172">The following are use cases where such a functionality is useful:</span></span>

-   <span data-ttu-id="298c8-173">維護需要 toobe 協調 hello 一般客戶使用。</span><span class="sxs-lookup"><span data-stu-id="298c8-173">Maintenance need toobe coordinated with hello end customer.</span></span>

-   <span data-ttu-id="298c8-174">Azure 所提供的 hello 排程的維護期間並不足夠。</span><span class="sxs-lookup"><span data-stu-id="298c8-174">hello scheduled maintenance window offered by Azure is not sufficient.</span></span>
    <span data-ttu-id="298c8-175">可能是 hello 視窗發生 toobe 在一週的 hello 忙碌時間或太長。</span><span class="sxs-lookup"><span data-stu-id="298c8-175">It could be that hello window happens toobe on hello busiest time of the week or it is too long.</span></span>

-   <span data-ttu-id="298c8-176">多個執行個體或多層式應用程式，您需要兩個 Vm 或特定順序 toofollow 之間有足夠的時間。</span><span class="sxs-lookup"><span data-stu-id="298c8-176">For multi-instance or multi-tier applications, you need sufficient time between two VMs or a certain sequence toofollow.</span></span>

<span data-ttu-id="298c8-177">當您呼叫的先佔式重新部署 VM 上時，它會移動 hello VM tooan 已經更新節點，然後開啟電源時它上，保留所有組態選項及相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="298c8-177">When you call for pre-emptive redeploy on a VM, it moves hello VM tooan already updated node and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="298c8-178">雖然這樣做，hello 暫存磁碟會遺失，而且會更新虛擬網路介面相關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="298c8-178">While doing so, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span>

<span data-ttu-id="298c8-179">系統會對每個 VM 啟用一次先佔式重新部署。</span><span class="sxs-lookup"><span data-stu-id="298c8-179">Pre-emptive redeploy is enabled once per VM.</span></span> <span data-ttu-id="298c8-180">如果 hello 程序期間發生錯誤時，hello 作業已中止，VM 不受影響的 hello 和它被排除 hello 計劃的維護反覆項目。</span><span class="sxs-lookup"><span data-stu-id="298c8-180">If there is an error during hello process, hello operation is aborted, hello VM is not impacted and it is excluded from hello planned maintenance iteration.</span></span> <span data-ttu-id="298c8-181">您會在與新的排程更新的時間內連絡並在您的 Vm 提供新商機 tooschedule 和順序 hello 的影響。</span><span class="sxs-lookup"><span data-stu-id="298c8-181">You will be contacted in a later time with a new schedule and offered a new opportunity tooschedule and sequence hello impact on your VMs.</span></span>