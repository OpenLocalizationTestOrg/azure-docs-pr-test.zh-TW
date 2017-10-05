---
title: "開始在 Xamarin.Forms 應用程式中使用 Mobile Apps 的驗證 | Microsoft Docs"
description: "了解如何使用 Mobile Apps 透過眾多識別提供者驗證 Xamarin Forms 應用程式使用者，包括 AAD、Google、Facebook、Twitter 和 Microsoft。"
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
ms.openlocfilehash: 9e14e95793bcc81ad46783fd50ba223eec4ea360
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="7da5b-103">將驗證新增至 Xamarin Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="7da5b-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="7da5b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7da5b-104">Overview</span></span>
<span data-ttu-id="7da5b-105">本主題說明如何從用戶端應用程式驗證 App Service 行動應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="7da5b-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="7da5b-106">在本教學課程中，您將使用 App Service 支援的識別提供者，將驗證新增至 Xamarin.Forms 快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="7da5b-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="7da5b-107">由行動應用程式成功驗證並授權之後，就會顯示使用者識別碼值，而您也將可以存取受限制的資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="7da5b-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7da5b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7da5b-108">Prerequisites</span></span>
<span data-ttu-id="7da5b-109">為了讓本教學課程產生最佳結果，建議您先完成 [建立 Xamarin.Forms 應用程式][1]教學課程。</span><span class="sxs-lookup"><span data-stu-id="7da5b-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="7da5b-110">完成本教學課程之後，您將會有一個多平台 TodoList 應用程式的 Xamarin.Forms 專案。</span><span class="sxs-lookup"><span data-stu-id="7da5b-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="7da5b-111">如果您不要使用下載的快速入門伺服器專案，必須將驗證擴充套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="7da5b-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="7da5b-112">如需伺服器擴充套件的詳細資訊，請參閱[使用 Azure Mobile Apps 的 .NET 後端伺服器 SDK][2]。</span><span class="sxs-lookup"><span data-stu-id="7da5b-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="7da5b-113">註冊應用程式進行驗證，並設定應用程式服務</span><span class="sxs-lookup"><span data-stu-id="7da5b-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="7da5b-114"><a name="redirecturl"></a>將您的應用程式新增至允許的外部重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="7da5b-114"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="7da5b-115">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="7da5b-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="7da5b-116">這讓驗證系統能夠在驗證程序完成之後，重新導向回到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da5b-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="7da5b-117">我們會在這整個教學課程中使用 URL 配置 appname。</span><span class="sxs-lookup"><span data-stu-id="7da5b-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="7da5b-118">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="7da5b-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="7da5b-119">它對於您的行動應用程式而言應該是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7da5b-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="7da5b-120">在伺服器端啟用重新導向：</span><span class="sxs-lookup"><span data-stu-id="7da5b-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="7da5b-121">在 [Azure 入口網站] 中，選取您的 App Service。</span><span class="sxs-lookup"><span data-stu-id="7da5b-121">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="7da5b-122">按一下 [驗證/授權] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="7da5b-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="7da5b-123">在 [允許的外部重新導向 URL] 中，輸入 `url_scheme_of_your_app://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="7da5b-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="7da5b-124">此字串中的 **url_scheme_of_your_app** 是您行動應用程式的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="7da5b-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="7da5b-125">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="7da5b-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="7da5b-126">請記下您選擇的字串，因為您將需要在數個位置中使用該 URL 配置來調整您的行動應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="7da5b-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="7da5b-127">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7da5b-127">Click **OK**.</span></span>

5. <span data-ttu-id="7da5b-128">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7da5b-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="7da5b-129">限制只有通過驗證的使用者具有權限</span><span class="sxs-lookup"><span data-stu-id="7da5b-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="7da5b-130">將驗證加入可攜式類別庫中</span><span class="sxs-lookup"><span data-stu-id="7da5b-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="7da5b-131">Mobile Apps 會使用 [MobileServiceClient][4] 的 [LoginAsync][3] 擴充方法，透過 App Service 驗證將使用者登入。</span><span class="sxs-lookup"><span data-stu-id="7da5b-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="7da5b-132">這個範例使用伺服器管理的驗證流程，在應用程式中顯示提供者的登入介面。</span><span class="sxs-lookup"><span data-stu-id="7da5b-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="7da5b-133">如需詳細資訊，請參閱[伺服器管理的驗證][5]。</span><span class="sxs-lookup"><span data-stu-id="7da5b-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="7da5b-134">若要在實際執行應用程式中提供更好的使用者體驗，您應該考慮改用[用戶端管理的驗證][6]。</span><span class="sxs-lookup"><span data-stu-id="7da5b-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="7da5b-135">為了驗證 Xamarin Forms 專案，請在應用程式的可攜式類別庫中定義 **IAuthenticate** 介面。</span><span class="sxs-lookup"><span data-stu-id="7da5b-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="7da5b-136">然後，將 [登入]  按鈕新增至可攜式類別庫中定義的使用者介面，讓您按一下來開始驗證。</span><span class="sxs-lookup"><span data-stu-id="7da5b-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="7da5b-137">驗證成功後，將會從行動應用程式後端載入資料。</span><span class="sxs-lookup"><span data-stu-id="7da5b-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="7da5b-138">為應用程式支援的每個平台實作 **IAuthenticate** 介面。</span><span class="sxs-lookup"><span data-stu-id="7da5b-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="7da5b-139">在 Visual Studio 或 Xamarin Studio 中，從名稱中有 **Portable** 的專案中開啟 App.cs，也就是可攜式類別庫專案，然後新增下列 `using` 陳述式︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="7da5b-140">在 App.cs 中，在 `App` 類別定義之前緊接著加入下列 `IAuthenticate` 介面定義。</span><span class="sxs-lookup"><span data-stu-id="7da5b-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="7da5b-141">將下列靜態成員新增至 **App** 類別，以使用平台特定實作來初始化介面。</span><span class="sxs-lookup"><span data-stu-id="7da5b-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="7da5b-142">從可攜式類別庫專案中開啟 TodoList.xaml，在 buttonsPanel  配置項目中，將下列 *Button* 項目新增至現有按鈕後面︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="7da5b-143">此按鈕會向行動應用程式後端觸發伺服器管理的驗證。</span><span class="sxs-lookup"><span data-stu-id="7da5b-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="7da5b-144">從可攜式類別庫專案中開啟 TodoList.xaml.cs，然後將下列欄位加入至 `TodoList` 類別︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="7da5b-145">使用下列程式碼取代 **OnAppearing** 方法：</span><span class="sxs-lookup"><span data-stu-id="7da5b-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="7da5b-146">此程式碼可確保只有在您通過驗證之後，才會從服務重新整理資料。</span><span class="sxs-lookup"><span data-stu-id="7da5b-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="7da5b-147">將下列有關 **Clicked** 事件的處理常式新增至 **TodoList** 類別︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="7da5b-148">儲存變更，並建置可攜式類別庫專案，以驗證沒有錯誤。</span><span class="sxs-lookup"><span data-stu-id="7da5b-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="7da5b-149">將驗證加入 Android 應用程式中</span><span class="sxs-lookup"><span data-stu-id="7da5b-149">Add authentication to the Android app</span></span>
<span data-ttu-id="7da5b-150">本節說明如何在 Android 應用程式專案中實作 **IAuthenticate** 介面。</span><span class="sxs-lookup"><span data-stu-id="7da5b-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="7da5b-151">如果您不要支援 Android 裝置，請略過這一節。</span><span class="sxs-lookup"><span data-stu-id="7da5b-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="7da5b-152">在 Visual Studio 或 Xamarin Studio 中，以滑鼠右鍵按一下 **droid** 專案，然後按一下 [設定為啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="7da5b-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="7da5b-153">按下 F5 在偵錯工具中啟動專案，然後確認在應用程式啟動後，發生狀態代碼 401 (未經授權) 的未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7da5b-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="7da5b-154">產生 401 代碼是因為只有獲授權的使用者才能存取後端。</span><span class="sxs-lookup"><span data-stu-id="7da5b-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="7da5b-155">開啟 Android 專案中的 MainActivity.cs，然後加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7da5b-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="7da5b-156">更新 **MainActivity** 類別來實作 **IAuthenticate** 介面，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="7da5b-157">更新 **MainActivity** 類別，新增 **IAuthenticate** 介面所需的 **MobileServiceUser** 欄位和 **Authenticate** 方法，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="7da5b-158">如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider][7]選擇不同的值。</span><span class="sxs-lookup"><span data-stu-id="7da5b-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="7da5b-159">在 AndroidManifest.xml 的 <application> 節點內新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7da5b-159">Add the following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="7da5b-160">在 **MainActivity** 類別的 **OnCreate** 方法中，在呼叫 `LoadApplication()` 之前新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7da5b-160">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="7da5b-161">此程式碼可確保在應用程式載入之前初始化驗證器。</span><span class="sxs-lookup"><span data-stu-id="7da5b-161">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="7da5b-162">重新建置應用程式，執行它，然後以您選擇的驗證提供者登入，並確認您能夠以已驗證的使用者身分存取資料表。</span><span class="sxs-lookup"><span data-stu-id="7da5b-162">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="7da5b-163">將驗證加入 iOS 應用程式中</span><span class="sxs-lookup"><span data-stu-id="7da5b-163">Add authentication to the iOS app</span></span>
<span data-ttu-id="7da5b-164">本節說明如何在 iOS 應用程式專案中實作 **IAuthenticate** 介面。</span><span class="sxs-lookup"><span data-stu-id="7da5b-164">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="7da5b-165">如果您不要支援 iOS 裝置，請略過這一節。</span><span class="sxs-lookup"><span data-stu-id="7da5b-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="7da5b-166">在 Visual Studio 或 Xamarin Studio 中，以滑鼠右鍵按一下 **iOS** 專案，然後按一下 [設定為啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="7da5b-166">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="7da5b-167">按下 F5 在偵錯工具中啟動專案，然後確認在應用程式啟動後，發生狀態代碼 401 (未經授權) 的未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7da5b-167">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="7da5b-168">產生 401 回應是因為只有獲授權的使用者才能存取後端。</span><span class="sxs-lookup"><span data-stu-id="7da5b-168">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="7da5b-169">開啟 iOS 專案中的 AppDelegate.cs，然後加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7da5b-169">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="7da5b-170">更新 **AppDelegate** 類別來實作 **IAuthenticate** 介面，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-170">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="7da5b-171">更新 **AppDelegate** 類別，新增 **IAuthenticate** 介面所需的 **MobileServiceUser** 欄位和 **Authenticate** 方法，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-171">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="7da5b-172">如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider] 選擇不同的值。</span><span class="sxs-lookup"><span data-stu-id="7da5b-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="7da5b-173">新增 OpenUrl(UIApplication app, NSUrl url, NSDictionary options) 方法多載來更新 AppDelegate 類別</span><span class="sxs-lookup"><span data-stu-id="7da5b-173">Update the AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="7da5b-174">在 **FinishedLaunching** 方法中，在呼叫 `LoadApplication()` 之前新增下面這行程式碼：</span><span class="sxs-lookup"><span data-stu-id="7da5b-174">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="7da5b-175">此程式碼可確保在應用程式載入之前初始化驗證器。</span><span class="sxs-lookup"><span data-stu-id="7da5b-175">This code ensures the authenticator is initialized before the app is loaded.</span></span>

6. <span data-ttu-id="7da5b-176">新增 **{url_scheme_of_your_app}** 到 Info.plist 中的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="7da5b-176">Add **{url_scheme_of_your_app}** to URL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="7da5b-177">重新建置應用程式，執行它，然後以您選擇的驗證提供者登入，並確認您能夠以已驗證的使用者身分存取資料表。</span><span class="sxs-lookup"><span data-stu-id="7da5b-177">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="7da5b-178">將驗證新增至 Windows 10 (包括 Phone) 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="7da5b-178">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="7da5b-179">本節說明如何在 Windows 10 應用程式專案中實作 **IAuthenticate** 介面。</span><span class="sxs-lookup"><span data-stu-id="7da5b-179">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="7da5b-180">相同的步驟適用於通用 Windows 平台 (UWP) 專案，但使用 **UWP** 專案 (內含已標註的變更)。</span><span class="sxs-lookup"><span data-stu-id="7da5b-180">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="7da5b-181">如果您不要支援 Windows 裝置，請略過這一節。</span><span class="sxs-lookup"><span data-stu-id="7da5b-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="7da5b-182">在 Visual Studio 中，以滑鼠右鍵按一下 **UWP** 專案，然後按一下 [設定為啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="7da5b-182">"In Visual Studio, right-click either the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="7da5b-183">按下 F5 在偵錯工具中啟動專案，然後確認在應用程式啟動後，發生狀態代碼 401 (未經授權) 的未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7da5b-183">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="7da5b-184">發生 401 回應是因為只有獲授權的使用者才能存取後端。</span><span class="sxs-lookup"><span data-stu-id="7da5b-184">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="7da5b-185">開啟 Windows 應用程式專案的 MainPage.xaml.cs，然後加入下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="7da5b-185">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="7da5b-186">以您的可攜式類別庫的命名空間取代 `<your_Portable_Class_Library_namespace>` 。</span><span class="sxs-lookup"><span data-stu-id="7da5b-186">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="7da5b-187">更新 **MainPage** 類別來實作 **IAuthenticate** 介面，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-187">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="7da5b-188">更新 **MainPage** 類別，新增 **IAuthenticate** 介面所需的 **MobileServiceUser** 欄位和 **Authenticate** 方法，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7da5b-188">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="7da5b-189">如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider] 選擇不同的值。</span><span class="sxs-lookup"><span data-stu-id="7da5b-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="7da5b-190">在 **MainPage** 類別的建構函式中，在呼叫 `LoadApplication()` 之前新增下面這行程式碼：</span><span class="sxs-lookup"><span data-stu-id="7da5b-190">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="7da5b-191">以您的可攜式類別庫的命名空間取代 `<your_Portable_Class_Library_namespace>` 。</span><span class="sxs-lookup"><span data-stu-id="7da5b-191">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="7da5b-192">如果您使用 **UWP**，請將下列 **OnActivated** 方法覆寫新增至 **App** 類別：</span><span class="sxs-lookup"><span data-stu-id="7da5b-192">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="7da5b-193">當此方法覆寫已存在時，請新增上述程式碼片段中的條件式程式碼。</span><span class="sxs-lookup"><span data-stu-id="7da5b-193">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="7da5b-194">通用 Windows 專案不需要此程式碼。</span><span class="sxs-lookup"><span data-stu-id="7da5b-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="7da5b-195">在 Package.appxmanifest 中新增 **{url_scheme_of_your_app}**。</span><span class="sxs-lookup"><span data-stu-id="7da5b-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="7da5b-196">重新建置應用程式，執行它，然後以您選擇的驗證提供者登入，並確認您能夠以已驗證的使用者身分存取資料表。</span><span class="sxs-lookup"><span data-stu-id="7da5b-196">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7da5b-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7da5b-197">Next steps</span></span>
<span data-ttu-id="7da5b-198">現在您已經完成了這個基本驗證的教學課程，可以考慮繼續進行下列其中一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="7da5b-198">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="7da5b-199">將推播通知新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="7da5b-199">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="7da5b-200">了解如何將推播通知支援新增至應用程式，並設定行動應用程式後端以使用 Azure 通知中樞傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="7da5b-200">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="7da5b-201">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="7da5b-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="7da5b-202">了解如何使用行動應用程式後端，將離線支援新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da5b-202">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="7da5b-203">離線同步處理可讓使用者與行動應用程式進行互動 (檢視、新增或修改資料)，即使沒有網路連接也可以。</span><span class="sxs-lookup"><span data-stu-id="7da5b-203">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
