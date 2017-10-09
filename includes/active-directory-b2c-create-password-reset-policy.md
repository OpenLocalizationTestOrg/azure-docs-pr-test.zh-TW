tooenable 重設您的應用程式在更細緻的密碼，您將需要 toocreate 密碼重設原則。 請注意該 hello 整個租用戶的密碼重設指定的選項[這裡](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md)。 此原則會描述 hello 體驗 hello 取用者會提供密碼重設期間，將會收到 hello hello 應用程式的權杖內容成功地完成。

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

在 hello 原則區段的設定中，選取**密碼重設原則**按一下**+ 加**。

![選取註冊或登入的原則，然後按一下 hello [新增] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

輸入原則**名稱**的應用程式 tooreference。 例如，輸入 `SSPR`。

選取 [識別提供者]，並勾選 [使用電子郵件地址重設密碼]。 按一下 [確定] 。

![選取身分識別提供者使用電子郵件地址重設密碼，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

選取 [應用程式宣告]。 選擇 傳送後 tooyour 應用程式想 hello 授權權杖中傳回的宣告之後成功的密碼重設的體驗。 例如，選取 [使用者的物件識別碼]。

![選取某些應用程式宣告，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

按一下**建立**tooadd hello 原則。 hello 原則會列為**B2C_1_SSPR**。 hello **B2C_1_**前置詞是附加的 toohello 名稱。

選取開啟 hello 原則**B2C_1_SSPR**。 請確認指定 hello 資料表中的 hello 設定，然後按一下 **立即執行**。

![選取原則並加以執行](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| 設定      | 值  |
| ------------ | ------ |
| **應用程式** | Contoso B2C 應用程式 |
| **選取回覆 URL** | `https://localhost:44316/` |

新的瀏覽器索引標籤隨即開啟，而且可以驗證 hello 密碼重設您的應用程式中的消費者體驗。

> [!NOTE]
> 它會佔用 tooa 分鐘的時間，建立原則，並更新 tootake 效果。
>
