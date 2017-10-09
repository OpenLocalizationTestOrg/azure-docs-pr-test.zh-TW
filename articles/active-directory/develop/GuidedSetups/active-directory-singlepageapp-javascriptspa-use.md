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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>使用 hello Microsoft 驗證程式庫 (MSAL) toosign 在 hello 使用者

1.  建立名為 `app.js` 的檔案。 如果您使用 Visual Studio 中，選取 hello 專案 （專案根資料夾中），以滑鼠右鍵按一下，然後選取： `Add`  >  `New Item`  >  `JavaScript File`:
2.  新增下列程式碼 tooyour hello`app.js`檔案：

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
### <a name="more-information"></a>相關資訊

使用者按一下 hello 之後*' 呼叫 Microsoft Graph API'* hello 第一次，按鈕`callGraphApi`方法呼叫`loginRedirect`toosign hello 使用者。 這個方法會導致重新導向 hello 使用者 toohello *Microsoft Azure Active Directory v2 端點*tooprompt 並驗證 hello 使用者的認證。 成功登入，因為 hello 使用者已重新導向後 toohello 原始*index.html*  頁面上，而語彙基元接收、 處理由`msal.js`和快取 hello hello 權杖中所包含的資訊。 這個語彙基元稱為 hello *ID 語彙基元*和包含 hello 使用者，例如 hello 使用者顯示名稱的基本資訊。 如果您計劃 toouse 任何資料提供任何基於此語彙基元，您需要確定此語彙基元所驗證的語彙基元 hello 您後端伺服器 tooguarantee toomake 發出 tooa 有效的使用者，您的應用程式。

hello SPA 本指南所產生並不會使用直接的 hello 的 ID 語彙基元-相反地，它會呼叫`acquireTokenSilent`及/或`acquireTokenRedirect`tooacquire*存取權杖*用 tooquery hello Microsoft Graph API。 如果您需要驗證 hello 的 ID 語彙基元的範例，看看[這](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 範例")GitHub-範例應用程式會使用 hello 範例ASP.NET Web API 的權杖驗證。

#### <a name="getting-a-user-token-interactively"></a>以互動方式取得使用者權杖

Hello 之後的初始登入，您不想 hello 詢問使用者 tooreauthenticate 每次需要 toorequest 語彙基元 tooaccess 資源 – 所以*acquireTokenSilent*應該使用大部分的 hello 階段 tooacquire token。 不過在情況下，您會需要使用者互動與 Azure Active Directory v2 端點 – tooforce 一些範例包括：
-   使用者可能需要 tooreenter 其認證，因為 hello 密碼已過期
-   您的應用程式要求存取 hello 至使用者需求 tooconsent 的 tooa 資源
-   需要雙因素驗證

呼叫 hello *acquireTokenRedirect(scope)*導致重新導向使用者 toohello Azure Active Directory v2 端點 (或*acquireTokenPopup(scope)*結果快顯視窗上的) 需要使用者的位置提供 hello 同意 toohello 的任一個確認他們的認證，與 toointeract 必要的資源或完成 hello 雙因素驗證。

#### <a name="getting-a-user-token-silently"></a>以無訊息方式取得使用者權杖
hello` acquireTokenSilent`方法會處理語彙基元收購並沒有任何使用者互動的更新。 之後`loginRedirect`(或`loginPopup`) 會針對要執行 hello 第一次， `acquireTokenSilent` hello 方法常用 tooobtain 權杖 tooaccess 呼叫 toorequest 的受保護的後續呼叫的資源，或更新權杖會以無訊息模式。
`acquireTokenSilent`可能會失敗，在某些情況下 – 例如，hello 使用者的密碼已過期。 您的應用程式可以透過兩種方式處理此例外狀況：

1.  呼叫太`acquireTokenRedirect`立即，而這會造成提示 hello 使用者 toosign 中的。 此模式常用於線上應用程式在 hello 應用程式可用 toohello 使用者沒有未經驗證的內容。 此 「 引導式的安裝程式所產生的 hello 範例會使用此模式。

2. 應用程式也可以進行互動式登入是必要項目，所以 hello 使用者可以選取 hello 正確的時間 toosign 中，或者 hello 應用程式可以重試的視覺指示 toohello 使用者`acquireTokenSilent`稍後。 這通常用於 hello 使用者可以使用 hello 應用程式的其他功能，而不被中斷-例如，發生未經驗證的內容 hello 應用程式中提供。 在此情況下，hello 使用者可以決定當他們想 toosign tooaccess hello 受保護的資源，或 toorefresh hello 過期的資訊。

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>呼叫 hello Microsoft Graph API，使用您剛取得 hello 語彙基元

新增下列程式碼 tooyour hello`app.js`檔案：

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>針對受保護 API 進行 REST 呼叫的詳細資訊

在本指南所建立的 hello 範例應用程式，hello`callWebApiWithToken()`方法是使用的 toomake HTTP`GET`針對受保護的資源需要權杖，然後再回到 hello 內容 toohello 呼叫端要求。 這個方法會加入 hello 取得語彙基元中 hello *HTTP 授權標頭*。 本指南所建立的 hello 範例應用程式，hello 資源已 hello Microsoft Graph API*我*端點 – 顯示 hello 使用者設定檔資訊。

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>加入方法 toosign 出 hello 使用者

新增下列程式碼 tooyour hello`app.js`檔案：

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
