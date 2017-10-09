---
title: "在 Azure Service Fabric aaaService 遠端 |Microsoft 文件"
description: "Service Fabric 遠端處理可讓用戶端與服務 toocommunicate 與服務，使用遠端程序呼叫的。"
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="7d163-103">使用 Reliable Services 的遠端服務</span><span class="sxs-lookup"><span data-stu-id="7d163-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d163-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="7d163-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="7d163-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="7d163-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="7d163-106">hello 可靠的服務架構提供遠端處理機制 tooquickly，並輕鬆地設定遠端程序呼叫服務。</span><span class="sxs-lookup"><span data-stu-id="7d163-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="7d163-107">設定在服務上的遠端處理</span><span class="sxs-lookup"><span data-stu-id="7d163-107">Set up remoting on a service</span></span>
<span data-ttu-id="7d163-108">只要兩個簡單步驟，就能設定服務的遠端處理：</span><span class="sxs-lookup"><span data-stu-id="7d163-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="7d163-109">建立服務 tooimplement 的介面。</span><span class="sxs-lookup"><span data-stu-id="7d163-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="7d163-110">這個介面會定義可供您服務上的遠端程序呼叫 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="7d163-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="7d163-111">hello 方法必須是工作傳回非同步方法。</span><span class="sxs-lookup"><span data-stu-id="7d163-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="7d163-112">hello 介面必須實作`microsoft.serviceFabric.services.remoting.Service`hello 服務的 toosignal 具有遠端服務介面。</span><span class="sxs-lookup"><span data-stu-id="7d163-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="7d163-113">在您的服務中使用遠端接聽程式。</span><span class="sxs-lookup"><span data-stu-id="7d163-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="7d163-114">這是提供遠端功能的 `CommunicationListener` 實作。</span><span class="sxs-lookup"><span data-stu-id="7d163-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="7d163-115">`FabricTransportServiceRemotingListener`可以是使用的 toocreate 使用 hello 預設遠端處理的傳輸通訊協定的遠端接聽程式。</span><span class="sxs-lookup"><span data-stu-id="7d163-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="7d163-116">例如，hello 下列無狀態服務會公開透過遠端程序呼叫的單一方法 tooget"Hello World"。</span><span class="sxs-lookup"><span data-stu-id="7d163-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="7d163-117">hello 引數和 hello 傳回 hello 服務介面中的型別可以是任何簡單、 複雜或自訂類型，但必須是可序列化。</span><span class="sxs-lookup"><span data-stu-id="7d163-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="7d163-118">呼叫遠端服務方法</span><span class="sxs-lookup"><span data-stu-id="7d163-118">Call remote service methods</span></span>
<span data-ttu-id="7d163-119">在服務上呼叫方法，藉由使用 hello 遠端處理堆疊方式是使用本機 proxy toohello 服務透過 hello`microsoft.serviceFabric.services.remoting.client.ServiceProxyBase`類別。</span><span class="sxs-lookup"><span data-stu-id="7d163-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="7d163-120">hello`ServiceProxyBase`方法會建立本機 proxy 使用 hello hello 服務的相同介面實作。</span><span class="sxs-lookup"><span data-stu-id="7d163-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="7d163-121">與該 proxy，您可以只 hello 介面從遠端呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="7d163-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="7d163-122">hello 遠端架構會傳播 hello 服務 toohello 用戶端在擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7d163-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="7d163-123">因此例外狀況處理邏輯在 hello 用戶端使用`ServiceProxyBase`可以直接處理 hello 服務擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7d163-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="7d163-124">服務 Proxy 存留期</span><span class="sxs-lookup"><span data-stu-id="7d163-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="7d163-125">建立 ServiceProxy 是輕量型作業，因此沒有限制使用者可建立的數量。</span><span class="sxs-lookup"><span data-stu-id="7d163-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="7d163-126">只要有需要，使用者可以重複使用服務 Proxy 。</span><span class="sxs-lookup"><span data-stu-id="7d163-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="7d163-127">使用者可以重新使用 hello 例外狀況下有相同的 proxy。</span><span class="sxs-lookup"><span data-stu-id="7d163-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="7d163-128">每個 ServiceProxy 包含通訊使用的用戶端 toosend 訊息上 hello 傳輸。</span><span class="sxs-lookup"><span data-stu-id="7d163-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="7d163-129">時叫用應用程式開發介面，我們會有內部的核取 toosee 通訊用的用戶端是否有效。</span><span class="sxs-lookup"><span data-stu-id="7d163-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="7d163-130">根據該結果，我們重新建立 hello 通訊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="7d163-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="7d163-131">因此使用者不需要 toorecreate serviceproxy 發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7d163-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="7d163-132">ServiceProxyFactory 存留期</span><span class="sxs-lookup"><span data-stu-id="7d163-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="7d163-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) 是一個為不同的遠端處理介面建立 Proxy 的處理站。</span><span class="sxs-lookup"><span data-stu-id="7d163-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="7d163-134">如果您使用 API `ServiceProxyBase.create` 來建立 Proxy，則架構會建立 `FabricServiceProxyFactory`。</span><span class="sxs-lookup"><span data-stu-id="7d163-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="7d163-135">它是一個實用 toocreate 手動時需要 toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory)屬性。</span><span class="sxs-lookup"><span data-stu-id="7d163-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="7d163-136">處理站是一項昂貴的作業。</span><span class="sxs-lookup"><span data-stu-id="7d163-136">Factory is an expensive operation.</span></span> <span data-ttu-id="7d163-137">`FabricServiceProxyFactory` 會維護通訊用戶端的快取。</span><span class="sxs-lookup"><span data-stu-id="7d163-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="7d163-138">最佳作法是 toocache`FabricServiceProxyFactory`越久。</span><span class="sxs-lookup"><span data-stu-id="7d163-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="7d163-139">遠端例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="7d163-139">Remoting Exception Handling</span></span>
<span data-ttu-id="7d163-140">服務 API，所擲回的所有 hello 遠端例外會當做 RuntimeException 或 FabricException 都傳送後 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="7d163-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="7d163-141">ServiceProxy 並處理 hello 服務資料分割建立的所有容錯移轉的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7d163-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="7d163-142">如果沒有與 hello 正確端點容錯移轉 Exceptions(Non-Transient Exceptions) 和重試 hello 呼叫重新解析 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="7d163-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="7d163-143">容錯移轉例外狀況的重試次數並無限制。</span><span class="sxs-lookup"><span data-stu-id="7d163-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="7d163-144">發生 TransientExceptions，它只會重試 hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="7d163-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="7d163-145">預設的重試參數會由 [OperationRetrySettings] 提供。</span><span class="sxs-lookup"><span data-stu-id="7d163-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="7d163-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings)使用者可以藉由傳遞 OperationRetrySettings 物件 tooServiceProxyFactory 建構函式中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="7d163-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d163-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d163-147">Next steps</span></span>
* [<span data-ttu-id="7d163-148">Reliable Services 的安全通訊</span><span class="sxs-lookup"><span data-stu-id="7d163-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
