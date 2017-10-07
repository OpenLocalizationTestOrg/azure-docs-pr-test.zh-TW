---
title: "使用內部負載平衡器-PowerShell 的 Azure 應用程式閘道 aaaUsing |Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定、 啟動和刪除 Azure 資源管理員的 Azure 應用程式閘道與內部負載平衡器 (ILB)"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>使用 Azure 資源管理員建立搭配內部負載平衡器 (ILB) 的應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 傳統 PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

與網際網路對向的 VIP 或不公開的 toohello 網際網路，也稱為內部負載平衡 (ILB) 端點的內部端點，則可以設定 azure 應用程式閘道。 ILB 設定 hello 閘道可用於不公開的 toohello 網際網路的內部特定業務應用程式。 它也可用於服務和內的多層式應用程式層放在不是公開的 toohello 網際網路的安全性界限內，但仍需要循環配置資源負載散發 」、 「 神奇工作階段的結果或 「 安全通訊端層 (SSL) 終止。

這篇文章會引導您 hello 步驟 tooconfigure 應用程式閘道搭配 ILB 一起運作。

## <a name="before-you-begin"></a>開始之前

1. 使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。 您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。
2. 您會建立應用程式閘道的虛擬網路和子網路。 請確定沒有虛擬機器或雲端部署使用 hello 子網路。 應用程式閘道必須單獨在虛擬網路子網路中。
3. 您設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或指派建立 hello 虛擬網路中，或是具有公用 IP/VIP 端點。

## <a name="what-is-required-toocreate-an-application-gateway"></a>什麼是必要的 toocreate 應用程式閘道？

* **後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。 hello 列出的 IP 位址應該是屬於 toohello 虛擬網路但不同子網路都會為 hello 應用程式閘道或應該是公用 IP/VIP。
* **後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。 這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。
* **前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。 流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。
* **接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些是區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。
* **規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。 目前，只有 hello*基本*規則支援。 hello*基本*規則是循環配置資源負載分佈。

## <a name="create-an-application-gateway"></a>建立應用程式閘道

使用 Azure 傳統和 Azure 資源管理員的 hello 差別在於 hello 順序建立 hello 應用程式閘道，必須設定 toobe hello 項目。
使用資源管理員，讓應用程式閘道的所有項目個別設定，然後放置在一起 toocreate hello 應用程式閘道資源。

以下是需要的 toocreate 應用程式閘道的 hello 步驟：

1. 建立資源管理員的資源群組
2. 建立虛擬網路和 hello 應用程式閘道的子網路
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

建立新的資源群組 (若使用現有的資源群組，請略過此步驟)。

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

Azure Resource Manager 需要所有的資源群組指定一個位置。 這當做 hello 預設位置，該資源群組中的資源。 請確定應用程式閘道使用的所有命令 toocreate 都 hello 相同資源群組。

在上述範例中的 hello，我們會建立名為"appgw rg 」 和 「 位置 」 美國西部 」 的資源群組。

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>建立虛擬網路和 hello 應用程式閘道的子網路

下列範例會示範如何 hello toocreate 使用資源管理員的虛擬網路：

### <a name="step-1"></a>步驟 1

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

此步驟會指派 hello 位址範圍 10.0.0.0/24 tooa 子網路使用的變數 toobe toocreate 虛擬網路。

### <a name="step-2"></a>步驟 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

此步驟會建立名為"appgwvnet"的虛擬網路中資源群組 」 appgw-rg"hello 前置詞 10.0.0.0/16 使用子網路 10.0.0.0/24 hello 美國西部地區。

### <a name="step-3"></a>步驟 3

```powershell
$subnet = $vnet.subnets[0]
```

此步驟會將指派 hello 子網路物件 toovariable $subnet hello 接下來的步驟。

## <a name="create-an-application-gateway-configuration-object"></a>建立應用程式閘道組態物件

### <a name="step-1"></a>步驟 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

這個步驟會建立名為 "gatewayIP01" 的應用程式閘道 IP 組態。 應用程式閘道啟動時，它會挑選設定 hello 子網路的 IP 位址，並傳送 hello 後端 IP 集區中的網路流量 toohello IP 位址。 請記住，每個執行個體需要一個 IP 位址。

### <a name="step-2"></a>步驟 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

此步驟會設定 hello 後端 IP 位址集區名稱為"10.1.1.8、 10.1.1.9，10.1.1.10"，"pool01 」 ip 位址。 這些是 hello 收到 hello 來自 hello 前端 IP 端點的網路流量的 IP 位址。 取代先前的 IP 位址 tooadd hello 您自己的應用程式的 IP 位址端點。

### <a name="step-3"></a>步驟 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

此步驟會在 hello 後端集區中設定應用程式閘道設定 「 poolsetting01"hello 負載平衡網路流量。

### <a name="step-4"></a>步驟 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

此步驟會設定名為"frontendport01"hello ILB hello 前端 IP 連接埠。

### <a name="step-5"></a>步驟 5

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

這個步驟會建立 hello 稱為 「 fipconfig01"前端 IP 組態，並與私人 IP 從 hello 目前虛擬網路子網路產生關聯。

### <a name="step-6"></a>步驟 6

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

此步驟會建立稱為 「 listener01"hello 接聽程式，並將 hello 前端連接埠 toohello 前端 IP 組態。

### <a name="step-7"></a>步驟 7

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

此步驟建立 hello 負載平衡器路由規則稱為 「 rule01"，設定 hello 負載平衡器行為。

### <a name="step-8"></a>步驟 8

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

此步驟會設定 hello hello 應用程式閘道執行個體大小。

> [!NOTE]
> 預設值的 hello *InstanceCount*為 2，最大值是 10。 預設值的 hello *GatewaySize*都是 Medium。 您可以在 Standard_Small、Standard_Medium 和 Standard_Large 之間選擇。

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>使用 New-AzureApplicationGateway 建立應用程式閘道

建立應用程式閘道的 hello 先前步驟中的所有組態項目。 在此範例中，hello 應用程式閘道又稱為 「 appgwtest"。

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

此步驟會建立應用程式閘道的 hello 先前步驟中的所有組態項目。 在 hello 範例 hello 應用程式閘道又稱為 「 appgwtest"。

## <a name="delete-an-application-gateway"></a>刪除應用程式閘道

toodelete 應用程式閘道，您需要下列步驟順序 toodo hello:

1. 使用 hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello 閘道。
2. 使用 hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello 閘道。
3. 確認已移除該 hello 閘道使用 hello `Get-AzureApplicationGateway` cmdlet。

### <a name="step-1"></a>步驟 1

取得 hello 應用程式閘道物件，並將它 tooa 變數 」 $getgw"。

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>步驟 2

使用`Stop-AzureRmApplicationGateway`toostop hello 應用程式閘道。 這個範例會顯示 hello `Stop-AzureRmApplicationGateway` cmdlet hello 第一行，後面接著 hello 輸出。

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

處於停止狀態 hello 應用程式閘道之後，請使用 hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello 服務。

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> hello **-強制**參數可以是使用的 toosuppress hello 移除確認訊息。

已移除 hello 服務的 tooverify，您可以使用 hello `Get-AzureRmApplicationGateway` cmdlet。 這不是必要步驟。

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>後續步驟

如果您想的 tooconfigure SSL 卸載，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。

如果您想 tooconfigure 搭配 ILB 一起運作的應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。

如果您想進一步了解一般負載平衡選項，請參閱：

* [Azure 負載平衡器](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure 流量管理員](https://azure.microsoft.com/documentation/services/traffic-manager/)

