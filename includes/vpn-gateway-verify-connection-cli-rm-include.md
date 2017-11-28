<span data-ttu-id="62fc4-101">您可以使用 [az network vpn-connection show](/cli/azure/network/vpn-connection#show) 命令來確認連線是否成功。</span><span class="sxs-lookup"><span data-stu-id="62fc4-101">You can verify that your connection succeeded by using the [az network vpn-connection show](/cli/azure/network/vpn-connection#show) command.</span></span> <span data-ttu-id="62fc4-102">在範例中， '--name' 是指您想要測試之連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="62fc4-102">In the example, '--name' refers to the name of the connection that you want to test.</span></span> <span data-ttu-id="62fc4-103">當系統在建立連線時，其連線狀態會顯示「連線中」。</span><span class="sxs-lookup"><span data-stu-id="62fc4-103">When the connection is in the process of being established, its connection status shows 'Connecting'.</span></span> <span data-ttu-id="62fc4-104">連線建立好之後，狀態會變更為 [已連線]。</span><span class="sxs-lookup"><span data-stu-id="62fc4-104">Once the connection is established, the status changes to 'Connected'.</span></span>

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

