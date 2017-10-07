---
title: "aaaAuto hello 傳統入口網站中調整雲端服務 |Microsoft 文件"
description: "（傳統）了解如何 toouse hello 雲端服務 web 角色或背景工作角色在 Azure 傳統入口網站 tooconfigure 自動調整規模規則。"
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
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="231a3-103">如何 tooconfigure 自動調整 hello 傳統入口網站中的雲端服務</span><span class="sxs-lookup"><span data-stu-id="231a3-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="231a3-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="231a3-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="231a3-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="231a3-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="231a3-106">在 hello hello Azure 傳統入口網站的標尺頁面上，您可以設定您的 web 角色或背景工作角色的自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="231a3-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="231a3-107">或者，您可以設定手動調整，而非規則型自動縮放比例。</span><span class="sxs-lookup"><span data-stu-id="231a3-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="231a3-108">本文著重於雲端服務 web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="231a3-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="231a3-109">當您直接建立虛擬機器 (傳統) 時，它會裝載於雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="231a3-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="231a3-110">某些這項資訊適用於 toothese 類型的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="231a3-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="231a3-111">調整虛擬機器的可用性設定組只正在它們開啟和關閉根據您設定的 hello 調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="231a3-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="231a3-112">如需有關虛擬機器和可用性設定組的詳細資訊，請參閱[管理 hello 可用性的虛擬機器](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="231a3-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="231a3-113">您應該考慮下列資訊，然後再設定您的應用程式的規模調整 hello:</span><span class="sxs-lookup"><span data-stu-id="231a3-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="231a3-114">調整受到核心使用量影響。</span><span class="sxs-lookup"><span data-stu-id="231a3-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="231a3-115">較大型的角色執行個體會使用較多核心。</span><span class="sxs-lookup"><span data-stu-id="231a3-115">Larger role instances use more cores.</span></span> <span data-ttu-id="231a3-116">您可以調整應用程式的核心 hello 限制只在您訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="231a3-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="231a3-117">例如，假設您的訂用帳戶有 20 個核心的限制。</span><span class="sxs-lookup"><span data-stu-id="231a3-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="231a3-118">如果您使用兩個中型大小的雲端服務 （4 核心總計） 執行應用程式，您可以只向上延展其他雲端服務部署您的訂用帳戶中的 hello 的剩餘 16 個核心。</span><span class="sxs-lookup"><span data-stu-id="231a3-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="231a3-119">如需關於大小的詳細資訊，請參閱[雲端服務的大小](cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="231a3-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="231a3-120">您必須先建立佇列並且將它與角色建立關聯，然後才能根據訊息臨界值調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="231a3-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="231a3-121">如需詳細資訊，請參閱[toouse hello 佇列儲存體服務的方式](../storage/queues/storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="231a3-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="231a3-122">您可以調整資源的連結的 tooyour 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="231a3-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="231a3-123">如需將資源連結的詳細資訊，請參閱[How to： 連結資源 tooa 雲端服務](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="231a3-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="231a3-124">tooenable 應用程式的高可用性，您應該確定部署與兩個或多個角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="231a3-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="231a3-125">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="231a3-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="231a3-126">Schedule scaling</span><span class="sxs-lookup"><span data-stu-id="231a3-126">Schedule scaling</span></span>
<span data-ttu-id="231a3-127">根據預設，所有角色皆未遵循特定的排程。</span><span class="sxs-lookup"><span data-stu-id="231a3-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="231a3-128">因此，變更任何設定適用於整個 hello 年的所有日期和 tooall 時間。</span><span class="sxs-lookup"><span data-stu-id="231a3-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="231a3-129">如果您想要您可以設定手動或自動縮放比例的 hello 遵循模式的其中一個：</span><span class="sxs-lookup"><span data-stu-id="231a3-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="231a3-130">工作日</span><span class="sxs-lookup"><span data-stu-id="231a3-130">Weekdays</span></span>
* <span data-ttu-id="231a3-131">週末</span><span class="sxs-lookup"><span data-stu-id="231a3-131">Weekends</span></span>
* <span data-ttu-id="231a3-132">週間夜</span><span class="sxs-lookup"><span data-stu-id="231a3-132">Week nights</span></span>
* <span data-ttu-id="231a3-133">週間早上</span><span class="sxs-lookup"><span data-stu-id="231a3-133">Week mornings</span></span>
* <span data-ttu-id="231a3-134">特定日期</span><span class="sxs-lookup"><span data-stu-id="231a3-134">Specific dates</span></span>
* <span data-ttu-id="231a3-135">特定日期範圍</span><span class="sxs-lookup"><span data-stu-id="231a3-135">Specific date ranges</span></span>

<span data-ttu-id="231a3-136">hello 排程會設定在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)上 hello</span><span class="sxs-lookup"><span data-stu-id="231a3-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="231a3-137">[雲端服務] > \[您的雲端服務\] > [調整] > \[生產或預備\] 頁面。</span><span class="sxs-lookup"><span data-stu-id="231a3-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="231a3-138">按一下 hello**設定排程時間**按鈕要為每個角色 toochange。</span><span class="sxs-lookup"><span data-stu-id="231a3-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![以排程為基礎的雲端服務自動調整][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="231a3-140">手動調整</span><span class="sxs-lookup"><span data-stu-id="231a3-140">Manual scale</span></span>
<span data-ttu-id="231a3-141">在 [hello**標尺**] 頁面上，您可以手動增加或減少執行個體的雲端服務中的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="231a3-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="231a3-142">如果您沒有建立排程時，此設定已針對每個已建立的排程或 tooall 時間。</span><span class="sxs-lookup"><span data-stu-id="231a3-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="231a3-143">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**，然後按一下hello hello 雲端服務 tooopen hello 儀表板名稱。</span><span class="sxs-lookup"><span data-stu-id="231a3-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="231a3-144">如果您沒有看到您的雲端服務，您可能需要從 toochange**生產**太**臨時**，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="231a3-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="231a3-145">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="231a3-145">Click **Scale**.</span></span>
3. <span data-ttu-id="231a3-146">選取您想要擴充選項 toochange hello 排程。</span><span class="sxs-lookup"><span data-stu-id="231a3-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="231a3-147">*無法排定的時間*是 hello 預設值，如果您沒有定義的排程。</span><span class="sxs-lookup"><span data-stu-id="231a3-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="231a3-148">尋找 hello**依度量調整**區段，然後選取**NONE**。</span><span class="sxs-lookup"><span data-stu-id="231a3-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="231a3-149">這項設定是所有角色的 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="231a3-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="231a3-150">Hello 雲端服務中的每個角色都有變更的執行個體 toouse hello 號碼的滑桿。</span><span class="sxs-lookup"><span data-stu-id="231a3-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![手動調整雲端服務角色][manual_scale]
   
    <span data-ttu-id="231a3-152">如果您需要更多執行個體，您可能需要 toochange hello[雲端服務的虛擬機器大小](cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="231a3-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="231a3-153">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="231a3-153">Click **Save**.</span></span>  
   <span data-ttu-id="231a3-154">系統隨即根據您做的選取來新增或移除角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="231a3-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="231a3-155">每當您看到![][tip_icon]移動滑鼠 tooit，您可以取得的特定設定執行作業的相關說明。</span><span class="sxs-lookup"><span data-stu-id="231a3-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="231a3-156">自動調整 - CPU</span><span class="sxs-lookup"><span data-stu-id="231a3-156">Automatic scale - CPU</span></span>
<span data-ttu-id="231a3-157">如果 hello 平均 CPU 使用量百分比高於或低於指定臨界值，可調整此模式。</span><span class="sxs-lookup"><span data-stu-id="231a3-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="231a3-158">在這種情況會建立或刪除角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="231a3-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="231a3-159">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**，然後按一下hello hello 雲端服務 tooopen hello 儀表板名稱。</span><span class="sxs-lookup"><span data-stu-id="231a3-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="231a3-160">如果您沒有看到您的雲端服務，您可能需要從 toochange**生產**太**臨時**，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="231a3-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="231a3-161">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="231a3-161">Click **Scale**.</span></span>
3. <span data-ttu-id="231a3-162">選取您想要擴充選項 toochange hello 排程。</span><span class="sxs-lookup"><span data-stu-id="231a3-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="231a3-163">*無法排定的時間*是 hello 預設值，如果您沒有定義的排程。</span><span class="sxs-lookup"><span data-stu-id="231a3-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="231a3-164">尋找 hello**依度量調整**區段，然後選取**CPU**。</span><span class="sxs-lookup"><span data-stu-id="231a3-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="231a3-165">現在您可以設定最小和最大範圍的角色執行個體、 hello 目標 CPU 使用量 (tootrigger 下向上延展)，以及多少執行個體 tooscale 向上和向下的。</span><span class="sxs-lookup"><span data-stu-id="231a3-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![根據 cpu 負載調整雲端服務角色][cpu_scale]

> [!TIP]
> <span data-ttu-id="231a3-167">每當您看到![][tip_icon]移動滑鼠 tooit，您可以取得的特定設定執行作業的相關說明。</span><span class="sxs-lookup"><span data-stu-id="231a3-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="231a3-168">自動調整 - 佇列</span><span class="sxs-lookup"><span data-stu-id="231a3-168">Automatic scale - Queue</span></span>
<span data-ttu-id="231a3-169">如果訊息在佇列中的 hello 數目變成高於或低於指定閾值，自動調整這個模式。</span><span class="sxs-lookup"><span data-stu-id="231a3-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="231a3-170">在這種情況會建立或刪除角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="231a3-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="231a3-171">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**，然後按一下hello hello 雲端服務 tooopen hello 儀表板名稱。</span><span class="sxs-lookup"><span data-stu-id="231a3-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="231a3-172">如果您沒有看到您的雲端服務，您可能需要從 toochange**生產**太**臨時**，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="231a3-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="231a3-173">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="231a3-173">Click **Scale**.</span></span>
3. <span data-ttu-id="231a3-174">尋找 hello**依度量調整**區段，然後選取**佇列**。</span><span class="sxs-lookup"><span data-stu-id="231a3-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="231a3-175">現在您可以設定最小和最大範圍的角色執行個體，hello 佇列以及每個執行個體，以及多少執行個體 tooscale 增加和減少的佇列訊息 tooprocess 數目。</span><span class="sxs-lookup"><span data-stu-id="231a3-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![根據訊息佇列調整雲端服務角色][queue_scale]

> [!TIP]
> <span data-ttu-id="231a3-177">每當您看到![][tip_icon]移動滑鼠 tooit，您可以取得的特定設定執行作業的相關說明。</span><span class="sxs-lookup"><span data-stu-id="231a3-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="231a3-178">調整連結的資源</span><span class="sxs-lookup"><span data-stu-id="231a3-178">Scale linked resources</span></span>
<span data-ttu-id="231a3-179">通常當您調整角色時，它會是有幫助 tooscale hello 資料庫 hello 應用程式也使用。</span><span class="sxs-lookup"><span data-stu-id="231a3-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="231a3-180">如果您將連結 hello 資料庫 toohello 雲端服務，您可以存取 hello hello 適當的連結，即可調整該資源的設定。</span><span class="sxs-lookup"><span data-stu-id="231a3-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="231a3-181">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**，然後按一下hello hello 雲端服務 tooopen hello 儀表板名稱。</span><span class="sxs-lookup"><span data-stu-id="231a3-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="231a3-182">如果您沒有看到您的雲端服務，您可能需要從 toochange**生產**太**臨時**，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="231a3-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="231a3-183">按一下 [調整] 。</span><span class="sxs-lookup"><span data-stu-id="231a3-183">Click **Scale**.</span></span>
3. <span data-ttu-id="231a3-184">尋找 hello**已連結的資源**區段，然後按一下**管理此資料庫的調整規模**。</span><span class="sxs-lookup"><span data-stu-id="231a3-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="231a3-185">如果您沒有看到 [連結的資源] 區段，您可能沒有任何連結的資源。</span><span class="sxs-lookup"><span data-stu-id="231a3-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
