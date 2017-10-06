---
title: "aaaConfigure 結束 tooend Azure 應用程式閘道搭配 SSL |Microsoft 文件"
description: "本文說明如何 tooconfigure 結束 tooend SSL 搭配使用 Azure 資源管理員 PowerShell 的應用程式閘道"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>使用應用程式閘道使用 PowerShell 設定結束 tooend SSL

## <a name="overview"></a>概觀

應用程式閘道支援結束 tooend 加密的流量。 應用程式閘道會終止在 hello 應用程式閘道的 hello SSL 連線。 hello 閘道會接著套用 hello 路由規則 toohello 流量重新加密 hello 封包，並將轉送 hello 封包 toohello 適當的後端基礎 hello 路由定義的規則。 Hello web 伺服器的任何回應 hello 會經歷相同的處理序後 toohello 終端使用者。

應用程式閘道支援的另一項功能是定義自訂 SSL 選項。 應用程式閘道支援下列通訊協定版本。 停用 hello**TLSv1.0**， **TLSv1.1**，和**TLSv1.2**也定義 hello 的加密套件 toouse 和 hello 喜好設定順序。  toolearn 進一步了解可設定的 SSL 選項，請瀏覽[SSL 原則概觀](application-gateway-SSL-policy-overview.md)。

> [!NOTE]
> 預設會停用 SSL 2.0 和 SSL 3.0，並且無法啟用。 它們會被視為不安全，而且不能 toobe 搭配應用程式閘道。

![案例影像][scenario]

## <a name="scenario"></a>案例

在此案例中，您學習如何應用程式閘道使用 toocreate 結束 tooend SSL 使用 PowerShell。

此案例將會：

* 建立名為 **appgw-rg** 的資源群組
* 建立名為 **appgwvnet** 且具有 10.0.0.0/16 位址空間的虛擬網路。
* 建立名為 **appgwsubnet** 和 **appsubnet** 的兩個子網路。
* 建立小型應用程式閘道支援結束 tooend SSL 加密，該限制 SSL 通訊協定版本和加密套件。

## <a name="before-you-begin"></a>開始之前

tooconfigure 結束 tooend SSL 與應用程式閘道，憑證需要 hello 閘道，而憑證所需的 hello 後端伺服器。 hello 閘道憑證是使用的 tooencrypt 和解密 hello 傳送的流量 tooit 使用 SSL。 hello 閘道憑證需要 toobe 個人資訊交換 (pfx) 格式。 這種檔案格式允許 hello 私用金鑰 toobe 匯出所需的流量 hello 應用程式閘道 tooperform hello 加密和解密。

End tooend SSL 加密 hello 後端必須是與應用程式閘道的白名單。 這是上傳 hello 的 hello 範例 toohello 應用程式閘道的公用憑證。 這可確保該 hello 應用程式閘道只會與已知的後端執行個體通訊。 這可以進一步保護 hello 結束 tooend 通訊。

此程序所述步驟 hello:

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

本節將引導您完成建立資源群組、 包含 hello 應用程式閘道。

### <a name="step-1"></a>步驟 1

登入 tooyour Azure 帳戶。

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>步驟 2

選取此案例中的 hello 訂用帳戶 toouse。

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>步驟 3

建立資源群組 (若使用現有的資源群組，請略過此步驟)。

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>建立虛擬網路和 hello 應用程式閘道的子網路

hello 下列範例會建立虛擬網路和兩個子網路。 一個子網路是使用的 toohold hello 應用程式閘道。 hello 其他子網路用於 hello 後端裝載 hello web 應用程式。

### <a name="step-1"></a>步驟 1

指派 hello 子網路用於 hello 本身的應用程式閘道的位址範圍。

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> 應該適當地調整針對應用程式閘道所設定的子網路大小。 應用程式閘道可以針對設定 too10 執行個體。 每個執行個體接受來自 hello 子網路的一個 IP 位址。 子網路太小可能會對相應放大應用程式閘道產生負面影響。
> 
> 

### <a name="step-2"></a>步驟 2

指派用於 hello 後端位址集區位址範圍 toobe。

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>步驟 3

建立虛擬網路與 hello hello 先前步驟中所定義的子網路。

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>步驟 4

擷取 hello 虛擬網路資源和子網路資源 toobe 用於 hello 下列步驟：

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>建立 hello 前端組態的公用 IP 位址

建立用於 hello 應用程式閘道的公用 IP 資源 toobe。 此公用 IP 位址會用於下列步驟。

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> 應用程式閘道不支援公用 IP 位址，建立定義網域標籤 hello 的使用。 只支援具有動態建立之網域標籤的公用 IP 位址。 如果您需要 hello 應用程式閘道的好記的 dns 名稱，則建議 toouse CNAME 記錄做為別名。

## <a name="create-an-application-gateway-configuration-object"></a>建立應用程式閘道組態物件

建立 hello 應用程式閘道之前，會設定所有設定項目。 hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。

### <a name="step-1"></a>步驟 1

建立應用程式閘道 IP 設定，此設定會設定哪些子網路 hello 應用程式閘道會使用。 應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。 請記住，每個執行個體需要一個 IP 位址。

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>步驟 2

建立前端 IP 組態，此設定對應的私人或公用 ip 位址 toohello 前端的 hello 應用程式閘道。 下列步驟將 hello 公用 IP 位址在前面步驟中的使用 hello 前端 IP 組態的 hello hello。

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>步驟 3

Hello 的 hello 後端 web 伺服器的 IP 位址設定 hello 後端 IP 位址集區。 這些 IP 位址是接收來自 hello 前端 IP 端點的 hello 網路流量的 hello IP 位址。 取代下列 IP 位址 tooadd hello 您自己的應用程式的 IP 位址端點。

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> 完整的網域名稱 (FQDN) 是藉由使用 hello-BackendFqdns 參數也是有效的值來取代 hello 後端伺服器的 ip 位址。 

### <a name="step-4"></a>步驟 4

設定 hello 前端 IP 連接埠 hello 公用 IP 端點。 此連接埠是使用者連線到的 hello 連接埠。

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>步驟 5

設定 hello hello 應用程式閘道的憑證。 此憑證是使用的 toodecrypt 和重新加密 hello hello 應用程式閘道上的流量。

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> 這個範例會設定 SSL 連接所使用的 hello 憑證。 hello 憑證必須以.pfx 格式 toobe 和 hello 密碼必須介於 4 too12 個字元之間。

### <a name="step-6"></a>步驟 6

建立 hello 應用程式閘道的 hello HTTP 接聽程式。 Hello 前端 ip 組態、 連接埠，以及 SSL 憑證 toouse 指派。

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>步驟 7

上傳 hello toobe hello SSL 用於啟用後端集區資源的憑證。

> [!NOTE]
> hello 預設探查 hello 從取得 hello 公開金鑰**預設**在 hello 後端的 IP 位址及比較 hello 公開金鑰值收到 toohello 公開金鑰值您在此處提供的 SSL 繫結。 hello 擷取的公開金鑰不一定就是預期的 hello 網站 toowhich 流量**如果**hello 後端上使用主機標頭和 SNI。 不確定，請瀏覽 https://127.0.0.1/ 上使用的憑證 hello 的後端 tooconfirm**預設**SSL 繫結。 使用本節中的 hello 公開金鑰，從該要求。 如果您使用主機標頭和 SNI HTTPS 繫結上，而且您不會收到的回應和憑證手動瀏覽器要求 toohttps://127.0.0.1/ hello 的後端上，您必須設定 hello 的後端上的預設 SSL 繫結。 如果不這樣做，探查失敗，而且 hello 後端不在允許清單。

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> 在此步驟中所提供的 hello 憑證應 hello 公開金鑰的 hello pfx 憑證存在於 hello 後端上。 匯出 hello 憑證 （不 hello 根憑證） 中的 hello 後端伺服器上安裝。CER 格式，並將它用於此步驟。 這個步驟白名單 hello 與 hello 應用程式閘道後的端。

### <a name="step-8"></a>步驟 8

設定 hello 應用程式閘道後端 http 設定。 指派 hello hello 前面步驟 toohello http 設定中上傳的憑證。

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>步驟 9

建立負載平衡器路由規則，設定 hello 負載平衡器行為。 在此範例中，會建立基本的循環配置資源規則。

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>步驟 10

設定執行個體大小以 hello hello 應用程式閘道。  hello 可用大小是**標準\_小**，**標準\_媒體**，和**標準\_大**。  容量，hello 可用的值為 1 到 10。

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> 若要進行測試，可以選擇執行個體計數 1。 請務必 tooknow 任何執行個體計數在兩個執行個體未涵蓋 hello SLA，並因此不建議使用。 用於開發測試，不用於生產環境中使用的 toobe 都小型的閘道。

### <a name="step-11"></a>步驟 11

設定 hello SSL 原則 toobe hello 應用程式閘道上使用。 應用程式閘道支援 hello 能力 tooset 最小版本的 SSL 通訊協定版本。

hello 下列的值是一份可定義通訊協定版本。

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

設定 hello 最小的通訊協定版本太**TLSv1_2** ，並讓**TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**， **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**，和**TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**只。

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>建立 hello 應用程式閘道

使用所有 hello 先前步驟，建立 hello 應用程式閘道。 hello 建立 hello 閘道會是長時間執行的處理程序。

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>限制現有應用程式閘道上的 SSL 通訊協定版本

hello 上述步驟會帶您完成建立應用程式與結束 tooend SSL 和停用特定的 SSL 通訊協定版本。 hello 下列範例會停用現有的應用程式閘道特定 SSL 原則。

### <a name="step-1"></a>步驟 1

擷取 hello 應用程式閘道 tooupdate。

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>步驟 2

定義 SSL 原則。 在下列範例的 hello，TLSv1.0 TLSv1.1 會停用並 hello 加密套件**TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**， **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**，和**TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256**是 hello 允許唯一的。

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>步驟 3

最後，更新 hello 閘道。 這最後一個步驟是長時間執行工作的重要 toonote 它。 完成時，結束的 tooend hello 應用程式閘道設定 SSL。

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

深入了解 web 應用程式與 Web 應用程式防火牆透過應用程式閘道的 hello 安全性強化造訪[Web 應用程式防火牆概觀](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
