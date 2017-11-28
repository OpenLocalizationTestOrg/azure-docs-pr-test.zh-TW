---
title: "動作項目型 Azure 微服務中的事件 | Microsoft Docs"
description: "Service Fabric Reliable Actor 事件簡介。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: d936670c548ff709fc2e935d3f28d94e4bde8a04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="actor-events"></a><span data-ttu-id="1d6d7-103">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="1d6d7-103">Actor events</span></span>
<span data-ttu-id="1d6d7-104">動作項目事件會將最佳效果通知從動作項目傳送到用戶端。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="1d6d7-105">動作項目事件是為了動作項目與用戶端之間的通訊而設計，不應用於動作項目與動作項目之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="1d6d7-106">下列程式碼片段顯示如何在應用程式中使用動作項目事件。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="1d6d7-107">定義描述動作項目所發佈事件的介面。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="1d6d7-108">此介面必須衍生自 `IActorEvents` 介面。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="1d6d7-109">方法的引數必須是 [資料合約序列化](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="1d6d7-110">當事件通知是單向且為最佳效果時，方法必須傳回無效。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-110">The methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="1d6d7-111">宣告由動作項目介面中動作項目發佈的事件。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-111">Declare the events published by the actor in the actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="1d6d7-112">在用戶端上，實作事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-112">On the client side, implement the event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="1d6d7-113">在用戶端上，對發佈事件的動作項目建立 Proxy，並訂閱其事件。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="1d6d7-114">發生容錯移轉時，動作項目會容錯移轉至不同的程序或節點。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="1d6d7-115">動作項目 Proxy 會管理使用中的訂用帳戶，並自動重新訂閱。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="1d6d7-116">您可以透過 `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API 控制重新訂閱間隔。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="1d6d7-117">若要取消訂閱，請使用 `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="1d6d7-118">在動作項目上，當事件發生時只發佈事件。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="1d6d7-119">如果有訂閱者訂閱事件，動作項目執行階段會將事件傳送至通知。</span><span class="sxs-lookup"><span data-stu-id="1d6d7-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="1d6d7-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d6d7-120">Next steps</span></span>
* [<span data-ttu-id="1d6d7-121">動作項目重新進入</span><span class="sxs-lookup"><span data-stu-id="1d6d7-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="1d6d7-122">動作項目診斷與效能監視</span><span class="sxs-lookup"><span data-stu-id="1d6d7-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="1d6d7-123">動作項目 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="1d6d7-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="1d6d7-124">C# 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="1d6d7-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="1d6d7-125">C# .NET Core 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="1d6d7-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="1d6d7-126">Java 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="1d6d7-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
