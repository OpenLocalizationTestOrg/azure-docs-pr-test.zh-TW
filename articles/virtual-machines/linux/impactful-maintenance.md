---
title: "對於 Azure 中的 Linux VM 進行的維護造成 VM 重新啟動 | Microsoft Docs"
description: "Linux 虛擬機器的維護造成 VM 重新啟動"
services: virtual-machines-linux
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: eb4b92d8-be0f-44f6-a6c3-f8f7efab09fe
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 25beee157bb869067e562189f86312dab173e68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="vm-restarting-maintenance"></a><span data-ttu-id="d4109-103">維護造成 VM 重新啟動</span><span class="sxs-lookup"><span data-stu-id="d4109-103">VM restarting maintenance</span></span>

<span data-ttu-id="d4109-104">有時會因為基礎結構的規劃維護而重新您的 VM。</span><span class="sxs-lookup"><span data-stu-id="d4109-104">There are few cases where your VMs are rebooted due to planned maintenance to the underlying infrastructure.</span></span> <span data-ttu-id="d4109-105">對於會對 Azure 中託管的 VM 可用性造成影響，下列是現在可供您使用的功能：</span><span class="sxs-lookup"><span data-stu-id="d4109-105">Being impactful to the availability of your VMs hosted in Azure, the following are now available for you to use:</span></span>

-   <span data-ttu-id="d4109-106">系統至少會在受到影響的 30 天前傳送通知。</span><span class="sxs-lookup"><span data-stu-id="d4109-106">Notification sent at least 30 days before the impact.</span></span>

-   <span data-ttu-id="d4109-107">每個 VM 在每次維護期間的可見性。</span><span class="sxs-lookup"><span data-stu-id="d4109-107">Visibility to the maintenance windows per each VM.</span></span>

-   <span data-ttu-id="d4109-108">可彈性設定並控管會影響 VM 的確切維護時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-108">Flexibility and control in setting the exact time for maintenance to impact your VMs.</span></span>

<span data-ttu-id="d4109-109">Microsoft Azure 中的維護會以反覆項目排程。</span><span class="sxs-lookup"><span data-stu-id="d4109-109">Maintenance in Microsoft Azure is scheduled in iterations.</span></span> <span data-ttu-id="d4109-110">初始反覆項目具有較小的範圍，以降低推出全新修正程式和功能所牽涉到的風險。</span><span class="sxs-lookup"><span data-stu-id="d4109-110">Initial iterations have smaller scope in order to reduce the risk involved in rolling out new fixes and capabilities.</span></span> <span data-ttu-id="d4109-111">後期反覆項目可能會跨越多個區域 (絕不會從相同的區域配對進行)。</span><span class="sxs-lookup"><span data-stu-id="d4109-111">Later iterations may span multiple regions (never from the same region pair).</span></span> <span data-ttu-id="d4109-112">VM 包含在單一維護反覆項目。</span><span class="sxs-lookup"><span data-stu-id="d4109-112">A VM is included in a single maintenance iteration.</span></span> <span data-ttu-id="d4109-113">如果反覆項目已中止，剩餘的 VM 會包含在其他日後的反覆項目中。</span><span class="sxs-lookup"><span data-stu-id="d4109-113">If an iteration is aborted, remaining VMs are included in another, future, iteration.</span></span>

<span data-ttu-id="d4109-114">規劃的維護反覆項目有兩個階段：先佔式維護期間和排程維護期間。</span><span class="sxs-lookup"><span data-stu-id="d4109-114">The planned maintenance iteration has two phases: Pre-emptive Maintenance Window and a Scheduled-Maintenance Window.</span></span>

<span data-ttu-id="d4109-115">**先佔式維護期間**可讓您在 VM 上彈性起始維護。</span><span class="sxs-lookup"><span data-stu-id="d4109-115">The **Pre-emptive Maintenance Window** provides you with the flexibility to initiate the maintenance on your VMs.</span></span> <span data-ttu-id="d4109-116">如此一來，您可以判斷 VM 何時受到影響、更新的結果，以及每次維護 VM 相隔的時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-116">By doing so, you can determine when your VMs are impacted, the sequence of the update, and the time between each VM being maintained.</span></span> <span data-ttu-id="d4109-117">您可以查詢每個 VM 來查看是否已規劃進行維護，並檢查上次所起始維護要求的結果。</span><span class="sxs-lookup"><span data-stu-id="d4109-117">You can query each VM to see whether it is planned for maintenance and check the result of your last initiated maintenance request.</span></span>

<span data-ttu-id="d4109-118">**排程維護期間**是 Azure 排程您的 VM 進行維護的時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-118">The **Scheduled Maintenance Window** is when Azure has scheduled your VMs for the maintenance.</span></span> <span data-ttu-id="d4109-119">在先佔式維護期間之後的這段期間，您仍然可以查詢維護期間，但是無法再協調維護。</span><span class="sxs-lookup"><span data-stu-id="d4109-119">During this time window, which follows the pre-emptive maintenance window, you can still query for the maintenance window, but no longer be able to orchestrate the maintenance.</span></span>

## <a name="availability-considerations-during-planned-maintenance"></a><span data-ttu-id="d4109-120">規劃維護期間的可用性考量</span><span class="sxs-lookup"><span data-stu-id="d4109-120">Availability considerations during planned maintenance</span></span> 

### <a name="paired-regions"></a><span data-ttu-id="d4109-121">配對的區域</span><span class="sxs-lookup"><span data-stu-id="d4109-121">Paired regions</span></span>

<span data-ttu-id="d4109-122">每個 Azure 區域都會與相同地理位置內的另一個區域配對，以共同形成區域配對。</span><span class="sxs-lookup"><span data-stu-id="d4109-122">Each Azure region is paired with another region within the same geography, together making a regional pair.</span></span> <span data-ttu-id="d4109-123">Azure 在執行維護作業時，只會更新區域配對中單一區域的虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4109-123">When executing maintenance, Azure will only update the Virtual Machine instances in a single region of its pair.</span></span> <span data-ttu-id="d4109-124">舉例來說，Azure 在更新美國中北部的虛擬機器時，就不會同時更新任何在美國中南部的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d4109-124">For example, when updating the Virtual Machines in North Central US, Azure will not update any Virtual Machines in South Central US at the same time.</span></span> <span data-ttu-id="d4109-125">這兩次更新作業會分別排定在不同的時間，以啟用區域之間的容錯移轉或負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="d4109-125">This will be scheduled at a separate time, enabling failover or load balancing between regions.</span></span> <span data-ttu-id="d4109-126">不過，像是北歐等其他區域可以和美國東部一同進行維護。</span><span class="sxs-lookup"><span data-stu-id="d4109-126">However, other regions such as North Europe can be under maintenance at the same time as East US.</span></span>
<span data-ttu-id="d4109-127">深入了解 [Azure 區域配對](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)。</span><span class="sxs-lookup"><span data-stu-id="d4109-127">Read more about [Azure region pairs](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span></span>

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a><span data-ttu-id="d4109-128">單一執行個體 VM 相較於可用性設定組或 VM 擴展集</span><span class="sxs-lookup"><span data-stu-id="d4109-128">Single instance VMs vs. availability set or VM scale set</span></span>

<span data-ttu-id="d4109-129">在 Azure 中使用虛擬機器部署工作負載時，您可以在可用性設定組中建立 VM，以便為應用程式提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="d4109-129">When deploying a workload using virtual machines in Azure, you can create the VMs within an availability set in order to provide high availability to your application.</span></span> <span data-ttu-id="d4109-130">這項組態可以確保在中斷或維護事件期間，至少有一部虛擬機器可供使用。</span><span class="sxs-lookup"><span data-stu-id="d4109-130">This configuration ensures that during either an outage or maintenance events, at least one virtual machine is available.</span></span>

<span data-ttu-id="d4109-131">在可用性設定組內，個別 VM 會散佈在多達 20 個更新網域。</span><span class="sxs-lookup"><span data-stu-id="d4109-131">Within an availability set, individual VMs are spread across up to 20 update domains.</span></span> <span data-ttu-id="d4109-132">在規劃維護期間，在任何指定時間只有單一更新網域受影響。</span><span class="sxs-lookup"><span data-stu-id="d4109-132">During planned maintenance, only a single update domain is impacted at any given time.</span></span> <span data-ttu-id="d4109-133">在規劃維護期間，受影響更新網域的順序可能不會循序進行。</span><span class="sxs-lookup"><span data-stu-id="d4109-133">The order of update domains being impacted may not proceed sequentially during planned maintenance.</span></span> <span data-ttu-id="d4109-134">對於單一執行個體 VM (不屬於可用性設定組)，無法預測或判定哪個和有多少 VM 會受到影響。</span><span class="sxs-lookup"><span data-stu-id="d4109-134">For single instance VMs (not part of availability set), there is no way to predict or determine which and how many VMs are impacted together.</span></span>

<span data-ttu-id="d4109-135">虛擬機器擴展集是一個可讓您以單一資源的形式，部署和管理一組相同 VM 的 Azure 計算資源。</span><span class="sxs-lookup"><span data-stu-id="d4109-135">Virtual machine scale sets are an Azure compute resource that enables you to deploy and manage a set of identical VMs as a single resource.</span></span>
<span data-ttu-id="d4109-136">擴展集提供與更新網域形式的可用性設定組類似的保證。</span><span class="sxs-lookup"><span data-stu-id="d4109-136">The scale set provides similar guarantees to an availability set in the form of update domains.</span></span> 

<span data-ttu-id="d4109-137">如需設定虛擬機器以取得高可用性的詳細資訊，請參閱[*管理 Windows 虛擬機器的可用性*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d4109-137">For more information about configuring your virtual machines for high availability, see [*Manage the availability of your Windows virtual machines*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="scheduled-events"></a><span data-ttu-id="d4109-138">排定的事件</span><span class="sxs-lookup"><span data-stu-id="d4109-138">Scheduled events</span></span>

<span data-ttu-id="d4109-139">Azure 中繼資料服務可讓您探索 Azure 中裝載的虛擬機器相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d4109-139">Azure Metadata Service enables you to discover information about your Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="d4109-140">排定的事件 (其中一個公開的類別) 會呈現即將發生的事件 (例如，重新開機) 相關資訊，您的應用程式才能做好準備以及限制中斷。</span><span class="sxs-lookup"><span data-stu-id="d4109-140">Scheduled Events, one of the exposed categories, surfaces information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span>

<span data-ttu-id="d4109-141">如需排定的事件有關的詳細資訊，請參閱 [Azure 中繼資料服務 - 排定的事件](../virtual-machines-scheduled-events.md)。</span><span class="sxs-lookup"><span data-stu-id="d4109-141">For more information about scheduled events, refer to [Azure Metadata Service - Scheduled Events](../virtual-machines-scheduled-events.md).</span></span>

## <a name="maintenance-discovery-and-notifications"></a><span data-ttu-id="d4109-142">維護探索和通知</span><span class="sxs-lookup"><span data-stu-id="d4109-142">Maintenance discovery and notifications</span></span>

<span data-ttu-id="d4109-143">個別 VM 層級的客戶可看見維護排程。</span><span class="sxs-lookup"><span data-stu-id="d4109-143">Maintenance schedule is visible to customers at the level of individual VMs.</span></span> <span data-ttu-id="d4109-144">您可以使用 Azure 入口網站、API、PowerShell 或 CLI 查詢先佔式和排程維護期間。</span><span class="sxs-lookup"><span data-stu-id="d4109-144">You can use Azure portal, API, PowerShell, or CLI to query for the pre-emptive and scheduled maintenance windows.</span></span> <span data-ttu-id="d4109-145">此外，一個 (或多個) VM 在程序期間受影響時，應該會收到通知 (電子郵件)。</span><span class="sxs-lookup"><span data-stu-id="d4109-145">In addition, expect to receive a notification (email) in the case where one (or more) of your VMs are impacted during the process.</span></span>

<span data-ttu-id="d4109-146">先佔式維護和排程維護階段開始時會發出通知。</span><span class="sxs-lookup"><span data-stu-id="d4109-146">Both pre-emptive maintenance and scheduled maintenance phases begin with a notification.</span></span> <span data-ttu-id="d4109-147">預期每個 Azure 訂用帳戶會收到單一通知。</span><span class="sxs-lookup"><span data-stu-id="d4109-147">Expect to receive a single notification per Azure subscription.</span></span> <span data-ttu-id="d4109-148">通知預設是傳送給訂用帳戶的管理員和共同管理員。</span><span class="sxs-lookup"><span data-stu-id="d4109-148">The notification is sent to the subscription’s admin and co-admin by default.</span></span> <span data-ttu-id="d4109-149">您也可以設定維護通知的對象。</span><span class="sxs-lookup"><span data-stu-id="d4109-149">You can also configure the audience for the maintenance notification.</span></span>

### <a name="view-the-maintenance-window-in-the-portal"></a><span data-ttu-id="d4109-150">在入口網站中檢視維護期間</span><span class="sxs-lookup"><span data-stu-id="d4109-150">View the maintenance window in the portal</span></span> 

<span data-ttu-id="d4109-151">您可以使用 Azure 入口網站尋找已排定進行維護的 VM。</span><span class="sxs-lookup"><span data-stu-id="d4109-151">You can use the Azure portal and look for VMs scheduled for maintenance.</span></span>

1.  <span data-ttu-id="d4109-152">登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d4109-152">Sign in to the Azure portal.</span></span>

2.  <span data-ttu-id="d4109-153">按一下並開啟 [虛擬機器] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d4109-153">Click and open the **Virtual Machines** blade.</span></span>

3.  <span data-ttu-id="d4109-154">按一下 [資料行] 按鈕開啟可用資料行的清單。</span><span class="sxs-lookup"><span data-stu-id="d4109-154">Click the **Columns** button to open the list of available columns to choose from</span></span>

4.  <span data-ttu-id="d4109-155">選取並新增 [維護期間]  資料行。</span><span class="sxs-lookup"><span data-stu-id="d4109-155">Select and add the **Maintenance Window** columns.</span></span> <span data-ttu-id="d4109-156">已排程維護的 VM 都會呈現維護期間。</span><span class="sxs-lookup"><span data-stu-id="d4109-156">VMs that are scheduled for maintenance have the maintenance windows surfaced.</span></span> <span data-ttu-id="d4109-157">一旦維護完成或中止，則維護期間將不再顯示。</span><span class="sxs-lookup"><span data-stu-id="d4109-157">Once maintenance is completed or aborted for a, the maintenance window is no longer be presented.</span></span>

### <a name="query-maintenance-details-using-the-azure-api"></a><span data-ttu-id="d4109-158">使用 Azure API 查詢維護詳細資料</span><span class="sxs-lookup"><span data-stu-id="d4109-158">Query maintenance details using the Azure API</span></span>

<span data-ttu-id="d4109-159">使用[取得 VM 資訊 API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get)，並尋找執行個體檢視來探索個別 VM 上的維護詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d4109-159">Use the [get VM information API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) and look for the instance view to discover the maintenance details on an individual VM.</span></span> <span data-ttu-id="d4109-160">回應包含下列元素：</span><span class="sxs-lookup"><span data-stu-id="d4109-160">The response includes the following elements:</span></span>

  - <span data-ttu-id="d4109-161">isCustomerInitiatedMaintenanceAllowed︰指出是否可以立即在 VM 上起始先佔式重新部署。</span><span class="sxs-lookup"><span data-stu-id="d4109-161">isCustomerInitiatedMaintenanceAllowed: Indicates whether you can now initiate pre-emptive redeploy on the VM.</span></span>

  - <span data-ttu-id="d4109-162">preMaintenanceWindowStartTime：先佔式維護期間的開始時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-162">preMaintenanceWindowStartTime: The start time of the pre-emptive maintenance window.</span></span>

  - <span data-ttu-id="d4109-163">preMaintenanceWindowEndTime：先佔式維護期間的結束時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-163">preMaintenanceWindowEndTime: The end time of the pre-emptive maintenance window.</span></span> <span data-ttu-id="d4109-164">此後，您再也無法在此 VM 上起始維護。</span><span class="sxs-lookup"><span data-stu-id="d4109-164">After this time, you will no longer be able to initiate maintenance on this VM.</span></span>
    
  - <span data-ttu-id="d4109-165">maintenanceWindowStartTime：您的 VM 受影響時排程維護期間的開始時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-165">maintenanceWindowStartTime: The start time of the scheduled maintenance window when your VM are impacted.</span></span>

  - <span data-ttu-id="d4109-166">maintenanceWindowEndTime：排程維護期間的結束時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-166">maintenanceWindowEndTime: The end time of the scheduled maintenance window.</span></span>
  
  - <span data-ttu-id="d4109-167">lastOperationResultCode：上次維護重新部署作業的結果。</span><span class="sxs-lookup"><span data-stu-id="d4109-167">lastOperationResultCode: The result of your last Maintenance-Redeploy operation.</span></span>
 
  - <span data-ttu-id="d4109-168">lastOperationMessage︰描述您上次維護重新部署作業結果的訊息。</span><span class="sxs-lookup"><span data-stu-id="d4109-168">lastOperationMessage:  Message describing the result of your last Maintenance-Redeploy operation.</span></span>


## <a name="pre-emptive-redeploy"></a><span data-ttu-id="d4109-169">先佔式重新部署</span><span class="sxs-lookup"><span data-stu-id="d4109-169">Pre-emptive redeploy</span></span>

<span data-ttu-id="d4109-170">先佔式重新部署動作可彈性控制對 Azure 中的 VM 進行維護的時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-170">Pre-emptive redeploy action provides the flexibility to control the time when maintenance is applied to your VMs in Azure.</span></span> <span data-ttu-id="d4109-171">規劃的維護從先佔式維護期間開始，在此您可以決定每個 VM 重新開機的確切時間。</span><span class="sxs-lookup"><span data-stu-id="d4109-171">Planned maintenance begins with a pre-emptive maintenance window where you can decide on the exact time for each of your VMs to be rebooted.</span></span> <span data-ttu-id="d4109-172">以下是這類功能很實用的使用案例：</span><span class="sxs-lookup"><span data-stu-id="d4109-172">The following are use cases where such a functionality is useful:</span></span>

-   <span data-ttu-id="d4109-173">需要與一般客戶協調維護。</span><span class="sxs-lookup"><span data-stu-id="d4109-173">Maintenance need to be coordinated with the end customer.</span></span>

-   <span data-ttu-id="d4109-174">Azure 提供的排定維護期間並不足夠。</span><span class="sxs-lookup"><span data-stu-id="d4109-174">The scheduled maintenance window offered by Azure is not sufficient.</span></span>
    <span data-ttu-id="d4109-175">該段期間可能剛好是一週最忙碌的時間或時間太長。</span><span class="sxs-lookup"><span data-stu-id="d4109-175">It could be that the window happens to be on the busiest time of the week or it is too long.</span></span>

-   <span data-ttu-id="d4109-176">對於多個執行個體或多層式應用程式，兩個 VM 需要有足夠的時間或遵循特定的順序。</span><span class="sxs-lookup"><span data-stu-id="d4109-176">For multi-instance or multi-tier applications, you need sufficient time between two VMs or a certain sequence to follow.</span></span>

<span data-ttu-id="d4109-177">當您呼叫 VM 上的先佔式重新部署時，它會將 VM 移至已更新的節點，並接著將它的電源重新開啟，保留所有組態選項和相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="d4109-177">When you call for pre-emptive redeploy on a VM, it moves the VM to an already updated node and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="d4109-178">這麼做的時候，暫存磁碟會遺失，而系統會更新與虛擬網路介面關聯的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4109-178">While doing so, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span>

<span data-ttu-id="d4109-179">系統會對每個 VM 啟用一次先佔式重新部署。</span><span class="sxs-lookup"><span data-stu-id="d4109-179">Pre-emptive redeploy is enabled once per VM.</span></span> <span data-ttu-id="d4109-180">如果在程序期間發生錯誤，作業就會中止，不會影響 VM 並將它排除在規劃的維護反覆項目之外。</span><span class="sxs-lookup"><span data-stu-id="d4109-180">If there is an error during the process, the operation is aborted, the VM is not impacted and it is excluded from the planned maintenance iteration.</span></span> <span data-ttu-id="d4109-181">稍後有新的排程時會連絡您，讓您有新的機會對您的 VM 排程及排序相關的影響。</span><span class="sxs-lookup"><span data-stu-id="d4109-181">You will be contacted in a later time with a new schedule and offered a new opportunity to schedule and sequence the impact on your VMs.</span></span>
