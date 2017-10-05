---
title: "手動調整執行個體計數或使用 Azure 入口網站自動調整 | Microsoft Docs"
description: "了解如何調整您的 Azure 服務。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: d171538ea57839eccddcc74ca099a39aee34ea10
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a><span data-ttu-id="e378a-103">手動或自動調整執行個體計數</span><span class="sxs-lookup"><span data-stu-id="e378a-103">Scale instance count manually or automatically</span></span>
<span data-ttu-id="e378a-104">在 [Azure 入口網站](https://portal.azure.com/)中，您可以手動設定服務的執行個體計數，或是藉由參數設定根據需求自行調整。</span><span class="sxs-lookup"><span data-stu-id="e378a-104">In the [Azure Portal](https://portal.azure.com/), you can manually set the instance count of your service, or, you can set parameters to have it automatically scale based on demand.</span></span> <span data-ttu-id="e378a-105">這通常稱為「相應放大」或「相應縮小」。</span><span class="sxs-lookup"><span data-stu-id="e378a-105">This is typically referred to as *Scale out* or *Scale in*.</span></span>

<span data-ttu-id="e378a-106">在根據執行個體計數進行調整之前，您應該考慮到調整除了會受到執行個體計數的影響以外，還會受到 **定價層** 的影響。</span><span class="sxs-lookup"><span data-stu-id="e378a-106">Before scaling based on instance count, you should consider that scaling is affected by **Pricing tier** in addition to instance count.</span></span> <span data-ttu-id="e378a-107">不同的定價層可以有不同數目的核心和記憶體，因此他們可以為相同數目的執行個體帶來較高的效能 (這就是「相應增加」或「相應減少」)。</span><span class="sxs-lookup"><span data-stu-id="e378a-107">Different pricing tiers can have different numbers cores and memory, and so they will have better performance for the same number of instances (which is *Scale up* or *Scale down*).</span></span> <span data-ttu-id="e378a-108">本文特別涵蓋了相應縮小和相應放大。</span><span class="sxs-lookup"><span data-stu-id="e378a-108">This article specifically covers *Scale in* and *out*.</span></span>

<span data-ttu-id="e378a-109">您可以在入口網站中進行調整，並且也可以使用 [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) 或 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) 來手動或自動調整級別。</span><span class="sxs-lookup"><span data-stu-id="e378a-109">You can scale in the portal, and you can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to adjust scale manually or automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="e378a-110">這篇文章說明如何在入口網站 ([http://portal.azure.com](http://portal.azure.com)) 中建立自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="e378a-110">This article describes how to create an autoscale setting in the portal at [http://portal.azure.com](http://portal.azure.com).</span></span> <span data-ttu-id="e378a-111">在此入口網站中建立的自動調整設定不能在傳統入口網站 ([http://manage.windowsazure.com](http://manage.windowsazure.com)) 中編輯。</span><span class="sxs-lookup"><span data-stu-id="e378a-111">Autoscale settings created in this portal cannot be edited it the classic portal ([http://manage.windowsazure.com](http://manage.windowsazure.com)).</span></span>
> 
> 

## <a name="scaling-manually"></a><span data-ttu-id="e378a-112">手動調整</span><span class="sxs-lookup"><span data-stu-id="e378a-112">Scaling manually</span></span>
1. <span data-ttu-id="e378a-113">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [瀏覽]，然後瀏覽至您想要調整的資源，例如 [App Service 方案]。</span><span class="sxs-lookup"><span data-stu-id="e378a-113">In the [Azure Portal](https://portal.azure.com/), click **Browse**, then navigate to the resource you want to scale, such as an **App Service plan**.</span></span>
2. <span data-ttu-id="e378a-114">按一下 [設定] > [相應放大 (App Service 方案)]。</span><span class="sxs-lookup"><span data-stu-id="e378a-114">Click **Settings > Scale out (App Service plan).**</span></span>
3. <span data-ttu-id="e378a-115">您可以在 [級別] 刀鋒視窗的頂端，查看服務的自動調整動作歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="e378a-115">At the top of the **Scale** blade you can see a history of autoscale actions of the service.</span></span>
   
    ![Scale blade](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > <span data-ttu-id="e378a-117">這個圖表僅會顯示自動調整所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="e378a-117">Only actions that are performed by autoscale will show up in this chart.</span></span> <span data-ttu-id="e378a-118">如果您手動調整執行個體計數，則此變更將不會反映在該圖表中。</span><span class="sxs-lookup"><span data-stu-id="e378a-118">If you manually adjust the instance count, the change will not be reflected in this chart.</span></span>
   > 
   > 
4. <span data-ttu-id="e378a-119">您可以使用滑桿手動調整 [ **執行個體** ] 數目。</span><span class="sxs-lookup"><span data-stu-id="e378a-119">You can manually adjust the number **Instances** with slider.</span></span>
5. <span data-ttu-id="e378a-120">按一下 [ **儲存** ] 命令，您的執行個體便會立即被調整到該數目。</span><span class="sxs-lookup"><span data-stu-id="e378a-120">Click the **Save** command and you'll be scaled to that number of instances almost immediately.</span></span>

## <a name="scaling-based-on-a-pre-set-metric"></a><span data-ttu-id="e378a-121">根據預先設定的計量進行調整</span><span class="sxs-lookup"><span data-stu-id="e378a-121">Scaling based on a pre-set metric</span></span>
<span data-ttu-id="e378a-122">如果您要讓執行個體數目根據計量自動調整，請在 [ **調整依據** ] 下拉式清單中選取您要的計量。</span><span class="sxs-lookup"><span data-stu-id="e378a-122">If you want the number of instances to automatically adjust based on a metric, select the metric you want in the **Scale by** dropdown.</span></span> <span data-ttu-id="e378a-123">例如在 [App Service 方案]，您可以根據 [CPU 百分比] 進行調整。</span><span class="sxs-lookup"><span data-stu-id="e378a-123">For example, for an **App Service plan** you can scale by **CPU Percentage**.</span></span>

1. <span data-ttu-id="e378a-124">當您選取計量時，您會看到一個滑桿，和/或可輸入您要調整的執行個體數目範圍文字方塊：</span><span class="sxs-lookup"><span data-stu-id="e378a-124">When you select a metric you'll get a slider, and/or, text boxes to enter the number of instances you want to scale between:</span></span>
   
    ![Scale blade with CPU Percentage](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    <span data-ttu-id="e378a-126">無論負載為何，自動調整絕對不會將您的服務調整低於或高於您的設定界限。</span><span class="sxs-lookup"><span data-stu-id="e378a-126">Autoscale will never take your service below or above the boundaries that you set, no matter your load.</span></span>
2. <span data-ttu-id="e378a-127">其次，您可以選擇計量的目標範圍。</span><span class="sxs-lookup"><span data-stu-id="e378a-127">Second, you choose the target range for the metric.</span></span> <span data-ttu-id="e378a-128">例如，如果您選擇 [ **CPU 百分比**]，您可以為服務中的所有執行個體設定平均 CPU 的目標。</span><span class="sxs-lookup"><span data-stu-id="e378a-128">For example, if you chose **CPU percentage**, you can set a target for the average CPU across all of the instances in your service.</span></span> <span data-ttu-id="e378a-129">當平均 CPU 超過您所定義的最大值時，便會發生相應放大，同樣地，每當平均 CPU 低於最小值時，便會發生相應縮小。</span><span class="sxs-lookup"><span data-stu-id="e378a-129">A scale out will happen when the average CPU exceeds the maximum you define, likewise, a scale in will happen whenever the average CPU drops below the minimum.</span></span>
3. <span data-ttu-id="e378a-130">按一下 [ **儲存** ] 命令。</span><span class="sxs-lookup"><span data-stu-id="e378a-130">Click the **Save** command.</span></span> <span data-ttu-id="e378a-131">自動調整每隔幾分鐘就會檢查一次，以確定您仍在計量的執行個體範圍和目標內。</span><span class="sxs-lookup"><span data-stu-id="e378a-131">Autoscale will check every few minutes to make sure that you are in the instance range and target for your metric.</span></span> <span data-ttu-id="e378a-132">當服務收到額外流量時，無需執行任何動作，您就會獲到更多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="e378a-132">When your service receives additional traffic,  you will get more instances without doing anything.</span></span>

## <a name="scale-based-on-other-metrics"></a><span data-ttu-id="e378a-133">根據其他計量進行調整</span><span class="sxs-lookup"><span data-stu-id="e378a-133">Scale based on other metrics</span></span>
<span data-ttu-id="e378a-134">您可以根據出現在 [ **調整依據** ] 下拉式清單中的計量 (預設格式除外) 進行調整，而且甚至可以有一組複雜的相應放大和相應縮小規則。</span><span class="sxs-lookup"><span data-stu-id="e378a-134">You can scale based on metrics other than the presets that appear in the **Scale by** dropdown, and can even have a complex set of scale out and scale in rules.</span></span>

### <a name="adding-or-changing-a-rule"></a><span data-ttu-id="e378a-135">新增或變更規則</span><span class="sxs-lookup"><span data-stu-id="e378a-135">Adding or changing a rule</span></span>
1. <span data-ttu-id="e378a-136">在 [調整依據] 下拉式清單中選擇 [排程和效能規則]：![效能規則](./media/insights-how-to-scale/Insights_PerformanceRules.png)</span><span class="sxs-lookup"><span data-stu-id="e378a-136">Choose the **schedule and performance rules** in the **Scale by** dropdown: ![Performance rules](./media/insights-how-to-scale/Insights_PerformanceRules.png)</span></span>
2. <span data-ttu-id="e378a-137">如果您先前有過自動調整，您便會看到先前使用的確切規則的檢視。</span><span class="sxs-lookup"><span data-stu-id="e378a-137">If you previously had autoscale, on you'll see a view of the exact rules that you had.</span></span>
3. <span data-ttu-id="e378a-138">若要根據另一個計量進行調整，請按一下 [ **新增規則** ] 資料列。</span><span class="sxs-lookup"><span data-stu-id="e378a-138">To scale based on another metric click the **Add Rule** row.</span></span> <span data-ttu-id="e378a-139">您也可以按一下其中一個現有資料列，將您先前使用的計量變更為所需的調整依據計量。</span><span class="sxs-lookup"><span data-stu-id="e378a-139">You can also click one of the existing rows to change from the metric you previously had to the metric you want to scale by.</span></span>
   <span data-ttu-id="e378a-140">![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)</span><span class="sxs-lookup"><span data-stu-id="e378a-140">![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)</span></span>
4. <span data-ttu-id="e378a-141">現在，您必須選取所需的調整依據計量。</span><span class="sxs-lookup"><span data-stu-id="e378a-141">Now you need to select which metric you want to scale by.</span></span> <span data-ttu-id="e378a-142">選擇計量時會有幾個考量事項：</span><span class="sxs-lookup"><span data-stu-id="e378a-142">When choosing a metric there are a couple things to consider:</span></span>
   
   * <span data-ttu-id="e378a-143">計量的來源 *資源* 。</span><span class="sxs-lookup"><span data-stu-id="e378a-143">The *resource* the metric comes from.</span></span> <span data-ttu-id="e378a-144">一般而言，這會與您要調整的資源相同。</span><span class="sxs-lookup"><span data-stu-id="e378a-144">Typically, this will be the same as the resource you are scaling.</span></span> <span data-ttu-id="e378a-145">不過，如果您想要根據儲存體佇列的深度進行調整，則資源就會是您的調整依據佇列。</span><span class="sxs-lookup"><span data-stu-id="e378a-145">However, if you want to scale by the depth of a Storage queue, the resource is the queue that you want to scale by.</span></span>
   * <span data-ttu-id="e378a-146">本身的 *計量名稱* 。</span><span class="sxs-lookup"><span data-stu-id="e378a-146">The *metric name* itself.</span></span>
   * <span data-ttu-id="e378a-147">計量的 *時間彙總* 。</span><span class="sxs-lookup"><span data-stu-id="e378a-147">The *time aggregation* of the metric.</span></span> <span data-ttu-id="e378a-148">這是資料在 *持續時間*內組合的方式。</span><span class="sxs-lookup"><span data-stu-id="e378a-148">This is how the data is combine over the *duration*.</span></span>
5. <span data-ttu-id="e378a-149">選擇您的計量之後，您會選擇計量的臨界值，以及運算子。</span><span class="sxs-lookup"><span data-stu-id="e378a-149">After choosing your metric you choose the threshold for the metric, and the operator.</span></span> <span data-ttu-id="e378a-150">例如，假設 [大於] 設為 [80%]。</span><span class="sxs-lookup"><span data-stu-id="e378a-150">For example, you could say **Greater than** **80%**.</span></span>
6. <span data-ttu-id="e378a-151">然後選擇您要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="e378a-151">Then choose the action that you want to take.</span></span> <span data-ttu-id="e378a-152">共有幾種不同的動作類型：</span><span class="sxs-lookup"><span data-stu-id="e378a-152">There are a couple different type of actions:</span></span>
   
   * <span data-ttu-id="e378a-153">增加或減少依據 - 這會新增或移除您所定義執行個體數目的 [ **值** ]</span><span class="sxs-lookup"><span data-stu-id="e378a-153">Increase or decrease by - this will add or remove the **Value** number of instances you define</span></span>
   * <span data-ttu-id="e378a-154">增加或減少百分比 - 這會以百分比來變更執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="e378a-154">Increase or decrease percent - this will change the instance count by a percent.</span></span> <span data-ttu-id="e378a-155">例如，您可以在 [ **值** ] 欄位中輸入 25，如果您目前有 8 個執行個體，則會增加 2 個執行個體。</span><span class="sxs-lookup"><span data-stu-id="e378a-155">For example, you could put 25 in the **Value** field, and if you currently had 8 instances, 2 would be added.</span></span>
   * <span data-ttu-id="e378a-156">增加或減少至 - 這會將執行個體計數設定為您所定義的 [ **值** ]。</span><span class="sxs-lookup"><span data-stu-id="e378a-156">Increase or decrease to - this will set the instance count to the **Value** you define.</span></span>
7. <span data-ttu-id="e378a-157">最後，您可以選擇等待期間 - 在前次調整動作之後，此規則要再次執行調整前所應等待的時間。</span><span class="sxs-lookup"><span data-stu-id="e378a-157">Finally, you can choose cool down - how long this rule should wait after the previous scale action to scale again.</span></span>
8. <span data-ttu-id="e378a-158">設定規則之後，請按 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="e378a-158">After configuring your rule hit **OK**.</span></span>
9. <span data-ttu-id="e378a-159">在設定您所有想要的規則之後，請務必要按 [ **儲存** ] 命令。</span><span class="sxs-lookup"><span data-stu-id="e378a-159">Once you have configured all of the rules you want, be sure to hit the **Save** command.</span></span>

### <a name="scaling-with-multiple-steps"></a><span data-ttu-id="e378a-160">使用多個步驟進行調整</span><span class="sxs-lookup"><span data-stu-id="e378a-160">Scaling with multiple steps</span></span>
<span data-ttu-id="e378a-161">以上都是基本範例。</span><span class="sxs-lookup"><span data-stu-id="e378a-161">The examples above are pretty basic.</span></span> <span data-ttu-id="e378a-162">不過，如果您想要更靈活地相應增加 (或減少)，您甚至可以為相同的計量新增多項調整規則。</span><span class="sxs-lookup"><span data-stu-id="e378a-162">However, if you want to be more agressive about scaling up (or down), you can even add multiple scale rules for the same metric.</span></span> <span data-ttu-id="e378a-163">例如，您可以在 CPU 百分比上定義兩項調整規則：</span><span class="sxs-lookup"><span data-stu-id="e378a-163">For example, you can define two scale rules on CPU percentage:</span></span>

1. <span data-ttu-id="e378a-164">如果 CPU 百分比高於 60%，則相應增加 1 個執行個體</span><span class="sxs-lookup"><span data-stu-id="e378a-164">Scale out by 1 instance if CPU percentage is above 60%</span></span>
2. <span data-ttu-id="e378a-165">如果 CPU 百分比高於 85%，則相應增加 3 個執行個體</span><span class="sxs-lookup"><span data-stu-id="e378a-165">Scale out by 3 instances if CPU percentage is above 85%</span></span>

![Multiple scale rules](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

<span data-ttu-id="e378a-167">透過這項附加規則，如果您的負載在調整動作之前超過 85%，您將會增加兩個執行個體，而不是一個。</span><span class="sxs-lookup"><span data-stu-id="e378a-167">With this additional rule, if your load exceeds 85% before a scale action, you will get two additional instances instead of one.</span></span>

## <a name="scale-based-on-a-schedule"></a><span data-ttu-id="e378a-168">根據排程進行調整</span><span class="sxs-lookup"><span data-stu-id="e378a-168">Scale based on a schedule</span></span>
<span data-ttu-id="e378a-169">根據預設，當您建立調整規則時，它會一律套用。</span><span class="sxs-lookup"><span data-stu-id="e378a-169">By default, when you create a scale rule it will  always apply.</span></span> <span data-ttu-id="e378a-170">當您按一下 [設定檔標頭] 時會看到：</span><span class="sxs-lookup"><span data-stu-id="e378a-170">You can see that when you click on the profile header:</span></span>

![設定檔](./media/insights-how-to-scale/Insights_Profile.png)

<span data-ttu-id="e378a-172">不過，在一天、一週和週末當中，您可能會想要進行更積極的調整。</span><span class="sxs-lookup"><span data-stu-id="e378a-172">However, you may want to have more agressive scaling during the day, or the week, than on the weekend.</span></span> <span data-ttu-id="e378a-173">您甚至可以在下班時間完全關閉您的服務。</span><span class="sxs-lookup"><span data-stu-id="e378a-173">You could even shut down your service entirely off working hours.</span></span>

1. <span data-ttu-id="e378a-174">若要這樣做，請在您的設定檔中選取 [週期性] 而不是 [一律使用]，然後選擇您要設定檔套用的時間。</span><span class="sxs-lookup"><span data-stu-id="e378a-174">To do this, on the profile you have, select **recurrence** instead of **always,** and choose the times that you want the profile to apply.</span></span>
2. <span data-ttu-id="e378a-175">例如，若要準備要在一週當中套用的設定檔，請在 [天] 下拉式清單中取消核取 [星期六] 和 [星期日]。</span><span class="sxs-lookup"><span data-stu-id="e378a-175">For example, to have a profile that applies during the week, in the **Days** dropdown uncheck **Saturday** and **Sunday**.</span></span>
3. <span data-ttu-id="e378a-176">若要準備要在白天當中套用的設定檔，請將 [ **開始時間** ] 設定為您要開始的當日時間。</span><span class="sxs-lookup"><span data-stu-id="e378a-176">To have a profile that applies during the daytime, set the **Start time** to the time of day that you want to start at.</span></span>
   
    ![預設週期](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. <span data-ttu-id="e378a-178">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e378a-178">Click **OK**.</span></span>
5. <span data-ttu-id="e378a-179">接下來，您必須新增您要在其他時候套用的設定檔。</span><span class="sxs-lookup"><span data-stu-id="e378a-179">Next, you will need to add the profile that you want to apply at other times.</span></span> <span data-ttu-id="e378a-180">按一下 [ **新增設定檔** ] 資料列。</span><span class="sxs-lookup"><span data-stu-id="e378a-180">Click the **Add Profile** row.</span></span>
    <span data-ttu-id="e378a-181">![下班](./media/insights-how-to-scale/Insights_ProfileOffWork.png)</span><span class="sxs-lookup"><span data-stu-id="e378a-181">![Off Work](./media/insights-how-to-scale/Insights_ProfileOffWork.png)</span></span>
6. <span data-ttu-id="e378a-182">為您的第二個新設定檔命名，例如，您可以把它叫做 **下班**。</span><span class="sxs-lookup"><span data-stu-id="e378a-182">Name your new, second, profile, for example you could call it **Off work**.</span></span>
7. <span data-ttu-id="e378a-183">然後再次選取 [ **週期性** ]，並選擇在這段期間您想要的執行個體計數範圍。</span><span class="sxs-lookup"><span data-stu-id="e378a-183">Then select **recurrence** again, and choose the instance count range you want during this time.</span></span>
8. <span data-ttu-id="e378a-184">和預設設定檔一樣，選擇要設定檔套用的 [天]，以及當天的 [開始時間]。</span><span class="sxs-lookup"><span data-stu-id="e378a-184">As with the Default profile, choose the **Days** you want this profile to apply to, and the **Start time** during the day.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e378a-185">自動調整會為您所選取的任何 [ **時區** ] 使用日光節約規則。</span><span class="sxs-lookup"><span data-stu-id="e378a-185">Autoscale will use the Daylight savings rules for whichever **Time zone** you select.</span></span> <span data-ttu-id="e378a-186">不過，在日光節約時間期間，UTC 時差會顯示基本的時區時差，而不是日光節約的 UTC 時差。</span><span class="sxs-lookup"><span data-stu-id="e378a-186">However, during Daylight savings time the UTC offset will show the base Time zone offset, not the Daylight savings UTC offset.</span></span>
   > 
   > 
9. <span data-ttu-id="e378a-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e378a-187">Click **OK**.</span></span>
10. <span data-ttu-id="e378a-188">現在，您必須新增您要在第二個設定檔期間套用的任何規則。</span><span class="sxs-lookup"><span data-stu-id="e378a-188">Now, you will need to add whatever rules you want to apply during your second profile.</span></span> <span data-ttu-id="e378a-189">按一下 [ **新增規則**]，然後您可以在預設設定檔中建構相同的規則。</span><span class="sxs-lookup"><span data-stu-id="e378a-189">Click **Add Rule**, and then you could construct the same rule you have during the Default profile.</span></span>
    
    ![新增規則至下班](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. <span data-ttu-id="e378a-191">請務必建立相應放大和相應縮小這兩個規則，否則在設定檔期間，執行個體計數將只增加 (或減少)。</span><span class="sxs-lookup"><span data-stu-id="e378a-191">Be sure to create both a rule for scale out and scale in, or else during the profile the instance count will only grow (or decrease).</span></span>
12. <span data-ttu-id="e378a-192">最後，按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="e378a-192">Finally, click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e378a-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e378a-193">Next steps</span></span>
* <span data-ttu-id="e378a-194">[監視服務計量](insights-how-to-customize-monitoring.md) 以確保您的服務可用且可回應。</span><span class="sxs-lookup"><span data-stu-id="e378a-194">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="e378a-195">[啟用監視和診斷](insights-how-to-use-diagnostics.md) 來在您服務中收集詳細的高頻率計量。</span><span class="sxs-lookup"><span data-stu-id="e378a-195">[Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="e378a-196">[接收警示通知](insights-receive-alert-notifications.md) 。</span><span class="sxs-lookup"><span data-stu-id="e378a-196">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="e378a-197">[監視應用程式效能](../application-insights/app-insights-azure-web-apps.md) 。</span><span class="sxs-lookup"><span data-stu-id="e378a-197">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span></span>
* <span data-ttu-id="e378a-198">[檢視事件和活動記錄檔](insights-debugging-with-events.md)以了解在您服務內發生的所有內容。</span><span class="sxs-lookup"><span data-stu-id="e378a-198">[View events and activity log](insights-debugging-with-events.md) to learn everything that has happened in your service.</span></span>
* <span data-ttu-id="e378a-199">[監視任何網頁的可用性和回應性](../application-insights/app-insights-monitor-web-app-availability.md) ，讓您可以找出您的頁面是否關閉。</span><span class="sxs-lookup"><span data-stu-id="e378a-199">[Monitor availability and responsiveness of any web page](../application-insights/app-insights-monitor-web-app-availability.md) with Application Insights so you can find out if your page is down.</span></span>

