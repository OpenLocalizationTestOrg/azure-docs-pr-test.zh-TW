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
# <a name="available-relay-apis"></a><span data-ttu-id="a9c8a-103">可用的轉送 API</span><span class="sxs-lookup"><span data-stu-id="a9c8a-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="a9c8a-104">執行階段 API</span><span class="sxs-lookup"><span data-stu-id="a9c8a-104">Runtime APIs</span></span>

<span data-ttu-id="a9c8a-105">hello 下表列出所有目前可用的轉送執行階段用戶端。</span><span class="sxs-lookup"><span data-stu-id="a9c8a-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="a9c8a-106">hello[更多資訊](#additional-information)> 一節包含每個執行階段程式庫 hello 狀態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a9c8a-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="a9c8a-107">語言/平台</span><span class="sxs-lookup"><span data-stu-id="a9c8a-107">Language/Platform</span></span> | <span data-ttu-id="a9c8a-108">可用的功能</span><span class="sxs-lookup"><span data-stu-id="a9c8a-108">Available feature</span></span> | <span data-ttu-id="a9c8a-109">用戶端封裝</span><span class="sxs-lookup"><span data-stu-id="a9c8a-109">Client package</span></span> | <span data-ttu-id="a9c8a-110">存放庫</span><span class="sxs-lookup"><span data-stu-id="a9c8a-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a9c8a-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="a9c8a-111">.NET Standard</span></span> | <span data-ttu-id="a9c8a-112">混合式連線</span><span class="sxs-lookup"><span data-stu-id="a9c8a-112">Hybrid Connections</span></span> | [<span data-ttu-id="a9c8a-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="a9c8a-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="a9c8a-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="a9c8a-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="a9c8a-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a9c8a-115">.NET Framework</span></span> | <span data-ttu-id="a9c8a-116">WCF 轉送</span><span class="sxs-lookup"><span data-stu-id="a9c8a-116">WCF Relay</span></span> | [<span data-ttu-id="a9c8a-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="a9c8a-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="a9c8a-118">N/A</span><span class="sxs-lookup"><span data-stu-id="a9c8a-118">N/A</span></span> |
| <span data-ttu-id="a9c8a-119">節點</span><span class="sxs-lookup"><span data-stu-id="a9c8a-119">Node</span></span> | <span data-ttu-id="a9c8a-120">混合式連線</span><span class="sxs-lookup"><span data-stu-id="a9c8a-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="a9c8a-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="a9c8a-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="a9c8a-122">其他資訊</span><span class="sxs-lookup"><span data-stu-id="a9c8a-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="a9c8a-123">.NET</span><span class="sxs-lookup"><span data-stu-id="a9c8a-123">.NET</span></span>
<span data-ttu-id="a9c8a-124">hello.NET 生態系統有多個執行階段，因此有多個.NET 程式庫建立事件中樞。</span><span class="sxs-lookup"><span data-stu-id="a9c8a-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="a9c8a-125">hello.NET Framework 程式庫的類型只能在.NET Framework 環境中執行時，使用.NET 核心或 hello.NET Framework 中，可以執行 hello.NET 標準程式庫。</span><span class="sxs-lookup"><span data-stu-id="a9c8a-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="a9c8a-126">如需 .NET Framework 的詳細資訊，請參閱[架構版本](/dotnet/articles/standard/frameworks#framework-versions)。</span><span class="sxs-lookup"><span data-stu-id="a9c8a-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9c8a-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9c8a-127">Next steps</span></span>
<span data-ttu-id="a9c8a-128">toolearn 深入了解 Azure 轉送，請前往下列連結：</span><span class="sxs-lookup"><span data-stu-id="a9c8a-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="a9c8a-129">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="a9c8a-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="a9c8a-130">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="a9c8a-130">Relay FAQ</span></span>](relay-faq.md)