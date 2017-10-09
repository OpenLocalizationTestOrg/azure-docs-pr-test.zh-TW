
1. <span data-ttu-id="ab7ad-101">按一下 hello**應用程式服務**按鈕，選取您的行動應用程式後端，選取**快速入門**，然後選取您用戶端平台 (iOS、 Android、 Xamarin、 Cordova)。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![已醒目提示 [Mobile Apps 快速入門] 的 Azure 入口網站][quickstart]

2. <span data-ttu-id="ab7ad-103">如果未設定資料庫連接，建立執行 hello 下列其中一個：</span><span class="sxs-lookup"><span data-stu-id="ab7ad-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![使用行動應用程式連接 toodatabase azure 入口網站][connect]

    <span data-ttu-id="ab7ad-105">a.</span><span class="sxs-lookup"><span data-stu-id="ab7ad-105">a.</span></span> <span data-ttu-id="ab7ad-106">建立新的 SQL Database 和伺服器。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-106">Create a new SQL database and server.</span></span>

    ![內含 Mobile Apps 建立新資料庫和伺服器的 Azure 入口網站][server]

    <span data-ttu-id="ab7ad-108">b.</span><span class="sxs-lookup"><span data-stu-id="ab7ad-108">b.</span></span> <span data-ttu-id="ab7ad-109">請等到 hello 資料連接已成功建立。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-109">Wait until hello data connection is successfully created.</span></span>

    ![成功建立資料連線的 Azure 入口網站通知][notification]

    <span data-ttu-id="ab7ad-111">c.</span><span class="sxs-lookup"><span data-stu-id="ab7ad-111">c.</span></span> <span data-ttu-id="ab7ad-112">資料連線必須成功。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-112">Data connection must be successful.</span></span>

    ![Azure 入口網站通知：「您已經有資料連線」][already-connection]

3. <span data-ttu-id="ab7ad-114">在 **2.建立資料表 API** 之下，選取 Node.js 作為**後端語言**。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="ab7ad-115">接受 hello 通知，然後選取 **建立 TodoItem 資料表**。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="ab7ad-116">這會在您的資料庫中建立新的待辦事項資料表。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="ab7ad-117">切換現有的後端 tooNode.js 會覆寫所有內容。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="ab7ad-118">相反地，請參閱.NET 後端 toocreate[與 hello.NET 後端伺服器 SDK 用於行動裝置應用程式][instructions]。</span><span class="sxs-lookup"><span data-stu-id="ab7ad-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
