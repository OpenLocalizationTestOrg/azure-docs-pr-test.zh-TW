
1. <span data-ttu-id="2719b-101">按一下**應用程式服務**按鈕，選取您的行動應用程式後端，選取**快速入門**，然後選取您用戶端平台 (iOS、 Android、 Xamarin、 Cordova)。</span><span class="sxs-lookup"><span data-stu-id="2719b-101">Click the **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Azure 入口網站以反白顯示的行動應用程式快速入門][quickstart]

2. <span data-ttu-id="2719b-103">如果未設定資料庫連接，建立一個由執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="2719b-103">If a database connection is not configured, create one by doing the following:</span></span>

    ![Azure 入口網站中使用行動應用程式連接資料庫][connect]

    <span data-ttu-id="2719b-105">a.</span><span class="sxs-lookup"><span data-stu-id="2719b-105">a.</span></span> <span data-ttu-id="2719b-106">建立新的 SQL 資料庫和伺服器。</span><span class="sxs-lookup"><span data-stu-id="2719b-106">Create a new SQL database and server.</span></span>

    ![與行動應用程式的 azure 入口網站建立新的資料庫和伺服器][server]

    <span data-ttu-id="2719b-108">b.</span><span class="sxs-lookup"><span data-stu-id="2719b-108">b.</span></span> <span data-ttu-id="2719b-109">等到成功建立資料連線為止。</span><span class="sxs-lookup"><span data-stu-id="2719b-109">Wait until the data connection is successfully created.</span></span>

    ![成功建立資料連接的 azure 入口網站的通知][notification]

    <span data-ttu-id="2719b-111">c.</span><span class="sxs-lookup"><span data-stu-id="2719b-111">c.</span></span> <span data-ttu-id="2719b-112">資料連線必須成功。</span><span class="sxs-lookup"><span data-stu-id="2719b-112">Data connection must be successful.</span></span>

    ![Azure 入口網站的通知，「 您已經有資料連接 」][already-connection]

3. <span data-ttu-id="2719b-114">在 **2.建立資料表 API** 之下，選取 Node.js 作為**後端語言**。</span><span class="sxs-lookup"><span data-stu-id="2719b-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="2719b-115">接受通知，然後選取 **建立 TodoItem 資料表**。</span><span class="sxs-lookup"><span data-stu-id="2719b-115">Accept the acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="2719b-116">這個動作會在資料庫中建立新的待辦項目資料表。</span><span class="sxs-lookup"><span data-stu-id="2719b-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="2719b-117">現有的後端切換到 Node.js，就會覆寫所有內容。</span><span class="sxs-lookup"><span data-stu-id="2719b-117">Switching an existing back end to Node.js overwrites all contents.</span></span> <span data-ttu-id="2719b-118">若要改為建立的.NET 後端，請參閱[搭配行動應用程式的.NET 後端伺服器 SDK][instructions]。</span><span class="sxs-lookup"><span data-stu-id="2719b-118">To create a .NET back end instead, see [Work with the .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
