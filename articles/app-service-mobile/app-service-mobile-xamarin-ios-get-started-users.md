---
title: "透過在 Xamarin iOS 行動應用程式驗證 aaaGet 已啟動"
description: "深入了解如何 toouse 行動應用程式 tooauthenticate 使用者透過不同的身分識別提供者，包括 AAD、 Google、 Facebook、 Twitter 和 Microsoft 的 Xamarin iOS 應用程式。"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="dfab0-103">新增驗證 tooyour Xamarin.iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="dfab0-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="dfab0-104">本主題說明如何 tooauthenticate 的 App Service 行動應用程式從用戶端應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="dfab0-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="dfab0-105">在本教學課程中，您可以新增使用身分識別提供者支援的應用程式服務的驗證 toohello Xamarin.iOS 快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="dfab0-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="dfab0-106">正在成功驗證和授權您的行動應用程式之後，會顯示 hello 使用者識別碼的值，而且您必須能夠 tooaccess 限制資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="dfab0-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="dfab0-107">您必須先完成 hello 教學課程[建立 Xamarin.iOS 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="dfab0-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="dfab0-108">如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 驗證擴充功能封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="dfab0-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="dfab0-109">如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="dfab0-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="dfab0-110">註冊應用程式進行驗證，並設定應用程式服務</span><span class="sxs-lookup"><span data-stu-id="dfab0-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="dfab0-111">新增您的應用程式 toohello 允許外部重新導向 Url</span><span class="sxs-lookup"><span data-stu-id="dfab0-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="dfab0-112">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="dfab0-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="dfab0-113">Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfab0-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="dfab0-114">在本教學課程中，我們使用 hello URL 配置_appname_整個。</span><span class="sxs-lookup"><span data-stu-id="dfab0-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="dfab0-115">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="dfab0-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="dfab0-116">它應該是唯一的 tooyour 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfab0-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="dfab0-117">hello 伺服器端 tooenable hello 重新導向：</span><span class="sxs-lookup"><span data-stu-id="dfab0-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="dfab0-118">在 hello [Azure 入口網站]，選取您的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="dfab0-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="dfab0-119">按一下 hello**驗證 / 授權**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="dfab0-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="dfab0-120">在 [hello**允許外部重新導向 Url**，輸入`url_scheme_of_your_app://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="dfab0-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="dfab0-121">hello **url_scheme_of_your_app**這個字串中為 [行動應用程式的 hello URL 配置。</span><span class="sxs-lookup"><span data-stu-id="dfab0-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="dfab0-122">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="dfab0-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="dfab0-123">請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="dfab0-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="dfab0-124">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="dfab0-124">Click **OK**.</span></span>

5. <span data-ttu-id="dfab0-125">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="dfab0-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="dfab0-126">限制 tooauthenticated 使用者權限</span><span class="sxs-lookup"><span data-stu-id="dfab0-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="dfab0-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="dfab0-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="dfab0-128">在 Visual Studio 或 Xamarin Studio，請裝置或模擬器上執行 hello 用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="dfab0-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="dfab0-129">請確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="dfab0-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="dfab0-130">hello 失敗是 hello 偵錯工具的記錄的 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="dfab0-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="dfab0-131">因此在 Visual Studio 中，您應該會看到 hello [輸出] 視窗中的 hello 失敗。</span><span class="sxs-lookup"><span data-stu-id="dfab0-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="dfab0-132">&nbsp;&nbsp;此未授權的失敗不會因為 hello 應用程式嘗試 tooaccess 未經驗證的使用者身分行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="dfab0-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="dfab0-133">hello *TodoItem*資料表現在需要驗證。</span><span class="sxs-lookup"><span data-stu-id="dfab0-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="dfab0-134">接下來，您將更新從 hello 行動裝置應用程式後端 hello 用戶端應用程式 toorequest 資源與已驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="dfab0-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="dfab0-135">新增驗證 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="dfab0-135">Add authentication toohello app</span></span>
<span data-ttu-id="dfab0-136">在本節中，您將修改 hello 應用程式 toodisplay 登入畫面之前顯示的資料。</span><span class="sxs-lookup"><span data-stu-id="dfab0-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="dfab0-137">Hello 應用程式啟動時，它將無法不連線 tooyour 應用程式服務，並不會顯示任何資料。</span><span class="sxs-lookup"><span data-stu-id="dfab0-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="dfab0-138">Hello 第一次後該 hello 使用者執行 hello 重新整理鍵筆勢，會顯示 hello 登入畫面。成功的登入之後 hello todo 項目的清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="dfab0-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="dfab0-139">在 hello 用戶端專案中，開啟 [hello 檔案**QSTodoService.cs**並加入 hello 下列 using 陳述式和`MobileServiceUser`與存取子 toohello QSTodoService 類別：</span><span class="sxs-lookup"><span data-stu-id="dfab0-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="dfab0-140">將名為的新方法加入**驗證**太**QSTodoService**以 hello 下列定義：</span><span class="sxs-lookup"><span data-stu-id="dfab0-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] <span data-ttu-id="dfab0-141">如果您使用 Facebook 以外的身分識別提供者，變更 hello 值太傳遞**LoginAsync** tooone hello 以下的上方： _MicrosoftAccount_， _Twitter_，_Google_，或_WindowsAzureActiveDirectory_。</span><span class="sxs-lookup"><span data-stu-id="dfab0-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="dfab0-142">開啟 **QSTodoListViewController.cs**。</span><span class="sxs-lookup"><span data-stu-id="dfab0-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="dfab0-143">修改 hello 方法定義**ViewDidLoad**太移除 hello 呼叫**RefreshAsync()**接近 hello 結束：</span><span class="sxs-lookup"><span data-stu-id="dfab0-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="dfab0-144">修改 hello 方法**RefreshAsync** tooauthenticate 如果 hello**使用者**屬性為 null。</span><span class="sxs-lookup"><span data-stu-id="dfab0-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="dfab0-145">加入下列程式碼頂端 hello hello 方法定義的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfab0-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="dfab0-146">開啟**d**，新增下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="dfab0-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="dfab0-147">開啟**Info.plist**檔案中，瀏覽過**URL 類型**在 hello**進階**> 一節。</span><span class="sxs-lookup"><span data-stu-id="dfab0-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="dfab0-148">現在設定 hello**識別碼**和 hello **URL 配置**URL 類型和按一下**加入 URL 類型**。</span><span class="sxs-lookup"><span data-stu-id="dfab0-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="dfab0-149">**URL 配置**應該為您的 {url_scheme_of_your_app} hello 相同。</span><span class="sxs-lookup"><span data-stu-id="dfab0-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="dfab0-150">在 Visual Studio 或 Xamarin Studio 中連接 tooyour Xamarin 組建主機在您 Mac 上，執行 hello 裝置或模擬器為目標的用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="dfab0-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="dfab0-151">請確認該 hello 應用程式會顯示任何資料。</span><span class="sxs-lookup"><span data-stu-id="dfab0-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="dfab0-152">Hello 清單中的項目，這會導致 hello 登入畫面 tooappear，藉以執行 hello 重新整理筆勢。</span><span class="sxs-lookup"><span data-stu-id="dfab0-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="dfab0-153">一旦您已經輸入有效的認證，hello 應用程式將會顯示 hello todo 項目的清單，而且您可以更新 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="dfab0-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[建立 Xamarin.iOS 應用程式]: app-service-mobile-xamarin-ios-get-started.md