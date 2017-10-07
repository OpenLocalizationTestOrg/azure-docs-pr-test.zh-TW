---
title: "aaaConfigure SSL 卸載 Azure 應用程式閘道-PowerShell 傳統 |Microsoft 文件"
description: "本文章提供應用程式閘道以 SSL 卸載使用 toocreate hello Azure 傳統部署模型的指示。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>設定 SSL 卸載的應用程式閘道使用 hello 傳統部署模型

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure 傳統 PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure 應用程式閘道可以在 hello 閘道 tooavoid 昂貴 SSL 解密工作 toohappen hello web 伺服陣列設定的 tooterminate hello Secure Sockets Layer (SSL) 工作階段。 Hello 前端伺服器安裝並管理 hello web 應用程式，也可以簡化 SSL 卸載。

## <a name="before-you-begin"></a>開始之前

1. 使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。 您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。
2. 請確認您的運作中虛擬網路具有有效子網路。 請確定沒有虛擬機器或雲端部署使用 hello 子網路。 hello 應用程式閘道必須單獨在虛擬網路子網路。
3. 您設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或指派建立 hello 虛擬網路中，或是具有公用 IP/VIP 端點。

tooconfigure SSL 卸載應用程式閘道上，執行 hello hello 依列出的順序執行步驟：

1. [建立應用程式閘道](#create-an-application-gateway)
2. [上傳 SSL 憑證](#upload-ssl-certificates)
3. [Hello 閘道設定](#configure-the-gateway)
4. [設定 hello 閘道組態](#set-the-gateway-configuration)
5. [啟動 hello 閘道](#start-the-gateway)
6. [驗證 hello 閘道器狀態](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>建立應用程式閘道

toocreate hello 閘道，使用 hello `New-AzureApplicationGateway` cmdlet，取代您自己 hello 值。 此時無法啟動的 hello 閘道計費。 計費開始在稍後步驟中，當 hello 閘道已順利啟動。

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

hello 閘道的 toovalidate 所建立，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。

在 hello 範例中，*描述*， *InstanceCount*，和*GatewaySize*是選擇性參數。 預設值的 hello *InstanceCount*為 2，最大值是 10。 預設值的 hello *GatewaySize*都是 Medium。 Small 和 Large 也是可用的值。 *如*和*DnsName*會顯示為空白，因為 hello 閘道尚未啟動。 執行中狀態的 hello hello 閘道之後，會建立這些值。

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>上傳 SSL 憑證

使用`Add-AzureApplicationGatewaySslCertificate`tooupload hello 伺服器憑證中的*pfx*格式 toohello 應用程式閘道。 hello 憑證名稱是使用者所選名稱，而且必須是唯一在 hello 應用程式閘道中。 此憑證是參照的 tooby hello 應用程式閘道上的所有憑證管理作業的這個名稱。

此下列範例顯示 hello cmdlet，在 hello 範例中的 hello 值取代為您自己。

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

接下來，驗證 hello 憑證上傳。 使用 hello `Get-AzureApplicationGatewayCertificate` cmdlet。

這個範例會顯示 hello cmdlet hello 第一行，後面接著 hello 輸出。

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> hello 憑證密碼有 toobe 之間 4 too12 字元、 字母或數字。 不接受使用特殊字元。

## <a name="configure-hello-gateway"></a>Hello 閘道設定

應用程式閘道組態是由多個值所組成。 hello 值可以繫結在一起的 tooconstruct hello 組態。

hello 的值如下：

* **後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。 列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。
* **後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。 流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。
* **規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。 目前，只有 hello*基本*規則支援。 hello*基本*規則是循環配置資源負載分佈。

**其他組態注意事項**

SSL 憑證設定，如 hello 中的通訊協定**HttpListener**也應該變更*Https* （區分大小寫）。 hello **SslCert**太新增項目**HttpListener** hello 與值設定的 toohello hello 上傳之前 SSL 憑證 > 一節中所使用相同的名稱。 hello 前端連接埠應為更新的 too443。

**tooenable cookie 為基礎的同質**： 應用程式閘道可以是來自用戶端工作階段的要求會導向的 toohello 設定的 tooensure hello web 伺服陣列中相同的 VM。 此案例中是由資料隱碼的工作階段 cookie，可讓 hello 閘道 toodirect 流量時，適當地完成。 tooenable cookie 架構親和性，設定**CookieBasedAffinity**太*啟用*在 hello **BackendHttpSettings**項目。

建立組態物件或使用組態 XML 檔案，即可建構組態。
tooconstruct 您使用組態 XML 檔案的組態，請使用下列範例 hello:

**組態 XML 範例**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a>設定 hello 閘道組態

接下來，您可以設定 hello 應用程式閘道。 您可以使用 hello`Set-AzureApplicationGatewayConfig`指令程式與組態的物件或設定 XML 檔案。

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>啟動 hello 閘道

一旦已設定 hello 閘道，使用 hello `Start-AzureApplicationGateway` cmdlet toostart hello 閘道。 在 hello 閘道已順利啟動後，就會開始計費，應用程式閘道。

> [!NOTE]
> hello `Start-AzureApplicationGateway` cmdlet 可能會佔用 toofinish too15 20 分鐘。
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>驗證 hello 閘道器狀態

使用 hello `Get-AzureApplicationGateway` hello 閘道 cmdlet toocheck hello 狀態。 如果`Start-AzureApplicationGateway`hello 先前步驟中，在成功*狀態*應執行和*如*和*DnsName*應該具有有效的項目。

這個範例會顯示應用程式閘道的執行中，已啟動，且準備好 tootake 流量。

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>後續步驟

如果您想進一步了解一般負載平衡選項，請參閱：

* [Azure 負載平衡器](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure 流量管理員](https://azure.microsoft.com/documentation/services/traffic-manager/)

