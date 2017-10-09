<!--author=alkohli last changed: 08/04/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall 從 hello Azure 入口網站更新

1. 在 hello StorSimple 服務頁面上，選取您的裝置。

    ![選取裝置](./media/storsimple-8000-install-update5-via-portal/update1.png)

2. 瀏覽過**裝置設定** > **裝置更新**。

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update5-via-portal/update2.png)

2. 有新的更新可用時，會顯示通知。 或者，在 hello**裝置更新**刀鋒視窗中，按一下 **掃描更新**。 Tooscan 可用的更新時，會建立一個作業。 Hello 作業順利完成時，會通知您。

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update5-via-portal/update3.png)

3. 我們建議您在裝置上套用更新之前，檢閱 hello 版本資訊。 按一下 tooapply 更新**安裝更新**。 在 hello**確認定期更新**刀鋒視窗中，檢閱 hello 必要條件 toocomplete 然後再套用更新。 選取您已準備好 tooupdate hello 裝置，然後按一下 hello 核取方塊 tooindicate**安裝**。

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update5-via-portal/update4.png)

6. 一組必要條件檢查會隨即開始。 這些檢查包括︰
   
   * **控制器健康情況檢查**tooverify 兩者 hello 裝置控制器皆狀況良好並線上。
   * **硬體元件健康情況檢查**tooverify 所有 hello StorSimple 裝置上的硬體元件均狀況良好。
   * **檢查 DATA 0** tooverify DATA 0 已啟用您的裝置上。 如果未啟用此介面，您必須啟用它，然後重試。

    下載並安裝所有的 hello 檢查成功完成時，才 hello 更新時。 Hello 檢查進行中時，會通知您。 如果 hello prechecks 失敗，您將會提供與 hello 失敗的原因。 解決這些問題，然後再重試 hello 作業。 如果您無法自行解決這些問題，您可能需要 toocontact Microsoft 支援服務。

7. Hello prechecks 成功完成之後，會建立更新工作。 已成功建立 hello 更新工作時，會通知您。
   
    ![建立更新工作](./media/storsimple-8000-install-update5-via-portal/update6.png)
   
    hello 更新然後會套用至您的裝置。

9. hello 更新所需的幾個小時 toocomplete。 選取 hello 更新工作，然後按一下**詳細資料**隨時 hello 工作 tooview hello 詳細資料。

    ![建立更新工作](./media/storsimple-8000-install-update5-via-portal/update8.png)

     您也可以監視 hello 更新作業，從 hello 進度**裝置設定 > 工作**。 在 hello**作業**刀鋒視窗中，您可以看到 hello 更新進度。

     ![建立更新工作](./media/storsimple-8000-install-update5-via-portal/update7.png)

10. Hello 工作完成後，瀏覽 toohello**裝置設定 > 裝置更新**。 現在應該更新 hello 軟體版本。

