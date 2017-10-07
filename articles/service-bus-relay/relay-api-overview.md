---
title: "aaaAzure 轉送 API 概觀 |Microsoft 文件"
description: "可用的 Azure 轉送 API 概觀"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a>可用的轉送 API

## <a name="runtime-apis"></a>執行階段 API

hello 下表列出所有目前可用的轉送執行階段用戶端。

hello[更多資訊](#additional-information)> 一節包含每個執行階段程式庫 hello 狀態的詳細資訊。

| 語言/平台 | 可用的功能 | 用戶端封裝 | 存放庫 |
| --- | --- | --- | --- |
| .NET Standard | 混合式連線 | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET Framework | WCF 轉送 | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | N/A |
| 節點 | 混合式連線 | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>其他資訊

#### <a name="net"></a>.NET
hello.NET 生態系統有多個執行階段，因此有多個.NET 程式庫建立事件中樞。 hello.NET Framework 程式庫的類型只能在.NET Framework 環境中執行時，使用.NET 核心或 hello.NET Framework 中，可以執行 hello.NET 標準程式庫。 如需 .NET Framework 的詳細資訊，請參閱[架構版本](/dotnet/articles/standard/frameworks#framework-versions)。

## <a name="next-steps"></a>後續步驟
toolearn 深入了解 Azure 轉送，請前往下列連結：
* [什麼是 Azure 轉送？](relay-what-is-it.md)
* [轉送常見問題集](relay-faq.md)