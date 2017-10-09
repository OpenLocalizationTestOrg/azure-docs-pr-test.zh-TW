### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="8a5b0-101">toomodify hello 區域網路閘道 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="8a5b0-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="8a5b0-102">如果您想 tooconnect toohas hello VPN 裝置變更其公用 IP 位址，您會需要 toomodify hello 區域網路閘道 tooreflect 變更。</span><span class="sxs-lookup"><span data-stu-id="8a5b0-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="8a5b0-103">可以變更 hello 閘道 IP 位址，但不會移除現有的 VPN 閘道連線 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="8a5b0-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="8a5b0-104">toomodify hello 閘道 IP 位址，取代 hello 值 'Site2' 和 'TestRG1' 以您自己使用 hello [az 網路本機閘道更新](https://docs.microsoft.com/cli/azure/network/local-gateway#update)命令。</span><span class="sxs-lookup"><span data-stu-id="8a5b0-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="8a5b0-105">請確認 hello IP 位址是正確的 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="8a5b0-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```