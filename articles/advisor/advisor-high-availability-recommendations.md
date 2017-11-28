---
title: "aaaAzure Advisor 高可用性建議 |Microsoft 文件"
description: "使用您的 Azure 部署的 Azure Advisor tooimprove 高可用性。"
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
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a><span data-ttu-id="facf9-103">建議程式高可用性建議</span><span class="sxs-lookup"><span data-stu-id="facf9-103">Advisor High Availability recommendations</span></span>

<span data-ttu-id="facf9-104">Azure Advisor 可協助您確保和改善的業務關鍵應用程式的 hello 持續性。</span><span class="sxs-lookup"><span data-stu-id="facf9-104">Azure Advisor helps you ensure and improve hello continuity of your business-critical applications.</span></span> <span data-ttu-id="facf9-105">您可以從 hello 取得高可用性建議 advisor**高可用性**hello Advisor 儀表板 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="facf9-105">You can get high availability recommendations by Advisor from hello **High Availability** tab of hello Advisor dashboard.</span></span>

![Hello Advisor 儀表板上高可用性 按鈕](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a><span data-ttu-id="facf9-107">確保虛擬機器的容錯</span><span class="sxs-lookup"><span data-stu-id="facf9-107">Ensure virtual machine fault tolerance</span></span>

<span data-ttu-id="facf9-108">建議程式會識別不屬於可用性設定組的虛擬機器，並建議將它們移至某個可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="facf9-108">Advisor identifies virtual machines that are not part of an availability set and recommends moving them into an availability set.</span></span> <span data-ttu-id="facf9-109">若要提供備援 tooyour 應用程式，我們建議您群組的可用性設定組中的兩個或多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="facf9-109">To provide redundancy tooyour application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="facf9-110">此組態可確保任一個計劃或非計劃性維護事件期間，至少一部虛擬機器可變更，同時符合 hello Azure 虛擬機器 SLA。</span><span class="sxs-lookup"><span data-stu-id="facf9-110">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets hello Azure virtual machine SLA.</span></span> <span data-ttu-id="facf9-111">您可以選擇任一 toocreate 可用性設定組的 hello 虛擬機器或 tooadd hello 虛擬機器 tooan 現有可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="facf9-111">You can choose either toocreate an availability set for hello virtual machine or tooadd hello virtual machine tooan existing availability set.</span></span>

> [!NOTE]
> <span data-ttu-id="facf9-112">如果您選擇 toocreate 可用性設定，您必須將一個以上的多個虛擬機器加入它。</span><span class="sxs-lookup"><span data-stu-id="facf9-112">If you choose toocreate an availability set, you must add at least one more virtual machine into it.</span></span> <span data-ttu-id="facf9-113">我們建議您分兩個或更多虛擬機器的可用性集 tooensure 發生中斷時可使用至少一部電腦。</span><span class="sxs-lookup"><span data-stu-id="facf9-113">We recommend that you group two or more virtual machines in an availability set tooensure that at least one machine is available during an outage.</span></span>

![Advisor 建議︰為了獲得虛擬機器備援功能，請使用可用性設定組](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a><span data-ttu-id="facf9-115">確保可用性設定組的容錯</span><span class="sxs-lookup"><span data-stu-id="facf9-115">Ensure availability set fault tolerance</span></span> 

<span data-ttu-id="facf9-116">Advisor 可識別包含單一虛擬機器的可用性設定組，並建議將一或多個虛擬機器 tooit。</span><span class="sxs-lookup"><span data-stu-id="facf9-116">Advisor identifies availability sets that contain a single virtual machine and recommends adding one or more virtual machines tooit.</span></span> <span data-ttu-id="facf9-117">若要提供備援 tooyour 應用程式，我們建議您群組的可用性設定組中的兩個或多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="facf9-117">To provide redundancy tooyour application, we recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="facf9-118">此組態可確保任一個計劃或非計劃性維護事件期間，至少一部虛擬機器可變更，同時符合 hello Azure 虛擬機器 SLA。</span><span class="sxs-lookup"><span data-stu-id="facf9-118">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine is available and meets hello Azure virtual machine SLA.</span></span> <span data-ttu-id="facf9-119">您可以在虛擬機器或 toouse 現有的虛擬機器和 tooadd 選擇任一 toocreate 它 toohello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="facf9-119">You can choose either toocreate a virtual machine or toouse an existing virtual machine, and tooadd it toohello availability set.</span></span>  

![Advisor 建議： 加入一或多個 Vm toothis 可用性設定組](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a><span data-ttu-id="facf9-121">確保應用程式閘道的容錯</span><span class="sxs-lookup"><span data-stu-id="facf9-121">Ensure application gateway fault tolerance</span></span>
<span data-ttu-id="facf9-122">tooensure hello 的關鍵任務應用程式由應用程式閘道所形成的業務續航力，Advisor 識別未設定為允許容錯功能的應用程式閘道器執行個體，並建議您可以採取的修復動作.</span><span class="sxs-lookup"><span data-stu-id="facf9-122">tooensure hello business continuity of mission-critical applications that are powered by application gateways, Advisor identifies application gateway instances that are not configured for fault tolerance, and it suggests remediation actions that you can take.</span></span> <span data-ttu-id="facf9-123">Advisor 可識別中型或大型的單一執行個體應用程式閘道，並建議再新增至少一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="facf9-123">Advisor identifies medium or large single-instance application gateways, and it recommends adding at least one more instance.</span></span> <span data-ttu-id="facf9-124">它也會識別單一或多重 instance 小型應用程式閘道，並建議移轉 toomedium 或大型的 Sku。</span><span class="sxs-lookup"><span data-stu-id="facf9-124">It also identifies single- or multi-instance small application gateways and recommends migrating toomedium or large SKUs.</span></span> <span data-ttu-id="facf9-125">Advisor 建議這些動作 tooensure 應用程式的閘道器執行個體所設定的 toosatisfy hello 目前 SLA 的需求，這些資源。</span><span class="sxs-lookup"><span data-stu-id="facf9-125">Advisor recommends these actions tooensure that your application gateway instances are configured toosatisfy hello current SLA requirements for these resources.</span></span>

![Advisor 建議︰部署兩個以上的中型或大型應用程式閘道執行個體](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a><span data-ttu-id="facf9-127">改善 hello 效能和可靠性的虛擬機器磁碟</span><span class="sxs-lookup"><span data-stu-id="facf9-127">Improve hello performance and reliability of virtual machine disks</span></span>

<span data-ttu-id="facf9-128">Advisor 可識別標準磁碟的虛擬機器，並建議升級 toopremium 磁碟。</span><span class="sxs-lookup"><span data-stu-id="facf9-128">Advisor identifies virtual machines with standard disks and recommends upgrading toopremium disks.</span></span>
 
<span data-ttu-id="facf9-129">針對執行時需要大量 I/O 之工作負載的虛擬機器，「Azure 進階儲存體」可提供高效能、低延遲的磁碟支援。</span><span class="sxs-lookup"><span data-stu-id="facf9-129">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines that run I/O-intensive workloads.</span></span> <span data-ttu-id="facf9-130">使用進階儲存體帳戶的虛擬機器磁碟會將資料儲存在固態硬碟 (SSD) 上。</span><span class="sxs-lookup"><span data-stu-id="facf9-130">Virtual machine disks that use premium storage accounts store data on solid-state drives (SSDs).</span></span> <span data-ttu-id="facf9-131">Hello 應用程式的最佳效能，我們建議您移轉需要高 IOPS toopremium 儲存任何虛擬機器磁碟。</span><span class="sxs-lookup"><span data-stu-id="facf9-131">For hello best performance for your application, we recommend that you migrate any virtual machine disks requiring high IOPS toopremium storage.</span></span> 

<span data-ttu-id="facf9-132">如果您的磁碟不需要高 IOPS，您可以讓磁碟留在標準儲存體中以節省成本。</span><span class="sxs-lookup"><span data-stu-id="facf9-132">If your disks do not require high IOPS, you can limit costs by maintaining them in standard storage.</span></span> <span data-ttu-id="facf9-133">標準儲存體會將虛擬機器磁碟資料儲存在硬碟機 (HDD) 而非 SSD 上。</span><span class="sxs-lookup"><span data-stu-id="facf9-133">Standard storage stores virtual machine disk data on hard disk drives (HDDs) instead of SSDs.</span></span> <span data-ttu-id="facf9-134">您可以選擇 toomigrate 虛擬機器磁碟 toopremium 磁碟。</span><span class="sxs-lookup"><span data-stu-id="facf9-134">You can choose toomigrate your virtual machine disks toopremium disks.</span></span> <span data-ttu-id="facf9-135">大部分的虛擬機器 SKU 都支援進階磁碟。</span><span class="sxs-lookup"><span data-stu-id="facf9-135">Premium disks are supported on most virtual machine SKUs.</span></span> <span data-ttu-id="facf9-136">不過，在某些情況下，如果您想 toouse 高階磁碟，您可能需要 tooupgrade 您的虛擬機器的 Sku 以及。</span><span class="sxs-lookup"><span data-stu-id="facf9-136">However, in some cases, if you want toouse premium disks, you might need tooupgrade your virtual machine SKUs as well.</span></span>

![Advisor 建議： 升級 toopremium 磁碟來改善您的虛擬機器磁碟 hello 可靠性](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a><span data-ttu-id="facf9-138">防止意外刪除虛擬機器的資料</span><span class="sxs-lookup"><span data-stu-id="facf9-138">Protect your virtual machine data from accidental deletion</span></span>
<span data-ttu-id="facf9-139">Advisor 會識別未啟用備份的虛擬機器，並建議啟用備份。</span><span class="sxs-lookup"><span data-stu-id="facf9-139">Advisor identifies virtual machines where backup is not enabled, and it recommends enabling backup.</span></span> <span data-ttu-id="facf9-140">設定虛擬機器備份可確保業務關鍵資料的 hello 可用性，以及提供防止被意外刪除或損毀。</span><span class="sxs-lookup"><span data-stu-id="facf9-140">Setting up virtual machine backup ensures hello availability of your business-critical data and offers protection against accidental deletion or corruption.</span></span>

![Advisor 建議： 設定虛擬機器備份 tooprotect 重要的資料](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a><span data-ttu-id="facf9-142">在 Advisor 中取得高可用性建議</span><span class="sxs-lookup"><span data-stu-id="facf9-142">Access high availability recommendations in Advisor</span></span>

1. <span data-ttu-id="facf9-143">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="facf9-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="facf9-144">在 hello 左窗格中，按一下 **更多服務**。</span><span class="sxs-lookup"><span data-stu-id="facf9-144">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="facf9-145">在 hello 服務功能表窗格底下**監視及管理**，按一下  **Azure Advisor**。</span><span class="sxs-lookup"><span data-stu-id="facf9-145">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="facf9-146">hello Advisor 儀表板會顯示。</span><span class="sxs-lookup"><span data-stu-id="facf9-146">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="facf9-147">在 hello Advisor 儀表板上按一下 hello**高可用性**索引標籤，然後再選取您想要的 tooreceive 建議的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="facf9-147">On hello Advisor dashboard, click hello **High Availability** tab, and then select hello subscription for which you want tooreceive recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="facf9-148">tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。</span><span class="sxs-lookup"><span data-stu-id="facf9-148">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="facf9-149">已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="facf9-149">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="facf9-150">此作業「只需要執行一次」。</span><span class="sxs-lookup"><span data-stu-id="facf9-150">This is a *one-time operation*.</span></span> <span data-ttu-id="facf9-151">Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。</span><span class="sxs-lookup"><span data-stu-id="facf9-151">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="facf9-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="facf9-152">Next steps</span></span>

<span data-ttu-id="facf9-153">如需 Advisor 建議的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="facf9-153">For more information about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="facf9-154">簡介 tooAzure Advisor</span><span class="sxs-lookup"><span data-stu-id="facf9-154">Introduction tooAzure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="facf9-155">開始使用建議程式</span><span class="sxs-lookup"><span data-stu-id="facf9-155">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="facf9-156">建議程式成本建議</span><span class="sxs-lookup"><span data-stu-id="facf9-156">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="facf9-157">建議程式效能建議</span><span class="sxs-lookup"><span data-stu-id="facf9-157">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="facf9-158">建議程式安全性建議</span><span class="sxs-lookup"><span data-stu-id="facf9-158">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

