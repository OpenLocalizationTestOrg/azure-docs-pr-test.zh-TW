---
title: "在 hello Reliable Actors framework aaaPolymorphism |Microsoft 文件"
description: "建立.NET 介面和 hello Reliable Actors framework tooreuse 功能中的類型和應用程式開發介面定義的階層。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Hello Reliable Actors framework 中的多型
架構可讓您使用許多 toobuild 執行者 hello Reliable Actors hello 相同技巧，您會在物件導向設計中使用。 這些技術的其中一個是多型，可讓類型以及介面從多 tooinherit 一般化父代。 Hello Reliable Actors 架構中的繼承通常會遵循 hello.NET 模型具有幾個額外條件約束。 發生 Java/Linux，它會遵循 hello Java 模型。

## <a name="interfaces"></a>介面
hello Reliable Actors 架構需要您 toodefine 至少一個介面 toobe 動作項目類型所實作。 這個介面是使用的 toogenerate proxy 類別，可供用戶端 toocommunicate 與您的動作項目。 只要動作項目類型及其所有父系所實作的每個介面最終都是衍生自 IActor(C#) 或 Actor(Java)，這些介面便可以從其他介面繼承。 IActor(C#) 和 Actor(Java) 分別 hello 平台定義基底介面的.NET 和 Java 的 hello 架構中的動作項目。 因此，hello 傳統的多型的範例使用圖形可能看起來像這樣：

![圖形動作項目的介面階層][shapes-interface-hierarchy]

## <a name="types"></a>類型
您也可以建立動作項目型別，衍生自 hello 基底動作項目類別所提供的 hello 平台的階層。 在圖形的 hello 情況下，您可能會有基底`Shape`(C#) 或`ShapeImpl`(Java) 類型：

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

子類型`Shape`(C#) 或`ShapeImpl`(Java) 可以覆寫來自基底 hello 的方法。

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

請注意 hello `ActorService` hello 動作項目類型的屬性。 這個屬性會告知 hello Reliable Actor framework 應自動建立服務以進行主控此類型的動作項目。 在某些情況下，您可能希望 toocreate 僅適用於子型別與共用功能的基底類型，並將不會使用的 tooinstantiate 具體的動作項目。 在這些情況下，您應該使用 hello`abstract`關鍵字 tooindicate 永遠不會建立動作項目，根據該型別。

## <a name="next-steps"></a>後續步驟
* 請參閱[hello Reliable Actors 架構如何運用 hello Service Fabric 平台](service-fabric-reliable-actors-platform.md)tooprovide 可靠性、 延展性及一致的狀態。
* 深入了解 hello[執行者生命週期](service-fabric-reliable-actors-lifecycle.md)。

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
