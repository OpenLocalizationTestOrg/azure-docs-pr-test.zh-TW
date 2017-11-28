---
title: "設定負載平衡器 TCP 閒置逾時 | Microsoft Docs"
description: "設定負載平衡器 TCP 閒置逾時"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="4f9a0-103">設定 Azure Load Balancer 的 TCP 閒置逾時設定</span><span class="sxs-lookup"><span data-stu-id="4f9a0-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="4f9a0-104">在預設組態中，Azure Load Balancer 的閒置逾時設定是 4 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="4f9a0-105">如果閒置期間超過逾時值，即無法保證仍能維持用戶端與雲端服務之間的 TCP 或 HTTP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="4f9a0-106">當連線關閉時，用戶端應用程式可能會收到以下錯誤訊息：「基礎連線已關閉：應該保持運作的連接卻被伺服器關閉。」</span><span class="sxs-lookup"><span data-stu-id="4f9a0-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="4f9a0-107">常見作法是使用 TCP Keep-Alive。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="4f9a0-108">此作法可讓連線保持長時間連線。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="4f9a0-109">如需詳細資訊，請參閱這些 [.NET 文章](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="4f9a0-110">啟用 Keep-Alive 之後，就會在連線無活動期間傳送封包。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="4f9a0-111">這些 Keep-Alive 封包可確保永遠不會達到閒置逾時值，因此可以長期維持連線。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="4f9a0-112">此設定僅適用於輸入連線。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="4f9a0-113">若要避免連線中斷，您必須使用比閒置逾時設定短的間隔來設定 TCP Keep-Alive，或增加閒置逾時值。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="4f9a0-114">為了支援這類情況，我們新增了可設定閒置逾時的支援。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="4f9a0-115">您現在可以設定 4 至 30 分鐘的持續時間。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="4f9a0-116">TCP Keep-Alive 非常適合用於電池使用時間不受約束的情況。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="4f9a0-117">不建議用於行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="4f9a0-118">在行動裝置應用程式中使用 TCP Keep-Alive 可能會更快耗盡裝置電池電力。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![TCP 逾時](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="4f9a0-120">下列各節說明如何在虛擬機器和雲端服務中變更閒置逾時設定。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="4f9a0-121">將執行個體層級公用 IP 的 TCP 逾時值設定為 15 分鐘</span><span class="sxs-lookup"><span data-stu-id="4f9a0-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="4f9a0-122">`IdleTimeoutInMinutes` 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="4f9a0-123">若未設定，則預設的逾時為 4 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="4f9a0-124">可接受的逾時範圍為 4 到 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="4f9a0-125">在虛擬機器上建立 Azure 端點時設定閒置逾時</span><span class="sxs-lookup"><span data-stu-id="4f9a0-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="4f9a0-126">若要變更端點的逾時設定，請使用以下方法：</span><span class="sxs-lookup"><span data-stu-id="4f9a0-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="4f9a0-127">若要抓取閒置逾時組態，請使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="4f9a0-127">To retrieve your idle timeout configuration, use the following command:</span></span>

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
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

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="4f9a0-128">在負載平衡端點集上設定 TCP 逾時</span><span class="sxs-lookup"><span data-stu-id="4f9a0-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="4f9a0-129">如果端點是負載平衡端點集的一部分，就必須在負載平衡端點集上設定 TCP 逾時。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="4f9a0-130">例如：</span><span class="sxs-lookup"><span data-stu-id="4f9a0-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="4f9a0-131">變更雲端服務的逾時設定</span><span class="sxs-lookup"><span data-stu-id="4f9a0-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="4f9a0-132">您可以使用 Azure SDK 來更新雲端服務。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="4f9a0-133">您需在 .csdef 檔案中進行雲端服務的端點設定。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="4f9a0-134">若要更新雲端服務部署的 TCP 逾時，就必須進行部署升級。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="4f9a0-135">如果只針對公用 IP 指定 TCP 逾時，則為例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="4f9a0-136">公用 IP 設定是在 .cscfg 中，而您可以透過更新和升級部署來更新這些設定。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="4f9a0-137">端點設定的 .csdef 變更如下：</span><span class="sxs-lookup"><span data-stu-id="4f9a0-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="4f9a0-138">公用 IP 上逾時設定的 .cscfg 變更如下：</span><span class="sxs-lookup"><span data-stu-id="4f9a0-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

```xml
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

## <a name="rest-api-example"></a><span data-ttu-id="4f9a0-139">REST API 範例</span><span class="sxs-lookup"><span data-stu-id="4f9a0-139">REST API example</span></span>

<span data-ttu-id="4f9a0-140">您可以使用服務管理 API 來設定 TCP 閒置逾時。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="4f9a0-141">請確定 `x-ms-version` 標頭已設定為 `2014-06-01` 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="4f9a0-142">在部署中的所有虛擬機器上，更新指定負載平衡輸入端點的組態。</span><span class="sxs-lookup"><span data-stu-id="4f9a0-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="4f9a0-143">要求</span><span class="sxs-lookup"><span data-stu-id="4f9a0-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="4f9a0-144">Response</span><span class="sxs-lookup"><span data-stu-id="4f9a0-144">Response</span></span>

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a><span data-ttu-id="4f9a0-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f9a0-145">Next steps</span></span>

[<span data-ttu-id="4f9a0-146">內部負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="4f9a0-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="4f9a0-147">開始設定網際網路對向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4f9a0-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="4f9a0-148">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="4f9a0-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
