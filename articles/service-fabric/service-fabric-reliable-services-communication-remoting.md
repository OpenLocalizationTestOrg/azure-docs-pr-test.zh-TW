---
title: "服務網狀架構中的遠端執行功能 aaaService |Microsoft 文件"
description: "Service Fabric 遠端處理可讓用戶端與服務 toocommunicate 與服務，使用遠端程序呼叫的。"
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
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="b27a2-103">使用 Reliable Services 的遠端服務</span><span class="sxs-lookup"><span data-stu-id="b27a2-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="b27a2-104">不服務繫結 tooa 特定通訊協定或堆疊，例如 WebAPI、 Windows Communication Foundation (WCF) 或其他項目，如 hello 可靠的服務架構提供遠端處理機制 tooquickly，並輕鬆地設定遠端程序呼叫服務。</span><span class="sxs-lookup"><span data-stu-id="b27a2-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="b27a2-105">設定在服務上的遠端處理</span><span class="sxs-lookup"><span data-stu-id="b27a2-105">Set up remoting on a service</span></span>
<span data-ttu-id="b27a2-106">只要兩個簡單步驟，就能設定服務的遠端處理：</span><span class="sxs-lookup"><span data-stu-id="b27a2-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="b27a2-107">建立服務 tooimplement 的介面。</span><span class="sxs-lookup"><span data-stu-id="b27a2-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="b27a2-108">這個介面會定義可供您服務上的遠端程序呼叫的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="b27a2-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="b27a2-109">hello 方法必須是工作傳回非同步方法。</span><span class="sxs-lookup"><span data-stu-id="b27a2-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="b27a2-110">hello 介面必須實作`Microsoft.ServiceFabric.Services.Remoting.IService`hello 服務的 toosignal 具有遠端服務介面。</span><span class="sxs-lookup"><span data-stu-id="b27a2-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="b27a2-111">在您的服務中使用遠端接聽程式。</span><span class="sxs-lookup"><span data-stu-id="b27a2-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="b27a2-112">這是提供遠端功能的 `ICommunicationListener` 實作。</span><span class="sxs-lookup"><span data-stu-id="b27a2-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="b27a2-113">hello`Microsoft.ServiceFabric.Services.Remoting.Runtime`命名空間包含的擴充方法，`CreateServiceRemotingListener`無狀態與可設定狀態服務，可以使用的 toocreate 遠端接聽程式使用 hello 預設遠端處理的傳輸通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b27a2-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="b27a2-114">注意： hello`Remoting`命名空間是可用以呼叫個別的 nuget 套件`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="b27a2-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="b27a2-115">例如，hello 下列無狀態服務會公開透過遠端程序呼叫的單一方法 tooget"Hello World"。</span><span class="sxs-lookup"><span data-stu-id="b27a2-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="b27a2-116">hello 引數和 hello 傳回 hello 服務介面中的型別可以是任何簡單、 複雜或自訂類型，但它們必須由 hello.NET 序列化[DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b27a2-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="b27a2-117">呼叫遠端服務方法</span><span class="sxs-lookup"><span data-stu-id="b27a2-117">Call remote service methods</span></span>
<span data-ttu-id="b27a2-118">在服務上呼叫方法，藉由使用 hello 遠端處理堆疊方式是使用本機 proxy toohello 服務透過 hello`Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy`類別。</span><span class="sxs-lookup"><span data-stu-id="b27a2-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="b27a2-119">hello`ServiceProxy`方法會建立本機 proxy 使用 hello hello 服務的相同介面實作。</span><span class="sxs-lookup"><span data-stu-id="b27a2-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="b27a2-120">與該 proxy，您可以只 hello 介面從遠端呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="b27a2-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="b27a2-121">hello 遠端架構會傳播 hello 服務 toohello 用戶端在擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b27a2-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="b27a2-122">因此例外狀況處理邏輯在 hello 用戶端使用`ServiceProxy`可以直接處理 hello 服務擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b27a2-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="b27a2-123">服務 Proxy 存留期</span><span class="sxs-lookup"><span data-stu-id="b27a2-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="b27a2-124">建立 ServiceProxy 是輕量型作業，因此沒有限制使用者可建立的數量。</span><span class="sxs-lookup"><span data-stu-id="b27a2-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="b27a2-125">只要有需要，使用者可以重複使用服務 Proxy 。</span><span class="sxs-lookup"><span data-stu-id="b27a2-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="b27a2-126">使用者可以重新使用 hello 例外狀況下有相同的 proxy。</span><span class="sxs-lookup"><span data-stu-id="b27a2-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="b27a2-127">每個 ServiceProxy 包含通訊使用的用戶端 toosend 訊息上 hello 傳輸。</span><span class="sxs-lookup"><span data-stu-id="b27a2-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="b27a2-128">時叫用應用程式開發介面，我們會有內部的核取 toosee 通訊用的用戶端是否有效。</span><span class="sxs-lookup"><span data-stu-id="b27a2-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="b27a2-129">根據該結果，我們重新建立 hello 通訊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="b27a2-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="b27a2-130">因此使用者不需要 toorecreate serviceproxy 發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b27a2-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="b27a2-131">ServiceProxyFactory 存留期</span><span class="sxs-lookup"><span data-stu-id="b27a2-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="b27a2-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) 是建立不同遠端介面 Proxy 的處理站。</span><span class="sxs-lookup"><span data-stu-id="b27a2-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="b27a2-133">如果您使用 API ServiceProxy.Create 建立 proxy 時，framework 就會建立 hello singelton ServiceProxyFactory。</span><span class="sxs-lookup"><span data-stu-id="b27a2-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="b27a2-134">它是一個實用 toocreate 手動時需要 toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory)屬性。</span><span class="sxs-lookup"><span data-stu-id="b27a2-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="b27a2-135">處理站是一項昂貴的作業。</span><span class="sxs-lookup"><span data-stu-id="b27a2-135">Factory is an expensive operation.</span></span> <span data-ttu-id="b27a2-136">ServiceProxyFactory 會保留通訊用戶端的快取。</span><span class="sxs-lookup"><span data-stu-id="b27a2-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="b27a2-137">最佳作法是 toocache ServiceProxyFactory 越久。</span><span class="sxs-lookup"><span data-stu-id="b27a2-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="b27a2-138">遠端例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="b27a2-138">Remoting Exception Handling</span></span>
<span data-ttu-id="b27a2-139">服務 API，所擲回的所有 hello 遠端例外會當做 AggregateException 都傳送後 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b27a2-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="b27a2-140">RemoteExceptions 否則應該是 DataContract 序列化[ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception)中它擲回 toohello proxy 應用程式開發介面與 hello 序列化錯誤。</span><span class="sxs-lookup"><span data-stu-id="b27a2-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="b27a2-141">ServiceProxy 並處理 hello 服務資料分割建立的所有容錯移轉的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b27a2-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="b27a2-142">如果沒有與 hello 正確端點容錯移轉 Exceptions(Non-Transient Exceptions) 和重試 hello 呼叫重新解析 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="b27a2-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="b27a2-143">容錯移轉例外狀況的重試次數並無限制。</span><span class="sxs-lookup"><span data-stu-id="b27a2-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="b27a2-144">發生 TransientExceptions，它只會重試 hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="b27a2-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="b27a2-145">預設的重試參數會由 [OperationRetrySettings] 提供。</span><span class="sxs-lookup"><span data-stu-id="b27a2-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="b27a2-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings)使用者可以藉由傳遞 OperationRetrySettings 物件 tooServiceProxyFactory 建構函式中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="b27a2-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b27a2-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b27a2-147">Next steps</span></span>
* [<span data-ttu-id="b27a2-148">在 Reliable Services 中搭配 OWIN 使用 Web API</span><span class="sxs-lookup"><span data-stu-id="b27a2-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="b27a2-149">使用 Reliable Services 的 WCF 通訊</span><span class="sxs-lookup"><span data-stu-id="b27a2-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="b27a2-150">Reliable Services 的安全通訊</span><span class="sxs-lookup"><span data-stu-id="b27a2-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
