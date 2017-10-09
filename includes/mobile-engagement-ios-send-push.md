### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>授與存取 tooyour 推播憑證 tooMobile Engagement
tooallow Mobile Engagement toosend 推播通知您的身分，您需要 toogrant 它存取 tooyour 憑證。 這是藉由設定和 hello Mobile Engagement 入口網站中輸入您的憑證。 請確定您已取得 .p12 憑證，如 [Apple 的文件](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

1. 瀏覽 tooyour Mobile Engagement 入口網站。 請確定您使用正確的 hello，然後按一下hello **Engage** hello 底部的按鈕：
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. 按一下 hello**設定**Engagement 入口網站頁面。 從該處，按一下 hello**原生推送**區段 tooupload p12 憑證：
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. 選取您的 p12，將它上傳並輸入您的密碼：
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>傳送通知 tooyour 應用程式
現在，我們將建立簡單的推播通知活動，則會傳送推播 tooour 應用程式：

1. 瀏覽 toohello**到達** 索引標籤中您的 Mobile Engagement 入口網站。
2. 按一下**新的 Announcement** toocreate 您的推播宣傳活動
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. 安裝程式 hello 第一個欄位的活動：
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * 提供您的行銷活動 **名稱** 。 
   * 選取 hello**傳遞時間**為**不在應用程式只**： 這是 hello 簡單 Apple 推播通知類型具有一些文字。
   * 在 hello 通知文字中，輸入第一個 hello**標題**供 hello hello 推入中的第一行。
   * 然後輸入您**訊息**供 hello 第二行
4. 向下捲動，並在 hello 內容區段選取**僅限通知**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. 您已完成設定 hello 最基本活動。 現在向下捲動並按一下**建立**按鈕 toosave 您推播通知的活動。 
6. 最後-按一下**Activate** toosend 推播通知。 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. 您可以在 hello 如下的 hello 通知中心收到 hello 通知，在您的 iOS 裝置上：
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. 如果您有搭配此 iOS 裝置的 Apple Watch 您會在 Apple Watch 上看到 hello 通知：
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

