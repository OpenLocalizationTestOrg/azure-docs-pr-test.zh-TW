---
title: "Reliable Actors 計時器和提醒 | Microsoft Docs"
description: "Service Fabric Reliable Actors 計時器和提醒簡介。"
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
ms.openlocfilehash: 06b026ce06e0f16a77ac238de0af2263f272933c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="a105a-103">動作項目計時器和提醒</span><span class="sxs-lookup"><span data-stu-id="a105a-103">Actor timers and reminders</span></span>
<span data-ttu-id="a105a-104">動作項目可藉由註冊計時器或提醒來排程本身的週期性工作。</span><span class="sxs-lookup"><span data-stu-id="a105a-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="a105a-105">本文示範如何使用計時器和提醒，以及說明它們之間的差異。</span><span class="sxs-lookup"><span data-stu-id="a105a-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="a105a-106">動作項目計時器</span><span class="sxs-lookup"><span data-stu-id="a105a-106">Actor timers</span></span>
<span data-ttu-id="a105a-107">動作項目計時器提供 .NET 或 Java 計時器的簡單包裝函式，以確保回呼方法採用動作項目執行階段所提供的回合式並行保證。</span><span class="sxs-lookup"><span data-stu-id="a105a-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="a105a-108">動作項目可以在其基底類別使用 `RegisterTimer`(C#) 或 `registerTimer`(Java) 和 `UnregisterTimer`(C#) 或 `unregisterTimer`(Java) 方法註冊和取消其計時器。</span><span class="sxs-lookup"><span data-stu-id="a105a-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="a105a-109">下列範例示範如何使用計時器 API。</span><span class="sxs-lookup"><span data-stu-id="a105a-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="a105a-110">API 和 .NET 計時器或 Java 計時器非常類似。</span><span class="sxs-lookup"><span data-stu-id="a105a-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="a105a-111">在此範例中，當計時器到期時，動作項目執行階段將會呼叫 `MoveObject`(C#) 或 `moveObject`(Java) 方法。</span><span class="sxs-lookup"><span data-stu-id="a105a-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="a105a-112">此方法保證會採用回合式並行存取。</span><span class="sxs-lookup"><span data-stu-id="a105a-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="a105a-113">這表示沒有其他動作項目方法或計時器/提醒回呼將在進行中，直到此回呼完成執行為止。</span><span class="sxs-lookup"><span data-stu-id="a105a-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

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
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

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
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
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

<span data-ttu-id="a105a-114">當回呼完成執行後，就會啟動下一期間的計時器。</span><span class="sxs-lookup"><span data-stu-id="a105a-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="a105a-115">這表示回呼執行時計時器將會停止，並在回呼完成時重新啟動。</span><span class="sxs-lookup"><span data-stu-id="a105a-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="a105a-116">動作項目執行階段會儲存在回呼完成時，對動作項目的狀態管理員所做的變更。</span><span class="sxs-lookup"><span data-stu-id="a105a-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="a105a-117">如果儲存狀態時發生錯誤，將會停用該動作項目物件並啟動新的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a105a-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="a105a-118">當動作項目在記憶體回收期間停用時，將會停止所有的計時器。</span><span class="sxs-lookup"><span data-stu-id="a105a-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="a105a-119">而在此之後不會叫用任何計時器回呼。</span><span class="sxs-lookup"><span data-stu-id="a105a-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="a105a-120">此外，動作項目執行階段並不保留任何停用前執行中的計時器資訊。</span><span class="sxs-lookup"><span data-stu-id="a105a-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="a105a-121">由動作項目來決定任何未來重新啟動時所需計時器的註冊。</span><span class="sxs-lookup"><span data-stu-id="a105a-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="a105a-122">如需詳細資訊，請參閱 [動作項目記憶體回收](service-fabric-reliable-actors-lifecycle.md)一節。</span><span class="sxs-lookup"><span data-stu-id="a105a-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="a105a-123">動作項目提醒</span><span class="sxs-lookup"><span data-stu-id="a105a-123">Actor reminders</span></span>
<span data-ttu-id="a105a-124">提醒是一個會在指定時間於動作項目上觸發持續性回呼的機制。</span><span class="sxs-lookup"><span data-stu-id="a105a-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="a105a-125">其功能很類似計時器。</span><span class="sxs-lookup"><span data-stu-id="a105a-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="a105a-126">但與計時器不同的是，在所有情況下都會觸發提醒，直到動作項目明確地取消註冊它們或動作項目明確刪除為止。</span><span class="sxs-lookup"><span data-stu-id="a105a-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="a105a-127">具體而言，動作項目的停用和容錯移轉會觸發提醒，因為動作項目執行階段所保存的動作項目提醒相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a105a-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="a105a-128">若要註冊提醒，動作項目會呼叫基底類別提供的 `RegisterReminderAsync` 方法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="a105a-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

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
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="a105a-129">在此範例中， `"Pay cell phone bill"` 為該提醒名稱。</span><span class="sxs-lookup"><span data-stu-id="a105a-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="a105a-130">這是動作項目用來唯一識別提醒的一個字串。</span><span class="sxs-lookup"><span data-stu-id="a105a-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="a105a-131">`BitConverter.GetBytes(amountInDollars)`(C#) 為與提醒相關聯的內容。</span><span class="sxs-lookup"><span data-stu-id="a105a-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="a105a-132">其會作為提醒回呼的引數傳回給動作項目，也就是 `IRemindable.ReceiveReminderAsync`(C#) 或 `Remindable.receiveReminderAsync`(Java)。</span><span class="sxs-lookup"><span data-stu-id="a105a-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="a105a-133">使用提醒的動作項目必須實作 `IRemindable` 介面，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a105a-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

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

<span data-ttu-id="a105a-134">當觸發提醒時，Reliable Actors 執行階段將會叫用動作項目上的 `ReceiveReminderAsync`(C#) 或 `receiveReminderAsync`(Java) 方法。</span><span class="sxs-lookup"><span data-stu-id="a105a-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="a105a-135">一個動作項目可以註冊多個提醒，而每當觸發這些提醒中的任一個時，便會叫用 `ReceiveReminderAsync`(C#) 或 `receiveReminderAsync`(Java) 方法。</span><span class="sxs-lookup"><span data-stu-id="a105a-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="a105a-136">動作項目可以使用傳遞至 `ReceiveReminderAsync`(C#) 或 `receiveReminderAsync`(Java) 方法的提醒名稱，以找出已觸發的提醒。</span><span class="sxs-lookup"><span data-stu-id="a105a-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="a105a-137">當 `ReceiveReminderAsync`(C#) 或 `receiveReminderAsync`(Java) 呼叫完成時，動作項目執行階段會儲存動作項目狀態。</span><span class="sxs-lookup"><span data-stu-id="a105a-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="a105a-138">如果儲存狀態時發生錯誤，將會停用該動作項目物件並啟動新的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a105a-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="a105a-139">若要將提醒取消註冊，動作項目會呼叫 `UnregisterReminderAsync`(C#) 或 `unregisterReminderAsync`(Java) 方法，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a105a-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="a105a-140">如上所示，`UnregisterReminderAsync`(C#) 或 `unregisterReminderAsync`(Java) 方法會接受 `IActorReminder`(C#) 或 `ActorReminder`(Java) 介面。</span><span class="sxs-lookup"><span data-stu-id="a105a-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="a105a-141">動作項目基底類別支援 `GetReminder`(C#) 或 `getReminder`(Java) 方法，在傳遞進提醒名稱時可以用來擷取 `IActorReminder`(C#) 或 `ActorReminder`(Java) 介面。</span><span class="sxs-lookup"><span data-stu-id="a105a-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="a105a-142">這很方便，因為動作項目不需保存從 `RegisterReminder`(C#) 或 `registerReminder`(Java) 方法呼叫傳回的 `IActorReminder`(C#) 或 `ActorReminder`(Java) 介面。</span><span class="sxs-lookup"><span data-stu-id="a105a-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a105a-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a105a-143">Next Steps</span></span>
<span data-ttu-id="a105a-144">深入了解 Reliable Actor 事件和重新進入：</span><span class="sxs-lookup"><span data-stu-id="a105a-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="a105a-145">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="a105a-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="a105a-146">動作項目重新進入</span><span class="sxs-lookup"><span data-stu-id="a105a-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
