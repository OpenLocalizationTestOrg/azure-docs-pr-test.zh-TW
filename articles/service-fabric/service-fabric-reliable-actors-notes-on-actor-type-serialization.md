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
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="a623c-103">Service Fabric Reliable Actors 類型序列化的注意事項</span><span class="sxs-lookup"><span data-stu-id="a623c-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="a623c-104">hello 所有方法的引數的 hello 工作的結果類型傳回的動作項目介面，在每個方法和物件儲存在動作項目的狀態管理員必須[資料合約序列化](https://msdn.microsoft.com/library/ms731923.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a623c-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="a623c-105">這也適用於 toohello 引數的定義中的 hello 方法[動作項目事件介面](service-fabric-reliable-actors-events.md)。</span><span class="sxs-lookup"><span data-stu-id="a623c-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="a623c-106">(動作項目事件介面方法一律會傳回無效)。</span><span class="sxs-lookup"><span data-stu-id="a623c-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="a623c-107">自訂資料類型</span><span class="sxs-lookup"><span data-stu-id="a623c-107">Custom data types</span></span>
<span data-ttu-id="a623c-108">在此範例中，下列動作項目介面的 hello 定義傳回呼叫的自訂資料類型的方法`VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="a623c-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="a623c-109">hello 介面藉由使用 hello 狀態管理員 toostore 執行者`VoicemailBox`物件：</span><span class="sxs-lookup"><span data-stu-id="a623c-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="a623c-110">在此範例中，hello`VoicemailBox`物件序列化時：</span><span class="sxs-lookup"><span data-stu-id="a623c-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="a623c-111">動作項目執行個體和呼叫端之間傳輸 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="a623c-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="a623c-112">hello 物件會儲存在 hello 狀態管理員，它會保存的 toodisk 和複寫 tooother 節點。</span><span class="sxs-lookup"><span data-stu-id="a623c-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="a623c-113">hello Reliable Actor 架構會使用 DataContract 序列化。</span><span class="sxs-lookup"><span data-stu-id="a623c-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="a623c-114">因此，hello 自訂資料物件和其成員必須以 hello 註解**DataContract**和**DataMember**分別屬性。</span><span class="sxs-lookup"><span data-stu-id="a623c-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="a623c-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a623c-115">Next steps</span></span>
* [<span data-ttu-id="a623c-116">動作項目生命週期與記憶體回收</span><span class="sxs-lookup"><span data-stu-id="a623c-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="a623c-117">動作項目計時器和提醒</span><span class="sxs-lookup"><span data-stu-id="a623c-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="a623c-118">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="a623c-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="a623c-119">動作項目重新進入</span><span class="sxs-lookup"><span data-stu-id="a623c-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="a623c-120">動作項目多型和物件導向的設計模式</span><span class="sxs-lookup"><span data-stu-id="a623c-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="a623c-121">動作項目診斷與效能監視</span><span class="sxs-lookup"><span data-stu-id="a623c-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
