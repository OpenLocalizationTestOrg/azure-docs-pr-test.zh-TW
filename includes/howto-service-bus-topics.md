## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="019dd-101">什麼是服務匯流排主題和訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="019dd-101">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="019dd-102">服務匯流排主題和訂用帳戶支援「發佈/訂閱」  訊息通訊模型。</span><span class="sxs-lookup"><span data-stu-id="019dd-102">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="019dd-103">使用主題和訂用帳戶時，分散式應用程式的元件彼此不直接通訊，相反的，他們會透過扮演中繼角色的主題來交換訊息。</span><span class="sxs-lookup"><span data-stu-id="019dd-103">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![主題概念](./media/howto-service-bus-topics/sb-topics-01.png)

<span data-ttu-id="019dd-105">有別於服務匯流排佇列，服務匯流排佇列中的每個訊息只會由單一取用者處理，主題和訂用帳戶採用發佈/訂用帳戶模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="019dd-105">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="019dd-106">一個主題可以登錄多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="019dd-106">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="019dd-107">當訊息傳送至主題時，每個訂用帳戶都可取得訊息來個別處理。</span><span class="sxs-lookup"><span data-stu-id="019dd-107">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="019dd-108">某個主題的訂用帳戶，類似可接收已傳送到主題之訊息複本的虛擬佇列。</span><span class="sxs-lookup"><span data-stu-id="019dd-108">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="019dd-109">您可以選擇為個別訂用帳戶針對主題登錄篩選規則，以篩選或限制主題的哪些訊息可以由哪些主題訂用帳戶接收。</span><span class="sxs-lookup"><span data-stu-id="019dd-109">You can optionally register filter rules for a topic on a per-subscription basis, which enables you to filter or restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="019dd-110">服務匯流排主題和訂用帳戶可讓您調整並處理許多使用者和應用程式上的大量訊息。</span><span class="sxs-lookup"><span data-stu-id="019dd-110">Service Bus topics and subscriptions enable you to scale and process a very large number of messages across many users and applications.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="019dd-111">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="019dd-111">Create a namespace</span></span>
<span data-ttu-id="019dd-112">若要開始在 Azure 中使用服務匯流排主題和訂用帳戶，首先必須建立「服務命名空間」 。</span><span class="sxs-lookup"><span data-stu-id="019dd-112">To begin using Service Bus topics and subscriptions in Azure, you must first create a *service namespace*.</span></span> <span data-ttu-id="019dd-113">命名空間提供範圍容器，可在應用程式內定址服務匯流排資源。</span><span class="sxs-lookup"><span data-stu-id="019dd-113">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="019dd-114">若要建立命名空間：</span><span class="sxs-lookup"><span data-stu-id="019dd-114">To create a namespace:</span></span>

1. <span data-ttu-id="019dd-115">登入 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="019dd-115">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="019dd-116">在入口網站的左方瀏覽窗格中，依序按一下 [新增]，[企業整合] 及 [服務匯流排]。</span><span class="sxs-lookup"><span data-stu-id="019dd-116">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="019dd-117">在 [建立命名空間]  對話方塊中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="019dd-117">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="019dd-118">系統會立即檢查此名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="019dd-118">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="019dd-119">確定命名空間名稱可用之後，請選擇定價層 ([基本]、[標準] 或 [進階])。</span><span class="sxs-lookup"><span data-stu-id="019dd-119">After making sure the namespace name is available, choose the pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="019dd-120">在 [訂用帳戶]  欄位中，選擇要在其中建立命名空間的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="019dd-120">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
6. <span data-ttu-id="019dd-121">在 [資源群組]  欄位中，選擇將存留命名空間的現有資源群組，或是建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="019dd-121">In the **Resource group** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="019dd-122">在 [位置] 中，選擇應裝載您命名空間的國家或地區。</span><span class="sxs-lookup"><span data-stu-id="019dd-122">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![建立命名空間][create-namespace]
8. <span data-ttu-id="019dd-124">按一下 [ **建立** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="019dd-124">Click the **Create** button.</span></span> <span data-ttu-id="019dd-125">此時系統會建立並啟用命名空間。</span><span class="sxs-lookup"><span data-stu-id="019dd-125">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="019dd-126">系統為帳戶提供資源時，您可能需要等幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="019dd-126">You might have to wait several minutes as the system provisions resources for your account.</span></span>

### <a name="obtain-the-credentials"></a><span data-ttu-id="019dd-127">取得認證</span><span class="sxs-lookup"><span data-stu-id="019dd-127">Obtain the credentials</span></span>
1. <span data-ttu-id="019dd-128">在命名空間清單中，按一下新建立的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="019dd-128">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="019dd-129">在 [服務匯流排命名空間] 刀鋒視窗中，按一下 [共用存取原則]。</span><span class="sxs-lookup"><span data-stu-id="019dd-129">In the **Service Bus namespace** blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="019dd-130">在 [共用存取原則] 刀鋒視窗中，按一下 **RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="019dd-130">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="019dd-132">在 [原則: RootManageSharedAccessKey] 刀鋒視窗中，按一下 [連接字串 - 主要金鑰] 旁邊的複製按鈕，將連接字串複製到剪貼簿以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="019dd-132">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span>
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


