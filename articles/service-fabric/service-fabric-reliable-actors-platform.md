---
title: "aaaReliable 上 Service Fabric 動作項目 |Microsoft 文件"
description: "描述如何 Reliable Actors 的分層上可靠的服務，並使用 hello hello Service Fabric 平台功能。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="a7fd9-103">Reliable Actors 使用 hello Service Fabric 平台的方式</span><span class="sxs-lookup"><span data-stu-id="a7fd9-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="a7fd9-104">本文說明 Reliable Actors hello Azure Service Fabric 平台上的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="a7fd9-105">位於呼叫 hello 可設定狀態可靠的服務實作的架構中執行 reliable Actors *actor 服務*。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="a7fd9-106">hello actor 服務包含所有 hello 元件所需的 toomanage hello 生命週期和訊息發送您的動作項目：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="a7fd9-107">hello 動作項目執行階段生命週期，記憶體回收，並強制執行單一執行緒存取。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="a7fd9-108">動作項目服務遠端接聽程式接受遠端存取呼叫 tooactors，並將它們傳送 tooa 發送器 tooroute toohello 適當的動作項目執行個體。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="a7fd9-109">hello 動作項目狀態提供者會包裝狀態提供者 （例如 hello 可靠集合狀態提供者），並提供動作項目狀態管理的介面卡。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="a7fd9-110">這些元件一起表單 hello Reliable Actor 架構。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="a7fd9-111">將服務分層</span><span class="sxs-lookup"><span data-stu-id="a7fd9-111">Service layering</span></span>
<span data-ttu-id="a7fd9-112">Hello actor 服務本身是可靠的服務，因為所有 hello[應用程式模型](service-fabric-application-model.md)，生命週期，[封裝](service-fabric-package-apps.md)，[部署](service-fabric-deploy-remove-applications.md)、 升級和縮放比例的概念可靠的服務套用 hello tooactor 服務相同方式。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![將動作項目服務分層][1]

<span data-ttu-id="a7fd9-114">hello 上圖顯示 hello hello Service Fabric 應用程式架構和使用者程式碼之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="a7fd9-115">藍色項目代表 hello 可靠的服務應用程式架構、 橙色代表 hello Reliable Actor 架構，而綠色代表使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="a7fd9-116">可靠的服務，在您的服務會繼承 hello`StatefulService`類別。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="a7fd9-117">這個類別本身是衍生自 `StatefulServiceBase` (或無狀態服務的 `StatelessService`)。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="a7fd9-118">中可靠的動作項目，您可以使用 hello 動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="a7fd9-119">hello actor 服務是 hello 的不同實作`StatefulServiceBase`類別實作 hello actor 模式執行您的動作項目。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="a7fd9-120">因為 hello actor 服務本身是實作的`StatefulServiceBase`，您可以撰寫您自己的服務衍生自`ActorService`和實作服務層級功能 hello 相同的方式進行繼承時`StatefulService`，例如：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="a7fd9-121">服務備份與還原。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-121">Service backup and restore.</span></span>
* <span data-ttu-id="a7fd9-122">適用於所有動作項目的共用功能，例如斷路器。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="a7fd9-123">Hello actor 服務本身和每個個別的動作項目上的遠端程序呼叫。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="a7fd9-124">Java/Linux 上目前不支援具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="a7fd9-125">使用 hello 行動服務</span><span class="sxs-lookup"><span data-stu-id="a7fd9-125">Using hello actor service</span></span>
<span data-ttu-id="a7fd9-126">動作項目執行個體具有存取 toohello 行動服務執行所在。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="a7fd9-127">透過 hello 行動服務，動作項目執行個體可以透過程式設計方式取得 hello 服務內容。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="a7fd9-128">hello 服務內容具有 hello 分割區識別碼、 服務名稱、 應用程式名稱和其他 Service Fabric 平台特定的資訊：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="a7fd9-129">如同所有可靠的服務，hello actor 服務必須向 hello Service Fabric 執行階段中的服務類型。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="a7fd9-130">Hello actor 服務 toorun 您的動作項目執行個體，也必須註冊動作項目類型與 hello 動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="a7fd9-131">hello`ActorRuntime`註冊方法為執行者執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="a7fd9-132">在 hello 最簡單的情況下，您就可以註冊您的動作項目類型和 hello actor 服務以預設設定將會隱含使用：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="a7fd9-133">或者，您可以使用服務所提供的 hello 註冊方法 tooconstruct hello 執行者自行 lambda。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="a7fd9-134">您可以再設定 hello 行動服務，並明確建構您的動作項目執行個體，您可以在其中插入透過其建構函式的相依性 tooyour 動作項目：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="a7fd9-135">動作項目服務方法</span><span class="sxs-lookup"><span data-stu-id="a7fd9-135">Actor service methods</span></span>
<span data-ttu-id="a7fd9-136">hello 行動服務會實作`IActorService`(C#) 或`ActorService`(Java)，它接著會實作`IService`(C#) 或`Service`(Java)。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="a7fd9-137">這是可靠的服務遠端處理，可讓服務方法的遠端程序呼叫所使用的 hello 介面。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="a7fd9-138">它包含的服務層級方法可使用服務遠端處理功能從遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="a7fd9-139">列舉動作項目</span><span class="sxs-lookup"><span data-stu-id="a7fd9-139">Enumerating actors</span></span>
<span data-ttu-id="a7fd9-140">hello 行動服務可讓用戶端 hello 執行者 hello 服務裝載 tooenumerate 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="a7fd9-141">因為 hello 行動服務資料分割的可設定狀態服務，執行列舉作業每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="a7fd9-142">因為每個資料分割可能包含許多參與者，以一組分頁式結果傳回 hello 列舉型別。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="a7fd9-143">hello 頁面被迴圈，直到讀取所有頁面。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="a7fd9-144">下列範例會示範如何 hello toocreate 行動服務的一個資料分割中的所有作用中執行者的清單：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="a7fd9-145">刪除動作項目</span><span class="sxs-lookup"><span data-stu-id="a7fd9-145">Deleting actors</span></span>
<span data-ttu-id="a7fd9-146">hello actor 服務也提供函式刪除動作項目：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-146">hello actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="a7fd9-147">如需有關刪除動作項目和其狀態的詳細資訊，請參閱 hello[執行者生命週期的文件](service-fabric-reliable-actors-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="a7fd9-148">自訂動作項目服務</span><span class="sxs-lookup"><span data-stu-id="a7fd9-148">Custom actor service</span></span>
<span data-ttu-id="a7fd9-149">您可以藉由使用 hello 執行者註冊 lambda，註冊您自己的自訂動作項目服務衍生自`ActorService`(C#) 和`FabricActorService`(Java)。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="a7fd9-150">在此自訂動作項目服務中，您可以撰寫繼承 `ActorService` (C#) 或 `FabricActorService` (Java) 的服務，以實作自己的服務層級功能。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="a7fd9-151">自訂動作項目服務繼承所有 hello 動作項目執行階段功能，從`ActorService`(C#) 或`FabricActorService`(Java) 而且可以使用的 tooimplement 您自己的服務方法。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
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
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="a7fd9-152">實作動作項目備份與還原</span><span class="sxs-lookup"><span data-stu-id="a7fd9-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="a7fd9-153">在下列範例的 hello，hello 自訂動作項目服務所公開執行者資料備份方法 tooback 透過 hello 遠端接聽程式中已有運用`ActorService`:</span><span class="sxs-lookup"><span data-stu-id="a7fd9-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="a7fd9-154">在此範例中，`IMyActorService` 是遠端處理協定，它會實作 `IService` (C#) 與 `Service` (Java)，然後透過 `MyActorService` 來實作。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="a7fd9-155">加上這個遠端服務合約，而方法`IMyActorService`現在也是可用 tooa 用戶端藉由建立透過遠端 proxy `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="a7fd9-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="a7fd9-156">應用程式模型</span><span class="sxs-lookup"><span data-stu-id="a7fd9-156">Application model</span></span>
<span data-ttu-id="a7fd9-157">動作項目服務是可靠的服務，因此 hello 應用程式模型是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="a7fd9-158">不過，hello 執行者 framework 建置工具讓您有產生部分 hello 應用程式模型檔案。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="a7fd9-159">服務資訊清單</span><span class="sxs-lookup"><span data-stu-id="a7fd9-159">Service manifest</span></span>
<span data-ttu-id="a7fd9-160">hello 執行者 framework 建置工具自動產生 hello 行動服務的 ServiceManifest.xml 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="a7fd9-161">此檔案包括：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-161">This file includes:</span></span>

* <span data-ttu-id="a7fd9-162">動作項目服務類型。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-162">Actor service type.</span></span> <span data-ttu-id="a7fd9-163">hello 型別名稱會產生以動作項目的專案名稱為基礎。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="a7fd9-164">根據您的動作項目上的 hello 持續性屬性，hello HasPersistedState 旗標會也隨之設定。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="a7fd9-165">程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-165">Code package.</span></span>
* <span data-ttu-id="a7fd9-166">組態封裝。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-166">Config package.</span></span>
* <span data-ttu-id="a7fd9-167">資源和端點。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="a7fd9-168">應用程式資訊清單</span><span class="sxs-lookup"><span data-stu-id="a7fd9-168">Application manifest</span></span>
<span data-ttu-id="a7fd9-169">hello 執行者 framework 建置工具自動建立您的行動服務的預設服務定義。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="a7fd9-170">hello 建置工具填入 hello 預設服務屬性：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="a7fd9-171">複本集計數取決於您的動作項目上的 hello 持續性屬性。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="a7fd9-172">在您的動作項目上的每個時間 hello 持續性屬性變更時，會據以重設 hello 預設服務定義中的 hello 複本集計數。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="a7fd9-173">資料分割配置和範圍會設定 tooUniform Int64 hello 完整 Int64 範圍。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="a7fd9-174">動作項目的 Service Fabric 資料分割概念</span><span class="sxs-lookup"><span data-stu-id="a7fd9-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="a7fd9-175">動作項目服務是已資料分割的具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="a7fd9-176">動作項目服務的每個分割區都包含一組動作項目。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="a7fd9-177">服務分割區會自動散佈於 Service Fabric 中的多個節點上。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="a7fd9-178">結果就是散佈動作項目執行個體。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-178">Actor instances are distributed as a result.</span></span>

![動作項目的資料分割和散佈][5]

<span data-ttu-id="a7fd9-180">您可以使用不同的分割區配置和分割區索引鍵範圍來建立 Reliable Services。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="a7fd9-181">hello 行動服務會使用 hello 完整 Int64 關鍵範圍 toomap 執行者 toopartitions hello Int64 資料分割配置。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="a7fd9-182">動作項目識別碼</span><span class="sxs-lookup"><span data-stu-id="a7fd9-182">Actor ID</span></span>
<span data-ttu-id="a7fd9-183">每個動作建立 hello 服務中的項目具有與它所 hello 表示相關聯的唯一識別碼`ActorId`類別。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="a7fd9-184">`ActorId`是不透明的識別碼值，可用於執行者統一分佈在 hello 服務資料分割之間產生隨機識別碼：</span><span class="sxs-lookup"><span data-stu-id="a7fd9-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="a7fd9-185">每個`ActorId`是雜湊的 tooan Int64。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="a7fd9-186">這就是為什麼 hello actor 服務必須使用 hello 完整 Int64 範圍的 Int64 資料分割配置。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="a7fd9-187">不過，自訂識別碼值可用於 `ActorID`，包括 GUID/UUID、字串和 Int64。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="a7fd9-188">當您使用的 Guid/Uuid 和字串 hello 值會是雜湊的 tooan Int64。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="a7fd9-189">不過，當您明確地提供 Int64 tooan `ActorId`，hello Int64 會對應直接 tooa 資料分割而不進一步雜湊。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="a7fd9-190">您可以使用這個技巧 toocontrol 分割 hello 執行者會放在其中。</span><span class="sxs-lookup"><span data-stu-id="a7fd9-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7fd9-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7fd9-191">Next steps</span></span>
* [<span data-ttu-id="a7fd9-192">動作項目狀態管理</span><span class="sxs-lookup"><span data-stu-id="a7fd9-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="a7fd9-193">動作項目生命週期與記憶體回收</span><span class="sxs-lookup"><span data-stu-id="a7fd9-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="a7fd9-194">動作項目 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="a7fd9-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="a7fd9-195">.NET 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="a7fd9-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="a7fd9-196">Java 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="a7fd9-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
