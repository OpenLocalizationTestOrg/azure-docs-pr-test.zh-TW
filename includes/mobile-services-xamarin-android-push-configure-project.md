
1. Hello 方案檢視中 (或**方案總管] 中**Visual Studio 中)，以滑鼠右鍵按一下 hello**元件**資料夾中，按一下 [**取得多元件...**，搜尋 hello **Google 雲端訊息用戶端**元件並將它加入 toohello 專案。
2. 開啟 hello ToDoActivity.cs 專案檔，然後加入下列 hello 使用陳述式 toohello 類別：
   
        using Gcm.Client;
3. 在 hello **ToDoActivity**類別中，新增下列新的程式碼的 hello: 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    這可讓您從 hello 推入處理常式服務程序的 tooaccess hello 行動用戶端執行個體。
4. 新增下列程式碼 toohello hello **OnCreate**方法之後 hello, **MobileServiceClient**建立：
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

您的 **ToDoActivity** 現在可供新增推送通知。

