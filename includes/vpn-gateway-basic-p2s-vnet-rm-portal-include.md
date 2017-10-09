toocreate hello Resource Manager 部署模型使用 hello Azure 入口網站中的 VNet，請遵循下列 hello 步驟。 hello 螢幕擷取畫面會提供範例。 是以您自己的確定 tooreplace hello 值。 如需有關使用虛擬網路的詳細資訊，請參閱 hello[虛擬網路概觀](../articles/virtual-network/virtual-networks-overview.md)。

1. 從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。
2. 按一下頁面底部的 [新增] **+**來單一登入應用程式。 在 hello**搜尋 hello marketplace**欄位中，輸入 「 虛擬網路 」。 找出**虛擬網路**hello 傳回從清單中，按一下 tooopen hello**虛擬網路**頁面。

  ![找出虛擬網路資源頁面](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/newvnetportal700.png "找出虛擬網路資源頁面")
3. Hello hello 虛擬網路 頁面上，從 hello 底端附近**選取部署模型**清單中，選取**資源管理員**，然後按一下**建立**。

  ![選取資源管理員](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/resourcemanager250.png "選取資源管理員")
4. 在 hello**建立虛擬網路**頁面上，設定 hello VNet 設定。 當您填滿 hello 欄位中時，hello 紅色驚嘆號會變成綠色的核取記號時 hello hello 欄位中輸入的字元都有效。 有些值可能會自動填入。 如果是這樣，hello 值取代您自己。 hello**建立虛擬網路**頁面看起來類似下列範例的 toohello:

  ![欄位驗證](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/createp2sgvnet.png "欄位驗證")
5. **名稱**： 輸入您的虛擬網路的 hello 名稱。
6. **位址空間**： 輸入 hello 位址空間。 如果您有多個位址空間 tooadd，加入您的第一個位址空間。 您可以建立 hello VNet 後的更新版本中，加入其他位址空間。
7. **子網路名稱**： 新增 hello 子網路名稱和子網路位址範圍。 您可以建立 hello VNet 後的更新版本中，新增其他子網路。
8. **訂用帳戶**： 確認該訂用帳戶所列的 hello 是 hello 正確。 您可以使用 [hello] 下拉式清單來變更訂用帳戶。
9. **資源群組**：選取現有資源群組，或輸入新資源群組的名稱以建立新的資源群組。 如果您要建立新的群組，根據 tooyour 名稱 hello 資源群組已規劃的組態值。 如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)。
10. **位置**： 選取您的 VNet 的 hello 位置。 hello 位置會決定您將部署 toothis VNet hello 資源所在的位置。
11. 選取**Pin toodashboard**如果您想 toobe 無法 toofind 輕鬆 hello 儀表板上，您的 VNet，然後按一下**建立**。

 ![Pin toodashboard](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/pintodashboard150.png "pin toodashboard")
12. 按一下後**建立**，您會看到磚儀表板上，將會反映您的 VNet hello 進度。 hello hello 磚變更正在建立 VNet。

  ![建立虛擬網路圖格](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/deploying150.png "建立虛擬網路圖格")