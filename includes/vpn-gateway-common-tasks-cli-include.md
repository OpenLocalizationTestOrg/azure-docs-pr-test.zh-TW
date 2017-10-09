### <a name="tooview-local-network-gateways"></a><span data-ttu-id="c31df-101">tooview 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="c31df-101">tooview local network gateways</span></span>

<span data-ttu-id="c31df-102">一份 hello 區域網路閘道，使用 hello tooview [az 網路本機閘道清單](https://docs.microsoft.com/cli/azure/network/local-gateway#list)命令。</span><span class="sxs-lookup"><span data-stu-id="c31df-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="c31df-103">tooverify hello 共用索引鍵的值</span><span class="sxs-lookup"><span data-stu-id="c31df-103">tooverify hello shared key values</span></span>

<span data-ttu-id="c31df-104">確認 hello 共用金鑰的值為 hello 您用於 VPN 裝置組態的相同值。</span><span class="sxs-lookup"><span data-stu-id="c31df-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="c31df-105">如果不是，執行一次使用 從 hello 裝置 hello 值 hello 連線，或更新裝置 hello 與 hello hello 傳回值。</span><span class="sxs-lookup"><span data-stu-id="c31df-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="c31df-106">hello 值必須符合。</span><span class="sxs-lookup"><span data-stu-id="c31df-106">hello values must match.</span></span> <span data-ttu-id="c31df-107">tooview hello 的共用金鑰，使用 hello [az 網路的 vpn 連線清單](https://docs.microsoft.com/cli/azure/network/vpn-connection#list)。</span><span class="sxs-lookup"><span data-stu-id="c31df-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="c31df-108">tooview hello VPN 閘道的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="c31df-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="c31df-109">toofind hello 公用 IP 位址的虛擬網路閘道，使用 hello [az 網路公用 ip 清單](https://docs.microsoft.com/cli/azure/network/public-ip#list)命令。</span><span class="sxs-lookup"><span data-stu-id="c31df-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="c31df-110">以方便閱讀，此範例中的 hello 輸出會是格式化的 toodisplay hello 清單的資料表中的公用 Ip。</span><span class="sxs-lookup"><span data-stu-id="c31df-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
