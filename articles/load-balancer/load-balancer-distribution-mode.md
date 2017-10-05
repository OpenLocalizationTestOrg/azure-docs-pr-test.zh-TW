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
# <a name="configure-the-distribution-mode-for-load-balancer"></a>設定負載平衡器的分配模式

## <a name="hash-based-distribution-mode"></a>雜湊型分配模式

預設的分配演算法是 5-tuple (來源 IP、來源連接埠、目的地 IP、目的地連接埠、通訊協定類型) 的雜湊，將流量對應至可用的伺服器。 它只在傳輸工作階段內提供綁定。 相同工作階段中的封包會被導向至負載平衡端點後面的相同資料中心 IP (DIP) 執行個體。 當用戶端從相同的來源 IP 啟動新的工作階段時，來源連接埠便會變更，進而導致流量進入不同的 DIP 端點。

![雜湊型負載平衡器](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

圖 1 - 5-tuple 分配

## <a name="source-ip-affinity-mode"></a>來源 IP 同質性模式

我們有另一個名為「來源 IP 同質性」(也稱為工作階段同質性或用戶端 IP 同質性) 的分配模式。 您可以設定 Azure Load Balancer 使用 2-tuple (來源 IP、目的地 IP) 或 3 個 Tuple (來源 IP、目的地 IP 通訊協定)，來將流量對應至可用伺服器。 使用來源 IP 同質性之後，從相同用戶端電腦啟動的連線會進入相同的 DIP 端點。

下圖說明 2-tuple 的設定。 注意到 2-tuple 會透過負載平衡器執行到虛擬機器 1 (VM1)，並由 VM2 和 VM3 備份。

![工作階段同質](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

圖 2 - 2-tuple 分配

來源 IP 同質性可解決 Azure Load Balancer 和遠端桌面 (RD) 閘道器之間的不相容性。 現在，您可以在單一雲端服務中建立 RD 閘道伺服器陣列。

另一個使用案例是媒體上傳，媒體上傳會透過 UDP 進行資料上傳，但可透過 TCP 進入控制台：

* 用戶端首先會對負載平衡的公用位址啟動 TCP 工作階段，接著被導向至特定 DIP，此通道便會保持作用中狀態以監視連接健康狀態
* 來自相同用戶端電腦的新 UDP 工作階段會在相同的負載平衡公用端點中啟動，我們希望此連接會像先前的 TCP 連接一樣被導向至相同的 DIP 端點，以便在高輸送量時執行媒體上傳，並同時透過 TCP 維持控制通道。

> [!NOTE]
> 當負載平衡集變更時 (移除或新增虛擬機器)，則會重新計算用戶端要求的分配。 您無法確定現有用戶端的新連接最後都會抵達相同的伺服器。 此外，使用來源 IP 同質性分配模式可能會導致流量的不相等分配。 在 Proxy 後方執行的用戶端可能會被視為唯一用戶端應用程式。

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>進行負載平衡器的來源 IP 同質性設定

針對虛擬機器，您可以使用 PowerShell 來變更逾時設定：

將 Azure 端點新增到虛擬機器，並設定負載平衡器分配模式

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution 可設定為 sourceIP 以使用 2-tuple (來源 IP、目的地 IP) 負載平衡、設定為 sourceIPProtocol 以使用 3-tuple (來源 IP、目的地 IP、通訊協定) 負載平衡，或設定為 none 以使用預設的 5-tuple 負載平衡行為。

使用下列命令以擷取端點負載平衡器分配模式組態：

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

如果 LoadBalancerDistribution 項目不存在，則 Azure 負載平衡器會使用預設的 5-tuple 演算法。

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a>在負載平衡端點集上設定分配模式

如果端點是負載平衡端點集的一部分，就必須在負載平衡端點集上設定分配模式：

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a>可變更分配模式的雲端服務組態

您可以利用 Azure SDK for .NET 2.5 (將於 11 月發行) 來更新雲端服務。 雲端服務的端點設定是設定於 .csdef 中。 若要更新雲端服務部署的負載平衡器分配模式，部署升級是必要的。
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

您可以使用服務管理 API 來設定負載平衡器分配。 請務必新增已設定為 `2014-09-01` 版或更高版本的 `x-ms-version` 標頭。

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a>在部署中更新指定負載平衡集的設定

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

LoadBalancerDistribution 的值可以是 sourceIP (適用於 2-tuple 同質性)、sourceIPProtocol (適用於 3-tuple 同質性) 或 none (適用於沒有同質性。 也就是 5-tuple)

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
