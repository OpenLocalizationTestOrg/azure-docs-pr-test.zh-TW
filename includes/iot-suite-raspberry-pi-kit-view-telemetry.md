## <a name="view-hello-telemetry"></a>檢視 hello 遙測

hello 覆盆子 Pi 現在正要傳送遙測 toohello 遠端監視解決方案。 您可以檢視 hello 遙測 hello 方案儀表板上。 您也可以傳送訊息 tooyour 覆盆子 Pi 從 hello 方案儀表板。

- 瀏覽 toohello 方案儀表板。
- 選取您的裝置在 hello**裝置 tooView**下拉式清單。
- 從 hello hello 遙測覆盆子 Pi 顯示 hello 儀表板上。

![顯示 hello 覆盆子 Pi 的遙測][img-telemetry-display]

## <a name="act-on-hello-device"></a>處理 hello 裝置

從 hello 方案儀表板，您可以覆盆子 Pi 上叫用方法。 當 hello 覆盆子 Pi 連接 toohello 遠端監視解決方案時，它會傳送 hello 方法，它支援的相關資訊。

- 在 hello 方案儀表板中，按一下 **裝置**toovisit hello**裝置**頁面。 選取在 hello 覆盆子 Pi**裝置清單**。 然後選擇 [方法]：

    ![在儀表板中列出裝置][img-list-devices]

- 在 hello**叫用方法**頁面上，選擇**LightBlink**在 hello**方法**下拉式清單。

- 選擇 [InvokeMethod]。 hello LED 連接的 toohello 覆盆子 Pi 閃爍數次。 hello hello 覆盆子 Pi 上的應用程式會傳送通知後 toohello 方案儀表板：

    ![顯示方法歷程記錄][img-method-history]

- 您可以切換 hello LED 開啟和關閉使用 hello **ChangeLightStatus**方法**LightStatusValue**設定得**1**如上或**0**為關閉。

> [!WARNING]
> 如果您離開 hello 遠端監視您的 Azure 帳戶中執行的解決方案，您所要支付 hello 次執行。 減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。 使用完畢時，請從您的 Azure 帳戶刪除 hello 預先設定的解決方案。


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md