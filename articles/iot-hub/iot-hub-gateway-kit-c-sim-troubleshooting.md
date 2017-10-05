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
ms.openlocfilehash: eae4c112accaefa8bd1bf85f7b43badc2f491dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="dce7e-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="dce7e-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="dce7e-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="dce7e-106">無法連線至 TI SensorTag</span><span class="sxs-lookup"><span data-stu-id="dce7e-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="dce7e-107">若要針對 SensorTag 連線問題進行疑難排解，請使用 [SensorTag 應用程式](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide)。</span><span class="sxs-lookup"><span data-stu-id="dce7e-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="dce7e-108">Intel NUC 有問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="dce7e-109">若要疑難排解啟動問題，請參閱[針對 Intel NUC 沒有開機的問題進行疑難排解](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html)。</span><span class="sxs-lookup"><span data-stu-id="dce7e-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="dce7e-110">若要疑難排解作業系統問題，請參閱[針對 Intel NUC 的作業系統問題進行疑難排解](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html)。</span><span class="sxs-lookup"><span data-stu-id="dce7e-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="dce7e-111">若要疑難排解其他問題，請參閱 [Intel NUC 的閃爍代碼和嗶聲代碼](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html)。</span><span class="sxs-lookup"><span data-stu-id="dce7e-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="dce7e-112">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="dce7e-113">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="dce7e-113">No response during gulp tasks</span></span>

<span data-ttu-id="dce7e-114">如果您遇到執行 gulp 工作的問題，您可以新增 `--verbose` 選項以進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="dce7e-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="dce7e-115">嘗試使用 `Ctrl + C` 終止目前的 gulp 工作，然後在主控台視窗中執行下列命令查看偵錯訊息。</span><span class="sxs-lookup"><span data-stu-id="dce7e-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="dce7e-116">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="dce7e-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="dce7e-117">裝置探索問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-117">Device discovery issues</span></span>

<span data-ttu-id="dce7e-118">如需使用 `discover-sensortag` 命令對常見問題進行疑難排解的說明，請參閱 [wiki 頁面](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl)。</span><span class="sxs-lookup"><span data-stu-id="dce7e-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="dce7e-119">npm 問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-119">npm issues</span></span>

<span data-ttu-id="dce7e-120">嘗試執行下列命令更新您的 npm 套件：</span><span class="sxs-lookup"><span data-stu-id="dce7e-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="dce7e-121">如果問題仍然存在，在本文結尾處留下您的意見，或在我們的[範例儲存機制](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started)建立 GitHub 問題。</span><span class="sxs-lookup"><span data-stu-id="dce7e-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="dce7e-122">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="dce7e-122">Remote Debugging</span></span>
> <span data-ttu-id="dce7e-123">下面的指示是用於針對本教學課程中使用的 node.js 指令碼偵錯。</span><span class="sxs-lookup"><span data-stu-id="dce7e-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="dce7e-124">在偵錯模式中執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="dce7e-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="dce7e-125">執行下列命令在偵錯模式中執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="dce7e-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="dce7e-126">偵錯引擎就緒時，您應該會在主控台輸出中看到`Debugger listening on port 5858`。</span><span class="sxs-lookup"><span data-stu-id="dce7e-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="dce7e-127">設定 Visual Studio Code 以連接到遠端裝置</span><span class="sxs-lookup"><span data-stu-id="dce7e-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="dce7e-128">開啟左側的 [偵錯] 面板。</span><span class="sxs-lookup"><span data-stu-id="dce7e-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="dce7e-129">按一下綠色的 [開始偵錯] \(F5) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dce7e-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="dce7e-130">Visual Studio Code 會開啟 `launch.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="dce7e-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="dce7e-131">更新 `launch.json` 檔案的下列內容。</span><span class="sxs-lookup"><span data-stu-id="dce7e-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="dce7e-132">將 `[device hostname or IP address]` 取代為實際裝置 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="dce7e-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="dce7e-134">附加至遠端應用程式</span><span class="sxs-lookup"><span data-stu-id="dce7e-134">Attach to the remote application</span></span>

<span data-ttu-id="dce7e-135">按一下綠色的 [開始偵錯] \(F5) 按鈕，以開始偵錯。</span><span class="sxs-lookup"><span data-stu-id="dce7e-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="dce7e-136">請參閱 [VS Code 中的 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) 以深入了解偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="dce7e-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![偵錯 BLE 範例](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="dce7e-138">Azure CLI 問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-138">Azure CLI issues</span></span>

<span data-ttu-id="dce7e-139">Azure 命令列介面 (Azure CLI) 是預覽組建。</span><span class="sxs-lookup"><span data-stu-id="dce7e-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="dce7e-140">若要尋求解決方案，您可以使用[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)。</span><span class="sxs-lookup"><span data-stu-id="dce7e-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="dce7e-141">如果您遇到任何與工具有關的錯誤，請在 GitHub 儲存機制的**問題**一節中提出[問題](https://github.com/Azure/azure-cli/issues)。</span><span class="sxs-lookup"><span data-stu-id="dce7e-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="dce7e-142">如需針對常見問題進行疑難排解的說明，請參閱[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="dce7e-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="dce7e-143">如果您看到「找不到符合需求的版本」，請執行下列命令將 pip 升級至最新版本。</span><span class="sxs-lookup"><span data-stu-id="dce7e-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="dce7e-144">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="dce7e-145">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="dce7e-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="dce7e-146">安裝 pip 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="dce7e-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="dce7e-147">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="dce7e-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="dce7e-148">先前安裝的某些 pip 套件是由根目錄建立，這會導致權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="dce7e-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="dce7e-149">解決方案是移除根目錄安裝的這些套件。</span><span class="sxs-lookup"><span data-stu-id="dce7e-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="dce7e-150">使用下列步驟以完成此工作：</span><span class="sxs-lookup"><span data-stu-id="dce7e-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="dce7e-151">移至 `/usr/local/lib/python2.7/site-packages`。</span><span class="sxs-lookup"><span data-stu-id="dce7e-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="dce7e-152">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="dce7e-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="dce7e-153">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="dce7e-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="dce7e-154">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="dce7e-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="dce7e-155">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="dce7e-156">如果您已使用 Azure CLI 成功佈建 Azure IoT 中樞，而且您需要工具來管理連接到 IoT 中樞的裝置，請嘗試下列工具。</span><span class="sxs-lookup"><span data-stu-id="dce7e-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="dce7e-157">裝置總管</span><span class="sxs-lookup"><span data-stu-id="dce7e-157">Device Explorer</span></span>

<span data-ttu-id="dce7e-158">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)會在您的 Windows 本機機器上執行，並且連接至 Azure 中的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dce7e-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="dce7e-159">它會與下列 [IoT 中樞端點](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/)通訊：</span><span class="sxs-lookup"><span data-stu-id="dce7e-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="dce7e-160">裝置身分識別管理，以佈建和管理 IoT 中樞已登錄的裝置。</span><span class="sxs-lookup"><span data-stu-id="dce7e-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="dce7e-161">接收裝置到雲端，以便可以監視從裝置傳送到 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="dce7e-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="dce7e-162">傳送裝置到雲端，以便可以從 IoT 中樞將訊息傳送至裝置。</span><span class="sxs-lookup"><span data-stu-id="dce7e-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="dce7e-163">在此工具內設定 IoT 中樞連接字串以使用它的所有功能。</span><span class="sxs-lookup"><span data-stu-id="dce7e-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="dce7e-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="dce7e-164">iothub-explorer</span></span>

<span data-ttu-id="dce7e-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) 是範例多平台 CLI 工具，可以管理裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="dce7e-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="dce7e-166">您可以使用此工具管理身分識別登錄中的裝置、監視裝置到雲端訊息，以及傳送雲端到裝置命令。</span><span class="sxs-lookup"><span data-stu-id="dce7e-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="dce7e-167">若要安裝最新 (發行前版本) 版本的 iothub-explorer 工具，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="dce7e-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="dce7e-168">若要取得所有 iothub-explorer 命令及其參數的額外說明，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="dce7e-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="dce7e-169">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dce7e-169">The Azure portal</span></span>

<span data-ttu-id="dce7e-170">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="dce7e-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="dce7e-171">您可能也會想要使用 [Azure 入口網站](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/)以協助佈建、管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="dce7e-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="dce7e-172">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="dce7e-172">Azure Storage issues</span></span>

<span data-ttu-id="dce7e-173">[Microsoft Azure 儲存體總管 (預覽)](http://storageexplorer.com/) 是 Microsoft 所提供的獨立應用程式，可供您在 Windows、macOS 和 Linux 上處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="dce7e-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="dce7e-174">透過使用此工具，您可以連接到資料表，並查看其中的資料。</span><span class="sxs-lookup"><span data-stu-id="dce7e-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="dce7e-175">您可以使用這項工具，對 Azure 儲存體問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="dce7e-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
