---
title: "設定負載平衡器分配模式 | Microsoft Docs"
description: "如何設定 Azure 負載平衡器分配模式以支援來源 IP 同質性"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="9f0a7-103">設定負載平衡器的分配模式</span><span class="sxs-lookup"><span data-stu-id="9f0a7-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="9f0a7-104">雜湊型分配模式</span><span class="sxs-lookup"><span data-stu-id="9f0a7-104">Hash-based distribution mode</span></span>

<span data-ttu-id="9f0a7-105">預設的分配演算法是 5-tuple (來源 IP、來源連接埠、目的地 IP、目的地連接埠、通訊協定類型) 的雜湊，將流量對應至可用的伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="9f0a7-106">它只在傳輸工作階段內提供綁定。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="9f0a7-107">相同工作階段中的封包會被導向至負載平衡端點後面的相同資料中心 IP (DIP) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="9f0a7-108">當用戶端從相同的來源 IP 啟動新的工作階段時，來源連接埠便會變更，進而導致流量進入不同的 DIP 端點。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![雜湊型負載平衡器](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="9f0a7-110">圖 1 - 5-tuple 分配</span><span class="sxs-lookup"><span data-stu-id="9f0a7-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="9f0a7-111">來源 IP 同質性模式</span><span class="sxs-lookup"><span data-stu-id="9f0a7-111">Source IP affinity mode</span></span>

<span data-ttu-id="9f0a7-112">我們有另一個名為「來源 IP 同質性」(也稱為工作階段同質性或用戶端 IP 同質性) 的分配模式。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="9f0a7-113">您可以設定 Azure Load Balancer 使用 2-tuple (來源 IP、目的地 IP) 或 3 個 Tuple (來源 IP、目的地 IP 通訊協定)，來將流量對應至可用伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="9f0a7-114">使用來源 IP 同質性之後，從相同用戶端電腦啟動的連線會進入相同的 DIP 端點。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="9f0a7-115">下圖說明 2-tuple 的設定。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="9f0a7-116">注意到 2-tuple 會透過負載平衡器執行到虛擬機器 1 (VM1)，並由 VM2 和 VM3 備份。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![工作階段同質](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="9f0a7-118">圖 2 - 2-tuple 分配</span><span class="sxs-lookup"><span data-stu-id="9f0a7-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="9f0a7-119">來源 IP 同質性可解決 Azure Load Balancer 和遠端桌面 (RD) 閘道器之間的不相容性。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="9f0a7-120">現在，您可以在單一雲端服務中建立 RD 閘道伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="9f0a7-121">另一個使用案例是媒體上傳，媒體上傳會透過 UDP 進行資料上傳，但可透過 TCP 進入控制台：</span><span class="sxs-lookup"><span data-stu-id="9f0a7-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="9f0a7-122">用戶端首先會對負載平衡的公用位址啟動 TCP 工作階段，接著被導向至特定 DIP，此通道便會保持作用中狀態以監視連接健康狀態</span><span class="sxs-lookup"><span data-stu-id="9f0a7-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="9f0a7-123">來自相同用戶端電腦的新 UDP 工作階段會在相同的負載平衡公用端點中啟動，我們希望此連接會像先前的 TCP 連接一樣被導向至相同的 DIP 端點，以便在高輸送量時執行媒體上傳，並同時透過 TCP 維持控制通道。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="9f0a7-124">當負載平衡集變更時 (移除或新增虛擬機器)，則會重新計算用戶端要求的分配。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="9f0a7-125">您無法確定現有用戶端的新連接最後都會抵達相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="9f0a7-126">此外，使用來源 IP 同質性分配模式可能會導致流量的不相等分配。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="9f0a7-127">在 Proxy 後方執行的用戶端可能會被視為唯一用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="9f0a7-128">進行負載平衡器的來源 IP 同質性設定</span><span class="sxs-lookup"><span data-stu-id="9f0a7-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="9f0a7-129">針對虛擬機器，您可以使用 PowerShell 來變更逾時設定：</span><span class="sxs-lookup"><span data-stu-id="9f0a7-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="9f0a7-130">將 Azure 端點新增到虛擬機器，並設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="9f0a7-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="9f0a7-131">LoadBalancerDistribution 可設定為 sourceIP 以使用 2-tuple (來源 IP、目的地 IP) 負載平衡、設定為 sourceIPProtocol 以使用 3-tuple (來源 IP、目的地 IP、通訊協定) 負載平衡，或設定為 none 以使用預設的 5-tuple 負載平衡行為。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="9f0a7-132">使用下列命令以擷取端點負載平衡器分配模式組態：</span><span class="sxs-lookup"><span data-stu-id="9f0a7-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15
    LoadBalancerDistribution : sourceIP

<span data-ttu-id="9f0a7-133">如果 LoadBalancerDistribution 項目不存在，則 Azure 負載平衡器會使用預設的 5-tuple 演算法。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="9f0a7-134">在負載平衡端點集上設定分配模式</span><span class="sxs-lookup"><span data-stu-id="9f0a7-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="9f0a7-135">如果端點是負載平衡端點集的一部分，就必須在負載平衡端點集上設定分配模式：</span><span class="sxs-lookup"><span data-stu-id="9f0a7-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="9f0a7-136">可變更分配模式的雲端服務組態</span><span class="sxs-lookup"><span data-stu-id="9f0a7-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="9f0a7-137">您可以利用 Azure SDK for .NET 2.5 (將於 11 月發行) 來更新雲端服務。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="9f0a7-138">雲端服務的端點設定是設定於 .csdef 中。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="9f0a7-139">若要更新雲端服務部署的負載平衡器分配模式，部署升級是必要的。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="9f0a7-140">適用於端點設定的 .csdef 變更範例如下：</span><span class="sxs-lookup"><span data-stu-id="9f0a7-140">Here is an example of .csdef changes for endpoint settings:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
<InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
    <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
</InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="api-example"></a><span data-ttu-id="9f0a7-141">API 範例</span><span class="sxs-lookup"><span data-stu-id="9f0a7-141">API example</span></span>

<span data-ttu-id="9f0a7-142">您可以使用服務管理 API 來設定負載平衡器分配。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="9f0a7-143">請務必新增已設定為 `2014-09-01` 版或更高版本的 `x-ms-version` 標頭。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="9f0a7-144">在部署中更新指定負載平衡集的設定</span><span class="sxs-lookup"><span data-stu-id="9f0a7-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="9f0a7-145">要求範例</span><span class="sxs-lookup"><span data-stu-id="9f0a7-145">Request example</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

<span data-ttu-id="9f0a7-146">LoadBalancerDistribution 的值可以是 sourceIP (適用於 2-tuple 同質性)、sourceIPProtocol (適用於 3-tuple 同質性) 或 none (適用於沒有同質性。</span><span class="sxs-lookup"><span data-stu-id="9f0a7-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="9f0a7-147">也就是 5-tuple)</span><span class="sxs-lookup"><span data-stu-id="9f0a7-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="9f0a7-148">Response</span><span class="sxs-lookup"><span data-stu-id="9f0a7-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="9f0a7-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f0a7-149">Next Steps</span></span>

[<span data-ttu-id="9f0a7-150">內部負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="9f0a7-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="9f0a7-151">開始設定網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="9f0a7-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="9f0a7-152">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="9f0a7-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
