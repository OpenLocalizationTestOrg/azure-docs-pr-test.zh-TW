> [!div class="op_single_selector"]
> * [裝置︰Node.js 服務︰Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [裝置︰Node.js 服務︰C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [裝置︰Java 服務︰Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

後端應用程式可以使用 Azure IoT 中樞基本類型，例如[裝置兩個][ lnk-devtwin]和[直接方法][lnk-c2dmethod]，tooremotely 啟動及監視裝置管理行動裝置上。 本教學課程會示範如何在後端應用程式和裝置的應用程式可以搭配 tooinitiate 和監視使用 IoT 中樞的遠端裝置重新開機。

從 hello 雲端中的後端應用程式使用直接的方法 tooinitiate 裝置管理動作 （例如重新開機，原廠重設和韌體更新）。 裝置 hello 負責：

* 處理從 IoT 中樞傳送嗨方法要求。
* 初始化 hello 裝置 hello 對應裝置的特定動作。
* 提供狀態更新，透過*報告屬性*tooIoT 中樞。

您可以使用後端應用程式中 hello 雲端 toorun 裝置兩個查詢 tooreport hello 進度您裝置的管理動作。

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
