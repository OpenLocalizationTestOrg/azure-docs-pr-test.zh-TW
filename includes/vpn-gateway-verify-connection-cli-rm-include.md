<span data-ttu-id="0d4a4-101">您可以確認您的連線成功使用 hello [az 網路 vpn 連線顯示](/cli/azure/network/vpn-connection#show)命令。</span><span class="sxs-lookup"><span data-stu-id="0d4a4-101">You can verify that your connection succeeded by using hello [az network vpn-connection show](/cli/azure/network/vpn-connection#show) command.</span></span> <span data-ttu-id="0d4a4-102">在 hello 範例中，'-名稱 ' 指的是您想 tootest hello 連接 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="0d4a4-102">In hello example, '--name' refers toohello name of hello connection that you want tootest.</span></span> <span data-ttu-id="0d4a4-103">Hello 處理序正在建立中 hello 連線時，其連接狀態會顯示 '連接到'。</span><span class="sxs-lookup"><span data-stu-id="0d4a4-103">When hello connection is in hello process of being established, its connection status shows 'Connecting'.</span></span> <span data-ttu-id="0d4a4-104">Hello 狀態 hello 連線建立之後，變更 too'Connected'。</span><span class="sxs-lookup"><span data-stu-id="0d4a4-104">Once hello connection is established, hello status changes too'Connected'.</span></span>

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

