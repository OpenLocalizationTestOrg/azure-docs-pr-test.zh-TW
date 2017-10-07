---
title: "動作項目為基礎的 Azure microservices 生命週期的 aaaOverview |Microsoft 文件"
description: "說明 Service Fabric Reliable Actor 生命週期、記憶體回收，以及手動刪除動作項目與其狀態"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>動作項目生命週期、自動記憶體回收，以及手動刪除
啟動動作項目 hello tooany 其方法進行呼叫的第一次。 動作項目是已停用 （記憶體回收 hello 執行者執行階段所收集），如果它不是可設定的一段時間。 動作項目與其狀態也可以隨時進行手動刪除。

## <a name="actor-activation"></a>啟用動作項目
啟動動作項目時，hello 會發生下列情況：

* 當動作項目有呼叫卻尚未為使用中時，會建立新的動作項目。
* 如果維護狀態，已載入 hello 動作項目的狀態。
* hello `OnActivateAsync` (C#) 或`onActivateAsync`(Java) （這會覆寫在 hello 動作項目實作） 會呼叫。
* hello 動作項目會視為使用中。

## <a name="actor-deactivation"></a>停用動作項目
當停用動作項目時，hello 會發生下列情況：

* 當動作項目不是一段時間時，它會從 hello 作用中的動作項目資料表中移除。
* hello `OnDeactivateAsync` (C#) 或`onDeactivateAsync`(Java) （這會覆寫在 hello 動作項目實作） 會呼叫。 這會清除所有 hello 計時器 hello 動作項目。 您不應該從此方法呼叫動作項目作業 (例如狀態變更)。

> [!TIP]
> hello Fabric 動作項目執行階段發出某些[tooactor 啟用和停用相關事件](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters)。 這些項目對於診斷與效能監視很有幫助。
>
>

### <a name="actor-garbage-collection"></a>動作項目記憶體回收
動作項目已停用時，釋放參考 toohello 動作項目物件，它可以進行記憶體回收通常由 hello common language runtime (CLR) 或 java 虛擬機器 (JVM) 記憶體回收行程。 廢棄項目收集只清除 hello 動作項目物件。它會**不**移除儲存在 hello 執行者狀態管理員的狀態。 hello 下一個時間 hello 執行者啟動、 建立新的動作項目物件，並還原其狀態。

哪些算是"的使用 的 hello 目的是要停用和記憶體回收？

* 一直收到呼叫
* `IRemindable.ReceiveReminderAsync`所叫用 （僅適用於 hello 動作項目使用提醒） 方法

> [!NOTE]
> 如果 hello 動作項目使用計時器，並叫用其計時器回呼，它會**不**計數，表示 「 正在使用 」。
>
>

我們進入停用的 hello 詳細資料之前，它會是重要 toodefine hello 下列條款：

* *掃描間隔*。 這是在哪一個 hello 執行者執行階段會掃描其作用中的動作項目資料表可以停用的執行者 hello 間隔和記憶體回收。 這個 hello 預設值為 1 分鐘。
* *閒置逾時*。 這是 hello 動作項目需要 tooremain 上未使用的時間量 （閒置） 之前可以停用和記憶體回收。 這個 hello 預設值是 60 分鐘的時間。

一般而言，您不需要 toochange 這些預設值。 不過，如有必要，可以在註冊[動作項目服務](service-fabric-reliable-actors-platform.md)時透過 `ActorServiceSettings` 變更這些間隔：

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
針對每個作用中動作項目 hello 動作項目執行階段會追蹤的 hello 已閒置 （也就是未使用） 的時間量。 hello 動作項目執行階段會檢查每個 hello 執行者的每個`ScanIntervalInSeconds`toosee 如果記憶體回收可以收集並收集它，如果已閒置`IdleTimeoutInSeconds`。

使用動作項目時，每當它閒置的時間是重設 too0。 在此之後，hello 動作項目進行記憶體回收才再次持續閒置的`IdleTimeoutInSeconds`。 恢復動作項目會被視為 toohave 已使用如果執行者介面方法或執行者提醒回呼在執行。 執行者是**不**toohave 會被視為已執行其計時器回呼時使用。

hello 下列圖表顯示 hello 生命週期的單一動作項目 tooillustrate 這些概念。

![閒置時間的範例][1]

hello 範例會顯示 hello 這個動作項目存留期上的動作項目方法呼叫，備忘提醒和計時器的 hello 影響。 hello 遵循有關 hello 範例的重點是值得一提的是：

* ScanInterval 和 IdleTimeout too5 和 10 分別設定。 （單位不重要，因為我們的目的在於 tooillustrate hello 概念。）
* 執行者所定義的 hello 掃描間隔為 5 toobe 記憶體回收會發生在 T = 0，5、 10、 15、 20、 25 的 hello 掃描。
* 定期計時器會在 T=4、8、12、16、20、24 時引發，並執行其回呼。 它不會影響 hello 執行者的 hello 閒置時間。
* 在 T = 7 的執行者方法呼叫 hello 閒置時間 too0 會重設，而延遲 hello hello 執行者的記憶體回收。
* T = 14 在執行的動作項目提醒回撥，進一步延遲 hello hello 執行者的記憶體回收。
* Hello 的記憶體回收掃描在 T = 25，期間 hello 執行者的閒置時間最後超過 hello 閒置逾時為 10，而且 hello 執行者記憶體回收。

動作項目正在執行其中一個方法時，無論在執行該方法時花費了多久的時間，動作項目絕對不會進行記憶體回收。 如先前所述，動作項目介面方法和提醒回呼的 hello 執行以防止記憶體回收 hello 執行者的閒置時間 too0 重設。 hello 執行計時器回呼不重設 hello 閒置時間 too0。 不過，hello 執行者的 hello 回收被延遲至 hello 計時器回呼已完成執行為止。

## <a name="deleting-actors-and-their-state"></a>刪除動作項目與其狀態
記憶體回收的已停用動作項目只會清除 hello 動作項目物件，但不會移除儲存動作項目的狀態管理員中的資料。 重新啟動動作項目時，其資料再次變成可用 tooit 透過 hello 狀態管理員。 在其中執行者將資料儲存在狀態管理員和停用，但是永遠不會重新啟動的情況下，可能需要 tooclean 其資料。

hello [Actor 服務](service-fabric-reliable-actors-platform.md)提供函式用於從遠端呼叫端刪除動作項目：

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

刪除動作項目具有下列效果根據 hello 動作項目在目前作用中的 hello:

* **作用中動作項目**
  * 動作項目會從作用中動作項目清單中移除並且停用。
  * 其狀態會永久刪除。
* **非作用中動作項目**
  * 其狀態會永久刪除。

請注意，呼叫動作項目無法刪除本身的其中一個動作項目方法，因為 hello 動作項目無法刪除執行中的 hello 執行階段已取得鎖定 hello 動作項目呼叫 tooenforce 單一執行緒的存取動作項目呼叫內容中時。

## <a name="next-steps"></a>後續步驟
* [動作項目計時器和提醒](service-fabric-reliable-actors-timers-reminders.md)
* [動作項目事件](service-fabric-reliable-actors-events.md)
* [動作項目重新進入](service-fabric-reliable-actors-reentrancy.md)
* [動作項目診斷與效能監視](service-fabric-reliable-actors-diagnostics.md)
* [動作項目 API 參考文件](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# 範例程式碼 (英文)](https://github.com/Azure/servicefabric-samples)
* [Java 範例程式碼 (英文)](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
