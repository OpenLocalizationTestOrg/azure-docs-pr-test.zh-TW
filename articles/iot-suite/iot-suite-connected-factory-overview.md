---
title: "aaaAzure IoT 套件連線 factory 概觀 |Microsoft 文件"
description: "Hello Azure IoT 套件的描述連接工廠預先設定的解決方案。"
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
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="c58f7-103">開始使用 hello 連接工廠預先設定的解決方案</span><span class="sxs-lookup"><span data-stu-id="c58f7-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="c58f7-104">Azure IoT 套件[預先設定的解決方案][ lnk-preconfigured-solutions]結合多個 Azure IoT 服務 toodeliver 端對端方案實作常見的 IoT 商務案例。</span><span class="sxs-lookup"><span data-stu-id="c58f7-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="c58f7-105">hello*連接的工廠*預先設定的方案連接 tooand 監視您工業的裝置。</span><span class="sxs-lookup"><span data-stu-id="c58f7-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="c58f7-106">您可以使用 hello 方案 tooanalyze hello 資料資料流，從您的裝置和 toodrive 操作產能和獲利率。</span><span class="sxs-lookup"><span data-stu-id="c58f7-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="c58f7-107">此教學課程會示範如何 tooprovision hello 連接工廠預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="c58f7-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="c58f7-108">它也會引導您透過預先設定的 hello 解決方案的 hello 基本功能。</span><span class="sxs-lookup"><span data-stu-id="c58f7-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="c58f7-109">您可以存取這些功能從 hello 方案*儀表板*部署預先設定的 hello 方案的一部分：</span><span class="sxs-lookup"><span data-stu-id="c58f7-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![連線處理站預先設定的解決方案儀表板][img-cf-home]

<span data-ttu-id="c58f7-111">toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c58f7-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="c58f7-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c58f7-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c58f7-113">如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。</span><span class="sxs-lookup"><span data-stu-id="c58f7-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="c58f7-114">佈建 hello 方案</span><span class="sxs-lookup"><span data-stu-id="c58f7-114">Provision hello solution</span></span>

1. <span data-ttu-id="c58f7-115">登入 tooazureiotsuite.com 使用您的 Azure 帳戶的認證，然後按一下 「**+**"toocreate 方案。</span><span class="sxs-lookup"><span data-stu-id="c58f7-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="c58f7-116">按一下**選取**上 hello**連接的工廠**磚。</span><span class="sxs-lookup"><span data-stu-id="c58f7-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="c58f7-117">輸入連線處理站預先設定的解決方案的 [解決方案名稱]。</span><span class="sxs-lookup"><span data-stu-id="c58f7-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="c58f7-118">選取 hello**訂用帳戶**和**區域**希望 toouse tooprovision hello 方案。</span><span class="sxs-lookup"><span data-stu-id="c58f7-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="c58f7-119">按一下**建立方案**toobegin hello 佈建程序。</span><span class="sxs-lookup"><span data-stu-id="c58f7-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="c58f7-120">這個程序通常需要幾分鐘的時間 toorun。</span><span class="sxs-lookup"><span data-stu-id="c58f7-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="c58f7-121">當您等候佈建程序 toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="c58f7-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="c58f7-122">按一下具有您方案的 hello 磚**佈建**狀態。</span><span class="sxs-lookup"><span data-stu-id="c58f7-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="c58f7-123">請注意 hello**佈建狀態**您 Azure 訂用帳戶中部署 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="c58f7-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="c58f7-124">佈建完成之後，hello 狀態變更太**準備**。</span><span class="sxs-lookup"><span data-stu-id="c58f7-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="c58f7-125">按一下您的方案在 hello 右窗格中的 hello 磚 toosee hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c58f7-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="c58f7-126">如果您遇到部署預先設定的 hello 解決方案的問題，請檢閱[hello azureiotsuite.com 網站的權限][ lnk-permissions]和 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="c58f7-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="c58f7-127">如果 hello 問題仍然存在，則在 hello 上建立服務票證[入口網站][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="c58f7-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="c58f7-128">有 toosee 如預期般詳細資料，未列出您的解決方案嗎？</span><span class="sxs-lookup"><span data-stu-id="c58f7-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="c58f7-129">請在 [使用者心聲](https://feedback.azure.com/forums/321918-azure-iot)中提供功能建議給我們。</span><span class="sxs-lookup"><span data-stu-id="c58f7-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="c58f7-130">案例概觀</span><span class="sxs-lookup"><span data-stu-id="c58f7-130">Scenario overview</span></span>

<span data-ttu-id="c58f7-131">當您將部署連接的 hello factory 預先設定的解決方案，都會填入 toostep 透過常見的工業案例可讓您的資源。</span><span class="sxs-lookup"><span data-stu-id="c58f7-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="c58f7-132">在此案例中，數個處理站連接 hello 資料值的必要的 toocompute toohello 方案報表整體設備效率 (OEE) 和關鍵效能指標 (Kpi)。</span><span class="sxs-lookup"><span data-stu-id="c58f7-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="c58f7-133">hello 下列各節說明您如何以：</span><span class="sxs-lookup"><span data-stu-id="c58f7-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="c58f7-134">監視處理站、生產線、站區 OEE 和 KPI 值</span><span class="sxs-lookup"><span data-stu-id="c58f7-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="c58f7-135">分析產生從這些裝置使用 Azure 時間數列 Insights hello 遙測資料</span><span class="sxs-lookup"><span data-stu-id="c58f7-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="c58f7-136">處理警示 toofix 問題</span><span class="sxs-lookup"><span data-stu-id="c58f7-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="c58f7-137">此案例中的主要功能是可以執行所有這些動作從 hello 方案儀表板的遠端。</span><span class="sxs-lookup"><span data-stu-id="c58f7-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="c58f7-138">您不需要實際存取 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="c58f7-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="c58f7-139">檢視 hello 方案儀表板</span><span class="sxs-lookup"><span data-stu-id="c58f7-139">View hello solution dashboard</span></span>

<span data-ttu-id="c58f7-140">hello 方案儀表板可讓您 toomanage hello 部署方案。</span><span class="sxs-lookup"><span data-stu-id="c58f7-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="c58f7-141">它是全域處理站組態的階層式表示法。</span><span class="sxs-lookup"><span data-stu-id="c58f7-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="c58f7-142">例如，您可以檢視 OEE 和 KPI、針對遙測和動作警示發佈新節點。</span><span class="sxs-lookup"><span data-stu-id="c58f7-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="c58f7-143">當 hello 佈建已完成，且您預先設定的解決方案 hello 磚指出**準備**，選擇**啟動**tooopen 連接的工廠方案入口網站的新索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c58f7-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![啟動 hello 預先設定的解決方案][img-launch-solution]

1. <span data-ttu-id="c58f7-145">根據預設，hello 方案入口網站會顯示 hello*儀表板*。</span><span class="sxs-lookup"><span data-stu-id="c58f7-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="c58f7-146">toonavigate tooother 區域 hello 入口網站的左側 hello hello 頁面使用 hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="c58f7-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![連線處理站預先設定的解決方案儀表板][cf-img-menu]

<span data-ttu-id="c58f7-148">hello 儀表板會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="c58f7-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="c58f7-149">A **Factory 清單**hello 狀態、 位置以及目前 production 組態會顯示 hello 方案中的面板。</span><span class="sxs-lookup"><span data-stu-id="c58f7-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="c58f7-150">當您第一次執行 hello 方案時，有的模擬的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="c58f7-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="c58f7-151">hello 生產線模擬被由三個實際 OPC UA 每個伺服器產品線，執行模擬的工作，共用資料。</span><span class="sxs-lookup"><span data-stu-id="c58f7-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="c58f7-152">如需有關 OPC UA 的詳細資訊，請參閱 hello[連接工廠常見問題集](iot-suite-faq-cf.md)。</span><span class="sxs-lookup"><span data-stu-id="c58f7-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="c58f7-153">A**對應**顯示 hello 位置，每個裝置的連線 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="c58f7-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="c58f7-154">hello 解決方案可以使用 hello Bing Maps API tooplot 資訊 hello 地圖上。</span><span class="sxs-lookup"><span data-stu-id="c58f7-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="c58f7-155">如果您的訂用帳戶已啟用 Bing 地圖服務企業版 API，則會自動使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="c58f7-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="c58f7-156">如果沒有，請參閱 hello[常見問題集][ lnk-faq] toolearn toomake hello 對應動態的方式。</span><span class="sxs-lookup"><span data-stu-id="c58f7-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="c58f7-157">**警示**面板，可顯示遙測或 OEE/KPI 值超過特定閾值時所產生的警示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="c58f7-158">**設備的整體效率**顯示 hello 整個企業中或 hello 原廠生產環境的 hello OEE 值行/站台您正在檢視的面板。</span><span class="sxs-lookup"><span data-stu-id="c58f7-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="c58f7-159">這個值是從 hello 站台檢視 toohello 企業層級彙總。</span><span class="sxs-lookup"><span data-stu-id="c58f7-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="c58f7-160">hello OEE 圖和其組成的項目可以進一步分析。</span><span class="sxs-lookup"><span data-stu-id="c58f7-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="c58f7-161">**關鍵效能指標**面板會顯示 hello 數所產生的單位和 hello 整個企業或 hello factory/實際列所使用的能源 / 站台您正在檢視。</span><span class="sxs-lookup"><span data-stu-id="c58f7-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="c58f7-162">這些值會從站台檢視 toohello 企業層級彙總。</span><span class="sxs-lookup"><span data-stu-id="c58f7-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="c58f7-163">檢視工廠</span><span class="sxs-lookup"><span data-stu-id="c58f7-163">View factories</span></span>

<span data-ttu-id="c58f7-164">hello*工廠*面板顯示 hello hello 方案、 狀態，以及目前 production 組態中的所有 hello factory 的地理位置。</span><span class="sxs-lookup"><span data-stu-id="c58f7-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="c58f7-165">從 hello 位置清單中，您可以瀏覽 toohello hello 方案階層架構中的其他層級。</span><span class="sxs-lookup"><span data-stu-id="c58f7-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="c58f7-166">hello hello 清單中的資料列為連結 hello 生產線在該位置的詳細資料的超連結。</span><span class="sxs-lookup"><span data-stu-id="c58f7-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="c58f7-167">就可能 toodrill 到 hello 生產線詳細資料，並向 toohello 站台層級檢視。</span><span class="sxs-lookup"><span data-stu-id="c58f7-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="c58f7-168">您也可以套用篩選器 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="c58f7-168">You can also apply a filter toohello list.</span></span>

![連線處理站預先設定的解決方案處理站][cf-img-factories] 

1. <span data-ttu-id="c58f7-170">hello **Factory 面板**顯示 hello 這個解決方案的處理站清單。</span><span class="sxs-lookup"><span data-stu-id="c58f7-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="c58f7-171">hello factory 清單一開始會顯示六個 hello 佈建程序所建立的處理站。</span><span class="sxs-lookup"><span data-stu-id="c58f7-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="c58f7-172">您可以加入其他的虛擬和實體裝置 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="c58f7-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="c58f7-173">tooview hello 詳細資料，處理站，按一下 hello hello factory 清單中的資料列。</span><span class="sxs-lookup"><span data-stu-id="c58f7-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="c58f7-174">tooview hello 詳細資料的實際執行列中，按一下 hello hello 清單中的資料列。</span><span class="sxs-lookup"><span data-stu-id="c58f7-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="c58f7-175">tooview hello 發佈的站台 hello 生產線上的 OPC UA 節點時，按一下 hello hello 清單中的資料列。</span><span class="sxs-lookup"><span data-stu-id="c58f7-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="c58f7-176">tooview hello 站中的特定節點的詳細資訊，按一下 hello hello 清單中的資料列。</span><span class="sxs-lookup"><span data-stu-id="c58f7-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="c58f7-177">此動作會啟動具有時間數列 Insights 視覺效果的 hello 內容面板。</span><span class="sxs-lookup"><span data-stu-id="c58f7-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="c58f7-178">按一下這些圖形 toodo 進一步的分析 hello 時間數列 Insights 總管環境中。</span><span class="sxs-lookup"><span data-stu-id="c58f7-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="c58f7-179">檢視地圖</span><span class="sxs-lookup"><span data-stu-id="c58f7-179">View map</span></span>

<span data-ttu-id="c58f7-180">如果您的訂用帳戶有存取 toohello Bing Maps API，hello*工廠*地圖顯示您 hello 地理位置和狀態的所有 hello factory hello 方案中。</span><span class="sxs-lookup"><span data-stu-id="c58f7-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="c58f7-181">toodrill 到 hello 位置詳細資料，按一下 hello hello 地圖上顯示的位置。</span><span class="sxs-lookup"><span data-stu-id="c58f7-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![連線處理站預先設定的解決方案地圖][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="c58f7-183">檢視警示</span><span class="sxs-lookup"><span data-stu-id="c58f7-183">View alerts</span></span>

<span data-ttu-id="c58f7-184">hello**警示** 面板會顯示因為產生的警示 tooa 報告值或導出的 OEE/KPI 值超過設定的閾值。</span><span class="sxs-lookup"><span data-stu-id="c58f7-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="c58f7-185">此面板會顯示每個階層的層級 hello，從 hello 站台層級檢視 toohello 全域檢視警示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="c58f7-186">hello 警示包含 hello 警示、 日期、 時間、 位置和發生次數的描述。</span><span class="sxs-lookup"><span data-stu-id="c58f7-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="c58f7-187">您可以深入了 toohello 資料造成 hello 警示使用 hello 時間數列 Insights 資料。</span><span class="sxs-lookup"><span data-stu-id="c58f7-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="c58f7-188">資料以視覺化方式檢視中的 hello 時間數列 Insights hello 警示，在適用情況。</span><span class="sxs-lookup"><span data-stu-id="c58f7-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="c58f7-189">如果您是系統管理員，您可以執行預設動作 hello 警示，例如：</span><span class="sxs-lookup"><span data-stu-id="c58f7-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="c58f7-190">關閉 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-190">Close hello alert.</span></span>
* <span data-ttu-id="c58f7-191">了解 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="c58f7-192">您可以選擇性地採取更複雜的動作。</span><span class="sxs-lookup"><span data-stu-id="c58f7-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="c58f7-193">例如，對於 hello 不足的壓力 OPC UA 節點 hello 組件，您可以：</span><span class="sxs-lookup"><span data-stu-id="c58f7-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="c58f7-194">在新的瀏覽器視窗中的網頁顯示支援資訊。</span><span class="sxs-lookup"><span data-stu-id="c58f7-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="c58f7-195">降低 hello 警示原因的 hello OPC UA 方法呼叫 hello 裝置上。</span><span class="sxs-lookup"><span data-stu-id="c58f7-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="c58f7-196">隱藏 hello 可用性的 hello 預設動作。</span><span class="sxs-lookup"><span data-stu-id="c58f7-196">Suppress hello availability of hello default actions.</span></span>

    ![連線處理站預先設定的解決方案警示][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="c58f7-198">這些警示在預先設定的 hello 方案中的組態檔中指定的規則所產生。</span><span class="sxs-lookup"><span data-stu-id="c58f7-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="c58f7-199">這些規則 hello OEE 或 OPC UA 節點值或 KPI 圖形已超過設定的閾值時產生警示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="c58f7-200">hello**警示面板**顯示 hello 這個方案中產生的警示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="c58f7-201">tooview hello 詳細資料的警示，按一下 hello 警示面板中的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="c58f7-202">toofurther 分析 hello 警示的資料，請按一下 hello 警示面板 tooopen hello 時間數列 Insights 總管環境中的 hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="c58f7-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="c58f7-203">tooaddress hello 警示，hello 警示面板中使用數個動作。</span><span class="sxs-lookup"><span data-stu-id="c58f7-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="c58f7-204">選擇 hello 適當的選項，然後按一下 hello 執行動作的命令按鈕。</span><span class="sxs-lookup"><span data-stu-id="c58f7-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="c58f7-205">檢視整體設備效率</span><span class="sxs-lookup"><span data-stu-id="c58f7-205">View overall equipment efficiency</span></span>

<span data-ttu-id="c58f7-206">OEE 率 hello hello 製造程序使用索引鍵與實際執行相關作業參數的效率。</span><span class="sxs-lookup"><span data-stu-id="c58f7-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="c58f7-207">OEE 是一套的業界標準的量值計算而乘以 hello 可用性率、 效能速度及品質速率： OEE = x 效能品質的可用性。</span><span class="sxs-lookup"><span data-stu-id="c58f7-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![連線處理站預先設定的解決方案 OEE][cf-img-oee]

1. <span data-ttu-id="c58f7-209">tooview OEE hello 階層中的任何層級瀏覽 toohello 您需要的特定檢視。</span><span class="sxs-lookup"><span data-stu-id="c58f7-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="c58f7-210">hello OEE 適用於該檢視會顯示 hello 面板，以及每個構成 hello OEE 百分比 hello 項目中。</span><span class="sxs-lookup"><span data-stu-id="c58f7-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="c58f7-211">toofurther 分析 hello OEE hello 階層資料中的任何層級，請按一下 hello OEE、 可用性、 效能或品質百分比。</span><span class="sxs-lookup"><span data-stu-id="c58f7-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="c58f7-212">內容面板會顯示時間序列 Insights 供電的視覺效果顯示 hello 過去一小時、 過去 24 小時和過去 7 天的資料。</span><span class="sxs-lookup"><span data-stu-id="c58f7-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![連線處理站預先設定的解決方案 TSI 視覺效果][cf-img-tsi-visualization]

3. <span data-ttu-id="c58f7-214">toofurther 分析 hello 警示的資料，請按一下 hello 警示面板中的 hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="c58f7-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="c58f7-215">這個動作會開啟 hello 時間數列 Insights 總管環境。</span><span class="sxs-lookup"><span data-stu-id="c58f7-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![連線處理站預先設定的解決方案 TSI 總管][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="c58f7-217">檢視關鍵效能指標</span><span class="sxs-lookup"><span data-stu-id="c58f7-217">View Key Performance Indicators</span></span>

<span data-ttu-id="c58f7-218">hello 解決方案提供兩個關鍵效能指標，*每小時的單位*和*能源使用 kwh*。</span><span class="sxs-lookup"><span data-stu-id="c58f7-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![連線處理站預先設定的解決方案 KPI][cf-img-kpi]

1. <span data-ttu-id="c58f7-220">每個小時或用於 hello 階層中的任何層級的能源 tooview 單位瀏覽 toohello 您需要的特定檢視。</span><span class="sxs-lookup"><span data-stu-id="c58f7-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="c58f7-221">hello 單位，每個小時和能源使用顯示在 [hello] 面板。</span><span class="sxs-lookup"><span data-stu-id="c58f7-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="c58f7-222">每個小時或用於進一步，hello 階層中的任何層級的能源 tooanalyze 單位按一下 hello 量測計中 hello**關鍵效能指標**面板。</span><span class="sxs-lookup"><span data-stu-id="c58f7-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="c58f7-223">內容面板隨即出現，並讓您從 hello 過去一小時、 過去 24 小時，以及過去 7 天的 hello tooview 資料的時間序列 Insights 電源視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c58f7-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="c58f7-224">案例檢閱</span><span class="sxs-lookup"><span data-stu-id="c58f7-224">Scenario review</span></span>

<span data-ttu-id="c58f7-225">在此案例中，您可以監視您處理站 OEE 和 Kpi 的值，hello 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="c58f7-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="c58f7-226">您則用於時間序列 Insights tooprovide 詳細資訊 toohelp 鑽研進一步 hello 遙測資料 OEE 和 Kpi toohelp 以偵測異常狀況。</span><span class="sxs-lookup"><span data-stu-id="c58f7-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="c58f7-227">您也會與您處理站使用 hello 警示面板 tooview 問題，而且您使用 hello 動作可用 tooyou tooresolve hello 警示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="c58f7-228">其他功能</span><span class="sxs-lookup"><span data-stu-id="c58f7-228">Other features</span></span>

<span data-ttu-id="c58f7-229">hello 下列各節說明一些其他功能 hello 連接工廠解決方案的 hello 前一個案例中未描述。</span><span class="sxs-lookup"><span data-stu-id="c58f7-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="c58f7-230">套用篩選條件</span><span class="sxs-lookup"><span data-stu-id="c58f7-230">Apply filters</span></span>

1. <span data-ttu-id="c58f7-231">按一下 hello **> 形箭號**toodisplay hello factory 位置面板或 hello 警示面板中可用的篩選器的清單。</span><span class="sxs-lookup"><span data-stu-id="c58f7-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="c58f7-232">hello 篩選面板會顯示您。</span><span class="sxs-lookup"><span data-stu-id="c58f7-232">hello filters panel is displayed for you.</span></span> 

    ![連線處理站預先設定的解決方案篩選條件][cf-img-alert-filter]

3. <span data-ttu-id="c58f7-234">選擇您需要的 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="c58f7-234">Choose hello filter that you require.</span></span> <span data-ttu-id="c58f7-235">它也是可能 tootype hello 篩選欄位中的任意文字。</span><span class="sxs-lookup"><span data-stu-id="c58f7-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="c58f7-236">然後您套用 hello 篩選。</span><span class="sxs-lookup"><span data-stu-id="c58f7-236">hello filter is then applied for you.</span></span> <span data-ttu-id="c58f7-237">漏斗圖，顯示 hello 工廠中並且會提醒資料表透過 hello 儀表板中，也會顯示 hello 篩選狀態。</span><span class="sxs-lookup"><span data-stu-id="c58f7-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![連線處理站預先設定的解決方案篩選條件][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="c58f7-239">使用中的篩選器不會影響顯示 hello OEE 和 KPI 的值，它只篩選 hello 列出內容。</span><span class="sxs-lookup"><span data-stu-id="c58f7-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="c58f7-240">tooclear 篩選中，按一下 hello 漏斗圖，然後按一下 hello 篩選內容面板中的篩選器。</span><span class="sxs-lookup"><span data-stu-id="c58f7-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="c58f7-241">hello 文字**所有**會顯示在 hello 處理站，並發出警示的資料表。</span><span class="sxs-lookup"><span data-stu-id="c58f7-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="c58f7-242">瀏覽 OPC UA 伺服器</span><span class="sxs-lookup"><span data-stu-id="c58f7-242">Browse an OPC UA server</span></span>

<span data-ttu-id="c58f7-243">當您部署預先設定的 hello 方案時，您會自動佈建模擬的 OPC UA 伺服器，您可以透過 hello 方案瀏覽器瀏覽。</span><span class="sxs-lookup"><span data-stu-id="c58f7-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="c58f7-244">這些伺服器是「模擬的 OPC UA 伺服器」。</span><span class="sxs-lookup"><span data-stu-id="c58f7-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="c58f7-245">模擬的伺服器輕易地為您 tooexperiment 與 hello 預先設定的方案而無須與 hello 需要 toodeploy 真正的實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="c58f7-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="c58f7-246">如果您想 tooconnect 真實世界的 OPC UA 伺服器 toohello 解決方案，請參閱 hello[連接 OPC UA 裝置連線的 toohello 預先設定的處理站解決方案][ lnk-connect-cf]教學課程。</span><span class="sxs-lookup"><span data-stu-id="c58f7-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="c58f7-247">按一下 hello **factory 圖示**hello 儀表板導覽列中。</span><span class="sxs-lookup"><span data-stu-id="c58f7-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![連線處理站預先設定的解決方案伺服器瀏覽器][cf-img-server-browser]

2. <span data-ttu-id="c58f7-249">從 hello 預先設定的清單中選擇其中一個 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c58f7-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="c58f7-250">此清單會顯示為您部署預先設定的 hello 方案中的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c58f7-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![連線處理站預先設定的解決方案伺服器選取][cf-img-server-choice]

3. <span data-ttu-id="c58f7-252">按一下 [連線]，[安全性] 對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="c58f7-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="c58f7-253">Hello 模擬對於安全 tooclick**繼續**</span><span class="sxs-lookup"><span data-stu-id="c58f7-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="c58f7-254">tooexpand hello 節點 hello 伺服器樹狀目錄中，按一下它。</span><span class="sxs-lookup"><span data-stu-id="c58f7-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="c58f7-255">正在發佈遙測的節點旁邊有勾號。</span><span class="sxs-lookup"><span data-stu-id="c58f7-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![連線處理站預先設定的解決方案伺服器樹狀目錄][cf-img-server-tree]

5. <span data-ttu-id="c58f7-257">以滑鼠右鍵按一下項目 tooread、 撰寫、 發行或呼叫該節點。</span><span class="sxs-lookup"><span data-stu-id="c58f7-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="c58f7-258">hello 動作可用 tooyou 取決於您的權限和 hello 節點的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="c58f7-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="c58f7-259">hello 讀取選項 toodisplays 內容面板顯示 hello 的 hello 特定節點的值。</span><span class="sxs-lookup"><span data-stu-id="c58f7-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="c58f7-260">hello 撰寫選項顯示的內容面板，您可以在此輸入新值。</span><span class="sxs-lookup"><span data-stu-id="c58f7-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="c58f7-261">hello 呼叫選項可顯示的節點，您可以在其中輸入 hello 呼叫 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="c58f7-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="c58f7-262">發佈節點</span><span class="sxs-lookup"><span data-stu-id="c58f7-262">Publish a node</span></span>

<span data-ttu-id="c58f7-263">當您瀏覽*模擬的 OPC UA 伺服器*，您也可以選擇 toopublish 新節點。</span><span class="sxs-lookup"><span data-stu-id="c58f7-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="c58f7-264">您可以分析這些節點 hello 方案中的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="c58f7-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="c58f7-265">這些*模擬 OPC UA 伺服器*讓它與 hello 預先設定的解決方案容易 tooexperiment 而不需部署實際的實體裝置。</span><span class="sxs-lookup"><span data-stu-id="c58f7-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="c58f7-266">瀏覽 tooa hello 想 toopublish 的 OPC UA 伺服器瀏覽器樹狀目錄中的節點。</span><span class="sxs-lookup"><span data-stu-id="c58f7-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="c58f7-267">以滑鼠右鍵按一下 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="c58f7-267">Right-click hello node.</span></span>

3. <span data-ttu-id="c58f7-268">選擇 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="c58f7-268">Choose **Publish**.</span></span>

    ![連線的處理站發佈節點][cf-img-publish-node]

4. <span data-ttu-id="c58f7-270">這會告訴您 hello 發行內容面板會顯示已成功。</span><span class="sxs-lookup"><span data-stu-id="c58f7-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="c58f7-271">hello 節點會出現在它旁邊的核取記號 hello 站台層級檢視。</span><span class="sxs-lookup"><span data-stu-id="c58f7-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![連線處理站預先設定的解決方案發佈成功][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="c58f7-273">命令與控制</span><span class="sxs-lookup"><span data-stu-id="c58f7-273">Command and control</span></span>

<span data-ttu-id="c58f7-274">命令，並控制您直接從 hello 雲端的業界裝置，可讓 hello 連線的 factory。</span><span class="sxs-lookup"><span data-stu-id="c58f7-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="c58f7-275">您可以使用此功能 toorespond tooalerts hello 裝置所產生。</span><span class="sxs-lookup"><span data-stu-id="c58f7-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="c58f7-276">例如，您可以傳送命令 toohello 裝置從 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="c58f7-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="c58f7-277">您可以找到 hello 可用命令 hello **StationCommands** hello OPC UA 伺服器瀏覽器樹狀目錄中的節點。</span><span class="sxs-lookup"><span data-stu-id="c58f7-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="c58f7-278">在此案例中，您可以開啟不足的壓力發行閥 hello 生產環境中的行慕尼黑的組件站台上。</span><span class="sxs-lookup"><span data-stu-id="c58f7-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="c58f7-279">toouse hello 命令和控制功能，您必須在 hello**管理員**hello 角色預先設定的方案部署。</span><span class="sxs-lookup"><span data-stu-id="c58f7-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="c58f7-280">瀏覽 toohello **StationCommands** hello OPC UA 伺服器瀏覽器樹狀目錄中的節點。</span><span class="sxs-lookup"><span data-stu-id="c58f7-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="c58f7-281">選擇您想使用 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="c58f7-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="c58f7-282">以滑鼠右鍵按一下 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="c58f7-282">Right-click hello node.</span></span>

4. <span data-ttu-id="c58f7-283">選擇 [呼叫]。</span><span class="sxs-lookup"><span data-stu-id="c58f7-283">Choose **Call**.</span></span>

    ![連線處理站預先設定的解決方案呼叫命令][cf-img-call-command]

5. <span data-ttu-id="c58f7-285">內容面板會出現告知您哪一種方法您即將 toocall 和任何參數的詳細資料不適用。</span><span class="sxs-lookup"><span data-stu-id="c58f7-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="c58f7-286">選擇 [呼叫]。</span><span class="sxs-lookup"><span data-stu-id="c58f7-286">Choose **Call**.</span></span>

    ![連線處理站預先設定的解決方案呼叫內容][cf-img-call-context]

7. <span data-ttu-id="c58f7-288">hello 內容面板會更新的 tooinform 您 hello 方法呼叫成功。</span><span class="sxs-lookup"><span data-stu-id="c58f7-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="c58f7-289">您可以確認 hello 呼叫成功讀取 hello hello 不足的壓力節點更新 hello 呼叫的結果值。</span><span class="sxs-lookup"><span data-stu-id="c58f7-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![連線處理站預先設定的解決方案呼叫成功][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="c58f7-291">Hello 幕後</span><span class="sxs-lookup"><span data-stu-id="c58f7-291">Behind hello scenes</span></span>

<span data-ttu-id="c58f7-292">當您部署預先設定的解決方案時，hello 部署程序會在 hello 您選取的 Azure 訂用帳戶中建立多個資源。</span><span class="sxs-lookup"><span data-stu-id="c58f7-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="c58f7-293">您可以檢視這些資源中 hello Azure[入口網站][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="c58f7-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="c58f7-294">hello 部署程序會建立**資源群組**根據您選擇您預先設定的解決方案 hello 名稱的名稱：</span><span class="sxs-lookup"><span data-stu-id="c58f7-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Hello Azure 入口網站中預先設定的解決方案][img-cf-portal]

<span data-ttu-id="c58f7-296">您可以檢視每個資源的 hello 設定 hello 資源群組中的 hello 清單中選取。</span><span class="sxs-lookup"><span data-stu-id="c58f7-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="c58f7-297">您也可以檢視預先設定的 hello 方案 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="c58f7-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="c58f7-298">hello 預先設定連接的工廠方案原始程式碼處於 hello [azure-iot-連線-原廠][ lnk-cfgithub] GitHub 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="c58f7-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="c58f7-299">完成之後，您可以從您的 Azure 訂閱 hello 上刪除 hello 預先設定的解決方案[azureiotsuite.com] [ lnk-azureiotsuite]站台。</span><span class="sxs-lookup"><span data-stu-id="c58f7-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="c58f7-300">此站台可讓您 tooeasily 刪除所有 hello 當您建立預先設定的 hello 方案已佈建的資源。</span><span class="sxs-lookup"><span data-stu-id="c58f7-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="c58f7-301">刪除所有項目 tooensure 相關 toohello 預先設定的解決方案，刪除上 hello [azureiotsuite.com] [ lnk-azureiotsuite]站台。</span><span class="sxs-lookup"><span data-stu-id="c58f7-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="c58f7-302">請勿刪除 hello hello 入口網站中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c58f7-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c58f7-303">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c58f7-303">Next Steps</span></span>

<span data-ttu-id="c58f7-304">既然您已部署預先設定的有效的解決方案，您可以繼續閱讀下列文章 hello 入門 IoT 套件：</span><span class="sxs-lookup"><span data-stu-id="c58f7-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="c58f7-305">[連線處理站預先設定的解決方案逐步解說][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="c58f7-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="c58f7-306">[連接裝置 toohello 預先設定連接的工廠解決方案][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="c58f7-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="c58f7-307">[Hello azureiotsuite.com 網站的權限][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="c58f7-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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