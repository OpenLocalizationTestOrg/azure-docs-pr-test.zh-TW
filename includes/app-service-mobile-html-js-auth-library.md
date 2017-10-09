### <a name="server-auth"></a>作法：向提供者驗證 (伺服器流程)
toohave 行動應用程式管理的應用程式中的 hello 驗證程序，您必須向您的身分識別提供者註冊您的應用程式。 然後在您的 Azure 應用程式服務，您需要 tooconfigure hello 應用程式識別碼和您的提供者所提供的密碼。
如需詳細資訊，請參閱 hello 教學課程[新增 authentication tooyour 應用程式](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md)。

當您註冊您的身分識別提供者之後時，呼叫 hello `.login()` hello 名稱提供者的方法。 例如，與 Facebook toologin 使用下列程式碼的 hello:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

hello hello 提供者有效值為 'aad'、 'facebook'、 'google'、 'microsoftaccount，' 和 'twitter'。

> [!NOTE]
> Google 驗證目前無法透過伺服器流程運作。  您必須使用 google tooauthenticate，[用戶端流程方法](#client-auth)。

在此情況下，Azure 應用程式服務會管理 hello OAuth 2.0 驗證流程。  它會顯示 hello hello 選提供者的登入頁面，並產生 hello 身分識別提供者的成功登入之後的應用程式服務驗證權杖。 hello 登入函式，完成時，分別會傳回 JSON 物件會公開 hello 使用者識別碼以及應用程式服務驗證語彙基元 hello userId 和 authenticationToken 欄位中。 您可以快取並重複使用此權杖，直到它到期為止。

###<a name="client-auth"></a>作法：向提供者驗證 (用戶端流程)

您的應用程式可以也獨立連絡 hello 身分識別提供者，然後提供 hello 傳回語彙基元 tooyour 應用程式服務進行驗證。 此用戶端流程可讓您 tooprovide 單一登入體驗的使用者或 tooretrieve hello 身分識別提供者的其他使用者資料。

#### <a name="social-authentication-basic-example"></a>社交驗證基本範例

這個範例會使用 Facebook 用戶端 SDK 進行驗證：

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
這個範例會假設該 hello 語彙基元提供 hello 個別提供者 SDK 會儲存在 hello token 的變數。

#### <a name="microsoft-account-example"></a>Microsoft 帳戶範例

下列範例會使用 hello hello Live SDK，可支援單一登入 Windows 市集應用程式使用的 Microsoft 帳戶：

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

這個範例會取得權杖向 Live Connect，這是提供的 tooyour 應用程式服務藉由呼叫 hello 登入函式。

###<a name="auth-getinfo"></a>如何： 取得 hello 驗證使用者的相關資訊

hello 驗證資訊可以擷取從 hello`/.auth/me`使用 HTTP 端點呼叫任何 AJAX 程式庫。  請確定您設定 hello`X-ZUMO-AUTH`標頭 tooyour 驗證權杖。  hello 驗證權杖會儲存在`client.currentUser.mobileServiceAuthenticationToken`。  例如，toouse hello 提取 API:

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

Fetch 可以 [npm 套件](https://www.npmjs.com/package/whatwg-fetch)的形式提供使用或從 [CDNJS](https://cdnjs.com/libraries/fetch) 使用瀏覽器下載。 您也可以使用 jQuery 或其他 AJAX API toofetch hello 資訊。  系統會以 JSON 物件形式接收資料。
