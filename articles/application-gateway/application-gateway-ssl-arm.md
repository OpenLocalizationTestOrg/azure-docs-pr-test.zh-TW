---
title: "aaaConfigure SSL 卸載 Azure 應用程式閘道-PowerShell |Microsoft 文件"
description: "本頁面提供的應用程式閘道以 SSL 卸載使用 Azure 資源管理員的指示 toocreate"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>使用 Azure 資源管理員設定適用於 SSL 的應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure 傳統 PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure 應用程式閘道可以在 hello 閘道 tooavoid 昂貴 SSL 解密工作 toohappen hello web 伺服陣列設定的 tooterminate hello Secure Sockets Layer (SSL) 工作階段。 Hello 前端伺服器安裝並管理 hello web 應用程式，也可以簡化 SSL 卸載。

## <a name="before-you-begin"></a>開始之前

1. 使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。 您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。
2. 您建立虛擬網路和 hello 應用程式閘道的子網路。 請確定沒有虛擬機器或雲端部署使用 hello 子網路。 應用程式閘道必須單獨在虛擬網路子網路中。
3. 設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或其端點建立 hello 虛擬網路中或與公用 IP/VIP 指派。

## <a name="what-is-required-toocreate-an-application-gateway"></a>什麼是必要的 toocreate 應用程式閘道？

* **後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。 列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。
* **後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。 流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些設定是區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。
* **規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。 目前，只有 hello*基本*規則支援。 hello*基本*規則是循環配置資源負載分佈。

**其他組態注意事項**

SSL 憑證設定，如 hello 中的通訊協定**HttpListener**也應該變更*Https* （區分大小寫）。 hello **SslCertificate**太新增項目**HttpListener** hello hello SSL 憑證設定的變數值。 hello 前端連接埠應為更新的 too443。

**tooenable cookie 為基礎的同質**： 應用程式閘道可以是來自用戶端工作階段的要求會導向的 toohello 設定的 tooensure hello web 伺服陣列中相同的 VM。 此案例中是由資料隱碼的工作階段 cookie，可讓 hello 閘道 toodirect 流量時，適當地完成。 tooenable cookie 架構親和性，設定**CookieBasedAffinity**太*啟用*在 hello **BackendHttpSettings**項目。

## <a name="create-an-application-gateway"></a>建立應用程式閘道

hello 使用 hello Azure 傳統部署模型和 Azure 資源管理員之間的差異是您建立應用程式閘道和 hello 需要的項目設定 toobe hello 順序。

使用資源管理員中，所有元件的應用程式閘道個別設定，然後放在一起 toocreate 應用程式閘道資源。

以下是 hello 所需的步驟 toocreate 應用程式閘道：

1. 建立資源管理員的資源群組
2. 建立虛擬網路、 子網路和 hello 應用程式閘道的公用 IP
3. 建立應用程式閘道組態物件
4. 建立應用程式閘道資源

## <a name="create-a-resource-group-for-resource-manager"></a>建立資源管理員的資源群組

請確定您切換 PowerShell 模式 toouse hello Azure 資源管理員 cmdlet。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。

### <a name="step-1"></a>步驟 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>步驟 2

請檢查 hello hello 帳戶的訂用帳戶。

```powershell
Get-AzureRmSubscription
```

您必須提示的 tooauthenticate 和您的認證。

### <a name="step-3"></a>步驟 3

選擇 Azure 訂用帳戶 toouse。

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>步驟 4

建立資源群組 (若使用現有的資源群組，請略過此步驟)。

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager 需要所有的資源群組指定一個位置。 此設定作為 hello 預設位置，該資源群組中的資源。 請確定應用程式閘道使用的所有命令 toocreate 都 hello 相同資源群組。

在 hello 上述範例中，我們建立一個稱為資源群組**appgw RG**和位置**美國西部**。

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>建立虛擬網路和 hello 應用程式閘道的子網路

下列範例會示範如何 hello toocreate 使用資源管理員的虛擬網路：

### <a name="step-1"></a>步驟 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

這個範例會指定 hello 位址範圍 10.0.0.0/24 tooa 子網路使用的變數 toobe toocreate 虛擬網路。

### <a name="step-2"></a>步驟 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

這個範例會建立虛擬網路，名為**appgwvnet**資源群組中**appgw rg** hello 前置詞 10.0.0.0/16 使用子網路 10.0.0.0/24 hello 美國西部地區。

### <a name="step-3"></a>步驟 3

```powershell
$subnet = $vnet.Subnets[0]
```

這個範例會將指派 hello 子網路物件 toovariable $subnet hello 接下來的步驟。

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>建立 hello 前端組態的公用 IP 位址

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

這個範例會建立公用 IP 資源**publicIP01**資源群組中**appgw rg** hello 美國西部地區。

## <a name="create-an-application-gateway-configuration-object"></a>建立應用程式閘道組態物件

### <a name="step-1"></a>步驟 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

此範例會建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。 應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。 請記住，每個執行個體需要一個 IP 位址。

### <a name="step-2"></a>步驟 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

這個範例會設定 hello 後端 IP 位址集區名稱為**pool01**與 IP 位址**134.170.185.46**， **134.170.188.221**， **134.170.185.50**. 這些值為 hello 收到 hello 來自 hello 前端 IP 端點的網路流量的 IP 位址。 取代從前面範例與 hello IP 位址的 web 應用程式端點的 hello hello IP 位址。

### <a name="step-3"></a>步驟 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

這個範例會設定應用程式閘道設定**poolsetting01** tooload 平衡 hello 後端集區中的網路流量。

### <a name="step-4"></a>步驟 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

這個範例會設定名為 hello 前端 IP 連接埠**frontendport01** hello 公用 IP 端點。

### <a name="step-5"></a>步驟 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

這個範例會設定 SSL 連接所使用的 hello 憑證。 hello 憑證必須以.pfx 格式 toobe 和 hello 密碼必須介於 4 too12 個字元之間。

### <a name="step-6"></a>步驟 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

這個範例會建立 hello 名為前端 IP 組態**fipconfig01**和相關聯 hello 與 hello 前端 IP 組態的公用 IP 位址。

### <a name="step-7"></a>步驟 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

這個範例會建立 hello 接聽程式名稱**listener01**和相關聯 hello 前端連接埠 toohello 前端 IP 組態和憑證。

### <a name="step-8"></a>步驟 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

這個範例會建立 hello 負載平衡器路由規則命名為**rule01** ，會設定 hello 負載平衡器行為。

### <a name="step-9"></a>步驟 9

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

這個範例會設定 hello hello 應用程式閘道執行個體大小。

> [!NOTE]
> 預設值的 hello *InstanceCount*為 2，最大值是 10。 預設值的 hello *GatewaySize*都是 Medium。 您可以在 Standard_Small、Standard_Medium 和 Standard_Large 之間選擇。

### <a name="step-10"></a>步驟 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

此步驟定義 hello SSL 原則 toouse hello 應用程式閘道。 請瀏覽[設定 SSL 的原則版本和應用程式閘道上的加密套件](application-gateway-configure-ssl-policy-powershell.md)toolearn 更多。

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>使用 New-AzureApplicationGateway 建立應用程式閘道

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

這個範例會建立應用程式閘道，並從先前步驟的 hello 的所有組態項目。 在 hello 範例中，稱為 hello 應用程式閘道**appgwtest**。

## <a name="get-application-gateway-dns-name"></a>取得應用程式閘道 DNS 名稱

一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。 當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。 tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。 [在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。 toodo hello 應用程式閘道及其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的這個，擷取詳細資料。 hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。 不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。


```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>後續步驟

如果您想 tooconfigure 內部負載平衡器 (ILB) 應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。

如果您想進一步了解一般負載平衡選項，請參閱：

* [Azure 負載平衡器](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure 流量管理員](https://azure.microsoft.com/documentation/services/traffic-manager/)

