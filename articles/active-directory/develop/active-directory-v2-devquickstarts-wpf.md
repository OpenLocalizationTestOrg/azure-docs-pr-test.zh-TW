---
title: "aaaAzure Active Directory v2.0.NET 原生應用程式 |Microsoft 文件"
description: "如何 toobuild.NET 原生應用程式的使用者使用簽署兩個人的 Microsoft 帳戶和工作或學校帳戶。"
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a>新增登入 tooa Windows 桌面應用程式
與 hello hello v2.0 端點，您可以快速加入驗證 tooyour 傳統型應用程式支援這兩個個人 Microsoft 帳戶和工作或學校帳戶。  它也可讓您的應用程式 toosecurely 通訊與後端 web 應用程式開發介面，以及[hello Microsoft Graph](https://graph.microsoft.io)和幾個 hello [Office 365 統一的 Api](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2)。

> [!NOTE]
> 並非所有的 Azure Active Directory (AD) 的案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

如[在裝置執行.NET 原生應用程式](active-directory-v2-flows.md#mobile-and-native-apps)，Azure AD 提供 Microsoft 身分識別驗證程式庫或 MSAL hello。  MSAL 的生活中的唯一目的是的 toomake 輕鬆的應用程式 tooget 權杖呼叫 web 服務。  toodemonstrate 多麼容易，所以這裡我們將建置.NET WPF 待辦事項清單應用程式的：

* 符號 hello 中的使用者 （& s) 取得存取權杖使用 hello [OAuth 2.0 驗證通訊協定](active-directory-v2-protocols.md)。
* 安全地呼叫受 OAuth 2.0 保護的後端待辦事項清單 Web 服務。
* 符號 hello 使用者登出。

## <a name="download-sample-code"></a>下載範例程式碼
此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet)。  您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip)或再製 hello 基本架構：

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

在本教學課程的 hello 結尾處提供 hello 完成應用程式。

## <a name="register-an-app"></a>註冊應用程式
在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循下列[詳細步驟](active-directory-v2-app-registration.md)。  請確定：

* 複製下 hello**應用程式識別碼**指派 tooyour 應用程式，您將需要它過期。
* 新增 hello**行動**平台應用程式。

## <a name="install--configure-msal"></a>安裝和設定 MSAL
您現在有了已向 Microsoft 註冊的應用程式，可以安裝 MSAL 並撰寫與您身分識別相關的程式碼。  為了讓 MSAL toobe 無法 toocommunicate hello v2.0 端點，您需要 tooprovide 它與您的應用程式註冊的一些資訊。

* 藉由加入使用 Package Manager Console hello MSAL toohello TodoListClient 專案開始。

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* 在 hello TodoListClient 專案中，開啟`app.config`。  取代 hello 中的項目 hello hello 值`<appSettings>`區段 tooreflect hello 值的輸入 hello 應用程式註冊入口網站。  每當使用 MSAL 時，您的程式碼便會參考這些值。
  
  * hello`ida:ClientId`為 hello**應用程式識別碼**您複製從 hello 入口網站應用程式。
* 在 hello TodoList 服務專案中，開啟`web.config`hello hello 專案根目錄中。  
  
  * 取代 hello`ida:Audience`相同值與 hello**應用程式識別碼**從 hello 入口網站。

## <a name="use-msal-tooget-tokens"></a>使用 MSAL tooget 語彙基元
hello MSAL 背後的基本原則是每當您的應用程式需要存取權杖，您只需呼叫`app.AcquireToken(...)`，和 MSAL 沒有 hello rest。  

* 在 hello`TodoListClient`專案中，開啟`MainWindow.xaml.cs`並找出 hello`OnInitialized(...)`方法。  hello 第一個步驟是您的應用程式的 tooinitialize `PublicClientApplication` -MSAL 的主要的類別，代表原生應用程式。  這是您用來傳遞 MSAL hello 座標需要 toocommunicate 與 Azure AD，並告訴它如何 toocache 語彙基元。

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* Hello 應用程式啟動時，我們想 toocheck，請參閱是否 hello 使用者已登入 hello 應用程式。  不過，我們還不想 tooinvoke 登入 UI-我們要 hello 使用者，因此按一下 [登入] toodo。  此外在 hello`OnInitialized(...)`方法：

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* 如果 hello 使用者未登入，而且使用者按一下 [登入] 按鈕 hello，我們想 tooinvoke 登入 UI，並擁有 hello 使用者輸入其認證。  實作 hello 登入按鈕處理常式：

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* 如果 hello 使用者成功登入時，MSAL 會接收和快取權杖，而且您可以繼續 toocall hello`GetTodoList()`方法進行部署。  所有使用者的工作時已離開 tooget 為 tooimplement hello`GetTodoList()`方法。

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a>執行
恭喜！ 您現在擁有可運作的.NET WPF 應用程式具有 hello 能力 tooauthenticate 使用者 （& s) 安全地呼叫使用 OAuth 2.0 的 Web Api。  執行您的兩個專案，並以個人的 Microsoft 或工作/學校的帳戶登入。  加入工作 toothat 使用者的待辦事項清單。  先登出，再重新登入為另一個使用者 tooview 其待辦事項清單。  關閉 hello 應用程式，並重新執行。  請注意如何 hello 使用者工作階段會保持不變-這是因為 hello app 會快取在本機檔案的語彙基元。

MSAL 可輕鬆 tooincorporate 常見的身分識別功能到應用程式使用個人和工作帳戶。  它會為您的快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，重新整理過期的權杖與多個負責 hello 中途的所有工作。  您只需 tooknow 是單一的應用程式開發介面呼叫， `app.AcquireTokenAsync(...)`。

如需參考，hello 完成 （不含您的組態值） 的範例[依現狀的.zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip)，或您可以將其複製從 GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>後續步驟
您現在可以進入更進階的主題。  您可能想 tootry:

* [保護與 hello v2.0 端點 hello TodoListService Web API](active-directory-v2-devquickstarts-dotnet-api.md)

如需其他資源，請參閱：  

* [hello v2.0 開發人員指南 >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "msal" 標籤 >>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>取得產品的安全性更新
我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。

