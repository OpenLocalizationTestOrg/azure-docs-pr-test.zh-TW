<span data-ttu-id="a0349-101">若要開始在 Azure 中使用服務匯流排佇列，您必須先使用 Azure 中的唯一名稱建立命名空間。</span><span class="sxs-lookup"><span data-stu-id="a0349-101">To begin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="a0349-102">命名空間提供範圍容器，可在應用程式內定址服務匯流排資源。</span><span class="sxs-lookup"><span data-stu-id="a0349-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="a0349-103">若要建立命名空間：</span><span class="sxs-lookup"><span data-stu-id="a0349-103">To create a namespace:</span></span>

1. <span data-ttu-id="a0349-104">登入 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="a0349-104">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a0349-105">在入口網站的左方瀏覽窗格中，依序按一下 [新增]，[企業整合] 及 [服務匯流排]。</span><span class="sxs-lookup"><span data-stu-id="a0349-105">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="a0349-106">在 [建立命名空間]  對話方塊中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="a0349-106">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="a0349-107">系統會立即檢查此名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="a0349-107">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="a0349-108">確定命名空間名稱可用之後，請選擇定價層 ([基本]、[標準] 或 [進階])。</span><span class="sxs-lookup"><span data-stu-id="a0349-108">After making sure the namespace name is available, choose the pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="a0349-109">在 [訂用帳戶]  欄位中，選擇要在其中建立命名空間的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0349-109">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
6. <span data-ttu-id="a0349-110">在 [資源群組]  欄位中，選擇將存留命名空間的現有資源群組，或是建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a0349-110">In the **Resource group** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="a0349-111">在 [位置] 中，選擇應裝載您命名空間的國家或地區。</span><span class="sxs-lookup"><span data-stu-id="a0349-111">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![建立命名空間][create-namespace]
8. <span data-ttu-id="a0349-113">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a0349-113">Click **Create**.</span></span> <span data-ttu-id="a0349-114">此時系統會建立並啟用命名空間。</span><span class="sxs-lookup"><span data-stu-id="a0349-114">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="a0349-115">系統為帳戶提供資源時，您可能需要等幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="a0349-115">You might have to wait several minutes as the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="a0349-116">取得管理認證</span><span class="sxs-lookup"><span data-stu-id="a0349-116">Obtain the management credentials</span></span>

1. <span data-ttu-id="a0349-117">在命名空間清單中，按一下新建立的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="a0349-117">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="a0349-118">在命名空間刀鋒視窗中，按一下 [共用存取原則]。</span><span class="sxs-lookup"><span data-stu-id="a0349-118">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="a0349-119">在 [共用存取原則] 刀鋒視窗中，按一下 **RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="a0349-119">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="a0349-121">在 [原則: RootManageSharedAccessKey] 刀鋒視窗中，按一下 [連接字串 - 主要金鑰] 旁邊的複製按鈕，將連接字串複製到剪貼簿以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="a0349-121">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="a0349-122">將此值貼到記事本或一些其他暫存位置。</span><span class="sxs-lookup"><span data-stu-id="a0349-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="a0349-124">重複前一個步驟，複製 [主要金鑰] 的值並貼到暫存位置以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="a0349-124">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
