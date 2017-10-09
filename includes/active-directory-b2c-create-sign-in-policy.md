tooenable 登入您的應用程式，您將需要 toocreate 登入的原則。 此原則成功的登入描述 hello 體驗，取用者會在登入期間進行，而且將會收到 hello hello 應用程式的權杖內容。

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]按一下 [登入原則]。

按一下**+ 加**在 hello hello 刀鋒視窗最上方。

hello**名稱**判斷您的應用程式所使用的 hello 登入的原則名稱。 例如，輸入 **SiIn**。

按一下 [識別提供者] 並選取 [本機帳戶登入]。 (選擇性) 您也可以選取社交身分識別提供者 (如果已經設定)。 按一下 [確定] 。

按一下 [應用程式宣告] 。 這裡可以選擇您想要傳回 hello 權杖中宣告傳送後 tooyour 後成功登入體驗的應用程式。 例如，選取 [顯示名稱]、[識別提供者]、[郵遞區號] 和 [使用者的物件識別碼]。 按一下 [確定] 。

按一下 [建立] 。 請注意您剛才建立的 hello 原則會顯示為**B2C_1_SiIn** (hello **B2C\_1\_** 片段會自動加入) 在 hello**登入原則**刀鋒視窗。

按一下以開啟 hello 原則**B2C_1_SiIn**。

選取**Contoso B2C 應用程式**在 hello**應用程式**下拉式清單和`https://localhost:44321/`在 hello**回覆 URL / 重新導向 URI**下拉式清單。

按一下 [立即執行] 。 新的瀏覽器索引標籤隨即開啟，而且您可以透過 hello 消費者體驗的登入您的應用程式。

> [!NOTE]
> 它會佔用 tooa 分鐘的時間，建立原則，並更新 tootake 效果。
>