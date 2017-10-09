[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister 行動或原生應用程式，使用 hello 設定 hello 資料表中指定。

![新行動或原生應用程式的範例註冊設定](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| 設定      | 範例值  | 說明                                        |
| ------------ | ------- | -------------------------------------------------- |
| **名稱** | Contoso B2C 應用程式 | 輸入**名稱**描述應用程式 tooconsumers hello 應用程式。 |
| **原生用戶端** | 是 | 針對行動或原生應用程式選取 [是]。 |
| **自訂重新導向 URI** | `com.onmicrosoft.contoso.appname://redirect/path` | 輸入具有自訂配置的重新導向 URI。 務必選擇[良好的重新導向 URI](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri)，但不包含特殊字元 (例如底線)。 |

按一下**建立**tooregister 您的應用程式。

您註冊新的應用程式會顯示 hello hello B2C 租用戶的應用程式清單中。 Hello 清單中選取行動或原生應用程式。 hello 應用程式的 [屬性] 窗格會顯示。

![應用程式屬性](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

請記下 hello 全域唯一**應用程式用戶端識別碼**。 您在您的應用程式程式碼中使用識別碼 hello。

如果您的原生應用程式呼叫 Azure AD B2C 所保護的 Web API，請執行下列步驟：
   1. 建立應用程式密碼將 toohello**金鑰**刀鋒視窗，然後按一下 hello**產生金鑰** 按鈕。 請記下 hello**應用程式金鑰**值。 您可以使用 hello 值做為您的應用程式程式碼中的 hello 應用程式密碼。
   2. 按一下 [API 存取][新增] 並選取您的 Web API 和範圍 (權限)。

> [!NOTE]
> **應用程式密鑰** 是重要的安全性認證，應該適當地加以保護。
> 
