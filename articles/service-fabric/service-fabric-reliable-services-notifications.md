---
title: "Reliable Services 通知 | Microsoft Docs"
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
ms.openlocfilehash: c6a53d851510ed5e6eec1f3ac0f636ad034a6d4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="d7c59-103">Reliable Services 通知</span><span class="sxs-lookup"><span data-stu-id="d7c59-103">Reliable Services notifications</span></span>
<span data-ttu-id="d7c59-104">通知可讓用戶端追蹤對於他們感興趣物件所進行的變更。</span><span class="sxs-lookup"><span data-stu-id="d7c59-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="d7c59-105">兩種類型的物件支援通知：「可靠的狀態管理員」和「可靠的字典」。</span><span class="sxs-lookup"><span data-stu-id="d7c59-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="d7c59-106">使用通知的常見原因如下：</span><span class="sxs-lookup"><span data-stu-id="d7c59-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="d7c59-107">建置具體化檢視 (例如次要索引) 或複本狀態的彙總篩選檢視。</span><span class="sxs-lookup"><span data-stu-id="d7c59-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="d7c59-108">可靠的字典中所有索引鍵的排序索引便是其中一個例子。</span><span class="sxs-lookup"><span data-stu-id="d7c59-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="d7c59-109">傳送監視資料，例如過去一小時內新增的使用者數目。</span><span class="sxs-lookup"><span data-stu-id="d7c59-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="d7c59-110">套用作業過程中即會引發通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="d7c59-111">因為如此，應該以最快速度處理通知，且同步事件不應包含任何耗費資源的作業。</span><span class="sxs-lookup"><span data-stu-id="d7c59-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="d7c59-112">可靠的狀態管理員通知</span><span class="sxs-lookup"><span data-stu-id="d7c59-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="d7c59-113">可靠的狀態管理員提供下列事件的通知︰</span><span class="sxs-lookup"><span data-stu-id="d7c59-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="d7c59-114">交易</span><span class="sxs-lookup"><span data-stu-id="d7c59-114">Transaction</span></span>
  * <span data-ttu-id="d7c59-115">認可</span><span class="sxs-lookup"><span data-stu-id="d7c59-115">Commit</span></span>
* <span data-ttu-id="d7c59-116">狀態管理員</span><span class="sxs-lookup"><span data-stu-id="d7c59-116">State manager</span></span>
  * <span data-ttu-id="d7c59-117">重建</span><span class="sxs-lookup"><span data-stu-id="d7c59-117">Rebuild</span></span>
  * <span data-ttu-id="d7c59-118">加入可靠的狀態</span><span class="sxs-lookup"><span data-stu-id="d7c59-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="d7c59-119">移除可靠的狀態</span><span class="sxs-lookup"><span data-stu-id="d7c59-119">Removal of a reliable state</span></span>

<span data-ttu-id="d7c59-120">可靠狀態管理員會追蹤目前傳遞的交易。</span><span class="sxs-lookup"><span data-stu-id="d7c59-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="d7c59-121">唯一會造成通知引發的交易狀態變更是認可交易。</span><span class="sxs-lookup"><span data-stu-id="d7c59-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="d7c59-122">可靠的狀態管理員會維護可靠狀態的集合，例如可靠的字典和可靠的佇列。</span><span class="sxs-lookup"><span data-stu-id="d7c59-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="d7c59-123">可靠的狀態管理員會在此集合變更時引發通知︰加入或移除可靠的狀態，或者重建整個集合時。</span><span class="sxs-lookup"><span data-stu-id="d7c59-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="d7c59-124">可靠的狀態管理員集合會在下列三種情況下重建：</span><span class="sxs-lookup"><span data-stu-id="d7c59-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="d7c59-125">復原︰當複本啟動時，它會從磁碟復原為先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="d7c59-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="d7c59-126">復原結束時，它會利用 **NotifyStateManagerChangedEventArgs** 引發事件，其中包含一組復原的可靠狀態。</span><span class="sxs-lookup"><span data-stu-id="d7c59-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="d7c59-127">完整備份︰在複本可加入組態集之前，必須先建置它。</span><span class="sxs-lookup"><span data-stu-id="d7c59-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="d7c59-128">有時，這需要主要複本的可靠狀態管理員的狀態完整複本，以套用到閒置的次要複本。</span><span class="sxs-lookup"><span data-stu-id="d7c59-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="d7c59-129">次要複本上的可靠狀態管理員會使用 **NotifyStateManagerChangedEventArgs** 引發事件，其中包含一組它從主要複本取得的可靠狀態。</span><span class="sxs-lookup"><span data-stu-id="d7c59-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="d7c59-130">還原︰在災害復原案例中，複本的狀態可經由 **RestoreAsync**從備份還原。</span><span class="sxs-lookup"><span data-stu-id="d7c59-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="d7c59-131">在這類案例中，主要複本上的可靠狀態管理員會使用 **NotifyStateManagerChangedEventArgs** 引發事件，其中包含一組它從備份還原來的可靠狀態。</span><span class="sxs-lookup"><span data-stu-id="d7c59-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="d7c59-132">若要註冊交易通知及/或狀態管理員通知，您必須向可靠的狀態管理員分別註冊 **TransactionChanged** 或 **StateManagerChanged** 事件。</span><span class="sxs-lookup"><span data-stu-id="d7c59-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="d7c59-133">註冊這些事件處理常式的常見位置是您的具狀態服務的建構函式。</span><span class="sxs-lookup"><span data-stu-id="d7c59-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="d7c59-134">當您註冊建構函式時，您也不會錯過 **IReliableStateManager**存留期間的變更所造成的任何通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="d7c59-135">**TransactionChanged** 事件處理常式會使用 **NotifyTransactionChangedEventArgs** ，來提供關於事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d7c59-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="d7c59-136">它包含指定變更類型的 Action 屬性 (例如， **NotifyTransactionChangedAction.Commit**)。</span><span class="sxs-lookup"><span data-stu-id="d7c59-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="d7c59-137">它也包含提供「指向變更之交易的參考」的交易屬性。</span><span class="sxs-lookup"><span data-stu-id="d7c59-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="d7c59-138">現在，只有認可交易才會引發 **TransactionChanged** 事件。</span><span class="sxs-lookup"><span data-stu-id="d7c59-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="d7c59-139">此動作等於 **NotifyTransactionChangedAction.Commit**。</span><span class="sxs-lookup"><span data-stu-id="d7c59-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="d7c59-140">但是在未來，可能會有其他類型的交易狀態變更可以引發事件。</span><span class="sxs-lookup"><span data-stu-id="d7c59-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="d7c59-141">我們建議您檢查動作，並只在您預期的事件發生時處理事件。</span><span class="sxs-lookup"><span data-stu-id="d7c59-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="d7c59-142">以下是範例 **TransactionChanged** 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="d7c59-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="d7c59-143">**StateManagerChanged** 事件處理常式使用 **NotifyStateManagerChangedEventArgs** 來提供事件的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d7c59-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="d7c59-144">**NotifyStateManagerChangedEventArgs** 有兩個子類別︰**NotifyStateManagerRebuildEventArgs** 和 **NotifyStateManagerSingleEntityChangedEventArgs**。</span><span class="sxs-lookup"><span data-stu-id="d7c59-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="d7c59-145">您使用 **NotifyStateManagerChangedEventArgs** 中的 Action 屬性將 **NotifyStateManagerChangedEventArgs** 轉換為正確的子類別︰</span><span class="sxs-lookup"><span data-stu-id="d7c59-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="d7c59-146">**NotifyStateManagerChangedAction.Rebuild**：**NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="d7c59-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="d7c59-147">**NotifyStateManagerChangedAction.Add** 和 **NotifyStateManagerChangedAction.Remove**：**NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="d7c59-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="d7c59-148">以下是範例 **StateManagerChanged** 通知處理常式。</span><span class="sxs-lookup"><span data-stu-id="d7c59-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="d7c59-149">可靠的字典通知</span><span class="sxs-lookup"><span data-stu-id="d7c59-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="d7c59-150">可靠的字典提供下列事件的通知︰</span><span class="sxs-lookup"><span data-stu-id="d7c59-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="d7c59-151">重建︰在 **ReliableDictionary** 從過去復原或複製的本機狀態或備份，復原其狀態時呼叫。</span><span class="sxs-lookup"><span data-stu-id="d7c59-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="d7c59-152">清除︰在透過 **ClearAsync** 方法清除 **ReliableDictionary** 的狀態時呼叫。</span><span class="sxs-lookup"><span data-stu-id="d7c59-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="d7c59-153">加入︰在已將項目加入至 **ReliableDictionary**時呼叫。</span><span class="sxs-lookup"><span data-stu-id="d7c59-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="d7c59-154">更新︰在已更新 **IReliableDictionary** 中的項目時呼叫。</span><span class="sxs-lookup"><span data-stu-id="d7c59-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="d7c59-155">移除︰在已刪除 **IReliableDictionary** 中的項目時呼叫。</span><span class="sxs-lookup"><span data-stu-id="d7c59-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="d7c59-156">若要註冊可靠的字典通知，使用者必須在 **IReliableDictionary** 上註冊事件處理常式 **DictionaryChanged**。</span><span class="sxs-lookup"><span data-stu-id="d7c59-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="d7c59-157">註冊這些事件處理常式的常見位置是在 **ReliableStateManager.StateManagerChanged** 加入通知中。</span><span class="sxs-lookup"><span data-stu-id="d7c59-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="d7c59-158">在將 **IReliableDictionary** 加入 **IReliableStateManager** 時註冊，可確保您不會錯過任何通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="d7c59-159">**ProcessStateManagerSingleEntityNotification** 是前述 **OnStateManagerChangedHandler** 範例所呼叫的範例方法。</span><span class="sxs-lookup"><span data-stu-id="d7c59-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="d7c59-160">上述程式碼會設定 **IReliableNotificationAsyncCallback** 介面以及 **DictionaryChanged**。</span><span class="sxs-lookup"><span data-stu-id="d7c59-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="d7c59-161">由於 **NotifyDictionaryRebuildEventArgs** 包含需要以非同步方式列舉的 **IAsyncEnumerable** 介面，因此會透過 **RebuildNotificationAsyncCallback** 而不是 **OnDictionaryChangedHandler** 來引發重建通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="d7c59-162">在上述程式碼中，於處理重建通知的過程中，會先清除所維護的彙總狀態。</span><span class="sxs-lookup"><span data-stu-id="d7c59-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="d7c59-163">因為正在利用新狀態重建可靠的集合，因此與先前的所有通知無關。</span><span class="sxs-lookup"><span data-stu-id="d7c59-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="d7c59-164">**DictionaryChanged** 事件處理常式會使用 **NotifyDictionaryChangedEventArgs** 來提供關於事件的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d7c59-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="d7c59-165">**NotifyDictionaryChangedEventArgs** 有五個子類別。</span><span class="sxs-lookup"><span data-stu-id="d7c59-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="d7c59-166">使用 **NotifyDictionaryChangedEventArgs** 中的 Action 屬性將 **NotifyDictionaryChangedEventArgs** 轉換為正確的子類別：</span><span class="sxs-lookup"><span data-stu-id="d7c59-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="d7c59-167">**NotifyDictionaryChangedAction.Rebuild**：**NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="d7c59-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="d7c59-168">**NotifyDictionaryChangedAction.Clear**：**NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="d7c59-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="d7c59-169">**NotifyDictionaryChangedAction.Add** 和 **NotifyDictionaryChangedAction.Remove**：**NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="d7c59-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="d7c59-170">**NotifyDictionaryChangedAction.Update**：**NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="d7c59-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="d7c59-171">**NotifyDictionaryChangedAction.Remove**：**NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="d7c59-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="d7c59-172">建議</span><span class="sxs-lookup"><span data-stu-id="d7c59-172">Recommendations</span></span>
* <span data-ttu-id="d7c59-173"> 完成通知事件。</span><span class="sxs-lookup"><span data-stu-id="d7c59-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="d7c59-174"> 執行任何耗費資源的作業 (例如 IO 作業) 做為同步事件的一部分。</span><span class="sxs-lookup"><span data-stu-id="d7c59-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="d7c59-175"> Action 類型。</span><span class="sxs-lookup"><span data-stu-id="d7c59-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="d7c59-176">未來可能會加入新的 Action 類型。</span><span class="sxs-lookup"><span data-stu-id="d7c59-176">New action types might be added in the future.</span></span>

<span data-ttu-id="d7c59-177">以下是要牢記在心的一些事項：</span><span class="sxs-lookup"><span data-stu-id="d7c59-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="d7c59-178">通知會在執行作業過程中引發。</span><span class="sxs-lookup"><span data-stu-id="d7c59-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="d7c59-179">例如，在還原作業的最後一個步驟引發還原通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="d7c59-180">處理通知事件之前，不會完成還原。</span><span class="sxs-lookup"><span data-stu-id="d7c59-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="d7c59-181">因為通知是在套用作業過程中引發，因此，用戶端只會看見本機認可作業的通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="d7c59-182">而且因為作業只保證會在本機認可 (亦即記錄)，所以它們不一定可在未來復原。</span><span class="sxs-lookup"><span data-stu-id="d7c59-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="d7c59-183">在取消復原路徑上，會針對每個套用的作業引發單一通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="d7c59-184">這表示，如果交易 T1 包含 Create(X)、Delete(X)、Create(X)，您將依序得到一個針對 X 建立的通知、一個針對刪除的通知，然後再收到一個建立的通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="d7c59-185">如果是包含多個作業的交易，作業將依使用者在主要本上收到它們的順序套用。</span><span class="sxs-lookup"><span data-stu-id="d7c59-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="d7c59-186">在處理錯誤的進度過程中，某些作業可能會復原。</span><span class="sxs-lookup"><span data-stu-id="d7c59-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="d7c59-187">通知會針對這類復原作業加以引發，將複本狀態輪換回到可靠的時間點。</span><span class="sxs-lookup"><span data-stu-id="d7c59-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="d7c59-188">復原通知的一個重要差異，是使用重複索引鍵的事件會彙總在一起。</span><span class="sxs-lookup"><span data-stu-id="d7c59-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="d7c59-189">例如，如果復原上述的 T1，使用者將會看到 Delete(X) 的單一通知。</span><span class="sxs-lookup"><span data-stu-id="d7c59-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7c59-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7c59-190">Next steps</span></span>
* [<span data-ttu-id="d7c59-191">可靠的集合</span><span class="sxs-lookup"><span data-stu-id="d7c59-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="d7c59-192">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="d7c59-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="d7c59-193">備份與還原 Reliable Services (災害復原)</span><span class="sxs-lookup"><span data-stu-id="d7c59-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="d7c59-194">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="d7c59-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

