---
title: "Reliable Actors 架構中的多型 | Microsoft Docs"
description: "在 Reliable Actors 架構中建置 .NET 介面和類型的階層，以重複使用功能和 API 定義。"
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
ms.openlocfilehash: 36a59a41b2261369a2062c76ef90aebf7e24a221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="polymorphism-in-the-reliable-actors-framework"></a><span data-ttu-id="dfac4-103">Reliable Actors 架構中的多型</span><span class="sxs-lookup"><span data-stu-id="dfac4-103">Polymorphism in the Reliable Actors framework</span></span>
<span data-ttu-id="dfac4-104">Reliable Actors 架構可讓您使用許多您會在物件導向設計中使用的相同技巧來建置動作項目。</span><span class="sxs-lookup"><span data-stu-id="dfac4-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="dfac4-105">這些技巧的其中之一就是多型，此技巧允許從更一般化的父系繼承類型和介面。</span><span class="sxs-lookup"><span data-stu-id="dfac4-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span></span> <span data-ttu-id="dfac4-106">Reliable Actors 架構中的繼承通常會遵循 .NET 模型，但有幾個額外的條件約束。</span><span class="sxs-lookup"><span data-stu-id="dfac4-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span></span> <span data-ttu-id="dfac4-107">針對 Java/Linux，它會遵循 Java 模型。</span><span class="sxs-lookup"><span data-stu-id="dfac4-107">In case of Java/Linux, it follows the Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="dfac4-108">介面</span><span class="sxs-lookup"><span data-stu-id="dfac4-108">Interfaces</span></span>
<span data-ttu-id="dfac4-109">Reliable Actors 架構會要求您至少定義一個要由動作項目類型實作的介面。</span><span class="sxs-lookup"><span data-stu-id="dfac4-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span></span> <span data-ttu-id="dfac4-110">此介面會用來產生可供用戶端用來與您的動作項目進行通訊的 Proxy 類別。</span><span class="sxs-lookup"><span data-stu-id="dfac4-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span></span> <span data-ttu-id="dfac4-111">只要動作項目類型及其所有父系所實作的每個介面最終都是衍生自 IActor(C#) 或 Actor(Java)，這些介面便可以從其他介面繼承。</span><span class="sxs-lookup"><span data-stu-id="dfac4-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="dfac4-112">IActor(C#) 和 Actor(Java) 分別是針對 .NET 和 Java 架構中動作項目的平台定義基底介面。</span><span class="sxs-lookup"><span data-stu-id="dfac4-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span></span> <span data-ttu-id="dfac4-113">因此，使用圖形的傳統多型範例可能會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="dfac4-113">Thus, the classic polymorphism example using shapes might look something like this:</span></span>

![圖形動作項目的介面階層][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="dfac4-115">類型</span><span class="sxs-lookup"><span data-stu-id="dfac4-115">Types</span></span>
<span data-ttu-id="dfac4-116">您也可以建立衍生自平台所提供之基底「動作項目」類別的動作項目類型階層。</span><span class="sxs-lookup"><span data-stu-id="dfac4-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span></span> <span data-ttu-id="dfac4-117">如果是圖形，您可能會有一個基底 `Shape`(C#) 或 `ShapeImpl`(Java) 類型：</span><span class="sxs-lookup"><span data-stu-id="dfac4-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="dfac4-118">`Shape`(C#) 或 `ShapeImpl`(Java) 的子類型可以從基底覆寫方法。</span><span class="sxs-lookup"><span data-stu-id="dfac4-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span></span>

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

<span data-ttu-id="dfac4-119">請注意動作項目類型上的 `ActorService` 屬性。</span><span class="sxs-lookup"><span data-stu-id="dfac4-119">Note the `ActorService` attribute on the actor type.</span></span> <span data-ttu-id="dfac4-120">此屬性會告知 Reliable Actor 架構應該自動建立一個服務來裝載此類型的動作項目。</span><span class="sxs-lookup"><span data-stu-id="dfac4-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="dfac4-121">在某些情況下，您可能會想要建立僅供與子類型共用功能而永遠不用來將具體動作項目具現化的基底類型。</span><span class="sxs-lookup"><span data-stu-id="dfac4-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span></span> <span data-ttu-id="dfac4-122">在這些情況下，您應該使用 `abstract` 關鍵字來指出您永遠不會根據該類型建立動作項目。</span><span class="sxs-lookup"><span data-stu-id="dfac4-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfac4-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfac4-123">Next steps</span></span>
* <span data-ttu-id="dfac4-124">請參閱 [Reliable Actors 架構如何利用 Service Fabric 平台](service-fabric-reliable-actors-platform.md) 以提供可靠性、延展性及一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="dfac4-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="dfac4-125">了解 [動作項目生命週期](service-fabric-reliable-actors-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="dfac4-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
