---
title: "在入口網站中自動調整雲端服務 | Microsoft Docs"
description: "了解如何使用入口網站在 Azure 中設定雲端服務 web 角色或背景工作角色的自動調整規則。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: e9683d4c5779450fd67fa42ab13095c7f201b4cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-portal"></a><span data-ttu-id="22b36-103">如何在入口網站中設定雲端服務的自動調整</span><span class="sxs-lookup"><span data-stu-id="22b36-103">How to configure auto scaling for a Cloud Service in the portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22b36-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="22b36-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="22b36-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="22b36-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="22b36-106">針對雲端服務背景工作角色設定條件，以觸發相應縮小或相應放大作業。</span><span class="sxs-lookup"><span data-stu-id="22b36-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="22b36-107">適用於角色的條件可以 CPU、磁碟或角色的網路負載為根據。</span><span class="sxs-lookup"><span data-stu-id="22b36-107">The conditions for the role can be based on the CPU, disk, or network load of the role.</span></span> <span data-ttu-id="22b36-108">您也可以根據訊息佇列或一些與您訂用帳戶相關聯的其他 Azure 資源的計量來設定條件。</span><span class="sxs-lookup"><span data-stu-id="22b36-108">You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="22b36-109">本文著重於雲端服務 web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="22b36-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="22b36-110">當您直接建立虛擬機器 (傳統) 時，它會裝載於雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="22b36-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="22b36-111">如果要調整標準虛擬機器，您可以將它與[可用性設定組](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)產生關聯，還可以手動開啟或關閉它們。</span><span class="sxs-lookup"><span data-stu-id="22b36-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="22b36-112">考量</span><span class="sxs-lookup"><span data-stu-id="22b36-112">Considerations</span></span>
<span data-ttu-id="22b36-113">在設定應用程式的調整之前，您應該先考量下列資訊：</span><span class="sxs-lookup"><span data-stu-id="22b36-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="22b36-114">調整受到核心使用量影響。</span><span class="sxs-lookup"><span data-stu-id="22b36-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="22b36-115">較大型的角色執行個體會使用較多核心。</span><span class="sxs-lookup"><span data-stu-id="22b36-115">Larger role instances use more cores.</span></span> <span data-ttu-id="22b36-116">您只能在訂用帳戶的核心限制內調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="22b36-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="22b36-117">例如，假設您的訂用帳戶有 20 個核心的限制。</span><span class="sxs-lookup"><span data-stu-id="22b36-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="22b36-118">如果您使用兩個中型大小的雲端服務來執行應用程式 (總計 4 個核心)，則您最多只能在訂用帳戶中相應增加所剩餘的 16 個核心的其他雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="22b36-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="22b36-119">如需關於大小的詳細資訊，請參閱[雲端服務的大小](cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="22b36-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="22b36-120">您可以依據佇列訊息臨界值來調整。</span><span class="sxs-lookup"><span data-stu-id="22b36-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="22b36-121">如需如何使用佇列的詳細資訊，請參閱 [如何使用佇列儲存體服務](../storage/queues/storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="22b36-121">For more information about how to use queues, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="22b36-122">您也可以調整與您訂用帳戶相關聯的其他資源。</span><span class="sxs-lookup"><span data-stu-id="22b36-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="22b36-123">若要對應用程式啟用高可用性，您應該確定應用程式是以兩個以上的角色執行個體來部署。</span><span class="sxs-lookup"><span data-stu-id="22b36-123">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="22b36-124">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="22b36-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="22b36-125">調整所在之處</span><span class="sxs-lookup"><span data-stu-id="22b36-125">Where scale is located</span></span>
<span data-ttu-id="22b36-126">當您選取雲端服務之後，應該會看見雲端服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="22b36-126">After you select your cloud service, you should have the cloud service blade visible.</span></span>

1. <span data-ttu-id="22b36-127">在 [雲端服務] 刀鋒視窗的 [角色和執行個體] 圖格上，選取雲端服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="22b36-127">On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.</span></span>   
   <span data-ttu-id="22b36-128">**重要**︰請務必按一下雲端服務角色，而不是角色底下的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="22b36-128">**IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="22b36-129">選取 [調整]  磚。</span><span class="sxs-lookup"><span data-stu-id="22b36-129">Select the **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="22b36-130">自動調整</span><span class="sxs-lookup"><span data-stu-id="22b36-130">Automatic scale</span></span>
<span data-ttu-id="22b36-131">您可以使用下列任一種模式來設定角色的調整規模設定：**手動**或**自動**。</span><span class="sxs-lookup"><span data-stu-id="22b36-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="22b36-132">「手動」是您預期的模式，您會設定執行個體的絕對計數。</span><span class="sxs-lookup"><span data-stu-id="22b36-132">Manual is as you would expect, you set the absolute count of instances.</span></span> <span data-ttu-id="22b36-133">但是，「自動」讓您能夠設定規則來控制您應該調整的方式和程度。</span><span class="sxs-lookup"><span data-stu-id="22b36-133">Automatic however allows you to set rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="22b36-134">將 [調整規模依據] 選項設定為 [排程及效能規則]。</span><span class="sxs-lookup"><span data-stu-id="22b36-134">Set the **Scale by** option to **schedule and performance rules**.</span></span>

![具有設定檔與規則的雲端服務調整規模設定](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="22b36-136">現有的設定檔。</span><span class="sxs-lookup"><span data-stu-id="22b36-136">An existing profile.</span></span>
2. <span data-ttu-id="22b36-137">新增父設定檔的規則。</span><span class="sxs-lookup"><span data-stu-id="22b36-137">Add a rule for the parent profile.</span></span>
3. <span data-ttu-id="22b36-138">新增另一個設定檔。</span><span class="sxs-lookup"><span data-stu-id="22b36-138">Add another profile.</span></span>

<span data-ttu-id="22b36-139">選取 [新增設定檔]。</span><span class="sxs-lookup"><span data-stu-id="22b36-139">Select **Add Profile**.</span></span> <span data-ttu-id="22b36-140">設定檔決定您要用於調整規模的模式︰**一律**、**週期性**、**固定日期**。</span><span class="sxs-lookup"><span data-stu-id="22b36-140">The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="22b36-141">當您設定設定檔與規則之後，請選取頂端的 [儲存]  圖示。</span><span class="sxs-lookup"><span data-stu-id="22b36-141">After you have configured the profile and rules, select the **Save** icon at the top.</span></span>

#### <a name="profile"></a><span data-ttu-id="22b36-142">設定檔</span><span class="sxs-lookup"><span data-stu-id="22b36-142">Profile</span></span>
<span data-ttu-id="22b36-143">設定檔會設定調整規模的最小和最大執行個體個數，而且也會在此調整範圍作用中時。</span><span class="sxs-lookup"><span data-stu-id="22b36-143">The profile sets minimum and maximum instances for the scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="22b36-144">**一律**</span><span class="sxs-lookup"><span data-stu-id="22b36-144">**Always**</span></span>

    <span data-ttu-id="22b36-145">一律讓此範圍的執行個體個數保持可用狀態。</span><span class="sxs-lookup"><span data-stu-id="22b36-145">Always keep this range of instances available.</span></span>  

    ![一律調整的雲端服務](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="22b36-147">**週期性**</span><span class="sxs-lookup"><span data-stu-id="22b36-147">**Recurrence**</span></span>

    <span data-ttu-id="22b36-148">選擇一組要調整的一週天數。</span><span class="sxs-lookup"><span data-stu-id="22b36-148">Choose a set of days of the week to scale.</span></span>

    ![具有週期性排程的雲端服務調整規模](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="22b36-150">**固定日期**</span><span class="sxs-lookup"><span data-stu-id="22b36-150">**Fixed Date**</span></span>

    <span data-ttu-id="22b36-151">要調整角色的固定日期範圍。</span><span class="sxs-lookup"><span data-stu-id="22b36-151">A fixed date range to scale the role.</span></span>

    ![具有固定日期的雲端服務調整規模](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="22b36-153">當您設定設定檔之後，請選取設定檔刀鋒視窗底部的 [確定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="22b36-153">After you have configured the profile, select the **OK** button at the bottom of the profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="22b36-154">規則</span><span class="sxs-lookup"><span data-stu-id="22b36-154">Rule</span></span>
<span data-ttu-id="22b36-155">規則會新增至設定檔，並顯示將觸發調整規模的條件。</span><span class="sxs-lookup"><span data-stu-id="22b36-155">Rules are added to a profile and represent a condition that triggers the scale.</span></span>

<span data-ttu-id="22b36-156">規則觸發程序是以雲端服務的計量 (CPU 使用量、磁碟活動或網路活動) 為依據，您可以在其中新增條件值。</span><span class="sxs-lookup"><span data-stu-id="22b36-156">The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value.</span></span> <span data-ttu-id="22b36-157">此外，您可以根據訊息佇列或一些與您訂用帳戶相關聯的其他 Azure 資源的計量來設定觸發程序。</span><span class="sxs-lookup"><span data-stu-id="22b36-157">Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="22b36-158">當您設定規則之後，請選取規則刀鋒視窗底部的 [確定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="22b36-158">After you have configured the rule, select the **OK** button at the bottom of the rule blade.</span></span>

## <a name="back-to-manual-scale"></a><span data-ttu-id="22b36-159">回到手動調整</span><span class="sxs-lookup"><span data-stu-id="22b36-159">Back to manual scale</span></span>
<span data-ttu-id="22b36-160">瀏覽至[調整規模設定](#where-scale-is-located)，並將 [調整規模依據] 選項設定為 [手動輸入的執行個體計數]。</span><span class="sxs-lookup"><span data-stu-id="22b36-160">Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.</span></span>

![具有設定檔與規則的雲端服務調整規模設定](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="22b36-162">這個設定會移除該角色的自動調整，然後您可以直接設定執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="22b36-162">This setting removes automated scaling from the role and then you can set the instance count directly.</span></span>

1. <span data-ttu-id="22b36-163">調整 (手動或自動) 選項。</span><span class="sxs-lookup"><span data-stu-id="22b36-163">The scale (manual or automated) option.</span></span>
2. <span data-ttu-id="22b36-164">角色執行個體滑桿，可用來設定要調整的執行個體。</span><span class="sxs-lookup"><span data-stu-id="22b36-164">A role instance slider to set the instances to scale to.</span></span>
3. <span data-ttu-id="22b36-165">要調整之角色的執行個體。</span><span class="sxs-lookup"><span data-stu-id="22b36-165">Instances of the role to scale to.</span></span>

<span data-ttu-id="22b36-166">當您設定調整規模設定之後，請選取頂端的 [儲存]  圖示。</span><span class="sxs-lookup"><span data-stu-id="22b36-166">After you have configured the scale settings, select the **Save** icon at the top.</span></span>
