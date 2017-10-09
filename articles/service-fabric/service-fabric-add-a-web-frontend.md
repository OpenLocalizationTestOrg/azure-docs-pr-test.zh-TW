---
title: "使用 ASP.NET Core Azure Service Fabric 應用程式的 web 前端 aaaCreate |Microsoft 文件"
description: "使用 ASP.NET Core 專案和服務間的通訊透過服務遠端公開 Service Fabric 應用程式 toohello web。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>使用 ASP.NET Core 建置應用程式的 Web 服務前端
根據預設，Azure Service Fabric 服務不提供公用介面 toohello web。 tooexpose 功能 tooHTTP 用戶端應用程式，您有 web 專案 tooact 做為進入點，然後從那裡 tooyour 通訊的 toocreate 個別的服務。

在本教學課程中，我們挑選我們離開的地方在 hello [Visual Studio 中建立第一個應用程式](service-fabric-create-your-first-application-in-visual-studio.md)教學課程和加入 ASP.NET Core web 服務前方 hello 可設定狀態的計數器服務。 如果您尚未這麼做，請返回並先逐步進行該教學課程。

## <a name="set-up-your-environment-for-aspnet-core"></a>設定環境使其適用於 ASP.NET Core

您需要 Visual Studio 2017 toofollow 本教學課程。 任何版本都可以。 

 - [安裝 Visual Studio 2017](https://www.visualstudio.com/)

toodevelop ASP.NET Core Service Fabric 應用程式，您應該有下列安裝的工作負載的 hello:
 - **Azure 開發** (在 [Web 和 Cloud] 之下)
 - **ASP.NET 與 Web 開發** (在 [Web 和 Cloud] 之下)
 - **.NET Core 跨平台開發** (在 [其他工具集] 之下)

>[!Note] 
>hello.NET Core tools for Visual Studio 2015 不會再正在更新，但是如果您仍在使用 Visual Studio 2015，您必須 toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core)安裝。

## <a name="add-an-aspnet-core-service-tooyour-application"></a>加入 ASP.NET Core service tooyour 應用程式
ASP.NET Core 是輕量型、 跨平台的 web 開發架構，您可以使用 toocreate 新式 web UI 和 web 應用程式開發介面。 

讓我們加入 ASP.NET Web API 專案 tooour 現有的應用程式。

1. 在 方案總管 中，以滑鼠右鍵按一下**服務**內 hello 應用程式專案，然後選擇 **新增 > 新增 Service Fabric 服務**。
   
    ![加入新的服務 tooan 現有應用程式][vs-add-new-service]
2. 在 hello**建立服務**頁面上，選擇**ASP.NET Core**並為它命名。
   
    ![在 [hello 新增服務] 對話方塊中選擇 ASP.NET web 服務][vs-new-service-dialog]

3. hello 下一個頁面會提供一組 ASP.NET Core 專案範本。 請注意，這些是 hello 相同，您會看到 是否您只需要編寫小量的額外的程式碼 tooregister 建立 Service Fabric 應用程式之外的 ASP.NET Core 專案選擇 hello 與 hello Service Fabric 執行階段服務。 在本教學課程中，選擇 [Web API]。 但是，您可以套用 hello 相同概念 toobuilding 完整 web 應用程式。
   
    ![選擇 ASP.NET 專案類型][vs-new-aspnet-project-dialog]
   
    建立 Web API 專案後，您的應用程式中應有兩個服務。 當您繼續 toobuild 您的應用程式，您可以加入更多服務完全 hello 中相同的方式。 每個服務都可以獨立設定版本和升級。

## <a name="run-hello-application"></a>執行 hello 應用程式
tooget 完成的內容，讓我們了解部署 hello 新應用程式，並採取提供查看 hello hello ASP.NET Core Web API 範本的預設行為。

1. 在 Visual Studio toodebug hello 應用程式，請按 F5。
2. 部署完成時，Visual Studio 會啟動瀏覽器 toohello 根的 hello ASP.NET Web API 服務。 hello ASP.NET Core Web API 範本不會提供預設行為 hello 根目錄，因此您應該會看到 404 錯誤 hello 瀏覽器中。
3. 新增`/api/values`toohello hello 瀏覽器中的位置。 這樣會叫用 hello`Get`上 hello ValuesController hello Web API 範本中的方法。 它會傳回所提供的 hello 範本--JSON 陣列，其中包含兩個字串 hello 預設回應：
   
    ![從 ASP.NET Core Web API 範本傳回的預設值][browser-aspnet-template-values]
   
    根據 hello hello 教學課程結束，此頁面會顯示我們可設定狀態的服務，而不是 hello hello 最近計數器值的預設字串。

## <a name="connect-hello-services"></a>Hello 服務連接
對於您與可靠服務通訊的方式，Service Fabric 會提供完整的彈性。 在單一應用程式中，您可能擁有可透過 TCP 存取的服務、可透過 HTTP REST API 存取的其他服務，並且還有其他可透過 Web 通訊端存取的服務。 如需有關可用的 hello 選項以及 hello 權衡取捨的背景，請參閱[與服務通訊](service-fabric-connect-and-communicate-with-services.md)。 在此教學課程中，我們使用[Service Fabric 服務遠端處理](service-fabric-reliable-services-communication-remoting.md)hello SDK 中提供。

Hello （模擬遠端程序呼叫或 Rpc） 服務遠端處理方法，在中，您會定義介面 tooact 為 hello hello 服務公開的合約。 然後，您可以使用該介面 toogenerate proxy 類別與 hello 服務互動。

### <a name="create-hello-remoting-interface"></a>建立 hello 遠端介面
讓我們開始建立 hello 介面 tooact 做為 hello hello 可設定狀態的服務和其他服務，在此案例的 hello ASP.NET Core web 專案之間的合約。 此介面必須使用 toomake RPC 呼叫，因此我們將建立它自己的類別庫專案中的所有服務所共用。

1. 在 [方案總管] 中，以滑鼠右鍵按一下您的方案並選擇 [加入] **將** > 。

2. 選擇 hello **Visual C#** hello 左瀏覽窗格中，然後選取 hello 中的項目**類別庫**範本。 請確定該 hello.NET Framework 版本設定太**4.5.2**。
   
    ![為具狀態服務建立介面專案][vs-add-class-library-project]

3. 安裝 hello **Microsoft.ServiceFabric.Services.Remoting** NuGet 封裝。 搜尋**Microsoft.ServiceFabric.Services.Remoting**在 hello NuGet 封裝管理員，並將它安裝在 hello 方案中使用服務遠端處理的所有專案包括：
   - hello 包含 hello 服務介面的類別庫專案
   - hello 可設定狀態服務專案
   - hello ASP.NET Core web 服務專案
   
    ![正在將 hello 服務 NuGet 封裝][vs-services-nuget-package]

4. Hello 類別庫中建立的介面具有單一方法， `GetCountAsync`，並擴充 hello 介面從`Microsoft.ServiceFabric.Services.Remoting.IService`。 hello 遠端介面必須衍生自這個介面 tooindicate 它已服務遠端處理介面。
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>在您可設定狀態的服務中實作 hello 介面
既然我們已經定義 hello 介面，現在需要 tooimplement 在 hello 具狀態服務。

1. 在您可設定狀態的服務中，加入包含 hello 介面的參考 toohello 類別庫專案。
   
    ![在 hello 具狀態服務中加入參考 toohello 類別庫專案][vs-add-class-library-reference]
2. 找出 hello 類別繼承自`StatefulService`，例如`MyStatefulService`，並將它延伸 tooimplement hello`ICounter`介面。
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. 現在，實作 hello hello 中定義的單一方法`ICounter`介面， `GetCountAsync`。
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>公開 hello 可設定狀態的服務，使用服務遠端接聽程式
以 hello`ICounter`介面實作，hello 最後一個步驟是 tooopen hello 服務遠端處理通訊通道。 對於具狀態服務，Service Fabric 會提供稱為 `CreateServiceReplicaListeners`的可覆寫方法。 使用此方法，您可以指定一或多個通訊接聽程式，根據您想 tooenable，為您的服務通訊的 hello 類型。

> [!NOTE]
> hello 等的方法，以開啟通訊通道 toostateless 服務稱為`CreateServiceInstanceListeners`。

在此情況下，我們將取代現有的 hello`CreateServiceReplicaListeners`方法，並提供的執行個體`ServiceRemotingListener`，這會建立 RPC 端點是可從用戶端透過呼叫`ServiceProxy`。  

hello `CreateServiceRemotingListener` hello 上的擴充方法`IService`介面可讓您 tooeasily 建立`ServiceRemotingListener`使用所有預設設定。 toouse 這個擴充方法，請確定您有 hello`Microsoft.ServiceFabric.Services.Remoting.Runtime`匯入的命名空間。 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>使用 hello ServiceProxy 類別 toointeract 與 hello 服務
我們可設定狀態的服務是透過 RPC 現在準備好 tooreceive 流量從其他服務。 因此，仍然從 hello ASP.NET web 服務加入 hello 與它的程式碼 toocommunicate。

1. 在 ASP.NET 專案中，新增參考 toohello 類別庫包含 hello`ICounter`介面。

2. 您稍早加入 hello **Microsoft.ServiceFabric.Services.Remoting** NuGet 封裝 toohello ASP.NET 專案。 此封裝提供 hello`ServiceProxy`類別您使用 toomake RPC 呼叫 toohello 可設定狀態的服務。 請確認此 NuGet 封裝安裝在 hello ASP.NET Core web 服務專案。

4. 在 hello**控制器**資料夾中，開啟 hello`ValuesController`類別。 請注意該 hello`Get`方法目前只會傳回"value1"和"value2"-符合我們稍早在 hello 瀏覽器中看到的硬式編碼的字串陣列。 取代這項實作以下列程式碼的 hello:
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    hello 第一行程式碼是 hello 金鑰一。 toocreate hello ICounter proxy toohello 具狀態服務，您需要 tooprovide 兩項資訊： hello 服務的分割區識別碼和 hello 名稱。
   
    您可以使用資料分割的 tooscale 可設定狀態服務分割成不同的值區，其狀態根據定義，例如客戶編號或郵遞區號的索引鍵。 一般應用程式中，在 hello 可設定狀態的服務只有一個資料分割，所以 hello 金鑰並不重要。 您提供任何索引鍵時，會造成 toohello 相同的資料分割。 toolearn 進一步了解資料分割的服務，請參閱[如何 toopartition Service Fabric 可靠服務](service-fabric-concepts-partitioning.md)。
   
    hello 服務名稱是 hello 表單網狀架構的 URI: /&lt;application_name&gt;/&lt;service_name&gt;。
   
    使用這兩個資訊片段，Service Fabric 可唯一識別要求應該要傳送的 hello 機器。 hello`ServiceProxy`類別也順暢地處理 hello 案例，其中裝載 hello 可設定狀態的服務資料分割的 hello 機器失敗，而另一部電腦必須升級的 tootake 其所在位置。 這個抽象層可讓撰寫 hello 與其他服務簡單得多的用戶端程式碼 toodeal。
   
    一旦 hello proxy，我們只叫用 hello`GetCountAsync`方法並傳回其結果。

5. 按 F5 再次 toorun hello 修改應用程式。 為之前，Visual Studio 會自動啟動 hello web 專案的 hello 瀏覽器 toohello 根目錄。 加入 hello 「 api/值 」 的路徑，以及您應該會看到 hello 傳回目前計數器值。
   
    ![hello 瀏覽器中顯示 hello 可設定狀態的計數器值][browser-aspnet-counter-value]
   
    重新整理 hello 瀏覽器定期 toosee hello 計數器值更新。

## <a name="kestrel-and-weblistener"></a>Kestrel 和 WebListener

hello 預設 ASP.NET Core web 伺服器，又稱為 Kestrel，是[目前不支援處理直接網際網路流量](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)。 如此一來，hello 適用於 Service Fabric ASP.NET Core 無狀態的服務範本會使用[WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener)預設。 

Service Fabric 服務中的深入了解 Kestrel 和 WebListener toolearn，請參閱太[Service Fabric 可靠的服務中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)。

## <a name="connecting-tooa-reliable-actor-service"></a>連接 tooa Reliable Actor 服務
本教學課程著重於新增會與具狀態服務通訊的 Web 前端。 不過，您可以依照類似的模型 tootalk tooactors。 當您建立 Reliable Actor 專案時，Visual Studio 會自動替您產生介面專案。 您可以使用該介面 toogenerate 執行者 proxy hello web 專案 toocommunicate 中，與 hello 動作項目。 會自動提供 hello 通訊通道。 因此您不需要 toodo 任何項目，是對等 tooestablishing`ServiceRemotingListener`像 hello 可設定狀態服務在本教學課程。

## <a name="how-web-services-work-on-your-local-cluster"></a>Web 服務在本機叢集上的運作方式
一般情況下，您可以部署完全 hello 相同 Service Fabric 應用程式 tooa 多電腦叢集您部署您的本機叢集上，並深信高它如預期運作。 這是因為您的本機叢集只是五個節點的組態是摺疊 tooa 單一電腦。

Tooweb 服務時，不過，還有一個索引鍵的細微差別。 當叢集位於負載平衡器後方，如同在 Azure 中時，您必須確保您的 web 服務每台機器上部署 hello 負載平衡器後只循 robins 流量分散到 hello 電腦。 您可以透過設定 hello `InstanceCount` hello 服務 toohello 特殊值"-1"。

相反地，當您在本機執行 web 服務，您需要 tooensure hello 服務該只有一個執行個體正在執行。 否則，您遇到衝突都在接聽 hello 相同的多個處理序從路徑與連接埠。 如此一來，hello web 服務執行個體計數應該設定太"1"的本機部署。

如何 tooconfigure 不同的值不同的環境，請參閱的 toolearn[管理多個環境的應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)。

## <a name="next-steps"></a>後續步驟
現在，您已使用 ASP.NET Core 為應用程式設定 Web 前端，請參閱 [Service Fabric Reliable Services 中的 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 以深入了解 ASP.NET Core 如何與 Service Fabric 合作。

下一步[深入了解與服務通訊](service-fabric-connect-and-communicate-with-services.md)一般的完整 tooget 圖片的服務如何通訊適用於 Service Fabric。

一旦您已經了解的服務通訊的運作方式，[在 Azure 中建立叢集，並部署您的應用程式 toohello 雲端](service-fabric-cluster-creation-via-portal.md)。

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
