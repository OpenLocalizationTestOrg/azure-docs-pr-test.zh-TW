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
# <a name="reliable-actors-reentrancy"></a>Reliable Actors 重新進入
hello Reliable Actors 執行階段中，依預設，可讓邏輯呼叫內容為基礎的重新進入。 這允許執行者 toobe reentrant 如果它們是在 hello 相同呼叫內容的鏈結。 例如，執行者 A 會傳送訊息 tooActor B 傳送訊息 tooActor c 的人員Hello 訊息處理的一部分，如果執行者 C 呼叫動作項目，hello 訊息是可重新進入，因此它不會允許。 屬於不同呼叫內容的其他任何訊息都將在動作項目 A 上遭到封鎖，直到其處理完畢為止。

有兩個選項可用來在 hello 中定義的動作項目重新進入`ActorReentrancyMode`列舉：

* `LogicalCallContext` (預設行為)
* `Disallowed` - 停用重新進入

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
可在註冊期間在 `ActorService`的設定中設定重新進入。 hello 設定適用於 tooall hello 行動服務中建立的動作項目執行個體。

hello 下列範例示範設定 hello 重新進入模式太 actor 服務`ActorReentrancyMode.Disallowed`。 在此情況下，如果執行者會傳送可重新進入的訊息 tooanother 執行者，類型的例外狀況`FabricException`就會擲回。

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


## <a name="next-steps"></a>後續步驟
* 深入了解 hello 中的重新進入[執行者 API 參考文件](https://msdn.microsoft.com/library/azure/dn971626.aspx)
