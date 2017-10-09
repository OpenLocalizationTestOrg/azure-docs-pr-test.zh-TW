### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>授與 Mobile Engagement 存取 tooyour GCM API 金鑰
tooallow Mobile Engagement toosend 推播通知您的身分，您需要 toogrant 它存取 tooyour API 金鑰。 這是藉由設定和 hello Mobile Engagement 入口網站中輸入您的金鑰。

1. 從 Azure 傳統入口網站，請確定您在 hello 應用程式，我們要使用此專案中，，然後按一下hello **Engage** hello 底部的按鈕：
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. 然後按一下 hello**設定** -> **原生推送**區段 tooenter GCM 金鑰：
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. 按一下 hello**編輯**前面圖示**API 金鑰**在 hello **GCM 設定**區段如下所示：
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. Hello 快顯視窗，在貼 hello 您之前取得 GCM 伺服器金鑰，然後再按一下**確定**。
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>傳送通知 tooyour 應用程式
現在，我們將建立簡單的推播通知活動所傳送的推播通知 tooour 應用程式。

1. 瀏覽 toohello**到達** 索引標籤中您的 Mobile Engagement 入口網站。
2. 按一下**新的 announcement** toocreate 您推播通知的活動。
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. 設定您的活動，透過下列步驟的 hello hello 第一個欄位：
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. 為您的活動命名。
   
    b. 選取 hello**傳遞類型**為*系統通知]-> [簡單*： 這是功能標題和小型的一行文字的 hello 簡單 Android 推播通知類型。
   
    c. 選取**傳遞時間**為*隨時*tooallow hello 應用程式 tooreceive 通知，是否 hello 應用程式會啟動與否。
   
    d. 在 hello 通知文字型別 hello**標題**，將會以粗體顯示在 hello 推入。
   
    e. 然後輸入您的 [訊息]。
4. 向下捲動，在 hello**內容**區段中，選取**僅限通知**。
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. 您已完成設定 hello 最基本活動可能。 現在，向下捲動並按一下 hello**建立**按鈕 toosave 您的活動。
6. 最後一個步驟： 按一下**Activate** tooactivate 活動 toosend 推播通知。
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

