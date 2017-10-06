---
title: "aaaCreate，啟動或刪除應用程式閘道 |Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定、 啟動和刪除 Azure 應用程式閘道"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>使用 PowerShell 建立、啟動或刪除應用程式閘道 

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure 傳統 PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager 範本](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure 應用程式閘道是第 7 層負載平衡器。 無論是在 hello 雲端或內部部署上，它會提供容錯移轉時，效能路由不同的伺服器之間的 HTTP 要求。 應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健全狀態探查、多網站支援，以及許多其他功能。 toofind 完整支援的功能清單，請瀏覽[應用程式閘道概觀](application-gateway-introduction.md)

本文將引導您完成 hello 步驟 toocreate、 設定、 啟動及刪除應用程式閘道。

## <a name="before-you-begin"></a>開始之前

1. 使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。 您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。
2. 如果您有現有的虛擬網路，選取現有的空白子網路，或僅用於在現有的虛擬網路中建立新的子網路，hello 應用程式閘道。 您無法將部署 hello 應用程式閘道 tooa 不同虛擬網路 hello 資源比您想 hello 應用程式閘道後方 toodeploy 除非使用了對等互連的 vnet。 toolearn 更造訪[對等互連的 Vnet](../virtual-network/virtual-network-peering-overview.md)
3. 請確認您的運作中虛擬網路具有有效子網路。 請確定沒有虛擬機器或雲端部署使用 hello 子網路。 hello 應用程式閘道必須單獨在虛擬網路子網路。
4. 您設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或指派建立 hello 虛擬網路中，或是具有公用 IP/VIP 端點。

## <a name="what-is-required-toocreate-an-application-gateway"></a>什麼是必要的 toocreate 應用程式閘道？

當您使用 hello`New-AzureApplicationGateway`命令 toocreate hello 應用程式閘道，此時設定任何設定，以及設定 hello 新建立的資源使用 XML 或設定物件。

hello 的值如下：

* **後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。 列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。
* **後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。 流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。
* **規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。

## <a name="create-an-application-gateway"></a>建立應用程式閘道

toocreate 應用程式閘道：

1. 建立應用程式閘道資源。
2. 建立設定 XML 檔案或設定物件。
3. 認可新建立的應用程式閘道資源 hello 組態 toohello。

> [!NOTE]
> 如果您需要 tooconfigure 自訂探查您應用程式閘道，請參閱[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-classic-ps.md)。 請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。

![案例範例][scenario]

### <a name="create-an-application-gateway-resource"></a>建立應用程式閘道資源

toocreate hello 閘道，使用 hello `New-AzureApplicationGateway` cmdlet，取代您自己 hello 值。 此時無法啟動的 hello 閘道計費。 計費開始在稍後步驟中，當 hello 閘道已順利啟動。

hello 下列範例會建立應用程式閘道使用名為"testvnet1"，稱為 「 子網路-1"的子網路的虛擬網路：

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

Description、InstanceCount 和 GatewaySize 為選擇性參數。

hello 閘道的 toovalidate 所建立，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> 預設值的 hello *InstanceCount*為 2，最大值是 10。 預設值的 hello *GatewaySize*都是 Medium。 您可以選擇 Small、Medium 和 Large。

*如*和*DnsName*會顯示為空白，因為 hello 閘道尚未啟動。 這些被建立一旦 hello 閘道處於執行中狀態的 hello。

## <a name="configure-hello-application-gateway"></a>設定 hello 應用程式閘道

您可以使用 XML 或設定物件，以設定 hello 應用程式閘道。

### <a name="configure-hello-application-gateway-by-using-xml"></a>使用 XML 設定 hello 應用程式閘道

在下列範例的 hello，您可以使用 XML 檔案 tooconfigure 所有應用程式閘道設定，並認可 toohello 應用程式閘道資源。  

#### <a name="step-1"></a>步驟 1

複製下列文字 tooNotepad hello。

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

編輯 hello hello 設定項目的 hello 括號之間的值。 儲存副檔名的.xml hello 檔案。

> [!IMPORTANT]
> Http 或 Https 的 hello 通訊協定項目會區分大小寫。

hello 下列範例顯示如何 toouse 組態檔案 tooset hello 應用程式閘道設定。 hello 範例負載平衡公用連接埠 80 上的 HTTP 流量，並將網路流量傳送兩個 IP 位址之間的 tooback 結束連接埠 80。

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a>步驟 2

接下來，設定 hello 應用程式閘道。 使用 hello `Set-AzureApplicationGatewayConfig` cmdlet 搭配組態 XML 檔案。

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>使用組態物件設定 hello 應用程式閘道

hello 下列範例顯示如何 tooconfigure hello 使用組態物件的應用程式閘道。 所有設定項目必須個別設定，並接著加入 tooan 應用程式閘道組態物件。 建立 hello 組態物件後，您可以使用 hello`Set-AzureApplicationGateway`命令 toocommit hello 組態 toohello 先前建立的應用程式閘道資源。

> [!NOTE]
> 之前指派值 tooeach 組態物件，您必須 toodeclare 何種物件 PowerShell 會使用儲存體。 hello 第一列 toocreate hello 個別項目定義項目的`Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)`可用。

#### <a name="step-1"></a>步驟 1

建立所有的個別設定項目。

建立 hello 前端 IP，hello 下列範例所示。

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

建立 hello 前端連接埠，hello 下列範例所示。

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

建立 hello 後端伺服器集區。

定義會加入 toohello 後端伺服器集區中 hello 下一個範例所示的 hello IP 位址。

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

使用 hello $server tooadd hello 值 toohello 後端集區物件 ($pool)。

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

建立 hello 後端伺服器集區設定。

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

建立 hello 接聽程式。

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

建立 hello 規則。

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>步驟 2

所有個別設定項目 tooan 應用程式閘道組態將物件指派 ($appgwconfig)。

加入 hello 前端 IP toohello 組態。

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

加入 hello 前端連接埠 toohello 組態。

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
加入 hello 後端伺服器集區 toohello 組態。

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

加入 hello 後端集區設定 toohello 組態。

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

加入 hello 接聽程式 toohello 組態。

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

加入 hello 規則 toohello 組態。

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>步驟 3
認可 hello 組態物件 toohello 應用程式閘道資源使用`Set-AzureApplicationGatewayConfig`。

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>啟動 hello 閘道

一旦已設定 hello 閘道，使用 hello `Start-AzureApplicationGateway` cmdlet toostart hello 閘道。 在 hello 閘道已順利啟動後，就會開始計費，應用程式閘道。

> [!NOTE]
> hello `Start-AzureApplicationGateway` cmdlet 可能會佔用 toofinish too15 20 分鐘。

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>驗證 hello 閘道器狀態

使用 hello `Get-AzureApplicationGateway` hello 閘道 cmdlet toocheck hello 狀態。 如果`Start-AzureApplicationGateway`hello 先前步驟中，在成功*狀態*應執行和*Vip*和*DnsName*應該具有有效的項目。

hello 下列範例將示範會啟動、 執行的應用程式閘道，並準備好 tootake 流量目的地為`http://<generated-dns-name>.cloudapp.net`。

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>刪除 hello 應用程式閘道

toodelete hello 應用程式閘道：

1. 使用 hello `Stop-AzureApplicationGateway` cmdlet toostop hello 閘道。
2. 使用 hello `Remove-AzureApplicationGateway` cmdlet tooremove hello 閘道。
3. 確認已移除該 hello 閘道使用 hello `Get-AzureApplicationGateway` cmdlet。

hello 下列範例顯示 hello `Stop-AzureApplicationGateway` cmdlet hello 第一行，後面接著 hello 輸出。

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

處於停止狀態 hello 應用程式閘道之後，請使用 hello `Remove-AzureApplicationGateway` cmdlet tooremove hello 服務。

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

已移除 hello 服務的 tooverify，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。 這不是必要步驟。

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>後續步驟

如果您想的 tooconfigure SSL 卸載，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。

如果您想 tooconfigure 內部負載平衡器的應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。

如果您想進一步了解一般負載平衡選項，請參閱：

* [Azure 負載平衡器](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure 流量管理員](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
