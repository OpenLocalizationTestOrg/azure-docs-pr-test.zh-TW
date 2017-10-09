## <a name="customize-and-extend-hello-device-management-actions"></a>自訂及擴充 hello 裝置管理動作

您的 IoT 解決方案可以展開 hello 定義一組的裝置管理模式，或使用 hello 裝置兩個與雲端到裝置方法基本型別啟用自訂的模式。 其他裝置管理動作範例還包括恢復出廠預設值、韌體更新、軟體更新、電源管理、網路和連線管理，以及資料加密。

## <a name="device-maintenance-windows"></a>裝置維護期間

一般而言，您可以設定裝置 tooperform 動作一次中斷與停機時間降到最低。 裝置的維護期間有常用的模式 toodefine hello 時間時裝置應該更新其設定。 可以使用所需的 hello hello 裝置兩個 toodefine 屬性後端方案，並將它啟用維護視窗可讓您裝置上的原則。 當裝置收到 hello 維護視窗原則時，它可以使用 hello 回報 hello 裝置兩個 tooreport hello hello 原則狀態 屬性。 hello 後端應用程式可以使用裝置的裝置和每個原則的兩個查詢 tooattest toocompliance。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以使用直接方法 tootrigger 遠端重新開機的裝置上。 您使用的 hello 報告的屬性 tooreport hello 上次重新啟動從 hello 裝置時間和查詢的 hello 裝置兩個 toodiscover hello 上次重新啟動從 hello 雲端 hello 裝置的時間。

toocontinue 開始使用 IoT 中樞與裝置管理模式，例如遠端透過 hello 空中韌體更新，請參閱：

[教學課程： 如何 toodo 韌體更新][lnk-fwupdate]

toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。

請參閱 < 開始使用 IoT 中樞 toocontinue[入門 IoT 邊緣][lnk-iot-edge]。

[lnk-fwupdate]: ../articles/iot-hub/iot-hub-node-node-firmware-update.md
[lnk-tutorial-jobs]: ../articles/iot-hub/iot-hub-node-node-schedule-jobs.md
[lnk-iot-edge]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md