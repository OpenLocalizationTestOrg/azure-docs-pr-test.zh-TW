---
title: "aaaReliable 服務通訊的概觀 |Microsoft 文件"
description: "模型的概觀 hello 可靠的服務通訊，包括服務上的開啟接聽程式、 解決端點和服務之間進行通訊。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="068e8-103">如何 toouse hello 可靠的服務通訊的應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="068e8-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="068e8-104">「Azure Service Fabric 即平台」完全不受服務間的通訊影響。</span><span class="sxs-lookup"><span data-stu-id="068e8-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="068e8-105">所有通訊協定和堆疊是可接受的從 UDP tooHTTP。</span><span class="sxs-lookup"><span data-stu-id="068e8-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="068e8-106">是由 toohello 服務開發人員 toochoose 服務應該之間的通訊方式。</span><span class="sxs-lookup"><span data-stu-id="068e8-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="068e8-107">hello 可靠的服務應用程式架構提供的內建通訊堆疊 Api，您可以使用 toobuild 以及自訂通訊元件。</span><span class="sxs-lookup"><span data-stu-id="068e8-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="068e8-108">設定服務通訊</span><span class="sxs-lookup"><span data-stu-id="068e8-108">Set up service communication</span></span>
<span data-ttu-id="068e8-109">hello 可靠的服務應用程式開發介面會用來進行服務通訊的一個簡單的介面。</span><span class="sxs-lookup"><span data-stu-id="068e8-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="068e8-110">tooopen 的端點，您的服務，只需實作此介面：</span><span class="sxs-lookup"><span data-stu-id="068e8-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="068e8-111">然後，您可以在服務基底類別方法覆寫項中傳回您的通訊接聽程式實作來新增該實作。</span><span class="sxs-lookup"><span data-stu-id="068e8-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="068e8-112">對於無狀態服務：</span><span class="sxs-lookup"><span data-stu-id="068e8-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="068e8-113">對於具狀態服務：</span><span class="sxs-lookup"><span data-stu-id="068e8-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="068e8-114">Java 中尚未支援具狀態 Reliable Services。</span><span class="sxs-lookup"><span data-stu-id="068e8-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="068e8-115">在這兩種情況下，您會傳回接聽程式的集合。</span><span class="sxs-lookup"><span data-stu-id="068e8-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="068e8-116">這樣服務 toolisten 上多個端點，可能需要使用不同的通訊協定，使用多個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="068e8-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="068e8-117">例如，您可能有 HTTP 接聽程式和個別的 WebSocket 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="068e8-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="068e8-118">每個接聽程式會取得名稱和 hello 產生集合*名稱： 位址*組會表示為 JSON 物件，當用戶端要求的服務執行個體或資料分割的 hello 接聽位址。</span><span class="sxs-lookup"><span data-stu-id="068e8-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="068e8-119">無狀態服務，在 hello 覆寫會傳回 ServiceInstanceListeners 的集合。</span><span class="sxs-lookup"><span data-stu-id="068e8-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="068e8-120">A`ServiceInstanceListener`包含函式 toocreate`ICommunicationListener(C#) / CommunicationListener(Java)`並給予名稱。</span><span class="sxs-lookup"><span data-stu-id="068e8-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="068e8-121">可設定狀態服務，hello 覆寫會傳回 ServiceReplicaListeners 的集合。</span><span class="sxs-lookup"><span data-stu-id="068e8-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="068e8-122">這是稍有不同的無狀態的對應項目，因為`ServiceReplicaListener`具有選項 tooopen`ICommunicationListener`次要複本上。</span><span class="sxs-lookup"><span data-stu-id="068e8-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="068e8-123">您不僅可以在服務中使用多個通訊接聽程式，也可以指定哪些接聽程式要在次要複本上接受要求，以及哪些接聽程式只在主要複本上進行接聽。</span><span class="sxs-lookup"><span data-stu-id="068e8-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="068e8-124">例如，您可以有一個只在主要複本上接受 RPC 呼叫的 ServiceRemotingListener，以及一個透過 HTTP 在次要複本上接受讀取要求的第二、自訂接聽程式：</span><span class="sxs-lookup"><span data-stu-id="068e8-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="068e8-125">建立服務的多個接聽程式時， **必須** 為每個接聽程式提供唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="068e8-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="068e8-126">最後，描述 hello 端點所需的 hello 中的 hello 服務[服務資訊清單](service-fabric-application-model.md)端點上的 [hello] 區段下方。</span><span class="sxs-lookup"><span data-stu-id="068e8-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="068e8-127">hello 通訊接聽程式可以存取 hello endpoint 資源從 hello 配置 tooit`CodePackageActivationContext`在 hello `ServiceContext`。</span><span class="sxs-lookup"><span data-stu-id="068e8-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="068e8-128">hello 接聽程式可以開始開啟時，接聽要求。</span><span class="sxs-lookup"><span data-stu-id="068e8-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="068e8-129">端點資源一般的 toohello 整個服務套件，與 hello 服務封裝啟動時，由 Service Fabric 配置它們。</span><span class="sxs-lookup"><span data-stu-id="068e8-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="068e8-130">多個服務複本裝載於共用相同的 ServiceHost hello hello 相同連接埠。</span><span class="sxs-lookup"><span data-stu-id="068e8-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="068e8-131">這表示該 hello 通訊接聽程式應支援連接埠共用。</span><span class="sxs-lookup"><span data-stu-id="068e8-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="068e8-132">hello 建議產生 hello 接聽位址時，這種方式，是 hello 通訊接聽程式 toouse hello 分割區識別碼和複本/執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="068e8-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="068e8-133">服務位址註冊</span><span class="sxs-lookup"><span data-stu-id="068e8-133">Service address registration</span></span>
<span data-ttu-id="068e8-134">系統服務呼叫 hello*命名服務*Service Fabric 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="068e8-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="068e8-135">hello 命名服務是服務和其每個執行個體或複本 hello 服務正在接聽的位址註冊機構。</span><span class="sxs-lookup"><span data-stu-id="068e8-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="068e8-136">當 hello`OpenAsync(C#) / openAsync(Java)`方法`ICommunicationListener(C#) / CommunicationListener(Java)`完成時，其傳回值取得 hello 命名服務中註冊。</span><span class="sxs-lookup"><span data-stu-id="068e8-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="068e8-137">這會傳回值，取得已發行在 hello 命名服務是的字串，其值可完全是任何項目。</span><span class="sxs-lookup"><span data-stu-id="068e8-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="068e8-138">此字串值是用戶端時，看到他們要求的 hello 命名服務的 hello 服務地址。</span><span class="sxs-lookup"><span data-stu-id="068e8-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="068e8-139">Service Fabric 提供 Api，可讓用戶端和其他服務 toothen，已要求此位址的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="068e8-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="068e8-140">這是很重要，因為 hello 服務位址不是靜態。</span><span class="sxs-lookup"><span data-stu-id="068e8-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="068e8-141">服務會移動 hello 叢集中進行資源平衡和可用性。</span><span class="sxs-lookup"><span data-stu-id="068e8-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="068e8-142">這是 hello 機制可讓用戶端 tooresolve hello 接聽服務位址。</span><span class="sxs-lookup"><span data-stu-id="068e8-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="068e8-143">逐步解說的完整如何 toowrite 通訊接聽程式，請參閱 < 針對[與 OWIN 自我主控的服務網狀架構 Web API 服務](service-fabric-reliable-services-communication-webapi.md)C# 中，而 for Java 中，您可以撰寫您自己的 HTTP 伺服器實作，請參閱 EchoServer 應用程式在 https://github.com/Azure-Samples/service-fabric-java-getting-started 範例。</span><span class="sxs-lookup"><span data-stu-id="068e8-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="068e8-144">與服務通訊</span><span class="sxs-lookup"><span data-stu-id="068e8-144">Communicating with a service</span></span>
<span data-ttu-id="068e8-145">hello 可靠的服務應用程式開發介面提供下列文件庫 toowrite 用戶端與服務通訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="068e8-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="068e8-146">服務端點解析</span><span class="sxs-lookup"><span data-stu-id="068e8-146">Service endpoint resolution</span></span>
<span data-ttu-id="068e8-147">與服務 hello 第一個步驟 toocommunication 是 tooresolve hello 資料分割或您想要 tootalk hello 服務執行個體的端點位址。</span><span class="sxs-lookup"><span data-stu-id="068e8-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="068e8-148">hello`ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)`公用程式類別，是可協助判斷 hello 在執行階段的服務端點的用戶端的基本基本類型。</span><span class="sxs-lookup"><span data-stu-id="068e8-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="068e8-149">在 Service Fabric 術語中，決定 hello 的服務端點的 hello 程序會為參考的 tooas hello*服務端點解析*。</span><span class="sxs-lookup"><span data-stu-id="068e8-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="068e8-150">在叢集內的 tooconnect tooservices，ServicePartitionResolver 可以建立使用預設設定。</span><span class="sxs-lookup"><span data-stu-id="068e8-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="068e8-151">這是建議大多數的情況下的使用方式的 hello:</span><span class="sxs-lookup"><span data-stu-id="068e8-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="068e8-152">tooconnect tooservices 不同叢集中，您可以使用一組叢集閘道端點建立 ServicePartitionResolver。</span><span class="sxs-lookup"><span data-stu-id="068e8-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="068e8-153">請注意，閘道端點都只是以不同的端點連接 toohello 相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="068e8-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="068e8-154">例如：</span><span class="sxs-lookup"><span data-stu-id="068e8-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="068e8-155">或者，`ServicePartitionResolver`可以給函式建立`FabricClient`toouse 內部：</span><span class="sxs-lookup"><span data-stu-id="068e8-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="068e8-156">`FabricClient`是使用與 hello 叢集上的各種管理操作的 hello Service Fabric 叢集 toocommunicate hello 物件。</span><span class="sxs-lookup"><span data-stu-id="068e8-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="068e8-157">當您想要更充分掌控服務分割解析程式與叢集互動的方式時，這非常實用。</span><span class="sxs-lookup"><span data-stu-id="068e8-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="068e8-158">`FabricClient`執行的內部快取，因此您很重要的 tooreuse 並一般而言成本較高的 toocreate`FabricClient`盡可能的執行個體。</span><span class="sxs-lookup"><span data-stu-id="068e8-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="068e8-159">解決方法是，則使用的 tooretrieve hello 位址的服務或資料分割的服務的服務資料分割。</span><span class="sxs-lookup"><span data-stu-id="068e8-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="068e8-160">可以輕鬆地使用 ServicePartitionResolver，來解決服務位址，但需要更多工作 tooensure hello 解析就可以使用位址正確。</span><span class="sxs-lookup"><span data-stu-id="068e8-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="068e8-161">您的用戶端是否 hello 連接嘗試因為暫時性錯誤而失敗，並可重試，需要 toodetect （例如，服務移或暫時無法使用），或永久錯誤 （例如，服務已刪除或 hello 要求的資源不存在）。</span><span class="sxs-lookup"><span data-stu-id="068e8-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="068e8-162">服務執行個體或複本可四處移動從節點 toonode 隨時可能有多種原因。</span><span class="sxs-lookup"><span data-stu-id="068e8-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="068e8-163">hello 服務位址透過 ServicePartitionResolver 解決您的用戶端程式碼嘗試 tooconnect hello 時間可能會過時。</span><span class="sxs-lookup"><span data-stu-id="068e8-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="068e8-164">在此情況下再次 hello 用戶端需要 toore 解析 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="068e8-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="068e8-165">提供先前 hello`ResolvedServicePartition`指出，再次 hello 解析程式需要 tootry 而不只是擷取快取的位址。</span><span class="sxs-lookup"><span data-stu-id="068e8-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="068e8-166">一般說來，hello 用戶端程式碼不需要直接操作以 hello ServicePartitionResolver。</span><span class="sxs-lookup"><span data-stu-id="068e8-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="068e8-167">就會建立並傳遞 toocommunication hello 可靠的服務應用程式開發介面中的用戶端處理站。</span><span class="sxs-lookup"><span data-stu-id="068e8-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="068e8-168">hello 處理站會在內部使用 hello 解析程式 toogenerate 可以是使用的 toocommunicate 與服務的用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="068e8-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="068e8-169">通訊用戶端和 Factory</span><span class="sxs-lookup"><span data-stu-id="068e8-169">Communication clients and factories</span></span>
<span data-ttu-id="068e8-170">hello 通訊 factory 程式庫實作容易正在重試連線 tooresolved 服務端點的典型錯誤處理重試模式。</span><span class="sxs-lookup"><span data-stu-id="068e8-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="068e8-171">hello factory 程式庫提供 hello 重試機制，而您提供 hello 錯誤處理常式。</span><span class="sxs-lookup"><span data-stu-id="068e8-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="068e8-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`定義會產生可以彼此通訊 tooa Service Fabric 服務的用戶端通訊用戶端處理站實作的 hello 基底介面。</span><span class="sxs-lookup"><span data-stu-id="068e8-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="068e8-173">hello 的 hello CommunicationClientFactory 取決於 hello 通訊堆疊，並且在 hello 用戶端希望 toocommunicate hello Service Fabric 服務所使用的實作。</span><span class="sxs-lookup"><span data-stu-id="068e8-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="068e8-174">hello 可靠的服務應用程式開發介面提供`CommunicationClientFactoryBase<TCommunicationClient>`。</span><span class="sxs-lookup"><span data-stu-id="068e8-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="068e8-175">這提供 hello CommunicationClientFactory 介面的基底實作，並且會執行工作所通用的 tooall hello 通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="068e8-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="068e8-176">（這些工作包括使用 ServicePartitionResolver toodetermine hello 服務端點。）</span><span class="sxs-lookup"><span data-stu-id="068e8-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="068e8-177">用戶端通常會實作 hello 抽象 CommunicationClientFactoryBase 類別 toohandle 邏輯的特定 toohello 通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="068e8-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="068e8-178">hello 通訊的用戶端只會接收位址，並使用它 tooconnect tooa 服務。</span><span class="sxs-lookup"><span data-stu-id="068e8-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="068e8-179">hello 用戶端可以使用它想要的任何通訊的協定。</span><span class="sxs-lookup"><span data-stu-id="068e8-179">hello client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="068e8-180">hello 用戶端處理站是主要負責建立通訊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="068e8-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="068e8-181">不會保留持續連線，例如 HTTP 用戶端的用戶端 hello factory 只需要 toocreate 和傳回 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="068e8-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="068e8-182">維護持續連線，某些二進位通訊協定，例如其他通訊協定應該也會驗證 hello factory toodetermine 是否 hello 連線需要 toobe 重新建立。</span><span class="sxs-lookup"><span data-stu-id="068e8-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="068e8-183">最後，例外狀況處理常式是負責決定哪些動作 tootake 時發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="068e8-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="068e8-184">例外狀況會分類為**可重試**和**不可重試**。</span><span class="sxs-lookup"><span data-stu-id="068e8-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="068e8-185">**非可重試**例外狀況只取得重新擲回後 toohello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="068e8-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="068e8-186">**不可重試**的例外狀況會進一步分類為**暫時性**和**非暫時性**。</span><span class="sxs-lookup"><span data-stu-id="068e8-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="068e8-187">**暫時性**例外狀況是只會重試而不重新解決 hello 服務端點位址。</span><span class="sxs-lookup"><span data-stu-id="068e8-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="068e8-188">這些會包含暫時性網路問題或不存在服務錯誤回應指出 hello 服務端點位址以外。</span><span class="sxs-lookup"><span data-stu-id="068e8-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="068e8-189">**非暫時性**例外狀況是需要 hello 服務端點位址 toobe 重新解決。</span><span class="sxs-lookup"><span data-stu-id="068e8-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="068e8-190">這包括例外狀況，以指出 hello 服務端點無法連線，表示 hello 服務移 tooa 不同的節點。</span><span class="sxs-lookup"><span data-stu-id="068e8-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="068e8-191">hello`TryHandleException`讓決策，以指定的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="068e8-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="068e8-192">如果它**不知道**應該傳回例外狀況的相關哪些決策 toomake **false**。</span><span class="sxs-lookup"><span data-stu-id="068e8-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="068e8-193">如果它**知道**哪些決策 toomake，它應該據此設定 hello 結果並傳回**true**。</span><span class="sxs-lookup"><span data-stu-id="068e8-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="068e8-194">總整理</span><span class="sxs-lookup"><span data-stu-id="068e8-194">Putting it all together</span></span>
<span data-ttu-id="068e8-195">與`ICommunicationClient(C#) / CommunicationClient(Java)`， `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`，和`IExceptionHandler(C#) / ExceptionHandler(Java)`周圍的通訊協定，建置`ServicePartitionClient(C#) / FabricServicePartitionClient(Java)`一起自動換行，並提供 hello 錯誤處理和服務磁碟分割位址解析圈這些元件。</span><span class="sxs-lookup"><span data-stu-id="068e8-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="068e8-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="068e8-196">Next steps</span></span>
* <span data-ttu-id="068e8-197">請在 [GitHub 上的 C# 範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount)或 [GitHub 上的 Java 範例專案](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog)中，參閱服務之間的 HTTP 通訊範例。</span><span class="sxs-lookup"><span data-stu-id="068e8-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="068e8-198">使用 Reliable Services 遠端服務進行遠端程序呼叫</span><span class="sxs-lookup"><span data-stu-id="068e8-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="068e8-199">在 Reliable Services 中使用 OWIN 的 Web API</span><span class="sxs-lookup"><span data-stu-id="068e8-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="068e8-200">使用 Reliable Services 的 WCF 通訊</span><span class="sxs-lookup"><span data-stu-id="068e8-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
