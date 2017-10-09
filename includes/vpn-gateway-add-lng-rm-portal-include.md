1. 在 hello 入口網站，從**所有資源**，按一下  **+ 加**。 在 hello**的所有項目**刀鋒視窗中 搜尋 方塊中，輸入**區域網路閘道**，然後按一下 tooreturn 資源的清單。 按一下**區域網路閘道**tooopen hello 刀鋒視窗中，然後按一下 **建立**tooopen hello**建立區域網路閘道**刀鋒視窗。
   
    ![建立區域網路閘道](./media/vpn-gateway-add-lng-rm-portal-include/lng.png)

2. 在 hello**建立區域網路閘道刀鋒視窗**，指定**名稱**您區域網路閘道的物件。 可能的話，請使用直覺式名稱，例如 **ClassicVNetLocal** 或 **TestVNet1Local**。 這樣可以方便您 tooidentify hello 區域網路閘道 hello 入口網站中。
3. 指定有效的公用**IP 位址**想 hello VPN 裝置或虛擬網路閘道 toowhich tooconnect。<br>**如果此本機網路表示內部部署位置：**指定您想要 tooconnect hello VPN 裝置 hello 公用 IP 位址。 它不得位於 NAT 後方且 toobe 連線到 azure。<br>**如果此區域網路代表另一個 VNet:**指定 hello 公用 IP 位址指派給該 VNet toohello 虛擬網路閘道。<br>**如果您還沒有 hello IP 位址：**您可以組成有效的預留位置 IP 位址，然後再返回並修改這個設定，再連接。
4. **位址空間**hello 網路，此本機網路表示參考 toohello 位址範圍。 您可以加入多個位址空間範圍。 請確定您在此處指定的 hello 範圍不得執行與您連接其他網路 toowhich 的範圍重疊。
5. 如**訂用帳戶**，確認該 hello 正確顯示訂用帳戶。
6. 如**資源群組**，選取您想 toouse hello 資源群組。 您可以建立新的資源群組或選取已建立的資源群組。
7. 如**位置**，選取將在其中建立此資源的 hello 位置。 您可能想 tooselect hello 中，位於您的 VNet 的相同位置，但是您不需要的 toodo 因此。
8. 按一下**建立**toocreate hello 區域網路閘道。

