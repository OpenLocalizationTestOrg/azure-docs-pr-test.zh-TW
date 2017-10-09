---
title: "Connect Raspberry Pi (C) tooAzure IoT-疑難排解 |Microsoft 文件"
description: "疑難排解 hello 覆盆子 Pi Node.js 體驗的頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 問題, 物聯網問題"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="32ca1-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="32ca1-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="32ca1-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="32ca1-106">hello 應用程式也會執行，但 hello LED 閃爍不</span><span class="sxs-lookup"><span data-stu-id="32ca1-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="32ca1-107">此問題，一律為相關的 toohardware 電路連線。</span><span class="sxs-lookup"><span data-stu-id="32ca1-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="32ca1-108">使用下列步驟 tooidentify 問題 hello:</span><span class="sxs-lookup"><span data-stu-id="32ca1-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="32ca1-109">請檢查您已選擇正確的 hello **GPIO**在面板。</span><span class="sxs-lookup"><span data-stu-id="32ca1-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="32ca1-110">hello 兩個連接埠應**GPIO GND (Pin 6)**和**GPIO 04 (Pin 7)**。</span><span class="sxs-lookup"><span data-stu-id="32ca1-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="32ca1-111">請檢查您的 LED hello 極性正確。</span><span class="sxs-lookup"><span data-stu-id="32ca1-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="32ca1-112">hello 長腳應該指出 hello**正數**，anode pin。</span><span class="sxs-lookup"><span data-stu-id="32ca1-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="32ca1-113">使用 hello **3.3V 釘選**和**GND Pin**覆盆子 Pi 3 為基礎。</span><span class="sxs-lookup"><span data-stu-id="32ca1-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="32ca1-114">Pi 視為 hello DC 電源。</span><span class="sxs-lookup"><span data-stu-id="32ca1-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="32ca1-115">請檢查該 hello LED 可正常運作。</span><span class="sxs-lookup"><span data-stu-id="32ca1-115">Check that hello LED works fine.</span></span>

![LED 規格](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="32ca1-117">其他硬體問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-117">Other hardware issues</span></span>
<span data-ttu-id="32ca1-118">如需解決常見的問題，在覆盆子 Pi 3 上的資訊，請參閱 hello[正式的疑難排解頁面](http://elinux.org/R-Pi_Troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="32ca1-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="32ca1-119">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="32ca1-120">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="32ca1-120">No response during gulp tasks</span></span>
<span data-ttu-id="32ca1-121">如果您遇到中執行的 gulp 工作的問題，您可以加入 hello`--verbose`偵錯的選項。</span><span class="sxs-lookup"><span data-stu-id="32ca1-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="32ca1-122">透過使用 Ctrl + C，嘗試使用 tooterminate 目前 gulp 工作，然後執行下列命令，在主控台視窗 toosee 偵錯訊息中的 hello。</span><span class="sxs-lookup"><span data-stu-id="32ca1-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="32ca1-123">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="32ca1-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="32ca1-124">裝置探索問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-124">Device discovery issues</span></span>
<span data-ttu-id="32ca1-125">如需協助疑難排解常見問題 hello`devdisco`命令，檢查 hello[讀我檔案](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md)。</span><span class="sxs-lookup"><span data-stu-id="32ca1-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="32ca1-126">npm 問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-126">npm issues</span></span>
<span data-ttu-id="32ca1-127">嘗試使用下列命令的 hello tooupdate npm 封裝：</span><span class="sxs-lookup"><span data-stu-id="32ca1-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="32ca1-128">如果 hello 問題仍然存在，讓您在 hello 本文結尾的註解或建立 GitHub 問題我們[範例儲存機制](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="32ca1-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="32ca1-129">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="32ca1-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="32ca1-130">偵錯模式執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="32ca1-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="32ca1-131">Hello 偵錯引擎就緒時，您應該會看到```Debugger listening on port 5858```hello 主控台輸出中。</span><span class="sxs-lookup"><span data-stu-id="32ca1-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="32ca1-132">設定 Visual Studio Code tooconnect toohello 遠端裝置</span><span class="sxs-lookup"><span data-stu-id="32ca1-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="32ca1-133">開啟 hello**偵錯**hello 左側面板。</span><span class="sxs-lookup"><span data-stu-id="32ca1-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="32ca1-134">按一下綠色的 hello**開始偵錯**(F5) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32ca1-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="32ca1-135">Visual Studio Code 會開啟 launch.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="32ca1-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="32ca1-136">更新內容之後的 hello hello launch.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="32ca1-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="32ca1-137">取代`[device hostname or IP address]`hello 實際裝置 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="32ca1-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="32ca1-138">toolearn 深入了解 hello Visual Studio 偵錯，請參閱太[偵錯 Visual Studio 程式碼](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes)。</span><span class="sxs-lookup"><span data-stu-id="32ca1-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![遠端偵錯組態](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="32ca1-140">附加 toohello 遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="32ca1-140">Attach toohello remote application</span></span>
<span data-ttu-id="32ca1-141">按一下綠色的 hello**開始偵錯**偵錯 (F5) 按鈕 toostart。</span><span class="sxs-lookup"><span data-stu-id="32ca1-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="32ca1-142">讀取[VS 程式碼中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 更多關於 hello 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="32ca1-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![遠端偵錯互動](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="32ca1-144">Azure CLI 問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-144">Azure CLI issues</span></span>
<span data-ttu-id="32ca1-145">hello Azure 命令列介面 (Azure CLI) 是預覽版。</span><span class="sxs-lookup"><span data-stu-id="32ca1-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="32ca1-146">tooseek 解決方案，您可以使用 hello[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)。</span><span class="sxs-lookup"><span data-stu-id="32ca1-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="32ca1-147">如果您遇到任何錯誤的 hello 工具，[問題](https://github.com/Azure/azure-cli/issues)在 hello**問題**hello GitHub 儲存機制的區段。</span><span class="sxs-lookup"><span data-stu-id="32ca1-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="32ca1-148">疑難排解一般問題的說明，請檢查 hello[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="32ca1-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="32ca1-149">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="32ca1-150">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="32ca1-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="32ca1-151">安裝 pip 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="32ca1-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="32ca1-152">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="32ca1-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="32ca1-153">從先前的安裝某些 pip 封裝所建立的根，會導致 hello 權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="32ca1-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="32ca1-154">hello 方案是 tooremove 由根安裝這些套件。</span><span class="sxs-lookup"><span data-stu-id="32ca1-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="32ca1-155">使用下列步驟 toocomplete hello 這項工作：</span><span class="sxs-lookup"><span data-stu-id="32ca1-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="32ca1-156">請移至：/usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="32ca1-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="32ca1-157">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="32ca1-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="32ca1-158">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="32ca1-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="32ca1-159">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="32ca1-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="32ca1-160">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="32ca1-161">如果您已成功佈建您的 Azure IoT 中樞與 Azure CLI 需要工具 toomanage hello 裝置 tooyour IoT 中樞連線，請再試一次 hello 下列工具。</span><span class="sxs-lookup"><span data-stu-id="32ca1-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="32ca1-162">裝置總管</span><span class="sxs-lookup"><span data-stu-id="32ca1-162">Device explorer</span></span>
<span data-ttu-id="32ca1-163">hello[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)工具 Windows 本機電腦上執行，並連接在 Azure 中的 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="32ca1-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="32ca1-164">它會與 hello 下列通訊[IoT 中樞端點](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="32ca1-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="32ca1-165">*裝置身分識別管理*tooprovision 和管理裝置與 IoT 中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="32ca1-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="32ca1-166">*接收裝置到雲端*讓您監視從您的裝置 tooyour IoT 中樞傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="32ca1-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="32ca1-167">*傳送雲端到裝置*讓您可以傳送訊息 tooyour 裝置從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="32ca1-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="32ca1-168">設定您的 IoT 中樞連接字串，此工具 toouse 內所有其功能。</span><span class="sxs-lookup"><span data-stu-id="32ca1-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="32ca1-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="32ca1-169">iothub-explorer</span></span>
<span data-ttu-id="32ca1-170">[iot 中樞總管](https://github.com/Azure/iothub-explorer)toomanage 裝置是範例多平台 CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="32ca1-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="32ca1-171">您可以使用 hello 身分識別登錄中的 hello 工具 toomanage hello 裝置、 監控裝置到雲端訊息和傳送雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="32ca1-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="32ca1-172">tooinstall hello 最新版本 （發行前版本） 的 hello iot 中樞總管工具，執行下列命令，命令列環境中的 hello:</span><span class="sxs-lookup"><span data-stu-id="32ca1-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="32ca1-173">您可以使用下列命令 tooget 所有相關的其他說明 hello iot 中樞總管命令和其參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="32ca1-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="32ca1-174">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="32ca1-174">Azure portal</span></span>
<span data-ttu-id="32ca1-175">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="32ca1-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="32ca1-176">您也可以 toouse hello [Azure 入口網站](../azure-portal-overview.md)toohelp 佈建、 管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="32ca1-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="32ca1-177">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="32ca1-177">Azure Storage issues</span></span>
<span data-ttu-id="32ca1-178">[Microsoft Azure 儲存體總管 （預覽）](http://storageexplorer.com)是獨立應用程式，microsoft 可讓您 toowork Windows、 macOS 和 Linux 的 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="32ca1-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="32ca1-179">使用此工具，您可以連接 tooyour 資料表，並查看 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="32ca1-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="32ca1-180">您可以使用此工具 tootroubleshoot 您 Azure 儲存體的問題。</span><span class="sxs-lookup"><span data-stu-id="32ca1-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

