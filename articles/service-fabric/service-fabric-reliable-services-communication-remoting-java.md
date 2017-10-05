---
title: "Azure Service Fabric 的服務遠端處理 | Microsoft Docs"
description: "Service Fabric 遠端處理可讓用戶端和服務使用遠端程序呼叫與服務進行通訊。"
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
ms.openlocfilehash: dc4a362b5737bb424ca2c196c85f4c51b6ee5e30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="af12b-103">使用 Reliable Services 的遠端服務</span><span class="sxs-lookup"><span data-stu-id="af12b-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af12b-104">Windows 上的 C# </span><span class="sxs-lookup"><span data-stu-id="af12b-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="af12b-105">在 Linux 上使用 Java</span><span class="sxs-lookup"><span data-stu-id="af12b-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="af12b-106">Reliable Services 架構提供遠端機制，以快速且輕鬆地為服務設定遠端程序呼叫。</span><span class="sxs-lookup"><span data-stu-id="af12b-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="af12b-107">設定在服務上的遠端處理</span><span class="sxs-lookup"><span data-stu-id="af12b-107">Set up remoting on a service</span></span>
<span data-ttu-id="af12b-108">只要兩個簡單步驟，就能設定服務的遠端處理：</span><span class="sxs-lookup"><span data-stu-id="af12b-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="af12b-109">建立服務實作的介面。</span><span class="sxs-lookup"><span data-stu-id="af12b-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="af12b-110">這個介面會定義可在您的服務上用於遠端程序呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="af12b-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="af12b-111">方法也必須是傳回工作的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="af12b-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="af12b-112">此介面必須實作 `microsoft.serviceFabric.services.remoting.Service` ，表示服務具有遠端處理介面。</span><span class="sxs-lookup"><span data-stu-id="af12b-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="af12b-113">在您的服務中使用遠端接聽程式。</span><span class="sxs-lookup"><span data-stu-id="af12b-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="af12b-114">這是提供遠端功能的 `CommunicationListener` 實作。</span><span class="sxs-lookup"><span data-stu-id="af12b-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="af12b-115">`FabricTransportServiceRemotingListener` 可以用來使用預設遠端傳輸通訊協定建立遠端接聽程式。</span><span class="sxs-lookup"><span data-stu-id="af12b-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="af12b-116">例如，下列無狀態服務服務會公開單一方法，透過遠端程序呼叫取得 "Hello World"。</span><span class="sxs-lookup"><span data-stu-id="af12b-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="af12b-117">服務介面中的引數和傳回類型可以是任何簡單、複雜或自訂的類型，但它們必須可以序列化。</span><span class="sxs-lookup"><span data-stu-id="af12b-117">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="af12b-118">呼叫遠端服務方法</span><span class="sxs-lookup"><span data-stu-id="af12b-118">Call remote service methods</span></span>
<span data-ttu-id="af12b-119">透過 `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 類別使用連至服務的本機 Proxy，可以在服務上使用遠端堆疊呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="af12b-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="af12b-120">`ServiceProxyBase` 方法會使用該服務所實作的相同介面，建立本機 Proxy。</span><span class="sxs-lookup"><span data-stu-id="af12b-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="af12b-121">您可以使用該 Proxy 直接在介面上遠端呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="af12b-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="af12b-122">遠端架構會將在服務擲回的例外狀況傳播給用戶端。</span><span class="sxs-lookup"><span data-stu-id="af12b-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="af12b-123">因此在用戶端使用 `ServiceProxyBase` 的例外狀況處理邏輯，可以直接處理服務擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="af12b-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="af12b-124">服務 Proxy 存留期</span><span class="sxs-lookup"><span data-stu-id="af12b-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="af12b-125">建立 ServiceProxy 是輕量型作業，因此沒有限制使用者可建立的數量。</span><span class="sxs-lookup"><span data-stu-id="af12b-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="af12b-126">只要有需要，使用者可以重複使用服務 Proxy 。</span><span class="sxs-lookup"><span data-stu-id="af12b-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="af12b-127">使用者可以重複使用相同的 Proxy，以防止發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="af12b-127">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="af12b-128">每個 ServiceProxy 皆包含用來透過網路傳送訊息的通訊用戶端。</span><span class="sxs-lookup"><span data-stu-id="af12b-128">Each ServiceProxy contains communication client used to send messages over the wire.</span></span> <span data-ttu-id="af12b-129">叫用 API 時，我們會透過內部檢查來查看用戶端是否使用有效的通訊。</span><span class="sxs-lookup"><span data-stu-id="af12b-129">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="af12b-130">根據結果，我們會重新建立通訊用戶端。</span><span class="sxs-lookup"><span data-stu-id="af12b-130">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="af12b-131">因此使用者不需要重新建立 serviceproxy，以免發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="af12b-131">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="af12b-132">ServiceProxyFactory 存留期</span><span class="sxs-lookup"><span data-stu-id="af12b-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="af12b-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) 是一個為不同的遠端處理介面建立 Proxy 的處理站。</span><span class="sxs-lookup"><span data-stu-id="af12b-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="af12b-134">如果您使用 API `ServiceProxyBase.create` 來建立 Proxy，則架構會建立 `FabricServiceProxyFactory`。</span><span class="sxs-lookup"><span data-stu-id="af12b-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="af12b-135">當您需要覆寫 [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) 屬性時，手動建立一個會相當有用。</span><span class="sxs-lookup"><span data-stu-id="af12b-135">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="af12b-136">處理站是一項昂貴的作業。</span><span class="sxs-lookup"><span data-stu-id="af12b-136">Factory is an expensive operation.</span></span> <span data-ttu-id="af12b-137">`FabricServiceProxyFactory` 會維護通訊用戶端的快取。</span><span class="sxs-lookup"><span data-stu-id="af12b-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="af12b-138">最佳做法是快取 `FabricServiceProxyFactory` 的時間愈長愈好。</span><span class="sxs-lookup"><span data-stu-id="af12b-138">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="af12b-139">遠端例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="af12b-139">Remoting Exception Handling</span></span>
<span data-ttu-id="af12b-140">服務 API 擲出的所有遠端例外狀況會以 RuntimeException 或 FabricException 的形式傳送回用戶端。</span><span class="sxs-lookup"><span data-stu-id="af12b-140">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="af12b-141">ServiceProxy 會處理服務分割區 (ServiceProxy 即是為其建立) 的所有容錯移轉列外狀況。</span><span class="sxs-lookup"><span data-stu-id="af12b-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="af12b-142">發生容錯移轉例外狀況 (非暫時性例外狀況) 時，ServiceProxy 會重新解析端點，然後以正確的端點再次嘗試呼叫。</span><span class="sxs-lookup"><span data-stu-id="af12b-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="af12b-143">容錯移轉例外狀況的重試次數並無限制。</span><span class="sxs-lookup"><span data-stu-id="af12b-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="af12b-144">若是發生 TransientExceptions，ServiceProxy 僅會重試呼叫。</span><span class="sxs-lookup"><span data-stu-id="af12b-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="af12b-145">預設的重試參數會由 [OperationRetrySettings] 提供。</span><span class="sxs-lookup"><span data-stu-id="af12b-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="af12b-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) 使用者可透過將 OperationRetrySettings 物件傳遞給 ServiceProxyFactory 建構函式來設定這些值。</span><span class="sxs-lookup"><span data-stu-id="af12b-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af12b-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af12b-147">Next steps</span></span>
* [<span data-ttu-id="af12b-148">Reliable Services 的安全通訊</span><span class="sxs-lookup"><span data-stu-id="af12b-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
