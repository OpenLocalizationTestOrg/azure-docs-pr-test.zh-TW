[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

<span data-ttu-id="f0d1d-101">tooregister 行動或原生應用程式，使用 hello 設定 hello 資料表中指定。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-101">tooregister your mobile or native application, use hello settings specified in hello table.</span></span>

![新行動或原生應用程式的範例註冊設定](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| <span data-ttu-id="f0d1d-103">設定</span><span class="sxs-lookup"><span data-stu-id="f0d1d-103">Setting</span></span>      | <span data-ttu-id="f0d1d-104">範例值</span><span class="sxs-lookup"><span data-stu-id="f0d1d-104">Sample value</span></span>  | <span data-ttu-id="f0d1d-105">說明</span><span class="sxs-lookup"><span data-stu-id="f0d1d-105">Description</span></span>                                        |
| ------------ | ------- | -------------------------------------------------- |
| <span data-ttu-id="f0d1d-106">**名稱**</span><span class="sxs-lookup"><span data-stu-id="f0d1d-106">**Name**</span></span> | <span data-ttu-id="f0d1d-107">Contoso B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="f0d1d-107">Contoso B2C app</span></span> | <span data-ttu-id="f0d1d-108">輸入**名稱**描述應用程式 tooconsumers hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-108">Enter a **Name** for hello application that describes your application tooconsumers.</span></span> |
| <span data-ttu-id="f0d1d-109">**原生用戶端**</span><span class="sxs-lookup"><span data-stu-id="f0d1d-109">**Native client**</span></span> | <span data-ttu-id="f0d1d-110">是</span><span class="sxs-lookup"><span data-stu-id="f0d1d-110">Yes</span></span> | <span data-ttu-id="f0d1d-111">針對行動或原生應用程式選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-111">Select **Yes** for a mobile or native application.</span></span> |
| <span data-ttu-id="f0d1d-112">**自訂重新導向 URI**</span><span class="sxs-lookup"><span data-stu-id="f0d1d-112">**Custom Redirect URI**</span></span> | `com.onmicrosoft.contoso.appname://redirect/path` | <span data-ttu-id="f0d1d-113">輸入具有自訂配置的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-113">Enter a redirect URI with a custom scheme.</span></span> <span data-ttu-id="f0d1d-114">務必選擇[良好的重新導向 URI](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri)，但不包含特殊字元 (例如底線)。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-114">Make sure you choose a [good redirect URI](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) and do not include special characters such as underscores.</span></span> |

<span data-ttu-id="f0d1d-115">按一下**建立**tooregister 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-115">Click **Create** tooregister your application.</span></span>

<span data-ttu-id="f0d1d-116">您註冊新的應用程式會顯示 hello hello B2C 租用戶的應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-116">Your newly registered application is displayed in hello applications list for hello B2C tenant.</span></span> <span data-ttu-id="f0d1d-117">Hello 清單中選取行動或原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-117">Select your mobile or native app from hello list.</span></span> <span data-ttu-id="f0d1d-118">hello 應用程式的 [屬性] 窗格會顯示。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-118">hello application's property pane is displayed.</span></span>

![應用程式屬性](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

<span data-ttu-id="f0d1d-120">請記下 hello 全域唯一**應用程式用戶端識別碼**。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-120">Make note of hello globally unique **Application Client ID**.</span></span> <span data-ttu-id="f0d1d-121">您在您的應用程式程式碼中使用識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-121">You use hello ID in your application's code.</span></span>

<span data-ttu-id="f0d1d-122">如果您的原生應用程式呼叫 Azure AD B2C 所保護的 Web API，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f0d1d-122">If your native application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="f0d1d-123">建立應用程式密碼將 toohello**金鑰**刀鋒視窗，然後按一下 hello**產生金鑰** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-123">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="f0d1d-124">請記下 hello**應用程式金鑰**值。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-124">Make note of hello **App key** value.</span></span> <span data-ttu-id="f0d1d-125">您可以使用 hello 值做為您的應用程式程式碼中的 hello 應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-125">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="f0d1d-126">按一下 [API 存取][新增] 並選取您的 Web API 和範圍 (權限)。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-126">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="f0d1d-127">**應用程式密鑰** 是重要的安全性認證，應該適當地加以保護。</span><span class="sxs-lookup"><span data-stu-id="f0d1d-127">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 
