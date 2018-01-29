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
ms.openlocfilehash: 51a9c8bd628ef9e65d04a3a4ddbdc127d84d4b54
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2017
---
# <a name="service-remoting-with-reliable-services"></a>使用 Reliable Services 的遠端服務
> [!div class="op_single_selector"]
> * [Windows 上的 C# ](service-fabric-reliable-services-communication-remoting.md)
> * [在 Linux 上使用 Java](service-fabric-reliable-services-communication-remoting-java.md)
>
>

Reliable Services 架構提供遠端機制，以快速且輕鬆地為服務設定遠端程序呼叫。

## <a name="set-up-remoting-on-a-service"></a>設定在服務上的遠端處理
只要兩個簡單步驟，就能設定服務的遠端處理：

1. 建立服務實作的介面。 這個介面會定義可在您的服務上用於遠端程序呼叫的方法。 方法也必須是傳回工作的非同步方法。 此介面必須實作 `microsoft.serviceFabric.services.remoting.Service` ，表示服務具有遠端處理介面。
2. 在您的服務中使用遠端接聽程式。 這是提供遠端功能的 `CommunicationListener` 實作。 `FabricTransportServiceRemotingListener` 可以用來使用預設遠端傳輸通訊協定建立遠端接聽程式。

例如，下列無狀態服務服務會公開單一方法，透過遠端程序呼叫取得 "Hello World"。

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
> 服務介面中的引數和傳回類型可以是任何簡單、複雜或自訂的類型，但它們必須可以序列化。
>
>

## <a name="call-remote-service-methods"></a>呼叫遠端服務方法
透過 `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` 類別使用連至服務的本機 Proxy，可以在服務上使用遠端堆疊呼叫方法。 `ServiceProxyBase` 方法會使用該服務所實作的相同介面，建立本機 Proxy。 您可以使用該 Proxy 直接在介面上遠端呼叫方法。

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

遠端架構會將在服務擲回的例外狀況傳播給用戶端。 因此在用戶端使用 `ServiceProxyBase` 的例外狀況處理邏輯，可以直接處理服務擲回的例外狀況。

## <a name="service-proxy-lifetime"></a>服務 Proxy 存留期
建立 ServiceProxy 是輕量型作業，因此沒有限制使用者可建立的數量。 只要有需要，使用者可以重複使用服務 Proxy 。 使用者可以重複使用相同的 Proxy，以防止發生例外狀況。 每個 ServiceProxy 皆包含用來透過網路傳送訊息的通訊用戶端。 叫用 API 時，我們會透過內部檢查來查看用戶端是否使用有效的通訊。 根據結果，我們會重新建立通訊用戶端。 因此使用者不需要重新建立 serviceproxy，以免發生例外狀況。

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory 存留期
[FabricServiceProxyFactory](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) 是一個為不同的遠端處理介面建立 Proxy 的處理站。 如果您使用 API `ServiceProxyBase.create` 來建立 Proxy，則架構會建立 `FabricServiceProxyFactory`。
當您需要覆寫 [ServiceRemotingClientFactory](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) 屬性時，手動建立一個會相當有用。
處理站是一項昂貴的作業。 `FabricServiceProxyFactory` 會維護通訊用戶端的快取。
最佳做法是快取 `FabricServiceProxyFactory` 的時間愈長愈好。

## <a name="remoting-exception-handling"></a>遠端例外狀況處理
服務 API 擲出的所有遠端例外狀況會以 RuntimeException 或 FabricException 的形式傳送回用戶端。

ServiceProxy 會處理服務分割區 (ServiceProxy 即是為其建立) 的所有容錯移轉列外狀況。 發生容錯移轉例外狀況 (非暫時性例外狀況) 時，ServiceProxy 會重新解析端點，然後以正確的端點再次嘗試呼叫。 容錯移轉例外狀況的重試次數並無限制。
若是發生 TransientExceptions，ServiceProxy 僅會重試呼叫。

預設的重試參數會由 [OperationRetrySettings] 提供。 (https://docs.microsoft.com/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings)使用者可以設定這些值將 OperationRetrySettings 物件傳遞給 ServiceProxyFactory 建構函式。

## <a name="next-steps"></a>後續步驟
* [Reliable Services 的安全通訊](service-fabric-reliable-services-secure-communication.md)
