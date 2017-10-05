---
title: "Azure 建議程式高可用性建議 | Microsoft Docs"
description: "使用 Azure 建議程式來改善 Azure 部署的高可用性。"
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 23c159471a6e5a7ad9cb545840e8afd3ac72ecba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-high-availability-recommendations"></a><span data-ttu-id="9b424-103">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="9b424-103">Advisor High Availability recommendations</span></span>

<span data-ttu-id="9b424-104">Azure Advisor 可協助您確保和改善業務關鍵應用程式的持續性。</span><span class="sxs-lookup"><span data-stu-id="9b424-104">Azure Advisor helps you ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="9b424-105">您可以從 [建議程式] 儀表板的 [高可用性] 索引標籤，利用建議程式取得高可用性建議。</span><span class="sxs-lookup"><span data-stu-id="9b424-105">You can get high availability recommendations by Advisor from the **High Availability** tab of the Advisor dashboard.</span></span>

![Advisor 儀表板上的 [高可用性] 按鈕](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a><span data-ttu-id="9b424-107">確保虛擬機器的容錯</span><span class="sxs-lookup"><span data-stu-id="9b424-107">Ensure virtual machine fault tolerance</span></span>

<span data-ttu-id="9b424-108">建議程式會識別不屬於可用性設定組的虛擬機器，並建議將它們移至某個可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="9b424-108">Advisor identifies virtual machines that are not part of an availability set and recommends moving them into an availability set.</span></span> <span data-ttu-id="9b424-109">若要為應用程式提供備援，建議您在可用性設定組中，將兩部以上的虛擬機器組成群組。</span><span class="sxs-lookup"><span data-stu-id="9b424-109">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="9b424-110">這項組態可以確保在規劃或未規劃的維護事件發生期間，至少有一部虛擬機器可以使用，且符合 Azure 虛擬機器 SLA。</span><span class="sxs-lookup"><span data-stu-id="9b424-110">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span></span> <span data-ttu-id="9b424-111">您可以選擇建立虛擬機器的可用性設定組，或將虛擬機器新增至現有的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="9b424-111">You can choose either to create an availability set for the virtual machine or to add the virtual machine to an existing availability set.</span></span>

> [!NOTE]
> <span data-ttu-id="9b424-112">如果您選擇建立可用性設定組，您必須至少再將一個虛擬機器新增至該可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="9b424-112">If you choose to create an availability set, you must add at least one more virtual machine into it.</span></span> <span data-ttu-id="9b424-113">我們建議讓兩部或多部虛擬機器組成一個可用性設定組，以確保至少有一部機器可用於中斷期間。</span><span class="sxs-lookup"><span data-stu-id="9b424-113">We recommend that you group two or more virtual machines in an availability set to ensure that at least one machine is available during an outage.</span></span>

![Advisor 建議︰為了獲得虛擬機器備援功能，請使用可用性設定組](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a><span data-ttu-id="9b424-115">確保可用性設定組的容錯</span><span class="sxs-lookup"><span data-stu-id="9b424-115">Ensure availability set fault tolerance</span></span> 

<span data-ttu-id="9b424-116">Advisor 會識別包含單一虛擬機器的可用性設定組，並建議將一部或多部虛擬機器新增至該可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="9b424-116">Advisor identifies availability sets that contain a single virtual machine and recommends adding one or more virtual machines to it.</span></span> <span data-ttu-id="9b424-117">若要為應用程式提供備援，建議您在可用性設定組中，將兩部以上的虛擬機器組成群組。</span><span class="sxs-lookup"><span data-stu-id="9b424-117">To provide redundancy to your application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="9b424-118">這項組態可以確保在規劃或未規劃的維護事件發生期間，至少有一部虛擬機器可以使用，且符合 Azure 虛擬機器 SLA。</span><span class="sxs-lookup"><span data-stu-id="9b424-118">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets the Azure virtual machine SLA.</span></span> <span data-ttu-id="9b424-119">您可以選擇建立虛擬機器或使用現有的虛擬機器，並將它新增至可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="9b424-119">You can choose either to create a virtual machine or to use an existing virtual machine, and to add it to the availability set.</span></span>  

![Advisor 建議︰在這個可用性設定組中新增一或多個 VM](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a><span data-ttu-id="9b424-121">確保應用程式閘道的容錯</span><span class="sxs-lookup"><span data-stu-id="9b424-121">Ensure application gateway fault tolerance</span></span>
<span data-ttu-id="9b424-122">為確保應用程式閘道所支援的關鍵任務應用程式擁有商務持續性，Advisor 會識別未設定容錯功能的應用程式閘道執行個體，並建議可行的修復動作。</span><span class="sxs-lookup"><span data-stu-id="9b424-122">To ensure the business continuity of mission-critical applications that are powered by application gateways, Advisor identifies application gateway instances that are not configured for fault tolerance, and it suggests remediation actions that you can take.</span></span> <span data-ttu-id="9b424-123">Advisor 可識別中型或大型的單一執行個體應用程式閘道，並建議再新增至少一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="9b424-123">Advisor identifies medium or large single-instance application gateways, and it recommends adding at least one more instance.</span></span> <span data-ttu-id="9b424-124">它也可識別單一或多重執行個體的小型應用程式閘道，並建議您移轉至中型或大型的 SKU。</span><span class="sxs-lookup"><span data-stu-id="9b424-124">It also identifies single- or multi-instance small application gateways and recommends migrating to medium or large SKUs.</span></span> <span data-ttu-id="9b424-125">Advisor 會建議這些動作，以確保應用程式閘道執行個體已設定為能夠符合這些資源目前的 SLA 需求。</span><span class="sxs-lookup"><span data-stu-id="9b424-125">Advisor recommends these actions to ensure that your application gateway instances are configured to satisfy the current SLA requirements for these resources.</span></span>

![Advisor 建議︰部署兩個以上的中型或大型應用程式閘道執行個體](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-the-performance-and-reliability-of-virtual-machine-disks"></a><span data-ttu-id="9b424-127">改善虛擬機器磁碟的效能和可靠性</span><span class="sxs-lookup"><span data-stu-id="9b424-127">Improve the performance and reliability of virtual machine disks</span></span>

<span data-ttu-id="9b424-128">Advisor 會識別使用標準磁碟的虛擬機器，並建議升級為進階磁碟。</span><span class="sxs-lookup"><span data-stu-id="9b424-128">Advisor identifies virtual machines with standard disks and recommends upgrading to premium disks.</span></span>
 
<span data-ttu-id="9b424-129">針對執行時需要大量 I/O 之工作負載的虛擬機器，「Azure 進階儲存體」可提供高效能、低延遲的磁碟支援。</span><span class="sxs-lookup"><span data-stu-id="9b424-129">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads.</span></span> <span data-ttu-id="9b424-130">使用進階儲存體帳戶的虛擬機器磁碟會將資料儲存在固態硬碟 (SSD) 上。</span><span class="sxs-lookup"><span data-stu-id="9b424-130">Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs).</span></span> <span data-ttu-id="9b424-131">為了讓應用程式發揮最佳效能，建議您將任何需要高 IOPS 的虛擬機器磁碟移轉到進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="9b424-131">For the best performance for your application, we recommend that you migrate any virtual machine disks requiring high IOPS to premium storage.</span></span> 

<span data-ttu-id="9b424-132">如果您的磁碟不需要高 IOPS，您可以讓磁碟留在標準儲存體中以節省成本。</span><span class="sxs-lookup"><span data-stu-id="9b424-132">If your disks do not require high IOPS, you can limit costs by maintaining them in standard storage.</span></span> <span data-ttu-id="9b424-133">標準儲存體會將虛擬機器磁碟資料儲存在硬碟機 (HDD) 而非 SSD 上。</span><span class="sxs-lookup"><span data-stu-id="9b424-133">Standard storage stores virtual machine disk data on hard disk drives (HDDs) instead of SSDs.</span></span> <span data-ttu-id="9b424-134">您可以選擇將虛擬機器磁碟移轉到進階磁碟。</span><span class="sxs-lookup"><span data-stu-id="9b424-134">You can choose to migrate your virtual machine disks to premium disks.</span></span> <span data-ttu-id="9b424-135">大部分的虛擬機器 SKU 都支援進階磁碟。</span><span class="sxs-lookup"><span data-stu-id="9b424-135">Premium disks are supported on most virtual machine SKUs.</span></span> <span data-ttu-id="9b424-136">不過在某些情況下，如果您想要使用進階磁碟，您可能還需要升級虛擬機器 SKU。</span><span class="sxs-lookup"><span data-stu-id="9b424-136">However, in some cases, if you want to use premium disks, you might need to upgrade your virtual machine SKUs as well.</span></span>

![Advisor 建議︰升級為進階磁碟以改善虛擬機器磁碟的可靠性](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a><span data-ttu-id="9b424-138">防止意外刪除虛擬機器的資料</span><span class="sxs-lookup"><span data-stu-id="9b424-138">Protect your virtual machine data from accidental deletion</span></span>
<span data-ttu-id="9b424-139">Advisor 會識別未啟用備份的虛擬機器，並建議啟用備份。</span><span class="sxs-lookup"><span data-stu-id="9b424-139">Advisor identifies virtual machines where backup is not enabled, and it recommends enabling backup.</span></span> <span data-ttu-id="9b424-140">設定虛擬機器備份可確保業務關鍵資料的可用性，並防止資料意外刪除或損毀。</span><span class="sxs-lookup"><span data-stu-id="9b424-140">Setting up virtual machine backup ensures the availability of your business-critical data and offers protection against accidental deletion or corruption.</span></span>

![Advisor 建議︰設定虛擬機器備份以保護關鍵任務資料](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a><span data-ttu-id="9b424-142">在 Advisor 中取得高可用性建議</span><span class="sxs-lookup"><span data-stu-id="9b424-142">Access high availability recommendations in Advisor</span></span>

1. <span data-ttu-id="9b424-143">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9b424-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9b424-144">在左側窗格中，按一下 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="9b424-144">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="9b424-145">在服務功能表窗格中，於 [監視和管理] 底下，按一下 [Azure Advisor]。</span><span class="sxs-lookup"><span data-stu-id="9b424-145">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="9b424-146">隨即會顯示 Advisor 儀表板。</span><span class="sxs-lookup"><span data-stu-id="9b424-146">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="9b424-147">在 [Advisor] 儀表板上，按一下 [高可用性] 索引標籤，然後選取您想要接收建議的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b424-147">On the Advisor dashboard, click the **High Availability** tab, and then select the subscription for which you want to receive recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="9b424-148">若要存取 Advisor 建議，您必須先向 Advisor「註冊您的訂用帳戶」。</span><span class="sxs-lookup"><span data-stu-id="9b424-148">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="9b424-149">當「訂用帳戶擁有者」啟動 Advisor 儀表板，然後按一下 [取得建議] 按鈕時，便會註冊訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b424-149">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="9b424-150">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="9b424-150">This is a *one-time operation*.</span></span> <span data-ttu-id="9b424-151">註冊訂用帳戶之後，您能以訂用帳戶、資源群組或特定資源的 [擁有者]、[參與者] 或 [讀取者] 身分存取 Advisor 建議。</span><span class="sxs-lookup"><span data-stu-id="9b424-151">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b424-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b424-152">Next steps</span></span>

<span data-ttu-id="9b424-153">如需 Advisor 建議的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9b424-153">For more information about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="9b424-154">Azure 建議程式簡介</span><span class="sxs-lookup"><span data-stu-id="9b424-154">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="9b424-155">開始使用建議程式</span><span class="sxs-lookup"><span data-stu-id="9b424-155">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="9b424-156">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="9b424-156">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="9b424-157">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="9b424-157">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="9b424-158">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="9b424-158">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

