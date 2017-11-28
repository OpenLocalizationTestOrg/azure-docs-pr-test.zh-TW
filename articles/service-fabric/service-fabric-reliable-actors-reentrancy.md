---
title: "以行動為基礎的 Azure microservices aaaReentrancy |Microsoft 文件"
description: "服務網狀架構 Reliable Actors 的簡介 tooreentrancy"
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
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="1f49f-103">Reliable Actors 重新進入</span><span class="sxs-lookup"><span data-stu-id="1f49f-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="1f49f-104">hello Reliable Actors 執行階段中，依預設，可讓邏輯呼叫內容為基礎的重新進入。</span><span class="sxs-lookup"><span data-stu-id="1f49f-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="1f49f-105">這允許執行者 toobe reentrant 如果它們是在 hello 相同呼叫內容的鏈結。</span><span class="sxs-lookup"><span data-stu-id="1f49f-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="1f49f-106">例如，執行者 A 會傳送訊息 tooActor B 傳送訊息 tooActor c 的人員Hello 訊息處理的一部分，如果執行者 C 呼叫動作項目，hello 訊息是可重新進入，因此它不會允許。</span><span class="sxs-lookup"><span data-stu-id="1f49f-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="1f49f-107">屬於不同呼叫內容的其他任何訊息都將在動作項目 A 上遭到封鎖，直到其處理完畢為止。</span><span class="sxs-lookup"><span data-stu-id="1f49f-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="1f49f-108">有兩個選項可用來在 hello 中定義的動作項目重新進入`ActorReentrancyMode`列舉：</span><span class="sxs-lookup"><span data-stu-id="1f49f-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="1f49f-109">`LogicalCallContext` (預設行為)</span><span class="sxs-lookup"><span data-stu-id="1f49f-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="1f49f-110">`Disallowed` - 停用重新進入</span><span class="sxs-lookup"><span data-stu-id="1f49f-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="1f49f-111">可在註冊期間在 `ActorService`的設定中設定重新進入。</span><span class="sxs-lookup"><span data-stu-id="1f49f-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="1f49f-112">hello 設定適用於 tooall hello 行動服務中建立的動作項目執行個體。</span><span class="sxs-lookup"><span data-stu-id="1f49f-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="1f49f-113">hello 下列範例示範設定 hello 重新進入模式太 actor 服務`ActorReentrancyMode.Disallowed`。</span><span class="sxs-lookup"><span data-stu-id="1f49f-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="1f49f-114">在此情況下，如果執行者會傳送可重新進入的訊息 tooanother 執行者，類型的例外狀況`FabricException`就會擲回。</span><span class="sxs-lookup"><span data-stu-id="1f49f-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="1f49f-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f49f-115">Next steps</span></span>
* <span data-ttu-id="1f49f-116">深入了解 hello 中的重新進入[執行者 API 參考文件](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="1f49f-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
