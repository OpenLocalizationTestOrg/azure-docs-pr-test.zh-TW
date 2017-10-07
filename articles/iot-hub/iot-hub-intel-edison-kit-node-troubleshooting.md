---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 4 課： 疑難排解 |Microsoft 文件"
description: "Intel Edison Node.js 經驗的疑難排解頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 疑難排解"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="bd16a-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="bd16a-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="bd16a-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="bd16a-105">Hardware issues</span></span>
<span data-ttu-id="bd16a-106">如需解決 Intel Edison 中常見的問題資訊，請參閱 hello[正式的疑難排解頁面](https://software.intel.com/en-us/node/637974)。</span><span class="sxs-lookup"><span data-stu-id="bd16a-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="bd16a-107">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="bd16a-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="bd16a-108">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="bd16a-108">No response during gulp tasks</span></span>
<span data-ttu-id="bd16a-109">如果您遇到執行 gulp 工作的問題，您可以新增 hello`--verbose`偵錯的選項。</span><span class="sxs-lookup"><span data-stu-id="bd16a-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="bd16a-110">嘗試使用目前 gulp 工作 tooterminate `Ctrl + C`，然後執行的 hello 遵從在主控台視窗 toosee 偵錯訊息中的命令。</span><span class="sxs-lookup"><span data-stu-id="bd16a-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="bd16a-111">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="bd16a-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="bd16a-112">NPM 問題</span><span class="sxs-lookup"><span data-stu-id="bd16a-112">NPM issues</span></span>
<span data-ttu-id="bd16a-113">請嘗試 tooupdate NPM 封裝以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="bd16a-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="bd16a-114">如果 hello 問題仍然存在，讓您在 hello 本文結尾的註解或建立 GitHub 問題我們[範例儲存機制][sample-repository]。</span><span class="sxs-lookup"><span data-stu-id="bd16a-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="bd16a-115">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="bd16a-115">Remote debugging</span></span>

### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="bd16a-116">偵錯模式執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="bd16a-116">Run hello sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="bd16a-117">Hello 偵錯引擎準備就緒之後，您應該能夠 toosee ```Debugger listening on port 5858``` hello 主控台輸出。</span><span class="sxs-lookup"><span data-stu-id="bd16a-117">Once hello debug engine is ready, you should be able toosee ```Debugger listening on port 5858``` from hello console output.</span></span>

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="bd16a-118">設定 VS Code tooconnect toohello 遠端裝置</span><span class="sxs-lookup"><span data-stu-id="bd16a-118">Configure VS Code tooconnect toohello remote device</span></span>

<span data-ttu-id="bd16a-119">開啟 hello**偵錯**從 hello 左側面板。</span><span class="sxs-lookup"><span data-stu-id="bd16a-119">Open hello **Debug** panel from hello left side.</span></span>

<span data-ttu-id="bd16a-120">按一下綠色的 hello**開始偵錯**(F5) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bd16a-120">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="bd16a-121">這樣會開啟 VS Code **launch.json**檔案，這需要 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="bd16a-121">VS Code would open a **launch.json** file, which you need tooupdate.</span></span>

<span data-ttu-id="bd16a-122">更新 hello **launch.json**檔案以 hello 下列內容，取代`[device hostname or IP address]`hello 實際裝置 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="bd16a-122">Update hello **launch.json** file with hello following content, replace `[device hostname or IP address]` with hello actual device IP address or hostname.</span></span>  

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

![遠端偵錯組態](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="bd16a-124">附加 toohello 遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="bd16a-124">Attach toohello remote application</span></span>

<span data-ttu-id="bd16a-125">按一下綠色的 hello**開始偵錯**(F5) 按鈕並享受偵錯。</span><span class="sxs-lookup"><span data-stu-id="bd16a-125">Click hello green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="bd16a-126">您可以閱讀[VS 程式碼中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 更多關於 hello 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="bd16a-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![遠端偵錯互動](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="bd16a-128">Azure-CLI 問題</span><span class="sxs-lookup"><span data-stu-id="bd16a-128">Azure-CLI issues</span></span>
<span data-ttu-id="bd16a-129">hello Azure 命令列介面 (Azure CLI) 是預覽版。</span><span class="sxs-lookup"><span data-stu-id="bd16a-129">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="bd16a-130">尋找方案中 hello[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)tooseek 解決方案。</span><span class="sxs-lookup"><span data-stu-id="bd16a-130">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="bd16a-131">當命令無法運作正常，再試一次 tooupgrade Azure cli toolatest 版本。</span><span class="sxs-lookup"><span data-stu-id="bd16a-131">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="bd16a-132">如果您遇到任何錯誤的 hello 工具，[問題](https://github.com/Azure/azure-cli/issues)在 hello**問題**hello GitHub 儲存機制的區段。</span><span class="sxs-lookup"><span data-stu-id="bd16a-132">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="bd16a-133">疑難排解一般問題的說明，請檢查 hello[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="bd16a-133">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="bd16a-134">如果您符合 「 找不到滿足 hello 需求的版本 」，請執行的 hello 下列的命令 tooupgrade pip toolastest 版本。</span><span class="sxs-lookup"><span data-stu-id="bd16a-134">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="bd16a-135">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="bd16a-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="bd16a-136">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="bd16a-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="bd16a-137">安裝 **pip** 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="bd16a-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="bd16a-138">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="bd16a-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="bd16a-139">某些**pip**從先前的安裝封裝所建立的根，會導致 hello 權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="bd16a-139">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="bd16a-140">hello 方案是 tooremove 由根安裝這些套件。</span><span class="sxs-lookup"><span data-stu-id="bd16a-140">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="bd16a-141">使用下列步驟 toocomplete hello 這項工作：</span><span class="sxs-lookup"><span data-stu-id="bd16a-141">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="bd16a-142">請移至：/usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="bd16a-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="bd16a-143">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="bd16a-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="bd16a-144">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="bd16a-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="bd16a-145">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="bd16a-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="bd16a-146">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="bd16a-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="bd16a-147">如果您已成功佈建您的 Azure IoT 中樞與`azure-cli`，而且您需要連線 tooyour IoT 中樞，遵循工具再試一次 hello 工具 toomanage hello 裝置：</span><span class="sxs-lookup"><span data-stu-id="bd16a-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="bd16a-148">裝置總管</span><span class="sxs-lookup"><span data-stu-id="bd16a-148">Device Explorer</span></span>
<span data-ttu-id="bd16a-149">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)Windows 本機電腦上執行並連接在 Azure 中的 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="bd16a-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="bd16a-150">它會與 hello 下列通訊[IoT 中樞端點](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="bd16a-150">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="bd16a-151">_裝置身分識別管理_tooprovision 和管理裝置與 IoT 中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="bd16a-151">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="bd16a-152">_接收裝置到雲端_讓您監視從您的裝置 tooyour IoT 中樞傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="bd16a-152">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="bd16a-153">_傳送雲端到裝置_讓您可以傳送訊息 tooyour 裝置從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="bd16a-153">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="bd16a-154">設定您`IoT hub connection string`這個工具 toouse 內所有其功能。</span><span class="sxs-lookup"><span data-stu-id="bd16a-154">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="bd16a-155">IoT 中樞總管</span><span class="sxs-lookup"><span data-stu-id="bd16a-155">IoT hub Explorer</span></span>
<span data-ttu-id="bd16a-156">[IoT 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具 toomanage 裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="bd16a-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="bd16a-157">您可以使用 hello 身分識別登錄中的 hello 工具 toomanage hello 裝置、 監控裝置到雲端訊息和傳送雲端到裝置命令。</span><span class="sxs-lookup"><span data-stu-id="bd16a-157">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="bd16a-158">tooinstall hello 最新版本 （發行前版本） 的 hello iot 中樞總管工具，執行下列命令，命令列環境中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd16a-158">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="bd16a-159">您可以使用下列命令 tooget 所有相關的其他說明 hello iot 中樞總管命令和其參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="bd16a-159">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="bd16a-160">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bd16a-160">Azure portal</span></span>
<span data-ttu-id="bd16a-161">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="bd16a-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="bd16a-162">您也可以 toouse hello [Azure 入口網站](../azure-portal-overview.md)toohelp 佈建、 管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="bd16a-162">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="bd16a-163">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="bd16a-163">Azure storage issues</span></span>
<span data-ttu-id="bd16a-164">[Microsoft Azure 儲存體總管 （預覽）](http://storageexplorer.com)是獨立的應用程式，您可以使用與 toowork microsoft [Azure 儲存體](https://azure.microsoft.com/en-us/services/storage/)Windows、 macOS 和 Linux 上的資料。</span><span class="sxs-lookup"><span data-stu-id="bd16a-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="bd16a-165">使用此工具，您可以連接 tooyour 資料表，並查看 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="bd16a-165">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="bd16a-166">您可以使用此工具 tootroubleshoot 您 Azure 儲存體的問題。</span><span class="sxs-lookup"><span data-stu-id="bd16a-166">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd16a-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd16a-167">Next steps</span></span>
<span data-ttu-id="bd16a-168">此頁面只會包含 hello Intel Edison 套件的最常見的問題。</span><span class="sxs-lookup"><span data-stu-id="bd16a-168">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="bd16a-169">您也可以保留下註解 tooreport 問題，取得進一步的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="bd16a-169">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="bd16a-170">請返回太[Intel Edison (Node.js) 快速入門](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="bd16a-170">Go back too[Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started