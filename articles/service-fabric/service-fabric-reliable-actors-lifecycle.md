---
title: "動作項目為基礎的 Azure microservices 生命週期的 aaaOverview |Microsoft 文件"
description: "說明 Service Fabric Reliable Actor 生命週期、記憶體回收，以及手動刪除動作項目與其狀態"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="40cfc-103">動作項目生命週期、自動記憶體回收，以及手動刪除</span><span class="sxs-lookup"><span data-stu-id="40cfc-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="40cfc-104">啟動動作項目 hello tooany 其方法進行呼叫的第一次。</span><span class="sxs-lookup"><span data-stu-id="40cfc-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="40cfc-105">動作項目是已停用 （記憶體回收 hello 執行者執行階段所收集），如果它不是可設定的一段時間。</span><span class="sxs-lookup"><span data-stu-id="40cfc-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="40cfc-106">動作項目與其狀態也可以隨時進行手動刪除。</span><span class="sxs-lookup"><span data-stu-id="40cfc-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="40cfc-107">啟用動作項目</span><span class="sxs-lookup"><span data-stu-id="40cfc-107">Actor activation</span></span>
<span data-ttu-id="40cfc-108">啟動動作項目時，hello 會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="40cfc-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="40cfc-109">當動作項目有呼叫卻尚未為使用中時，會建立新的動作項目。</span><span class="sxs-lookup"><span data-stu-id="40cfc-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="40cfc-110">如果維護狀態，已載入 hello 動作項目的狀態。</span><span class="sxs-lookup"><span data-stu-id="40cfc-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="40cfc-111">hello `OnActivateAsync` (C#) 或`onActivateAsync`(Java) （這會覆寫在 hello 動作項目實作） 會呼叫。</span><span class="sxs-lookup"><span data-stu-id="40cfc-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="40cfc-112">hello 動作項目會視為使用中。</span><span class="sxs-lookup"><span data-stu-id="40cfc-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="40cfc-113">停用動作項目</span><span class="sxs-lookup"><span data-stu-id="40cfc-113">Actor deactivation</span></span>
<span data-ttu-id="40cfc-114">當停用動作項目時，hello 會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="40cfc-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="40cfc-115">當動作項目不是一段時間時，它會從 hello 作用中的動作項目資料表中移除。</span><span class="sxs-lookup"><span data-stu-id="40cfc-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="40cfc-116">hello `OnDeactivateAsync` (C#) 或`onDeactivateAsync`(Java) （這會覆寫在 hello 動作項目實作） 會呼叫。</span><span class="sxs-lookup"><span data-stu-id="40cfc-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="40cfc-117">這會清除所有 hello 計時器 hello 動作項目。</span><span class="sxs-lookup"><span data-stu-id="40cfc-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="40cfc-118">您不應該從此方法呼叫動作項目作業 (例如狀態變更)。</span><span class="sxs-lookup"><span data-stu-id="40cfc-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="40cfc-119">hello Fabric 動作項目執行階段發出某些[tooactor 啟用和停用相關事件](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters)。</span><span class="sxs-lookup"><span data-stu-id="40cfc-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="40cfc-120">這些項目對於診斷與效能監視很有幫助。</span><span class="sxs-lookup"><span data-stu-id="40cfc-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="40cfc-121">動作項目記憶體回收</span><span class="sxs-lookup"><span data-stu-id="40cfc-121">Actor garbage collection</span></span>
<span data-ttu-id="40cfc-122">動作項目已停用時，釋放參考 toohello 動作項目物件，它可以進行記憶體回收通常由 hello common language runtime (CLR) 或 java 虛擬機器 (JVM) 記憶體回收行程。</span><span class="sxs-lookup"><span data-stu-id="40cfc-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="40cfc-123">廢棄項目收集只清除 hello 動作項目物件。它會**不**移除儲存在 hello 執行者狀態管理員的狀態。</span><span class="sxs-lookup"><span data-stu-id="40cfc-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="40cfc-124">hello 下一個時間 hello 執行者啟動、 建立新的動作項目物件，並還原其狀態。</span><span class="sxs-lookup"><span data-stu-id="40cfc-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="40cfc-125">哪些算是"的使用 的 hello 目的是要停用和記憶體回收？</span><span class="sxs-lookup"><span data-stu-id="40cfc-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="40cfc-126">一直收到呼叫</span><span class="sxs-lookup"><span data-stu-id="40cfc-126">Receiving a call</span></span>
* <span data-ttu-id="40cfc-127">`IRemindable.ReceiveReminderAsync`所叫用 （僅適用於 hello 動作項目使用提醒） 方法</span><span class="sxs-lookup"><span data-stu-id="40cfc-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="40cfc-128">如果 hello 動作項目使用計時器，並叫用其計時器回呼，它會**不**計數，表示 「 正在使用 」。</span><span class="sxs-lookup"><span data-stu-id="40cfc-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="40cfc-129">我們進入停用的 hello 詳細資料之前，它會是重要 toodefine hello 下列條款：</span><span class="sxs-lookup"><span data-stu-id="40cfc-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="40cfc-130">*掃描間隔*。</span><span class="sxs-lookup"><span data-stu-id="40cfc-130">*Scan interval*.</span></span> <span data-ttu-id="40cfc-131">這是在哪一個 hello 執行者執行階段會掃描其作用中的動作項目資料表可以停用的執行者 hello 間隔和記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="40cfc-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="40cfc-132">這個 hello 預設值為 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="40cfc-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="40cfc-133">*閒置逾時*。</span><span class="sxs-lookup"><span data-stu-id="40cfc-133">*Idle timeout*.</span></span> <span data-ttu-id="40cfc-134">這是 hello 動作項目需要 tooremain 上未使用的時間量 （閒置） 之前可以停用和記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="40cfc-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="40cfc-135">這個 hello 預設值是 60 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="40cfc-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="40cfc-136">一般而言，您不需要 toochange 這些預設值。</span><span class="sxs-lookup"><span data-stu-id="40cfc-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="40cfc-137">不過，如有必要，可以在註冊[動作項目服務](service-fabric-reliable-actors-platform.md)時透過 `ActorServiceSettings` 變更這些間隔：</span><span class="sxs-lookup"><span data-stu-id="40cfc-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
<span data-ttu-id="40cfc-138">針對每個作用中動作項目 hello 動作項目執行階段會追蹤的 hello 已閒置 （也就是未使用） 的時間量。</span><span class="sxs-lookup"><span data-stu-id="40cfc-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="40cfc-139">hello 動作項目執行階段會檢查每個 hello 執行者的每個`ScanIntervalInSeconds`toosee 如果記憶體回收可以收集並收集它，如果已閒置`IdleTimeoutInSeconds`。</span><span class="sxs-lookup"><span data-stu-id="40cfc-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="40cfc-140">使用動作項目時，每當它閒置的時間是重設 too0。</span><span class="sxs-lookup"><span data-stu-id="40cfc-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="40cfc-141">在此之後，hello 動作項目進行記憶體回收才再次持續閒置的`IdleTimeoutInSeconds`。</span><span class="sxs-lookup"><span data-stu-id="40cfc-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="40cfc-142">恢復動作項目會被視為 toohave 已使用如果執行者介面方法或執行者提醒回呼在執行。</span><span class="sxs-lookup"><span data-stu-id="40cfc-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="40cfc-143">執行者是**不**toohave 會被視為已執行其計時器回呼時使用。</span><span class="sxs-lookup"><span data-stu-id="40cfc-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="40cfc-144">hello 下列圖表顯示 hello 生命週期的單一動作項目 tooillustrate 這些概念。</span><span class="sxs-lookup"><span data-stu-id="40cfc-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![閒置時間的範例][1]

<span data-ttu-id="40cfc-146">hello 範例會顯示 hello 這個動作項目存留期上的動作項目方法呼叫，備忘提醒和計時器的 hello 影響。</span><span class="sxs-lookup"><span data-stu-id="40cfc-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="40cfc-147">hello 遵循有關 hello 範例的重點是值得一提的是：</span><span class="sxs-lookup"><span data-stu-id="40cfc-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="40cfc-148">ScanInterval 和 IdleTimeout too5 和 10 分別設定。</span><span class="sxs-lookup"><span data-stu-id="40cfc-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="40cfc-149">（單位不重要，因為我們的目的在於 tooillustrate hello 概念。）</span><span class="sxs-lookup"><span data-stu-id="40cfc-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="40cfc-150">執行者所定義的 hello 掃描間隔為 5 toobe 記憶體回收會發生在 T = 0，5、 10、 15、 20、 25 的 hello 掃描。</span><span class="sxs-lookup"><span data-stu-id="40cfc-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="40cfc-151">定期計時器會在 T=4、8、12、16、20、24 時引發，並執行其回呼。</span><span class="sxs-lookup"><span data-stu-id="40cfc-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="40cfc-152">它不會影響 hello 執行者的 hello 閒置時間。</span><span class="sxs-lookup"><span data-stu-id="40cfc-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="40cfc-153">在 T = 7 的執行者方法呼叫 hello 閒置時間 too0 會重設，而延遲 hello hello 執行者的記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="40cfc-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="40cfc-154">T = 14 在執行的動作項目提醒回撥，進一步延遲 hello hello 執行者的記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="40cfc-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="40cfc-155">Hello 的記憶體回收掃描在 T = 25，期間 hello 執行者的閒置時間最後超過 hello 閒置逾時為 10，而且 hello 執行者記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="40cfc-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="40cfc-156">動作項目正在執行其中一個方法時，無論在執行該方法時花費了多久的時間，動作項目絕對不會進行記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="40cfc-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="40cfc-157">如先前所述，動作項目介面方法和提醒回呼的 hello 執行以防止記憶體回收 hello 執行者的閒置時間 too0 重設。</span><span class="sxs-lookup"><span data-stu-id="40cfc-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="40cfc-158">hello 執行計時器回呼不重設 hello 閒置時間 too0。</span><span class="sxs-lookup"><span data-stu-id="40cfc-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="40cfc-159">不過，hello 執行者的 hello 回收被延遲至 hello 計時器回呼已完成執行為止。</span><span class="sxs-lookup"><span data-stu-id="40cfc-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="40cfc-160">刪除動作項目與其狀態</span><span class="sxs-lookup"><span data-stu-id="40cfc-160">Deleting actors and their state</span></span>
<span data-ttu-id="40cfc-161">記憶體回收的已停用動作項目只會清除 hello 動作項目物件，但不會移除儲存動作項目的狀態管理員中的資料。</span><span class="sxs-lookup"><span data-stu-id="40cfc-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="40cfc-162">重新啟動動作項目時，其資料再次變成可用 tooit 透過 hello 狀態管理員。</span><span class="sxs-lookup"><span data-stu-id="40cfc-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="40cfc-163">在其中執行者將資料儲存在狀態管理員和停用，但是永遠不會重新啟動的情況下，可能需要 tooclean 其資料。</span><span class="sxs-lookup"><span data-stu-id="40cfc-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="40cfc-164">hello [Actor 服務](service-fabric-reliable-actors-platform.md)提供函式用於從遠端呼叫端刪除動作項目：</span><span class="sxs-lookup"><span data-stu-id="40cfc-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="40cfc-165">刪除動作項目具有下列效果根據 hello 動作項目在目前作用中的 hello:</span><span class="sxs-lookup"><span data-stu-id="40cfc-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="40cfc-166">**作用中動作項目**</span><span class="sxs-lookup"><span data-stu-id="40cfc-166">**Active Actor**</span></span>
  * <span data-ttu-id="40cfc-167">動作項目會從作用中動作項目清單中移除並且停用。</span><span class="sxs-lookup"><span data-stu-id="40cfc-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="40cfc-168">其狀態會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="40cfc-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="40cfc-169">**非作用中動作項目**</span><span class="sxs-lookup"><span data-stu-id="40cfc-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="40cfc-170">其狀態會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="40cfc-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="40cfc-171">請注意，呼叫動作項目無法刪除本身的其中一個動作項目方法，因為 hello 動作項目無法刪除執行中的 hello 執行階段已取得鎖定 hello 動作項目呼叫 tooenforce 單一執行緒的存取動作項目呼叫內容中時。</span><span class="sxs-lookup"><span data-stu-id="40cfc-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40cfc-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="40cfc-172">Next steps</span></span>
* [<span data-ttu-id="40cfc-173">動作項目計時器和提醒</span><span class="sxs-lookup"><span data-stu-id="40cfc-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="40cfc-174">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="40cfc-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="40cfc-175">動作項目重新進入</span><span class="sxs-lookup"><span data-stu-id="40cfc-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="40cfc-176">動作項目診斷與效能監視</span><span class="sxs-lookup"><span data-stu-id="40cfc-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="40cfc-177">動作項目 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="40cfc-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="40cfc-178">C# 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="40cfc-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="40cfc-179">Java 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="40cfc-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
