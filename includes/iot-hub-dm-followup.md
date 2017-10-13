## <a name="customize-and-extend-the-device-management-actions"></a>自訂及延伸裝置管理動作

您的 IoT 解決方案可以透過使用裝置對應項和雲端到裝置方法基元，擴充一組已定義的裝置管理模式或啟用自訂模式。 其他裝置管理動作範例還包括恢復出廠預設值、韌體更新、軟體更新、電源管理、網路和連線管理，以及資料加密。

## <a name="device-maintenance-windows"></a>裝置維護期間

一般而言，您會設定讓裝置在產生最短中斷和停機時間的時機執行動作。 裝置維護期間是用來定義裝置組態更新時機的常用模式。 您的後端解決方案可以使用所需的裝置對應項 (twin) 屬性，在您的裝置上定義可啟用維護期間的原則並啟用該原則。 當裝置收到維護期間原則時，它可以使用回報的裝置對應項 (twin) 屬性來回報原則的狀態。 接著，後端 App 便可使用裝置對應項 (twin) 查詢來證明是否符合裝置及每個原則的規定。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已使用直接方法在裝置上觸發遠端重新開機。 您已使用報告屬性來從裝置回報上次重新開機時間，以及查詢裝置對應項來從雲端探索裝置的上次重新開機時間。

若要繼續開始使用「IoT 中樞」和裝置管理模式 (例如遠端無線韌體更新)，請參閱︰

[教學課程：如何進行韌體更新][lnk-fwupdate]

若要了解如何擴充您的 IoT 解決方案以及在多個裝置上排程方法呼叫，請參閱[排程及廣播作業][lnk-tutorial-jobs]教學課程。

若要繼續開始使用 IoT 中樞，請參閱[開始使用 IoT Edge][lnk-iot-edge]。

[lnk-fwupdate]: ../articles/iot-hub/iot-hub-node-node-firmware-update.md
[lnk-tutorial-jobs]: ../articles/iot-hub/iot-hub-node-node-schedule-jobs.md
[lnk-iot-edge]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md