## <a name="configure-hello-nodejs-simulated-device"></a>設定 hello Node.js 模擬的裝置
1. Hello 遠端監視儀表板上，按一下  **+ 新增裝置**然後再加入*自訂裝置*。 記下 hello IoT 中樞的主機名稱、 裝置識別碼和裝置金鑰。 您需要它們在此教學課程稍後當您準備 hello remote_monitoring.js 裝置用戶端應用程式。
2. 請確定 Node.js 0.12.x 版或更新版本已經安裝在您的開發電腦上。 執行`node --version`在命令提示字元，或在殼層 toocheck hello 版本。 Linux 上使用封裝管理員 tooinstall Node.js 的相關資訊，請參閱[透過封裝管理員的安裝 Node.js][node-linux]。
3. 安裝 Node.js 之後，複製 hello 最新版 hello [azure iot-sdk 節點][ lnk-github-repo]儲存機制 tooyour 開發電腦。 一律使用 hello**主要**hello hello 程式庫和範例的最新版本的分支。
4. 從您的本機複本的 hello [azure iot-sdk 節點][ lnk-github-repo]儲存機制、 hello 節點/裝置範例 tooan 空白資料夾中的下列兩個檔案，在開發電腦上的複本 hello:
   
   * packages.json
   * remote_monitoring.js
5. 開啟 hello remote_monitoring.js 檔案，並尋找下列變數定義 hello:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. 以您裝置的連接字串取代 **[IoT 中樞裝置連接字串]** 。 使用 IoT 中樞的主機名稱、 裝置識別碼，與您記下的步驟 1 中的裝置識別碼 hello 值。 裝置連接字串具有下列格式的 hello:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    如果您的 IoT 中樞的主機名稱是**contoso**和您的裝置識別碼是**mydevice**，您的連接字串看起來像下列程式碼片段的 hello:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. 儲存 hello 檔案。 執行下列命令殼層或包含這些檔案 tooinstall hello 必要套件 hello 資料夾中的命令提示字元中的 hello，然後再執行 hello 範例應用程式：
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>觀察運作中的動態遙測
hello 儀表板會顯示 hello 氣溫和溼度遙測，從現有的模擬裝置 hello:

![hello 預設儀表板][image1]

如果您選取您已執行 hello 前一節中的 hello Node.js 模擬的裝置，您會看到溫度、 溼度和外部溫度遙測：

![新增外部溫度 toohello 儀表板][image2]

hello 遠端監視解決方案會自動偵測 hello 其他外部溫度遙測類型，並將其 toohello 圖表 hello 儀表板上。

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png