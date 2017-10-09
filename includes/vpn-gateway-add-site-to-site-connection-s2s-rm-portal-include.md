1. 瀏覽 tooand 開啟 hello 刀鋒視窗中的虛擬網路閘道。 有多個方式 toonavigate。 在本例中，巡覽 toohello 閘道 'VNet1GW' 太移**TestVNet1]-> [概觀]-> [已連接裝置]-> [VNet1GW**。
2. 如 VNet1GW hello] 刀鋒視窗，按一下 [**連線**。 在 hello hello 連線刀鋒視窗頂端，按一下**+ 加**tooopen hello**加入連接**刀鋒視窗。

    ![建立站對站連線](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. 在 hello**加入連接**刀鋒視窗中，在 hello 填滿值 toocreate 您的連線。

  - **名稱：**為您的連線命名。 我們在範例中使用 **VNet1toSite2**。
  - **連線類型：**選取 [站對站 (IPSec)]。
  - **虛擬網路閘道：** hello 值固定的因為您從這個閘道連接。
  - **區域網路閘道：**按一下**選擇區域網路閘道**和您想 toouse 選取 hello 區域網路閘道。 在我們的範例中，我們使用 **Site2**。
  - **共用的金鑰：** hello 值必須符合您使用本機的內部部署 VPN 裝置的 hello 值。 在 hello 範例中，我們使用 'abc123'，但您可以 （而且也應該） 使用更複雜的項目。 hello 重要件事就是您在此處指定的 hello 該值必須是相同的值，指定設定 VPN 裝置時的 hello。
  - 其餘的值的 hello**訂用帳戶**，**資源群組**，和**位置**固定的。

4. 按一下**確定**toocreate 您的連線。 您會看到*建立連線*快閃囉 」 畫面上。
5. 您可以在 hello 檢視 hello 連接**連線**刀鋒視窗中的 hello 虛擬網路閘道。 hello 狀態就會從*未知*太*連接*，然後太*Succeeded*。
