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
# <a name="wcf-based-communication-stack-for-reliable-services"></a>適用於 Reliable Services 的 WCF 式通訊堆疊
hello 可靠服務架構可讓服務的服務想 toouse 作者 toochoose hello 通訊堆疊。 它們可以透過 hello 他們所選擇的 hello 通訊堆疊，插入**ICommunicationListener**傳回 hello [CreateServiceReplicaListeners 或 CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md)方法。 hello 架構提供服務作者都想 toouse WCF 為基礎的通訊以 hello Windows Communication Foundation (WCF) 為基礎的 hello 通訊堆疊的實作。

## <a name="wcf-communication-listener"></a>WCF 通訊接聽程式
hello 特定 WCF 實作**ICommunicationListener**係由 hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener**類別。

假設我們有類型 `ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

我們可以在 hello 服務 hello 下列方式來建立 WCF 通訊接聽程式。

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

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>撰寫 hello WCF 通訊堆疊的用戶端
撰寫用戶端與服務使用 WCF，hello framework toocommunicate 提供**WcfClientCommunicationFactory**，這是 hello 特定 WCF 實作[ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

您可以從 hello 存取 hello WCF 通訊通道**WcfCommunicationClient**建立 hello **WcfCommunicationClientFactory**。

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

用戶端程式碼可以使用 hello **WcfCommunicationClientFactory**以及 hello **WcfCommunicationClient**實作**ServicePartitionClient** toodeterminehello 服務端點，並與 hello 服務進行通訊。

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
> hello 預設 ServicePartitionResolver 假設該 hello 用戶端在相同叢集 hello 服務執行。 如果也就不是 hello 的情況下，建立 ServicePartitionResolver 物件，並傳入 hello 叢集連接端點。
> 
> 

## <a name="next-steps"></a>後續步驟
* [使用 Reliable Services 遠端服務進行遠端程序呼叫](service-fabric-reliable-services-communication-remoting.md)
* [在 Reliable Services 中搭配 OWIN 使用 Web API](service-fabric-reliable-services-communication-webapi.md)
* [Reliable Services 的安全通訊](service-fabric-reliable-services-secure-communication.md)

