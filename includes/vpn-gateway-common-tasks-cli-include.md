### <a name="tooview-local-network-gateways"></a>tooview 區域網路閘道

一份 hello 區域網路閘道，使用 hello tooview [az 網路本機閘道清單](https://docs.microsoft.com/cli/azure/network/local-gateway#list)命令。

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>tooverify hello 共用索引鍵的值

確認 hello 共用金鑰的值為 hello 您用於 VPN 裝置組態的相同值。 如果不是，執行一次使用 從 hello 裝置 hello 值 hello 連線，或更新裝置 hello 與 hello hello 傳回值。 hello 值必須符合。 tooview hello 的共用金鑰，使用 hello [az 網路的 vpn 連線清單](https://docs.microsoft.com/cli/azure/network/vpn-connection#list)。

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>tooview hello VPN 閘道的公用 IP 位址

toofind hello 公用 IP 位址的虛擬網路閘道，使用 hello [az 網路公用 ip 清單](https://docs.microsoft.com/cli/azure/network/public-ip#list)命令。 以方便閱讀，此範例中的 hello 輸出會是格式化的 toodisplay hello 清單的資料表中的公用 Ip。

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
