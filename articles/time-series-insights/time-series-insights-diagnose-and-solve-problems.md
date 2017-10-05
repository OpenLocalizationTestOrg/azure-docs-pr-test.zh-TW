---
title: "診斷並解決問題 | Microsoft Docs"
description: "本教學課程說明如何在 Time Series Insights 環境中診斷並解決問題"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 4b8d5fdab1744b2db658917f91d6dac05db30d2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a><span data-ttu-id="1cc87-103">在 Time Series Insights 環境中診斷與解決問題</span><span class="sxs-lookup"><span data-stu-id="1cc87-103">Diagnose and solve problems in your Time Series Insights environment</span></span>

## <a name="i-dont-see-my-data"></a><span data-ttu-id="1cc87-104">我看不見我的資料</span><span class="sxs-lookup"><span data-stu-id="1cc87-104">I don't see my data</span></span>
<span data-ttu-id="1cc87-105">以下是您無法在 [Azure Time Series Insights 入口網站](https://insights.timeseries.azure.com)環境中看到資料的可能原因。</span><span class="sxs-lookup"><span data-stu-id="1cc87-105">Here are some reasons why you might not see your data in your environment in the [Azure Time Series Insights portal](https://insights.timeseries.azure.com).</span></span>

### <a name="your-event-source-doesnt-have-data-in-json-format"></a><span data-ttu-id="1cc87-106">您事件來源的資料不是 JSON 格式</span><span class="sxs-lookup"><span data-stu-id="1cc87-106">Your event source doesn't have data in JSON format</span></span>
<span data-ttu-id="1cc87-107">Azure Time Series Insights 現在只支援 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="1cc87-107">Azure Time Series Insights supports only JSON data today.</span></span> <span data-ttu-id="1cc87-108">如需 JSON 範例，請參閱[支援的 JSON 樣貌](time-series-insights-send-events.md#supported-json-shapes)。</span><span class="sxs-lookup"><span data-stu-id="1cc87-108">For JSON samples, see [Supported JSON shapes](time-series-insights-send-events.md#supported-json-shapes).</span></span>

### <a name="when-you-registered-your-event-source-you-didnt-provide-the-key-that-has-the-required-permission"></a><span data-ttu-id="1cc87-109">當您註冊事件來源時，您未提供具有必要權限的索引鍵</span><span class="sxs-lookup"><span data-stu-id="1cc87-109">When you registered your event source, you didn't provide the key that has the required permission</span></span>
* <span data-ttu-id="1cc87-110">針對 IoT 中樞，您必須提供具有「服務連接」權限的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1cc87-110">For an IoT hub, you need to provide the key that has **service connect** permission.</span></span>

   ![IoT 中樞服務連線權限](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   <span data-ttu-id="1cc87-112">如上圖所示，iothubowner 與 service 原則都會運作，因為兩者皆有「服務連接」權限。</span><span class="sxs-lookup"><span data-stu-id="1cc87-112">As shown in the preceding image, either of the policies **iothubowner** and **service** would work, because both have **service connect** permission.</span></span>
* <span data-ttu-id="1cc87-113">針對事件中樞，您必須提供具有「接聽」權限的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1cc87-113">For an event hub, you need to provide the key that has **Listen** permission.</span></span>

   ![事件中樞接聽權限](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   <span data-ttu-id="1cc87-115">如上圖所示，read 與 manage 原則皆可運作，因為兩者皆有「接聽」權限。</span><span class="sxs-lookup"><span data-stu-id="1cc87-115">As shown in the preceding image, either of the policies **read** and **manage** would work, because both have **Listen** permission.</span></span>

### <a name="the-provided-consumer-group-is-not-exclusive-to-time-series-insights"></a><span data-ttu-id="1cc87-116">所提供的取用者群組不是 Time Series Insights 專用</span><span class="sxs-lookup"><span data-stu-id="1cc87-116">The provided consumer group is not exclusive to Time Series Insights</span></span>
<span data-ttu-id="1cc87-117">對於 IoT 中樞或事件中樞，在註冊期間，我們會要求您指定應用於讀取資料的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="1cc87-117">For an IoT hub or an event hub, during registration we require you to specify the consumer group that should be used for reading your data.</span></span> <span data-ttu-id="1cc87-118">不可共用此取用者群組。</span><span class="sxs-lookup"><span data-stu-id="1cc87-118">This consumer group must not be shared.</span></span> <span data-ttu-id="1cc87-119">如果共用，基礎事件中樞會自動且隨機地與其中一個讀取器中斷連線。</span><span class="sxs-lookup"><span data-stu-id="1cc87-119">If it's shared, the underlying event hub automatically disconnects one of the readers randomly.</span></span>

## <a name="i-see-my-data-but-theres-a-lag"></a><span data-ttu-id="1cc87-120">我可以看到我的資料，但有延遲情形</span><span class="sxs-lookup"><span data-stu-id="1cc87-120">I see my data, but there's a lag</span></span>
<span data-ttu-id="1cc87-121">以下是您在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)環境中看到部分資料的原因。</span><span class="sxs-lookup"><span data-stu-id="1cc87-121">Here are reasons why you might see partial data in your environment in the [Time Series Insights portal](https://insights.timeseries.azure.com).</span></span>

### <a name="your-environment-is-getting-throttled"></a><span data-ttu-id="1cc87-122">您的環境正在進行節流</span><span class="sxs-lookup"><span data-stu-id="1cc87-122">Your environment is getting throttled</span></span>
<span data-ttu-id="1cc87-123">節流限制會根據環境 SKU 類型和容量來強制執行。</span><span class="sxs-lookup"><span data-stu-id="1cc87-123">The throttling limit is enforced based on the environment's SKU type and capacity.</span></span> <span data-ttu-id="1cc87-124">環境中所有的事件來源皆共用此容量。</span><span class="sxs-lookup"><span data-stu-id="1cc87-124">All event sources in the environment share this capacity.</span></span> <span data-ttu-id="1cc87-125">如果IoT 中樞或事件中樞的事件來源正在推送超過強制限制的資料，您會看到節流和延遲情形。</span><span class="sxs-lookup"><span data-stu-id="1cc87-125">If the event source for your IoT hub or event hub is pushing data beyond the enforced limits, you see throttling and a lag.</span></span>

<span data-ttu-id="1cc87-126">下圖顯示有 SKU 的 S1 且容量為 3 的 Time Series Insights 環境。</span><span class="sxs-lookup"><span data-stu-id="1cc87-126">The following diagram shows a Time Series Insights environment that has a SKU of S1 and a capacity of 3.</span></span> <span data-ttu-id="1cc87-127">該環境可以每日輸入 3 百萬個事件。</span><span class="sxs-lookup"><span data-stu-id="1cc87-127">It can ingress 3 million events per day.</span></span>

![環境 SKU 目前容量](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

<span data-ttu-id="1cc87-129">假設此環境正以下圖所示的輸入速率從事件中樞輸入訊息：</span><span class="sxs-lookup"><span data-stu-id="1cc87-129">Assume that this environment is ingesting messages from an event hub with the ingress rate shown in the following diagram:</span></span>

![事件中樞的範例輸入率](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

<span data-ttu-id="1cc87-131">如圖所示，每日輸入速率為 ~67,000 則訊息。</span><span class="sxs-lookup"><span data-stu-id="1cc87-131">As shown in the diagram, the daily ingress rate is ~67,000 messages.</span></span> <span data-ttu-id="1cc87-132">此速率可轉譯為大約每分鐘 46 則訊息。</span><span class="sxs-lookup"><span data-stu-id="1cc87-132">This rate translates roughly to 46 messages every minute.</span></span> <span data-ttu-id="1cc87-133">如果每個事件中樞訊息被壓平合併為單一 Time Series Insights 事件，則此環境看不見節流。</span><span class="sxs-lookup"><span data-stu-id="1cc87-133">If each event hub message is flattened to a single Time Series Insights event, this environment sees no throttling.</span></span> <span data-ttu-id="1cc87-134">如果每個事件中樞訊息被壓平合併為 100 個 Time Series Insights 事件，則每分鐘應內嵌 4,600 個事件。</span><span class="sxs-lookup"><span data-stu-id="1cc87-134">If each event hub message is flattened to 100 Time Series Insights events, then 4,600 events should be ingested every minute.</span></span> <span data-ttu-id="1cc87-135">容量為 3 的 S1 SKU 環境每分鐘只能輸入 2,100 個事件 (每天 1 百萬個事件 = 每 3 單位每分鐘 700 個事件 = 每分鐘 2,100 個事件)。</span><span class="sxs-lookup"><span data-stu-id="1cc87-135">An S1 SKU environment that has a capacity of 3 can ingress only 2,100 events every minute (1 million events per day = 700 events per minute at 3 units = 2,100 events per minute).</span></span> <span data-ttu-id="1cc87-136">因此您會看見延遲情形是因為節流。</span><span class="sxs-lookup"><span data-stu-id="1cc87-136">Therefore you see a lag due to throttling.</span></span> 

<span data-ttu-id="1cc87-137">若要概略了解壓平合併邏輯的運作方式，請參閱[支援的 JSON 樣貌](time-series-insights-send-events.md#supported-json-shapes)。</span><span class="sxs-lookup"><span data-stu-id="1cc87-137">For a high-level understanding of how flattening logic works, see [Supported JSON shapes](time-series-insights-send-events.md#supported-json-shapes).</span></span>

#### <a name="recommended-steps"></a><span data-ttu-id="1cc87-138">建議的步驟</span><span class="sxs-lookup"><span data-stu-id="1cc87-138">Recommended steps</span></span>
<span data-ttu-id="1cc87-139">若要修正延遲情形，請增加您環境的 SKU 容量。</span><span class="sxs-lookup"><span data-stu-id="1cc87-139">To fix the lag, increase the SKU capacity of your environment.</span></span> <span data-ttu-id="1cc87-140">如需詳細資訊，請參閱[如何調整您的 Time Series Insights 環境規模](time-series-insights-how-to-scale-your-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="1cc87-140">For more information, see [How to scale your Time Series Insights environment](time-series-insights-how-to-scale-your-environment.md).</span></span>

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a><span data-ttu-id="1cc87-141">您正在推送歷程記錄資料並造成輸入緩慢</span><span class="sxs-lookup"><span data-stu-id="1cc87-141">You're pushing historical data and causing slow ingress</span></span>
<span data-ttu-id="1cc87-142">如果您正與現有事件來源連線，則您的 IoT 中樞或事件中樞裡可能已有資料。</span><span class="sxs-lookup"><span data-stu-id="1cc87-142">If you are connecting an existing event source, it's likely that your IoT hub or event hub already has data in it.</span></span> <span data-ttu-id="1cc87-143">因此環境會從事件來源訊息保留期間開始時開始提取資料。</span><span class="sxs-lookup"><span data-stu-id="1cc87-143">So the environment starts pulling data from the beginning of the event source's message retention period.</span></span> 

<span data-ttu-id="1cc87-144">此行為是預設行為且無法覆寫。</span><span class="sxs-lookup"><span data-stu-id="1cc87-144">This behavior is the default behavior and cannot be overridden.</span></span> <span data-ttu-id="1cc87-145">您可以進行節流，並且可能需要一段時間才能趕上正在輸入的歷程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="1cc87-145">You can engage throttling, and it may take a while to catch up on ingesting historical data.</span></span>

#### <a name="recommended-steps"></a><span data-ttu-id="1cc87-146">建議的步驟</span><span class="sxs-lookup"><span data-stu-id="1cc87-146">Recommended steps</span></span>
<span data-ttu-id="1cc87-147">若要修正延遲，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1cc87-147">To fix the lag, take the following steps:</span></span>
1. <span data-ttu-id="1cc87-148">將 SKU 容量增加到最大允許值 (在此案例中是 10)。</span><span class="sxs-lookup"><span data-stu-id="1cc87-148">Increase the SKU capacity to the maximum allowed value (10 in this case).</span></span> <span data-ttu-id="1cc87-149">增加容量後，輸入程序會開始加快速度來趕上。</span><span class="sxs-lookup"><span data-stu-id="1cc87-149">After the capacity is increased, the ingress process starts catching up much faster.</span></span> <span data-ttu-id="1cc87-150">您可以從 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)的可用性圖表中看到我們趕上的速度有多快。</span><span class="sxs-lookup"><span data-stu-id="1cc87-150">You can visualize how quickly you're catching up through the availability chart in the [Time Series Insights portal](https://insights.timeseries.azure.com).</span></span> <span data-ttu-id="1cc87-151">增加容量需支付費用。</span><span class="sxs-lookup"><span data-stu-id="1cc87-151">You are charged for the increased capacity.</span></span>
2. <span data-ttu-id="1cc87-152">趕上延遲時間後，即可將 SKU 容量降回到正常的輸入速率。</span><span class="sxs-lookup"><span data-stu-id="1cc87-152">After the lag is caught up, decrease the SKU capacity back to your normal ingress rate.</span></span>

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a><span data-ttu-id="1cc87-153">我的事件來源的時間戳記屬性名稱設定沒有作用</span><span class="sxs-lookup"><span data-stu-id="1cc87-153">My event source's *timestamp property name* setting doesn't work</span></span>
<span data-ttu-id="1cc87-154">請確定名稱和值符合下列規則︰</span><span class="sxs-lookup"><span data-stu-id="1cc87-154">Ensure that the name and value conform to the following rules:</span></span>
* <span data-ttu-id="1cc87-155">時間戳記屬性名稱有_區分大小寫_。</span><span class="sxs-lookup"><span data-stu-id="1cc87-155">The timestamp property name is _case-sensitive_.</span></span>
* <span data-ttu-id="1cc87-156">來自事件來源的時間戳記屬性值 (JSON 字串) 格式應是「yyyy-MM-ddTHH:mm:ss.FFFFFFFK」。</span><span class="sxs-lookup"><span data-stu-id="1cc87-156">The timestamp property value that's coming from your event source, as a JSON string, should have the format _yyyy-MM-ddTHH:mm:ss.FFFFFFFK_.</span></span> <span data-ttu-id="1cc87-157">字串的範例如 “2008-04-12T12:53Z”。</span><span class="sxs-lookup"><span data-stu-id="1cc87-157">An example of such a string is “2008-04-12T12:53Z”.</span></span>
