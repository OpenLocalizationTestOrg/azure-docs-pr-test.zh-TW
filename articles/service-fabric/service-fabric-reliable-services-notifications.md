---
title: "aaaReliable 服務通知 |Microsoft 文件"
description: "Service Fabric Reliable Services 通知的概念文件"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="7bf53-103">Reliable Services 通知</span><span class="sxs-lookup"><span data-stu-id="7bf53-103">Reliable Services notifications</span></span>
<span data-ttu-id="7bf53-104">通知可讓用戶端所進行的 tooan 物件他們感興趣的 tootrack hello 變更。</span><span class="sxs-lookup"><span data-stu-id="7bf53-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="7bf53-105">兩種類型的物件支援通知：「可靠的狀態管理員」和「可靠的字典」。</span><span class="sxs-lookup"><span data-stu-id="7bf53-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="7bf53-106">使用通知的常見原因如下：</span><span class="sxs-lookup"><span data-stu-id="7bf53-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="7bf53-107">建置具體化檢視，例如次要索引，或篩選的檢視 hello 複本狀態的彙總資料。</span><span class="sxs-lookup"><span data-stu-id="7bf53-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="7bf53-108">可靠的字典中所有索引鍵的排序索引便是其中一個例子。</span><span class="sxs-lookup"><span data-stu-id="7bf53-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="7bf53-109">傳送監視資料，例如 hello 加入 hello 在過去一小時內的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="7bf53-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="7bf53-110">套用作業過程中即會引發通知。</span><span class="sxs-lookup"><span data-stu-id="7bf53-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="7bf53-111">因為如此，應該以最快速度處理通知，且同步事件不應包含任何耗費資源的作業。</span><span class="sxs-lookup"><span data-stu-id="7bf53-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="7bf53-112">可靠的狀態管理員通知</span><span class="sxs-lookup"><span data-stu-id="7bf53-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="7bf53-113">Reliable 狀態管理員提供通知 hello 下列事件：</span><span class="sxs-lookup"><span data-stu-id="7bf53-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="7bf53-114">交易</span><span class="sxs-lookup"><span data-stu-id="7bf53-114">Transaction</span></span>
  * <span data-ttu-id="7bf53-115">認可</span><span class="sxs-lookup"><span data-stu-id="7bf53-115">Commit</span></span>
* <span data-ttu-id="7bf53-116">狀態管理員</span><span class="sxs-lookup"><span data-stu-id="7bf53-116">State manager</span></span>
  * <span data-ttu-id="7bf53-117">重建</span><span class="sxs-lookup"><span data-stu-id="7bf53-117">Rebuild</span></span>
  * <span data-ttu-id="7bf53-118">加入可靠的狀態</span><span class="sxs-lookup"><span data-stu-id="7bf53-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="7bf53-119">移除可靠的狀態</span><span class="sxs-lookup"><span data-stu-id="7bf53-119">Removal of a reliable state</span></span>

<span data-ttu-id="7bf53-120">Reliable 狀態管理員會追蹤 hello 目前傳遞的交易。</span><span class="sxs-lookup"><span data-stu-id="7bf53-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="7bf53-121">hello 會導致引發通知 toobe 的交易狀態的唯一變更是認可交易。</span><span class="sxs-lookup"><span data-stu-id="7bf53-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="7bf53-122">可靠的狀態管理員會維護可靠狀態的集合，例如可靠的字典和可靠的佇列。</span><span class="sxs-lookup"><span data-stu-id="7bf53-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="7bf53-123">Reliable 狀態管理員在此集合變更時，就會引發通知： 加入或移除，穩定的狀態或重建 hello 整個集合。</span><span class="sxs-lookup"><span data-stu-id="7bf53-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="7bf53-124">在三個情況下，就會重建 hello 可靠狀態管理員集合：</span><span class="sxs-lookup"><span data-stu-id="7bf53-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="7bf53-125">復原： 複本啟動時，它會復原先前的狀態從 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="7bf53-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="7bf53-126">在復原 hello 最後，它會使用**NotifyStateManagerChangedEventArgs** toofire 事件包含 hello 組復原可靠的狀態。</span><span class="sxs-lookup"><span data-stu-id="7bf53-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="7bf53-127">完整複製： 複本可以加入 hello 組態集之前，它有 toobe 建置。</span><span class="sxs-lookup"><span data-stu-id="7bf53-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="7bf53-128">有時候，這需要可靠狀態管理員的狀態從 hello 主要複本 toobe 套用的 toohello 閒置次要複本的完整複本。</span><span class="sxs-lookup"><span data-stu-id="7bf53-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="7bf53-129">在 hello 次要複本會使用 Reliable 狀態管理員**NotifyStateManagerChangedEventArgs** toofire 事件包含 hello 組可靠它取得從 hello 主要複本的狀態。</span><span class="sxs-lookup"><span data-stu-id="7bf53-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="7bf53-130">還原方面： 災害復原案例，在 hello 複本的狀態可以從備份還原透過**RestoreAsync**。</span><span class="sxs-lookup"><span data-stu-id="7bf53-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="7bf53-131">在這種情況下，可靠 hello 主要複本上的狀態管理員會使用**NotifyStateManagerChangedEventArgs** toofire 包含 hello 組可靠的狀態，便從 hello 備份還原的事件。</span><span class="sxs-lookup"><span data-stu-id="7bf53-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="7bf53-132">tooregister 交易通知及/或狀態管理員通知，您需要以 hello tooregister **TransactionChanged**或**StateManagerChanged**可靠狀態管理員上的事件。</span><span class="sxs-lookup"><span data-stu-id="7bf53-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="7bf53-133">常見的位置與這些事件處理常式 tooregister 是 hello 建構函式，您可設定狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="7bf53-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="7bf53-134">當您註冊 hello 建構函式上時，您也不會錯過 hello 存留期間的變更所造成的任何通知**IReliableStateManager**。</span><span class="sxs-lookup"><span data-stu-id="7bf53-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="7bf53-135">hello **TransactionChanged**事件處理常式使用**NotifyTransactionChangedEventArgs** tooprovide hello 事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7bf53-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="7bf53-136">它包含的 hello 動作屬性 (例如， **NotifyTransactionChangedAction.Commit**) 指定變更的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="7bf53-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="7bf53-137">它也包含 hello 提供變更的參考 toohello 交易的交易屬性。</span><span class="sxs-lookup"><span data-stu-id="7bf53-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="7bf53-138">現在， **TransactionChanged** hello 交易被認可時，才會引發事件。</span><span class="sxs-lookup"><span data-stu-id="7bf53-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="7bf53-139">hello 動作就等於太**NotifyTransactionChangedAction.Commit**。</span><span class="sxs-lookup"><span data-stu-id="7bf53-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="7bf53-140">但是在未來的 hello，可能會引發事件對於其他類型的交易狀態變更。</span><span class="sxs-lookup"><span data-stu-id="7bf53-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="7bf53-141">我們建議您檢查 hello 動作和處理 hello 事件只有在您預期的其中一個。</span><span class="sxs-lookup"><span data-stu-id="7bf53-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="7bf53-142">以下是範例 **TransactionChanged** 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="7bf53-142">Following is an example **TransactionChanged** event handler.</span></span>

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

<span data-ttu-id="7bf53-143">hello **StateManagerChanged**事件處理常式使用**NotifyStateManagerChangedEventArgs** tooprovide hello 事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7bf53-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="7bf53-144">**NotifyStateManagerChangedEventArgs** 有兩個子類別︰**NotifyStateManagerRebuildEventArgs** 和 **NotifyStateManagerSingleEntityChangedEventArgs**。</span><span class="sxs-lookup"><span data-stu-id="7bf53-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="7bf53-145">使用中的 hello 動作屬性**NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello 正確的子類別：</span><span class="sxs-lookup"><span data-stu-id="7bf53-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="7bf53-146">**NotifyStateManagerChangedAction.Rebuild**：**NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="7bf53-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="7bf53-147">**NotifyStateManagerChangedAction.Add** 和 **NotifyStateManagerChangedAction.Remove**：**NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="7bf53-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="7bf53-148">以下是範例 **StateManagerChanged** 通知處理常式。</span><span class="sxs-lookup"><span data-stu-id="7bf53-148">Following is an example **StateManagerChanged** notification handler.</span></span>

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="7bf53-149">可靠的字典通知</span><span class="sxs-lookup"><span data-stu-id="7bf53-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="7bf53-150">可靠的字典提供 hello 下列事件的通知：</span><span class="sxs-lookup"><span data-stu-id="7bf53-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="7bf53-151">重建︰在 **ReliableDictionary** 從過去復原或複製的本機狀態或備份，復原其狀態時呼叫。</span><span class="sxs-lookup"><span data-stu-id="7bf53-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="7bf53-152">清除： 時呼叫 hello 狀態**ReliableDictionary**已清除透過 hello **ClearAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="7bf53-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="7bf53-153">加入： 當太加入項目時呼叫**ReliableDictionary**。</span><span class="sxs-lookup"><span data-stu-id="7bf53-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="7bf53-154">更新︰在已更新 **IReliableDictionary** 中的項目時呼叫。</span><span class="sxs-lookup"><span data-stu-id="7bf53-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="7bf53-155">移除︰在已刪除 **IReliableDictionary** 中的項目時呼叫。</span><span class="sxs-lookup"><span data-stu-id="7bf53-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="7bf53-156">tooget 可靠字典通知，您需要以 hello tooregister **DictionaryChanged**上的事件處理常式**IReliableDictionary**。</span><span class="sxs-lookup"><span data-stu-id="7bf53-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="7bf53-157">常見的位置使用這些事件處理常式 tooregister 處於 hello **ReliableStateManager.StateManagerChanged**將通知。</span><span class="sxs-lookup"><span data-stu-id="7bf53-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="7bf53-158">註冊時**IReliableDictionary**太加入**IReliableStateManager**可確保您不會遺漏任何通知。</span><span class="sxs-lookup"><span data-stu-id="7bf53-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="7bf53-159">**ProcessStateManagerSingleEntityNotification**是 hello 範例方法上述該 hello **OnStateManagerChangedHandler**範例會呼叫。</span><span class="sxs-lookup"><span data-stu-id="7bf53-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="7bf53-160">hello 上述程式碼中設定 hello **IReliableNotificationAsyncCallback**介面，以及與**DictionaryChanged**。</span><span class="sxs-lookup"><span data-stu-id="7bf53-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="7bf53-161">因為**NotifyDictionaryRebuildEventArgs**包含**IAsyncEnumerable**介面-這必須以非同步方式-列舉 toobe 重建通知會透過引發**RebuildNotificationAsyncCallback**而不是**OnDictionaryChangedHandler**。</span><span class="sxs-lookup"><span data-stu-id="7bf53-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> <span data-ttu-id="7bf53-162">Hello 一部分處理 hello 重建通知，前面的程式碼，在第一個 hello 會維持已清除的彙總的狀態。</span><span class="sxs-lookup"><span data-stu-id="7bf53-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="7bf53-163">正在重建 hello 可靠集合與新的狀態，所有先前的通知是因為不相關。</span><span class="sxs-lookup"><span data-stu-id="7bf53-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="7bf53-164">hello **DictionaryChanged**事件處理常式使用**NotifyDictionaryChangedEventArgs** tooprovide hello 事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7bf53-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="7bf53-165">**NotifyDictionaryChangedEventArgs** 有五個子類別。</span><span class="sxs-lookup"><span data-stu-id="7bf53-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="7bf53-166">使用中的 hello 動作屬性**NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello 正確的子類別：</span><span class="sxs-lookup"><span data-stu-id="7bf53-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="7bf53-167">**NotifyDictionaryChangedAction.Rebuild**：**NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="7bf53-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="7bf53-168">**NotifyDictionaryChangedAction.Clear**：**NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="7bf53-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="7bf53-169">**NotifyDictionaryChangedAction.Add** 和 **NotifyDictionaryChangedAction.Remove**：**NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="7bf53-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="7bf53-170">**NotifyDictionaryChangedAction.Update**：**NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="7bf53-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="7bf53-171">**NotifyDictionaryChangedAction.Remove**：**NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="7bf53-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a><span data-ttu-id="7bf53-172">建議</span><span class="sxs-lookup"><span data-stu-id="7bf53-172">Recommendations</span></span>
* <span data-ttu-id="7bf53-173"> 完成通知事件。</span><span class="sxs-lookup"><span data-stu-id="7bf53-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="7bf53-174"> 執行任何耗費資源的作業 (例如 IO 作業) 做為同步事件的一部分。</span><span class="sxs-lookup"><span data-stu-id="7bf53-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="7bf53-175">*請勿*處理 hello 事件之前，請檢查 hello 動作類型。</span><span class="sxs-lookup"><span data-stu-id="7bf53-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="7bf53-176">Hello 未來可能會加入新的動作類型。</span><span class="sxs-lookup"><span data-stu-id="7bf53-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="7bf53-177">以下是一些事情 tookeep 記住：</span><span class="sxs-lookup"><span data-stu-id="7bf53-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="7bf53-178">Hello 執行作業的一部分，會引發通知。</span><span class="sxs-lookup"><span data-stu-id="7bf53-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="7bf53-179">例如，還原通知就會引發 hello 的還原作業的最後一個步驟。</span><span class="sxs-lookup"><span data-stu-id="7bf53-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="7bf53-180">處理 hello 通知事件之前，將無法完成還原。</span><span class="sxs-lookup"><span data-stu-id="7bf53-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="7bf53-181">Hello 套用作業的一部分，會引發通知，因為用戶端就會看到只在本機認可作業的通知。</span><span class="sxs-lookup"><span data-stu-id="7bf53-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="7bf53-182">而且因為作業會保證在本機認可的 toobe （亦即，記錄），它們可能會或可能不在未來的 hello 中復原。</span><span class="sxs-lookup"><span data-stu-id="7bf53-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="7bf53-183">Hello 取消復原路徑上，單一通知會針對每個套用的作業引發。</span><span class="sxs-lookup"><span data-stu-id="7bf53-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="7bf53-184">這表示，如果交易 T1 包含 Create(X)、 Delete(X) 和 Create(X)，您會得到一則通知針對 hello 建立 X、 一個為 hello 刪除，一個用於 hello 建立同樣地，依此順序。</span><span class="sxs-lookup"><span data-stu-id="7bf53-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="7bf53-185">包含多項作業的交易，作業會套用已收到 hello hello 使用者的主要複本上的 hello 順序。</span><span class="sxs-lookup"><span data-stu-id="7bf53-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="7bf53-186">在處理錯誤的進度過程中，某些作業可能會復原。</span><span class="sxs-lookup"><span data-stu-id="7bf53-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="7bf53-187">這類復原作業，輪流 hello hello 複本後 tooa 穩定點狀態，都會引發通知。</span><span class="sxs-lookup"><span data-stu-id="7bf53-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="7bf53-188">復原通知的一個重要差異，是使用重複索引鍵的事件會彙總在一起。</span><span class="sxs-lookup"><span data-stu-id="7bf53-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="7bf53-189">例如，如果復原的交易 T1，您會看到單一通知 tooDelete(X)。</span><span class="sxs-lookup"><span data-stu-id="7bf53-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bf53-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7bf53-190">Next steps</span></span>
* [<span data-ttu-id="7bf53-191">可靠的集合</span><span class="sxs-lookup"><span data-stu-id="7bf53-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="7bf53-192">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="7bf53-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="7bf53-193">備份與還原 Reliable Services (災害復原)</span><span class="sxs-lookup"><span data-stu-id="7bf53-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="7bf53-194">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="7bf53-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

