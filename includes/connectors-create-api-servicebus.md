### <a name="prerequisites"></a>必要條件
您必須具有[服務匯流排](https://azure.microsoft.com/services/service-bus/)帳戶。  

您可以在邏輯應用程式中使用 Azure 服務匯流排帳戶之前，您必須授權 hello 邏輯應用程式 tooconnect tooyour 服務匯流排帳戶。 幸運的是，您可以輕鬆地在 hello Azure 入口網站上的應用程式邏輯中。  

以下是您的邏輯應用程式 tooconnect tooyour Service Bus 帳戶 hello 步驟 tooauthorize:  

1. toocreate hello 邏輯應用程式的設計工具，在連線 tooService 匯流排上，選取**顯示 Microsoft managed Api** hello 下拉式清單中。 然後輸入**服務匯流排**hello [搜尋] 方塊中。 選取 hello 觸發程序或 toouse 要執行的動作。  
    ![服務匯流排連線圖像 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. 如果您尚未建立任何連線 tooService 匯流排之前，您將會提示的 tooprovide 服務匯流排認證。 這些認證是使用的 tooauthorize 您邏輯應用程式 tooconnect tooand 存取您的服務匯流排帳戶資料。 hello Service Bus 連接器必須 hello 連接字串 hello 服務匯流排命名空間。 它也需要**管理**權限。 如果您的連接字串 hello 命名空間或特定的實體是它是否包含 hello 的好方法 tooknow`EntityPath`參數。 如果是的話，它不 hello 邏輯應用程式的權限的連接字串。  
    ![服務匯流排連接字串](./media/connectors-create-api-servicebus/connectionstring.png)
3. 在收到 hello hello 命名空間的連接字串之後，您可以使用它的 hello 邏輯應用程式中的應用程式開發介面連接。  
    ![服務匯流排連線圖像 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. 請注意 hello 連線已建立，而且現在可用以 hello 其他 tooproceed 邏輯應用程式中的步驟。  
    ![服務匯流排連線圖像 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

