---
title: "動作項目 aaaReliable 執行者注意事項輸入序列化 |Microsoft 文件"
description: "討論定義可以使用的 toodefine 服務網狀架構 Reliable Actors 狀態的可序列化類別和介面的基本需求"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a>Service Fabric Reliable Actors 類型序列化的注意事項
hello 所有方法的引數的 hello 工作的結果類型傳回的動作項目介面，在每個方法和物件儲存在動作項目的狀態管理員必須[資料合約序列化](https://msdn.microsoft.com/library/ms731923.aspx)。 這也適用於 toohello 引數的定義中的 hello 方法[動作項目事件介面](service-fabric-reliable-actors-events.md)。 (動作項目事件介面方法一律會傳回無效)。

## <a name="custom-data-types"></a>自訂資料類型
在此範例中，下列動作項目介面的 hello 定義傳回呼叫的自訂資料類型的方法`VoicemailBox`:

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

hello 介面藉由使用 hello 狀態管理員 toostore 執行者`VoicemailBox`物件：

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

在此範例中，hello`VoicemailBox`物件序列化時：

* 動作項目執行個體和呼叫端之間傳輸 hello 物件。
* hello 物件會儲存在 hello 狀態管理員，它會保存的 toodisk 和複寫 tooother 節點。

hello Reliable Actor 架構會使用 DataContract 序列化。 因此，hello 自訂資料物件和其成員必須以 hello 註解**DataContract**和**DataMember**分別屬性。

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a>後續步驟
* [動作項目生命週期與記憶體回收](service-fabric-reliable-actors-lifecycle.md)
* [動作項目計時器和提醒](service-fabric-reliable-actors-timers-reminders.md)
* [動作項目事件](service-fabric-reliable-actors-events.md)
* [動作項目重新進入](service-fabric-reliable-actors-reentrancy.md)
* [動作項目多型和物件導向的設計模式](service-fabric-reliable-actors-polymorphism.md)
* [動作項目診斷與效能監視](service-fabric-reliable-actors-diagnostics.md)
