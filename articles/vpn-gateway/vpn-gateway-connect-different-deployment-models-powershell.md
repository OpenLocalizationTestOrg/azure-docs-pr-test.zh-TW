---
title: "連接傳統虛擬網路 tooAzure 資源管理員 Vnet: PowerShell |Microsoft 文件"
description: "深入了解如何 toocreate 傳統 Vnet 和資源管理員使用 VPN 閘道和 PowerShell 的 Vnet 之間的 VPN 連線"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>使用 PowerShell 從不同的部署模型連接虛擬網路



本文章將示範如何 tooconnect 傳統 Vnet tooResource 管理員 Vnet tooallow hello 位於彼此的 hello 不同的部署模型 toocommunicate 中的資源。 這篇文章中的 hello 步驟使用 PowerShell，但您也可以建立這個 hello Azure 入口網站使用此清單中選取 hello 發行項的組態。

> [!div class="op_single_selector"]
> * [入口網站](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

連接傳統的 VNet tooa 資源管理員 VNet 是類似 tooconnecting VNet tooan 在內部部署站台位置。 這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。 您可以在不同訂用帳戶和不同區域中的 VNet 之間建立連線。 只要 hello 閘道設定使用動態或路由為基礎，您也可以連接到已連線 tooon 內部部署網路的 Vnet。 如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。 

如果您的 Vnet 中 hello 相同區域中，您可能會想 tooinstead 考慮它們使用對等互連的 VNet 連接。 VNet 對等互連不會使用 VPN 閘道。 如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。 

## <a name="before-beginning"></a>開始之前

hello 下列步驟引導您完成 hello 設定必要 tooconfigure 動態或路由型閘道的每個 VNet 和建立 hello 閘道之間的 VPN 連線。 此組態不支援靜態或路由式閘道。

### <a name="prerequisites"></a>必要條件

* 已建立兩個 Vnet。
* hello 的位址範圍 hello Vnet 不彼此重疊或重疊的任何 hello hello 閘道可能連接到其他連接的範圍。
* 您已安裝 hello 最新版的 PowerShell cmdlet。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需詳細資訊。 請確定您安裝服務管理 (SM) hello 和 hello 資源管理員 (RM) cmdlet。 

### <a name="exampleref"></a>設定範例

您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。

**傳統 VNet 設定**

VNet 名稱 = ClassicVNet  <br>
位置 = West US <br>
虛擬網路位址空間 = 10.0.0.0/24 <br>
子網路 1 = 10.0.0.0/27 <br>
GatewaySubnet = 10.0.0.32/29 <br>
區域網路名稱 = RMVNetLocal <br>
GatewayType = DynamicRouting

**Resource Manager VNet 設定**

VNet 名稱 = RMVNet  <br>
資源群組 = RG1 <br>
虛擬網路的 IP 位址空間 = 192.168.0.0/16 <br>
子網路 1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
位置 = 美國東部 <br>
閘道公用 IP 名稱 = gwpip <br>
區域網路閘道 = ClassicVNetLocal <br>
虛擬網路閘道名稱 = RMGateway <br>
閘道 IP 位址組態 = gwipconfig

## <a name="createsmgw"></a>區段 1-設定 hello 傳統的 VNet
### <a name="part-1---download-your-network-configuration-file"></a>第 1 部份 - 下載您的網路組態檔
1. 登入 tooyour hello PowerShell 主控台中的 Azure 帳戶使用提升權限的權限。 hello 下列 cmdlet 會提示您輸入 hello 登入認證您的 Azure 帳戶。 登入之後，它會下載您的帳戶設定，使其可用 tooAzure PowerShell。 使用 hello SM PowerShell cmdlet toocomplete hello 組態的這個部分。

  ```powershell
  Add-AzureAccount
  ```
2. 藉由執行下列命令的 hello 匯出您的 Azure 網路組態檔。 您可以變更 hello hello 檔 tooexport tooa 不同位置的必要的位置。

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. 開啟 hello.xml 檔案下載 tooedit 它。 如需 hello 網路組態檔的範例，請參閱 hello[網路組態結構描述](https://msdn.microsoft.com/library/jj157100.aspx)。

### <a name="part-2--verify-hello-gateway-subnet"></a>組件 2-確認 hello 閘道子網路
在 hello **Netcfg**項目，如果其中一個已尚未建立加入閘道子網路 tooyour VNet。 當使用 hello 網路組態檔，hello 閘道子網路必須命名為"GatewaySubnet 」 或 Azure 無法辨識，並將它當做閘道子網路。

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**範例：**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>第 3 部分-加入 hello 區域網路網站
hello 區域網路網站，您將加入代表 hello RM VNet toowhich 想 tooconnect。 新增**LocalNetworkSites**元素 toohello 檔案如果還不存在。 此時在 hello 組態 hello VPNGatewayAddress 可以是任何有效的公用 IP 位址因為我們尚未建立 hello hello 資源管理員 VNet 閘道。 一旦我們建立 hello 閘道時，我們將在 hello 正確公用 IP 位址已指派 toohello RM 閘道以取代此預留位置 IP 位址。

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>第 4 部分-將 hello VNet 與 hello 區域網路網站產生關聯
在本節中，我們在此指定您想 tooconnect hello 區域網路網站 hello VNet 對。 在此情況下，它為 hello 稍早所參考的資源管理員 VNet。 請確定 hello 名稱相符。 此步驟不會建立閘道。 它會指定將連線 hello hello 閘道的區域網路。

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>第 5-儲存 hello 檔案並上傳
儲存 hello 檔案，然後將它匯入 tooAzure 藉由執行下列命令的 hello。 請確定您變更視您環境的 hello 檔案路徑。

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

您會看到類似的結果顯示 hello 匯入成功。

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>第 6-建立 hello 閘道

執行此範例之前，請參閱 toohello hello 的確切名稱，Azure，您所下載的網路組態檔必須要有 toosee。 hello 網路組態檔包含傳統的虛擬網路的 hello 值。 有時傳統時會建立傳統的 VNet 設定中變更 Vnet hello 網路組態檔中的 hello 名稱 hello Azure 入口網站，因為 toohello hello 部署模型的差異。 例如，如果您使用傳統的 VNet 名為 ' 傳統 VNet' 並建立名為 'ClassicRG' 的資源群組中的 Azure 入口網站 toocreate hello，hello 網路組態檔中包含的 hello 名稱會是轉換的 too'Group ClassicRG 傳統 VNet'。 指定時 hello 名稱包含空格的 VNet，請使用引號括住 hello 值。


使用下列範例 toocreate 動態路由閘道的 hello:

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

您可以查看 hello 狀態 hello 閘道使用 hello **Get AzureVNetGateway** cmdlet。

## <a name="creatermgw"></a>區段 2： 設定 hello RM VNet 閘道
toocreate hello RM VNet VPN 閘道，請遵循下列指示的 hello。 在擷取 hello 傳統 VNet 的閘道 hello 公用 IP 位址之後，不要開始 hello 步驟，直到。 

1. 登入 tooyour hello PowerShell 主控台中的 Azure 帳戶。 hello 下列 cmdlet 會提示您輸入 hello 登入認證您的 Azure 帳戶。 登入之後，使其可用 tooAzure PowerShell，會下載您的帳戶設定。

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  如果您有多個訂用帳戶，請取得 Azure 訂用帳戶的清單。

  ```powershell
  Get-AzureRmSubscription
  ```
   
  指定您想 toouse hello 訂用帳戶。

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. 建立區域網路閘道。 在虛擬網路中，hello 區域網路閘道通常是指 tooyour 在內部部署位置。 在此情況下，hello 區域網路閘道是指 tooyour 傳統的 VNet。 指定的名稱之 Azure，請參閱 tooit，和也指定 hello 位址空間前置詞。 Azure 會使用您指定哪些流量 toosend tooyour 內部部署位置 tooidentify hello IP 位址首碼。 如果您需要 tooadjust hello 資訊之後，再建立您的閘道，您可以修改 hello 值和執行的 hello 範例一次。
   
   **-名稱**是您希望 tooassign toorefer toohello 區域網路閘道的 hello 名稱。<br>
   **-AddressPrefix**為 hello 傳統 VNet 位址空間。<br>
   **-GatewayIpAddress** hello 公用 IP 位址的 hello 傳統 VNet 的閘道。 請務必 toochange hello 以下的範例 tooreflect hello 正確的 IP 位址。<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. 要求的公用 IP 位址 toobe 配置的 toohello 虛擬網路閘道 hello 資源管理員的 VNet。 您無法指定您想 toouse hello IP 位址。 hello IP 位址是以動態方式配置 toohello 虛擬網路閘道。 不過，這不表示 hello 的 IP 位址變更。 hello 虛擬網路閘道的 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。 它不會在調整大小、 重設，或其他內部維護/升級 hello 閘道的變更。

  在此步驟中，我們也會設定用於後續步驟中的變數。

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. 確認您的虛擬網路有閘道子網路。 如果閘道器子網路不存在，請新增一個。 請確定名為 hello 閘道子網路*GatewaySubnet*。
5. 擷取用於 hello 閘道，藉由執行下列命令的 hello hello 子網路。 在此步驟中，我們也會設定變數的 toobe hello 下一個步驟中所使用。
   
   **-名稱**hello 的 VNet 的資源管理員的名稱。<br>
   **-ResourceGroupName**為 hello 資源群組 VNet 相關聯的 hello。 hello 閘道子網路用於此 VNet 必須已經存在，以及必須命名為*GatewaySubnet* toowork 正確。<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. 建立 hello 閘道 IP 位址組態。 hello 閘道組態會定義 hello 子網路和公用 IP 位址 toouse hello。 使用下列範例 toocreate hello 閘道設定。

  在此步驟中，hello **-SubnetId**和**-PublicIpAddressId**參數必須傳遞 hello id 屬性從 hello 子網路和 IP 位址的物件，分別。 您無法使用簡單的字串。 這些變數會設定在 hello 步驟 toorequest 公用 IP 並 hello 步驟 tooretrieve hello 子網路。

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. 執行下列命令的 hello 建立 hello 資源管理員虛擬網路閘道。 hello`-VpnType`必須*RouteBased*。 可能需要 45 分鐘或更 hello 閘道 toocreate。

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. 一旦建立 hello VPN 閘道，請複製 hello 公用 IP 位址。 您使用它時設定傳統 VNet 的 hello 區域網路設定。 您可以使用下列 cmdlet tooretrieve hello 公用 IP 位址的 hello。 hello 公用 IP 位址會列示在 hello 做為傳回*IpAddress*。

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>第 3 節： 修改 hello 傳統 VNet 本機站台設定

在本節中，您使用 hello 傳統的 VNet。 您要取代指定 hello 本機站台設定，將會使用的 tooconnect toohello 資源管理員 VNet 閘道時所使用的 hello 預留位置 IP 位址。 

1. 匯出 hello 網路組態檔。

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. 使用文字編輯器，修改 VPNGatewayAddress hello 值。 Hello 預留位置 IP 位址取代 hello 資源管理員閘道的 hello 公用 IP 位址，然後儲存 hello 的變更。

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. 匯入 hello 修改網路設定檔 tooAzure。

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>區段 4： 建立 hello 閘道之間的連接
建立 hello 閘道之間的連線需要 PowerShell。 您可能需要 tooadd 您 Azure 帳戶 toouse hello 精簡 hello PowerShell cmdlet。 因此，使用 toodo **Add-azureaccount**。

1. 在 hello PowerShell 主控台中，設定您的共用的金鑰。 在執行之前 hello 指令程式，請參閱 toohello hello 的確切名稱，Azure，您所下載的網路組態檔必須要有 toosee。 在指定 hello 名稱包含空格的 VNet，使用單一引號括住 hello 值。<br><br>在下列範例中， **-VNetName** hello hello 名稱傳統 VNet 和**-LocalNetworkSiteName** hello 您為 hello 區域網路網站指定的名稱。 hello **-SharedKey**是產生及指定的值。 在 hello 範例中，我們使用 'abc123'，但您可以產生並使用更複雜的項目。 hello 重要件事就是您在此處指定的 hello 該值必須是相同的值建立您的連線時，指定 hello 下一個步驟中的 hello。 應該會顯示 hello 傳回**狀態： 成功**。

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. 執行下列命令的 hello 建立 hello VPN 連線：
   
  設定 hello 變數。

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  建立 hello 連線。 請注意該 hello **-ConnectionType**是 IPsec 不 Vnet2Vnet。

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>第 5 節︰驗證您的連線

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>從傳統 VNet tooyour 資源管理員 VNet tooverify hello 連線

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Azure 入口網站

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>從資源管理員 VNet tooyour tooverify hello 連接傳統的 VNet

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Azure 入口網站

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>VNet 對 VNet 常見問題集

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

