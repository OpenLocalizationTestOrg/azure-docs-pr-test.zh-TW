---
title: "aaaWhat 是 Azure 事件中樞與為何使用 |Microsoft 文件"
description: "概觀和簡介 tooAzure 事件中心的雲端規模遙測擷取，從網站、 應用程式和裝置"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="375ef-103">何謂事件中樞？</span><span class="sxs-lookup"><span data-stu-id="375ef-103">What is Event Hubs?</span></span>

<span data-ttu-id="375ef-104">Azure 事件中樞是可高度調整的資料串流平台，以及每秒能夠接收和處理數百萬個事件的事件內嵌服務。</span><span class="sxs-lookup"><span data-stu-id="375ef-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="375ef-105">事件中樞可以處理及儲存分散式軟體和裝置所產生的事件、資料或遙測。</span><span class="sxs-lookup"><span data-stu-id="375ef-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="375ef-106">資料會傳送 tooan 事件中心可以轉換及儲存使用任何即時的分析提供者或批次/儲存體介面卡。</span><span class="sxs-lookup"><span data-stu-id="375ef-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="375ef-107">與 hello 能力 tooprovide[發佈-訂閱功能](https://msdn.microsoft.com/library/aa560414.aspx)巨量資料的低延遲與大規模事件中心做為 「 開啟遞增"hello。</span><span class="sxs-lookup"><span data-stu-id="375ef-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="375ef-108">為何使用事件中樞？</span><span class="sxs-lookup"><span data-stu-id="375ef-108">Why use Event Hubs?</span></span>

<span data-ttu-id="375ef-109">事件中樞的事件和遙測處理功能特別適用於︰</span><span class="sxs-lookup"><span data-stu-id="375ef-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="375ef-110">應用程式檢測</span><span class="sxs-lookup"><span data-stu-id="375ef-110">Application instrumentation</span></span>
* <span data-ttu-id="375ef-111">使用者經驗或工作流程處理</span><span class="sxs-lookup"><span data-stu-id="375ef-111">User experience or workflow processing</span></span>
* <span data-ttu-id="375ef-112">物聯網 (IoT) 案例</span><span class="sxs-lookup"><span data-stu-id="375ef-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="375ef-113">例如，事件中樞能追蹤行動應用程式中的行為、接收 Web 伺服陣列的流量資訊、擷取遊戲機遊戲中的遊戲內部事件，或是從產業用機器、連接的車輛或其他裝置收集遙測。</span><span class="sxs-lookup"><span data-stu-id="375ef-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="375ef-114">Azure 事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="375ef-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="375ef-115">hello 常見事件中心在解決方案架構中所扮演的角色是 「 前端 」 是事件管線，通常稱為 hello*事件擷取器*。</span><span class="sxs-lookup"><span data-stu-id="375ef-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="375ef-116">事件擷取器是元件或服務位於事件發行者 」 和 「 從 hello 中取用這些事件的事件資料流的事件取用者 toodecouple hello 生產之間。</span><span class="sxs-lookup"><span data-stu-id="375ef-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="375ef-117">hello 下圖說明這個架構：</span><span class="sxs-lookup"><span data-stu-id="375ef-117">hello following figure depicts this architecture:</span></span>

![事件中樞](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="375ef-119">事件中樞提供訊息串流處理能力，但特性迴異於傳統企業傳訊。</span><span class="sxs-lookup"><span data-stu-id="375ef-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="375ef-120">事件中樞功能是以高輸送量和事件處理案例為重點。</span><span class="sxs-lookup"><span data-stu-id="375ef-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="375ef-121">因此，事件中心是與不同[Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)傳訊，但未實作的一些 hello 功能可供[服務匯流排傳訊](/azure/service-bus-messaging/)實體，例如主題。</span><span class="sxs-lookup"><span data-stu-id="375ef-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="375ef-122">事件中樞功能</span><span class="sxs-lookup"><span data-stu-id="375ef-122">Event Hubs features</span></span>

<span data-ttu-id="375ef-123">事件中心包含下列索引鍵項目 hello:</span><span class="sxs-lookup"><span data-stu-id="375ef-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="375ef-124">[**事件產生者/發行者**](event-hubs-features.md#event-publishers)： 傳送資料 tooan 事件中心的實體。</span><span class="sxs-lookup"><span data-stu-id="375ef-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="375ef-125">透過 AMQP 1.0 或 HTTPS 發佈事件。</span><span class="sxs-lookup"><span data-stu-id="375ef-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="375ef-126">[**擷取**](event-hubs-features.md#capture)： 可讓您 toocapture 事件中心資料流處理資料，並將它儲存在 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="375ef-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="375ef-127">[**資料分割**](event-hubs-features.md#partitions)： 可讓每個取用者 tooonly 讀取的特定子集或資料分割，hello 事件資料流。</span><span class="sxs-lookup"><span data-stu-id="375ef-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="375ef-128">[**SAS 權杖**](event-hubs-features.md#sas-tokens)： 識別並驗證 hello 事件發行者。</span><span class="sxs-lookup"><span data-stu-id="375ef-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="375ef-129">[**事件取用者**](event-hubs-features.md#event-consumers)：任何從事件中樞讀取事件資料的實體。</span><span class="sxs-lookup"><span data-stu-id="375ef-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="375ef-130">事件取用者會透過 AMQP 1.0 連線。</span><span class="sxs-lookup"><span data-stu-id="375ef-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="375ef-131">[**取用者群組**](event-hubs-features.md#consumer-groups)： 提供取用應用程式與 hello 事件資料流的不同檢視，個別啟用這些取用者 tooact 每個倍數。</span><span class="sxs-lookup"><span data-stu-id="375ef-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="375ef-132">[**輸送量單位**](event-hubs-features.md#capacity)：預先購買的容量單位。</span><span class="sxs-lookup"><span data-stu-id="375ef-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="375ef-133">每個磁碟分割有 1 個輸送量單位的規模上限。</span><span class="sxs-lookup"><span data-stu-id="375ef-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="375ef-134">如需這些和其他事件中心功能的技術詳細資訊，請參閱 hello[事件中心功能概觀](event-hubs-features.md)。</span><span class="sxs-lookup"><span data-stu-id="375ef-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="375ef-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="375ef-135">Next steps</span></span>

<span data-ttu-id="375ef-136">如需詳細的事件中樞價格資訊，請參閱[事件中樞價格](https://azure.microsoft.com/pricing/details/event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="375ef-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="375ef-137">如需有關事件中心的詳細資訊，請造訪下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="375ef-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="375ef-138">開始使用[事件中樞教學課程](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="375ef-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="375ef-139">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="375ef-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="375ef-140">使用事件中樞的範例應用程式</span><span class="sxs-lookup"><span data-stu-id="375ef-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

