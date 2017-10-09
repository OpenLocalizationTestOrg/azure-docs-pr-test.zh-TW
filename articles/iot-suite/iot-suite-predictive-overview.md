---
title: "aaaPredictive 維護預先設定的解決方案 |Microsoft 文件"
description: "Hello Azure IoT 套件預測性維護描述預先設定的解決方案。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="918ee-103">預先設定的預測性維護解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="918ee-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="918ee-104">hello*預測性維護*[預先設定的解決方案][ lnk_preconfigured_solutions]是其中一個 hello [Microsoft Azure IoT 套件][ lnk_iot_suite]預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="918ee-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="918ee-105">此解決方案應用了 [Azure Machine Learning][lnk-machine-learning]，整合了即時裝置遙測集合與預測模型。</span><span class="sxs-lookup"><span data-stu-id="918ee-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="918ee-106">與 Azure IoT 套件，您可以快速並輕鬆地連接 tooand 監視器資產，並分析即時儀表板和視覺效果中的遙測。</span><span class="sxs-lookup"><span data-stu-id="918ee-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="918ee-107">在 hello 預測性維護方案中，hello 儀表板和視覺效果提供您新的資訊，磁碟機效率以及增強的營收的資料流。</span><span class="sxs-lookup"><span data-stu-id="918ee-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="918ee-108">hello 案例</span><span class="sxs-lookup"><span data-stu-id="918ee-108">hello Scenario</span></span>

<span data-ttu-id="918ee-109">Fabrikam 是區域性航空公司，而以優惠的價格為客戶提供優良的服務，是該公司努力的目標。</span><span class="sxs-lookup"><span data-stu-id="918ee-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="918ee-110">維護問題是造成航班延誤的原因之一，而引擎維護又是其中最為棘手的項目。</span><span class="sxs-lookup"><span data-stu-id="918ee-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="918ee-111">Fabrikam 必須避免引擎失敗期間飛行代價，會定期檢查其引擎和排程根據 tooa 計劃的維護。</span><span class="sxs-lookup"><span data-stu-id="918ee-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="918ee-112">不過，引擎不一定有的飛機 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="918ee-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="918ee-113">所以有一些引擎維護工作並非必要。</span><span class="sxs-lookup"><span data-stu-id="918ee-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="918ee-114">但嚴重者若在執行維護工作之前發生問題，可能會造成飛機停飛。</span><span class="sxs-lookup"><span data-stu-id="918ee-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="918ee-115">如果位置則飛機其中 hello 右側的技術人員或零件無法使用，這些問題可能會特別是很費時。</span><span class="sxs-lookup"><span data-stu-id="918ee-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="918ee-116">Fabrikam 的飛機 hello 引擎已執行檢測與感應器監視期間飛行 engine 狀況。</span><span class="sxs-lookup"><span data-stu-id="918ee-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="918ee-117">Fabrikam 使用 hello 預測性維護方案 toocollect hello 感應器資料收集期間 hello 班機。</span><span class="sxs-lookup"><span data-stu-id="918ee-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="918ee-118">引擎操作的累積年和之後資料失敗，Fabrikam 的資料科學家有模型化方式 toopredict hello 剩餘的生命週期 (RUL) 飛機引擎。</span><span class="sxs-lookup"><span data-stu-id="918ee-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="918ee-119">hello 模型使用中的 hello 引擎感應器四種資料引擎損耗，導致 tooeventual 失敗之間的相互關聯。</span><span class="sxs-lookup"><span data-stu-id="918ee-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="918ee-120">當 Fabrikam 繼續 tooperform 規則視察 tooensure 安全時，它現在可以使用 hello 模型 toocompute hello RUL 每個引擎在每個班機之後。</span><span class="sxs-lookup"><span data-stu-id="918ee-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="918ee-121">hello 模型使用 hello 遙測 hello 飛行期間收集從 hello 引擎。</span><span class="sxs-lookup"><span data-stu-id="918ee-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="918ee-122">Fabrikam 現在已可以預測未來的失敗點，並預先規劃維護及維修計劃。</span><span class="sxs-lookup"><span data-stu-id="918ee-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="918ee-123">hello 解決方案模型會使用實際的引擎損耗資料。</span><span class="sxs-lookup"><span data-stu-id="918ee-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="918ee-124">Fabrikam 可以預測 hello 點，需要維護時，最佳化其操作 tooreduce 成本。</span><span class="sxs-lookup"><span data-stu-id="918ee-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="918ee-125">維護協調者會使用排程器︰</span><span class="sxs-lookup"><span data-stu-id="918ee-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="918ee-126">計劃維護 toocoincide 飛機停止的特定位置。</span><span class="sxs-lookup"><span data-stu-id="918ee-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="918ee-127">確定有足夠的時間而不會造成排程中斷是供 hello 飛機 toobe 停止服務。</span><span class="sxs-lookup"><span data-stu-id="918ee-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="918ee-128">tooschedule 技術人員 tooensure 飛機會有效率地服務，不含等候時間。</span><span class="sxs-lookup"><span data-stu-id="918ee-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="918ee-129">庫存控制管理員因為會收到維護計畫，所以可以據此最佳化其訂單程序與備用零件庫存。</span><span class="sxs-lookup"><span data-stu-id="918ee-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="918ee-130">這些活動啟用 Fabrikam toominimize 飛機地面時間並降低作業成本，同時確保乘客和團隊 hello 安全。</span><span class="sxs-lookup"><span data-stu-id="918ee-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="918ee-131">toounderstand 如何[Azure IoT 套件][ lnk_iot_suite]提供 hello 功能客戶需要 toorealize hello 可能的預測性維護，請檢閱這[資訊圖][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="918ee-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="918ee-132">如何建置 hello 預測性維護方案</span><span class="sxs-lookup"><span data-stu-id="918ee-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="918ee-133">hello 解決方案會使用現有的 Azure 機器學習模型提供作為範本 tooshow 從裝置透過 IoT 套件服務所收集的遙測使用這些功能。</span><span class="sxs-lookup"><span data-stu-id="918ee-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="918ee-134">Microsoft 已建[迴歸模型][ lnk_regression_model]飛機引擎可公開可用的資料為基礎的<sup>\[1\]</sup>，並逐步指引 toouse hello 模型的方式。</span><span class="sxs-lookup"><span data-stu-id="918ee-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="918ee-135">hello Azure IoT 預測性維護方案會使用此範本所建立的 hello 迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="918ee-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="918ee-136">hello 模型是部署到您的 Azure 訂用帳戶，並透過自動產生的 API 公開。</span><span class="sxs-lookup"><span data-stu-id="918ee-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="918ee-137">hello 解決方案包含測試資料表示 （的總計 100) 4 hello 子集引擎和 hello 4 （的總 21) 感應器資料流。</span><span class="sxs-lookup"><span data-stu-id="918ee-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="918ee-138">此資料是足夠 tooprovide 精確的結果從 hello 定型的模型。</span><span class="sxs-lookup"><span data-stu-id="918ee-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="918ee-139">*\[1\] A. Saxena and K. Goebel (2008)。《渦輪風扇發動機性能下降模擬資料集》(Turbofan Engine Degradation Simulation Data Set)，NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="918ee-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="918ee-140">開始使用預測性維護</span><span class="sxs-lookup"><span data-stu-id="918ee-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="918ee-141">本教學課程會示範如何 tooprovision hello 預測性維護方案。</span><span class="sxs-lookup"><span data-stu-id="918ee-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="918ee-142">它會引導您完成 hello 預測性維護方案 hello 基本功能。</span><span class="sxs-lookup"><span data-stu-id="918ee-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="918ee-143">您可以存取這些功能透過 hello 方案儀表板與 hello 預先設定的方案一起部署。</span><span class="sxs-lookup"><span data-stu-id="918ee-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="918ee-144">toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="918ee-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="918ee-145">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="918ee-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="918ee-146">如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。</span><span class="sxs-lookup"><span data-stu-id="918ee-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="918ee-147">登入太[azureiotsuite.com] [ lnk-azureiotsuite]使用您的 Azure 帳戶的認證，再按一下 **+**  toocreate 方案。</span><span class="sxs-lookup"><span data-stu-id="918ee-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="918ee-148">按一下**選取**hello**預測性維護**磚。</span><span class="sxs-lookup"><span data-stu-id="918ee-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="918ee-149">輸入預先設定的預測性維護解決方案的 [解決方案名稱]。</span><span class="sxs-lookup"><span data-stu-id="918ee-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="918ee-150">選取 hello**區域**和**訂用帳戶**希望 toouse tooprovision hello 方案。</span><span class="sxs-lookup"><span data-stu-id="918ee-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="918ee-151">按一下**建立方案**toobegin hello 佈建程序。</span><span class="sxs-lookup"><span data-stu-id="918ee-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="918ee-152">這個程序通常需要幾分鐘的時間 toorun。</span><span class="sxs-lookup"><span data-stu-id="918ee-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="918ee-153">等候佈建程序 toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="918ee-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="918ee-154">按一下具有您方案的 hello 磚**佈建**狀態。</span><span class="sxs-lookup"><span data-stu-id="918ee-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="918ee-155">請注意 hello**佈建狀態**您 Azure 訂用帳戶中部署 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="918ee-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="918ee-156">佈建完成之後，hello 狀態變更太**準備**。</span><span class="sxs-lookup"><span data-stu-id="918ee-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="918ee-157">按一下您的方案在 hello 右窗格中的 hello 磚 toosee hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="918ee-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="918ee-158">從這個窗格中，您可以啟動 hello 方案儀表板和存取 hello Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="918ee-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="918ee-159">如果您遇到部署預先設定的 hello 解決方案的問題，請檢閱[hello azureiotsuite.com 網站的權限][ lnk-permissions]和 hello[常見問題集][ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="918ee-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="918ee-160">如果 hello 問題仍然存在，則在 hello 上建立服務票證[入口網站][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="918ee-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="918ee-161">有 toosee 如預期般詳細資料，未列出您的解決方案嗎？</span><span class="sxs-lookup"><span data-stu-id="918ee-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="918ee-162">請在 [使用者心聲](https://feedback.azure.com/forums/321918-azure-iot)中提供功能建議給我們。</span><span class="sxs-lookup"><span data-stu-id="918ee-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="918ee-163">檢視 hello 方案</span><span class="sxs-lookup"><span data-stu-id="918ee-163">View hello solution</span></span>

<span data-ttu-id="918ee-164">本節會引導您完成 hello 方案 UI。</span><span class="sxs-lookup"><span data-stu-id="918ee-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="918ee-165">預測性維護儀表板</span><span class="sxs-lookup"><span data-stu-id="918ee-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="918ee-166">此頁面 hello web 應用程式中的使用 PowerBI JavaScript 控制項 (請參閱 hello [PowerBI 視覺效果儲存機制][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="918ee-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="918ee-167">hello hello blob 儲存體中的資料流分析工作的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="918ee-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="918ee-168">hello RUL 和循環計數每飛機引擎。</span><span class="sxs-lookup"><span data-stu-id="918ee-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="918ee-169">觀察 hello 雲端解決方案的 hello 行為</span><span class="sxs-lookup"><span data-stu-id="918ee-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="918ee-170">在 hello Azure 入口網站中瀏覽 toohello 資源群組 hello 方案名稱與您選擇 tooview 佈建的資源。</span><span class="sxs-lookup"><span data-stu-id="918ee-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="918ee-171">當您佈建 hello 預先設定的方案時，您會收到含有連結 toohello Machine Learning 工作區的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="918ee-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="918ee-172">您也可以導覽 toohello Machine Learning 工作區，從 hello [azureiotsuite.com] [ lnk-azureiotsuite]頁面為您佈建的方案。</span><span class="sxs-lookup"><span data-stu-id="918ee-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="918ee-173">圖格時，此頁面提供 hello 方案是在 hello**準備**狀態。</span><span class="sxs-lookup"><span data-stu-id="918ee-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="918ee-174">在 hello 方案入口網站中，您可以看到該 hello 範例使用四個模擬的裝置 toorepresent 兩個飛機佈建與每個飛機各有四個感應器的兩個引擎。</span><span class="sxs-lookup"><span data-stu-id="918ee-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="918ee-175">當您第一次瀏覽 toohello 方案入口網站時，就會停止 hello 模擬。</span><span class="sxs-lookup"><span data-stu-id="918ee-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="918ee-176">按一下**開始模擬**toobegin hello 模擬。</span><span class="sxs-lookup"><span data-stu-id="918ee-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="918ee-177">hello 感應器歷程記錄、 RUL、 週期和 RUL 記錄填入 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="918ee-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="918ee-178">當 RUL 小於 160 （選擇供示範之用的任意臨界值），hello 方案入口網站會顯示 RUL 顯示警告的符號 下一步 toohello。</span><span class="sxs-lookup"><span data-stu-id="918ee-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="918ee-179">hello 方案入口網站也會反白顯示黃色 hello 飛機引擎。</span><span class="sxs-lookup"><span data-stu-id="918ee-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="918ee-180">請注意，hello RUL 值需要一般向下趨勢整體，但通常 toobounce 向上和向下。</span><span class="sxs-lookup"><span data-stu-id="918ee-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="918ee-181">這個行為會因各種週期長度 hello 和 hello 模型精確度。</span><span class="sxs-lookup"><span data-stu-id="918ee-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="918ee-182">hello 完整模擬會大約 35 分鐘 toocomplete 148 循環。</span><span class="sxs-lookup"><span data-stu-id="918ee-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="918ee-183">第一個大約 5 分鐘的時間達到 hello 160 RUL 門檻 hello 和這兩個引擎叫用 hello 臨界值，約 8 分鐘。</span><span class="sxs-lookup"><span data-stu-id="918ee-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="918ee-184">hello 模擬執行透過 hello 完整資料集 148 循環，settles 最終 RUL 和週期的值。</span><span class="sxs-lookup"><span data-stu-id="918ee-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="918ee-185">您可以停止 hello 模擬在任何點，但按一下**開始模擬**重新執行 hello 模擬從 hello 開始 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="918ee-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="918ee-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="918ee-186">Next steps</span></span>

<span data-ttu-id="918ee-187">深入了解 Azure IoT 如何讓預測性維護的情況下，讀取 toolearn[擷取值從 hello 物聯網][lnk_capture_value]。</span><span class="sxs-lookup"><span data-stu-id="918ee-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="918ee-188">採取[逐步解說][ lnk-predictive-walkthrough]的 hello 預測性維護方案。</span><span class="sxs-lookup"><span data-stu-id="918ee-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="918ee-189">您也可以探索 hello 的某些其他特性和功能 hello IoT 套件預先設定的解決方案：</span><span class="sxs-lookup"><span data-stu-id="918ee-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="918ee-190">[IoT 套件的常見問題集][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="918ee-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="918ee-191">[從 hello 接地 IoT 安全性][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="918ee-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/