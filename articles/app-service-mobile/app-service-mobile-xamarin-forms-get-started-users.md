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
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>新增驗證 tooyour Xamarin Forms 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>概觀
本主題說明如何 tooauthenticate 的 App Service 行動應用程式從用戶端應用程式的使用者。 本教學課程中，您可以將驗證加入使用身分識別提供者支援的應用程式服務的 hello Xamarin Forms 快速入門專案。 正在成功驗證和授權您的行動應用程式後，會顯示 hello 使用者識別碼的值，並會限制可以 tooaccess 資料表資料。

## <a name="prerequisites"></a>必要條件
本教學課程 hello 獲得最佳結果，我們建議您先完成 hello[建立 Xamarin Forms 應用程式][ 1]教學課程。 完成本教學課程之後，您將會有一個多平台 TodoList 應用程式的 Xamarin.Forms 專案。

如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 驗證擴充功能封裝 tooyour 專案。 如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK][2]。

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>註冊應用程式進行驗證，並設定應用程式服務
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url

安全的驗證會要求您為應用程式定義新的 URL 配置。 Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。 在本教學課程中，我們使用 hello URL 配置_appname_整個。 不過，您可以使用任何您選擇的 URL 結構描述。 它應該是唯一的 tooyour 行動應用程式。 hello 伺服器端 tooenable hello 重新導向：

1. 在 hello [Azure 入口網站]，選取您的應用程式服務。

2. 按一下 hello**驗證 / 授權**功能表選項。

3. 在 hello**允許外部重新導向 Url**，輸入`url_scheme_of_your_app://easyauth.callback`。  hello **url_scheme_of_your_app**這個字串中為 行動應用程式的 hello URL 配置。  它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。  請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。

4. 按一下 [確定] 。

5. 按一下 [儲存] 。

## <a name="restrict-permissions-tooauthenticated-users"></a>限制 tooauthenticated 使用者權限
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>加入驗證 toohello 可攜式類別程式庫
行動應用程式會使用 hello [LoginAsync] [ 3] hello 上的擴充方法[MobileServiceClient] [ 4] toosign 在使用者與應用程式服務驗證。 這個範例會使用在 hello 應用程式中顯示 hello 提供者的登入介面的管理伺服器的驗證流程。 如需詳細資訊，請參閱[伺服器管理的驗證][5]。 若要在實際執行應用程式中提供更好的使用者體驗，您應該考慮改用[用戶端管理的驗證][6]。

使用 Xamarin Forms 專案，tooauthenticate 定義**IAuthenticate** hello 應用程式的 hello 可攜式類別庫中的介面。 然後加入**登入**定義 hello 可攜式類別庫，您按一下按鈕 toohello 使用者介面 toostart 驗證。 在成功驗證之後，資料會載入從 hello 行動裝置應用程式後端。

實作 hello **IAuthenticate**每個平台應用程式所支援的介面。

1. 在 Visual Studio 或 Xamarin Studio，請從與 hello 專案中開啟 App.cs**可攜式**hello 名稱，亦即可攜式類別庫專案，然後加入下列 hello`using`陳述式：

        using System.Threading.Tasks;
2. 在 App.cs，加入 hello 下列`IAuthenticate`介面定義之前 hello`App`類別定義。

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. 平台特定實作的 tooinitialize hello 介面新增下列靜態成員 toohello hello**應用程式**類別。

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. 開啟 TodoList.xaml 從 hello 可攜式類別庫專案，加入下列 hello**按鈕**hello 中的項目*buttonsPanel*之後 hello 現有按鈕的配置元素：

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    此按鈕會向行動應用程式後端觸發伺服器管理的驗證。
5. 開啟 TodoList.xaml.cs 從 hello 可攜式類別庫專案，然後新增下列欄位 toohello hello`TodoList`類別：

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. 取代 hello **OnAppearing**方法，以下列程式碼的 hello:

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

    此程式碼可確保，只重新整理資料從 hello 服務之後已經過驗證。
7. 新增下列 hello 的處理常式的 hello**已按下**事件 toohello **TodoList**類別：

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. 儲存您的變更，並重建 hello 可攜式類別庫專案，確認沒有發生錯誤。

## <a name="add-authentication-toohello-android-app"></a>新增驗證 toohello Android 應用程式
此區段會顯示如何 tooimplement hello **IAuthenticate** hello Android 應用程式專案中的介面。 如果您不要支援 Android 裝置，請略過這一節。

1. 在 Visual Studio 或 Xamarin Studio，以滑鼠右鍵按一下 hello **droid**專案，然後**設定為啟始專案**。
2. 按 F5 toostart hello hello 偵錯工具中的專案，然後確認應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。 hello 401 程式碼會產生 hello 後端存取，所以 僅限受限制的 tooauthorized 使用者。
3. Hello Android 專案中，開啟 Weatherapp 並加入下列 hello`using`陳述式：

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. 更新 hello **MainActivity**類別 tooimplement hello **IAuthenticate**介面，如下所示：

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. 更新 hello **MainActivity**類別藉由新增**MobileServiceUser**欄位和**驗證**方法所需的 hello **IAuthenticate**介面，如下所示：

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

    如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider][7]選擇不同的值。

6. 新增下列程式碼內的 hello <application> AndroidManifest.xml 節點：

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

1. 新增下列程式碼 toohello hello **OnCreate**方法 hello **MainActivity**太類別 hello 呼叫之前`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    此程式碼可確保 hello 應用程式載入之前初始化 hello 驗證器。
2. 重建 hello 應用程式，請執行此程式碼，然後使用 hello 驗證提供者選擇，並確認您能夠 tooaccess 資料，以驗證的使用者登入。

## <a name="add-authentication-toohello-ios-app"></a>新增驗證 toohello iOS 應用程式
此區段會顯示如何 tooimplement hello **IAuthenticate** hello 的 iOS 應用程式專案中的介面。 如果您不要支援 iOS 裝置，請略過這一節。

1. 在 Visual Studio 或 Xamarin Studio，以滑鼠右鍵按一下 hello **iOS**專案，然後**設定為啟始專案**。
2. 按 F5 toostart hello hello 偵錯工具中的專案，然後確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。 因為 hello 後端的存取限制的 tooauthorized 使用者才不會產生 hello 401 回應。
3. Hello 的 iOS 專案中開啟 d，然後加入下列 hello`using`陳述式：

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. 更新 hello **AppDelegate**類別 tooimplement hello **IAuthenticate**介面，如下所示：

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. 更新 hello **AppDelegate**類別藉由新增**MobileServiceUser**欄位和**驗證**方法所需的 hello **IAuthenticate**介面，如下所示：

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

    如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider] 選擇不同的值。

6. 加入 OpenUrl （uiapplication # 應用程式，NSUrl url NSDictionary 選項） 方法多載，以更新 hello AppDelegate 類別

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. 新增下列一行程式碼 toohello hello **FinishedLaunching**太呼叫方法，再 hello`LoadApplication()`:

        App.Init(this);

    此程式碼可確保載入 hello 應用程式之前，會初始化 hello 驗證器。

6. 新增**{url_scheme_of_your_app}** tooURL Info.plist 中的配置。

7. 重建 hello 應用程式，請執行此程式碼，然後使用 hello 驗證提供者選擇，並確認您能夠 tooaccess 資料，以驗證的使用者登入。

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>新增驗證 tooWindows 10 （包括電話） 應用程式專案
此區段會顯示如何 tooimplement hello **IAuthenticate** hello Windows 10 應用程式專案中的介面。 相同的步驟適用於通用 Windows 平台 (UWP) 專案，但使用 hello hello **UWP**專案 （標註的變更）。 如果您不要支援 Windows 裝置，請略過這一節。

1. 「 在 Visual Studio 中，以滑鼠右鍵按一下任一個 hello **UWP**專案，然後**設定為啟始專案**。
2. 按 F5 toostart hello hello 偵錯工具中的專案，然後確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。 hello 401 回應不會因為 hello 後端的存取是僅限受限制的 tooauthorized 使用者。
3. 開啟 MainPage.xaml.cs hello Windows 應用程式專案，並加入下列 hello`using`陳述式：

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    取代`<your_Portable_Class_Library_namespace>`與 hello 可攜式類別庫的命名空間。
4. 更新 hello **MainPage**類別 tooimplement hello **IAuthenticate**介面，如下所示：

        public sealed partial class MainPage : IAuthenticate
5. 更新 hello **MainPage**類別藉由新增**MobileServiceUser**欄位和**驗證**方法所需的 hello **IAuthenticate**介面，如下所示：

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

    如果您使用 Facebook 以外的識別提供者，請為 [MobileServiceAuthenticationProvider] 選擇不同的值。

1. 新增下列一行程式碼 hello hello 建構函式中的 hello **MainPage**太類別 hello 呼叫之前`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    取代`<your_Portable_Class_Library_namespace>`與 hello 可攜式類別庫的命名空間。

3. 如果您使用**UWP**，加入下列 hello **OnActivated**方法覆寫 toohello**應用程式**類別：

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Hello 方法覆寫已存在時，將上述程式碼片段的 hello hello 條件式程式碼。  通用 Windows 專案不需要此程式碼。

3. 在 Package.appxmanifest 中新增 **{url_scheme_of_your_app}**。 

4. 重建 hello 應用程式，請執行此程式碼，然後使用 hello 驗證提供者選擇，並確認您能夠 tooaccess 資料，以驗證的使用者登入。

## <a name="next-steps"></a>後續步驟
現在，您完成本教學課程中基本驗證，請考慮 tooone hello 遵循教學課程的上繼續進行：

* [新增推播通知 tooyour 應用程式](app-service-mobile-xamarin-forms-get-started-push.md)

  了解如何 tooadd 推播通知支援 tooyour 應用程式，並設定行動裝置應用程式後端 toouse Azure 通知中樞 toosend 推播通知。
* [啟用應用程式的離線同步處理](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  了解如何離線 tooadd 支援使用行動裝置應用程式後端應用程式。 離線同步處理可讓終端使用者 toointeract 與行動裝置應用程式-檢視、 加入或修改資料集，即使在沒有網路連線。

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
