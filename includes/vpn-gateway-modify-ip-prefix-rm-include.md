### <a name="noconnection"></a>toomodify 區域網路閘道 IP 位址首碼不閘道連線

tooadd 其他位址前置詞：

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

tooremove 位址首碼：<br>
會省略您不再需要的 hello 前置詞。 在此範例中，我們不再需要的前置詞 20.0.0.0/24 （從 hello 上述範例中），因此，我們更新 hello 區域網路閘道，但不包括該前置詞。

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify 區域網路閘道的 IP 位址首碼為現有的閘道連線

如果您有閘道連接和要 tooadd 或移除 hello IP 位址前置詞包含在您的本機網路閘道，您會需要 toodo hello 依照依順序的步驟。 這會導致您 VPN 連線的停機時間。 修改 IP 位址前置詞，您無須 toodelete hello VPN 閘道。 您只需要 tooremove hello 連線。


1. 移除 hello 連線。

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. 修改您的本機網路閘道的 hello 位址首碼。
   
  設定 hello LocalNetworkGateway hello 變數。

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  修改 hello 前置詞。
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. 建立 hello 連線。 在此範例中，我們會設定 IPsec 連線類型。 當您重新建立您的連線時，使用指定的 hello 連接類型來設定。 其他連接類型，請參閱 hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx)頁面。
   
  設定 hello VirtualNetworkGateway hello 變數。

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  建立 hello 連線。 這個範例會使用 hello 變數 $local 您在步驟 2 中設定。

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```