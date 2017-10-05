---
title: "Azure Functions 的最佳作法 | Microsoft Docs"
description: "了解 Azure Functions 的最佳作法與模式。"
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 模式, 最佳作法, 函數, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 645a5dd16e72619e7c2470ab8f03098f0fa6c7f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-the-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="4c1c1-104">將 Azure Functions 效能和可靠性最佳化</span><span class="sxs-lookup"><span data-stu-id="4c1c1-104">Optimize the performance and reliability of Azure Functions</span></span>

<span data-ttu-id="4c1c1-105">本文提供指引來改善函式應用程式的效能和可靠性。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-105">This article provides guidance to improve the performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="4c1c1-106">避免長時間執行的函式</span><span class="sxs-lookup"><span data-stu-id="4c1c1-106">Avoid long running functions</span></span>

<span data-ttu-id="4c1c1-107">大型長時間執行的函式可能會造成非預期的逾時問題。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="4c1c1-108">函式可能會因為許多 Node.js 相依性而變大。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-108">A function can become large due to many Node.js dependencies.</span></span> <span data-ttu-id="4c1c1-109">匯入相依性也可能會造成載入時間增加，而導致未預期的逾時。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="4c1c1-110">系統會以明確和隱含方式載入相依性。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="4c1c1-111">您的程式碼載入的單一模組可能會載入其本身的其他模組。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="4c1c1-112">在可能時，將大型函式重構為較小的函式集，共用運作並快速傳回回應。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="4c1c1-113">例如，Webhook 或 HTTP 觸發程序函式可能要求在特定時間限制內的通知回應；Webhook 通常需要立即的回應。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks to require an immediate response.</span></span> <span data-ttu-id="4c1c1-114">您可以將 HTTP 觸發程序承載傳遞到要由佇列觸發程序函式處理的佇列中。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-114">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span></span> <span data-ttu-id="4c1c1-115">此方法可讓您延後實際工作，並傳回立即回應。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-115">This approach allows you to defer the actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="4c1c1-116">跨函式通訊</span><span class="sxs-lookup"><span data-stu-id="4c1c1-116">Cross function communication</span></span>

<span data-ttu-id="4c1c1-117">整合多個函式時，對跨函式通訊使用儲存體佇列通常是最佳作法。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-117">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span></span>  <span data-ttu-id="4c1c1-118">主要原因是儲存體佇列更便宜和容易佈建。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-118">The main reason is storage queues are cheaper and much easier to provision.</span></span> 

<span data-ttu-id="4c1c1-119">儲存體佇列中個別訊息大小限制在 64 KB。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-119">Individual messages in a storage queue are limited in size to 64 KB.</span></span> <span data-ttu-id="4c1c1-120">如果您需要在函式之間傳遞更大型的訊息，Azure 服務匯流排佇列可用來支援大小上限為 256 KB 的訊息。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-120">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span></span>

<span data-ttu-id="4c1c1-121">如果您需要在處理之前篩選訊息，服務匯流排主題會很實用。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="4c1c1-122">事件中樞對於支援大量通訊很有用。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-122">Event hubs are useful to support high volume communications.</span></span>


## <a name="write-functions-to-be-stateless"></a><span data-ttu-id="4c1c1-123">撰寫無狀態函式</span><span class="sxs-lookup"><span data-stu-id="4c1c1-123">Write functions to be stateless</span></span> 

<span data-ttu-id="4c1c1-124">若可能，Functions 應該是無狀態和具有等冪性。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="4c1c1-125">將任何必要的狀態資訊與您的資料產生關聯。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-125">Associate any required state information with your data.</span></span> <span data-ttu-id="4c1c1-126">例如，正在處理訂單就可能具有相關聯的 `state` 成員。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="4c1c1-127">函式本身保持無狀態時，函式可以依據該狀態處理訂單。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-127">A function could process an order based on that state while the function itself remains stateless.</span></span> 

<span data-ttu-id="4c1c1-128">特別建議計時器觸發程序使用等冪函式。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="4c1c1-129">例如，如果您有一天必須執行一次的項目，請編寫它，使得它可在一天中的任何時間執行，並具有相同的結果。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span></span> <span data-ttu-id="4c1c1-130">特定日沒有工作時，就可以結束函式。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-130">The function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="4c1c1-131">如果先前的執行無法完成，下一次執行應該會定停止的位置開始。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-131">Also if a previous run failed to complete, the next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="4c1c1-132">編寫防禦性函式</span><span class="sxs-lookup"><span data-stu-id="4c1c1-132">Write defensive functions</span></span>

<span data-ttu-id="4c1c1-133">假設您的函式可能隨時會遇到例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="4c1c1-134">設計您的函式，使得它能夠在下一次執行期間從先前的失敗點繼續執行。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-134">Design your functions with the ability to continue from a previous fail point during the next execution.</span></span> <span data-ttu-id="4c1c1-135">假設需要執行下列動作的案例︰</span><span class="sxs-lookup"><span data-stu-id="4c1c1-135">Consider a scenario that requires the following actions:</span></span>

1. <span data-ttu-id="4c1c1-136">查詢資料庫中的 10,000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="4c1c1-137">對每個資料列建立佇列訊息，來進一步處理向下一行。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-137">Create a queue message for each of those rows to process further down the line.</span></span>
 
<span data-ttu-id="4c1c1-138">根據系統的複雜程度，您可能會有︰相關的下游服務行為不當、網路中斷或到達配額限制等等。這所有方面都隨時會影響您的函式。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="4c1c1-139">您必須設計您的函式，以對其做好準備。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-139">You need to design your functions to be prepared for it.</span></span>

<span data-ttu-id="4c1c1-140">如果在插入這些項目中的 5,000 個至佇列以進行處理之後發生失敗，您的程式碼如何因應？</span><span class="sxs-lookup"><span data-stu-id="4c1c1-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="4c1c1-141">追蹤集合中您已完成的項目。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="4c1c1-142">否則，您可能下一次又將它們插入。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="4c1c1-143">這對您的工作流程會有嚴重影響。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="4c1c1-144">如果佇列項目已經過處理，請讓您的函式成為無作業。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-144">If a queue item was already processed, allow your function to be a no-op.</span></span>

<span data-ttu-id="4c1c1-145">利用已針對您在 Azure Functions 平台中所使用元件提供的防禦性措施。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-145">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span></span> <span data-ttu-id="4c1c1-146">例如，請參閱文件中**處理有害的佇列訊息**中的 [Azure 儲存體佇列觸發程序](functions-bindings-storage-queue.md#trigger)。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-146">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a><span data-ttu-id="4c1c1-147">不要在相同函式應用程式中混用測試和實際執行程式碼</span><span class="sxs-lookup"><span data-stu-id="4c1c1-147">Don't mix test and production code in the same function app</span></span>

<span data-ttu-id="4c1c1-148">函式應用程式內的 Functions 會共用資源。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-148">Functions within a function app share resources.</span></span> <span data-ttu-id="4c1c1-149">例如，共用記憶體。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-149">For example, memory is shared.</span></span> <span data-ttu-id="4c1c1-150">如果您在生產環境中使用函式應用程式，請勿對它新增與測試相關的函式和資源。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-150">If you're using a function app in production, don't add test-related functions and resources to it.</span></span> <span data-ttu-id="4c1c1-151">在實際執行程式碼執行期間可能導致發生未預期的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="4c1c1-152">對於在實際執行函式應用程式中載入的項目，請務必小心。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="4c1c1-153">記憶體會在應用程式中的每個函式間平均分配。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-153">Memory is averaged across each function in the app.</span></span>

<span data-ttu-id="4c1c1-154">如果您在多個 .Net 函式中參考某個共用組件，請將它置於通用的共用資料夾中。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="4c1c1-155">使用類似下列的範例陳述式來參考組件︰</span><span class="sxs-lookup"><span data-stu-id="4c1c1-155">Reference the assembly with a statement similar to the following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="4c1c1-156">否則，很容易不小心在函式之間部署相同二進位檔但不同行為的多個測試版本。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-156">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span></span>

<span data-ttu-id="4c1c1-157">請勿在實際執行程式碼中使用詳細資訊記錄。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="4c1c1-158">它對效能會有負面影響。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="4c1c1-159">使用非同步程式碼但避免封鎖呼叫</span><span class="sxs-lookup"><span data-stu-id="4c1c1-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="4c1c1-160">非同步程式設計是建議的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="4c1c1-161">不過，請務必避免在 `Task` 執行個體上參考 `Result` 屬性或呼叫 `Wait` 方法。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-161">However, always avoid referencing the `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="4c1c1-162">這個方法可能會導致執行緒耗盡。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-162">This approach can lead to thread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="4c1c1-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c1c1-163">Next steps</span></span>
<span data-ttu-id="4c1c1-164">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="4c1c1-164">For more information, see the following resources:</span></span>

<span data-ttu-id="4c1c1-165">因為 Azure Functions 使用 Azure App Service，所以您也應該充分了解 Azure App Service 指導方針。</span><span class="sxs-lookup"><span data-stu-id="4c1c1-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="4c1c1-166">HTTP 效能最佳化的模式與做法</span><span class="sxs-lookup"><span data-stu-id="4c1c1-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

