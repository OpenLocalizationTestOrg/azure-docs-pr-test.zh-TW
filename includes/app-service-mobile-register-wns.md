
1. 在 Visual Studio 方案總管 中，請在 hello Windows 市集應用程式專案，以滑鼠右鍵按一下，然後按一下**存放區** > **將應用程式建立關聯以 hello 存放區**。

    ![建立應用程式與 Windows 市集的關聯](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. 在 hello 精靈 中，按一下 **下一步**，並以您的 Microsoft 帳戶登入。 在 保留應用程式名稱 中輸入應用程式名稱，然後按一下保留。
3. Hello 應用程式註冊已成功建立，請選取 hello 新應用程式名稱後，請按一下**下一步**，然後按一下**關聯**。 這會將所需的 hello Windows 市集註冊資訊 toohello 應用程式資訊清單。
4. 重複步驟 1 和 3 hello Windows Phone 市集應用程式專案，使用 hello 您先前建立 hello Windows 市集應用程式相同的登錄。  
5. 瀏覽 toohello [Windows 開發人員中心](https://dev.windows.com/en-us/overview)，並以您的 Microsoft 帳戶登入。 按一下 在 hello 新應用程式註冊**我的應用程式**，然後展開**服務** > **推播通知**。
6. 在 hello**推播通知**頁面上，按一下**Live 服務 」 站台**下**Windows 推播通知服務 (WNS) 和 Microsoft Azure 行動應用程式**。 請記下的 hello hello 值**封裝 SID**和 hello*目前*值**應用程式密碼**。 

    ![Hello 開發人員中心的應用程式設定](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > hello 應用程式密碼和封裝 SID 是重要的安全性認證。 請勿與任何人共用這些值，或與您的應用程式一起散發密碼。
   >
   >
