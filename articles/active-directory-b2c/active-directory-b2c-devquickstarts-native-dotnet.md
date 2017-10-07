---
title: "Active Directory B2C aaaAzure |Microsoft 文件"
description: "如何 toobuild Windows 桌面應用程式，包含登入、 註冊，以及使用 Azure Active Directory B2C 分析管理。"
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Azure AD B2C：建置 Windows 桌面應用程式
藉由使用 Azure Active Directory (Azure AD) B2C，您可以在幾個簡短步驟中加入功能強大的自助式身分識別管理功能 tooyour 傳統型應用程式。 這篇文章將示範如何 toocreate.NET Windows Presentation Foundation (WPF) 「 待辦事項清單 」 應用程式，其中包含註冊、 登入的使用者和管理設定檔。 hello 應用程式會使用使用者名稱或電子郵件包含支援註冊和登入。 它也會支援以社交帳戶 (例如 Facebook 和 Google) 來註冊及登入。

## <a name="get-an-azure-ad-b2c-directory"></a>取得 Azure AD B2C 目錄
您必須先建立目錄或租用戶，才可使用 Azure AD B2C。  目錄是適用於所有使用者、app、群組等項目的容器。 如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) ，再繼續進行本指南。

## <a name="create-an-application"></a>建立應用程式
接下來，您需要 toocreate 應用程式中 B2C 目錄。 提供 Azure AD，它需要 toosecurely 通訊與您的應用程式的資訊。 toocreate 的應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。  請務必：

* 包含**原生用戶端**hello 應用程式中。
* 複製 hello**重新導向 URI** `urn:ietf:wg:oauth:2.0:oob`。 它是 hello 預設 URL，此程式碼範例。
* 複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。 稍後您將會用到此資訊。

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>建立您的原則
在 Azure AD B2C 中，每個使用者經驗皆由 [原則](active-directory-b2c-reference-policies.md)所定義。 此程式碼範例包含三種身分識別體驗：註冊、登入和編輯設定檔。 中所述，每個類型，需要 toocreate 原則[原則參考文件](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)。 當您建立 hello 三個原則時，請務必：

* 選擇 [**使用者識別碼註冊**或**電子郵件註冊**hello 身分識別提供者] 刀鋒視窗中。
* 在註冊原則中，選擇 [顯示名稱]  和其他註冊屬性。
* 針對每個原則選擇 [顯示名稱] 和 [物件識別碼] 宣告做為應用程式宣告。 您也可以選擇其他宣告。
* 複製 hello**名稱**的每個原則建立之後。 就不應有 hello 前置詞`b2c_1_`。  稍後您將需要這些原則名稱。

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

您已成功建立 hello 三個原則之後，您便準備好 toobuild 您的應用程式。

## <a name="download-hello-code"></a>下載 hello 程式碼
hello 本教學課程中的程式碼[維護 GitHub 上](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet)。 移 toobuild hello 範例時，您可以[下載為.zip 檔案的基本架構專案](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip)。 您也可以複製 hello 基本架構：

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

hello 完成應用程式也是[可以做為.zip 檔案](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)或 hello `complete` hello 分支相同的儲存機制。

下載 hello 範例程式碼之後，開啟 hello Visual Studio.sln 檔案 tooget 啟動。 hello`TaskClient`專案是 hello hello 使用者 WPF 桌面應用程式互動。 基於 hello 本教學課程中，它會呼叫後端工作 web API，裝載在 Azure 中，儲存每個使用者的待辦事項清單。  您不需要 toobuild hello web API，我們已經為您執行它。

toolearn 如何安全地使用 Azure AD B2C，來驗證要求的 web API 簽出[web API 使用者入門文件](active-directory-b2c-devquickstarts-api-dotnet.md)。

## <a name="execute-policies"></a>執行原則
您的應用程式可藉由傳送驗證訊息指定他們想 tooexecute hello HTTP 要求的一部分的 hello 原則會與 Azure AD B2C 通訊。 對於.NET 桌面應用程式，您可以使用 hello 預覽 Microsoft 驗證程式庫 (MSAL) toosend OAuth 2.0 驗證訊息、 執行原則，以及該呼叫 web Api 取得的權杖。

### <a name="install-msal"></a>安裝 MSAL
新增 MSAL toohello `TaskClient` hello Visual Studio Package Manager Console 的專案。

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>輸入 B2C 詳細資料
開啟 hello 檔案`Globals.cs`並取代每個 hello 屬性值。 這個類別用在整個`TaskClient`tooreference 常用的值。

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a>建立 hello PublicClientApplication
hello MSAL 主要類別是`PublicClientApplication`。 此類別代表 hello Azure AD B2C 系統中的應用程式。 當 hello 應用程式初始化建立的執行個體`PublicClientApplication`中`MainWindow.xaml.cs`。 這可用於整個 hello 視窗。

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a>起始註冊流程
當使用者選擇 toosigns 組成時，您會想 tooinitiate 會使用您所建立的 hello 註冊原則的註冊流程。 藉由使用 MSAL，您只要呼叫 `pca.AcquireTokenAsync(...)`即可。 hello 您太傳遞的參數`AcquireTokenAsync(...)`判斷哪一個語彙基元收到，用於 hello 驗證要求，以及其他 hello 原則。

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a>起始登入流程
您可以起始 hello 的登入流程起始註冊流程的方式相同。 當使用者登入時，會進行相同的 hello 呼叫 tooMSAL，這次請使用您登入的原則：

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a>起始編輯設定檔流程
同樣地，您可以在 hello 中執行的編輯設定檔原則相同的方式：

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

在所有這些案例中，MSAL 會傳回 `AuthenticationResult` 中的權杖，或是擲回例外狀況。 每當您從 MSAL，取得權杖，您可以使用 hello `AuthenticationResult.User` hello 應用程式，例如 hello UI 中的 tooupdate hello 使用者資料的物件。 ADAL 也快取 hello hello 應用程式的其他部分中使用的語彙基元。

### <a name="check-for-tokens-on-app-start"></a>在應用程式啟動時檢查權杖
您也可以使用 MSAL tookeep 追蹤 hello 使用者的登入狀態。  在此應用程式，我們會想 hello 使用者 tooremain 登入，即使他們關閉 hello 應用程式，並重新開啟它。  傳回內 hello`OnInitialized`覆寫時，使用 MSAL 的`AcquireTokenSilent`方法 toocheck 快取權杖：

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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
```

## <a name="call-hello-task-api"></a>呼叫 hello 工作應用程式開發介面
您現在已經使用 MSAL tooexecute 原則，並取得語彙基元。  當您想 toouse 其中一個這些語彙基元 toocall hello 工作應用程式開發介面時，您可以再次使用 MSAL 的`AcquireTokenSilent`方法 toocheck 快取權杖：

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

當太 hello 呼叫`AcquireTokenSilentAsync(...)`成功語彙基元並在找到 hello 快取中，您可以加入 hello 語彙基元 toohello `Authorization` hello HTTP 要求標頭。 hello 工作 web API 將會使用此標頭 tooauthenticate hello 要求 tooread hello 使用者的待辦事項清單：

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>符號 hello 使用者登出
最後，您可以使用 MSAL 與 hello 應用程式時 hello 使用者選取的使用者工作階段的 tooend**登出**。當使用 MSAL，這可以藉由清除所有來自 hello 權杖快取的 hello 權杖：

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a>執行 hello 範例應用程式
最後，建置並執行 hello 範例。  註冊 hello 應用程式使用電子郵件地址或使用者名稱。 先登出再重新登入為 hello 相同使用者。 編輯該使用者的設定檔。 請登出，然後以不同的使用者身分登入。

## <a name="add-social-idps"></a>新增社交 IDP
目前，hello 應用程式僅支援使用者註冊和登入使用**本機帳戶**。 這些是儲存在 B2C 目錄中使用使用者名稱和密碼的帳戶。 藉由使用 Azure AD B2C，您可以新增對其他身分識別提供者 (IDP) 的支援，但不需變更任何程式碼。

tooadd 社交 IDPs tooyour 應用程式中，遵循開始 hello 詳細這些文章中的指示。 針對每個 IDP 想 toosupport，您必須在該系統 tooregister 應用程式，並取得用戶端識別碼。

* [將 Facebook 設定為 IDP](active-directory-b2c-setup-fb-app.md)
* [將 Google 設定為 IDP](active-directory-b2c-setup-goog-app.md)
* [將 Amazon 設定為 IDP](active-directory-b2c-setup-amzn-app.md)
* [將 LinkedIn 設定為 IDP](active-directory-b2c-setup-li-app.md)

新增 hello 身分識別提供者 tooyour B2C 目錄之後，您需要的每個 tooinclude hello 新 IDPs，做為您三個原則述 hello tooedit[原則參考文件](active-directory-b2c-reference-policies.md)。 儲存您的原則之後，請再次執行 hello 應用程式。 您應該會看到新 IDPs 加入為登入並註冊選項，在每個身分識別體驗中的 hello。

您可以試驗您的原則，並觀察 hello 範例應用程式上的效果。 新增或移除 IDP、管理應用程式宣告，或變更註冊屬性。 試驗到您能夠了解原則、驗證要求和 MSAL 如何結合在一起為止。

如需參考，hello 完成範例[提供成.zip 檔案](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip)。 您也可以從 Github 複製它：

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
