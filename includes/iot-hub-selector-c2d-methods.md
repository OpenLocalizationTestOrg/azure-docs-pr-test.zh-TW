> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

Azure IoT 中樞是一項完全受管理的服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。 先前的教學課程 ([開始使用 IoT 中樞]和[傳送雲端到裝置訊息與 IoT 中樞]) 說明 hello 基本裝置到雲端 」 和 「 雲端到裝置訊息功能的 IoT 中樞。 IoT 中樞也可讓您 hello 能力 tooinvoke 非持續性方法，從 hello 雲端的裝置上。 直接方法表示要求-回覆互動 HTTP 呼叫成功或失敗 （之後立即使用者指定的逾時），裝置類似 tooan toolet hello 使用者知道的 hello 呼叫 hello 狀態。 [叫用的裝置上直接方法][ lnk-devguide-methods]描述更詳細的直接方法，並提供指引 toouse 時直接方法，而不是雲端到裝置訊息或想要的屬性。

本教學課程說明如何：

* 使用 hello Azure 入口網站 toocreate IoT 中樞，並在您的 IoT 中樞中建立裝置身分識別。
* 建立直接的方法可以呼叫 hello 雲端之模擬的裝置應用程式。
* 建立主控台應用程式會呼叫 hello 模擬的裝置的應用程式透過您的 IoT 中樞中的直接的方法。

> [!NOTE]
> 在這個階段，直接的方法都是只有裝置上支援的 tooIoT 集線器使用連線的 hello MQTT 通訊協定。 請參閱 toohello [MQTT 支援][ lnk-devguide-mqtt]文章的指示現有裝置的應用程式 toouse tooconvert MQTT。


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[傳送雲端到裝置訊息與 IoT 中樞]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[開始使用 IoT 中樞]: ../articles/iot-hub/iot-hub-node-node-getstarted.md