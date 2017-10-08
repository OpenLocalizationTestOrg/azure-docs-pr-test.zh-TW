---
title: "aaaAuto hello 入口網站中調整雲端服務 |Microsoft 文件"
description: "了解如何 toouse hello 雲端服務 web 角色或背景工作角色在 Azure 入口網站 tooconfigure 自動調整規模規則。"
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
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="3133b-103">如何 tooconfigure 自動調整 hello 入口網站中的雲端服務</span><span class="sxs-lookup"><span data-stu-id="3133b-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3133b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3133b-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="3133b-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="3133b-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="3133b-106">針對雲端服務背景工作角色設定條件，以觸發相應縮小或相應放大作業。</span><span class="sxs-lookup"><span data-stu-id="3133b-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="3133b-107">hello 角色 hello 條件可以根據 hello CPU、 磁碟或 hello 角色的網路負載。</span><span class="sxs-lookup"><span data-stu-id="3133b-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="3133b-108">您也可以設定其他 Azure 資源與您訂用帳戶相關聯的訊息佇列或 hello 標準為基礎的條件。</span><span class="sxs-lookup"><span data-stu-id="3133b-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="3133b-109">本文著重於雲端服務 web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="3133b-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="3133b-110">當您直接建立虛擬機器 (傳統) 時，它會裝載於雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="3133b-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="3133b-111">如果要調整標準虛擬機器，您可以將它與[可用性設定組](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)產生關聯，還可以手動開啟或關閉它們。</span><span class="sxs-lookup"><span data-stu-id="3133b-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="3133b-112">考量</span><span class="sxs-lookup"><span data-stu-id="3133b-112">Considerations</span></span>
<span data-ttu-id="3133b-113">您應該考慮下列資訊，然後再設定您的應用程式的規模調整 hello:</span><span class="sxs-lookup"><span data-stu-id="3133b-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="3133b-114">調整受到核心使用量影響。</span><span class="sxs-lookup"><span data-stu-id="3133b-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="3133b-115">較大型的角色執行個體會使用較多核心。</span><span class="sxs-lookup"><span data-stu-id="3133b-115">Larger role instances use more cores.</span></span> <span data-ttu-id="3133b-116">您可以調整應用程式的核心 hello 限制只在您訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3133b-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="3133b-117">例如，假設您的訂用帳戶有 20 個核心的限制。</span><span class="sxs-lookup"><span data-stu-id="3133b-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="3133b-118">如果您使用兩個中型大小的雲端服務 （4 核心總計） 執行應用程式，您可以只向上延展其他雲端服務部署您的訂用帳戶中的 hello 的剩餘 16 個核心。</span><span class="sxs-lookup"><span data-stu-id="3133b-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="3133b-119">如需關於大小的詳細資訊，請參閱[雲端服務的大小](cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="3133b-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="3133b-120">您可以依據佇列訊息臨界值來調整。</span><span class="sxs-lookup"><span data-stu-id="3133b-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="3133b-121">如需有關如何 toouse 佇列，請參閱[toouse hello 佇列儲存體服務的方式](../storage/queues/storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="3133b-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="3133b-122">您也可以調整與您訂用帳戶相關聯的其他資源。</span><span class="sxs-lookup"><span data-stu-id="3133b-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="3133b-123">tooenable 應用程式的高可用性，您應該確定部署與兩個或多個角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3133b-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="3133b-124">如需詳細資訊，請參閱 [服務等級協定](https://azure.microsoft.com/support/legal/sla/)。</span><span class="sxs-lookup"><span data-stu-id="3133b-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="3133b-125">調整所在之處</span><span class="sxs-lookup"><span data-stu-id="3133b-125">Where scale is located</span></span>
<span data-ttu-id="3133b-126">選取您的雲端服務之後，您應該有 hello 雲端服務刀鋒視窗中顯示。</span><span class="sxs-lookup"><span data-stu-id="3133b-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="3133b-127">Hello 雲端服務] 刀鋒視窗，在 [hello**角色和執行個體**磚中，選取 hello hello 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="3133b-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="3133b-128">**重要**： 請確定 tooclick hello 雲端服務角色，不 hello 低於 hello 角色的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3133b-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="3133b-129">選取 hello**標尺**磚。</span><span class="sxs-lookup"><span data-stu-id="3133b-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="3133b-130">自動調整</span><span class="sxs-lookup"><span data-stu-id="3133b-130">Automatic scale</span></span>
<span data-ttu-id="3133b-131">您可以使用下列任一種模式來設定角色的調整規模設定：**手動**或**自動**。</span><span class="sxs-lookup"><span data-stu-id="3133b-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="3133b-132">如您預期為手動時，設定執行個體 hello 絕對計數。</span><span class="sxs-lookup"><span data-stu-id="3133b-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="3133b-133">自動但是可讓您 tooset 規則會控制如何及說明更您應該進行調整。</span><span class="sxs-lookup"><span data-stu-id="3133b-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="3133b-134">設定 hello**縮放**太選項**排程和效能規則**。</span><span class="sxs-lookup"><span data-stu-id="3133b-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![具有設定檔與規則的雲端服務調整規模設定](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="3133b-136">現有的設定檔。</span><span class="sxs-lookup"><span data-stu-id="3133b-136">An existing profile.</span></span>
2. <span data-ttu-id="3133b-137">加入 hello 父系設定檔的規則。</span><span class="sxs-lookup"><span data-stu-id="3133b-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="3133b-138">新增另一個設定檔。</span><span class="sxs-lookup"><span data-stu-id="3133b-138">Add another profile.</span></span>

<span data-ttu-id="3133b-139">選取 [新增設定檔]。</span><span class="sxs-lookup"><span data-stu-id="3133b-139">Select **Add Profile**.</span></span> <span data-ttu-id="3133b-140">hello 設定檔會決定哪一種模式要 hello 標尺的 toouse:**一律**，**循環**，**固定日期**。</span><span class="sxs-lookup"><span data-stu-id="3133b-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="3133b-141">您已設定 hello 設定檔和規則之後，請選取 hello**儲存**hello 上方的圖示。</span><span class="sxs-lookup"><span data-stu-id="3133b-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="3133b-142">設定檔</span><span class="sxs-lookup"><span data-stu-id="3133b-142">Profile</span></span>
<span data-ttu-id="3133b-143">hello 設定檔設定最小和最大執行個體的 hello 調整，而且也時這個標尺範圍作用中。</span><span class="sxs-lookup"><span data-stu-id="3133b-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="3133b-144">**一律**</span><span class="sxs-lookup"><span data-stu-id="3133b-144">**Always**</span></span>

    <span data-ttu-id="3133b-145">一律讓此範圍的執行個體個數保持可用狀態。</span><span class="sxs-lookup"><span data-stu-id="3133b-145">Always keep this range of instances available.</span></span>  

    ![一律調整的雲端服務](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="3133b-147">**週期性**</span><span class="sxs-lookup"><span data-stu-id="3133b-147">**Recurrence**</span></span>

    <span data-ttu-id="3133b-148">選擇一組天數的 hello 週 tooscale。</span><span class="sxs-lookup"><span data-stu-id="3133b-148">Choose a set of days of hello week tooscale.</span></span>

    ![具有週期性排程的雲端服務調整規模](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="3133b-150">**固定日期**</span><span class="sxs-lookup"><span data-stu-id="3133b-150">**Fixed Date**</span></span>

    <span data-ttu-id="3133b-151">固定的日期範圍 tooscale hello 角色。</span><span class="sxs-lookup"><span data-stu-id="3133b-151">A fixed date range tooscale hello role.</span></span>

    ![具有固定日期的雲端服務調整規模](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="3133b-153">您已設定 hello 設定檔之後，請選取 hello**確定**在 hello hello 設定檔 刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3133b-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="3133b-154">規則</span><span class="sxs-lookup"><span data-stu-id="3133b-154">Rule</span></span>
<span data-ttu-id="3133b-155">規則會加入 tooa 設定檔，並代表觸發程序 hello 小數位數的條件。</span><span class="sxs-lookup"><span data-stu-id="3133b-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="3133b-156">hello 規則觸發程序為基礎的 hello 雲端服務 （CPU 使用量、 磁碟活動或網路活動） 的度量 toowhich 您可以加入條件式值。</span><span class="sxs-lookup"><span data-stu-id="3133b-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="3133b-157">此外，您可以根據其他 Azure 資源與您訂用帳戶相關聯的訊息佇列或 hello 度量 hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="3133b-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="3133b-158">您已設定 hello 規則之後，請選取 hello**確定**在 hello hello 規則刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3133b-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="3133b-159">備份 toomanual 小數位數</span><span class="sxs-lookup"><span data-stu-id="3133b-159">Back toomanual scale</span></span>
<span data-ttu-id="3133b-160">瀏覽 toohello[縮放設定](#where-scale-is-located)組 hello 和**縮放**太選項**手動輸入執行個體計數**。</span><span class="sxs-lookup"><span data-stu-id="3133b-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![具有設定檔與規則的雲端服務調整規模設定](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="3133b-162">這個設定會移除從 hello 角色自動縮放比例，然後直接設定 hello 執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="3133b-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="3133b-163">hello 小數位數 （手動或自動） 選項。</span><span class="sxs-lookup"><span data-stu-id="3133b-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="3133b-164">角色執行個體滑桿 tooset hello 執行個體至 tooscale。</span><span class="sxs-lookup"><span data-stu-id="3133b-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="3133b-165">Hello 角色 tooscale 到的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3133b-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="3133b-166">您已設定 hello 調整規模設定之後，請選取 hello**儲存**hello 上方的圖示。</span><span class="sxs-lookup"><span data-stu-id="3133b-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
