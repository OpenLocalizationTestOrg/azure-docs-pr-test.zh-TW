### <a name="to-modify-the-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="54c57-101">修改區域網路閘道 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="54c57-101">To modify the local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="54c57-102">如果您想要連線的 VPN 裝置已變更其公用 IP 位址，您需要修改區域網路閘道，以反映該變更。</span><span class="sxs-lookup"><span data-stu-id="54c57-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="54c57-103">您可變更閘道 IP 位址，而不需移除現有的 VPN 閘道連線 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="54c57-103">The gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="54c57-104">若要修改閘道 IP 位址，使用 [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) 命令以您自己的值取代 'Site2' 和 'TestRG1'。</span><span class="sxs-lookup"><span data-stu-id="54c57-104">To modify the gateway IP address, replace the values 'Site2' and 'TestRG1' with your own using the [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="54c57-105">確認輸出中的 IP 位址正確無誤︰</span><span class="sxs-lookup"><span data-stu-id="54c57-105">Verify that the IP address is correct in the output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```