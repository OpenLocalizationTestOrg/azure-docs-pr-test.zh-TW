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
# <a name="reliable-services-notifications"></a>Reliable Services 通知
通知可讓用戶端所進行的 tooan 物件他們感興趣的 tootrack hello 變更。 兩種類型的物件支援通知：「可靠的狀態管理員」和「可靠的字典」。

使用通知的常見原因如下：

* 建置具體化檢視，例如次要索引，或篩選的檢視 hello 複本狀態的彙總資料。 可靠的字典中所有索引鍵的排序索引便是其中一個例子。
* 傳送監視資料，例如 hello 加入 hello 在過去一小時內的使用者數目。

套用作業過程中即會引發通知。 因為如此，應該以最快速度處理通知，且同步事件不應包含任何耗費資源的作業。

## <a name="reliable-state-manager-notifications"></a>可靠的狀態管理員通知
Reliable 狀態管理員提供通知 hello 下列事件：

* 交易
  * 認可
* 狀態管理員
  * 重建
  * 加入可靠的狀態
  * 移除可靠的狀態

Reliable 狀態管理員會追蹤 hello 目前傳遞的交易。 hello 會導致引發通知 toobe 的交易狀態的唯一變更是認可交易。

可靠的狀態管理員會維護可靠狀態的集合，例如可靠的字典和可靠的佇列。 Reliable 狀態管理員在此集合變更時，就會引發通知： 加入或移除，穩定的狀態或重建 hello 整個集合。
在三個情況下，就會重建 hello 可靠狀態管理員集合：

* 復原： 複本啟動時，它會復原先前的狀態從 hello 磁碟。 在復原 hello 最後，它會使用**NotifyStateManagerChangedEventArgs** toofire 事件包含 hello 組復原可靠的狀態。
* 完整複製： 複本可以加入 hello 組態集之前，它有 toobe 建置。 有時候，這需要可靠狀態管理員的狀態從 hello 主要複本 toobe 套用的 toohello 閒置次要複本的完整複本。 在 hello 次要複本會使用 Reliable 狀態管理員**NotifyStateManagerChangedEventArgs** toofire 事件包含 hello 組可靠它取得從 hello 主要複本的狀態。
* 還原方面： 災害復原案例，在 hello 複本的狀態可以從備份還原透過**RestoreAsync**。 在這種情況下，可靠 hello 主要複本上的狀態管理員會使用**NotifyStateManagerChangedEventArgs** toofire 包含 hello 組可靠的狀態，便從 hello 備份還原的事件。

tooregister 交易通知及/或狀態管理員通知，您需要以 hello tooregister **TransactionChanged**或**StateManagerChanged**可靠狀態管理員上的事件。 常見的位置與這些事件處理常式 tooregister 是 hello 建構函式，您可設定狀態的服務。 當您註冊 hello 建構函式上時，您也不會錯過 hello 存留期間的變更所造成的任何通知**IReliableStateManager**。

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

hello **TransactionChanged**事件處理常式使用**NotifyTransactionChangedEventArgs** tooprovide hello 事件的詳細資料。 它包含的 hello 動作屬性 (例如， **NotifyTransactionChangedAction.Commit**) 指定變更的 hello 型別。 它也包含 hello 提供變更的參考 toohello 交易的交易屬性。

> [!NOTE]
> 現在， **TransactionChanged** hello 交易被認可時，才會引發事件。 hello 動作就等於太**NotifyTransactionChangedAction.Commit**。 但是在未來的 hello，可能會引發事件對於其他類型的交易狀態變更。 我們建議您檢查 hello 動作和處理 hello 事件只有在您預期的其中一個。
> 
> 

以下是範例 **TransactionChanged** 事件處理常式。

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

hello **StateManagerChanged**事件處理常式使用**NotifyStateManagerChangedEventArgs** tooprovide hello 事件的詳細資料。
**NotifyStateManagerChangedEventArgs** 有兩個子類別︰**NotifyStateManagerRebuildEventArgs** 和 **NotifyStateManagerSingleEntityChangedEventArgs**。
使用中的 hello 動作屬性**NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello 正確的子類別：

* **NotifyStateManagerChangedAction.Rebuild**：**NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** 和 **NotifyStateManagerChangedAction.Remove**：**NotifyStateManagerSingleEntityChangedEventArgs**

以下是範例 **StateManagerChanged** 通知處理常式。

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

## <a name="reliable-dictionary-notifications"></a>可靠的字典通知
可靠的字典提供 hello 下列事件的通知：

* 重建︰在 **ReliableDictionary** 從過去復原或複製的本機狀態或備份，復原其狀態時呼叫。
* 清除： 時呼叫 hello 狀態**ReliableDictionary**已清除透過 hello **ClearAsync**方法。
* 加入： 當太加入項目時呼叫**ReliableDictionary**。
* 更新︰在已更新 **IReliableDictionary** 中的項目時呼叫。
* 移除︰在已刪除 **IReliableDictionary** 中的項目時呼叫。

tooget 可靠字典通知，您需要以 hello tooregister **DictionaryChanged**上的事件處理常式**IReliableDictionary**。 常見的位置使用這些事件處理常式 tooregister 處於 hello **ReliableStateManager.StateManagerChanged**將通知。
註冊時**IReliableDictionary**太加入**IReliableStateManager**可確保您不會遺漏任何通知。

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
> **ProcessStateManagerSingleEntityNotification**是 hello 範例方法上述該 hello **OnStateManagerChangedHandler**範例會呼叫。
> 
> 

hello 上述程式碼中設定 hello **IReliableNotificationAsyncCallback**介面，以及與**DictionaryChanged**。 因為**NotifyDictionaryRebuildEventArgs**包含**IAsyncEnumerable**介面-這必須以非同步方式-列舉 toobe 重建通知會透過引發**RebuildNotificationAsyncCallback**而不是**OnDictionaryChangedHandler**。

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
> Hello 一部分處理 hello 重建通知，前面的程式碼，在第一個 hello 會維持已清除的彙總的狀態。 正在重建 hello 可靠集合與新的狀態，所有先前的通知是因為不相關。
> 
> 

hello **DictionaryChanged**事件處理常式使用**NotifyDictionaryChangedEventArgs** tooprovide hello 事件的詳細資料。
**NotifyDictionaryChangedEventArgs** 有五個子類別。 使用中的 hello 動作屬性**NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello 正確的子類別：

* **NotifyDictionaryChangedAction.Rebuild**：**NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**：**NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** 和 **NotifyDictionaryChangedAction.Remove**：**NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**：**NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**：**NotifyDictionaryItemRemovedEventArgs**

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

## <a name="recommendations"></a>建議
*  完成通知事件。
*  執行任何耗費資源的作業 (例如 IO 作業) 做為同步事件的一部分。
* *請勿*處理 hello 事件之前，請檢查 hello 動作類型。 Hello 未來可能會加入新的動作類型。

以下是一些事情 tookeep 記住：

* Hello 執行作業的一部分，會引發通知。 例如，還原通知就會引發 hello 的還原作業的最後一個步驟。 處理 hello 通知事件之前，將無法完成還原。
* Hello 套用作業的一部分，會引發通知，因為用戶端就會看到只在本機認可作業的通知。 而且因為作業會保證在本機認可的 toobe （亦即，記錄），它們可能會或可能不在未來的 hello 中復原。
* Hello 取消復原路徑上，單一通知會針對每個套用的作業引發。 這表示，如果交易 T1 包含 Create(X)、 Delete(X) 和 Create(X)，您會得到一則通知針對 hello 建立 X、 一個為 hello 刪除，一個用於 hello 建立同樣地，依此順序。
* 包含多項作業的交易，作業會套用已收到 hello hello 使用者的主要複本上的 hello 順序。
* 在處理錯誤的進度過程中，某些作業可能會復原。 這類復原作業，輪流 hello hello 複本後 tooa 穩定點狀態，都會引發通知。 復原通知的一個重要差異，是使用重複索引鍵的事件會彙總在一起。 例如，如果復原的交易 T1，您會看到單一通知 tooDelete(X)。

## <a name="next-steps"></a>後續步驟
* [可靠的集合](service-fabric-work-with-reliable-collections.md)
* [Reliable Services 快速入門](service-fabric-reliable-services-quick-start.md)
* [備份與還原 Reliable Services (災害復原)](service-fabric-reliable-services-backup-restore.md)
* [可靠的集合的開發人員參考資料](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

