---
title: "Azure 事件中樞範例 | Microsoft Docs"
description: "Azure 事件中樞範例"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="a642a-103">事件中樞範例</span><span class="sxs-lookup"><span data-stu-id="a642a-103">Event Hubs samples</span></span> 

<span data-ttu-id="a642a-104">「Azure 事件中樞」範例集示範 [Azure 事件中樞](/azure/event-hubs/)中的主要功能。</span><span class="sxs-lookup"><span data-stu-id="a642a-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="a642a-105">本主題分類及描述可用的範例與每個範例的連結。</span><span class="sxs-lookup"><span data-stu-id="a642a-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="a642a-106">在撰寫本文時，事件中樞範例位於數個不同的位置：</span><span class="sxs-lookup"><span data-stu-id="a642a-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="a642a-107">MSDN 開發人員程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a642a-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="a642a-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="a642a-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="a642a-109">如需不同版本的 .NET Framework 的詳細資訊，請參閱[架構與目標](/dotnet/articles/standard/frameworks)。</span><span class="sxs-lookup"><span data-stu-id="a642a-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="a642a-110">更多的範例會隨時新增，所以請經常回到這裡查看更新。</span><span class="sxs-lookup"><span data-stu-id="a642a-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="a642a-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="a642a-111">.NET Standard</span></span>

<span data-ttu-id="a642a-112">下列範例會示範如何使用 [.NET Standard 程式庫](/dotnet/articles/standard/library)的[事件中樞用戶端](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md)傳送與接收事件。</span><span class="sxs-lookup"><span data-stu-id="a642a-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="a642a-113">傳送事件</span><span class="sxs-lookup"><span data-stu-id="a642a-113">Send events</span></span> 

<span data-ttu-id="a642a-114">[開始傳送](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender)範例示範如何撰寫一個 .NET Core 主控台應用程式，以將事件傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="a642a-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="a642a-115">接收事件</span><span class="sxs-lookup"><span data-stu-id="a642a-115">Receive events</span></span> 

<span data-ttu-id="a642a-116">[開始使用事件處理器主機接收](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver)範例是一個 .NET Core 主控台應用程式，可使用事件處理器主機從事件中樞接收訊息。</span><span class="sxs-lookup"><span data-stu-id="a642a-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="a642a-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a642a-117">.NET Framework</span></span>   

<span data-ttu-id="a642a-118">這些範例會示範 Azure 事件中樞的各種其他功能，以 [.NET Framework 程式庫](/dotnet/framework/index)為目標。</span><span class="sxs-lookup"><span data-stu-id="a642a-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="a642a-119">通知使用者收到的事件</span><span class="sxs-lookup"><span data-stu-id="a642a-119">Notify users of events received</span></span>

<span data-ttu-id="a642a-120">[AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) 範例通知使用者從感應器或其他系統接收到的資料。</span><span class="sxs-lookup"><span data-stu-id="a642a-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="a642a-121">開始使用事件中心</span><span class="sxs-lookup"><span data-stu-id="a642a-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="a642a-122">[開始使用事件中樞](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097)範例示範「事件中樞」的基本功能，例如如何建立事件中樞、將事件傳送到事件中樞，以及使用[事件處理器主機](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)來取用事件。</span><span class="sxs-lookup"><span data-stu-id="a642a-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="a642a-123">相應放大事件處理</span><span class="sxs-lookup"><span data-stu-id="a642a-123">Scale out event processing</span></span> 

<span data-ttu-id="a642a-124">[相應放大事件處理](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3)範例示範如何使用 [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) 來分散事件中樞資料流耗用量的工作負載。</span><span class="sxs-lookup"><span data-stu-id="a642a-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="a642a-125">它示範如何實作 **EventProcessor** 和 **EventProcessorFactory** 物件，以管理事件資料流。</span><span class="sxs-lookup"><span data-stu-id="a642a-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="a642a-126">將資料從 SQL 提取到事件中樞</span><span class="sxs-lookup"><span data-stu-id="a642a-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="a642a-127">[提取 SQL 資料](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql)範例示範如何從 SQL 資料表提取資料並將資料推送到事件中樞，以作為下游分析應用程式中的輸入。</span><span class="sxs-lookup"><span data-stu-id="a642a-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="a642a-128">將 Web 資料提取到事件中樞</span><span class="sxs-lookup"><span data-stu-id="a642a-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="a642a-129">[從 Web 匯入資料](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb)範例示範如何從公用摘要 (例如交通部的交通資訊摘要) 提取資料並將資料推送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="a642a-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a642a-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a642a-130">Next steps</span></span>

<span data-ttu-id="a642a-131">請造訪下列連結深入了解 .NET Framework 版本︰</span><span class="sxs-lookup"><span data-stu-id="a642a-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="a642a-132">架構與目標</span><span class="sxs-lookup"><span data-stu-id="a642a-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="a642a-133">.NET Framework 4.6 和 4.5</span><span class="sxs-lookup"><span data-stu-id="a642a-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="a642a-134">您可以參閱下列文章，深入了解事件中樞：</span><span class="sxs-lookup"><span data-stu-id="a642a-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="a642a-135">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="a642a-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="a642a-136">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="a642a-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="a642a-137">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="a642a-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)