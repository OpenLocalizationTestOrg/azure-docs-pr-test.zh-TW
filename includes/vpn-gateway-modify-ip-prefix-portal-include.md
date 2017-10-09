### <a name="noconnection"></a>toomodify 區域網路閘道 IP 位址首碼不閘道連線

#### <a name="tooadd-additional-address-prefixes"></a>tooadd 其他位址前置詞：

1. 在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。
2. 新增 hello IP 位址空間中 hello*新增其他位址範圍*方塊。
3. 按一下**儲存**toosave 您的設定。

#### <a name="tooremove-address-prefixes"></a>tooremove 位址首碼：

1. 在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。
2. 按一下 hello **'...'**想 tooremove hello 包含 hello 前置詞的程式行。
3. 按一下 [移除] 。
4. 按一下**儲存**toosave 您的設定。

### <a name="withconnection"></a>toomodify 區域網路閘道的 IP 位址首碼為現有的閘道連線

如果您有閘道連接和要 tooadd 或移除 hello IP 位址前置詞包含在您的本機網路閘道，您會需要 toodo hello 依照依順序的步驟。 這會導致您 VPN 連線的停機時間。 修改 IP 位址前置詞，您無須 toodelete hello VPN 閘道。 您只需要 tooremove hello 連線。

#### <a name="1-remove-hello-connection"></a>1.移除 hello 連線。

1. 在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**連線**。
2. 按一下 hello **...**在每個連線的 hello 一行，然後按一下**刪除**。
3. 按一下**儲存**toosave 您的設定。

#### <a name="2-modify-hello-address-prefixes"></a>2.修改 hello 位址前置詞。

tooadd 其他位址前置詞：

1. 在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。
2. 加入 hello IP 位址空間。
3. 按一下**儲存**toosave 您的設定。

tooremove 位址首碼：

1. 在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。
2. 按一下 hello **...**想 tooremove hello 包含 hello 前置詞的程式行。
3. 按一下 [移除] 。
4. 按一下**儲存**toosave 您的設定。

#### <a name="3-recreate-hello-connection"></a>3.重新建立 hello 連線。

1. 瀏覽您的 VNet toohello 虛擬網路閘道。 (不 hello 本機網路閘道。)
2. 在 hello 虛擬網路閘道，在 hello**設定**區段中，按一下**連線**。
3. 按一下 hello **+ 加**tooopen hello**加入連接**刀鋒視窗。
4. 重新建立您的連線。
5. 按一下**確定**toocreate hello 連線。
