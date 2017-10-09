---
title: "設定 S2S VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則：Azure Resource Manager：PowerShell | Microsoft Docs"
description: "本文將引導您使用 Azure Resource Manager 和 PowerShell，設定與 Azure VPN 閘道之 S2S 或 VNet 對 VNet 連線的 IPsec/IKE 原則。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>設定 S2S VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則

這篇文章會引導您 hello 步驟 tooconfigure 使用 hello Resource Manager 部署模型和 PowerShell 的站對站 VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則。

## <a name="about"></a>關於 Azure VPN 閘道的 IPsec 和 IKE 原則參數
IPsec 和 IKE 通訊協定標準支援各種不同的密碼編譯演算法的各種組合。 請參閱太[有關密碼編譯需求和 Azure VPN 閘道](vpn-gateway-about-compliance-crypto.md)toosee 這如何可協助確保跨單位和 VNet 對 VNet 連線能力滿足您的相容性或安全性需求。

這篇文章會提供指示 toocreate 和設定 IPsec/IKE 原則並套用 tooa 新的或現有的連接：

* [組件 1-工作流程 toocreate 而且設定 IPsec/IKE 原則](#workflow)
* [第 2 部分 - 支援的密碼編譯演算法和金鑰長度](#params)
* [第 3 部分 - 使用 IPsec/IKE 原則建立新的 S2S VPN 連線](#crossprem)
* [第 4 部分 - 使用 IPsec/IKE 原則建立新的 VNet 對 VNet 連線](#vnet2vnet)
* [第 5 部分 - 管理 (建立、新增、移除) 連線的 IPsec/IKE 原則](#managepolicy)

> [!IMPORTANT]
> 1. 請注意，IPsec/IKE 原則僅適用於下列閘道 Sku 的 hello:
>    * ***VpnGw1、VpnGw2、VpnGw3*** (路由式)
>    * ***Standard*** 和 ***HighPerformance*** (路由式)
> 2. 每個給定的連線只能指定***一個***原則組合。
> 3. 您必須同時對 IKE (主要模式) 和 IPsec (快速模式) 指定所有的演算法和參數。 系統不允許只指定一部分原則。
> 4. 請洽詢您 tooensure hello 原則在內部部署 VPN 裝置支援的 VPN 裝置廠商規格。 S2S 或 VNet 對 VNet 連線無法建立是否 hello 原則不相容。

## <a name ="workflow"></a>組件 1-工作流程 toocreate 而且設定 IPsec/IKE 原則
本節將概述 hello 工作流程 toocreate 和 update IPsec/IKE 原則 S2S VPN 或 VNet 對 VNet 連線：
1. 建立虛擬網路和 VPN 閘道
2. 建立區域網路閘道以進行跨單位連線，或建立另一個虛擬網路和閘道以進行 VNet 對 VNet 連線。
3. 使用選取的演算法和參數建立 IPsec/IKE 原則
4. 使用 hello IPsec/IKE 原則建立連線 （IPsec 或 VNet2VNet）
5. 新增/更新/移除現有連線的 IPsec/IKE 原則

這篇文章中的 hello 指示可協助您安裝及設定 IPsec/IKE 原則 hello 圖表所示：

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>第 2 部分 - 支援的密碼編譯演算法和金鑰長度

hello 下表列出支援的 hello 密碼編譯演算法和金鑰長度可設定 hello 客戶：

| **IPsec/IKEv2**  | **選項**    |
| ---  | --- 
| IKEv2 加密 | AES256、AES192、AES128、DES3、DES  
| IKEv2 完整性  | SHA384、SHA256、SHA1、MD5  |
| DH 群組         | DHGroup24、ECP384、ECP256、DHGroup14、DHGroup2048、DHGroup2、DHGroup1、無 |
| IPsec 加密 | GCMAES256、GCMAES192、GCMAES128、AES256、AES192、AES128、DES3、DES、無    |
| IPsec 完整性  | GCMASE256、GCMAES192、GCMAES128、SHA256、SHA1、MD5 |
| PFS 群組        | PFS24、ECP384、ECP256、PFS2048、PFS2、PFS1、無 
| QM SA 存留期   | (**選擇性**：如果未指定，即會使用預設值)<br>秒 (整數；**最小 300**/預設值 27000 秒)<br>KB 數 (整數；**最小 1024**/預設值 102400000 KB 數)   |
| 流量選取器 | UsePolicyBasedTrafficSelectors** ($True/$False；**選擇性**，如果未指定，即為預設的 $False)    |
|  |  |

> [!IMPORTANT]
> 1. **如果 GCMAES 會用於 IPsec 加密演算法，您必須選取 hello IPsec 完整性; 相同的 GCMAES 演算法和金鑰長度例如，兩個使用 GCMAES128**
> 2. IKEv2 主要模式 SA 存留期會固定為 28,800 秒 hello Azure VPN 閘道
> 3. 設定"UsePolicyBasedTrafficSelectors 」 太 $True 的連接上會設定 hello Azure VPN 閘道 tooconnect toopolicy 型 VPN 防火牆在內部部署。 如果您啟用 PolicyBasedTrafficSelectors，您需要的 tooensure VPN 裝置已定義從 hello Azure 虛擬網路的前置詞，您在內部部署網路 （區域網路閘道） 前置詞的所有組合的 hello 相符流量選取器而不是任何-到-any。 例如，如果您在內部部署網路的前置詞為 10.1.0.0/16 和 10.2.0.0/16，而且您虛擬網路的前置詞為 192.168.0.0/16 和 172.16.0.0/16，您需要下列流量選取器 toospecify hello:
>    * 10.1.0.0/16 <====> 192.168.0.0/16
>    * 10.1.0.0/16 <====> 172.16.0.0/16
>    * 10.2.0.0/16 <====> 192.168.0.0/16
>    * 10.2.0.0/16 <====> 172.16.0.0/16

如需原則式流量選取器的詳細資訊，請參閱[連線多個內部部署原則式 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)。

下表將列出 hello hello 對應 hello 自訂原則所支援的 Diffie-hellman 群組：

| **Diffie-Hellman 群組**  | **DHGroup**              | **PFSGroup** | **金鑰長度** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | 768 位元 MODP   |
| 2                         | DHGroup2                 | PFS2         | 1024 位元 MODP  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | 2048 位元 MODP  |
| 19                        | ECP256                   | ECP256       | 256 位元 ECP    |
| 20                        | ECP384                   | ECP284       | 384 位元 ECP    |
| 24                        | DHGroup24                | PFS24        | 2048 位元 MODP  |

請參閱太[RFC3526](https://tools.ietf.org/html/rfc3526)和[RFC5114](https://tools.ietf.org/html/rfc5114)如需詳細資訊。

## <a name ="crossprem"></a>第 3 部分 - 使用 IPsec/IKE 原則建立新的 S2S VPN 連線

本節將引導您完成建立 S2S VPN 連線的 IPsec/IKE 原則 hello 步驟。 hello 下列步驟建立 hello 連線 hello 圖表所示：

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

如需建立 S2S VPN 連線的詳細逐步指示，請參閱[建立 S2S VPN 連線](vpn-gateway-create-site-to-site-rm-powershell.md)。

### <a name="before"></a>開始之前

* 請確認您有 Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。
* 安裝 hello Azure 資源管理員 PowerShell cmdlet。 請參閱[Azure PowerShell 概觀](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。

### <a name="createvnet1"></a>步驟 1-建立 hello 虛擬網路、 VPN 閘道與區域網路閘道

#### <a name="1-declare-your-variables"></a>1.宣告變數

對於此練習，我們一開始先宣告我們的變數。 設定用於生產環境時，請以您自己是確定 tooreplace hello 值。

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2.連接 tooyour 訂用帳戶，並建立新的資源群組

請確定切換 tooPowerShell 模式 toouse hello 資源管理員 cmdlet。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。

開啟 PowerShell 主控台並連接 tooyour 帳戶。 使用下列範例 toohelp 您連接的 hello:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3.建立 hello 虛擬網路、 VPN 閘道與區域網路閘道

hello 下列範例會建立 hello 虛擬網路，TestVNet1，三個的子網路與 hello VPN 閘道。 替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。 如果您將其命名為其他名稱，閘道建立會失敗。

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="s2sconnection"></a>步驟 2 - 使用 IPsec/IKE 原則建立 S2S VPN 連線

#### <a name="1-create-an-ipsecike-policy"></a>1.建立 IPsec/IKE 原則

下列範例指令碼的 hello 建立 IPsec/IKE 原則以 hello 下列演算法和參數：

* IKEv2：AES256、SHA384、DHGroup24
* IPsec：AES256、SHA256、PFS24、SA 存留期 7200 秒和 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

如果您使用 GCMAES ipsec 時，您必須使用 hello 相同 GCMAES 演算法和金鑰長度 IPsec 加密和完整性，例如：

* IKEv2：AES256、SHA384、DHGroup24
* IPsec：**GCMAES256、GCMAES256**、PFS24、SA 存留期 7200 秒和 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2.建立 hello S2S VPN 連線以 hello IPsec/IKE 原則

建立 S2S VPN 連線並套用 hello 稍早建立的 IPsec/IKE 原則。

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

您可以選擇性地加入 「-UsePolicyBasedTrafficSelectors $True"toohello 連線 cmdlet tooenable Azure VPN 閘道 tooconnect toopolicy 型 VPN 裝置上建立內部部署，如上面所述。

> [!IMPORTANT]
> 之後 IPsec/IKE 原則指定的連接上，將只會傳送或接受 hello 與指定的密碼編譯演算法和金鑰長度，在該特定的連接上的 IPsec/IKE 建議 hello Azure VPN 閘道。 請確定在內部部署 VPN 裝置 hello 連接使用，或接受 hello 確切原則的組合，否則將不建立 hello S2S VPN 通道。


## <a name ="vnet2vnet"></a>第 4 部分 - 使用 IPsec/IKE 原則建立新的 VNet 對 VNet 連線

建立 VNet 對 VNet 連線的 IPsec/IKE 原則的 hello 步驟是類似 toothat S2S VPN 連線。 hello 下列範例指令碼建立 hello 連線 hello 圖表所示：

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

如需建立 VNet 對 VNet 連線的詳細步驟，請參閱[建立 VNet 對 VNet 連線](vpn-gateway-vnet-vnet-rm-ps.md)。 您必須先完成[3 篇](#crossprem)toocreate 並設定 TestVNet1 hello VPN 閘道。

### <a name="createvnet2"></a>步驟 1-建立 hello 第二個虛擬網路和 VPN 閘道

#### <a name="1-declare-your-variables"></a>1.宣告變數

為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2.在 hello 新資源群組中建立 hello 第二個虛擬網路和 VPN 閘道

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>步驟 2-建立 VNet toVNet 連接以 hello IPsec/IKE 原則

類似 toohello S2S VPN 連線，建立一個 IPsec/IKE 原則，然後套用 toopolicy toohello 新的連接。

#### <a name="1-create-an-ipsecike-policy"></a>1.建立 IPsec/IKE 原則

下列範例指令碼的 hello 建立不同的 IPsec/IKE 原則以 hello 下列演算法和參數：
* IKEv2：AES128、SHA1、DHGroup14
* IPsec：GCMAES128、GCMAES128、PFS14、SA 存留期 7200 秒和 4096KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2.建立 VNet 對 VNet 連線以 hello IPsec/IKE 原則

建立 VNet 對 VNet 連線並套用您所建立的 hello IPsec/IKE 原則。 在此範例中，兩個閘道位於 hello 相同訂用帳戶。 因此它可能 toocreate 而且設定與這兩個連線 hello hello 中相同的 IPsec/IKE 原則相同的 PowerShell 工作階段。

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> 之後 IPsec/IKE 原則指定的連接上，將只會傳送或接受 hello 與指定的密碼編譯演算法和金鑰長度，在該特定的連接上的 IPsec/IKE 建議 hello Azure VPN 閘道。 請確定 hello IPsec 原則的兩個連線都 hello 相同，否則將不建立 VNet 對 VNet 連線。

完成這些步驟之後，hello 連接在幾分鐘的時間，而且您必須遵循網路拓樸 hello 開頭中所示的 hello:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>第 5 部分 - 更新連線的 IPsec/IKE 原則

hello 最後一節將示範如何 toomanage 現有 S2S 或 VNet 對 VNet 連線的 IPsec/IKE 原則。 hello 練習下方會引導您完成下列作業的連接上的 hello:

1. 顯示連線的 hello IPsec/IKE 原則
2. 加入或更新 hello IPsec/IKE 原則 tooa 連線
3. 從連線移除 hello IPsec/IKE 原則

hello 相同的步驟套用 tooboth S2S 和 VNet 對 VNet 連線。

> [!IMPORTANT]
> 只有 Standard 和 HighPerformance 以路由為基礎的 VPN 閘道才支援 IPsec/IKE 原則。 它不適用於 hello 基本閘道 SKU 或 hello 以原則為基礎的 VPN 閘道。

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1.顯示連線的 hello IPsec/IKE 原則

hello 下列範例顯示如何 tooget hello 在連接上設定的 IPsec/IKE 原則。 hello 指令碼也會繼續從上述的 hello 練習。

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

如果有任何 hello 最後一個命令會列出 hello hello 連接上設定目前 IPsec/IKE 原則。 下列範例輸出的 hello 是 hello 連接：

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

如果未設定的 IPsec/IKE 原則，hello 命令 (PS > $connection6.policy) 取得傳回空白。 它並不表示 IPsec/IKE hello 連接上未設定，但沒有自訂 IPsec/IKE 原則。 hello 實際連接會使用您在內部部署 VPN 裝置和 hello Azure VPN 閘道之間進行交涉 hello 預設原則。

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2.新增或更新連線的 IPsec/IKE 原則

hello 步驟 tooadd 新原則或更新現有的連接上的原則是 hello 相同： 建立新的原則，然後套用新原則 toohello 連線 hello。

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

tooenable"UsePolicyBasedTrafficSelectors 」 時連接 tooan 內部以原則為基礎的 VPN 裝置，新增 hello"-UsePolicyBaseTrafficSelectors"參數 toohello cmdlet，或將其設定太 $False toodisable hello 選項：

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

您可以取得 hello 連線一次 toocheck 如果 hello 原則更新。

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

您應該會看到 hello hello 最後一行中，輸出 hello 下列範例所示：

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3.移除連線的 IPsec/IKE 原則

一旦您從連線移除 hello 自訂原則，hello Azure VPN 閘道會還原後 toohello [IPsec/IKE 提案徵求書的預設清單](vpn-gateway-about-vpn-devices.md)並再次重新交涉，與您的內部部署 VPN 裝置。

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

您可以使用 hello 相同的指令碼 toocheck 如果 hello 原則已經移除了 hello 連線。

## <a name="next-steps"></a>後續步驟

如需以原則為基礎的流量選取器的詳細資訊，請參閱[連線多個內部部署以原則為基礎的 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)。

一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。
