---
title: "Azure 函式的 aaaBest 作法 |Microsoft 文件"
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
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="ddd57-104">最佳化 hello 效能和可靠性的 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="ddd57-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="ddd57-105">本文提供指引 tooimprove hello 效能和可靠性的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddd57-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="ddd57-106">避免長時間執行的函式</span><span class="sxs-lookup"><span data-stu-id="ddd57-106">Avoid long running functions</span></span>

<span data-ttu-id="ddd57-107">大型長時間執行的函式可能會造成非預期的逾時問題。</span><span class="sxs-lookup"><span data-stu-id="ddd57-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="ddd57-108">函式可以變得很大，因為 toomany Node.js 相依性的。</span><span class="sxs-lookup"><span data-stu-id="ddd57-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="ddd57-109">匯入相依性也可能會造成載入時間增加，而導致未預期的逾時。</span><span class="sxs-lookup"><span data-stu-id="ddd57-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="ddd57-110">系統會以明確和隱含方式載入相依性。</span><span class="sxs-lookup"><span data-stu-id="ddd57-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="ddd57-111">您的程式碼載入的單一模組可能會載入其本身的其他模組。</span><span class="sxs-lookup"><span data-stu-id="ddd57-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="ddd57-112">在可能時，將大型函式重構為較小的函式集，共用運作並快速傳回回應。</span><span class="sxs-lookup"><span data-stu-id="ddd57-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="ddd57-113">例如，webhook 或 HTTP 觸發程序函式可能需要在特定時間限制; 內的通知回應很常見的 webhook toorequire 立即回應。</span><span class="sxs-lookup"><span data-stu-id="ddd57-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="ddd57-114">您可以將 hello HTTP 觸發程序裝載傳遞至處理佇列的觸發程序函式的佇列 toobe。</span><span class="sxs-lookup"><span data-stu-id="ddd57-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="ddd57-115">此方法可讓您 toodefer hello 實際工作，並立即的回應傳回。</span><span class="sxs-lookup"><span data-stu-id="ddd57-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="ddd57-116">跨函式通訊</span><span class="sxs-lookup"><span data-stu-id="ddd57-116">Cross function communication</span></span>

<span data-ttu-id="ddd57-117">整合多個函式，通常是最佳作法 toouse 儲存體佇列的跨函式的通訊。</span><span class="sxs-lookup"><span data-stu-id="ddd57-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="ddd57-118">hello 主要原因是儲存體佇列的成本較低，更容易 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="ddd57-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="ddd57-119">儲存體佇列中的個別訊息僅限於大小 too64 KB。</span><span class="sxs-lookup"><span data-stu-id="ddd57-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="ddd57-120">如果您需要 toopass 函式之間的較大訊息時，Azure 服務匯流排佇列可能是使用的 toosupport 向上 too256 KB 的訊息大小。</span><span class="sxs-lookup"><span data-stu-id="ddd57-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="ddd57-121">如果您需要在處理之前篩選訊息，服務匯流排主題會很實用。</span><span class="sxs-lookup"><span data-stu-id="ddd57-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="ddd57-122">事件中心是有用的 toosupport 大量通訊。</span><span class="sxs-lookup"><span data-stu-id="ddd57-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="ddd57-123">撰寫函式 toobe 無狀態</span><span class="sxs-lookup"><span data-stu-id="ddd57-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="ddd57-124">若可能，Functions 應該是無狀態和具有等冪性。</span><span class="sxs-lookup"><span data-stu-id="ddd57-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="ddd57-125">將任何必要的狀態資訊與您的資料產生關聯。</span><span class="sxs-lookup"><span data-stu-id="ddd57-125">Associate any required state information with your data.</span></span> <span data-ttu-id="ddd57-126">例如，正在處理訂單就可能具有相關聯的 `state` 成員。</span><span class="sxs-lookup"><span data-stu-id="ddd57-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="ddd57-127">函式無法處理 hello 函式本身仍無狀態時，依據該狀態的順序。</span><span class="sxs-lookup"><span data-stu-id="ddd57-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="ddd57-128">特別建議計時器觸發程序使用等冪函式。</span><span class="sxs-lookup"><span data-stu-id="ddd57-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="ddd57-129">例如，如果您有絕對必須執行一天一次的項目，將它寫入讓它可以執行任何 hello 一天的時間與 hello 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="ddd57-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="ddd57-130">沒有特定的一天的工作時，就可以結束 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="ddd57-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="ddd57-131">也表示上次執行失敗，toocomplete，接下來執行的 hello 應該挑選中斷的位置。</span><span class="sxs-lookup"><span data-stu-id="ddd57-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="ddd57-132">編寫防禦性函式</span><span class="sxs-lookup"><span data-stu-id="ddd57-132">Write defensive functions</span></span>

<span data-ttu-id="ddd57-133">假設您的函式可能隨時會遇到例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ddd57-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="ddd57-134">設計您的函式與 hello 能力 toocontinue 從先前的失敗點 hello 下一步 執行期間。</span><span class="sxs-lookup"><span data-stu-id="ddd57-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="ddd57-135">請考慮需要 hello 下列動作的案例：</span><span class="sxs-lookup"><span data-stu-id="ddd57-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="ddd57-136">查詢資料庫中的 10,000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="ddd57-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="ddd57-137">為每個向 hello 列進一步這些資料列 tooprocess 建立佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="ddd57-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="ddd57-138">根據系統的複雜程度，您可能會有︰相關的下游服務行為不當、網路中斷或到達配額限制等等。這所有方面都隨時會影響您的函式。</span><span class="sxs-lookup"><span data-stu-id="ddd57-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="ddd57-139">您需要 toodesign 準備您的函式 toobe。</span><span class="sxs-lookup"><span data-stu-id="ddd57-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="ddd57-140">如果在插入這些項目中的 5,000 個至佇列以進行處理之後發生失敗，您的程式碼如何因應？</span><span class="sxs-lookup"><span data-stu-id="ddd57-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="ddd57-141">追蹤集合中您已完成的項目。</span><span class="sxs-lookup"><span data-stu-id="ddd57-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="ddd57-142">否則，您可能下一次又將它們插入。</span><span class="sxs-lookup"><span data-stu-id="ddd57-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="ddd57-143">這對您的工作流程會有嚴重影響。</span><span class="sxs-lookup"><span data-stu-id="ddd57-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="ddd57-144">如果已經處理佇列項目，可讓函式 toobe 無作業。</span><span class="sxs-lookup"><span data-stu-id="ddd57-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="ddd57-145">利用下防禦措施已提供您使用在 hello Azure 函式平台的元件。</span><span class="sxs-lookup"><span data-stu-id="ddd57-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="ddd57-146">例如，請參閱**處理佇列有害訊息**hello 文件中[Azure 儲存體佇列觸發程序](functions-bindings-storage-queue.md#trigger)。</span><span class="sxs-lookup"><span data-stu-id="ddd57-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="ddd57-147">請勿混合測試和生產環境中的程式碼 hello 相同函式應用程式</span><span class="sxs-lookup"><span data-stu-id="ddd57-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="ddd57-148">函式應用程式內的 Functions 會共用資源。</span><span class="sxs-lookup"><span data-stu-id="ddd57-148">Functions within a function app share resources.</span></span> <span data-ttu-id="ddd57-149">例如，共用記憶體。</span><span class="sxs-lookup"><span data-stu-id="ddd57-149">For example, memory is shared.</span></span> <span data-ttu-id="ddd57-150">如果您在生產環境中使用的函式應用程式，不加入測試相關的函式和資源 tooit。</span><span class="sxs-lookup"><span data-stu-id="ddd57-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="ddd57-151">在實際執行程式碼執行期間可能導致發生未預期的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="ddd57-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="ddd57-152">對於在實際執行函式應用程式中載入的項目，請務必小心。</span><span class="sxs-lookup"><span data-stu-id="ddd57-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="ddd57-153">記憶體會平均值 hello 應用程式中的每個函式。</span><span class="sxs-lookup"><span data-stu-id="ddd57-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="ddd57-154">如果您在多個 .Net 函式中參考某個共用組件，請將它置於通用的共用資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ddd57-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="ddd57-155">參考陳述式的類似 toohello，下列範例與 hello 組件：</span><span class="sxs-lookup"><span data-stu-id="ddd57-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="ddd57-156">否則，很容易 tooaccidentally 部署的 hello 函式相同的行為方式之間的二進位檔的多個測試版本。</span><span class="sxs-lookup"><span data-stu-id="ddd57-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="ddd57-157">請勿在實際執行程式碼中使用詳細資訊記錄。</span><span class="sxs-lookup"><span data-stu-id="ddd57-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="ddd57-158">它對效能會有負面影響。</span><span class="sxs-lookup"><span data-stu-id="ddd57-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="ddd57-159">使用非同步程式碼但避免封鎖呼叫</span><span class="sxs-lookup"><span data-stu-id="ddd57-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="ddd57-160">非同步程式設計是建議的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="ddd57-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="ddd57-161">不過，一律避免參考 hello`Result`屬性或呼叫`Wait`方法`Task`執行個體。</span><span class="sxs-lookup"><span data-stu-id="ddd57-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="ddd57-162">這個方法會導致 toothread 耗盡。</span><span class="sxs-lookup"><span data-stu-id="ddd57-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="ddd57-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddd57-163">Next steps</span></span>
<span data-ttu-id="ddd57-164">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="ddd57-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="ddd57-165">因為 Azure Functions 使用 Azure App Service，所以您也應該充分了解 Azure App Service 指導方針。</span><span class="sxs-lookup"><span data-stu-id="ddd57-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="ddd57-166">HTTP 效能最佳化的模式與做法</span><span class="sxs-lookup"><span data-stu-id="ddd57-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

