> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

這個逐步解說中的 hello[模擬裝置雲端上傳範例]為您示範如何 toouse [Azure IoT 邊緣][ lnk-sdk]從模擬 toosend 裝置到雲端遙測 tooIoT 中樞裝置。

本逐步解說涵蓋下列項目：

* **架構**: hello 的架構資訊[模擬裝置雲端上傳範例]。
* **建置並執行**: hello 步驟需要的 toobuild 和執行的 hello 範例。

## <a name="architecture"></a>架構

hello[模擬裝置雲端上傳範例]顯示 toocreate 傳送遙測資料閘道如何模擬裝置 tooan IoT 中樞。 裝置可能無法 tooconnect 直接 tooIoT 中樞因為 hello 裝置：

* 未使用 IoT 中樞所了解的通訊協定。
* 不是十分聰明 tooremember hello 分派識別 tooit IoT 中樞。

IoT 邊緣閘道可以解決這些問題中 hello 下列方法：

* hello 閘道了解 hello hello 裝置使用的通訊協定、 收到 hello 裝置從裝置到雲端遙測和轉送這些訊息 tooIoT 集線器使用了解的 hello IoT 中樞通訊協定。

* hello 閘道對應 IoT 中樞識別 toodevices，並會作為 proxy，當裝置傳送訊息 tooIoT 中樞。

hello 下列圖表顯示 hello hello 範例的主要元件，包括 hello IoT 邊緣模組：

![][1]

hello 模組不會將訊息直接 tooeach 其他。 hello 模組發佈訊息 tooan 內部 broker 傳送 hello 訊息 toohello 其他模組使用的訂用帳戶的機制。 如需詳細資訊，請參閱[開始使用 Azure IoT Edge][lnk-gw-getstarted]。

### <a name="protocol-ingestion-module"></a>通訊協定擷取模組

此模組為起點來接收資料，並從裝置透過 hello 閘道，並置於 hello 雲端 hello。 在 hello 模組 hello 範例：

1. 建立模擬溫度資料。 如果您使用實體裝置，hello 模組會讀取資料，從這些實體裝置。
1. 建立訊息。
1. 模擬的 hello 溫度資料放入 hello 訊息內容。
1. 加入具有假的 MAC 位址 toohello 訊息的屬性。
1. 讓 hello 訊息可用 toohello 下一個模組中的 hello 鏈結。

呼叫 hello 模組**通訊協定 X 擷取**hello 在上圖中稱為**模擬的裝置**hello 原始程式碼中。

### <a name="mac-lt-gt-iot-hub-id-module"></a>MAC &lt;-&gt; IoT 中樞識別碼模組

此模組會掃描具有 Mac 位址屬性的訊息。 在 hello 範例中，hello 通訊協定擷取模組會將 hello MAC 位址屬性。 如果 hello 模組發現這類屬性，就會加入 IoT 中樞裝置金鑰 toohello 訊息的另一個屬性。 hello 模組然後讓 hello 鏈結中的 hello 訊息可用 toohello 下一個模組。

hello 開發人員設定 MAC 位址與 IoT 中樞識別 tooassociate hello 模擬裝置與 IoT 中樞裝置身分識別之間的對應。 hello 開發人員 hello 模組組態的一部分，請以手動方式加入 hello 對應。

> [!NOTE]
> 此範例使用 MAC 位址作為唯一裝置識別碼，並將它與 IoT 中樞裝置身分識別相互關聯。 不過，您可以撰寫使用不同唯一識別碼的專屬模組。 例如，您的裝置可能會有唯一的數列數字或 hello 遙測資料可能包含重複的內嵌的裝置名稱。

### <a name="iot-hub-communication-module"></a>IoT 中樞通訊模組

此模組會採用與 IoT 中樞的訊息已指派 hello 前一個模組的裝置屬性。 hello 模組會傳送 hello 訊息內容 tooIoT 集線器使用 hello HTTP 通訊協定。 HTTP 是 hello 的了解三種通訊協定的 IoT 中樞的其中一個。

而不是開啟的每個模擬裝置的連線，此模組會從 hello 閘道 toohello IoT 中樞開啟單一 HTTP 連線。 hello 模組然後信號分離透過該連線的所有 hello 模擬裝置的連線。 這個方法可讓單一閘道 tooconnect 許多更多裝置。

## <a name="before-you-get-started"></a>開始之前

開始之前，您必須：

* [建立 IoT 中樞][ lnk-create-hub]在您 Azure 訂用帳戶，您需要集線器 toocomplete hello 名稱本逐步解說。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* 加入兩個裝置 tooyour IoT 中樞，並記下其識別碼及裝置機碼。 您可以使用 hello[裝置總管][ lnk-device-explorer]或[iot 中樞總管][ lnk-iothub-explorer]工具 tooadd hello 中建立您的裝置 toohello IoT 中樞上一個步驟，並擷取其索引鍵。

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[模擬裝置雲端上傳範例]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md