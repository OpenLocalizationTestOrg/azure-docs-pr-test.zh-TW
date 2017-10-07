---
title: "以 hello ASP.NET Core aaaService 通訊 |Microsoft 文件"
description: "深入了解如何 toouse ASP.NET 核心中無狀態與可設定狀態可靠的服務。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>Service Fabric Reliable Services 中的 ASP.NET Core

ASP.NET Core 是新的開放原始碼和跨平台架構，可建置現代化雲端網際網路連線的應用程式，例如 web 應用程式、IoT 應用程式，以及行動後端。 

本文是服務網狀架構可靠的服務使用 hello 中服務的 ASP.NET Core 深度指南 toohosting **Microsoft.ServiceFabric.AspNetCore。*** 的 NuGet 套件集。

如需 Service Fabric 中 ASP.NET Core 的簡介教學課程，以及如何安裝開發環境設定的指示，請參閱[使用 ASP.NET Core 為應用程式建置 Web 前端應用程式](service-fabric-add-a-web-frontend.md)。

hello 本文其餘部分，假設您已熟悉 ASP.NET Core。 如果不是，我們建議您閱讀 hello [ASP.NET Core 基礎](https://docs.microsoft.com/aspnet/core/fundamentals/index)。

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>Hello Service Fabric 環境中的 ASP.NET Core

雖然 ASP.NET Core 應用程式可以執行只能在執行完整的.NET Framework，Service Fabric 服務目前的 hello 或.NET 核心上 hello 完整.NET Framework。 這表示當您建置 ASP.NET Core Service Fabric 服務時，您必須仍目標 hello 完整.NET Framework。

可在 Service Fabric 中以兩種方式使用 ASP.NET Core︰
 - **裝載作為客體可執行檔**。 這是主要使用的 toorun 現有 ASP.NET Core 應用程式服務的網狀架構上沒有變更程式碼。
 - **在 Reliable Service 內部執行**. 這允許更貼近 hello Service Fabric 執行階段，並允許可設定狀態的 ASP.NET 核心服務。

hello 這篇文章的其餘部分將說明如何 toouse ASP.NET Core 內可靠的服務使用 hello 以 hello Service Fabric SDK 的出貨的 ASP.NET Core 整合元件。 

## <a name="service-fabric-service-hosting"></a>Service Fabric 服務裝載

在 Service Fabric 中，您服務的一或多個執行個體及/或複本會在服務主機處理序中執行，這是執行您的服務程式碼的可執行檔。 您身為服務作者，擁有 hello 服務主機處理序，Service Fabric 會啟用，並監視您。

（向上 tooMVC 5) 的傳統 ASP.NET 是透過 System.Web.dll 緊密結合的 tooIIS。 ASP.NET Core 提供 hello web 伺服器和 web 應用程式之間的分隔。 這可讓 web 應用程式 toobe 可攜式不同的網頁伺服器之間，也可讓 web 伺服器 toobe*自我裝載*，這表示您可以啟動 web 伺服器在自己的程序，但不要的 tooa 程序擁有的專用 web例如，IIS 伺服器軟體。 

在順序 toocombine Service Fabric 服務和 ASP.NET，為客體可執行檔，或者在可靠的服務中，您必須能夠 toostart ASP.NET 服務的主機處理序內。 自我裝載的 ASP.NET Core 可讓您 toodo 這。

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>在 Reliable Service 中裝載 ASP.NET Core
自我裝載的 ASP.NET 核心應用程式通常會在應用程式的進入點，例如 hello 建立 WebHost`static void Main()`方法中的`Program.cs`。 在此案例中 WebHost 的 hello 生命週期是 hello 的 hello 程序的繫結的 toohello 生命週期。

![在處理序中裝載 ASP.NET Core][0]

不過，hello 應用程式進入點不是 hello 地方 toocreate WebHost 可靠的服務中，因為只會用 hello 應用程式進入點 tooregister 服務類型，與 hello Service Fabric 執行階段，讓它可能會建立該服務的執行個體型別。 hello WebHost 中應該建立可靠的服務本身。 Hello 服務主機處理序內的服務執行個體及/或複本可能經過多個週期。 

Reliable Service 執行個體是由您衍生自 `StatelessService` 或 `StatefulService` 的服務類別代表。 服務的 hello 通訊堆疊包含在`ICommunicationListener`您的服務類別中實作。 hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 封裝包含實作的`ICommunicationListener`，啟動並管理 hello ASP.NET Core WebHost Kestrel 或 WebListener 可靠的服務中。

![在 Reliable Service 中裝載 ASP.NET Core][1]

## <a name="aspnet-core-icommunicationlisteners"></a>ASP.NET Core ICommunicationListeners
hello `ICommunicationListener` Kestrel 和實作 WebListener 在 hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 封裝有相似的使用模式，但執行稍有不同的動作特定 tooeach web 伺服器。 

這兩個通訊接聽程式提供的建構函式會採用下列引數的 hello:
 - **`ServiceContext serviceContext`**: hello`ServiceContext`包含 hello 執行服務的相關資訊的物件。
 - **`string endpointName`**: hello 名稱`Endpoint`ServiceManifest.xml 中的組態。 這主要是 hello 兩個通訊接聽程式的不同之處： WebListener**需要**`Endpoint`組態，而 Kestrel 沒有。
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**：您所實作並在其中建立並傳回 `IWebHost` 的 lambda。 這可讓您 tooconfigure `IWebHost` hello 方式就像平常 ASP.NET Core 應用程式中。 hello lambda 提供 URL，這產生的您根據 hello Service Fabric 整合選項您使用和 hello`Endpoint`您提供的組態。 然後可以修改或做為 URL-toostart hello 的網頁伺服器。

## <a name="service-fabric-integration-middleware"></a>Service Fabric 整合中介軟體
hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet 套件會包含 hello`UseServiceFabricIntegration`上的擴充方法`IWebHostBuilder`，將服務網狀架構的中介軟體。 此中介軟體設定 hello Kestrel 或 WebListener `ICommunicationListener` tooregister 唯一的服務 URL 與 hello Service Fabric 命名服務，然後驗證用戶端要求 tooensure 用戶端連線 toohello 正確的服務。 這是必要，在共用主機環境，例如服務網狀架構，其中多個 web 應用程式相同的實體或虛擬機器可以在 hello 中執行，但是不會使用唯一的主機名稱，但是不小心連接 toohello 錯誤的服務 tooprevent 用戶端。 在 hello 下一節中詳細描述此案例。

### <a name="a-case-of-mistaken-identity"></a>誤用身分識別的案例
不論通訊協定，服務複本會接聽唯一 IP:port 組合。 服務複本啟動之後 IP:port 端點上接聽，它會報告該端點位址 toohello Service Fabric 命名服務用戶端或其他服務，可以探索到。 如果服務使用，且剛好都可以使用動態指派的應用程式連接埠，服務複本 hello 先前已的另一個服務相同 IP:port 端點 hello 相同的實體或虛擬機器。 這可能會造成用戶端 toomistakely 連接 toohello 錯誤的服務。 這種情況會發生下列事件順序的 hello:

 1. 服務 A 透過 HTTP 接聽 10.0.0.1:30000。 
 2. 用戶端解析服務 A 並取得位址 10.0.0.1:30000
 3. 服務移 tooa 另一個節點。
 4. 服務 B 會存放在 10.0.0.1，且剛好都使用 hello 相同的連接埠 30000。
 5. 用戶端會嘗試使用快取的位址 10.0.0.1:30000 tooconnect tooservice A。
 6. 用戶端是連接已成功連接的 tooservice B 他不知道它現在 toohello 錯誤的服務。

在隨機時間可能是很困難 toodiagnose，這會造成錯誤。 

### <a name="using-unique-service-urls"></a>使用唯一的服務 URL
此服務 tooprevent 張貼端點 toohello 命名服務，且其唯一的識別碼，以及驗證期間用戶端要求的唯一識別碼。 這在非惡意租用戶受信任環境中的服務之間為合作式動作。 這在惡意租用戶環境中不會提供安全服務驗證。

在受信任的環境中，hello hello 所加入的中介軟體`UseServiceFabricIntegration`方法會自動將附加的唯一識別碼 toohello 位址張貼 toohello 命名服務及驗證每個要求該識別項。 如果 hello 識別碼不符合，hello 中介軟體會立即傳回 HTTP 410 Gone 回應。

使用動態指派連接埠的服務應該要使用此中介軟體。

使用固定的唯一連接埠之服務在合作的環境中沒有這個問題。 固定的唯一通訊埠通常用於外部對向服務至用戶端應用程式 tooconnect 需已知的連接埠。 例如，大部分對網際網路開放的 web 應用程式會使用 web 瀏覽器連接的連接埠 80 或 443。 在此情況下，不應啟用 hello 唯一識別碼。

hello 下圖顯示 hello 要求流程 hello 中介軟體啟用：

![Service Fabric ASP.NET Core 整合][2]

Kestrel 和 WebListener`ICommunicationListener`實作會使用這項機制在完全 hello 相同的方式。 雖然 WebListener 就可以在內部區分根據唯一的 URL 路徑使用 hello 基礎要求*http.sys*連接埠共用功能，功能*不*hello WebListener所使用`ICommunicationListener`實作因為會導致在 hello 稍早所述的案例中的 HTTP 503 和 HTTP 404 錯誤狀態碼。 反而能夠讓它很難 hello 錯誤的用戶端 toodetermine hello 意圖以 HTTP 503 HTTP 404 已經常用的 tooindicate 其他錯誤。 因此，Kestrel 和 WebListener`ICommunicationListener`實作標準化 hello 中介軟體提供的 hello`UseServiceFabricIntegration`擴充方法，讓用戶端只需 tooperform 服務端點重新解決 HTTP 410 回應所引發的動作。

## <a name="weblistener-in-reliable-services"></a>Reliable Services 中的 WebListener
可以藉由匯入 hello 可靠的服務中使用 WebListener **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet 封裝。 此套件包含`WebListenerCommunicationListener`，實作`ICommunicationListener`，可讓您 toocreate 可靠的服務內部 ASP.NET Core WebHost WebListener 用作 hello web 伺服器。

WebListener 建置在 hello [Windows HTTP 伺服器 API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx)。 這會使用 hello *http.sys*核心驅動程式使用 IIS tooprocess HTTP 要求和傳送它們 tooprocesses 執行 web 應用程式。 這可讓多個處理序上 hello 相同實體或虛擬機器 toohost web 應用程式上 hello 明確地區分由唯一的 URL 路徑或主機名稱的相同連接埠。 這些功能來裝載多個網站中 hello 可用於 Service Fabric 相同叢集中。

hello 下列圖表說明了如何 WebListener 使用 hello *http.sys* Windows 上的連接埠共用的核心驅動程式：

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>無狀態服務中的 WebListener
toouse`WebListener`無狀態服務，在覆寫 hello`CreateServiceInstanceListeners`方法，並傳回`WebListenerCommunicationListener`執行個體：

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a>具狀態服務中的 WebListener

`WebListenerCommunicationListener`目前不是以用於可設定狀態服務到期與 hello 基礎 toocomplications *http.sys*連接埠共用功能。 如需詳細資訊，請參閱下列區段上動態連接埠配置以 WebListener hello。 對於可設定狀態服務，Kestrel 會是 hello 建議使用 web 伺服器。

### <a name="endpoint-configuration"></a>端點組態

`Endpoint`不需要對使用 hello Windows HTTP 伺服器 API，包括 WebListener 網頁伺服器的組態。 使用 hello Windows HTTP 伺服器 API 網頁伺服器的第一次必須保留其 URL 與*http.sys* (通常這是以 hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx)工具)。 這個動作需要您服務預設未具有的提高權限。 hello"http"或"https"hello 選項`Protocol`hello 屬性`Endpoint`中的組態*ServiceManifest.xml*可用特別 tooinstruct hello Service Fabric 執行階段 tooregister URL*http.sys*代替您使用 hello [*強式萬用字元*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL 前置詞。

例如，tooreserve`http://+:80`服務中，hello 下列組態應該用於 ServiceManifest.xml:

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

而且必須在 hello 端點名稱傳遞 toohello`WebListenerCommunicationListener`建構函式：

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a>搭配使用 WebListener 與靜態連接埠
toouse WebListener，使用靜態連接埠提供 hello hello 連接埠號碼`Endpoint`組態：

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>搭配使用 WebListener 與動態連接埠
toouse WebListener，動態指派連接埠省略 hello`Port`屬性在 hello`Endpoint`組態：

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

請注意，依 `Endpoint` 組態配置的動態連接埠只提供每個主機處理序一個連接埠。 hello 目前裝載模型可讓多個服務執行個體及/或複本 toobe hello 中裝載的服務網狀架構相同的處理序，這表示每個會共用相同連接埠時透過 hello 配置的 hello`Endpoint`組態。 多個 WebListener 執行個體可以共用連接埠使用 hello 基礎*http.sys*連接埠共用功能，但不是支援`WebListenerCommunicationListener`到期，它會導致用戶端要求 toohello 複雜性。 動態連接埠使用量 Kestrel 是 hello 建議使用 web 伺服器。

## <a name="kestrel-in-reliable-services"></a>Reliable Services 中的 Kestrel
可以藉由匯入 hello 可靠的服務中使用 kestrel **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet 封裝。 此套件包含`KestrelCommunicationListener`，實作`ICommunicationListener`，可讓您 toocreate 可靠的服務內部 ASP.NET Core WebHost Kestrel 用作 hello web 伺服器。

Kestrel 根據 libuv 是 ASP.NET Core 的跨平台 web 伺服器，為跨平台非同步 I/O 程式庫。 不同於 WebListener，Kestrel 不會使用集中式端點管理員，例如 http.sys。 且不同於 WebListener，Kestrel 不支援多個處理序之間的連接埠共用。 Kestrel 的每個執行個體必須使用唯一的連接埠。

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>無狀態服務中的 Kestrel
toouse`Kestrel`無狀態服務，在覆寫 hello`CreateServiceInstanceListeners`方法，並傳回`KestrelCommunicationListener`執行個體：

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a>具狀態服務中的 Kestrel
toouse`Kestrel`具狀態服務，在覆寫 hello`CreateServiceReplicaListeners`方法，並傳回`KestrelCommunicationListener`執行個體：

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

在此範例中的單一執行個體`IReliableStateManager`提供 toohello WebHost 相依性插入容器。 這並非絕對必要，但它可讓您 toouse`IReliableStateManager`和可靠的集合，在您的 MVC 控制器動作方法。

請注意，`Endpoint`組態名稱是**不**太提供`KestrelCommunicationListener`中可設定狀態的服務。 在 hello 之後 > 一節中詳細的說明。

### <a name="endpoint-configuration"></a>端點組態
`Endpoint`組態並不是必要的 toouse Kestrel。 

Kestrel 是簡單的獨立 web 伺服器。不同於 WebListener （或 HttpListener），就不需要`Endpoint`中的組態*ServiceManifest.xml*因為不需要 URL 註冊先前 toostarting。 

#### <a name="use-kestrel-with-a-static-port"></a>搭配使用 Kestrel 與靜態連接埠
靜態連接埠可以設定在 hello`Endpoint`搭配 Kestrel ServiceManifest.xml 的組態。 雖然這並非絕對必要，它會提供兩個潛在的好處︰
 1. Hello 連接埠不是落在 hello 應用程式連接埠範圍中，如果它已透過 hello OS 防火牆開啟由服務網狀架構。
 2. hello 透過提供 URL tooyou`KestrelCommunicationListener`會使用此連接埠。

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

如果`Endpoint`是設定，其名稱必須傳入 hello`KestrelCommunicationListener`建構函式： 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

如果`Endpoint`不使用組態，請省略 hello 中的 hello 名稱`KestrelCommunicationListener`建構函式。 在此情況下，會使用動態連接埠。 請參閱 hello 下一節，如需詳細資訊。

#### <a name="use-kestrel-with-a-dynamic-port"></a>搭配使用 Kestrel 與動態連接埠
Kestrel 無法使用從 hello hello 自動連接埠指派`Endpoint`組態在 ServiceManifest.xml 中，因為從自動連接埠指派`Endpoint`設定會指派唯一的連接埠，每個*主機處理序*與單一主機處理序可以包含多個 Kestrel 執行個體。 因為 Kestrel 不支援連接埠共用，這並不會如每個 Kestrel 執行個體必須在唯一連接埠上開啟一般運作。

toouse 動態連接埠指派與 Kestrel，只要省略 hello `Endpoint` ServiceManifest.xml 中的設定完全，並不會傳遞端點名稱 toohello`KestrelCommunicationListener`建構函式：

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

此設定會`KestrelCommunicationListener`會自動選取未使用的連接埠從 hello 應用程式連接埠範圍。

## <a name="scenarios-and-configurations"></a>案例和組態
本章節描述下列案例的 hello，並提供 hello 建議的網頁伺服器、 連接埠組態，Service Fabric 整合選項和其他設定 tooachieve 組合正常運作的服務：
 - 外部公開 ASP.NET Core 無狀態服務
 - 內部公開 ASP.NET Core 無狀態服務
 - 內部公開 ASP.NET Core 具狀態服務

**外部公開**是一種可從外部 hello 叢集中，通常是透過負載平衡器連線的端點會公開服務。

**僅供內部使用**服務是其中一個端點，才可從 hello 叢集內存取。

> [!NOTE]
> 可設定狀態的服務端點通常不應該公開 toohello 網際網路。 Service Fabric 服務解析，例如 hello Azure 負載平衡器，不需要知道的負載平衡器後方的叢集將會無法 tooexpose 可設定狀態服務，因為 hello 負載平衡器將不能 toolocate 並路由傳送流量 toohello適當的可設定狀態服務複本。 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>外部公開 ASP.NET Core 無狀態服務
WebListener 是 hello 建議在 Windows 上的外部的網際網路對向 HTTP 端點所公開的前端服務的網頁伺服器。 它提供更好的保護以免於攻擊，並支援 Kestrel 所沒有的功能，例如 Windows 驗證和連接埠共用。 

Kestrel 這一次不支援作為邊緣 (網際網路) 伺服器。 必須使用反向 proxy 伺服器，例如 IIS 或 Nginx toohandle 流量 hello 公用網際網路。
 
當公開的 toohello 網際網路，無狀態服務應該使用的已知且穩定的端點是可連線透過負載平衡器。 這是您將提供您的應用程式的 toousers hello URL。 建議使用下列組態的 hello:

|  |  | **注意事項** |
| --- | --- | --- |
| Web 伺服器 | WebListener | 如果 hello 服務只公開的 tooa 信任的網路，這類內部網路，就可能會使用 Kestrel。 否則，WebListener 是 hello 慣用選項。 |
| 連接埠組態 | 靜態 | 已知的靜態連接埠應該設定在 hello`Endpoints`組態的 ServiceManifest.xml 中，例如 HTTP 為 80 或 443 的 HTTPS。 |
| ServiceFabricIntegrationOptions | None | hello`ServiceFabricIntegrationOptions.None`以便 hello 服務不會嘗試 toovalidate 內送要求的唯一識別碼設定 Service Fabric 整合中介軟體時應使用的選項。 外部應用程式的使用者將不會知道唯一 hello hello 中介軟體所使用的識別資訊。 |
| 執行個體計數 | -1 | 在一般使用案例，hello 執行個體計數設定必須將設定太"-1"，以便可以從負載平衡器接收流量的所有節點上執行個體。 |

如果多個外部公開的服務共用的 hello 相同設定的節點，則應該使用唯一的但穩定的 URL 路徑。 這可以藉由修改 hello URL 提供設定 IWebHost 時完成。 請注意這適用於僅 tooWebListener。

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a>僅供內部使用的無狀態 ASP.NET Core 服務
只會從呼叫 hello 叢集內的無狀態服務應使用唯一的 Url，而且多個服務之間的 tooensure 合作時動態指派連接埠。 建議使用下列組態的 hello:

|  |  | **注意事項** |
| --- | --- | --- |
| Web 伺服器 | Kestrel | 雖然 WebListener 可能用於內部無狀態服務，Kestrel 是 hello 建議伺服器 tooallow 多個服務執行個體 tooshare 主機。  |
| 連接埠組態 | 動態指派 | 多個具狀態服務的複本可能會共用主機處理序或主機作業系統，因此需要唯一的連接埠。 |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | 使用動態連接埠指派，這個設定會被誤認為 hello 識別問題稍早所述。 |
| InstanceCount | any | hello 執行個體計數設定可以設定 tooany 值必要 toooperate hello 服務。 |

### <a name="internal-only-stateful-aspnet-core-service"></a>僅供內部使用的具狀態 ASP.NET Core 服務
只會從呼叫 hello 叢集內的可設定狀態服務應該使用多個服務之間的動態指派連接埠 tooensure 合作。 建議使用下列組態的 hello:

|  |  | **注意事項** |
| --- | --- | --- |
| Web 伺服器 | Kestrel | hello`WebListenerCommunicationListener`不是使用可設定狀態的服務複本共用主控件程序。 |
| 連接埠組態 | 動態指派 | 多個具狀態服務的複本可能會共用主機處理序或主機作業系統，因此需要唯一的連接埠。 |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | 使用動態連接埠指派，這個設定會被誤認為 hello 識別問題稍早所述。 |

## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 偵錯 Service Fabric 應用程式](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
