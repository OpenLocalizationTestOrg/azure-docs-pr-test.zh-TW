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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="8421b-103">用於 hello Microsoft Graph API 中的 hello Microsoft 驗證程式庫 (MSAL) tooget 語彙基元</span><span class="sxs-lookup"><span data-stu-id="8421b-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="8421b-104">本節說明如何 toouse MSAL tooget 語彙基元 hello Microsoft Graph API。</span><span class="sxs-lookup"><span data-stu-id="8421b-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="8421b-105">在`MainWindow.xaml.cs`，加入 hello MSAL 程式庫 toohello 類別的參考：</span><span class="sxs-lookup"><span data-stu-id="8421b-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="8421b-106">將 <code>MainWindow</code> 類別程式碼取代為：</span><span class="sxs-lookup"><span data-stu-id="8421b-106">Replace <code>MainWindow</code> class code with:</span></span>
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
### <a name="more-information"></a><span data-ttu-id="8421b-107">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="8421b-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="8421b-108">以互動方式取得使用者權杖</span><span class="sxs-lookup"><span data-stu-id="8421b-108">Getting a user token interactive</span></span>
<span data-ttu-id="8421b-109">呼叫 hello`AcquireTokenAsync`方法的結果 視窗，提示 hello 使用者 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="8421b-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="8421b-110">應用程式通常需要以互動方式 hello 中的使用者 toosign 第一次需要 tooaccess 受保護的資源，或無訊息作業 tooacquire 權杖就會失敗 （例如 hello 使用者密碼到期時）。</span><span class="sxs-lookup"><span data-stu-id="8421b-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="8421b-111">以無訊息方式取得使用者權杖</span><span class="sxs-lookup"><span data-stu-id="8421b-111">Getting a user token silently</span></span>
<span data-ttu-id="8421b-112">`AcquireTokenSilentAsync` 會處理權杖取得和更新作業，不需要與使用者進行任何互動。</span><span class="sxs-lookup"><span data-stu-id="8421b-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="8421b-113">之後`AcquireTokenAsync`會針對要執行 hello 第一次， `AcquireTokenSilentAsync` hello 所使用的一般方法 tooobtain 權杖 tooaccess 呼叫 toorequest 的受保護的後續呼叫的資源，或更新權杖會以無訊息模式。</span><span class="sxs-lookup"><span data-stu-id="8421b-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="8421b-114">最後，`AcquireTokenSilentAsync`將會失敗 – 例如 hello 使用者已登出，或已變更其密碼，另一個裝置上的。</span><span class="sxs-lookup"><span data-stu-id="8421b-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="8421b-115">當 MSAL 偵測到 hello 問題可透過要求互動的動作來解決時，它就會引發`MsalUiRequiredException`。</span><span class="sxs-lookup"><span data-stu-id="8421b-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="8421b-116">您的應用程式可以透過兩種方式處理此例外狀況：</span><span class="sxs-lookup"><span data-stu-id="8421b-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="8421b-117">進行呼叫，以針對`AcquireTokenAsync`立即，這會導致提示 toosign 中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="8421b-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="8421b-118">此模式通常用於線上應用程式在沒有離線內容 hello 應用程式中可供 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="8421b-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="8421b-119">hello 此引導式的安裝程式所產生的範例會使用此模式： 您可以看到它動作 hello 中第一次執行 hello 範例： 沒有任何使用者都用過 hello 應用程式，因為`PublicClientApp.Users.FirstOrDefault()`會包含 null 值，和`MsalUiRequiredException`擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8421b-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="8421b-120">hello hello 範例中的程式碼，則控制代碼藉由呼叫 hello 例外狀況`AcquireTokenAsync`導致提示 toosign 中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="8421b-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="8421b-121">應用程式也可以進行互動式登入是必要項目，所以 hello 使用者可以選取 hello 正確的時間 toosign 中，或者 hello 應用程式可以重試的視覺指示 toohello 使用者`AcquireTokenSilentAsync`稍後。</span><span class="sxs-lookup"><span data-stu-id="8421b-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="8421b-122">這通常用於 hello 使用者可以使用 hello 應用程式的其他功能，而不被中斷-例如，沒有離線內容 hello 應用程式中提供。</span><span class="sxs-lookup"><span data-stu-id="8421b-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="8421b-123">在此情況下，hello 使用者可以決定當他們想 toosign tooaccess hello 受保護的資源，或 toorefresh hello 過期的資訊，或您的應用程式可以決定 tooretry`AcquireTokenSilentAsync`網路還原之後變成暫時無法使用時。</span><span class="sxs-lookup"><span data-stu-id="8421b-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="8421b-124">呼叫 hello Microsoft Graph API，使用您剛取得 hello 語彙基元</span><span class="sxs-lookup"><span data-stu-id="8421b-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="8421b-125">將以下 tooyour hello 新方法加入`MainWindow.xaml.cs`。</span><span class="sxs-lookup"><span data-stu-id="8421b-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="8421b-126">hello 方法是使用的 toomake`GET`對 Graph API 的使用授權標頭的要求：</span><span class="sxs-lookup"><span data-stu-id="8421b-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="8421b-127">針對受保護 API 進行 REST 呼叫的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="8421b-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="8421b-128">在此範例應用程式，hello`GetHttpContentWithToken`方法是使用的 toomake HTTP`GET`針對受保護的資源需要權杖，然後再回到 hello 內容 toohello 呼叫端要求。</span><span class="sxs-lookup"><span data-stu-id="8421b-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="8421b-129">這個方法會加入 hello 取得語彙基元中 hello *HTTP 授權標頭*。</span><span class="sxs-lookup"><span data-stu-id="8421b-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="8421b-130">此範例中，hello 資源為 hello Microsoft Graph API*我*端點 – 顯示 hello 使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="8421b-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="8421b-131">加入方法 toosign 出 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="8421b-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="8421b-132">新增下列方法 tooyour hello `MainWindow.xaml.cs` toosign 出 hello 使用者：</span><span class="sxs-lookup"><span data-stu-id="8421b-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="8421b-133">關於登出的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="8421b-133">More info on Sign-Out</span></span>

<span data-ttu-id="8421b-134">`SignOutButton_Click`移除 hello MSAL 使用者快取中的使用者，讓未來的要求 tooacquire 語彙基元才會成功則由 toobe 互動式，這會有效地指示 MSAL tooforget hello 目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="8421b-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="8421b-135">雖然此範例中的 hello 應用程式支援單一使用者，但是 MSAL 支援的案例，其中多個帳戶可以是登入在 hello 相同時間 – 範例可以是電子郵件應用程式使用者有多個帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="8421b-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="8421b-136">顯示基本權杖資訊</span><span class="sxs-lookup"><span data-stu-id="8421b-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="8421b-137">新增下列方法 tootooyour hello `MainWindow.xaml.cs` toodisplay hello 權杖相關的基本資訊：</span><span class="sxs-lookup"><span data-stu-id="8421b-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="8421b-138">相關資訊</span><span class="sxs-lookup"><span data-stu-id="8421b-138">More Information</span></span>

<span data-ttu-id="8421b-139">透過取得 token *OpenID Connect*也包含資訊相關 toohello 使用者的小型子集。</span><span class="sxs-lookup"><span data-stu-id="8421b-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="8421b-140">`DisplayBasicTokenInfo`會顯示包含在 hello 權杖中的基本資訊： 例如，hello 使用者的顯示名稱和識別碼，以及 hello 權杖到期日期和 hello 字串本身 hello 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="8421b-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="8421b-141">這項資訊會顯示您 toosee。</span><span class="sxs-lookup"><span data-stu-id="8421b-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="8421b-142">您可以叫用 hello*呼叫 Microsoft Graph API*按鈕多次，並查看該相同的語彙基元已重複使用的後續要求的 hello。</span><span class="sxs-lookup"><span data-stu-id="8421b-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="8421b-143">您也可以查看當 MSAL 決定它是時間 toorenew hello 語彙基元要擴充的 hello 到期日。</span><span class="sxs-lookup"><span data-stu-id="8421b-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

