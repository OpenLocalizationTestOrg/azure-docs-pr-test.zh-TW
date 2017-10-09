---
title: "開始使用 aaaGet 預先設定的解決方案 |Microsoft 文件"
description: "請遵循此教學課程 toolearn toodeploy Azure IoT 套件預先方案的設定。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="50ec7-103">開始使用預先設定的 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="50ec7-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="50ec7-104">Azure IoT 套件[預先設定的解決方案][ lnk-preconfigured-solutions]結合多個 Azure IoT 服務 toodeliver 端對端方案實作常見的 IoT 商務案例。</span><span class="sxs-lookup"><span data-stu-id="50ec7-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="50ec7-105">hello*遠端監視*預先設定的方案連接 tooand 監視您的裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="50ec7-106">您可以藉由自動回應 toothat 的資料流的處理序使用 hello 方案 tooanalyze hello 資料資料流，從您的裝置和 tooimprove 業務的結果。</span><span class="sxs-lookup"><span data-stu-id="50ec7-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="50ec7-107">本教學課程會示範如何 tooprovision hello 遠端監視預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="50ec7-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="50ec7-108">它也會引導您透過預先設定的 hello 解決方案的 hello 基本功能。</span><span class="sxs-lookup"><span data-stu-id="50ec7-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="50ec7-109">您可以存取這些功能從 hello 方案*儀表板*部署預先設定的 hello 方案的一部分：</span><span class="sxs-lookup"><span data-stu-id="50ec7-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![遠端監視預先設定解決方案儀表板][img-dashboard]

<span data-ttu-id="50ec7-111">toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ec7-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="50ec7-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ec7-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="50ec7-113">如需詳細資訊，請參閱 [Azure 免費試用][lnk_free_trial]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="50ec7-114">案例概觀</span><span class="sxs-lookup"><span data-stu-id="50ec7-114">Scenario overview</span></span>

<span data-ttu-id="50ec7-115">當您部署的 hello 遠端監視預先設定的解決方案時，它會預先填入資源，可讓您 toostep 透過常見的遠端監視案例。</span><span class="sxs-lookup"><span data-stu-id="50ec7-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="50ec7-116">在此案例中，數個裝置連線的 toohello 方案報告未預期的溫度值。</span><span class="sxs-lookup"><span data-stu-id="50ec7-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="50ec7-117">hello 下列各節說明您如何以：</span><span class="sxs-lookup"><span data-stu-id="50ec7-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="50ec7-118">識別 hello 裝置傳送未預期的溫度值。</span><span class="sxs-lookup"><span data-stu-id="50ec7-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="50ec7-119">設定這些裝置 toosend 更多詳細的遙測。</span><span class="sxs-lookup"><span data-stu-id="50ec7-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="50ec7-120">透過更新這些裝置上的 hello 韌體中修正 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="50ec7-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="50ec7-121">請確認您的動作已解析 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="50ec7-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="50ec7-122">此案例中的主要功能是可以執行所有這些動作從 hello 方案儀表板的遠端。</span><span class="sxs-lookup"><span data-stu-id="50ec7-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="50ec7-123">您不需要實際存取 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="50ec7-124">檢視 hello 方案儀表板</span><span class="sxs-lookup"><span data-stu-id="50ec7-124">View hello solution dashboard</span></span>

<span data-ttu-id="50ec7-125">hello 方案儀表板可讓您 toomanage hello 部署方案。</span><span class="sxs-lookup"><span data-stu-id="50ec7-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="50ec7-126">例如，您可以檢視遙測、新增裝置及設定規則。</span><span class="sxs-lookup"><span data-stu-id="50ec7-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="50ec7-127">當 hello 佈建已完成，且您預先設定的解決方案 hello 磚指出**準備**，選擇**啟動**tooopen 遠端監視方案入口網站中的新索引標籤。</span><span class="sxs-lookup"><span data-stu-id="50ec7-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![啟動 hello 預先設定的解決方案][img-launch-solution]

1. <span data-ttu-id="50ec7-129">根據預設，hello 方案入口網站會顯示 hello*儀表板*。</span><span class="sxs-lookup"><span data-stu-id="50ec7-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="50ec7-130">您可以瀏覽 tooother hello 方案入口網站左側 hello hello 頁面使用 hello 功能表區域。</span><span class="sxs-lookup"><span data-stu-id="50ec7-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![遠端監視預先設定解決方案儀表板][img-menu]

<span data-ttu-id="50ec7-132">hello 儀表板會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="50ec7-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="50ec7-133">顯示每個裝置 hello 位置的地圖，連接 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="50ec7-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="50ec7-134">當您第一次執行 hello 方案時，有 25 個模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="50ec7-135">hello 模擬的裝置都會實作為 Azure WebJobs 而且 hello 解決方案使用 hello Bing Maps API tooplot 資訊 hello 地圖上。</span><span class="sxs-lookup"><span data-stu-id="50ec7-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="50ec7-136">請參閱 hello[常見問題集][ lnk-faq] toolearn toomake hello 對應動態的方式。</span><span class="sxs-lookup"><span data-stu-id="50ec7-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="50ec7-137">[遙測歷程記錄] 面板會從所選的裝置繪製近乎即時的溼度和溫度遙測，並顯示彙總資料，例如最大、最小和平均溼度。</span><span class="sxs-lookup"><span data-stu-id="50ec7-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="50ec7-138">[警示歷程記錄] 面板會在遙測值超過臨界值時顯示最近的警示事件。</span><span class="sxs-lookup"><span data-stu-id="50ec7-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="50ec7-139">建立預先設定的 hello 解決方案加法 toohello 範例中，您可以定義您自己的警示。</span><span class="sxs-lookup"><span data-stu-id="50ec7-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="50ec7-140">[作業] 面板顯示已排程作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="50ec7-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="50ec7-141">您可以在 [管理作業] 頁面排程您自己的作業。</span><span class="sxs-lookup"><span data-stu-id="50ec7-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="50ec7-142">檢視警示</span><span class="sxs-lookup"><span data-stu-id="50ec7-142">View alarms</span></span>

<span data-ttu-id="50ec7-143">hello 警示歷程記錄面板會顯示五個裝置會比預期的遙測值更高的報告。</span><span class="sxs-lookup"><span data-stu-id="50ec7-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Hello 方案儀表板上的 TODO 警示歷程記錄][img-alarms]

> [!NOTE]
> <span data-ttu-id="50ec7-145">包含在預先設定的 hello 方案中的規則會產生這些警示。</span><span class="sxs-lookup"><span data-stu-id="50ec7-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="50ec7-146">當裝置傳送嗨溫度值超過 60 時，此規則會產生警示。</span><span class="sxs-lookup"><span data-stu-id="50ec7-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="50ec7-147">您可以選擇定義您自己的規則和動作[規則](#add-a-rule)和[動作](#add-an-action)hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="50ec7-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="50ec7-148">檢視裝置</span><span class="sxs-lookup"><span data-stu-id="50ec7-148">View devices</span></span>

<span data-ttu-id="50ec7-149">hello*裝置*清單會顯示所有已註冊的 hello 裝置 hello 方案中。</span><span class="sxs-lookup"><span data-stu-id="50ec7-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="50ec7-150">Hello 裝置清單中，您可以檢視和編輯裝置中繼資料、 新增或移除裝置，並叫用在裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="50ec7-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="50ec7-151">您可以篩選和排序 hello hello 裝置清單中的裝置清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="50ec7-152">您也可以自訂 hello hello 裝置清單中顯示的資料行。</span><span class="sxs-lookup"><span data-stu-id="50ec7-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="50ec7-153">選擇**裝置**tooshow hello 裝置清單，此解決方案。</span><span class="sxs-lookup"><span data-stu-id="50ec7-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Hello 方案入口網站中檢視 hello 裝置清單][img-devicelist]

1. <span data-ttu-id="50ec7-155">hello 裝置清單一開始會顯示 hello 佈建程序所建立的 25 個模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="50ec7-156">您可以加入其他的虛擬和實體裝置 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="50ec7-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="50ec7-157">tooview hello 詳細資料的裝置 hello 裝置清單中選擇裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Hello 方案入口網站中檢視 hello 裝置詳細資料][img-devicedetails]

<span data-ttu-id="50ec7-159">hello**裝置詳細資料**面板包含六個區段：</span><span class="sxs-lookup"><span data-stu-id="50ec7-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="50ec7-160">啟用您 toocustomize hello 裝置圖示、 停用裝置 hello、 加入規則，叫用方法，或傳送命令的連結集合。</span><span class="sxs-lookup"><span data-stu-id="50ec7-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="50ec7-161">如需命令 (裝置對雲端的訊息) 和方法 (直接方法) 的比較，請參閱[雲端對裝置的通訊指引][lnk-c2d-guidance]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="50ec7-162">hello**裝置兩個-標記**區段可讓您的裝置 hello tooedit 標記值。</span><span class="sxs-lookup"><span data-stu-id="50ec7-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="50ec7-163">您可以在 hello 裝置清單中顯示標記值，並使用標記值 toofilter hello 裝置清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="50ec7-164">hello**裝置兩個-需要屬性**區段可讓您 tooset 屬性值傳送 toobe toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="50ec7-165">hello**裝置兩個-報告屬性**區段會顯示傳送嗨裝置的屬性值。</span><span class="sxs-lookup"><span data-stu-id="50ec7-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="50ec7-166">hello**裝置屬性**> 一節顯示的資訊，例如 hello 裝置 hello 身分識別登錄從金鑰識別碼和驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="50ec7-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="50ec7-167">hello**最近工作**區段會顯示最近鎖定此裝置的任何工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="50ec7-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="50ec7-168">篩選器 hello 裝置清單</span><span class="sxs-lookup"><span data-stu-id="50ec7-168">Filter hello device list</span></span>

<span data-ttu-id="50ec7-169">您可以使用篩選器 toodisplay 只有傳送未預期的溫度值的裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="50ec7-170">hello 遠端監視預先設定的解決方案包括 hello**狀況不良的裝置**篩選 tooshow 裝置平均的溫度值大於 60。</span><span class="sxs-lookup"><span data-stu-id="50ec7-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="50ec7-171">您也可以[建立自己的篩選](#add-a-filter)。</span><span class="sxs-lookup"><span data-stu-id="50ec7-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="50ec7-172">選擇**開啟已儲存的篩選器**toodisplay 可用的篩選器的清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="50ec7-173">然後選擇 **狀況不良的裝置**tooapply hello 篩選：</span><span class="sxs-lookup"><span data-stu-id="50ec7-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![顯示 hello 篩選清單][img-unhealthy-filter]

1. <span data-ttu-id="50ec7-175">hello 裝置清單現在會顯示只有裝置平均的溫度值大於 60。</span><span class="sxs-lookup"><span data-stu-id="50ec7-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![檢視 hello 篩選過的裝置清單，顯示處於狀況不良的裝置][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="50ec7-177">更新所需屬性</span><span class="sxs-lookup"><span data-stu-id="50ec7-177">Update desired properties</span></span>

<span data-ttu-id="50ec7-178">您現在已識別一組裝置，可能需要修復。</span><span class="sxs-lookup"><span data-stu-id="50ec7-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="50ec7-179">不過，您可以決定 hello 資料頻率為 15 秒是不夠的清除 hello 問題的診斷。</span><span class="sxs-lookup"><span data-stu-id="50ec7-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="50ec7-180">您有多個資料點 toobetter 變更 hello 遙測頻率 toofive 秒 tooprovide 診斷 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="50ec7-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="50ec7-181">您可以將這個組態變更 tooyour 遠端裝置從 hello 方案入口網站。</span><span class="sxs-lookup"><span data-stu-id="50ec7-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="50ec7-182">您可以進行 hello 變更一次，評估 hello 影響，並接著處理 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="50ec7-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="50ec7-183">請遵循這些步驟 toorun 變更 hello 作業**TelemetryInterval**預期 hello 受影響裝置的屬性。</span><span class="sxs-lookup"><span data-stu-id="50ec7-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="50ec7-184">當 hello 裝置收到 hello 新**TelemetryInterval**屬性值，變更其組態 toosend 遙測每隔五秒而不是每隔 15 秒：</span><span class="sxs-lookup"><span data-stu-id="50ec7-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="50ec7-185">雖然您會在 hello 裝置清單中顯示的狀況不良的裝置 hello 清單，選擇 **作業排程器**，然後**編輯裝置兩個**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="50ec7-186">呼叫 hello 作業**變更遙測間隔**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="50ec7-187">變更 hello hello 值**所需的屬性**名稱**所需。Config.TelemetryInterval** toofive 秒。</span><span class="sxs-lookup"><span data-stu-id="50ec7-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="50ec7-188">選擇 [排程]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-188">Choose **Schedule**.</span></span>

    ![變更 hello TelemetryInterval 屬性 toofive 秒][img-change-interval]

1. <span data-ttu-id="50ec7-190">您可以監視 hello 作業上 hello hello 進度**管理作業**hello 入口網站頁面中的。</span><span class="sxs-lookup"><span data-stu-id="50ec7-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="50ec7-191">如果您想要個別裝置 toochange 所需的屬性值，使用 hello**所需的屬性**> 一節中 hello**裝置詳細資料**面板而不是執行作業。</span><span class="sxs-lookup"><span data-stu-id="50ec7-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="50ec7-192">這項作業設定 hello hello 值**TelemetryInterval**預期在 hello 裝置兩個屬性的所有 hello hello 篩選所選取的裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="50ec7-193">hello 裝置從 hello 裝置兩個擷取這個值，並更新其行為。</span><span class="sxs-lookup"><span data-stu-id="50ec7-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="50ec7-194">當裝置擷取，並處理從裝置的兩個所需的屬性時，它會設定 hello 對應回報的值屬性。</span><span class="sxs-lookup"><span data-stu-id="50ec7-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="50ec7-195">叫用方法</span><span class="sxs-lookup"><span data-stu-id="50ec7-195">Invoke methods</span></span>

<span data-ttu-id="50ec7-196">Hello 工作執行時，您會注意到在 hello 狀況不良的裝置清單中所有這些裝置具有舊 （早於 1.6 版） 韌體版本。</span><span class="sxs-lookup"><span data-stu-id="50ec7-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![檢視 hello 回報 hello 狀況不良的裝置的韌體版本][img-old-firmware]

<span data-ttu-id="50ec7-198">此韌體版本可能會非預期的 hello hello 根本原因的溫度值，因為您知道其他狀況良好的裝置已最近更新的 tooversion 2.0。</span><span class="sxs-lookup"><span data-stu-id="50ec7-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="50ec7-199">您可以使用內建的 hello**舊的韌體裝置**篩選 tooidentify 舊的韌體版本與任何裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="50ec7-200">從 hello 入口網站，然後您可以從遠端更新所有 hello 裝置仍在執行舊的韌體版本：</span><span class="sxs-lookup"><span data-stu-id="50ec7-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="50ec7-201">選擇**開啟已儲存的篩選器**toodisplay 可用的篩選器的清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="50ec7-202">然後選擇 **舊的韌體裝置**tooapply hello 篩選：</span><span class="sxs-lookup"><span data-stu-id="50ec7-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![顯示 hello 篩選清單][img-old-filter]

1. <span data-ttu-id="50ec7-204">hello 裝置清單現在會顯示只使用舊的韌體版本的裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="50ec7-205">這份清單包括 hello 五個裝置由 hello**狀況不良的裝置**篩選器和三個額外的裝置：</span><span class="sxs-lookup"><span data-stu-id="50ec7-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![檢視 hello 篩選過的裝置清單，顯示舊的裝置][img-filtered-old-list]

1. <span data-ttu-id="50ec7-207">選擇 [作業排程器]，然後選擇 [叫用方法]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="50ec7-208">設定**工作名稱**太**韌體更新 tooversion 2.0**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="50ec7-209">選擇**InitiateFirmwareUpdate**為 hello**方法**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="50ec7-210">設定 hello **FwPackageUri**參數太**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="50ec7-211">選擇 [排程]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-211">Choose **Schedule**.</span></span> <span data-ttu-id="50ec7-212">hello 作業 toorun 現在 hello 預設值為。</span><span class="sxs-lookup"><span data-stu-id="50ec7-212">hello default is for hello job toorun now.</span></span>

    ![建立工作 tooupdate hello 韌體的 hello 選取裝置][img-method-update]

> [!NOTE]
> <span data-ttu-id="50ec7-214">如果您想 tooinvoke 個別的裝置上的方法，請選擇**方法**在 hello**裝置詳細資料**面板而不是執行作業。</span><span class="sxs-lookup"><span data-stu-id="50ec7-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="50ec7-215">這項作業會叫用 hello **InitiateFirmwareUpdate**直接 hello 篩選所選取的所有 hello 裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="50ec7-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="50ec7-216">裝置立即回應 tooIoT 集線器，然後以非同步方式啟動 hello 韌體更新程序。</span><span class="sxs-lookup"><span data-stu-id="50ec7-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="50ec7-217">hello 下列螢幕擷取畫面所示，hello 裝置會提供有關 hello 韌體更新程序，透過報告的屬性值，狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="50ec7-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="50ec7-218">選擇 hello**重新整理**hello 裝置和工作清單中的圖示 tooupdate hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="50ec7-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="50ec7-219">![工作清單會顯示 hello 韌體更新清單執行][img-update-1]
![顯示韌體更新狀態的裝置清單][img-update-2]
![工作清單顯示 hello 韌體更新清單完成][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="50ec7-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="50ec7-220">在實際執行環境中，您可以排程工作 toorun 指定的維護期間。</span><span class="sxs-lookup"><span data-stu-id="50ec7-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="50ec7-221">案例檢閱</span><span class="sxs-lookup"><span data-stu-id="50ec7-221">Scenario review</span></span>

<span data-ttu-id="50ec7-222">在此案例中，您可以識別潛在問題某些遠端裝置上 hello 儀表板和篩選器使用 hello 警示歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="50ec7-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="50ec7-223">您接著使用的 hello 篩選器和作業 tooremotely 設定 hello 裝置 tooprovide 詳細的資訊 toohelp 診斷 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="50ec7-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="50ec7-224">最後，您可以在 hello 受影響裝置上使用篩選器和作業 tooschedule 維護。</span><span class="sxs-lookup"><span data-stu-id="50ec7-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="50ec7-225">如果您傳回 toohello 儀表板，您可以檢查，不再有任何來自您方案中的裝置的警示。</span><span class="sxs-lookup"><span data-stu-id="50ec7-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="50ec7-226">您可以使用篩選 hello 韌體的 tooverify 最新的方案中的所有 hello 裝置，且沒有其他的狀況不良的裝置：</span><span class="sxs-lookup"><span data-stu-id="50ec7-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![篩選會顯示所有裝置具有最新版本的韌體][img-updated]

![篩選會顯示所有裝置狀況良好][img-healthy]

## <a name="other-features"></a><span data-ttu-id="50ec7-229">其他功能</span><span class="sxs-lookup"><span data-stu-id="50ec7-229">Other features</span></span>

<span data-ttu-id="50ec7-230">hello 下列章節說明一些其他功能的 hello 遠端監視預先設定的解決方案未描述 hello 前一個案例的一部分。</span><span class="sxs-lookup"><span data-stu-id="50ec7-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="50ec7-231">自訂資料行</span><span class="sxs-lookup"><span data-stu-id="50ec7-231">Customize columns</span></span>

<span data-ttu-id="50ec7-232">您可以自訂顯示 hello 裝置清單中選擇的 hello 資訊**資料行編輯器**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="50ec7-233">資料行顯示回報屬性和標籤值，您可以新增和移除這些資料行。</span><span class="sxs-lookup"><span data-stu-id="50ec7-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="50ec7-234">您也可以重新排列及重新命名資料行︰</span><span class="sxs-lookup"><span data-stu-id="50ec7-234">You can also reorder and rename columns:</span></span>

   ![資料行編輯器 ionic hello 裝置清單][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="50ec7-236">自訂 hello 裝置圖示</span><span class="sxs-lookup"><span data-stu-id="50ec7-236">Customize hello device icon</span></span>

<span data-ttu-id="50ec7-237">您可以自訂顯示 hello hello 裝置清單中的 hello 裝置圖示**裝置詳細資料** 面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="50ec7-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="50ec7-238">選擇 hello 鉛筆圖示 tooopen hello**編輯映像**面板裝置：</span><span class="sxs-lookup"><span data-stu-id="50ec7-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![開啟裝置影像編輯器][img-startimageedit]

1. <span data-ttu-id="50ec7-240">上傳新的映像，或使用其中一種 hello 現有的映像，然後選擇**儲存**:</span><span class="sxs-lookup"><span data-stu-id="50ec7-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![編輯裝置影像編輯器][img-imageedit]

1. <span data-ttu-id="50ec7-242">hello 影像選取現在會顯示 hello**圖示**hello 裝置的資料行。</span><span class="sxs-lookup"><span data-stu-id="50ec7-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="50ec7-243">hello 映像會儲存在 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="50ec7-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="50ec7-244">在 hello 裝置兩個標記包含連結 toohello 映像 blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="50ec7-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="50ec7-245">新增裝置</span><span class="sxs-lookup"><span data-stu-id="50ec7-245">Add a device</span></span>

<span data-ttu-id="50ec7-246">當您部署預先設定的 hello 方案時，您會自動佈建 25 個您可以在 hello 裝置清單中看到的範例裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="50ec7-247">這些裝置是在 Azure WebJob 中執行的 *模擬裝置* 。</span><span class="sxs-lookup"><span data-stu-id="50ec7-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="50ec7-248">模擬的裝置輕易地為您 tooexperiment 未 hello 需要 toodeploy 真正的實體裝置 hello 預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="50ec7-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="50ec7-249">如果您想 tooconnect 實際裝置 toohello 方案，請參閱 hello[連接您的裝置 toohello 遠端監視預先設定的解決方案][ lnk-connect-rm]教學課程。</span><span class="sxs-lookup"><span data-stu-id="50ec7-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="50ec7-250">hello 下列步驟說明如何 tooadd 模擬的裝置 toohello 方案：</span><span class="sxs-lookup"><span data-stu-id="50ec7-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="50ec7-251">瀏覽後 toohello 裝置清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="50ec7-252">tooadd 是裝置，請選擇**+ 新增裝置**hello 左下角中。</span><span class="sxs-lookup"><span data-stu-id="50ec7-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![新增裝置 toohello 預先設定的解決方案][img-adddevice]

1. <span data-ttu-id="50ec7-254">選擇**加入新**上 hello**模擬裝置**磚。</span><span class="sxs-lookup"><span data-stu-id="50ec7-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![在儀表板中設定新的裝置詳細資料][img-addnew]

   <span data-ttu-id="50ec7-256">在加法 toocreating 新模擬的裝置，您也可以將實體裝置如果您選擇 toocreate**自訂裝置**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="50ec7-257">toolearn 進一步了解連接的實體裝置 toohello 解決方案，請參閱[連接您的裝置 toohello IoT 套件遠端監視預先設定的解決方案][lnk-connect-rm]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="50ec7-258">選取 [自行定義裝置識別碼]，然後輸入唯一的裝置識別碼名稱，例如 **mydevice_01**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="50ec7-259">選擇 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="50ec7-259">Choose **Create**.</span></span>

   ![儲存新的裝置][img-definedevice]

1. <span data-ttu-id="50ec7-261">在步驟 3 的**新增模擬的裝置**，選擇**完成**tooreturn toohello 裝置清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="50ec7-262">您可以檢視您的裝置**執行**hello 裝置清單中。</span><span class="sxs-lookup"><span data-stu-id="50ec7-262">You can view your device **Running** in hello device list.</span></span>

    ![檢視裝置清單中的新裝置][img-runningnew]

1. <span data-ttu-id="50ec7-264">您也可以檢視 hello 模擬從新裝置 hello 儀表板上的遙測：</span><span class="sxs-lookup"><span data-stu-id="50ec7-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![從新裝置檢視遙測][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="50ec7-266">停用並刪除裝置</span><span class="sxs-lookup"><span data-stu-id="50ec7-266">Disable and delete a device</span></span>

<span data-ttu-id="50ec7-267">您可以停用裝置，並且在已停用之後移除：</span><span class="sxs-lookup"><span data-stu-id="50ec7-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![停用並移除裝置][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="50ec7-269">新增規則</span><span class="sxs-lookup"><span data-stu-id="50ec7-269">Add a rule</span></span>

<span data-ttu-id="50ec7-270">沒有您剛才加入 hello 新裝置的規則。</span><span class="sxs-lookup"><span data-stu-id="50ec7-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="50ec7-271">在本節中，您可以將 hello 溫度回報 hello 新裝置超過 47 度時，會觸發警示的規則。</span><span class="sxs-lookup"><span data-stu-id="50ec7-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="50ec7-272">開始之前，請注意，hello hello 儀表板上新的裝置 hello 遙測記錄顯示 hello 裝置溫度絕不會超出 45 度。</span><span class="sxs-lookup"><span data-stu-id="50ec7-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="50ec7-273">瀏覽後 toohello 裝置清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="50ec7-274">tooadd 規則 hello 裝置，請選取您新的裝置中 hello**裝置清單**，然後選擇 **加入規則**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="50ec7-275">建立規則，其使用**溫度**hello 資料欄位，並使用為**AlarmTemp** hello 輸出 hello 溫度超出 47 度時：</span><span class="sxs-lookup"><span data-stu-id="50ec7-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![新增裝置規則][img-adddevicerule]

1. <span data-ttu-id="50ec7-277">您的變更，選擇 toosave**儲存和檢視規則**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="50ec7-278">選擇**命令**hello 新裝置 hello 裝置詳細資料窗格中。</span><span class="sxs-lookup"><span data-stu-id="50ec7-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![新增裝置規則][img-adddevicerule2]

1. <span data-ttu-id="50ec7-280">選取**ChangeSetPointTemp** hello 命令清單和組**SetPointTemp** too45。</span><span class="sxs-lookup"><span data-stu-id="50ec7-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="50ec7-281">然後選擇 [傳送命令]：</span><span class="sxs-lookup"><span data-stu-id="50ec7-281">Then choose **Send Command**:</span></span>

    ![新增裝置規則][img-adddevicerule3]

1. <span data-ttu-id="50ec7-283">瀏覽後 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="50ec7-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="50ec7-284">在一段時間之後, 您會看到新的項目在 hello**警示歷程記錄**窗格 hello 溫度回報您的新裝置時超過 hello 47 度臨界值：</span><span class="sxs-lookup"><span data-stu-id="50ec7-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![新增裝置規則][img-adddevicerule4]

1. <span data-ttu-id="50ec7-286">您可以檢閱和編輯您的所有規則上 hello**規則**hello 儀表板頁面：</span><span class="sxs-lookup"><span data-stu-id="50ec7-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![列出裝置規則][img-rules]

1. <span data-ttu-id="50ec7-288">您可以檢閱和編輯所有可以採取上 hello 回應 tooa 規則中的 hello 動作**動作**hello 儀表板頁面：</span><span class="sxs-lookup"><span data-stu-id="50ec7-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![列出裝置動作][img-actions]

> [!NOTE]
> <span data-ttu-id="50ec7-290">它是可能 toodefine 動作可以傳送電子郵件訊息，或在回應 tooa SMS 規則，或與某個特定業務系統進行整合[邏輯應用程式][lnk-logic-apps]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="50ec7-291">如需詳細資訊，請參閱 hello[連接邏輯應用程式的 Azure IoT 套件遠端監視的 tooyour 預先設定的解決方案][lnk-logicapptutorial]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="50ec7-292">管理篩選</span><span class="sxs-lookup"><span data-stu-id="50ec7-292">Manage filters</span></span>

<span data-ttu-id="50ec7-293">在 hello 裝置清單中，您可以建立、 儲存及重新載入篩選器 toodisplay 自訂的裝置連線的 tooyour 中樞清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="50ec7-294">toocreate 篩選：</span><span class="sxs-lookup"><span data-stu-id="50ec7-294">toocreate a filter:</span></span>

1. <span data-ttu-id="50ec7-295">選擇的裝置 hello 清單上方的 hello 編輯篩選器圖示：</span><span class="sxs-lookup"><span data-stu-id="50ec7-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Hello 開啟篩選編輯器][img-editfiltericon]

1. <span data-ttu-id="50ec7-297">在 hello**篩選編輯器**，新增 hello 欄位、 運算子和值 toofilter hello 裝置清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="50ec7-298">您可以加入多個子句 toorefine 篩選器。</span><span class="sxs-lookup"><span data-stu-id="50ec7-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="50ec7-299">選擇**篩選**tooapply hello 篩選：</span><span class="sxs-lookup"><span data-stu-id="50ec7-299">Choose **Filter** tooapply hello filter:</span></span>

    ![建立篩選][img-filtereditor]

1. <span data-ttu-id="50ec7-301">此範例中，依製造商和型號的篩選 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="50ec7-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![篩選的清單][img-filterelist]

1. <span data-ttu-id="50ec7-303">toosave 您的篩選器，以自訂的名稱，選擇 hello**存**圖示：</span><span class="sxs-lookup"><span data-stu-id="50ec7-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![新增篩選][img-savefilter]

1. <span data-ttu-id="50ec7-305">tooreapply 您先前儲存的篩選器選擇 hello**開啟已儲存的篩選器**圖示：</span><span class="sxs-lookup"><span data-stu-id="50ec7-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![開啟篩選][img-openfilter]

<span data-ttu-id="50ec7-307">您可以根據裝置識別碼、裝置狀態、所需屬性、回報屬性和標籤，以建立篩選。</span><span class="sxs-lookup"><span data-stu-id="50ec7-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="50ec7-308">您可以新增您自己的自訂標籤 tooa 裝置在 hello**標記**hello 區段**裝置詳細資料**面板，或在多個裝置上執行作業 tooupdate 標記。</span><span class="sxs-lookup"><span data-stu-id="50ec7-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="50ec7-309">在 hello**篩選編輯器**，您可以使用 hello**進階檢視**tooedit hello 查詢文字直接。</span><span class="sxs-lookup"><span data-stu-id="50ec7-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="50ec7-310">命令</span><span class="sxs-lookup"><span data-stu-id="50ec7-310">Commands</span></span>

<span data-ttu-id="50ec7-311">從 hello**裝置詳細資料**面板中，您可以傳送命令 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="50ec7-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="50ec7-312">在裝置第一次啟動時，它會傳送 hello 的相關資訊的命令支援 toohello 方案。</span><span class="sxs-lookup"><span data-stu-id="50ec7-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="50ec7-313">如需命令和方法的 hello 差異的討論，請參閱[Azure IoT 中樞雲端到裝置選項][lnk-c2d-guidance]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="50ec7-314">選擇**命令**在 hello**裝置詳細資料**hello 選裝置的面板：</span><span class="sxs-lookup"><span data-stu-id="50ec7-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![儀表板中的裝置命令][img-devicecommands]

1. <span data-ttu-id="50ec7-316">選取**PingDevice**從 hello 命令清單。</span><span class="sxs-lookup"><span data-stu-id="50ec7-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="50ec7-317">選擇 [傳送命令]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="50ec7-318">您可以看到 hello hello 命令歷程記錄中的 hello 命令狀態。</span><span class="sxs-lookup"><span data-stu-id="50ec7-318">You can see hello status of hello command in hello command history.</span></span>

   ![儀表板中的命令狀態][img-pingcommand]

<span data-ttu-id="50ec7-320">hello 方案追蹤每個命令時會傳送 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="50ec7-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="50ec7-321">一開始是 hello 結果**暫止**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="50ec7-322">Hello 結果時 hello 裝置回報它已執行 hello 命令，設定得**成功**。</span><span class="sxs-lookup"><span data-stu-id="50ec7-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="50ec7-323">Hello 幕後</span><span class="sxs-lookup"><span data-stu-id="50ec7-323">Behind hello scenes</span></span>

<span data-ttu-id="50ec7-324">當您部署預先設定的解決方案時，hello 部署程序會在 hello 您選取的 Azure 訂用帳戶中建立多個資源。</span><span class="sxs-lookup"><span data-stu-id="50ec7-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="50ec7-325">您可以檢視這些資源中 hello Azure[入口網站][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="50ec7-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="50ec7-326">hello 部署程序會建立**資源群組**根據您選擇您預先設定的解決方案 hello 名稱的名稱：</span><span class="sxs-lookup"><span data-stu-id="50ec7-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Hello Azure 入口網站中預先設定的解決方案][img-portal]

<span data-ttu-id="50ec7-328">您可以檢視每個資源的 hello 設定 hello 資源群組中的 hello 清單中選取。</span><span class="sxs-lookup"><span data-stu-id="50ec7-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="50ec7-329">您也可以檢視預先設定的 hello 方案 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="50ec7-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="50ec7-330">遠端監視預先設定的方案原始碼 hello 處於 hello [azure iot-遠端-監視][ lnk-rmgithub] GitHub 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="50ec7-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="50ec7-331">hello **DeviceAdministration**資料夾包含 hello 原始程式碼 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="50ec7-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="50ec7-332">hello**模擬器**資料夾包含 hello 模擬的裝置 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="50ec7-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="50ec7-333">hello **EventProcessor**資料夾包含 hello 後端程序處理 hello 傳入遙測 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="50ec7-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="50ec7-334">完成之後，您可以從您的 Azure 訂閱 hello 上刪除 hello 預先設定的解決方案[azureiotsuite.com] [ lnk-azureiotsuite]站台。</span><span class="sxs-lookup"><span data-stu-id="50ec7-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="50ec7-335">此站台可讓您 tooeasily 刪除所有 hello 當您建立預先設定的 hello 方案已佈建的資源。</span><span class="sxs-lookup"><span data-stu-id="50ec7-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="50ec7-336">刪除所有項目 tooensure 相關 toohello 預先設定的解決方案，刪除上 hello [azureiotsuite.com] [ lnk-azureiotsuite]站台，並不會刪除 hello hello 入口網站中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="50ec7-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50ec7-337">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50ec7-337">Next Steps</span></span>

<span data-ttu-id="50ec7-338">既然您已部署預先設定的有效的解決方案，您可以繼續閱讀下列文章 hello 入門 IoT 套件：</span><span class="sxs-lookup"><span data-stu-id="50ec7-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="50ec7-339">[遠端監視預先設定解決方案逐步解說][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="50ec7-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="50ec7-340">[連接您的裝置 toohello 遠端監視預先設定的解決方案][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="50ec7-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="50ec7-341">[Hello azureiotsuite.com 網站的權限][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="50ec7-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md