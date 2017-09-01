> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

[Simulated Device Cloud Upload 範例]的這個逐步解說示範如何使用 [Azure IoT Edge][lnk-sdk]，將裝置到雲端遙測從模擬裝置傳送到 IoT 中樞。

本逐步解說涵蓋下列項目：

* **架構**：[Simulated Device Cloud Upload 範例]的架構資訊。
* **建置和執行**︰建置和執行範例所需的步驟。

## <a name="architecture"></a>架構

[Simulated Device Cloud Upload 範例]示範如何建立閘道，以將遙測從模擬裝置傳送到 IoT 中樞。 裝置可能無法直接連線到 IoT 中樞的原因如下：

* 未使用 IoT 中樞所了解的通訊協定。
* 不夠聰明，無法記住 IoT 中樞指派給它的身分識別。

IoT Edge 閘道可以下列方式解決這些問題：

* 閘道了解裝置所使用的通訊協定、從裝置接收裝置到雲端遙測，並使用 IoT 中樞所了解的通訊協定將這些訊息轉送到 IoT 中樞。

* 閘道將 IoT 中樞身分識別對應到裝置，並且會在裝置將訊息傳送到 IoT 中樞時作為 proxy。

下圖顯示範例的主要元件 (包含 IoT Edge 模組)︰

![][1]

模組不會彼此直接傳遞訊息。 模組會將訊息發佈到內部訊息代理程式，而內部代理程式會使用訂用帳戶機制將訊息傳遞到其他模組。 如需詳細資訊，請參閱[開始使用 Azure IoT Edge][lnk-gw-getstarted]。

### <a name="protocol-ingestion-module"></a>通訊協定擷取模組

此模組是一個起點，能透過閘道從裝置取得資料，以及將資料傳遞到雲端。 在範例中，模組會：

1. 建立模擬溫度資料。 如果您是使用實際裝置，此模組會讀取這些裝置中的資料。
1. 建立訊息。
1. 將模擬溫度資料放到訊息內容。
1. 將包含假 MAC 位址的屬性新增至訊息。
1. 讓訊息可供鏈結中的下一個模組使用。

在原始程式碼中，上圖中的**通訊協定 X 擷取**模組稱為**模擬裝置**。

### <a name="mac-lt-gt-iot-hub-id-module"></a>MAC &lt;-&gt; IoT 中樞識別碼模組

此模組會掃描具有 Mac 位址屬性的訊息。 在範例中，通訊協定擷取模組會新增 MAC 位址屬性。 如果模組發現這類屬性，就會將包含 IoT 中樞裝置索引鍵的另一個屬性新增到訊息。 接著，模組會讓訊息可供鏈結中的下一個模組使用。

開發人員會設定 MAC 位址與 IoT 中樞身分識別之間的對應，將模擬的裝置與 IoT 中樞裝置身分識別建立關聯。 開發人員會以手動新增對應，作為模組設定的一部分。

> [!NOTE]
> 此範例使用 MAC 位址作為唯一裝置識別碼，並將它與 IoT 中樞裝置身分識別相互關聯。 不過，您可以撰寫使用不同唯一識別碼的專屬模組。 例如，您的裝置可能會有唯一的序號，或是遙測資料可能包含唯一的內嵌裝置名稱。

### <a name="iot-hub-communication-module"></a>IoT 中樞通訊模組

此模組所採用的訊息包含 IoT 中樞裝置索引鍵屬性，已由前一個模組指定。 此模組會使用 HTTP 通訊協定，將訊息內容傳送到 IoT 中樞。 HTTP 是 IoT 中樞所了解的三種通訊協定中的其中一種。

此模組不會開啟每個模擬裝置的連線，而是會開啟從閘道至 IoT 中樞的單一 HTTP 連線。 接著，模組會透過該連線，從所有的模擬裝置進行多工連線。 這個方法可讓單一閘道連線許多其他裝置。

## <a name="before-you-get-started"></a>開始之前

開始之前，您必須：

* 於 Azure 訂用帳戶中[建立 IoT 中樞][lnk-create-hub]時，您需要中樞名稱才能完成此逐步解說。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。
* 將兩個裝置加入 IoT 中樞中，並記下其識別碼和裝置金鑰。 您可以使用[裝置總管][lnk-device-explorer]或 [iothub-explorer][lnk-iothub-explorer] 工具，將您的裝置新增到在上一個步驟中建立的 IoT 中樞並擷取其金鑰。

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[Simulated Device Cloud Upload 範例]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md