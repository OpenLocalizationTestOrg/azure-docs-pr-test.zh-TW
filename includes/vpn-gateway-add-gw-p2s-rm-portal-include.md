1. 在 hello 入口網站，在 hello 左邊，按一下   **+** 在搜尋中輸入虛擬網路閘道 '。 找出**虛擬網路閘道**hello 搜尋中傳回，並按一下 hello 項目。 在 hello**虛擬網路閘道**頁面上，按一下**建立**底部 hello hello 頁面 tooopen hello**建立虛擬網路閘道**頁面。
2. 在 hello**建立虛擬網路閘道**頁面上，輸入您的虛擬網路閘道的 hello 值。

  ![建立虛擬網路閘道頁面欄位](./media/vpn-gateway-add-gw-p2s-rm-portal-include/p2sgw.png "建立虛擬網路閘道頁面欄位")
3. **名稱**：為您的閘道命名。 命名閘道不是 hello 與命名閘道子網路相同。 它的 hello 您所建立的 hello 閘道物件名稱。
4. 閘道類型︰選取 [VPN]。 VPN 閘道使用 hello 虛擬網路閘道類型**VPN**。
5. **VPN 類型**： 選取您的組態所指定的 hello VPN 類型。 大部分組態需要路由式 VPN 類型。
6. **SKU**： 從 hello 下拉式清單中選取 hello 閘道 SKU。 列出在 hello 下拉式清單中的 hello Sku hello 您所選取的 VPN 類型而定。
7. **位置**： 調整 hello**位置**欄位 toopoint toohello 位置虛擬網路所在的位置。 Hello 位置並未指向 toohello 區域虛擬網路所在的位置，如果 hello 虛擬網路不會出現在下拉式清單中 「 選擇虛擬網路' hello。
8. 選擇 hello 虛擬網路 toowhich 想 tooadd 閘道。 按一下**虛擬網路**tooopen hello**選擇虛擬網路**頁面。 選取 hello VNet。 如果您沒有看到您的 VNet，請確定 hello**位置**欄位指向您的虛擬網路所在的 toohello 區域。
9. **公用 IP 位址**： 建立公用 IP 位址動態指派公用 IP 位址物件 toowhich。 按一下**公用 IP 位址**tooopen hello**選擇公用 IP 位址**頁面。 按一下**+ 建立新**tooopen hello**建立公用 IP 位址頁面**。 輸入公用 IP 位址的名稱。 按一下**確定**toosave 您的變更。 建立 hello VPN 閘道時，會動態指定 hello IP 位址。 VPN 閘道目前僅支援*動態*公用 IP 位址配置。 不過，它並不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。 hello 公用 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。 它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。
10. **訂用帳戶**： 確認該 hello 正確選取訂用帳戶。
11. **資源群組**： 此設定由 hello 您選取的虛擬網路。
12. 不會調整 hello**位置**您所指定 hello 先前的設定之後。
13. 請確認 hello 設定。 如果您希望您的閘道 tooappear hello 儀表板上，您可以選取**Pin toodashboard** hello hello 頁底端。
14. 按一下**建立**toobegin 建立 hello 閘道。 hello 設定會進行驗證，並將部署的 hello 閘道。 建立閘道可能佔用 too45 分鐘。

建立 hello 閘道後，您可以檢視 hello 已被指派 tooit 藉由檢視 hello 虛擬網路的 IP 位址。 hello 閘道會顯示為連接的裝置。 您可以按一下 hello 連接裝置 （您的虛擬網路閘道） tooview 的詳細資訊。
