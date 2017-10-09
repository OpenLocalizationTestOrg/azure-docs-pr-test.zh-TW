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
# <a name="service-remoting-with-reliable-services"></a>使用 Reliable Services 的遠端服務
> [!div class="op_single_selector"]
> * [Windows 上的 C# ](service-fabric-reliable-services-communication-remoting.md)
> * [在 Linux 上使用 Java](service-fabric-reliable-services-communication-remoting-java.md)
>
>

hello 可靠的服務架構提供遠端處理機制 tooquickly，並輕鬆地設定遠端程序呼叫服務。

## <a name="set-up-remoting-on-a-service"></a>設定在服務上的遠端處理
只要兩個簡單步驟，就能設定服務的遠端處理：

1. 建立服務 tooimplement 的介面。 這個介面會定義可供您服務上的遠端程序呼叫 hello 方法。 hello 方法必須是工作傳回非同步方法。 hello 介面必須實作`microsoft.serviceFabric.services.remoting.Service`hello 服務的 toosignal 具有遠端服務介面。
2. 在您的服務中使用遠端接聽程式。 這是提供遠端功能的 `CommunicationListener` 實作。 `FabricTransportServiceRemotingListener`可以是使用的 toocreate 使用 hello 預設遠端處理的傳輸通訊協定的遠端接聽程式。

例如，hello 下列無狀態服務會公開透過遠端程序呼叫的單一方法 tooget"Hello World"。

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
> hello 引數和 hello 傳回 hello 服務介面中的型別可以是任何簡單、 複雜或自訂類型，但必須是可序列化。
>
>

## <a name="call-remote-service-methods"></a>呼叫遠端服務方法
在服務上呼叫方法，藉由使用 hello 遠端處理堆疊方式是使用本機 proxy toohello 服務透過 hello`microsoft.serviceFabric.services.remoting.client.ServiceProxyBase`類別。 hello`ServiceProxyBase`方法會建立本機 proxy 使用 hello hello 服務的相同介面實作。 與該 proxy，您可以只 hello 介面從遠端呼叫方法。

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

hello 遠端架構會傳播 hello 服務 toohello 用戶端在擲回的例外狀況。 因此例外狀況處理邏輯在 hello 用戶端使用`ServiceProxyBase`可以直接處理 hello 服務擲回的例外狀況。

## <a name="service-proxy-lifetime"></a>服務 Proxy 存留期
建立 ServiceProxy 是輕量型作業，因此沒有限制使用者可建立的數量。 只要有需要，使用者可以重複使用服務 Proxy 。 使用者可以重新使用 hello 例外狀況下有相同的 proxy。 每個 ServiceProxy 包含通訊使用的用戶端 toosend 訊息上 hello 傳輸。 時叫用應用程式開發介面，我們會有內部的核取 toosee 通訊用的用戶端是否有效。 根據該結果，我們重新建立 hello 通訊的用戶端。 因此使用者不需要 toorecreate serviceproxy 發生例外狀況。

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory 存留期
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) 是一個為不同的遠端處理介面建立 Proxy 的處理站。 如果您使用 API `ServiceProxyBase.create` 來建立 Proxy，則架構會建立 `FabricServiceProxyFactory`。
它是一個實用 toocreate 手動時需要 toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory)屬性。
處理站是一項昂貴的作業。 `FabricServiceProxyFactory` 會維護通訊用戶端的快取。
最佳作法是 toocache`FabricServiceProxyFactory`越久。

## <a name="remoting-exception-handling"></a>遠端例外狀況處理
服務 API，所擲回的所有 hello 遠端例外會當做 RuntimeException 或 FabricException 都傳送後 toohello 用戶端。

ServiceProxy 並處理 hello 服務資料分割建立的所有容錯移轉的例外狀況。 如果沒有與 hello 正確端點容錯移轉 Exceptions(Non-Transient Exceptions) 和重試 hello 呼叫重新解析 hello 端點。 容錯移轉例外狀況的重試次數並無限制。
發生 TransientExceptions，它只會重試 hello 呼叫。

預設的重試參數會由 [OperationRetrySettings] 提供。 (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings)使用者可以藉由傳遞 OperationRetrySettings 物件 tooServiceProxyFactory 建構函式中設定這些值。

## <a name="next-steps"></a>後續步驟
* [Reliable Services 的安全通訊](service-fabric-reliable-services-secure-communication.md)
