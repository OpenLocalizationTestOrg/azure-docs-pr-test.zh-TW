---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 疑難排解 | Microsoft Docs"
description: "Raspberry Pi Node.js 體驗的疑難排解頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 問題, 物聯網問題"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 828669db23fa8d608029134fbe364033456d935a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="59fcc-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="59fcc-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="59fcc-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="59fcc-106">應用程式正確執行，但 LED 未閃爍</span><span class="sxs-lookup"><span data-stu-id="59fcc-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="59fcc-107">這個問題一律與硬體線路連接相關。</span><span class="sxs-lookup"><span data-stu-id="59fcc-107">This issue is always related to the hardware circuit connectivity.</span></span> <span data-ttu-id="59fcc-108">使用下列步驟識別問題。</span><span class="sxs-lookup"><span data-stu-id="59fcc-108">Use the following steps to identify problems.</span></span>

1. <span data-ttu-id="59fcc-109">檢查您是否在您的板上選擇正確的 **GPIO**。</span><span class="sxs-lookup"><span data-stu-id="59fcc-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="59fcc-110">兩個連接埠應該是 **GPIO GND (Pin 6)** 和 **GPIO 04 (Pin 7)**。</span><span class="sxs-lookup"><span data-stu-id="59fcc-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="59fcc-111">檢查您的 LED 極性是否正確。</span><span class="sxs-lookup"><span data-stu-id="59fcc-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="59fcc-112">較長的腳應該是**正極**，陽極針腳。</span><span class="sxs-lookup"><span data-stu-id="59fcc-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="59fcc-113">在 Raspberry Pi 3 上使用 **3.3V Pin** 和 **GND Pin**。</span><span class="sxs-lookup"><span data-stu-id="59fcc-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="59fcc-114">將 Pi 視為 DC 電源。</span><span class="sxs-lookup"><span data-stu-id="59fcc-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="59fcc-115">檢查 LED 是否運作正常。</span><span class="sxs-lookup"><span data-stu-id="59fcc-115">Check that the LED works fine.</span></span>

![LED 規格](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="59fcc-117">其他硬體問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-117">Other hardware issues</span></span>
<span data-ttu-id="59fcc-118">如需解決 Raspberry Pi 3 上常見問題的詳細資訊，請參閱[官方疑難排解頁面](http://elinux.org/R-Pi_Troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="59fcc-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="59fcc-119">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="59fcc-120">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="59fcc-120">No response during gulp tasks</span></span>
<span data-ttu-id="59fcc-121">如果您遇到執行 gulp 工作的問題，您可以新增 `--verbose` 選項以進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="59fcc-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="59fcc-122">嘗試使用 `Ctrl + C` 終止目前的 gulp 工作，然後在主控台視窗中執行下列命令查看偵錯訊息。</span><span class="sxs-lookup"><span data-stu-id="59fcc-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="59fcc-123">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="59fcc-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="59fcc-124">裝置探索問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-124">Device discovery issues</span></span>
<span data-ttu-id="59fcc-125">如需使用 `devdisco` 命令對常見問題進行疑難排解的說明，請參閱[讀我檔案](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md)。</span><span class="sxs-lookup"><span data-stu-id="59fcc-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="59fcc-126">NPM 問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-126">NPM issues</span></span>
<span data-ttu-id="59fcc-127">嘗試使用下列命令更新您的 NPM 套件：</span><span class="sxs-lookup"><span data-stu-id="59fcc-127">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="59fcc-128">如果問題仍然存在，請在本文結尾處留下您的意見，或在我們的[範例儲存機制](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)提出 GitHub 問題。</span><span class="sxs-lookup"><span data-stu-id="59fcc-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="59fcc-129">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="59fcc-129">Remote debugging</span></span>

<span data-ttu-id="59fcc-130">Visual Studio Code C/C++ Extension 中即將提供遠端偵錯支援。</span><span class="sxs-lookup"><span data-stu-id="59fcc-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="59fcc-131">目前，您可以透過您慣用 SSH 終端機來使用 GDB︰</span><span class="sxs-lookup"><span data-stu-id="59fcc-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="59fcc-132">Azure-CLI 問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-132">Azure-CLI issues</span></span>
<span data-ttu-id="59fcc-133">Azure 命令列介面 (Azure CLI) 是預覽組建。</span><span class="sxs-lookup"><span data-stu-id="59fcc-133">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="59fcc-134">在[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)中尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="59fcc-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="59fcc-135">當命令未如預期般運作時，請嘗試將 Azure-cli 升級至最新版本。</span><span class="sxs-lookup"><span data-stu-id="59fcc-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="59fcc-136">如果您遇到任何與工具有關的錯誤，請在 GitHub 儲存機制的**問題**一節中提出[問題](https://github.com/Azure/azure-cli/issues)。</span><span class="sxs-lookup"><span data-stu-id="59fcc-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="59fcc-137">如需針對常見問題進行疑難排解的說明，請參閱[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="59fcc-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="59fcc-138">如果您看到「找不到符合需求的版本」，請執行下列命令將 pip 升級至最新版本。</span><span class="sxs-lookup"><span data-stu-id="59fcc-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="59fcc-139">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="59fcc-140">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="59fcc-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="59fcc-141">安裝 **pip** 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="59fcc-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="59fcc-142">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="59fcc-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="59fcc-143">先前安裝的某些 **pip** 套件是由根目錄建立，這會導致權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="59fcc-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="59fcc-144">解決方案是移除根目錄安裝的這些套件。</span><span class="sxs-lookup"><span data-stu-id="59fcc-144">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="59fcc-145">使用下列步驟以完成此工作：</span><span class="sxs-lookup"><span data-stu-id="59fcc-145">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="59fcc-146">請移至：/usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="59fcc-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="59fcc-147">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="59fcc-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="59fcc-148">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="59fcc-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="59fcc-149">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="59fcc-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="59fcc-150">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="59fcc-151">如果您已使用 `azure-cli` 成功佈建 Azure IoT 中樞，而且您需要工具來管理連接到 IoT 中樞的裝置，請嘗試下列工具：</span><span class="sxs-lookup"><span data-stu-id="59fcc-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="59fcc-152">裝置總管</span><span class="sxs-lookup"><span data-stu-id="59fcc-152">Device Explorer</span></span>
<span data-ttu-id="59fcc-153">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)會在您的 Windows 本機機器上執行，並且連接至 Azure 中的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="59fcc-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="59fcc-154">它會與下列 [IoT 中樞端點](iot-hub-devguide.md)通訊：</span><span class="sxs-lookup"><span data-stu-id="59fcc-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="59fcc-155">*裝置身分識別管理*以佈建和管理已向 IoT 中樞註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="59fcc-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="59fcc-156">*接收裝置到雲端*以便可以監視從裝置傳送到 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="59fcc-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="59fcc-157">*傳送裝置到雲端*以便可以從 IoT 中樞將訊息傳送至裝置。</span><span class="sxs-lookup"><span data-stu-id="59fcc-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="59fcc-158">在此工具內設定您的 `IoT hub connection string`以使用它的所有功能。</span><span class="sxs-lookup"><span data-stu-id="59fcc-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="59fcc-159">IoT 中樞總管</span><span class="sxs-lookup"><span data-stu-id="59fcc-159">IoT hub Explorer</span></span>
<span data-ttu-id="59fcc-160">[IoT 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具，可以管理裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="59fcc-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="59fcc-161">您可以使用此工具管理身分識別登錄中的裝置、監視裝置到雲端訊息，以及傳送雲端到裝置命令。</span><span class="sxs-lookup"><span data-stu-id="59fcc-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="59fcc-162">若要安裝最新 (發行前版本) 版本 iothub-explorer 工具，請在命令列環境中執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="59fcc-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="59fcc-163">您可以使用下列命令取得所有 iothub-explorer 命令及其參數的額外說明：</span><span class="sxs-lookup"><span data-stu-id="59fcc-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="59fcc-164">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="59fcc-164">Azure portal</span></span>
<span data-ttu-id="59fcc-165">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="59fcc-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="59fcc-166">您可能也會想要使用 [Azure 入口網站](../azure-portal-overview.md)以協助佈建、管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="59fcc-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="59fcc-167">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="59fcc-167">Azure storage issues</span></span>
<span data-ttu-id="59fcc-168">[Microsoft Azure 儲存體總管 (預覽)](http://storageexplorer.com) 是 Microsoft 所提供的獨立應用程式，可供您在 Windows、macOS 和 Linux 上處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="59fcc-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="59fcc-169">透過使用此工具，您可以連接到資料表，並查看其中的資料。</span><span class="sxs-lookup"><span data-stu-id="59fcc-169">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="59fcc-170">您可以使用這項工具，對 Azure 儲存體問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="59fcc-170">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
