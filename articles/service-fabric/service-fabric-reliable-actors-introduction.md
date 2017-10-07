---
title: "aaaService 網狀架構可靠的動作項目概觀 |Microsoft 文件"
description: "簡介 toohello 服務網狀架構 Reliable Actors 程式撰寫模型。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>簡介 tooService 網狀架構 Reliable Actors
Reliable Actors 是根據 hello Service Fabric 應用程式架構[Virtual Actor](http://research.microsoft.com/en-us/projects/orleans/)模式。 hello 可靠的執行者 API 提供了單一執行緒程式撰寫模型之上 hello 延展性和可靠性保證服務網狀架構所提供。

## <a name="what-are-actors"></a>什麼是動作項目？
動作項目是隔離且獨立的計算與狀態單位，且具備單一執行緒執行。 hello [actor 模式](https://en.wikipedia.org/wiki/Actor_model)是並行或分散式系統中的大量的這些執行者可以同時執行，以及各自的運算模型。 動作項目可以彼此通訊，而且可以建立多個動作項目。

### <a name="when-toouse-reliable-actors"></a>當 toouse Reliable Actors
服務網狀架構 Reliable Actors 是 hello 執行者設計模式的實作。 如同任何軟體設計模式中，是否 toouse 特定的模式會根據軟體設計問題 hello 決策符合 hello 模式。

雖然 hello 執行者設計模式可以是很好的調整的 tooa 許多分散式的系統問題及案例、 仔細地考量 hello hello 模式和 hello 架構實作必須進行的條件約束。 做為一般的指導，請考慮 hello actor 模式 toomodel 您的問題或案例如果：

* 您的問題領域涉及大量 (數千個或更多) 小型、獨立且隔離的狀態和邏輯單位。
* 您想使用單一執行緒的物件不需要重大的互動，舉凡外部元件，包括跨的執行者集合查詢狀態 toowork。
* 您的動作項目執行個體將不會藉由發出 I/O 作業，使用無法預期的延遲來封鎖呼叫端。

## <a name="actors-in-service-fabric"></a>Service Fabric 中的動作項目
在 Service Fabric 動作項目會實作在 hello Reliable Actors framework： 動作項目模式的應用程式架構之上[Service Fabric 可靠服務](service-fabric-reliable-services-introduction.md)。 您撰寫的每個 Reliable Actor 服務實際上都是已資料分割的具狀態可靠服務。

每個動作項目定義為動作項目類型的執行個體，相同 toohello 方式.NET 物件的.NET 型別執行個體。 例如，可能實作計算機 hello 功能動作項目類型，可能是該類型的不同節點分散叢集的許多參與者。 每一個這類的動作項目都有唯一的動作項目識別碼識別。

### <a name="actor-lifetime"></a>動作項目生命週期
Service Fabric 動作項目都是虛擬的這表示它們的存留時間不繫結的 tootheir 記憶體中表示。 如此一來，不需要 toobe 明確建立或終結。 hello Reliable Actors 執行階段會自動啟動動作項目 hello 第一次收到要求的動作項目 id。 如果動作項目不是一段時間，hello Reliable Actors 執行階段記憶體回收-收集 hello 記憶體內部物件。 它也會維護知識的動作項目 hello 存在應該需要 toobe 稍後重新啟動。 如需詳細資訊，請參閱 [動作項目生命週期與記憶體回收](service-fabric-reliable-actors-lifecycle.md)。

這個虛擬動作項目存留期抽象層通訊 hello 虛擬執行者模型，因為某些注意事項，且事實上 hello Reliable Actors 實作偏離有時候這種模型。

* 動作項目會自動啟動 （導致動作項目建構的物件 toobe） hello 第一次將訊息傳送 tooits 動作項目識別碼。 在一段時間之後, hello 動作項目物件是記憶體回收。 Hello 在未來，同樣地，使用 hello 動作項目識別碼可能會建構物件 toobe 新動作項目。 動作項目狀態存留時間超過 hello 物件的存留時間會儲存在 hello 狀態管理員時。
* 針對動作項目識別碼呼叫任何動作項目方法都會啟動該動作項目。 基於這個理由，動作項目類型都有由 hello 執行階段隱含地呼叫其建構函式。 因此，用戶端程式碼無法成功參數 toohello 動作項目類型的建構函式，雖然參數可能會依據 hello 服務本身傳遞 toohello 執行者建構函式。 hello 結果是，執行者可能會建構部分初始化的狀態，在呼叫其他方法的 hello 時間如果 hello 動作項目需要從 hello 用戶端的初始化參數。 沒有 hello 啟動動作項目從 hello 用戶端的單一進入點。
* 雖然 Reliable Actors 會隱含地建立動作項目物件。您沒有 hello 能力 tooexplicitly 刪除動作項目和其狀態。

### <a name="distribution-and-failover"></a>散佈和容錯移轉
Service Fabric tooprovide 延展性和可靠性，分散執行者整個 hello 叢集並自動將它們從失敗的節點 toohealthy 的視需要移轉。 這是 [已資料分割的具狀態可靠服務](service-fabric-concepts-partitioning.md)上的一個抽象概念。 發佈、 延展性、 可靠性和自動容錯移轉所有提供必定 hello 事實內呼叫 hello 可設定狀態 Reliable Service 執行執行者*Actor 服務*。

執行者會分散到 hello 的 hello 行動服務的資料分割，分割區區的分散於 hello Service Fabric 叢集中的節點。 每個服務分割區都會包含一組動作項目。 Service Fabric 管理分散和容錯移轉的 hello 服務資料分割。

例如，具有 9 個資料分割的行動服務部署的 toothree 使用 hello 預設動作項目資料分割的位置節點會據此分散式：

![Reliable Actors 散佈][2]

hello 執行者架構會管理您的資料分割配置和索引鍵範圍設定。 這會簡化一些選項，但也會帶來一些考量︰

* 可靠的服務可讓您 toochoose 資料分割配置，索引鍵的範圍 （當使用資料分割配置的範圍），以及資料分割計數。 Reliable Actors 限制的 toohello 範圍的資料分割配置 （hello 統一 Int64 配置），而且需要使用 hello 完整 Int64 範圍。
* 根據預設，動作項目會隨機放入分割區，形成平均散佈的結果。
* 由於動作項目是隨機放置的，所以應該預期動作項目作業一律需要網路通訊，包括方法呼叫資料的序列化和還原序列化，因而導致延遲和額外負荷。
* 在進階案例中，很可能 toocontrol 動作項目資料分割配置使用 Int64 執行者 toospecific 資料分割對應的識別碼。 不過，這樣做會導致動作項目以不對稱方式散佈於分割區上。

如需有關如何資料分割動作項目服務的詳細資訊，請參閱太[分割概念的執行者](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors)。

### <a name="actor-communication"></a>動作項目通訊
執行者互動的介面，實作 hello 介面 hello 執行者與 hello 用戶端取得 proxy tooan 執行者 hello 透過共用中定義相同的介面。 這個介面會以非同步的方式是使用的 tooinvoke 執行者方法，因為 hello 介面上的每個方法必須傳回工作。

方法引動過程和它們對回應最後會導致在網路要求跨 hello 叢集，因此 hello 引數和傳回必須可序列化 hello 平台的 hello 工作 hello 結果類型。 特別是，它們必須是 [資料合約序列化](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)。

#### <a name="hello-actor-proxy"></a>hello 執行者 proxy
hello Reliable Actors 用戶端應用程式開發介面提供動作項目執行個體與行動用戶端之間的通訊。 與 actor toocommunicate，用戶端會建立實作 hello 執行者介面執行者 proxy 物件。 hello 用戶端會與 hello 執行者互動 hello proxy 物件上的叫用方法。 hello 執行者 proxy 可用於用戶端以動作項目和動作項目以動作項目通訊。

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


請注意，hello 兩項資訊會使用 toocreate hello 執行者 proxy 物件是 hello 動作項目識別碼和 hello 應用程式名稱。 hello 動作項目識別碼可唯一識別 hello 動作項目，雖然 hello 應用程式名稱會識別 hello [Service Fabric 應用程式](service-fabric-reliable-actors-platform.md#application-model)hello 動作項目部署的位置。

hello `ActorProxy`(C#) / `ActorProxyBase`hello 用戶端 (Java) 類別執行 hello 需要解析 toolocate hello 動作項目識別碼，並使用它開啟的通訊通道。 它也會重試 toolocate hello 動作項目在 hello 的通訊失敗和容錯移轉的情況下。 如此一來，訊息傳遞具有下列特性的 hello:

* 最好進行訊息傳遞。
* 動作項目可能會收到 hello 重複的訊息相同的用戶端。

### <a name="concurrency"></a>並行
hello Reliable Actors 執行階段會提供簡單開啟為基礎的存取模型的存取動作方法。 這表示動作項目物件代碼內永遠只能有一個執行緒為使用中。 回合式存取會大幅簡化並行系統，因為不需要使用同步機制來進行資料存取。 這也表示系統必須設計成與 hello 單一執行緒存取的情況，每個動作項目執行個體的特殊考量。

* 單一動作項目執行個體無法一次處理一個以上的要求。 動作項目執行個體可能會造成的輸送量瓶頸，如果預期的 toohandle 並行要求。
* 如果外部的要求會同時進行的 hello 執行者 tooone 時的兩個執行者之間的循環的要求，另一方動作項目可能會發生死結。 hello 動作項目執行階段會自動動作項目上的逾時的時間呼叫，並擲回例外狀況 toohello 呼叫端 toointerrupt 發生死結狀況。

![Reliable Actors 通訊][3]

#### <a name="turn-based-access"></a>回合式存取
開啟包含 hello 完成執行的動作項目中的方法從其他執行者或用戶端的回應 tooa 要求或 hello 完整執行[計時器/提醒](service-fabric-reliable-actors-timers-reminders.md)回呼。 雖然這些方法和回呼是非同步，hello 執行者執行階段不會不會交錯它們。 必須完整完成一個回合，才能允許進行下一回合。 換句話說，目前正在執行的動作項目方法或計時器/提醒回呼必須是完全完成新的呼叫 tooa 方法之前，或允許回呼。 方法或回撥會被視為 toohave 完成如果 hello 方法已傳回 hello 執行或回呼和 hello hello 方法或回撥所傳回的工作已完成。 值得強調的是，即使是在不同的方法、計時器與回呼之間，仍會遵守回合式並行。

hello 執行者執行階段，便會強制關閉並行輪流 hello 開頭處取得每個動作項目鎖定並釋放結尾 hello hello hello 鎖定開啟。 因此，回合式並行會依各個動作項目強制執行，不會在動作項目之間強制執行。 動作項目方法和計時器/提醒回撥可代表不同的動作項目同時執行。

hello 下列範例將說明上述概念 hello。 如果有一個動作項目類型實作兩個非同步方法 (假設為 Method1 與 Method2)，也就是計時器與提醒。 hello 圖顯示以 hello 執行這些方法和回呼代表兩個動作項目以時間表的範例 (*ActorId1*和*ActorId2*) 隸屬 toothis 動作項目類型。

![Reliable Actors 執行階段回合式並行和存取][1]

此圖遵循下列慣例：

* 每個垂直行顯示 hello 邏輯的執行流程方法或回呼代表特定的動作項目。
* 依時間先後順序，會出現較新的事件發生以下較舊的 hello 標示每個垂直行上的事件。
* 時間表對應 toodifferent 執行者會使用不同的色彩。
* 反白顯示為使用的 tooindicate hello 持續時間的 hello 每個動作項目鎖定代表方法或回呼。

一些重點 tooconsider:

* 雖然*Method1*執行代表*ActorId2*回應 tooclient 要求中*xyz789*，另一個用戶端要求 (*abc123*)到達時，也需要*Method1* toobe 執行者*ActorId2*。 不過，hello 的第二次執行*Method1* hello 之前執行完成之前不會開始。 同樣地，好提醒您註冊*ActorId2*時引發*Method1*是否正以回應 tooclient 要求執行*xyz789*。 hello 提醒執行回呼的這兩個執行後才*Method1*都已完成。 這是因為 tooturn 為基礎的強制執行的並行存取*ActorId2*。
* 開啟並行也同樣地，強制針對*ActorId1*hello 執行所示*Method1*， *Method2*，和 hello 代表計時器回呼*ActorId1*以序列方式發生。
* 代表 ActorId1 執行 Method1 與代表 ActorId2 執行重疊。 這是因為回合式並行只會在動作項目內強制執行，不會在動作項目間強制執行。
* 在某些 hello/回呼方法執行的 hello `Task`(C#) / `CompletableFuture`(Java) 傳回 hello/回呼方法完成之後 hello 方法會傳回。 在某些其他 hello 非同步作業已經完成 hello hello 方法/回呼傳回的時間。 在這兩種情況下，這兩個 hello 方法/回呼傳回和 hello 非同步作業完成之後，才會釋放 hello 每個動作項目鎖定。

#### <a name="reentrancy"></a>重新進入
hello 執行者執行階段預設允許重新進入。 這表示，如果執行者方法*動作項目 A*上呼叫方法*動作項目 B*，接著呼叫另一個方法上*動作項目 A*，toorun 允許方法。 這是因為它屬於 hello 的相同邏輯的呼叫鏈結的內容。 所有的計時器佇列與提醒呼叫 hello 新邏輯呼叫內容的開頭。 請參閱 hello [Reliable Actors 重新進入](service-fabric-reliable-actors-reentrancy.md)如需詳細資訊。

#### <a name="scope-of-concurrency-guarantees"></a>並行保證的範圍
hello 執行者執行階段提供這些並行保證在其中它所控制的這些方法的引動過程 hello 的情況下。 例如，它會提供這些保證 hello 方法引動過程會在回應 tooa 用戶端要求中完成，以及計時器和提示的回呼。 不過，如果 hello 行動程式碼直接叫用這些方法之外 hello hello 執行者執行階段所提供的機制，然後 hello 執行階段無法提供任何並行保證。 例如，如果 hello 方法會叫用 hello 內容未與 hello 執行者方法所傳回的 hello 工作相關聯的某些工作中，然後 hello 執行階段無法提供並行保證。 如果 hello 方法從執行緒叫用該 hello 動作項目會建立其本身，則 hello 執行階段也無法提供並行的保證。 因此，tooperform 背景作業，動作項目應該使用[執行者計時器和執行者提醒](service-fabric-reliable-actors-timers-reminders.md)，尊重開啟基礎的並行存取。

## <a name="next-steps"></a>後續步驟
* 從建置您的第一個 Reliable Actors 服務開始著手：
   * [開始在 .NET 上使用 Reliable Actors](service-fabric-reliable-actors-get-started.md)
   * [開始在 Java 上使用 Reliable Actors](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
