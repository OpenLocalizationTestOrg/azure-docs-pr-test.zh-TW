1. 在 hello hello 入口網站頁面的左側，按一下   **+** 在搜尋中輸入虛擬網路閘道 '。 在 [結果] 中，找出並按一下 [虛擬網路閘道]。
2. 在 hello hello '虛擬網路閘道' 刀鋒視窗底部，按一下 **建立**。 這會開啟 hello**建立虛擬網路閘道**刀鋒視窗。

    ![建立虛擬網路閘道刀鋒視窗欄位](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "新增閘道")

3. 在 hello**建立虛擬網路閘道**刀鋒視窗中，指定您的虛擬網路閘道的 hello 值。

  - **名稱**：為您的閘道命名。 這不是 hello 與命名閘道子網路相同。 它的 hello 您所建立的 hello 閘道物件名稱。
  - 閘道類型︰選取 [VPN]。 VPN 閘道使用 hello 虛擬網路閘道類型**VPN**。 
  - **VPN 類型**： 選取您的組態所指定的 hello VPN 類型。 大部分組態需要路由式 VPN 類型。
  - **SKU**： 從 hello 下拉式清單中選取 hello 閘道 SKU。 列出在 hello 下拉式清單中的 hello Sku hello 您所選取的 VPN 類型而定。 如需閘道 SKU 的詳細資訊，請參閱[閘道 SKU](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku)。
  - **位置**： 您可能需要 tooscroll toosee 位置。 調整 hello**位置**欄位 toopoint toohello 位置虛擬網路所在的位置。 Hello 位置並未指向 toohello 區域虛擬網路所在的位置，如果 hello 虛擬網路不會出現在下一個步驟的 hello '選擇的虛擬網路' 下拉式清單。
  - **虛擬網路**： 選擇 hello 虛擬網路 toowhich 想 tooadd 此閘道。 按一下**虛擬網路**tooopen hello '選擇的虛擬網路' 刀鋒視窗。 選取 hello VNet。 如果您沒有看到您的 VNet，請確定 hello 位置欄位指向您的虛擬網路所在的 toohello 區域。
  - **公用 IP 位址**: hello 建立公用 IP 位址 刀鋒視窗中建立公用 IP 位址物件。 建立 hello VPN 閘道時，會動態指定 hello 公用 IP 位址。 VPN 閘道目前僅支援*動態*公用 IP 位址配置。 不過，這不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。 hello 公用 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。 它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。

    - 首先，請按一下**公用 IP 位址**tooopen hello '選擇公用 IP 位址' 刀鋒視窗中，然後按一下 **+ 建立新**tooopen hello 建立公用 IP 位址 刀鋒視窗。
    - 接下來，輸入**名稱**公用 IP 位址，然後按一下**確定**在 hello 這個刀鋒視窗 toosave 底部 您的變更。

      ![建立公用 IP](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "建立 PIP")

4. 請確認 hello 設定。 您可以選取**Pin toodashboard**底部 hello hello 刀鋒視窗，如果您想要您的閘道 tooappear hello 儀表板上。 
5. 按一下**建立**toobegin 建立 hello VPN 閘道。 hello 設定將會驗證，而且您將會看見 hello hello 儀表板上的磚的 「 部署虛擬網路閘道 」。 建立閘道可能佔用 too45 分鐘。 您可能需要 toorefresh 入口網站頁面 toosee hello 完成狀態。

建立 hello 閘道後，檢視 hello 已被指派 tooit 藉由查看 hello hello 入口網站中的虛擬網路的 IP 位址。 hello 閘道將會顯示為連接的裝置。 您可以按一下 hello 連接裝置 （您的虛擬網路閘道） tooview 的詳細資訊。
