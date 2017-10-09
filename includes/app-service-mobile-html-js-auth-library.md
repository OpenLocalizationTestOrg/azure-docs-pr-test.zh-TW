### <span data-ttu-id="d9493-101"><a name="server-auth"></a>作法：向提供者驗證 (伺服器流程)</span><span class="sxs-lookup"><span data-stu-id="d9493-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="d9493-102">toohave 行動應用程式管理的應用程式中的 hello 驗證程序，您必須向您的身分識別提供者註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9493-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="d9493-103">然後在您的 Azure 應用程式服務，您需要 tooconfigure hello 應用程式識別碼和您的提供者所提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="d9493-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="d9493-104">如需詳細資訊，請參閱 hello 教學課程[新增 authentication tooyour 應用程式](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="d9493-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="d9493-105">當您註冊您的身分識別提供者之後時，呼叫 hello `.login()` hello 名稱提供者的方法。</span><span class="sxs-lookup"><span data-stu-id="d9493-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="d9493-106">例如，與 Facebook toologin 使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9493-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="d9493-107">hello hello 提供者有效值為 'aad'、 'facebook'、 'google'、 'microsoftaccount，' 和 'twitter'。</span><span class="sxs-lookup"><span data-stu-id="d9493-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="d9493-108">Google 驗證目前無法透過伺服器流程運作。</span><span class="sxs-lookup"><span data-stu-id="d9493-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="d9493-109">您必須使用 google tooauthenticate，[用戶端流程方法](#client-auth)。</span><span class="sxs-lookup"><span data-stu-id="d9493-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="d9493-110">在此情況下，Azure 應用程式服務會管理 hello OAuth 2.0 驗證流程。</span><span class="sxs-lookup"><span data-stu-id="d9493-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="d9493-111">它會顯示 hello hello 選提供者的登入頁面，並產生 hello 身分識別提供者的成功登入之後的應用程式服務驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="d9493-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="d9493-112">hello 登入函式，完成時，分別會傳回 JSON 物件會公開 hello 使用者識別碼以及應用程式服務驗證語彙基元 hello userId 和 authenticationToken 欄位中。</span><span class="sxs-lookup"><span data-stu-id="d9493-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="d9493-113">您可以快取並重複使用此權杖，直到它到期為止。</span><span class="sxs-lookup"><span data-stu-id="d9493-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="d9493-114"><a name="client-auth"></a>作法：向提供者驗證 (用戶端流程)</span><span class="sxs-lookup"><span data-stu-id="d9493-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="d9493-115">您的應用程式可以也獨立連絡 hello 身分識別提供者，然後提供 hello 傳回語彙基元 tooyour 應用程式服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d9493-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="d9493-116">此用戶端流程可讓您 tooprovide 單一登入體驗的使用者或 tooretrieve hello 身分識別提供者的其他使用者資料。</span><span class="sxs-lookup"><span data-stu-id="d9493-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="d9493-117">社交驗證基本範例</span><span class="sxs-lookup"><span data-stu-id="d9493-117">Social Authentication basic example</span></span>

<span data-ttu-id="d9493-118">這個範例會使用 Facebook 用戶端 SDK 進行驗證：</span><span class="sxs-lookup"><span data-stu-id="d9493-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="d9493-119">這個範例會假設該 hello 語彙基元提供 hello 個別提供者 SDK 會儲存在 hello token 的變數。</span><span class="sxs-lookup"><span data-stu-id="d9493-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="d9493-120">Microsoft 帳戶範例</span><span class="sxs-lookup"><span data-stu-id="d9493-120">Microsoft Account example</span></span>

<span data-ttu-id="d9493-121">下列範例會使用 hello hello Live SDK，可支援單一登入 Windows 市集應用程式使用的 Microsoft 帳戶：</span><span class="sxs-lookup"><span data-stu-id="d9493-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="d9493-122">這個範例會取得權杖向 Live Connect，這是提供的 tooyour 應用程式服務藉由呼叫 hello 登入函式。</span><span class="sxs-lookup"><span data-stu-id="d9493-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="d9493-123"><a name="auth-getinfo"></a>如何： 取得 hello 驗證使用者的相關資訊</span><span class="sxs-lookup"><span data-stu-id="d9493-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="d9493-124">hello 驗證資訊可以擷取從 hello`/.auth/me`使用 HTTP 端點呼叫任何 AJAX 程式庫。</span><span class="sxs-lookup"><span data-stu-id="d9493-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="d9493-125">請確定您設定 hello`X-ZUMO-AUTH`標頭 tooyour 驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="d9493-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="d9493-126">hello 驗證權杖會儲存在`client.currentUser.mobileServiceAuthenticationToken`。</span><span class="sxs-lookup"><span data-stu-id="d9493-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="d9493-127">例如，toouse hello 提取 API:</span><span class="sxs-lookup"><span data-stu-id="d9493-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="d9493-128">Fetch 可以 [npm 套件](https://www.npmjs.com/package/whatwg-fetch)的形式提供使用或從 [CDNJS](https://cdnjs.com/libraries/fetch) 使用瀏覽器下載。</span><span class="sxs-lookup"><span data-stu-id="d9493-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="d9493-129">您也可以使用 jQuery 或其他 AJAX API toofetch hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="d9493-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="d9493-130">系統會以 JSON 物件形式接收資料。</span><span class="sxs-lookup"><span data-stu-id="d9493-130">Data is received as a JSON object.</span></span>
