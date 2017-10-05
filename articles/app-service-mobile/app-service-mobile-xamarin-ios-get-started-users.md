---
title: "開始在 Xamarin iOS 中使用行動應用程式的驗證"
description: "了解如何使用行動應用程式透過眾多識別提供者驗證 Xamarin iOS 應用程式使用者，包括 AAD、Google、Facebook、Twitter 和 Microsoft。"
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
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="45fb1-103">將驗證新增至 Xamarin.iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="45fb1-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="45fb1-104">本主題說明如何從用戶端應用程式驗證 App Service 行動應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="45fb1-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="45fb1-105">在本教學課程中，您將使用 App Service 支援的身分識別提供者，將驗證新增至 Xamarin.iOS 快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="45fb1-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="45fb1-106">由行動應用程式成功驗證並授權之後，就會顯示使用者識別碼值，而您也將可以存取受限制的資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="45fb1-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="45fb1-107">您必須先完成 [建立 Xamarin.iOS 應用程式]教學課程。</span><span class="sxs-lookup"><span data-stu-id="45fb1-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="45fb1-108">如果您不要使用下載的快速入門伺服器專案，必須將驗證擴充套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="45fb1-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="45fb1-109">如需伺服器擴充套件的詳細資訊，請參閱 [使用 Azure 行動應用程式的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="45fb1-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="45fb1-110">註冊應用程式進行驗證，並設定應用程式服務</span><span class="sxs-lookup"><span data-stu-id="45fb1-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="45fb1-111">將您的應用程式新增至允許的外部重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="45fb1-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="45fb1-112">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="45fb1-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="45fb1-113">這讓驗證系統能夠在驗證程序完成之後，重新導向回到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45fb1-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="45fb1-114">我們會在這整個教學課程中使用 URL 配置 appname。</span><span class="sxs-lookup"><span data-stu-id="45fb1-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="45fb1-115">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="45fb1-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="45fb1-116">它對於您的行動應用程式而言應該是唯一的。</span><span class="sxs-lookup"><span data-stu-id="45fb1-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="45fb1-117">在伺服器端啟用重新導向：</span><span class="sxs-lookup"><span data-stu-id="45fb1-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="45fb1-118">在 [Azure 入口網站] 中，選取您的 App Service。</span><span class="sxs-lookup"><span data-stu-id="45fb1-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="45fb1-119">按一下 [驗證/授權] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="45fb1-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="45fb1-120">在 [允許的外部重新導向 URL] 中，輸入 `url_scheme_of_your_app://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="45fb1-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="45fb1-121">此字串中的 **url_scheme_of_your_app** 是您行動應用程式的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="45fb1-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="45fb1-122">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="45fb1-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="45fb1-123">請記下您選擇的字串，因為您將需要在數個位置中使用該 URL 配置來調整您的行動應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="45fb1-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="45fb1-124">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="45fb1-124">Click **OK**.</span></span>

5. <span data-ttu-id="45fb1-125">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="45fb1-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="45fb1-126">限制只有通過驗證的使用者具有權限</span><span class="sxs-lookup"><span data-stu-id="45fb1-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="45fb1-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="45fb1-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="45fb1-128">在 Visual Studio 或 Xamarin Studio 中，在裝置或模擬器上執行用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="45fb1-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="45fb1-129">確認在應用程式啟動後，發生狀態代碼 401 (未經授權) 的未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="45fb1-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="45fb1-130">失敗都會記錄到偵錯工具主控台。</span><span class="sxs-lookup"><span data-stu-id="45fb1-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="45fb1-131">因此在 Visual Studio 中，您應該會在 [輸出] 視窗中看到失敗。</span><span class="sxs-lookup"><span data-stu-id="45fb1-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="45fb1-132">&nbsp;&nbsp;應用程式嘗試以未經驗證的使用者身分存取您的行動應用程式後端，因此發生此未經授權的失敗。</span><span class="sxs-lookup"><span data-stu-id="45fb1-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="45fb1-133">*TodoItem* 資料表現在需要驗證。</span><span class="sxs-lookup"><span data-stu-id="45fb1-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="45fb1-134">接下來，您將會更新用戶端應用程式，利用已驗證的使用者身分來要求行動應用程式後端的資源。</span><span class="sxs-lookup"><span data-stu-id="45fb1-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="45fb1-135">將驗證新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="45fb1-135">Add authentication to the app</span></span>
<span data-ttu-id="45fb1-136">在本節中您將修改應用程式，以先顯示登入畫面再顯示資料。</span><span class="sxs-lookup"><span data-stu-id="45fb1-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="45fb1-137">應用程式在啟動時將不會連接到您的應用程式服務，且不會顯示任何資料。</span><span class="sxs-lookup"><span data-stu-id="45fb1-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="45fb1-138">在使用者第一次執行重新整理動作後，登入畫面將會出現；在成功登入後，將會顯示 todo 項目清單。</span><span class="sxs-lookup"><span data-stu-id="45fb1-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="45fb1-139">在用戶端專案中開啟檔案 **QSTodoService.cs**，將下列 using 陳述式和具有存取子的 `MobileServiceUser`新增至 QSTodoService 類別：</span><span class="sxs-lookup"><span data-stu-id="45fb1-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="45fb1-140">使用下列定義，將名為 **Authenticate** 的新方法新增至 **QSTodoService**：</span><span class="sxs-lookup"><span data-stu-id="45fb1-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="45fb1-141">如果您使用的身分識別提供者不是 Facebook，請將傳給上述 **LoginAsync** 的值變更為下列其中一個：MicrosoftAccount、Twitter、Google 或 WindowsAzureActiveDirectory。</span><span class="sxs-lookup"><span data-stu-id="45fb1-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="45fb1-142">開啟 **QSTodoListViewController.cs**。</span><span class="sxs-lookup"><span data-stu-id="45fb1-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="45fb1-143">修改 **ViewDidLoad** 的方法定義，移除結尾附近的 **RefreshAsync()** 呼叫：</span><span class="sxs-lookup"><span data-stu-id="45fb1-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="45fb1-144">修改方法 **RefreshAsync**，以驗證 **User** 屬性是否為 null。</span><span class="sxs-lookup"><span data-stu-id="45fb1-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="45fb1-145">在方法定義最上方新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="45fb1-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="45fb1-146">開啟 **AppDelegate.cs**，新增下列方法：</span><span class="sxs-lookup"><span data-stu-id="45fb1-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="45fb1-147">開啟 **Info.plist** 檔案，瀏覽至 [進階] 區段中的 [URL 類型]。</span><span class="sxs-lookup"><span data-stu-id="45fb1-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="45fb1-148">立即設定 URL 類型的 [識別碼] 和 [URL 配置]，然後按一下 [新增 URL 類型]。</span><span class="sxs-lookup"><span data-stu-id="45fb1-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="45fb1-149">[URL 配置] 應該與您的 {url_scheme_of_your_app} 相同。</span><span class="sxs-lookup"><span data-stu-id="45fb1-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="45fb1-150">在 Visual Studio 或連線到您 Mac 上之 Xamarin 建置主機的 Xamarin Studio 中，以裝置或模擬器為目標執行用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="45fb1-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="45fb1-151">確認應用程式未顯示資料。</span><span class="sxs-lookup"><span data-stu-id="45fb1-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="45fb1-152">將項目清單往下拉以執行重新整理動作，這會使登入畫面出現。</span><span class="sxs-lookup"><span data-stu-id="45fb1-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="45fb1-153">在您成功輸入有效認證後，應用程式將會顯示 todo 項目清單，且您可以對資料進行更新。</span><span class="sxs-lookup"><span data-stu-id="45fb1-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="45fb1-154">[建立 Xamarin.iOS 應用程式]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="45fb1-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>