---
title: "Reliable Services 通訊概觀 | Microsoft Docs"
description: "Reliable Services 通訊模型概觀，其中包括開啟服務的接聽程式、解析端點和服務間通訊。"
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
ms.openlocfilehash: b418904f50b772c12bfcdbb95beb9312c8b9fb00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="d8689-103">如何使用 Reliable Services 通訊 API</span><span class="sxs-lookup"><span data-stu-id="d8689-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="d8689-104">「Azure Service Fabric 即平台」完全不受服務間的通訊影響。</span><span class="sxs-lookup"><span data-stu-id="d8689-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="d8689-105">所有通訊協定和堆疊 (從 UDP 到 HTTP) 都可接受。</span><span class="sxs-lookup"><span data-stu-id="d8689-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="d8689-106">它是由服務開發人員選擇服務應有的通訊方式。</span><span class="sxs-lookup"><span data-stu-id="d8689-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="d8689-107">Reliable Services 應用程式架構會提供內建的通訊堆疊以及 API，讓您可用來建置自訂通訊元件。</span><span class="sxs-lookup"><span data-stu-id="d8689-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="d8689-108">設定服務通訊</span><span class="sxs-lookup"><span data-stu-id="d8689-108">Set up service communication</span></span>
<span data-ttu-id="d8689-109">Reliable Services API 使用一個簡單的服務通訊介面。</span><span class="sxs-lookup"><span data-stu-id="d8689-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="d8689-110">若要開啟服務的端點，只要實作此介面即可：</span><span class="sxs-lookup"><span data-stu-id="d8689-110">To open an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="d8689-111">然後，您可以在服務基底類別方法覆寫項中傳回您的通訊接聽程式實作來新增該實作。</span><span class="sxs-lookup"><span data-stu-id="d8689-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="d8689-112">對於無狀態服務：</span><span class="sxs-lookup"><span data-stu-id="d8689-112">For stateless services:</span></span>

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

<span data-ttu-id="d8689-113">對於具狀態服務：</span><span class="sxs-lookup"><span data-stu-id="d8689-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="d8689-114">Java 中尚未支援具狀態 Reliable Services。</span><span class="sxs-lookup"><span data-stu-id="d8689-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="d8689-115">在這兩種情況下，您會傳回接聽程式的集合。</span><span class="sxs-lookup"><span data-stu-id="d8689-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="d8689-116">這可讓您的服務透過多個接聽程式，可能使使用不同的通訊協定，在多個端點上接聽。</span><span class="sxs-lookup"><span data-stu-id="d8689-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="d8689-117">例如，您可能有 HTTP 接聽程式和個別的 WebSocket 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d8689-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="d8689-118">每個接聽程式都會獲得一個名稱及所產生的名稱集合：當用戶端要求服務執行個體或資料分割的接聽位址時，系統會以 JSON 物件的形式呈現位址配對。</span><span class="sxs-lookup"><span data-stu-id="d8689-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="d8689-119">在無狀態服務中，覆寫項會傳回 ServiceInstanceListeners 的集合。</span><span class="sxs-lookup"><span data-stu-id="d8689-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="d8689-120">`ServiceInstanceListener` 會包含可建立 `ICommunicationListener(C#) / CommunicationListener(Java)` 的函式，並會為它命名。</span><span class="sxs-lookup"><span data-stu-id="d8689-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="d8689-121">就具狀態服務而言，覆寫項則會傳回 ServiceReplicaListeners 集合。</span><span class="sxs-lookup"><span data-stu-id="d8689-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="d8689-122">這與其無狀態的對應項稍有不同，因為 `ServiceReplicaListener` 可以選擇在次要複本上將 `ICommunicationListener` 開啟。</span><span class="sxs-lookup"><span data-stu-id="d8689-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="d8689-123">您不僅可以在服務中使用多個通訊接聽程式，也可以指定哪些接聽程式要在次要複本上接受要求，以及哪些接聽程式只在主要複本上進行接聽。</span><span class="sxs-lookup"><span data-stu-id="d8689-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="d8689-124">例如，您可以有一個只在主要複本上接受 RPC 呼叫的 ServiceRemotingListener，以及一個透過 HTTP 在次要複本上接受讀取要求的第二、自訂接聽程式：</span><span class="sxs-lookup"><span data-stu-id="d8689-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="d8689-125">建立服務的多個接聽程式時， **必須** 為每個接聽程式提供唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="d8689-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="d8689-126">最後，在 [服務資訊清單](service-fabric-application-model.md) 中有關端點的區段下方說明服務所需的端點。</span><span class="sxs-lookup"><span data-stu-id="d8689-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="d8689-127">通訊接聽程式可以從 `ServiceContext` 中的 `CodePackageActivationContext` 存取配置給它的端點資源。</span><span class="sxs-lookup"><span data-stu-id="d8689-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="d8689-128">然後接聽程式會在開啟時開始接聽要求。</span><span class="sxs-lookup"><span data-stu-id="d8689-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="d8689-129">端點資源通用於整個服務封裝，並在服務封裝啟動時由 Service Fabric 配置。</span><span class="sxs-lookup"><span data-stu-id="d8689-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="d8689-130">裝載於相同 ServiceHost 的多個服務複本可能會共用相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="d8689-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="d8689-131">這表示通訊接聽程式應該支援連接埠共用。</span><span class="sxs-lookup"><span data-stu-id="d8689-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="d8689-132">建議做法是讓通訊接聽程式在產生接聽位址時，使用資料分割識別碼和複本/執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="d8689-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="d8689-133">服務位址註冊</span><span class="sxs-lookup"><span data-stu-id="d8689-133">Service address registration</span></span>
<span data-ttu-id="d8689-134">名為「命名服務」  的系統服務會在 Service Fabric 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="d8689-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="d8689-135">命名服務是適用於服務及其位址的註冊機構，而服務的每個執行個體或複本正在其上接聽。</span><span class="sxs-lookup"><span data-stu-id="d8689-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="d8689-136">當 `ICommunicationListener(C#) / CommunicationListener(Java)` 的 `OpenAsync(C#) / openAsync(Java)` 方法完成時，它的傳回值會在命名服務中註冊。</span><span class="sxs-lookup"><span data-stu-id="d8689-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="d8689-137">這個在命名服務中發佈的傳回值是一個字串，其值完全可以是任何項目。</span><span class="sxs-lookup"><span data-stu-id="d8689-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="d8689-138">這個字串值是用戶端向命名服務要求服務的位址時將會看見的內容。</span><span class="sxs-lookup"><span data-stu-id="d8689-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

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

    // the string returned here will be published in the Naming Service.
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

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="d8689-139">Service Fabric 提供 API，讓用戶端和其他服務之後能夠依服務名稱來要求這個位址。</span><span class="sxs-lookup"><span data-stu-id="d8689-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="d8689-140">這一點很重要，因為服務位址不是靜態的。</span><span class="sxs-lookup"><span data-stu-id="d8689-140">This is important because the service address is not static.</span></span> <span data-ttu-id="d8689-141">服務會為了資源平衡和可用性目的在叢集中移動。</span><span class="sxs-lookup"><span data-stu-id="d8689-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="d8689-142">這是可讓用戶端解析服務接聽位址的機制。</span><span class="sxs-lookup"><span data-stu-id="d8689-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="d8689-143">如需如何撰寫通訊接聽程式的完整逐步解說，請參閱 [Service Fabric Web API 服務與 OWIN 自我裝載](service-fabric-reliable-services-communication-webapi.md) (若為 C#)，而您可以撰寫自己的 HTTP 伺服器實作 (若為 Java)，請參閱 https://github.com/Azure-Samples/service-fabric-java-getting-started EchoServer 中的應用程式範例。</span><span class="sxs-lookup"><span data-stu-id="d8689-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="d8689-144">與服務通訊</span><span class="sxs-lookup"><span data-stu-id="d8689-144">Communicating with a service</span></span>
<span data-ttu-id="d8689-145">Reliable Services API 提供下列程式庫來撰寫與服務通訊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="d8689-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="d8689-146">服務端點解析</span><span class="sxs-lookup"><span data-stu-id="d8689-146">Service endpoint resolution</span></span>
<span data-ttu-id="d8689-147">與服務通訊的第一個步驟是，解析您想要通訊之服務的分割區或執行個體的端點位址。</span><span class="sxs-lookup"><span data-stu-id="d8689-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="d8689-148">`ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` 公用程式類別是一個基本類型，可協助用戶端在執行階段判斷服務的端點。</span><span class="sxs-lookup"><span data-stu-id="d8689-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="d8689-149">在 Service Fabric 術語中，判斷服務端點的程序稱為「服務端點解析」 。</span><span class="sxs-lookup"><span data-stu-id="d8689-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="d8689-150">若要連線到叢集內的服務，可以使用預設設定建立 ServicePartitionResolver。</span><span class="sxs-lookup"><span data-stu-id="d8689-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="d8689-151">這是大多數情況的建議用法︰</span><span class="sxs-lookup"><span data-stu-id="d8689-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="d8689-152">若要連線到不同叢集中的服務，可利用一組叢集閘道端點來建立 ServicePartitionResolver。</span><span class="sxs-lookup"><span data-stu-id="d8689-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="d8689-153">請注意，閘道端點就只是可用來連接到相同叢集的不同端點。</span><span class="sxs-lookup"><span data-stu-id="d8689-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="d8689-154">例如：</span><span class="sxs-lookup"><span data-stu-id="d8689-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="d8689-155">另外，可為 `ServicePartitionResolver` 指定一個函式來建立 `FabricClient`，以便在內部使用：</span><span class="sxs-lookup"><span data-stu-id="d8689-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

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

<span data-ttu-id="d8689-156">`FabricClient` 是為了叢集上各種管理作業而用來與 Service Fabric 叢集通訊的物件。</span><span class="sxs-lookup"><span data-stu-id="d8689-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="d8689-157">當您想要更充分掌控服務分割解析程式與叢集互動的方式時，這非常實用。</span><span class="sxs-lookup"><span data-stu-id="d8689-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="d8689-158">`FabricClient` 會在內部執行快取但建立的成本通常很高，因此一定要儘可能重複使用 `FabricClient` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="d8689-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="d8689-159">解析方法接著可用於擷取服務或已資料分割之服務的服務分割區的位址。</span><span class="sxs-lookup"><span data-stu-id="d8689-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="d8689-160">服務位址可以使用 ServicePartitionResolver 輕鬆地加以解析，但需要執行更多工作，才能確保解析的位址可正確使用。</span><span class="sxs-lookup"><span data-stu-id="d8689-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="d8689-161">您的用戶端必須偵測連線嘗試是否因為暫時性錯誤而失敗且可重試 (例如，服務已移動或暫時無法使用)，或因永久錯誤而失敗 (例如，已刪除服務，或要求的資源不存在)。</span><span class="sxs-lookup"><span data-stu-id="d8689-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="d8689-162">服務執行個體或複本隨時都可基於多重因素在節點間移動。</span><span class="sxs-lookup"><span data-stu-id="d8689-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="d8689-163">透過 ServicePartitionResolver 解析的服務位址，可能會在您的用戶端程式碼嘗試連線之前過時。</span><span class="sxs-lookup"><span data-stu-id="d8689-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="d8689-164">再回到該情況，用戶端必須重新解析位址。</span><span class="sxs-lookup"><span data-stu-id="d8689-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="d8689-165">提供先前的 `ResolvedServicePartition` ，表示解析程式需要再試一次，而不只是擷取快取的位址。</span><span class="sxs-lookup"><span data-stu-id="d8689-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="d8689-166">通常用戶端程式碼不需要直接搭配 ServicePartitionResolver 使用。</span><span class="sxs-lookup"><span data-stu-id="d8689-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="d8689-167">它已建立並傳遞給 Reliable Services API 中的通訊用戶端 Factory。</span><span class="sxs-lookup"><span data-stu-id="d8689-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="d8689-168">Factory 會在內部使用解析程式來產生可用來與服務通訊的用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="d8689-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="d8689-169">通訊用戶端和 Factory</span><span class="sxs-lookup"><span data-stu-id="d8689-169">Communication clients and factories</span></span>
<span data-ttu-id="d8689-170">通訊 Factory 程式庫會實作典型的錯誤處理重試模式，更容易重試與已解析服務端點的連接。</span><span class="sxs-lookup"><span data-stu-id="d8689-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="d8689-171">儘管您提供錯誤處理常式，Factory 程式庫還是會提供重試機制。</span><span class="sxs-lookup"><span data-stu-id="d8689-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="d8689-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` 定義通訊用戶端 Factory 所實作的基底介面，並產生可以與 Service Fabric 服務通訊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="d8689-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="d8689-173">CommunicationClientFactory 的實作取決於用戶端想要通訊的 Service Fabric 服務所使用的通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="d8689-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="d8689-174">Reliable Services API 提供 `CommunicationClientFactoryBase<TCommunicationClient>`。</span><span class="sxs-lookup"><span data-stu-id="d8689-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="d8689-175">這樣可以提供 CommunicationClientFactory 介面的基底實作，並執行所有通訊堆疊都通用的工作。</span><span class="sxs-lookup"><span data-stu-id="d8689-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="d8689-176">(這些工作包括使用 ServicePartitionResolver 來判斷服務端點)。</span><span class="sxs-lookup"><span data-stu-id="d8689-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="d8689-177">用戶端通常會實作 CommunicationClientFactoryBase 抽象類別來處理通訊堆疊專用的邏輯。</span><span class="sxs-lookup"><span data-stu-id="d8689-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="d8689-178">通訊用戶端只會接收位址，並使用它來連接到服務。</span><span class="sxs-lookup"><span data-stu-id="d8689-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="d8689-179">用戶端可以使用它想要的任何通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d8689-179">The client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="d8689-180">用戶端 Factory 主要是負責建立通訊用戶端。</span><span class="sxs-lookup"><span data-stu-id="d8689-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="d8689-181">對於不會維持持續連線的用戶端 (例如 HTTP 用戶端)，用戶端 Factory 只需建立並傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="d8689-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="d8689-182">其他會維持持續連線的通訊協定 (例如某些二進位通訊協定) 也應該由 Factory 驗證，以判斷是否需要重新建立連線。</span><span class="sxs-lookup"><span data-stu-id="d8689-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

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

<span data-ttu-id="d8689-183">最後，例外狀況處理常式會負責判斷發生例外狀況時所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="d8689-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="d8689-184">例外狀況會分類為**可重試**和**不可重試**。</span><span class="sxs-lookup"><span data-stu-id="d8689-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="d8689-185">**不可重試**的例外狀況只會重新擲回給呼叫端。</span><span class="sxs-lookup"><span data-stu-id="d8689-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="d8689-186">**不可重試**的例外狀況會進一步分類為**暫時性**和**非暫時性**。</span><span class="sxs-lookup"><span data-stu-id="d8689-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="d8689-187">**暫時性** 例外狀況是只會重試而不會重新解析服務端點位址的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d8689-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="d8689-188">這類例外狀況包括暫時性網路問題或服務錯誤回應，但不包括指出服務端點位址不存在的錯誤回應。</span><span class="sxs-lookup"><span data-stu-id="d8689-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="d8689-189">**非暫時性** 例外狀況是需要重新解析服務端點位址的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d8689-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="d8689-190">這類例外狀況包括指出無法連上服務端點 (表示服務已移至其他節點) 的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d8689-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="d8689-191">`TryHandleException` 會做出有關特定例外狀況的決定。</span><span class="sxs-lookup"><span data-stu-id="d8689-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="d8689-192">如果它**不知道**要對例外狀況做出哪些決定，則應傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="d8689-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="d8689-193">如果它**知道**如何做決定，則應該據以設定結果並傳回 **true**。</span><span class="sxs-lookup"><span data-stu-id="d8689-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

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

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
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

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="d8689-194">總整理</span><span class="sxs-lookup"><span data-stu-id="d8689-194">Putting it all together</span></span>
<span data-ttu-id="d8689-195">使用以通訊協定建構的 `ICommunicationClient(C#) / CommunicationClient(Java)`、`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` 和 `IExceptionHandler(C#) / ExceptionHandler(Java)`，`ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` 會將它全部包裝在一起，並為這些元件提供錯誤處理和服務分割區位址解析迴圈。</span><span class="sxs-lookup"><span data-stu-id="d8689-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
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
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="d8689-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8689-196">Next steps</span></span>
* <span data-ttu-id="d8689-197">請在 [GitHub 上的 C# 範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount)或 [GitHub 上的 Java 範例專案](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog)中，參閱服務之間的 HTTP 通訊範例。</span><span class="sxs-lookup"><span data-stu-id="d8689-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="d8689-198">使用 Reliable Services 遠端服務進行遠端程序呼叫</span><span class="sxs-lookup"><span data-stu-id="d8689-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="d8689-199">在 Reliable Services 中使用 OWIN 的 Web API</span><span class="sxs-lookup"><span data-stu-id="d8689-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="d8689-200">使用 Reliable Services 的 WCF 通訊</span><span class="sxs-lookup"><span data-stu-id="d8689-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
