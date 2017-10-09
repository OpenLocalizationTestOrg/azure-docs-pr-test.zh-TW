---
title: "aaaAutoscaling 與 App Service 環境 v1"
description: "自動調整和 App Service 環境"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a><span data-ttu-id="31295-103">自動調整和 App Service 環境 v1</span><span class="sxs-lookup"><span data-stu-id="31295-103">Autoscaling and App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="31295-104">這篇文章是關於 hello App Service 環境 v1。</span><span class="sxs-lookup"><span data-stu-id="31295-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="31295-105">沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。</span><span class="sxs-lookup"><span data-stu-id="31295-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="31295-106">有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。</span><span class="sxs-lookup"><span data-stu-id="31295-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

<span data-ttu-id="31295-107">Azure App Service 環境支援「自動調整」 。</span><span class="sxs-lookup"><span data-stu-id="31295-107">Azure App Service environments support *autoscaling*.</span></span> <span data-ttu-id="31295-108">您可以根據度量或排程自動調整個別的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="31295-108">You can autoscale individual worker pools based on metrics or schedule.</span></span>

![背景工作集區的自動調整選項。][intro]

<span data-ttu-id="31295-110">自動調整資源使用率藉由最佳化自動成長和壓縮 App Service 環境 toofit 預算和/或載入設定檔。</span><span class="sxs-lookup"><span data-stu-id="31295-110">Autoscaling optimizes your resource utilization by automatically growing and shrinking an App Service environment toofit your budget and or load profile.</span></span>

## <a name="configure-worker-pool-autoscale"></a><span data-ttu-id="31295-111">設定背景工作集區自動調整</span><span class="sxs-lookup"><span data-stu-id="31295-111">Configure worker pool autoscale</span></span>
<span data-ttu-id="31295-112">您可以存取 hello 自動調整規模功能從 hello**設定**hello 背景工作集區 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="31295-112">You can access hello autoscale functionality from hello **Settings** tab of hello worker pool.</span></span>

![Hello 背景工作集區的 [設定] 索引標籤。][settings-scale]

<span data-ttu-id="31295-114">從該處，hello 介面應該相當熟悉，因為它是相同的體驗，您會看到當您調整應用程式服務計劃的 hello。</span><span class="sxs-lookup"><span data-stu-id="31295-114">From there, hello interface should be fairly familiar since it is hello same experience that you see when you scale an App Service plan.</span></span> 

![手動調整設定。][scale-manual]

<span data-ttu-id="31295-116">您也可以設定自動調整設定檔。</span><span class="sxs-lookup"><span data-stu-id="31295-116">You can also configure an autoscale profile.</span></span>

![自動調整設定。][scale-profile]

<span data-ttu-id="31295-118">自動調整規模設定檔是在您的標尺上的有用 tooset 限制。</span><span class="sxs-lookup"><span data-stu-id="31295-118">Autoscale profiles are useful tooset limits on your scale.</span></span> <span data-ttu-id="31295-119">如此一來，您可以同時藉由設定下限調整值 (1) 獲得一致的效能體驗和藉由設定上限 (2) 獲得可預測的資本支出。</span><span class="sxs-lookup"><span data-stu-id="31295-119">This way, you can have a consistent performance experience by setting a lower bound scale value (1) and a predictable spend cap by setting an upper bound (2).</span></span>

![設定檔中的調整設定。][scale-profile2]

<span data-ttu-id="31295-121">定義設定檔之後，您可以加入自動調整規模規則 tooscale 向上或向下 hello hello hello hello 設定檔所定義的範圍內的背景工作集區中的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="31295-121">After you define a profile, you can add autoscale rules tooscale up or down hello number of instances in hello worker pool within hello bounds defined by hello profile.</span></span> <span data-ttu-id="31295-122">自動調整規則是以度量為基礎。</span><span class="sxs-lookup"><span data-stu-id="31295-122">Autoscale rules are based on metrics.</span></span>

![調整規則。][scale-rule]

 <span data-ttu-id="31295-124">任何背景工作集區或前端的度量可以使用的 toodefine 自動調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="31295-124">Any worker pool or front-end metrics can be used toodefine autoscale rules.</span></span> <span data-ttu-id="31295-125">這些度量資訊是的 hello 的相同度量資訊，您可以在 hello 資源刀鋒視窗圖形中監視或設定警示。</span><span class="sxs-lookup"><span data-stu-id="31295-125">These metrics are hello same metrics you can monitor in hello resource blade graphs or set alerts for.</span></span>

## <a name="autoscale-example"></a><span data-ttu-id="31295-126">自動調整範例</span><span class="sxs-lookup"><span data-stu-id="31295-126">Autoscale example</span></span>
<span data-ttu-id="31295-127">App Service 環境的自動調整可使用逐步解說一個案例來加以說明。</span><span class="sxs-lookup"><span data-stu-id="31295-127">Autoscale of an App Service environment can best be illustrated by walking through a scenario.</span></span>

<span data-ttu-id="31295-128">這篇文章會說明所有 hello 需要考量，當您設定自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="31295-128">This article explains all hello necessary considerations when you set up autoscale.</span></span> <span data-ttu-id="31295-129">hello 文章會引導您進入互動播放時自動調整的因素在 App Service 環境中裝載的應用程式服務環境的 hello。</span><span class="sxs-lookup"><span data-stu-id="31295-129">hello article walks you through hello interactions that come into play when you factor in autoscaling App Service environments that are hosted in App Service Environment.</span></span>

### <a name="scenario-introduction"></a><span data-ttu-id="31295-130">案例簡介</span><span class="sxs-lookup"><span data-stu-id="31295-130">Scenario introduction</span></span>
<span data-ttu-id="31295-131">Frank 具有企業已移轉的一部分，他會管理 tooan App Service 環境的 hello 工作負載的 sysadmin 權限。</span><span class="sxs-lookup"><span data-stu-id="31295-131">Frank is a sysadmin for an enterprise who has migrated a portion of hello workloads that he manages tooan App Service environment.</span></span>

<span data-ttu-id="31295-132">hello App Service 環境設定 toomanual 小數位數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31295-132">hello App Service environment is configured toomanual scale as follows:</span></span>

* <span data-ttu-id="31295-133">**前端：** 3</span><span class="sxs-lookup"><span data-stu-id="31295-133">**Front ends:** 3</span></span>
* <span data-ttu-id="31295-134">**背景工作集區 1**：10</span><span class="sxs-lookup"><span data-stu-id="31295-134">**Worker pool 1**: 10</span></span>
* <span data-ttu-id="31295-135">**背景工作集區 2**：5</span><span class="sxs-lookup"><span data-stu-id="31295-135">**Worker pool 2**: 5</span></span>
* <span data-ttu-id="31295-136">**背景工作集區 3**：5</span><span class="sxs-lookup"><span data-stu-id="31295-136">**Worker pool 3**: 5</span></span>

<span data-ttu-id="31295-137">背景工作集區 1 是用於生產工作負載，而背景工作集區 2 和背景工作集區 3 用於品質保證 (QA) 及開發工作負載。</span><span class="sxs-lookup"><span data-stu-id="31295-137">Worker pool 1 is used for production workloads, while worker pool 2 and worker pool 3 are used for quality assurance (QA) and development workloads.</span></span>

<span data-ttu-id="31295-138">hello 應用程式服務計劃 QA 和開發人員設定 toomanual 小數位數。</span><span class="sxs-lookup"><span data-stu-id="31295-138">hello App Service plans for QA and dev are configured toomanual scale.</span></span> <span data-ttu-id="31295-139">hello 生產應用程式服務方案是設定與變化 tooautoscale toodeal 負載和流量。</span><span class="sxs-lookup"><span data-stu-id="31295-139">hello production App Service plan is set tooautoscale toodeal with variations in load and traffic.</span></span>

<span data-ttu-id="31295-140">Frank 是很熟悉 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31295-140">Frank is very familiar with hello application.</span></span> <span data-ttu-id="31295-141">他知道 hello 尖峰負載是上午 9:00 和下午 6:00 之間因為這是在 hello office 時，員工使用的特定業務 (LOB) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31295-141">He knows that hello peak hours for load are between 9:00 AM and 6:00 PM because this is a line-of-business (LOB) application that employees use while they are in hello office.</span></span> <span data-ttu-id="31295-142">之後當使用者下班時，使用量便會下降。</span><span class="sxs-lookup"><span data-stu-id="31295-142">Usage drops after that when users are done for that day.</span></span> <span data-ttu-id="31295-143">非尖峰時間仍有某些負載因為使用者可以從遠端存取 hello 應用程式，使用其行動裝置或家用電腦。</span><span class="sxs-lookup"><span data-stu-id="31295-143">Outside peak hours, there is still some load because users can access hello app remotely by using their mobile devices or home PCs.</span></span> <span data-ttu-id="31295-144">hello 實際執行應用程式服務方案已設定 tooautoscale 根據 CPU 使用量，以 hello 下列規則：</span><span class="sxs-lookup"><span data-stu-id="31295-144">hello production App Service plan is already configured tooautoscale based on CPU usage with hello following rules:</span></span>

![LOB 應用程式的特定設定。][asp-scale]

| <span data-ttu-id="31295-146">**自動調整設定檔 - 工作日 - App Service 方案**</span><span class="sxs-lookup"><span data-stu-id="31295-146">**Autoscale profile – Weekdays – App Service plan**</span></span> | <span data-ttu-id="31295-147">**自動調整設定檔 - 週末 - App Service 方案**</span><span class="sxs-lookup"><span data-stu-id="31295-147">**Autoscale profile – Weekends – App Service plan**</span></span> |
| --- | --- |
| <span data-ttu-id="31295-148">**名稱：** 工作日設定檔</span><span class="sxs-lookup"><span data-stu-id="31295-148">**Name:** Weekday profile</span></span> |<span data-ttu-id="31295-149">**名稱：** 週末設定檔</span><span class="sxs-lookup"><span data-stu-id="31295-149">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="31295-150">**調整規模：** 排程和效能規則</span><span class="sxs-lookup"><span data-stu-id="31295-150">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="31295-151">**調整規模：** 排程和效能規則</span><span class="sxs-lookup"><span data-stu-id="31295-151">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="31295-152">**設定檔：** 工作日</span><span class="sxs-lookup"><span data-stu-id="31295-152">**Profile:** Weekdays</span></span> |<span data-ttu-id="31295-153">**設定檔：** 週末</span><span class="sxs-lookup"><span data-stu-id="31295-153">**Profile:** Weekend</span></span> |
| <span data-ttu-id="31295-154">**類型：** 循環</span><span class="sxs-lookup"><span data-stu-id="31295-154">**Type:** Recurrence</span></span> |<span data-ttu-id="31295-155">**類型：** 循環</span><span class="sxs-lookup"><span data-stu-id="31295-155">**Type:** Recurrence</span></span> |
| <span data-ttu-id="31295-156">**以範圍為目標：** 5 too20 執行個體</span><span class="sxs-lookup"><span data-stu-id="31295-156">**Target range:** 5 too20 instances</span></span> |<span data-ttu-id="31295-157">**以範圍為目標：** 3 too10 執行個體</span><span class="sxs-lookup"><span data-stu-id="31295-157">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="31295-158">**星期幾：** 星期一、星期二、星期三、星期四、星期五</span><span class="sxs-lookup"><span data-stu-id="31295-158">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="31295-159">**星期幾：** 星期六、星期日</span><span class="sxs-lookup"><span data-stu-id="31295-159">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="31295-160">**開始時間︰** 上午 9:00</span><span class="sxs-lookup"><span data-stu-id="31295-160">**Start time:** 9:00 AM</span></span> |<span data-ttu-id="31295-161">**開始時間︰** 上午 9:00</span><span class="sxs-lookup"><span data-stu-id="31295-161">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="31295-162">**時區：** UTC-08</span><span class="sxs-lookup"><span data-stu-id="31295-162">**Time zone:** UTC-08</span></span> |<span data-ttu-id="31295-163">**時區：** UTC-08</span><span class="sxs-lookup"><span data-stu-id="31295-163">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="31295-164">**自動調整規則 (相應增加)**</span><span class="sxs-lookup"><span data-stu-id="31295-164">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="31295-165">**自動調整規則 (相應增加)**</span><span class="sxs-lookup"><span data-stu-id="31295-165">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="31295-166">**資源：** 生產環境 (App Service 環境)</span><span class="sxs-lookup"><span data-stu-id="31295-166">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="31295-167">**資源：** 生產環境 (App Service 環境)</span><span class="sxs-lookup"><span data-stu-id="31295-167">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="31295-168">**度量：** CPU %</span><span class="sxs-lookup"><span data-stu-id="31295-168">**Metric:** CPU %</span></span> |<span data-ttu-id="31295-169">**度量：** CPU %</span><span class="sxs-lookup"><span data-stu-id="31295-169">**Metric:** CPU %</span></span> |
| <span data-ttu-id="31295-170">**作業：** 大於 60%</span><span class="sxs-lookup"><span data-stu-id="31295-170">**Operation:** Greater than 60%</span></span> |<span data-ttu-id="31295-171">**作業：** 大於 80%</span><span class="sxs-lookup"><span data-stu-id="31295-171">**Operation:** Greater than 80%</span></span> |
| <span data-ttu-id="31295-172">**持續時間：** 5 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-172">**Duration:** 5 Minutes</span></span> |<span data-ttu-id="31295-173">**持續時間：** 10 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-173">**Duration:** 10 Minutes</span></span> |
| <span data-ttu-id="31295-174">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-174">**Time aggregation:** Average</span></span> |<span data-ttu-id="31295-175">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-175">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="31295-176">**動作：** 計數增加 2</span><span class="sxs-lookup"><span data-stu-id="31295-176">**Action:** Increase count by 2</span></span> |<span data-ttu-id="31295-177">**動作：** 計數增加 1</span><span class="sxs-lookup"><span data-stu-id="31295-177">**Action:** Increase count by 1</span></span> |
| <span data-ttu-id="31295-178">**冷卻時間 (分鐘)：** 15</span><span class="sxs-lookup"><span data-stu-id="31295-178">**Cool down (minutes):** 15</span></span> |<span data-ttu-id="31295-179">**冷卻時間 (分鐘)：** 20</span><span class="sxs-lookup"><span data-stu-id="31295-179">**Cool down (minutes):** 20</span></span> |
|  | |
| <span data-ttu-id="31295-180">**自動調整規則 (相應減少)**</span><span class="sxs-lookup"><span data-stu-id="31295-180">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="31295-181">**自動調整規則 (相應減少)**</span><span class="sxs-lookup"><span data-stu-id="31295-181">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="31295-182">**資源：** 生產環境 (App Service 環境)</span><span class="sxs-lookup"><span data-stu-id="31295-182">**Resource:** Production (App Service Environment)</span></span> |<span data-ttu-id="31295-183">**資源：** 生產環境 (App Service 環境)</span><span class="sxs-lookup"><span data-stu-id="31295-183">**Resource:** Production (App Service Environment)</span></span> |
| <span data-ttu-id="31295-184">**度量：** CPU %</span><span class="sxs-lookup"><span data-stu-id="31295-184">**Metric:** CPU %</span></span> |<span data-ttu-id="31295-185">**度量：** CPU %</span><span class="sxs-lookup"><span data-stu-id="31295-185">**Metric:** CPU %</span></span> |
| <span data-ttu-id="31295-186">**作業：** 少於 30 %</span><span class="sxs-lookup"><span data-stu-id="31295-186">**Operation:** Less than 30%</span></span> |<span data-ttu-id="31295-187">**作業：** 少於 20 %</span><span class="sxs-lookup"><span data-stu-id="31295-187">**Operation:** Less than 20%</span></span> |
| <span data-ttu-id="31295-188">**持續時間：** 10 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-188">**Duration:** 10 minutes</span></span> |<span data-ttu-id="31295-189">**持續時間：** 15 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-189">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="31295-190">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-190">**Time aggregation:** Average</span></span> |<span data-ttu-id="31295-191">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-191">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="31295-192">**動作：** 計數減少 1</span><span class="sxs-lookup"><span data-stu-id="31295-192">**Action:** Decrease count by 1</span></span> |<span data-ttu-id="31295-193">**動作：** 計數減少 1</span><span class="sxs-lookup"><span data-stu-id="31295-193">**Action:** Decrease count by 1</span></span> |
| <span data-ttu-id="31295-194">**冷卻時間 (分鐘)：** 20</span><span class="sxs-lookup"><span data-stu-id="31295-194">**Cool down (minutes):** 20</span></span> |<span data-ttu-id="31295-195">**冷卻時間 (分鐘)：** 10</span><span class="sxs-lookup"><span data-stu-id="31295-195">**Cool down (minutes):** 10</span></span> |

### <a name="app-service-plan-inflation-rate"></a><span data-ttu-id="31295-196">App Service 方案擴大率</span><span class="sxs-lookup"><span data-stu-id="31295-196">App Service plan inflation rate</span></span>
<span data-ttu-id="31295-197">設定的 tooautoscale 應用程式服務計劃進行每小時的最大速率。</span><span class="sxs-lookup"><span data-stu-id="31295-197">App Service plans that are configured tooautoscale do so at a maximum rate per hour.</span></span> <span data-ttu-id="31295-198">此速率可以是根據計算 hello hello 自動調整規模規則上所提供的值。</span><span class="sxs-lookup"><span data-stu-id="31295-198">This rate can be calculated based on hello values provided on hello autoscale rule.</span></span>

<span data-ttu-id="31295-199">了解及計算 hello*應用程式服務計劃變大速率*很重要的 App Service 環境的自動調整規模，因為小數位數變更 tooa 背景工作集區不是瞬間完成。</span><span class="sxs-lookup"><span data-stu-id="31295-199">Understanding and calculating hello *App Service plan inflation rate* is important for App Service environment autoscale because scale changes tooa worker pool are not instantaneous.</span></span>

<span data-ttu-id="31295-200">hello 應用程式服務計劃變大率的計算方式如下：</span><span class="sxs-lookup"><span data-stu-id="31295-200">hello App Service plan inflation rate is calculated as follows:</span></span>

![App Service 方案擴大率計算。][ASP-Inflation]

<span data-ttu-id="31295-202">根據 hello 自動調整規模 – hello 週間日設定檔的 hello 生產應用程式服務方案的向外延展規則：</span><span class="sxs-lookup"><span data-stu-id="31295-202">Based on hello Autoscale – Scale Up rule for hello Weekday profile of hello production App Service plan:</span></span>

![根據「自動調整 - 相應增加」規則的工作日 App Service 方案擴大率。][Equation1]

<span data-ttu-id="31295-204">在 hello 案例中的 hello 自動調整規模 – hello 週末設定檔的 hello 生產應用程式服務方案的向外延展規則 hello 公式會解析成：</span><span class="sxs-lookup"><span data-stu-id="31295-204">In hello case of hello Autoscale – Scale Up rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>

![根據「自動調整 - 相應增加」規則的週末 App Service 方案擴大率。][Equation2]

<span data-ttu-id="31295-206">此值也可以針對相應減少作業計算。</span><span class="sxs-lookup"><span data-stu-id="31295-206">This value can also be calculated for scale-down operations.</span></span>

<span data-ttu-id="31295-207">根據 hello 自動調整規模 – hello 週間日設定檔的 hello 生產應用程式服務方案的向下規則這看起來如下：</span><span class="sxs-lookup"><span data-stu-id="31295-207">Based on hello Autoscale – Scale Down rule for hello Weekday profile of hello production App Service plan, this would look as follows:</span></span>

![根據「自動調整 - 相應減少」規則的工作日 App Service 方案擴大率。][Equation3]

<span data-ttu-id="31295-209">在 hello 案例中的 hello 自動調整規模 – hello 週末設定檔的 hello 生產應用程式服務方案的向下規則 hello 公式會解析成：</span><span class="sxs-lookup"><span data-stu-id="31295-209">In hello case of hello Autoscale – Scale Down rule for hello Weekend profile of hello production App Service plan, hello formula would resolve to:</span></span>  

![根據「自動調整 - 相應減少」規則的週末 App Service 方案擴大率。][Equation4]

<span data-ttu-id="31295-211">hello 生產應用程式服務方案所能成長的八個執行個體/小時 hello 週的最大速率和四個執行個體/小時 hello 週末期間。</span><span class="sxs-lookup"><span data-stu-id="31295-211">hello production App Service plan can grow at a maximum rate of eight instances/hour during hello week and four instances/hour during hello weekend.</span></span> <span data-ttu-id="31295-212">它可以釋放執行個體的四個執行個體/小時 hello 週的最大速率和六個執行個體/小時在週末期間。</span><span class="sxs-lookup"><span data-stu-id="31295-212">It can release instances at a maximum rate of four instances/hour during hello week and six instances/hour during weekends.</span></span>

<span data-ttu-id="31295-213">如果多個應用程式服務計劃裝載於背景工作集區，您必須 toocalculate hello*總擴大速率*所有 hello 應用程式服務計劃正在進行的 hello 擴大速率 hello 總和裝載該背景工作集區中。</span><span class="sxs-lookup"><span data-stu-id="31295-213">If multiple App Service plans are being hosted in a worker pool, you have toocalculate hello *total inflation rate* as hello sum of hello inflation rate for all hello App Service plans that are being hosting in that worker pool.</span></span>

![裝載於背景工作集區中的多個 App Service 方案的總擴大率計算。][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a><span data-ttu-id="31295-215">使用 hello 應用程式服務計劃變大速率 toodefine 背景工作集區自動調整規模規則</span><span class="sxs-lookup"><span data-stu-id="31295-215">Use hello App Service plan inflation rate toodefine worker pool autoscale rules</span></span>
<span data-ttu-id="31295-216">背景工作集區設定的 tooautoscale 應用程式服務計劃要配置的緩衝區容量該主機。</span><span class="sxs-lookup"><span data-stu-id="31295-216">Worker pools that host App Service plans that are configured tooautoscale need to be allocated a buffer of capacity.</span></span> <span data-ttu-id="31295-217">hello 緩衝區可 hello 自動調整規模作業 toogrow，而且視壓縮應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="31295-217">hello buffer allows for hello autoscale operations toogrow and shrink the App Service plan as needed.</span></span> <span data-ttu-id="31295-218">hello 最小緩衝區是 hello 計算總應用程式服務計劃變大率。</span><span class="sxs-lookup"><span data-stu-id="31295-218">hello minimum buffer would be hello calculated Total App Service Plan Inflation Rate.</span></span>

<span data-ttu-id="31295-219">由於 App Service 環境調整規模作業會花一些時間 tooapply，進一步指定縮放作業正在進行時可能發生的變更應該考量的任何變更。</span><span class="sxs-lookup"><span data-stu-id="31295-219">Because App Service environment scale operations take some time tooapply, any change should account for further demand changes that could happen while a scale operation is in progress.</span></span> <span data-ttu-id="31295-220">tooaccommodate 這樣的延遲，我們建議您使用 hello 計算總應用程式服務計劃變大速率為 hello 加入每個自動調整規模作業的執行個體數目下限。</span><span class="sxs-lookup"><span data-stu-id="31295-220">tooaccommodate this latency, we recommend that you use hello calculated Total App Service Plan Inflation Rate as hello minimum number of instances that are added for each autoscale operation.</span></span>

<span data-ttu-id="31295-221">Frank 可使用這項資訊定義 hello 下列自動調整規模設定檔和規則：</span><span class="sxs-lookup"><span data-stu-id="31295-221">With this information, Frank can define hello following autoscale profile and rules:</span></span>

![LOB 範例的自動調整設定檔規則。][Worker-Pool-Scale]

| <span data-ttu-id="31295-223">**自動調整設定檔 - 工作日**</span><span class="sxs-lookup"><span data-stu-id="31295-223">**Autoscale profile – Weekdays**</span></span> | <span data-ttu-id="31295-224">**自動調整設定檔 - 週末**</span><span class="sxs-lookup"><span data-stu-id="31295-224">**Autoscale profile – Weekends**</span></span> |
| --- | --- |
| <span data-ttu-id="31295-225">**名稱：** 工作日設定檔</span><span class="sxs-lookup"><span data-stu-id="31295-225">**Name:** Weekday profile</span></span> |<span data-ttu-id="31295-226">**名稱：** 週末設定檔</span><span class="sxs-lookup"><span data-stu-id="31295-226">**Name:** Weekend profile</span></span> |
| <span data-ttu-id="31295-227">**調整規模：** 排程和效能規則</span><span class="sxs-lookup"><span data-stu-id="31295-227">**Scale by:** Schedule and performance rules</span></span> |<span data-ttu-id="31295-228">**調整規模：** 排程和效能規則</span><span class="sxs-lookup"><span data-stu-id="31295-228">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="31295-229">**設定檔：** 工作日</span><span class="sxs-lookup"><span data-stu-id="31295-229">**Profile:** Weekdays</span></span> |<span data-ttu-id="31295-230">**設定檔：** 週末</span><span class="sxs-lookup"><span data-stu-id="31295-230">**Profile:** Weekend</span></span> |
| <span data-ttu-id="31295-231">**類型：** 循環</span><span class="sxs-lookup"><span data-stu-id="31295-231">**Type:** Recurrence</span></span> |<span data-ttu-id="31295-232">**類型：** 循環</span><span class="sxs-lookup"><span data-stu-id="31295-232">**Type:** Recurrence</span></span> |
| <span data-ttu-id="31295-233">**以範圍為目標：** 13 too25 執行個體</span><span class="sxs-lookup"><span data-stu-id="31295-233">**Target range:** 13 too25 instances</span></span> |<span data-ttu-id="31295-234">**以範圍為目標：** 6 too15 個執行個體</span><span class="sxs-lookup"><span data-stu-id="31295-234">**Target range:** 6 too15 instances</span></span> |
| <span data-ttu-id="31295-235">**星期幾：** 星期一、星期二、星期三、星期四、星期五</span><span class="sxs-lookup"><span data-stu-id="31295-235">**Days:** Monday, Tuesday, Wednesday, Thursday, Friday</span></span> |<span data-ttu-id="31295-236">**星期幾：** 星期六、星期日</span><span class="sxs-lookup"><span data-stu-id="31295-236">**Days:** Saturday, Sunday</span></span> |
| <span data-ttu-id="31295-237">**開始時間︰** 上午 7:00</span><span class="sxs-lookup"><span data-stu-id="31295-237">**Start time:** 7:00 AM</span></span> |<span data-ttu-id="31295-238">**開始時間︰** 上午 9:00</span><span class="sxs-lookup"><span data-stu-id="31295-238">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="31295-239">**時區：** UTC-08</span><span class="sxs-lookup"><span data-stu-id="31295-239">**Time zone:** UTC-08</span></span> |<span data-ttu-id="31295-240">**時區：** UTC-08</span><span class="sxs-lookup"><span data-stu-id="31295-240">**Time zone:** UTC-08</span></span> |
|  | |
| <span data-ttu-id="31295-241">**自動調整規則 (相應增加)**</span><span class="sxs-lookup"><span data-stu-id="31295-241">**Autoscale rule (Scale Up)**</span></span> |<span data-ttu-id="31295-242">**自動調整規則 (相應增加)**</span><span class="sxs-lookup"><span data-stu-id="31295-242">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="31295-243">**資源：** 背景工作集區 1</span><span class="sxs-lookup"><span data-stu-id="31295-243">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="31295-244">**資源：** 背景工作集區 1</span><span class="sxs-lookup"><span data-stu-id="31295-244">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="31295-245">**度量：** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="31295-245">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="31295-246">**度量：** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="31295-246">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="31295-247">**作業：** 少於 8</span><span class="sxs-lookup"><span data-stu-id="31295-247">**Operation:** Less than 8</span></span> |<span data-ttu-id="31295-248">**作業：** 少於 3</span><span class="sxs-lookup"><span data-stu-id="31295-248">**Operation:** Less than 3</span></span> |
| <span data-ttu-id="31295-249">**持續時間：** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-249">**Duration:** 20 minutes</span></span> |<span data-ttu-id="31295-250">**持續時間：** 30 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-250">**Duration:** 30 minutes</span></span> |
| <span data-ttu-id="31295-251">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-251">**Time aggregation:** Average</span></span> |<span data-ttu-id="31295-252">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-252">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="31295-253">**動作：** 計數增加 8</span><span class="sxs-lookup"><span data-stu-id="31295-253">**Action:** Increase count by 8</span></span> |<span data-ttu-id="31295-254">**動作：** 計數增加 3</span><span class="sxs-lookup"><span data-stu-id="31295-254">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="31295-255">**冷卻時間 (分鐘)：** 180</span><span class="sxs-lookup"><span data-stu-id="31295-255">**Cool down (minutes):** 180</span></span> |<span data-ttu-id="31295-256">**冷卻時間 (分鐘)：** 180</span><span class="sxs-lookup"><span data-stu-id="31295-256">**Cool down (minutes):** 180</span></span> |
|  | |
| <span data-ttu-id="31295-257">**自動調整規則 (相應減少)**</span><span class="sxs-lookup"><span data-stu-id="31295-257">**Autoscale rule (Scale Down)**</span></span> |<span data-ttu-id="31295-258">**自動調整規則 (相應減少)**</span><span class="sxs-lookup"><span data-stu-id="31295-258">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="31295-259">**資源：** 背景工作集區 1</span><span class="sxs-lookup"><span data-stu-id="31295-259">**Resource:** Worker pool 1</span></span> |<span data-ttu-id="31295-260">**資源：** 背景工作集區 1</span><span class="sxs-lookup"><span data-stu-id="31295-260">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="31295-261">**度量：** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="31295-261">**Metric:** WorkersAvailable</span></span> |<span data-ttu-id="31295-262">**度量：** WorkersAvailable</span><span class="sxs-lookup"><span data-stu-id="31295-262">**Metric:** WorkersAvailable</span></span> |
| <span data-ttu-id="31295-263">**作業：** 大於 8</span><span class="sxs-lookup"><span data-stu-id="31295-263">**Operation:** Greater than 8</span></span> |<span data-ttu-id="31295-264">**作業：** 大於 3</span><span class="sxs-lookup"><span data-stu-id="31295-264">**Operation:** Greater than 3</span></span> |
| <span data-ttu-id="31295-265">**持續時間：** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-265">**Duration:** 20 minutes</span></span> |<span data-ttu-id="31295-266">**持續時間：** 15 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-266">**Duration:** 15 minutes</span></span> |
| <span data-ttu-id="31295-267">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-267">**Time aggregation:** Average</span></span> |<span data-ttu-id="31295-268">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-268">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="31295-269">**動作：** 計數減少 2</span><span class="sxs-lookup"><span data-stu-id="31295-269">**Action:** Decrease count by 2</span></span> |<span data-ttu-id="31295-270">**動作：** 計數減少 3</span><span class="sxs-lookup"><span data-stu-id="31295-270">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="31295-271">**冷卻時間 (分鐘)：** 120</span><span class="sxs-lookup"><span data-stu-id="31295-271">**Cool down (minutes):** 120</span></span> |<span data-ttu-id="31295-272">**冷卻時間 (分鐘)：** 120</span><span class="sxs-lookup"><span data-stu-id="31295-272">**Cool down (minutes):** 120</span></span> |

<span data-ttu-id="31295-273">hello hello 設定檔中定義的目標範圍的計算方式 hello hello 應用程式服務方案的設定檔 + 緩衝區中定義的最小執行個體。</span><span class="sxs-lookup"><span data-stu-id="31295-273">hello Target range defined in hello profile is calculated by hello minimum instances defined in the profile for hello App Service plan + buffer.</span></span>

<span data-ttu-id="31295-274">hello 最大範圍是裝載於 hello 背景工作集區的所有應用程式服務方案的 hello 最大範圍的 hello 總和。</span><span class="sxs-lookup"><span data-stu-id="31295-274">hello Maximum range would be hello sum of all hello maximum ranges for all App Service plans hosted in hello worker pool.</span></span>

<span data-ttu-id="31295-275">hello hello 調整規則的增加計數應該組 tooat X 應用程式服務計劃變大速率，標尺的最少 1 組成。</span><span class="sxs-lookup"><span data-stu-id="31295-275">hello Increase count for hello scale up rules should be set tooat least 1X the App Service Plan Inflation Rate for scale up.</span></span>

<span data-ttu-id="31295-276">減少計數可能都已調整的 toosomething 之間 1/2 X 或 1 X hello 標尺的應用程式服務計劃變大速率，向下。</span><span class="sxs-lookup"><span data-stu-id="31295-276">Decrease count can be adjusted toosomething between 1/2X or 1X hello App Service Plan Inflation Rate for scale down.</span></span>

### <a name="autoscale-for-front-end-pool"></a><span data-ttu-id="31295-277">前端集區的自動調整</span><span class="sxs-lookup"><span data-stu-id="31295-277">Autoscale for front-end pool</span></span>
<span data-ttu-id="31295-278">前端自動調整規則比背景工作集區規則簡單。</span><span class="sxs-lookup"><span data-stu-id="31295-278">Rules for front-end autoscale are simpler than for worker pools.</span></span> <span data-ttu-id="31295-279">您主要應該</span><span class="sxs-lookup"><span data-stu-id="31295-279">Primarily, you should</span></span>  
<span data-ttu-id="31295-280">請確定 hello 測量與 hello cooldown 計時器的持續時間，考慮，App Service 方案上的調整規模作業不是瞬間完成。</span><span class="sxs-lookup"><span data-stu-id="31295-280">make sure that duration of hello measurement and hello cooldown timers consider that scale operations on an App Service plan are not instantaneous.</span></span>

<span data-ttu-id="31295-281">此案例中，Frank 知道該 hello 錯誤速率增加之後前端達到 80%的 CPU 使用率，並設定 hello 自動調整規模規則 tooincrease 執行個體，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31295-281">For this scenario, Frank knows that hello error rate increases after front ends reach 80% CPU utilization and sets hello autoscale rule tooincrease instances as follows:</span></span>

![前端集區的自動調整設定。][Front-End-Scale]

| <span data-ttu-id="31295-283">**自動調整設定檔 - 前端**</span><span class="sxs-lookup"><span data-stu-id="31295-283">**Autoscale profile – Front ends**</span></span> |
| --- |
| <span data-ttu-id="31295-284">**名稱：** 自動調整 - 前端</span><span class="sxs-lookup"><span data-stu-id="31295-284">**Name:** Autoscale – Front ends</span></span> |
| <span data-ttu-id="31295-285">**調整規模：** 排程和效能規則</span><span class="sxs-lookup"><span data-stu-id="31295-285">**Scale by:** Schedule and performance rules</span></span> |
| <span data-ttu-id="31295-286">**設定檔：** 每日</span><span class="sxs-lookup"><span data-stu-id="31295-286">**Profile:** Everyday</span></span> |
| <span data-ttu-id="31295-287">**類型：** 循環</span><span class="sxs-lookup"><span data-stu-id="31295-287">**Type:** Recurrence</span></span> |
| <span data-ttu-id="31295-288">**以範圍為目標：** 3 too10 執行個體</span><span class="sxs-lookup"><span data-stu-id="31295-288">**Target range:** 3 too10 instances</span></span> |
| <span data-ttu-id="31295-289">**星期幾：** 每日</span><span class="sxs-lookup"><span data-stu-id="31295-289">**Days:** Everyday</span></span> |
| <span data-ttu-id="31295-290">**開始時間︰** 上午 9:00</span><span class="sxs-lookup"><span data-stu-id="31295-290">**Start time:** 9:00 AM</span></span> |
| <span data-ttu-id="31295-291">**時區：** UTC-08</span><span class="sxs-lookup"><span data-stu-id="31295-291">**Time zone:** UTC-08</span></span> |
|  |
| <span data-ttu-id="31295-292">**自動調整規則 (相應增加)**</span><span class="sxs-lookup"><span data-stu-id="31295-292">**Autoscale rule (Scale Up)**</span></span> |
| <span data-ttu-id="31295-293">**資源：** 前端集區</span><span class="sxs-lookup"><span data-stu-id="31295-293">**Resource:** Front-end pool</span></span> |
| <span data-ttu-id="31295-294">**度量：** CPU %</span><span class="sxs-lookup"><span data-stu-id="31295-294">**Metric:** CPU %</span></span> |
| <span data-ttu-id="31295-295">**作業：** 大於 60%</span><span class="sxs-lookup"><span data-stu-id="31295-295">**Operation:** Greater than 60%</span></span> |
| <span data-ttu-id="31295-296">**持續時間：** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-296">**Duration:** 20 minutes</span></span> |
| <span data-ttu-id="31295-297">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-297">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="31295-298">**動作：** 計數增加 3</span><span class="sxs-lookup"><span data-stu-id="31295-298">**Action:** Increase count by 3</span></span> |
| <span data-ttu-id="31295-299">**冷卻時間 (分鐘)：** 120</span><span class="sxs-lookup"><span data-stu-id="31295-299">**Cool down (minutes):** 120</span></span> |
|  |
| <span data-ttu-id="31295-300">**自動調整規則 (相應減少)**</span><span class="sxs-lookup"><span data-stu-id="31295-300">**Autoscale rule (Scale Down)**</span></span> |
| <span data-ttu-id="31295-301">**資源：** 背景工作集區 1</span><span class="sxs-lookup"><span data-stu-id="31295-301">**Resource:** Worker pool 1</span></span> |
| <span data-ttu-id="31295-302">**度量：** CPU %</span><span class="sxs-lookup"><span data-stu-id="31295-302">**Metric:** CPU %</span></span> |
| <span data-ttu-id="31295-303">**作業：** 少於 30 %</span><span class="sxs-lookup"><span data-stu-id="31295-303">**Operation:** Less than 30%</span></span> |
| <span data-ttu-id="31295-304">**持續時間：** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="31295-304">**Duration:** 20 Minutes</span></span> |
| <span data-ttu-id="31295-305">**時間彙總：** 平均</span><span class="sxs-lookup"><span data-stu-id="31295-305">**Time aggregation:** Average</span></span> |
| <span data-ttu-id="31295-306">**動作：** 計數減少 3</span><span class="sxs-lookup"><span data-stu-id="31295-306">**Action:** Decrease count by 3</span></span> |
| <span data-ttu-id="31295-307">**冷卻時間 (分鐘)：** 120</span><span class="sxs-lookup"><span data-stu-id="31295-307">**Cool down (minutes):** 120</span></span> |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
