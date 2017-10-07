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
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>新增驗證 tooyour Xamarin.Android 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

本主題說明如何 tooauthenticate 使用者的行動裝置應用程式，從用戶端應用程式。 在本教學課程中，您可以新增使用身分識別提供者支援的 Azure 行動應用程式驗證 toohello 快速入門專案。 正在順利通過驗證，並在 hello 行動裝置應用程式中獲得授權之後, 會顯示 hello 使用者識別碼的值。

本教學課程根據 hello 行動裝置應用程式快速入門。 您必須也先完成 hello 教學課程[建立 Xamarin.Android 應用程式]。 如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 驗證擴充功能封裝 tooyour 專案。 如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。

## <a name="register"></a>註冊應用程式進行驗證，並設定應用程式服務
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url

安全的驗證會要求您為應用程式定義新的 URL 配置。 Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。 在本教學課程中，我們使用 hello URL 配置_appname_整個。 不過，您可以使用任何您選擇的 URL 結構描述。 它應該是唯一的 tooyour 行動應用程式。 hello 伺服器端 tooenable hello 重新導向：

1. 在 hello [Azure 入口網站]，選取您的應用程式服務。

2. 按一下 hello**驗證 / 授權**功能表選項。

3. 在 hello**允許外部重新導向 Url**，輸入`url_scheme_of_your_app://easyauth.callback`。  hello **url_scheme_of_your_app**這個字串中為 行動應用程式的 hello URL 配置。  它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。  請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。

4. 按一下 [確定] 。

5. 按一下 [儲存] 。

## <a name="permissions"></a>限制 tooauthenticated 使用者權限
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

在 Visual Studio 或 Xamarin Studio，請裝置或模擬器上執行 hello 用戶端專案。 請確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。 這是因為 hello 應用程式嘗試 tooaccess 未經驗證的使用者身分行動裝置應用程式後端。 hello *TodoItem*資料表現在需要驗證。

接下來，您將更新從 hello 行動裝置應用程式後端 hello 用戶端應用程式 toorequest 資源與已驗證的使用者。

## <a name="add-authentication"></a>新增驗證 toohello 應用程式
hello 應用程式會更新的 toorequire 使用者 tootap hello**登入**按鈕，然後資料會顯示之前，先驗證。

1. 新增下列程式碼 toohello hello **TodoActivity**類別：
   
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
   
    這樣會建立新的方法 tooauthenticate 使用者以及方法的處理常式的新**登入** 按鈕。 上述的 hello 範例程式碼中的 hello 使用者會驗證使用 Facebook 登入。 對話是一次驗證使用的 toodisplay hello 使用者識別碼。
   
   > [!NOTE]
   > 如果您使用 Facebook 以外的身分識別提供者，變更 hello 值太傳遞**LoginAsync** tooone hello 以下的上方： *MicrosoftAccount*， *Twitter*，*Google*，或*WindowsAzureActiveDirectory*。
   > 
   > 
2. 在 hello **OnCreate**方法、 刪除或下列一行程式碼的註解外 hello:
   
        OnRefreshItemsSelected ();
3. 在 hello Activity_To_Do.axml 檔案中，加入下列 hello *LoginUser*按鈕前 hello 現有*AddItem*按鈕：
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. 新增下列項目 toohello Strings.xml 資源檔的 hello:
   
        <string name="login_button_text">Sign in</string>
5. 開啟 hello AndroidManifest.xml 檔案，加入下列程式碼內的 hello `<application>` XML 項目：

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. 在 Visual Studio 或 Xamarin Studio 中，裝置或模擬器上執行 hello 用戶端專案，並使用您所選擇的身分識別提供者登入。 當您已成功登入，hello 應用程式將會顯示登入識別碼，而且 hello 份 todo 項目，以及您可以繼續更新 toohello 資料。

<!-- URLs. -->
[建立 Xamarin.Android 應用程式]: app-service-mobile-xamarin-android-get-started.md