---
title: "與可靠的集合 aaaWorking |Microsoft 文件"
description: "了解 hello 與可靠的集合所使用的最佳作法。"
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a>使用可靠的集合
Service Fabric 提供了可設定狀態的程式設計模型使用 too.NET 開發人員透過可靠的集合。 具體來說，Service Fabric 提供了可靠的字典和可靠的佇列類別。 當您使用這些類別時，您的狀態是分割的 (延展性)、複寫的 (可用性)，且在分割區內交易 (ACID 語意)。 讓我們看看可靠字典物件的一般用法，並看看它究竟做些什麼。

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

可靠的字典物件上的所有作業 (除了無法復原的 ClearAsync)，都需要一個 ITransaction 物件。 此物件具有與其相關聯試圖 toomake tooany 可靠字典和/或單一資料分割內的可靠的佇列物件的任何或所有變更。 取得 itransaction:: 藉由呼叫 hello 磁碟分割物件的 StateManager 的 CreateTransaction 方法。

在上述的 hello 程式碼，傳遞 tooa 可靠字典的 AddAsync 方法 hello itransaction:: 物件。 就內部而言，可接受的索引鍵的字典方法會採用 hello 索引鍵相關聯的讀取器/寫入器鎖定。 如果 hello 方法修改 hello 索引鍵的值，hello 方法使用的寫入鎖定 hello 索引鍵上，如果 hello 方法只會讀取 hello 索引鍵的值，然後讀取的鎖定採取 hello 索引鍵。 因為 AddAsync 修改新的索引鍵 hello 值 toohello，傳入的 hello 機碼的寫入鎖定會取得值。 因此，如果 2 （或以上） 的執行緒嘗試以 hello tooadd 值相同索引鍵在 hello 相同時間，一個執行緒將會取得 hello 寫入鎖定，hello 其他執行緒會封鎖。 根據預設，方法會封鎖的總 too4 秒 tooacquire hello 鎖定;4 秒之後，hello 方法會擲回 TimeoutException。 如果您想使用，方法多載存在允許您 toopass 明確的逾時值。

通常，您可以撰寫您的程式碼 tooreact tooa TimeoutException 所攔截和重試 hello 整個作業 （如上述的 hello 程式碼所示）。 在我的簡單程式碼中，只呼叫 Task.Delay 每次傳遞 100 毫秒。 但在實際狀況裡，最好還是改用某種指數型的撤退延遲。

Hello 鎖定，則一旦 AddAsync 將 hello 的索引鍵和值物件參考 tooan 內部的暫存目錄與 hello itransaction:: 物件相關聯。 這是 tooprovide 您讀取您-擁有-寫入語意。 也就是說，呼叫 AddAsync，稍後呼叫 tooTryGetValueAsync 後 (使用 hello itransaction:: 相同的物件) 會傳回 hello 值，即使尚未認可 hello 交易。 接下來，AddAsync 序列化您的金鑰和值物件 toobyte 陣列，並將附加 hello 本機節點上的這些位元組陣列 tooa 記錄檔。 最後，AddAsync 傳送嗨位元組陣列 tooall hello 次要複本，他們擁有 hello 相同索引鍵/值的資訊。 即使 hello 索引鍵/值的資訊已寫入 tooa 記錄檔，hello 資訊之前不能算是 hello 字典的組件相關聯的 hello 交易已認可。

在上述的 hello 程式碼，hello 呼叫 tooCommitAsync 認可的所有 hello 交易的作業。 具體來說，它會附加認可資訊 toohello hello 本機節點上的記錄檔，並也會傳送 hello 認可記錄 tooall hello 次要複本。 所有資料變更會視為永久性而與所操作經由都 hello itransaction:: 物件的索引鍵相關聯的任何鎖定被釋放因此其他執行緒 / 交易可以操作回覆都 hello 複本的仲裁 （多數），一旦都 hello 相同的索引鍵和其值。

如果未呼叫 CommitAsync （通常是因為 tooan 擲回例外狀況），取得處置 hello itransaction:: 物件。 當處置未認可 itransaction:: 物件，Service Fabric 附加中止資訊 toohello 本機節點的記錄檔，並不需要 toobe 傳送的 hello tooany 次要複本。 且已透過 hello 交易操作的索引鍵相關聯的任何鎖定，會釋放。

## <a name="common-pitfalls-and-how-tooavoid-them"></a>常見的問題及如何 tooavoid 它們
既然您了解 hello 可靠集合在內部運作的方式，讓我們看看其中一些常見的誤用。 請參閱下列程式碼 hello:

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

當使用一般的.NET 字典，您可以加入索引鍵/值 toohello 字典，然後變更 hello （例如 LastLogin) 屬性值。 不過，這段程式碼和可靠的字典不會合作無間。 請記住 hello 從先前的討論，tooAddAsync 序列化 hello 索引鍵/值的 hello 呼叫物件 toobyte 陣列，並儲存 hello 陣列 tooa 本機檔案，然後傳送 toohello 次要複本。 如果您之後變更的屬性，這樣會變更; 記憶體中的 hello 屬性的值它不會影響 hello 本機檔案或傳送 toohello 複本 hello 資料。 如果 hello 處理序損毀，什麼是在記憶體中是被丟棄。 新的處理序啟動，或如果另一個複本變成主要，然後 hello 舊屬性值時可用。

我無法壓力夠是多麼的輕鬆 toomake hello 種如上所示的錯誤。 而，將只可了解 hello 錯誤時效能降低的 hello 程序。 hello 正確方式 toowrite hello 程式碼是只需 tooreverse hello 兩行：


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

這是另一個常見的錯誤︰

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

同樣地，使用標準.NET 字典時，hello 上述的程式碼會正常運作，且常見的模式： hello 開發人員會使用值的索引鍵 toolook。 如果 hello 值存在，hello 開發人員會變更屬性的值。 不過，與可靠的集合，此程式碼表現相同的問題如先前所討論的 hello:**您必須修改物件，一旦您所給 tooa 可靠的集合。**

hello 正確方式 tooupdate 可靠的集合中的值是 tooget 參考 toohello 現有值，請考慮 hello 物件參照 tooby 這個不可變的參考。 接著，建立新的物件，也就是 hello 原始物件的完全相同複本。 現在，您可以修改此新物件 hello 狀態，並寫入 hello 新物件 hello 集合，讓它取得序列化 toobyte 陣列附加的 toohello 本機檔案和傳送 toohello 複本。 認可 hello 變更 hello 記憶體中的物件，hello 本機檔案，且所有 hello 複本都有 hello 之後相同確切的狀態。 大功告成！

下列程式碼 hello 可靠的集合中，值將顯示 hello 正確方式 tooupdate:

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>定義不可變的資料型別 tooprevent 程式設計錯誤
在理想情況下，我們希望 hello 編譯器 tooreport 錯誤時您不小心產生的物件，您應該 tooconsider 不可變的狀態會改變的程式碼。 但是，hello C# 編譯器並沒有 hello 能力 toodo 這。 如此，tooavoid 潛在程式設計人員的錯誤，我們強烈建議您定義您搭配可靠集合 toobe 不可變的類型使用的 hello 型別。 具體而言，這表示您從 toocore 實值類型 （例如 [Int32、 UInt64 等] 的數字、 DateTime、 Guid、 TimeSpan 和類似的 hello）。 當然，您也可以使用字串。 它是最佳的 tooavoid 集合屬性，做為序列化和還原序列化它們可經常會降低效能。 不過，如果您想 toouse 集合屬性時，我們強烈建議使用 hello。網路的不可變的集合程式庫 ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/))。 可以從 http://nuget.org 下載這個程式庫。另外，也建議您盡可能密封類別，並將欄位變成唯讀。

hello 下方的使用者資訊類型會示範如何的不可變的 toodefine 鍵入如何利用上述建議。

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

hello ItemId 類型也是不可變的類型，如下所示：

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a>結構描述版本控制 (升級)
就內部而言，可靠的集合會使用 .NET 的 DataContractSerializer 序列化物件。 hello 序列化物件是保存的 toohello 主要複本的本機磁碟，而且也會傳輸的 toohello 次要複本。 為您的服務成熟，很可能您會想 toochange hello 種類的資料 （結構描述），您的服務要求。 您必須十二萬分地謹慎對待資料的版本控制方法。 首先和最重要，您都必須能夠 toodeserialize 舊資料。 具體而言，這表示您還原序列化程式碼必須是無限具有回溯相容性： 版本 333 的服務程式碼必須是能夠 toooperate 上放置可靠的集合中的服務程式碼第 1 版 5 年以前的資料。

而且，服務程式碼一次只能升級一個網域。 所以，在升級期間，您會同時執行兩個不同版本的服務程式碼。 您必須避免 hello 新版本的服務程式碼使用 hello 新結構描述，因為舊版的服務程式碼可能不是能 toohandle hello 新結構描述。 如果可能的話，您應該設計服務 toobe 的往後相容的每個版本 1 的版本。 具體而言，這表示 V1 的服務程式碼應該可以 toosimply 略過任何結構描述項目不會明確地處理。 不過，它必須能夠 toosave 它並不明確了解並只將它寫入任何資料更新的字典索引鍵或值時傳回。

> [!WARNING]
> 雖然您可以修改的索引鍵的 hello 結構描述，您必須確定您的金鑰雜湊程式碼和等於演算法是穩定。 如果您變更其中一種演算法的運作方式，就能 toolook hello 可靠字典中的 hello 金鑰過一次。
>
>

或者，您可以執行什麼是通常參照的 tooas 2 階段升級。 有了 2 階段升級時，您必須升級您的服務從 V1 tooV2: V2 包含 hello 知道如何 toodeal hello 新結構描述變更，但這段程式碼不會執行的程式碼。 當 hello V2 程式碼讀取 V1 資料時，它會在其上運作，並將 V1 資料。 然後，在所有的升級網域之間 hello 升級已完成之後，您可以以某種方式發出信號給 toohello 執行 V2 執行個體的 hello 升級已完成。 (其中一種方式 toosignal 這是 tooroll 組態升級時，這是為什麼會 2 階段升級。)現在，hello V2 執行個體可以讀取 V1 資料、 將它轉換 tooV2 資料、 操作，並為 V2 資料寫出。 當其他執行個體讀取 V2 資料時，不需要 tooconvert，它們只處理，並寫出 V2 資料。

## <a name="next-steps"></a>後續步驟
toolearn 需建立轉寄相容的資料合約，請參閱[向前相容資料合約](https://msdn.microsoft.com/library/ms731083.aspx)。

toolearn 最佳實務，資料合約版本控制，請參閱[資料合約版本控制](https://msdn.microsoft.com/library/ms731138.aspx)。

toolearn 如何 tooimplement 版本容錯資料合約，請參閱[版本相容序列化回呼](https://msdn.microsoft.com/library/ms733734.aspx)。

toolearn tooprovide 跨多個版本，可以交互操作的資料結構的請參閱[IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx)。
