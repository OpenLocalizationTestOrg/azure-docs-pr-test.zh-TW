---
title: "應用程式閘道使用的 URL 路由規則的 aaaCreate |Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定 Azure 應用程式閘道使用的 URL 路由規則"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>使用路徑型路由建立應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

路徑為基礎的路由 URL 可讓您 tooassociate 路由根據 hello 的 Http 要求的 URL 路徑。 它會檢查是否有設定 hello 應用程式閘道中的 hello URL 路由 tooa 後端集區。 接著會傳送 hello 網路流量 toohello 定義後端集區。 URL 為基礎的路由的常見用法是不同的內容類型 toodifferent 後端伺服器集區的 tooload 平衡要求。

URL 為基礎的路由導入了新的規則類型 tooapplication 閘道。 應用程式閘道具有 2 種規則類型：基本和 PathBasedRouting。 基本規則類型提供循環配置資源服務的 hello 後端集區時 PathBasedRouting 此外 tooround 循環配置資源發佈，也會考量 hello 要求 URL 的路徑模式並選擇 hello 後端集區。

## <a name="scenario"></a>案例

在下列範例的 hello，應用程式閘道為 contoso.com 的流量提供兩個後端伺服器集區： 視訊的伺服器集區及影像伺服器集區。

要求 http://contoso.com/image * 會路由傳送 tooimage 伺服器集區 (pool1)，及 http://contoso.com/video * 會路由傳送 toovideo 伺服器集區 (pool2)。 如果沒有 hello 路徑模式符合，會選取預設的伺服器集區 (pool1)。

![URL 路由](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>開始之前

1. 使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。 您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。
2. 您會建立應用程式閘道的虛擬網路和子網路。 請確定沒有虛擬機器或雲端部署使用 hello 子網路。 hello 應用程式閘道必須單獨在虛擬網路子網路。
3. hello 伺服器加入 toohello 後端集區 toouse hello 應用程式閘道必須存在，或其端點建立 hello 虛擬網路中或與公用 IP/VIP 指派。

## <a name="what-is-required-toocreate-an-application-gateway"></a>什麼是必要的 toocreate 應用程式閘道？

* **後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。 列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。
* **後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。 流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。
* **規則：** hello 規則繫結 hello 接聽程式，hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。

## <a name="create-an-application-gateway"></a>建立應用程式閘道

使用 Azure 傳統和 Azure 資源管理員的 hello 差別在於 hello 順序建立 hello 應用程式閘道，必須設定 toobe hello 項目。

使用資源管理員，讓應用程式閘道的所有項目個別設定，然後放置在一起 toocreate hello 應用程式閘道資源。

以下是需要的 toocreate 應用程式閘道的 hello 步驟：

1. 建立資源管理員的資源群組。
2. 建立虛擬網路、 子網路和 hello 應用程式閘道的公用 IP。
3. 建立應用程式閘道組態物件。
4. 建立應用程式閘道資源。

## <a name="create-a-resource-group-for-resource-manager"></a>建立資源管理員的資源群組

請確定您使用 Azure PowerShell hello 最新版本。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。

### <a name="step-1"></a>步驟 1

登入 tooAzure

```powershell
Login-AzureRmAccount
```

您必須提示的 tooauthenticate 和您的認證。<BR>

### <a name="step-2"></a>步驟 2

請檢查 hello hello 帳戶的訂用帳戶。

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>步驟 3

選擇 Azure 訂用帳戶 toouse。 <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>步驟 4

建立資源群組 (若使用現有的資源群組，請略過此步驟)。

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

或者，您也可以針對應用程式閘道建立資源群組的標記：

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

Azure Resource Manager 需要所有的資源群組指定一個位置。 此資源群組用做 hello 預設位置，該資源群組中的資源。 請確定所有命令 toocreate 應用程式閘道使用 hello 相同的資源群組。

在 hello 上述範例中，我們會建立資源群組，稱為 「 appgw RG 」 和 「 美國西部 」 的位置。

> [!NOTE]
> 如果您需要 tooconfigure 自訂探查您應用程式閘道，請參閱[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-ps.md)。 請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>建立虛擬網路和 hello 應用程式閘道的子網路

下列範例會示範如何 hello toocreate 使用資源管理員的虛擬網路。 這個範例會建立 hello 應用程式閘道的 VNET。 應用程式閘道需要它自己的子網路，因此 hello 子網路建立的應用程式閘道 hello 小於 hello VNET 位址空間。 這可讓其他資源，包括但不是限於的 tooweb 伺服器 toobe 設定 hello 中相同的 VNET。

### <a name="step-1"></a>步驟 1

指派 hello 位址範圍 10.0.0.0/24 toohello 子網路使用的變數 toobe toocreate 虛擬網路。  這會建立 hello hello hello 下一個範例中使用的應用程式閘道的子網路設定物件。

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>步驟 2

建立虛擬網路，名為**appgwvnet**資源群組中**appgw rg** hello 前置詞 10.0.0.0/16 使用子網路 10.0.0.0/24 hello 美國西部地區。 如此即完成 hello hello VNET 與 hello 應用程式閘道 tooreside 的單一子網路設定。

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>步驟 3

將 hello 子網路變數指派下一個步驟，這會傳遞 toohello`New-AzureRMApplicationGateway`指令程式在後續步驟。

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>建立 hello 前端組態的公用 IP 位址

建立公用 IP 資源**publicIP01**資源群組中**appgw rg** hello 美國西部地區。 應用程式閘道可以使用的公用 IP 位址、 內部 IP 位址或兩個 tooreceive 要求進行負載平衡。  此範例中僅使用公用 IP 位址。 在下列範例的 hello，沒有 DNS 名稱已針對建立 hello 公用 IP 位址。  應用程式閘道在不支援公用 IP 位址上自訂 DNS 名稱。  如果需要 hello 公用端點的自訂名稱，CNAME 記錄應建立 hello 公用 IP 位址的 toopoint toohello 自動產生 DNS 名稱。

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Hello 服務啟動時，會指派 toohello 應用程式閘道 IP 位址。

## <a name="create-application-gateway-configuration"></a>建立應用程式閘道組態

所有設定項目必須都設定才能建立 hello 應用程式閘道。 hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。

### <a name="step-1"></a>步驟 1

建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。 應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。 請記住，每個執行個體需要一個 IP 位址。

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>步驟 2

設定 hello 後端 IP 位址集區名稱為**pool01**和**pool2** IP 位址與**pool1**和**pool2**。 這些 IP 位址是裝載 hello hello 應用程式閘道所保護的 web 應用程式 toobe hello 資源 hello IP 位址。 這些後端集區成員是所有驗證的 toobe 良好探查，無論是基本的探查 」 或 「 自訂探查。  接著路由傳送流量 toothem 當要求進入 hello 應用程式閘道。 後端集區可供多個規則內 hello 應用程式閘道，這表示一個後端集區無法用於相同位於 hello 的多個 web 應用程式主機。

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

在此範例中，有兩個後端集區 tooroute 網路流量 hello URL 路徑。 有一個集區會接收來自 URL 路徑 "/video" 的流量，而另一個集區會接收來自路徑 "/image" 的流量。 取代先前您自己的應用程式的 IP 位址端點的 IP 位址 tooadd hello。 

### <a name="step-3"></a>步驟 3

設定應用程式閘道設定**poolsetting01**和**poolsetting02** hello hello 後端集區中，負載平衡網路流量。 在此範例中，您可以設定不同的後端集區設定 hello 後端集區。 每個後端集區都可以有它自己的後端集區設定。  後端 HTTP 設定使用規則 tooroute 流量 toohello 正確的後端集區成員。 這會決定 hello 通訊協定和連接埠傳送流量 toohello 後端集區成員時所使用。 Cookie 架構工作階段，也取決於 hello 後端 HTTP 設定。  Cookie 架構工作階段相似性啟用時，會傳送流量 toohello 相同的後端，為每個封包的先前要求。

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>步驟 4

設定公用 IP 端點 hello 前端 IP。 hello 前端 IP 組態物件會使用接聽程式 toorelate hello 向外面對 hello 接聽程式 IP 位址。

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>步驟 5

設定應用程式閘道 hello 前端連接埠。 hello 前端連接埠組態物件會使用接聽程式 toodefine 哪些連接埠 hello 應用程式閘道接聽 hello 接聽程式上的流量。

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>步驟 6

Hello 接聽程式設定。 此步驟會設定 hello hello 公用 IP 位址的接聽程式，以及使用 tooreceive 連入網路流量的連接埠。 hello 下列範例會使用前端 IP 組態之前設定的 hello、 前端連接埠組態和通訊協定 （http 或 https），並設定 hello 接聽程式。 在此範例中，hello 接聽 tooHTTP hello 公用 IP 位址上稍早建立的連接埠 80 上的流量。

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>步驟 7

設定 URL 規則路徑 hello 後端集區。 這個步驟會設定應用程式閘道所使用的 hello 相對路徑，並定義 hello hello URL 路徑與指派 toohandle hello 連入流量的 hello 後端集區之間的對應。

> [!IMPORTANT]
> 每個路徑開頭必須 / 和 hello 唯一地方"\*」 允許，則在 hello 結束。 有效範例包括 /xyz、/xyz* 或 /xyz/*。 hello fed toohello 路徑比對器的字串不包含任何文字 hello 之後第一次"？"或"#"，且這些字元不得使用。 

hello 下列範例會建立兩個規則： 一個用於 「 / 影像 /"路徑路由流量 tooback 端"pool1"和另一種用於 「 / 視訊 /"路徑路由流量 tooback 端"pool2。 」 這些規則可確保每一組 url 的流量會路由的 toohello 後端。 例如，http://contoso.com/image/figure1.jpg 進入 toopool1 到 http://contoso.com/video/example.mp4 進入 toopool2。

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

如果 hello 路徑不符合任何 hello 預先定義的路徑規則，hello 規則路徑對應設定也會設定預設的後端位址集區。 比方說，http://contoso.com/shoppingcart/test.html 會 toopool1，因為它定義為 hello 預設集區不相符的流量。

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>步驟 8

建立規則設定。 此步驟會設定 hello 應用程式閘道 toouse URL 路徑為基礎的路由。 hello`$urlPathMap`變數定義在 hello 先前的步驟是現在使用的 toocreate hello 路徑為基礎的規則。 在此步驟中，我們建立 hello 規則關聯的接聽程式與 hello 稍早建立的 url 路徑對應。

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>步驟 9

設定 hello 數量的執行個體和 hello 應用程式閘道的大小。

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>建立應用程式閘道

建立應用程式閘道與 hello 先前步驟中的所有組態物件。

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>取得應用程式閘道 DNS 名稱

一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。 當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。 tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。 [在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。 tooconfigure hello 前端 IP CNAME 記錄，擷取 hello 應用程式閘道和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的詳細資料。 hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄。 不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。

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

如果您想的 toolearn Secure Sockets Layer (SSL) 卸載時，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl-arm.md)。

