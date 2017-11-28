---
title: "aaaReliable 執行者計時器和提醒 |Microsoft 文件"
description: "簡介 tootimers 和服務網狀架構 Reliable Actors 的備忘提醒。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="e2c0d-103">動作項目計時器和提醒</span><span class="sxs-lookup"><span data-stu-id="e2c0d-103">Actor timers and reminders</span></span>
<span data-ttu-id="e2c0d-104">動作項目可藉由註冊計時器或提醒來排程本身的週期性工作。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="e2c0d-105">本文將說明如何 toouse 計時器和提醒，並說明 hello 兩者之間的差異。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="e2c0d-106">動作項目計時器</span><span class="sxs-lookup"><span data-stu-id="e2c0d-106">Actor timers</span></span>
<span data-ttu-id="e2c0d-107">執行者計時器提供的簡單包裝函式的.NET 或 Java 計時器 tooensure hello 回呼方法會採用 hello 的執行者執行階段提供的 hello 開啟並行保證。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="e2c0d-108">執行者可以使用 hello `RegisterTimer`(C#) 或`registerTimer`(Java) 和`UnregisterTimer`(C#) 或`unregisterTimer`(Java) 方法在其基底類別 tooregister 和取消註冊計時器。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="e2c0d-109">下列的 hello 範例顯示 hello 計時器應用程式開發介面使用。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="e2c0d-110">hello 應用程式開發介面是非常類似 toohello.NET timer 或 Java 計時器。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="e2c0d-111">在此範例中，當 hello 計時器的到期 hello 執行者執行階段會呼叫 hello `MoveObject`(C#) 或`moveObject`(Java) 方法。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="e2c0d-112">hello 方法保證 toorespect hello 開啟基礎並行存取。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="e2c0d-113">這表示沒有其他動作項目方法或計時器/提醒回呼將在進行中，直到此回呼完成執行為止。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="e2c0d-114">hello hello 計時器的下一個週期開始之後 hello 回呼已完成執行。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="e2c0d-115">這表示該 hello 計時器時 hello 回呼正在執行，並已啟動 hello 回呼完成時停止。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="e2c0d-116">hello 執行者執行階段將變更儲存動作項目 toohello 狀態管理員 hello 回呼完成時。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="e2c0d-117">如果儲存 hello 狀態時，發生錯誤，將會停用該動作項目物件，並將啟用的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="e2c0d-118">Hello 動作項目停用記憶體回收的一部分時，會停止所有的計時器。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="e2c0d-119">而在此之後不會叫用任何計時器回呼。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="e2c0d-120">此外，hello 執行者執行階段不會保留任何資訊之前停用執行 hello 計時器。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="e2c0d-121">它是最多 toohello 執行者 tooregister 任何需要在 hello 未來重新啟動時的計時器。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="e2c0d-122">如需詳細資訊，請參閱 hello 一節[執行者回收](service-fabric-reliable-actors-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="e2c0d-123">動作項目提醒</span><span class="sxs-lookup"><span data-stu-id="e2c0d-123">Actor reminders</span></span>
<span data-ttu-id="e2c0d-124">提醒會機制 tootrigger 永續性的回呼，在動作項目上指定的時間。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="e2c0d-125">其功能非常類似 tootimers。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="e2c0d-126">但不同於計時器提醒觸發在所有情況下直到 hello 執行者明確取消註冊它們，或明確刪除 hello 動作項目。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="e2c0d-127">具體來說，提醒會觸發跨動作項目和停用和容錯移轉，因為 hello 執行者執行階段保存提醒 hello 執行者的資訊。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="e2c0d-128">tooregister 提醒，執行者呼叫 hello `RegisterReminderAsync` hello 基底類別，提供 hello 下列範例所示的方法：</span><span class="sxs-lookup"><span data-stu-id="e2c0d-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="e2c0d-129">在此範例中， `"Pay cell phone bill"` hello 提醒名稱。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="e2c0d-130">這是 hello 動作項目使用的字串 toouniquely 識別提醒。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="e2c0d-131">`BitConverter.GetBytes(amountInDollars)`(C#) 是與 hello 提醒相關聯的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="e2c0d-132">它將回復 toohello 動作項目以傳遞的引數 toohello 提醒回撥，也就是`IRemindable.ReceiveReminderAsync`(C#) 或`Remindable.receiveReminderAsync`(Java)。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="e2c0d-133">使用提醒的動作項目必須實作 hello`IRemindable`介面，如以下 hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="e2c0d-134">Hello Reliable Actors 執行階段提醒觸發時，將會叫用 hello `ReceiveReminderAsync`(C#) 或`receiveReminderAsync`hello 動作項目上的 (Java) 方法。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="e2c0d-135">執行者可以註冊多個備忘提醒，及 hello `ReceiveReminderAsync`(C#) 或`receiveReminderAsync`(Java) 方法會叫用任何這些備忘提醒觸發時機。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="e2c0d-136">hello 動作項目可以使用 hello 提醒名稱傳入 toohello `ReceiveReminderAsync`(C#) 或`receiveReminderAsync`(Java) 方法 toofigure 哪一個已觸發的提醒。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="e2c0d-137">hello 執行者執行階段會儲存 hello 執行者 」 狀態時 hello `ReceiveReminderAsync`(C#) 或`receiveReminderAsync`(Java) 呼叫完成。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="e2c0d-138">如果儲存 hello 狀態時，發生錯誤，將會停用該動作項目物件，並將啟用的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="e2c0d-139">toounregister 提醒，執行者呼叫 hello `UnregisterReminderAsync`(C#) 或`unregisterReminderAsync`(Java) 方法，如以下的 hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="e2c0d-140">如上所示，hello `UnregisterReminderAsync`(C#) 或`unregisterReminderAsync`(Java) 方法會接受`IActorReminder`(C#) 或`ActorReminder`(Java) 介面。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="e2c0d-141">hello 執行者基底類別支援`GetReminder`(C#) 或`getReminder`(Java) 方法，可以使用的 tooretrieve hello `IActorReminder`(C#) 或`ActorReminder`傳入 hello 提醒名稱 (Java) 介面。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="e2c0d-142">這是很方便，因為 hello 動作項目不需要 toopersist hello `IActorReminder`(C#) 或`ActorReminder`(Java) 介面傳回從 hello `RegisterReminder`(C#) 或`registerReminder`(Java) 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="e2c0d-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2c0d-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2c0d-143">Next Steps</span></span>
<span data-ttu-id="e2c0d-144">深入了解 Reliable Actor 事件和重新進入：</span><span class="sxs-lookup"><span data-stu-id="e2c0d-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="e2c0d-145">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="e2c0d-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="e2c0d-146">動作項目重新進入</span><span class="sxs-lookup"><span data-stu-id="e2c0d-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
