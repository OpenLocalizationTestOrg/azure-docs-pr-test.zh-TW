---
title: "aaaHow toouse 與應用程式閘道的虛擬網路中的 Azure API 管理 |Microsoft 文件"
description: "深入了解如何 toosetup 和內部虛擬網路與應用程式閘道 (WAF) 做為前端中設定 Azure API 管理"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>整合內部 VNET 中的 API 管理與應用程式閘道 

##<a name="overview"></a>概觀
 
hello API 管理服務可以在內部的模式，使其只能從 hello 虛擬網路中存取的虛擬網路設定。 Azure 應用程式閘道是一項 PAAS 服務，可提供第 7 層負載平衡器。 它可做為反向 Proxy 服務，並在其供應項目中提供 Web 應用程式防火牆 (WAF)。

結合使用 hello 應用程式閘道前端內部 VNET 中佈建 API 管理可讓 hello 下列案例：

* 使用 hello 相同取用者內部和外部的取用者耗用量的 API 管理資源。
* 使用單一 API 管理資源，並在 API 管理中定義一部分 API 供外部取用者使用。
* 提供周全的方式 tooswitch 存取 tooAPI 管理 hello 從公用網際網路開啟和關閉。 

##<a name="scenario"></a>案例
這份文件將涵蓋如何 toouse 單一的 API 管理服務的內部和外部的取用者，並將其做為單一前端的兩個內部部署和雲端應用程式開發介面。 您也會看到如何 tooexpose 您的應用程式開發介面 （在其以綠色反白顯示 hello 範例） 的子集供外部使用使用中應用程式閘道所提供的 hello PathBasedRouting 功能。

Hello 第一個安裝程式範例中是只能從虛擬網路中管理您的 Api。 內部取用者 (以橘色醒目提示) 則可存取所有的內部和外部 API。 流量不會傳遞高效能的 tooInternet 透過 Express Route 電路。

![URL 路由](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"></a>開始之前

1. 使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。 您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。
2. 建立虛擬網路，並為 API 管理和應用程式閘道建立個別子網路。 
3. 如果您想 toocreate hello 虛擬網路的自訂 DNS 伺服器，請啟動 hello 部署前。 檢查它的運作方式是確保在 hello 虛擬網路中的新子網路中建立的虛擬機器可以解析和存取所有 Azure 服務端點。

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>需要的 toocreate API 管理和應用程式閘道之間的整合為何？

* **後端伺服器集區：**這是 hello 內部虛擬 IP 位址的 hello API 管理服務。
* **後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**這是 hello 應用程式閘道開啟 hello 公用連接埠。 叫用它的流量取得重新導向的 tooone hello 的後端伺服器。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。
* **規則：** hello 規則繫結的接聽程式 tooa 後端伺服器集區。
* **自訂的健全狀況探查：**應用程式閘道，根據預設，使用 IP 位址的探查 toofigure out hello 在哪些伺服器 BackendAddressPool 在使用中。 hello API 管理服務只會回應 toorequests 具有 hello 正確的主機標頭，因此 hello 預設探查失敗。 自訂的健全狀況探查需要定義 toobe toohelp 應用程式閘道判斷出 hello 服務正在執行，而且應該將要求轉送。
* **自訂網域的憑證：** tooaccess API 管理從 hello 網際網路需要 toocreate 其主機名稱 toohello 應用程式閘道前端 DNS 名稱的 CNAME 對應。 這可確保 hello 主機名稱標頭和傳送憑證 tooApplication tooAPI 轉送閘道管理一個 APIM 可辨識為有效。

## <a name="overview-steps"></a>整合 API 管理和應用程式閘道的所需步驟 

1. 建立資源管理員的資源群組。
2. 建立虛擬網路、 子網路和 hello 應用程式閘道的公用 IP。 為 API 管理建立其他子網路。
3. 建立 API 管理服務，在上面所建立的 hello VNET 子網路內，並確定您使用 hello 內部的模式。
4. 安裝程式在 hello API 管理服務中的 hello 自訂網域名稱。
5. 建立應用程式閘道組態物件。
6. 建立應用程式閘道資源。
7. 建立 CNAME，從 hello 公開 DNS 名稱的 hello 應用程式閘道 toohello API 管理 proxy 主機名稱。

## <a name="create-a-resource-group-for-resource-manager"></a>建立資源管理員的資源群組

請確定您使用 Azure PowerShell hello 最新版本。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。

### <a name="step-1"></a>步驟 1

登入 tooAzure

```powershell
Login-AzureRmAccount
```

使用您的認證進行驗證。<BR>

### <a name="step-2"></a>步驟 2

檢查 hello 訂閱 hello 帳戶，並加以選取。

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>步驟 3

建立資源群組 (若使用現有的資源群組，請略過此步驟)。

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Azure Resource Manager 需要所有的資源群組指定一個位置。 這當做 hello 預設位置，該資源群組中的資源。 請確定所有命令 toocreate 應用程式閘道使用 hello 相同的資源群組。

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>建立虛擬網路和 hello 應用程式閘道的子網路

hello 下列範例示範如何使用虛擬網路的 toocreate hello 資源管理員。

### <a name="step-1"></a>步驟 1

指派 hello 位址範圍 10.0.0.0/24 toohello 子網路變數 toobe 建立虛擬網路時使用應用程式閘道。

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>步驟 2

指派 hello 位址範圍 10.0.1.0/24 toohello 子網路變數 toobe 建立虛擬網路時使用的 API 管理。

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>步驟 3

建立虛擬網路，名為**appgwvnet**資源群組中**apim-appGw-RG**使用 hello 前置詞 10.0.0.0/16 hello 美國西部地區與子網路 10.0.0.0/24 10.0.1.0/24。

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>步驟 4

指派子網路變數 hello 接下來的步驟

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>在以內部模式設定的 VNET 內建立 API 管理服務

hello 下列範例顯示如何 toocreate 在 VNET 中的 API 管理服務設定為僅限內部存取。

### <a name="step-1"></a>步驟 1
建立使用 hello 子網路 $apimsubnetdata 上面所建立的應用程式開發介面管理虛擬網路物件。

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>步驟 2
建立 API 管理服務，hello 虛擬網路內。

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
上述命令 hello 成功之後，請參閱太[需要 tooaccess 內部 VNET API 管理服務的 DNS 設定](api-management-using-with-internal-vnet.md#apim-dns-configuration)tooaccess 它。

## <a name="set-up-a-custom-domain-name-in-api-management"></a>在 API 管理中設定自訂網域名稱

### <a name="step-1"></a>步驟 1
Hello 憑證上傳具有私密金鑰的 hello 網域。 這個範例中就會是 `*.contoso.net`。 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>步驟 2
Hello 憑證上傳，一旦建立 hello proxy 主機名稱設定物件的主機名稱與`api.contoso.net`，如 hello 範例憑證授權單位提供 hello`*.contoso.net`網域。 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>建立 hello 前端組態的公用 IP 位址

建立公用 IP 資源**publicIP01**資源群組中**apim-appGw-RG** hello 美國西部地區。

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Hello 服務啟動時，會指派 toohello 應用程式閘道 IP 位址。

## <a name="create-application-gateway-configuration"></a>建立應用程式閘道組態

所有設定項目必須都設定才能建立 hello 應用程式閘道。 hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。

### <a name="step-1"></a>步驟 1

建立名為 **gatewayIP01** 的應用程式閘道 IP 組態。 應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。 請記住，每個執行個體需要一個 IP 位址。

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>步驟 2

設定 hello 前端 IP 連接埠 hello 公用 IP 端點。 此連接埠是使用者連線到的 hello 連接埠。

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>步驟 3

設定公用 IP 端點 hello 前端 IP。

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>步驟 4

設定 hello 憑證 hello 應用程式閘道使用 toodecrypt 和重新加密 hello 流量通過。

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>步驟 5

建立 hello 應用程式閘道的 hello HTTP 接聽程式。 Hello 前端 IP 組態、 連接埠，以及 ssl 憑證 tooit 指派。

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>步驟 6

建立 API 管理服務的自訂探查 toohello `ContosoApi` proxy 網域端點。 hello 路徑`/status-0123456789abcdef`預設健全狀況的端點上所有的 hello API 管理服務裝載。 設定`api.contoso.net`自訂探查主機名稱 toosecure 為使用 SSL 憑證。

> [!NOTE]
> hello hostname `contosoapi.azure-api.net` hello 預設 proxy 主機名稱設定名為的服務時`contosoapi`公用 Azure 中建立。 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>步驟 7

上傳 hello toobe 用於 hello 啟用 SSL 的後端集區的資源上的憑證。 這是 hello 同一個憑證，您在上述步驟 4 中提供。

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>步驟 8

設定 HTTP hello 應用程式閘道後端設定。 這包括設定之後會取消的後端要求逾時限制。 此值與不同 hello 探查的逾時。

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>步驟 9

設定名為後端 IP 位址集區**apimbackend**上面建立 hello 內部的虛擬 ip 位址的 hello API 管理服務。

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>步驟 10

建立虛擬 (不存在) 後端的設定。 我們不想要從應用程式閘道透過 API 管理 tooexpose 要求 tooAPI 路徑將會叫用這個後端，並傳回 404。

設定 hello dummy 後端 HTTP 設定。

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

設定空的後端**dummyBackendPool**，哪些點 tooa FQDN 位址**dummybackend.com**。這個 FQDN 的地址不存在於 hello 虛擬網路中。

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

建立規則，設定預設指向 toohello 不存在後端應用程式閘道會使用該 hello **dummybackend.com** hello 虛擬網路中。

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>步驟 11

設定 URL 規則路徑 hello 後端集區。 這可讓某些 hello 從 API 管理 Api 所公開 toohello 公用只選取。 例如，如果有 `Echo API` (/echo/)、`Calculator API` (/calc/) 等，則讓 `Echo API` 只能從網際網路存取。 

hello 下列範例會建立一個簡單的規則，為 「 hello 」 / 「 回應 /"路徑路由流量 toohello 後端 」 apimProxyBackendPool"。

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

如果不符合 hello 路徑 hello 路徑規則，我們想要從 API 管理，hello 規則路徑對應組態也會設定名為的後端位址集區預設 tooenable **dummyBackendPool**。 例如，http://api.contoso.net/calc/ * 會太**dummyBackendPool**定義為 hello 預設集區不相符的流量。

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

hello 上面步驟可確保，只會要求 hello 路徑"/ 回應 」 可通過 hello 應用程式閘道。 要求 tooother API 管理中設定的應用程式開發介面會從應用程式閘道從 hello 網際網路存取時擲回 404 錯誤。 

### <a name="step-12"></a>步驟 12

建立 hello 應用程式閘道 toouse URL 路徑為基礎的路由規則設定。

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>步驟 13

設定 hello 數量的執行個體和 hello 應用程式閘道的大小。 這裡我們使用 hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md)以 hello API 管理資源的提高安全性。

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>步驟 14

「 防止 」 模式中設定 WAF toobe。
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>建立應用程式閘道

建立應用程式閘道與 hello 先前步驟中的所有 hello 組態物件。

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME hello API 管理 proxy 主機名稱 toohello 公開 DNS 名稱的 hello 應用程式閘道資源

一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。 當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱，這可能不是容易 toouse。 

hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄指向 hello APIM proxy 主機名稱 (例如`api.contoso.net`hello 上述範例中) toothis DNS 名稱。 tooconfigure hello 前端 IP CNAME 記錄，擷取 hello 應用程式閘道的 hello 詳細資料和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目。 因為 hello VIP 可能會變更在重新啟動閘道，不建議 hello 使用 A 記錄。

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"></a>摘要
在 VNET 中設定的 azure API 管理提供單一閘道介面設定的所有 Api，它們是裝載在內部部署還是在 hello 雲端。 使用 API 管理中整合應用程式閘道提供 hello 彈性，選擇性地啟用特定應用程式開發介面 toobe hello 網際網路上進行存取，以及提供 Web 應用程式防火牆做為前端 tooyour API 管理執行個體。

##<a name="next-steps"></a>後續步驟
* 深入了解 Azure 應用程式閘道
  * [應用程式閘道概觀](../application-gateway/application-gateway-introduction.md)
  * [應用程式閘道 Web 應用程式防火牆](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [使用路徑型路由的應用程式閘道](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* 深入了解 API 管理和 VNET
  * [使用 API 管理只能在 hello VNET](api-management-using-with-internal-vnet.md)
  * [在 VNET 中使用 API 管理](api-management-using-with-vnet.md)
