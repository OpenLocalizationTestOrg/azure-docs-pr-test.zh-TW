---
title: "aaaScale 手動或透過 Azure 入口網站的自動調整執行個體計數 |Microsoft 文件"
description: "深入了解如何 tooscale Azure 服務。"
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
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a><span data-ttu-id="68edb-103">手動或自動調整執行個體計數</span><span class="sxs-lookup"><span data-stu-id="68edb-103">Scale instance count manually or automatically</span></span>
<span data-ttu-id="68edb-104">在 [hello [Azure 入口網站](https://portal.azure.com/)、 您可以手動設定 hello 執行個體計數，您的服務，或您可以設定自動調整規模的 toohave 根據需求的參數。</span><span class="sxs-lookup"><span data-stu-id="68edb-104">In hello [Azure Portal](https://portal.azure.com/), you can manually set hello instance count of your service, or, you can set parameters toohave it automatically scale based on demand.</span></span> <span data-ttu-id="68edb-105">這是通常參照的 tooas*向外延展*或*縮放*。</span><span class="sxs-lookup"><span data-stu-id="68edb-105">This is typically referred tooas *Scale out* or *Scale in*.</span></span>

<span data-ttu-id="68edb-106">調整執行個體計數為基礎之前，您應該考慮的縮放比例會受到**定價層**加法 tooinstance 計數中。</span><span class="sxs-lookup"><span data-stu-id="68edb-106">Before scaling based on instance count, you should consider that scaling is affected by **Pricing tier** in addition tooinstance count.</span></span> <span data-ttu-id="68edb-107">不同的定價層可以有不同數量的核心和記憶體，並且因此會有較佳效能 hello 相同數目的執行個體 (也就是*向上延展*或*向下調整*)。</span><span class="sxs-lookup"><span data-stu-id="68edb-107">Different pricing tiers can have different numbers cores and memory, and so they will have better performance for hello same number of instances (which is *Scale up* or *Scale down*).</span></span> <span data-ttu-id="68edb-108">本文特別涵蓋了相應縮小和相應放大。</span><span class="sxs-lookup"><span data-stu-id="68edb-108">This article specifically covers *Scale in* and *out*.</span></span>

<span data-ttu-id="68edb-109">您可以調整在 hello 入口網站，而且您也可以使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx)或[.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust 在手動或自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="68edb-109">You can scale in hello portal, and you can also use hello [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust scale manually or automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="68edb-110">本文說明如何自動調整設定在 hello 入口網站的 toocreate [http://portal.azure.com](http://portal.azure.com)。在此入口網站中建立的自動調整規模設定無法編輯它 hello 傳統入口網站 ([http://manage.windowsazure.com](http://manage.windowsazure.com))。</span><span class="sxs-lookup"><span data-stu-id="68edb-110">This article describes how toocreate an autoscale setting in hello portal at [http://portal.azure.com](http://portal.azure.com). Autoscale settings created in this portal cannot be edited it hello classic portal ([http://manage.windowsazure.com](http://manage.windowsazure.com)).</span></span>
> 
> 

## <a name="scaling-manually"></a><span data-ttu-id="68edb-111">手動調整</span><span class="sxs-lookup"><span data-stu-id="68edb-111">Scaling manually</span></span>
1. <span data-ttu-id="68edb-112">在 [hello [Azure 入口網站](https://portal.azure.com/)，按一下 [**瀏覽**，然後瀏覽 toohello 想資源 tooscale，例如**應用程式服務方案**。</span><span class="sxs-lookup"><span data-stu-id="68edb-112">In hello [Azure Portal](https://portal.azure.com/), click **Browse**, then navigate toohello resource you want tooscale, such as an **App Service plan**.</span></span>
2. <span data-ttu-id="68edb-113">按一下 [設定] > [相應放大 (App Service 方案)]。</span><span class="sxs-lookup"><span data-stu-id="68edb-113">Click **Settings > Scale out (App Service plan).**</span></span>
3. <span data-ttu-id="68edb-114">頂端的 hello hello**標尺**刀鋒視窗，您可以看到 hello 服務的自動調整規模動作的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="68edb-114">At hello top of hello **Scale** blade you can see a history of autoscale actions of hello service.</span></span>
   
    ![Scale blade](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > <span data-ttu-id="68edb-116">這個圖表僅會顯示自動調整所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="68edb-116">Only actions that are performed by autoscale will show up in this chart.</span></span> <span data-ttu-id="68edb-117">如果您手動調整 hello 執行個體計數，hello 變更將不會反映在此圖表中。</span><span class="sxs-lookup"><span data-stu-id="68edb-117">If you manually adjust hello instance count, hello change will not be reflected in this chart.</span></span>
   > 
   > 
4. <span data-ttu-id="68edb-118">您可以手動調整 hello 數目**執行個體**使用滑桿。</span><span class="sxs-lookup"><span data-stu-id="68edb-118">You can manually adjust hello number **Instances** with slider.</span></span>
5. <span data-ttu-id="68edb-119">按一下 hello**儲存**命令，而且將會是幾乎立即調整 toothat 執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="68edb-119">Click hello **Save** command and you'll be scaled toothat number of instances almost immediately.</span></span>

## <a name="scaling-based-on-a-pre-set-metric"></a><span data-ttu-id="68edb-120">根據預先設定的計量進行調整</span><span class="sxs-lookup"><span data-stu-id="68edb-120">Scaling based on a pre-set metric</span></span>
<span data-ttu-id="68edb-121">如果您想要的執行個體的 tooautomatically 調整根據度量的 hello 數字，選取 hello hello 中您要的度量**縮放**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="68edb-121">If you want hello number of instances tooautomatically adjust based on a metric, select hello metric you want in hello **Scale by** dropdown.</span></span> <span data-ttu-id="68edb-122">例如在 [App Service 方案]，您可以根據 [CPU 百分比] 進行調整。</span><span class="sxs-lookup"><span data-stu-id="68edb-122">For example, for an **App Service plan** you can scale by **CPU Percentage**.</span></span>

1. <span data-ttu-id="68edb-123">當選取度量，得到滑桿，及/或，您想要的 tooscale 之間文字方塊 tooenter hello 執行個體數目：</span><span class="sxs-lookup"><span data-stu-id="68edb-123">When you select a metric you'll get a slider, and/or, text boxes tooenter hello number of instances you want tooscale between:</span></span>
   
    ![Scale blade with CPU Percentage](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    <span data-ttu-id="68edb-125">自動調整規模絕對不會接受服務低於或高於 hello 界限的設定，無論您的負載。</span><span class="sxs-lookup"><span data-stu-id="68edb-125">Autoscale will never take your service below or above hello boundaries that you set, no matter your load.</span></span>
2. <span data-ttu-id="68edb-126">第二，您可以選擇 hello hello 度量的目標範圍。</span><span class="sxs-lookup"><span data-stu-id="68edb-126">Second, you choose hello target range for hello metric.</span></span> <span data-ttu-id="68edb-127">例如，如果您選擇**CPU 百分比**，您可以設定目標 hello 平均 CPU hello 執行個體的所有服務中。</span><span class="sxs-lookup"><span data-stu-id="68edb-127">For example, if you chose **CPU percentage**, you can set a target for hello average CPU across all of hello instances in your service.</span></span> <span data-ttu-id="68edb-128">Hello 平均 CPU 超過 hello 您定義的最大值時，將會發生向外的延展，同樣地，每當 hello 平均 CPU 必須低於最小的 hello 將會發生在標尺。</span><span class="sxs-lookup"><span data-stu-id="68edb-128">A scale out will happen when hello average CPU exceeds hello maximum you define, likewise, a scale in will happen whenever hello average CPU drops below hello minimum.</span></span>
3. <span data-ttu-id="68edb-129">按一下 hello**儲存**命令。</span><span class="sxs-lookup"><span data-stu-id="68edb-129">Click hello **Save** command.</span></span> <span data-ttu-id="68edb-130">自動調整規模將會檢查確定您在您的度量是在 hello 執行個體範圍和目標每隔幾分鐘的時間 toomake。</span><span class="sxs-lookup"><span data-stu-id="68edb-130">Autoscale will check every few minutes toomake sure that you are in hello instance range and target for your metric.</span></span> <span data-ttu-id="68edb-131">當服務收到額外流量時，無需執行任何動作，您就會獲到更多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="68edb-131">When your service receives additional traffic,  you will get more instances without doing anything.</span></span>

## <a name="scale-based-on-other-metrics"></a><span data-ttu-id="68edb-132">根據其他計量進行調整</span><span class="sxs-lookup"><span data-stu-id="68edb-132">Scale based on other metrics</span></span>
<span data-ttu-id="68edb-133">您可以調整根據度量資訊會出現在 hello 的 hello 預設以外**縮放**下拉式清單中，並可以即使有一組複雜的向外延展並調整規模規則中。</span><span class="sxs-lookup"><span data-stu-id="68edb-133">You can scale based on metrics other than hello presets that appear in hello **Scale by** dropdown, and can even have a complex set of scale out and scale in rules.</span></span>

### <a name="adding-or-changing-a-rule"></a><span data-ttu-id="68edb-134">新增或變更規則</span><span class="sxs-lookup"><span data-stu-id="68edb-134">Adding or changing a rule</span></span>
1. <span data-ttu-id="68edb-135">選擇 hello**排程和效能規則**在 hello**縮放**下拉式清單中：![效能規則](./media/insights-how-to-scale/Insights_PerformanceRules.png)</span><span class="sxs-lookup"><span data-stu-id="68edb-135">Choose hello **schedule and performance rules** in hello **Scale by** dropdown: ![Performance rules](./media/insights-how-to-scale/Insights_PerformanceRules.png)</span></span>
2. <span data-ttu-id="68edb-136">如果您先前已自動調整規模，在您會看到您所擁有的 hello 確切規則的檢視。</span><span class="sxs-lookup"><span data-stu-id="68edb-136">If you previously had autoscale, on you'll see a view of hello exact rules that you had.</span></span>
3. <span data-ttu-id="68edb-137">tooscale 根據另一個公制按一下 hello**加入規則**資料列。</span><span class="sxs-lookup"><span data-stu-id="68edb-137">tooscale based on another metric click hello **Add Rule** row.</span></span> <span data-ttu-id="68edb-138">您也可以按一下其中一個的 hello 現有資料列 toochange 從 hello 度量，您先前必須要由 tooscale toohello 度量。</span><span class="sxs-lookup"><span data-stu-id="68edb-138">You can also click one of hello existing rows toochange from hello metric you previously had toohello metric you want tooscale by.</span></span>
   <span data-ttu-id="68edb-139">![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)</span><span class="sxs-lookup"><span data-stu-id="68edb-139">![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)</span></span>
4. <span data-ttu-id="68edb-140">現在您需要的 tooselect 要由 tooscale 的度量。</span><span class="sxs-lookup"><span data-stu-id="68edb-140">Now you need tooselect which metric you want tooscale by.</span></span> <span data-ttu-id="68edb-141">當選擇度量有幾件事 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="68edb-141">When choosing a metric there are a couple things tooconsider:</span></span>
   
   * <span data-ttu-id="68edb-142">hello*資源*hello 度量來源。</span><span class="sxs-lookup"><span data-stu-id="68edb-142">hello *resource* hello metric comes from.</span></span> <span data-ttu-id="68edb-143">一般而言，這會是 hello 與 hello 資源會擴充相同。</span><span class="sxs-lookup"><span data-stu-id="68edb-143">Typically, this will be hello same as hello resource you are scaling.</span></span> <span data-ttu-id="68edb-144">不過，如果您想要的儲存體佇列的 hello 深度 tooscale，hello 資源是您想要依 tooscale 的 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="68edb-144">However, if you want tooscale by hello depth of a Storage queue, hello resource is hello queue that you want tooscale by.</span></span>
   * <span data-ttu-id="68edb-145">hello*衡量標準名稱*本身。</span><span class="sxs-lookup"><span data-stu-id="68edb-145">hello *metric name* itself.</span></span>
   * <span data-ttu-id="68edb-146">hello*時間彙總*hello 標準。</span><span class="sxs-lookup"><span data-stu-id="68edb-146">hello *time aggregation* of hello metric.</span></span> <span data-ttu-id="68edb-147">這是 hello 資料如何透過 hello 是結合*持續時間*。</span><span class="sxs-lookup"><span data-stu-id="68edb-147">This is how hello data is combine over hello *duration*.</span></span>
5. <span data-ttu-id="68edb-148">選擇您的度量之後，您會選擇 hello 度量和 hello 運算子 hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="68edb-148">After choosing your metric you choose hello threshold for hello metric, and hello operator.</span></span> <span data-ttu-id="68edb-149">例如，假設 [大於] 設為 [80%]。</span><span class="sxs-lookup"><span data-stu-id="68edb-149">For example, you could say **Greater than** **80%**.</span></span>
6. <span data-ttu-id="68edb-150">然後選擇 [hello 動作的 tootake。</span><span class="sxs-lookup"><span data-stu-id="68edb-150">Then choose hello action that you want tootake.</span></span> <span data-ttu-id="68edb-151">共有幾種不同的動作類型：</span><span class="sxs-lookup"><span data-stu-id="68edb-151">There are a couple different type of actions:</span></span>
   
   * <span data-ttu-id="68edb-152">增加或減少-這會加入或移除 hello**值**您定義的執行個體的數目</span><span class="sxs-lookup"><span data-stu-id="68edb-152">Increase or decrease by - this will add or remove hello **Value** number of instances you define</span></span>
   * <span data-ttu-id="68edb-153">增加或減少百分比-這會以百分比變更 hello 執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="68edb-153">Increase or decrease percent - this will change hello instance count by a percent.</span></span> <span data-ttu-id="68edb-154">例如，您可以將 25 放在 hello**值**] 欄位中，而且如果您目前有 8 個執行個體時，會加入 2。</span><span class="sxs-lookup"><span data-stu-id="68edb-154">For example, you could put 25 in hello **Value** field, and if you currently had 8 instances, 2 would be added.</span></span>
   * <span data-ttu-id="68edb-155">增加或減少太-這會將 hello 執行個體計數 toohello**值**您定義。</span><span class="sxs-lookup"><span data-stu-id="68edb-155">Increase or decrease too- this will set hello instance count toohello **Value** you define.</span></span>
7. <span data-ttu-id="68edb-156">最後，您可以選擇關閉-之後 hello 先前延展動作 tooscale 一次這項規則應等待多久 cool。</span><span class="sxs-lookup"><span data-stu-id="68edb-156">Finally, you can choose cool down - how long this rule should wait after hello previous scale action tooscale again.</span></span>
8. <span data-ttu-id="68edb-157">設定規則之後，請按 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="68edb-157">After configuring your rule hit **OK**.</span></span>
9. <span data-ttu-id="68edb-158">一旦您已設定的所有您想要的 hello 規則，可確定 toohit hello**儲存**命令。</span><span class="sxs-lookup"><span data-stu-id="68edb-158">Once you have configured all of hello rules you want, be sure toohit hello **Save** command.</span></span>

### <a name="scaling-with-multiple-steps"></a><span data-ttu-id="68edb-159">使用多個步驟進行調整</span><span class="sxs-lookup"><span data-stu-id="68edb-159">Scaling with multiple steps</span></span>
<span data-ttu-id="68edb-160">上述的 hello 範例是相當基本。</span><span class="sxs-lookup"><span data-stu-id="68edb-160">hello examples above are pretty basic.</span></span> <span data-ttu-id="68edb-161">不過，如果您想 toobe 更積極的調整規模 （上下），您甚至可以將加入多個小數位數的規則 hello 相同度量。</span><span class="sxs-lookup"><span data-stu-id="68edb-161">However, if you want toobe more agressive about scaling up (or down), you can even add multiple scale rules for hello same metric.</span></span> <span data-ttu-id="68edb-162">例如，您可以在 CPU 百分比上定義兩項調整規則：</span><span class="sxs-lookup"><span data-stu-id="68edb-162">For example, you can define two scale rules on CPU percentage:</span></span>

1. <span data-ttu-id="68edb-163">如果 CPU 百分比高於 60%，則相應增加 1 個執行個體</span><span class="sxs-lookup"><span data-stu-id="68edb-163">Scale out by 1 instance if CPU percentage is above 60%</span></span>
2. <span data-ttu-id="68edb-164">如果 CPU 百分比高於 85%，則相應增加 3 個執行個體</span><span class="sxs-lookup"><span data-stu-id="68edb-164">Scale out by 3 instances if CPU percentage is above 85%</span></span>

![Multiple scale rules](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

<span data-ttu-id="68edb-166">透過這項附加規則，如果您的負載在調整動作之前超過 85%，您將會增加兩個執行個體，而不是一個。</span><span class="sxs-lookup"><span data-stu-id="68edb-166">With this additional rule, if your load exceeds 85% before a scale action, you will get two additional instances instead of one.</span></span>

## <a name="scale-based-on-a-schedule"></a><span data-ttu-id="68edb-167">根據排程進行調整</span><span class="sxs-lookup"><span data-stu-id="68edb-167">Scale based on a schedule</span></span>
<span data-ttu-id="68edb-168">根據預設，當您建立調整規則時，它會一律套用。</span><span class="sxs-lookup"><span data-stu-id="68edb-168">By default, when you create a scale rule it will  always apply.</span></span> <span data-ttu-id="68edb-169">您可以看到，當您按一下 hello 設定檔的標頭：</span><span class="sxs-lookup"><span data-stu-id="68edb-169">You can see that when you click on hello profile header:</span></span>

![設定檔](./media/insights-how-to-scale/Insights_Profile.png)

<span data-ttu-id="68edb-171">不過，您可能想 toohave 更積極的縮放比例 hello 天或 hello 週期間比 hello 週末。</span><span class="sxs-lookup"><span data-stu-id="68edb-171">However, you may want toohave more agressive scaling during hello day, or hello week, than on hello weekend.</span></span> <span data-ttu-id="68edb-172">您甚至可以在下班時間完全關閉您的服務。</span><span class="sxs-lookup"><span data-stu-id="68edb-172">You could even shut down your service entirely off working hours.</span></span>

1. <span data-ttu-id="68edb-173">toodo，在 hello 設定檔，選取**循環**而不是**一定**選擇 hello 時間的 hello 設定檔 tooapply。</span><span class="sxs-lookup"><span data-stu-id="68edb-173">toodo this, on hello profile you have, select **recurrence** instead of **always,** and choose hello times that you want hello profile tooapply.</span></span>
2. <span data-ttu-id="68edb-174">例如，toohave hello 週 hello 期間套用的設定檔**天**下拉式清單中取消選取**星期六**和**星期日**。</span><span class="sxs-lookup"><span data-stu-id="68edb-174">For example, toohave a profile that applies during hello week, in hello **Days** dropdown uncheck **Saturday** and **Sunday**.</span></span>
3. <span data-ttu-id="68edb-175">toohave hello 白天，將 hello 期間套用的設定檔**開始時間**toohello 當日時間，您想要在 toostart。</span><span class="sxs-lookup"><span data-stu-id="68edb-175">toohave a profile that applies during hello daytime, set hello **Start time** toohello time of day that you want toostart at.</span></span>
   
    ![預設週期](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. <span data-ttu-id="68edb-177">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="68edb-177">Click **OK**.</span></span>
5. <span data-ttu-id="68edb-178">接下來，您將需要您在其他時候想 tooapply tooadd hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="68edb-178">Next, you will need tooadd hello profile that you want tooapply at other times.</span></span> <span data-ttu-id="68edb-179">按一下 hello**新增設定檔**資料列。</span><span class="sxs-lookup"><span data-stu-id="68edb-179">Click hello **Add Profile** row.</span></span>
    <span data-ttu-id="68edb-180">![下班](./media/insights-how-to-scale/Insights_ProfileOffWork.png)</span><span class="sxs-lookup"><span data-stu-id="68edb-180">![Off Work](./media/insights-how-to-scale/Insights_ProfileOffWork.png)</span></span>
6. <span data-ttu-id="68edb-181">為您的第二個新設定檔命名，例如，您可以把它叫做 **下班**。</span><span class="sxs-lookup"><span data-stu-id="68edb-181">Name your new, second, profile, for example you could call it **Off work**.</span></span>
7. <span data-ttu-id="68edb-182">然後選取**循環**一次，然後選擇您想要在這段期間的 hello 執行個體計數範圍。</span><span class="sxs-lookup"><span data-stu-id="68edb-182">Then select **recurrence** again, and choose hello instance count range you want during this time.</span></span>
8. <span data-ttu-id="68edb-183">以 hello 預設設定檔，選擇 [hello**天**您希望此設定檔 tooapply，和 hello**開始時間**hello 一天。</span><span class="sxs-lookup"><span data-stu-id="68edb-183">As with hello Default profile, choose hello **Days** you want this profile tooapply to, and hello **Start time** during hello day.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="68edb-184">自動調整規模會使用 hello 日光節約規則為準**時區**您選取。</span><span class="sxs-lookup"><span data-stu-id="68edb-184">Autoscale will use hello Daylight savings rules for whichever **Time zone** you select.</span></span> <span data-ttu-id="68edb-185">不過，在 hello UTC 位移會顯示 hello 基底的時區位移，不 hello 日光節約 UTC 位移的日光節約時間期間。</span><span class="sxs-lookup"><span data-stu-id="68edb-185">However, during Daylight savings time hello UTC offset will show hello base Time zone offset, not hello Daylight savings UTC offset.</span></span>
   > 
   > 
9. <span data-ttu-id="68edb-186">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="68edb-186">Click **OK**.</span></span>
10. <span data-ttu-id="68edb-187">現在，您將需要 tooadd 任何規則您想 tooapply 期間您的第二個設定檔。</span><span class="sxs-lookup"><span data-stu-id="68edb-187">Now, you will need tooadd whatever rules you want tooapply during your second profile.</span></span> <span data-ttu-id="68edb-188">按一下**加入規則**，然後您可以建構 hello 相同規則您擁有 hello 預設設定檔期間。</span><span class="sxs-lookup"><span data-stu-id="68edb-188">Click **Add Rule**, and then you could construct hello same rule you have during hello Default profile.</span></span>
    
    ![新增規則 toooff 工作](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. <span data-ttu-id="68edb-190">要確定 toocreate 這兩個向外的延展和規則中的小數位數，否則期間 hello 設定檔 hello 執行個體計數將只成長 （或減少）。</span><span class="sxs-lookup"><span data-stu-id="68edb-190">Be sure toocreate both a rule for scale out and scale in, or else during hello profile hello instance count will only grow (or decrease).</span></span>
12. <span data-ttu-id="68edb-191">最後，按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="68edb-191">Finally, click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68edb-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68edb-192">Next steps</span></span>
* <span data-ttu-id="68edb-193">[監視服務計量](insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。</span><span class="sxs-lookup"><span data-stu-id="68edb-193">[Monitor service metrics](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="68edb-194">[啟用監視和診斷](insights-how-to-use-diagnostics.md)toocollect 詳細高頻率度量，您的服務。</span><span class="sxs-lookup"><span data-stu-id="68edb-194">[Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="68edb-195">每當發生作業事件或計量超過臨界值時，[接收警示通知](insights-receive-alert-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="68edb-195">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="68edb-196">[監視應用程式效能](../application-insights/app-insights-azure-web-apps.md)如果您想 toounderstand 完全如何您的程式碼執行 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="68edb-196">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want toounderstand exactly how your code is performing in hello cloud.</span></span>
* <span data-ttu-id="68edb-197">[檢視事件和活動記錄檔](insights-debugging-with-events.md)toolearn 所有發生在您的服務中的項目。</span><span class="sxs-lookup"><span data-stu-id="68edb-197">[View events and activity log](insights-debugging-with-events.md) toolearn everything that has happened in your service.</span></span>
* <span data-ttu-id="68edb-198">[監視任何網頁的可用性和回應性](../application-insights/app-insights-monitor-web-app-availability.md) ，讓您可以找出您的頁面是否關閉。</span><span class="sxs-lookup"><span data-stu-id="68edb-198">[Monitor availability and responsiveness of any web page](../application-insights/app-insights-monitor-web-app-availability.md) with Application Insights so you can find out if your page is down.</span></span>

