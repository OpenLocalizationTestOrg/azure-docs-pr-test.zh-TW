[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

<span data-ttu-id="aa914-101">若要註冊您的行動或原生應用程式，請使用資料表中所指定的設定。</span><span class="sxs-lookup"><span data-stu-id="aa914-101">To register your mobile or native application, use the settings specified in the table.</span></span>

![新行動或原生應用程式的範例註冊設定](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| <span data-ttu-id="aa914-103">設定</span><span class="sxs-lookup"><span data-stu-id="aa914-103">Setting</span></span>      | <span data-ttu-id="aa914-104">範例值</span><span class="sxs-lookup"><span data-stu-id="aa914-104">Sample value</span></span>  | <span data-ttu-id="aa914-105">說明</span><span class="sxs-lookup"><span data-stu-id="aa914-105">Description</span></span>                                        |
| ------------ | ------- | -------------------------------------------------- |
| <span data-ttu-id="aa914-106">**名稱**</span><span class="sxs-lookup"><span data-stu-id="aa914-106">**Name**</span></span> | <span data-ttu-id="aa914-107">Contoso B2C 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa914-107">Contoso B2C app</span></span> | <span data-ttu-id="aa914-108">輸入應用程式的 [名稱]，此名稱可為取用者說明您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa914-108">Enter a **Name** for the application that describes your application to consumers.</span></span> |
| <span data-ttu-id="aa914-109">**原生用戶端**</span><span class="sxs-lookup"><span data-stu-id="aa914-109">**Native client**</span></span> | <span data-ttu-id="aa914-110">是</span><span class="sxs-lookup"><span data-stu-id="aa914-110">Yes</span></span> | <span data-ttu-id="aa914-111">針對行動或原生應用程式選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="aa914-111">Select **Yes** for a mobile or native application.</span></span> |
| <span data-ttu-id="aa914-112">**自訂重新導向 URI**</span><span class="sxs-lookup"><span data-stu-id="aa914-112">**Custom Redirect URI**</span></span> | `com.onmicrosoft.contoso.appname://redirect/path` | <span data-ttu-id="aa914-113">輸入具有自訂配置的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="aa914-113">Enter a redirect URI with a custom scheme.</span></span> <span data-ttu-id="aa914-114">務必選擇[良好的重新導向 URI](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri)，但不包含特殊字元 (例如底線)。</span><span class="sxs-lookup"><span data-stu-id="aa914-114">Make sure you choose a [good redirect URI](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) and do not include special characters such as underscores.</span></span> |

<span data-ttu-id="aa914-115">按一下 [建立]  以註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa914-115">Click **Create** to register your application.</span></span>

<span data-ttu-id="aa914-116">新註冊的應用程式會顯示在 B2C 租用戶的應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="aa914-116">Your newly registered application is displayed in the applications list for the B2C tenant.</span></span> <span data-ttu-id="aa914-117">從清單中選取行動或原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa914-117">Select your mobile or native app from the list.</span></span> <span data-ttu-id="aa914-118">應用程式的 [屬性] 窗格隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="aa914-118">The application's property pane is displayed.</span></span>

![應用程式屬性](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

<span data-ttu-id="aa914-120">請記下全域唯一的 [應用程式用戶端識別碼]。</span><span class="sxs-lookup"><span data-stu-id="aa914-120">Make note of the globally unique **Application Client ID**.</span></span> <span data-ttu-id="aa914-121">您可在您的應用程式程式碼中使用此識別碼。</span><span class="sxs-lookup"><span data-stu-id="aa914-121">You use the ID in your application's code.</span></span>

<span data-ttu-id="aa914-122">如果您的原生應用程式呼叫 Azure AD B2C 所保護的 Web API，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="aa914-122">If your native application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="aa914-123">前往 [金鑰] 刀鋒視窗，然後按一下 [產生金鑰] 按鈕，以建立應用程式祕密。</span><span class="sxs-lookup"><span data-stu-id="aa914-123">Create an application secret by going to the **Keys** blade and clicking the **Generate Key** button.</span></span> <span data-ttu-id="aa914-124">請記下 [應用程式金鑰] 值。</span><span class="sxs-lookup"><span data-stu-id="aa914-124">Make note of the **App key** value.</span></span> <span data-ttu-id="aa914-125">您可以使用此值，作為應用程式程式碼中的應用程式祕密。</span><span class="sxs-lookup"><span data-stu-id="aa914-125">You use the value as the application secret in your application's code.</span></span>
   2. <span data-ttu-id="aa914-126">按一下 [API 存取][新增] 並選取您的 Web API 和範圍 (權限)。</span><span class="sxs-lookup"><span data-stu-id="aa914-126">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="aa914-127">**應用程式密鑰** 是重要的安全性認證，應該適當地加以保護。</span><span class="sxs-lookup"><span data-stu-id="aa914-127">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 
