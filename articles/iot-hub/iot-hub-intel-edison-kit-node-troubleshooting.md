---
title: "將 Intel Edison (節點) 連接到 Azure IoT - 第 4 課：疑難排解 | Microsoft Docs"
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
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="1ee0b-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="1ee0b-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="1ee0b-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="1ee0b-105">Hardware issues</span></span>
<span data-ttu-id="1ee0b-106">如需解決 Intel Edison 上常見問題的詳細資訊，請參閱[官方疑難排解頁面](https://software.intel.com/en-us/node/637974)。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="1ee0b-107">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="1ee0b-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="1ee0b-108">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="1ee0b-108">No response during gulp tasks</span></span>
<span data-ttu-id="1ee0b-109">如果您遇到執行 gulp 工作的問題，您可以新增 `--verbose` 選項以進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="1ee0b-110">嘗試使用 `Ctrl + C` 終止目前的 gulp 工作，然後在主控台視窗中執行下列命令查看偵錯訊息。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="1ee0b-111">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="1ee0b-112">NPM 問題</span><span class="sxs-lookup"><span data-stu-id="1ee0b-112">NPM issues</span></span>
<span data-ttu-id="1ee0b-113">嘗試使用下列命令更新您的 NPM 套件：</span><span class="sxs-lookup"><span data-stu-id="1ee0b-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="1ee0b-114">如果問題仍然存在，在本文結尾處留下您的意見，或在我們的[範例儲存機制][sample-repository]建立 GitHub 問題。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="1ee0b-115">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="1ee0b-115">Remote debugging</span></span>

### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="1ee0b-116">在偵錯模式中執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="1ee0b-116">Run the sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="1ee0b-117">偵錯引擎一旦就緒，您應該就能從主控台輸出看到 ```Debugger listening on port 5858```。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span></span>

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a><span data-ttu-id="1ee0b-118">設定 VS Code 以連接到遠端裝置</span><span class="sxs-lookup"><span data-stu-id="1ee0b-118">Configure VS Code to connect to the remote device</span></span>

<span data-ttu-id="1ee0b-119">從左側開啟 [偵錯] 面板。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-119">Open the **Debug** panel from the left side.</span></span>

<span data-ttu-id="1ee0b-120">按一下綠色的 [開始偵錯] \(F5) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-120">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="1ee0b-121">VS Code 會開啟 **launch.json** 檔案，您必須更新該檔案。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-121">VS Code would open a **launch.json** file, which you need to update.</span></span>

<span data-ttu-id="1ee0b-122">使用下列內容更新 **launch.json** 檔案，使用實際裝置的 IP 位址或主機名稱取代 `[device hostname or IP address]`。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span></span>  

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="1ee0b-124">附加至遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="1ee0b-124">Attach to the remote application</span></span>

<span data-ttu-id="1ee0b-125">按一下綠色的 [開始偵錯] \(F5) 按鈕，然後享受偵錯過程。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="1ee0b-126">您可以閱讀 [VS Code 中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) 以深入了解偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![遠端偵錯互動](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="1ee0b-128">Azure-CLI 問題</span><span class="sxs-lookup"><span data-stu-id="1ee0b-128">Azure-CLI issues</span></span>
<span data-ttu-id="1ee0b-129">Azure 命令列介面 (Azure CLI) 是預覽組建。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-129">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="1ee0b-130">在[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)中尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="1ee0b-131">當命令未如預期般運作時，請嘗試將 Azure-cli 升級至最新版本。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="1ee0b-132">如果您遇到任何與工具有關的錯誤，請在 GitHub 儲存機制的**問題**一節中提出[問題](https://github.com/Azure/azure-cli/issues)。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="1ee0b-133">如需針對常見問題進行疑難排解的說明，請參閱[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="1ee0b-134">如果您看到「找不到符合需求的版本」，請執行下列命令將 pip 升級至最新版本。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="1ee0b-135">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="1ee0b-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="1ee0b-136">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="1ee0b-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="1ee0b-137">安裝 **pip** 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="1ee0b-138">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="1ee0b-139">先前安裝的某些 **pip** 套件是由根目錄建立，這會導致權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="1ee0b-140">解決方案是移除根目錄安裝的這些套件。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-140">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="1ee0b-141">使用下列步驟以完成此工作：</span><span class="sxs-lookup"><span data-stu-id="1ee0b-141">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="1ee0b-142">請移至：/usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="1ee0b-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="1ee0b-143">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="1ee0b-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="1ee0b-144">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="1ee0b-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="1ee0b-145">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="1ee0b-146">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="1ee0b-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="1ee0b-147">如果您已使用 `azure-cli` 成功佈建 Azure IoT 中樞，而且您需要工具來管理連接到 IoT 中樞的裝置，請嘗試下列工具：</span><span class="sxs-lookup"><span data-stu-id="1ee0b-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="1ee0b-148">裝置總管</span><span class="sxs-lookup"><span data-stu-id="1ee0b-148">Device Explorer</span></span>
<span data-ttu-id="1ee0b-149">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)會在您的 Windows 本機機器上執行，並且連接至 Azure 中的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="1ee0b-150">它會與下列 [IoT 中樞端點](iot-hub-devguide.md)通訊：</span><span class="sxs-lookup"><span data-stu-id="1ee0b-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="1ee0b-151">_裝置身分識別管理_以佈建和管理已向 IoT 中樞註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="1ee0b-152">_接收裝置到雲端_以便可以監視從裝置傳送到 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="1ee0b-153">_傳送裝置到雲端_以便可以從 IoT 中樞將訊息傳送至裝置。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="1ee0b-154">在此工具內設定您的 `IoT hub connection string`以使用它的所有功能。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="1ee0b-155">IoT 中樞總管</span><span class="sxs-lookup"><span data-stu-id="1ee0b-155">IoT hub Explorer</span></span>
<span data-ttu-id="1ee0b-156">[IoT 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具，可以管理裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="1ee0b-157">您可以使用此工具管理身分識別登錄中的裝置、監視裝置到雲端訊息，以及傳送雲端到裝置命令。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="1ee0b-158">若要安裝最新 (發行前版本) 版本 iothub-explorer 工具，請在命令列環境中執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="1ee0b-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="1ee0b-159">您可以使用下列命令取得所有 iothub-explorer 命令及其參數的額外說明：</span><span class="sxs-lookup"><span data-stu-id="1ee0b-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="1ee0b-160">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1ee0b-160">Azure portal</span></span>
<span data-ttu-id="1ee0b-161">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="1ee0b-162">您可能也會想要使用 [Azure 入口網站](../azure-portal-overview.md)以協助佈建、管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="1ee0b-163">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="1ee0b-163">Azure storage issues</span></span>
<span data-ttu-id="1ee0b-164">[Microsoft Azure 儲存體總管 (預覽)](http://storageexplorer.com) 是 Microsoft 所提供的獨立應用程式，可供您在 Windows、macOS 和 Linux 上處理 [Azure 儲存體](https://azure.microsoft.com/en-us/services/storage/)資料。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="1ee0b-165">透過使用此工具，您可以連接到資料表，並查看其中的資料。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-165">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="1ee0b-166">您可以使用這項工具，對 Azure 儲存體問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-166">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ee0b-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ee0b-167">Next steps</span></span>
<span data-ttu-id="1ee0b-168">此頁面只包括 Intel Edison 套件最常見的問題。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-168">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="1ee0b-169">您也可以在底部留下註解來報告問題，以便進行進一步的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1ee0b-169">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="1ee0b-170">返回[開始使用 Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1ee0b-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started