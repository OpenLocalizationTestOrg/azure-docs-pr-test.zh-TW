
1. <span data-ttu-id="82ebb-101">在 [方案] 檢視 (或 Visual Studio 中的 [方案總管]) 中，以滑鼠右鍵按一下 [元件] 資料夾，按一下 [取得更多元件]，搜尋 **Google 雲端通訊用戶端**並將其加入至專案。</span><span class="sxs-lookup"><span data-stu-id="82ebb-101">In the Solution view (or **Solution Explorer** in Visual Studio), right-click the **Components** folder, click  **Get More Components...**, search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>
2. <span data-ttu-id="82ebb-102">開啟 ToDoActivity.cs 專案檔案，然後將下列 using 陳述式加入至類別：</span><span class="sxs-lookup"><span data-stu-id="82ebb-102">Open the ToDoActivity.cs project file and add the following using statement to the class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="82ebb-103">將下列新程式碼加入至 **ToDoActivity** 類別：</span><span class="sxs-lookup"><span data-stu-id="82ebb-103">In the **ToDoActivity** class, add the following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return the current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return the Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="82ebb-104">這樣做可讓您從推播處理常式服務處理程序存取行動服務用戶端執行個體。</span><span class="sxs-lookup"><span data-stu-id="82ebb-104">This enables you to access the mobile client instance from the push handler service process.</span></span>
4. <span data-ttu-id="82ebb-105">在建立 **MobileServiceClient** 之後，將下列程式碼加入至 **OnCreate** 方法：</span><span class="sxs-lookup"><span data-stu-id="82ebb-105">Add the following code to the **OnCreate** method, after the **MobileServiceClient** is created:</span></span>
   
       // Set the current instance of TodoActivity.
       instance = this;
   
       // Make sure the GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register the app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="82ebb-106">您的 **ToDoActivity** 現在可供新增推送通知。</span><span class="sxs-lookup"><span data-stu-id="82ebb-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

