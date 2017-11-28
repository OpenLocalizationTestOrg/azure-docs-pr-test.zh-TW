---
title: "Azure IoT 套件連線處理站概觀 | Microsoft Docs"
description: "Azure IoT 套件連線處理站預先設定的解決方案說明。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: d502c8e2e2715899279f6ebcf7ed89c19a1bb9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-connected-factory-preconfigured-solution"></a><span data-ttu-id="17272-103">開始使用 Azure IoT 套件連線處理站預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="17272-103">Get started with the connected factory preconfigured solution</span></span>

<span data-ttu-id="17272-104">Azure IoT 套件[預先設定的解決方案][lnk-preconfigured-solutions]結合了多項 Azure IoT 服務，以提供可實作常見 IoT 商務案例的端對端解決方案。</span><span class="sxs-lookup"><span data-stu-id="17272-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="17272-105">「連線處理站廠」預先設定的解決方案會連線並監視您的工業裝置。</span><span class="sxs-lookup"><span data-stu-id="17272-105">The *connected factory* preconfigured solution connects to and monitors your industrial devices.</span></span> <span data-ttu-id="17272-106">您可以使用此解決方案來分析裝置的資料流，以及提升營運生產力和獲利率。</span><span class="sxs-lookup"><span data-stu-id="17272-106">You can use the solution to analyze the stream of data from your devices and to drive operational productivity and profitability.</span></span>

<span data-ttu-id="17272-107">本教學課程示範如何佈建連線處理站預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="17272-107">This tutorial shows you how to provision the connected factory preconfigured solution.</span></span> <span data-ttu-id="17272-108">其中也逐步說明預先設定解決方案的基本功能。</span><span class="sxs-lookup"><span data-stu-id="17272-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="17272-109">您可以從隨預先設定解決方案一起部署的解決方案儀表板中，存取其中許多功能：</span><span class="sxs-lookup"><span data-stu-id="17272-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![連線處理站預先設定的解決方案儀表板][img-cf-home]

<span data-ttu-id="17272-111">若要完成此教學課程，您需要一個有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="17272-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="17272-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="17272-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="17272-113">如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。</span><span class="sxs-lookup"><span data-stu-id="17272-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-the-solution"></a><span data-ttu-id="17272-114">佈建解決方案</span><span class="sxs-lookup"><span data-stu-id="17272-114">Provision the solution</span></span>

1. <span data-ttu-id="17272-115">使用 Azure 帳戶認證登入 azureiotsuite.com，然後按一下 "**+**" 以建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="17272-115">Log on to azureiotsuite.com using your Azure account credentials, and click "**+**" to create a solution.</span></span>
2. <span data-ttu-id="17272-116">按一下 [連線處理站] 圖格上的 [選取]。</span><span class="sxs-lookup"><span data-stu-id="17272-116">Click **Select** on the **Connected factory** tile.</span></span>
3. <span data-ttu-id="17272-117">輸入連線處理站預先設定的解決方案的 [解決方案名稱]。</span><span class="sxs-lookup"><span data-stu-id="17272-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="17272-118">選取您要用來佈建解決方案的 [訂用帳戶] 和 [區域]。</span><span class="sxs-lookup"><span data-stu-id="17272-118">Select the **Subscription** and **Region** you want to use to provision the solution.</span></span>
5. <span data-ttu-id="17272-119">按一下 [建立解決方案]  開始佈建程序。</span><span class="sxs-lookup"><span data-stu-id="17272-119">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="17272-120">此程序通常需要數分鐘的執行時間。</span><span class="sxs-lookup"><span data-stu-id="17272-120">This process typically takes several minutes to run.</span></span>

### <a name="while-you-wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="17272-121">在您等候佈建程序完成時</span><span class="sxs-lookup"><span data-stu-id="17272-121">While you wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="17272-122">按一下狀態為 **佈建中** 的解決方案圖格。</span><span class="sxs-lookup"><span data-stu-id="17272-122">Click the tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="17272-123">請注意， **佈建狀態** 說明您的 Azure 訂用帳戶中已經佈建 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="17272-123">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="17272-124">佈建完成之後，狀態會變更為 **就緒**。</span><span class="sxs-lookup"><span data-stu-id="17272-124">Once provisioning completes, the status changes to **Ready**.</span></span>
4. <span data-ttu-id="17272-125">按一下圖格，就會在右邊窗格中看到解決方案的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="17272-125">Click the tile to see the details of your solution in the right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="17272-126">如果您在佈建預先設定的解決方案時遇到問題，請參閱 [azureiotsuite.com 網站的權限][lnk-permissions]和[連線的處理站常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="17272-126">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="17272-127">如果問題持續發生，請在[入口網站][lnk-portal]建立服務票證。</span><span class="sxs-lookup"><span data-stu-id="17272-127">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="17272-128">是否有您預期會看到但沒有列出的解決方案詳細資料？</span><span class="sxs-lookup"><span data-stu-id="17272-128">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="17272-129">請在 [使用者心聲](https://feedback.azure.com/forums/321918-azure-iot)中提供功能建議給我們。</span><span class="sxs-lookup"><span data-stu-id="17272-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="17272-130">案例概觀</span><span class="sxs-lookup"><span data-stu-id="17272-130">Scenario overview</span></span>

<span data-ttu-id="17272-131">當您部署連線處理站預先設定的解決方案時，它會預先填入可讓您逐步執行常見產業案例的資源。</span><span class="sxs-lookup"><span data-stu-id="17272-131">When you deploy the connected factory preconfigured solution, it is prepopulated with resources that enable you to step through a common industrial scenario.</span></span> <span data-ttu-id="17272-132">在此案例中，連線至解決方案的數個工廠會報告計算整體設備效率 (OEE) 和關鍵效能指標 (KPI) 所需的資料值。</span><span class="sxs-lookup"><span data-stu-id="17272-132">In this scenario, several factories connected to the solution report the data values required to compute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="17272-133">下列各節將示範如何：</span><span class="sxs-lookup"><span data-stu-id="17272-133">The following sections show you how to:</span></span>

* <span data-ttu-id="17272-134">監視處理站、生產線、站區 OEE 和 KPI 值</span><span class="sxs-lookup"><span data-stu-id="17272-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="17272-135">使用 Azure Time Series Insights 分析這些裝置產生的遙測資料</span><span class="sxs-lookup"><span data-stu-id="17272-135">Analyze the telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="17272-136">處理警示以修正問題</span><span class="sxs-lookup"><span data-stu-id="17272-136">Act on alerts to fix issues</span></span>

<span data-ttu-id="17272-137">此案例的主要功能是您可以從解決方案儀表板遠端執行所有這些動作。</span><span class="sxs-lookup"><span data-stu-id="17272-137">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="17272-138">您不需要實際存取裝置。</span><span class="sxs-lookup"><span data-stu-id="17272-138">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="17272-139">檢視解決方案儀表板</span><span class="sxs-lookup"><span data-stu-id="17272-139">View the solution dashboard</span></span>

<span data-ttu-id="17272-140">解決方案儀表板可讓您管理部署的解決方案。</span><span class="sxs-lookup"><span data-stu-id="17272-140">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="17272-141">它是全域處理站組態的階層式表示法。</span><span class="sxs-lookup"><span data-stu-id="17272-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="17272-142">例如，您可以檢視 OEE 和 KPI、針對遙測和動作警示發佈新節點。</span><span class="sxs-lookup"><span data-stu-id="17272-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="17272-143">當佈建完成且預先設定解決方案的圖格指示 [就緒] 時，選擇 [啟動] 以在新的索引標籤中開啟連線處理站解決方案入口網站。</span><span class="sxs-lookup"><span data-stu-id="17272-143">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your connected factory solution portal in a new tab.</span></span>

    ![啟動預先設定的解決方案][img-launch-solution]

1. <span data-ttu-id="17272-145">根據預設，此解決方案入口網站會顯示儀表板。</span><span class="sxs-lookup"><span data-stu-id="17272-145">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="17272-146">若要瀏覽至入口網站的其他區域，請使用頁面左側的功能表。</span><span class="sxs-lookup"><span data-stu-id="17272-146">To navigate to other areas of the portal, use the menu on the left-hand side of the page.</span></span>

    ![連線處理站預先設定的解決方案儀表板][cf-img-menu]

<span data-ttu-id="17272-148">儀表板會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="17272-148">The dashboard displays the following information:</span></span>

* <span data-ttu-id="17272-149">**處理站清單**面板，可顯示解決方案的狀態、位置和目前生產組態。</span><span class="sxs-lookup"><span data-stu-id="17272-149">A **Factory list** panel that shows the status, location, and current production configuration in the solution.</span></span> <span data-ttu-id="17272-150">當您第一次執行解決方案時，有數個模擬裝置。</span><span class="sxs-lookup"><span data-stu-id="17272-150">When you first run the solution, there are a number of simulated devices.</span></span> <span data-ttu-id="17272-151">生產線模擬是由每條生產線上執行模擬工作及共用資料的三部實際 OPC UA 伺服器所構成。</span><span class="sxs-lookup"><span data-stu-id="17272-151">The production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="17272-152">如需 OPC UA 的詳細資訊，請參閱[連線的處理站常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="17272-152">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="17272-153">**地圖**，可顯示連線至解決方案之每個裝置的位置。</span><span class="sxs-lookup"><span data-stu-id="17272-153">A **map** that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="17272-154">解決方案可以使用 Bing 地圖服務 API 在地圖上繪製資訊。</span><span class="sxs-lookup"><span data-stu-id="17272-154">The solution can use the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="17272-155">如果您的訂用帳戶已啟用 Bing 地圖服務企業版 API，則會自動使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="17272-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="17272-156">如未啟用，請參閱[常見問題集][lnk-faq]以了解如何讓地圖變成動態。</span><span class="sxs-lookup"><span data-stu-id="17272-156">If not, see the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="17272-157">**警示**面板，可顯示遙測或 OEE/KPI 值超過特定閾值時所產生的警示。</span><span class="sxs-lookup"><span data-stu-id="17272-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="17272-158">**整體設備效率**面板，可顯示整個企業或您所檢視之處理站/生產線/站區的 OEE 值。</span><span class="sxs-lookup"><span data-stu-id="17272-158">An **Overall Equipment Efficiency** panel that shows the OEE values for the whole enterprise, or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="17272-159">此值會從站區檢視彙總至企業層級。</span><span class="sxs-lookup"><span data-stu-id="17272-159">This value is aggregated from the station view to the enterprise level.</span></span> <span data-ttu-id="17272-160">您可以進一步分析 OEE 數字及其組成元素。</span><span class="sxs-lookup"><span data-stu-id="17272-160">The OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="17272-161">**關鍵效能指標**面板，可顯示所產生的單位數，以及整個企業或您所檢視之處理站/生產線/站區所使用的能源。</span><span class="sxs-lookup"><span data-stu-id="17272-161">**Key Performance Indicators** panel that displays the number of units produced and energy used by the whole enterprise or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="17272-162">這些值會從站區檢視彙總至企業層級。</span><span class="sxs-lookup"><span data-stu-id="17272-162">These values are aggregated from a station view to the enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="17272-163">檢視工廠</span><span class="sxs-lookup"><span data-stu-id="17272-163">View factories</span></span>

<span data-ttu-id="17272-164">*工廠*面板，可顯示解決方案中所有工廠的地理位置、其狀態和目前的生產組態。</span><span class="sxs-lookup"><span data-stu-id="17272-164">The *Factories* panel shows you the geographical location of all the factories in the solution, their status, and current production configuration.</span></span> <span data-ttu-id="17272-165">從 [位置] 清單，您可以瀏覽至解決方案階層中的其他層級。</span><span class="sxs-lookup"><span data-stu-id="17272-165">From the locations list, you can navigate to the other levels in the solution hierarchy.</span></span> <span data-ttu-id="17272-166">清單中的資料列是一些超連結，可連結該位置的生產線詳細資料。</span><span class="sxs-lookup"><span data-stu-id="17272-166">The rows in the list are hyperlinks that link details of the production lines at that location.</span></span> <span data-ttu-id="17272-167">您可以接著深入探詢生產線詳細資料，並向下切入到站區層級檢視。</span><span class="sxs-lookup"><span data-stu-id="17272-167">It is then possible to drill into the production line details and down to the station level view.</span></span> <span data-ttu-id="17272-168">您也可以將篩選條件套用至清單。</span><span class="sxs-lookup"><span data-stu-id="17272-168">You can also apply a filter to the list.</span></span>

![連線處理站預先設定的解決方案處理站][cf-img-factories] 

1. <span data-ttu-id="17272-170">**處理站面板**會顯示此解決方案的處理站清單。</span><span class="sxs-lookup"><span data-stu-id="17272-170">The **Factory panel** shows the factory list for this solution.</span></span>

2. <span data-ttu-id="17272-171">處理站清單最初會顯示佈建程序所建立的 6 個處理站。</span><span class="sxs-lookup"><span data-stu-id="17272-171">The factory list initially shows six factories created by the provisioning process.</span></span> <span data-ttu-id="17272-172">您可以將其他模擬裝置和實體裝置新增至解決方案。</span><span class="sxs-lookup"><span data-stu-id="17272-172">You can add additional simulated and physical devices to the solution.</span></span>

3. <span data-ttu-id="17272-173">若要檢視處理站的詳細資訊，請按一下處理站清單中的資料列。</span><span class="sxs-lookup"><span data-stu-id="17272-173">To view the details of a factory, click the row in the factory list.</span></span>

4. <span data-ttu-id="17272-174">若要檢視生產線的詳細資訊，請按一下清單中的資料列。</span><span class="sxs-lookup"><span data-stu-id="17272-174">To view the details of a production line, click the row in the list.</span></span>

5. <span data-ttu-id="17272-175">若要檢視生產線上站區的已發佈 OPC UA 節點，請按一下清單中的資料列。</span><span class="sxs-lookup"><span data-stu-id="17272-175">To view the published OPC UA nodes of a station on the production line, click the row in the list.</span></span>

6. <span data-ttu-id="17272-176">若要檢視站區中特定節點的詳細資料，請按一下清單中的資料列。</span><span class="sxs-lookup"><span data-stu-id="17272-176">To view details on a specific node in the station, click the row in the list.</span></span> <span data-ttu-id="17272-177">這個動作會啟動具有 Time Series Insights 視覺效果的內容面板。</span><span class="sxs-lookup"><span data-stu-id="17272-177">This action launches the context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="17272-178">按一下這些圖形，在 Time Series Insights 總管環境中做進一步分析。</span><span class="sxs-lookup"><span data-stu-id="17272-178">Click these graphs to do further analysis in the Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="17272-179">檢視地圖</span><span class="sxs-lookup"><span data-stu-id="17272-179">View map</span></span>

<span data-ttu-id="17272-180">如果您的訂用帳戶可存取 Bing 地圖服務 API，則「工廠」地圖會顯示解決方案中所有工廠的地理位置和狀態。</span><span class="sxs-lookup"><span data-stu-id="17272-180">If your subscription has access to the Bing Maps API, the *Factories* map shows you the geographical location and status of all the factories in the solution.</span></span> <span data-ttu-id="17272-181">若要深入探詢位置詳細資料，請按一下地圖上顯示的位置。</span><span class="sxs-lookup"><span data-stu-id="17272-181">To drill into the location details, click the locations displayed on the map.</span></span>

![連線處理站預先設定的解決方案地圖][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="17272-183">檢視警示</span><span class="sxs-lookup"><span data-stu-id="17272-183">View alerts</span></span>

<span data-ttu-id="17272-184">[警示] 面板會顯示因為回報的值或計算的 OEE/KPI 值超過其設定的閾值而產生的警示。</span><span class="sxs-lookup"><span data-stu-id="17272-184">The **Alert** panel shows you alerts generated due to a reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="17272-185">此面板會顯示階層供每個層級的警示 (從站區層級檢視到全域檢視)。</span><span class="sxs-lookup"><span data-stu-id="17272-185">This panel displays alerts at each level of the hierarchy, from the station level view to the global view.</span></span> <span data-ttu-id="17272-186">警示包含警示描述、日期、時間、位置和發生次數。</span><span class="sxs-lookup"><span data-stu-id="17272-186">The alerts contain a description of the alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="17272-187">您可以使用 Time Series Insights 資料深入解析造成警示的資料。</span><span class="sxs-lookup"><span data-stu-id="17272-187">You can gain insights in to the data that caused the alert using the Time Series Insights data.</span></span> <span data-ttu-id="17272-188">Time Series Insights 資料會在適用的警示中顯現。</span><span class="sxs-lookup"><span data-stu-id="17272-188">The Time Series Insights data is visualized in the alerts where applicable.</span></span> <span data-ttu-id="17272-189">如果您是系統管理員，您可以對警示採取預設動作，例如︰</span><span class="sxs-lookup"><span data-stu-id="17272-189">If you are an Administrator, you can take default actions on the alerts such as:</span></span>

* <span data-ttu-id="17272-190">關閉警示。</span><span class="sxs-lookup"><span data-stu-id="17272-190">Close the alert.</span></span>
* <span data-ttu-id="17272-191">認知警示。</span><span class="sxs-lookup"><span data-stu-id="17272-191">Acknowledge the alert.</span></span>

<span data-ttu-id="17272-192">您可以選擇性地採取更複雜的動作。</span><span class="sxs-lookup"><span data-stu-id="17272-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="17272-193">例如，對於組件的壓力 OPC UA 節點，您可以︰</span><span class="sxs-lookup"><span data-stu-id="17272-193">For example, for the Pressure OPC UA Node of the Assembly you could:</span></span>

* <span data-ttu-id="17272-194">在新的瀏覽器視窗中的網頁顯示支援資訊。</span><span class="sxs-lookup"><span data-stu-id="17272-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="17272-195">在裝置上呼叫 OPC UA 方法，以緩和警示的原因。</span><span class="sxs-lookup"><span data-stu-id="17272-195">Mitigate the cause of the alert by calling an OPC UA method on the device.</span></span>
* <span data-ttu-id="17272-196">隱藏預設動作的可用性。</span><span class="sxs-lookup"><span data-stu-id="17272-196">Suppress the availability of the default actions.</span></span>

    ![連線處理站預先設定的解決方案警示][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="17272-198">這些警示是由預先設定之解決方案中的組態檔中指定的規則所產生。</span><span class="sxs-lookup"><span data-stu-id="17272-198">These alerts are generated by rules that are specified in a configuration file in the preconfigured solution.</span></span> <span data-ttu-id="17272-199">當 OEE 或 KPI 數字或 OPC UA 節點值超過其設定的閾值時，這些規則即可產生警示。</span><span class="sxs-lookup"><span data-stu-id="17272-199">These rules can generate alerts when the OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="17272-200">[警示] 面板會顯示在此解決方案中產生的警示。</span><span class="sxs-lookup"><span data-stu-id="17272-200">The **Alerts panel** shows the alerts generated in this solution.</span></span>

2. <span data-ttu-id="17272-201">若要檢視警示的詳細資訊，請按一下 [警示] 面板中的警示。</span><span class="sxs-lookup"><span data-stu-id="17272-201">To view the details of an alert, click the alert in the alerts panel.</span></span>

3. <span data-ttu-id="17272-202">若要進一步分析警示資料，請按一下警示面板中的圖表，以開啟 Time Series Insights 總管環境。</span><span class="sxs-lookup"><span data-stu-id="17272-202">To further analyze the alert data, click the graph in the alert panel to open the Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="17272-203">若要解決警示，可在 [警示] 面板中執行數個動作。</span><span class="sxs-lookup"><span data-stu-id="17272-203">To address the alert, several actions are available in the alert panel.</span></span> <span data-ttu-id="17272-204">選擇適當的選項，然後按一下 [執行動作命令] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="17272-204">Choose the appropriate option for you and click the execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="17272-205">檢視整體設備效率</span><span class="sxs-lookup"><span data-stu-id="17272-205">View overall equipment efficiency</span></span>

<span data-ttu-id="17272-206">OEE 會使用重要生產相關作業參數來評比製造程序的效率。</span><span class="sxs-lookup"><span data-stu-id="17272-206">OEE rates the efficiency of the manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="17272-207">OEE 是一種業界標準量值，其計算方式是將可用率、效能率和品質率相乘︰OEE = 可用項 x 效能 x 品質。</span><span class="sxs-lookup"><span data-stu-id="17272-207">OEE is an industry standard measure calculated by multiplying the availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![連線處理站預先設定的解決方案 OEE][cf-img-oee]

1. <span data-ttu-id="17272-209">若要檢視階層中任何層級的 OEE，請瀏覽至您所需的特定檢視。</span><span class="sxs-lookup"><span data-stu-id="17272-209">To view OEE for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="17272-210">適用於該檢視的 OEE 會連同構成 OEE 百分比的每個元素顯示在面板中。</span><span class="sxs-lookup"><span data-stu-id="17272-210">The OEE for that view displays in the panel along with each of the elements that make up the OEE percentage.</span></span>

2. <span data-ttu-id="17272-211">若要進一步分析階層資料中任何層級的 OEE，請按一下 OEE、可用性、效能或品質百分比。</span><span class="sxs-lookup"><span data-stu-id="17272-211">To further analyze the OEE for any level in the hierarchy data, click either the OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="17272-212">內容面板會以 Time Series Insights 支援的視覺效果呈現，其中顯示過去一小時、過去 24 小時和過去 7 天的資料。</span><span class="sxs-lookup"><span data-stu-id="17272-212">A context panel appears with Time Series Insights powered visualizations that shows data from the last hour, last 24 hours, and last 7 days.</span></span>

    ![連線處理站預先設定的解決方案 TSI 視覺效果][cf-img-tsi-visualization]

3. <span data-ttu-id="17272-214">若要進一步分析警示資料，請按一下警示面板上的圖表。</span><span class="sxs-lookup"><span data-stu-id="17272-214">To further analyze the alert data, click the graph in the alert panel.</span></span> <span data-ttu-id="17272-215">這個動作會開啟 Time Series Insights 總管環境。</span><span class="sxs-lookup"><span data-stu-id="17272-215">This action opens the Time Series Insights explorer environment.</span></span>

    ![連線處理站預先設定的解決方案 TSI 總管][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="17272-217">檢視關鍵效能指標</span><span class="sxs-lookup"><span data-stu-id="17272-217">View Key Performance Indicators</span></span>

<span data-ttu-id="17272-218">此解決方案會提供兩個關鍵效能指標：「每小時單位數」和「所用能源 (kwh)」。</span><span class="sxs-lookup"><span data-stu-id="17272-218">The solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![連線處理站預先設定的解決方案 KPI][cf-img-kpi]

1. <span data-ttu-id="17272-220">若要檢視階層中任何層級的每小時單位數或所用能源，請瀏覽至您所需的特定檢視。</span><span class="sxs-lookup"><span data-stu-id="17272-220">To view units per hour or energy used for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="17272-221">每小時單位數和所用能源會顯示在面板中。</span><span class="sxs-lookup"><span data-stu-id="17272-221">The units per hour and energy used display in the panel.</span></span>

2. <span data-ttu-id="17272-222">若要進一步分析階層中任何層級的每小時單位數和所用能源，請按一下 [關鍵效能指標] 面板中的量測計。</span><span class="sxs-lookup"><span data-stu-id="17272-222">To analyze units per hour or energy used for any level in the hierarchy further, click the gauge in the **Key Performance Indicators** panel.</span></span> <span data-ttu-id="17272-223">內容面板會以 Time Series Insights 支援的視覺效果呈現，可讓您檢視過去一小時、過去 24 小時和過去 7 天的資料。</span><span class="sxs-lookup"><span data-stu-id="17272-223">A context panel appears with Time Series Insights powered visualizations enabling you to view data from the last hour, the last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="17272-224">案例檢閱</span><span class="sxs-lookup"><span data-stu-id="17272-224">Scenario review</span></span>

<span data-ttu-id="17272-225">在此案例中，您會在儀表板中監視您的工廠 OEE 和 KPI 值。</span><span class="sxs-lookup"><span data-stu-id="17272-225">In this scenario, you monitored your factories OEE and KPIs values, in the dashboard.</span></span> <span data-ttu-id="17272-226">接著使用 Time Series Insights 來提供詳細資訊，協助深入探詢 OEE 和 KPI 遙測資料，進而協助偵測異常狀況。</span><span class="sxs-lookup"><span data-stu-id="17272-226">You then used Time Series Insights to provide more information to help drill further into the telemetry data for OEE and KPIs to help with detecting anomalies.</span></span> <span data-ttu-id="17272-227">您也使用警示面板來檢視工廠問題，並使用可供您使用的動作來解決警示。</span><span class="sxs-lookup"><span data-stu-id="17272-227">You also used the alert panel to view issues with your factories and you used the actions available to you to resolve the alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="17272-228">其他功能</span><span class="sxs-lookup"><span data-stu-id="17272-228">Other features</span></span>

<span data-ttu-id="17272-229">下列各節說明連線的處理站解決方案的一些其他功能，這些功能在前一個情節中並未說明。</span><span class="sxs-lookup"><span data-stu-id="17272-229">The following sections describe some additional features of the connected factory solution that are not described in the previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="17272-230">套用篩選條件</span><span class="sxs-lookup"><span data-stu-id="17272-230">Apply filters</span></span>

1. <span data-ttu-id="17272-231">按一下 [>形箭號] 可在 [處理站位置] 面板或 [警示] 面板中顯示可用的篩選條件清單。</span><span class="sxs-lookup"><span data-stu-id="17272-231">Click the **chevron** to display a list of available filters in either the factory locations panel or the alerts panel.</span></span>

2. <span data-ttu-id="17272-232">[篩選條件] 面板隨即為您顯示。</span><span class="sxs-lookup"><span data-stu-id="17272-232">The filters panel is displayed for you.</span></span> 

    ![連線處理站預先設定的解決方案篩選條件][cf-img-alert-filter]

3. <span data-ttu-id="17272-234">選擇您需要的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="17272-234">Choose the filter that you require.</span></span> <span data-ttu-id="17272-235">也可以在篩選欄位中輸入任意文字。</span><span class="sxs-lookup"><span data-stu-id="17272-235">It is also possible to type free text into the filter fields.</span></span>

4. <span data-ttu-id="17272-236">接著會為您套用此篩選條件。</span><span class="sxs-lookup"><span data-stu-id="17272-236">The filter is then applied for you.</span></span> <span data-ttu-id="17272-237">透過工廠和警示資料表中顯示的漏斗圖示，篩選條件狀態也會顯示在儀表板中。</span><span class="sxs-lookup"><span data-stu-id="17272-237">The filter state is also shown in the dashboard via a funnel that displays in the factories and alerts tables.</span></span>

    ![連線處理站預先設定的解決方案篩選條件][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="17272-239">使用中篩選條件不會影響已顯示的 OEE 和 KPI 值，它只會篩選清單內容。</span><span class="sxs-lookup"><span data-stu-id="17272-239">An active filter does not affect the displayed OEE and KPI values, it only filters the list contents.</span></span>

5. <span data-ttu-id="17272-240">若要清除篩選條件，請按一下漏斗圖示並按一下篩選內容面板中的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="17272-240">To clear a filter, click the funnel and click filter in the filter context panel.</span></span> <span data-ttu-id="17272-241">[所有] 這兩個字會顯示在工廠和警示資料表中。</span><span class="sxs-lookup"><span data-stu-id="17272-241">The text **All** is displayed in the factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="17272-242">瀏覽 OPC UA 伺服器</span><span class="sxs-lookup"><span data-stu-id="17272-242">Browse an OPC UA server</span></span>

<span data-ttu-id="17272-243">當您部署預先設定的解決方案時，會自動佈建您可透過解決方案瀏覽器瀏覽的模擬 OPC UA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="17272-243">When you deploy the preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via the solution browser.</span></span> <span data-ttu-id="17272-244">這些伺服器是「模擬的 OPC UA 伺服器」。</span><span class="sxs-lookup"><span data-stu-id="17272-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="17272-245">模擬伺服器可讓您輕鬆對預先設定的解決方案進行實驗，而不需要部署真實的實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="17272-245">Simulated servers make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical servers.</span></span> <span data-ttu-id="17272-246">若要將真實 OPC UA 伺服器連線至解決方案，請參閱[將 OPC UA 裝置連線至連線處理站預先設定的解決方案][lnk-connect-cf]教學課程。</span><span class="sxs-lookup"><span data-stu-id="17272-246">If you do want to connect a real OPC UA server to the solution, see the [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="17272-247">按一下儀表板導覽列中的**處理站圖示**。</span><span class="sxs-lookup"><span data-stu-id="17272-247">Click the **factory icon** in the dashboard navigation bar.</span></span>

    ![連線處理站預先設定的解決方案伺服器瀏覽器][cf-img-server-browser]

2. <span data-ttu-id="17272-249">從預先設定的清單中選擇其中一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="17272-249">Choose one of the servers from the preconfigured list.</span></span> <span data-ttu-id="17272-250">這份清單會顯示在預先設定的解決方案中為您部署的伺服器。</span><span class="sxs-lookup"><span data-stu-id="17272-250">This list shows the servers that are deployed for you in the preconfigured solution.</span></span>

    ![連線處理站預先設定的解決方案伺服器選取][cf-img-server-choice]

3. <span data-ttu-id="17272-252">按一下 [連線]，[安全性] 對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="17272-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="17272-253">若要進行模擬，您可以放心按一下 [繼續]</span><span class="sxs-lookup"><span data-stu-id="17272-253">For the simulation, it is safe to click **Proceed**</span></span>

4. <span data-ttu-id="17272-254">若要展開伺服器樹狀目錄中的任何節點，請按一下該節點。</span><span class="sxs-lookup"><span data-stu-id="17272-254">To expand any of the nodes in the server tree, click it.</span></span> <span data-ttu-id="17272-255">正在發佈遙測的節點旁邊有勾號。</span><span class="sxs-lookup"><span data-stu-id="17272-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![連線處理站預先設定的解決方案伺服器樹狀目錄][cf-img-server-tree]

5. <span data-ttu-id="17272-257">以滑鼠右鍵按一下要讀取、寫入、發佈或呼叫該節點的項目。</span><span class="sxs-lookup"><span data-stu-id="17272-257">Right-click an item to read, write, publish, or call that node.</span></span> <span data-ttu-id="17272-258">您可使用的動作取決於您的節點權限和屬性。</span><span class="sxs-lookup"><span data-stu-id="17272-258">The actions available to you depend on your permissions and the attributes of the node.</span></span> <span data-ttu-id="17272-259">讀取選項會顯示一個內容面板，以顯示特定節點的值。</span><span class="sxs-lookup"><span data-stu-id="17272-259">The read option to displays a context panel showing the value of the specific node.</span></span> <span data-ttu-id="17272-260">寫入選項會顯示一個內容面板，您可以在此輸入新值。</span><span class="sxs-lookup"><span data-stu-id="17272-260">The write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="17272-261">呼叫選項會顯示一個節點，您可以在此輸入呼叫的參數。</span><span class="sxs-lookup"><span data-stu-id="17272-261">The call option displays a node where you can enter the parameters for the call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="17272-262">發佈節點</span><span class="sxs-lookup"><span data-stu-id="17272-262">Publish a node</span></span>

<span data-ttu-id="17272-263">當您瀏覽*模擬的 OPC UA 伺服器*時，也可以選擇發佈新的節點。</span><span class="sxs-lookup"><span data-stu-id="17272-263">When you browse a *simulated OPC UA server*, you can also choose to publish new nodes.</span></span> <span data-ttu-id="17272-264">您可以分析解決方案中這些節點的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="17272-264">You can analyze the telemetry from these nodes in the solution.</span></span> <span data-ttu-id="17272-265">這些「模擬的 OPC UA 伺服器」可讓您輕鬆對解決方案進行實驗，而不需要部署真實的實體裝置。</span><span class="sxs-lookup"><span data-stu-id="17272-265">These *simulated OPC UA servers* make it easy to experiment with the preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="17272-266">瀏覽至 OPC UA 伺服器瀏覽器樹狀目錄中您想要發佈的節點。</span><span class="sxs-lookup"><span data-stu-id="17272-266">Browse to a node in the OPC UA server browser tree that you wish to publish.</span></span>

2. <span data-ttu-id="17272-267">以滑鼠右鍵按一下節點。</span><span class="sxs-lookup"><span data-stu-id="17272-267">Right-click the node.</span></span>

3. <span data-ttu-id="17272-268">選擇 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="17272-268">Choose **Publish**.</span></span>

    ![連線的處理站發佈節點][cf-img-publish-node]

4. <span data-ttu-id="17272-270">隨即顯示一個內容面板，告訴您發佈成功。</span><span class="sxs-lookup"><span data-stu-id="17272-270">A context panel appears which tells you that the publish has succeeded.</span></span> <span data-ttu-id="17272-271">此節點會出現在站區層級檢視中，且旁邊有核取記號。</span><span class="sxs-lookup"><span data-stu-id="17272-271">The node appears in the station level view with a check mark beside it.</span></span>

    ![連線處理站預先設定的解決方案發佈成功][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="17272-273">命令與控制</span><span class="sxs-lookup"><span data-stu-id="17272-273">Command and control</span></span>

<span data-ttu-id="17272-274">連線處理站可讓您直接從雲端指揮及控制您的工業裝置。</span><span class="sxs-lookup"><span data-stu-id="17272-274">The connected factory allows you command and control your industry devices directly from the cloud.</span></span> <span data-ttu-id="17272-275">您可以使用這項功能來回應裝置所產生的警示。</span><span class="sxs-lookup"><span data-stu-id="17272-275">You can use this feature to respond to alerts generated by the device.</span></span> <span data-ttu-id="17272-276">例如，您可以從雲端將命令傳送到裝置。</span><span class="sxs-lookup"><span data-stu-id="17272-276">For example, you could send a command to the device from the cloud.</span></span> <span data-ttu-id="17272-277">您可以在 OPC UA 伺服器瀏覽器樹狀目錄的 **StationCommands** 節點中找到可用的命令。</span><span class="sxs-lookup"><span data-stu-id="17272-277">You can find the available commands in the **StationCommands** node in the OPC UA servers browser tree.</span></span> <span data-ttu-id="17272-278">在此情節中，您會開啟慕尼黑生產線的裝配站上的洩壓閥。</span><span class="sxs-lookup"><span data-stu-id="17272-278">In this scenario, you open a pressure release valve on the assembly station of a production line in Munich.</span></span> <span data-ttu-id="17272-279">若要使用命令與控制功能，您必須具備預先設定解決方案部署的 [系統管理員] 角色。</span><span class="sxs-lookup"><span data-stu-id="17272-279">To use the command and control functionality, you must be in the **Administrator** role for the preconfigured solution deployment.</span></span>

1. <span data-ttu-id="17272-280">瀏覽至 OPC UA 伺服器瀏覽器樹狀目錄中的 **StationCommands** 節點。</span><span class="sxs-lookup"><span data-stu-id="17272-280">Browse to the **StationCommands** node in the OPC UA server browser tree.</span></span>

2. <span data-ttu-id="17272-281">選擇您想要使用的命令。</span><span class="sxs-lookup"><span data-stu-id="17272-281">Choose the command that you wish use.</span></span>

3. <span data-ttu-id="17272-282">以滑鼠右鍵按一下節點。</span><span class="sxs-lookup"><span data-stu-id="17272-282">Right-click the node.</span></span>

4. <span data-ttu-id="17272-283">選擇 [呼叫]。</span><span class="sxs-lookup"><span data-stu-id="17272-283">Choose **Call**.</span></span>

    ![連線處理站預先設定的解決方案呼叫命令][cf-img-call-command]

5. <span data-ttu-id="17272-285">隨即顯示一個內容面板，告知您即將呼叫的方法以及適用的任何參數詳細資料。</span><span class="sxs-lookup"><span data-stu-id="17272-285">A context panel appears informing you which method you are about to call and any parameter details is applicable.</span></span>

6. <span data-ttu-id="17272-286">選擇 [呼叫]。</span><span class="sxs-lookup"><span data-stu-id="17272-286">Choose **Call**.</span></span>

    ![連線處理站預先設定的解決方案呼叫內容][cf-img-call-context]

7. <span data-ttu-id="17272-288">內容面板會進行更新，告知您方法呼叫成功。</span><span class="sxs-lookup"><span data-stu-id="17272-288">The context panel is updated to inform you that the method call succeeded.</span></span> <span data-ttu-id="17272-289">您可以讀取因為呼叫而更新的壓力節點值，藉此確認呼叫成功。</span><span class="sxs-lookup"><span data-stu-id="17272-289">You can verify the call succeeded by reading the value of the pressure node that updated as a result of the call.</span></span>

    ![連線處理站預先設定的解決方案呼叫成功][cf-img-call-success]


## <a name="behind-the-scenes"></a><span data-ttu-id="17272-291">在幕後</span><span class="sxs-lookup"><span data-stu-id="17272-291">Behind the scenes</span></span>

<span data-ttu-id="17272-292">當您部署預先設定的解決方案時，部署程序會在您選取的 Azure 訂用帳戶中建立多個資源。</span><span class="sxs-lookup"><span data-stu-id="17272-292">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="17272-293">您可以在 Azure [入口網站][lnk-portal]中檢視這些資源。</span><span class="sxs-lookup"><span data-stu-id="17272-293">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="17272-294">部署程序會建立 **資源群組** ，其名稱是以您為預先設定的解決方案選擇的名稱為基礎︰</span><span class="sxs-lookup"><span data-stu-id="17272-294">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Azure 入口網站中的預先設定解決方案][img-cf-portal]

<span data-ttu-id="17272-296">選取資源群組中的資源清單中的資源，即可檢視該資源的設定。</span><span class="sxs-lookup"><span data-stu-id="17272-296">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="17272-297">您也可以檢視預先設定的解決方案的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="17272-297">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="17272-298">連線處理站預先設定的解決方案原始程式碼位於 [azure-iot-connected-factory][lnk-cfgithub] GitHub 存放庫中：</span><span class="sxs-lookup"><span data-stu-id="17272-298">The connected factory preconfigured solution source code is in the [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="17272-299">完成之後，您可以從 [azureiotsuite.com][lnk-azureiotsuite] 網站上的 Azure 訂用帳戶中刪除預先設定解決方案。</span><span class="sxs-lookup"><span data-stu-id="17272-299">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="17272-300">這個網站可讓您輕鬆刪除在建立預先設定解決方案時已佈建的所有資源。</span><span class="sxs-lookup"><span data-stu-id="17272-300">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="17272-301">若要確保您刪除與預先設定解決方案相關的所有項目，請在 [azureiotsuite.com][lnk-azureiotsuite] 網站上進行刪除。</span><span class="sxs-lookup"><span data-stu-id="17272-301">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="17272-302">請勿刪除入口網站中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="17272-302">Do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17272-303">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17272-303">Next Steps</span></span>

<span data-ttu-id="17272-304">您現已部署運作中預先設定的解決方案，您可以繼續閱讀下列文章，了解如何開始使用 IoT 套件︰</span><span class="sxs-lookup"><span data-stu-id="17272-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="17272-305">[連線處理站預先設定的解決方案逐步解說][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="17272-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="17272-306">[將裝置連線至連線處理站預先設定的解決方案][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="17272-306">[Connect your device to the Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="17272-307">[azureiotsuite.com 網站的權限][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="17272-307">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md