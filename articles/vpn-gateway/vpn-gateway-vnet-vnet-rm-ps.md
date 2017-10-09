---
title: "連接 Azure 虛擬網路 tooanother VNet: PowerShell |Microsoft 文件"
description: "本文將逐步引導您使用 Azure 資源管理員和 PowerShell，將虛擬網路連接在一起。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>使用 PowerShell 設定 VNet 對 VNet 的 VPN 閘道連線

本文章將示範如何 toocreate 虛擬網路之間的 VPN 閘道連線。 hello 虛擬網路可在 hello 相同或不同區域，並從 hello 相同或不同的訂用帳戶。 當連接的 Vnet，從不同的訂用帳戶，hello 訂用帳戶不需要與相關聯的 toobe hello 相同的 Active Directory 租用戶。 

這篇文章中的 hello 步驟套用 toohello Resource Manager 部署模型，並使用 PowerShell。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [連線不同的部署模型 - Azure 入口網站](vpn-gateway-connect-different-deployment-models-portal.md)
> * [連線不同的部署模型 - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting VNet tooan 在內部部署站台位置。 這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。 如果您的 Vnet hello 中相同的區域，您可能會想 tooconsider 它們使用對等互連的 VNet 連接。 VNet 對等互連不會使用 VPN 閘道。 如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。

您可以將 VNet 對 VNet 通訊與多站台組態結合。 這可讓您建立結合內部虛擬網路連線使用跨單位連線的網路拓樸 hello 下列圖表所示：

![關於連線](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>為什麼要連接虛擬網路？

您可以遵循原因 hello tooconnect 虛擬網路：

* **跨區域的異地備援和異地目前狀態**

  * 您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。
  * 您可以使用 Azure 流量管理員和負載平衡器，利用異地備援跨多個 Azure 區域設定高度可用的工作負載。 重要的一個例子是 tooset 設定 SQL Always On 與分配到多個 Azure 區域的可用性群組。
* **具有隔離或管理界限的區域性多層式應用程式**

  * 在 hello 相同區域中，您可以設定多層應用程式與多個虛擬網路連接在一起，因為 tooisolation 或系統管理需求。

如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。

## <a name="which-set-of-steps-should-i-use"></a>我應該使用哪個步驟集？

在本文中，您會看到兩組不同的步驟。 一組步驟[Vnet 中的 hello 相同訂用帳戶](#samesub)，而另一個用於[位於不同的訂用帳戶中的 Vnet](#difsub)。 hello hello 組之間的主要差異是您可以在建立及設定中的所有虛擬網路和閘道資源 hello 同一個 PowerShell 工作階段。

hello 本文章中的步驟使用會在每個區段的 hello 開頭宣告的變數。 如果您已經使用現有的 Vnet，修改 hello 變數 tooreflect hello 中設定您自己的環境。 如果您想要了解虛擬網路的名稱解析，請參閱[名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。

## <a name="samesub"></a>如何 tooconnect Vnet 處於 hello 相同訂用帳戶

![v2v 圖表](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>開始之前

在開始之前，您需要 tooinstall hello 最新版本的 hello Azure 資源管理員 PowerShell cmdlet，至少 4.0 或更新版本。 如需安裝 hello PowerShell cmdlet 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

### <a name="Step1"></a>步驟 1 - 規劃 IP 位址範圍

在 hello 下列步驟，我們會建立兩個虛擬網路，以及其個別的閘道子網路和設定。 我們再建立 hello 之間的 VPN 連線兩個 Vnet。 它是您的網路設定的重要 tooplan hello IP 位址範圍。 請記住，您必須先確定您的 VNet 範圍或區域網路範圍沒有以任何方式重疊。 在這些範例中，我們不會包含 DNS 伺服器。 如果您想要了解虛擬網路的名稱解析，請參閱[名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。

我們使用下列值 hello 範例中的 hello:

**TestVNet1 的值︰**

* VNet 名稱︰TestVNet1
* 資源群組︰TestRG1
* 位置：美國東部
* TestVNet1：10.11.0.0/16 和 10.12.0.0/16
* FrontEnd：10.11.0.0/24
* BackEnd：10.12.0.0/24
* GatewaySubnet：10.12.255.0/27
* GatewayName：VNet1GW
* 公用 IP: VNet1GWIP
* VPNType：RouteBased
* Connection(1to4)：VNet1toVNet4
* Connection(1to5)：VNet1toVNet5
* ConnectionType：VNet2VNet

**TestVNet4 的值︰**

* VNet 名稱︰TestVNet4
* TestVNet2：10.41.0.0/16 和 10.42.0.0/16
* FrontEnd：10.41.0.0/24
* BackEnd：10.42.0.0/24
* GatewaySubnet：10.42.255.0/27
* 資源群組：TestRG4
* 位置：美國西部
* GatewayName：VNet4GW
* 公用 IP：VNet4GWIP
* VPNType：RouteBased
* 連線︰VNet4toVNet1
* ConnectionType：VNet2VNet


### <a name="Step2"></a>步驟 2 - 建立及設定 TestVNet1

1. 宣告變數。 這個範例會宣告 hello 針對此練習使用 hello 值的變數。 在大部分情況下，您應該 hello 值取代您自己。 不過，您可以使用這些變數，如果您正在透過 hello 步驟 toobecome 熟悉這種類型的組態。 修改 hello 變數，如有需要然後複製並貼至 PowerShell 主控台。

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Tooyour 帳戶連接。 使用下列範例 toohelp 您連接的 hello:

  ```powershell
  Login-AzureRmAccount
  ```

  請檢查 hello hello 帳戶的訂用帳戶。

  ```powershell
  Get-AzureRmSubscription
  ```

  指定您想 toouse hello 訂用帳戶。

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. 建立新的資源群組。

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. 建立 hello TestVNet1 的子網路組態。 此範例會建立一個名為 TestVNet1 的虛擬網路和三個子網路：一個名為 GatewaySubnet、一個名為 FrontEnd，另一個名為 Backend。 替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。 如果您將其命名為其他名稱，閘道建立會失敗。

  hello 下列範例會使用您先前設定的 hello 變數。 在此範例中，使用 /27 hello 閘道子網路。 雖然可能 toocreate 閘道子網路為/29，我們建議您建立較大的子網路選取至少是/28 或 /27 包含多個位址。 這可讓足夠位址 tooaccommodate 可能其他組態，您可能想在 hello 未來。

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. 建立 TestVNet1。

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. 要求的公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。 請注意該 hello AllocationMethod 是動態。 您無法指定您想 toouse hello IP 位址。 它是動態配置的 tooyour 閘道。 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. 建立 hello 閘道設定。 hello 閘道組態會定義 hello 子網路和公用 IP 位址 toouse hello。 使用 hello 範例 toocreate 閘道設定。

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. 建立 TestVNet1 hello 閘道。 在此步驟中，您建立您 TestVNet1 hello 虛擬網路閘道。 VNet 對 VNet 組態需要 RouteBased VpnType。 建立閘道可以通常要花費 45 分鐘以上，視 hello 選取的閘道 SKU。

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>步驟 3 - 建立及設定 TestVNet4

設定 TestVNet1 後，請建立 TestVNet4。 請遵循下面取代您自己時所需 hello 值 hello 步驟。 此步驟即可 hello 內相同的 PowerShell 工作階段因為它處於 hello 相同訂用帳戶。

1. 宣告變數。 為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. 建立新的資源群組。

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. 建立 hello TestVNet4 的子網路組態。

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. 建立 TestVNet4。

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. 要求公用 IP 位址。

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. 建立 hello 閘道設定。

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. 建立 hello TestVNet4 閘道。 建立閘道可以通常要花費 45 分鐘以上，視 hello 選取的閘道 SKU。

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>步驟 4-建立 hello 連線

1. 取得這兩個虛擬網路閘道。 如果 hello 閘道 hello 中都相同的訂用帳戶，和它們在 hello 範例中，您可以完成此步驟在 hello 同一個 PowerShell 工作階段。

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. 建立 hello TestVNet1 tooTestVNet4 連線。 在此步驟中，您會從 TestVNet1 tooTestVNet4 建立 hello 連線。 您會看見 hello 範例中所參考的共用的金鑰。 您可以使用您自己的值為 hello 共用金鑰。 hello 很重要的是該 hello 共用的金鑰必須符合這兩個連接。 建立連接，可能會同時 toocomplete 短。

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. 建立 hello TestVNet4 tooTestVNet1 連線。 除了您要建立 hello 連線從 TestVNet4 tooTestVNet1 類似 toohello 一個以上版本，則此步驟。 請確定 hello 共用金鑰相符。 幾分鐘後，就會建立 hello 連線。

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. 確認您的連線。 請參閱 hello 節[如何 tooverify 連線](#verify)。

## <a name="difsub"></a>如何 tooconnect Vnet 位於不同的訂用帳戶

![v2v 圖表](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

在此案例中，我們會連接 TestVNet1 和 TestVNet5。 TestVNet1 和 TestVNet5 位於不同的訂用帳戶中。 hello 訂用帳戶不需要與 hello 相關聯的 toobe 相同的 Active Directory 租用戶。 這些步驟與 hello 先前設定的 hello 差異是部分 hello 組態步驟需要 toobe hello 第二個訂閱 hello 內容中的個別 PowerShell 工作階段中執行。 特別是當 hello 兩個訂用帳戶屬於 toodifferent 組織。

### <a name="step-5---create-and-configure-testvnet1"></a>步驟 5 - 建立及設定 TestVNet1

您必須先完成[步驟 1](#Step1)和[步驟 2](#Step2) hello 先前從區段 toocreate 並設定 TestVNet1 hello TestVNet1 VPN 閘道。 此組態中，您不需要的 toocreate TestVNet4 hello 前一節，雖然如果您建立它，它不會衝突進行這些步驟。 一旦您完成步驟 1 和步驟 2，繼續進行步驟 6 toocreate TestVNet5。 

### <a name="step-6---verify-hello-ip-address-ranges"></a>步驟 6-確認 hello IP 位址範圍

它是重要 toomake 確定 hello 新的虛擬網路，TestVNet5，hello IP 位址空間不與任何 VNet 範圍或區域網路閘道的範圍重疊。 在此範例中，hello 虛擬網路可能屬於 toodifferent 組織。 針對此練習，您可以使用下列值 hello TestVNet5 hello:

**TestVNet5 的值︰**

* VNet 名稱︰TestVNet5
* 資源群組：TestRG5
* 位置：日本東部
* TestVNet5：10.51.0.0/16 和 10.52.0.0/16
* FrontEnd：10.51.0.0/24
* BackEnd：10.52.0.0/24
* GatewaySubnet：10.52.255.0.0/27
* GatewayName：VNet5GW
* 公用 IP：VNet5GWIP
* VPNType：RouteBased
* 連線︰VNet5toVNet1
* ConnectionType：VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>步驟 7 - 建立及設定 TestVNet5

Hello hello 新訂用帳戶內容中，必須完成此步驟。 此組件可能會由擁有 hello 訂用帳戶的另一個組織中的 hello 系統管理員執行。

1. 宣告變數。 為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. 連接 toosubscription 5。 開啟 PowerShell 主控台並連接 tooyour 帳戶。 使用下列範例 toohelp 您連接的 hello:

  ```powershell
  Login-AzureRmAccount
  ```

  請檢查 hello hello 帳戶的訂用帳戶。

  ```powershell
  Get-AzureRmSubscription
  ```

  指定您想 toouse hello 訂用帳戶。

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. 建立新的資源群組。

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. 建立 hello TestVNet5 的子網路組態。

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. 建立 TestVNet5。

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. 要求公用 IP 位址。

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. 建立 hello 閘道設定。

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. 建立 hello TestVNet5 閘道。

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>步驟 8-建立 hello 連線

在此範例中，因為 hello 閘道在 hello 不同訂用帳戶，我們已分割此步驟中兩個 PowerShell 工作階段標示為 [訂用帳戶 1] 和 [訂用帳戶 5]。

1. **[訂用帳戶 1]**訂用帳戶 1 的 get hello 虛擬網路閘道。 登入，然後再執行下列範例中的 hello 連接 tooSubscription 1:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  複製下列項目 hello hello 輸出，並傳送訂用帳戶 5 這些 toohello 系統管理員，透過電子郵件或其他方法。

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  這兩個元素會有值類似 toohello 下列範例輸出：

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[訂用帳戶 5]**訂用帳戶 5 get hello 虛擬網路閘道。 登入，然後再執行下列範例中的 hello 連接 tooSubscription 5:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  複製下列項目 hello hello 輸出，並傳送訂用帳戶 1 這些 toohello 系統管理員，透過電子郵件或其他方法。

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  這兩個元素會有值類似 toohello 下列範例輸出：

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[訂用帳戶 1]**建立 hello TestVNet1 tooTestVNet5 連線。 在此步驟中，您會從 TestVNet1 tooTestVNet5 建立 hello 連線。 這裡的 hello 差異是因為它是不同的訂用帳戶中的 $vnet5gw 也無法直接取得。 您將需要 toocreate 新的 PowerShell 物件的 hello hello 前面步驟中，用以表示從訂用帳戶 1 的值。 使用下列的 hello 範例。 取代您自己的值為 hello 名稱、 識別碼和共用的金鑰。 hello 很重要的是該 hello 共用的金鑰必須符合這兩個連接。 建立連接，可能會同時 toocomplete 短。

  連接 tooSubscription 1，才能執行下列範例中的 hello:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[訂用帳戶 5]**建立 hello TestVNet5 tooTestVNet1 連線。 除了您要建立 hello 連線從 TestVNet5 tooTestVNet1 類似 toohello 一個以上版本，則此步驟。 建立根據 hello 值取自訂用帳戶 1 的 PowerShell 物件的相同程序也適用於此處也 hello。 在此步驟中，請確定 hello 共用索引鍵的符合。

  連接 tooSubscription 5，才能執行下列範例中的 hello:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>如何 tooverify 連接

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>VNet 對 VNet 常見問題集

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>後續步驟

* 一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 請參閱 hello[虛擬機器文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)如需詳細資訊。
* BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。
