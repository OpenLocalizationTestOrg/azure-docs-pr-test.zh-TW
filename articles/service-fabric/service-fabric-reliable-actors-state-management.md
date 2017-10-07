---
title: "狀態管理則 aaaReliable 執行者 |Microsoft 文件"
description: "說明如何管理、保存及且複寫 Reliable Actors 狀態以提供高可用性。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a>Reliable Actors 狀態管理
Reliable Actors 是可封裝邏輯和狀態的單一執行緒物件。 可靠的服務上，執行動作項目，因為它們可以維護狀態可靠地使用 hello 可靠的服務使用的相同持續性和複寫機制。 如此一來，在重新啟動之後記憶體回收，或它們到期 tooresource 平衡或升級叢集中的節點之間移動時失敗之後, 使用執行者不會喪失其狀態。

## <a name="state-persistence-and-replication"></a>狀態持續性和複寫
會被視為所有 Reliable Actors*可設定狀態*因為每個動作項目執行個體對應 tooa 的唯一識別碼。 這表示相同的動作項目識別碼都是該重複的呼叫 toohello 路由 toohello 相同的動作項目執行個體。 在無狀態的系統中，相較之下，用戶端呼叫並不保證 toobe 路由 toohello 每次相同的伺服器。 基於這個理由，動作項目服務永遠都是具狀態服務。

即使動作項目會被視為具狀態，但並不表示它們必須以可靠的方式儲存狀態。 執行者可以選擇 hello 層級的狀態持續性，而且複寫根據其資料儲存體需求：

* **將狀態保存**： 狀態已保存的 toodisk 和複寫的 too3 或多個複本。 這是 hello 最持久狀態儲存選項，可以透過完整的叢集中斷將保存狀態。
* **變動性狀態**： 會複寫的 too3 或多個複本，而只保留在記憶體中狀態。 這可針對節點失敗和動作項目失敗，以及在升級和資源平衡期間提供恢復能力。 不過，狀態不是保存的 toodisk。 因此如果所有複本都都遺失了一次，hello 狀態也會是遺失。
* **沒有保存的狀態**： 未複寫或寫入 toodisk 狀態。 這個層級是針對只能夠可靠地不需要 toomaintain 狀態的動作項目。

每個層級的持續性只是您服務的不同「狀態供應器」和「複寫」組態。 不論是否狀態寫入 toodisk 取決於 hello 狀態提供者--在可靠的服務，儲存狀態中的 hello 元件。 複寫取決於要使用多少個複本來部署服務。 如同可靠的服務，同時 hello 狀態提供者，可以輕鬆地手動設定複本計數。 hello 執行者 framework 會提供屬性，當使用動作項目，會自動選取 預設狀態提供者，並且會自動產生複本計數 tooachieve 其中一個三個持續性設定的設定。 在衍生類別不繼承 hello StatePersistence 屬性時，每個動作項目類型必須提供其 StatePersistence 層級。

### <a name="persisted-state"></a>保存的狀態
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
這項設定使用磁碟上儲存資料，並自動設定 hello 服務複本計數 too3 狀態提供者。

### <a name="volatile-state"></a>變動性狀態
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
這項設定使用中記憶體-僅限狀態提供者，並設定 hello 複本計數 too3。

### <a name="no-persisted-state"></a>沒有保存的狀態
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
這項設定使用中記憶體-僅限狀態提供者，並設定 hello 複本計數 too1。

### <a name="defaults-and-generated-settings"></a>預設值和產生的設定
當您使用 hello`StatePersistence`狀態提供者的屬性，會自動為您選擇在執行階段 hello actor 服務啟動時。 hello 複本計數，不過，設定在編譯時期 hello Visual Studio 動作項目所建置工具。 hello 建置工具自動產生*預設服務*ApplicationManifest.xml 中的 hello 動作項目服務。 參數是針對「複本集大小下限」和「目標複本集大小」建立。

您可以手動變更這些參數。 但每個時間 hello`StatePersistence`屬性變更，hello 參數會設定 toohello 複本集大小的預設值選取 hello`StatePersistence`屬性，覆寫任何先前的值。 換句話說，hello ServiceManifest.xml 中設定有效值*只*覆寫在建置階段，當您變更 hello`StatePersistence`屬性值。

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a>狀態管理員
每個動作項目執行個體都有它自己的狀態管理員︰以可靠方式儲存金鑰-值組的字典式資料結構。 hello 狀態管理員是狀態提供者的包裝函式。 您可以使用它 toostore 資料不論使用哪一個持續性設定。 它不提供任何保證的變動性 （在記憶體-僅限） 的狀態設定 tooa，可以變更執行的動作項目服務保存透過輪流升級時保留資料的 [狀態] 設定。 不過，它是執行中的服務可能 toochange 複寫計數。

狀態管理員索引鍵必須是字串。 值是泛型值，而且可以是任何類型，包括自訂類型。 儲存在 hello 狀態管理員中的值必須是可序列化的資料合約，因為它們可能會在複寫期間傳輸 hello 網路 tooother 節點上，且可能被寫入 toodisk，根據動作項目的狀態持續性設定。

hello 狀態管理員公開一般字典方法管理狀態，類似 toothose 可靠的字典中找到。

### <a name="accessing-state"></a>存取狀態
依索引鍵，可以透過 hello 狀態管理員存取狀態。 狀態管理員方法全都是非同步的，因為當動作項目具有保存的狀態時，它們可能需要磁碟 I/O。 第一次存取時，會將狀態物件快取於記憶體中。 重複存取作業會從記憶體中直接存取物件並以同步方式傳回，而不會造成磁碟 I/O 或非同步內容切換的負擔。 狀態物件會移除從 hello 快取，在下列情況下的 hello:

* 動作項目方法會擲回未處理的例外狀況之後擷取 hello 狀態管理員物件。
* 動作項目會在已停用之後或因為失敗而重新啟動。
* hello 狀態提供者頁面狀態 toodisk。 這個行為取決於 hello 狀態提供者實作。 hello 的 hello 預設狀態提供者`Persisted`設定具有這個行為。

您可以擷取狀態，透過標準*取得*作業會擲回`KeyNotFoundException`(C#) 或`NoSuchElementException`(Java) 如果項目不存在 hello 機碼：

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

如果索引鍵的項目不存在，您也可以使用不會擲回任何項目的 *TryGet* 方法來擷取狀態：

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a>儲存狀態
hello 狀態管理員擷取方法會傳回參考 tooan 物件，在本機記憶體。 修改此單獨的本機記憶體中的物件不會造成它 toobe 長期儲存。 物件是從 hello 狀態管理員擷取和修改時間，它必須插入 hello 狀態管理員 toobe 長期儲存。

您可以使用無條件插入狀態*設定*，這是 hello hello 的對等`dictionary["key"] = value`語法：

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

您可以使用 *Add* 方法來新增狀態。 這個方法會擲回`InvalidOperationException`(C#) 或`IllegalStateException`(Java) 嘗試 tooadd 已經存在的索引鍵時。

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

您也可以使用 *TryAdd* 方法來新增狀態。 這個方法不會嘗試 tooadd 已經存在的索引鍵時擲回。

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

在 hello 動作項目方法結尾，hello 狀態管理員會自動儲存任何已加入或修改所插入或更新作業的值。 保存 toodisk 和複寫，視使用的 hello 設定而定，可以包含 [儲存]。 尚未經過修改的值不會保存或複寫。 如果沒有任何值已經被修改，hello 儲存作業任何作用。 若要儲存失敗，hello 修改過的狀態會捨棄並重新載入 hello 原始狀態。

您也可以儲存狀態以手動方式呼叫 hello`SaveStateAsync`上 hello 動作項目基底的方法：

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a>移除狀態
您可以將狀態永久從動作項目的狀態管理員呼叫 hello*移除*方法。 這個方法會擲回`KeyNotFoundException`(C#) 或`NoSuchElementException`(Java) 嘗試 tooremove 不存在的索引鍵時。

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

您也可以移除狀態永久使用 hello *TryRemove*方法。 這個方法不會嘗試 tooremove 不存在的索引鍵時擲回。

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a>後續步驟

必須序列化其寫入 toodisk 之前和複寫的高可用性儲存在 Reliable Actors 的狀態。 深入了解[動作項目類型序列化](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)。

接著，深入了解[動作項目診斷與效能監視](service-fabric-reliable-actors-diagnostics.md)。
