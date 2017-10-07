---
title: "aaaConnect 並與 Azure Service Fabric 服務 |Microsoft 文件"
description: "了解如何 tooresolve，連線，並與服務的網狀架構中的服務通訊。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>連接至 Service Fabric 中的服務並與其進行通訊
在 Service Fabric 中，服務會在 Service Fabric 叢集中的某處執行，通常是分散到多個 VM。 可以移動它從同一個地方 tooanother hello 服務擁有者，或自動 Service Fabric。 服務不是靜態繫結的 tooa 特定電腦或位址。

Service Fabric 應用程式通常是由許多不同的服務組成，每一個服務用來執行特定的工作。 完整的函式，例如轉譯的 web 應用程式的不同部分時，可能會與彼此 tooform 通訊這些服務。 也有一些用戶端連接 tooand 的應用程式與服務通訊。 本文將討論如何 tooset 和服務網狀架構中的服務之間的通訊。

這段 Microsoft Virtual Academy 影片也會討論服務通訊︰<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>引進您自己的通訊協定
Service Fabric 幫助您管理您的服務的 hello 生命週期，但不會決定有關您的服務所執行的作業。 這包含通訊： 服務網狀架構，您的服務端點的連入要求的機會 tooset，開啟您的服務使用的任何通訊協定或通訊堆疊的需求。 您的服務會接聽一般 **IP:port** 位址，使用任何定址配置，例如 URI。 多個服務執行個體或複本可能會共用主控件程序，在此情況下它們將會需要不同連接埠 toouse 或使用連接埠共用機制，例如 windows hello http.sys 核心驅動程式。 在任一情況下，主機處理序中的每個服務執行個體或複本必須可以唯一定址。

![服務端點][1]

## <a name="service-discovery-and-resolution"></a>服務探索和解析
在分散式系統中，服務可能會從一部機器 tooanother 隨著時間而移。 發生這種情形的原因有很多，包括資源平衡、升級、容錯移轉或向外延展。這表示服務端點位址變更為 hello 服務移 toonodes 具有不同的 IP 位址，並可能會在不同的連接埠上開啟如果 hello 服務會使用動態選取的連接埠。

![服務的分佈][7]

Service Fabric 提供探索和解決方式呼叫服務 hello 命名服務。 hello 命名服務會維護對應的資料表命名為服務執行個體 toohello 它們接聽的端點位址。 Service Fabric 中的所有已命名服務執行個體，皆如 URI 擁有唯一的名稱，例如， `"fabric:/MyApplication/MyService"`。 hello hello 服務名稱不會隨 hello hello 服務存留期間變更，就只有 hello 端點位址，可以變更服務移動時。 這是類似 toowebsites 有常數的 Url，但可能會在其中變更 hello IP 位址。 可解決網站 Url tooIP 位址，hello 網站上的類似 tooDNS Service Fabric 服務名稱 tootheir 端點位址，對應的註冊機構。

![服務端點][2]

解決和連接 tooservices 牽涉到下列步驟執行，在迴圈中的 hello:

* **解決**: 服務已從發行的 Get hello 端點 hello 命名服務。
* **連接**： 透過 toohello 服務指定任何通訊協定就會使用該端點上的。
* **重試**： 連接嘗試可能會失敗的原因，例如，如果 hello 服務已移動，因為 hello 最後一個時間 hello 端點位址已解決任何數目。 在此情況下，hello 之前解決並連接步驟需要 toobe 重試，而且這個循環會重複進行直到 hello 連線成功。

## <a name="connecting-tooother-services"></a>Tooother 服務連線
服務連接 tooeach 其他叢集內通常可以直接存取的其他服務的 hello 端點由於 hello 叢集中的節點位於 hello 相同的區域網路。 toomake 更容易 tooconnect 服務之間，Service Fabric 提供使用的其他服務 hello 命名服務。 DNS 服務和反向 proxy 服務。


### <a name="dns-service"></a>DNS 服務
因為許多服務，特別是容器化服務，可以有現有的 URL 名稱，所以無法 tooresolve 這些使用 hello 標準 DNS 通訊協定 （而非 hello 命名服務通訊協定），是很方便，尤其是在應用程式 「 提起和 shift 」案例。 這正是哪些 hello DNS 服務會。 它可讓您 toomap DNS 名稱 tooa 服務名稱，並因此解決端點 IP 位址。 

中所顯示的 hello 與下列圖表中，hello hello Service Fabric 叢集中執行的 DNS 服務對應然後 hello 命名服務 tooreturn hello 端點位址 tooconnect 至來解析 DNS 名稱 tooservice 名稱。 hello hello 服務的 DNS 名稱是在建立 hello 時提供。 

![服務端點][9]

如需有關如何查看 toouse hello DNS 服務[DNS 服務在 Azure Service Fabric](service-fabric-dnsservice.md)發行項。

### <a name="reverse-proxy-service"></a>反向 Proxy服務
服務會公開包括 HTTPS 的 HTTP 端點的 hello 叢集中的 hello 反向 proxy 位址。 hello 反向 proxy 大幅簡化呼叫其他服務和其方法，讓特定 URI 格式和連接控制代碼 hello 解決，，所需的一項服務 toocommunicate 與另一個使用的重試步驟 hello 命名服務。 換句話說，它會隱藏 hello 從您的命名服務藉由這只要呼叫 URL 呼叫其他服務時。

![服務端點][10]

如需如何 toouse hello 反向 proxy 服務的詳細資訊，請參閱[反向 proxy，在 Azure Service Fabric](service-fabric-reverseproxy.md)發行項。

## <a name="connections-from-external-clients"></a>從外部用戶端連接
服務連接 tooeach 其他叢集內通常可以直接存取的其他服務的 hello 端點由於 hello 叢集中的節點位於 hello 相同的區域網路。 但是，在相同的環境中，叢集可能會位於負載平衡器後方，該負載平衡器會透過有限制的一組連接埠路由傳送外部輸入流量。 在這些情況下，仍可以與對方進行通訊及解析的地址使用 hello 命名服務，但額外的步驟必須採用的 tooallow 外部用戶端 tooconnect tooservices 服務。

## <a name="service-fabric-in-azure"></a>Azure 中的 Service Fabric
Azure 中的 Service Fabric 叢集位於 Azure 負載平衡器後方。 所有外部流量 toohello 叢集必須經過 hello 負載平衡器。 hello 負載平衡器會自動轉送流量輸入隨機指定的連接埠 tooa*節點*具有相同的通訊埠開啟的 hello。 hello Azure 負載平衡器只知道在 hello 上開啟的連接埠*節點*，並不知道有關由個別的連接埠開啟*服務*。

![Azure 負載平衡器和 Service Fabric 拓撲][3]

例如，在連接埠上順序 tooaccept 外部流量**80**，必須設定下列項目 hello:

1. 寫入在連接埠 80 上接聽的服務。 在 hello 服務 ServiceManifest.xml 中設定連接埠 80，接聽程式中開啟 hello 服務，例如自我裝載的 web 伺服器。

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. 在 Azure 中建立 Service Fabric 叢集，並指定連接埠**80**作為自訂端點連接埠將主控 hello 服務的 hello 節點型別。 如果您有一個以上的節點型別時，您可以設定*位置條件約束*hello 服務 tooensure 它只會執行具有開啟的 hello 自訂端點連接埠的 hello 節點型別的上。

    ![開啟節點類型上的連接埠][4]
3. 一旦建立 hello 叢集之後，設定 hello Azure 負載平衡器的連接埠 80 上的 hello 叢集資源群組 tooforward 流量。 在建立叢集，以透過 hello Azure 入口網站時，這會自動設定每一個已設定的自訂端點連接埠。

    ![轉送流量在 hello Azure 負載平衡器][5]
4. 是否 hello Azure 負載平衡器使用探查 toodetermine 或不 toosend 流量 tooa 特定節點。 hello 探查定期檢查正在回應 hello 節點每個節點 toodetermine 上的端點。 如果 hello 探查失敗 tooreceive 回應設定的次數之後，hello 負載平衡器會停止傳送流量 toothat 節點。 建立叢集，以透過 hello Azure 入口網站，探查會自動設定每一個已設定的自訂端點連接埠。

    ![轉送流量在 hello Azure 負載平衡器][8]

它是 hello Azure 負載平衡器與 hello 探查只知道 hello 的重要 tooremember*節點*，不 hello*服務*hello 節點上執行。 hello Azure 負載平衡器仍會一律傳送回應 toohello 探查的流量 toonodes，所以必須特別小心 tooensure 可用的服務可以 toorespond toohello 探查 hello 節點上。

## <a name="reliable-services-built-in-communication-api-options"></a>Reliable Services：內建的通訊 API 選項
hello 可靠的服務架構隨附數個預先建立的通訊選項。 其中一個最適合您的 hello 決策取決於 hello 所選擇的程式設計模型、 hello 通訊架構及程式設計語言撰寫您的服務中的 hello hello。

* **沒有任何特定的通訊協定：**如果您不需要特定的通訊架構選擇，但您想 tooget 項目啟動並執行快速，則 hello 理想的選項是[服務遠端處理](service-fabric-reliable-services-communication-remoting.md)，可讓可靠的服務和 Reliable Actors 強型別遠端程序呼叫。 這是 hello 最簡單且最快方式 tooget 啟動服務通訊。 遠端服務會處理服務位址、連接、重試和錯誤處理的解析。 這同時適用 C# 和 Java 應用程式。
* **HTTP**︰對於無從驗證語言的通訊，HTTP 提供業界標準的選擇，具有工具與許多不同語言的 HTTP 伺服器，都受到 Service Fabric 的支援。 服務可以使用任何可用的 HTTP 堆疊，包括 C# 應用程式適用的 [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md)。 在 C# 撰寫的用戶端可以利用 hello`ICommunicationClient`和`ServicePartitionClient`類別，而 for Java，請使用 hello`CommunicationClient`和`FabricServicePartitionClient`類別， [service 解析、 HTTP 連接和重試迴圈](service-fabric-reliable-services-communication.md)。
* **WCF**： 如果您有現有程式碼使用 WCF 與您通訊的架構，則您可以使用 hello `WcfCommunicationListener` hello 伺服器端和`WcfCommunicationClient`和`ServicePartitionClient`hello 用戶端類別。 不過，這只適用以 Windows 為基礎的叢集上的 C# 應用程式。 如需詳細資訊，請參閱這篇文章關於[WCF 為基礎的 hello 通訊堆疊實作](service-fabric-reliable-services-communication-wcf.md)。

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>使用自訂通訊協定以及其他通訊架構
服務可以使用任何通訊協定或架構進行通訊，無論是透過 TCP 通訊端的自訂二進位通訊協定，或透過 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)或 [Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)的串流事件。 Service Fabric 提供通訊應用程式開發介面中所有 hello 運作 toodiscover 並連接時，您可以插入您的通訊堆疊，從您區隔。 請參閱本文有關 hello[可靠的服務通訊模型](service-fabric-reliable-services-communication.md)如需詳細資訊。

## <a name="next-steps"></a>後續步驟
了解 hello 概念與應用程式開發介面提供 hello[可靠的服務通訊模型](service-fabric-reliable-services-communication.md)，然後快速開始使用[服務遠端處理](service-fabric-reliable-services-communication-remoting.md)或如何移深入 toolearn toowrite通訊接聽程式使用[與 OWIN 自我裝載的 Web API](service-fabric-reliable-services-communication-webapi.md)。

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
