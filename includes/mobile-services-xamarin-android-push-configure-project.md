
1. <span data-ttu-id="6fda7-101">Hello 方案檢視中 (或**方案總管] 中**Visual Studio 中)，以滑鼠右鍵按一下 hello**元件**資料夾中，按一下 [**取得多元件...**，搜尋 hello **Google 雲端訊息用戶端**元件並將它加入 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="6fda7-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="6fda7-102">開啟 hello ToDoActivity.cs 專案檔，然後加入下列 hello 使用陳述式 toohello 類別：</span><span class="sxs-lookup"><span data-stu-id="6fda7-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="6fda7-103">在 hello **ToDoActivity**類別中，新增下列新的程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6fda7-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
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
   
    <span data-ttu-id="6fda7-104">這可讓您從 hello 推入處理常式服務程序的 tooaccess hello 行動用戶端執行個體。</span><span class="sxs-lookup"><span data-stu-id="6fda7-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="6fda7-105">新增下列程式碼 toohello hello **OnCreate**方法之後 hello, **MobileServiceClient**建立：</span><span class="sxs-lookup"><span data-stu-id="6fda7-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="6fda7-106">您的 **ToDoActivity** 現在可供新增推送通知。</span><span class="sxs-lookup"><span data-stu-id="6fda7-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

