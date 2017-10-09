
1. 按一下 hello**應用程式服務**按鈕，選取您的行動應用程式後端，選取**快速入門**，然後選取您用戶端平台 (iOS、 Android、 Xamarin、 Cordova)。

    ![已醒目提示 [Mobile Apps 快速入門] 的 Azure 入口網站][quickstart]

2. 如果未設定資料庫連接，建立執行 hello 下列其中一個：

    ![使用行動應用程式連接 toodatabase azure 入口網站][connect]

    a. 建立新的 SQL Database 和伺服器。

    ![內含 Mobile Apps 建立新資料庫和伺服器的 Azure 入口網站][server]

    b. 請等到 hello 資料連接已成功建立。

    ![成功建立資料連線的 Azure 入口網站通知][notification]

    c. 資料連線必須成功。

    ![Azure 入口網站通知：「您已經有資料連線」][already-connection]

3. 在 **2.建立資料表 API** 之下，選取 Node.js 作為**後端語言**。 
 
4. 接受 hello 通知，然後選取 **建立 TodoItem 資料表**。  
    這會在您的資料庫中建立新的待辦事項資料表。 

    >[!IMPORTANT]
    > 切換現有的後端 tooNode.js 會覆寫所有內容。 相反地，請參閱.NET 後端 toocreate[與 hello.NET 後端伺服器 SDK 用於行動裝置應用程式][instructions]。

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
