---
title: "Service Fabric 上的 Reliable Actors | Microsoft Docs"
description: "說明 Reliable Actors 如何在 Reliable Services 上分層，以及如何使用 Service Fabric 平台的功能。"
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
ms.openlocfilehash: 0a12da52b6e74c721cd25f89e7cde3c07153a396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="3df89-103">Reliable Acto 如何使用 Service Fabric 平台</span><span class="sxs-lookup"><span data-stu-id="3df89-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="3df89-104">本文說明 Reliable Actors 在 Azure Service Fabric 平台上的運作方式。</span><span class="sxs-lookup"><span data-stu-id="3df89-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="3df89-105">Reliable Actors 會在名為*動作項目服務*的具狀態可靠服務實作上裝載的架構中執行。</span><span class="sxs-lookup"><span data-stu-id="3df89-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="3df89-106">動作項目服務包含管理生命週期和您的動作項目用於發送之訊息所需的所有元件︰</span><span class="sxs-lookup"><span data-stu-id="3df89-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="3df89-107">動作項目執行階段會管理生命週期、記憶體回收，並強制執行單一執行緒存取。</span><span class="sxs-lookup"><span data-stu-id="3df89-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="3df89-108">動作項目服務遠端處理接聽程式會接受對動作項目進行的遠端存取呼叫，並將它們傳送到發送器，以路由傳送到適當的動作項目執行個體。</span><span class="sxs-lookup"><span data-stu-id="3df89-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="3df89-109">動作項目狀態供應器會包裝狀態供應器 (例如「可靠的集合」狀態供應器)，並提供配接器來進行動作項目狀態管理。</span><span class="sxs-lookup"><span data-stu-id="3df89-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="3df89-110">這些元件一起構成 Reliable Actor 架構。</span><span class="sxs-lookup"><span data-stu-id="3df89-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="3df89-111">將服務分層</span><span class="sxs-lookup"><span data-stu-id="3df89-111">Service layering</span></span>
<span data-ttu-id="3df89-112">由於動作項目服務本身是一個 Reliable Service，因此 Reliable Services 的所有 [應用程式模型](service-fabric-application-model.md)、生命週期、[封裝](service-fabric-package-apps.md)、[部署](service-fabric-deploy-remove-applications.md)、升級及調整概念都會以相同方式套用到動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="3df89-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![將動作項目服務分層][1]

<span data-ttu-id="3df89-114">上圖顯示 Service Fabric 應用程式架構和使用者程式碼之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="3df89-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="3df89-115">藍色項目代表 Reliable Services 應用程式架構、橘色代表 Reliable Actor 架構，而綠色代表使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="3df89-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="3df89-116">在 Reliable Services 中，您的服務會繼承 `StatefulService` 類別。</span><span class="sxs-lookup"><span data-stu-id="3df89-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="3df89-117">這個類別本身是衍生自 `StatefulServiceBase` (或無狀態服務的 `StatelessService`)。</span><span class="sxs-lookup"><span data-stu-id="3df89-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="3df89-118">在 Reliable Actors 中，您會使用動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="3df89-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="3df89-119">動作項目服務是 `StatefulServiceBase` 類別的不同實作，此類別會實作動作項目執行所在的動作項目模式。</span><span class="sxs-lookup"><span data-stu-id="3df89-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="3df89-120">由於動作項目服務本身只是 `StatefulServiceBase` 的實作，因此，您可以自行撰寫衍生自 `ActorService` 的服務，並以您在繼承 `StatefulService` 時所使用的相同方式來實作服務層級功能，例如︰</span><span class="sxs-lookup"><span data-stu-id="3df89-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="3df89-121">服務備份與還原。</span><span class="sxs-lookup"><span data-stu-id="3df89-121">Service backup and restore.</span></span>
* <span data-ttu-id="3df89-122">適用於所有動作項目的共用功能，例如斷路器。</span><span class="sxs-lookup"><span data-stu-id="3df89-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="3df89-123">遠端處理程序會在動作項目服務本身，以及每個個別動作項目上進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="3df89-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="3df89-124">Java/Linux 上目前不支援具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="3df89-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="3df89-125">使用動作項目服務</span><span class="sxs-lookup"><span data-stu-id="3df89-125">Using the actor service</span></span>
<span data-ttu-id="3df89-126">動作項目執行個體具有其執行所在之動作項目服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="3df89-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="3df89-127">透過動作項目服務，動作項目執行個體可以程式設計方式取得服務內容。</span><span class="sxs-lookup"><span data-stu-id="3df89-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="3df89-128">服務內容包含分割區識別碼、服務名稱、應用程式名稱及其他 Service Fabric 平台特定的資訊：</span><span class="sxs-lookup"><span data-stu-id="3df89-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="3df89-129">就像所有 Reliable Services，動作項目服務必須在 Service Fabric 執行階段，利用某個服務類型來註冊。</span><span class="sxs-lookup"><span data-stu-id="3df89-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="3df89-130">為了讓動作項目服務執行您的動作項目執行個體，也必須向動作項目服務註冊動作項目類型。</span><span class="sxs-lookup"><span data-stu-id="3df89-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="3df89-131">`ActorRuntime` 註冊方法會替動作項目執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="3df89-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="3df89-132">在最簡單的情況下，您只需註冊動作項目類型，並隱含地使用具備預設設定的動作項目服務︰</span><span class="sxs-lookup"><span data-stu-id="3df89-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="3df89-133">或者，您可以使用註冊方法提供的 Lambda，來建構自己的動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="3df89-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="3df89-134">您可以設定動作項目服務，以及明確地建構您的動作項目執行個體，您可以透過其建構函式，將相依性插入動作項目︰</span><span class="sxs-lookup"><span data-stu-id="3df89-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="3df89-135">動作項目服務方法</span><span class="sxs-lookup"><span data-stu-id="3df89-135">Actor service methods</span></span>
<span data-ttu-id="3df89-136">動作項目服務會實作 `IActorService` (C#) 或 `ActorService` (Java)，而它會接著實作 `IService` (C#) 或 `Service` (Java)。</span><span class="sxs-lookup"><span data-stu-id="3df89-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="3df89-137">這是 Reliable Services 遠端處理功能所使用的介面，能夠在服務方法上進行遠端程序呼叫。</span><span class="sxs-lookup"><span data-stu-id="3df89-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="3df89-138">它包含的服務層級方法可使用服務遠端處理功能從遠端呼叫。</span><span class="sxs-lookup"><span data-stu-id="3df89-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="3df89-139">列舉動作項目</span><span class="sxs-lookup"><span data-stu-id="3df89-139">Enumerating actors</span></span>
<span data-ttu-id="3df89-140">動作項目服務允許用戶端列舉服務所裝載之動作項目的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3df89-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="3df89-141">因為動作項目服務是已資料分割的具狀態服務，所以會針對每個分割區執行列舉。</span><span class="sxs-lookup"><span data-stu-id="3df89-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="3df89-142">由於每個分割區可能包含許多動作項目，因此，列舉會以一組分頁式結果形式傳回。</span><span class="sxs-lookup"><span data-stu-id="3df89-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="3df89-143">頁面會以迴圈方式讀取，直到讀取所有頁面為止。</span><span class="sxs-lookup"><span data-stu-id="3df89-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="3df89-144">下列範例示範如何在動作項目服務的其中一個分割區中，建立所有作用中動作項目的清單︰</span><span class="sxs-lookup"><span data-stu-id="3df89-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="3df89-145">刪除動作項目</span><span class="sxs-lookup"><span data-stu-id="3df89-145">Deleting actors</span></span>
<span data-ttu-id="3df89-146">動作項目服務也會提供用來刪除動作項目的函式︰</span><span class="sxs-lookup"><span data-stu-id="3df89-146">The actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="3df89-147">如需刪除動作項目及其狀態的詳細資訊，請參閱[動作項目生命週期文件](service-fabric-reliable-actors-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="3df89-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="3df89-148">自訂動作項目服務</span><span class="sxs-lookup"><span data-stu-id="3df89-148">Custom actor service</span></span>
<span data-ttu-id="3df89-149">您可以使用動作項目註冊 lambda，註冊自 `ActorService` (C#) 和 `FabricActorService` (Java) 延伸的自訂動作項目服務。</span><span class="sxs-lookup"><span data-stu-id="3df89-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="3df89-150">在此自訂動作項目服務中，您可以撰寫繼承 `ActorService` (C#) 或 `FabricActorService` (Java) 的服務，以實作自己的服務層級功能。</span><span class="sxs-lookup"><span data-stu-id="3df89-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="3df89-151">自訂動作項目服務會繼承來自 `ActorService` (C#) 或 `FabricActorService` (Java) 的所有動作項目執行階段功能，並可用來實作您自己的服務方法。</span><span class="sxs-lookup"><span data-stu-id="3df89-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="3df89-152">實作動作項目備份與還原</span><span class="sxs-lookup"><span data-stu-id="3df89-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="3df89-153">在下列範例中，自訂動作項目服務會利用已經存在於 `ActorService`中的遠端處理接聽程式，藉以公開用來備份動作項目資料的方法：</span><span class="sxs-lookup"><span data-stu-id="3df89-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

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
           // store the contents of backupInfo.Directory
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
           // store the contents of backupInfo.Directory
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


<span data-ttu-id="3df89-154">在此範例中，`IMyActorService` 是遠端處理協定，它會實作 `IService` (C#) 與 `Service` (Java)，然後透過 `MyActorService` 來實作。</span><span class="sxs-lookup"><span data-stu-id="3df89-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="3df89-155">藉由新增這個遠端處理協定，透過使用 `ActorServiceProxy` 建立遠端 Proxy，`IMyActorService` 上的方法現在也可供用戶端使用：</span><span class="sxs-lookup"><span data-stu-id="3df89-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="3df89-156">應用程式模型</span><span class="sxs-lookup"><span data-stu-id="3df89-156">Application model</span></span>
<span data-ttu-id="3df89-157">動作項目服務是 Reliable Services，因此應用程式模型是一樣的。</span><span class="sxs-lookup"><span data-stu-id="3df89-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="3df89-158">不過，動作項目架構建置工具可為您產生某些應用程式模型檔案。</span><span class="sxs-lookup"><span data-stu-id="3df89-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="3df89-159">服務資訊清單</span><span class="sxs-lookup"><span data-stu-id="3df89-159">Service manifest</span></span>
<span data-ttu-id="3df89-160">動作項目架構建置工具會自動產生動作項目服務的 ServiceManifest.xml 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="3df89-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="3df89-161">此檔案包括：</span><span class="sxs-lookup"><span data-stu-id="3df89-161">This file includes:</span></span>

* <span data-ttu-id="3df89-162">動作項目服務類型。</span><span class="sxs-lookup"><span data-stu-id="3df89-162">Actor service type.</span></span> <span data-ttu-id="3df89-163">類型名稱是根據您的動作項目專案名稱來產生。</span><span class="sxs-lookup"><span data-stu-id="3df89-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="3df89-164">根據動作項目上的持續性屬性，也會據以設定 HasPersistedState 旗標。</span><span class="sxs-lookup"><span data-stu-id="3df89-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="3df89-165">程式碼封裝。</span><span class="sxs-lookup"><span data-stu-id="3df89-165">Code package.</span></span>
* <span data-ttu-id="3df89-166">組態封裝。</span><span class="sxs-lookup"><span data-stu-id="3df89-166">Config package.</span></span>
* <span data-ttu-id="3df89-167">資源和端點。</span><span class="sxs-lookup"><span data-stu-id="3df89-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="3df89-168">應用程式資訊清單</span><span class="sxs-lookup"><span data-stu-id="3df89-168">Application manifest</span></span>
<span data-ttu-id="3df89-169">動作項目架構建置工具會自動建立適用於您動作項目服務的預設服務定義。</span><span class="sxs-lookup"><span data-stu-id="3df89-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="3df89-170">建置工具會填入預設服務屬性︰</span><span class="sxs-lookup"><span data-stu-id="3df89-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="3df89-171">複本集數量取決於動作項目上的持續性屬性。</span><span class="sxs-lookup"><span data-stu-id="3df89-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="3df89-172">每當動作項目上的持續性屬性變更時，預設服務定義中的複本集數量會據以重設。</span><span class="sxs-lookup"><span data-stu-id="3df89-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="3df89-173">分割區配置和範圍會利用完整的 Int64 索引鍵範圍設定為「平均的 Int64 」。</span><span class="sxs-lookup"><span data-stu-id="3df89-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="3df89-174">動作項目的 Service Fabric 資料分割概念</span><span class="sxs-lookup"><span data-stu-id="3df89-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="3df89-175">動作項目服務是已資料分割的具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="3df89-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="3df89-176">動作項目服務的每個分割區都包含一組動作項目。</span><span class="sxs-lookup"><span data-stu-id="3df89-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="3df89-177">服務分割區會自動散佈於 Service Fabric 中的多個節點上。</span><span class="sxs-lookup"><span data-stu-id="3df89-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="3df89-178">結果就是散佈動作項目執行個體。</span><span class="sxs-lookup"><span data-stu-id="3df89-178">Actor instances are distributed as a result.</span></span>

![動作項目的資料分割和散佈][5]

<span data-ttu-id="3df89-180">您可以使用不同的分割區配置和分割區索引鍵範圍來建立 Reliable Services。</span><span class="sxs-lookup"><span data-stu-id="3df89-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="3df89-181">動作項目服務會搭配完整的 Int64 索引鍵範圍使用 Int64 資料分割配置，來將動作項目對應到分割區。</span><span class="sxs-lookup"><span data-stu-id="3df89-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="3df89-182">動作項目識別碼</span><span class="sxs-lookup"><span data-stu-id="3df89-182">Actor ID</span></span>
<span data-ttu-id="3df89-183">服務中建立的每個動作項目都具有與它相關聯的唯一識別碼，由 `ActorId` 類別來表示。</span><span class="sxs-lookup"><span data-stu-id="3df89-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="3df89-184">`ActorId` 是不透明的識別碼值，可藉由產生隨機識別碼，在服務分割區上平均散佈動作項目。</span><span class="sxs-lookup"><span data-stu-id="3df89-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="3df89-185">每個 `ActorId` 雜湊為 int64。</span><span class="sxs-lookup"><span data-stu-id="3df89-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="3df89-186">這就是為什麼動作項目服務必須搭配完整的 Int64 索引鍵範圍使用 Int64 資料分割配置的原因。</span><span class="sxs-lookup"><span data-stu-id="3df89-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="3df89-187">不過，自訂識別碼值可用於 `ActorID`，包括 GUID/UUID、字串和 Int64。</span><span class="sxs-lookup"><span data-stu-id="3df89-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="3df89-188">您使用 GUID/UUID 和字串時，已將值雜湊為 Int64。</span><span class="sxs-lookup"><span data-stu-id="3df89-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="3df89-189">不過，在您將 Int64 明確提供給 `ActorId`之前，Int64 將會直接對應到分割區，而不需進一步雜湊。</span><span class="sxs-lookup"><span data-stu-id="3df89-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="3df89-190">您可以使用這項技術控制要將動作項目放置於哪個分割區。</span><span class="sxs-lookup"><span data-stu-id="3df89-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3df89-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3df89-191">Next steps</span></span>
* [<span data-ttu-id="3df89-192">動作項目狀態管理</span><span class="sxs-lookup"><span data-stu-id="3df89-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="3df89-193">動作項目生命週期與記憶體回收</span><span class="sxs-lookup"><span data-stu-id="3df89-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="3df89-194">動作項目 API 參考文件</span><span class="sxs-lookup"><span data-stu-id="3df89-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="3df89-195">.NET 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="3df89-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="3df89-196">Java 範例程式碼 (英文)</span><span class="sxs-lookup"><span data-stu-id="3df89-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
