## <a name="what-are-service-bus-topics-and-subscriptions"></a>什麼是服務匯流排主題和訂用帳戶？
服務匯流排主題和訂用帳戶支援「發佈/訂閱」  訊息通訊模型。 使用主題和訂用帳戶時，分散式應用程式的元件彼此不直接通訊，相反的，他們會透過扮演中繼角色的主題來交換訊息。

![主題概念](./media/howto-service-bus-topics/sb-topics-01.png)

有別於服務匯流排佇列，服務匯流排佇列中的每個訊息只會由單一取用者處理，主題和訂用帳戶採用發佈/訂用帳戶模式，提供一對多的通訊形式。 就可以註冊多個訂用帳戶 tooa 主題。 當訊息傳送 tooa 主題時，它就可使用可用 tooeach 訂用帳戶 toohandle/處理序分開。

訂用帳戶 tooa 主題類似於虛擬佇列，可接收 toohello 主題傳送 hello 訊息複本。 （選擇性），您可以註冊以每個訂用帳戶為基礎，可讓您 toofilter 主題的篩選規則，或限制的主題訂用帳戶所收到的訊息 tooa 主題。

服務匯流排主題和訂閱 tooscale 可讓您和跨許多使用者和應用程式處理非常大量的訊息。

## <a name="create-a-namespace"></a>建立命名空間
toobegin 使用服務匯流排主題和訂用帳戶在 Azure 中，您必須先建立*服務命名空間*。 命名空間提供範圍容器，可在應用程式內定址服務匯流排資源。

toocreate 命名空間：

1. 登入 toohello [Azure 入口網站][Azure portal]。
2. 在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，然後按一下**企業整合**，然後按一下 **Service Bus**。
3. 在 [hello**建立命名空間**] 對話方塊中，輸入命名空間名稱。 hello 系統立即檢查 toosee hello 名稱是否可用。
4. 提供讓確定 hello 命名空間名稱之後，選擇定價層 （Basic、 Standard 或 Premium） 中的 hello。
5. 在 hello**訂用帳戶**欄位中，選擇哪些 toocreate hello 命名空間中的 Azure 訂用帳戶。
6. 在 hello**資源群組**欄位中，選擇現有的資源群組中的 hello 命名空間將 live、 或另外新建一個。      
7. 在**位置**，選擇 hello 國家或地區，應該在其中裝載您的命名空間。
   
    ![建立命名空間][create-namespace]
8. 按一下 hello**建立** 按鈕。 hello 系統現在建立您的命名空間，並啟用它。 您可能需要幾分鐘的時間為 hello 系統佈建資源帳戶 toowait。

### <a name="obtain-hello-credentials"></a>取得 hello 認證
1. 在 [hello] 清單中的命名空間，hello 新建立的命名空間名稱。
2. 在 hello**服務匯流排命名空間**刀鋒視窗中，按一下 **共用存取原則**。
3. 在 hello**共用存取原則**刀鋒視窗中，按一下  **RootManageSharedAccessKey**。
   
    ![connection-info][connection-info]
4. 在 hello**原則： RootManageSharedAccessKey**刀鋒視窗中，按一下 hello 複製 按鈕旁邊太**連接字串對主索引鍵**，toocopy hello 連接字串 tooyour 剪貼簿供稍後使用。
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


