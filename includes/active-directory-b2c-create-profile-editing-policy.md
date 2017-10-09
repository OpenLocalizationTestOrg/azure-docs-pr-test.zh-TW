<span data-ttu-id="a7be2-101">tooenable 設定檔編輯您的應用程式上，您將需要 toocreate 編輯原則的設定檔。</span><span class="sxs-lookup"><span data-stu-id="a7be2-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="a7be2-102">此原則描述 hello 體驗，取用者會通過期間的 hello 應用程式將會成功完成時收到的權杖設定檔編輯和 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="a7be2-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="a7be2-103">在 hello 原則區段的設定中，選取**編輯原則的設定檔**按一下**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="a7be2-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![選取設定檔編輯原則，然後按一下 hello [新增] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="a7be2-105">輸入原則**名稱**的應用程式 tooreference。</span><span class="sxs-lookup"><span data-stu-id="a7be2-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="a7be2-106">例如，輸入 `SiPe`。</span><span class="sxs-lookup"><span data-stu-id="a7be2-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="a7be2-107">選取 [識別提供者]，然後勾選 [本機帳戶登入]。</span><span class="sxs-lookup"><span data-stu-id="a7be2-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="a7be2-108">(選擇性) 您也可以選取社交身分識別提供者 (如果已經設定)。</span><span class="sxs-lookup"><span data-stu-id="a7be2-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="a7be2-109">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a7be2-109">Click **OK**.</span></span>

![選取身分識別提供者的本機帳戶登入，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="a7be2-111">選取 [設定檔屬性]。</span><span class="sxs-lookup"><span data-stu-id="a7be2-111">Select **Profile attributes**.</span></span> <span data-ttu-id="a7be2-112">選擇屬性 hello 取用者可以檢視和編輯其設定檔中。</span><span class="sxs-lookup"><span data-stu-id="a7be2-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="a7be2-113">例如，勾選 [國家/區域]、[顯示名稱] 和 [郵遞區號]。</span><span class="sxs-lookup"><span data-stu-id="a7be2-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="a7be2-114">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a7be2-114">Click **OK**.</span></span>

![選取的某些屬性，然後按一下 hello [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="a7be2-116">選取 [應用程式宣告]。</span><span class="sxs-lookup"><span data-stu-id="a7be2-116">Select **Application claims**.</span></span> <span data-ttu-id="a7be2-117">選擇您要在 hello 授權權杖中傳回的宣告傳送後 tooyour 後成功的設定檔編輯體驗的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7be2-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="a7be2-118">例如，選取 [顯示名稱] 和 [郵遞區號]。</span><span class="sxs-lookup"><span data-stu-id="a7be2-118">For example, select **Display Name**, **Postal Code**.</span></span>

![選取某些應用程式宣告，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="a7be2-120">按一下**建立**tooadd hello 原則。</span><span class="sxs-lookup"><span data-stu-id="a7be2-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="a7be2-121">hello 原則會列為**B2C_1_SiPe**。</span><span class="sxs-lookup"><span data-stu-id="a7be2-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="a7be2-122">hello **B2C_1_**前置詞是附加的 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="a7be2-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="a7be2-123">選取開啟 hello 原則**B2C_1_SiPe**。</span><span class="sxs-lookup"><span data-stu-id="a7be2-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="a7be2-124">請確認指定 hello 資料表中的 hello 設定，然後按一下 **立即執行**。</span><span class="sxs-lookup"><span data-stu-id="a7be2-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![選取原則並加以執行](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="a7be2-126">設定</span><span class="sxs-lookup"><span data-stu-id="a7be2-126">Setting</span></span>      | <span data-ttu-id="a7be2-127">值</span><span class="sxs-lookup"><span data-stu-id="a7be2-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="a7be2-128">**應用程式**</span><span class="sxs-lookup"><span data-stu-id="a7be2-128">**Applications**</span></span> | <span data-ttu-id="a7be2-129">Contoso B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="a7be2-129">Contoso B2C app</span></span> |
| <span data-ttu-id="a7be2-130">**選取回覆 URL**</span><span class="sxs-lookup"><span data-stu-id="a7be2-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="a7be2-131">新的瀏覽器索引標籤隨即開啟，而且可以驗證 hello 設定檔設定，請編輯經驗。</span><span class="sxs-lookup"><span data-stu-id="a7be2-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="a7be2-132">它會佔用 tooa 分鐘的時間，建立原則，並更新 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="a7be2-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>