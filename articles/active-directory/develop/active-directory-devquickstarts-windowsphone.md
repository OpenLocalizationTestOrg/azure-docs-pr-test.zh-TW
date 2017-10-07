---
title: "aaaAzure AD Windows Phone 開始使用 |Microsoft 文件"
description: "Toobuild Windows Phone 應用程式整合與 Azure AD 進行登入，並呼叫 Azure AD 保護應用程式開發介面使用 OAuth 的方式。"
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>整合 Azure AD 與 Windows Phone 應用程式
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Visual Studio 2017 不支援 Windows Phone 8.1 和舊版專案。  如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。

如果您正在開發 Windows Phone 8.1 應用程式，Azure AD，使其簡單又直接您 tooauthenticate 為您的使用者使用其 Active Directory 帳戶。  它也可讓您的應用程式 toosecurely 取用任何 web API 受到 Azure AD，例如 hello Office 365 Api 或 hello Azure API。

> [!NOTE]
> 此程式碼範例會使用 ADAL 2.0 版。  Hello 最新技術，您可能會想 tooinstead 再試一次我們[Windows 通用教學課程中使用 ADAL v3.0](active-directory-devquickstarts-windowsstore.md)。  如果您確實要建置適用於 Windows Phone 8.1 的應用程式，這是 hello 正確的位置。  ADAL v2.0 仍完整支援，且 hello 開發應用程式 agianst Windows Phone 8.1 建議的方法來使用 Azure AD。
> 
> 

對於.NET 原生用戶端需要 tooaccess 受保護的資源，Azure AD 會提供 Active Directory 驗證程式庫或 ADAL hello。  ADAL 的生活中的唯一目的是 toomake 輕鬆的應用程式 tooget 存取語彙基元。  toodemonstrate 多麼容易，所以這裡，我們將建立 「 目錄搜尋程式 「 Windows Phone 8.1 應用程式的：

* 取得存取權杖來呼叫 hello Azure AD Graph API 使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。
* 搜尋目錄以尋找具有指定 UPN 的使用者。
* 將使用者登出。

toobuild hello 完整運作應用程式，您將需要：

1. 向 Azure AD 註冊您的應用程式。
2. 安裝及設定 ADAL。
3. 使用來自 Azure AD 的 ADAL tooget 語彙基元。

啟動，tooget[下載基本架構的專案](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)。  每一個都是 Visual Studio 2013 解決方案。  您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。  如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

## <a name="1-register-hello-directory-searcher-application"></a>1.註冊 hello 目錄搜尋程式應用程式
tooenable 您應用程式 tooget 語彙基元中，您必須先在您的 Azure AD 租用戶 tooregister，並授與權限 tooaccess hello Azure AD Graph API:

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶，並在 hello**目錄**清單中，選擇您希望 tooregister 您的應用程式的 hello Active Directory 租用戶。
3. 按一下**更服務**在 hello 左側瀏覽，然後選擇  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選擇 [新增]。
5. 依照 hello 提示，並建立新**原生用戶端應用程式**。
  * hello**名稱**hello 的應用程式將會描述您應用程式 tooend 使用者
  * hello**重新導向 Uri**是配置和字串的組合，Azure AD 將會使用 tooreturn 權杖回應。  現在請先輸入預留位置值，例如 `http://DirectorySearcher`。  我們稍後將會取代此值。
6. 完成註冊後，AAD 會為您的應用程式指派唯一的應用程式識別碼。  您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式 索引標籤。
7. 從 hello**設定**頁面上，選擇**必要的使用權限**選擇**新增**。 選取 hello **Microsoft Graph**為 hello 應用程式開發介面，並加入 hello**讀取目錄資料**權限下的**委派的權限**。  這會讓使用者您應用程式 tooquery hello Graph API。

## <a name="2-install--configure-adal"></a>2.安裝和設定 ADAL
既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。  為了讓 ADAL toobe 無法 toocommunicate 與 Azure AD，您需要 tooprovide 它與您的應用程式註冊的一些資訊。

* 藉由加入使用 Package Manager Console hello ADAL toohello DirectorySearcher 專案開始。

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* 在 hello DirectorySearcher 專案中，開啟`MainPage.xaml.cs`。  Hello 中的 hello 值取代為`Config Values`區域 tooreflect hello 值的輸入 hello Azure 入口網站。  每當使用 ADAL 時，您的程式碼便會參考這些值。
  * hello`tenant`是 hello Azure AD 租用戶，例如 contoso.onmicrosoft.com 網域
  * hello`clientId`是 hello clientId 您複製從 hello 入口網站應用程式。
* 您現在會需要您的 Windows Phone 應用程式的 toodiscover hello 回呼 uri。  在 hello 中這一行設定中斷點`MainPage`方法：

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* 執行 hello 應用程式，並複製擱置在一旁的 hello 值`redirectUri`hello 中斷點叫用時。  您應該會看到類似下面的畫面

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* 在 [hello**設定**hello Azure 管理入口網站中，於應用程式] 索引標籤，以取代 hello hello 值**RedirectUri**具有這個值。  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3.使用 ADAL tooGet 語彙基元從 AAD
hello ADAL 背後的基本原則是，只要您的應用程式需要存取權杖，它只會呼叫`authContext.AcquireToken(…)`，ADAL 沒有 hello rest 和。  

* hello 第一個步驟是您的應用程式的 tooinitialize `AuthenticationContext` -ADAL 的主要類別。  這是您用來傳遞 ADAL hello 座標需要 toocommunicate 與 Azure AD，並告訴它如何 toocache 語彙基元。

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* 立即找出 hello `Search(...)` hello 使用者 cliks hello hello 應用程式的 UI 中的 「 搜尋 」 按鈕時將會叫用的方法。  這個方法可以讓的使用者的 UPN 開頭指定搜尋詞彙的 hello GET 要求 Azure AD Graph API toohello tooquery。  但是順序 tooquery hello Graph API，在中，您需要在 hello access_token tooinclude`Authorization`要求標頭的 hello-這是 ADAL 的運作方式。

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* 如果需要互動式驗證，ADAL 會使用 Windows Phone Web 驗證代理人 」 (WAB) 和[接續模型](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/)toodisplay hello Azure AD 登入頁面。  當 hello 使用者登入時，您的應用程式需要 toopass ADAL hello 結果的 hello WAB 互動。  這很簡單，只實作 hello`ContinueWebAuthentication`介面：

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* 現在時間 toouse hello`AuthenticationResult`傳回 tooyour 應用程式的 ADAL。  在 hello`QueryGraph(...)`回呼，附加 hello access_token 貴用戶取得 toohello hello 授權標頭中的 GET 要求：

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* 您也可以使用 hello`AuthenticationResult`物件 toodisplay hello 使用者應用程式中的資訊。 在 [hello`QueryGraph(...)`方法中，使用 hello 結果 tooshow hello 使用者的識別碼在 hello] 頁面上：

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* 最後，您可以使用 ADAL toosign hello 使用者登出的應用程式。  Hello 使用者按一下 hello 「 登出 」 按鈕時，我們想要太 hello 下一個呼叫的 tooensure`AcquireTokenSilentAsync(...)`將會失敗。  使用 ADAL，這非常簡單，只要清除 hello 權杖快取項目：

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

恭喜！ 您現在擁有可運作的 Windows Phone 應用程式具有 hello 能力 tooauthenticate 使用者、 安全地呼叫 Web Api 使用 OAuth 2.0，並取得 hello 使用者的基本資訊。  如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。  執行 DirectorySearcher 應用程式，並使用其中一個使用者登入。  根據 UPN 搜尋其他使用者。  關閉 hello 應用程式，並重新執行。  請注意如何 hello 使用者工作階段會保持不變。  登出，再以另一個使用者身分重新登入。

ADAL 可讓您輕鬆 tooincorporate 所有這些常見的身分識別功能到您的應用程式。  它會為您的快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，重新整理過期的權杖與多個負責 hello 中途的所有工作。  您只需 tooknow 是單一的應用程式開發介面呼叫， `authContext.AcquireToken*(…)`。

已完成的 hello 範例 （不含您的組態值） 所提供，供您參考[這裡](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip)。  您現在可以移動 tooadditional 身分識別案例。  您可能想 tootry:

[使用 Azure AD 保護 .NET Web API >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

