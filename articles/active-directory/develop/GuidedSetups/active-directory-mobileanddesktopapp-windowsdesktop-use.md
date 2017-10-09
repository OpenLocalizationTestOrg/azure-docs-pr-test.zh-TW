---
title: "aaaAzure AD v2 Windows 桌面快速入門-使用 |Microsoft 文件"
description: "Windows Desktop .NET (XAML) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>用於 hello Microsoft Graph API 中的 hello Microsoft 驗證程式庫 (MSAL) tooget 語彙基元

本節說明如何 toouse MSAL tooget 語彙基元 hello Microsoft Graph API。

1.  在`MainWindow.xaml.cs`，加入 hello MSAL 程式庫 toohello 類別的參考：

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
將 <code>MainWindow</code> 類別程式碼取代為：
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>詳細資訊
#### <a name="getting-a-user-token-interactive"></a>以互動方式取得使用者權杖
呼叫 hello`AcquireTokenAsync`方法的結果 視窗，提示 hello 使用者 toosign 中的。 應用程式通常需要以互動方式 hello 中的使用者 toosign 第一次需要 tooaccess 受保護的資源，或無訊息作業 tooacquire 權杖就會失敗 （例如 hello 使用者密碼到期時）。

#### <a name="getting-a-user-token-silently"></a>以無訊息方式取得使用者權杖
`AcquireTokenSilentAsync` 會處理權杖取得和更新作業，不需要與使用者進行任何互動。 之後`AcquireTokenAsync`會針對要執行 hello 第一次， `AcquireTokenSilentAsync` hello 所使用的一般方法 tooobtain 權杖 tooaccess 呼叫 toorequest 的受保護的後續呼叫的資源，或更新權杖會以無訊息模式。
最後，`AcquireTokenSilentAsync`將會失敗 – 例如 hello 使用者已登出，或已變更其密碼，另一個裝置上的。 當 MSAL 偵測到 hello 問題可透過要求互動的動作來解決時，它就會引發`MsalUiRequiredException`。 您的應用程式可以透過兩種方式處理此例外狀況：

1.  進行呼叫，以針對`AcquireTokenAsync`立即，這會導致提示 toosign 中的 hello 使用者。 此模式通常用於線上應用程式在沒有離線內容 hello 應用程式中可供 hello 使用者。 hello 此引導式的安裝程式所產生的範例會使用此模式： 您可以看到它動作 hello 中第一次執行 hello 範例： 沒有任何使用者都用過 hello 應用程式，因為`PublicClientApp.Users.FirstOrDefault()`會包含 null 值，和`MsalUiRequiredException`擲回例外狀況。 hello hello 範例中的程式碼，則控制代碼藉由呼叫 hello 例外狀況`AcquireTokenAsync`導致提示 toosign 中的 hello 使用者。

2.  應用程式也可以進行互動式登入是必要項目，所以 hello 使用者可以選取 hello 正確的時間 toosign 中，或者 hello 應用程式可以重試的視覺指示 toohello 使用者`AcquireTokenSilentAsync`稍後。 這通常用於 hello 使用者可以使用 hello 應用程式的其他功能，而不被中斷-例如，沒有離線內容 hello 應用程式中提供。 在此情況下，hello 使用者可以決定當他們想 toosign tooaccess hello 受保護的資源，或 toorefresh hello 過期的資訊，或您的應用程式可以決定 tooretry`AcquireTokenSilentAsync`網路還原之後變成暫時無法使用時。
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>呼叫 hello Microsoft Graph API，使用您剛取得 hello 語彙基元

1. 將以下 tooyour hello 新方法加入`MainWindow.xaml.cs`。 hello 方法是使用的 toomake`GET`對 Graph API 的使用授權標頭的要求：

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>針對受保護 API 進行 REST 呼叫的詳細資訊

在此範例應用程式，hello`GetHttpContentWithToken`方法是使用的 toomake HTTP`GET`針對受保護的資源需要權杖，然後再回到 hello 內容 toohello 呼叫端要求。 這個方法會加入 hello 取得語彙基元中 hello *HTTP 授權標頭*。 此範例中，hello 資源為 hello Microsoft Graph API*我*端點 – 顯示 hello 使用者設定檔資訊。
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>加入方法 toosign 出 hello 使用者

1. 新增下列方法 tooyour hello `MainWindow.xaml.cs` toosign 出 hello 使用者：

```csharp
/// <summary>
/// Sign out hello current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>關於登出的詳細資訊

`SignOutButton_Click`移除 hello MSAL 使用者快取中的使用者，讓未來的要求 tooacquire 語彙基元才會成功則由 toobe 互動式，這會有效地指示 MSAL tooforget hello 目前的使用者。
雖然此範例中的 hello 應用程式支援單一使用者，但是 MSAL 支援的案例，其中多個帳戶可以是登入在 hello 相同時間 – 範例可以是電子郵件應用程式使用者有多個帳戶的位置。
<!--end-collapse-->

## <a name="display-basic-token-information"></a>顯示基本權杖資訊

1. 新增下列方法 tootooyour hello `MainWindow.xaml.cs` toodisplay hello 權杖相關的基本資訊：

```csharp
/// <summary>
/// Display basic information contained in hello token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a>相關資訊

透過取得 token *OpenID Connect*也包含資訊相關 toohello 使用者的小型子集。 `DisplayBasicTokenInfo`會顯示包含在 hello 權杖中的基本資訊： 例如，hello 使用者的顯示名稱和識別碼，以及 hello 權杖到期日期和 hello 字串本身 hello 存取權杖。 這項資訊會顯示您 toosee。 您可以叫用 hello*呼叫 Microsoft Graph API*按鈕多次，並查看該相同的語彙基元已重複使用的後續要求的 hello。 您也可以查看當 MSAL 決定它是時間 toorenew hello 語彙基元要擴充的 hello 到期日。
<!--end-collapse-->

