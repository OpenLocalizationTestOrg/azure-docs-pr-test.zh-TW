<span data-ttu-id="6e324-101">若要在您的應用程式中啟用設定檔編輯功能，您必須建立設定檔編輯原則。</span><span class="sxs-lookup"><span data-stu-id="6e324-101">To enable profile editing on your application, you will need to create a profile editing policy.</span></span> <span data-ttu-id="6e324-102">此原則描述取用者在設定檔編輯期間將會經歷的體驗，以及成功完成時，應用程式將收到的權杖內容。</span><span class="sxs-lookup"><span data-stu-id="6e324-102">This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="6e324-103">在設定的原則區段中，選取 [設定檔編輯原則]，然後按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="6e324-103">In the policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![選取設定檔編輯原則，然後按一下 [新增] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="6e324-105">輸入原則 [名稱]，以供您的應用程式參考。</span><span class="sxs-lookup"><span data-stu-id="6e324-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="6e324-106">例如，輸入 `SiPe`。</span><span class="sxs-lookup"><span data-stu-id="6e324-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="6e324-107">選取 [識別提供者]，然後勾選 [本機帳戶登入]。</span><span class="sxs-lookup"><span data-stu-id="6e324-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="6e324-108">(選擇性) 您也可以選取社交身分識別提供者 (如果已經設定)。</span><span class="sxs-lookup"><span data-stu-id="6e324-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="6e324-109">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="6e324-109">Click **OK**.</span></span>

![以識別提供者身分來選取 [本機帳戶登入]，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="6e324-111">選取 [設定檔屬性]。</span><span class="sxs-lookup"><span data-stu-id="6e324-111">Select **Profile attributes**.</span></span> <span data-ttu-id="6e324-112">選擇取用者可以在其設定檔中檢視及編輯的屬性。</span><span class="sxs-lookup"><span data-stu-id="6e324-112">Choose attributes the consumer can view and edit in their profile.</span></span> <span data-ttu-id="6e324-113">例如，勾選 [國家/區域]、[顯示名稱] 和 [郵遞區號]。</span><span class="sxs-lookup"><span data-stu-id="6e324-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="6e324-114">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="6e324-114">Click **OK**.</span></span>

![選取某些屬性，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="6e324-116">選取 [應用程式宣告]。</span><span class="sxs-lookup"><span data-stu-id="6e324-116">Select **Application claims**.</span></span> <span data-ttu-id="6e324-117">選擇成功編輯設定檔後，您要在授權權杖中傳回給應用程式的宣告。</span><span class="sxs-lookup"><span data-stu-id="6e324-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful profile editing experience.</span></span> <span data-ttu-id="6e324-118">例如，選取 [顯示名稱] 和 [郵遞區號]。</span><span class="sxs-lookup"><span data-stu-id="6e324-118">For example, select **Display Name**, **Postal Code**.</span></span>

![選取某些應用程式宣告，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="6e324-120">按一下 [建立] 以新增原則。</span><span class="sxs-lookup"><span data-stu-id="6e324-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="6e324-121">此原則列示為 **B2C_1_SiPe**。</span><span class="sxs-lookup"><span data-stu-id="6e324-121">The policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="6e324-122">名稱會附加 **B2C_1_** 前置詞。</span><span class="sxs-lookup"><span data-stu-id="6e324-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="6e324-123">選取 [B2C_1_SiPe] 以開啟原則。</span><span class="sxs-lookup"><span data-stu-id="6e324-123">Open the policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="6e324-124">驗證資料表中指定的設定，然後按一下 [立刻執行]。</span><span class="sxs-lookup"><span data-stu-id="6e324-124">Verify the settings specified in the table then click **Run now**.</span></span>

![選取原則並加以執行](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="6e324-126">設定</span><span class="sxs-lookup"><span data-stu-id="6e324-126">Setting</span></span>      | <span data-ttu-id="6e324-127">值</span><span class="sxs-lookup"><span data-stu-id="6e324-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="6e324-128">**應用程式**</span><span class="sxs-lookup"><span data-stu-id="6e324-128">**Applications**</span></span> | <span data-ttu-id="6e324-129">Contoso B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="6e324-129">Contoso B2C app</span></span> |
| <span data-ttu-id="6e324-130">**選取回覆 URL**</span><span class="sxs-lookup"><span data-stu-id="6e324-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="6e324-131">新的瀏覽器索引標籤隨即開啟，您可以依照設定驗證設定檔編輯取用者體驗。</span><span class="sxs-lookup"><span data-stu-id="6e324-131">A new browser tab opens, and you can verify the profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="6e324-132">建立和更新原則後，需要經過一分鐘才會生效。</span><span class="sxs-lookup"><span data-stu-id="6e324-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>