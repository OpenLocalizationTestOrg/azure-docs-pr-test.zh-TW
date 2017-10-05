---
title: "Reliable Services WCF 通訊堆疊 | Microsoft Docs"
description: "Service Fabric 內建的 WCF 通訊堆疊提供 Reliable Services 專用的用戶端服務 WCF 通訊。"
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
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="f5a08-103">適用於 Reliable Services 的 WCF 式通訊堆疊</span><span class="sxs-lookup"><span data-stu-id="f5a08-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="f5a08-104">Reliable Services 架構允許服務作者選擇其想要針對服務使用的通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="f5a08-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="f5a08-105">他們可以透過從 **CreateServiceReplicaListeners 或 CreateServiceInstanceListeners** 方法傳回的 [ICommunicationListener](service-fabric-reliable-services-communication.md) ，來外掛所選擇的通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="f5a08-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="f5a08-106">服務作者如果想要使用 Windows Communication Foundation (WCF) 式通訊，架構可提供以 WCF 式實作的通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="f5a08-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="f5a08-107">WCF 通訊接聽程式</span><span class="sxs-lookup"><span data-stu-id="f5a08-107">WCF Communication Listener</span></span>
<span data-ttu-id="f5a08-108">**ICommunicationListener** 的 ECF 特定實作係由 **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** 類別提供。</span><span class="sxs-lookup"><span data-stu-id="f5a08-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="f5a08-109">假設我們有類型 `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="f5a08-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="f5a08-110">我們可以透過下列方式在服務中建立 WCF 通訊接聽程式。</span><span class="sxs-lookup"><span data-stu-id="f5a08-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="f5a08-111">撰寫適用於 WCF 通訊堆疊的用戶端</span><span class="sxs-lookup"><span data-stu-id="f5a08-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="f5a08-112">為了撰寫能夠使用 WCF 來與服務進行通訊的用戶端，架構提供了 **WcfClientCommunicationFactory**，也就是 [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md)的 WCF 特定實作。</span><span class="sxs-lookup"><span data-stu-id="f5a08-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="f5a08-113">WCF 通訊通道可以從 **WcfCommunicationClientFactory** 建立的 **WcfCommunicationClient** 來存取。</span><span class="sxs-lookup"><span data-stu-id="f5a08-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="f5a08-114">用戶端程式碼可以使用 **WcfCommunicationClientFactory** 連同實作 **ServicePartitionClient** 的 **WcfCommunicationClient** 來決定服務端點，並與服務通訊。</span><span class="sxs-lookup"><span data-stu-id="f5a08-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="f5a08-115">預設 ServicePartitionResolver 假設用戶端正在與服務相同的叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="f5a08-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="f5a08-116">如果不是這樣，請建立 ServicePartitionResolver 物件，並傳入叢集連接端點。</span><span class="sxs-lookup"><span data-stu-id="f5a08-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f5a08-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5a08-117">Next steps</span></span>
* [<span data-ttu-id="f5a08-118">使用 Reliable Services 遠端服務進行遠端程序呼叫</span><span class="sxs-lookup"><span data-stu-id="f5a08-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="f5a08-119">在 Reliable Services 中搭配 OWIN 使用 Web API</span><span class="sxs-lookup"><span data-stu-id="f5a08-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="f5a08-120">Reliable Services 的安全通訊</span><span class="sxs-lookup"><span data-stu-id="f5a08-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

