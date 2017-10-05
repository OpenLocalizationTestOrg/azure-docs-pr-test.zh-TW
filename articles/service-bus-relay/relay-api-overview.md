---
title: "Azure 轉送 API 概觀 | Microsoft Docs"
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
ms.openlocfilehash: 8d93a0344adc3b0b7617f3a7d85124142d7a7555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="0109f-103">可用的轉送 API</span><span class="sxs-lookup"><span data-stu-id="0109f-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="0109f-104">執行階段 API</span><span class="sxs-lookup"><span data-stu-id="0109f-104">Runtime APIs</span></span>

<span data-ttu-id="0109f-105">下表列出所有目前可用的轉送執行階段用戶端。</span><span class="sxs-lookup"><span data-stu-id="0109f-105">The following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="0109f-106">[更多資訊](#additional-information)章節包含每個執行階段程式庫之狀態的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0109f-106">The [additional information](#additional-information) section contains more information about the status of each runtime library.</span></span>

| <span data-ttu-id="0109f-107">語言/平台</span><span class="sxs-lookup"><span data-stu-id="0109f-107">Language/Platform</span></span> | <span data-ttu-id="0109f-108">可用的功能</span><span class="sxs-lookup"><span data-stu-id="0109f-108">Available feature</span></span> | <span data-ttu-id="0109f-109">用戶端封裝</span><span class="sxs-lookup"><span data-stu-id="0109f-109">Client package</span></span> | <span data-ttu-id="0109f-110">存放庫</span><span class="sxs-lookup"><span data-stu-id="0109f-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0109f-111">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="0109f-111">.NET Standard</span></span> | <span data-ttu-id="0109f-112">混合式連線</span><span class="sxs-lookup"><span data-stu-id="0109f-112">Hybrid Connections</span></span> | [<span data-ttu-id="0109f-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="0109f-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="0109f-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="0109f-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="0109f-115">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0109f-115">.NET Framework</span></span> | <span data-ttu-id="0109f-116">WCF 轉送</span><span class="sxs-lookup"><span data-stu-id="0109f-116">WCF Relay</span></span> | [<span data-ttu-id="0109f-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="0109f-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="0109f-118">N/A</span><span class="sxs-lookup"><span data-stu-id="0109f-118">N/A</span></span> |
| <span data-ttu-id="0109f-119">節點</span><span class="sxs-lookup"><span data-stu-id="0109f-119">Node</span></span> | <span data-ttu-id="0109f-120">混合式連線</span><span class="sxs-lookup"><span data-stu-id="0109f-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="0109f-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="0109f-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="0109f-122">其他資訊</span><span class="sxs-lookup"><span data-stu-id="0109f-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="0109f-123">.NET</span><span class="sxs-lookup"><span data-stu-id="0109f-123">.NET</span></span>
<span data-ttu-id="0109f-124">.NET 生態系統有多個執行階段，因此有多個適用於事件中樞的 .NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="0109f-124">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="0109f-125">.NET Standard 程式庫可使用 .NET Core 或 .NET Framework 執行，然而 .NET Framework 程式庫只能在 .NET Framework 環境中執行。</span><span class="sxs-lookup"><span data-stu-id="0109f-125">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="0109f-126">如需 .NET Framework 的詳細資訊，請參閱[架構版本](/dotnet/articles/standard/frameworks#framework-versions)。</span><span class="sxs-lookup"><span data-stu-id="0109f-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0109f-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0109f-127">Next steps</span></span>
<span data-ttu-id="0109f-128">若要深入了解 Azure 轉送，請造訪下列連結：</span><span class="sxs-lookup"><span data-stu-id="0109f-128">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="0109f-129">什麼是 Azure 轉送？</span><span class="sxs-lookup"><span data-stu-id="0109f-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="0109f-130">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="0109f-130">Relay FAQ</span></span>](relay-faq.md)