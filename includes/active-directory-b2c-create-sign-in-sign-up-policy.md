<span data-ttu-id="ae7c3-101">tooenable 登入您的應用程式，您將需要 toocreate 登入的原則。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-101">tooenable sign-in on your application, you will need toocreate a sign-in policy.</span></span> <span data-ttu-id="ae7c3-102">此原則成功的登入描述 hello 體驗，取用者會在登入期間進行，而且將會收到 hello hello 應用程式的權杖內容。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-102">This policy describes hello experiences that consumers will go through during sign-in and hello contents of tokens that hello application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="ae7c3-103">在 hello 原則區段的設定中，選取**註冊或登入的原則**按一下**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-103">In hello policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![選取註冊或登入原則，然後按一下 [新增] 按鈕](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="ae7c3-105">輸入原則**名稱**的應用程式 tooreference。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="ae7c3-106">例如，輸入 `SiUpIn`。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="ae7c3-107">選取 [識別提供者]，然後勾選 [電子郵件註冊]。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="ae7c3-108">(選擇性) 您也可以選取社交身分識別提供者 (如果已經設定)。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="ae7c3-109">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-109">Click **OK**.</span></span>

![選取身分識別提供者的電子郵件註冊，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="ae7c3-111">選取 [註冊屬性]。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="ae7c3-112">選擇屬性要在註冊期間 toocollect hello 取用者。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-112">Choose attributes you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="ae7c3-113">例如，勾選 [國家/區域]、[顯示名稱] 和 [郵遞區號]。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="ae7c3-114">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-114">Click **OK**.</span></span>

![選取的某些屬性，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="ae7c3-116">選取 [應用程式宣告]。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-116">Select **Application claims**.</span></span> <span data-ttu-id="ae7c3-117">選擇您要在 hello 授權權杖中傳回的宣告傳送後 tooyour 後成功註冊或登入體驗的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="ae7c3-118">例如，選取 [顯示名稱]、[識別提供者]、[郵遞區號]、[使用者是新的] 和 [使用者的物件識別碼]。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![選取某些應用程式宣告，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="ae7c3-120">按一下**建立**tooadd hello 原則。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="ae7c3-121">hello 原則會列為**B2C_1_SiUpIn**。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-121">hello policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="ae7c3-122">hello **B2C_1_**前置詞是附加的 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="ae7c3-123">選取開啟 hello 原則**B2C_1_SiUpIn**。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-123">Open hello policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="ae7c3-124">請確認指定 hello 資料表中的 hello 設定，然後按一下 **立即執行**。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![選取原則並加以執行](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="ae7c3-126">設定</span><span class="sxs-lookup"><span data-stu-id="ae7c3-126">Setting</span></span>      | <span data-ttu-id="ae7c3-127">值</span><span class="sxs-lookup"><span data-stu-id="ae7c3-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="ae7c3-128">**應用程式**</span><span class="sxs-lookup"><span data-stu-id="ae7c3-128">**Applications**</span></span> | <span data-ttu-id="ae7c3-129">Contoso B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="ae7c3-129">Contoso B2C app</span></span> |
| <span data-ttu-id="ae7c3-130">**選取回覆 URL**</span><span class="sxs-lookup"><span data-stu-id="ae7c3-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="ae7c3-131">新的瀏覽器索引標籤隨即開啟，而且您可以確認 hello 註冊或登入經驗設定。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-131">A new browser tab opens, and you can verify hello sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="ae7c3-132">它會佔用 tooa 分鐘的時間，建立原則，並更新 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="ae7c3-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>