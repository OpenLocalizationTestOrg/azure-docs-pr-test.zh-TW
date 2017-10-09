## <a name="create-a-device-identity"></a>建立裝置識別

在本節中，您會使用 hello [Azure 入口網站][ lnk-azure-portal] toocreate IoT 中樞中的 hello 身分識別登錄中的裝置識別身分。 裝置無法連線 tooIoT 中樞，除非它有 hello 身分識別登錄中的項目。 如需詳細資訊，請參閱 hello hello 「 身分識別登錄 」 一節[IoT 中樞開發人員指南][lnk-devguide-identity]。 hello**裝置總管**hello 入口網站可協助您產生唯一的裝置識別碼和您的裝置在連接 tooIoT 中樞時，可以使用 tooidentify 本身的索引鍵。 裝置識別碼會區分大小寫。

1. 請確定您已登入 toohello [Azure 入口網站][lnk-azure-portal]。

1. 在 hello Jumpbar，按一下 **所有資源**並尋找您的 IoT 中樞資源。

    ![瀏覽 tooyour Iot 中樞][img-find-iothub]

1. 開啟您的 IoT 中樞資源時，請按一下 hello**裝置總管**工具，，然後按一下**新增**hello 頂端。 提供 hello 名稱，新的裝置，例如**myDeviceId**，然後按一下**儲存**。

    ![在入口網站中建立裝置識別][img-create-device]

   這會為您的 IoT 中樞建立新的裝置識別。

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. 在 hello**裝置總管**的裝置清單中，按一下新建立的 hello 裝置，並記下 hello**連接字串---主索引鍵**。 

    ![裝置連接字串][img-connection-string]

> [!NOTE]
> hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。 它會儲存裝置識別碼和金鑰 toouse 安全性認證，以及您可以針對個別裝置使用 toodisable 存取啟用/停用旗標。 如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用特定應用程式存放區。 如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

