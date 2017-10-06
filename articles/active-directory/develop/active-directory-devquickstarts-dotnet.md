---
title: "aaaAzure AD.NET 開始使用 |Microsoft 文件"
description: "Toobuild.NET 的 Windows 桌面應用程式整合與 Azure AD 進行登入，並呼叫 Azure AD 保護應用程式開發介面使用 OAuth 的方式。"
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>將 Azure AD 整合至 Windows 桌面 WPF 應用程式
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

如果您正在開發的桌面應用程式，Azure AD，使其簡單又直接您 tooauthenticate 為您的使用者使用其 Active Directory 帳戶。  它也可讓您的應用程式 toosecurely 取用任何 web API 受到 Azure AD，例如 hello Office 365 Api 或 hello Azure API。

對於.NET 原生用戶端需要 tooaccess 受保護的資源，Azure AD 會提供 Active Directory 驗證程式庫或 ADAL hello。  ADAL 的生活中的唯一目的是 toomake 輕鬆的應用程式 tooget 存取語彙基元。  toodemonstrate 多麼容易，所以這裡我們會建置.NET WPF 待辦事項清單應用程式，用的：

* 取得存取權杖來呼叫 hello Azure AD Graph API 使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。
* 在目錄中搜尋具有指定別名的使用者。
* 將使用者登出。

toobuild hello 完整運作應用程式，您將需要：

1. 向 Azure AD 註冊您的應用程式。
2. 安裝及設定 ADAL。
3. 使用來自 Azure AD 的 ADAL tooget 語彙基元。

啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)。  您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。  如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

## <a name="1-register-hello-directorysearcher-application"></a>1.註冊 hello DirectorySearcher 應用程式
tooenable 您應用程式 tooget 語彙基元中，您必須先在您的 Azure AD 租用戶 tooregister，並授與權限 tooaccess hello Azure AD Graph API:

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶，並在 hello**目錄**清單中，選擇您希望 tooregister 您的應用程式的 hello Active Directory 租用戶。
3. 按一下**更服務**在 hello 左側瀏覽，然後選擇  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選擇 [新增]。
5. 依照 hello 提示，並建立新**原生用戶端應用程式**。
  * hello**名稱**hello 的應用程式將會描述您應用程式 tooend 使用者
  * hello**重新導向 Uri**是配置和字串的組合，Azure AD 將會使用 tooreturn 權杖回應。  輸入值的特定 tooyour 應用程式，例如`http://DirectorySearcher`。
6. 完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。  您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式頁面。
7. 從 hello**設定**頁面上，選擇**必要的使用權限**選擇**新增**。 選取 hello **Microsoft Graph**為 hello 應用程式開發介面，並加入 hello**讀取目錄資料**權限下的**委派的權限**。  這會讓使用者您應用程式 tooquery hello Graph API。

## <a name="2-install--configure-adal"></a>2.安裝和設定 ADAL
既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。  為了讓 ADAL toobe 無法 toocommunicate 與 Azure AD，您需要 tooprovide 它與您的應用程式註冊的一些資訊。

* 藉由加入使用 Package Manager Console hello ADAL toohello DirectorySearcher 專案開始。

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* 在 hello DirectorySearcher 專案中，開啟`app.config`。  取代 hello 中的項目 hello hello 值`<appSettings>`區段 tooreflect hello 值的輸入 hello Azure 入口網站。  每當使用 ADAL 時，您的程式碼便會參考這些值。
  * hello`ida:Tenant`是 hello Azure AD 租用戶，例如 contoso.onmicrosoft.com 網域
  * hello`ida:ClientId`是 hello clientId 您複製從 hello 入口網站應用程式。
  * hello`ida:RedirectUri`為 hello 重新導向註冊，讓您在 hello 入口網站的 url。

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.  使用 ADAL tooGet 語彙基元從 AAD
hello ADAL 背後的基本原則是，只要您的應用程式需要存取權杖，它只會呼叫`authContext.AcquireTokenAsync(...)`，ADAL 沒有 hello rest 和。  

* 在 hello`DirectorySearcher`專案中，開啟`MainWindow.xaml.cs`並找出 hello`MainWindow()`方法。  hello 第一個步驟是您的應用程式的 tooinitialize `AuthenticationContext` -ADAL 的主要類別。  這是您用來傳遞 ADAL hello 座標需要 toocommunicate 與 Azure AD，並告訴它如何 toocache 語彙基元。

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* 立即找出 hello `Search(...)` hello 使用者 cliks hello hello 應用程式的 UI 中的 「 搜尋 」 按鈕時將會叫用的方法。  這個方法可以讓的使用者的 UPN 開頭指定搜尋詞彙的 hello GET 要求 Azure AD Graph API toohello tooquery。  但是順序 tooquery hello Graph API，在中，您需要在 hello access_token tooinclude`Authorization`要求標頭的 hello-這是 ADAL 的運作方式。

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* 當您的應用程式藉由呼叫要求語彙基元`AcquireTokenAsync(...)`，ADAL 會嘗試 tooreturn 語彙基元不要求 hello 使用者認證。  ADAL 會判斷該 hello 使用者需要 toosign tooget 語彙基元中的，如果它會顯示登入 對話方塊中，收集 hello 使用者的認證，並傳回驗證成功後的權杖。  如果 ADAL 因故無法 tooreturn 語彙基元，則會擲回`AdalException`。
* 請注意該 hello`AuthenticationResult`物件包含`UserInfo`可以是您的應用程式可能需要使用的 toocollect 資訊的物件。  在 hello DirectorySearcher，`UserInfo`是使用的 toocustomize hello 應用程式的 UI 與 hello 使用者識別碼。
* Hello 使用者按一下 hello 「 登出 」 按鈕時，我們想要太 hello 下一個呼叫的 tooensure`AcquireTokenAsync(...)`會要求中的 hello 使用者 toosign。  使用 ADAL，這非常簡單，只要清除 hello 權杖快取項目：

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* 不過，如果 hello 使用者不按一下 hello 「 登出 」 按鈕時，您會想 toomaintain hello 使用者工作階段的 hello 下次執行 hello DirectorySearcher。  Hello 應用程式啟動時，您可以檢查 ADAL 的權杖快取中的現有的語彙基元，並據此更新 hello UI。  在 hello`CheckForCachedToken()`方法，讓瀏覽另一個呼叫`AcquireTokenAsync(...)`，傳入 hello 這次`PromptBehavior.Never`參數。  `PromptBehavior.Never`hello 使用者應該不會提示您進行登入，，和 ADAL 應該改為擲回例外狀況是否無法 tooreturn 語彙基元，則會告訴 ADAL。

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

恭喜！ 您現在擁有可運作的.NET WPF 應用程式具有 hello 能力 tooauthenticate 使用者、 安全地呼叫 Web Api 使用 OAuth 2.0，並取得 hello 使用者的基本資訊。  如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。  執行 DirectorySearcher 應用程式，並使用其中一個使用者登入。  根據 UPN 搜尋其他使用者。  關閉 hello 應用程式，並重新執行。  請注意如何 hello 使用者工作階段會保持不變。  登出，再以另一個使用者身分重新登入。

ADAL 可讓您輕鬆 tooincorporate 所有這些常見的身分識別功能到您的應用程式。  它會為您的快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，重新整理過期的權杖與多個負責 hello 中途的所有工作。  您只需 tooknow 是單一的應用程式開發介面呼叫， `authContext.AcquireTokenAsync(...)`。

已完成的 hello 範例 （不含您的組態值） 所提供，供您參考[這裡](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip)。  您現在可以移動 tooadditional 案例。  您可能想 tootry:

[使用 Azure AD 保護 .NET Web API >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

