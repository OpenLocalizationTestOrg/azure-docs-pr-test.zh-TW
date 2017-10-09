## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="07922-101">準備 Azure 資源管理員要求的 tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="07922-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="07922-102">您必須驗證您在使用 hello 的資源執行的所有 hello 作業[Azure Resource Manager] [ lnk-authenticate-arm]與 Azure Active Directory (AD)。</span><span class="sxs-lookup"><span data-stu-id="07922-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="07922-103">hello 最簡單的方式 tooconfigure 這是 toouse PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="07922-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="07922-104">安裝 hello [Azure PowerShell cmdlet] [ lnk-powershell-install]繼續進行之前。</span><span class="sxs-lookup"><span data-stu-id="07922-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="07922-105">hello 下列步驟顯示如何使用 PowerShell 建立 AD 應用程式的密碼驗證設定 tooset。</span><span class="sxs-lookup"><span data-stu-id="07922-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="07922-106">您可以在標準 PowerShell 工作階段中執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="07922-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="07922-107">登入 tooyour Azure 訂用帳戶使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="07922-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="07922-108">如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07922-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="07922-109">使用下列命令 toolist hello Azure 訂用帳戶可讓您 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="07922-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="07922-110">使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toomanage IoT 中樞的 hello。</span><span class="sxs-lookup"><span data-stu-id="07922-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="07922-111">您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：</span><span class="sxs-lookup"><span data-stu-id="07922-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="07922-112">請記下您的 **TenantId** 和 **SubscriptionId**。</span><span class="sxs-lookup"><span data-stu-id="07922-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="07922-113">您稍後需要這些資訊。</span><span class="sxs-lookup"><span data-stu-id="07922-113">You need them later.</span></span>
3. <span data-ttu-id="07922-114">建立新的 Azure Active Directory 應用程式，使用下列命令、 取代 hello 預留位置 hello:</span><span class="sxs-lookup"><span data-stu-id="07922-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="07922-115">**{Display name}：**應用程式的顯示名稱，如 **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="07922-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="07922-116">**{首頁 URL}:** hello hello 首頁，應用程式的 URL，例如**http://mysampleapp/home**。</span><span class="sxs-lookup"><span data-stu-id="07922-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="07922-117">此 URL 不需要 toopoint tooa 實際的應用程式。</span><span class="sxs-lookup"><span data-stu-id="07922-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="07922-118">**{Application identifier}：**唯一識別碼，如 **http://mysampleapp**。</span><span class="sxs-lookup"><span data-stu-id="07922-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="07922-119">此 URL 不需要 toopoint tooa 實際的應用程式。</span><span class="sxs-lookup"><span data-stu-id="07922-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="07922-120">**{Password}:** tooauthenticate 搭配您的應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="07922-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="07922-121">請記下 hello **ApplicationId** hello 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="07922-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="07922-122">您稍後需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="07922-122">You need this later.</span></span>
5. <span data-ttu-id="07922-123">建立新的服務主體使用下列命令、 取代 hello **{MyApplicationId}**以 hello **ApplicationId** hello 上一個步驟：</span><span class="sxs-lookup"><span data-stu-id="07922-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="07922-124">設定角色指派，使用下列命令、 取代 hello **{MyApplicationId}**與您**ApplicationId**。</span><span class="sxs-lookup"><span data-stu-id="07922-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="07922-125">您現在已經完成建立 hello Azure AD 應用程式，可讓您 tooauthenticate 從您自訂的 C# 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07922-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="07922-126">您需要下列值稍後在本教學課程中的 hello:</span><span class="sxs-lookup"><span data-stu-id="07922-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="07922-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="07922-127">TenantId</span></span>
* <span data-ttu-id="07922-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="07922-128">SubscriptionId</span></span>
* <span data-ttu-id="07922-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="07922-129">ApplicationId</span></span>
* <span data-ttu-id="07922-130">密碼</span><span class="sxs-lookup"><span data-stu-id="07922-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
