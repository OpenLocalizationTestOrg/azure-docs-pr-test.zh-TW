---
title: "Azure 事件中樞 API 概觀 | Microsoft Docs"
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
ms.openlocfilehash: 40cd76e1aacb68d6051cae4a3c90a8970f5449f0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="available-event-hubs-apis"></a><span data-ttu-id="08c45-103">可用的事件中樞 API</span><span class="sxs-lookup"><span data-stu-id="08c45-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="08c45-104">執行階段 API</span><span class="sxs-lookup"><span data-stu-id="08c45-104">Runtime APIs</span></span>

<span data-ttu-id="08c45-105">以下是所有目前可用之 Azure 事件中樞執行階段用戶端的說明。</span><span class="sxs-lookup"><span data-stu-id="08c45-105">The following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="08c45-106">雖然這些程式庫其中也包括有限的管理功能，但也有專用於管理作業的[特定程式庫](#management-apis)。</span><span class="sxs-lookup"><span data-stu-id="08c45-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated to management operations.</span></span> <span data-ttu-id="08c45-107">這些程式庫的核心重點是從事件中樞傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="08c45-107">The core focus of these libraries is to send and receive messages from an event hub.</span></span>

<span data-ttu-id="08c45-108">如需每個執行階段程式庫目前狀態的詳細資料，請參閱[其他資訊](#additional-information)。</span><span class="sxs-lookup"><span data-stu-id="08c45-108">See [additional information](#additional-information) for more details on the current status of each runtime library.</span></span>

| <span data-ttu-id="08c45-109">語言/平台</span><span class="sxs-lookup"><span data-stu-id="08c45-109">Language/Platform</span></span> | <span data-ttu-id="08c45-110">用戶端封裝</span><span class="sxs-lookup"><span data-stu-id="08c45-110">Client package</span></span> | <span data-ttu-id="08c45-111">EventProcessorHost 封裝</span><span class="sxs-lookup"><span data-stu-id="08c45-111">EventProcessorHost package</span></span> | <span data-ttu-id="08c45-112">存放庫</span><span class="sxs-lookup"><span data-stu-id="08c45-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c45-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="08c45-113">.NET Standard</span></span> | [<span data-ttu-id="08c45-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="08c45-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="08c45-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="08c45-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="08c45-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="08c45-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="08c45-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="08c45-117">.NET Framework</span></span> | [<span data-ttu-id="08c45-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="08c45-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="08c45-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="08c45-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="08c45-120">N/A</span><span class="sxs-lookup"><span data-stu-id="08c45-120">N/A</span></span> |
| <span data-ttu-id="08c45-121">Java</span><span class="sxs-lookup"><span data-stu-id="08c45-121">Java</span></span> | [<span data-ttu-id="08c45-122">Maven</span><span class="sxs-lookup"><span data-stu-id="08c45-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="08c45-123">Maven</span><span class="sxs-lookup"><span data-stu-id="08c45-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="08c45-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="08c45-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="08c45-125">節點</span><span class="sxs-lookup"><span data-stu-id="08c45-125">Node</span></span> | [<span data-ttu-id="08c45-126">NPM</span><span class="sxs-lookup"><span data-stu-id="08c45-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="08c45-127">N/A</span><span class="sxs-lookup"><span data-stu-id="08c45-127">N/A</span></span> | [<span data-ttu-id="08c45-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="08c45-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="08c45-129">C</span><span class="sxs-lookup"><span data-stu-id="08c45-129">C</span></span> | <span data-ttu-id="08c45-130">N/A</span><span class="sxs-lookup"><span data-stu-id="08c45-130">N/A</span></span> | <span data-ttu-id="08c45-131">N/A</span><span class="sxs-lookup"><span data-stu-id="08c45-131">N/A</span></span> | [<span data-ttu-id="08c45-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="08c45-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="08c45-133">其他資訊</span><span class="sxs-lookup"><span data-stu-id="08c45-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="08c45-134">.NET</span><span class="sxs-lookup"><span data-stu-id="08c45-134">.NET</span></span>
<span data-ttu-id="08c45-135">.NET 生態系統有多個執行階段，因此有多個適用於事件中樞的 .NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="08c45-135">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="08c45-136">.NET Standard 程式庫可使用 .NET Core 或 .NET Framework 執行，然而 .NET Framework 程式庫只能在 .NET Framework 環境中執行。</span><span class="sxs-lookup"><span data-stu-id="08c45-136">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="08c45-137">如需 .NET Framework 的詳細資訊，請參閱[架構版本](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions)。</span><span class="sxs-lookup"><span data-stu-id="08c45-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="08c45-138">節點</span><span class="sxs-lookup"><span data-stu-id="08c45-138">Node</span></span>

<span data-ttu-id="08c45-139">Node.js 程式庫目前為預覽版，並且由 Microsoft 員工和外部參與者當作業餘專案維護。</span><span class="sxs-lookup"><span data-stu-id="08c45-139">The Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="08c45-140">我們非常歡迎所有的參與，包括原始程式碼，而且都會加以檢閱。</span><span class="sxs-lookup"><span data-stu-id="08c45-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="08c45-141">管理 API</span><span class="sxs-lookup"><span data-stu-id="08c45-141">Management APIs</span></span>

<span data-ttu-id="08c45-142">以下是目前所有可用的管理特定程式庫清單。</span><span class="sxs-lookup"><span data-stu-id="08c45-142">The following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="08c45-143">這些程式庫都不包含執行階段作業，而且唯一的用途是管理事件中樞項目。</span><span class="sxs-lookup"><span data-stu-id="08c45-143">None of these libraries contain runtime operations, and are for the sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="08c45-144">語言/平台</span><span class="sxs-lookup"><span data-stu-id="08c45-144">Language/Platform</span></span> | <span data-ttu-id="08c45-145">管理封裝</span><span class="sxs-lookup"><span data-stu-id="08c45-145">Management package</span></span> | <span data-ttu-id="08c45-146">存放庫</span><span class="sxs-lookup"><span data-stu-id="08c45-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08c45-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="08c45-147">.NET Standard</span></span> | [<span data-ttu-id="08c45-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="08c45-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="08c45-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="08c45-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="08c45-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08c45-150">Next steps</span></span>
<span data-ttu-id="08c45-151">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="08c45-151">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="08c45-152">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="08c45-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="08c45-153">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="08c45-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="08c45-154">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="08c45-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)