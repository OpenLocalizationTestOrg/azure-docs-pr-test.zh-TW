## <a name="create-an-iot-hub"></a>建立 IoT 中樞

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **新增** > **物聯網** > **IoT 中樞**。

   ![在 hello Azure 入口網站中建立 IoT 中樞](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. 在 [hello **IoT 中樞**] 窗格中，輸入下列資訊 IoT 中樞的 hello:

     **名稱**： 輸入 hello IoT 中樞名稱。 如果您所輸入的 hello 名稱是有效的則會出現綠色的核取記號。

     **定價與級別層**： 選取 hello **F1-免費**層。 對此範例而言，此選項就已足夠。 如需詳細資訊，請參閱 hello[定價與級別層](https://azure.microsoft.com/pricing/details/iot-hub/)。

     **資源群組**： 建立資源群組 toohost hello IoT 中樞或使用現有的我的最愛。 如需詳細資訊，請參閱[使用資源群組 toomanage 您的 Azure 資源](../articles/azure-resource-manager/resource-group-portal.md)。

     **位置**： 選取 hello 最接近 hello IoT 中樞建立所在的位置 tooyou。

     **Pin toodashboard**： 選取此選項，讓您輕鬆存取 tooyour IoT 中樞從 hello 儀表板。

   ![輸入資訊 toocreate IoT 中樞](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. 按一下 [建立] 。 IoT 中樞可能需要幾分鐘的時間 toocreate。 您可以看到進度 hello**通知**窗格。

   ![查看 IoT 中樞的進度通知](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. 建立 IoT 中樞之後，請按一下該 hello 儀表板上。 請記下 hello **Hostname**，然後按一下**共用存取原則**。

   ![取得 hello 的 IoT 中樞的主機名稱](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. 在 [hello**共用存取原則**] 窗格中，按一下 hello **iothubowner**原則，然後複製並記 hello**連接字串**的 IoT 中樞。 如需詳細資訊，請參閱[控制存取 tooIoT 中樞](../articles/iot-hub/iot-hub-devguide-security.md)。

> [!NOTE] 
在此設定教學課程中，您不需要此 iothubowner 連接字串。 不過，您可能需要它 hello 不同 IoT 案例的教學課程的某些後完成此安裝。

   ![取得 IoT 中樞連接字串](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>在您的裝置 hello IoT 中樞註冊裝置

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，開啟您的 IoT 中樞。

2. 按一下 [裝置總管]。
3. 在 hello 裝置總管 窗格中，按一下 **新增**tooadd 裝置 tooyour IoT 中樞。 然後 hello 遵循：

   **裝置識別碼**： 輸入 hello 識別碼 hello 新增裝置。 裝置識別碼會區分大小寫。

   **驗證類型**：選取 [對稱金鑰]。

   **自動產生金鑰**：選取此核取方塊。

   **連接裝置 tooIoT 中樞**： 按一下**啟用**。

   ![在 [hello 的 IoT 中樞的裝置總管] 中新增裝置](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. 按一下 [儲存] 。
5. 建立 hello 裝置之後，開啟 hello 裝置在 hello**裝置總管**窗格。
6. 記下 hello 連接字串 hello 主索引鍵。

   ![取得 hello 裝置連接字串](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
