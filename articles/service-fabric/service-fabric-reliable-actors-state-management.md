---
title: "Reliable Actors 狀態管理 | Microsoft Docs"
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
ms.openlocfilehash: aca8cf2b94e8b746a5cac6af021c7221a29b7345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="581f8-103">Reliable Actors 狀態管理</span><span class="sxs-lookup"><span data-stu-id="581f8-103">Reliable Actors state management</span></span>
<span data-ttu-id="581f8-104">Reliable Actors 是可封裝邏輯和狀態的單一執行緒物件。</span><span class="sxs-lookup"><span data-stu-id="581f8-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="581f8-105">由於動作項目會在 Reliable Services 上執行，因此，它們可以利用 Reliable Services 所使用的相同持續性和複寫機制，以可靠的方式維護狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="581f8-106">如此一來，動作項目就不會在失敗之後、在記憶體回收之後重新啟動，或者因為資源平衡和升級的緣故而在叢集中的節點之間移動時，遺失它們的狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="581f8-107">狀態持續性和複寫</span><span class="sxs-lookup"><span data-stu-id="581f8-107">State persistence and replication</span></span>
<span data-ttu-id="581f8-108">所有的 Reliable Actors 會被視為「具狀態」  ，因為每個動作項目執行個體都會對應到唯一的識別碼。</span><span class="sxs-lookup"><span data-stu-id="581f8-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="581f8-109">這表示，對同一個動作項目識別碼所進行的重複呼叫會路由傳送到同一個動作項目執行個體。</span><span class="sxs-lookup"><span data-stu-id="581f8-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="581f8-110">相較之下，在無狀態系統中，用戶端呼叫不一定每次都會路由傳送到同一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="581f8-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="581f8-111">基於這個理由，動作項目服務永遠都是具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="581f8-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="581f8-112">即使動作項目會被視為具狀態，但並不表示它們必須以可靠的方式儲存狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="581f8-113">動作項目可以根據其資料儲存體需求來選擇狀態持續性和複寫的層級︰</span><span class="sxs-lookup"><span data-stu-id="581f8-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="581f8-114">**保存的狀態︰** 狀態會保存於磁碟，並複寫至 3 個以上的複本。</span><span class="sxs-lookup"><span data-stu-id="581f8-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span></span> <span data-ttu-id="581f8-115">這是最持久的狀態儲存選項，可透過完整的叢集中斷來保存狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="581f8-116">**變動性狀態︰** 狀態會複寫至 3 個以上的複本，而且只會保存於記憶體中。</span><span class="sxs-lookup"><span data-stu-id="581f8-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="581f8-117">這可針對節點失敗和動作項目失敗，以及在升級和資源平衡期間提供恢復能力。</span><span class="sxs-lookup"><span data-stu-id="581f8-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="581f8-118">不過，狀態不會保存到磁碟。</span><span class="sxs-lookup"><span data-stu-id="581f8-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="581f8-119">因此，如果同時遺失所有複本，狀態也會遺失。</span><span class="sxs-lookup"><span data-stu-id="581f8-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="581f8-120">**沒有保存的狀態︰** 狀態不會複寫，也不會寫入磁碟。</span><span class="sxs-lookup"><span data-stu-id="581f8-120">**No persisted state**: State is not replicated or written to disk.</span></span> <span data-ttu-id="581f8-121">此層級適用於完全不需要以可靠方式維護狀態的動作項目。</span><span class="sxs-lookup"><span data-stu-id="581f8-121">This level is for actors that simply don't need to maintain state reliably.</span></span>

<span data-ttu-id="581f8-122">每個層級的持續性只是您服務的不同「狀態供應器」和「複寫」組態。</span><span class="sxs-lookup"><span data-stu-id="581f8-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="581f8-123">是否要將狀態寫入磁碟取決於「狀態供應器」(Reliable Service 中儲存狀態的元件)。</span><span class="sxs-lookup"><span data-stu-id="581f8-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="581f8-124">複寫取決於要使用多少個複本來部署服務。</span><span class="sxs-lookup"><span data-stu-id="581f8-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="581f8-125">就如同 Reliable Services，您可以輕鬆地手動設定狀態供應器和複本計數。</span><span class="sxs-lookup"><span data-stu-id="581f8-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="581f8-126">動作項目架構提供屬性，在動作項目上使用時，會自動選取預設的狀態供應器，並自動產生複本計數的設定，以達到這三個持續性設定的其中一個。</span><span class="sxs-lookup"><span data-stu-id="581f8-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span> <span data-ttu-id="581f8-127">衍生的類別不會繼承 StatePersistence 屬性，每個 Actor 類型必須提供其 StatePersistence 層級。</span><span class="sxs-lookup"><span data-stu-id="581f8-127">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="581f8-128">保存的狀態</span><span class="sxs-lookup"><span data-stu-id="581f8-128">Persisted state</span></span>
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
<span data-ttu-id="581f8-129">此設定會使用狀態供應器，在磁碟上儲存資料，並自動將服務複本計數設定為 3。</span><span class="sxs-lookup"><span data-stu-id="581f8-129">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="581f8-130">變動性狀態</span><span class="sxs-lookup"><span data-stu-id="581f8-130">Volatile state</span></span>
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
<span data-ttu-id="581f8-131">此設定會使用僅在記憶體中的狀態供應器，並將複本計數設定為 3。</span><span class="sxs-lookup"><span data-stu-id="581f8-131">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="581f8-132">沒有保存的狀態</span><span class="sxs-lookup"><span data-stu-id="581f8-132">No persisted state</span></span>
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
<span data-ttu-id="581f8-133">此設定會使用僅在記憶體中的狀態供應器，並將複本計數設定為 1。</span><span class="sxs-lookup"><span data-stu-id="581f8-133">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="581f8-134">預設值和產生的設定</span><span class="sxs-lookup"><span data-stu-id="581f8-134">Defaults and generated settings</span></span>
<span data-ttu-id="581f8-135">您使用 `StatePersistence` 屬性時，在動作項目服務啟動時，會在執行階段自動為您選取狀態供應器。</span><span class="sxs-lookup"><span data-stu-id="581f8-135">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="581f8-136">不過，複本計數是在編譯時期由 Visual Studio 動作項目建置工具所設定。</span><span class="sxs-lookup"><span data-stu-id="581f8-136">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="581f8-137">建置工具會在 ApplicationManifest.xml 中自動為動作項目服務產生「預設服務」。</span><span class="sxs-lookup"><span data-stu-id="581f8-137">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="581f8-138">參數是針對「複本集大小下限」和「目標複本集大小」建立。</span><span class="sxs-lookup"><span data-stu-id="581f8-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="581f8-139">您可以手動變更這些參數。</span><span class="sxs-lookup"><span data-stu-id="581f8-139">You can change these parameters manually.</span></span> <span data-ttu-id="581f8-140">不過，每當 `StatePersistence` 屬性變更時，參數會設定為所選 `StatePersistence` 屬性的預設複本集大小值，並覆寫所有舊值。</span><span class="sxs-lookup"><span data-stu-id="581f8-140">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="581f8-141">換句話說，您在 ServiceManifest.xml 中設定的值將*只*會在您變更 `StatePersistence` 屬性值時，於建置階段覆寫。</span><span class="sxs-lookup"><span data-stu-id="581f8-141">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="581f8-142">狀態管理員</span><span class="sxs-lookup"><span data-stu-id="581f8-142">State manager</span></span>
<span data-ttu-id="581f8-143">每個動作項目執行個體都有它自己的狀態管理員︰以可靠方式儲存金鑰-值組的字典式資料結構。</span><span class="sxs-lookup"><span data-stu-id="581f8-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="581f8-144">狀態管理員是包住狀態供應器的包裝函式。</span><span class="sxs-lookup"><span data-stu-id="581f8-144">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="581f8-145">您可以使用它來儲存的資料，不論哪一個會使用持續性設定。</span><span class="sxs-lookup"><span data-stu-id="581f8-145">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="581f8-146">它不保證執行中的動作項目服務可以透過輪流升級從變動性 (僅在記憶體中) 狀態設定變更保存的狀態設定，同時保留資料。</span><span class="sxs-lookup"><span data-stu-id="581f8-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="581f8-147">但是，針對執行中的服務變更複本計數是可行的。</span><span class="sxs-lookup"><span data-stu-id="581f8-147">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="581f8-148">狀態管理員索引鍵必須是字串。</span><span class="sxs-lookup"><span data-stu-id="581f8-148">State manager keys must be strings.</span></span> <span data-ttu-id="581f8-149">值是泛型值，而且可以是任何類型，包括自訂類型。</span><span class="sxs-lookup"><span data-stu-id="581f8-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="581f8-150">儲存在狀態管理員中的值必須是可進行資料合約序列化的，因為根據動作項目的狀態持續性設定，它們可能會在複寫期間透過網路傳輸至其他節點，而且可能會寫入磁碟。</span><span class="sxs-lookup"><span data-stu-id="581f8-150">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="581f8-151">狀態管理員會公開一般字典方法來管理狀態，類似於在可靠的字典中找到的項目。</span><span class="sxs-lookup"><span data-stu-id="581f8-151">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="581f8-152">存取狀態</span><span class="sxs-lookup"><span data-stu-id="581f8-152">Accessing state</span></span>
<span data-ttu-id="581f8-153">狀態可以透過狀態管理員依索引鍵來存取。</span><span class="sxs-lookup"><span data-stu-id="581f8-153">State can be accessed through the state manager by key.</span></span> <span data-ttu-id="581f8-154">狀態管理員方法全都是非同步的，因為當動作項目具有保存的狀態時，它們可能需要磁碟 I/O。</span><span class="sxs-lookup"><span data-stu-id="581f8-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="581f8-155">第一次存取時，會將狀態物件快取於記憶體中。</span><span class="sxs-lookup"><span data-stu-id="581f8-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="581f8-156">重複存取作業會從記憶體中直接存取物件並以同步方式傳回，而不會造成磁碟 I/O 或非同步內容切換的負擔。</span><span class="sxs-lookup"><span data-stu-id="581f8-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="581f8-157">狀態物件會在下列情況中從快取移除︰</span><span class="sxs-lookup"><span data-stu-id="581f8-157">A state object is removed from the cache in the following cases:</span></span>

* <span data-ttu-id="581f8-158">從狀態管理員中擷取物件之後，動作項目方法會擲回未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="581f8-158">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span></span>
* <span data-ttu-id="581f8-159">動作項目會在已停用之後或因為失敗而重新啟動。</span><span class="sxs-lookup"><span data-stu-id="581f8-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="581f8-160">狀態供應器會將狀態分頁到磁碟。</span><span class="sxs-lookup"><span data-stu-id="581f8-160">The state provider pages state to disk.</span></span> <span data-ttu-id="581f8-161">這個行為取決於狀態供應器實作。</span><span class="sxs-lookup"><span data-stu-id="581f8-161">This behavior depends on the state provider implementation.</span></span> <span data-ttu-id="581f8-162">`Persisted` 設定的預設狀態供應器具有這個行為。</span><span class="sxs-lookup"><span data-stu-id="581f8-162">The default state provider for the `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="581f8-163">如果索引鍵的項目不存在，您可以使用會擲回 `KeyNotFoundException`(C#) 或 `NoSuchElementException`(Java) 的標準 *Get* 作業來擷取狀態：</span><span class="sxs-lookup"><span data-stu-id="581f8-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span></span>

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

<span data-ttu-id="581f8-164">如果索引鍵的項目不存在，您也可以使用不會擲回任何項目的 *TryGet* 方法來擷取狀態：</span><span class="sxs-lookup"><span data-stu-id="581f8-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="581f8-165">儲存狀態</span><span class="sxs-lookup"><span data-stu-id="581f8-165">Saving state</span></span>
<span data-ttu-id="581f8-166">狀態管理員擷取方法會傳回本機記憶體中物件的參考。</span><span class="sxs-lookup"><span data-stu-id="581f8-166">The state manager retrieval methods return a reference to an object in local memory.</span></span> <span data-ttu-id="581f8-167">在本機記憶體中單獨修改此物件並不會永久儲存該物件。</span><span class="sxs-lookup"><span data-stu-id="581f8-167">Modifying this object in local memory alone does not cause it to be saved durably.</span></span> <span data-ttu-id="581f8-168">從狀態管理員中擷取並修改物件時，必須將它重新插入狀態管理員，才能永久儲存。</span><span class="sxs-lookup"><span data-stu-id="581f8-168">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span></span>

<span data-ttu-id="581f8-169">您可以使用無條件的 *Set* 來插入狀態，這相當於 `dictionary["key"] = value` 語法︰</span><span class="sxs-lookup"><span data-stu-id="581f8-169">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="581f8-170">您可以使用 *Add* 方法來新增狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="581f8-171">這個方法會在它新增已存在的索引鍵時擲回 `InvalidOperationException`(C#) 或 `IllegalStateException`(Java)。</span><span class="sxs-lookup"><span data-stu-id="581f8-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span></span>

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

<span data-ttu-id="581f8-172">您也可以使用 *TryAdd* 方法來新增狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="581f8-173">此方法不會在它嘗試新增已存在的索引鍵時擲回任何項目。</span><span class="sxs-lookup"><span data-stu-id="581f8-173">This method does not throw when it tries to add a key that already exists.</span></span>

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

<span data-ttu-id="581f8-174">在動作項目方法結束時，狀態管理員會自動儲存透過插入或更新作業所新增或修改的任何值。</span><span class="sxs-lookup"><span data-stu-id="581f8-174">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="581f8-175">根據所使用的設定，「儲存」可以包括保存到磁碟與複本。</span><span class="sxs-lookup"><span data-stu-id="581f8-175">A "save" can include persisting to disk and replication, depending on the settings used.</span></span> <span data-ttu-id="581f8-176">尚未經過修改的值不會保存或複寫。</span><span class="sxs-lookup"><span data-stu-id="581f8-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="581f8-177">如果未修改任何值，儲存作業就不會有任何動作。</span><span class="sxs-lookup"><span data-stu-id="581f8-177">If no values have been modified, the save operation does nothing.</span></span> <span data-ttu-id="581f8-178">如果儲存失敗，將會捨棄已修改的狀態並重新載入原始的狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-178">If saving fails, the modified state is discarded and the original state is reloaded.</span></span>

<span data-ttu-id="581f8-179">您也可以呼叫動作項目基底上的 `SaveStateAsync` 方法來手動儲存狀態︰</span><span class="sxs-lookup"><span data-stu-id="581f8-179">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="581f8-180">移除狀態</span><span class="sxs-lookup"><span data-stu-id="581f8-180">Removing state</span></span>
<span data-ttu-id="581f8-181">您可以藉由呼叫 *Remove* 方法，從動作項目的狀態管理員中永久移除狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-181">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span></span> <span data-ttu-id="581f8-182">這個方法會在它嘗試移除不存在的索引鍵時擲回 `KeyNotFoundException`(C#) 或 `NoSuchElementException`(Java)。</span><span class="sxs-lookup"><span data-stu-id="581f8-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span></span>

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

<span data-ttu-id="581f8-183">您也可以使用 *TryRemove* 方法永久移除狀態。</span><span class="sxs-lookup"><span data-stu-id="581f8-183">You can also remove state permanently by using the *TryRemove* method.</span></span> <span data-ttu-id="581f8-184">此方法不會在它嘗試移除不存在的索引鍵時擲回任何項目。</span><span class="sxs-lookup"><span data-stu-id="581f8-184">This method does not throw when it tries to remove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="581f8-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="581f8-185">Next steps</span></span>

<span data-ttu-id="581f8-186">儲存在 Reliable Actors 中的狀態必須先經過序列化，才能寫入到磁碟中並進行複寫來提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="581f8-186">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span></span> <span data-ttu-id="581f8-187">深入了解[動作項目類型序列化](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="581f8-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="581f8-188">接著，深入了解[動作項目診斷與效能監視](service-fabric-reliable-actors-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="581f8-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
