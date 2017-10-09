## <a name="view-device-telemetry-in-hello-dashboard"></a>Hello 儀表板中檢視裝置遙測
在遠端監視解決方案可讓您 tooview hello 遙測您的裝置傳送 tooIoT 中樞 hello hello 儀表板。

1. 在瀏覽器中傳回 toohello 遠端監視方案儀表板，按一下 **裝置**在 hello 左側面板 toonavigate toohello**裝置清單**。
2. 在 hello**裝置清單**，您應該會看到您的裝置 hello 狀態是**執行**。 如果沒有，請按一下**啟用裝置**在 hello**裝置詳細資料**面板。
   
    ![檢視裝置狀態][18]
3. 按一下**儀表板**tooreturn toohello 儀表板中，選取您的裝置在 hello**裝置 tooView**下拉式 tooview 其遙測。 來自 hello 範例應用程式的 hello 遙測是 50 個單位的內部溫度、 55 單位外部溫度和溼度的 50 個單位。
   
    ![檢視裝置遙測資料][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a>在裝置上叫用方法
hello 遠端監視解決方案中的 hello 儀表板可讓您透過 IoT 中樞裝置上的 tooinvoke 方法。 比方說，在遠端監視解決方案的 hello 您可以叫用方法 toosimulate 重新開機裝置。

1. Hello 遠端監視方案儀表板中，按一下 **裝置**在 hello 左側面板 toonavigate toohello**裝置清單**。
2. 按一下**裝置識別碼**裝置 hello**裝置清單**。
3. 在 hello**裝置詳細資料** 面板中，按一下 **方法**。
   
    ![裝置方法][13]
4. 在 hello**方法**下拉式清單中，選取**InitiateFirmwareUpdate**，然後在**FWPACKAGEURI**輸入空的 URL。 按一下**叫用方法**toocall hello 方法 hello 裝置上的。
   
    ![叫用裝置方法][14]
   

5. 您會看到 hello 主控台 hello 裝置處理 hello 方法時，執行您裝置的程式碼中的訊息。 hello 方法結果的 hello hello 方案入口網站新增 toohello 歷程記錄：

    ![檢視方法歷程記錄][img-method-history]

## <a name="next-steps"></a>後續步驟
hello 文章[預先設定的自訂方案][ lnk-customize]描述一些您可以擴充此範例的方法。 可能的延伸模組包括使用真實的感應器和實作其他命令。

您可以進一步了解 hello [hello azureiotsuite.com 網站的權限][lnk-permissions]。

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
