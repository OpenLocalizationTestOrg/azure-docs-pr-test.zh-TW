---
title: "Azure 時間數列深入解析的 aaaOverview |Microsoft 文件"
description: "簡介 tooAzure 時間數列深入解析，新的服務的時間序列資料分析和 IoT 解決方案"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a><span data-ttu-id="d761e-103">什麼是 Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="d761e-103">What is Azure Time Series Insights</span></span>

<span data-ttu-id="d761e-104">Azure 的時間序列 Insights 是使用儲存體、 分析和視覺效果元件可讓您輕鬆 tooingest、 儲存、 瀏覽及同時分析數十億個事件對受管理的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d761e-104">Azure Time Series Insights is a managed cloud service with storage, analytics, and visualization components that make it easy tooingest, store, explore and analyze billions of events simultaneously.</span></span> <span data-ttu-id="d761e-105">Time Series Insights 可讓您以全域方式檢視資料，這可協助您探索隱藏的趨勢和異常狀況，並近乎即時地執行根本原因分析，進而快速驗證 IoT 解決方案並避免代價高昂的裝置停機。</span><span class="sxs-lookup"><span data-stu-id="d761e-105">Time Series Insights gives you a global view of your data, letting you quickly validate your IoT Solutions, and avoid costly device downtime, by helping you discover hidden trends and anomalies, and conduct root-cause analyses in near real-time.</span></span> <span data-ttu-id="d761e-106">時間序列 Insights 內嵌事件仲介 （例如 IoT 中樞或事件中心） 從時間序列資料、 索引 hello 資料和淘汰時可設定的保留原則為基礎的資料。</span><span class="sxs-lookup"><span data-stu-id="d761e-106">Time Series Insights ingests time-series data from event-brokers (e.g. IoT Hubs or Event Hubs), indexes hello data, and retires data based on a configurable retention policy.</span></span> <span data-ttu-id="d761e-107">使用者會使用透過直覺式的 UX 或 REST 查詢 Api 的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d761e-107">Users consume hello data either through an intuitive UX or REST Query APIs.</span></span>

![Time Series Insight 概觀](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a><span data-ttu-id="d761e-109">主要案例</span><span class="sxs-lookup"><span data-stu-id="d761e-109">Primary scenarios</span></span>

* <span data-ttu-id="d761e-110">在短短幾分鐘內監視和驗證 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="d761e-110">Monitor and validate IoT solutions in minutes.</span></span>
* <span data-ttu-id="d761e-111">大規模視覺化和分析 IoT 資料。</span><span class="sxs-lookup"><span data-stu-id="d761e-111">Visualize and analyze IoT data at scale.</span></span>
* <span data-ttu-id="d761e-112">加速進行根本原因分析和異常偵測。</span><span class="sxs-lookup"><span data-stu-id="d761e-112">Expedite root-cause analysis and anomaly detection.</span></span>
* <span data-ttu-id="d761e-113">建立含有多個裝置、工廠和資料的全域檢視。</span><span class="sxs-lookup"><span data-stu-id="d761e-113">Create a global view of multiple devices, plants, and data.</span></span>

## <a name="capabilities-and-benefits"></a><span data-ttu-id="d761e-114">功能和優點</span><span class="sxs-lookup"><span data-stu-id="d761e-114">Capabilities and benefits</span></span>

* <span data-ttu-id="d761e-115">**啟動的簡單 tooget**: Azure 時間數列 Insights 需要沒有足夠的事前資料準備工作，而且是非常快速地執行。</span><span class="sxs-lookup"><span data-stu-id="d761e-115">**Easy tooget started**: Azure Time Series Insights requires no up-front data preparation and is incredibly fast.</span></span> <span data-ttu-id="d761e-116">連接您的 Azure IoT 中樞或事件中心中的事件 toobillions 以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="d761e-116">Connect toobillions of events in your Azure IoT Hub or Event Hub in minutes.</span></span> <span data-ttu-id="d761e-117">一旦連接之後，以視覺化方式檢視和與感應器資料互動，以秒為單位 tooquickly 驗證您的 IoT 解決方案。</span><span class="sxs-lookup"><span data-stu-id="d761e-117">Once connected, visualize and interact with sensor data in seconds tooquickly validate your IoT solutions.</span></span> <span data-ttu-id="d761e-118">時間序列 Insights 是簡單 toouse;您可以互動與您的資料，而不需要撰寫一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="d761e-118">Time Series Insights is easy toouse; you can interact with your data without writing a single line of code.</span></span>  <span data-ttu-id="d761e-119">沒有任何新的語言 toolearn;時間序列 Insights 對於進階使用者，提供細微、 任意文字的查詢介面，並指向，然後按一下瀏覽所有。</span><span class="sxs-lookup"><span data-stu-id="d761e-119">There is no new language toolearn; Time Series Insights provides a granular, free-text query surface for advanced users, and point and click exploration for all.</span></span>

* <span data-ttu-id="d761e-120">**接近即時的深入資訊**： 時間序列 Insights 可以內嵌數百萬個每日的感應器事件以一分鐘的延遲，因此您可以快速反應 toochanges。</span><span class="sxs-lookup"><span data-stu-id="d761e-120">**Near Real-time insights**: Time Series Insights can ingest hundreds of millions of sensor events per day, with one minute latency, so you can react toochanges quickly.</span></span> <span data-ttu-id="d761e-121">Time Series Insights 協助您深入地了解感應器資料，它會協助您快速找出趨勢和異常狀況，進行複雜的根本原因分析，並避免耗費成本的停機時間。</span><span class="sxs-lookup"><span data-stu-id="d761e-121">Time Series Insights helps you gain deep insights into your sensor data by helping you spot trends and anomalies quickly, conduct complex root-cause analyses, and avoid costly downtime.</span></span> <span data-ttu-id="d761e-122">藉由啟用交叉相互關聯之間即時和歷史資料，時間序列 Insights 可協助您解除鎖定隱藏的 hello 資料中的趨勢。</span><span class="sxs-lookup"><span data-stu-id="d761e-122">By enabling cross-correlation between real-time and historical data, Time Series Insights helps you unlock hidden trends in hello data.</span></span>

* <span data-ttu-id="d761e-123">**建置自訂解決方案**：將 Azure Time Series Insights 資料內嵌至現有應用程式，或使用 Time Series Insights REST API 建立新的自訂解決方案。</span><span class="sxs-lookup"><span data-stu-id="d761e-123">**Build custom solutions**: Embed Azure Time Series Insights data into your existing applications, or create new custom solutions with Time Series Insights REST APIs.</span></span> <span data-ttu-id="d761e-124">建立及共用個人化檢視，您可以共用其他 tooexplore 您探索。</span><span class="sxs-lookup"><span data-stu-id="d761e-124">Creating and sharing personalized views you can share for others tooexplore your discoveries.</span></span>

* <span data-ttu-id="d761e-125">**延展性**： 時間序列 Insights 是大規模的設計的 toosupport IoT。</span><span class="sxs-lookup"><span data-stu-id="d761e-125">**Scalability**: Time Series Insights is designed toosupport IoT at scale.</span></span> <span data-ttu-id="d761e-126">在預覽中，可以輸入從 1 百萬個 too100 百萬個事件每天，使用預設保留跨越的 31 天。</span><span class="sxs-lookup"><span data-stu-id="d761e-126">In Preview, it can ingress from 1 million too100 million events per day, with a default retention span of 31 days.</span></span> <span data-ttu-id="d761e-127">您可以用近乎即時的方式，來為即時資料流以及大量的歷史資料呈現視覺效果並對其進行分析。</span><span class="sxs-lookup"><span data-stu-id="d761e-127">You can visualize and analyze live data streams in near real-time, alongside vast amounts of historical data.</span></span> <span data-ttu-id="d761e-128">向前移動，輸入與保留的速度將會增加 tooaccommodate 不斷演變的企業規模。</span><span class="sxs-lookup"><span data-stu-id="d761e-128">Moving forward, ingress and retention rates will increase tooaccommodate an ever evolving enterprise scale.</span></span>

## <a name="time-series-insights-glossary"></a><span data-ttu-id="d761e-129">Time Series Insights 詞彙</span><span class="sxs-lookup"><span data-stu-id="d761e-129">Time Series Insights glossary</span></span>

* <span data-ttu-id="d761e-130">**環境**︰環境是具有輸入和儲存容量的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d761e-130">**Environment**: An environment is an Azure resource with ingress and storage capacity.</span></span>  <span data-ttu-id="d761e-131">客戶佈建透過 hello 與它們所需容量的 Azure 入口網站的環境。</span><span class="sxs-lookup"><span data-stu-id="d761e-131">Customers provision environments through hello Azure portal with their required capacity.</span></span>
* <span data-ttu-id="d761e-132">**事件來源**：事件來源衍生自事件代理人，例如 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="d761e-132">**Event Source**: An Event Source is derived from an event broker, like Azure Event Hubs.</span></span>  <span data-ttu-id="d761e-133">時間序列 Insights 直接連接 tooEvent 來源，而不需要撰寫任何程式碼擷取 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="d761e-133">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without writing any code.</span></span> <span data-ttu-id="d761e-134">目前，Time Series Insights 支援 Azure 事件中樞與 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d761e-134">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span>
* <span data-ttu-id="d761e-135">**參考資料**： 時間序列 Insights 提供使用者 hello 能力 toojoin 時間序列資料與參考資料。</span><span class="sxs-lookup"><span data-stu-id="d761e-135">**Reference data**: Time Series Insights provides users hello ability toojoin time series data with reference data.</span></span>  <span data-ttu-id="d761e-136">參考資料可以包含關於裝置的中繼資料，也可以包含其他較不常變更的靜態資料。</span><span class="sxs-lookup"><span data-stu-id="d761e-136">Reference data can include metadata about devices, or other static data that changes relatively infrequently.</span></span> <span data-ttu-id="d761e-137">時間序列 Insights 聯結可讓使用者 toovisualize hello 與資料流的參考資料和分析此資料接近即時。</span><span class="sxs-lookup"><span data-stu-id="d761e-137">Time Series Insights joins hello reference data with data streams, allowing users toovisualize and analyze this data in near real-time.</span></span>
