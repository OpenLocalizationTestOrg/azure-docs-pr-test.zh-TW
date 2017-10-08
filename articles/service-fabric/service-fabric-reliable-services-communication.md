---
title: "aaaReliable 服務通訊的概觀 |Microsoft 文件"
description: "模型的概觀 hello 可靠的服務通訊，包括服務上的開啟接聽程式、 解決端點和服務之間進行通訊。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>如何 toouse hello 可靠的服務通訊的應用程式開發介面
「Azure Service Fabric 即平台」完全不受服務間的通訊影響。 所有通訊協定和堆疊是可接受的從 UDP tooHTTP。 是由 toohello 服務開發人員 toochoose 服務應該之間的通訊方式。 hello 可靠的服務應用程式架構提供的內建通訊堆疊 Api，您可以使用 toobuild 以及自訂通訊元件。

## <a name="set-up-service-communication"></a>設定服務通訊
hello 可靠的服務應用程式開發介面會用來進行服務通訊的一個簡單的介面。 tooopen 的端點，您的服務，只需實作此介面：

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

然後，您可以在服務基底類別方法覆寫項中傳回您的通訊接聽程式實作來新增該實作。

對於無狀態服務：

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

對於具狀態服務：

> [!NOTE]
> Java 中尚未支援具狀態 Reliable Services。
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

在這兩種情況下，您會傳回接聽程式的集合。 這樣服務 toolisten 上多個端點，可能需要使用不同的通訊協定，使用多個接聽程式。 例如，您可能有 HTTP 接聽程式和個別的 WebSocket 接聽程式。 每個接聽程式會取得名稱和 hello 產生集合*名稱： 位址*組會表示為 JSON 物件，當用戶端要求的服務執行個體或資料分割的 hello 接聽位址。

無狀態服務，在 hello 覆寫會傳回 ServiceInstanceListeners 的集合。 A`ServiceInstanceListener`包含函式 toocreate`ICommunicationListener(C#) / CommunicationListener(Java)`並給予名稱。 可設定狀態服務，hello 覆寫會傳回 ServiceReplicaListeners 的集合。 這是稍有不同的無狀態的對應項目，因為`ServiceReplicaListener`具有選項 tooopen`ICommunicationListener`次要複本上。 您不僅可以在服務中使用多個通訊接聽程式，也可以指定哪些接聽程式要在次要複本上接受要求，以及哪些接聽程式只在主要複本上進行接聽。

例如，您可以有一個只在主要複本上接受 RPC 呼叫的 ServiceRemotingListener，以及一個透過 HTTP 在次要複本上接受讀取要求的第二、自訂接聽程式：

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> 建立服務的多個接聽程式時， **必須** 為每個接聽程式提供唯一的名稱。
>
>

最後，描述 hello 端點所需的 hello 中的 hello 服務[服務資訊清單](service-fabric-application-model.md)端點上的 [hello] 區段下方。

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

hello 通訊接聽程式可以存取 hello endpoint 資源從 hello 配置 tooit`CodePackageActivationContext`在 hello `ServiceContext`。 hello 接聽程式可以開始開啟時，接聽要求。

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> 端點資源一般的 toohello 整個服務套件，與 hello 服務封裝啟動時，由 Service Fabric 配置它們。 多個服務複本裝載於共用相同的 ServiceHost hello hello 相同連接埠。 這表示該 hello 通訊接聽程式應支援連接埠共用。 hello 建議產生 hello 接聽位址時，這種方式，是 hello 通訊接聽程式 toouse hello 分割區識別碼和複本/執行個體識別碼。
>
>

### <a name="service-address-registration"></a>服務位址註冊
系統服務呼叫 hello*命名服務*Service Fabric 叢集上執行。 hello 命名服務是服務和其每個執行個體或複本 hello 服務正在接聽的位址註冊機構。 當 hello`OpenAsync(C#) / openAsync(Java)`方法`ICommunicationListener(C#) / CommunicationListener(Java)`完成時，其傳回值取得 hello 命名服務中註冊。 這會傳回值，取得已發行在 hello 命名服務是的字串，其值可完全是任何項目。 此字串值是用戶端時，看到他們要求的 hello 命名服務的 hello 服務地址。

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

Service Fabric 提供 Api，可讓用戶端和其他服務 toothen，已要求此位址的服務名稱。 這是很重要，因為 hello 服務位址不是靜態。 服務會移動 hello 叢集中進行資源平衡和可用性。 這是 hello 機制可讓用戶端 tooresolve hello 接聽服務位址。

> [!NOTE]
> 逐步解說的完整如何 toowrite 通訊接聽程式，請參閱 < 針對[與 OWIN 自我主控的服務網狀架構 Web API 服務](service-fabric-reliable-services-communication-webapi.md)C# 中，而 for Java 中，您可以撰寫您自己的 HTTP 伺服器實作，請參閱 EchoServer 應用程式在 https://github.com/Azure-Samples/service-fabric-java-getting-started 範例。
>
>

## <a name="communicating-with-a-service"></a>與服務通訊
hello 可靠的服務應用程式開發介面提供下列文件庫 toowrite 用戶端與服務通訊的 hello。

### <a name="service-endpoint-resolution"></a>服務端點解析
與服務 hello 第一個步驟 toocommunication 是 tooresolve hello 資料分割或您想要 tootalk hello 服務執行個體的端點位址。 hello`ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)`公用程式類別，是可協助判斷 hello 在執行階段的服務端點的用戶端的基本基本類型。 在 Service Fabric 術語中，決定 hello 的服務端點的 hello 程序會為參考的 tooas hello*服務端點解析*。

在叢集內的 tooconnect tooservices，ServicePartitionResolver 可以建立使用預設設定。 這是建議大多數的情況下的使用方式的 hello:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooconnect tooservices 不同叢集中，您可以使用一組叢集閘道端點建立 ServicePartitionResolver。 請注意，閘道端點都只是以不同的端點連接 toohello 相同叢集中。 例如：

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

或者，`ServicePartitionResolver`可以給函式建立`FabricClient`toouse 內部：

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

`FabricClient`是使用與 hello 叢集上的各種管理操作的 hello Service Fabric 叢集 toocommunicate hello 物件。 當您想要更充分掌控服務分割解析程式與叢集互動的方式時，這非常實用。 `FabricClient`執行的內部快取，因此您很重要的 tooreuse 並一般而言成本較高的 toocreate`FabricClient`盡可能的執行個體。

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

解決方法是，則使用的 tooretrieve hello 位址的服務或資料分割的服務的服務資料分割。

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

可以輕鬆地使用 ServicePartitionResolver，來解決服務位址，但需要更多工作 tooensure hello 解析就可以使用位址正確。 您的用戶端是否 hello 連接嘗試因為暫時性錯誤而失敗，並可重試，需要 toodetect （例如，服務移或暫時無法使用），或永久錯誤 （例如，服務已刪除或 hello 要求的資源不存在）。 服務執行個體或複本可四處移動從節點 toonode 隨時可能有多種原因。 hello 服務位址透過 ServicePartitionResolver 解決您的用戶端程式碼嘗試 tooconnect hello 時間可能會過時。 在此情況下再次 hello 用戶端需要 toore 解析 hello 位址。 提供先前 hello`ResolvedServicePartition`指出，再次 hello 解析程式需要 tootry 而不只是擷取快取的位址。

一般說來，hello 用戶端程式碼不需要直接操作以 hello ServicePartitionResolver。 就會建立並傳遞 toocommunication hello 可靠的服務應用程式開發介面中的用戶端處理站。 hello 處理站會在內部使用 hello 解析程式 toogenerate 可以是使用的 toocommunicate 與服務的用戶端物件。

### <a name="communication-clients-and-factories"></a>通訊用戶端和 Factory
hello 通訊 factory 程式庫實作容易正在重試連線 tooresolved 服務端點的典型錯誤處理重試模式。 hello factory 程式庫提供 hello 重試機制，而您提供 hello 錯誤處理常式。

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`定義會產生可以彼此通訊 tooa Service Fabric 服務的用戶端通訊用戶端處理站實作的 hello 基底介面。 hello 的 hello CommunicationClientFactory 取決於 hello 通訊堆疊，並且在 hello 用戶端希望 toocommunicate hello Service Fabric 服務所使用的實作。 hello 可靠的服務應用程式開發介面提供`CommunicationClientFactoryBase<TCommunicationClient>`。 這提供 hello CommunicationClientFactory 介面的基底實作，並且會執行工作所通用的 tooall hello 通訊堆疊。 （這些工作包括使用 ServicePartitionResolver toodetermine hello 服務端點。） 用戶端通常會實作 hello 抽象 CommunicationClientFactoryBase 類別 toohandle 邏輯的特定 toohello 通訊堆疊。

hello 通訊的用戶端只會接收位址，並使用它 tooconnect tooa 服務。 hello 用戶端可以使用它想要的任何通訊的協定。

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

hello 用戶端處理站是主要負責建立通訊的用戶端。 不會保留持續連線，例如 HTTP 用戶端的用戶端 hello factory 只需要 toocreate 和傳回 hello 用戶端。 維護持續連線，某些二進位通訊協定，例如其他通訊協定應該也會驗證 hello factory toodetermine 是否 hello 連線需要 toobe 重新建立。  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

最後，例外狀況處理常式是負責決定哪些動作 tootake 時發生例外狀況。 例外狀況會分類為**可重試**和**不可重試**。

* **非可重試**例外狀況只取得重新擲回後 toohello 呼叫端。
* **不可重試**的例外狀況會進一步分類為**暫時性**和**非暫時性**。
  * **暫時性**例外狀況是只會重試而不重新解決 hello 服務端點位址。 這些會包含暫時性網路問題或不存在服務錯誤回應指出 hello 服務端點位址以外。
  * **非暫時性**例外狀況是需要 hello 服務端點位址 toobe 重新解決。 這包括例外狀況，以指出 hello 服務端點無法連線，表示 hello 服務移 tooa 不同的節點。

hello`TryHandleException`讓決策，以指定的例外狀況。 如果它**不知道**應該傳回例外狀況的相關哪些決策 toomake **false**。 如果它**知道**哪些決策 toomake，它應該據此設定 hello 結果並傳回**true**。

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a>總整理
與`ICommunicationClient(C#) / CommunicationClient(Java)`， `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`，和`IExceptionHandler(C#) / ExceptionHandler(Java)`周圍的通訊協定，建置`ServicePartitionClient(C#) / FabricServicePartitionClient(Java)`一起自動換行，並提供 hello 錯誤處理和服務磁碟分割位址解析圈這些元件。

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a>後續步驟
* 請在 [GitHub 上的 C# 範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount)或 [GitHub 上的 Java 範例專案](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog)中，參閱服務之間的 HTTP 通訊範例。
* [使用 Reliable Services 遠端服務進行遠端程序呼叫](service-fabric-reliable-services-communication-remoting.md)
* [在 Reliable Services 中使用 OWIN 的 Web API](service-fabric-reliable-services-communication-webapi.md)
* [使用 Reliable Services 的 WCF 通訊](service-fabric-reliable-services-communication-wcf.md)
