---
title: "aaaConfigure 負載平衡器通訊模式 |Microsoft 文件"
description: "如何 tooconfigure Azure 負載平衡器通訊模式 toosupport 來源 IP 相似性"
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
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>設定負載平衡器的 hello 分散模式

## <a name="hash-based-distribution-mode"></a>雜湊型分配模式

hello 預設分配演算法是 5 個 tuple (來源 IP、 來源連接埠，目的地 IP、 目的地連接埠通訊協定類型) 雜湊 toomap 流量 tooavailable 伺服器。 它只在傳輸工作階段內提供綁定。 在相同的工作階段將為的 hello 封包導向的 toohello hello 負載平衡端點之後執行個體的相同資料中心 IP (DIP)。 Hello 用戶端啟動時從新的工作階段 hello 相同的來源 IP、 hello 來源連接埠變更，並造成 hello 流量 toogo tooa 不同 DIP 的端點。

![雜湊型負載平衡器](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

圖 1 - 5-tuple 分配

## <a name="source-ip-affinity-mode"></a>來源 IP 同質性模式

我們有另一個名為「來源 IP 同質性」(也稱為工作階段同質性或用戶端 IP 同質性) 的分配模式。 Azure 負載平衡器可以設定的 toouse 2-tuple （來源 IP、 目的地 IP） 或 3 tuple （來源 IP、 目的地 IP 通訊協定） toomap 流量 toohello 可用的伺服器。 使用來源 IP 親和性，連線從起始 hello 相同用戶端電腦會進入 toohello 相同 DIP 端點。

hello 下列圖表說明 2-tuple 組態。 請注意 hello 2-tuple 透過 hello 負載平衡器 toovirtual 機器 1 (VM1) 然後 VM2 和 VM3 所備份的執行方式。

![工作階段同質](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

圖 2 - 2-tuple 分配

來源 IP 親和性可解決 hello Azure 負載平衡器和遠端桌面閘道之間的不相容。 現在，您可以在單一雲端服務中建立 RD 閘道伺服器陣列。

另一個使用案例是媒體上傳 hello 資料上傳會透過 UDP 進行，但 hello 控制平面透過 TCP 來達成：

* 用戶端第一次初始化 toohello 負載平衡公用位址的 TCP 工作階段、 取得特定的 DIP，此通道是導向的 tooa 左 active toomonitor hello 連線健全狀況
* 新的工作階段 UDP hello 相同用戶端電腦是從起始 toohello 相同負載平衡公用端點，這裡 hello 預期這個連接也會導向的 toohello 相同 DIP 端點做為 hello 先前的 TCP 連接，以便上傳媒體可以是同時也會維護透過 TCP 控制通道，以執行於高輸送量。

> [!NOTE]
> 當負載平衡集變更 （移除或新增虛擬機器） 時、 hello 發佈的用戶端要求會重新計算。 您不能相依於新的連線，從現有的用戶端最後 hello 在相同伺服器。 此外，使用來源 IP 同質性分配模式可能會導致流量的不相等分配。 在 Proxy 後方執行的用戶端可能會被視為唯一用戶端應用程式。

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>進行負載平衡器的來源 IP 同質性設定

針對虛擬機器，您可以使用 PowerShell toochange 逾時設定：

新增 Azure 端點 tooa 虛擬機器並設定負載平衡器通訊模式

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution 可以設定 toosourceIP 2-tuple （來源 IP、 目的地 IP） 負載平衡，負載平衡 3 tuple （來源 IP、 目的地 IP 通訊協定），或無 sourceIPProtocol 如果您要的 5 個 tuple 負載平衡的 hello 預設行為。

使用下列 tooretrieve 端點負載平衡器通訊模式組態 hello:

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

如果 hello LoadBalancerDistribution 項目不存在 hello Azure 負載平衡器會使用 hello 預設 5-tuple 演算法。

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>設定負載平衡端點集 hello 分散模式

如果端點是負載平衡端點集的一部分，必須設定 hello 分散模式 hello 負載平衡端點集：

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>雲端服務組態 toochange 分散模式

您可以利用 hello Azure SDK for.NET 2.5 (toobe 11 月發行) tooupdate 您的雲端服務。 在 hello.csdef 中進行雲端服務的端點設定。 順序 tooupdate hello 負載平衡器通訊模式將雲端服務部署，在部署升級則是必要項目。
適用於端點設定的 .csdef 變更範例如下：

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

## <a name="api-example"></a>API 範例

您可以設定使用 hello 服務管理 API 的 hello 負載平衡器發佈。 請確定 tooadd hello`x-ms-version`標頭設定 tooversion`2014-09-01`或更高版本。

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>更新部署中的 hello 組態的 hello 指定負載平衡集

#### <a name="request-example"></a>要求範例

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

LoadBalancerDistribution hello 值可以是 sourceIP 2-tuple 親和性、 sourceIPProtocol 3 tuple 親和性或無 （無親和性。 也就是 5-tuple)

#### <a name="response"></a>Response

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>後續步驟

[內部負載平衡器概觀](load-balancer-internal-overview.md)

[開始設定網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
