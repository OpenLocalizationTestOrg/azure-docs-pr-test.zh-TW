---
title: "Reliable Actors 的動作項目類型序列化註解 | Microsoft Docs"
description: "說明定義可用於定義 Service Fabric Reliable Actors 狀態與介面其可序列化類別的基本需求"
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
ms.openlocfilehash: 4b48b893e5a3bf5620f00a336576efe1ad63def8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="d57e5-103">Service Fabric Reliable Actors 類型序列化的注意事項</span><span class="sxs-lookup"><span data-stu-id="d57e5-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="d57e5-104">所有方法的引數、動作項目介面中每個方法所傳回之工作的結果類型，以及動作項目的狀態管理員中儲存的物件都必須[可資料合約序列化](https://msdn.microsoft.com/library/ms731923.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d57e5-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="d57e5-105">這也適用於在 [動作項目事件介面](service-fabric-reliable-actors-events.md)中定義的方法引數。</span><span class="sxs-lookup"><span data-stu-id="d57e5-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="d57e5-106">(動作項目事件介面方法一律會傳回無效)。</span><span class="sxs-lookup"><span data-stu-id="d57e5-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="d57e5-107">自訂資料類型</span><span class="sxs-lookup"><span data-stu-id="d57e5-107">Custom data types</span></span>
<span data-ttu-id="d57e5-108">在此範例中，下列動作項目介面會定義一個方法，以傳回名為 `VoicemailBox` 的自訂資料類型：</span><span class="sxs-lookup"><span data-stu-id="d57e5-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="d57e5-109">此介面是由動作項目實作，其使用狀態管理員來儲存 `VoicemailBox` 物件︰</span><span class="sxs-lookup"><span data-stu-id="d57e5-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="d57e5-110">在此範例中， `VoicemailBox` 物件會在下列情況進行序列化︰</span><span class="sxs-lookup"><span data-stu-id="d57e5-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="d57e5-111">在動作項目執行個體與呼叫端之間傳輸物件。</span><span class="sxs-lookup"><span data-stu-id="d57e5-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="d57e5-112">物件已儲存在狀態管理員，以保存到磁碟並複寫到其他節點。</span><span class="sxs-lookup"><span data-stu-id="d57e5-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="d57e5-113">Reliable Actor 架構會使用 DataContract 序列化。</span><span class="sxs-lookup"><span data-stu-id="d57e5-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="d57e5-114">因此，自訂資料物件與其成員必須使用 **DataContract** 和 **DataMember** 屬性分別註解。</span><span class="sxs-lookup"><span data-stu-id="d57e5-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="d57e5-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d57e5-115">Next steps</span></span>
* [<span data-ttu-id="d57e5-116">動作項目生命週期與記憶體回收</span><span class="sxs-lookup"><span data-stu-id="d57e5-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="d57e5-117">動作項目計時器和提醒</span><span class="sxs-lookup"><span data-stu-id="d57e5-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="d57e5-118">動作項目事件</span><span class="sxs-lookup"><span data-stu-id="d57e5-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="d57e5-119">動作項目重新進入</span><span class="sxs-lookup"><span data-stu-id="d57e5-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="d57e5-120">動作項目多型和物件導向的設計模式</span><span class="sxs-lookup"><span data-stu-id="d57e5-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="d57e5-121">動作項目診斷與效能監視</span><span class="sxs-lookup"><span data-stu-id="d57e5-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
