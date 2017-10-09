<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall 從 hello Azure 入口網站更新

1. 在 hello StorSimple 服務頁面上，選取您的裝置。 瀏覽過**裝置** > **維護**。
2. 在 hello hello 頁面底部，按一下**掃描更新**。 Tooscan 可用的更新時，會建立一個作業。 Hello 作業順利完成時，會通知您。
3. 在 hello**軟體更新**區段 hello 相同頁面上，hello 新軟體更新可供使用。 我們建議您在裝置上套用更新之前，檢閱 hello 版本資訊。
4. 在 hello hello 頁面底部，按一下 **安裝更新**，然後**確定**。
5. 在 hello**安裝更新**對話方塊中，請確定您已依照 hello 建議，然後選取 **我了解上述需求的 hello，而且已準備好 tooupgrade 我的裝置**按一下 hello 核取按鈕。
   
    ![確認訊息](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. 一組必要條件檢查會隨即開始。 這些檢查包括︰
   
   * **控制器健康情況檢查**tooverify 兩者 hello 裝置控制器皆狀況良好並線上。
   * **硬體元件健康情況檢查**tooverify 所有 hello StorSimple 裝置上的硬體元件均狀況良好。
   * **檢查 DATA 0** tooverify DATA 0 已啟用您的裝置上。 如果未啟用此介面，您必須啟用它，然後重試。
   * **DATA 2 與 DATA 3 檢查**tooverify DATA 2 和 DATA 3 網路介面不會啟用。 如果已啟用這些介面，然後您必須停用這些然後再試 tooupdate 您的裝置。 只有在您要從執行 GA 軟體的裝置更新時，才需要執行這項檢查。 執行 0.1、0.2 或 0.3 版的裝置將不需要這項檢查。
   * **閘道核取**任何裝置上執行 版本先前 tooUpdate 1。 這項檢查會在執行更新前 1 軟體的所有 hello 裝置上執行，但設定不同於 DATA 0 網路介面閘道的 hello 裝置上會失敗。
     
     如果所有檢查都成功，則會套用 hello 更新。 Hello 檢查進行中時，會通知您。
     
     ![前置檢查通知](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     hello 以下是的範例中的 hello 檢查失敗。 您必須驗證兩個 hello 裝置控制器狀況良好且在線上。 您也需要 toocheck hello hello 硬體元件健全狀況。 在此範例中，需要注意控制器 0 及控制器 1 元件。 如果您無法自行解決這些問題，您可能需要 toocontact Microsoft 支援服務。
     
       ![檢查失敗](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Hello 檢查成功完成之後，會建立更新工作。 已成功建立 hello 更新工作時，會通知您。
   
    ![建立更新工作](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    hello 更新然後會套用至您的裝置。
    
8. hello 更新作業，toomonitor hello 進度按一下**檢視工作**。 在 [hello**作業**] 頁面上，您可以看到 hello 更新進度。
9. hello 更新所需的幾個小時 toocomplete。 選取 hello 更新工作，然後按一下**詳細資料**隨時 hello 工作 tooview hello 詳細資料。
10. Hello 工作完成後，瀏覽 toohello**維護**頁面上，然後向下捲動太**軟體更新**。

