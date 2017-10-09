---
title: "模擬裝置與 Azure IoT 閘道 - 疑難排解 | Microsoft Docs"
description: "Intel NUC 閘道器的疑難排解頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 問題, 物聯網問題"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="b18b8-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b18b8-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="b18b8-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="b18b8-106">無法連線至 TI SensorTag</span><span class="sxs-lookup"><span data-stu-id="b18b8-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="b18b8-107">tootroubleshoot SensorTag 連線問題，使用 hello [SensorTag 應用程式](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide)。</span><span class="sxs-lookup"><span data-stu-id="b18b8-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="b18b8-108">Intel NUC 有問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="b18b8-109">tootroubleshoot 開機問題，請參閱太[疑難排解 Intel NUC 否開機問題](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html)。</span><span class="sxs-lookup"><span data-stu-id="b18b8-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="b18b8-110">tootroubleshoot 作業系統問題，請參閱太[Intel NUC 上的作業系統問題的疑難排解](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html)。</span><span class="sxs-lookup"><span data-stu-id="b18b8-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="b18b8-111">tootroubleshoot 其他問題，請參閱太[閃爍的代碼和發出嗶聲代碼 Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html)。</span><span class="sxs-lookup"><span data-stu-id="b18b8-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="b18b8-112">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="b18b8-113">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="b18b8-113">No response during gulp tasks</span></span>

<span data-ttu-id="b18b8-114">如果您遇到中執行的 gulp 工作的問題，您可以加入 hello`--verbose`偵錯的選項。</span><span class="sxs-lookup"><span data-stu-id="b18b8-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="b18b8-115">嘗試使用目前 gulp 工作 tooterminate `Ctrl + C`，然後執行的 hello 遵從在主控台視窗 toosee 偵錯訊息中的命令。</span><span class="sxs-lookup"><span data-stu-id="b18b8-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="b18b8-116">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="b18b8-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="b18b8-117">裝置探索問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-117">Device discovery issues</span></span>

<span data-ttu-id="b18b8-118">如需協助疑難排解常見問題 hello`discover-sensortag`命令，檢查 hello [wiki 頁面](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl)。</span><span class="sxs-lookup"><span data-stu-id="b18b8-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="b18b8-119">npm 問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-119">npm issues</span></span>

<span data-ttu-id="b18b8-120">嘗試執行下列命令的 hello tooupdate npm 封裝：</span><span class="sxs-lookup"><span data-stu-id="b18b8-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="b18b8-121">如果 hello 問題仍然存在，讓您在 hello 本文結尾的註解或建立 GitHub 問題我們[範例儲存機制](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="b18b8-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="b18b8-122">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="b18b8-122">Remote Debugging</span></span>
> <span data-ttu-id="b18b8-123">下面的指示是用於針對本教學課程中使用的 node.js 指令碼偵錯。</span><span class="sxs-lookup"><span data-stu-id="b18b8-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="b18b8-124">偵錯模式執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b18b8-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="b18b8-125">藉由執行下列命令的 hello 偵錯模式執行 hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="b18b8-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="b18b8-126">Hello 偵錯引擎就緒時，您應該會看到`Debugger listening on port 5858`hello 主控台輸出中。</span><span class="sxs-lookup"><span data-stu-id="b18b8-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="b18b8-127">設定 Visual Studio Code tooconnect toohello 遠端裝置</span><span class="sxs-lookup"><span data-stu-id="b18b8-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="b18b8-128">開啟 hello**偵錯**hello 左側面板。</span><span class="sxs-lookup"><span data-stu-id="b18b8-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="b18b8-129">按一下綠色的 hello**開始偵錯**(F5) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b18b8-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="b18b8-130">Visual Studio Code 會開啟 `launch.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="b18b8-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="b18b8-131">更新 hello`launch.json`以 hello 內容之後的檔案。</span><span class="sxs-lookup"><span data-stu-id="b18b8-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="b18b8-132">取代`[device hostname or IP address]`hello 實際裝置 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="b18b8-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![遠端偵錯組態](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="b18b8-134">附加 toohello 遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="b18b8-134">Attach toohello remote application</span></span>

<span data-ttu-id="b18b8-135">按一下綠色的 hello**開始偵錯**偵錯 (F5) 按鈕 toostart。</span><span class="sxs-lookup"><span data-stu-id="b18b8-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="b18b8-136">讀取[VS 程式碼中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 更多關於 hello 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="b18b8-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![偵錯 BLE 範例](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="b18b8-138">Azure CLI 問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-138">Azure CLI issues</span></span>

<span data-ttu-id="b18b8-139">hello Azure 命令列介面 (Azure CLI) 是預覽版。</span><span class="sxs-lookup"><span data-stu-id="b18b8-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="b18b8-140">tooseek 解決方案，您可以使用 hello[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)。</span><span class="sxs-lookup"><span data-stu-id="b18b8-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="b18b8-141">如果您遇到任何錯誤的 hello 工具，[問題](https://github.com/Azure/azure-cli/issues)在 hello**問題**hello GitHub 儲存機制的區段。</span><span class="sxs-lookup"><span data-stu-id="b18b8-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="b18b8-142">疑難排解一般問題的說明，請檢查 hello[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="b18b8-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="b18b8-143">如果您符合 「 找不到滿足 hello 需求的版本 」，請執行的 hello 下列的命令 tooupgrade pip toolastest 版本。</span><span class="sxs-lookup"><span data-stu-id="b18b8-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="b18b8-144">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="b18b8-145">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="b18b8-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="b18b8-146">安裝 pip 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="b18b8-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="b18b8-147">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="b18b8-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="b18b8-148">從先前的安裝某些 pip 封裝所建立的根，會導致 hello 權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="b18b8-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="b18b8-149">hello 方案是 tooremove 由根安裝這些套件。</span><span class="sxs-lookup"><span data-stu-id="b18b8-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="b18b8-150">使用下列步驟 toocomplete hello 這項工作：</span><span class="sxs-lookup"><span data-stu-id="b18b8-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="b18b8-151">跳過`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="b18b8-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="b18b8-152">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="b18b8-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="b18b8-153">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="b18b8-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="b18b8-154">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="b18b8-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="b18b8-155">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="b18b8-156">如果您已成功佈建您的 Azure IoT 中樞與 hello Azure CLI 需要工具 toomanage hello 裝置 tooyour IoT 中樞連線，請再試一次 hello 下列工具。</span><span class="sxs-lookup"><span data-stu-id="b18b8-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="b18b8-157">裝置總管</span><span class="sxs-lookup"><span data-stu-id="b18b8-157">Device Explorer</span></span>

<span data-ttu-id="b18b8-158">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)Windows 本機電腦上執行並連接在 Azure 中的 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b18b8-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="b18b8-159">它會與 hello 下列通訊[IoT 中樞端點](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="b18b8-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="b18b8-160">裝置身分識別管理 tooprovision 和管理裝置與 IoT 中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="b18b8-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="b18b8-161">接收裝置到雲端，所以您可以監視從您的裝置 tooyour IoT 中樞傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="b18b8-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="b18b8-162">傳送雲端到裝置，因此您可以傳送訊息 tooyour 裝置從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b18b8-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="b18b8-163">設定您的 IoT 中樞連接字串，此工具 toouse 內所有其功能。</span><span class="sxs-lookup"><span data-stu-id="b18b8-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="b18b8-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="b18b8-164">iothub-explorer</span></span>

<span data-ttu-id="b18b8-165">[iot 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具 toomanage 裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="b18b8-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="b18b8-166">您可以使用 hello 身分識別登錄中的 hello 工具 toomanage hello 裝置、 監控裝置到雲端訊息和傳送雲端到裝置命令。</span><span class="sxs-lookup"><span data-stu-id="b18b8-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="b18b8-167">tooinstall hello 最新 （發行前版本） 版本的 hello iot 中樞總管工具，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b18b8-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="b18b8-168">tooget 所有相關的其他說明 hello iot 中樞總管命令和它們的參數，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b18b8-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="b18b8-169">hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b18b8-169">hello Azure portal</span></span>

<span data-ttu-id="b18b8-170">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b18b8-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="b18b8-171">您也可以 toouse hello [Azure 入口網站](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/)toohelp 佈建、 管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b18b8-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="b18b8-172">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="b18b8-172">Azure Storage issues</span></span>

<span data-ttu-id="b18b8-173">[Microsoft Azure 儲存體總管 （預覽）](http://storageexplorer.com/)是獨立應用程式，microsoft 可讓您 toowork Windows、 macOS 和 Linux 的 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="b18b8-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="b18b8-174">使用此工具，您可以連接 tooyour 資料表，並查看 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b18b8-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="b18b8-175">您可以使用此工具 tootroubleshoot 您 Azure 儲存體的問題。</span><span class="sxs-lookup"><span data-stu-id="b18b8-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
