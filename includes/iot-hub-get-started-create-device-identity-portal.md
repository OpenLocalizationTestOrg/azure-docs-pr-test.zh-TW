## <a name="create-a-device-identity"></a><span data-ttu-id="d5de6-101">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="d5de6-101">Create a device identity</span></span>

<span data-ttu-id="d5de6-102">在本節中，您會使用 hello [Azure 入口網站][ lnk-azure-portal] toocreate IoT 中樞中的 hello 身分識別登錄中的裝置識別身分。</span><span class="sxs-lookup"><span data-stu-id="d5de6-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="d5de6-103">裝置無法連線 tooIoT 中樞，除非它有 hello 身分識別登錄中的項目。</span><span class="sxs-lookup"><span data-stu-id="d5de6-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="d5de6-104">如需詳細資訊，請參閱 hello hello 「 身分識別登錄 」 一節[IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="d5de6-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d5de6-105">hello**裝置總管**hello 入口網站可協助您產生唯一的裝置識別碼和您的裝置在連接 tooIoT 中樞時，可以使用 tooidentify 本身的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d5de6-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="d5de6-106">裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="d5de6-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="d5de6-107">請確定您已登入 toohello [Azure 入口網站][lnk-azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="d5de6-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="d5de6-108">在 hello Jumpbar，按一下 **所有資源**並尋找您的 IoT 中樞資源。</span><span class="sxs-lookup"><span data-stu-id="d5de6-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![瀏覽 tooyour Iot 中樞][img-find-iothub]

1. <span data-ttu-id="d5de6-110">開啟您的 IoT 中樞資源時，請按一下 hello**裝置總管**工具，，然後按一下**新增**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="d5de6-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="d5de6-111">提供 hello 名稱，新的裝置，例如**myDeviceId**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="d5de6-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![在入口網站中建立裝置識別][img-create-device]

   <span data-ttu-id="d5de6-113">這會為您的 IoT 中樞建立新的裝置識別。</span><span class="sxs-lookup"><span data-stu-id="d5de6-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="d5de6-114">在 hello**裝置總管**的裝置清單中，按一下新建立的 hello 裝置，並記下 hello**連接字串---主索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="d5de6-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![裝置連接字串][img-connection-string]

> [!NOTE]
> <span data-ttu-id="d5de6-116">hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d5de6-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="d5de6-117">它會儲存裝置識別碼和金鑰 toouse 安全性認證，以及您可以針對個別裝置使用 toodisable 存取啟用/停用旗標。</span><span class="sxs-lookup"><span data-stu-id="d5de6-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="d5de6-118">如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用特定應用程式存放區。</span><span class="sxs-lookup"><span data-stu-id="d5de6-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="d5de6-119">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="d5de6-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

