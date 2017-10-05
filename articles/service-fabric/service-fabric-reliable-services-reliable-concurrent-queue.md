---
title: "Azure Service Fabric 中的 ReliableConcurrentQueue"
description: "ReliableConcurrentQueue 是高輸送量佇列，可進行平行加入佇列以及清除佇列。"
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 122cb48149477f295a65b8ee623c647b6db10a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="f5c95-103">Azure Service Fabric 中的 ReliableConcurrentQueue 簡介</span><span class="sxs-lookup"><span data-stu-id="f5c95-103">Introduction to ReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="f5c95-104">可靠的並行佇列是非同步、交易式和複寫的佇列，特徵是加入佇列與清除佇列作業的高並行存取。</span><span class="sxs-lookup"><span data-stu-id="f5c95-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="f5c95-105">它旨在提供高輸送量和低延遲，方法是將[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)所提供的嚴格 FIFO 順序放寬，並改為提供最佳的順序。</span><span class="sxs-lookup"><span data-stu-id="f5c95-105">It is designed to deliver high throughput and low latency by relaxing the strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="f5c95-106">API</span><span class="sxs-lookup"><span data-stu-id="f5c95-106">APIs</span></span>

|<span data-ttu-id="f5c95-107">並行佇列</span><span class="sxs-lookup"><span data-stu-id="f5c95-107">Concurrent Queue</span></span>                |<span data-ttu-id="f5c95-108">可靠的並行佇列</span><span class="sxs-lookup"><span data-stu-id="f5c95-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="f5c95-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="f5c95-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="f5c95-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="f5c95-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="f5c95-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="f5c95-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="f5c95-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="f5c95-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="f5c95-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="f5c95-113">int Count()</span></span>                    | <span data-ttu-id="f5c95-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="f5c95-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="f5c95-115">與[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)進行比較</span><span class="sxs-lookup"><span data-stu-id="f5c95-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="f5c95-116">可靠的並行佇列會以[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)替代形式提供。</span><span class="sxs-lookup"><span data-stu-id="f5c95-116">Reliable Concurrent Queue is offered as an alternative to [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="f5c95-117">它應用於不需要嚴格 FIFO 順序的情況，因為保證 FIFO 使用並行存取時需要有所取捨。</span><span class="sxs-lookup"><span data-stu-id="f5c95-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="f5c95-118">[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)會使用鎖定來強制使用 FIFO 順序，並且一次最多允許一個交易加入佇列，以及一次最多允許一個交易清除佇列。</span><span class="sxs-lookup"><span data-stu-id="f5c95-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks to enforce FIFO ordering, with at most one transaction allowed to enqueue and at most one transaction allowed to dequeue at a time.</span></span> <span data-ttu-id="f5c95-119">相較之下，可靠的並行佇列會放寬排序條件約束，並允許任何數目的並行交易可交錯其加入佇列及清除佇列作業。</span><span class="sxs-lookup"><span data-stu-id="f5c95-119">In comparison, Reliable Concurrent Queue relaxes the ordering constraint and allows any number concurrent transactions to interleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="f5c95-120">會提供最佳順序，不過，一律無法保證可靠並行佇列中兩個值的相對順序。</span><span class="sxs-lookup"><span data-stu-id="f5c95-120">Best-effort ordering is provided, however the relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="f5c95-121">每當多個並行交易執行加入佇列或清除佇列時，可靠的並行佇列會提供比[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)更高的輸送量和更低的延遲。</span><span class="sxs-lookup"><span data-stu-id="f5c95-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="f5c95-122">ReliableConcurrentQueue 的範例使用情況為[訊息佇列](https://en.wikipedia.org/wiki/Message_queue)案例。</span><span class="sxs-lookup"><span data-stu-id="f5c95-122">A sample use case for the ReliableConcurrentQueue is the [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="f5c95-123">在此案例中，一個或多個訊息生產者會建立項目並加以新增至佇列，而一個或多個訊息取用者則會從佇列中提取訊息並加以處理。</span><span class="sxs-lookup"><span data-stu-id="f5c95-123">In this scenario, one or more message producers create and add items to the queue, and one or more message consumers pull messages from the queue and process them.</span></span> <span data-ttu-id="f5c95-124">多個產生者和取用者可以獨立運作，使用並行交易以處理佇列。</span><span class="sxs-lookup"><span data-stu-id="f5c95-124">Multiple producers and consumers can work independently, using concurrent transactions in order to process the queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="f5c95-125">使用方針</span><span class="sxs-lookup"><span data-stu-id="f5c95-125">Usage Guidelines</span></span>
* <span data-ttu-id="f5c95-126">佇列會預期佇列中的項目具有低保留期限。</span><span class="sxs-lookup"><span data-stu-id="f5c95-126">The queue expects that the items in the queue have a low retention period.</span></span> <span data-ttu-id="f5c95-127">也就是項目在佇列中不會長時間停留。</span><span class="sxs-lookup"><span data-stu-id="f5c95-127">That is, the items would not stay in the queue for a long time.</span></span>
* <span data-ttu-id="f5c95-128">佇列並不保證嚴格的 FIFO 順序。</span><span class="sxs-lookup"><span data-stu-id="f5c95-128">The queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="f5c95-129">佇列不會閱讀它自己的寫入。</span><span class="sxs-lookup"><span data-stu-id="f5c95-129">The queue does not read its own writes.</span></span> <span data-ttu-id="f5c95-130">如果項目在交易內加入佇列，則同一個交易內的清除佇列者將看不到它。</span><span class="sxs-lookup"><span data-stu-id="f5c95-130">If an item is enqueued within a transaction, it will not be visible to a dequeuer within the same transaction.</span></span>
* <span data-ttu-id="f5c95-131">清除佇列不會彼此互相隔離。</span><span class="sxs-lookup"><span data-stu-id="f5c95-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="f5c95-132">如果已在交易 txnA 中將項目 A 清除佇列，則即使 txnA 不認可，並行交易 txnB 也看不到項目 A。</span><span class="sxs-lookup"><span data-stu-id="f5c95-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible to a concurrent transaction *txnB*.</span></span>  <span data-ttu-id="f5c95-133">如果 txnA 中止，txnB 就可立即看到 A。</span><span class="sxs-lookup"><span data-stu-id="f5c95-133">If *txnA* aborts, *A* will become visible to *txnB* immediately.</span></span>
* <span data-ttu-id="f5c95-134">可將 TryPeekAsync 行為加以實作，方法是使用 TryDequeueAsync，然後中止交易。</span><span class="sxs-lookup"><span data-stu-id="f5c95-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="f5c95-135">程式設計模式一節中可以找到這個範例。</span><span class="sxs-lookup"><span data-stu-id="f5c95-135">An example of this can be found in the Programming Patterns section.</span></span>
* <span data-ttu-id="f5c95-136">計數為非交易式。</span><span class="sxs-lookup"><span data-stu-id="f5c95-136">Count is non-transactional.</span></span> <span data-ttu-id="f5c95-137">它可用來了解佇列中元素的數目，但會以時間點表示且無法依賴。</span><span class="sxs-lookup"><span data-stu-id="f5c95-137">It can be used to get an idea of the number of elements in the queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="f5c95-138">交易使用中時，不應在清除佇列的項目上執行昂貴的處理，以避免長時間執行交易可能會對系統造成的效能影響。</span><span class="sxs-lookup"><span data-stu-id="f5c95-138">Expensive processing on the dequeued items should not be performed while the transaction is active, to avoid long-running transactions which may have a performance impact on the system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="f5c95-139">程式碼片段</span><span class="sxs-lookup"><span data-stu-id="f5c95-139">Code Snippets</span></span>
<span data-ttu-id="f5c95-140">讓我們看看幾個程式碼片段，和其預期的輸出。</span><span class="sxs-lookup"><span data-stu-id="f5c95-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="f5c95-141">本節中會忽略例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="f5c95-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="f5c95-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="f5c95-142">EnqueueAsync</span></span>
<span data-ttu-id="f5c95-143">以下是使用 EnqueueAsync 的幾個程式碼片段，隨後是其預期的輸出。</span><span class="sxs-lookup"><span data-stu-id="f5c95-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="f5c95-144">案例 1︰單一加入佇列工作</span><span class="sxs-lookup"><span data-stu-id="f5c95-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="f5c95-145">假設已順利完成工作，且沒有修改佇列的並行交易。</span><span class="sxs-lookup"><span data-stu-id="f5c95-145">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="f5c95-146">使用者可以預期佇列會以下列任何一個順序來包含項目︰</span><span class="sxs-lookup"><span data-stu-id="f5c95-146">The user can expect the queue to contain the items in any of the following orders:</span></span>

> <span data-ttu-id="f5c95-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="f5c95-147">10, 20</span></span>

> <span data-ttu-id="f5c95-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="f5c95-148">20, 10</span></span>


- <span data-ttu-id="f5c95-149">案例 2︰平行加入佇列工作</span><span class="sxs-lookup"><span data-stu-id="f5c95-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="f5c95-150">假設已順利完成工作、工作以平行方式執行，且沒有其他修改佇列的並行交易。</span><span class="sxs-lookup"><span data-stu-id="f5c95-150">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="f5c95-151">無法推斷佇列中的項目順序。</span><span class="sxs-lookup"><span data-stu-id="f5c95-151">No inference can be made about the order of items in the queue.</span></span> <span data-ttu-id="f5c95-152">此程式碼片段中，項目會以下列 4 個之一出現！</span><span class="sxs-lookup"><span data-stu-id="f5c95-152">For this code snippet, the items may appear in any of the 4!</span></span> <span data-ttu-id="f5c95-153">可能的排序。</span><span class="sxs-lookup"><span data-stu-id="f5c95-153">possible orderings.</span></span>  <span data-ttu-id="f5c95-154">佇列會嘗試以原始順序保留項目 (佇列)，但可能會因並行作業或錯誤而強制將它們重新排序。</span><span class="sxs-lookup"><span data-stu-id="f5c95-154">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="f5c95-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="f5c95-155">DequeueAsync</span></span>
<span data-ttu-id="f5c95-156">以下是使用 TryDequeueAsync 的幾個程式碼片段，隨後是預期的輸出。</span><span class="sxs-lookup"><span data-stu-id="f5c95-156">Here are a few code snippets for using TryDequeueAsync followed by the expected outputs.</span></span> <span data-ttu-id="f5c95-157">假設已將佇列中的下列項目填入佇列︰</span><span class="sxs-lookup"><span data-stu-id="f5c95-157">Assume that the queue is already populated with the following items in the queue:</span></span>
> <span data-ttu-id="f5c95-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="f5c95-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="f5c95-159">案例 1︰單一清除佇列工作</span><span class="sxs-lookup"><span data-stu-id="f5c95-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="f5c95-160">假設已順利完成工作，且沒有修改佇列的並行交易。</span><span class="sxs-lookup"><span data-stu-id="f5c95-160">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="f5c95-161">由於無法推斷佇列中的項目順序，任何三個項目都可能會以任何順序加以清除佇列。</span><span class="sxs-lookup"><span data-stu-id="f5c95-161">Since no inference can be made about the order of the items in the queue, any three of the items may be dequeued, in any order.</span></span> <span data-ttu-id="f5c95-162">佇列會嘗試以原始順序保留項目 (佇列)，但可能會因並行作業或錯誤而強制將它們重新排序。</span><span class="sxs-lookup"><span data-stu-id="f5c95-162">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>  

- <span data-ttu-id="f5c95-163">案例 2︰平行清除佇列工作</span><span class="sxs-lookup"><span data-stu-id="f5c95-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="f5c95-164">假設已順利完成工作、工作以平行方式執行，且沒有其他修改佇列的並行交易。</span><span class="sxs-lookup"><span data-stu-id="f5c95-164">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="f5c95-165">由於無法推斷佇列中的項目順序，dequeue1 和 dequeue2 都會以任何順序包含任何兩個項目。</span><span class="sxs-lookup"><span data-stu-id="f5c95-165">Since no inference can be made about the order of the items in the queue, the lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="f5c95-166">相同項目不會同時出現在兩份清單中。</span><span class="sxs-lookup"><span data-stu-id="f5c95-166">The same item will *not* appear in both lists.</span></span> <span data-ttu-id="f5c95-167">因此，如果 dequeue1 包含 10、*30*，dequeue2 就會包含 *20*、*40*。</span><span class="sxs-lookup"><span data-stu-id="f5c95-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="f5c95-168">案例 3︰使用交易中止來清除佇列排序</span><span class="sxs-lookup"><span data-stu-id="f5c95-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="f5c95-169">使用執行中的清除佇列將交易中止，會將項目放回佇列的前端。</span><span class="sxs-lookup"><span data-stu-id="f5c95-169">Aborting a transaction with in-flight dequeues puts the items back on the head of the queue.</span></span> <span data-ttu-id="f5c95-170">無法保證將項目放回佇列前端的順序。</span><span class="sxs-lookup"><span data-stu-id="f5c95-170">The order in which the items are put back on the head of the queue is not guaranteed.</span></span> <span data-ttu-id="f5c95-171">我們來看看下面的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f5c95-171">Let us look at the following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort the transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="f5c95-172">假設已依下列順序將項目清除佇列︰</span><span class="sxs-lookup"><span data-stu-id="f5c95-172">Assume that the items were dequeued in the following order:</span></span>
> <span data-ttu-id="f5c95-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="f5c95-173">10, 20</span></span>

<span data-ttu-id="f5c95-174">當我們將交易中止時，會依下列任何一個順序將項目新增回佇列的前端︰</span><span class="sxs-lookup"><span data-stu-id="f5c95-174">When we abort the transaction, the items would be added back to the head of the queue in any of the following orders:</span></span>
> <span data-ttu-id="f5c95-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="f5c95-175">10, 20</span></span>

> <span data-ttu-id="f5c95-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="f5c95-176">20, 10</span></span>

<span data-ttu-id="f5c95-177">這也適用於交易未成功認可的所有情況。</span><span class="sxs-lookup"><span data-stu-id="f5c95-177">The same is true for all cases where the transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="f5c95-178">程式設計模式</span><span class="sxs-lookup"><span data-stu-id="f5c95-178">Programming Patterns</span></span>
<span data-ttu-id="f5c95-179">在本節中，我們來看看幾個可能有助於使用 ReliableConcurrentQueue 的程式設計模式。</span><span class="sxs-lookup"><span data-stu-id="f5c95-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="f5c95-180">批次清除佇列</span><span class="sxs-lookup"><span data-stu-id="f5c95-180">Batch Dequeues</span></span>
<span data-ttu-id="f5c95-181">建議的程式設計模式是使取用者工作以批次方式清除佇列，而不是一次執行一個清除佇列。</span><span class="sxs-lookup"><span data-stu-id="f5c95-181">A recommended programming pattern is for the consumer task to batch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="f5c95-182">使用者可以選擇節流處理每個批次或批次大小之間的延遲。</span><span class="sxs-lookup"><span data-stu-id="f5c95-182">The user can choose to throttle delays between every batch or the batch size.</span></span> <span data-ttu-id="f5c95-183">下列程式碼片段會示範此程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="f5c95-183">The following code snippet shows this programming model.</span></span>  <span data-ttu-id="f5c95-184">請注意，在此範例中，交易認可後即完成處理，因此如果在處理時發生錯誤，未處理的項目就會遺失而未經處理。</span><span class="sxs-lookup"><span data-stu-id="f5c95-184">Note that in this example, the processing is done after the transaction is committed, so if a fault were to occur while processing, the unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="f5c95-185">或者，可以在交易的範圍內完成處理，不過，這可能會對效能造成負面影響，而且需要處理已經處理的項目。</span><span class="sxs-lookup"><span data-stu-id="f5c95-185">Alternatively, the processing can be done within the transaction's scope, however this may have a negative impact on performance and requires handling of the items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break the for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="f5c95-186">以通知作為基礎的最佳處理</span><span class="sxs-lookup"><span data-stu-id="f5c95-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="f5c95-187">另一個有趣的程式設計模式是使用計數 API。</span><span class="sxs-lookup"><span data-stu-id="f5c95-187">Another interesting programming pattern uses the Count API.</span></span> <span data-ttu-id="f5c95-188">在這裡，我們可以針對佇列實作以通知作為基礎的最佳處理。</span><span class="sxs-lookup"><span data-stu-id="f5c95-188">Here, we can implement best-effort notification-based processing for the queue.</span></span> <span data-ttu-id="f5c95-189">佇列計數可以用來將加入佇列或清除佇列工作進行節流處理。</span><span class="sxs-lookup"><span data-stu-id="f5c95-189">The queue Count can be used to throttle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="f5c95-190">請注意，如同先前的範例，因為處理發生於交易外部，如果在處理期間發生錯誤，未處理的項目可能就會遺失。</span><span class="sxs-lookup"><span data-stu-id="f5c95-190">Note that as in the previous example, since the processing occurs outside the transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If the queue does not have the threshold number of items, delay the task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process the queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="f5c95-191">盡可能清空</span><span class="sxs-lookup"><span data-stu-id="f5c95-191">Best-Effort Drain</span></span>
<span data-ttu-id="f5c95-192">由於資料結構的並行本質，無法保證可將佇列清空。</span><span class="sxs-lookup"><span data-stu-id="f5c95-192">A drain of the queue cannot be guaranteed due to the concurrent nature of the data structure.</span></span>  <span data-ttu-id="f5c95-193">即使在佇列上沒有進行中的使用者作業，特定的 TryDequeueAsync 呼叫可能不會傳回先前已加入佇列並且受到認可的項目。</span><span class="sxs-lookup"><span data-stu-id="f5c95-193">It is possible that, even if no user operations on the queue are in-flight, a particular call to TryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="f5c95-194">清除佇列最終保證可看到加入佇列的項目，不過，沒有超出訊號範圍通訊機制的獨立取用者，無法得知佇列已觸達穩定狀態，即使已將所有的產生者停止，且不允許任何新的加入佇列作業亦然。</span><span class="sxs-lookup"><span data-stu-id="f5c95-194">The enqueued item is guaranteed to *eventually* become visible to dequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that the queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="f5c95-195">因此，已盡可能清空作業，實作如下。</span><span class="sxs-lookup"><span data-stu-id="f5c95-195">Thus, the drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="f5c95-196">使用者應該將所有進一步的生產者和取用者工作停止，並在嘗試清空佇列之前，等待任何進行中的交易加以認可或中止。</span><span class="sxs-lookup"><span data-stu-id="f5c95-196">The user should stop all further producer and consumer tasks, and wait for any in-flight transactions to commit or abort, before attempting to drain the queue.</span></span>  <span data-ttu-id="f5c95-197">如果使用者知道佇列中預期的項目數目，就可以設定通知，發出所有項目皆已清除佇列的訊號。</span><span class="sxs-lookup"><span data-stu-id="f5c95-197">If the user knows the expected number of items in the queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer the dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="f5c95-198">預覽</span><span class="sxs-lookup"><span data-stu-id="f5c95-198">Peek</span></span>
<span data-ttu-id="f5c95-199">ReliableConcurrentQueue 不會提供 TryPeekAsync API。</span><span class="sxs-lookup"><span data-stu-id="f5c95-199">ReliableConcurrentQueue does not provide the *TryPeekAsync* api.</span></span> <span data-ttu-id="f5c95-200">使用者可以預覽語意，方法是使用 TryDequeueAsync 然後將交易中止。</span><span class="sxs-lookup"><span data-stu-id="f5c95-200">Users can get the peek semantic by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="f5c95-201">在此範例中，僅在項目大於 10 時，才會處理清除佇列。</span><span class="sxs-lookup"><span data-stu-id="f5c95-201">In this example, dequeues are processed only if the item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process the item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="f5c95-202">必須閱讀</span><span class="sxs-lookup"><span data-stu-id="f5c95-202">Must Read</span></span>
* [<span data-ttu-id="f5c95-203">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="f5c95-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="f5c95-204">使用 Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="f5c95-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="f5c95-205">Reliable Services 通知</span><span class="sxs-lookup"><span data-stu-id="f5c95-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="f5c95-206">備份與還原 Reliable Services (災害復原)</span><span class="sxs-lookup"><span data-stu-id="f5c95-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="f5c95-207">Reliable State Manager 設定</span><span class="sxs-lookup"><span data-stu-id="f5c95-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="f5c95-208">開始使用 Service Fabric Web API 服務</span><span class="sxs-lookup"><span data-stu-id="f5c95-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="f5c95-209">Reliable Services 程式設計模型的進階用法</span><span class="sxs-lookup"><span data-stu-id="f5c95-209">Advanced Usage of the Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="f5c95-210">可靠集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="f5c95-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
