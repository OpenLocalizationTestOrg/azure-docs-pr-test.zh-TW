1. <span data-ttu-id="f8430-101">登入 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="f8430-101">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="f8430-102">在入口網站的左方瀏覽窗格中，依序按一下 [新增]、[企業整合] 及 [轉送]。</span><span class="sxs-lookup"><span data-stu-id="f8430-102">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="f8430-103">在 [建立命名空間]  對話方塊中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="f8430-103">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="f8430-104">系統會立即檢查此名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="f8430-104">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="f8430-105">在 [訂用帳戶]  欄位中，選擇要在其中建立命名空間的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8430-105">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
5. <span data-ttu-id="f8430-106">在 **[資源群組](../articles/azure-resource-manager/resource-group-portal.md)** 欄位中，選擇將存留命名空間的現有資源群組，或是建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f8430-106">In the **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="f8430-107">在 [位置] 中，選擇應裝載您命名空間的國家或地區。</span><span class="sxs-lookup"><span data-stu-id="f8430-107">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![建立命名空間][create-namespace]
7. <span data-ttu-id="f8430-109">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f8430-109">Click **Create**.</span></span> <span data-ttu-id="f8430-110">此時系統會建立並啟用命名空間。</span><span class="sxs-lookup"><span data-stu-id="f8430-110">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="f8430-111">幾分鐘後，系統便會為您的帳戶佈建資源。</span><span class="sxs-lookup"><span data-stu-id="f8430-111">After a few minutes, the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="f8430-112">取得管理認證</span><span class="sxs-lookup"><span data-stu-id="f8430-112">Obtain the management credentials</span></span>
1. <span data-ttu-id="f8430-113">在命名空間清單中，按一下新建立的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="f8430-113">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="f8430-114">在命名空間刀鋒視窗中，按一下 [共用存取原則]。</span><span class="sxs-lookup"><span data-stu-id="f8430-114">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="f8430-115">在 [共用存取原則] 刀鋒視窗中，按一下 **RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="f8430-115">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="f8430-117">在 [原則: RootManageSharedAccessKey] 刀鋒視窗中，按一下 [連接字串 - 主要金鑰] 旁邊的複製按鈕，將連接字串複製到剪貼簿以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="f8430-117">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="f8430-118">將此值貼到記事本或一些其他暫存位置。</span><span class="sxs-lookup"><span data-stu-id="f8430-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="f8430-120">重複前一個步驟，複製 [主要金鑰] 的值並貼到暫存位置以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="f8430-120">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
