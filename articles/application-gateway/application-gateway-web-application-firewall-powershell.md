---
title: "aaaConfigure web 應用程式防火牆 Azure 應用程式閘道 |Microsoft 文件"
description: "本文提供指引 toostart 使用 web 應用程式在現有或新的應用程式閘道上的防火牆。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>在新的或現有的應用程式閘道上設定 Web 應用程式防火牆

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

了解如何 toocreate web 應用程式防火牆啟用應用程式閘道，或將 web 應用程式防火牆 tooan 現有應用程式閘道。

hello web 應用程式中的防火牆 (WAF) Azure 應用程式閘道會從網頁型的常見攻擊，例如 SQL 資料隱碼、 跨網站指令碼的攻擊和工作階段倘若保護 web 應用程式。

Azure 應用程式閘道是第 7 層負載平衡器。 無論是在 hello 雲端或內部部署上，它會提供容錯移轉時，效能路由不同的伺服器之間的 HTTP 要求。 應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健康情況探查、多網站支援，以及許多其他功能。 toofind 完整支援的功能清單，請造訪：[應用程式閘道概觀](application-gateway-introduction.md)。

hello 下列文章將示範如何太[加入現有的應用程式閘道的 web 應用程式防火牆 tooan](#add-web-application-firewall-to-an-existing-application-gateway)和[建立應用程式閘道使用 web 應用程式防火牆](#create-an-application-gateway-with-web-application-firewall)。

![案例影像][scenario]

## <a name="waf-configuration-differences"></a>WAF 組態差異

如果您已閱讀[使用 PowerShell 建立應用程式閘道](application-gateway-create-gateway-arm.md)，當您了解 hello SKU 設定 tooconfigure 建立應用程式閘道。 WAF 提供額外的設定 toodefine 時應用程式閘道上設定 hello SKU。 沒有您在 hello 應用程式閘道本身進行任何其他變更。

| **設定** | **詳細資料**
|---|---|
|**SKU** |不具有 WAF 的一般應用程式閘道支援 **Standard\_Small**、**Standard\_Medium** 和 **Standard\_Large** 大小。 使用 WAF hello 介紹，有兩個額外的 Sku， **WAF\_媒體**和**WAF\_大**。 小型應用程式閘道不支援 WAF。|
|**層級** | hello 可用的值為**標準**或**WAF**。 使用 Web 應用程式防火牆時，必須選擇 **WAF** 。|
|**模式** | 這項設定是 WAF hello 模式。 允許的值為**偵測**和**防止**。 當 WAF 設定為偵測模式時，所有威脅會儲存在記錄檔中。 在防止模式中，還是會記錄事件，但 hello 攻擊者收到 hello 應用程式閘道 403 未經授權的回應。|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>加入 web 應用程式防火牆 tooan 現有應用程式閘道

請確定您使用 Azure PowerShell hello 最新版本。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。

1. 登入 tooyour Azure 帳戶。

    ```powershell
    Login-AzureRmAccount
    ```

2. 選取此案例中的 hello 訂用帳戶 toouse。

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. 擷取您要加入至 web 應用程式防火牆的 hello 閘道。

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. 設定 hello web 應用程式防火牆 sku。 hello 可用大小是**WAF\_大**和**WAF\_媒體**。 使用 web 應用程式的防火牆時 hello 階層必須**WAF**，設定 hello sku 時，必須確認 hello 容量。

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. 設定 hello WAF hello 下列範例中所定義：

   如**FirewallMode**，hello 可用的值為預防和偵測。

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. 更新應用程式閘道 hello hello hello 前面步驟中所定義的設定。

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

此命令會更新 web 應用程式防火牆 hello 應用程式閘道。 請瀏覽[應用程式閘道診斷](application-gateway-diagnostics.md)toounderstand tooview 記錄您的應用程式閘道的方式。 WAF toohello 安全性本質，因為記錄檔需要 toobe 定期檢閱 toounderstand hello 安全性狀態的 web 應用程式。

## <a name="create-an-application-gateway-with-web-application-firewall"></a>建立具有 Web 應用程式防火牆的應用程式閘道

hello 下列步驟引導您進行整個 hello 開頭 tooend 使用 web 應用程式防火牆中建立應用程式閘道的程序。

請確定您使用 Azure PowerShell hello 最新版本。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。

1. 執行登入 tooAzure `Login-AzureRmAccount`，您會使用您的認證的提示的 tooauthenticate。

1. 執行檢查 hello 訂閱 hello 帳戶`Get-AzureRmSubscription`

1. 選擇 Azure 訂用帳戶 toouse。

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>建立資源群組

建立 hello 應用程式閘道的資源群組。

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager 需要所有的資源群組指定一個位置。 此位置用於 hello 預設位置為該資源群組。 請確定所有命令使用的應用程式閘道 toocreate 都 hello 相同的資源群組。

在上述範例中的 hello，我們會建立名為"appgw RG 」 和 「 位置 」 美國西部。 」 的資源群組

> [!NOTE]
> 如果您需要 tooconfigure 自訂探查您應用程式閘道，請參閱[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-ps.md)。 請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。

### <a name="configure-virtual-network"></a>設定虛擬網路

應用程式閘道需要有自己的子網路。 在此步驟中，您可以建立具有 10.0.0.0/16 和兩個子網路的位址空間，一個用於 hello 應用程式閘道，一個用於後端集區成員的虛擬網路。

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>設定公用 IP 位址

在訂單 toohandle 外部要求中，應用程式閘道需要公用 IP 位址。 這個公用 IP 位址不能有`DomainNameLabel`定義 toobe hello 應用程式閘道所使用。

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>設定應用程式閘道 hello

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> 建立與 hello 基本 web 應用程式的防火牆設定的應用程式閘道設定成使用 CR 3.0 保護。

## <a name="get-application-gateway-dns-name"></a>取得應用程式閘道 DNS 名稱

一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。 當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。 tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。 [在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。 tooconfigure 別名，擷取 hello 應用程式閘道和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 附加項目 toohello 應用程式閘道的詳細資料。 hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。 不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。

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

深入了解如何 tooconfigure 診斷記錄，toolog hello 或之事件的偵測到使用 web 應用程式防火牆阻止造訪[應用程式閘道診斷](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
