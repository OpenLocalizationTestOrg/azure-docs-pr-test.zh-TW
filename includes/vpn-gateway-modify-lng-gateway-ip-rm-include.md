### <a name="gwipnoconnection"></a>toomodify hello 區域網路閘道 'GatewayIpAddress'-沒有閘道連線

如果您想 tooconnect toohas hello VPN 裝置變更其公用 IP 位址，您會需要 toomodify hello 區域網路閘道 tooreflect 變更。 使用 hello 範例 toomodify 沒有閘道連線的區域網路閘道。

當修改這個值，您也可以修改在 hello hello 位址前置詞相同的時間。 確定 toouse hello 現有名稱區域網路閘道處於順序 toooverwrite hello 目前設定。 如果您使用不同的名稱，您會建立新的區域網路閘道，而非覆寫 hello 現有的我的最愛。

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>toomodify hello 區域網路閘道 'GatewayIpAddress'-現有的閘道連線

如果您想 tooconnect toohas hello VPN 裝置變更其公用 IP 位址，您會需要 toomodify hello 區域網路閘道 tooreflect 變更。 如果閘道連線已存在，您必須先 tooremove hello 連線。 移除 hello 連線之後，您可以修改 hello 閘道 IP 位址，並重新建立新的連接。 您也可以修改在 hello hello 位址前置詞相同的時間。 這會導致您 VPN 連線的停機時間。 當修改 hello 閘道 IP 位址，您不需要 toodelete hello VPN 閘道。 您只需要 tooremove hello 連線。
 

1. 移除 hello 連線。 您可以使用 ' Get AzureRmVirtualNetworkGatewayConnection' hello cmdlet 找到 hello 您連線的名稱。

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. 修改 hello 'GatewayIpAddress' 值。 您也可以修改在 hello hello 位址前置詞相同的時間。 是確定 toouse hello 現有名稱區域網路閘道 toooverwrite hello 目前的設定。 如果沒有，您會建立新的區域網路閘道，而非覆寫 hello 現有的我的最愛。

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. 建立 hello 連線。 在此範例中，我們會設定 IPsec 連線類型。 當您重新建立您的連線時，使用指定的 hello 連接類型來設定。 其他連接類型，請參閱 hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx)頁面。  tooobtain hello VirtualNetworkGateway 名稱，您可以執行 hello ' Get AzureRmVirtualNetworkGateway' 指令程式。
   
    設定 hello 變數。

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    建立 hello 連線。

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```