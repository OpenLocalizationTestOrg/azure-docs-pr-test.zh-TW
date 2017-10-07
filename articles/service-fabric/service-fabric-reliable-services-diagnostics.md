---
title: "aaaStateful 可靠 Services 診斷 |Microsoft 文件"
description: "具狀態 Reliable Services 診斷功能"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>具狀態 Reliable Services 診斷功能
hello 可設定狀態的可靠的服務 StatefulServiceBase 類別發出[EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)事件可能是使用的 toodebug hello 服務，提供深入了解如何運作，hello runtime，協助您進行疑難排解。

## <a name="eventsource-events"></a>EventSource 事件
hello 可設定狀態的可靠的服務 StatefulServiceBase 類別 hello EventSource 名稱是 「 Microsoft-ServiceFabric-服務 」。 這個事件來源的事件會出現在[診斷事件](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio)正在 hello 服務時，視窗[在 Visual Studio 中偵錯](service-fabric-debugging-your-application.md)。

可協助您收集和/或檢視 EventSource 事件之工具和技術的範例包括 [PerfView](http://www.microsoft.com/download/details.aspx?id=28567)、[Microsoft Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)和 [Microsoft TraceEvent 程式庫](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent)。

## <a name="events"></a>事件
| 事件名稱 | 事件識別碼 | Level | 事件說明 |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |資訊 |啟動服務 RunAsync 工作時發出 |
| StatefulRunAsyncCancellation |2 |資訊 |取消服務 RunAsync 工作時發出 |
| StatefulRunAsyncCompletion |3 |資訊 |完成服務 RunAsync 工作時發出 |
| StatefulRunAsyncSlowCancellation |4 |警告 |當服務 RunAsync 工作花費過長 toocomplete 取消時，就發出 |
| StatefulRunAsyncFailure |5 |錯誤 |服務 RunAsync 工作擲回例外狀況時發出 |

## <a name="interpret-events"></a>解譯事件
StatefulRunAsyncInvocation、 StatefulRunAsyncCompletion 和 StatefulRunAsyncCancellation 事件會很有用的 toohello 服務寫入器 toounderstand hello 的生命週期服務--，以及當啟動、 已取消，或已完成服務的 hello 時間. 偵錯服務問題或了解 hello 服務生命週期時，這非常有用。

服務寫入器應該特別注意 tooStatefulRunAsyncSlowCancellation 和 StatefulRunAsyncFailure 事件，因為它們表示 hello 服務的問題。

只要 hello 服務 RunAsync() 工作擲回例外狀況，就會發出 StatefulRunAsyncFailure。 通常，擲回例外狀況表示發生錯誤或 hello 服務中的 bug。 此外，hello 例外狀況會導致 hello 服務 toofail，因此它是移動的 tooa 不同節點。 這是很昂貴的作業，並 hello 服務移動時，可以延遲傳入的要求。 服務寫入器應該判斷 hello hello 例外狀況的原因，可能的話，請減少這種情況。

只要 hello RunAsync 工作的取消要求費時超過 4 秒，就會發出 StatefulRunAsyncSlowCancellation。 當服務會花太長 toocomplete 取消作業時，它會影響 hello hello 服務 toobe 快速地重新啟動另一個節點上的能力。 這可能會影響 hello hello 服務的整體可用性。

## <a name="next-steps"></a>後續步驟
* [PerfView 中的 EventSource 提供者](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
