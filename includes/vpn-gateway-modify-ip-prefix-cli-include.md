### <a name="noconnection"></a>toomodify 區域網路閘道 IP 位址首碼不閘道連線

如果您沒有閘道連線，而且您想要 tooadd 或移除 IP 位址前置詞，您會使用 hello 相同命令，您會使用 toocreate hello 區域網路閘道， [az 網路本機閘道建立](https://docs.microsoft.com/cli/azure/network/local-gateway#create)。 您也可以使用這個命令 tooupdate hello 閘道 IP 位址的 hello VPN 裝置。 toooverwrite hello 目前的設定，使用您的本機網路閘道 hello 現有名稱。 如果您使用不同的名稱，您會建立新的區域網路閘道，而非覆寫 hello 現有的我的最愛。

必須指定每次您進行變更、 hello 的前置詞的完整清單，您想 toochange 不只是 hello 前置詞。 指定您想 tookeep 只有 hello 前置詞。 在此案例中為 10.0.0.0/24 和 20.0.0.0/24

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify 區域網路閘道的 IP 位址首碼為現有的閘道連線

如果您有閘道連接和要 tooadd 或移除 IP 位址前置詞，您可以更新 hello 前置詞使用[az 網路本機閘道更新](https://docs.microsoft.com/cli/azure/network/local-gateway#update)。 這會導致您 VPN 連線的停機時間。 當修改 hello IP 位址前置詞時，您不需要 toodelete hello VPN 閘道。

必須指定每次您進行變更、 hello 的前置詞的完整清單，您想 toochange 不只是 hello 前置詞。 在此範例中，10.0.0.0/24 和 20.0.0.0/24 已存在。 我們加入 hello 前置詞 30.0.0.0/24 和 40.0.0.0/24，並指定所有 4 hello 前置詞，更新時。

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```