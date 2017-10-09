tooenable 登入您的應用程式，您將需要 toocreate 登入的原則。 此原則成功的登入描述 hello 體驗，取用者會在登入期間進行，而且將會收到 hello hello 應用程式的權杖內容。

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

在 hello 原則區段的設定中，選取**註冊或登入的原則**按一下**+ 加**。

![選取註冊或登入原則，然後按一下 [新增] 按鈕](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

輸入原則**名稱**的應用程式 tooreference。 例如，輸入 `SiUpIn`。

選取 [識別提供者]，然後勾選 [電子郵件註冊]。 (選擇性) 您也可以選取社交身分識別提供者 (如果已經設定)。 按一下 [確定] 。

![選取身分識別提供者的電子郵件註冊，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

選取 [註冊屬性]。 選擇屬性要在註冊期間 toocollect hello 取用者。 例如，勾選 [國家/區域]、[顯示名稱] 和 [郵遞區號]。 按一下 [確定] 。

![選取的某些屬性，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

選取 [應用程式宣告]。 選擇您要在 hello 授權權杖中傳回的宣告傳送後 tooyour 後成功註冊或登入體驗的應用程式。 例如，選取 [顯示名稱]、[識別提供者]、[郵遞區號]、[使用者是新的] 和 [使用者的物件識別碼]。

![選取某些應用程式宣告，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

按一下**建立**tooadd hello 原則。 hello 原則會列為**B2C_1_SiUpIn**。 hello **B2C_1_**前置詞是附加的 toohello 名稱。

選取開啟 hello 原則**B2C_1_SiUpIn**。 請確認指定 hello 資料表中的 hello 設定，然後按一下 **立即執行**。

![選取原則並加以執行](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| 設定      | 值  |
| ------------ | ------ |
| **應用程式** | Contoso B2C 應用程式 |
| **選取回覆 URL** | `https://localhost:44316/` |

新的瀏覽器索引標籤隨即開啟，而且您可以確認 hello 註冊或登入經驗設定。

> [!NOTE]
> 它會佔用 tooa 分鐘的時間，建立原則，並更新 tootake 效果。
>