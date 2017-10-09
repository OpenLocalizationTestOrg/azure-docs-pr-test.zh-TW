[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister 您的 web API，使用指定 hello 資料表中的 hello 設定。

![新 Web API 的範例註冊設定](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| 設定      | 範例值  | 說明                                        |
| ------------ | ------- | -------------------------------------------------- |
| **名稱** | Contoso B2C API | 輸入**名稱**描述您 API tooconsumers hello 應用程式。 | 
| **包含 Web 應用程式 / Web API** | 是 | 針對 Web API 選取 [是]。 |
| **允許隱含流程** | 是 | 如果您的應用程式使用 [OpenID Connect 登入](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md)，請選取 [是] |
| **回覆 URL** | `https://localhost:44316/` | 回覆 URL 是 Azure AD B2C 傳回您應用程式要求之任何權杖的所在端點。 輸入[適當的](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) [回覆 URL]。 在此範例中，您的 Web API 位於本機並在通訊埠 44316 上進行接聽。 |
| **應用程式識別碼 URI** | api | hello 應用程式識別碼 URI 是用於您的 web API 的 hello 識別項。 hello URI 包括 hello 網域時產生的完整識別碼。 |

按一下**建立**tooregister 您的應用程式。

您註冊新的應用程式會顯示 hello hello B2C 租用戶的應用程式清單中。 Hello 清單中選取您的 web API。 hello API 的 [屬性] 窗格會顯示。

![Web API 屬性](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

請記下 hello 全域唯一**應用程式用戶端識別碼**。 您在您的應用程式程式碼中使用識別碼 hello。
