---
title: "Service Fabric aaaAzure 反向 proxy |Microsoft 文件"
description: "用於從內部和外部 hello 叢集通訊 toomicroservices Service Fabric 反向 proxy。"
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
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="8f6ca-103">Azure Service Fabric 中的反向 Proxy</span><span class="sxs-lookup"><span data-stu-id="8f6ca-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="8f6ca-104">內建於 Azure Service Fabric hello 反向 proxy 位址 microservices 公開 HTTP 端點的 hello Service Fabric 叢集中。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="8f6ca-105">微服務通訊模型</span><span class="sxs-lookup"><span data-stu-id="8f6ca-105">Microservices communication model</span></span>
<span data-ttu-id="8f6ca-106">Service Fabric 中的 Microservices 通常子集 hello 叢集中虛擬機器上執行，並可以從一個虛擬機器 tooanother 移動基於各種原因。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="8f6ca-107">因此，microservices hello 端點可以動態變更。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="8f6ca-108">hello 典型模式 toocommunicate toohello 微服務是 hello 下列解決迴圈：</span><span class="sxs-lookup"><span data-stu-id="8f6ca-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="8f6ca-109">解決一開始是透過 hello 命名服務的 hello 服務位置。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="8f6ca-110">連接 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-110">Connect toohello service.</span></span>
3. <span data-ttu-id="8f6ca-111">判斷連接失敗的 hello 原因和解決 hello 服務位置，必要時。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="8f6ca-112">此程序通常牽涉到包裝在實作 hello 服務解析和重試原則的重試迴圈中的用戶端通訊程式庫。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="8f6ca-113">如需詳細資訊，請參閱[連線至服務並與其進行通訊](service-fabric-connect-and-communicate-with-services.md)。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="8f6ca-114">使用 hello 反向 proxy 通訊</span><span class="sxs-lookup"><span data-stu-id="8f6ca-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="8f6ca-115">服務網狀架構中的 hello 反向 proxy 會 hello 叢集中的所有 hello 節點上執行。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="8f6ca-116">它代表用戶端上執行 hello 整個服務解析程序，接著才遞交 hello 用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="8f6ca-117">因此，在 hello 叢集執行的用戶端可以使用任何用戶端 HTTP 通訊程式庫 tootalk toohello 目標服務使用 hello 反向 proxy 上執行的本機 hello 相同的節點。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![內部通訊][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="8f6ca-119">到達 microservices 從外部 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="8f6ca-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="8f6ca-120">microservices hello 預設外部通訊模型是選擇加入的模型，其中每個服務無法存取直接來自外部用戶端。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="8f6ca-121">[Azure 負載平衡器](../load-balancer/load-balancer-overview.md)，這是 microservices 和外部的用戶端之間的網路界限執行網路位址轉譯，以及轉送外部要求 toointernal IP:port 端點。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="8f6ca-122">toomake 微服務端點直接存取 tooexternal 用戶端，您必須先設定負載平衡器 tooforward 流量 tooeach 埠 hello 服務會使用 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="8f6ca-123">此外，大部分 microservices，特別是可設定狀態 microservices 生活 hello 叢集的所有節點上。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="8f6ca-124">hello microservices 可以在容錯移轉節點之間移動。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="8f6ca-125">在這種情況下，負載平衡器無法有效地判斷 hello 位置 hello 複本 toowhich hello 目標節點它應該轉送流量。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="8f6ca-126">到達 microservices 透過從外部 hello 叢集 hello 反向 proxy</span><span class="sxs-lookup"><span data-stu-id="8f6ca-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="8f6ca-127">您不需要設定負載平衡器中的 hello 的個別服務的連接埠，您可以設定只 hello 連接埠 hello 反向 proxy 負載平衡器中。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="8f6ca-128">此設定可讓用戶端 hello 叢集外使用 hello 反向 proxy，而不需要其他設定的連接 hello 叢集內的服務。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![外部通訊][0]

> [!WARNING]
> <span data-ttu-id="8f6ca-130">當您在負載平衡器設定 hello 反向 proxy 的連接埠時，hello 叢集中的所有 microservices 公開 （expose) 的 HTTP 端點都都可以從 hello 叢集外定址。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="8f6ca-131">URI 格式，以解決服務使用 hello 反向 proxy</span><span class="sxs-lookup"><span data-stu-id="8f6ca-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="8f6ca-132">hello 反向 proxy 會使用特定的統一資源識別元 (URI) 格式 tooidentify hello 服務磁碟分割 toowhich hello 連入要求應該轉送：</span><span class="sxs-lookup"><span data-stu-id="8f6ca-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="8f6ca-133">**http （s):** hello 反向 proxy 可以設定的 tooaccept HTTP 或 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="8f6ca-134">HTTPS 轉寄，請參閱太[tooa 安全服務連接與 hello 反向 proxy](service-fabric-reverseproxy-configure-secure-communication.md)一旦反向 proxy 安裝 toolisten 程式 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="8f6ca-135">**叢集的完整的網域名稱 (FQDN) |內部 IP:**外部的用戶端，您可以設定 hello 反向 proxy，因此可以存取透過 hello 叢集網域，例如 mycluster.eastus.cloudapp.azure.com。根據預設，hello 反向 proxy 執行每個節點上。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="8f6ca-136">內部流量，hello 反向 proxy 可以連線到 localhost 或任何內部節點 IP，例如 10.0.0.1。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="8f6ca-137">**連接埠：**這是 hello 連接埠，例如 19081，已指定為 hello 反向 proxy。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="8f6ca-138">**ServiceInstanceName:**這是 hello 嘗試 tooreach hello 沒有部署的 hello 服務執行個體的完整限定名稱"fabric: /"配置。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="8f6ca-139">比方說，tooreach hello *fabric: / myapp/myservice/*服務，您會使用*myapp/myservice*。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="8f6ca-140">hello 服務執行個體名稱是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="8f6ca-141">Hello URL 中的 hello 服務執行個體名稱中使用不同的大小寫導致 hello 要求 toofail 404 （找不到）。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="8f6ca-142">**後置詞路徑：**這是 hello 實際的 URL 路徑，例如*myapi/值/新增/3*，針對您想要 tooconnect hello 服務。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="8f6ca-143">**PartitionKey:**資料分割的服務，這是 hello 資料分割的 tooreach hello 計算的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="8f6ca-144">請注意，這是*不*hello 資料分割識別碼 GUID。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="8f6ca-145">這個參數不需要使用 hello 單一資料分割配置的服務。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="8f6ca-146">**PartitionKind:**這是 hello 服務資料分割配置。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="8f6ca-147">這可以是 'Int64Range' 或 'Named'。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="8f6ca-148">這個參數不需要使用 hello 單一資料分割配置的服務。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="8f6ca-149">**ListenerName** hello hello 服務端點會 hello 表單的 {< 端點 >: {"Listener1":"Endpoint1"、"Listener2":"Endpoint2"}}。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="8f6ca-150">當 hello 服務會公開多個端點時，這會識別 hello 端點應該送給 hello 用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="8f6ca-151">這可以省略如果 hello 服務只能有一個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="8f6ca-152">**TargetReplicaSelector**這會指定應該如何選取 hello 目標複本或執行個體。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="8f6ca-153">Hello 目標服務可設定狀態時，hello TargetReplicaSelector 可以是 hello 下列其中之一: 'PrimaryReplica'、 'RandomSecondaryReplica，' 或 'RandomReplica'。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="8f6ca-154">若未指定這個參數，hello 預設值是 'PrimaryReplica'。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="8f6ca-155">Hello 目標服務無狀態時，反向 proxy 會挑選 hello 服務磁碟分割 tooforward hello 要求的隨機執行個體。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="8f6ca-156">**逾時：**這會指定 hello hello 反向 proxy toohello 服務代表 hello 用戶端要求所建立的 hello HTTP 要求的逾時。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="8f6ca-157">hello 預設值為 60 秒。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="8f6ca-158">這是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="8f6ca-159">使用方式範例</span><span class="sxs-lookup"><span data-stu-id="8f6ca-159">Example usage</span></span>
<span data-ttu-id="8f6ca-160">例如，讓我們來看 hello *fabric: / MyApp/MyService*開啟下列 URL 的 hello HTTP 接聽程式的服務：</span><span class="sxs-lookup"><span data-stu-id="8f6ca-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="8f6ca-161">以下是 hello 服務的 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="8f6ca-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="8f6ca-162">如果 hello 服務使用 hello 單一資料分割配置，hello *PartitionKey*和*PartitionKind*查詢字串參數，就不需要與 hello 服務可以達到使用 hello 閘道為：</span><span class="sxs-lookup"><span data-stu-id="8f6ca-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="8f6ca-163">外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="8f6ca-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="8f6ca-164">內部： `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="8f6ca-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="8f6ca-165">如果 hello 服務使用 hello 統一 Int64 資料分割配置，hello *PartitionKey*和*PartitionKind*查詢字串參數必須是使用的 tooreach hello 服務的資料分割：</span><span class="sxs-lookup"><span data-stu-id="8f6ca-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="8f6ca-166">外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="8f6ca-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="8f6ca-167">內部： `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="8f6ca-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="8f6ca-168">tooreach hello 資源 hello 服務所公開，只要將 hello hello URL 中的服務名稱之後的 hello 資源路徑：</span><span class="sxs-lookup"><span data-stu-id="8f6ca-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="8f6ca-169">外部： `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="8f6ca-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="8f6ca-170">內部： `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="8f6ca-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="8f6ca-171">hello 閘道會將這些要求 toohello 服務 URL:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="8f6ca-172">連接埠共用服務特殊處理</span><span class="sxs-lookup"><span data-stu-id="8f6ca-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="8f6ca-173">Azure 應用程式閘道嘗試的 tooresolve 服務一次地址，然後重試 hello 要求，無法連絡服務時。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="8f6ca-174">這是應用程式閘道的主要優點，因為用戶端程式碼不需要它自己的服務解析 tooimplement，解決迴圈。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="8f6ca-175">一般而言，當服務無法連線，hello 服務執行個體或複本已被移 tooa 不同的節點，做為其標準的生命週期的一部分。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="8f6ca-176">當發生這種情況時，可能會收到應用程式閘道，網路連線錯誤，指出端點上 hello 沒有長開啟原本解析位址。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="8f6ca-177">不過，複本或服務執行個體可以共用主機處理序，在由以 http.sys 為基礎的 Web 伺服器託管時也可以共用連接埠，這些 Web 伺服器包括︰</span><span class="sxs-lookup"><span data-stu-id="8f6ca-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="8f6ca-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="8f6ca-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="8f6ca-179">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="8f6ca-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="8f6ca-180">Katana</span><span class="sxs-lookup"><span data-stu-id="8f6ca-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="8f6ca-181">在此情況下，可能是該 hello 網頁伺服器位於 hello 主控件程序和回應 toorequests，但 hello 解決服務執行個體或複本已無法再使用 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="8f6ca-182">在此情況下，hello 閘道會收到 HTTP 404 回應 hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="8f6ca-183">因此，HTTP 404 有兩個不同意義︰</span><span class="sxs-lookup"><span data-stu-id="8f6ca-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="8f6ca-184">案例 1: hello 服務位址是正確的但 hello hello 使用者要求的資源不存在。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="8f6ca-185">案例 2: hello 服務位址不正確，並且 hello hello 使用者要求的資源可能存在的不同節點上。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="8f6ca-186">hello 第一種情況是會被視為使用者錯誤標準 HTTP 404。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="8f6ca-187">不過，在 hello 第二個情況下，hello 使用者已要求資源存在。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="8f6ca-188">應用程式閘道已無法 toolocate 它因為 hello 服務本身已移動。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="8f6ca-189">應用程式閘道需求 tooresolve hello 位址一次，再重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="8f6ca-190">應用程式閘道，因此必須介於這兩種情況的方式 toodistinguish。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="8f6ca-191">toomake 的區別，從 hello 伺服器則需要提示。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="8f6ca-192">根據預設，應用程式閘道會假設案例 #2，並再次嘗試 tooresolve 和問題 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="8f6ca-193">第 1 個 tooApplication 閘道 tooindicate，hello 服務應該會傳回下列 HTTP 回應標頭的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="8f6ca-194">此 HTTP 回應標頭表示一般 HTTP 404 情況中的 hello 要求的資源不存在，以及應用程式閘道將會再次嘗試 tooresolve hello 服務位址。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="8f6ca-195">設定和組態</span><span class="sxs-lookup"><span data-stu-id="8f6ca-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="8f6ca-196">透過 Azure 入口網站啟用反向 Proxy</span><span class="sxs-lookup"><span data-stu-id="8f6ca-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="8f6ca-197">Azure 入口網站提供選項 tooenable 反向 proxy，建立新的 Service Fabric 叢集時。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="8f6ca-198">在下**建立 Service Fabric 叢集**，步驟 2： 叢集設定中，節點型別組態，選取 hello 核取方塊太 「 啟用反向 proxy 」。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="8f6ca-199">設定安全的反向 proxy，可以指定 SSL 憑證在步驟 3： 安全性、 設定叢集安全性設定、 選取 hello 核取方塊太"Include 反向 proxy 的 SSL 憑證"，而且輸入 hello 憑證詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="8f6ca-200">透過 Azure Resource Manager 範本啟用反向 Proxy</span><span class="sxs-lookup"><span data-stu-id="8f6ca-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="8f6ca-201">您可以使用 hello [Azure Resource Manager 範本](service-fabric-cluster-creation-via-arm.md)tooenable hello 反向 proxy 服務網狀架構中的 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="8f6ca-202">請參閱太[設定 HTTPS 反向 Proxy 安全叢集中](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster)Azure 資源管理員的範本範例 tooconfigure 安全反向 proxy 的憑證和處理憑證變換。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="8f6ca-203">首先，您取得 hello 範本 hello 叢集的 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="8f6ca-204">您可以使用 hello 範例範本，或建立自訂的資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="8f6ca-205">然後，您可以使用下列步驟的 hello 啟用 hello 反向 proxy:</span><span class="sxs-lookup"><span data-stu-id="8f6ca-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="8f6ca-206">定義在 hello hello 反向 proxy 的連接埠[參數 > 一節](../azure-resource-manager/resource-group-authoring-templates.md)的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="8f6ca-207">針對每個在 hello hello nodetype 物件指定 hello 連接埠**叢集**[資源類型] 區段中](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="8f6ca-208">hello 參數名稱，reverseProxyEndpointPort 識別 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

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
3. <span data-ttu-id="8f6ca-209">tooaddress hello 反向 proxy，從外部 hello Azure 叢集上，設定您指定在步驟 1 中的 hello 通訊埠的 hello Azure 負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

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
4. <span data-ttu-id="8f6ca-210">tooconfigure hello hello 反向 proxy，連接埠上的 SSL 憑證加入 hello 憑證 toohello ***reverseProxyCertificate***屬性在 hello**叢集**[資源類型] 區段](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8f6ca-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

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

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="8f6ca-211">支援不同 hello 叢集憑證中的反向 proxy 憑證</span><span class="sxs-lookup"><span data-stu-id="8f6ca-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="8f6ca-212">如果與 hello 憑證來保護 hello 叢集不同 hello 反向 proxy 的憑證，然後 hello 先前指定應該 hello 虛擬機器上安裝憑證，並加入 toohello 存取控制清單 (ACL)，如此可以 Service Fabric存取它。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="8f6ca-213">作法是在 hello **virtualMachineScaleSets** [資源類型 區段中](../resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="8f6ca-214">進行安裝時，將該憑證 toohello osProfile。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="8f6ca-215">hello 範本的 hello 延伸區段，可以更新 hello ACL 中的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

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
> <span data-ttu-id="8f6ca-216">當您使用不同於 hello 叢集憑證 tooenable hello 反向 proxy 上現有的叢集中的憑證時，安裝 hello 反向 proxy 的憑證，並更新 hello ACL hello 叢集上的，才能啟用 hello 反向 proxy。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="8f6ca-217">完整的 hello [Azure Resource Manager 範本](service-fabric-cluster-creation-via-arm.md)部署使用所述的 hello 設定先前在開始部署 tooenable hello 反向 proxy 之前在步驟 1-4。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f6ca-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f6ca-218">Next steps</span></span>
* <span data-ttu-id="8f6ca-219">請參閱 [GitHub 上的範例專案](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)中服務之間的 HTTP 通訊範例。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="8f6ca-220">與 hello 反向 proxy 轉送 toosecure HTTP 服務</span><span class="sxs-lookup"><span data-stu-id="8f6ca-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="8f6ca-221">使用 Reliable Services 遠端服務進行遠端程序呼叫</span><span class="sxs-lookup"><span data-stu-id="8f6ca-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="8f6ca-222">在 Reliable Services 中使用 OWIN 的 Web API</span><span class="sxs-lookup"><span data-stu-id="8f6ca-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="8f6ca-223">使用 Reliable Services 的 WCF 通訊</span><span class="sxs-lookup"><span data-stu-id="8f6ca-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="8f6ca-224">如需其他反向 Proxy 組態選項，請參閱[自訂 Service Fabric 叢集設定](service-fabric-cluster-fabric-settings.md)中的ApplicationGateway/Http 一節。</span><span class="sxs-lookup"><span data-stu-id="8f6ca-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
