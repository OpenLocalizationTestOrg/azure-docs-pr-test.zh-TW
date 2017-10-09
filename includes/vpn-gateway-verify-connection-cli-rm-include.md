您可以確認您的連線成功使用 hello [az 網路 vpn 連線顯示](/cli/azure/network/vpn-connection#show)命令。 在 hello 範例中，'-名稱 ' 指的是您想 tootest hello 連接 toohello 名稱。 Hello 處理序正在建立中 hello 連線時，其連接狀態會顯示 '連接到'。 Hello 狀態 hello 連線建立之後，變更 too'Connected'。

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

