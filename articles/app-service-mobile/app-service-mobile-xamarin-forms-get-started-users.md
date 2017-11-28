---
title: "透過 Xamarin Forms 應用程式中的行動應用程式驗證 aaaGet Started |Microsoft 文件"
description: "深入了解如何 toouse 行動應用程式 tooauthenticate 使用者透過不同的身分識別提供者，包括 AAD、 Google、 Facebook、 Twitter 和 Microsoft 應用程式 Xamarin Forms。"
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="1dce1-103">新增驗證 tooyour Xamarin Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="1dce1-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="1dce1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1dce1-104">Overview</span></span>
<span data-ttu-id="1dce1-105">本主題說明如何 tooauthenticate 的 App Service 行動應用程式從用戶端應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="1dce1-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="1dce1-106">本教學課程中，您可以將驗證加入使用身分識別提供者支援的應用程式服務的 hello Xamarin Forms 快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="1dce1-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="1dce1-107">正在成功驗證和授權您的行動應用程式後，會顯示 hello 使用者識別碼的值，並會限制可以 tooaccess 資料表資料。</span><span class="sxs-lookup"><span data-stu-id="1dce1-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dce1-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="1dce1-108">Prerequisites</span></span>
<span data-ttu-id="1dce1-109">本教學課程 hello 獲得最佳結果，我們建議您先完成 hello[建立 Xamarin Forms 應用程式][ 1]教學課程。</span><span class="sxs-lookup"><span data-stu-id="1dce1-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="1dce1-110">完成本教學課程之後，您將會有一個多平台 TodoList 應用程式的 Xamarin.Forms 專案。</span><span class="sxs-lookup"><span data-stu-id="1dce1-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="1dce1-111">如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 驗證擴充功能封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="1dce1-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="1dce1-112">如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK][2]。</span><span class="sxs-lookup"><span data-stu-id="1dce1-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="1dce1-113">註冊應用程式進行驗證，並設定應用程式服務</span><span class="sxs-lookup"><span data-stu-id="1dce1-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="1dce1-114"><a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url</span><span class="sxs-lookup"><span data-stu-id="1dce1-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="1dce1-115">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="1dce1-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="1dce1-116">Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1dce1-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="1dce1-117">在本教學課程中，我們使用 hello URL 配置_appname_整個。</span><span class="sxs-lookup"><span data-stu-id="1dce1-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="1dce1-118">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="1dce1-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="1dce1-119">它應該是唯一的 tooyour 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="1dce1-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="1dce1-120">hello 伺服器端 tooenable hello 重新導向：</span><span class="sxs-lookup"><span data-stu-id="1dce1-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="1dce1-121">在 hello [Azure 入口網站]，選取您的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="1dce1-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="1dce1-122">按一下 hello**驗證 / 授權**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="1dce1-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="1dce1-123">在 hello**允許外部重新導向 Url**，輸入`url_scheme_of_your_app://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="1dce1-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="1dce1-124">hello **url_scheme_of_your_app**這個字串中為 行動應用程式的 hello URL 配置。</span><span class="sxs-lookup"><span data-stu-id="1dce1-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="1dce1-125">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="1dce1-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="1dce1-126">請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="1dce1-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="1dce1-127">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1dce1-127">Click **OK**.</span></span>

5. <span data-ttu-id="1dce1-128">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1dce1-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="1dce1-129">限制 tooauthenticated 使用者權限</span><span class="sxs-lookup"><span data-stu-id="1dce1-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="1dce1-130">加入驗證 toohello 可攜式類別程式庫</span><span class="sxs-lookup"><span data-stu-id="1dce1-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="1dce1-131">行動應用程式會使用 hello [LoginAsync] [ 3] hello 上的擴充方法[MobileServiceClient] [ 4] toosign 在使用者與應用程式服務驗證。</span><span class="sxs-lookup"><span data-stu-id="1dce1-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="1dce1-132">這個範例會使用在 hello 應用程式中顯示 hello 提供者的登入介面的管理伺服器的驗證流程。</span><span class="sxs-lookup"><span data-stu-id="1dce1-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="1dce1-133">如需詳細資訊，請參閱[伺服器管理的驗證][5]。</span><span class="sxs-lookup"><span data-stu-id="1dce1-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="1dce1-134">若要在實際執行應用程式中提供更好的使用者體驗，您應該考慮改用[用戶端管理的驗證][6]。</span><span class="sxs-lookup"><span data-stu-id="1dce1-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="1dce1-135">使用 Xamarin Forms 專案，tooauthenticate 定義**IAuthenticate** hello 應用程式的 hello 可攜式類別庫中的介面。</span><span class="sxs-lookup"><span data-stu-id="1dce1-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="1dce1-136">然後加入**登入**定義 hello 可攜式類別庫，您按一下按鈕 toohello 使用者介面 toostart 驗證。</span><span class="sxs-lookup"><span data-stu-id="1dce1-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="1dce1-137">在成功驗證之後，資料會載入從 hello 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="1dce1-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="1dce1-138">實作 hello **IAuthenticate**每個平台應用程式所支援的介面。</span><span class="sxs-lookup"><span data-stu-id="1dce1-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="1dce1-139">在 Visual Studio 或 Xamarin Studio，請從與 hello 專案中開啟 App.cs**可攜式**hello 名稱，亦即可攜式類別庫專案，然後加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="1dce1-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="1dce1-140">在 App.cs，加入 hello 下列`IAuthenticate`介面定義之前 hello`App`類別定義。</span><span class="sxs-lookup"><span data-stu-id="1dce1-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="1dce1-141">平台特定實作的 tooinitialize hello 介面新增下列靜態成員 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="1dce1-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="1dce1-142">開啟 TodoList.xaml 從 hello 可攜式類別庫專案，加入下列 hello**按鈕**hello 中的項目*buttonsPanel*之後 hello 現有按鈕的配置元素：</span><span class="sxs-lookup"><span data-stu-id="1dce1-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="1dce1-143">此按鈕會向行動應用程式後端觸發伺服器管理的驗證。</span><span class="sxs-lookup"><span data-stu-id="1dce1-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="1dce1-144">開啟 TodoList.xaml.cs 從 hello 可攜式類別庫專案，然後新增下列欄位 toohello hello`TodoList`類別：</span><span class="sxs-lookup"><span data-stu-id="1dce1-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="1dce1-145">取代 hello **OnAppearing**方法，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dce1-145">Replace hello **OnAppearing** method with hello following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="1dce1-146">此程式碼可確保，只重新整理資料從 hello 服務之後已經過驗證。</span><span class="sxs-lookup"><span data-stu-id="1dce1-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="1dce1-147">新增下列 hello 的處理常式的 hello**已按下**事件 toohello **TodoList**類別：</span><span class="sxs-lookup"><span data-stu-id="1dce1-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="1dce1-148">儲存您的變更，並重建 hello 可攜式類別庫專案，確認沒有發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1dce1-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="1dce1-149">新增驗證 toohello Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="1dce1-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="1dce1-150">此區段會顯示如何 tooimplement hello **IAuthenticate** hello Android 應用程式專案中的介面。</span><span class="sxs-lookup"><span data-stu-id="1dce1-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="1dce1-151">如果您不要支援 Android 裝置，請略過這一節。</span><span class="sxs-lookup"><span data-stu-id="1dce1-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="1dce1-152">在 Visual Studio 或 Xamarin Studio，以滑鼠右鍵按一下 hello **droid**專案，然後**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="1dce1-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="1dce1-153">按 F5 toostart hello hello 偵錯工具中的專案，然後確認應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="1dce1-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="1dce1-154">hello 401 程式碼會產生 hello 後端存取，所以 僅限受限制的 tooauthorized 使用者。</span><span class="sxs-lookup"><span data-stu-id="1dce1-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="1dce1-155">Hello Android 專案中，開啟 Weatherapp 並加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="1dce1-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="1dce1-156">更新 hello **MainActivity**類別 tooimplement hello **IAuthenticate**介面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1dce1-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="1dce1-157">更新 hello **MainActivity**類別藉由新增**MobileServiceUser**欄位和**驗證**方法所需的 hello **IAuthenticate**介面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1dce1-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="1dce1-158">如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider][7]選擇不同的值。</span><span class="sxs-lookup"><span data-stu-id="1dce1-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="1dce1-159">新增下列程式碼內的 hello <application> AndroidManifest.xml 節點：</span><span class="sxs-lookup"><span data-stu-id="1dce1-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. <span data-ttu-id="1dce1-160">新增下列程式碼 toohello hello **OnCreate**方法 hello **MainActivity**太類別 hello 呼叫之前`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="1dce1-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="1dce1-161">此程式碼可確保 hello 應用程式載入之前初始化 hello 驗證器。</span><span class="sxs-lookup"><span data-stu-id="1dce1-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="1dce1-162">重建 hello 應用程式，請執行此程式碼，然後使用 hello 驗證提供者選擇，並確認您能夠 tooaccess 資料，以驗證的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="1dce1-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="1dce1-163">新增驗證 toohello iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="1dce1-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="1dce1-164">此區段會顯示如何 tooimplement hello **IAuthenticate** hello 的 iOS 應用程式專案中的介面。</span><span class="sxs-lookup"><span data-stu-id="1dce1-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="1dce1-165">如果您不要支援 iOS 裝置，請略過這一節。</span><span class="sxs-lookup"><span data-stu-id="1dce1-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="1dce1-166">在 Visual Studio 或 Xamarin Studio，以滑鼠右鍵按一下 hello **iOS**專案，然後**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="1dce1-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="1dce1-167">按 F5 toostart hello hello 偵錯工具中的專案，然後確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="1dce1-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="1dce1-168">因為 hello 後端的存取限制的 tooauthorized 使用者才不會產生 hello 401 回應。</span><span class="sxs-lookup"><span data-stu-id="1dce1-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="1dce1-169">Hello 的 iOS 專案中開啟 d，然後加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="1dce1-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="1dce1-170">更新 hello **AppDelegate**類別 tooimplement hello **IAuthenticate**介面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1dce1-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="1dce1-171">更新 hello **AppDelegate**類別藉由新增**MobileServiceUser**欄位和**驗證**方法所需的 hello **IAuthenticate**介面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1dce1-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="1dce1-172">如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider] 選擇不同的值。</span><span class="sxs-lookup"><span data-stu-id="1dce1-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="1dce1-173">加入 OpenUrl （uiapplication # 應用程式，NSUrl url NSDictionary 選項） 方法多載，以更新 hello AppDelegate 類別</span><span class="sxs-lookup"><span data-stu-id="1dce1-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="1dce1-174">新增下列一行程式碼 toohello hello **FinishedLaunching**太呼叫方法，再 hello`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="1dce1-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="1dce1-175">此程式碼可確保載入 hello 應用程式之前，會初始化 hello 驗證器。</span><span class="sxs-lookup"><span data-stu-id="1dce1-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="1dce1-176">新增**{url_scheme_of_your_app}** tooURL Info.plist 中的配置。</span><span class="sxs-lookup"><span data-stu-id="1dce1-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="1dce1-177">重建 hello 應用程式，請執行此程式碼，然後使用 hello 驗證提供者選擇，並確認您能夠 tooaccess 資料，以驗證的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="1dce1-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="1dce1-178">新增驗證 tooWindows 10 （包括電話） 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="1dce1-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="1dce1-179">此區段會顯示如何 tooimplement hello **IAuthenticate** hello Windows 10 應用程式專案中的介面。</span><span class="sxs-lookup"><span data-stu-id="1dce1-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="1dce1-180">相同的步驟適用於通用 Windows 平台 (UWP) 專案，但使用 hello hello **UWP**專案 （標註的變更）。</span><span class="sxs-lookup"><span data-stu-id="1dce1-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="1dce1-181">如果您不要支援 Windows 裝置，請略過這一節。</span><span class="sxs-lookup"><span data-stu-id="1dce1-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="1dce1-182">「 在 Visual Studio 中，以滑鼠右鍵按一下任一個 hello **UWP**專案，然後**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="1dce1-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="1dce1-183">按 F5 toostart hello hello 偵錯工具中的專案，然後確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="1dce1-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="1dce1-184">hello 401 回應不會因為 hello 後端的存取是僅限受限制的 tooauthorized 使用者。</span><span class="sxs-lookup"><span data-stu-id="1dce1-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="1dce1-185">開啟 MainPage.xaml.cs hello Windows 應用程式專案，並加入下列 hello`using`陳述式：</span><span class="sxs-lookup"><span data-stu-id="1dce1-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="1dce1-186">取代`<your_Portable_Class_Library_namespace>`與 hello 可攜式類別庫的命名空間。</span><span class="sxs-lookup"><span data-stu-id="1dce1-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="1dce1-187">更新 hello **MainPage**類別 tooimplement hello **IAuthenticate**介面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1dce1-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="1dce1-188">更新 hello **MainPage**類別藉由新增**MobileServiceUser**欄位和**驗證**方法所需的 hello **IAuthenticate**介面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1dce1-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="1dce1-189">如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider] 選擇不同的值。</span><span class="sxs-lookup"><span data-stu-id="1dce1-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="1dce1-190">新增下列一行程式碼 hello hello 建構函式中的 hello **MainPage**太類別 hello 呼叫之前`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="1dce1-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="1dce1-191">取代`<your_Portable_Class_Library_namespace>`與 hello 可攜式類別庫的命名空間。</span><span class="sxs-lookup"><span data-stu-id="1dce1-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="1dce1-192">如果您使用**UWP**，加入下列 hello **OnActivated**方法覆寫 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="1dce1-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="1dce1-193">Hello 方法覆寫已存在時，將上述程式碼片段的 hello hello 條件式程式碼。</span><span class="sxs-lookup"><span data-stu-id="1dce1-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="1dce1-194">通用 Windows 專案不需要此程式碼。</span><span class="sxs-lookup"><span data-stu-id="1dce1-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="1dce1-195">在 Package.appxmanifest 中新增 **{url_scheme_of_your_app}**。</span><span class="sxs-lookup"><span data-stu-id="1dce1-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="1dce1-196">重建 hello 應用程式，請執行此程式碼，然後使用 hello 驗證提供者選擇，並確認您能夠 tooaccess 資料，以驗證的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="1dce1-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dce1-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1dce1-197">Next steps</span></span>
<span data-ttu-id="1dce1-198">現在，您完成本教學課程中基本驗證，請考慮 tooone hello 遵循教學課程的上繼續進行：</span><span class="sxs-lookup"><span data-stu-id="1dce1-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="1dce1-199">新增推播通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="1dce1-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="1dce1-200">了解如何 tooadd 推播通知支援 tooyour 應用程式，並設定行動裝置應用程式後端 toouse Azure 通知中樞 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="1dce1-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="1dce1-201">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="1dce1-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="1dce1-202">了解如何離線 tooadd 支援使用行動裝置應用程式後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1dce1-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="1dce1-203">離線同步處理可讓終端使用者 toointeract 與行動裝置應用程式-檢視、 加入或修改資料集，即使在沒有網路連線。</span><span class="sxs-lookup"><span data-stu-id="1dce1-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
