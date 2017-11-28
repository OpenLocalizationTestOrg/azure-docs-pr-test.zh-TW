---
title: "透過 Xamarin Android 行動應用程式驗證 aaaGet 已啟動"
description: "深入了解如何您的 Xamarin Android 應用程式，透過不同的身分識別提供者，包括 AAD、 Google、 Facebook、 Twitter 和 Microsoft toouse 行動應用程式 tooauthenticate 使用者。"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="0bc8a-103">新增驗證 tooyour Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="0bc8a-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="0bc8a-104">本主題說明如何 tooauthenticate 使用者的行動裝置應用程式，從用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="0bc8a-105">在本教學課程中，您可以新增使用身分識別提供者支援的 Azure 行動應用程式驗證 toohello 快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="0bc8a-106">正在順利通過驗證，並在 hello 行動裝置應用程式中獲得授權之後, 會顯示 hello 使用者識別碼的值。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="0bc8a-107">本教學課程根據 hello 行動裝置應用程式快速入門。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="0bc8a-108">您必須也先完成 hello 教學課程[建立 Xamarin.Android 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="0bc8a-109">如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 驗證擴充功能封裝 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="0bc8a-110">如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="0bc8a-111"><a name="register"></a>註冊應用程式進行驗證，並設定應用程式服務</span><span class="sxs-lookup"><span data-stu-id="0bc8a-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="0bc8a-112"><a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url</span><span class="sxs-lookup"><span data-stu-id="0bc8a-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="0bc8a-113">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="0bc8a-114">Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="0bc8a-115">在本教學課程中，我們使用 hello URL 配置_appname_整個。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="0bc8a-116">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="0bc8a-117">它應該是唯一的 tooyour 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="0bc8a-118">hello 伺服器端 tooenable hello 重新導向：</span><span class="sxs-lookup"><span data-stu-id="0bc8a-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="0bc8a-119">在 hello [Azure 入口網站]，選取您的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="0bc8a-120">按一下 hello**驗證 / 授權**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="0bc8a-121">在 hello**允許外部重新導向 Url**，輸入`url_scheme_of_your_app://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="0bc8a-122">hello **url_scheme_of_your_app**這個字串中為 行動應用程式的 hello URL 配置。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="0bc8a-123">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="0bc8a-124">請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="0bc8a-125">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-125">Click **OK**.</span></span>

5. <span data-ttu-id="0bc8a-126">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-126">Click **Save**.</span></span>

## <span data-ttu-id="0bc8a-127"><a name="permissions"></a>限制 tooauthenticated 使用者權限</span><span class="sxs-lookup"><span data-stu-id="0bc8a-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="0bc8a-128">在 Visual Studio 或 Xamarin Studio，請裝置或模擬器上執行 hello 用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="0bc8a-129">請確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="0bc8a-130">這是因為 hello 應用程式嘗試 tooaccess 未經驗證的使用者身分行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="0bc8a-131">hello *TodoItem*資料表現在需要驗證。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="0bc8a-132">接下來，您將更新從 hello 行動裝置應用程式後端 hello 用戶端應用程式 toorequest 資源與已驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="0bc8a-133"><a name="add-authentication"></a>新增驗證 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0bc8a-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="0bc8a-134">hello 應用程式會更新的 toorequire 使用者 tootap hello**登入**按鈕，然後資料會顯示之前，先驗證。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="0bc8a-135">新增下列程式碼 toohello hello **TodoActivity**類別：</span><span class="sxs-lookup"><span data-stu-id="0bc8a-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="0bc8a-136">這樣會建立新的方法 tooauthenticate 使用者以及方法的處理常式的新**登入** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="0bc8a-137">上述的 hello 範例程式碼中的 hello 使用者會驗證使用 Facebook 登入。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="0bc8a-138">對話是一次驗證使用的 toodisplay hello 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0bc8a-139">如果您使用 Facebook 以外的身分識別提供者，變更 hello 值太傳遞**LoginAsync** tooone hello 以下的上方： *MicrosoftAccount*， *Twitter*，*Google*，或*WindowsAzureActiveDirectory*。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="0bc8a-140">在 hello **OnCreate**方法、 刪除或下列一行程式碼的註解外 hello:</span><span class="sxs-lookup"><span data-stu-id="0bc8a-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="0bc8a-141">在 hello Activity_To_Do.axml 檔案中，加入下列 hello *LoginUser*按鈕前 hello 現有*AddItem*按鈕：</span><span class="sxs-lookup"><span data-stu-id="0bc8a-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="0bc8a-142">新增下列項目 toohello Strings.xml 資源檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="0bc8a-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="0bc8a-143">開啟 hello AndroidManifest.xml 檔案，加入下列程式碼內的 hello `<application>` XML 項目：</span><span class="sxs-lookup"><span data-stu-id="0bc8a-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="0bc8a-144">在 Visual Studio 或 Xamarin Studio 中，裝置或模擬器上執行 hello 用戶端專案，並使用您所選擇的身分識別提供者登入。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="0bc8a-145">當您已成功登入，hello 應用程式將會顯示登入識別碼，而且 hello 份 todo 項目，以及您可以繼續更新 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="0bc8a-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[建立 Xamarin.Android 應用程式]: app-service-mobile-xamarin-android-get-started.md