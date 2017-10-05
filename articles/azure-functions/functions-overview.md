---
title: "Azure Functions 概觀 | Microsoft Docs"
description: "了解如何使用 Azure Functions，在數分鐘內最佳化非同步的工作負載。"
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 4ca35962e9ff8320f74a28b62144e63f3022c6e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="an-introduction-to-azure-functions"></a><span data-ttu-id="27191-104">Azure Functions 簡介</span><span class="sxs-lookup"><span data-stu-id="27191-104">An introduction to Azure Functions</span></span>  
<span data-ttu-id="27191-105">Azure Functions 是可在雲端輕鬆執行程式碼片段或「函數」的解決方案。</span><span class="sxs-lookup"><span data-stu-id="27191-105">Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud.</span></span> <span data-ttu-id="27191-106">您可以只撰寫處理手邊問題所需的程式碼，而不需擔心要執行它的整個應用程式或基礎結構。</span><span class="sxs-lookup"><span data-stu-id="27191-106">You can write just the code you need for the problem at hand, without worrying about a whole application or the infrastructure to run it.</span></span> <span data-ttu-id="27191-107">Functions 可讓開發更有生產力，而且您可以使用您選擇的開發語言，例如 C#、F#、Node.js、Python 或 PHP。</span><span class="sxs-lookup"><span data-stu-id="27191-107">Functions can make development even more productive, and you can use your development language of choice, such as C#, F#, Node.js, Python or PHP.</span></span> <span data-ttu-id="27191-108">只需對您的程式碼執行的時間付費，並信任 Azure 視需要調整。</span><span class="sxs-lookup"><span data-stu-id="27191-108">Pay only for the time your code runs and trust Azure to scale as needed.</span></span> <span data-ttu-id="27191-109">Azure Functions 可讓您在 Microsoft Azure 上開發無伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="27191-109">Azure Functions lets you develop serverless applications on Microsoft Azure.</span></span>

<span data-ttu-id="27191-110">本主題提供 Azure Functions 的高階概觀。</span><span class="sxs-lookup"><span data-stu-id="27191-110">This topic provides a high-level overview of Azure Functions.</span></span> <span data-ttu-id="27191-111">如果您想要直接進入正題並開始使用 Azure Functions，請從 [建立您的第一個Azure Functions](functions-create-first-azure-function.md)著手。</span><span class="sxs-lookup"><span data-stu-id="27191-111">If you want to jump right in and get started with Azure Functions, start with [Create your first Azure Function](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="27191-112">如果您要尋找更多有關 Functions 的技術資訊，請參閱 [開發人員參考](functions-reference.md)。</span><span class="sxs-lookup"><span data-stu-id="27191-112">If you are looking for more technical information about Functions, see the [developer reference](functions-reference.md).</span></span>

## <a name="features"></a><span data-ttu-id="27191-113">特性</span><span class="sxs-lookup"><span data-stu-id="27191-113">Features</span></span>
<span data-ttu-id="27191-114">以下是 Azure Functions 的一些主要功能︰</span><span class="sxs-lookup"><span data-stu-id="27191-114">Here are some key features of Azure Functions:</span></span>

* <span data-ttu-id="27191-115">**選擇的語言** - 使用 C#、F#、Node.js、Python、PHP、batch、bash 或任何可執行檔撰寫函式。</span><span class="sxs-lookup"><span data-stu-id="27191-115">**Choice of language** - Write functions using C#, F#, Node.js, Python, PHP, batch, bash, or any executable.</span></span>
* <span data-ttu-id="27191-116">**使用即付費價格模式** - 只對執行您的程式碼所花的時間付費。</span><span class="sxs-lookup"><span data-stu-id="27191-116">**Pay-per-use pricing model** - Pay only for the time spent running your code.</span></span> <span data-ttu-id="27191-117">請參閱[價格區段](#pricing)中的使用情況主控方案選項。</span><span class="sxs-lookup"><span data-stu-id="27191-117">See the Consumption hosting plan option in the [pricing section](#pricing).</span></span>  
* <span data-ttu-id="27191-118">**自備相依性** - Functions 支援 NuGet 和 NPM，以便您使用您最愛的程式庫。</span><span class="sxs-lookup"><span data-stu-id="27191-118">**Bring your own dependencies** - Functions supports NuGet and NPM, so you can use your favorite libraries.</span></span>  
* <span data-ttu-id="27191-119">**整合式安全性** - 利用 OAuth 提供者 (如 Azure Active Directory、Facebook、Google、Twitter 和 Microsoft 帳戶) 保護 HTTP 觸發的函數。</span><span class="sxs-lookup"><span data-stu-id="27191-119">**Integrated security** - Protect HTTP-triggered functions with OAuth providers such as Azure Active Directory, Facebook, Google, Twitter, and Microsoft Account.</span></span>  
* <span data-ttu-id="27191-120">**簡化整合** - 輕鬆地利用 Azure 服務和軟體即服務 (SaaS) 供應項目。</span><span class="sxs-lookup"><span data-stu-id="27191-120">**Simplified integration** - Easily leverage Azure services and software-as-a-service (SaaS) offerings.</span></span> <span data-ttu-id="27191-121">請參閱[整合區段](#integrations)以取得相關範例。</span><span class="sxs-lookup"><span data-stu-id="27191-121">See the [integrations section](#integrations) for some examples.</span></span>  
* <span data-ttu-id="27191-122">**彈性開發** - 直接在入口網站中撰寫函數的程式碼，或透過 GitHub、Visual Studio Team Services 和其他 [支援的開發工具](../app-service-web/web-sites-deploy.md#deploy-using-an-ide)設定連續整合和部署程式碼。</span><span class="sxs-lookup"><span data-stu-id="27191-122">**Flexible development** - Code your functions right in the portal or set up continuous integration and deploy your code through GitHub, Visual Studio Team Services, and other [supported development tools](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).</span></span>  
* <span data-ttu-id="27191-123">**開放原始碼** - Functions 執行階段是開放原始碼的平台並 [可在 GitHub 上取得](https://github.com/azure/azure-webjobs-sdk-script)。</span><span class="sxs-lookup"><span data-stu-id="27191-123">**Open-source** - The Functions runtime is open-source and [available on GitHub](https://github.com/azure/azure-webjobs-sdk-script).</span></span>  

## <a name="what-can-i-do-with-functions"></a><span data-ttu-id="27191-124">我可以用 Functions 來做什麼？</span><span class="sxs-lookup"><span data-stu-id="27191-124">What can I do with Functions?</span></span>
<span data-ttu-id="27191-125">Azure Functions 是處理資料、整合系統、使用物聯網 (IoT)，以及建置簡單 API 和微服務的絕佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="27191-125">Azure Functions is a great solution for processing data, integrating systems, working with the internet-of-things (IoT), and building simple APIs and microservices.</span></span> <span data-ttu-id="27191-126">考慮將 Functions 用於如下的工作：映像或訂單處理、檔案維護，或者您要排程執行的任何工作。</span><span class="sxs-lookup"><span data-stu-id="27191-126">Consider Functions for tasks like image or order processing, file maintenance, or for any tasks that you want to run on a schedule.</span></span> 

<span data-ttu-id="27191-127">Functions 提供範本，可讓您開始使用重要的案例，包括下列案例︰</span><span class="sxs-lookup"><span data-stu-id="27191-127">Functions provides templates to get you started with key scenarios, including the following:</span></span>

* <span data-ttu-id="27191-128">**BlobTrigger** - 在新增至容器時，處理 Azure 儲存體 blob。</span><span class="sxs-lookup"><span data-stu-id="27191-128">**BlobTrigger** - Process Azure Storage blobs when they are added to containers.</span></span> <span data-ttu-id="27191-129">您可以使用此函式調整映像大小。</span><span class="sxs-lookup"><span data-stu-id="27191-129">You might use this function for image resizing.</span></span>
* <span data-ttu-id="27191-130">**EventHubTrigger** - 回應傳送到 Azure 事件中樞的事件。</span><span class="sxs-lookup"><span data-stu-id="27191-130">**EventHubTrigger** -  Respond to events delivered to an Azure Event Hub.</span></span> <span data-ttu-id="27191-131">特別適合用於應用程式檢測、使用者經驗或工作流程處理及物聯網 (IoT) 案例。</span><span class="sxs-lookup"><span data-stu-id="27191-131">Particularly useful in application instrumentation, user experience or workflow processing, and Internet of Things (IoT) scenarios.</span></span>
* <span data-ttu-id="27191-132">**泛型 webhook** - 處理來自支援 webhook 的任何服務的 webhook HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="27191-132">**Generic webhook** - Process webhook HTTP requests from any service that supports webhooks.</span></span>
* <span data-ttu-id="27191-133">**GitHub webhook** - 回應您的 GitHub 儲存機制中發生的事件。</span><span class="sxs-lookup"><span data-stu-id="27191-133">**GitHub webhook** - Respond to events that occur in your GitHub repositories.</span></span> <span data-ttu-id="27191-134">如需範例，請參閱 [建立 Webhook 或 API 函數](functions-create-a-web-hook-or-api-function.md)。</span><span class="sxs-lookup"><span data-stu-id="27191-134">For an example, see [Create a webhook or API function](functions-create-a-web-hook-or-api-function.md).</span></span>
* <span data-ttu-id="27191-135">**HTTPTrigger** - 使用 HTTP 要求觸發程式碼的執行。</span><span class="sxs-lookup"><span data-stu-id="27191-135">**HTTPTrigger** - Trigger the execution of your code by using an HTTP request.</span></span>
* <span data-ttu-id="27191-136">**QueueTrigger** - 在訊息送達 Azure 儲存體佇列中時回應。</span><span class="sxs-lookup"><span data-stu-id="27191-136">**QueueTrigger** - Respond to messages as they arrive in an Azure Storage queue.</span></span> <span data-ttu-id="27191-137">如需範例，請參閱[建立繫結至 Azure 服務的 Azure Function](functions-create-an-azure-connected-function.md)。</span><span class="sxs-lookup"><span data-stu-id="27191-137">For an example, see [Create an Azure Function that binds to an Azure service](functions-create-an-azure-connected-function.md).</span></span>
* <span data-ttu-id="27191-138">**ServiceBusQueueTrigger** - 將程式碼連接至其他 Azure 服務或內部部署服務，方法是接聽訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="27191-138">**ServiceBusQueueTrigger** - Connect your code to other Azure services or on-premises services by listening to message queues.</span></span> 
* <span data-ttu-id="27191-139">**ServiceBusTopicTrigger** - 將程式碼連接至其他 Azure 服務或內部部署服務，方法是訂閱主題。</span><span class="sxs-lookup"><span data-stu-id="27191-139">**ServiceBusTopicTrigger** - Connect your code to other Azure services or on-premises services by subscribing to topics.</span></span> 
* <span data-ttu-id="27191-140">**TimerTrigger** - 在預先定義的排程執行清除或其他批次工作。</span><span class="sxs-lookup"><span data-stu-id="27191-140">**TimerTrigger** - Execute cleanup or other batch tasks on a predefined schedule.</span></span> <span data-ttu-id="27191-141">如需範例，請參閱 [建立事件處理函數](functions-create-an-event-processing-function.md)。</span><span class="sxs-lookup"><span data-stu-id="27191-141">For an example, see [Create an event processing function](functions-create-an-event-processing-function.md).</span></span>

<span data-ttu-id="27191-142">Azure Functions 支援「觸發」，這是開始執行您的程式碼的方式，以及「繫結」，這是針對輸入和輸出資料簡化編碼的方式。</span><span class="sxs-lookup"><span data-stu-id="27191-142">Azure Functions supports *triggers*, which are ways to start execution of your code, and *bindings*, which are ways to simplify coding for input and output data.</span></span> <span data-ttu-id="27191-143">如需 Azure Functions 提供的觸發和繫結的詳細說明，請參閱 [Azure Functions 觸發和繫結開發人員參考](functions-triggers-bindings.md)。</span><span class="sxs-lookup"><span data-stu-id="27191-143">For a detailed description of the triggers and bindings that Azure Functions provides, see [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span>

## <span data-ttu-id="27191-144"><a name="integrations"></a>整合</span><span class="sxs-lookup"><span data-stu-id="27191-144"><a name="integrations"></a>Integrations</span></span>
<span data-ttu-id="27191-145">Azure Functions 可以與各種 Azure 和協力廠商服務整合。</span><span class="sxs-lookup"><span data-stu-id="27191-145">Azure Functions integrates with various Azure and 3rd-party services.</span></span> <span data-ttu-id="27191-146">這些服務可以觸發您的函式並開始執行，或做為您程式碼的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="27191-146">These services can trigger your function and start execution, or they can serve as input and output for your code.</span></span> <span data-ttu-id="27191-147">Azure Functions 支援下列服務整合。</span><span class="sxs-lookup"><span data-stu-id="27191-147">The following service integrations are supported by Azure Functions.</span></span> 

* <span data-ttu-id="27191-148">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="27191-148">Azure Cosmos DB</span></span>
* <span data-ttu-id="27191-149">Azure 事件中心</span><span class="sxs-lookup"><span data-stu-id="27191-149">Azure Event Hubs</span></span> 
* <span data-ttu-id="27191-150">Azure Mobile Apps (資料表)</span><span class="sxs-lookup"><span data-stu-id="27191-150">Azure Mobile Apps (tables)</span></span>
* <span data-ttu-id="27191-151">Azure 通知中心</span><span class="sxs-lookup"><span data-stu-id="27191-151">Azure Notification Hubs</span></span>
* <span data-ttu-id="27191-152">Azure 服務匯流排 (佇列和主題)</span><span class="sxs-lookup"><span data-stu-id="27191-152">Azure Service Bus (queues and topics)</span></span>
* <span data-ttu-id="27191-153">Azure 儲存體 (Blob、佇列和資料表)</span><span class="sxs-lookup"><span data-stu-id="27191-153">Azure Storage (blob, queues, and tables)</span></span> 
* <span data-ttu-id="27191-154">GitHub (webhook)</span><span class="sxs-lookup"><span data-stu-id="27191-154">GitHub (webhooks)</span></span>
* <span data-ttu-id="27191-155">內部部署 (使用服務匯流排)</span><span class="sxs-lookup"><span data-stu-id="27191-155">On-premises (using Service Bus)</span></span>
* <span data-ttu-id="27191-156">Twilio (SMS 訊息)</span><span class="sxs-lookup"><span data-stu-id="27191-156">Twilio (SMS messages)</span></span>

## <span data-ttu-id="27191-157"><a name="pricing"></a>Functions 的計費方式</span><span class="sxs-lookup"><span data-stu-id="27191-157"><a name="pricing"></a>How much does Functions cost?</span></span>
<span data-ttu-id="27191-158">Azure Functions 有兩種價格方案，選擇一個最適合您的需求的方案︰</span><span class="sxs-lookup"><span data-stu-id="27191-158">Azure Functions has two kinds of pricing plans, choose the one that best fits your needs:</span></span> 

* <span data-ttu-id="27191-159">**使用情況方案**：當您的函式執行時，Azure 會提供所有必要的運算資源。</span><span class="sxs-lookup"><span data-stu-id="27191-159">**Consumption plan** - When your function runs, Azure provides all of the necessary computational resources.</span></span> <span data-ttu-id="27191-160">您不必擔心資源管理，您只需為您的程式碼執行時間支付費用。</span><span class="sxs-lookup"><span data-stu-id="27191-160">You don't have to worry about resource management, and you only pay for the time that your code runs.</span></span> 
* <span data-ttu-id="27191-161">**App Service 方案** - 可讓您如同 Web、行動及 API 應用程式一樣執行函數。</span><span class="sxs-lookup"><span data-stu-id="27191-161">**App Service plan** - Run your functions just like your web, mobile, and API apps.</span></span> <span data-ttu-id="27191-162">當您已準備對其他應用程式使用 App Service 時，您可以在相同方案上執行您的函數，不會產生額外的費用。</span><span class="sxs-lookup"><span data-stu-id="27191-162">When you are already using App Service for your other applications, you can run your functions on the same plan at no additional cost.</span></span> 

<span data-ttu-id="27191-163">在 [Functions 價格](https://azure.microsoft.com/pricing/details/functions/)頁面上可取得完整的價格詳細資料。</span><span class="sxs-lookup"><span data-stu-id="27191-163">Full pricing details are available on the [Functions Pricing page](https://azure.microsoft.com/pricing/details/functions/).</span></span> <span data-ttu-id="27191-164">如需有關調整函數的詳細資訊，請參閱 [如何調整 Azure Functions](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="27191-164">For more information about scaling your functions, see [How to scale Azure Functions](functions-scale.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27191-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27191-165">Next Steps</span></span>
* [<span data-ttu-id="27191-166">建立您的第一個Azure Functions</span><span class="sxs-lookup"><span data-stu-id="27191-166">Create your first Azure Function</span></span>](functions-create-first-azure-function.md)  
  <span data-ttu-id="27191-167">直接進入正題並使用 Azure Functions 快速入門建立您的第一個函數。</span><span class="sxs-lookup"><span data-stu-id="27191-167">Jump right in and create your first function using the Azure Functions quickstart.</span></span> 
* [<span data-ttu-id="27191-168">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="27191-168">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="27191-169">提供更多有關 Azure Functions 執行階段的技術資訊，以及可供撰寫函數程式碼及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="27191-169">Provides more technical information about the Azure Functions runtime and a reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="27191-170">測試 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="27191-170">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="27191-171">說明可用於測試函式的各種工具和技巧。</span><span class="sxs-lookup"><span data-stu-id="27191-171">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="27191-172">如何調整 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="27191-172">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="27191-173">討論 Azure Functions 可用的服務方案，包括使用情況主控方案，以及如何選擇正確的方案。</span><span class="sxs-lookup"><span data-stu-id="27191-173">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 
* [<span data-ttu-id="27191-174">深入了解 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="27191-174">Learn more about Azure App Service</span></span>](../app-service/app-service-value-prop-what-is.md)  
  <span data-ttu-id="27191-175">Azure Functions 會利用 Azure App Service 平台執行核心功能，例如部署、環境變數和診斷。</span><span class="sxs-lookup"><span data-stu-id="27191-175">Azure Functions leverages the Azure App Service platform for core functionality like deployments, environment variables, and diagnostics.</span></span> 

