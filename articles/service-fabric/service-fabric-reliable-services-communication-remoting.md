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
# <a name="service-remoting-with-reliable-services"></a>使用 Reliable Services 的遠端服務
不服務繫結 tooa 特定通訊協定或堆疊，例如 WebAPI、 Windows Communication Foundation (WCF) 或其他項目，如 hello 可靠的服務架構提供遠端處理機制 tooquickly，並輕鬆地設定遠端程序呼叫服務。

## <a name="set-up-remoting-on-a-service"></a>設定在服務上的遠端處理
只要兩個簡單步驟，就能設定服務的遠端處理：

1. 建立服務 tooimplement 的介面。 這個介面會定義可供您服務上的遠端程序呼叫的 hello 方法。 hello 方法必須是工作傳回非同步方法。 hello 介面必須實作`Microsoft.ServiceFabric.Services.Remoting.IService`hello 服務的 toosignal 具有遠端服務介面。
2. 在您的服務中使用遠端接聽程式。 這是提供遠端功能的 `ICommunicationListener` 實作。 hello`Microsoft.ServiceFabric.Services.Remoting.Runtime`命名空間包含的擴充方法，`CreateServiceRemotingListener`無狀態與可設定狀態服務，可以使用的 toocreate 遠端接聽程式使用 hello 預設遠端處理的傳輸通訊協定。

注意： hello`Remoting`命名空間是可用以呼叫個別的 nuget 套件`Microsoft.ServiceFabric.Services.Remoting` 

例如，hello 下列無狀態服務會公開透過遠端程序呼叫的單一方法 tooget"Hello World"。

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
> hello 引數和 hello 傳回 hello 服務介面中的型別可以是任何簡單、 複雜或自訂類型，但它們必須由 hello.NET 序列化[DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx)。
>
>

## <a name="call-remote-service-methods"></a>呼叫遠端服務方法
在服務上呼叫方法，藉由使用 hello 遠端處理堆疊方式是使用本機 proxy toohello 服務透過 hello`Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy`類別。 hello`ServiceProxy`方法會建立本機 proxy 使用 hello hello 服務的相同介面實作。 與該 proxy，您可以只 hello 介面從遠端呼叫方法。

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

hello 遠端架構會傳播 hello 服務 toohello 用戶端在擲回的例外狀況。 因此例外狀況處理邏輯在 hello 用戶端使用`ServiceProxy`可以直接處理 hello 服務擲回的例外狀況。

## <a name="service-proxy-lifetime"></a>服務 Proxy 存留期
建立 ServiceProxy 是輕量型作業，因此沒有限制使用者可建立的數量。 只要有需要，使用者可以重複使用服務 Proxy 。 使用者可以重新使用 hello 例外狀況下有相同的 proxy。 每個 ServiceProxy 包含通訊使用的用戶端 toosend 訊息上 hello 傳輸。 時叫用應用程式開發介面，我們會有內部的核取 toosee 通訊用的用戶端是否有效。 根據該結果，我們重新建立 hello 通訊的用戶端。 因此使用者不需要 toorecreate serviceproxy 發生例外狀況。

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory 存留期
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) 是建立不同遠端介面 Proxy 的處理站。 如果您使用 API ServiceProxy.Create 建立 proxy 時，framework 就會建立 hello singelton ServiceProxyFactory。
它是一個實用 toocreate 手動時需要 toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory)屬性。
處理站是一項昂貴的作業。 ServiceProxyFactory 會保留通訊用戶端的快取。
最佳作法是 toocache ServiceProxyFactory 越久。

## <a name="remoting-exception-handling"></a>遠端例外狀況處理
服務 API，所擲回的所有 hello 遠端例外會當做 AggregateException 都傳送後 toohello 用戶端。 RemoteExceptions 否則應該是 DataContract 序列化[ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception)中它擲回 toohello proxy 應用程式開發介面與 hello 序列化錯誤。

ServiceProxy 並處理 hello 服務資料分割建立的所有容錯移轉的例外狀況。 如果沒有與 hello 正確端點容錯移轉 Exceptions(Non-Transient Exceptions) 和重試 hello 呼叫重新解析 hello 端點。 容錯移轉例外狀況的重試次數並無限制。
發生 TransientExceptions，它只會重試 hello 呼叫。

預設的重試參數會由 [OperationRetrySettings] 提供。 (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings)使用者可以藉由傳遞 OperationRetrySettings 物件 tooServiceProxyFactory 建構函式中設定這些值。

## <a name="next-steps"></a>後續步驟
* [在 Reliable Services 中搭配 OWIN 使用 Web API](service-fabric-reliable-services-communication-webapi.md)
* [使用 Reliable Services 的 WCF 通訊](service-fabric-reliable-services-communication-wcf.md)
* [Reliable Services 的安全通訊](service-fabric-reliable-services-secure-communication.md)
