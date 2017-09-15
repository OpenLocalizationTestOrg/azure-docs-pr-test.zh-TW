## <a name="create-a-device-identity"></a><span data-ttu-id="8f969-101">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="8f969-101">Create a device identity</span></span>

<span data-ttu-id="8f969-102">在本節中，您會使用 [Azure 入口網站][lnk-azure-portal]在 IoT 中樞的身分識別登錄中建立裝置識別。</span><span class="sxs-lookup"><span data-stu-id="8f969-102">In this section, you use the [Azure portal][lnk-azure-portal] to create a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="8f969-103">裝置無法連線到 IoT 中樞，除非它在身分識別登錄中具有項目。</span><span class="sxs-lookup"><span data-stu-id="8f969-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="8f969-104">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]的＜身分識別登錄＞一節。</span><span class="sxs-lookup"><span data-stu-id="8f969-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="8f969-105">入口網站中的 [Device Explorer] 會協助您產生唯一的裝置識別碼及金鑰，當裝置連線至 IoT 中樞時，可以用來識別裝置本身。</span><span class="sxs-lookup"><span data-stu-id="8f969-105">The **Device Explorer** in the portal helps you generate a unique device ID and key that your device can use to identify itself when it connects to IoT Hub.</span></span> <span data-ttu-id="8f969-106">裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8f969-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="8f969-107">確定您已登入 [Azure 入口網站][lnk-azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="8f969-107">Make sure you are signed in to the [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="8f969-108">在 Jumpbar 中，按一下 [所有資源] 並尋找您的 IoT 中樞資源。</span><span class="sxs-lookup"><span data-stu-id="8f969-108">In the Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![瀏覽至您的 IoT 中樞][img-find-iothub]

1. <span data-ttu-id="8f969-110">當您的 IoT 中樞資源開啟時，按一下 [Device Explorer] 工具，然後按一下頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8f969-110">When your IoT hub resource is opened, click the **Device Explorer** tool, and then click **Add** at the top.</span></span> <span data-ttu-id="8f969-111">提供新裝置的名稱 (例如 **myDeviceId**)，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="8f969-111">Provide the name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![在入口網站中建立裝置識別][img-create-device]

   <span data-ttu-id="8f969-113">這會為您的 IoT 中樞建立新的裝置識別。</span><span class="sxs-lookup"><span data-stu-id="8f969-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="8f969-114">在 [Device Explorer] 的裝置清單中，按一下新建立的裝置並記下 [連接字串---主索引鍵]。</span><span class="sxs-lookup"><span data-stu-id="8f969-114">In the **Device Explorer**'s device list, click the newly created device and make note of the **Connection string---primary key**.</span></span> 

    ![裝置連接字串][img-connection-string]

> [!NOTE]
> <span data-ttu-id="8f969-116">IoT 中樞身分識別登錄只會儲存裝置身分識別，以啟用對 IoT 中樞的安全存取。</span><span class="sxs-lookup"><span data-stu-id="8f969-116">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="8f969-117">它會儲存裝置識別碼和金鑰來作為安全性認證，以及啟用或停用旗標，讓您用來停用個別裝置的存取。</span><span class="sxs-lookup"><span data-stu-id="8f969-117">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="8f969-118">如果您的應用程式需要儲存其他裝置特定的中繼資料，它應該使用應用程式專用的存放區。</span><span class="sxs-lookup"><span data-stu-id="8f969-118">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="8f969-119">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="8f969-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

