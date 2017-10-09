1. <span data-ttu-id="4a9b0-101">登入 toohello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="4a9b0-102">在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，然後按一下**企業整合**，然後按一下**轉送**。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="4a9b0-103">在 [hello**建立命名空間**] 對話方塊中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="4a9b0-104">hello 系統立即檢查 toosee hello 名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="4a9b0-105">在 hello**訂用帳戶**欄位中，選擇哪些 toocreate hello 命名空間中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="4a9b0-106">在 hello **[資源群組](../articles/azure-resource-manager/resource-group-portal.md)**欄位中，選擇現有的資源群組中的 hello 命名空間將 live、 或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="4a9b0-107">在**位置**，選擇 hello 國家或地區，應該在其中裝載您的命名空間。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![建立命名空間][create-namespace]
7. <span data-ttu-id="4a9b0-109">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-109">Click **Create**.</span></span> <span data-ttu-id="4a9b0-110">hello 系統現在建立您的命名空間，並啟用它。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="4a9b0-111">請稍候幾分鐘，為您的帳戶 hello 系統提供的資源。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="4a9b0-112">取得 hello 管理認證</span><span class="sxs-lookup"><span data-stu-id="4a9b0-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="4a9b0-113">在 [hello] 清單中的命名空間，hello 新建立的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="4a9b0-114">在 hello 命名空間刀鋒視窗中，按一下 **共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="4a9b0-115">在 hello**共用存取原則**刀鋒視窗中，按一下  **RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="4a9b0-117">在 hello**原則： RootManageSharedAccessKey**刀鋒視窗中，按一下 hello 複製 按鈕旁邊太**連接字串對主索引鍵**，toocopy hello 連接字串 tooyour 剪貼簿供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="4a9b0-118">將此值貼到記事本或一些其他暫存位置。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="4a9b0-120">重複的 hello 先前步驟中，複製並貼上的 hello 值**主索引鍵**tooa 暫存位置，供日後使用。</span><span class="sxs-lookup"><span data-stu-id="4a9b0-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
