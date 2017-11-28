---
title: "aaaDiagnose 並解決問題 |Microsoft 文件"
description: "本教學課程涵蓋如何 toodiagnose 並解決問題，在時間序列 Insights 環境"
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
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a><span data-ttu-id="419a1-103">在 Time Series Insights 環境中診斷與解決問題</span><span class="sxs-lookup"><span data-stu-id="419a1-103">Diagnose and solve problems in your Time Series Insights environment</span></span>

## <a name="i-dont-see-my-data"></a><span data-ttu-id="419a1-104">我看不見我的資料</span><span class="sxs-lookup"><span data-stu-id="419a1-104">I don't see my data</span></span>
<span data-ttu-id="419a1-105">以下是一些原因為什麼您可能不會看到您的資料在您的環境中 hello [Azure 時間數列 Insights 入口網站](https://insights.timeseries.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="419a1-105">Here are some reasons why you might not see your data in your environment in hello [Azure Time Series Insights portal](https://insights.timeseries.azure.com).</span></span>

### <a name="your-event-source-doesnt-have-data-in-json-format"></a><span data-ttu-id="419a1-106">您事件來源的資料不是 JSON 格式</span><span class="sxs-lookup"><span data-stu-id="419a1-106">Your event source doesn't have data in JSON format</span></span>
<span data-ttu-id="419a1-107">Azure Time Series Insights 現在只支援 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="419a1-107">Azure Time Series Insights supports only JSON data today.</span></span> <span data-ttu-id="419a1-108">如需 JSON 範例，請參閱[支援的 JSON 樣貌](time-series-insights-send-events.md#supported-json-shapes)。</span><span class="sxs-lookup"><span data-stu-id="419a1-108">For JSON samples, see [Supported JSON shapes](time-series-insights-send-events.md#supported-json-shapes).</span></span>

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a><span data-ttu-id="419a1-109">當您註冊事件來源時，您未提供具有 hello 所需的權限的 hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="419a1-109">When you registered your event source, you didn't provide hello key that has hello required permission</span></span>
* <span data-ttu-id="419a1-110">IoT 中樞，您需要具有 tooprovide hello 金鑰**服務連線**權限。</span><span class="sxs-lookup"><span data-stu-id="419a1-110">For an IoT hub, you need tooprovide hello key that has **service connect** permission.</span></span>

   ![IoT 中樞服務連線權限](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   <span data-ttu-id="419a1-112">示 hello 前面映像，其中一個 hello 原則**iothubowner**和**服務**運作，因為兩者都有**服務連線**權限。</span><span class="sxs-lookup"><span data-stu-id="419a1-112">As shown in hello preceding image, either of hello policies **iothubowner** and **service** would work, because both have **service connect** permission.</span></span>
* <span data-ttu-id="419a1-113">事件中心，您需要具有 tooprovide hello 金鑰**接聽**權限。</span><span class="sxs-lookup"><span data-stu-id="419a1-113">For an event hub, you need tooprovide hello key that has **Listen** permission.</span></span>

   ![事件中樞接聽權限](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   <span data-ttu-id="419a1-115">示 hello 前面映像，其中一個 hello 原則**讀取**和**管理**運作，因為兩者都有**接聽**權限。</span><span class="sxs-lookup"><span data-stu-id="419a1-115">As shown in hello preceding image, either of hello policies **read** and **manage** would work, because both have **Listen** permission.</span></span>

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a><span data-ttu-id="419a1-116">hello 提供取用者群組不是獨占 tooTime 數列 Insights</span><span class="sxs-lookup"><span data-stu-id="419a1-116">hello provided consumer group is not exclusive tooTime Series Insights</span></span>
<span data-ttu-id="419a1-117">IoT 中樞或事件中心，請在註冊期間我們需要您應該用來讀取資料的 toospecify hello 取用者群組。</span><span class="sxs-lookup"><span data-stu-id="419a1-117">For an IoT hub or an event hub, during registration we require you toospecify hello consumer group that should be used for reading your data.</span></span> <span data-ttu-id="419a1-118">不可共用此取用者群組。</span><span class="sxs-lookup"><span data-stu-id="419a1-118">This consumer group must not be shared.</span></span> <span data-ttu-id="419a1-119">如果它共用，基礎事件中心 hello 自動中斷連線 hello 讀取器的其中一個隨機。</span><span class="sxs-lookup"><span data-stu-id="419a1-119">If it's shared, hello underlying event hub automatically disconnects one of hello readers randomly.</span></span>

## <a name="i-see-my-data-but-theres-a-lag"></a><span data-ttu-id="419a1-120">我可以看到我的資料，但有延遲情形</span><span class="sxs-lookup"><span data-stu-id="419a1-120">I see my data, but there's a lag</span></span>
<span data-ttu-id="419a1-121">以下是為什麼您可能會看到您的環境中 hello 的部分資料的原因[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="419a1-121">Here are reasons why you might see partial data in your environment in hello [Time Series Insights portal](https://insights.timeseries.azure.com).</span></span>

### <a name="your-environment-is-getting-throttled"></a><span data-ttu-id="419a1-122">您的環境正在進行節流</span><span class="sxs-lookup"><span data-stu-id="419a1-122">Your environment is getting throttled</span></span>
<span data-ttu-id="419a1-123">會強制執行節流限制的 hello，根據 hello 環境 SKU 類型和容量。</span><span class="sxs-lookup"><span data-stu-id="419a1-123">hello throttling limit is enforced based on hello environment's SKU type and capacity.</span></span> <span data-ttu-id="419a1-124">Hello 環境中的所有事件來源會都共用此容量。</span><span class="sxs-lookup"><span data-stu-id="419a1-124">All event sources in hello environment share this capacity.</span></span> <span data-ttu-id="419a1-125">如果 hello IoT 中心] 或 [事件中樞的事件來源是 hello 強制執行限制之外的資料，您會看到節流和延遲。</span><span class="sxs-lookup"><span data-stu-id="419a1-125">If hello event source for your IoT hub or event hub is pushing data beyond hello enforced limits, you see throttling and a lag.</span></span>

<span data-ttu-id="419a1-126">hello 下列圖表顯示的時間序列 Insights 環境具有 SKU S1 和 3 的容量。</span><span class="sxs-lookup"><span data-stu-id="419a1-126">hello following diagram shows a Time Series Insights environment that has a SKU of S1 and a capacity of 3.</span></span> <span data-ttu-id="419a1-127">該環境可以每日輸入 3 百萬個事件。</span><span class="sxs-lookup"><span data-stu-id="419a1-127">It can ingress 3 million events per day.</span></span>

![環境 SKU 目前容量](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

<span data-ttu-id="419a1-129">假設此環境擷取自事件中心的訊息，以 hello 輸入速率 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="419a1-129">Assume that this environment is ingesting messages from an event hub with hello ingress rate shown in hello following diagram:</span></span>

![事件中樞的範例輸入率](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

<span data-ttu-id="419a1-131">Hello 圖表所示，每日輸入速率 hello 是 ~ 67,000 訊息。</span><span class="sxs-lookup"><span data-stu-id="419a1-131">As shown in hello diagram, hello daily ingress rate is ~67,000 messages.</span></span> <span data-ttu-id="419a1-132">此比率將轉譯大致 too46 訊息每隔一分鐘。</span><span class="sxs-lookup"><span data-stu-id="419a1-132">This rate translates roughly too46 messages every minute.</span></span> <span data-ttu-id="419a1-133">如果每個事件中樞的訊息是扁平化的 tooa 單一時間序列 Insights 事件，會看到此環境沒有節流。</span><span class="sxs-lookup"><span data-stu-id="419a1-133">If each event hub message is flattened tooa single Time Series Insights event, this environment sees no throttling.</span></span> <span data-ttu-id="419a1-134">如果每個事件中樞的訊息是扁平化的 too100 時間數列 Insights 事件，然後 4,600 事件應該被 ingested 每隔一分鐘。</span><span class="sxs-lookup"><span data-stu-id="419a1-134">If each event hub message is flattened too100 Time Series Insights events, then 4,600 events should be ingested every minute.</span></span> <span data-ttu-id="419a1-135">容量為 3 的 S1 SKU 環境每分鐘只能輸入 2,100 個事件 (每天 1 百萬個事件 = 每 3 單位每分鐘 700 個事件 = 每分鐘 2,100 個事件)。</span><span class="sxs-lookup"><span data-stu-id="419a1-135">An S1 SKU environment that has a capacity of 3 can ingress only 2,100 events every minute (1 million events per day = 700 events per minute at 3 units = 2,100 events per minute).</span></span> <span data-ttu-id="419a1-136">因此，您看到延隔時間到期 toothrottling。</span><span class="sxs-lookup"><span data-stu-id="419a1-136">Therefore you see a lag due toothrottling.</span></span> 

<span data-ttu-id="419a1-137">若要概略了解壓平合併邏輯的運作方式，請參閱[支援的 JSON 樣貌](time-series-insights-send-events.md#supported-json-shapes)。</span><span class="sxs-lookup"><span data-stu-id="419a1-137">For a high-level understanding of how flattening logic works, see [Supported JSON shapes](time-series-insights-send-events.md#supported-json-shapes).</span></span>

#### <a name="recommended-steps"></a><span data-ttu-id="419a1-138">建議的步驟</span><span class="sxs-lookup"><span data-stu-id="419a1-138">Recommended steps</span></span>
<span data-ttu-id="419a1-139">toofix hello 延隔時間，增加 hello 環境的 SKU 容量。</span><span class="sxs-lookup"><span data-stu-id="419a1-139">toofix hello lag, increase hello SKU capacity of your environment.</span></span> <span data-ttu-id="419a1-140">如需詳細資訊，請參閱[如何 tooscale 時間數列 Insights 環境](time-series-insights-how-to-scale-your-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="419a1-140">For more information, see [How tooscale your Time Series Insights environment](time-series-insights-how-to-scale-your-environment.md).</span></span>

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a><span data-ttu-id="419a1-141">您正在推送歷程記錄資料並造成輸入緩慢</span><span class="sxs-lookup"><span data-stu-id="419a1-141">You're pushing historical data and causing slow ingress</span></span>
<span data-ttu-id="419a1-142">如果您正與現有事件來源連線，則您的 IoT 中樞或事件中樞裡可能已有資料。</span><span class="sxs-lookup"><span data-stu-id="419a1-142">If you are connecting an existing event source, it's likely that your IoT hub or event hub already has data in it.</span></span> <span data-ttu-id="419a1-143">因此 hello 環境啟動 hello 事件來源的訊息保留期限的 hello 開頭從中提取資料。</span><span class="sxs-lookup"><span data-stu-id="419a1-143">So hello environment starts pulling data from hello beginning of hello event source's message retention period.</span></span> 

<span data-ttu-id="419a1-144">此行為是 hello 預設行為，而且不能覆寫。</span><span class="sxs-lookup"><span data-stu-id="419a1-144">This behavior is hello default behavior and cannot be overridden.</span></span> <span data-ttu-id="419a1-145">您可以進行節流，而且可能需要一段 toocatch 向上上擷取歷程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="419a1-145">You can engage throttling, and it may take a while toocatch up on ingesting historical data.</span></span>

#### <a name="recommended-steps"></a><span data-ttu-id="419a1-146">建議的步驟</span><span class="sxs-lookup"><span data-stu-id="419a1-146">Recommended steps</span></span>
<span data-ttu-id="419a1-147">toofix hello 延隔，採取下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="419a1-147">toofix hello lag, take hello following steps:</span></span>
1. <span data-ttu-id="419a1-148">增加 hello SKU 容量 toohello 最大允許值 (在本例中為 10)。</span><span class="sxs-lookup"><span data-stu-id="419a1-148">Increase hello SKU capacity toohello maximum allowed value (10 in this case).</span></span> <span data-ttu-id="419a1-149">Hello 容量會增加之後，hello 輸入開始程序趕上進度更快。</span><span class="sxs-lookup"><span data-stu-id="419a1-149">After hello capacity is increased, hello ingress process starts catching up much faster.</span></span> <span data-ttu-id="419a1-150">您可以視覺化速度您正在趕上透過 hello 可用性圖表中 hello[時間數列 Insights 入口網站](https://insights.timeseries.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="419a1-150">You can visualize how quickly you're catching up through hello availability chart in hello [Time Series Insights portal](https://insights.timeseries.azure.com).</span></span> <span data-ttu-id="419a1-151">您必須支付 hello 增加容量。</span><span class="sxs-lookup"><span data-stu-id="419a1-151">You are charged for hello increased capacity.</span></span>
2. <span data-ttu-id="419a1-152">Hello 延隔時間趕上之後，會降低 hello SKU 容量後 tooyour 一般輸入速率。</span><span class="sxs-lookup"><span data-stu-id="419a1-152">After hello lag is caught up, decrease hello SKU capacity back tooyour normal ingress rate.</span></span>

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a><span data-ttu-id="419a1-153">我的事件來源的時間戳記屬性名稱設定沒有作用</span><span class="sxs-lookup"><span data-stu-id="419a1-153">My event source's *timestamp property name* setting doesn't work</span></span>
<span data-ttu-id="419a1-154">請確定 hello 名稱和值符合 toohello 下列規則：</span><span class="sxs-lookup"><span data-stu-id="419a1-154">Ensure that hello name and value conform toohello following rules:</span></span>
* <span data-ttu-id="419a1-155">hello 時間戳記屬性名稱_區分大小寫_。</span><span class="sxs-lookup"><span data-stu-id="419a1-155">hello timestamp property name is _case-sensitive_.</span></span>
* <span data-ttu-id="419a1-156">hello 時間戳記屬性值，來自事件來源，為 JSON 字串時，應該具有 hello 格式_yyyy-MM-Yyyy-mm-ddthh。SS'.'FFFFFFFK_。</span><span class="sxs-lookup"><span data-stu-id="419a1-156">hello timestamp property value that's coming from your event source, as a JSON string, should have hello format _yyyy-MM-ddTHH:mm:ss.FFFFFFFK_.</span></span> <span data-ttu-id="419a1-157">字串的範例如 “2008-04-12T12:53Z”。</span><span class="sxs-lookup"><span data-stu-id="419a1-157">An example of such a string is “2008-04-12T12:53Z”.</span></span>
