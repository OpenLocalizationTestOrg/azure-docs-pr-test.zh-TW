Azure 客戶每月可以解除鎖定 25,000 封免費電子郵件。 這些 25,000 的免費每月電子郵件可讓您存取 tooadvanced 報告和分析和[所有 Api] [ all APIs] （Web、 SMTP、 事件、 剖析等等）。 SendGrid 所提供的其他服務的相關資訊，請造訪 hello [SendGrid 解決方案][ SendGrid Solutions]頁面。

### <a name="toosign-up-for-a-sendgrid-account"></a>toosign SendGrid 帳戶
1. 登入 toohello [Azure 管理入口網站][Azure Management Portal]。
2. 在左側 hello hello 功能表上，按一下**新增**。

    ![command-bar-new][command-bar-new]
3. 依序按一下 [附加元件] 和 [SendGrid 電子郵件傳遞]。

    ![sendgrid-store][sendgrid-store]
4. 完成 hello 註冊表單並選取**建立**。

    ![sendgrid-create][sendgrid-create]
5. 輸入**名稱**tooidentify 您的 SendGrid 服務您的 Azure 設定中。 名稱的長度必須介於 1 到 100 個字元之間，而且只能包含英數字元、連字號、句點和底線。 hello 名稱必須是唯一的訂閱 Azure 市集項目清單中。
6. 輸入並確認您的**密碼**。
7. 選擇您的**訂用帳戶**。
8. 建立新的**資源群組**或使用現有的資源群組。
9. 在 hello**定價層**區段中，選取您想要註冊 toosign hello SendGrid 計劃。

    ![sendgrid-pricing][sendgrid-pricing]
10. 輸入**促銷代碼** (如果有的話)。
11. 輸入**連絡人資訊**。
12. 檢閱並接受 hello**法律條款**。
13. 確認購買之後，您會看到**部署成功**快顯視窗，您會看到您的帳戶列在 hello**所有資源**> 一節。

    ![all-resources][all-resources]

    您已完成購買程序，並按下 hello 之後**管理**按鈕 tooinitiate hello 電子郵件驗證程序，將會收到的電子郵件，詢問您 tooverify SendGrid 從您的帳戶。 如果您未收到這封電子郵件，或者無法驗證您的帳戶，請參閱本常見問題集。

    ![manage][manage]

    **除非您已經驗證您的帳戶，您只可以傳送向上 too100 電子郵件/日。**

    toomodify 您的訂用帳戶方案或 hello SendGrid 連絡設定中，按一下您的 SendGrid 服務 tooopen hello SendGrid Marketplace 儀表板 hello 名稱，請參閱。

    ![settings][settings]

    使用 SendGrid 的電子郵件的 toosend，您必須提供您的 API 金鑰。

### <a name="toofind-your-sendgrid-api-key"></a>toofind SendGrid API 金鑰
1. 按一下 [管理] 。

    ![manage][manage]
2. 在您的 SendGrid 儀表板，選取**設定**然後**API 金鑰**hello hello 左邊的功能表中。

    ![api-keys][api-keys]

3. 按一下 hello**建立 API 金鑰**下拉式清單中選取**一般 API 金鑰**。

    ![general-api-key][general-api-key]
4. 最少提供 hello**此機碼名稱**並提供完整存取權限太**Mail 傳送**選取**儲存**。

    ![access][access]
5. 您的 API 將會在此時顯示一次。 請是確定 toostore 它安全地。

### <a name="toofind-your-sendgrid-credentials"></a>toofind 您的 SendGrid 認證
1. 按一下 hello 索引鍵圖示 toofind 您**Username**。

    ![key][key]
2. 您在安裝程式選擇一個 hello hello 密碼。 您可以選取**變更密碼**或**重設密碼**toomake 的任何變更。

toomanage 您電子郵件傳遞能力設定，請按一下 hello**管理 按鈕**。 這會重新導向 tooyour SendGrid 儀表板。

    ![manage][manage]

    For more information on sending email through SendGrid, visit hello [Email API Overview][Email API Overview].

<!--images-->

[command-bar-new]: ./media/sendgrid-sign-up/new-addon.png
[sendgrid-store]: ./media/sendgrid-sign-up/sendgrid-store.png
[sendgrid-create]: ./media/sendgrid-sign-up/sendgrid-create.png
[sendgrid-pricing]: ./media/sendgrid-sign-up/sendgrid-pricing.png
[all-resources]: ./media/sendgrid-sign-up/all-resources.png
[manage]: ./media/sendgrid-sign-up/manage.png
[settings]: ./media/sendgrid-sign-up/settings.png
[api-keys]: ./media/sendgrid-sign-up/api-keys.png
[general-api-key]: ./media/sendgrid-sign-up/general-api-key.png
[access]: ./media/sendgrid-sign-up/access.png
[key]: ./media/sendgrid-sign-up/key.png

<!--Links-->

[SendGrid Solutions]: https://sendgrid.com/solutions
[Azure Management Portal]: https://manage.windowsazure.com
[SendGrid Getting Started]: http://sendgrid.com/docs
[SendGrid Provisioning Process]: https://support.sendgrid.com/hc/articles/200181628-Why-is-my-account-being-provisioned-
[all APIs]: https://sendgrid.com/docs/API_Reference/index.html
[Email API Overview]: https://sendgrid.com/docs/API_Reference/Web_API_v3/Mail/index.html
