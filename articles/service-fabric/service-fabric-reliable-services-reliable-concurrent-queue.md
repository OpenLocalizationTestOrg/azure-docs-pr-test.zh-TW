---
title: "在 Azure Service Fabric aaaReliableConcurrentQueue"
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
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="bf158-103">在 Azure Service Fabric 簡介 tooReliableConcurrentQueue</span><span class="sxs-lookup"><span data-stu-id="bf158-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="bf158-104">可靠的並行佇列是非同步、交易式和複寫的佇列，特徵是加入佇列與清除佇列作業的高並行存取。</span><span class="sxs-lookup"><span data-stu-id="bf158-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="bf158-105">它是設計的 toodeliver 高輸送量和低延遲的放鬆 hello 嚴格 FIFO 順序提供[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)並改為提供最佳順序。</span><span class="sxs-lookup"><span data-stu-id="bf158-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="bf158-106">API</span><span class="sxs-lookup"><span data-stu-id="bf158-106">APIs</span></span>

|<span data-ttu-id="bf158-107">並行佇列</span><span class="sxs-lookup"><span data-stu-id="bf158-107">Concurrent Queue</span></span>                |<span data-ttu-id="bf158-108">可靠的並行佇列</span><span class="sxs-lookup"><span data-stu-id="bf158-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="bf158-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="bf158-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="bf158-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="bf158-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="bf158-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="bf158-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="bf158-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="bf158-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="bf158-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="bf158-113">int Count()</span></span>                    | <span data-ttu-id="bf158-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="bf158-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="bf158-115">與[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)進行比較</span><span class="sxs-lookup"><span data-stu-id="bf158-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="bf158-116">太可靠的並行佇列提供替代[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bf158-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="bf158-117">它應用於不需要嚴格 FIFO 順序的情況，因為保證 FIFO 使用並行存取時需要有所取捨。</span><span class="sxs-lookup"><span data-stu-id="bf158-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="bf158-118">[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)使用鎖定 tooenforce FIFO 順序，最多允許 tooenqueue 一個交易與在大部分的允許 toodequeue 一次一筆交易。</span><span class="sxs-lookup"><span data-stu-id="bf158-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="bf158-119">相較之下，可靠的並行佇列會放寬 hello 排序條件約束可讓任何數字的並行交易 toointerleave 其 enqueue 和清除佇列作業。</span><span class="sxs-lookup"><span data-stu-id="bf158-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="bf158-120">最佳順序為提供，不過 hello 相對順序的可靠的並行佇列中的兩個值不可以保證。</span><span class="sxs-lookup"><span data-stu-id="bf158-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="bf158-121">每當多個並行交易執行加入佇列或清除佇列時，可靠的並行佇列會提供比[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)更高的輸送量和更低的延遲。</span><span class="sxs-lookup"><span data-stu-id="bf158-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="bf158-122">範例使用案例 hello ReliableConcurrentQueue 是 hello[訊息佇列](https://en.wikipedia.org/wiki/Message_queue)案例。</span><span class="sxs-lookup"><span data-stu-id="bf158-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="bf158-123">在此案例中，一或多個訊息產生者建立和加入項目 toohello 佇列，和一或多個訊息取用者提取從 hello 佇列的訊息，並進行處理。</span><span class="sxs-lookup"><span data-stu-id="bf158-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="bf158-124">多個產生者和消費者可以獨立工作，使用並行的交易順序 tooprocess hello 佇列中。</span><span class="sxs-lookup"><span data-stu-id="bf158-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="bf158-125">使用方針</span><span class="sxs-lookup"><span data-stu-id="bf158-125">Usage Guidelines</span></span>
* <span data-ttu-id="bf158-126">hello 佇列預期 hello hello 佇列中的項目具有較低的保留期間。</span><span class="sxs-lookup"><span data-stu-id="bf158-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="bf158-127">也就是 hello 項目不願意 hello 佇列中時間太長。</span><span class="sxs-lookup"><span data-stu-id="bf158-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="bf158-128">hello 佇列不保證有嚴格的 FIFO 順序。</span><span class="sxs-lookup"><span data-stu-id="bf158-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="bf158-129">hello 佇列不會讀取其本身的寫入。</span><span class="sxs-lookup"><span data-stu-id="bf158-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="bf158-130">如果項目是在交易內加入佇列，不會顯示 tooa dequeuer hello 內相同的交易。</span><span class="sxs-lookup"><span data-stu-id="bf158-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="bf158-131">清除佇列不會彼此互相隔離。</span><span class="sxs-lookup"><span data-stu-id="bf158-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="bf158-132">如果項目*A*在交易中從佇列中清除*txnA*，即使*txnA*未認可，項目*A*並不會顯示 tooa 並行交易*txnB*。</span><span class="sxs-lookup"><span data-stu-id="bf158-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="bf158-133">如果*txnA*中止， *A*將變成可見太*txnB*立即。</span><span class="sxs-lookup"><span data-stu-id="bf158-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="bf158-134">*TryPeekAsync*行為可以透過使用實作*TryDequeueAsync* ，然後中止 hello 交易。</span><span class="sxs-lookup"><span data-stu-id="bf158-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="bf158-135">這個範例，請參閱 hello 程式設計模式 > 一節中。</span><span class="sxs-lookup"><span data-stu-id="bf158-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="bf158-136">計數為非交易式。</span><span class="sxs-lookup"><span data-stu-id="bf158-136">Count is non-transactional.</span></span> <span data-ttu-id="bf158-137">它可以是使用的 tooget hello hello 佇列中的元素數目的了解代表的時間點，但無法依賴。</span><span class="sxs-lookup"><span data-stu-id="bf158-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="bf158-138">昂貴處理 hello 從佇列中清除項目不應執行 hello 異動處於作用中時 tooavoid 長時間執行的交易可能會有 hello 系統上的效能造成影響。</span><span class="sxs-lookup"><span data-stu-id="bf158-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="bf158-139">程式碼片段</span><span class="sxs-lookup"><span data-stu-id="bf158-139">Code Snippets</span></span>
<span data-ttu-id="bf158-140">讓我們看看幾個程式碼片段，和其預期的輸出。</span><span class="sxs-lookup"><span data-stu-id="bf158-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="bf158-141">本節中會忽略例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="bf158-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="bf158-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="bf158-142">EnqueueAsync</span></span>
<span data-ttu-id="bf158-143">以下是使用 EnqueueAsync 的幾個程式碼片段，隨後是其預期的輸出。</span><span class="sxs-lookup"><span data-stu-id="bf158-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="bf158-144">案例 1︰單一加入佇列工作</span><span class="sxs-lookup"><span data-stu-id="bf158-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="bf158-145">假設 hello 工作已順利完成，而且會有沒有並行交易修改 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="bf158-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="bf158-146">hello 使用者可以在任何下列訂單的 hello 預期 hello 佇列 toocontain hello 項目：</span><span class="sxs-lookup"><span data-stu-id="bf158-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="bf158-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="bf158-147">10, 20</span></span>

> <span data-ttu-id="bf158-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="bf158-148">20, 10</span></span>


- <span data-ttu-id="bf158-149">案例 2︰平行加入佇列工作</span><span class="sxs-lookup"><span data-stu-id="bf158-149">*Case 2: Parallel Enqueue Task*</span></span>

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

<span data-ttu-id="bf158-150">假設 hello 工作成功完成 hello 工作已執行，以平行方式，和已修改 hello 佇列沒有其他並行交易。</span><span class="sxs-lookup"><span data-stu-id="bf158-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="bf158-151">沒有推斷可 hello 順序 hello 佇列中的項目有關。</span><span class="sxs-lookup"><span data-stu-id="bf158-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="bf158-152">此程式碼片段，如 hello 項目可能會出現在任何 hello 4 ！</span><span class="sxs-lookup"><span data-stu-id="bf158-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="bf158-153">可能的排序。</span><span class="sxs-lookup"><span data-stu-id="bf158-153">possible orderings.</span></span>  <span data-ttu-id="bf158-154">hello 佇列會嘗試 tookeep hello 項目順序 hello 原始 （佇列），但可能會強制的 tooreorder 它們到期 tooconcurrent 作業或錯誤。</span><span class="sxs-lookup"><span data-stu-id="bf158-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="bf158-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="bf158-155">DequeueAsync</span></span>
<span data-ttu-id="bf158-156">以下是幾個程式碼片段使用 TryDequeueAsync 後面接著 hello 預期輸出。</span><span class="sxs-lookup"><span data-stu-id="bf158-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="bf158-157">假設該 hello 佇列已經填入下列項目 hello 佇列中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bf158-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="bf158-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="bf158-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="bf158-159">案例 1︰單一清除佇列工作</span><span class="sxs-lookup"><span data-stu-id="bf158-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="bf158-160">假設 hello 工作已順利完成，而且會有沒有並行交易修改 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="bf158-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="bf158-161">關於 hello 順序的 hello hello 佇列中的項目成為沒有推斷，因為任何三個 hello 項目可能是佇列中清除，以任何順序。</span><span class="sxs-lookup"><span data-stu-id="bf158-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="bf158-162">hello 佇列會嘗試 tookeep hello 項目順序 hello 原始 （佇列），但可能會強制的 tooreorder 它們到期 tooconcurrent 作業或錯誤。</span><span class="sxs-lookup"><span data-stu-id="bf158-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="bf158-163">案例 2︰平行清除佇列工作</span><span class="sxs-lookup"><span data-stu-id="bf158-163">*Case 2: Parallel Dequeue Task*</span></span>

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

<span data-ttu-id="bf158-164">假設 hello 工作成功完成 hello 工作已執行，以平行方式，和已修改 hello 佇列沒有其他並行交易。</span><span class="sxs-lookup"><span data-stu-id="bf158-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="bf158-165">關於 hello 順序的 hello hello 佇列中的項目成為沒有推斷，因為 hello 清單*dequeue1*和*dequeue2*將每個包含任何兩個項目，依任何順序。</span><span class="sxs-lookup"><span data-stu-id="bf158-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="bf158-166">相同的項目將的 hello*不*出現在這兩個清單中。</span><span class="sxs-lookup"><span data-stu-id="bf158-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="bf158-167">因此，如果 dequeue1 包含 10、*30*，dequeue2 就會包含 *20*、*40*。</span><span class="sxs-lookup"><span data-stu-id="bf158-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="bf158-168">案例 3︰使用交易中止來清除佇列排序</span><span class="sxs-lookup"><span data-stu-id="bf158-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="bf158-169">中止的交易進行中，從佇列取出的將 hello 項目回復 hello 佇列的 hello 最上層節點。</span><span class="sxs-lookup"><span data-stu-id="bf158-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="bf158-170">不保證在其中 hello 項目會放回 hello 佇列 hello 開頭的 hello 順序。</span><span class="sxs-lookup"><span data-stu-id="bf158-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="bf158-171">讓我們看看下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="bf158-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="bf158-172">假設 hello 項目已從佇列清除 hello 順序中：</span><span class="sxs-lookup"><span data-stu-id="bf158-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="bf158-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="bf158-173">10, 20</span></span>

<span data-ttu-id="bf158-174">當我們中止 hello 交易時，hello 項目中要新增後 toohello head hello 佇列的任何下列訂單 hello:</span><span class="sxs-lookup"><span data-stu-id="bf158-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="bf158-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="bf158-175">10, 20</span></span>

> <span data-ttu-id="bf158-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="bf158-176">20, 10</span></span>

<span data-ttu-id="bf158-177">hello 也適用於所有情況下，其中 hello 交易未成功*已認可*。</span><span class="sxs-lookup"><span data-stu-id="bf158-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="bf158-178">程式設計模式</span><span class="sxs-lookup"><span data-stu-id="bf158-178">Programming Patterns</span></span>
<span data-ttu-id="bf158-179">在本節中，我們來看看幾個可能有助於使用 ReliableConcurrentQueue 的程式設計模式。</span><span class="sxs-lookup"><span data-stu-id="bf158-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="bf158-180">批次清除佇列</span><span class="sxs-lookup"><span data-stu-id="bf158-180">Batch Dequeues</span></span>
<span data-ttu-id="bf158-181">建議的程式設計模式是針對 hello 取用者工作 toobatch 其佇列中清除，而不是執行一個清除佇列一次。</span><span class="sxs-lookup"><span data-stu-id="bf158-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="bf158-182">hello 使用者可以選擇每個批次或 hello 批次大小之間 toothrottle 延遲。</span><span class="sxs-lookup"><span data-stu-id="bf158-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="bf158-183">hello 下列程式碼片段示範這個程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="bf158-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="bf158-184">請注意，在此範例中，hello 處理已完成之後 hello 交易被認可，, 因此如果錯誤處理 toooccur，hello 未處理的項目將會遺失而不需經過處理。</span><span class="sxs-lookup"><span data-stu-id="bf158-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="bf158-185">或者，可以完成 hello 處理 hello 交易在範圍內，不過這可能會對效能造成負面影響，而且需要已處理的 hello 項目處理。</span><span class="sxs-lookup"><span data-stu-id="bf158-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

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
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="bf158-186">以通知作為基礎的最佳處理</span><span class="sxs-lookup"><span data-stu-id="bf158-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="bf158-187">另一個有趣的程式設計模式會使用 hello 計數 API。</span><span class="sxs-lookup"><span data-stu-id="bf158-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="bf158-188">在這裡，我們可以實作最佳通知型處理 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="bf158-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="bf158-189">hello 佇列計數可以是使用的 toothrottle 的加入佇列或清除佇列工作。</span><span class="sxs-lookup"><span data-stu-id="bf158-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="bf158-190">請注意，如同 hello 先前的範例，由於 hello 處理 hello 交易之外，就會發生未處理的項目可能會遺失是否在處理期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="bf158-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

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
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="bf158-191">盡可能清空</span><span class="sxs-lookup"><span data-stu-id="bf158-191">Best-Effort Drain</span></span>
<span data-ttu-id="bf158-192">由於 toohello hello 資料結構的並行處理的本質，無法保證 hello 佇列可清空。</span><span class="sxs-lookup"><span data-stu-id="bf158-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="bf158-193">它是可能的即使 hello 佇列上的沒有使用者作業進行中，特定呼叫 tooTryDequeueAsync 可能不會傳回一個項目先前已加入佇列，並被認可。</span><span class="sxs-lookup"><span data-stu-id="bf158-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="bf158-194">hello 加入佇列的項目太保證*最終*變成可見 toodequeue，不過沒有的頻外通訊機制，獨立的取用者不知道該 hello 佇列已達到穩定狀態，即使所有產生者已停止，並不允許任何新的佇列作業。</span><span class="sxs-lookup"><span data-stu-id="bf158-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="bf158-195">因此，hello 清空作業是最佳方式下實作。</span><span class="sxs-lookup"><span data-stu-id="bf158-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="bf158-196">hello 使用者應該停止所有進一步的生產者和取用者工作，並等候任何進行中的交易 toocommit 」 或 「 中止 」，然後再嘗試 toodrain hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="bf158-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="bf158-197">Hello 使用者知道預期的 hello hello 佇列中的項目數目，如果它們可以表示所有項目已清除佇列的通知設定。</span><span class="sxs-lookup"><span data-stu-id="bf158-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

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
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="bf158-198">預覽</span><span class="sxs-lookup"><span data-stu-id="bf158-198">Peek</span></span>
<span data-ttu-id="bf158-199">ReliableConcurrentQueue 不提供 hello *TryPeekAsync*應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="bf158-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="bf158-200">使用者可以取得 hello 查看語意*TryDequeueAsync* ，然後中止 hello 交易。</span><span class="sxs-lookup"><span data-stu-id="bf158-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="bf158-201">在此範例中，從佇列取出 hello 項目的值大於 1 時，才會處理*10*。</span><span class="sxs-lookup"><span data-stu-id="bf158-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
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

## <a name="must-read"></a><span data-ttu-id="bf158-202">必須閱讀</span><span class="sxs-lookup"><span data-stu-id="bf158-202">Must Read</span></span>
* [<span data-ttu-id="bf158-203">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="bf158-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="bf158-204">使用 Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="bf158-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="bf158-205">Reliable Services 通知</span><span class="sxs-lookup"><span data-stu-id="bf158-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="bf158-206">備份與還原 Reliable Services (災害復原)</span><span class="sxs-lookup"><span data-stu-id="bf158-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="bf158-207">Reliable State Manager 設定</span><span class="sxs-lookup"><span data-stu-id="bf158-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="bf158-208">開始使用 Service Fabric Web API 服務</span><span class="sxs-lookup"><span data-stu-id="bf158-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="bf158-209">Hello 可靠的服務程式設計模型的進階的用法</span><span class="sxs-lookup"><span data-stu-id="bf158-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="bf158-210">可靠集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="bf158-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
