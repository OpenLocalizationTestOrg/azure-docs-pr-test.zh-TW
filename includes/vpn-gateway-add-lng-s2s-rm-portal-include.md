1. 在 hello 入口網站，從**所有資源**，按一下  **+ 加**。 
2. 在 hello**一切**刀鋒視窗中 搜尋 方塊中，輸入**區域網路閘道**，然後按一下 toosearch。 這會傳回清單。 按一下**區域網路閘道**tooopen hello 刀鋒視窗中，然後按一下 **建立**tooopen hello**建立區域網路閘道**刀鋒視窗。

  ![建立區域網路閘道](./media/vpn-gateway-add-lng-s2s-rm-portal-include/createlng.png)

3. 在 hello**刀鋒視窗中的區域網路閘道建立**，指定您的本機網路閘道的 hello 值。

  - **名稱：**指定區域網路閘道物件的名稱。
  - **IP 位址：**這是您想要 Azure tooconnect hello VPN 裝置的 hello 公用 IP 位址。 指定有效的公用 IP 位址。 hello IP 位址不得位於 NAT 後方且 toobe 連線到 azure。 如果您目前還沒有 hello IP 位址，您可以使用 hello hello 螢幕擷取畫面，顯示的值，但您將需要回 toogo 並取代 hello 公用 IP 位址的 VPN 裝置的預留位置 IP 位址。 否則，Azure 將不會無法 tooconnect。
  - **位址空間**hello 網路，此本機網路表示參考 toohello 位址範圍。 您可以加入多個位址空間範圍。 請確定您在此處指定的 hello 範圍不得執行與您想要 tooconnect 其他網路的範圍重疊。 Azure 會路由傳送嗨您指定 toohello 在內部部署 VPN 裝置 IP 位址的位址範圍。 *這裡使用您自己的值，不 hello hello 螢幕擷取畫面所示值*。
  - **訂用帳戶：**確認該 hello 正確顯示訂用帳戶。
  - **資源群組：**想 toouse 選取 hello 資源群組。 您可以建立新的資源群組或選取已建立的資源群組。
  - **位置：**選取 hello 位置中，將會建立此物件。 您可能想 tooselect hello 中，位於您的 VNet 的相同位置，但是您不需要的 toodo 因此。

4. 當您完成指定 hello 值時，按一下 **建立**底部 hello hello 刀鋒視窗 toocreate hello 區域網路閘道。
