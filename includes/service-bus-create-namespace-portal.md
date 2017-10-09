<span data-ttu-id="c97d2-101">使用服務匯流排 toobegin 排入佇列，在 Azure 中，您必須先使用 Azure 中是唯一的名稱建立命名空間。</span><span class="sxs-lookup"><span data-stu-id="c97d2-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="c97d2-102">命名空間提供範圍容器，可在應用程式內定址服務匯流排資源。</span><span class="sxs-lookup"><span data-stu-id="c97d2-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="c97d2-103">toocreate 命名空間：</span><span class="sxs-lookup"><span data-stu-id="c97d2-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="c97d2-104">登入 toohello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="c97d2-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="c97d2-105">在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，然後按一下**企業整合**，然後按一下 **Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="c97d2-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="c97d2-106">在 [hello**建立命名空間**] 對話方塊中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="c97d2-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="c97d2-107">hello 系統立即檢查 toosee hello 名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="c97d2-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="c97d2-108">提供讓確定 hello 命名空間名稱之後，選擇定價層 （Basic、 Standard 或 Premium） 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="c97d2-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="c97d2-109">在 hello**訂用帳戶**欄位中，選擇哪些 toocreate hello 命名空間中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c97d2-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="c97d2-110">在 hello**資源群組**欄位中，選擇現有的資源群組中的 hello 命名空間將 live、 或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="c97d2-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="c97d2-111">在**位置**，選擇 hello 國家或地區，應該在其中裝載您的命名空間。</span><span class="sxs-lookup"><span data-stu-id="c97d2-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![建立命名空間][create-namespace]
8. <span data-ttu-id="c97d2-113">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c97d2-113">Click **Create**.</span></span> <span data-ttu-id="c97d2-114">hello 系統現在建立您的命名空間，並啟用它。</span><span class="sxs-lookup"><span data-stu-id="c97d2-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="c97d2-115">您可能需要幾分鐘的時間為 hello 系統佈建資源帳戶 toowait。</span><span class="sxs-lookup"><span data-stu-id="c97d2-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="c97d2-116">取得 hello 管理認證</span><span class="sxs-lookup"><span data-stu-id="c97d2-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="c97d2-117">在 [hello] 清單中的命名空間，hello 新建立的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="c97d2-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="c97d2-118">在 hello 命名空間刀鋒視窗中，按一下 **共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="c97d2-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="c97d2-119">在 hello**共用存取原則**刀鋒視窗中，按一下  **RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="c97d2-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="c97d2-121">在 hello**原則： RootManageSharedAccessKey**刀鋒視窗中，按一下 hello 複製 按鈕旁邊太**連接字串對主索引鍵**，toocopy hello 連接字串 tooyour 剪貼簿供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="c97d2-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="c97d2-122">將此值貼到記事本或一些其他暫存位置。</span><span class="sxs-lookup"><span data-stu-id="c97d2-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="c97d2-124">重複的 hello 先前步驟中，複製並貼上的 hello 值**主索引鍵**tooa 暫存位置，供日後使用。</span><span class="sxs-lookup"><span data-stu-id="c97d2-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
