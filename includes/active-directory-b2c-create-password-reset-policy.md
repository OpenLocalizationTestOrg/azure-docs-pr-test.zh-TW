<span data-ttu-id="9fb7f-101">tooenable 重設您的應用程式在更細緻的密碼，您將需要 toocreate 密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="9fb7f-102">請注意該 hello 整個租用戶的密碼重設指定的選項[這裡](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md)。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="9fb7f-103">此原則會描述 hello 體驗 hello 取用者會提供密碼重設期間，將會收到 hello hello 應用程式的權杖內容成功地完成。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="9fb7f-104">在 hello 原則區段的設定中，選取**密碼重設原則**按一下**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![選取註冊或登入的原則，然後按一下 hello [新增] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="9fb7f-106">輸入原則**名稱**的應用程式 tooreference。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="9fb7f-107">例如，輸入 `SSPR`。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="9fb7f-108">選取 [識別提供者]，並勾選 [使用電子郵件地址重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="9fb7f-109">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-109">Click **OK**.</span></span>

![選取身分識別提供者使用電子郵件地址重設密碼，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="9fb7f-111">選取 [應用程式宣告]。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-111">Select **Application claims**.</span></span> <span data-ttu-id="9fb7f-112">選擇 傳送後 tooyour 應用程式想 hello 授權權杖中傳回的宣告之後成功的密碼重設的體驗。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="9fb7f-113">例如，選取 [使用者的物件識別碼]。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-113">For example, select **User's Object ID**.</span></span>

![選取某些應用程式宣告，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="9fb7f-115">按一下**建立**tooadd hello 原則。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="9fb7f-116">hello 原則會列為**B2C_1_SSPR**。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="9fb7f-117">hello **B2C_1_**前置詞是附加的 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="9fb7f-118">選取開啟 hello 原則**B2C_1_SSPR**。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="9fb7f-119">請確認指定 hello 資料表中的 hello 設定，然後按一下 **立即執行**。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![選取原則並加以執行](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="9fb7f-121">設定</span><span class="sxs-lookup"><span data-stu-id="9fb7f-121">Setting</span></span>      | <span data-ttu-id="9fb7f-122">值</span><span class="sxs-lookup"><span data-stu-id="9fb7f-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="9fb7f-123">**應用程式**</span><span class="sxs-lookup"><span data-stu-id="9fb7f-123">**Applications**</span></span> | <span data-ttu-id="9fb7f-124">Contoso B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="9fb7f-124">Contoso B2C app</span></span> |
| <span data-ttu-id="9fb7f-125">**選取回覆 URL**</span><span class="sxs-lookup"><span data-stu-id="9fb7f-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="9fb7f-126">新的瀏覽器索引標籤隨即開啟，而且可以驗證 hello 密碼重設您的應用程式中的消費者體驗。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="9fb7f-127">它會佔用 tooa 分鐘的時間，建立原則，並更新 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="9fb7f-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
