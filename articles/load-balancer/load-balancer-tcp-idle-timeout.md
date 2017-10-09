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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>設定 Azure Load Balancer 的 TCP 閒置逾時設定

在預設組態中，Azure Load Balancer 的閒置逾時設定是 4 分鐘。 如果一段時間的長度大於 hello 逾時值，保證 hello TCP 或 HTTP 工作階段仍可維持 hello 用戶端和雲端服務之間。

Hello 連接關閉時，用戶端應用程式可能會收到下列錯誤訊息的 hello:"hello 基礎連接已關閉： 必須保持運作的 toobe hello 伺服器已關閉的連接。 」

常見的作法是 toouse TCP 保持連線。 這種作法會讓 hello 連線作用更長的時間。 如需詳細資訊，請參閱這些 [.NET 文章](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx)。 保持啟用，hello 連接上的無活動期間傳送封包。 永遠不會達到 hello 閒置逾時值，並維持 hello 連線長，請確定這些保持運作封包。

此設定僅適用於輸入連線。 tooavoid 遺失 hello 連線，您必須設定 hello TCP 保持連接間隔 hello 閒置逾時設定或增加 hello 閒置逾時值大於或等於。 toosupport 這類情況下，我們已加入支援可設定的閒置逾時。 您現在可以設定 4 too30 分鐘持續時間。

TCP Keep-Alive 非常適合用於電池使用時間不受約束的情況。 不建議用於行動應用程式。 使用 TCP 保持連線的行動應用程式中耗電 hello 裝置電池速度更快。

![TCP 逾時](./media/load-balancer-tcp-idle-timeout/image1.png)

hello 下列各節說明如何 toochange 閒置逾時設定的虛擬機器和雲端服務。

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>設定程式執行個體層級公用 IP too15 分鐘 hello TCP 逾時

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` 為選擇性。 如果未設定，hello 預設逾時為 4 分鐘。 hello 可接受的逾時範圍為 4 的 too30 分鐘。

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>建立虛擬機器上的 Azure 端點時設定 hello 閒置逾時

toochange hello 逾時設定的端點，請使用下列 hello:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve 您的閒置逾時設定，下列命令使用 hello:

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>負載平衡端點集上設定 hello TCP 逾時

如果端點屬於負載平衡端點集的一部分，hello TCP 逾時必須設定 hello 負載平衡端點集。 例如：

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>變更雲端服務的逾時設定

您可以使用 hello Azure SDK tooupdate 您的雲端服務。 您可以建立雲端服務的端點設定 hello.csdef 檔案中。 更新雲端服務部署的 hello TCP 逾時，將需要部署升級。 例外狀況是 hello TCP 逾時，如果要指定僅針對公用 IP。 公用 IP 設定會在 hello.cscfg 檔案中，並透過部署更新和升級加以更新。

端點設定的 hello.csdef 變更如下：

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

公用 Ip 上 hello 逾時設定的 hello.cscfg 變更如下：

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

## <a name="rest-api-example"></a>REST API 範例

您可以使用 hello 服務管理 API，以設定 hello TCP 閒置逾時。 請確定該 hello`x-ms-version`標頭設定 tooversion`2014-06-01`或更新版本。 將指定的負載平衡輸入的端點的 hello 更新 hello 組態在部署中的所有虛擬機器上。

### <a name="request"></a>要求

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Response

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

## <a name="next-steps"></a>後續步驟

[內部負載平衡器概觀](load-balancer-internal-overview.md)

[開始設定網際網路對向負載平衡器](load-balancer-get-started-internet-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)
