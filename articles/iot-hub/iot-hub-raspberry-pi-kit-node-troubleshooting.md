---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 疑難排解 | Microsoft Docs"
description: "Raspberry Pi Node.js 體驗的疑難排解頁面"
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
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="ba3c9-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="ba3c9-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="ba3c9-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="ba3c9-106">應用程式正確執行，但 LED 未閃爍</span><span class="sxs-lookup"><span data-stu-id="ba3c9-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="ba3c9-107">這個問題一律與硬體線路連接相關。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="ba3c9-108">使用下列步驟識別問題：</span><span class="sxs-lookup"><span data-stu-id="ba3c9-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="ba3c9-109">檢查您是否在您的板上選擇正確的 **GPIO**。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="ba3c9-110">兩個連接埠應該是 **GPIO GND (Pin 6)** 和 **GPIO 04 (Pin 7)**。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="ba3c9-111">檢查您的 LED 極性是否正確。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="ba3c9-112">較長的腳應該是**正極**，陽極針腳。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="ba3c9-113">在 Raspberry Pi 3 上使用 **3.3V Pin** 和 **GND Pin**。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="ba3c9-114">將 Pi 視為 DC 電源。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="ba3c9-115">檢查 LED 是否運作正常。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-115">Check that the LED works fine.</span></span>

![LED 規格](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="ba3c9-117">其他硬體問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-117">Other hardware issues</span></span>
<span data-ttu-id="ba3c9-118">如需解決 Raspberry Pi 3 上常見問題的詳細資訊，請參閱[官方疑難排解頁面](http://elinux.org/R-Pi_Troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="ba3c9-119">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="ba3c9-120">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="ba3c9-120">No response during gulp tasks</span></span>
<span data-ttu-id="ba3c9-121">如果您遇到執行 gulp 工作的問題，您可以新增 `--verbose` 選項以進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="ba3c9-122">嘗試使用 Ctrl + C 終止目前的 gulp 工作，然後在主控台視窗中執行下列命令，以查看偵錯訊息。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="ba3c9-123">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="ba3c9-124">裝置探索問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-124">Device discovery issues</span></span>
<span data-ttu-id="ba3c9-125">如需使用 `devdisco` 命令對常見問題進行疑難排解的說明，請參閱[讀我檔案](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md)。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="ba3c9-126">npm 問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-126">npm issues</span></span>
<span data-ttu-id="ba3c9-127">嘗試使用下列命令更新您的 npm 套件：</span><span class="sxs-lookup"><span data-stu-id="ba3c9-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="ba3c9-128">如果問題仍然存在，在本文結尾處留下您的意見，或在我們的[範例儲存機制](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started)建立 GitHub 問題。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="ba3c9-129">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="ba3c9-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="ba3c9-130">在偵錯模式中執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="ba3c9-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="ba3c9-131">偵錯引擎就緒時，您應該會在主控台輸出中看到```Debugger listening on port 5858```。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="ba3c9-132">設定 Visual Studio Code 以連接到遠端裝置</span><span class="sxs-lookup"><span data-stu-id="ba3c9-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="ba3c9-133">開啟左側的 [偵錯] 面板。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="ba3c9-134">按一下綠色的 [開始偵錯] \(F5) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="ba3c9-135">Visual Studio Code 會開啟 launch.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="ba3c9-136">使用下列內容更新 launch.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="ba3c9-137">將 `[device hostname or IP address]` 取代為實際裝置 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="ba3c9-138">若要深入了解 Visual Studio 偵錯，請參閱[在 Visual Studio Code 中偵錯](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes)。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="ba3c9-140">附加至遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="ba3c9-140">Attach to the remote application</span></span>
<span data-ttu-id="ba3c9-141">按一下綠色的 [開始偵錯] \(F5) 按鈕，以開始偵錯。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="ba3c9-142">請參閱 [VS Code 中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) 以深入了解偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![遠端偵錯互動](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="ba3c9-144">Azure CLI 問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-144">Azure CLI issues</span></span>
<span data-ttu-id="ba3c9-145">Azure 命令列介面 (Azure CLI) 是預覽組建。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="ba3c9-146">若要尋求解決方案，您可以使用[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="ba3c9-147">如果您遇到任何與工具有關的錯誤，請在 GitHub 儲存機制的**問題**一節中提出[問題](https://github.com/Azure/azure-cli/issues)。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="ba3c9-148">如需針對常見問題進行疑難排解的說明，請參閱[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="ba3c9-149">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="ba3c9-150">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="ba3c9-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="ba3c9-151">安裝 pip 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="ba3c9-152">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="ba3c9-153">先前安裝的某些 pip 套件是由根目錄建立，這會導致權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="ba3c9-154">解決方案是移除根目錄安裝的這些套件。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="ba3c9-155">使用下列步驟以完成此工作：</span><span class="sxs-lookup"><span data-stu-id="ba3c9-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="ba3c9-156">請移至：/usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="ba3c9-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="ba3c9-157">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="ba3c9-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="ba3c9-158">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="ba3c9-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="ba3c9-159">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="ba3c9-160">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="ba3c9-161">如果您已使用 Azure CLI 成功佈建 Azure IoT 中樞，而且您需要工具來管理連接到 IoT 中樞的裝置，請嘗試下列工具。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="ba3c9-162">裝置總管</span><span class="sxs-lookup"><span data-stu-id="ba3c9-162">Device explorer</span></span>
<span data-ttu-id="ba3c9-163">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)工具在您的 Windows 本機電腦上執行，並連接至 Azure 中的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="ba3c9-164">它會與下列 [IoT 中樞端點](iot-hub-devguide.md)通訊：</span><span class="sxs-lookup"><span data-stu-id="ba3c9-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="ba3c9-165">*裝置身分識別管理*以佈建和管理已向 IoT 中樞註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="ba3c9-166">*接收裝置到雲端*以便可以監視從裝置傳送到 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="ba3c9-167">*傳送裝置到雲端*以便可以從 IoT 中樞將訊息傳送至裝置。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="ba3c9-168">在此工具內設定 IoT 中樞連接字串以使用它的所有功能。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="ba3c9-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="ba3c9-169">iothub-explorer</span></span>
<span data-ttu-id="ba3c9-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) 是用來管理裝置的多平台 CLI 工具例子。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="ba3c9-171">您可以使用此工具管理身分識別登錄中的裝置、監視裝置到雲端訊息，以及傳送雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="ba3c9-172">若要安裝最新 (發行前版本) 版本 iothub-explorer 工具，請在命令列環境中執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ba3c9-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="ba3c9-173">您可以使用下列命令取得所有 iothub-explorer 命令及其參數的額外說明：</span><span class="sxs-lookup"><span data-stu-id="ba3c9-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="ba3c9-174">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ba3c9-174">Azure portal</span></span>
<span data-ttu-id="ba3c9-175">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="ba3c9-176">您可能也會想要使用 [Azure 入口網站](../azure-portal-overview.md)以協助佈建、管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="ba3c9-177">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="ba3c9-177">Azure Storage issues</span></span>
<span data-ttu-id="ba3c9-178">[Microsoft Azure 儲存體總管 (預覽)](http://storageexplorer.com) 是 Microsoft 所提供的獨立應用程式，可供您在 Windows、macOS 和 Linux 上處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="ba3c9-179">透過使用此工具，您可以連接到資料表，並查看其中的資料。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="ba3c9-180">您可以使用這項工具，對 Azure 儲存體問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="ba3c9-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

