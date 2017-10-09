---
title: "aaaConfigure 負載平衡器 TCP 閒置逾時 |Microsoft 文件"
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
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="6f1ea-103">設定 Azure Load Balancer 的 TCP 閒置逾時設定</span><span class="sxs-lookup"><span data-stu-id="6f1ea-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="6f1ea-104">在預設組態中，Azure Load Balancer 的閒置逾時設定是 4 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="6f1ea-105">如果一段時間的長度大於 hello 逾時值，保證 hello TCP 或 HTTP 工作階段仍可維持 hello 用戶端和雲端服務之間。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="6f1ea-106">Hello 連接關閉時，用戶端應用程式可能會收到下列錯誤訊息的 hello:"hello 基礎連接已關閉： 必須保持運作的 toobe hello 伺服器已關閉的連接。 」</span><span class="sxs-lookup"><span data-stu-id="6f1ea-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="6f1ea-107">常見的作法是 toouse TCP 保持連線。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="6f1ea-108">這種作法會讓 hello 連線作用更長的時間。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="6f1ea-109">如需詳細資訊，請參閱這些 [.NET 文章](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="6f1ea-110">保持啟用，hello 連接上的無活動期間傳送封包。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="6f1ea-111">永遠不會達到 hello 閒置逾時值，並維持 hello 連線長，請確定這些保持運作封包。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="6f1ea-112">此設定僅適用於輸入連線。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="6f1ea-113">tooavoid 遺失 hello 連線，您必須設定 hello TCP 保持連接間隔 hello 閒置逾時設定或增加 hello 閒置逾時值大於或等於。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="6f1ea-114">toosupport 這類情況下，我們已加入支援可設定的閒置逾時。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="6f1ea-115">您現在可以設定 4 too30 分鐘持續時間。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="6f1ea-116">TCP Keep-Alive 非常適合用於電池使用時間不受約束的情況。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="6f1ea-117">不建議用於行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="6f1ea-118">使用 TCP 保持連線的行動應用程式中耗電 hello 裝置電池速度更快。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![TCP 逾時](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="6f1ea-120">hello 下列各節說明如何 toochange 閒置逾時設定的虛擬機器和雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="6f1ea-121">設定程式執行個體層級公用 IP too15 分鐘 hello TCP 逾時</span><span class="sxs-lookup"><span data-stu-id="6f1ea-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="6f1ea-122">`IdleTimeoutInMinutes` 為選擇性。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="6f1ea-123">如果未設定，hello 預設逾時為 4 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="6f1ea-124">hello 可接受的逾時範圍為 4 的 too30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="6f1ea-125">建立虛擬機器上的 Azure 端點時設定 hello 閒置逾時</span><span class="sxs-lookup"><span data-stu-id="6f1ea-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="6f1ea-126">toochange hello 逾時設定的端點，請使用下列 hello:</span><span class="sxs-lookup"><span data-stu-id="6f1ea-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="6f1ea-127">tooretrieve 您的閒置逾時設定，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="6f1ea-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="6f1ea-128">負載平衡端點集上設定 hello TCP 逾時</span><span class="sxs-lookup"><span data-stu-id="6f1ea-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="6f1ea-129">如果端點屬於負載平衡端點集的一部分，hello TCP 逾時必須設定 hello 負載平衡端點集。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="6f1ea-130">例如：</span><span class="sxs-lookup"><span data-stu-id="6f1ea-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="6f1ea-131">變更雲端服務的逾時設定</span><span class="sxs-lookup"><span data-stu-id="6f1ea-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="6f1ea-132">您可以使用 hello Azure SDK tooupdate 您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="6f1ea-133">您可以建立雲端服務的端點設定 hello.csdef 檔案中。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="6f1ea-134">更新雲端服務部署的 hello TCP 逾時，將需要部署升級。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="6f1ea-135">例外狀況是 hello TCP 逾時，如果要指定僅針對公用 IP。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="6f1ea-136">公用 IP 設定會在 hello.cscfg 檔案中，並透過部署更新和升級加以更新。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="6f1ea-137">端點設定的 hello.csdef 變更如下：</span><span class="sxs-lookup"><span data-stu-id="6f1ea-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="6f1ea-138">公用 Ip 上 hello 逾時設定的 hello.cscfg 變更如下：</span><span class="sxs-lookup"><span data-stu-id="6f1ea-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="6f1ea-139">REST API 範例</span><span class="sxs-lookup"><span data-stu-id="6f1ea-139">REST API example</span></span>

<span data-ttu-id="6f1ea-140">您可以使用 hello 服務管理 API，以設定 hello TCP 閒置逾時。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="6f1ea-141">請確定該 hello`x-ms-version`標頭設定 tooversion`2014-06-01`或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="6f1ea-142">將指定的負載平衡輸入的端點的 hello 更新 hello 組態在部署中的所有虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="6f1ea-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="6f1ea-143">要求</span><span class="sxs-lookup"><span data-stu-id="6f1ea-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="6f1ea-144">Response</span><span class="sxs-lookup"><span data-stu-id="6f1ea-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6f1ea-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f1ea-145">Next steps</span></span>

[<span data-ttu-id="6f1ea-146">內部負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="6f1ea-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="6f1ea-147">開始設定網際網路對向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="6f1ea-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="6f1ea-148">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="6f1ea-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
