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
# <a name="add-authentication-tooyour-xamarinios-app"></a>新增驗證 tooyour Xamarin.iOS 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

本主題說明如何 tooauthenticate 的 App Service 行動應用程式從用戶端應用程式的使用者。 在本教學課程中，您可以新增使用身分識別提供者支援的應用程式服務的驗證 toohello Xamarin.iOS 快速入門專案。 正在成功驗證和授權您的行動應用程式之後，會顯示 hello 使用者識別碼的值，而且您必須能夠 tooaccess 限制資料表的資料。

您必須先完成 hello 教學課程[建立 Xamarin.iOS 應用程式]。 如果您不要使用 hello 下載快速入門的伺服器專案，您必須新增 hello 驗證擴充功能封裝 tooyour 專案。 如需伺服器擴充功能封裝的詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>註冊應用程式進行驗證，並設定應用程式服務
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>新增您的應用程式 toohello 允許外部重新導向 Url

安全的驗證會要求您為應用程式定義新的 URL 配置。 Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。 在本教學課程中，我們使用 hello URL 配置_appname_整個。 不過，您可以使用任何您選擇的 URL 結構描述。 它應該是唯一的 tooyour 行動應用程式。 hello 伺服器端 tooenable hello 重新導向：

1. 在 hello [Azure 入口網站]，選取您的應用程式服務。

2. 按一下 hello**驗證 / 授權**功能表選項。

3. 在 [hello**允許外部重新導向 Url**，輸入`url_scheme_of_your_app://easyauth.callback`。  hello **url_scheme_of_your_app**這個字串中為 [行動應用程式的 hello URL 配置。  它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。  請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。

4. 按一下 [確定] 。

5. 按一下 [儲存] 。

## <a name="restrict-permissions-tooauthenticated-users"></a>限制 tooauthenticated 使用者權限
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. 在 Visual Studio 或 Xamarin Studio，請裝置或模擬器上執行 hello 用戶端專案。 請確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。 hello 失敗是 hello 偵錯工具的記錄的 toohello 主控台。 因此在 Visual Studio 中，您應該會看到 hello [輸出] 視窗中的 hello 失敗。

&nbsp;&nbsp;此未授權的失敗不會因為 hello 應用程式嘗試 tooaccess 未經驗證的使用者身分行動裝置應用程式後端。 hello *TodoItem*資料表現在需要驗證。

接下來，您將更新從 hello 行動裝置應用程式後端 hello 用戶端應用程式 toorequest 資源與已驗證的使用者。

## <a name="add-authentication-toohello-app"></a>新增驗證 toohello 應用程式
在本節中，您將修改 hello 應用程式 toodisplay 登入畫面之前顯示的資料。 Hello 應用程式啟動時，它將無法不連線 tooyour 應用程式服務，並不會顯示任何資料。 Hello 第一次後該 hello 使用者執行 hello 重新整理鍵筆勢，會顯示 hello 登入畫面。成功的登入之後 hello todo 項目的清單隨即出現。

1. 在 hello 用戶端專案中，開啟 [hello 檔案**QSTodoService.cs**並加入 hello 下列 using 陳述式和`MobileServiceUser`與存取子 toohello QSTodoService 類別：
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. 將名為的新方法加入**驗證**太**QSTodoService**以 hello 下列定義：

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

    >[AZURE.NOTE] 如果您使用 Facebook 以外的身分識別提供者，變更 hello 值太傳遞**LoginAsync** tooone hello 以下的上方： _MicrosoftAccount_， _Twitter_，_Google_，或_WindowsAzureActiveDirectory_。

3. 開啟 **QSTodoListViewController.cs**。 修改 hello 方法定義**ViewDidLoad**太移除 hello 呼叫**RefreshAsync()**接近 hello 結束：
   
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
4. 修改 hello 方法**RefreshAsync** tooauthenticate 如果 hello**使用者**屬性為 null。 加入下列程式碼頂端 hello hello 方法定義的 hello:
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. 開啟**d**，新增下列方法 hello:

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. 開啟**Info.plist**檔案中，瀏覽過**URL 類型**在 hello**進階**> 一節。 現在設定 hello**識別碼**和 hello **URL 配置**URL 類型和按一下**加入 URL 類型**。 **URL 配置**應該為您的 {url_scheme_of_your_app} hello 相同。
7. 在 Visual Studio 或 Xamarin Studio 中連接 tooyour Xamarin 組建主機在您 Mac 上，執行 hello 裝置或模擬器為目標的用戶端專案。 請確認該 hello 應用程式會顯示任何資料。
   
    Hello 清單中的項目，這會導致 hello 登入畫面 tooappear，藉以執行 hello 重新整理筆勢。 一旦您已經輸入有效的認證，hello 應用程式將會顯示 hello todo 項目的清單，而且您可以更新 toohello 資料。

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[建立 Xamarin.iOS 應用程式]: app-service-mobile-xamarin-ios-get-started.md