---
title: "在傳統入口網站中自動調整雲端服務 | Microsoft Docs"
description: "(傳統) 了解如何使用傳統入口網站，在 Azure 中設定雲端服務 Web 角色或背景工作角色的自動調整規則。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="efd12-103">如何在傳統入口網站中設定雲端服務的自動調整</span><span class="sxs-lookup"><span data-stu-id="efd12-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="efd12-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="efd12-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="efd12-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="efd12-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="efd12-106">在 Azure 傳統入口網站的 [調整] 頁面上，您可以設定您 web 角色或背景工作角色的自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="efd12-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="efd12-107">或者，您可以設定手動調整，而非規則型自動縮放比例。</span><span class="sxs-lookup"><span data-stu-id="efd12-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="efd12-108">本文著重於雲端服務 web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="efd12-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="efd12-109">當您直接建立虛擬機器 (傳統) 時，它會裝載於雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="efd12-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="efd12-110">其中有些資訊適用於這些類型的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="efd12-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="efd12-111">調整虛擬機器的可用性設定組只是根據您設定的調整規則將其關閉或開啟。</span><span class="sxs-lookup"><span data-stu-id="efd12-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="efd12-112">如需虛擬機器和可用性設定組的詳細資訊，請參閱 [管理虛擬機器的可用性](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="efd12-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="efd12-113">在設定應用程式的調整之前，您應該先考量下列資訊：</span><span class="sxs-lookup"><span data-stu-id="efd12-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="efd12-114">調整受到核心使用量影響。</span><span class="sxs-lookup"><span data-stu-id="efd12-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="efd12-115">較大型的角色執行個體會使用較多核心。</span><span class="sxs-lookup"><span data-stu-id="efd12-115">Larger role instances use more cores.</span></span> <span data-ttu-id="efd12-116">您只能在訂用帳戶的核心限制內調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="efd12-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="efd12-117">例如，假設您的訂用帳戶有 20 個核心的限制。</span><span class="sxs-lookup"><span data-stu-id="efd12-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="efd12-118">如果您使用兩個中型大小的雲端服務來執行應用程式 (總計 4 個核心)，則您最多只能在訂用帳戶中相應增加所剩餘的 16 個核心的其他雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="efd12-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="efd12-119">如需關於大小的詳細資訊，請參閱[雲端服務的大小](cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="efd12-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="efd12-120">您必須先建立佇列並且將它與角色建立關聯，然後才能根據訊息臨界值調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="efd12-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="efd12-121">如需詳細資訊，請參閱 [如何使用佇列儲存體服務](../storage/queues/storage-dotnet-how-to-use-queues.md)(英文)。</span><span class="sxs-lookup"><span data-stu-id="efd12-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="efd12-122">您可以調整與您雲端服務連結的資源。</span><span class="sxs-lookup"><span data-stu-id="efd12-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="efd12-123">如需關於連結資源的詳細資訊，請參閱 [作法：將資源連結到雲端服務](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="efd12-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="efd12-124">若要對應用程式啟用高可用性，您應該確定應用程式是以兩個以上的角色執行個體來部署。</span><span class="sxs-lookup"><span data-stu-id="efd12-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="efd12-125">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="efd12-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="efd12-126">Schedule scaling</span><span class="sxs-lookup"><span data-stu-id="efd12-126">Schedule scaling</span></span>
<span data-ttu-id="efd12-127">根據預設，所有角色皆未遵循特定的排程。</span><span class="sxs-lookup"><span data-stu-id="efd12-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="efd12-128">因此，任何變更的設定皆可套用到所有時間和全年中的所有天數。</span><span class="sxs-lookup"><span data-stu-id="efd12-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="efd12-129">您可以根據意願將手動或自動調整設定為下列其中一個模式︰</span><span class="sxs-lookup"><span data-stu-id="efd12-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="efd12-130">工作日</span><span class="sxs-lookup"><span data-stu-id="efd12-130">Weekdays</span></span>
* <span data-ttu-id="efd12-131">週末</span><span class="sxs-lookup"><span data-stu-id="efd12-131">Weekends</span></span>
* <span data-ttu-id="efd12-132">週間夜</span><span class="sxs-lookup"><span data-stu-id="efd12-132">Week nights</span></span>
* <span data-ttu-id="efd12-133">週間早上</span><span class="sxs-lookup"><span data-stu-id="efd12-133">Week mornings</span></span>
* <span data-ttu-id="efd12-134">特定日期</span><span class="sxs-lookup"><span data-stu-id="efd12-134">Specific dates</span></span>
* <span data-ttu-id="efd12-135">特定日期範圍</span><span class="sxs-lookup"><span data-stu-id="efd12-135">Specific date ranges</span></span>

<span data-ttu-id="efd12-136">這個排程設定可以在 [雲端服務] [Azure 傳統入口網站](https://manage.windowsazure.com/) 頁面上的</span><span class="sxs-lookup"><span data-stu-id="efd12-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="efd12-137">[雲端服務] > \[您的雲端服務\] > [調整] > \[生產或預備\] 頁面。</span><span class="sxs-lookup"><span data-stu-id="efd12-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="efd12-138">對您想要變更的每個角色按一下 [設定排程時間]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="efd12-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![以排程為基礎的雲端服務自動調整][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="efd12-140">手動調整</span><span class="sxs-lookup"><span data-stu-id="efd12-140">Manual scale</span></span>
<span data-ttu-id="efd12-141">在 [調整]  頁面上，您可以手動增加或減少雲端服務中執行的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="efd12-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="efd12-142">這項設定會針對您已建立的每個排程進行，或者在您尚未建立排程時隨時進行。</span><span class="sxs-lookup"><span data-stu-id="efd12-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="efd12-143">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，按一下 [雲端服務]，然後按一下雲端服務的名稱以開啟儀表板。</span><span class="sxs-lookup"><span data-stu-id="efd12-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="efd12-144">如果您沒有看到您的雲端服務，您可能需要從 [生產] 變更為 [預備]，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="efd12-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="efd12-145">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="efd12-145">Click **Scale**.</span></span>
3. <span data-ttu-id="efd12-146">選取您想要變更其調整選項的排程。</span><span class="sxs-lookup"><span data-stu-id="efd12-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="efd12-147">如果您尚未定義排程，則預設為 [無排程時間]。</span><span class="sxs-lookup"><span data-stu-id="efd12-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="efd12-148">尋找 [依度量調整規模] 區段，然後選取 [無]。</span><span class="sxs-lookup"><span data-stu-id="efd12-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="efd12-149">這項設定是所有角色的預設。</span><span class="sxs-lookup"><span data-stu-id="efd12-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="efd12-150">雲端服務中的每個角色都有個滑桿可變更要使用的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="efd12-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![手動調整雲端服務角色][manual_scale]
   
    <span data-ttu-id="efd12-152">如果您需要更多執行個體，您可能需要變更 [雲端服務虛擬機器大小](cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="efd12-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="efd12-153">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="efd12-153">Click **Save**.</span></span>  
   <span data-ttu-id="efd12-154">系統隨即根據您做的選取來新增或移除角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="efd12-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="efd12-155">每當您看到 ![][tip_icon]，請將滑鼠移向它，您就可以取得特定設定執行作業的相關說明。</span><span class="sxs-lookup"><span data-stu-id="efd12-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="efd12-156">自動調整 - CPU</span><span class="sxs-lookup"><span data-stu-id="efd12-156">Automatic scale - CPU</span></span>
<span data-ttu-id="efd12-157">此模式可以調整平均 CPU 使用量百分比高於或低於指定的臨界值。</span><span class="sxs-lookup"><span data-stu-id="efd12-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="efd12-158">在這種情況會建立或刪除角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="efd12-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="efd12-159">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，按一下 [雲端服務]，然後按一下雲端服務的名稱以開啟儀表板。</span><span class="sxs-lookup"><span data-stu-id="efd12-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="efd12-160">如果您沒有看到您的雲端服務，您可能需要從 [生產] 變更為 [預備]，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="efd12-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="efd12-161">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="efd12-161">Click **Scale**.</span></span>
3. <span data-ttu-id="efd12-162">選取您想要變更其調整選項的排程。</span><span class="sxs-lookup"><span data-stu-id="efd12-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="efd12-163">如果您尚未定義排程，則預設為 [無排程時間]。</span><span class="sxs-lookup"><span data-stu-id="efd12-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="efd12-164">尋找 [依度量調整規模] 區段，然後選取 [CPU]。</span><span class="sxs-lookup"><span data-stu-id="efd12-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="efd12-165">現在您可以設定角色執行個體的最小和最大範圍、目標 CPU 使用量 (以觸發相應增加)，以及向上和向下調整的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="efd12-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![根據 cpu 負載調整雲端服務角色][cpu_scale]

> [!TIP]
> <span data-ttu-id="efd12-167">每當您看到 ![][tip_icon]，請將滑鼠移向它，您就可以取得特定設定執行作業的相關說明。</span><span class="sxs-lookup"><span data-stu-id="efd12-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="efd12-168">自動調整 - 佇列</span><span class="sxs-lookup"><span data-stu-id="efd12-168">Automatic scale - Queue</span></span>
<span data-ttu-id="efd12-169">此模式會自動調整佇列中的訊息數目高於或低於指定的臨界值。</span><span class="sxs-lookup"><span data-stu-id="efd12-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="efd12-170">在這種情況會建立或刪除角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="efd12-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="efd12-171">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，按一下 [雲端服務]，然後按一下雲端服務的名稱以開啟儀表板。</span><span class="sxs-lookup"><span data-stu-id="efd12-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="efd12-172">如果您沒有看到您的雲端服務，您可能需要從 [生產] 變更為 [預備]，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="efd12-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="efd12-173">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="efd12-173">Click **Scale**.</span></span>
3. <span data-ttu-id="efd12-174">尋找 [依度量調整規模] 區段，然後選取 [佇列]。</span><span class="sxs-lookup"><span data-stu-id="efd12-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="efd12-175">現在您可以設定角色執行個體的最小和最大範圍、每個執行個體要處理的佇列和佇列訊息數目，以及相應增加和減少的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="efd12-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![根據訊息佇列調整雲端服務角色][queue_scale]

> [!TIP]
> <span data-ttu-id="efd12-177">每當您看到 ![][tip_icon]，請將滑鼠移向它，您就可以取得特定設定執行作業的相關說明。</span><span class="sxs-lookup"><span data-stu-id="efd12-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="efd12-178">調整連結的資源</span><span class="sxs-lookup"><span data-stu-id="efd12-178">Scale linked resources</span></span>
<span data-ttu-id="efd12-179">通常，當您調整角色時，連應用程式所使用的資料庫也一起調整會比較好。</span><span class="sxs-lookup"><span data-stu-id="efd12-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="efd12-180">如果您將資料庫連結至雲端服務，您可以按一下適當的連結來存取該資源的調整設定。</span><span class="sxs-lookup"><span data-stu-id="efd12-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="efd12-181">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，按一下 [雲端服務]，然後按一下雲端服務的名稱以開啟儀表板。</span><span class="sxs-lookup"><span data-stu-id="efd12-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="efd12-182">如果您沒有看到您的雲端服務，您可能需要從 [生產] 變更為 [預備]，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="efd12-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="efd12-183">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="efd12-183">Click **Scale**.</span></span>
3. <span data-ttu-id="efd12-184">尋找 [連結的資源] 區段，然後按一下 [管理這個資料庫的調整規模]。</span><span class="sxs-lookup"><span data-stu-id="efd12-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="efd12-185">如果您沒有看到 [連結的資源] 區段，您可能沒有任何連結的資源。</span><span class="sxs-lookup"><span data-stu-id="efd12-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
