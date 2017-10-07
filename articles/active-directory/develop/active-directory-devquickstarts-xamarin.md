---
title: "aaaAzure AD Xamarin 使用者入門 |Microsoft 文件"
description: "建置 Xamarin 應用程式來與 Azure AD 整合進行登入，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>將 Azure AD 整合至 Xamarin 應用程式
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Xamarin 可讓您使用 C# 撰寫可在 iOS、Android 和 Windows (行動裝置和電腦) 上執行的行動應用程式。 如果您要建置 xamarin 應用程式，Azure Active Directory (Azure AD)，使其具有其 Azure AD 帳戶的簡單 tooauthenticate 使用者。 hello 應用程式安全地也可以使用任何受 Azure AD，例如 Office 365 Api hello 或 hello Azure 應用程式開發介面的 web 應用程式開發介面。

針對需要 tooaccess 受保護資源的 Xamarin 應用程式，Azure AD 提供 hello Active Directory 驗證程式庫 (ADAL)。 hello 的 ADAL 的唯一目的是 toomake 輕鬆的應用程式 tooget 存取權杖。 是，本文將說明如何輕鬆 toodemonstrate 如何 toobuild DirectorySearcher 應用程式的：

* 可在 iOS、Android、Windows 桌面、Windows Phone 和 Windows 市集上執行。
* 使用單一的可攜式類別庫 (PCL) tooauthenticate 使用者，並取得 hello Azure AD Graph API 的語彙基元。
* 搜尋目錄以尋找具有指定 UPN 的使用者。

## <a name="before-you-get-started"></a>開始之前
* 下載 hello[基本架構專案](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip)，或下載 hello[完成的範例](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip)。 每一個下載都是 Visual Studio 2013 解決方案。
* 您也需要哪些 toocreate 使用者和註冊 hello 應用程式中的 Azure AD 租用戶。 如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

當您準備好時，後續 hello 程序在 hello 接下來四個區段。

## <a name="step-1-set-up-your-xamarin-development-environment"></a>步驟 1：設定您的 Xamarin 開發環境
因為本教學課程包含 iOS、Android 和 Windows 專案，所以您需要 Visual Studio 和 Xamarin。 toocreate hello 所需的環境，完成 hello 程序中[設定及安裝 Visual Studio 和 Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) MSDN 上。 hello 指示包含正在等待 hello 安裝 toobe 完成時，您可以檢閱 toolearn 深入了解 Xamarin 的資料。

Hello 安裝程式完成之後，請在 Visual Studio 中開啟 hello 方案。 您會在其中看到六個專案：五個平台特定專案和一個 PCL，DirectorySearcher.cs，可跨所有平台共用。

## <a name="step-2-register-hello-directorysearcher-app"></a>步驟 2： 註冊 hello DirectorySearcher 應用程式
tooenable hello 應用程式 tooget 語彙基元，您必須先 tooregister 在您的 Azure AD 租用戶，並授與權限 tooaccess hello Azure AD Graph API。 方式如下：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶。 然後，在 hello**目錄**清單中，選取 hello Active Directory 租用戶想 tooregister hello 應用程式。
3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 新的 toocreate**原生用戶端應用程式**，依照 hello 提示。
  * **名稱**描述 hello 應用程式 toousers。
  * **重新導向 URI**是配置和字串的組合，Azure AD 使用 tooreturn 權杖回應。 輸入值，(例如， http://DirectorySearcher )。
6. 完成註冊之後，Azure AD 會指派給 hello 應用程式是唯一的應用程式識別碼。 從 hello 複製 hello 值**應用程式**索引標籤上，因為您將需要更新版本。
7. 在 hello**設定**頁面上，選取**必要的使用權限**，然後選取**新增**。
8. 選取**Microsoft Graph**為 hello 應用程式開發介面。 在下**委派的權限**，新增 hello**讀取目錄資料**權限。  
這個動作可讓 hello 應用程式 tooquery hello Graph API 的使用者。

## <a name="step-3-install-and-configure-adal"></a>步驟 3：安裝及設定 ADAL
既然您在 Azure AD 中已有應用程式，您現在便可安裝 ADAL，並撰寫身分識別相關程式碼。 tooenable ADAL toocommunicate 與 Azure AD，不妨 hello 應用程式註冊的一些資訊。

1. 使用 Package Manager Console hello 新增 ADAL toohello DirectorySearcher 專案。

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    請注意這兩個程式庫參考會加入 tooeach 專案： hello PCL 部分 ADAL 與平台專屬部分。
2. 在 hello DirectorySearcherLib 專案中，開啟 DirectorySearcher.cs。
3. Hello 類別成員值取代為您輸入 hello Azure 入口網站中的 hello 值。 您的程式碼是指 toothese 值，每當它會使用 ADAL。

  * hello*租用戶*hello 網域，您的 Azure AD 租用戶 (例如 contoso.onmicrosoft.com)。
  * hello *clientId* hello hello 應用程式，您所複製 hello 入口網站的用戶端識別碼。
  * hello *returnUri*是 hello 重新導向在 hello 入口網站 (例如，http://DirectorySearcher) 中所輸入的 URI。

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>從 Azure AD 的步驟 4： 使用 ADAL tooget 語彙基元
幾乎所有的 hello 應用程式的驗證邏輯在於`DirectorySearcher.SearchByAlias(...)`。 所有 hello 平台專屬專案中，必須是 toopass 內容參數 toohello `DirectorySearcher` PCL。

1. 開啟 DirectorySearcher.cs，，然後加入新的參數 toohello`SearchByAlias(...)`方法。 `IPlatformParameters`是 hello 封裝 hello 平台專屬的內容參數物件 ADAL 的需求 tooperform hello 驗證。

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. 初始化`AuthenticationContext`，這是 hello 的 ADAL 的主要類別。  
此動作將 ADAL hello 協調其需求 toocommunicate 與 Azure AD。
3. 呼叫`AcquireTokenAsync(...)`，它會接受 hello`IPlatformParameters`物件，並叫用 hello 是必要的 tooreturn 語彙基元 toohello 應用程式的驗證流程。

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    `AcquireTokenAsync(...)`第一次嘗試 tooreturn hello 的語彙基元要求而不提示使用者 tooenter 其認證 （透過快取，或重新整理舊的權杖） 的資源 (在本例中的 hello Graph API)。 在必要時，它會顯示使用者 hello Azure AD 登入頁面之前取得 hello 要求的語彙基元。
4. 附加 hello 存取語彙基元 toohello Graph API 要求中 hello**授權**標頭：

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

這就是 hello `DirectorySearcher` PCL 和 hello 應用程式的身分識別相關的程式碼。 剩下的就是 toocall hello`SearchByAlias(...)`每個平台檢視中的方法和 tooadd 正確處理程式碼在需要時，hello UI 生命週期。

### <a name="android"></a>Android
1. Weatherapp，在加入呼叫太`SearchByAlias(...)`hello 按鈕中按一下 處理常式：

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. 覆寫 hello`OnActivityResult`存留週期方法 tooforward 任何驗證重新導向後 toohello 適當的方法。 ADAL 針對 Android 中的此項作業提供協助程式方法：

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>Windows 桌面
將 MainWindow.xaml.cs 中, 進行呼叫太`SearchByAlias(...)`藉由傳遞`WindowInteropHelper`hello desktop`PlatformParameters`物件：

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
在 DirSearchClient_iOSViewController.cs，hello iOS`PlatformParameters`物件會使用參考 toohello 檢視控制器：

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Windows Universal
在 Windows 通用，開啟 MainPage.xaml.cs，然後實作 hello`Search`方法。 這個方法會視需要共用的專案 tooupdate UI 中使用的 helper 方法。

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>後續步驟
您現在擁有一個能夠在五個不同平台之間驗證使用者並使用 OAuth 2.0 安全地呼叫 Web API 的運作中 Xamarin 應用程式。

如果您沒有已填入您的租用戶與使用者，現在是 hello 時間 toodo 因此。

1. 執行 DirectorySearcher 應用程式，然後使用其中一個 hello 使用者登入。
2. 根據 UPN 搜尋其他使用者。

ADAL 可讓一般身分識別功能輕鬆 tooincorporate 到 hello 應用程式。 它會負責所有 hello dirty 工作，例如快取管理、 OAuth 通訊協定支援，呈現 hello 使用者與登入 UI，並重新整理過期語彙基元。 您需要 tooknow 單一 API 呼叫`authContext.AcquireToken*(…)`。

如需參考，下載 hello[完成的範例](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip)（不含您的組態值）。

您現在可以移動 tooadditional 身分識別案例。 例如，嘗試[使用 Azure AD 來保護 .NET Web API](active-directory-devquickstarts-webapi-dotnet.md)。

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
