---
title: "連接至 Azure Service Fabric 中的服務並與其進行通訊 | Microsoft Docs"
description: "了解如何解析、連接至 Service Fabric 應用程式中的服務並與其進行通訊。"
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
ms.openlocfilehash: 3e61ad19df34c6a57da43e26bd2ab9d7ecdbf98e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="edda7-103">連接至 Service Fabric 中的服務並與其進行通訊</span><span class="sxs-lookup"><span data-stu-id="edda7-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="edda7-104">在 Service Fabric 中，服務會在 Service Fabric 叢集中的某處執行，通常是分散到多個 VM。</span><span class="sxs-lookup"><span data-stu-id="edda7-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="edda7-105">它可以由服務擁有者或是 Service Fabric 自動從某個位置移到其他位置。</span><span class="sxs-lookup"><span data-stu-id="edda7-105">It can be moved from one place to another, either by the service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="edda7-106">服務無法以靜態方式繫結至特定電腦或位址。</span><span class="sxs-lookup"><span data-stu-id="edda7-106">Services are not statically tied to a particular machine or address.</span></span>

<span data-ttu-id="edda7-107">Service Fabric 應用程式通常是由許多不同的服務組成，每一個服務用來執行特定的工作。</span><span class="sxs-lookup"><span data-stu-id="edda7-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="edda7-108">這些服務可能會彼此進行通訊以形成完整的函式，例如轉譯 Web 應用程式的不同部分。</span><span class="sxs-lookup"><span data-stu-id="edda7-108">These services may communicate with each other to form a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="edda7-109">有些用戶端應用程式會連接到服務並與其通訊。</span><span class="sxs-lookup"><span data-stu-id="edda7-109">There are also client applications that connect to and communicate with services.</span></span> <span data-ttu-id="edda7-110">本文件討論如何設定您在 Service Fabric 中的服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="edda7-110">This document discusses how to set up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="edda7-111">這段 Microsoft Virtual Academy 影片也會討論服務通訊︰<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="edda7-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="edda7-112">引進您自己的通訊協定</span><span class="sxs-lookup"><span data-stu-id="edda7-112">Bring your own protocol</span></span>
<span data-ttu-id="edda7-113">Service Fabric 可以幫助管理您的服務的生命週期，但是它不會決定您的服務要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="edda7-113">Service Fabric helps manage the lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="edda7-114">這包含通訊：</span><span class="sxs-lookup"><span data-stu-id="edda7-114">This includes communication.</span></span> <span data-ttu-id="edda7-115">當您的服務是由 Service Fabric 開啟時，就是您的服務設定連入要求端點的機會，使用您想要的任何通訊協定或通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="edda7-115">When your service is opened by Service Fabric, that's your service's opportunity to set up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="edda7-116">您的服務會接聽一般 **IP:port** 位址，使用任何定址配置，例如 URI。</span><span class="sxs-lookup"><span data-stu-id="edda7-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="edda7-117">多個服務執行個體或複本可能共用主機處理序，在此情況下，它們必須使用不同的連接埠，或使用連接埠共用機制，如 Windows 的 http.sys 核心驅動程式。</span><span class="sxs-lookup"><span data-stu-id="edda7-117">Multiple service instances or replicas may share a host process, in which case they will either need to use different ports or use a port-sharing mechanism, such as the http.sys kernel driver in Windows.</span></span> <span data-ttu-id="edda7-118">在任一情況下，主機處理序中的每個服務執行個體或複本必須可以唯一定址。</span><span class="sxs-lookup"><span data-stu-id="edda7-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![服務端點][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="edda7-120">服務探索和解析</span><span class="sxs-lookup"><span data-stu-id="edda7-120">Service discovery and resolution</span></span>
<span data-ttu-id="edda7-121">在分散式系統中，服務可能會隨著時間從一部電腦移動到另一部電腦。</span><span class="sxs-lookup"><span data-stu-id="edda7-121">In a distributed system, services may move from one machine to another over time.</span></span> <span data-ttu-id="edda7-122">發生這種情形的原因有很多，包括資源平衡、升級、容錯移轉或向外延展。</span><span class="sxs-lookup"><span data-stu-id="edda7-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out.</span></span> <span data-ttu-id="edda7-123">這表示服務端點位址會在服務移至具有不同 IP 位址的節點時變更，而且如果服務使用動態選取的連接埠，可能會在不同的連接埠上開啟。</span><span class="sxs-lookup"><span data-stu-id="edda7-123">This means service endpoint addresses change as the service moves to nodes with different IP addresses, and may open on different ports if the service uses a dynamically selected port.</span></span>

![服務的分佈][7]

<span data-ttu-id="edda7-125">Service Fabric 提供稱為「命名服務」的探索和解析服務。</span><span class="sxs-lookup"><span data-stu-id="edda7-125">Service Fabric provides a discovery and resolution service called the Naming Service.</span></span> <span data-ttu-id="edda7-126">「命名服務」會維護資料表，該資料表將已命名服務執行個體對應至它們接聽的端點位址。</span><span class="sxs-lookup"><span data-stu-id="edda7-126">The Naming Service maintains a table that maps named service instances to the endpoint addresses they listen on.</span></span> <span data-ttu-id="edda7-127">Service Fabric 中的所有已命名服務執行個體，皆如 URI 擁有唯一的名稱，例如， `"fabric:/MyApplication/MyService"`。</span><span class="sxs-lookup"><span data-stu-id="edda7-127">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="edda7-128">服務的名稱不會隨著服務的存留期變更，當服務移動時，只有端點位址可以變更。</span><span class="sxs-lookup"><span data-stu-id="edda7-128">The name of the service does not change over the lifetime of the service, it's only the endpoint addresses that can change when services move.</span></span> <span data-ttu-id="edda7-129">這類似於具有常數 URL 的網站，但 IP 位址可能會變更。</span><span class="sxs-lookup"><span data-stu-id="edda7-129">This is analogous to websites that have constant URLs but where the IP address may change.</span></span> <span data-ttu-id="edda7-130">並且類似於 Web 上的 DNS，可解析連接至 IP 位址的網站 URL，Service Fabric 具有註冊機構，會將服務名稱對應至其端點位址。</span><span class="sxs-lookup"><span data-stu-id="edda7-130">And similar to DNS on the web, which resolves website URLs to IP addresses, Service Fabric has a registrar that maps service names to their endpoint address.</span></span>

![服務端點][2]

<span data-ttu-id="edda7-132">解析和連接到服務牽涉到在迴圈中執行的下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="edda7-132">Resolving and connecting to services involves the following steps run in a loop:</span></span>

* <span data-ttu-id="edda7-133">**解析**︰取得端點，該端點是由服務從「命名服務」所發佈。</span><span class="sxs-lookup"><span data-stu-id="edda7-133">**Resolve**: Get the endpoint that a service has published from the Naming Service.</span></span>
* <span data-ttu-id="edda7-134">**連接**︰透過在該端點上所使用的任何通訊協定連接至服務。</span><span class="sxs-lookup"><span data-stu-id="edda7-134">**Connect**: Connect to the service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="edda7-135">**重試**︰連接嘗試可能會因為各種原因而失敗，例如，如果服務自從上次端點位址解析之後已經移動。</span><span class="sxs-lookup"><span data-stu-id="edda7-135">**Retry**: A connection attempt may fail for any number of reasons, for example if the service has moved since the last time the endpoint address was resolved.</span></span> <span data-ttu-id="edda7-136">在此情況下，則必須重試先前的解析和連接步驟，且此循環會重複執行直到連接成功為止。</span><span class="sxs-lookup"><span data-stu-id="edda7-136">In that case, the preceding resolve and connect steps need to be retried, and this cycle is repeated until the connection succeeds.</span></span>

## <a name="connecting-to-other-services"></a><span data-ttu-id="edda7-137">連接到其他服務</span><span class="sxs-lookup"><span data-stu-id="edda7-137">Connecting to other services</span></span>
<span data-ttu-id="edda7-138">叢集內彼此連接的服務通常可以直接存取其他服務的端點，因為叢集中的節點位於相同的本機網路上。</span><span class="sxs-lookup"><span data-stu-id="edda7-138">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="edda7-139">為了能夠更輕鬆在服務之間連接，Service Fabric 提供使用「命名服務」的額外服務。</span><span class="sxs-lookup"><span data-stu-id="edda7-139">To make is easier to connect between services, Service Fabric provides additional services that use the Naming Service.</span></span> <span data-ttu-id="edda7-140">DNS 服務和反向 proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="edda7-140">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="edda7-141">DNS 服務</span><span class="sxs-lookup"><span data-stu-id="edda7-141">DNS service</span></span>
<span data-ttu-id="edda7-142">由於許多服務 (特別是容器化服務) 都可以有現有的 URL 名稱，因此能夠使用標準 DNS 通訊協定 (而不是「命名服務」通訊協定) 來解析這些名稱就非常便利，特別是在應用程式的「隨即轉移」案例中。</span><span class="sxs-lookup"><span data-stu-id="edda7-142">Since many services, especially containerized services, can have an existing URL name, being able to resolve these using the standard DNS protocol (rather than the Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="edda7-143">這就是 DNS 服務的功能所在。</span><span class="sxs-lookup"><span data-stu-id="edda7-143">This is exactly what the DNS service does.</span></span> <span data-ttu-id="edda7-144">它可讓您將 DNS 服務對應到某個服務名稱，再由此解析端點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="edda7-144">It enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="edda7-145">如下圖所示，在 Service Fabric 叢集中執行的 DNS 服務會將 DNS 名稱對應到服務名稱，然後由「命名服務」解析後傳回要連接的端點位址。</span><span class="sxs-lookup"><span data-stu-id="edda7-145">As shown in the following diagram, the DNS service, running in the Service Fabric cluster, maps DNS names to service names which are then resolved by the Naming Service to return the endpoint addresses to connect to.</span></span> <span data-ttu-id="edda7-146">服務的 DNS 名稱是在建立時提供的。</span><span class="sxs-lookup"><span data-stu-id="edda7-146">The DNS name for the service is provided at the time of creation.</span></span> 

![服務端點][9]

<span data-ttu-id="edda7-148">如需有關如何使用 DNS 服務的更多詳細資料，請參閱 [Azure Service Fabric 中的 DNS 服務](service-fabric-dnsservice.md)一文。</span><span class="sxs-lookup"><span data-stu-id="edda7-148">For more details on how to use the DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="edda7-149">反向 Proxy服務</span><span class="sxs-lookup"><span data-stu-id="edda7-149">Reverse proxy service</span></span>
<span data-ttu-id="edda7-150">反向 Proxy 可處理叢集中公開 HTTP 端點 (包括 HTTPS) 的服務。</span><span class="sxs-lookup"><span data-stu-id="edda7-150">The reverse proxy addresses services in the cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="edda7-151">反向 Proxy 藉由採用特定的 URI 格式，以及處理一個服務使用「命名服務」與另一個服務進行通訊所需的解析、連接、重試步驟，將呼叫其他服務及其方法大幅簡化。</span><span class="sxs-lookup"><span data-stu-id="edda7-151">The reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles the resolve, connect, retry steps required for one service to communicate with another using the Naming Serivce.</span></span> <span data-ttu-id="edda7-152">換句話說，它會在呼叫其他服務時，透過讓此呼叫就像呼叫 URL 一樣簡單，對您隱藏「命名服務」。</span><span class="sxs-lookup"><span data-stu-id="edda7-152">In other words, it hides the Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![服務端點][10]

<span data-ttu-id="edda7-154">如需有關如何使用反向 Proxy 服務的詳細資訊，請參閱 [Azure Service Fabric 中的反向 Proxy](service-fabric-reverseproxy.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="edda7-154">For more details on how to use the reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="edda7-155">從外部用戶端連接</span><span class="sxs-lookup"><span data-stu-id="edda7-155">Connections from external clients</span></span>
<span data-ttu-id="edda7-156">叢集內彼此連接的服務通常可以直接存取其他服務的端點，因為叢集中的節點位於相同的本機網路上。</span><span class="sxs-lookup"><span data-stu-id="edda7-156">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="edda7-157">但是，在相同的環境中，叢集可能會位於負載平衡器後方，該負載平衡器會透過有限制的一組連接埠路由傳送外部輸入流量。</span><span class="sxs-lookup"><span data-stu-id="edda7-157">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="edda7-158">在這些情況下，服務仍然可以使用「命名服務」，彼此進行通訊及解析位址，但是必須採取額外的步驟，讓外部用戶端連接至服務。</span><span class="sxs-lookup"><span data-stu-id="edda7-158">In these cases, services can still communicate with each other and resolve addresses using the Naming Service, but extra steps must be taken to allow external clients to connect to services.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="edda7-159">Azure 中的 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="edda7-159">Service Fabric in Azure</span></span>
<span data-ttu-id="edda7-160">Azure 中的 Service Fabric 叢集位於 Azure 負載平衡器後方。</span><span class="sxs-lookup"><span data-stu-id="edda7-160">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="edda7-161">到叢集的所有外部流量必須經過負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="edda7-161">All external traffic to the cluster must pass through the load balancer.</span></span> <span data-ttu-id="edda7-162">負載平衡器會自動將指定連接埠上的輸入流量轉送至具有相同的開啟連接埠的隨機「節點」  。</span><span class="sxs-lookup"><span data-stu-id="edda7-162">The load balancer will automatically forward traffic inbound on a given port to a random *node* that has the same port open.</span></span> <span data-ttu-id="edda7-163">Azure Load Balancer 只會知道「節點」上開啟的連接埠，它不知道由個別「服務」開啟的連接埠。</span><span class="sxs-lookup"><span data-stu-id="edda7-163">The Azure Load Balancer only knows about ports open on the *nodes*, it does not know about ports open by individual *services*.</span></span>

![Azure 負載平衡器和 Service Fabric 拓撲][3]

<span data-ttu-id="edda7-165">例如，若要在連接埠 **80**上接受外部流量，必須設定下列項目︰</span><span class="sxs-lookup"><span data-stu-id="edda7-165">For example, in order to accept external traffic on port **80**, the following things must be configured:</span></span>

1. <span data-ttu-id="edda7-166">寫入在連接埠 80 上接聽的服務。</span><span class="sxs-lookup"><span data-stu-id="edda7-166">Write a service that listens on port 80.</span></span> <span data-ttu-id="edda7-167">在服務的 ServiceManifest.xml 中設定連接埠 80，並且在服務中開啟接聽程式，例如自我裝載的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="edda7-167">Configure port 80 in the service's ServiceManifest.xml and open a listener in the service, for example, a self-hosted web server.</span></span>

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
2. <span data-ttu-id="edda7-168">在 Azure 中建立 Service Fabric 叢集，並指定連接埠 **80** 做為將裝載服務的節點類型的自訂端點連接埠。</span><span class="sxs-lookup"><span data-stu-id="edda7-168">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for the node type that will host the service.</span></span> <span data-ttu-id="edda7-169">如果您有一個以上的節點類型，您可以在服務上設定「放置條件約束」  ，以確保它只會在具有已開啟的自訂端點連接埠的節點類型上執行。</span><span class="sxs-lookup"><span data-stu-id="edda7-169">If you have more than one node type, you can set up a *placement constraint* on the service to ensure it only runs on the node type that has the custom endpoint port opened.</span></span>

    ![開啟節點類型上的連接埠][4]
3. <span data-ttu-id="edda7-171">一旦建立叢集，在叢集的資源群組中設定 Azure 負載平衡器，以轉送連接埠 80 上的流量。</span><span class="sxs-lookup"><span data-stu-id="edda7-171">Once the cluster has been created, configure the Azure Load Balancer in the cluster's Resource Group to forward traffic on port 80.</span></span> <span data-ttu-id="edda7-172">透過 Azure 入口網站建立叢集時，會針對每個已設定的自訂端點連接埠設定這個項目。</span><span class="sxs-lookup"><span data-stu-id="edda7-172">When creating a cluster through the Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![轉送 Azure 負載平衡器的流量][5]
4. <span data-ttu-id="edda7-174">Azure 負載平衡器使用探查，來決定是否要將流量傳送到特定節點。</span><span class="sxs-lookup"><span data-stu-id="edda7-174">The Azure Load Balancer uses a probe to determine whether or not to send traffic to a particular node.</span></span> <span data-ttu-id="edda7-175">探查會定期檢查每個節點上的端點，以判斷節點是否有回應。</span><span class="sxs-lookup"><span data-stu-id="edda7-175">The probe periodically checks an endpoint on each node to determine whether or not the node is responding.</span></span> <span data-ttu-id="edda7-176">如果探查在設定的次數之後無法接收到回應，負載平衡器會停止將流量傳送到該節點。</span><span class="sxs-lookup"><span data-stu-id="edda7-176">If the probe fails to receive a response after a configured number of times, the load balancer stops sending traffic to that node.</span></span> <span data-ttu-id="edda7-177">透過 Azure 入口網站建立叢集時，會針對每個已設定的自訂端點連接埠自動設定探查。</span><span class="sxs-lookup"><span data-stu-id="edda7-177">When creating a cluster through the Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![轉送 Azure 負載平衡器的流量][8]

<span data-ttu-id="edda7-179">請務必記住，Azure Load Balancer 和探查只知道「節點」，不知道在節點上執行的「服務」。</span><span class="sxs-lookup"><span data-stu-id="edda7-179">It's important to remember that the Azure Load Balancer and the probe only know about the *nodes*, not the *services* running on the nodes.</span></span> <span data-ttu-id="edda7-180">Azure 負載平衡器一律會將流量傳送到回應探查的節點，因此必須小心以確保可以在能夠回應探查的節點上使用服務。</span><span class="sxs-lookup"><span data-stu-id="edda7-180">The Azure Load Balancer will always send traffic to nodes that respond to the probe, so care must be taken to ensure services are available on the nodes that are able to respond to the probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="edda7-181">Reliable Services：內建的通訊 API 選項</span><span class="sxs-lookup"><span data-stu-id="edda7-181">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="edda7-182">Reliable Services 架構隨附數個預先建置的通訊選項。</span><span class="sxs-lookup"><span data-stu-id="edda7-182">The Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="edda7-183">最適合您選項的決定取決於如何選擇程式設計模型、通訊架構以及用來撰寫您服務的程式語言。</span><span class="sxs-lookup"><span data-stu-id="edda7-183">The decision about which one will work best for you depends on the choice of the programming model, the communication framework, and the programming language that your services are written in.</span></span>

* <span data-ttu-id="edda7-184">**沒有特定通訊協定**：如果您沒有特定的通訊架構選擇，但您想要快速啟動並執行，則適合您的理想選項為[遠端服務](service-fabric-reliable-services-communication-remoting.md)，允許 Reliable Services 和 Reliable Actors 的強型別遠端程序呼叫。</span><span class="sxs-lookup"><span data-stu-id="edda7-184">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want to get something up and running quickly, then the ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="edda7-185">若要開始使用服務通訊，這是最簡單且快速的方式。</span><span class="sxs-lookup"><span data-stu-id="edda7-185">This is the easiest and fastest way to get started with service communication.</span></span> <span data-ttu-id="edda7-186">遠端服務會處理服務位址、連接、重試和錯誤處理的解析。</span><span class="sxs-lookup"><span data-stu-id="edda7-186">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="edda7-187">這同時適用 C# 和 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="edda7-187">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="edda7-188">**HTTP**︰對於無從驗證語言的通訊，HTTP 提供業界標準的選擇，具有工具與許多不同語言的 HTTP 伺服器，都受到 Service Fabric 的支援。</span><span class="sxs-lookup"><span data-stu-id="edda7-188">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="edda7-189">服務可以使用任何可用的 HTTP 堆疊，包括 C# 應用程式適用的 [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md)。</span><span class="sxs-lookup"><span data-stu-id="edda7-189">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="edda7-190">以 C# 撰寫的用戶端可以利用 `ICommunicationClient` 和 `ServicePartitionClient` 類別，而使用 Java 的用戶端則可以利用 `CommunicationClient` 和 `FabricServicePartitionClient` 進行[服務解析、HTTP 連線和重試迴圈](service-fabric-reliable-services-communication.md)。</span><span class="sxs-lookup"><span data-stu-id="edda7-190">Clients written in C# can leverage the `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use the `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="edda7-191">**WCF**：若您有現有的程式碼且使用 WCF 作為通訊架構，則您可以針對伺服器端使用 `WcfCommunicationListener` 類別，並針對用戶端使用 `WcfCommunicationClient` 和 `ServicePartitionClient` 類別。</span><span class="sxs-lookup"><span data-stu-id="edda7-191">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use the `WcfCommunicationListener` for the server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for the client.</span></span> <span data-ttu-id="edda7-192">不過，這只適用以 Windows 為基礎的叢集上的 C# 應用程式。</span><span class="sxs-lookup"><span data-stu-id="edda7-192">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="edda7-193">如需詳細資訊，請參閱本文中 [通訊堆疊的 WCF 式實作](service-fabric-reliable-services-communication-wcf.md)。</span><span class="sxs-lookup"><span data-stu-id="edda7-193">For more details, see this article about [WCF-based implementation of the communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="edda7-194">使用自訂通訊協定以及其他通訊架構</span><span class="sxs-lookup"><span data-stu-id="edda7-194">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="edda7-195">服務可以使用任何通訊協定或架構進行通訊，無論是透過 TCP 通訊端的自訂二進位通訊協定，或透過 [Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)或 [Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)的串流事件。</span><span class="sxs-lookup"><span data-stu-id="edda7-195">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="edda7-196">Service Fabric 提供通訊 API，您可以將通訊堆疊插入其中，同時讓您免於探索和連接的所有工作。</span><span class="sxs-lookup"><span data-stu-id="edda7-196">Service Fabric provides communication APIs that you can plug your communication stack into, while all the work to discover and connect is abstracted from you.</span></span> <span data-ttu-id="edda7-197">如需詳細資訊，請參閱本文中 [Reliable Service 通訊模型](service-fabric-reliable-services-communication.md) 。</span><span class="sxs-lookup"><span data-stu-id="edda7-197">See this article about the [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edda7-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="edda7-198">Next steps</span></span>
<span data-ttu-id="edda7-199">您可以在 [Reliable Services 通訊模型](service-fabric-reliable-services-communication.md)中深入了解概念和可用的 API，然後快速地開始使用[遠端服務](service-fabric-reliable-services-communication-remoting.md)或深入了解如何使用 [Web API 與 OWIN 自我裝載](service-fabric-reliable-services-communication-webapi.md)撰寫通訊接聽程式。</span><span class="sxs-lookup"><span data-stu-id="edda7-199">Learn more about the concepts and APIs available in the [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth to learn how to write a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
