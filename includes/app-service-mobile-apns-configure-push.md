

1. 在您的 Mac 上啟動 **Keychain Access**。 於 hello 上左導覽列中，在**類別**，開啟**My 憑證**。 找出您下載 hello 前一節中的 hello SSL 憑證，並公開其內容。 選取只 hello 憑證 （未選取 hello 私密金鑰），和[將它匯出](https://support.apple.com/kb/PH20122?locale=en_US)。
2. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **瀏覽所有** > **應用程式服務**，按一下您的行動應用程式後端。 在 [設定] 中，按一下 [App Service 推播]，然後按一下通知中樞名稱。 跳過**Apple 推播通知服務** > **上傳憑證**。 上傳 hello.p12 檔案，選取正確的 hello**模式**（根據您的用戶端 SSL 憑證與前面的是否為生產環境或沙箱）。 儲存任何變更。

您的服務現在是使用推播通知，在 iOS 上設定的 toowork。

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
