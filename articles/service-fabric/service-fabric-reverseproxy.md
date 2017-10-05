---
title: "Azure Service Fabric 反向 Proxy | Microsoft Docs"
description: "使用 Service Fabric 反向 Proxy 從叢集內部和外部與微服務進行通訊。"
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 7897458e9e4a0bbe185bd3f7b4c133c1b26769f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="8329a-103">Azure Service Fabric 中的反向 Proxy</span><span class="sxs-lookup"><span data-stu-id="8329a-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="8329a-104">Azure Service Fabric 內建的反向 Proxy 可解析 Service Fabric 叢集中公開 HTTP 端點的微服務。</span><span class="sxs-lookup"><span data-stu-id="8329a-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="8329a-105">微服務通訊模型</span><span class="sxs-lookup"><span data-stu-id="8329a-105">Microservices communication model</span></span>
<span data-ttu-id="8329a-106">Service Fabric 中的微服務通常在叢集中的虛擬機器子集上執行，而且會因為各種原因在不同的虛擬機器之間移動。</span><span class="sxs-lookup"><span data-stu-id="8329a-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span></span> <span data-ttu-id="8329a-107">因此，微服務的端點可以動態變更。</span><span class="sxs-lookup"><span data-stu-id="8329a-107">So, the endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="8329a-108">與微服務通訊的一般模式是如下的解析迴圈：</span><span class="sxs-lookup"><span data-stu-id="8329a-108">The typical pattern to communicate to the microservice is the following resolve loop:</span></span>

1. <span data-ttu-id="8329a-109">起初透過命名服務解析服務位置。</span><span class="sxs-lookup"><span data-stu-id="8329a-109">Resolve the service location initially through the naming service.</span></span>
2. <span data-ttu-id="8329a-110">連線至服務。</span><span class="sxs-lookup"><span data-stu-id="8329a-110">Connect to the service.</span></span>
3. <span data-ttu-id="8329a-111">判斷連線失敗的原因，必要時再重新解析服務位置。</span><span class="sxs-lookup"><span data-stu-id="8329a-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span></span>

<span data-ttu-id="8329a-112">此程序通常涉及將用戶端通訊程式庫包裝在重試迴圈，以實作服務解析再重試原則。</span><span class="sxs-lookup"><span data-stu-id="8329a-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span></span>
<span data-ttu-id="8329a-113">如需詳細資訊，請參閱[連線至服務並與其進行通訊](service-fabric-connect-and-communicate-with-services.md)。</span><span class="sxs-lookup"><span data-stu-id="8329a-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-the-reverse-proxy"></a><span data-ttu-id="8329a-114">使用反向 Proxy 進行通訊</span><span class="sxs-lookup"><span data-stu-id="8329a-114">Communicating by using the reverse proxy</span></span>
<span data-ttu-id="8329a-115">Service Fabric 中的反向 Proxy 會在叢集的所有節點上執行。</span><span class="sxs-lookup"><span data-stu-id="8329a-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span></span> <span data-ttu-id="8329a-116">它代表用戶端執行整個服務的解析程序，接著再轉送用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="8329a-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span></span> <span data-ttu-id="8329a-117">因此，在叢集上執行的用戶端可使用任一用戶端 HTTP 通訊程式庫，透過在同一節點本機上執行的反向 Proxy 與目標服務通訊。</span><span class="sxs-lookup"><span data-stu-id="8329a-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span></span>

![內部通訊][1]

## <a name="reaching-microservices-from-outside-the-cluster"></a><span data-ttu-id="8329a-119">從叢集外部連線到微服務</span><span class="sxs-lookup"><span data-stu-id="8329a-119">Reaching microservices from outside the cluster</span></span>
<span data-ttu-id="8329a-120">微服務的預設外部通訊模型是選擇加入模型，每項服務都無法從外部用戶端直接存取。</span><span class="sxs-lookup"><span data-stu-id="8329a-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="8329a-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md) 是微服務與外部用戶端之間的網路界限，負責執行網路位址轉譯，並將外部要求轉送給內部的 IP:port 端點。</span><span class="sxs-lookup"><span data-stu-id="8329a-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span></span> <span data-ttu-id="8329a-122">若要讓微服務的端點能直接從外部用戶端來存取，您必須先將 Load Balancer 設為轉送流量到服務在叢集中使用的每個連接埠。</span><span class="sxs-lookup"><span data-stu-id="8329a-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span></span> <span data-ttu-id="8329a-123">此外，大部分的微服務 (特別是可設定狀態的微服務) 不存在於叢集的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="8329a-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span></span> <span data-ttu-id="8329a-124">微服務可以在容錯移轉時於節點之間移動。</span><span class="sxs-lookup"><span data-stu-id="8329a-124">The microservices can move between nodes on failover.</span></span> <span data-ttu-id="8329a-125">在這種情況下，Load Balancer 無法有效地判斷它應該將流量轉送到之複本的目標節點位置。</span><span class="sxs-lookup"><span data-stu-id="8329a-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span></span>

### <a name="reaching-microservices-via-the-reverse-proxy-from-outside-the-cluster"></a><span data-ttu-id="8329a-126">從叢集外部透過反向 Proxy 連線到微服務</span><span class="sxs-lookup"><span data-stu-id="8329a-126">Reaching microservices via the reverse proxy from outside the cluster</span></span>
<span data-ttu-id="8329a-127">您可以在 Load Balancer 中直接設定反向 Proxy 的連接埠，而不需要在 Load Balancer 中設定個別服務的連接埠。</span><span class="sxs-lookup"><span data-stu-id="8329a-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span></span> <span data-ttu-id="8329a-128">此組態可讓叢集外部的用戶端透過反向 Proxy 連線到叢集內部的服務，而不需要額外設定。</span><span class="sxs-lookup"><span data-stu-id="8329a-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span></span>

![外部通訊][0]

> [!WARNING]
> <span data-ttu-id="8329a-130">當您在 Load Balancer 中設定反向 Proxy 的連接埠時，叢集中公開 HTTP 端點的所有微服務就能從叢集外部尋址。</span><span class="sxs-lookup"><span data-stu-id="8329a-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-the-reverse-proxy"></a><span data-ttu-id="8329a-131">透過反向 Proxy 定址服務的 URI 格式</span><span class="sxs-lookup"><span data-stu-id="8329a-131">URI format for addressing services by using the reverse proxy</span></span>
<span data-ttu-id="8329a-132">反向 Proxy 使用特定的統一資源識別項 (URI) 格式來識別連入要求應該轉送到哪個服務資料分割︰</span><span class="sxs-lookup"><span data-stu-id="8329a-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="8329a-133">**http(s)：** 反向 Proxy 可設定為接受 HTTP 或 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="8329a-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="8329a-134">對於 HTTPS 轉送，在您設定反向 Proxy 於 HTTPS 接聽後，請參閱[使用反向 Proxy 連線安全的服務](service-fabric-reverseproxy-configure-secure-communication.md)。</span><span class="sxs-lookup"><span data-stu-id="8329a-134">For HTTPS forwarding, refer to [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup to listen on HTTPS.</span></span>
* <span data-ttu-id="8329a-135">**叢集完整網域名稱 (FQDN) | 內部 IP：**如果是外部用戶端，您可以設定反向 Proxy 讓其可透過叢集網域 (例如 mycluster.eastus.cloudapp.azure.com) 來聯繫到。根據預設，反向 Proxy 會在每個節點上執行。</span><span class="sxs-lookup"><span data-stu-id="8329a-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, the reverse proxy runs on every node.</span></span> <span data-ttu-id="8329a-136">如果是內部流量，反向 Proxy 可在 localhost 或任何內部節點 IP (例如 10.0.0.1) 上聯繫到。</span><span class="sxs-lookup"><span data-stu-id="8329a-136">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="8329a-137">**連接埠︰**這是為反向 Proxy 指定的連接埠，例如 19081。</span><span class="sxs-lookup"><span data-stu-id="8329a-137">**Port:** This is the port, such as 19081, that has been specified for the reverse proxy.</span></span>
* <span data-ttu-id="8329a-138">**ServiceInstanceName：**這是您嘗試不使用「fabric:/」配置來連線到之已部署服務執行個體的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="8329a-138">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span></span> <span data-ttu-id="8329a-139">例如，若要連線到 fabric:/myapp/myservice/ 服務，可以使用 myapp/myservice。</span><span class="sxs-lookup"><span data-stu-id="8329a-139">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="8329a-140">服務執行個體名稱區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8329a-140">The service instance name is case-sensitive.</span></span> <span data-ttu-id="8329a-141">對於 URL 中的服務執行個體名稱使用不同的大小寫，會導致要求失敗，並顯示「404 (找不到)」。</span><span class="sxs-lookup"><span data-stu-id="8329a-141">Using a different casing for the service instance name in the URL causes the requests to fail with 404 (Not Found).</span></span>
* <span data-ttu-id="8329a-142">**尾碼路徑︰**這是要連線到之服務的實際 URL 路徑，例如 myapi/values/add/3。</span><span class="sxs-lookup"><span data-stu-id="8329a-142">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span></span>
* <span data-ttu-id="8329a-143">**PartitionKey：**若為資料分割服務，這是您想要連線的資料分割計算資料分割金鑰。</span><span class="sxs-lookup"><span data-stu-id="8329a-143">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span></span> <span data-ttu-id="8329a-144">請注意，這不是  資料分割識別碼 GUID。</span><span class="sxs-lookup"><span data-stu-id="8329a-144">Note that this is *not* the partition ID GUID.</span></span> <span data-ttu-id="8329a-145">使用單一資料分割配置的服務不需要這個參數。</span><span class="sxs-lookup"><span data-stu-id="8329a-145">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="8329a-146">**PartitionKind：**這是服務資料分割配置。</span><span class="sxs-lookup"><span data-stu-id="8329a-146">**PartitionKind:** This is the service partition scheme.</span></span> <span data-ttu-id="8329a-147">這可以是 'Int64Range' 或 'Named'。</span><span class="sxs-lookup"><span data-stu-id="8329a-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="8329a-148">使用單一資料分割配置的服務不需要這個參數。</span><span class="sxs-lookup"><span data-stu-id="8329a-148">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="8329a-149">**ListenerName** 服務傳回的端點格式為 {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}。</span><span class="sxs-lookup"><span data-stu-id="8329a-149">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="8329a-150">當服務公開多個端點時，這可識別用戶端要求應該轉送至哪個端點。</span><span class="sxs-lookup"><span data-stu-id="8329a-150">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span></span> <span data-ttu-id="8329a-151">如果服務只有一個接聽程式，這可省略。</span><span class="sxs-lookup"><span data-stu-id="8329a-151">This can be omitted if the service has only one listener.</span></span>
* <span data-ttu-id="8329a-152">**TargetReplicaSelector** 這指定應該如何選取目標複本或執行個體。</span><span class="sxs-lookup"><span data-stu-id="8329a-152">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span></span>
  * <span data-ttu-id="8329a-153">當目標服務具狀態時，TargetReplicaSelector 可以是下列其中一個：'PrimaryReplica'、'RandomSecondaryReplica' 或 'RandomReplica'。</span><span class="sxs-lookup"><span data-stu-id="8329a-153">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="8329a-154">未指定此參數時，預設值是 'PrimaryReplica'。</span><span class="sxs-lookup"><span data-stu-id="8329a-154">When this parameter is not specified, the default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="8329a-155">當目標服務無狀態時，反向 Proxy 會挑選服務資料分割的隨機執行個體，將要求轉送至此執行個體。</span><span class="sxs-lookup"><span data-stu-id="8329a-155">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span></span>
* <span data-ttu-id="8329a-156">**逾時︰**指定由反向 Proxy 建立的 HTTP 要求代替用戶端要求傳送到服務的逾時。</span><span class="sxs-lookup"><span data-stu-id="8329a-156">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span></span> <span data-ttu-id="8329a-157">預設值為 60 秒。</span><span class="sxs-lookup"><span data-stu-id="8329a-157">The default value is 60 seconds.</span></span> <span data-ttu-id="8329a-158">這是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="8329a-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="8329a-159">使用方式範例</span><span class="sxs-lookup"><span data-stu-id="8329a-159">Example usage</span></span>
<span data-ttu-id="8329a-160">例如，讓我們採用在下列 URL 上開啟 HTTP 接聽程式的 fabric:/MyApp/MyService 服務：</span><span class="sxs-lookup"><span data-stu-id="8329a-160">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="8329a-161">以下是服務的資源︰</span><span class="sxs-lookup"><span data-stu-id="8329a-161">Following are the resources for the service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="8329a-162">如果服務使用單一資料分割配置，則不需要 PartitionKey 和 PartitionKind 查詢字串參數，可透過閘道以下列方式連線到服務︰</span><span class="sxs-lookup"><span data-stu-id="8329a-162">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span></span>

* <span data-ttu-id="8329a-163">外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="8329a-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="8329a-164">內部： `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="8329a-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="8329a-165">如果服務使用統一 Int64 資料分割配置，則必須使用 PartitionKey 和 PartitionKind 查詢字串參數來連線到服務的資料分割︰</span><span class="sxs-lookup"><span data-stu-id="8329a-165">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span></span>

* <span data-ttu-id="8329a-166">外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="8329a-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="8329a-167">內部： `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="8329a-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="8329a-168">若要連線到服務公開的資源，只要將資源路徑放在 URL 的服務名稱之後︰</span><span class="sxs-lookup"><span data-stu-id="8329a-168">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span></span>

* <span data-ttu-id="8329a-169">外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="8329a-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="8329a-170">內部： `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="8329a-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="8329a-171">閘道會將這些要求轉送到服務的 URL：</span><span class="sxs-lookup"><span data-stu-id="8329a-171">The gateway will then forward these requests to the service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="8329a-172">連接埠共用服務特殊處理</span><span class="sxs-lookup"><span data-stu-id="8329a-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="8329a-173">Azure 應用程式閘道會嘗試重新解析服務位址，並在無法連線到服務時重試要求。</span><span class="sxs-lookup"><span data-stu-id="8329a-173">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span></span> <span data-ttu-id="8329a-174">這是應用程式閘道的主要好處，因為用戶端程式碼不需要實作自己的服務解決方案和解析迴圈。</span><span class="sxs-lookup"><span data-stu-id="8329a-174">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="8329a-175">通常，當服務無法連線時，即表示服務執行個體或複本已移至另一個節點，這是其一般生命週期的過程。</span><span class="sxs-lookup"><span data-stu-id="8329a-175">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span></span> <span data-ttu-id="8329a-176">發生這種情況時，應用程式閘道可能會收到指出端點已不在原先解析的位址上開啟的網路連線錯誤。</span><span class="sxs-lookup"><span data-stu-id="8329a-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span></span>

<span data-ttu-id="8329a-177">不過，複本或服務執行個體可以共用主機處理序，在由以 http.sys 為基礎的 Web 伺服器託管時也可以共用連接埠，這些 Web 伺服器包括︰</span><span class="sxs-lookup"><span data-stu-id="8329a-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="8329a-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="8329a-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="8329a-179">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="8329a-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="8329a-180">Katana</span><span class="sxs-lookup"><span data-stu-id="8329a-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="8329a-181">在此情況下，可能是 Web 伺服器可用於主機處理序和回應要求，但已解析的服務執行個體或複本已無法再於主機上提供。</span><span class="sxs-lookup"><span data-stu-id="8329a-181">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span></span> <span data-ttu-id="8329a-182">在此情況下，閘道將從 Web 伺服器收到 HTTP 404 回應。</span><span class="sxs-lookup"><span data-stu-id="8329a-182">In this case, the gateway will receive an HTTP 404 response from the web server.</span></span> <span data-ttu-id="8329a-183">因此，HTTP 404 有兩個不同意義︰</span><span class="sxs-lookup"><span data-stu-id="8329a-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="8329a-184">案例 1︰服務位址正確，但使用者所要求的資源不存在。</span><span class="sxs-lookup"><span data-stu-id="8329a-184">Case #1: The service address is correct, but the resource that the user requested does not exist.</span></span>
- <span data-ttu-id="8329a-185">案例 2︰服務位址不正確，而且使用者所要求的資源可能存在於不同節點上。</span><span class="sxs-lookup"><span data-stu-id="8329a-185">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span></span>

<span data-ttu-id="8329a-186">第一個案例是一般的 HTTP 404，會被視為使用者錯誤。</span><span class="sxs-lookup"><span data-stu-id="8329a-186">The first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="8329a-187">不過，在第二個案例中，使用者要求了存在的資源。</span><span class="sxs-lookup"><span data-stu-id="8329a-187">However, in the second case, the user has requested a resource that does exist.</span></span> <span data-ttu-id="8329a-188">應用程式閘道之所以找不到它，是因為服務本身已移動。</span><span class="sxs-lookup"><span data-stu-id="8329a-188">Application Gateway was unable to locate it because the service itself has moved.</span></span> <span data-ttu-id="8329a-189">應用程式閘道必須重新解析位址，然後重試要求。</span><span class="sxs-lookup"><span data-stu-id="8329a-189">Application Gateway needs to resolve the address again and retry the request.</span></span>

<span data-ttu-id="8329a-190">應用程式閘道因此需要能夠區分這兩種案例的方法。</span><span class="sxs-lookup"><span data-stu-id="8329a-190">Application Gateway thus needs a way to distinguish between these two cases.</span></span> <span data-ttu-id="8329a-191">為了區分，您需要來自伺服器的提示。</span><span class="sxs-lookup"><span data-stu-id="8329a-191">To make that distinction, a hint from the server is required.</span></span>

* <span data-ttu-id="8329a-192">根據預設，應用程式閘道會採用案例 2，並嘗試重新解析並發出要求。</span><span class="sxs-lookup"><span data-stu-id="8329a-192">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span></span>
* <span data-ttu-id="8329a-193">若要向應用程式閘道表明是案例 1，服務應傳回下列 HTTP 回應標頭︰</span><span class="sxs-lookup"><span data-stu-id="8329a-193">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="8329a-194">此 HTTP 回應標頭表示指出一般的 HTTP 404 情況，即要求的資源不存在，應用程式閘道將不會嘗試重新解析服務位址。</span><span class="sxs-lookup"><span data-stu-id="8329a-194">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="8329a-195">設定和組態</span><span class="sxs-lookup"><span data-stu-id="8329a-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="8329a-196">透過 Azure 入口網站啟用反向 Proxy</span><span class="sxs-lookup"><span data-stu-id="8329a-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="8329a-197">Azure 入口網站提供選項，以在建立新的 Service Fabric 叢集時啟用反向 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8329a-197">Azure portal provides an option to enable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="8329a-198">在**建立 Service Fabric 叢集**下，步驟 2：叢集設定、節點類型設定，選取核取方塊以「啟用反向 Proxy」。</span><span class="sxs-lookup"><span data-stu-id="8329a-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select the checkbox to "Enable reverse proxy".</span></span>
<span data-ttu-id="8329a-199">針對設定安全的反向 Proxy，可以在步驟 3 指定 SSL 憑證：安全性、設定叢集安全性設定，選取核取方塊以「包含反向 Proxy 的 SSL 憑證」，然後輸入憑證詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8329a-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select the checkbox to "Include a SSL certificate for reverse proxy" and enter the certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="8329a-200">透過 Azure Resource Manager 範本啟用反向 Proxy</span><span class="sxs-lookup"><span data-stu-id="8329a-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="8329a-201">您可以使用 [Azure Resource Manager 範本](service-fabric-cluster-creation-via-arm.md)為叢集啟用 Service Fabric 中的反向 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8329a-201">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span></span>

<span data-ttu-id="8329a-202">請參閱[在安全的叢集中設定 HTTPS 反向 Proxy](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster)，以取得使用憑證設定安全反向 Proxy 和處理憑證變換的 Azure Resource Manager 範本範例。</span><span class="sxs-lookup"><span data-stu-id="8329a-202">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="8329a-203">首先，您要取得想要部署之叢集的範本。</span><span class="sxs-lookup"><span data-stu-id="8329a-203">First, you get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="8329a-204">您可以使用範例範本或建立自訂的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="8329a-204">You can either use the sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="8329a-205">然後，您可以使用下列步驟來啟用反向 Proxy︰</span><span class="sxs-lookup"><span data-stu-id="8329a-205">Then, you can enable the reverse proxy by using the following steps:</span></span>

1. <span data-ttu-id="8329a-206">在範本的 [參數區段](../azure-resource-manager/resource-group-authoring-templates.md) 定義反向 Proxy 的連接埠。</span><span class="sxs-lookup"><span data-stu-id="8329a-206">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="8329a-207">在**叢集**的[資源類型區段](../azure-resource-manager/resource-group-authoring-templates.md)中為每個節點類型物件指定連接埠。</span><span class="sxs-lookup"><span data-stu-id="8329a-207">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="8329a-208">連接埠是以參數名稱 reverseProxyEndpointPort 識別。</span><span class="sxs-lookup"><span data-stu-id="8329a-208">The port is identified by the parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="8329a-209">若要從 Azure 叢集外部定址反向 Proxy，請為您在步驟 1 指定的連接埠設定 Azure Load Balancer 規則。</span><span class="sxs-lookup"><span data-stu-id="8329a-209">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="8329a-210">若要在連接埠上設定反向 Proxy 的 SSL 憑證，請將憑證新增至**叢集**的[資源類型區段](../resource-group-authoring-templates.md)中的 ***reverseProxyCertificate*** 屬性。</span><span class="sxs-lookup"><span data-stu-id="8329a-210">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-the-cluster-certificate"></a><span data-ttu-id="8329a-211">支援不同於叢集憑證的反向 Proxy 憑證</span><span class="sxs-lookup"><span data-stu-id="8329a-211">Supporting a reverse proxy certificate that's different from the cluster certificate</span></span>
 <span data-ttu-id="8329a-212">如果反向 Proxy 憑證不同於保護叢集的憑證，則先前指定的憑證應該安裝在虛擬機器上，並新增至存取控制清單 (ACL)，讓 Service Fabric 可以存取它。</span><span class="sxs-lookup"><span data-stu-id="8329a-212">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="8329a-213">這可以在 **virtualMachineScaleSets** 的[資源類型區段](../resource-group-authoring-templates.md)來完成。</span><span class="sxs-lookup"><span data-stu-id="8329a-213">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="8329a-214">若要進行安裝，請將該憑證新增至 osProfile。</span><span class="sxs-lookup"><span data-stu-id="8329a-214">For installation, add that certificate to the osProfile.</span></span> <span data-ttu-id="8329a-215">範本的延伸模組可以更新 ACL 中的憑證。</span><span class="sxs-lookup"><span data-stu-id="8329a-215">The extension section of the template can update the certificate in the ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="8329a-216">當您使用不同於叢集憑證的憑證在現有叢集上啟用反向 Proxy 時，請先在叢集上安裝反向 Proxy 憑證並更新 ACL，再啟用反向 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8329a-216">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span></span> <span data-ttu-id="8329a-217">先使用先前所述設定完成 [Azure Resource Manager 範本](service-fabric-cluster-creation-via-arm.md)部署，再開始於步驟 1-4 中啟用反向 Proxy 的部署。</span><span class="sxs-lookup"><span data-stu-id="8329a-217">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8329a-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8329a-218">Next steps</span></span>
* <span data-ttu-id="8329a-219">請參閱 [GitHub 上的範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)中服務之間的 HTTP 通訊範例。</span><span class="sxs-lookup"><span data-stu-id="8329a-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="8329a-220">透過反向 Proxy 轉送到安全的 HTTP 服務</span><span class="sxs-lookup"><span data-stu-id="8329a-220">Forwarding to secure HTTP service with the reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="8329a-221">使用 Reliable Services 遠端服務進行遠端程序呼叫</span><span class="sxs-lookup"><span data-stu-id="8329a-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="8329a-222">在 Reliable Services 中使用 OWIN 的 Web API</span><span class="sxs-lookup"><span data-stu-id="8329a-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="8329a-223">使用 Reliable Services 的 WCF 通訊</span><span class="sxs-lookup"><span data-stu-id="8329a-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="8329a-224">如需其他反向 Proxy 組態選項，請參閱[自訂 Service Fabric 叢集設定](service-fabric-cluster-fabric-settings.md)中的ApplicationGateway/Http 一節。</span><span class="sxs-lookup"><span data-stu-id="8329a-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
