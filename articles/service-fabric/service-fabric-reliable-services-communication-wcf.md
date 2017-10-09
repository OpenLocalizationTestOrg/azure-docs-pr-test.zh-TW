---
title: "aaaReliable 服務 WCF 通訊堆疊 |Microsoft 文件"
description: "hello 內建 WCF 通訊堆疊中 Service Fabric 提供可靠的服務的 WCF 用戶端服務通訊。"
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="443a8-103">適用於 Reliable Services 的 WCF 式通訊堆疊</span><span class="sxs-lookup"><span data-stu-id="443a8-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="443a8-104">hello 可靠服務架構可讓服務的服務想 toouse 作者 toochoose hello 通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="443a8-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="443a8-105">它們可以透過 hello 他們所選擇的 hello 通訊堆疊，插入**ICommunicationListener**傳回 hello [CreateServiceReplicaListeners 或 CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md)方法。</span><span class="sxs-lookup"><span data-stu-id="443a8-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="443a8-106">hello 架構提供服務作者都想 toouse WCF 為基礎的通訊以 hello Windows Communication Foundation (WCF) 為基礎的 hello 通訊堆疊的實作。</span><span class="sxs-lookup"><span data-stu-id="443a8-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="443a8-107">WCF 通訊接聽程式</span><span class="sxs-lookup"><span data-stu-id="443a8-107">WCF Communication Listener</span></span>
<span data-ttu-id="443a8-108">hello 特定 WCF 實作**ICommunicationListener**係由 hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener**類別。</span><span class="sxs-lookup"><span data-stu-id="443a8-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="443a8-109">假設我們有類型 `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="443a8-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="443a8-110">我們可以在 hello 服務 hello 下列方式來建立 WCF 通訊接聽程式。</span><span class="sxs-lookup"><span data-stu-id="443a8-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="443a8-111">撰寫 hello WCF 通訊堆疊的用戶端</span><span class="sxs-lookup"><span data-stu-id="443a8-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="443a8-112">撰寫用戶端與服務使用 WCF，hello framework toocommunicate 提供**WcfClientCommunicationFactory**，這是 hello 特定 WCF 實作[ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="443a8-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="443a8-113">您可以從 hello 存取 hello WCF 通訊通道**WcfCommunicationClient**建立 hello **WcfCommunicationClientFactory**。</span><span class="sxs-lookup"><span data-stu-id="443a8-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="443a8-114">用戶端程式碼可以使用 hello **WcfCommunicationClientFactory**以及 hello **WcfCommunicationClient**實作**ServicePartitionClient** toodeterminehello 服務端點，並與 hello 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="443a8-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="443a8-115">hello 預設 ServicePartitionResolver 假設該 hello 用戶端在相同叢集 hello 服務執行。</span><span class="sxs-lookup"><span data-stu-id="443a8-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="443a8-116">如果也就不是 hello 的情況下，建立 ServicePartitionResolver 物件，並傳入 hello 叢集連接端點。</span><span class="sxs-lookup"><span data-stu-id="443a8-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="443a8-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="443a8-117">Next steps</span></span>
* [<span data-ttu-id="443a8-118">使用 Reliable Services 遠端服務進行遠端程序呼叫</span><span class="sxs-lookup"><span data-stu-id="443a8-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="443a8-119">在 Reliable Services 中搭配 OWIN 使用 Web API</span><span class="sxs-lookup"><span data-stu-id="443a8-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="443a8-120">Reliable Services 的安全通訊</span><span class="sxs-lookup"><span data-stu-id="443a8-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

