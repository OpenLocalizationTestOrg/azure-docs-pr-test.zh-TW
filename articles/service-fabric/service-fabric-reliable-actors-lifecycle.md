---
title: "動作項目型 Azure 微服務生命週期概觀 | Microsoft Docs"
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
ms.openlocfilehash: 75b7b77a0bef2051599a4f61183109cfb2ffff3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="c346a-103">動作項目生命週期、自動記憶體回收，以及手動刪除</span><span class="sxs-lookup"><span data-stu-id="c346a-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="c346a-104">第一次呼叫動作項目的方法時就會啟動動作項目。</span><span class="sxs-lookup"><span data-stu-id="c346a-104">An actor is activated the first time a call is made to any of its methods.</span></span> <span data-ttu-id="c346a-105">如果有一段可設定的時間未使用動作項目，動作項目就會停用 (由動作項目執行階段進行記憶體回收)。</span><span class="sxs-lookup"><span data-stu-id="c346a-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="c346a-106">動作項目與其狀態也可以隨時進行手動刪除。</span><span class="sxs-lookup"><span data-stu-id="c346a-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="c346a-107">啟用動作項目</span><span class="sxs-lookup"><span data-stu-id="c346a-107">Actor activation</span></span>
<span data-ttu-id="c346a-108">啟用動作項目後，會發生下列情況︰</span><span class="sxs-lookup"><span data-stu-id="c346a-108">When an actor is activated, the following occurs:</span></span>

* <span data-ttu-id="c346a-109">當動作項目有呼叫卻尚未為使用中時，會建立新的動作項目。</span><span class="sxs-lookup"><span data-stu-id="c346a-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="c346a-110">載入動作項目狀態 (如果正在維護狀態)</span><span class="sxs-lookup"><span data-stu-id="c346a-110">The actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="c346a-111">會呼叫 `OnActivateAsync` (C#) 或 `onActivateAsync` (Java) 方法 (可在動作項目實作中被覆寫)。</span><span class="sxs-lookup"><span data-stu-id="c346a-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span>
* <span data-ttu-id="c346a-112">動作項目現在被視為作用中。</span><span class="sxs-lookup"><span data-stu-id="c346a-112">The actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="c346a-113">停用動作項目</span><span class="sxs-lookup"><span data-stu-id="c346a-113">Actor deactivation</span></span>
<span data-ttu-id="c346a-114">停用動作項目後，會發生下列情況︰</span><span class="sxs-lookup"><span data-stu-id="c346a-114">When an actor is deactivated, the following occurs:</span></span>

* <span data-ttu-id="c346a-115">動作項目若一段時間未使用，便會從使用中動作項目資料表移除。</span><span class="sxs-lookup"><span data-stu-id="c346a-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span></span>
* <span data-ttu-id="c346a-116">會呼叫 `OnDeactivateAsync` (C#) 或 `onDeactivateAsync` (Java) 方法 (可在動作項目實作中被覆寫)。</span><span class="sxs-lookup"><span data-stu-id="c346a-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span> <span data-ttu-id="c346a-117">這會清除動作項目的所有計時器。</span><span class="sxs-lookup"><span data-stu-id="c346a-117">This clears all the timers for the actor.</span></span> <span data-ttu-id="c346a-118">您不應該從此方法呼叫動作項目作業 (例如狀態變更)。</span><span class="sxs-lookup"><span data-stu-id="c346a-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="c346a-119">網狀架構動作項目的執行階段會發出某些[與動作項目啟用和停用相關的事件](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters)。</span><span class="sxs-lookup"><span data-stu-id="c346a-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="c346a-120">這些項目對於診斷與效能監視很有幫助。</span><span class="sxs-lookup"><span data-stu-id="c346a-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="c346a-121">動作項目記憶體回收</span><span class="sxs-lookup"><span data-stu-id="c346a-121">Actor garbage collection</span></span>
<span data-ttu-id="c346a-122">停用動作項目後，動作項目物件的參考會釋出，而且通常可由 Common Language Runtime (CLR) 或 Java 虛擬機器 (JVM) 記憶體回收行程進行記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="c346a-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="c346a-123">記憶體回收只會清除動作項目物件；它 **不會** 移除動作項目的狀態管理員中儲存的狀態。</span><span class="sxs-lookup"><span data-stu-id="c346a-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span></span> <span data-ttu-id="c346a-124">下次啟用動作項目時，會建立新的動作項目物件並還原其狀態。</span><span class="sxs-lookup"><span data-stu-id="c346a-124">The next time the actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="c346a-125">就停用和記憶體回收的用途而言，什麼算是「一直在使用中」？</span><span class="sxs-lookup"><span data-stu-id="c346a-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="c346a-126">一直收到呼叫</span><span class="sxs-lookup"><span data-stu-id="c346a-126">Receiving a call</span></span>
* <span data-ttu-id="c346a-127">`IRemindable.ReceiveReminderAsync` 方法 (僅適用於動作項目使用提醒時)。</span><span class="sxs-lookup"><span data-stu-id="c346a-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="c346a-128">如果動作項目使用計時器，且已叫用其計時器回撥，則 **不** 算是「一直使用中」。</span><span class="sxs-lookup"><span data-stu-id="c346a-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="c346a-129">在進入停用的細節前，最重要的是定義下列詞彙：</span><span class="sxs-lookup"><span data-stu-id="c346a-129">Before we go into the details of deactivation, it is important to define the following terms:</span></span>

* <span data-ttu-id="c346a-130">*掃描間隔*。</span><span class="sxs-lookup"><span data-stu-id="c346a-130">*Scan interval*.</span></span> <span data-ttu-id="c346a-131">這是動作項目執行階段掃描其作用中動作項目資料表中，是否有動作項目可予以停用和進行記憶體回收的間隔。</span><span class="sxs-lookup"><span data-stu-id="c346a-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="c346a-132">預設值為 1 分鐘。</span><span class="sxs-lookup"><span data-stu-id="c346a-132">The default value for this is 1 minute.</span></span>
* <span data-ttu-id="c346a-133">*閒置逾時*。</span><span class="sxs-lookup"><span data-stu-id="c346a-133">*Idle timeout*.</span></span> <span data-ttu-id="c346a-134">這是動作項目維持未使用 (閒置) 所需的時間長度，過此時間後即可停用和進行記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="c346a-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="c346a-135">預設值為 60 分鐘。</span><span class="sxs-lookup"><span data-stu-id="c346a-135">The default value for this is 60 minutes.</span></span>

<span data-ttu-id="c346a-136">通常不需要變更這些預設值。</span><span class="sxs-lookup"><span data-stu-id="c346a-136">Typically, you do not need to change these defaults.</span></span> <span data-ttu-id="c346a-137">不過，如有必要，可以在註冊[動作項目服務](service-fabric-reliable-actors-platform.md)時透過 `ActorServiceSettings` 變更這些間隔：</span><span class="sxs-lookup"><span data-stu-id="c346a-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

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
<span data-ttu-id="c346a-138">對於每個作用中動作項目，動作項目執行階段會持續追蹤動作項目已閒置 (亦即未使用) 的時間。</span><span class="sxs-lookup"><span data-stu-id="c346a-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="c346a-139">動作項目執行階段每隔 `ScanIntervalInSeconds` 就會檢查每個動作項目，查看其是否可進行記憶體回收，如果已閒置 `IdleTimeoutInSeconds`，就會將其回收。</span><span class="sxs-lookup"><span data-stu-id="c346a-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="c346a-140">只要使用動作項目，其閒置時間就會重設為 0。</span><span class="sxs-lookup"><span data-stu-id="c346a-140">Anytime an actor is used, its idle time is reset to 0.</span></span> <span data-ttu-id="c346a-141">在此之後，只有當動作項目再次閒置達 `IdleTimeoutInSeconds`時，才會將動作項目作為記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="c346a-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="c346a-142">請回想一下，當動作項目介面方法或動作項目提醒回撥執行時，動作項目會視為已使用。</span><span class="sxs-lookup"><span data-stu-id="c346a-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="c346a-143">如果動作項目的計時器回撥執行時， **不會** 將動作項目視為已使用。</span><span class="sxs-lookup"><span data-stu-id="c346a-143">An actor is **not** considered to have been used if its timer callback is executed.</span></span>

<span data-ttu-id="c346a-144">下圖顯示單一動作項目的生命週期來說明下列概念。</span><span class="sxs-lookup"><span data-stu-id="c346a-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span></span>

![閒置時間的範例][1]

<span data-ttu-id="c346a-146">範例將說明動作項目方法呼叫、提醒，以及此動作項目存留期之計時器的影響。</span><span class="sxs-lookup"><span data-stu-id="c346a-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span></span> <span data-ttu-id="c346a-147">範例中有幾下幾點值得注意：</span><span class="sxs-lookup"><span data-stu-id="c346a-147">The following points about the example are worth mentioning:</span></span>

* <span data-ttu-id="c346a-148">ScanInterval 及 IdleTimeout 分別設為 5 和 10。</span><span class="sxs-lookup"><span data-stu-id="c346a-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span></span> <span data-ttu-id="c346a-149">(單位並不重要，因為我們的目的只為了說明概念)。</span><span class="sxs-lookup"><span data-stu-id="c346a-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span></span>
* <span data-ttu-id="c346a-150">系統會依照掃描間隔為 5 的定義，在 T=0、5、10、15、20、25 時掃描是否有可作為記憶體回收的動作項目。</span><span class="sxs-lookup"><span data-stu-id="c346a-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span></span>
* <span data-ttu-id="c346a-151">定期計時器會在 T=4、8、12、16、20、24 時引發，並執行其回呼。</span><span class="sxs-lookup"><span data-stu-id="c346a-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="c346a-152">這不會影響動作項目的閒置時間。</span><span class="sxs-lookup"><span data-stu-id="c346a-152">It does not impact the idle time of the actor.</span></span>
* <span data-ttu-id="c346a-153">在 T=7 的動作項目方法呼叫會將閒置時間重設為 0，並延遲動作項目的記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="c346a-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="c346a-154">動作項目提醒回撥會在 T=14 執行，並進一步延遲動作項目的廢棄項目收集。</span><span class="sxs-lookup"><span data-stu-id="c346a-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="c346a-155">在 T=25 的記憶體回收期間，動作項目的閒置時間最後會超過為 10 的閒置逾時，並會將動作項目作為記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="c346a-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span></span>

<span data-ttu-id="c346a-156">動作項目正在執行其中一個方法時，無論在執行該方法時花費了多久的時間，動作項目絕對不會進行記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="c346a-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="c346a-157">如先前所述，執行動作項目介面方法和提醒回撥會將動作項目的閒置時間重設為 0，來防止廢棄項目收集。</span><span class="sxs-lookup"><span data-stu-id="c346a-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span></span> <span data-ttu-id="c346a-158">執行計時器回撥不會將閒置時間重設為 0。</span><span class="sxs-lookup"><span data-stu-id="c346a-158">The execution of timer callbacks does not reset the idle time to 0.</span></span> <span data-ttu-id="c346a-159">不過，計時器回撥完成執行之前，會延遲動作項目的廢棄項目收集。</span><span class="sxs-lookup"><span data-stu-id="c346a-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="c346a-160">刪除動作項目與其狀態</span><span class="sxs-lookup"><span data-stu-id="c346a-160">Deleting actors and their state</span></span>
<span data-ttu-id="c346a-161">已停用動作項目的記憶體回收只會清除動作項目物件；但不會移除動作項目的狀態管理員中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="c346a-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="c346a-162">重新啟用動作項目後，會再次透過狀態管理員提供其資料。</span><span class="sxs-lookup"><span data-stu-id="c346a-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span></span> <span data-ttu-id="c346a-163">在動作項目將資料儲存於狀態管理員後停用，而永遠不會重新啟用的情況下，可能需要清除其資料。</span><span class="sxs-lookup"><span data-stu-id="c346a-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span></span>

<span data-ttu-id="c346a-164">[動作項目服務](service-fabric-reliable-actors-platform.md) 提供了從遠端呼叫端刪除動作項目的函式︰</span><span class="sxs-lookup"><span data-stu-id="c346a-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

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

<span data-ttu-id="c346a-165">根據動作項目目前是否作用中而定，刪除動作項目具有下列效果︰</span><span class="sxs-lookup"><span data-stu-id="c346a-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span></span>

* <span data-ttu-id="c346a-166">**作用中動作項目**</span><span class="sxs-lookup"><span data-stu-id="c346a-166">**Active Actor**</span></span>
  * <span data-ttu-id="c346a-167">動作項目會從作用中動作項目清單中移除並且停用。</span><span class="sxs-lookup"><span data-stu-id="c346a-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="c346a-168">其狀態會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="c346a-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="c346a-169">**非作用中動作項目**</span><span class="sxs-lookup"><span data-stu-id="c346a-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="c346a-170">其狀態會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="c346a-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="c346a-171">請注意，動作項目無法從其中一個動作項目方法呼叫刪除本身，因為在動作項目呼叫內容中執行動作項目時無法刪除該動作項目，而執行階段已取得動作項目呼叫的鎖定以強制執行單一執行緒存取。</span><span class="sxs-lookup"><span data-stu-id="c346a-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c346a-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c346a-172">Next steps</span></span>
* [<span data-ttu-id="c346a-173">動作項目計時器和提醒</span><span class="sxs-lookup"><span data-stu-id="c346a-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="c346a-174">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="c346a-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="c346a-175">動作項目重新進入</span><span class="sxs-lookup"><span data-stu-id="c346a-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="c346a-176">動作項目診斷與效能監視</span><span class="sxs-lookup"><span data-stu-id="c346a-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="c346a-177">動作項目 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="c346a-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="c346a-178">C# 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="c346a-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="c346a-179">Java 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="c346a-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
