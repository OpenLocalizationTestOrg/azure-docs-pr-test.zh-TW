使用服務匯流排 toobegin 排入佇列，在 Azure 中，您必須先使用 Azure 中是唯一的名稱建立命名空間。 命名空間提供範圍容器，可在應用程式內定址服務匯流排資源。

toocreate 命名空間：

1. 登入 toohello [Azure 入口網站][Azure portal]。
2. 在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，然後按一下**企業整合**，然後按一下 **Service Bus**。
3. 在 [hello**建立命名空間**] 對話方塊中，輸入命名空間名稱。 hello 系統立即檢查 toosee hello 名稱是否可用。
4. 提供讓確定 hello 命名空間名稱之後，選擇定價層 （Basic、 Standard 或 Premium） 中的 hello。
5. 在 hello**訂用帳戶**欄位中，選擇哪些 toocreate hello 命名空間中的 Azure 訂用帳戶。
6. 在 hello**資源群組**欄位中，選擇現有的資源群組中的 hello 命名空間將 live、 或另外新建一個。      
7. 在**位置**，選擇 hello 國家或地區，應該在其中裝載您的命名空間。
   
    ![建立命名空間][create-namespace]
8. 按一下 [建立] 。 hello 系統現在建立您的命名空間，並啟用它。 您可能需要幾分鐘的時間為 hello 系統佈建資源帳戶 toowait。

### <a name="obtain-hello-management-credentials"></a>取得 hello 管理認證

1. 在 [hello] 清單中的命名空間，hello 新建立的命名空間名稱。
2. 在 hello 命名空間刀鋒視窗中，按一下 **共用存取原則**。
3. 在 hello**共用存取原則**刀鋒視窗中，按一下  **RootManageSharedAccessKey**。
   
    ![connection-info][connection-info]
4. 在 hello**原則： RootManageSharedAccessKey**刀鋒視窗中，按一下 hello 複製 按鈕旁邊太**連接字串對主索引鍵**，toocopy hello 連接字串 tooyour 剪貼簿供稍後使用。 將此值貼到記事本或一些其他暫存位置。
   
    ![connection-string][connection-string]

5. 重複的 hello 先前步驟中，複製並貼上的 hello 值**主索引鍵**tooa 暫存位置，供日後使用。

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
