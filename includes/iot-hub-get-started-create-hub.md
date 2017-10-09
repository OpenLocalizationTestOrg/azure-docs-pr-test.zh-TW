## <a name="create-an-iot-hub"></a><span data-ttu-id="a7d7a-101">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="a7d7a-101">Create an IoT hub</span></span>
<span data-ttu-id="a7d7a-102">建立以您模擬的裝置應用程式 tooconnect IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="a7d7a-103">hello 下列步驟說明如何 toocomplete 此工作所使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="a7d7a-104">登入 toohello [Azure 入口網站][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="a7d7a-105">在 hello Jumpbar，按一下 **新增** > **物聯網** > **IoT 中樞**。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Azure 入口網站 Jumpbar][1]
1. <span data-ttu-id="a7d7a-107">在 hello **IoT 中樞**刀鋒視窗中，選擇您的 IoT 中樞的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![IoT 中樞刀鋒視窗][2]
   
   1. <span data-ttu-id="a7d7a-109">在 hello**名稱**方塊中，輸入您的 IoT 中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="a7d7a-110">如果 hello**名稱**有效且可用，綠色的核取記號會出現在 hello**名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="a7d7a-111">選取一個[定價和調整層][lnk-pricing]。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="a7d7a-112">本教學課程不需要特定層。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="a7d7a-113">此教學課程中，使用 hello 免費 F1 層。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="a7d7a-114">在 [資源群組]中，建立資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="a7d7a-115">如需詳細資訊，請參閱[資源使用您的 Azure 資源群組 toomanage][lnk-resource-groups]。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="a7d7a-116">在**位置**，選取 hello 位置 toohost IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="a7d7a-117">在本教學課程中，選擇最接近您的位置。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="a7d7a-118">選擇好 IoT 中樞組態選項時，按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="a7d7a-119">它可能需要幾分鐘，讓 Azure toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="a7d7a-120">toocheck hello 狀態，您可以監視 hello 開始面板或 hello 通知面板中的 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![新增 IoT 中樞狀態][3]
1. <span data-ttu-id="a7d7a-122">已成功建立 hello IoT 中樞，按一下您的 IoT 中樞 hello 新的 IoT 中樞的 hello Azure 入口網站 tooopen hello 刀鋒視窗中的 hello 新磚。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="a7d7a-123">請記下 hello **Hostname**，然後按一下**共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![新增 IoT 中樞刀鋒視窗][4]
1. <span data-ttu-id="a7d7a-125">在 hello**共用存取原則**刀鋒視窗中，按一下 hello **iothubowner**原則，然後複製並記下的 hello IoT 中樞連接字串中 hello **iothubowner**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="a7d7a-126">如需詳細資訊，請參閱[存取控制][ lnk-access-control]在 hello 《 IoT 中樞開發人員指南 》。</span><span class="sxs-lookup"><span data-stu-id="a7d7a-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
    ![共用存取原則刀鋒視窗][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
