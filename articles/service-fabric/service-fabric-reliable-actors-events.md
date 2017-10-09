---
title: "以行動為基礎的 Azure microservices aaaEvents |Microsoft 文件"
description: "服務網狀架構 Reliable Actors 的簡介 tooevents。"
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
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="bf2c8-103">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="bf2c8-103">Actor events</span></span>
<span data-ttu-id="bf2c8-104">動作項目事件會提供從 hello 執行者 toohello 用戶端方式 toosend 最佳通知。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="bf2c8-105">動作項目事件是為了動作項目與用戶端之間的通訊而設計，不應用於動作項目與動作項目之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="bf2c8-106">hello 下列程式碼片段顯示如何在應用程式中的 toouse 動作項目事件。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="bf2c8-107">定義描述 hello 事件 hello 動作項目所發行的介面。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="bf2c8-108">此介面必須衍生自 hello`IActorEvents`介面。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="bf2c8-109">hello 方法的 hello 引數必須是[資料合約序列化](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="bf2c8-110">hello 方法必須傳回 void，為事件通知是一種方式和最佳效果。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="bf2c8-111">宣告 hello hello 執行者介面中的 hello 執行者所發行的事件。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-111">Declare hello events published by hello actor in hello actor interface.</span></span>

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
<span data-ttu-id="bf2c8-112">Hello 用戶端，實作 hello 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-112">On hello client side, implement hello event handler.</span></span>

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

<span data-ttu-id="bf2c8-113">Hello 用戶端上建立發行 hello 事件 proxy toohello 動作項目，並訂閱 tooits 事件。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="bf2c8-114">在 hello 事件中的容錯移轉期間，hello 執行者可以容錯移轉 tooa 不同處理序或節點。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="bf2c8-115">hello 執行者 proxy 管理 hello 使用中的訂閱，並自動重新訂閱。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="bf2c8-116">您可以控制透過 hello hello 重新訂用帳戶間隔`ActorProxyEventExtensions.SubscribeAsync<TEvent>`應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="bf2c8-117">toounsubscribe，使用 hello`ActorProxyEventExtensions.UnsubscribeAsync<TEvent>`應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="bf2c8-118">在 hello 動作項目，只要將發行 hello 事件發生。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="bf2c8-119">如果 「 訂閱者 」 toohello 事件，hello 執行者執行階段會傳送它們 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="bf2c8-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="bf2c8-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf2c8-120">Next steps</span></span>
* [<span data-ttu-id="bf2c8-121">動作項目重新進入</span><span class="sxs-lookup"><span data-stu-id="bf2c8-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="bf2c8-122">動作項目診斷與效能監視</span><span class="sxs-lookup"><span data-stu-id="bf2c8-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="bf2c8-123">動作項目 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="bf2c8-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="bf2c8-124">C# 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="bf2c8-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="bf2c8-125">C# .NET Core 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="bf2c8-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="bf2c8-126">Java 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="bf2c8-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
