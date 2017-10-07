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
# <a name="event-hubs-samples"></a>事件中樞範例 

hello 組 Azure 事件中樞的範例示範中的主要功能[Azure 事件中心](/azure/event-hubs/)。 這篇文章分類，並說明可用的連結 tooeach hello 範例。

在 hello 撰寫本文時，事件中心範例位於許多不同的地方：

- [MSDN 開發人員程式碼範例](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

如需有關不同版本的 hello.NET Framework 的詳細資訊，請參閱[架構與目標](/dotnet/articles/standard/frameworks)。

更多的範例會隨時新增，所以請經常回到這裡查看更新。

## <a name="net-standard"></a>.NET Standard

hello 下列範例會示範如何 toosend 與接收事件使用 hello[事件中心用戶端](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md)hello [.NET 標準程式庫](/dotnet/articles/standard/library)。

### <a name="send-events"></a>傳送事件 

hello[開始傳送](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender)範例會示範如何 toowrite.NET Core 主控台應用程式傳送事件 tooan 事件中心。

### <a name="receive-events"></a>接收事件 

hello[開始接收以 hello 事件處理器主機](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver)範例是從使用 hello 事件處理器主機事件中心接收訊息的.NET Core 主控台應用程式。

## <a name="net-framework"></a>.NET Framework   

這些範例會示範各種其他功能的 Azure 事件中樞，目標 hello [.NET Framework 程式庫](/dotnet/framework/index)。
 
### <a name="notify-users-of-events-received"></a>通知使用者收到的事件

hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications)範例，通知使用者從感應器或其他系統收到的資料。

### <a name="get-started-with-event-hubs"></a>開始使用事件中心 

hello[事件中心入門](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097)範例會示範事件中心而言，等方式 toocreate 事件中心，傳送事件 tooan 事件中心取用事件使用 hello hello 基本功能[事件處理器主機](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>相應放大事件處理 

hello[擴充的事件處理](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3)範例會示範如何 toouse hello[事件處理器主機](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)toodistribute hello 工作負載事件中心資料流耗用量。 它會顯示如何 tooimplement hello **EventProcessor**和**EventProcessorFactory** toomanage hello 事件資料流物件。 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>將資料從 SQL 提取到事件中樞

hello[提取 SQL 資料](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql)範例會示範如何從 SQL toopull 資料資料表，並將它推送 tooan 事件中心 toouse 做為輸入，在下游分析應用程式。

### <a name="pull-web-data-into-an-event-hub"></a>將 Web 資料提取到事件中樞 

hello[匯入資料，從 hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb)範例會示範如何從公用 toopull 資料摘要 （例如 hello 部門的運輸工具的流量資訊摘要），並將它推送 tooan 事件中心。

## <a name="next-steps"></a>後續步驟

深入了解.NET Framework 版本瀏覽下列連結查看 hello:

- [架構與目標](/dotnet/articles/standard/frameworks)
- [.NET Framework 4.6 和 4.5](/dotnet/framework/index)

您可以進一步了解事件中心 hello 下列文章中：

- [事件中樞概觀](event-hubs-what-is-event-hubs.md)
- [建立事件中樞](event-hubs-create.md)
- [事件中樞常見問題集](event-hubs-faq.md)