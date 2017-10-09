### <a name="gwipnoconnection"></a>toomodify hello 區域網路閘道 IP 位址沒有閘道連線

使用 hello 範例 toomodify 沒有閘道連線的區域網路閘道。 當修改這個值，您也可以修改在 hello hello 位址前置詞相同的時間。

1. 在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。
2. 在 hello **IP 位址**方塊中，修改 hello IP 位址。
3. 按一下**儲存**toosave hello 設定。

### <a name="gwipwithconnection"></a>toomodify hello 區域網路閘道閘道 IP 位址-現有的閘道連線

toomodify 已連接的區域網路閘道，您需要 toofirst 移除 hello 連線。 移除 hello 連線之後，您可以修改 hello 閘道 IP 位址，並重新建立新的連接。 您也可以修改在 hello hello 位址前置詞相同的時間。 這會導致您 VPN 連線的停機時間。 當修改 hello 閘道 IP 位址，您不需要 toodelete hello VPN 閘道。 您只需要 tooremove hello 連線。
 
#### <a name="1-remove-hello-connection"></a>1.移除 hello 連線。

1. 在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**連線**。
2. 按一下 hello **...**該行 hello hello 連線，然後按一下**刪除**。
3. 按一下**儲存**toosave 您的設定。

#### <a name="2-modify-hello-ip-address"></a>2.修改 hello IP 位址。

您也可以修改在 hello hello 位址前置詞相同的時間。

1. 在 hello **IP 位址**方塊中，修改 hello IP 位址。
2. 按一下**儲存**toosave hello 設定。

#### <a name="3-recreate-hello-connection"></a>3.重新建立 hello 連線。

1. 瀏覽您的 VNet toohello 虛擬網路閘道。 (不 hello 本機網路閘道。)
2. 在 hello 虛擬網路閘道，在 hello**設定**區段中，按一下**連線**。
3. 按一下 hello **+ 加**tooopen hello**加入連接**刀鋒視窗。
4. 重新建立您的連線。
5. 按一下**確定**toocreate hello 連線。
