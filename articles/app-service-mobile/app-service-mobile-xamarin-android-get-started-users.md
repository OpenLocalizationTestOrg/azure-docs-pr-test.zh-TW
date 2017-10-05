---
title: "開始在 Xamarin Android 中使用行動應用程式的驗證"
description: "了解如何使用行動應用程式透過眾多識別提供者驗證 Xamarin Android 應用程式使用者，包括 AAD、Google、Facebook、Twitter 和 Microsoft。"
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
ms.openlocfilehash: 8f9a1109018c708d52cdcb7b8bce43861cecd31c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="35494-103">將驗證新增至 Xamarin.Android 應用程式</span><span class="sxs-lookup"><span data-stu-id="35494-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="35494-104">本主題說明如何從用戶端應用程式驗證行動應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="35494-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="35494-105">在本教學課程中，您會使用 Azure 行動應用程式所支援的身分識別提供者將驗證新增至快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="35494-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="35494-106">在行動應用程式中成功驗證並授權之後，就會顯示使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="35494-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="35494-107">本教學課程以行動應用程式快速入門為基礎。</span><span class="sxs-lookup"><span data-stu-id="35494-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="35494-108">您也必須先完成 [建立 Xamarin.Android 應用程式教學課程]。</span><span class="sxs-lookup"><span data-stu-id="35494-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="35494-109">如果您不要使用下載的快速入門伺服器專案，必須將驗證擴充套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="35494-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="35494-110">如需伺服器擴充套件的詳細資訊，請參閱 [使用 Azure 行動應用程式的 .NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="35494-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="35494-111"><a name="register"></a>註冊應用程式進行驗證，並設定應用程式服務</span><span class="sxs-lookup"><span data-stu-id="35494-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="35494-112"><a name="redirecturl"></a>將您的應用程式新增至允許的外部重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="35494-112"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="35494-113">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="35494-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="35494-114">這讓驗證系統能夠在驗證程序完成之後，重新導向回到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="35494-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="35494-115">我們會在這整個教學課程中使用 URL 配置 appname。</span><span class="sxs-lookup"><span data-stu-id="35494-115">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="35494-116">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="35494-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="35494-117">它對於您的行動應用程式而言應該是唯一的。</span><span class="sxs-lookup"><span data-stu-id="35494-117">It should be unique to your mobile application.</span></span> <span data-ttu-id="35494-118">在伺服器端啟用重新導向：</span><span class="sxs-lookup"><span data-stu-id="35494-118">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="35494-119">在 [Azure 入口網站] 中，選取您的 App Service。</span><span class="sxs-lookup"><span data-stu-id="35494-119">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="35494-120">按一下 [驗證/授權] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="35494-120">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="35494-121">在 [允許的外部重新導向 URL] 中，輸入 `url_scheme_of_your_app://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="35494-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="35494-122">此字串中的 **url_scheme_of_your_app** 是您行動應用程式的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="35494-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="35494-123">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="35494-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="35494-124">請記下您選擇的字串，因為您將需要在數個位置中使用該 URL 配置來調整您的行動應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="35494-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="35494-125">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="35494-125">Click **OK**.</span></span>

5. <span data-ttu-id="35494-126">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="35494-126">Click **Save**.</span></span>

## <span data-ttu-id="35494-127"><a name="permissions"></a>限制只有通過驗證的使用者具有權限</span><span class="sxs-lookup"><span data-stu-id="35494-127"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="35494-128">在 Visual Studio 或 Xamarin Studio 中，在裝置或模擬器上執行用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="35494-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="35494-129">確認在應用程式啟動後，發生狀態代碼 401 (未經授權) 的未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="35494-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="35494-130">這是因為應用程式嘗試以未驗證的使用者身分存取您的行動應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="35494-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="35494-131">*TodoItem* 資料表現在需要驗證。</span><span class="sxs-lookup"><span data-stu-id="35494-131">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="35494-132">接下來，您將會更新用戶端應用程式，利用已驗證的使用者身分來要求行動應用程式後端的資源。</span><span class="sxs-lookup"><span data-stu-id="35494-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="35494-133"><a name="add-authentication"></a>將驗證新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="35494-133"><a name="add-authentication"></a>Add authentication to the app</span></span>
<span data-ttu-id="35494-134">應用程式已更新，要求使用者在資料顯示前點選 [登入]  按鈕並驗證。</span><span class="sxs-lookup"><span data-stu-id="35494-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="35494-135">將下列程式碼加入 **TodoActivity** 類別：</span><span class="sxs-lookup"><span data-stu-id="35494-135">Add the following code to the **TodoActivity** class:</span></span>
   
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
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="35494-136">這會建立一個新方法以驗證使用者，以及建立新 [登入]  按鈕的方法處理常式。</span><span class="sxs-lookup"><span data-stu-id="35494-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="35494-137">上述範例程式碼中的使用者是使用 Facebook 登入進行驗證。</span><span class="sxs-lookup"><span data-stu-id="35494-137">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="35494-138">對話方塊會在驗證後用來顯示使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="35494-138">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="35494-139">如果您使用的身分識別提供者不是 Facebook，請將傳遞給上述 **LoginAsync** 的值變更為下列其中之一：MicrosoftAccount、Twitter、Google 或 WindowsAzureActiveDirectory。</span><span class="sxs-lookup"><span data-stu-id="35494-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="35494-140">在 **OnCreate** 方法中，刪除或註解下列程式碼行：</span><span class="sxs-lookup"><span data-stu-id="35494-140">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="35494-141">在 Activity_To_Do.axml 檔案中，在現有的 AddItem 按鈕之前加入下列 LoginUser 按鈕定義：</span><span class="sxs-lookup"><span data-stu-id="35494-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="35494-142">將下列元素新增到 Strings.xml 資源檔：</span><span class="sxs-lookup"><span data-stu-id="35494-142">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="35494-143">開啟 AndroidManifest.xml 檔案，在 `<application>` XML 元素內新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="35494-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="35494-144">在 Visual Studio 或 Xamarin Studio 中，在裝置或模擬器上執行用戶端專案，並使用您選擇的身分識別提供者登入。</span><span class="sxs-lookup"><span data-stu-id="35494-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="35494-145">當您成功登入後，應用程式將會顯示您的登入識別碼以及 todo 項目的清單，您可以對資料進行更新。</span><span class="sxs-lookup"><span data-stu-id="35494-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
<span data-ttu-id="35494-146">[建立 Xamarin.Android 應用程式教學課程]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="35494-146">[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>