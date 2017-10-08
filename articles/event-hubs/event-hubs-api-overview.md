---
title: "aaaAzure 事件中心 API 概觀 |Microsoft 文件"
description: "可用的 Azure 事件中樞 API 概觀"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a>可用的事件中樞 API

## <a name="runtime-apis"></a>執行階段 API

hello 以下是所有目前可用的 Azure 事件中心執行階段用戶端的描述。 雖然某些這些程式庫也包含有限的管理功能，但在[特定文件庫](#management-apis)專用 toomanagement 作業。 這些程式庫的 hello 核心焦點是 toosend，和從事件中心接收訊息。

請參閱[更多資訊](#additional-information)如需有關每個執行階段程式庫的 hello 目前狀態。

| 語言/平台 | 用戶端封裝 | EventProcessorHost 封裝 | 存放庫 |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET Framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | N/A |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| 節點 | [NPM](https://www.npmjs.com/package/azure-event-hubs) | N/A | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | N/A | N/A | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>其他資訊

#### <a name="net"></a>.NET
hello.NET 生態系統有多個執行階段，因此有多個.NET 程式庫建立事件中樞。 hello.NET Framework 程式庫的類型只能在.NET Framework 環境中執行時，使用.NET 核心或 hello.NET Framework 中，可以執行 hello.NET 標準程式庫。 如需 .NET Framework 的詳細資訊，請參閱[架構版本](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions)。

#### <a name="node"></a>節點

hello Node.js 程式庫目前為預覽狀態，並由 Microsoft 員工和外部提供者維護為戶端專案。 我們非常歡迎所有的參與，包括原始程式碼，而且都會加以檢閱。

## <a name="management-apis"></a>管理 API

hello 下列是所有目前可用的管理特定的程式庫的清單。 沒有任何這些程式庫包含執行階段作業，而且對於 hello 唯一用途就是管理事件中心的實體。

| 語言/平台 | 管理封裝 | 存放庫 |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
* [事件中樞常見問題集](event-hubs-faq.md)