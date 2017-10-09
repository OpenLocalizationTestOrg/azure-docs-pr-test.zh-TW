此工作會使用 VNet 的 hello 步驟 hello 下列組態的參考清單中的 hello 值為基礎。 其他設定和名稱也會概述於這份清單中。 雖然我們沒有新增根據這份清單中的 hello 值的變數，我們不直接在 hello 步驟中的任何使用這份清單。 您可以複製 hello 清單 toouse，做為參考，取代您自己 hello 值。

**組態參考清單**

* 虛擬網路名稱 = "TestVNet"
* 虛擬網路位址空間 = 192.168.0.0/16
* 資源群組 = "TestRG"
* Subnet1 名稱 = "FrontEnd" 
* Subnet1 位址空間 = "192.168.1.0/24"
* 閘道器子網路名稱："GatewaySubnet"，您必須一律將閘道器子網路命名為 *GatewaySubnet*。
* 閘道子網路位址空間 = "192.168.200.0/26"
* 區域 = "East US"
* 閘道名稱 = "GW"
* 閘道 IP 名稱 = "GWIP"
* 閘道 IP 組態名稱 = "gwipconf"
* 類型 = "ExpressRoute"，ExpressRoute 組態需要有這個類型。
* 閘道公用 IP 名稱 = "gwpip"

## <a name="add-a-gateway"></a>新增閘道
1. 連接 tooyour Azure 訂用帳戶。

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. 宣告您在本練習中使用的變數。 為確定 tooedit 想 toouse hello 範例 tooreflect hello 設定。

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. 以變數儲存在 hello 虛擬網路物件。

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. 加入閘道子網路 tooyour 虛擬網路。 hello 閘道子網路必須命名為"GatewaySubnet"。 您應建立 /27 或更大 (/26、/25 等) 的閘道子網路。

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. 將 hello 組態設定。

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. 以變數儲存在 hello 閘道子網路。

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. 要求公用 IP 位址。 建立 hello 閘道之前，已要求 hello IP 位址。 您不能指定您想 toouse; hello IP 位址它會動態配置。 Hello 下一個組態區段中，您將使用此 IP 位址。 hello AllocationMethod 必須是動態。

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. 建立您的閘道器的 hello 組態。 hello 閘道組態會定義 hello 子網路和公用 IP 位址 toouse hello。 在此步驟中，您要指定您建立 hello 閘道時所使用的 hello 組態。 這個步驟實際上不會建立 hello 閘道物件。 使用以下 toocreate hello 範例閘道設定。

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. 建立 hello 閘道。 在此步驟中，hello **-gatewaytype 的授權**尤其重要。 您必須使用 hello 值**ExpressRoute**。 執行這些 cmdlet 之後, hello 閘道可能需要 45 分鐘或更多 toocreate。

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>確認已建立 hello 閘道
使用下列命令已建立 hello 閘道的 tooverify hello:

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>調整閘道器大小
有幾個 [閘道 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)。 您可以使用下列隨時命令 toochange hello 閘道 SKU 的 hello。

> [!IMPORTANT]
> 此命令不適用於 UltraPerformance 閘道。 toochange 閘道 tooan UltraPerformance 閘道，先移除現有的 ExpressRoute 閘道的 hello，然後再建立新的 UltraPerformance 閘道。 toodowngrade UltraPerformance 閘道，從您的閘道先移除 hello UltraPerformance 閘道，然後再建立新的閘道。
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>移除閘道器
使用下列命令 tooremove 閘道 hello:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```