> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。 IoT 中樞保存每個裝置連接 tooit 裝置兩個。

使用裝置對應項可以：

* 從您的解決方案後端儲存裝置中繼資料。
* 報告目前的狀態資訊，例如可用的功能和條件 （例如，hello 連線使用方式），從您的裝置應用程式。
* 同步處理長時間執行工作流程 （例如韌體和組態更新） 裝置的應用程式與後端應用程式之間的 hello 的狀態。
* 查詢裝置中繼資料、組態或狀態。

> [!NOTE]
> 裝置對應項是設計來進行同步處理和查詢裝置組態和條件。 有關在中找到 toouse 裝置雙[了解裝置雙][lnk-twins]。

裝置對應項會儲存在 IoT 中樞，並且包含︰

* *標記*，只能由 hello 方案後端; 存取裝置中繼資料
* *所需屬性*，JSON 物件的可修改由 hello 解決方案回結束作業，並觀察 hello 裝置的應用程式; 以及
* *報告內容*，hello 裝置應用程式的可修改、 可讀性更高的 hello 方案後端的 JSON 物件。 標籤和屬性不能包含陣列，但物件可以是巢狀的。

![][img-twin]

此外，hello 方案後端可以查詢裝置雙根據所有 hello 上述資料。
請參閱太[了解裝置雙][ lnk-twins]如需有關裝置雙和 toohello [IoT 中樞的查詢語言][ lnk-query]參考用於查詢。

> [!NOTE]
> 此時，裝置雙都只連接 tooIoT 中樞的裝置可以存取使用 hello MQTT 通訊協定。 請參閱 toohello [MQTT 支援][ lnk-devguide-mqtt]文章的指示現有裝置的應用程式 toouse tooconvert MQTT。

本教學課程說明如何：

* 建立後端應用程式，將它新增*標記*tooa 裝置的兩個，並報告其連線的模擬的裝置應用程式通道為*報告屬性*上 hello 裝置兩個。
* 查詢從 hello 標記與先前建立的屬性上使用篩選器後端應用程式的裝置。

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md