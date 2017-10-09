## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="0149f-101">什麼是服務匯流排主題和訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="0149f-101">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="0149f-102">服務匯流排主題和訂用帳戶支援「發佈/訂閱」  訊息通訊模型。</span><span class="sxs-lookup"><span data-stu-id="0149f-102">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="0149f-103">使用主題和訂用帳戶時，分散式應用程式的元件彼此不直接通訊，相反的，他們會透過扮演中繼角色的主題來交換訊息。</span><span class="sxs-lookup"><span data-stu-id="0149f-103">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![主題概念](./media/howto-service-bus-topics/sb-topics-01.png)

<span data-ttu-id="0149f-105">有別於服務匯流排佇列，服務匯流排佇列中的每個訊息只會由單一取用者處理，主題和訂用帳戶採用發佈/訂用帳戶模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="0149f-105">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="0149f-106">就可以註冊多個訂用帳戶 tooa 主題。</span><span class="sxs-lookup"><span data-stu-id="0149f-106">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="0149f-107">當訊息傳送 tooa 主題時，它就可使用可用 tooeach 訂用帳戶 toohandle/處理序分開。</span><span class="sxs-lookup"><span data-stu-id="0149f-107">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="0149f-108">訂用帳戶 tooa 主題類似於虛擬佇列，可接收 toohello 主題傳送 hello 訊息複本。</span><span class="sxs-lookup"><span data-stu-id="0149f-108">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="0149f-109">（選擇性），您可以註冊以每個訂用帳戶為基礎，可讓您 toofilter 主題的篩選規則，或限制的主題訂用帳戶所收到的訊息 tooa 主題。</span><span class="sxs-lookup"><span data-stu-id="0149f-109">You can optionally register filter rules for a topic on a per-subscription basis, which enables you toofilter or restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="0149f-110">服務匯流排主題和訂閱 tooscale 可讓您和跨許多使用者和應用程式處理非常大量的訊息。</span><span class="sxs-lookup"><span data-stu-id="0149f-110">Service Bus topics and subscriptions enable you tooscale and process a very large number of messages across many users and applications.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="0149f-111">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="0149f-111">Create a namespace</span></span>
<span data-ttu-id="0149f-112">toobegin 使用服務匯流排主題和訂用帳戶在 Azure 中，您必須先建立*服務命名空間*。</span><span class="sxs-lookup"><span data-stu-id="0149f-112">toobegin using Service Bus topics and subscriptions in Azure, you must first create a *service namespace*.</span></span> <span data-ttu-id="0149f-113">命名空間提供範圍容器，可在應用程式內定址服務匯流排資源。</span><span class="sxs-lookup"><span data-stu-id="0149f-113">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="0149f-114">toocreate 命名空間：</span><span class="sxs-lookup"><span data-stu-id="0149f-114">toocreate a namespace:</span></span>

1. <span data-ttu-id="0149f-115">登入 toohello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="0149f-115">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="0149f-116">在 hello hello 入口網站的左側瀏覽窗格中按一下**新增**，然後按一下**企業整合**，然後按一下 **Service Bus**。</span><span class="sxs-lookup"><span data-stu-id="0149f-116">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="0149f-117">在 [hello**建立命名空間**] 對話方塊中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="0149f-117">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="0149f-118">hello 系統立即檢查 toosee hello 名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="0149f-118">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="0149f-119">提供讓確定 hello 命名空間名稱之後，選擇定價層 （Basic、 Standard 或 Premium） 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="0149f-119">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="0149f-120">在 hello**訂用帳戶**欄位中，選擇哪些 toocreate hello 命名空間中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0149f-120">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="0149f-121">在 hello**資源群組**欄位中，選擇現有的資源群組中的 hello 命名空間將 live、 或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="0149f-121">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="0149f-122">在**位置**，選擇 hello 國家或地區，應該在其中裝載您的命名空間。</span><span class="sxs-lookup"><span data-stu-id="0149f-122">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![建立命名空間][create-namespace]
8. <span data-ttu-id="0149f-124">按一下 hello**建立** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0149f-124">Click hello **Create** button.</span></span> <span data-ttu-id="0149f-125">hello 系統現在建立您的命名空間，並啟用它。</span><span class="sxs-lookup"><span data-stu-id="0149f-125">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="0149f-126">您可能需要幾分鐘的時間為 hello 系統佈建資源帳戶 toowait。</span><span class="sxs-lookup"><span data-stu-id="0149f-126">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-credentials"></a><span data-ttu-id="0149f-127">取得 hello 認證</span><span class="sxs-lookup"><span data-stu-id="0149f-127">Obtain hello credentials</span></span>
1. <span data-ttu-id="0149f-128">在 [hello] 清單中的命名空間，hello 新建立的命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="0149f-128">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="0149f-129">在 hello**服務匯流排命名空間**刀鋒視窗中，按一下 **共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="0149f-129">In hello **Service Bus namespace** blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="0149f-130">在 hello**共用存取原則**刀鋒視窗中，按一下  **RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="0149f-130">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="0149f-132">在 hello**原則： RootManageSharedAccessKey**刀鋒視窗中，按一下 hello 複製 按鈕旁邊太**連接字串對主索引鍵**，toocopy hello 連接字串 tooyour 剪貼簿供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="0149f-132">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span>
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


