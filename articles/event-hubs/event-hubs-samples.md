---
title: "aaaAzure 事件中心範例 |Microsoft 文件"
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
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="52499-103">事件中樞範例</span><span class="sxs-lookup"><span data-stu-id="52499-103">Event Hubs samples</span></span> 

<span data-ttu-id="52499-104">hello 組 Azure 事件中樞的範例示範中的主要功能[Azure 事件中心](/azure/event-hubs/)。</span><span class="sxs-lookup"><span data-stu-id="52499-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="52499-105">這篇文章分類，並說明可用的連結 tooeach hello 範例。</span><span class="sxs-lookup"><span data-stu-id="52499-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="52499-106">在 hello 撰寫本文時，事件中心範例位於許多不同的地方：</span><span class="sxs-lookup"><span data-stu-id="52499-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="52499-107">MSDN 開發人員程式碼範例</span><span class="sxs-lookup"><span data-stu-id="52499-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="52499-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="52499-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="52499-109">如需有關不同版本的 hello.NET Framework 的詳細資訊，請參閱[架構與目標](/dotnet/articles/standard/frameworks)。</span><span class="sxs-lookup"><span data-stu-id="52499-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="52499-110">更多的範例會隨時新增，所以請經常回到這裡查看更新。</span><span class="sxs-lookup"><span data-stu-id="52499-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="52499-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="52499-111">.NET Standard</span></span>

<span data-ttu-id="52499-112">hello 下列範例會示範如何 toosend 與接收事件使用 hello[事件中心用戶端](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md)hello [.NET 標準程式庫](/dotnet/articles/standard/library)。</span><span class="sxs-lookup"><span data-stu-id="52499-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="52499-113">傳送事件</span><span class="sxs-lookup"><span data-stu-id="52499-113">Send events</span></span> 

<span data-ttu-id="52499-114">hello[開始傳送](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender)範例會示範如何 toowrite.NET Core 主控台應用程式傳送事件 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="52499-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="52499-115">接收事件</span><span class="sxs-lookup"><span data-stu-id="52499-115">Receive events</span></span> 

<span data-ttu-id="52499-116">hello[開始接收以 hello 事件處理器主機](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver)範例是從使用 hello 事件處理器主機事件中心接收訊息的.NET Core 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="52499-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="52499-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="52499-117">.NET Framework</span></span>   

<span data-ttu-id="52499-118">這些範例會示範各種其他功能的 Azure 事件中樞，目標 hello [.NET Framework 程式庫](/dotnet/framework/index)。</span><span class="sxs-lookup"><span data-stu-id="52499-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="52499-119">通知使用者收到的事件</span><span class="sxs-lookup"><span data-stu-id="52499-119">Notify users of events received</span></span>

<span data-ttu-id="52499-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications)範例，通知使用者從感應器或其他系統收到的資料。</span><span class="sxs-lookup"><span data-stu-id="52499-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="52499-121">開始使用事件中心</span><span class="sxs-lookup"><span data-stu-id="52499-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="52499-122">hello[事件中心入門](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097)範例會示範事件中心而言，等方式 toocreate 事件中心，傳送事件 tooan 事件中心取用事件使用 hello hello 基本功能[事件處理器主機](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="52499-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="52499-123">相應放大事件處理</span><span class="sxs-lookup"><span data-stu-id="52499-123">Scale out event processing</span></span> 

<span data-ttu-id="52499-124">hello[擴充的事件處理](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3)範例會示範如何 toouse hello[事件處理器主機](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)toodistribute hello 工作負載事件中心資料流耗用量。</span><span class="sxs-lookup"><span data-stu-id="52499-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="52499-125">它會顯示如何 tooimplement hello **EventProcessor**和**EventProcessorFactory** toomanage hello 事件資料流物件。</span><span class="sxs-lookup"><span data-stu-id="52499-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="52499-126">將資料從 SQL 提取到事件中樞</span><span class="sxs-lookup"><span data-stu-id="52499-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="52499-127">hello[提取 SQL 資料](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql)範例會示範如何從 SQL toopull 資料資料表，並將它推送 tooan 事件中心 toouse 做為輸入，在下游分析應用程式。</span><span class="sxs-lookup"><span data-stu-id="52499-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="52499-128">將 Web 資料提取到事件中樞</span><span class="sxs-lookup"><span data-stu-id="52499-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="52499-129">hello[匯入資料，從 hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb)範例會示範如何從公用 toopull 資料摘要 （例如 hello 部門的運輸工具的流量資訊摘要），並將它推送 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="52499-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52499-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52499-130">Next steps</span></span>

<span data-ttu-id="52499-131">深入了解.NET Framework 版本瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="52499-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="52499-132">架構與目標</span><span class="sxs-lookup"><span data-stu-id="52499-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="52499-133">.NET Framework 4.6 和 4.5</span><span class="sxs-lookup"><span data-stu-id="52499-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="52499-134">您可以進一步了解事件中心 hello 下列文章中：</span><span class="sxs-lookup"><span data-stu-id="52499-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="52499-135">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="52499-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="52499-136">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="52499-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="52499-137">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="52499-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)