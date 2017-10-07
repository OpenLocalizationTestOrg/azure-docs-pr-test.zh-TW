---
title: "應用程式來裝載多個站台閘道 aaaCreate |Microsoft 文件"
description: "本頁面提供的指示 toocreate，設定裝載多個 web 應用程式上 hello Azure 應用程式閘道相同的閘道。"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>建立應用程式閘道來裝載多個 Web 應用程式

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)

多個站台裝載可讓您以上一個 web 應用程式的 toodeploy hello 上相同的應用程式閘道。 它依賴在 hello 的傳入 HTTP 要求，而 toodetermine 的接聽程式將會收到流量的主機標頭存在。 hello 接聽程式，然後指示流量 tooappropriate 後端集區中的 hello 閘道 hello 規則定義的設定。 在啟用 SSL 的 web 應用程式，應用程式閘道依賴 hello 伺服器名稱指示 (SNI) 延伸模組 toochoose hello 正確接聽程式 hello 網路流量。 多個站台裝載的常見用法是不同的網頁網域 toodifferent 後端伺服器集區的 tooload 平衡要求。 同樣的多個相同的根網域也無法裝載在 hello 的子網域 hello 相同的應用程式閘道。

## <a name="scenario"></a>案例

在下列範例的 hello，應用程式閘道為 contoso.com 和 fabrikam.com 的流量提供兩個後端伺服器集區： contoso 伺服器集區及 fabrikam 伺服器集區。 類似的安裝程式可能使用的 toohost 子網域，例如 app.contoso.com 和 blog.contoso.com。

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>開始之前

1. 使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。 您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。
2. hello 伺服器加入 toohello 後端集區 toouse hello 應用程式閘道必須存在，或其端點建立在 hello 虛擬網路中不同的子網路或公用 IP/指派的 VIP。

## <a name="requirements"></a>需求

* **後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。 列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。 您也可以使用 FQDN。
* **後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。 流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。 針對啟用多站台功能的應用程式閘道，會一併新增主機名稱和 SNI 指示器。
* **規則：** hello 規則繫結 hello 接聽程式，hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。 規則會在處理 hello 排列順序，而且將會導向流量，透過 hello 比對，不論明確性比較的第一個規則。 比方說，如果您有使用基本的接聽程式的規則和規則，使用多站台接聽程式同時在相同連接埠，與 hello 規則 hello hello 多站台接聽程式必須列出 hello 規則之前為 hello 多站台規則 toofunction 順序中的 hello 基本接聽程式預期的。

## <a name="create-an-application-gateway"></a>建立應用程式閘道

hello 以下是需要 toocreate 應用程式閘道 hello 步驟：

1. 建立資源管理員的資源群組。
2. 建立虛擬網路、 子網路和 hello 應用程式閘道的公用 IP。
3. 建立應用程式閘道組態物件。
4. 建立應用程式閘道資源。

## <a name="create-a-resource-group-for-resource-manager"></a>建立資源管理員的資源群組

請確定您使用 Azure PowerShell hello 最新版本。 如需詳細資訊，可在[搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md) 取得。

### <a name="step-1"></a>步驟 1

登入 tooAzure

```powershell
Login-AzureRmAccount
```
您必須提示的 tooauthenticate 和您的認證。

### <a name="step-2"></a>步驟 2

請檢查 hello hello 帳戶的訂用帳戶。

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>步驟 3

選擇 Azure 訂用帳戶 toouse。

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>步驟 4

建立資源群組 (若使用現有的資源群組，請略過此步驟)。

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

或者，您也可以針對應用程式閘道建立資源群組的標記：

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Azure Resource Manager 需要所有的資源群組指定一個位置。 此位置用於 hello 預設位置為該資源群組。 請確定所有命令 toocreate 應用程式閘道使用 hello 相同的資源群組。

在 hello 上述範例中，我們建立一個稱為資源群組**appgw RG**位置**美國西部**。

> [!NOTE]
> 如果您需要 tooconfigure 自訂探查您應用程式閘道，請參閱[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-ps.md)。 請造訪[自訂探查和健全狀況監視](application-gateway-probe-overview.md)以取得詳細資訊。

## <a name="create-a-virtual-network-and-subnets"></a>建立虛擬網路和子網路

下列範例會示範如何 hello toocreate 使用資源管理員的虛擬網路。 此步驟中會建立兩個子網路。 hello 第一個子網路是 hello 應用程式閘道本身。 應用程式閘道需要它自己的子網路 toohold 其執行個體。 在該子網路中只能部署其他應用程式閘道。 hello 第二個子網路是使用的 toohold hello 應用程式後端伺服器。

### <a name="step-1"></a>步驟 1

指派 hello 位址範圍 10.0.0.0/24 toohello 子網路變數 toobe 使用的 toohold hello 應用程式閘道。

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>步驟 2

指派 hello 位址範圍 10.0.1.0/24 toohello subnet2 變數 toobe 用於 hello 後端集區。

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>步驟 3

建立虛擬網路，名為**appgwvnet**資源群組中**appgw rg** hello 前置詞 10.0.0.0/16 使用子網路 10.0.0.0/24 hello 美國西部地區和 10.0.1.0/24。

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>步驟 4

指派的子網路變數 hello 接下來的步驟，以建立應用程式閘道。

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>建立 hello 前端組態的公用 IP 位址

建立公用 IP 資源**publicIP01**資源群組中**appgw rg** hello 美國西部地區。

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Hello 服務啟動時，會指派 toohello 應用程式閘道 IP 位址。

## <a name="create-application-gateway-configuration"></a>建立應用程式閘道組態

您必須 tooset 所有組態項目，才能建立 hello 應用程式閘道。 hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。

### <a name="step-1"></a>步驟 1

建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。 應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。 請記住，每個執行個體需要一個 IP 位址。

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>步驟 2

設定 hello 後端 IP 位址集區名稱為**pool01**和**pool2**與 IP 位址**134.170.185.46**， **134.170.188.221**，**134.170.185.50**如**pool1**和**134.170.186.46**， **134.170.189.221**， **134.170.186.50**如**pool2**。

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

在此範例中，有兩個後端集區 tooroute 網路流量 hello 要求站台。 其中一個集區會接收來自 "contoso.com" 站台的流量，而另一個集區則會接收來自 "fabrikam.com" 站台的流量。 您有上述您自己的應用程式的 IP 位址端點的 IP 位址 tooadd tooreplace hello。 您也可以使用公用 IP 位址、FQDN 或 VM 的後端執行個體 NIC 來取代內部 IP 位址。 在 PowerShell 使用的 Fqdn，而不是 Ip toospecify"-BackendFQDNs"參數。

### <a name="step-3"></a>步驟 3

設定應用程式閘道設定**poolsetting01**和**poolsetting02** hello hello 後端集區中，負載平衡網路流量。 在此範例中，您可以設定不同的後端集區設定 hello 後端集區。 每個後端集區都可以有它自己的後端集區設定。

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>步驟 4

設定公用 IP 端點 hello 前端 IP。

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>步驟 5

設定應用程式閘道 hello 前端連接埠。

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>步驟 6

設定兩個 SSL 憑證 hello 兩個網站，我們會在此範例中的 toosupport。 一個憑證是針對 contoso.com 流量，且其他 hello fabrikam.com 流量。 這些憑證應該是「憑證授權單位」為您的網站簽發的憑證。 也支援自我簽署憑證，但不建議用於生產環境流量。

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>步驟 7

在此範例中，設定兩個 web sites hello 的兩個接聽程式。 此步驟會設定 hello 接聽程式，公用 IP 位址、 連接埠及主機使用 tooreceive 連入流量。 HostName 參數是為了支援多個站台，而且應該設定 toohello 適當網站的 hello 接收流量。 時，RequireServerNameIndication 參數應設為 tootrue 的網站若需要 ssl 的支援，在多個主機的案例。 如果需要 SSL 支援，您也需要 toospecify hello SSL 憑證也就是該 web 應用程式使用的 toosecure 流量。 FrontendIPConfiguration FrontendPort 及主機名稱的 hello 組合必須是唯一 tooa 接聽程式。 每個接聽程式可以支援一個憑證。

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>步驟 8

建立兩個設定 hello 兩個 web 應用程式在此範例中的規則。 規則會將接聽程式、後端集區及 http 設定繫結在一起。 此步驟會設定 hello 應用程式閘道 toouse 基本路由規則，一個用於每個網站。 流量 tooeach 網站接收其設定的接聽程式，並接著會導向 tooits 設定後端集區，使用 hello hello BackendHttpSettings 中指定的屬性。

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>步驟 9

設定 hello 數量的執行個體和 hello 應用程式閘道的大小。

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>建立應用程式閘道

建立應用程式閘道與 hello 先前步驟中的所有組態物件。

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> 應用程式閘道的佈建是長時間執行的作業，而且可能需要一些時間 toocomplete。
> 
> 

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

深入了解如何 tooprotect 與網站[應用程式閘道的 Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)

