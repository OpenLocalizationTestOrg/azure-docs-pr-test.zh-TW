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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>在 Azure Service Fabric 簡介 tooReliableConcurrentQueue
可靠的並行佇列是非同步、交易式和複寫的佇列，特徵是加入佇列與清除佇列作業的高並行存取。 它是設計的 toodeliver 高輸送量和低延遲的放鬆 hello 嚴格 FIFO 順序提供[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)並改為提供最佳順序。

## <a name="apis"></a>API

|並行佇列                |可靠的並行佇列                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Task EnqueueAsync(ITransaction tx, T item)                       |
| bool TryDequeue(out T result)  | Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)  |
| int Count()                    | long Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>與[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)進行比較

太可靠的並行佇列提供替代[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)。 它應用於不需要嚴格 FIFO 順序的情況，因為保證 FIFO 使用並行存取時需要有所取捨。  [可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)使用鎖定 tooenforce FIFO 順序，最多允許 tooenqueue 一個交易與在大部分的允許 toodequeue 一次一筆交易。 相較之下，可靠的並行佇列會放寬 hello 排序條件約束可讓任何數字的並行交易 toointerleave 其 enqueue 和清除佇列作業。 最佳順序為提供，不過 hello 相對順序的可靠的並行佇列中的兩個值不可以保證。

每當多個並行交易執行加入佇列或清除佇列時，可靠的並行佇列會提供比[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)更高的輸送量和更低的延遲。

範例使用案例 hello ReliableConcurrentQueue 是 hello[訊息佇列](https://en.wikipedia.org/wiki/Message_queue)案例。 在此案例中，一或多個訊息產生者建立和加入項目 toohello 佇列，和一或多個訊息取用者提取從 hello 佇列的訊息，並進行處理。 多個產生者和消費者可以獨立工作，使用並行的交易順序 tooprocess hello 佇列中。

## <a name="usage-guidelines"></a>使用方針
* hello 佇列預期 hello hello 佇列中的項目具有較低的保留期間。 也就是 hello 項目不願意 hello 佇列中時間太長。
* hello 佇列不保證有嚴格的 FIFO 順序。
* hello 佇列不會讀取其本身的寫入。 如果項目是在交易內加入佇列，不會顯示 tooa dequeuer hello 內相同的交易。
* 清除佇列不會彼此互相隔離。 如果項目*A*在交易中從佇列中清除*txnA*，即使*txnA*未認可，項目*A*並不會顯示 tooa 並行交易*txnB*。  如果*txnA*中止， *A*將變成可見太*txnB*立即。
* *TryPeekAsync*行為可以透過使用實作*TryDequeueAsync* ，然後中止 hello 交易。 這個範例，請參閱 hello 程式設計模式 > 一節中。
* 計數為非交易式。 它可以是使用的 tooget hello hello 佇列中的元素數目的了解代表的時間點，但無法依賴。
* 昂貴處理 hello 從佇列中清除項目不應執行 hello 異動處於作用中時 tooavoid 長時間執行的交易可能會有 hello 系統上的效能造成影響。

## <a name="code-snippets"></a>程式碼片段
讓我們看看幾個程式碼片段，和其預期的輸出。 本節中會忽略例外狀況處理。

### <a name="enqueueasync"></a>EnqueueAsync
以下是使用 EnqueueAsync 的幾個程式碼片段，隨後是其預期的輸出。

- 案例 1︰單一加入佇列工作

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

假設 hello 工作已順利完成，而且會有沒有並行交易修改 hello 佇列。 hello 使用者可以在任何下列訂單的 hello 預期 hello 佇列 toocontain hello 項目：

> 10, 20

> 20, 10


- 案例 2︰平行加入佇列工作

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

假設 hello 工作成功完成 hello 工作已執行，以平行方式，和已修改 hello 佇列沒有其他並行交易。 沒有推斷可 hello 順序 hello 佇列中的項目有關。 此程式碼片段，如 hello 項目可能會出現在任何 hello 4 ！ 可能的排序。  hello 佇列會嘗試 tookeep hello 項目順序 hello 原始 （佇列），但可能會強制的 tooreorder 它們到期 tooconcurrent 作業或錯誤。


### <a name="dequeueasync"></a>DequeueAsync
以下是幾個程式碼片段使用 TryDequeueAsync 後面接著 hello 預期輸出。 假設該 hello 佇列已經填入下列項目 hello 佇列中的 hello:
> 10, 20, 30, 40, 50, 60

- 案例 1︰單一清除佇列工作

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

假設 hello 工作已順利完成，而且會有沒有並行交易修改 hello 佇列。 關於 hello 順序的 hello hello 佇列中的項目成為沒有推斷，因為任何三個 hello 項目可能是佇列中清除，以任何順序。 hello 佇列會嘗試 tookeep hello 項目順序 hello 原始 （佇列），但可能會強制的 tooreorder 它們到期 tooconcurrent 作業或錯誤。  

- 案例 2︰平行清除佇列工作

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

假設 hello 工作成功完成 hello 工作已執行，以平行方式，和已修改 hello 佇列沒有其他並行交易。 關於 hello 順序的 hello hello 佇列中的項目成為沒有推斷，因為 hello 清單*dequeue1*和*dequeue2*將每個包含任何兩個項目，依任何順序。

相同的項目將的 hello*不*出現在這兩個清單中。 因此，如果 dequeue1 包含 10、*30*，dequeue2 就會包含 *20*、*40*。

- 案例 3︰使用交易中止來清除佇列排序

中止的交易進行中，從佇列取出的將 hello 項目回復 hello 佇列的 hello 最上層節點。 不保證在其中 hello 項目會放回 hello 佇列 hello 開頭的 hello 順序。 讓我們看看下列程式碼的 hello:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
假設 hello 項目已從佇列清除 hello 順序中：
> 10, 20

當我們中止 hello 交易時，hello 項目中要新增後 toohello head hello 佇列的任何下列訂單 hello:
> 10, 20

> 20, 10

hello 也適用於所有情況下，其中 hello 交易未成功*已認可*。

## <a name="programming-patterns"></a>程式設計模式
在本節中，我們來看看幾個可能有助於使用 ReliableConcurrentQueue 的程式設計模式。

### <a name="batch-dequeues"></a>批次清除佇列
建議的程式設計模式是針對 hello 取用者工作 toobatch 其佇列中清除，而不是執行一個清除佇列一次。 hello 使用者可以選擇每個批次或 hello 批次大小之間 toothrottle 延遲。 hello 下列程式碼片段示範這個程式設計模型。  請注意，在此範例中，hello 處理已完成之後 hello 交易被認可，, 因此如果錯誤處理 toooccur，hello 未處理的項目將會遺失而不需經過處理。  或者，可以完成 hello 處理 hello 交易在範圍內，不過這可能會對效能造成負面影響，而且需要已處理的 hello 項目處理。

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

### <a name="best-effort-notification-based-processing"></a>以通知作為基礎的最佳處理
另一個有趣的程式設計模式會使用 hello 計數 API。 在這裡，我們可以實作最佳通知型處理 hello 佇列。 hello 佇列計數可以是使用的 toothrottle 的加入佇列或清除佇列工作。  請注意，如同 hello 先前的範例，由於 hello 處理 hello 交易之外，就會發生未處理的項目可能會遺失是否在處理期間發生錯誤。

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

### <a name="best-effort-drain"></a>盡可能清空
由於 toohello hello 資料結構的並行處理的本質，無法保證 hello 佇列可清空。  它是可能的即使 hello 佇列上的沒有使用者作業進行中，特定呼叫 tooTryDequeueAsync 可能不會傳回一個項目先前已加入佇列，並被認可。  hello 加入佇列的項目太保證*最終*變成可見 toodequeue，不過沒有的頻外通訊機制，獨立的取用者不知道該 hello 佇列已達到穩定狀態，即使所有產生者已停止，並不允許任何新的佇列作業。 因此，hello 清空作業是最佳方式下實作。

hello 使用者應該停止所有進一步的生產者和取用者工作，並等候任何進行中的交易 toocommit 」 或 「 中止 」，然後再嘗試 toodrain hello 佇列。  Hello 使用者知道預期的 hello hello 佇列中的項目數目，如果它們可以表示所有項目已清除佇列的通知設定。

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

### <a name="peek"></a>預覽
ReliableConcurrentQueue 不提供 hello *TryPeekAsync*應用程式開發介面。 使用者可以取得 hello 查看語意*TryDequeueAsync* ，然後中止 hello 交易。 在此範例中，從佇列取出 hello 項目的值大於 1 時，才會處理*10*。

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

## <a name="must-read"></a>必須閱讀
* [Reliable Services 快速入門](service-fabric-reliable-services-quick-start.md)
* [使用 Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Reliable Services 通知](service-fabric-reliable-services-notifications.md)
* [備份與還原 Reliable Services (災害復原)](service-fabric-reliable-services-backup-restore.md)
* [Reliable State Manager 設定](service-fabric-reliable-services-configuration.md)
* [開始使用 Service Fabric Web API 服務](service-fabric-reliable-services-communication-webapi.md)
* [Hello 可靠的服務程式設計模型的進階的用法](service-fabric-reliable-services-advanced-usage.md)
* [可靠集合的開發人員參考資料](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
