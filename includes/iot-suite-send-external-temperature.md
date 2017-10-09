## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="dc812-101">設定 hello Node.js 模擬的裝置</span><span class="sxs-lookup"><span data-stu-id="dc812-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="dc812-102">Hello 遠端監視儀表板上，按一下  **+ 新增裝置**然後再加入*自訂裝置*。</span><span class="sxs-lookup"><span data-stu-id="dc812-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="dc812-103">記下 hello IoT 中樞的主機名稱、 裝置識別碼和裝置金鑰。</span><span class="sxs-lookup"><span data-stu-id="dc812-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="dc812-104">您需要它們在此教學課程稍後當您準備 hello remote_monitoring.js 裝置用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc812-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="dc812-105">請確定 Node.js 0.12.x 版或更新版本已經安裝在您的開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="dc812-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="dc812-106">執行`node --version`在命令提示字元，或在殼層 toocheck hello 版本。</span><span class="sxs-lookup"><span data-stu-id="dc812-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="dc812-107">Linux 上使用封裝管理員 tooinstall Node.js 的相關資訊，請參閱[透過封裝管理員的安裝 Node.js][node-linux]。</span><span class="sxs-lookup"><span data-stu-id="dc812-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="dc812-108">安裝 Node.js 之後，複製 hello 最新版 hello [azure iot-sdk 節點][ lnk-github-repo]儲存機制 tooyour 開發電腦。</span><span class="sxs-lookup"><span data-stu-id="dc812-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="dc812-109">一律使用 hello**主要**hello hello 程式庫和範例的最新版本的分支。</span><span class="sxs-lookup"><span data-stu-id="dc812-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="dc812-110">從您的本機複本的 hello [azure iot-sdk 節點][ lnk-github-repo]儲存機制、 hello 節點/裝置範例 tooan 空白資料夾中的下列兩個檔案，在開發電腦上的複本 hello:</span><span class="sxs-lookup"><span data-stu-id="dc812-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="dc812-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="dc812-111">packages.json</span></span>
   * <span data-ttu-id="dc812-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="dc812-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="dc812-113">開啟 hello remote_monitoring.js 檔案，並尋找下列變數定義 hello:</span><span class="sxs-lookup"><span data-stu-id="dc812-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="dc812-114">以您裝置的連接字串取代 **[IoT 中樞裝置連接字串]** 。</span><span class="sxs-lookup"><span data-stu-id="dc812-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="dc812-115">使用 IoT 中樞的主機名稱、 裝置識別碼，與您記下的步驟 1 中的裝置識別碼 hello 值。</span><span class="sxs-lookup"><span data-stu-id="dc812-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="dc812-116">裝置連接字串具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc812-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="dc812-117">如果您的 IoT 中樞的主機名稱是**contoso**和您的裝置識別碼是**mydevice**，您的連接字串看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc812-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. 儲存 hello 檔案。 <span data-ttu-id="dc812-119">執行下列命令殼層或包含這些檔案 tooinstall hello 必要套件 hello 資料夾中的命令提示字元中的 hello，然後再執行 hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="dc812-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="dc812-120">觀察運作中的動態遙測</span><span class="sxs-lookup"><span data-stu-id="dc812-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="dc812-121">hello 儀表板會顯示 hello 氣溫和溼度遙測，從現有的模擬裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="dc812-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![hello 預設儀表板][image1]

<span data-ttu-id="dc812-123">如果您選取您已執行 hello 前一節中的 hello Node.js 模擬的裝置，您會看到溫度、 溼度和外部溫度遙測：</span><span class="sxs-lookup"><span data-stu-id="dc812-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![新增外部溫度 toohello 儀表板][image2]

<span data-ttu-id="dc812-125">hello 遠端監視解決方案會自動偵測 hello 其他外部溫度遙測類型，並將其 toohello 圖表 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="dc812-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png