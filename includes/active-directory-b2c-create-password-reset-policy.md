<span data-ttu-id="e07b1-101">若要在您的應用程式上啟用更細緻的密碼重設，您必須建立密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="e07b1-101">To enable fine-grained password reset on your application, you will need to create a password reset policy.</span></span> <span data-ttu-id="e07b1-102">請注意，[這裡](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md)包含租用戶密碼重設的所有選項。</span><span class="sxs-lookup"><span data-stu-id="e07b1-102">Note that the tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="e07b1-103">此原則描述取用者在密碼重設期間將經歷的體驗，以及成功完成時，應用程式將收到的權杖內容。</span><span class="sxs-lookup"><span data-stu-id="e07b1-103">This policy describes the experiences that the consumers will go through during password reset and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="e07b1-104">在設定的原則區段中，選取 [密碼重設原則]，然後按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="e07b1-104">In the policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![選取註冊或登入原則，然後按一下 [新增] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="e07b1-106">輸入原則 [名稱]，以供您的應用程式參考。</span><span class="sxs-lookup"><span data-stu-id="e07b1-106">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="e07b1-107">例如，輸入 `SSPR`。</span><span class="sxs-lookup"><span data-stu-id="e07b1-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="e07b1-108">選取 [識別提供者]，並勾選 [使用電子郵件地址重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="e07b1-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="e07b1-109">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e07b1-109">Click **OK**.</span></span>

![以電子郵件地址作為識別提供者來選取重設密碼，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="e07b1-111">選取 [應用程式宣告]。</span><span class="sxs-lookup"><span data-stu-id="e07b1-111">Select **Application claims**.</span></span> <span data-ttu-id="e07b1-112">選擇在成功進行密碼重設之後，您要在授權權杖中傳回給應用程式的宣告。</span><span class="sxs-lookup"><span data-stu-id="e07b1-112">Choose claims you want returned in the authorization tokens sent back to your application after a successful password reset experience.</span></span> <span data-ttu-id="e07b1-113">例如，選取 [使用者的物件識別碼]。</span><span class="sxs-lookup"><span data-stu-id="e07b1-113">For example, select **User's Object ID**.</span></span>

![選取某些應用程式宣告，然後按一下 [確定] 按鈕](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="e07b1-115">按一下 [建立] 以新增原則。</span><span class="sxs-lookup"><span data-stu-id="e07b1-115">Click **Create** to add the policy.</span></span> <span data-ttu-id="e07b1-116">此原則列示為 **B2C_1_SSPR**。</span><span class="sxs-lookup"><span data-stu-id="e07b1-116">The policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="e07b1-117">名稱會附加 **B2C_1_** 前置詞。</span><span class="sxs-lookup"><span data-stu-id="e07b1-117">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="e07b1-118">選取 **B2C_1_SSPR** 以開啟原則。</span><span class="sxs-lookup"><span data-stu-id="e07b1-118">Open the policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="e07b1-119">驗證資料表中指定的設定，然後按一下 [立刻執行]。</span><span class="sxs-lookup"><span data-stu-id="e07b1-119">Verify the settings specified in the table then click **Run now**.</span></span>

![選取原則並加以執行](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="e07b1-121">設定</span><span class="sxs-lookup"><span data-stu-id="e07b1-121">Setting</span></span>      | <span data-ttu-id="e07b1-122">值</span><span class="sxs-lookup"><span data-stu-id="e07b1-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="e07b1-123">**應用程式**</span><span class="sxs-lookup"><span data-stu-id="e07b1-123">**Applications**</span></span> | <span data-ttu-id="e07b1-124">Contoso B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="e07b1-124">Contoso B2C app</span></span> |
| <span data-ttu-id="e07b1-125">**選取回覆 URL**</span><span class="sxs-lookup"><span data-stu-id="e07b1-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="e07b1-126">新的瀏覽器索引標籤隨即開啟，您可以在應用程式中驗證密碼重設取用者體驗。</span><span class="sxs-lookup"><span data-stu-id="e07b1-126">A new browser tab opens, and you can verify the password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="e07b1-127">建立和更新原則後，需要經過一分鐘才會生效。</span><span class="sxs-lookup"><span data-stu-id="e07b1-127">It takes up to a minute for policy creation and updates to take effect.</span></span>
>
