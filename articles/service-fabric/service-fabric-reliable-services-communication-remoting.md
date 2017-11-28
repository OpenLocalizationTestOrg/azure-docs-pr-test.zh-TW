---
title: "<span data-ttu-id=\"783f0-101\">Service Fabric 的服務遠端處理 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"783f0-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"783f0-102\">Service Fabric 遠端處理可讓用戶端和服務使用遠端程序呼叫與服務進行通訊。</span><span class=\"sxs-lookup\"><span data-stu-id=\"783f0-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="783f0-103">使用 Reliable Services 的遠端服務</span><span class="sxs-lookup"><span data-stu-id="783f0-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="783f0-104">對於未繫結至特定通訊協定或堆疊 (例如 WebAPI、Windows Communication Foundation (WCF) 或其他項目) 的服務，Reliable Services 架構會提供遠端機制，以便快速且輕鬆設定服務遠端程序呼叫。</span><span class="sxs-lookup"><span data-stu-id="783f0-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="783f0-105">設定在服務上的遠端處理</span><span class="sxs-lookup"><span data-stu-id="783f0-105">Set up remoting on a service</span></span>
<span data-ttu-id="783f0-106">只要兩個簡單步驟，就能設定服務的遠端處理：</span><span class="sxs-lookup"><span data-stu-id="783f0-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="783f0-107">建立服務實作的介面。</span><span class="sxs-lookup"><span data-stu-id="783f0-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="783f0-108">這個介面會定義方法，可在您的服務上用於遠端程序呼叫。</span><span class="sxs-lookup"><span data-stu-id="783f0-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="783f0-109">方法也必須是傳回工作的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="783f0-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="783f0-110">此介面必須實作 `Microsoft.ServiceFabric.Services.Remoting.IService` ，表示服務具有遠端處理介面。</span><span class="sxs-lookup"><span data-stu-id="783f0-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="783f0-111">在您的服務中使用遠端接聽程式。</span><span class="sxs-lookup"><span data-stu-id="783f0-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="783f0-112">這是提供遠端功能的 `ICommunicationListener` 實作。</span><span class="sxs-lookup"><span data-stu-id="783f0-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="783f0-113">`Microsoft.ServiceFabric.Services.Remoting.Runtime` 命名空間包含一個適用於無狀態與具狀態服務的擴充方法 `CreateServiceRemotingListener`，可用於建立使用預設遠端傳輸通訊協定的遠端接聽程式。</span><span class="sxs-lookup"><span data-stu-id="783f0-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="783f0-114">注意：`Remoting` 命名空間是以名為 `Microsoft.ServiceFabric.Services.Remoting` 的個別 Nuget 套件形式來提供使用</span><span class="sxs-lookup"><span data-stu-id="783f0-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="783f0-115">例如，下列無狀態服務服務會公開單一方法，透過遠端程序呼叫取得 "Hello World"。</span><span class="sxs-lookup"><span data-stu-id="783f0-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="783f0-116">服務介面中的引數和傳回類型可以是任何簡單、複雜或自訂的類型，但必須可由 .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx)序列化。</span><span class="sxs-lookup"><span data-stu-id="783f0-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="783f0-117">呼叫遠端服務方法</span><span class="sxs-lookup"><span data-stu-id="783f0-117">Call remote service methods</span></span>
<span data-ttu-id="783f0-118">透過 `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` 類別使用連至服務的本機 Proxy，可以在服務上使用遠端堆疊呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="783f0-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="783f0-119">`ServiceProxy` 方法會使用該服務所實作的相同介面，建立本機 Proxy。</span><span class="sxs-lookup"><span data-stu-id="783f0-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="783f0-120">您可以使用該 Proxy 直接在介面上遠端呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="783f0-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="783f0-121">遠端架構會將在服務擲回的例外狀況傳播給用戶端。</span><span class="sxs-lookup"><span data-stu-id="783f0-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="783f0-122">因此在用戶端使用 `ServiceProxy` 的例外狀況處理邏輯，可以直接處理服務擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="783f0-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="783f0-123">服務 Proxy 存留期</span><span class="sxs-lookup"><span data-stu-id="783f0-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="783f0-124">建立 ServiceProxy 是輕量型作業，因此沒有限制使用者可建立的數量。</span><span class="sxs-lookup"><span data-stu-id="783f0-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="783f0-125">只要有需要，使用者可以重複使用服務 Proxy 。</span><span class="sxs-lookup"><span data-stu-id="783f0-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="783f0-126">使用者可以重複使用相同的 Proxy，以防止發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="783f0-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="783f0-127">每個 ServiceProxy 皆包含用戶端透過網路傳送訊息時所用的通訊。</span><span class="sxs-lookup"><span data-stu-id="783f0-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="783f0-128">叫用 API 時，我們會透過內部檢查來查看用戶端是否使用有效的通訊。</span><span class="sxs-lookup"><span data-stu-id="783f0-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="783f0-129">根據結果，我們會重新建立通訊用戶端。</span><span class="sxs-lookup"><span data-stu-id="783f0-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="783f0-130">因此使用者不需要重新建立 serviceproxy，以免發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="783f0-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="783f0-131">ServiceProxyFactory 存留期</span><span class="sxs-lookup"><span data-stu-id="783f0-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="783f0-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) 是建立不同遠端介面 Proxy 的處理站。</span><span class="sxs-lookup"><span data-stu-id="783f0-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="783f0-133">如果您使用 API ServiceProxy.Create 建立 Proxy，則架構會建立單一 ServiceProxyFactory。</span><span class="sxs-lookup"><span data-stu-id="783f0-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="783f0-134">當您需要覆寫 [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) 屬性時，最實用的方式是手動建立一個。</span><span class="sxs-lookup"><span data-stu-id="783f0-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="783f0-135">處理站是一項昂貴的作業。</span><span class="sxs-lookup"><span data-stu-id="783f0-135">Factory is an expensive operation.</span></span> <span data-ttu-id="783f0-136">ServiceProxyFactory 會保留通訊用戶端的快取。</span><span class="sxs-lookup"><span data-stu-id="783f0-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="783f0-137">最佳做法是快取 ServiceProxyFactory 的時間愈長愈好。</span><span class="sxs-lookup"><span data-stu-id="783f0-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="783f0-138">遠端例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="783f0-138">Remoting Exception Handling</span></span>
<span data-ttu-id="783f0-139">服務 API 擲出的所有遠端例外狀況會以 AggregateException 的形式傳送回用戶端。</span><span class="sxs-lookup"><span data-stu-id="783f0-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="783f0-140">RemoteExceptions 應可進行 DataContract 序列化，否則 Proxy API 會收到包含序列化錯誤的 [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception)。</span><span class="sxs-lookup"><span data-stu-id="783f0-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="783f0-141">ServiceProxy 會處理服務分割區 (ServiceProxy 即是為其建立) 的所有容錯移轉列外狀況。</span><span class="sxs-lookup"><span data-stu-id="783f0-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="783f0-142">發生容錯移轉例外狀況 (非暫時性例外狀況) 時，ServiceProxy 會重新解析端點，然後以正確的端點再次嘗試呼叫。</span><span class="sxs-lookup"><span data-stu-id="783f0-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="783f0-143">容錯移轉例外狀況的重試次數並無限制。</span><span class="sxs-lookup"><span data-stu-id="783f0-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="783f0-144">若是發生 TransientExceptions，ServiceProxy 僅會重試呼叫。</span><span class="sxs-lookup"><span data-stu-id="783f0-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="783f0-145">預設的重試參數會由 [OperationRetrySettings] 提供。</span><span class="sxs-lookup"><span data-stu-id="783f0-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="783f0-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) 使用者可透過將 OperationRetrySettings 物件傳遞至 ServiceProxyFactory 建構函式來設定這些值。</span><span class="sxs-lookup"><span data-stu-id="783f0-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="783f0-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="783f0-147">Next steps</span></span>
* [<span data-ttu-id="783f0-148">在 Reliable Services 中搭配 OWIN 使用 Web API</span><span class="sxs-lookup"><span data-stu-id="783f0-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="783f0-149">使用 Reliable Services 的 WCF 通訊</span><span class="sxs-lookup"><span data-stu-id="783f0-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="783f0-150">Reliable Services 的安全通訊</span><span class="sxs-lookup"><span data-stu-id="783f0-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
