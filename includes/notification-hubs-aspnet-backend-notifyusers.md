## <a name="create-the-webapi-project"></a><span data-ttu-id="d8fe3-101">建立 WebAPI 專案</span><span class="sxs-lookup"><span data-stu-id="d8fe3-101">Create the WebAPI Project</span></span>
<span data-ttu-id="d8fe3-102">新的 ASP.NET WebAPI 後端將會在後續各節中建立，而且有三個主要用途：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="d8fe3-103">**驗證用戶端**：稍後會加入訊息處理常式，以驗證用戶端要求並將使用者與要求產生關聯。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span></span>
2. <span data-ttu-id="d8fe3-104">**用戶端通知註冊**：之後，您將加入一個控制器來處理新的註冊，以便用戶端裝置接收通知。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span></span> <span data-ttu-id="d8fe3-105">經過驗證的使用者名稱會自動加入至註冊作為 [標記](https://msdn.microsoft.com/library/azure/dn530749.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="d8fe3-106">**傳送通知給用戶端**：之後，您也會加入一個控制器，以便使用者對與標記相關聯的裝置和用戶端觸發安全的推播。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span></span> 

<span data-ttu-id="d8fe3-107">下列步驟說明如何建立新的 ASP.NET WebAPI 後端：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-107">The following steps show how to create the new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d8fe3-108">如果您使用 Visual Studio 2015 或更新版本，在開始本教學課程之前，請確定您已安裝最新版本的 NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span></span> <span data-ttu-id="d8fe3-109">若要檢查版本，請啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-109">To check, start Visual Studio.</span></span> <span data-ttu-id="d8fe3-110">在 [工具] 功能表中，按一下 [擴充功能和更新]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-110">From the **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="d8fe3-111">搜尋您的 Visual Studio 版本適用的 **NuGet Package Manager**，然後確定您已安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have the latest version.</span></span> <span data-ttu-id="d8fe3-112">否則的話，請解除安裝，然後重新安裝 NuGet Package Manager。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="d8fe3-113">確定您已安裝 Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) 以供網站部署。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="d8fe3-114">啟動 Visual Studio 或 Visual Studio Express。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="d8fe3-115">按一下 [伺服器總管]  並登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-115">Click **Server Explorer** and sign in to your Azure account.</span></span> <span data-ttu-id="d8fe3-116">Visual Studio 將需要您登入，才能在您的帳戶上建立網站資源。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-116">Visual Studio will need you signed in to create the web site resources on your account.</span></span>
2. <span data-ttu-id="d8fe3-117">在 Visual Studio 中，依序按一下 [檔案]、[新增]、[專案]，展開 [範本]、[Visual C#]，再按一下 [Web] 和 [ASP.NET Web 應用程式]，輸入名稱 **AppBackend**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="d8fe3-118">在 [新增 ASP.NET 專案] 對話方塊中，按一下 [Web API]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="d8fe3-119">在[設定 Microsoft Azure Web 應用程式] 對話方塊中，選擇訂用帳戶，和您已經建立的 [App Service 方案]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="d8fe3-120">您也可以選擇 [建立新的應用程式服務計劃]  ，並從對話方塊建立一個。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-120">You can also choose **Create a new app service plan** and create one from the dialog.</span></span> <span data-ttu-id="d8fe3-121">在此教學課程中您不需要資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="d8fe3-122">一旦您選取您的應用程式服務計劃，按一下 [確定]  來建立專案。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-122">Once you have selected your app service plan, click **OK** to create the project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a><span data-ttu-id="d8fe3-123">向 WebAPI 後端驗證用戶端</span><span class="sxs-lookup"><span data-stu-id="d8fe3-123">Authenticating Clients to the WebAPI Backend</span></span>
<span data-ttu-id="d8fe3-124">在本節中，您將為新的後端建立名為 **AuthenticationTestHandler** 新訊息處理常式類別。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span></span> <span data-ttu-id="d8fe3-125">這個類別衍生自 [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) 並加入為訊息處理常式，以便處理進入後端的所有要求。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span></span> 

1. <span data-ttu-id="d8fe3-126">在 [方案總管] 中，以滑鼠右鍵按一下 [AppBackend] 專案，然後依序按一下 [新增] 和 [類別]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="d8fe3-127">將新類別命名為 **AuthenticationTestHandler.cs**，然後按一下 [新增] 以產生類別。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span></span> <span data-ttu-id="d8fe3-128">為了簡單起見，將使用此類別透過 *基本驗證* 驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="d8fe3-129">請注意，您的應用程式可以使用任何驗證結構描述。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="d8fe3-130">在 AuthenticationTestHandler.cs 中，加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="d8fe3-131">在 AuthenticationTestHandler.cs 中，以下列程式碼取代 `AuthenticationTestHandler` 類別定義。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span></span> 
   
    <span data-ttu-id="d8fe3-132">下列三個條件都成立時，這個處理常式將授權要求：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-132">This handler will authorize the request when the following three conditions are all true:</span></span>
   
   * <span data-ttu-id="d8fe3-133">要求已包含 *授權* 標頭。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-133">The request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="d8fe3-134">要求使用 *基本* 驗證。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-134">The request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="d8fe3-135">使用者名稱字串和密碼字串是相同的字串。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-135">The user name string and the password string are the same string.</span></span>
     
     <span data-ttu-id="d8fe3-136">否則，將會拒絕此要求。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-136">Otherwise, the request will be rejected.</span></span> <span data-ttu-id="d8fe3-137">這不是真正的驗證和授權方法。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="d8fe3-138">這只是本教學課程中一個非常簡單的範例。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="d8fe3-139">如果要求訊息已經由 `AuthenticationTestHandler`驗證及授權，則基本驗證使用者會附加至 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx)上的目前要求。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="d8fe3-140">之後另一個控制器 (RegisterController) 會使用 HttpContext 中的使用者資訊，將 [標記](https://msdn.microsoft.com/library/azure/dn530749.aspx) 新增至通知註冊要求。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span></span>
     
       <span data-ttu-id="d8fe3-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="d8fe3-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach the new principal object to the current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       <span data-ttu-id="d8fe3-142">}</span><span class="sxs-lookup"><span data-stu-id="d8fe3-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="d8fe3-143">**安全性注意事項`AuthenticationTestHandler`：** 類別未提供真正的驗證。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="d8fe3-144">它僅可用於模仿基本驗證而且並不安全。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-144">It is used only to mimic basic authentication and is not secure.</span></span> <span data-ttu-id="d8fe3-145">您必須在生產應用程式和服務中實作安全的驗證機制。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="d8fe3-146">在 **App_Start/WebApiConfig.cs** 類別中 `Register` 方法的結尾加入下列程式碼以註冊訊息處理常式：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="d8fe3-147">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-the-webapi-backend"></a><span data-ttu-id="d8fe3-148">使用 WebAPI 後端註冊通知</span><span class="sxs-lookup"><span data-stu-id="d8fe3-148">Registering for Notifications using the WebAPI Backend</span></span>
<span data-ttu-id="d8fe3-149">在本節中，我們會將新的控制器加入至 WebAPI 後端來處理要求，以使用通知中樞的用戶端程式庫，為使用者和裝置註冊通知。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span></span> <span data-ttu-id="d8fe3-150">控制器將會對已由 `AuthenticationTestHandler`驗證並附加至 HttpContext 的使用者，新增使用者標記。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span></span> <span data-ttu-id="d8fe3-151">此標記會有以下字串格式： `"username:<actual username>"`。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-151">The tag will have the string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="d8fe3-152">在 [方案總管] 中，以滑鼠右鍵按一下 [AppBackend] 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="d8fe3-153">按一下左側的 [線上]，並在 [搜尋] 方塊中搜尋 **Microsoft.Azure.NotificationHubs**。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span></span>
3. <span data-ttu-id="d8fe3-154">按一下結果清單中的 [Microsoft Azure 通知中樞]，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="d8fe3-155">請完成安裝，然後關閉 [NuGet Package Manager] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-155">Complete the installation, then close the NuGet package manager window.</span></span>
   
    <span data-ttu-id="d8fe3-156">這會使用 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 封裝</a>加入對 Azure 通知中樞 SDK 的參考。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="d8fe3-157">我們現在將建立新的類別檔案，代表與用來傳送通知的通知中樞間的連接。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span></span> <span data-ttu-id="d8fe3-158">在 [方案總管] 中，於以滑鼠右鍵按一下 **Models** 資料夾上，按一下 [新增]，然後按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="d8fe3-159">將新類別命名為 **Notifications.cs**，然後按一下 [新增] 以產生類別。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="d8fe3-160">在 Notifications.cs 中，將下列 `using` 陳述式新增在檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-160">In Notifications.cs, add the following `using` statement at the top of the file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="d8fe3-161">以下列內容取代 `Notifications` 類別定義，並確定以通知中樞的連接字串 (含完整存取權) 和中心名稱 (可在 [Azure 傳統入口網站](http://manage.windowsazure.com)取代) 取代兩個預留位置：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="d8fe3-162">接下來我們將建立名為 **RegisterController** 的新控制器。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="d8fe3-163">在 [方案總管] 中，以滑鼠右鍵按一下 **Controllers** 資料夾，然後按一下 [新增]，再按一下 [控制器]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="d8fe3-164">按一下 [Web API 2 控制器 -- 空白] 項目，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="d8fe3-165">將新類別命名為 **RegisterController**，然後再次按一下 [新增] 以產生控制器。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="d8fe3-166">在 RegisterController.cs 中，加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-166">In RegisterController.cs, add the following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="d8fe3-167">在 `RegisterController` 類別定義中加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-167">Add the following code inside the `RegisterController` class definition.</span></span> <span data-ttu-id="d8fe3-168">請注意，在此程式碼中，我們會為已附加至 HttpContext 的使用者新增使用者標記。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span></span> <span data-ttu-id="d8fe3-169">我們新增的訊息篩選器 `AuthenticationTestHandler`會驗證此使用者並附加至 HttpContext。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="d8fe3-170">您也可以新增選擇性檢查，以驗證使用者是否有權註冊所要求的標籤。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span></span>
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at the specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed to add these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. <span data-ttu-id="d8fe3-171">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-171">Save your changes.</span></span>

## <a name="sending-notifications-from-the-webapi-backend"></a><span data-ttu-id="d8fe3-172">從 WebAPI 後端傳送通知</span><span class="sxs-lookup"><span data-stu-id="d8fe3-172">Sending Notifications from the WebAPI Backend</span></span>
<span data-ttu-id="d8fe3-173">在本節中，您會加入新的控制器，以便用戶端裝置使用 ASP.NET WebAPI 後端中的 Azure 通知中樞服務管理程式庫，根據使用者名稱標記傳送通知。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="d8fe3-174">建立另一個名為 **NotificationsController**的新控制器。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="d8fe3-175">以您在上一節中建立 **RegisterController** 的相同方式來建立新控制器。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-175">Create it the same way you created the **RegisterController** in the previous section.</span></span>
2. <span data-ttu-id="d8fe3-176">在 NotificationsController.cs 中，加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="d8fe3-176">In NotificationsController.cs, add the following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="d8fe3-177">在 **NotificationsController** 類別中新增下列方法。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-177">Add the following method to the **NotificationsController** class.</span></span>
   
    <span data-ttu-id="d8fe3-178">此程式碼會傳送以平台通知服務 (PNS) `pns` 參數為基礎的通知類型。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="d8fe3-179">`to_tag` 的值用來設定訊息上的 *username* 標記。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-179">The value of `to_tag` is used to set the *username* tag on the message.</span></span> <span data-ttu-id="d8fe3-180">此標記必須符合作用中通知中樞註冊的使用者名稱標記。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="d8fe3-181">通知訊息是取自 POST 要求主體，並針對目標 PNS 格式化。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span></span> 
   
    <span data-ttu-id="d8fe3-182">根據您的支援裝置用來接收通知的平台通知服務 (PNS)，使用不同的格式可支援不同的通知。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="d8fe3-183">例如在 Windows 裝置上，您可以搭配 WNS 使用不受其他 PNS 直接支援的 [快顯通知](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="d8fe3-184">因此您的後端必須針對您想要支援的裝置 PNS，將通知格式化為支援的通知。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span></span> <span data-ttu-id="d8fe3-185">然後在 [NotificationHubClient 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="d8fe3-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. <span data-ttu-id="d8fe3-186">按 **F5** 鍵以執行應用程式，並確保工作到目前為止的準確性。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span></span> <span data-ttu-id="d8fe3-187">應用程式應即啟動網頁瀏覽器，並顯示 ASP.NET 首頁。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-187">The app should launch a web browser and display the ASP.NET home page.</span></span> 

## <a name="publish-the-new-webapi-backend"></a><span data-ttu-id="d8fe3-188">發佈新的 WebAPI 後端</span><span class="sxs-lookup"><span data-stu-id="d8fe3-188">Publish the new WebAPI Backend</span></span>
1. <span data-ttu-id="d8fe3-189">為了可以從所有裝置存取此應用程式，我們現在可以將它部署到 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="d8fe3-190">以滑鼠右鍵按一下 **AppBackend** 專案，然後選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-190">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="d8fe3-191">選取 [Microsoft Azure App Service] 作為發佈目標，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="d8fe3-192">這會開啟 [建立 App Service] 對話方塊，協助您建立在 Azure 中執行 ASP.NET Web 應用程式所需的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-192">This opens the Create App Service dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="d8fe3-193">在 [建立 App Service] 對話方塊中，選取您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-193">In the **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="d8fe3-194">按一下 [變更類型] 並選取 [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="d8fe3-195">保留指定的 [Web 應用程式名稱] 並選取 [訂用帳戶]、[資源群組] 和 [App Service 方案]。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-195">Keep the **Web App Name** given and select the **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="d8fe3-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-196">Click **Create**.</span></span>

4. <span data-ttu-id="d8fe3-197">記下 [摘要] 區段中的 [網站 URL] 屬性。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-197">Make a note of the **Site URL** property in the **Summary** section.</span></span> <span data-ttu-id="d8fe3-198">我們後續將在本教學課程中參考此 URL 作為您的 *後端端點* 。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-198">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="d8fe3-199">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-199">Click **Publish**.</span></span>

5. <span data-ttu-id="d8fe3-200">精靈完成後，它會將 ASP.NET Web 應用程式發佈至 Azure，然後在預設瀏覽器中啟動該應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-200">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>  <span data-ttu-id="d8fe3-201">您的應用程式將可在 Azure App Service 中檢視。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="d8fe3-202">URL 會使用您稍早指定的 Web 應用程式名稱，其格式為 http://<app_name>.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="d8fe3-202">The URL uses the web app name that you specified earlier, with the format http://<app_name>.azurewebsites.net.</span></span>

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
