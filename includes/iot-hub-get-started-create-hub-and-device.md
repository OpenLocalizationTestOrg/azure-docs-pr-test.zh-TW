## <a name="create-an-iot-hub"></a><span data-ttu-id="7a933-101">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="7a933-101">Create an IoT hub</span></span>

1. <span data-ttu-id="7a933-102">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [新增] > [物聯網] >  [IoT 中樞]。</span><span class="sxs-lookup"><span data-stu-id="7a933-102">In the [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![在 Azure 入口網站中建立 IoT 中樞](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="7a933-104">在 [IoT 中樞] 窗格中，輸入 IoT 中樞的下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="7a933-104">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

     <span data-ttu-id="7a933-105">**名稱**：輸入 IoT 中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="7a933-105">**Name**: Enter the name of your IoT hub.</span></span> <span data-ttu-id="7a933-106">如果您輸入的名稱有效，則會出現綠色核取記號。</span><span class="sxs-lookup"><span data-stu-id="7a933-106">If the name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="7a933-107">**定價與級別層**︰選取 [F1 - 免費層]。</span><span class="sxs-lookup"><span data-stu-id="7a933-107">**Pricing and scale tier**: Select the **F1 - Free** tier.</span></span> <span data-ttu-id="7a933-108">對此範例而言，此選項就已足夠。</span><span class="sxs-lookup"><span data-stu-id="7a933-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="7a933-109">如需詳細資訊，請參閱[定價與級別層](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="7a933-109">For more information, see the [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="7a933-110">**資源群組**：建立用以裝載 IoT 中樞的資源群組，或使用現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="7a933-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="7a933-111">如需詳細資訊，請參閱[使用資源群組管理您的 Azure 資源](../articles/azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7a933-111">For more information, see [Use resource groups to manage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="7a933-112">**位置**︰選取與您最接近的位置，以在其中建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7a933-112">**Location**: Select the closest location to you where the IoT hub is created.</span></span>

     <span data-ttu-id="7a933-113">**釘選到儀表板**：選取此選項可讓您從儀表板輕鬆地存取 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7a933-113">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

   ![輸入資訊以建立 IoT 中樞](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="7a933-115">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7a933-115">Click **Create**.</span></span> <span data-ttu-id="7a933-116">建立 IoT 中樞可能需要數分鐘。</span><span class="sxs-lookup"><span data-stu-id="7a933-116">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="7a933-117">您可以在 [通知] 窗格中看到進度。</span><span class="sxs-lookup"><span data-stu-id="7a933-117">You can see progress in the **Notifications** pane.</span></span>

   ![查看 IoT 中樞的進度通知](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="7a933-119">建立 IoT 中樞之後，請在儀表板上按一下它。</span><span class="sxs-lookup"><span data-stu-id="7a933-119">After your IoT hub is created, click it on the dashboard.</span></span> <span data-ttu-id="7a933-120">請記下**主機名稱**，然後按一下 [共用存取原則]。</span><span class="sxs-lookup"><span data-stu-id="7a933-120">Make a note of the **Hostname**, and then click **Shared access policies**.</span></span>

   ![取得 IoT 中樞的主機名稱](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="7a933-122">在 [共用存取原則] 窗格中，按一下 [iothubowner] 原則，然後複製並記下 IoT 中樞的**連接字串**。</span><span class="sxs-lookup"><span data-stu-id="7a933-122">In the **Shared access policies** pane, click the **iothubowner** policy, and then copy and make a note of the **Connection string** of your IoT hub.</span></span> <span data-ttu-id="7a933-123">如需詳細資訊，請參閱[控制 IoT 中樞的存取權](../articles/iot-hub/iot-hub-devguide-security.md)。</span><span class="sxs-lookup"><span data-stu-id="7a933-123">For more information, see [Control access to IoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="7a933-124">在此設定教學課程中，您不需要此 iothubowner 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7a933-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="7a933-125">不過，在您完成此設定之後，您可能需要在不同 IoT 案例的一些教學課程中使用到它。</span><span class="sxs-lookup"><span data-stu-id="7a933-125">However, you may need it for some of the tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![取得 IoT 中樞連接字串](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a><span data-ttu-id="7a933-127">在裝置的 IoT 中樞中註冊裝置</span><span class="sxs-lookup"><span data-stu-id="7a933-127">Register a device in the IoT hub for your device</span></span>

1. <span data-ttu-id="7a933-128">在 [Azure 入口網站](https://portal.azure.com/)中，開啟 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7a933-128">In the [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="7a933-129">按一下 [裝置總管]。</span><span class="sxs-lookup"><span data-stu-id="7a933-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="7a933-130">在 [裝置總管] 窗格中，按一下 [新增] 將裝置新增到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7a933-130">In the Device Explorer pane, click **Add** to add a device to your IoT hub.</span></span> <span data-ttu-id="7a933-131">然後執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="7a933-131">Then do the following:</span></span>

   <span data-ttu-id="7a933-132">**裝置識別碼**︰輸入新裝置的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7a933-132">**Device ID**: Enter the ID of the new device.</span></span> <span data-ttu-id="7a933-133">裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7a933-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="7a933-134">**驗證類型**：選取 [對稱金鑰]。</span><span class="sxs-lookup"><span data-stu-id="7a933-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="7a933-135">**自動產生金鑰**：選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7a933-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="7a933-136">**將裝置連線至 IoT 中樞**：按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="7a933-136">**Connect device to IoT Hub**: Click **Enable**.</span></span>

   ![在 IoT 中樞的裝置總管中新增裝置](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="7a933-138">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7a933-138">Click **Save**.</span></span>
5. <span data-ttu-id="7a933-139">建立裝置之後，請在 [裝置總管] 窗格中開啟裝置。</span><span class="sxs-lookup"><span data-stu-id="7a933-139">After the device is created, open the device in the **Device Explorer** pane.</span></span>
6. <span data-ttu-id="7a933-140">記下連接字串的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7a933-140">Make a note of the primary key of the connection string.</span></span>

   ![取得裝置連接字串](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
