tooenable 設定檔編輯您的應用程式上，您將需要 toocreate 編輯原則的設定檔。 此原則描述 hello 體驗，取用者會通過期間的 hello 應用程式將會成功完成時收到的權杖設定檔編輯和 hello 內容。

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

在 hello 原則區段的設定中，選取**編輯原則的設定檔**按一下**+ 加**。

![選取設定檔編輯原則，然後按一下 hello [新增] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

輸入原則**名稱**的應用程式 tooreference。 例如，輸入 `SiPe`。

選取 [識別提供者]，然後勾選 [本機帳戶登入]。 (選擇性) 您也可以選取社交身分識別提供者 (如果已經設定)。 按一下 [確定] 。

![選取身分識別提供者的本機帳戶登入，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

選取 [設定檔屬性]。 選擇屬性 hello 取用者可以檢視和編輯其設定檔中。 例如，勾選 [國家/區域]、[顯示名稱] 和 [郵遞區號]。 按一下 [確定] 。

![選取的某些屬性，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

選取 [應用程式宣告]。 選擇您要在 hello 授權權杖中傳回的宣告傳送後 tooyour 後成功的設定檔編輯體驗的應用程式。 例如，選取 [顯示名稱] 和 [郵遞區號]。

![選取某些應用程式宣告，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

按一下**建立**tooadd hello 原則。 hello 原則會列為**B2C_1_SiPe**。 hello **B2C_1_**前置詞是附加的 toohello 名稱。

選取開啟 hello 原則**B2C_1_SiPe**。 請確認指定 hello 資料表中的 hello 設定，然後按一下 **立即執行**。

![選取原則並加以執行](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| 設定      | 值  |
| ------------ | ------ |
| **應用程式** | Contoso B2C 應用程式 |
| **選取回覆 URL** | `https://localhost:44316/` |

新的瀏覽器索引標籤隨即開啟，而且可以驗證 hello 設定檔設定，請編輯經驗。

> [!NOTE]
> 它會佔用 tooa 分鐘的時間，建立原則，並更新 tootake 效果。
>