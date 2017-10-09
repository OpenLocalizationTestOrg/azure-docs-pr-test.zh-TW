---
title: "以 ASP.NET Web API hello aaaService 通訊 |Microsoft 文件"
description: "了解如何逐步使用 tooimplement 服務通訊 hello 與 OWIN 自我主控 hello 可靠的服務應用程式開發介面中的 ASP.NET Web API。"
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>開始使用：Service Fabric Web API 服務與 OWIN 自我裝載 | Microsoft Azure
Azure Service Fabric 置於 hello 電源雙手當您決定要服務 toocommunicate，使用者與彼此。 本教學課程著重於使用 ASP.NET Web API 與 Open Web Interface for .NET (OWIN) 自我裝載在 Service Fabric 的 Reliable Services API 中實作服務通訊。 我們將深入探討深 hello 可靠的服務可插式通訊應用程式開發介面。 我們也會使用 Web 應用程式開發介面中的逐步範例 tooshow 您如何 tooset 註冊自訂通訊接聽程式。

## <a name="introduction-tooweb-api-in-service-fabric"></a>服務網狀架構的簡介 tooWeb 應用程式開發介面
ASP.NET Web API 是建立 HTTP Api 之上 hello.NET Framework 受歡迎且功能強大的架構。 如果您不熟悉 hello framework，請參閱[開始使用 ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn 更多。

服務網狀架構中的 web 應用程式開發介面是 hello 相同 ASP.NET Web API，您熟悉且愛用。 hello 其間的差異在於如何您*主機*Web API 應用程式。 您不會使用 Microsoft Internet Information Services (IIS)。 toobetter 瞭解 hello 差異，我們將其分成兩個部分：

1. hello Web API 應用程式 （包括控制站和模型）
2. hello 主機 （hello web 伺服器，通常是 IIS）

Web API 應用程式本身不會變更。 它並無不同 hello 過去，您可能會寫入 Web API 應用程式和大部分的應用程式程式碼應能 toosimply 移動。 但如果您已經已裝載於 IIS，您用來裝載 hello 應用程式可能會稍有不同於您所用的。 我們取得 toohello 裝載部分之前，讓我們先開始項目比較熟悉： hello Web API 應用程式。

## <a name="create-hello-application"></a>建立 hello 應用程式
若要開始，請在 Visual Studio 2015 中，建立具有單一無狀態服務的新 Service Fabric 應用程式。

使用 Web 應用程式開發介面的無狀態服務的 Visual Studio 範本是可用 tooyou。 在本教學課程中，我們將從頭建置 Web API 專案，這就是您選取此範本時所會得到的結果。

選取空白無狀態服務專案 toolearn 如何 hello 無狀態服務 Web API 範本的開頭和只沿用 toobuild 從頭開始，或您的 Web API 專案。  

hello 第一個步驟是 toopull Web API 的某些 NuGet 封裝中。 我們希望 toouse hello 封裝是 Microsoft.AspNet.WebApi.OwinSelfHost。 此套件包含所有 hello 必要的 Web 應用程式開發介面封裝以及 hello*主機*封裝。 這在稍後會很重要。

已安裝 hello 封裝之後，您可以開始建置出 hello 基本 Web API 專案結構。 如果您已使用 Web 應用程式開發介面，hello 專案結構應該看起來很類似。 首先新增 `Controllers` 目錄和簡單值控制站︰

**ValuesController.cs**

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

接下來，新增啟動類別在 hello 專案根 tooregister hello 路由、 格式器及任何其他組態設定。 這也是 Web 應用程式開發介面其中插入 toohello*主機*，這將可再次回到稍後。 

**Startup.cs**

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

這是 hello 應用程式組件。 此時，我們設定只 hello 基本 Web API 專案版面配置。 目前為止，它不應該看起來非常不同，從 Web API 專案，您可能會寫入 hello 過去或 hello 基本 Web API 範本。 您的商務邏輯則是放在 hello 控制站和模型像往常一樣。

現在我們怎麼辦才能實際執行裝載？

## <a name="service-hosting"></a>服務裝載
在 Service Fabric 中，您的服務會在服務主機處理序 中執行，這是執行您的服務程式碼的可執行檔。 當您使用 hello 可靠的服務應用程式開發介面撰寫的服務時，您的服務專案只會編譯 tooan 可執行檔，註冊您的服務類型，並執行您的程式碼。 當您在 .NET 中的 Service Fabric 上撰寫服務時，在大部分情況下都是如此。 當您開啟 Program.cs hello 無狀態服務專案中時，您應該會看到：

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

如果這看起來可疑像是 hello 進入點 tooa 主控台應用程式，這是因為它是。

進一步詳細 hello 服務主機處理序與服務登錄已超出本文的 hello 範圍。 但它是用於重要 tooknow 現在*自己的處理序中執行您的服務程式碼*。

## <a name="self-host-web-api-with-an-owin-host"></a>自我裝載 Web API 與 OWIN 主機
假設您的 Web API 應用程式程式碼裝載在自己的處理序，如何具 tooa web 伺服器？ 輸入 [OWIN](http://owin.org/)。 OWIN 只是 .NET Web 應用程式和 Web 伺服器之間的合約。 傳統上使用 ASP.NET （向上 tooMVC 5) 時，hello web 應用程式是透過 System.Web 緊密結合的 tooIIS。 不過，Web 應用程式開發介面會實作 OWIN，所以您可以撰寫分離 web 應用程式，從它裝載的 hello web 伺服器。 因此，您可以使用可在自己的程序中啟動的自我裝載  OWIN web 伺服器。 這完全符合我們剛說明 hello Service Fabric 裝載模型。

在本文中，我們會使用為 hello OWIN 主機 Katana hello Web API 應用程式。 Katana 是根據開放原始碼 OWIN 主機實作[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)和 hello Windows [HTTP 伺服器 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)。

> [!NOTE]
> 深入了解 Katana，移 toohello toolearn [Katana 網站](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana)。 如需快速概觀 toouse Katana tooself 主機 Web API，請參閱[使用 OWIN tooSelf 主機 ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api)。
> 
> 

## <a name="set-up-hello-web-server"></a>設定 hello 網頁伺服器
hello 可靠的服務應用程式開發介面提供，以便讓使用者和用戶端 tooconnect toohello 服務的通訊堆疊中插入通訊進入點：

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

hello 網頁伺服器 （和任何其他通訊堆疊，您用於未來的例如 WebSockets hello） 應該使用 hello ICommunicationListener 介面 toointegrate 正確 hello 系統。 這個 hello 原因將會變得更加明顯 hello 步驟中的。

首先，建立一個稱為 OwinCommunicationListener 的類別，其實作 ICommunicationListener：

**OwinCommunicationListener.cs：**

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

hello ICommunicationListener 介面提供三個方法 toomanage 通訊接聽程式為您的服務：

* 。 開始接聽要求。
* 。 停止接聽要求，完成任何進行中的要求，並正常關機。
* 中止。 取消所有項目，並立即停止。

項目 hello 接聽程式將會需要 toofunction tooget 啟動，加入私用類別成員。 這些會初始化透過 hello 建構函式，並稍後使用，當您設定 hello 接聽的 URL。

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a>實作 OpenAsync
tooset hello web 伺服器，您需要兩個資訊片段：

* *URL 路徑前置詞*。 雖然這是選擇性的它是適合您 tooset 這個向上現在，讓您安全地可以裝載多個 web 服務應用程式中。
* *連接埠*。

取得 hello web 伺服器的連接埠之前，重要的是您了解 Service Fabric 提供應用程式層級，可做為您的應用程式與 hello 基礎作業系統上執行之間的緩衝區。 因此，Service Fabric 提供方式 tooconfigure*端點*為您的服務。 Service Fabric 可確保端點可供服務 toouse。 如此一來，您不需要 tooconfigure 它們自己 hello 基礎作業系統環境中。 您輕鬆地可以主控 Service Fabric 應用程式中不同的環境，而不需要 toomake 任何變更 tooyour 應用程式。 (例如，您也可以裝載 hello 自己的資料中心或 Azure 中相同的應用程式。)

在 PackageRoot\ServiceManifest.xml 中設定 HTTP 端點：

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

這個步驟很重要，因為受限制的認證 （Windows 上的網路服務） 下執行 hello 服務主機處理序。 這表示您的服務將不會有存取 tooset HTTP 端點，其本身。 藉由使用 hello 端點組態，Service Fabric 會知道 hello 服務的 URL 會接聽 tooset hello 適當的存取控制清單 (ACL)。 服務網狀架構也提供標準位置 tooconfigure 端點。

返回 OwinCommunicationListener.cs 中，您可以開始實作 OpenAsync。 這是您用來啟動 hello web 伺服器。 首先，取得 hello 端點資訊，並建立 hello hello 服務將接聽的 URL。 hello URL 將是 hello 接聽程式是否使用中的無狀態的服務或可設定狀態的服務而有所不同。 可設定狀態的服務，hello 接聽程式需要唯一的每一個可設定狀態的服務複本它會接聽在位址的 toocreate。 針對無狀態服務，hello 位址可以是簡單許多。 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

請注意這裡用 "http://+"。 這是 toomake 確定該 hello 網頁伺服器正在接聽所有可用的位址，包括 localhost、 FQDN 和 hello 機器的 IP。

hello OpenAsync 實作是 hello 最重要原因之一為什麼 hello 網頁伺服器 （或任何通訊堆疊） 實作直接從 ICommunicationListener，而不是只將它開啟`RunAsync()`hello 服務中。 hello OpenAsync 傳回值是 hello hello web 伺服器的位址接聽。 這個地址傳回 toohello 系統時，它會向 hello 服務註冊 hello 位址。 Service Fabric 提供 API，可讓用戶端和其他服務 toothen，已要求此位址的服務名稱。 這是很重要，因為 hello 服務位址不是靜態。 服務會移動 hello 叢集中進行資源平衡和可用性。 這是 hello 機制，可讓用戶端 tooresolve hello 接聽服務位址。

這一點，OpenAsync 啟動 hello web 伺服器，並傳回 hello 位址上接聽。 請注意，它會接聽"http://+"，但 OpenAsync 傳回 hello 位址之前，hello"+"會取代 hello IP 或 FQDN，目前在 hello 節點。 這個方法所傳回的 hello 位址是向 hello 系統。 它也是用戶端和其他服務要求服務位址時所看到的位址。 如需用戶端 toocorrectly 連接 tooit、 hello 位址中需要實際的 IP 或 FQDN。

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

請注意這參考傳入 toohello OwinCommunicationListener hello 建構函式中的 hello 啟動類別。 Hello web 伺服器 toobootstrap hello Web API 應用程式會使用這個啟動執行個體。

hello`ServiceEventSource.Current.Message()`行稍後會顯示 hello 診斷事件視窗中，當您執行 hello 應用程式 tooconfirm hello 網頁伺服器已順利啟動。

## <a name="implement-closeasync-and-abort"></a>實作 CloseAsync 和 Abort
最後，實作 CloseAsync 與 Abort toostop hello web 伺服器。 hello web 伺服器可以透過處置 OpenAsync 期間所建立的 hello 伺服器控點停止。

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

實作在本例中，CloseAsync 和中止只會停止 hello web 伺服器。 您也可以選擇 tooperform CloseAsync hello web 伺服器的更適當地協調關機。 例如，hello 關機無法等候進行中的要求 toobe hello 傳回之前完成。

## <a name="start-hello-web-server"></a>啟動 hello web 伺服器
您現在已經準備就緒 toocreate，並傳回 OwinCommunicationListener toostart hello web 伺服器的執行個體。 在 hello 服務類別 (WebService.cs)，覆寫 hello`CreateServiceInstanceListeners()`方法：

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

這是其中 hello Web API*應用程式*和 hello OWIN*主機*最後符合。 hello 主機 (OwinCommunicationListener) 會指定執行個體的 hello*應用程式*(Web API) 透過 hello 啟動類別。 然後 Service Fabric 會管理其生命週期。 通常可以針對任何通訊堆疊運用相同的模式。

## <a name="put-it-all-together"></a>組合在一起
在此範例中，您不需要任何項目在 hello toodo`RunAsync()`方法，因此只會移除覆寫。

hello 最終服務實作應該非常簡單。 它只需要 toocreate hello 通訊接聽程式：

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

完整的 hello`OwinCommunicationListener`類別：

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

既然您已經就地將 hello 的所有項目，您的專案看起來應該像一般 Web API 應用程式使用可靠的服務應用程式開發介面的進入點和 OWIN 主機。

## <a name="run-and-connect-through-a-web-browser"></a>透過 Web 瀏覽器執行並連線
如果您尚未這麼做，請 [設定開發環境](service-fabric-get-started.md)。

您現在可以建置並部署您的服務。 按**F5**在 Visual Studio toobuild 並部署 hello 應用程式。 在 hello 診斷事件視窗中，您應該會看到一個訊息，指出 http://localhost:8281 上開啟該 hello 網頁伺服器 /。

> [!NOTE]
> 如果 hello 連接埠已經開啟您的電腦上的另一個處理序，您可能會看到以下錯誤。 這表示無法開啟該 hello 接聽項。 如果這 hello 案例，請嘗試使用不同的通訊埠 hello ServiceManifest.xml 中的端點組態。
> 
> 

一旦 hello 服務正常執行，請開啟瀏覽器，並瀏覽太[http://localhost:8281/api/值](http://localhost:8281/api/values)tootest 它。

## <a name="scale-it-out"></a>相應放大
向外延展無狀態的 web 應用程式通常表示加入更多電腦，並向上 hello web 應用程式在其上。 Service Fabric 協調流程引擎可以這麼做為您每當 tooa 叢集中加入新的節點。 當您建立無狀態服務的執行個體時，您可以指定 hello 數目要 toocreate 的執行個體。 Service Fabric hello 叢集中節點上，將該執行個體數目。 它可確保不 toocreate 多個執行個體的任何一個節點上。 您也可以指示 Service Fabric tooalways 每個節點上建立執行個體，藉由指定**-1** hello 執行個體計數。 這樣可保證，每當您將節點 tooscale 出您的叢集時，您無狀態服務的執行個體將會建立 hello 新節點上。 這個值是 hello 服務執行個體的屬性，所以它會設定當您建立的服務執行個體。 您可以透過 PowerShell 設定：

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

您也可以在 Visual Studio 無狀態服務專案中定義預設服務時設定：

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

如需有關如何 toocreate 應用程式和服務執行個體，請參閱[部署應用程式](service-fabric-deploy-remove-applications.md)。

## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 偵錯 Service Fabric 應用程式](service-fabric-debugging-your-application.md)

