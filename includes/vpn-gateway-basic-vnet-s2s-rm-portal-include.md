toocreate hello Resource Manager 部署模型使用 hello Azure 入口網站中的 VNet，請遵循下列 hello 步驟。 使用 hello[範例值](#values)如果您使用下列步驟做教學課程。 如果您不為教學課程進行下列步驟，是以您自己的確定 tooreplace hello 值。 如需有關使用虛擬網路的詳細資訊，請參閱 hello[虛擬網路概觀](../articles/virtual-network/virtual-networks-overview.md)。

1. 從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)並以您的 Azure 帳戶登入。
2. 按一下 [新增] 。 在 hello**搜尋 hello marketplace**欄位中，輸入 虛擬網路。 找出**虛擬網路**hello 傳回從清單中，按一下 tooopen hello**虛擬網路**刀鋒視窗。
3. Hello hello 虛擬網路刀鋒視窗中，從 hello 底端附近**選取部署模型**清單中，選取**資源管理員**，然後按一下**建立**。 這會開啟刀鋒視窗中 建立虛擬網路' hello。

    ![建立虛擬網路刀鋒視窗](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "建立虛擬網路刀鋒視窗")
4. 在 hello**建立虛擬網路**刀鋒視窗中，設定 hello VNet 設定。 當您填滿 hello 欄位中時，hello 紅色驚嘆號會變成綠色的核取記號時 hello hello 欄位中輸入的字元都有效。

  - **名稱**： 輸入您的虛擬網路的 hello 名稱。 在此範例中，我們使用 TestVNet1。
  - **位址空間**： 輸入 hello 位址空間。 如果您有多個位址空間 tooadd，加入您的第一個位址空間。 您可以建立 hello VNet 後的更新版本中，加入其他位址空間。 請確定您指定不會與您在內部部署位置的 hello 位址空間重疊該 hello 位址空間。
  - **子網路名稱**： 新增 hello 第一個子網路名稱和子網路位址範圍。 您之後可以加入其他子網路和 hello 閘道子網路，在建立此 VNet 後。 
  - **訂用帳戶**： 確認列出的 hello 訂閱是 hello 正確。 您可以使用 [hello] 下拉式清單來變更訂用帳戶。
  - **資源群組**：選取現有資源群組，或輸入新資源群組的名稱以建立新的資源群組。 如果您要建立新的群組，根據 tooyour 名稱 hello 資源群組已規劃的組態值。 如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)。
  - **位置**： 選取您的 VNet 的 hello 位置。 hello 位置會決定您將部署 toothis VNet hello 資源所在的位置。

5. 選取**Pin toodashboard**如果您想 toobe 無法 toofind 輕鬆 hello 儀表板上，您的 VNet，然後按一下**建立**。 按一下後**建立**，您會看到磚儀表板上，將會反映您的 VNet hello 進度。 hello hello 磚變更正在建立 VNet。
