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
# <a name="actor-events"></a>動作項目事件
動作項目事件會提供從 hello 執行者 toohello 用戶端方式 toosend 最佳通知。 動作項目事件是為了動作項目與用戶端之間的通訊而設計，不應用於動作項目與動作項目之間的通訊。

hello 下列程式碼片段顯示如何在應用程式中的 toouse 動作項目事件。

定義描述 hello 事件 hello 動作項目所發行的介面。 此介面必須衍生自 hello`IActorEvents`介面。 hello 方法的 hello 引數必須是[資料合約序列化](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)。 hello 方法必須傳回 void，為事件通知是一種方式和最佳效果。

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
宣告 hello hello 執行者介面中的 hello 執行者所發行的事件。

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
Hello 用戶端，實作 hello 事件處理常式。

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

Hello 用戶端上建立發行 hello 事件 proxy toohello 動作項目，並訂閱 tooits 事件。

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

在 hello 事件中的容錯移轉期間，hello 執行者可以容錯移轉 tooa 不同處理序或節點。 hello 執行者 proxy 管理 hello 使用中的訂閱，並自動重新訂閱。 您可以控制透過 hello hello 重新訂用帳戶間隔`ActorProxyEventExtensions.SubscribeAsync<TEvent>`應用程式開發介面。 toounsubscribe，使用 hello`ActorProxyEventExtensions.UnsubscribeAsync<TEvent>`應用程式開發介面。

在 hello 動作項目，只要將發行 hello 事件發生。 如果 「 訂閱者 」 toohello 事件，hello 執行者執行階段會傳送它們 hello 通知。

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>後續步驟
* [動作項目重新進入](service-fabric-reliable-actors-reentrancy.md)
* [動作項目診斷與效能監視](service-fabric-reliable-actors-diagnostics.md)
* [動作項目 API 參考文件](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# 範例程式碼 (英文)](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [C# .NET Core 範例程式碼](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Java 範例程式碼 (英文)](http://github.com/Azure-Samples/service-fabric-java-getting-started)
