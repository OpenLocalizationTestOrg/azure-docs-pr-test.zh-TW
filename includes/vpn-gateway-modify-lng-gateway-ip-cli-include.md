### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>toomodify hello 區域網路閘道 'gatewayIpAddress'

如果您想 tooconnect toohas hello VPN 裝置變更其公用 IP 位址，您會需要 toomodify hello 區域網路閘道 tooreflect 變更。 可以變更 hello 閘道 IP 位址，但不會移除現有的 VPN 閘道連線 （如果有的話）。 toomodify hello 閘道 IP 位址，取代 hello 值 'Site2' 和 'TestRG1' 以您自己使用 hello [az 網路本機閘道更新](https://docs.microsoft.com/cli/azure/network/local-gateway#update)命令。

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

請確認 hello IP 位址是正確的 hello 輸出：

```
"gatewayIpAddress": "23.99.222.170",
```