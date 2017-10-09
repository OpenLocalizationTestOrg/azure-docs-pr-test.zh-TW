## <a name="create-hello-webapi-project"></a><span data-ttu-id="4c596-101">建立 hello WebAPI 專案</span><span class="sxs-lookup"><span data-stu-id="4c596-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="4c596-102">Hello 以下各節中建立新的 ASP.NET WebAPI 後端，而且會有三個主要用途：</span><span class="sxs-lookup"><span data-stu-id="4c596-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="4c596-103">**驗證用戶端**： 更新 tooauthenticate 用戶端要求和關聯的 hello 與 hello 要求的使用者，將會加入訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="4c596-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="4c596-104">**用戶端通知註冊**： 之後，您將加入新的用戶端裝置 tooreceive 通知註冊控制器 toohandle。</span><span class="sxs-lookup"><span data-stu-id="4c596-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="4c596-105">hello 已驗證的使用者名稱會自動加入做為 toohello 註冊[標記](https://msdn.microsoft.com/library/azure/dn530749.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4c596-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="4c596-106">**傳送通知 tooClients**： 更新版本中，您也會加入控制器 tooprovide 方法，讓使用者 tootrigger 安全發送 toodevices 和與 hello 標籤相關聯的用戶端。</span><span class="sxs-lookup"><span data-stu-id="4c596-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="4c596-107">hello 下列步驟顯示如何 toocreate hello 新的 ASP.NET WebAPI 後端：</span><span class="sxs-lookup"><span data-stu-id="4c596-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4c596-108">如果您使用 Visual Studio 2015 或更早版本，再開始本教學課程，請確定您已安裝的 NuGet 套件管理員 hello hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="4c596-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="4c596-109">toocheck 啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4c596-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="4c596-110">從 hello**工具**功能表上，按一下 **擴充功能和更新**。</span><span class="sxs-lookup"><span data-stu-id="4c596-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="4c596-111">搜尋**NuGet 套件管理員**您版本的 Visual Studio 中，並確定您擁有 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="4c596-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="4c596-112">如果沒有，請解除安裝，然後再重新安裝 hello NuGet 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="4c596-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="4c596-113">請確定您已安裝 Visual Studio hello [Azure SDK](https://azure.microsoft.com/downloads/)網站部署。</span><span class="sxs-lookup"><span data-stu-id="4c596-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="4c596-114">啟動 Visual Studio 或 Visual Studio Express。</span><span class="sxs-lookup"><span data-stu-id="4c596-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="4c596-115">按一下**伺服器總管**並登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c596-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="4c596-116">Visual Studio 將會需要您登入 toocreate hello 網站資源，在您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c596-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="4c596-117">在 Visual Studio 中，按一下 **檔案**，然後按一下**新增**，然後**專案**，依序展開**範本**， **Visual C#**，然後按一下 **Web**和**ASP.NET Web 應用程式**，型別 hello 名稱**AppBackend**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4c596-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="4c596-118">在 hello**新增 ASP.NET 專案** 對話方塊中，按一下**Web API**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4c596-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="4c596-119">在 [hello**設定的 Microsoft Azure Web 應用程式**] 對話方塊中，選擇訂用帳戶，和**App Service 方案**您已經建立。</span><span class="sxs-lookup"><span data-stu-id="4c596-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="4c596-120">您也可以選擇**建立新的應用程式服務方案**建立一個從 hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4c596-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="4c596-121">在此教學課程中您不需要資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c596-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="4c596-122">一旦您已選取您的應用程式服務方案中，按一下 **確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="4c596-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="4c596-123">驗證用戶端 toohello WebAPI 後端</span><span class="sxs-lookup"><span data-stu-id="4c596-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="4c596-124">在本節中，您將建立新的訊息處理常式類別，名為**AuthenticationTestHandler** hello 新的後端。</span><span class="sxs-lookup"><span data-stu-id="4c596-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="4c596-125">這個類別衍生自[DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx)並加入做為訊息處理常式，所以它可以處理傳入 hello 後端的所有要求。</span><span class="sxs-lookup"><span data-stu-id="4c596-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="4c596-126">在 方案總管 中，以滑鼠右鍵按一下 hello **AppBackend**專案中，按一下 **新增**，然後按一下 **類別**。</span><span class="sxs-lookup"><span data-stu-id="4c596-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="4c596-127">Hello 新類別命名**AuthenticationTestHandler.cs**，然後按一下**新增**toogenerate hello 類別。</span><span class="sxs-lookup"><span data-stu-id="4c596-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="4c596-128">這個類別會使用的 tooauthenticate 使用者使用*基本驗證*為了簡單起見。</span><span class="sxs-lookup"><span data-stu-id="4c596-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="4c596-129">請注意，您的應用程式可以使用任何驗證結構描述。</span><span class="sxs-lookup"><span data-stu-id="4c596-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="4c596-130">在 AuthenticationTestHandler.cs，加入 hello 下列`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="4c596-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="4c596-131">在 AuthenticationTestHandler.cs，取代 hello`AuthenticationTestHandler`以下列程式碼的 hello 類別定義。</span><span class="sxs-lookup"><span data-stu-id="4c596-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="4c596-132">Hello 下列三個條件都成立時，這個處理常式會授權 hello 要求：</span><span class="sxs-lookup"><span data-stu-id="4c596-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="4c596-133">hello 要求包含*授權*標頭。</span><span class="sxs-lookup"><span data-stu-id="4c596-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="4c596-134">hello 要求使用*基本*驗證。</span><span class="sxs-lookup"><span data-stu-id="4c596-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="4c596-135">hello 使用者名稱字串 hello 密碼會是與字串 hello 相同的字串。</span><span class="sxs-lookup"><span data-stu-id="4c596-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="4c596-136">否則，將會拒絕 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="4c596-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="4c596-137">這不是真正的驗證和授權方法。</span><span class="sxs-lookup"><span data-stu-id="4c596-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="4c596-138">這只是本教學課程中一個非常簡單的範例。</span><span class="sxs-lookup"><span data-stu-id="4c596-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="4c596-139">如果 hello 要求訊息已驗證，及授權的 hello `AuthenticationTestHandler`，hello 基本驗證的使用者將會附加的 toohello 目前要求上 hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4c596-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="4c596-140">Hello HttpContext 中的使用者資訊將供另一個控制站 (RegisterController) 更新 tooadd[標記](https://msdn.microsoft.com/library/azure/dn530749.aspx)toohello 通知註冊要求。</span><span class="sxs-lookup"><span data-stu-id="4c596-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="4c596-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="4c596-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
                       // Attach hello new principal object toohello current HttpContext object
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
       <span data-ttu-id="4c596-142">}</span><span class="sxs-lookup"><span data-stu-id="4c596-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="4c596-143">**安全性注意事項**: hello`AuthenticationTestHandler`類別不提供，則為 true 的驗證。</span><span class="sxs-lookup"><span data-stu-id="4c596-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="4c596-144">它是使用唯一 toomimic 基本驗證，並不安全。</span><span class="sxs-lookup"><span data-stu-id="4c596-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="4c596-145">您必須在生產應用程式和服務中實作安全的驗證機制。</span><span class="sxs-lookup"><span data-stu-id="4c596-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="4c596-146">新增下列程式碼結尾 hello hello hello`Register`方法在 hello **App_Start/WebApiConfig.cs**類別 tooregister hello 訊息處理常式：</span><span class="sxs-lookup"><span data-stu-id="4c596-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="4c596-147">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="4c596-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="4c596-148">註冊使用 hello WebAPI 後端的通知</span><span class="sxs-lookup"><span data-stu-id="4c596-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="4c596-149">在本節中，我們將新的控制器 toohello WebAPI 後端 toohandle 要求 tooregister 使用者和裝置 hello 用戶端程式庫使用通知中樞的通知。</span><span class="sxs-lookup"><span data-stu-id="4c596-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="4c596-150">hello 控制器會加入使用者標記 hello 使用者通過驗證，並附加 toohello HttpContext 由 hello `AuthenticationTestHandler`。</span><span class="sxs-lookup"><span data-stu-id="4c596-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="4c596-151">hello 標記將會有 hello 字串格式， `"username:<actual username>"`。</span><span class="sxs-lookup"><span data-stu-id="4c596-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="4c596-152">在 [方案總管] 中，以滑鼠右鍵按一下 hello **AppBackend**專案，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="4c596-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="4c596-153">在 hello 左側，按一下 **線上**，並搜尋**Microsoft.Azure.NotificationHubs**在 hello**搜尋**方塊。</span><span class="sxs-lookup"><span data-stu-id="4c596-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="4c596-154">在 hello 結果清單中，按一下  **Microsoft Azure 通知中樞**，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="4c596-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="4c596-155">完成 hello 安裝，然後關閉 hello NuGet 封裝管理員 視窗。</span><span class="sxs-lookup"><span data-stu-id="4c596-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="4c596-156">這會將參考 toohello Azure 通知中樞 SDK 使用 hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 集線器 NuGet 封裝</a>。</span><span class="sxs-lookup"><span data-stu-id="4c596-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="4c596-157">現在，我們將建立新的類別檔案，表示與通知中樞用 toosend 通知 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="4c596-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="4c596-158">在 hello 方案總管 中，以滑鼠右鍵按一下 hello**模型**資料夾中，按一下**新增**，然後按一下 **類別**。</span><span class="sxs-lookup"><span data-stu-id="4c596-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="4c596-159">Hello 新類別命名**Notifications.cs**，然後按一下 **新增**toogenerate hello 類別。</span><span class="sxs-lookup"><span data-stu-id="4c596-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="4c596-160">在 Notifications.cs，加入 hello 下列`using`在 hello hello 檔案最上方的陳述式：</span><span class="sxs-lookup"><span data-stu-id="4c596-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="4c596-161">取代 hello`Notifications`類別 hello 下列定義，請確定 tooreplace hello 兩預留位置取代 hello 連接字串 （具有完整權限） 您的通知中樞，和 hello 中樞名稱 (可在[Azure 傳統入口網站](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="4c596-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="4c596-162">接下來我們將建立名為 **RegisterController** 的新控制器。</span><span class="sxs-lookup"><span data-stu-id="4c596-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="4c596-163">在 方案總管 中，以滑鼠右鍵按一下 hello**控制器**資料夾，然後按一下 **新增**，然後按一下 **控制器**。</span><span class="sxs-lookup"><span data-stu-id="4c596-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="4c596-164">按一下 hello **Web API 2 控制器-空白**項目，然後再按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="4c596-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="4c596-165">Hello 新類別命名**RegisterController**，然後按一下**新增**再次 toogenerate hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="4c596-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="4c596-166">在 RegisterController.cs，加入 hello 下列`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="4c596-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="4c596-167">新增下列程式碼內 hello hello`RegisterController`類別定義。</span><span class="sxs-lookup"><span data-stu-id="4c596-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="4c596-168">請注意，在這段程式碼中，我們將加入使用者標記，這是 hello 使用者附加 toohello HttpContext。</span><span class="sxs-lookup"><span data-stu-id="4c596-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="4c596-169">hello 使用者通過驗證，並附加 toohello HttpContext hello 訊息篩選器，我們加入， `AuthenticationTestHandler`。</span><span class="sxs-lookup"><span data-stu-id="4c596-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="4c596-170">您也可以加入 hello 使用者的選用檢查 tooverify 具有權限的 hello tooregister 要求標記。</span><span class="sxs-lookup"><span data-stu-id="4c596-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
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
        // This creates or updates a registration (with provided channelURI) at hello specified id
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
   
            // add check if user is allowed tooadd these tags
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
10. <span data-ttu-id="4c596-171">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="4c596-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="4c596-172">從 hello WebAPI 後端傳送通知</span><span class="sxs-lookup"><span data-stu-id="4c596-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="4c596-173">本節中，您會加入新的控制站可公開方法，讓用戶端裝置 toosend hello hello ASP.NET WebAPI 後端中使用 Azure 通知中心服務管理程式庫的使用者名稱標記為基礎的通知。</span><span class="sxs-lookup"><span data-stu-id="4c596-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="4c596-174">建立另一個名為 **NotificationsController**的新控制器。</span><span class="sxs-lookup"><span data-stu-id="4c596-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="4c596-175">建立 hello 相同的方式建立 hello **RegisterController** hello 前一節。</span><span class="sxs-lookup"><span data-stu-id="4c596-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="4c596-176">在 NotificationsController.cs，加入 hello 下列`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="4c596-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="4c596-177">新增下列方法 toohello hello **NotificationsController**類別。</span><span class="sxs-lookup"><span data-stu-id="4c596-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="4c596-178">此程式碼傳送 hello 平台通知服務 (PNS) 為基礎的通知類型`pns`參數。</span><span class="sxs-lookup"><span data-stu-id="4c596-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="4c596-179">hello 值`to_tag`為使用的 tooset hello *username*標記的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="4c596-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="4c596-180">此標記必須符合作用中通知中樞註冊的使用者名稱標記。</span><span class="sxs-lookup"><span data-stu-id="4c596-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="4c596-181">hello 通知訊息是取自 hello hello POST 要求主體，而且 hello 目標 PNS 格式化。</span><span class="sxs-lookup"><span data-stu-id="4c596-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="4c596-182">Hello 平台通知服務 (PNS) 支援的裝置使用 tooreceive 通知，根據不同的通知使用不同格式支援。</span><span class="sxs-lookup"><span data-stu-id="4c596-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="4c596-183">例如在 Windows 裝置上，您可以搭配 WNS 使用不受其他 PNS 直接支援的 [快顯通知](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="4c596-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="4c596-184">因此您的後端 hello PNS 的裝置必須受支援的通知至 tooformat hello 通知您計劃 toosupport。</span><span class="sxs-lookup"><span data-stu-id="4c596-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="4c596-185">然後使用 hello 適當的傳送應用程式開發介面上 hello [NotificationHubClient 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="4c596-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="4c596-186">按**F5** toorun hello 應用程式和 tooensure hello 工作的準確性為止。</span><span class="sxs-lookup"><span data-stu-id="4c596-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="4c596-187">hello 應用程式應該啟動網頁瀏覽器，並顯示 hello ASP.NET 首頁。</span><span class="sxs-lookup"><span data-stu-id="4c596-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="4c596-188">發行 hello 新 WebAPI 後端</span><span class="sxs-lookup"><span data-stu-id="4c596-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="4c596-189">現在我們將部署此應用程式 tooan Azure 網站順序 toomake 中的所有的裝置可以存取它。</span><span class="sxs-lookup"><span data-stu-id="4c596-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="4c596-190">以滑鼠右鍵按一下 hello **AppBackend**專案，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="4c596-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="4c596-191">選取 [Microsoft Azure App Service] 作為發佈目標，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="4c596-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="4c596-192">這會開啟 hello 建立應用程式服務 對話方塊可幫助您在 Azure 中建立所有 hello 所需的 Azure 資源 toorun hello ASP.NET web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c596-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="4c596-193">在 [hello**建立 App Service** ] 對話方塊中，選取您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c596-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="4c596-194">按一下 [變更類型] 並選取 [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4c596-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="4c596-195">保留 hello **Web 應用程式名稱**給定的並選取 hello**訂用帳戶**，**資源群組**，和**App Service 方案**。</span><span class="sxs-lookup"><span data-stu-id="4c596-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="4c596-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4c596-196">Click **Create**.</span></span>

4. <span data-ttu-id="4c596-197">請記下 hello**網站 URL**屬性在 hello**摘要**> 一節。</span><span class="sxs-lookup"><span data-stu-id="4c596-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="4c596-198">我們將 toothis URL 做為您*後端端點*稍後在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="4c596-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="4c596-199">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="4c596-199">Click **Publish**.</span></span>

5. <span data-ttu-id="4c596-200">Hello 精靈完成後，其所發行 hello ASP.NET web 應用程式 tooAzure，然後啟動 hello hello 預設瀏覽器中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c596-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="4c596-201">您的應用程式將可在 Azure App Service 中檢視。</span><span class="sxs-lookup"><span data-stu-id="4c596-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="4c596-202">hello URL 會使用您稍早，指定與 hello 格式 http://<app_name>.azurewebsites.net hello web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="4c596-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

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
