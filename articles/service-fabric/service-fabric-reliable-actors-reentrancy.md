---
title: "動作項目型 Azure 微服務中的重新進入 | Microsoft Docs"
description: "Service Fabric Reliable Actors 重新進入簡介"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 00fcccb379bf1ba3875fbaba57a05b00fa228622
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="f5537-103">Reliable Actors 重新進入</span><span class="sxs-lookup"><span data-stu-id="f5537-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="f5537-104">Reliable Actors 執行階段預設允許邏輯呼叫以內容為基礎的重新進入。</span><span class="sxs-lookup"><span data-stu-id="f5537-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="f5537-105">這允許位於相同的呼叫內容鏈結的動作項目可重新進入。</span><span class="sxs-lookup"><span data-stu-id="f5537-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="f5537-106">例如，動作項目 A 傳送訊息給動作項目 B，而動作項目 B 又將訊息傳送給動作項目 C。當處理訊息時，如果動作項目 C 呼叫動作項目 A，則此訊息是可以重新進入的，因此將允許此訊息。</span><span class="sxs-lookup"><span data-stu-id="f5537-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="f5537-107">屬於不同呼叫內容的其他任何訊息都將在動作項目 A 上遭到封鎖，直到其處理完畢為止。</span><span class="sxs-lookup"><span data-stu-id="f5537-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="f5537-108">有兩個選項適用於 `ActorReentrancyMode` 列舉中定義的動作項目重新進入︰</span><span class="sxs-lookup"><span data-stu-id="f5537-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="f5537-109">`LogicalCallContext` (預設行為)</span><span class="sxs-lookup"><span data-stu-id="f5537-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="f5537-110">`Disallowed` - 停用重新進入</span><span class="sxs-lookup"><span data-stu-id="f5537-110">`Disallowed` - disables reentrancy</span></span>

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
<span data-ttu-id="f5537-111">可在註冊期間在 `ActorService`的設定中設定重新進入。</span><span class="sxs-lookup"><span data-stu-id="f5537-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="f5537-112">此設定適用於動作項目服務中建立的所有動作項目執行個體。</span><span class="sxs-lookup"><span data-stu-id="f5537-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="f5537-113">下列範例會示範動作項目服務如何將重新進入模式設定為 `ActorReentrancyMode.Disallowed`。</span><span class="sxs-lookup"><span data-stu-id="f5537-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="f5537-114">在此情況下，如果動作項目傳送可重新進入的訊息給另一個動作項目類型，就會擲回 `FabricException` 類型的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f5537-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="f5537-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5537-115">Next steps</span></span>
* <span data-ttu-id="f5537-116">參閱[動作項目 API 參考文件](https://msdn.microsoft.com/library/azure/dn971626.aspx)來深入了解重新進入</span><span class="sxs-lookup"><span data-stu-id="f5537-116">Learn more about reentrancy in the [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
