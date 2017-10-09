## <a name="create-an-iot-hub"></a><span data-ttu-id="75f2f-101">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="75f2f-101">Create an IoT hub</span></span>

1. <span data-ttu-id="75f2f-102">在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **物聯網** > **IoT 中樞**。</span><span class="sxs-lookup"><span data-stu-id="75f2f-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![在 hello Azure 入口網站中建立 IoT 中樞](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="75f2f-104">在 [hello **IoT 中樞**] 窗格中，輸入下列資訊 IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="75f2f-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="75f2f-105">**名稱**： 輸入 hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="75f2f-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="75f2f-106">如果您所輸入的 hello 名稱是有效的則會出現綠色的核取記號。</span><span class="sxs-lookup"><span data-stu-id="75f2f-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="75f2f-107">**定價與級別層**： 選取 hello **F1-免費**層。</span><span class="sxs-lookup"><span data-stu-id="75f2f-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="75f2f-108">對此範例而言，此選項就已足夠。</span><span class="sxs-lookup"><span data-stu-id="75f2f-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="75f2f-109">如需詳細資訊，請參閱 hello[定價與級別層](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="75f2f-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="75f2f-110">**資源群組**： 建立資源群組 toohost hello IoT 中樞或使用現有的我的最愛。</span><span class="sxs-lookup"><span data-stu-id="75f2f-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="75f2f-111">如需詳細資訊，請參閱[使用資源群組 toomanage 您的 Azure 資源](../articles/azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="75f2f-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="75f2f-112">**位置**： 選取 hello 最接近 hello IoT 中樞建立所在的位置 tooyou。</span><span class="sxs-lookup"><span data-stu-id="75f2f-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="75f2f-113">**Pin toodashboard**： 選取此選項，讓您輕鬆存取 tooyour IoT 中樞從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="75f2f-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![輸入資訊 toocreate IoT 中樞](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="75f2f-115">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="75f2f-115">Click **Create**.</span></span> <span data-ttu-id="75f2f-116">IoT 中樞可能需要幾分鐘的時間 toocreate。</span><span class="sxs-lookup"><span data-stu-id="75f2f-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="75f2f-117">您可以看到進度 hello**通知**窗格。</span><span class="sxs-lookup"><span data-stu-id="75f2f-117">You can see progress in hello **Notifications** pane.</span></span>

   ![查看 IoT 中樞的進度通知](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="75f2f-119">建立 IoT 中樞之後，請按一下該 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="75f2f-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="75f2f-120">請記下 hello **Hostname**，然後按一下**共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="75f2f-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![取得 hello 的 IoT 中樞的主機名稱](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="75f2f-122">在 [hello**共用存取原則**] 窗格中，按一下 hello **iothubowner**原則，然後複製並記 hello**連接字串**的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="75f2f-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="75f2f-123">如需詳細資訊，請參閱[控制存取 tooIoT 中樞](../articles/iot-hub/iot-hub-devguide-security.md)。</span><span class="sxs-lookup"><span data-stu-id="75f2f-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="75f2f-124">在此設定教學課程中，您不需要此 iothubowner 連接字串。</span><span class="sxs-lookup"><span data-stu-id="75f2f-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="75f2f-125">不過，您可能需要它 hello 不同 IoT 案例的教學課程的某些後完成此安裝。</span><span class="sxs-lookup"><span data-stu-id="75f2f-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![取得 IoT 中樞連接字串](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="75f2f-127">在您的裝置 hello IoT 中樞註冊裝置</span><span class="sxs-lookup"><span data-stu-id="75f2f-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="75f2f-128">在 hello [Azure 入口網站](https://portal.azure.com/)，開啟您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="75f2f-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="75f2f-129">按一下 [裝置總管]。</span><span class="sxs-lookup"><span data-stu-id="75f2f-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="75f2f-130">在 hello 裝置總管 窗格中，按一下 **新增**tooadd 裝置 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="75f2f-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="75f2f-131">然後 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="75f2f-131">Then do hello following:</span></span>

   <span data-ttu-id="75f2f-132">**裝置識別碼**： 輸入 hello 識別碼 hello 新增裝置。</span><span class="sxs-lookup"><span data-stu-id="75f2f-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="75f2f-133">裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="75f2f-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="75f2f-134">**驗證類型**：選取 [對稱金鑰]。</span><span class="sxs-lookup"><span data-stu-id="75f2f-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="75f2f-135">**自動產生金鑰**：選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="75f2f-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="75f2f-136">**連接裝置 tooIoT 中樞**： 按一下**啟用**。</span><span class="sxs-lookup"><span data-stu-id="75f2f-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![在 [hello 的 IoT 中樞的裝置總管] 中新增裝置](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="75f2f-138">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="75f2f-138">Click **Save**.</span></span>
5. <span data-ttu-id="75f2f-139">建立 hello 裝置之後，開啟 hello 裝置在 hello**裝置總管**窗格。</span><span class="sxs-lookup"><span data-stu-id="75f2f-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="75f2f-140">記下 hello 連接字串 hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="75f2f-140">Make a note of hello primary key of hello connection string.</span></span>

   ![取得 hello 裝置連接字串](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
