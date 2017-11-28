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
# <a name="available-event-hubs-apis"></a><span data-ttu-id="31881-103">可用的事件中樞 API</span><span class="sxs-lookup"><span data-stu-id="31881-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="31881-104">執行階段 API</span><span class="sxs-lookup"><span data-stu-id="31881-104">Runtime APIs</span></span>

<span data-ttu-id="31881-105">hello 以下是所有目前可用的 Azure 事件中心執行階段用戶端的描述。</span><span class="sxs-lookup"><span data-stu-id="31881-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="31881-106">雖然某些這些程式庫也包含有限的管理功能，但在[特定文件庫](#management-apis)專用 toomanagement 作業。</span><span class="sxs-lookup"><span data-stu-id="31881-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="31881-107">這些程式庫的 hello 核心焦點是 toosend，和從事件中心接收訊息。</span><span class="sxs-lookup"><span data-stu-id="31881-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="31881-108">請參閱[更多資訊](#additional-information)如需有關每個執行階段程式庫的 hello 目前狀態。</span><span class="sxs-lookup"><span data-stu-id="31881-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="31881-109">語言/平台</span><span class="sxs-lookup"><span data-stu-id="31881-109">Language/Platform</span></span> | <span data-ttu-id="31881-110">用戶端封裝</span><span class="sxs-lookup"><span data-stu-id="31881-110">Client package</span></span> | <span data-ttu-id="31881-111">EventProcessorHost 封裝</span><span class="sxs-lookup"><span data-stu-id="31881-111">EventProcessorHost package</span></span> | <span data-ttu-id="31881-112">存放庫</span><span class="sxs-lookup"><span data-stu-id="31881-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="31881-113">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="31881-113">.NET Standard</span></span> | [<span data-ttu-id="31881-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="31881-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="31881-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="31881-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="31881-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="31881-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="31881-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="31881-117">.NET Framework</span></span> | [<span data-ttu-id="31881-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="31881-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="31881-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="31881-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="31881-120">N/A</span><span class="sxs-lookup"><span data-stu-id="31881-120">N/A</span></span> |
| <span data-ttu-id="31881-121">Java</span><span class="sxs-lookup"><span data-stu-id="31881-121">Java</span></span> | [<span data-ttu-id="31881-122">Maven</span><span class="sxs-lookup"><span data-stu-id="31881-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="31881-123">Maven</span><span class="sxs-lookup"><span data-stu-id="31881-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="31881-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="31881-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="31881-125">節點</span><span class="sxs-lookup"><span data-stu-id="31881-125">Node</span></span> | [<span data-ttu-id="31881-126">NPM</span><span class="sxs-lookup"><span data-stu-id="31881-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="31881-127">N/A</span><span class="sxs-lookup"><span data-stu-id="31881-127">N/A</span></span> | [<span data-ttu-id="31881-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="31881-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="31881-129">C</span><span class="sxs-lookup"><span data-stu-id="31881-129">C</span></span> | <span data-ttu-id="31881-130">N/A</span><span class="sxs-lookup"><span data-stu-id="31881-130">N/A</span></span> | <span data-ttu-id="31881-131">N/A</span><span class="sxs-lookup"><span data-stu-id="31881-131">N/A</span></span> | [<span data-ttu-id="31881-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="31881-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="31881-133">其他資訊</span><span class="sxs-lookup"><span data-stu-id="31881-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="31881-134">.NET</span><span class="sxs-lookup"><span data-stu-id="31881-134">.NET</span></span>
<span data-ttu-id="31881-135">hello.NET 生態系統有多個執行階段，因此有多個.NET 程式庫建立事件中樞。</span><span class="sxs-lookup"><span data-stu-id="31881-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="31881-136">hello.NET Framework 程式庫的類型只能在.NET Framework 環境中執行時，使用.NET 核心或 hello.NET Framework 中，可以執行 hello.NET 標準程式庫。</span><span class="sxs-lookup"><span data-stu-id="31881-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="31881-137">如需 .NET Framework 的詳細資訊，請參閱[架構版本](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions)。</span><span class="sxs-lookup"><span data-stu-id="31881-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="31881-138">節點</span><span class="sxs-lookup"><span data-stu-id="31881-138">Node</span></span>

<span data-ttu-id="31881-139">hello Node.js 程式庫目前為預覽狀態，並由 Microsoft 員工和外部提供者維護為戶端專案。</span><span class="sxs-lookup"><span data-stu-id="31881-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="31881-140">我們非常歡迎所有的參與，包括原始程式碼，而且都會加以檢閱。</span><span class="sxs-lookup"><span data-stu-id="31881-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="31881-141">管理 API</span><span class="sxs-lookup"><span data-stu-id="31881-141">Management APIs</span></span>

<span data-ttu-id="31881-142">hello 下列是所有目前可用的管理特定的程式庫的清單。</span><span class="sxs-lookup"><span data-stu-id="31881-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="31881-143">沒有任何這些程式庫包含執行階段作業，而且對於 hello 唯一用途就是管理事件中心的實體。</span><span class="sxs-lookup"><span data-stu-id="31881-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="31881-144">語言/平台</span><span class="sxs-lookup"><span data-stu-id="31881-144">Language/Platform</span></span> | <span data-ttu-id="31881-145">管理封裝</span><span class="sxs-lookup"><span data-stu-id="31881-145">Management package</span></span> | <span data-ttu-id="31881-146">存放庫</span><span class="sxs-lookup"><span data-stu-id="31881-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="31881-147">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="31881-147">.NET Standard</span></span> | [<span data-ttu-id="31881-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="31881-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="31881-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="31881-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="31881-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31881-150">Next steps</span></span>
<span data-ttu-id="31881-151">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="31881-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="31881-152">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="31881-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="31881-153">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="31881-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="31881-154">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="31881-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)