## <a name="create-an-iot-hub"></a>建立 IoT 中樞
建立以您模擬的裝置應用程式 tooconnect IoT 中樞。 hello 下列步驟說明如何 toocomplete 此工作所使用 hello Azure 入口網站。

1. 登入 toohello [Azure 入口網站][lnk-portal]。
1. 在 hello Jumpbar，按一下 **新增** > **物聯網** > **IoT 中樞**。
   
    ![Azure 入口網站 Jumpbar][1]
1. 在 hello **IoT 中樞**刀鋒視窗中，選擇您的 IoT 中樞的 hello 組態。
   
    ![IoT 中樞刀鋒視窗][2]
   
   1. 在 hello**名稱**方塊中，輸入您的 IoT 中樞的名稱。 如果 hello**名稱**有效且可用，綠色的核取記號會出現在 hello**名稱**方塊。
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. 選取一個[定價和調整層][lnk-pricing]。 本教學課程不需要特定層。 此教學課程中，使用 hello 免費 F1 層。
   1. 在 [資源群組]中，建立資源群組，或選取現有的資源群組。 如需詳細資訊，請參閱[資源使用您的 Azure 資源群組 toomanage][lnk-resource-groups]。
   1. 在**位置**，選取 hello 位置 toohost IoT 中樞。 在本教學課程中，選擇最接近您的位置。
1. 選擇好 IoT 中樞組態選項時，按一下 [建立] 。  它可能需要幾分鐘，讓 Azure toocreate IoT 中樞。 toocheck hello 狀態，您可以監視 hello 開始面板或 hello 通知面板中的 hello 進度。
   
    ![新增 IoT 中樞狀態][3]
1. 已成功建立 hello IoT 中樞，按一下您的 IoT 中樞 hello 新的 IoT 中樞的 hello Azure 入口網站 tooopen hello 刀鋒視窗中的 hello 新磚。 請記下 hello **Hostname**，然後按一下**共用存取原則**。
   
    ![新增 IoT 中樞刀鋒視窗][4]
1. 在 hello**共用存取原則**刀鋒視窗中，按一下 hello **iothubowner**原則，然後複製並記下的 hello IoT 中樞連接字串中 hello **iothubowner**刀鋒視窗。 如需詳細資訊，請參閱[存取控制][ lnk-access-control]在 hello 《 IoT 中樞開發人員指南 》。
   
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
