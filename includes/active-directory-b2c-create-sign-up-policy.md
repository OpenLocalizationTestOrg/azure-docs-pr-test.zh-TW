<span data-ttu-id="2650e-101">tooenable 註冊您的應用程式上，您需要 toocreate 註冊的原則。</span><span class="sxs-lookup"><span data-stu-id="2650e-101">tooenable sign-up on your application, you need toocreate a sign-up policy.</span></span> <span data-ttu-id="2650e-102">此原則描述成功註冊 hello 體驗，取用者經過在註冊期間，收到 hello hello 應用程式的權杖內容。</span><span class="sxs-lookup"><span data-stu-id="2650e-102">This policy describes hello experiences that consumers go through during sign-up and hello contents of tokens that hello application receives on successful sign-ups.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="2650e-103">按一下 [註冊原則] 。</span><span class="sxs-lookup"><span data-stu-id="2650e-103">Click **Sign-up policies**.</span></span>

<span data-ttu-id="2650e-104">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="2650e-104">Click **+Add** at hello top of hello blade.</span></span>

<span data-ttu-id="2650e-105">hello**名稱**判斷您的應用程式所使用的 hello 註冊的原則名稱。</span><span class="sxs-lookup"><span data-stu-id="2650e-105">hello **Name** determines hello sign-up policy name used by your application.</span></span> <span data-ttu-id="2650e-106">例如，輸入 **SiUp**。</span><span class="sxs-lookup"><span data-stu-id="2650e-106">For example, enter **SiUp**.</span></span>

<span data-ttu-id="2650e-107">按一下 [識別提供者] 並選取 [電子郵件註冊]。</span><span class="sxs-lookup"><span data-stu-id="2650e-107">Click **Identity providers** and select **Email signup**.</span></span> <span data-ttu-id="2650e-108">(選擇性) 您也可以選取社交身分識別提供者 (如果已經設定)。</span><span class="sxs-lookup"><span data-stu-id="2650e-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="2650e-109">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2650e-109">Click **OK**.</span></span>

<span data-ttu-id="2650e-110">按一下 [註冊屬性] 。</span><span class="sxs-lookup"><span data-stu-id="2650e-110">Click **Sign-up attributes**.</span></span> <span data-ttu-id="2650e-111">這裡可以選擇屬性的 toocollect hello 取用者在註冊期間。</span><span class="sxs-lookup"><span data-stu-id="2650e-111">Here you choose attributes that you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="2650e-112">例如，選取 [國家/區域]、[顯示名稱] 和 [郵遞區號]。</span><span class="sxs-lookup"><span data-stu-id="2650e-112">For example, select **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="2650e-113">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2650e-113">Click **OK**.</span></span>

<span data-ttu-id="2650e-114">按一下 [應用程式宣告] 。</span><span class="sxs-lookup"><span data-stu-id="2650e-114">Click **Application claims**.</span></span> <span data-ttu-id="2650e-115">這裡可以選擇您想要傳回 hello 權杖中宣告傳送後 tooyour 後成功的註冊體驗的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2650e-115">Here you choose claims that you want returned in hello tokens sent back tooyour application after a successful sign-up experience.</span></span> <span data-ttu-id="2650e-116">例如，選取 [顯示名稱]、[身分識別提供者]、[郵遞區號]、[使用者是新的] 和 [使用者的物件識別碼]。</span><span class="sxs-lookup"><span data-stu-id="2650e-116">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new**, and **User's Object ID**.</span></span>

<span data-ttu-id="2650e-117">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2650e-117">Click **Create**.</span></span> <span data-ttu-id="2650e-118">建立 hello 原則會顯示為**B2C_1_SiUp** (hello **B2C\_1\_** 片段會自動加入) 在 hello**註冊原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2650e-118">hello policy created appears as **B2C_1_SiUp** (hello **B2C\_1\_** fragment is automatically added) in hello **Sign-up policies** blade.</span></span>

<span data-ttu-id="2650e-119">按一下以開啟 hello 原則**B2C_1_SiUp**。</span><span class="sxs-lookup"><span data-stu-id="2650e-119">Open hello policy by clicking **B2C_1_SiUp**.</span></span>

<span data-ttu-id="2650e-120">選取**Contoso B2C 應用程式**在 hello**應用程式**下拉式清單和`https://localhost:44321/`在 hello**回覆 URL / 重新導向 URI**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="2650e-120">Select **Contoso B2C app** in hello **Applications** drop-down and `https://localhost:44321/` in hello **Reply URL / Redirect URI** drop-down.</span></span>

<span data-ttu-id="2650e-121">按一下 [立即執行] 。</span><span class="sxs-lookup"><span data-stu-id="2650e-121">Click **Run now**.</span></span> <span data-ttu-id="2650e-122">新的瀏覽器索引標籤隨即開啟，而且您可以透過 hello 註冊您的應用程式的取用者經驗。</span><span class="sxs-lookup"><span data-stu-id="2650e-122">A new browser tab opens, and you can run through hello consumer experience of signing up for your application.</span></span>

> [!NOTE]
> <span data-ttu-id="2650e-123">它會佔用 tooa 分鐘的時間，建立原則，並更新 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="2650e-123">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>