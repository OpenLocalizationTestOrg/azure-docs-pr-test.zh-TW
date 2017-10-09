---
title: "aaaAzure AD v2 JS SPA 引導式安裝-使用 |Microsoft 文件"
description: "JavaScript SPA 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="b44e5-103">使用 hello Microsoft 驗證程式庫 (MSAL) toosign 在 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="b44e5-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="b44e5-104">建立名為 `app.js` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b44e5-104">Create a file named `app.js`.</span></span> <span data-ttu-id="b44e5-105">如果您使用 Visual Studio 中，選取 hello 專案 （專案根資料夾中），以滑鼠右鍵按一下，然後選取： `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="b44e5-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="b44e5-106">新增下列程式碼 tooyour hello`app.js`檔案：</span><span class="sxs-lookup"><span data-stu-id="b44e5-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="b44e5-107">相關資訊</span><span class="sxs-lookup"><span data-stu-id="b44e5-107">More Information</span></span>

<span data-ttu-id="b44e5-108">使用者按一下 hello 之後*' 呼叫 Microsoft Graph API'* hello 第一次，按鈕`callGraphApi`方法呼叫`loginRedirect`toosign hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="b44e5-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="b44e5-109">這個方法會導致重新導向 hello 使用者 toohello *Microsoft Azure Active Directory v2 端點*tooprompt 並驗證 hello 使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="b44e5-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="b44e5-110">成功登入，因為 hello 使用者已重新導向後 toohello 原始*index.html*  頁面上，而語彙基元接收、 處理由`msal.js`和快取 hello hello 權杖中所包含的資訊。</span><span class="sxs-lookup"><span data-stu-id="b44e5-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="b44e5-111">這個語彙基元稱為 hello *ID 語彙基元*和包含 hello 使用者，例如 hello 使用者顯示名稱的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="b44e5-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="b44e5-112">如果您計劃 toouse 任何資料提供任何基於此語彙基元，您需要確定此語彙基元所驗證的語彙基元 hello 您後端伺服器 tooguarantee toomake 發出 tooa 有效的使用者，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b44e5-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="b44e5-113">hello SPA 本指南所產生並不會使用直接的 hello 的 ID 語彙基元-相反地，它會呼叫`acquireTokenSilent`及/或`acquireTokenRedirect`tooacquire*存取權杖*用 tooquery hello Microsoft Graph API。</span><span class="sxs-lookup"><span data-stu-id="b44e5-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="b44e5-114">如果您需要驗證 hello 的 ID 語彙基元的範例，看看[這](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 範例")GitHub-範例應用程式會使用 hello 範例ASP.NET Web API 的權杖驗證。</span><span class="sxs-lookup"><span data-stu-id="b44e5-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="b44e5-115">以互動方式取得使用者權杖</span><span class="sxs-lookup"><span data-stu-id="b44e5-115">Getting a user token interactively</span></span>

<span data-ttu-id="b44e5-116">Hello 之後的初始登入，您不想 hello 詢問使用者 tooreauthenticate 每次需要 toorequest 語彙基元 tooaccess 資源 – 所以*acquireTokenSilent*應該使用大部分的 hello 階段 tooacquire token。</span><span class="sxs-lookup"><span data-stu-id="b44e5-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="b44e5-117">不過在情況下，您會需要使用者互動與 Azure Active Directory v2 端點 – tooforce 一些範例包括：</span><span class="sxs-lookup"><span data-stu-id="b44e5-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="b44e5-118">使用者可能需要 tooreenter 其認證，因為 hello 密碼已過期</span><span class="sxs-lookup"><span data-stu-id="b44e5-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="b44e5-119">您的應用程式要求存取 hello 至使用者需求 tooconsent 的 tooa 資源</span><span class="sxs-lookup"><span data-stu-id="b44e5-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="b44e5-120">需要雙因素驗證</span><span class="sxs-lookup"><span data-stu-id="b44e5-120">Two factor authentication is required</span></span>

<span data-ttu-id="b44e5-121">呼叫 hello *acquireTokenRedirect(scope)*導致重新導向使用者 toohello Azure Active Directory v2 端點 (或*acquireTokenPopup(scope)*結果快顯視窗上的) 需要使用者的位置提供 hello 同意 toohello 的任一個確認他們的認證，與 toointeract 必要的資源或完成 hello 雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="b44e5-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="b44e5-122">以無訊息方式取得使用者權杖</span><span class="sxs-lookup"><span data-stu-id="b44e5-122">Getting a user token silently</span></span>
<span data-ttu-id="b44e5-123">hello` acquireTokenSilent`方法會處理語彙基元收購並沒有任何使用者互動的更新。</span><span class="sxs-lookup"><span data-stu-id="b44e5-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="b44e5-124">之後`loginRedirect`(或`loginPopup`) 會針對要執行 hello 第一次， `acquireTokenSilent` hello 方法常用 tooobtain 權杖 tooaccess 呼叫 toorequest 的受保護的後續呼叫的資源，或更新權杖會以無訊息模式。</span><span class="sxs-lookup"><span data-stu-id="b44e5-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="b44e5-125">`acquireTokenSilent`可能會失敗，在某些情況下 – 例如，hello 使用者的密碼已過期。</span><span class="sxs-lookup"><span data-stu-id="b44e5-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="b44e5-126">您的應用程式可以透過兩種方式處理此例外狀況：</span><span class="sxs-lookup"><span data-stu-id="b44e5-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="b44e5-127">呼叫太`acquireTokenRedirect`立即，而這會造成提示 hello 使用者 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="b44e5-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="b44e5-128">此模式常用於線上應用程式在 hello 應用程式可用 toohello 使用者沒有未經驗證的內容。</span><span class="sxs-lookup"><span data-stu-id="b44e5-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="b44e5-129">此 「 引導式的安裝程式所產生的 hello 範例會使用此模式。</span><span class="sxs-lookup"><span data-stu-id="b44e5-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="b44e5-130">應用程式也可以進行互動式登入是必要項目，所以 hello 使用者可以選取 hello 正確的時間 toosign 中，或者 hello 應用程式可以重試的視覺指示 toohello 使用者`acquireTokenSilent`稍後。</span><span class="sxs-lookup"><span data-stu-id="b44e5-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="b44e5-131">這通常用於 hello 使用者可以使用 hello 應用程式的其他功能，而不被中斷-例如，發生未經驗證的內容 hello 應用程式中提供。</span><span class="sxs-lookup"><span data-stu-id="b44e5-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="b44e5-132">在此情況下，hello 使用者可以決定當他們想 toosign tooaccess hello 受保護的資源，或 toorefresh hello 過期的資訊。</span><span class="sxs-lookup"><span data-stu-id="b44e5-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="b44e5-133">呼叫 hello Microsoft Graph API，使用您剛取得 hello 語彙基元</span><span class="sxs-lookup"><span data-stu-id="b44e5-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="b44e5-134">新增下列程式碼 tooyour hello`app.js`檔案：</span><span class="sxs-lookup"><span data-stu-id="b44e5-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in hello page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in hello page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="b44e5-135">針對受保護 API 進行 REST 呼叫的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="b44e5-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="b44e5-136">在本指南所建立的 hello 範例應用程式，hello`callWebApiWithToken()`方法是使用的 toomake HTTP`GET`針對受保護的資源需要權杖，然後再回到 hello 內容 toohello 呼叫端要求。</span><span class="sxs-lookup"><span data-stu-id="b44e5-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="b44e5-137">這個方法會加入 hello 取得語彙基元中 hello *HTTP 授權標頭*。</span><span class="sxs-lookup"><span data-stu-id="b44e5-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="b44e5-138">本指南所建立的 hello 範例應用程式，hello 資源已 hello Microsoft Graph API*我*端點 – 顯示 hello 使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="b44e5-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="b44e5-139">加入方法 toosign 出 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="b44e5-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="b44e5-140">新增下列程式碼 tooyour hello`app.js`檔案：</span><span class="sxs-lookup"><span data-stu-id="b44e5-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
