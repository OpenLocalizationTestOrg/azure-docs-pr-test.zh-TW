---
title: "aaaAzure AD Windows 市集開始使用 |Microsoft 文件"
description: "建置與 Azure AD 整合來進行登入的 Windows 市集應用程式，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>將 Azure AD 與 Windows 市集應用程式整合
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Visual Studio 2017 不支援 Windows Store 8.1 和舊版專案。  如需詳細資訊，請參閱 [Visual Studio 2017 平台目標及相容性](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)。

如果您正在開發 hello Windows 市集應用程式，Azure Active Directory (Azure AD)，使其簡單又直接 tooauthenticate 您的使用者使用其 Active Directory 帳戶。 藉由整合與 Azure AD，應用程式可以安全地使用任何 web 應用程式開發介面中受到 Azure AD，例如 Office 365 Api hello 或 hello Azure API。

針對 Windows 市集桌面應用程式需要 tooaccess 受保護的資源，Azure AD 提供 hello Active Directory 驗證程式庫 (ADAL)。 hello 的 ADAL 的唯一目的是 toomake 輕鬆 hello 應用程式 tooget 存取權杖。 toodemonstrate 多麼容易的是，本文將說明如何 toobuild DirectorySearcher Windows 市集應用程式的：

* 取得存取權杖來呼叫 hello Azure AD Graph API 使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。
* 搜尋目錄以尋找具有指定使用者主體名稱 (UPN) 的使用者。
* 將使用者登出。

## <a name="before-you-get-started"></a>開始之前
* 下載 hello[基本架構專案](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip)，或下載 hello[完成的範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)。 每一個下載項目都是 Visual Studio 2015 解決方案。
* 您也需要哪些 toocreate 使用者和註冊 hello 應用程式中的 Azure AD 租用戶。 如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

當您準備好時，後續 hello 程序在 hello 接下來三個區段。

## <a name="step-1-register-hello-directorysearcher-app"></a>步驟 1： 註冊 hello DirectorySearcher 應用程式
tooenable hello 應用程式 tooget 語彙基元，您必須先 tooregister 在您的 Azure AD 租用戶，並授與權限 tooaccess hello Azure AD Graph API。 方式如下：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶。 然後，在 hello**目錄**清單中，選取 hello Active Directory 租用戶想 tooregister hello 應用程式。
3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 請遵循 hello 提示 toocreate**原生用戶端應用程式**。
  * **名稱**描述 hello 應用程式 toousers。
  * **重新導向 URI**是配置和字串的組合，Azure AD 使用 tooreturn 權杖回應。 暫時先輸入一個預留位置值 (例如 **http://DirectorySearcher**)。 您稍後將取代 hello 值。
6. Hello 註冊完成之後，Azure AD 會指派給 hello 應用程式是唯一的應用程式識別碼。 複製在 hello hello 值**應用程式**索引標籤上，因為您將需要更新版本。
7. 在 hello**設定**頁面上，選取**必要的使用權限**，然後選取**新增**。
8. Hello **Azure Active Directory**應用程式中，選取**Microsoft Graph**為 hello 應用程式開發介面。
9. 在下**委派的權限**，新增 hello **hello 登入的使用者身分存取 hello 目錄**權限。 如此可讓 hello 應用程式 tooquery hello Graph API 的使用者。

## <a name="step-2-install-and-configure-adal"></a>步驟 2：安裝及設定 ADAL
既然您在 Azure AD 中已有應用程式，您現在便可安裝 ADAL，並撰寫身分識別相關程式碼。 tooenable ADAL toocommunicate 與 Azure AD，不妨 hello 應用程式註冊的一些資訊。

1. 使用 Package Manager Console hello 新增 ADAL toohello DirectorySearcher 專案。

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. 在 hello DirectorySearcher 專案中，開啟 MainPage.xaml.cs。
3. Hello 中的 hello 值取代為**組態值**區域與您輸入 hello Azure 入口網站中的 hello 值。 您的程式碼是指 toothese 值，每當它會使用 ADAL。
  * hello*租用戶*hello 網域，您的 Azure AD 租用戶 (例如 contoso.onmicrosoft.com)。
  * hello *clientId* hello hello 應用程式，您所複製 hello 入口網站的用戶端識別碼。
4. 您現在會針對 Windows 市集應用程式需要 toodiscover hello 回呼 URI。 在 hello 中這一行設定中斷點`MainPage`方法：
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. 建置 hello 方案，並確認封裝的所有參考都會都還原。 如果遺漏任何套件，請開啟 hello NuGet 封裝管理員，並加以還原。
6. 執行 hello 應用程式，並將複製的 hello 值`redirectUri`hello 中斷點叫用時。 hello 值看起來應該類似下列 hello:

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. 在 [hello**設定**hello Azure 入口網站中的 hello 應用程式] 索引標籤加入**RedirectUri**以 hello 上述值。  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>從 Azure AD 的步驟 3： 使用 ADAL tooget 語彙基元
hello ADAL 背後的基本原則是，每當 hello 應用程式需要存取權杖，它只會呼叫`authContext.AcquireToken(…)`，ADAL 沒有 hello rest 和。  

1. 初始化 hello 應用程式`AuthenticationContext`，這是 hello 的 ADAL 的主要類別。 這個動作會傳遞 ADAL hello 座標與 Azure AD toocommunicate 地告訴它如何 toocache 語彙基元。

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. 找出 hello`Search(...)`方法，當使用者按一下 hello 叫用**搜尋**hello 應用程式的 UI 上的按鈕。 這個方法可以讓的使用者的 UPN 開頭指定搜尋詞彙的 hello get 要求 Azure AD Graph API toohello tooquery。 tooquery hello Graph API hello 要求中包含存取權杖**授權**標頭。 這就是 ADAL 的切入點。

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    當 hello 應用程式藉由呼叫要求語彙基元`AcquireTokenAsync(...)`，ADAL 會嘗試 tooreturn 語彙基元不要求 hello 使用者認證。 如果 ADAL 會判斷該 hello 使用者需要 toosign tooget 語彙基元中的，它會顯示登入對話方塊中，會收集 hello 使用者的認證，而且在驗證成功後，傳回的語彙基元。 如果 ADAL 因故無法 tooreturn 語彙基元，hello *AuthenticationResult*是錯誤的狀態。
3. 現在它是您剛擷取時間 toouse hello 存取權杖。 此外在 hello`Search(...)`方法，附加 hello Graph API 中 hello 取得要求的語彙基元 toohello**授權**標頭：

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. 您可以使用 hello`AuthenticationResult`物件 toodisplay hello 應用程式，例如 hello 使用者的識別碼中的 hello 使用者資訊：

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. 您也可以使用 ADAL toosign hello 應用程式外的使用者。 當 hello 使用者按一下 hello**登出**按鈕，請確定該 hello 下一個呼叫太`AcquireTokenAsync(...)`顯示登入的檢視。 使用 ADAL，此動作非常簡單，只要清除 hello 權杖快取的：

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>後續步驟
現在，您會有可運作的 Windows 市集應用程式可以驗證使用者，安全地呼叫 web Api 使用 OAuth 2.0，並取得 hello 使用者的基本資訊。

如果您沒有已填入您的租用戶與使用者，現在是 hello 時間 toodo 因此。
1. 執行 DirectorySearcher 應用程式，然後使用其中一個 hello 使用者登入。
2. 根據 UPN 搜尋其他使用者。
3. 關閉 hello 應用程式，並重新執行它。 請注意如何 hello 使用者工作階段會保持不變。
4. 以滑鼠右鍵按一下 toodisplay hello 下方列，登出，再以其他使用者身分登入。

ADAL 可讓您輕鬆 tooincorporate 所有 hello 應用程式到這些一般身分識別功能。 它會負責所有 hello dirty 工作，例如快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，並重新整理過期語彙基元。 您需要 tooknow 單一 API 呼叫`authContext.AcquireToken*(…)`。

如需參考，下載 hello[完成的範例](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip)（不含您的組態值）。

您現在可以移動 tooadditional 身分識別案例。 例如，嘗試[使用 Azure AD 來保護 .NET Web API](active-directory-devquickstarts-webapi-dotnet.md)。

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
