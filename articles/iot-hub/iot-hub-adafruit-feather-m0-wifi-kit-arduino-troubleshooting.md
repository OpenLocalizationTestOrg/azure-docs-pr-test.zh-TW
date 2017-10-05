---
title: "將 Arduino (C) 連接到 Azure IoT - 疑難排解 | Microsoft Docs"
description: "Adafruit Feather M0 WiFi Arduino 經驗的疑難排解頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 疑難排解"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3bb369da9148300a80e7d351522a4d908e926996
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="d64ad-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="d64ad-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="d64ad-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="d64ad-105">Hardware issues</span></span>
<span data-ttu-id="d64ad-106">如需解決 Adafruit Feather M0 WiFi Arduino 面板上常見問題的詳細資訊，請參閱[官方疑難排解頁面](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq)。</span><span class="sxs-lookup"><span data-stu-id="d64ad-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see the [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="d64ad-107">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="d64ad-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="d64ad-108">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="d64ad-108">No response during gulp tasks</span></span>
<span data-ttu-id="d64ad-109">如果您遇到執行 gulp 工作的問題，您可以新增 `--verbose` 選項以進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="d64ad-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="d64ad-110">嘗試使用 `Ctrl + C` 終止目前的 gulp 工作，然後在主控台視窗中執行下列命令查看偵錯訊息。</span><span class="sxs-lookup"><span data-stu-id="d64ad-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="d64ad-111">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d64ad-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="d64ad-112">或者，您可以新增 `--listen` 來開啟序列連接埠，以輸出裝置記錄檔資訊。</span><span class="sxs-lookup"><span data-stu-id="d64ad-112">Or you can add `--listen` to open serial port to output device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="d64ad-113">NPM 問題</span><span class="sxs-lookup"><span data-stu-id="d64ad-113">NPM issues</span></span>
<span data-ttu-id="d64ad-114">嘗試使用下列命令更新您的 NPM 套件：</span><span class="sxs-lookup"><span data-stu-id="d64ad-114">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="d64ad-115">如果問題仍然存在，在本文結尾處留下您的意見，或在我們的[範例儲存機制][sample-repository]建立 GitHub 問題。</span><span class="sxs-lookup"><span data-stu-id="d64ad-115">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="d64ad-116">Azure-CLI 問題</span><span class="sxs-lookup"><span data-stu-id="d64ad-116">Azure-CLI issues</span></span>
<span data-ttu-id="d64ad-117">Azure 命令列介面 (Azure CLI) 是預覽組建。</span><span class="sxs-lookup"><span data-stu-id="d64ad-117">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="d64ad-118">在[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)中尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="d64ad-118">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="d64ad-119">當命令未如預期般運作時，請嘗試將 Azure-cli 升級至最新版本。</span><span class="sxs-lookup"><span data-stu-id="d64ad-119">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="d64ad-120">如果您遇到任何與工具有關的錯誤，請在 GitHub 儲存機制的**問題**一節中提出[問題](https://github.com/Azure/azure-cli/issues)。</span><span class="sxs-lookup"><span data-stu-id="d64ad-120">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="d64ad-121">如需針對常見問題進行疑難排解的說明，請參閱[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="d64ad-121">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="d64ad-122">如果您看到「找不到符合需求的版本」，請執行下列命令將 pip 升級至最新版本。</span><span class="sxs-lookup"><span data-stu-id="d64ad-122">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="d64ad-123">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="d64ad-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="d64ad-124">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="d64ad-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="d64ad-125">安裝 **pip** 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="d64ad-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="d64ad-126">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="d64ad-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="d64ad-127">先前安裝的某些 **pip** 套件是由根目錄建立，這會導致權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="d64ad-127">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="d64ad-128">解決方案是移除根目錄安裝的這些套件。</span><span class="sxs-lookup"><span data-stu-id="d64ad-128">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="d64ad-129">使用下列步驟以完成此工作：</span><span class="sxs-lookup"><span data-stu-id="d64ad-129">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="d64ad-130">請移至：/usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="d64ad-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="d64ad-131">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="d64ad-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="d64ad-132">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="d64ad-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="d64ad-133">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="d64ad-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="d64ad-134">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="d64ad-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="d64ad-135">如果您已使用 `azure-cli` 成功佈建 Azure IoT 中樞，而且您需要工具來管理連接到 IoT 中樞的裝置，請嘗試下列工具：</span><span class="sxs-lookup"><span data-stu-id="d64ad-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="d64ad-136">裝置總管</span><span class="sxs-lookup"><span data-stu-id="d64ad-136">Device Explorer</span></span>
<span data-ttu-id="d64ad-137">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)會在您的 Windows 本機機器上執行，並且連接至 Azure 中的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d64ad-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="d64ad-138">它會與下列 [IoT 中樞端點](iot-hub-devguide.md)通訊：</span><span class="sxs-lookup"><span data-stu-id="d64ad-138">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="d64ad-139">*裝置身分識別管理*以佈建和管理已向 IoT 中樞註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="d64ad-139">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="d64ad-140">*接收裝置到雲端*以便可以監視從裝置傳送到 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="d64ad-140">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="d64ad-141">*傳送裝置到雲端*以便可以從 IoT 中樞將訊息傳送至裝置。</span><span class="sxs-lookup"><span data-stu-id="d64ad-141">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="d64ad-142">在此工具內設定您的 `IoT hub connection string`以使用它的所有功能。</span><span class="sxs-lookup"><span data-stu-id="d64ad-142">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="d64ad-143">IoT 中樞總管</span><span class="sxs-lookup"><span data-stu-id="d64ad-143">IoT hub Explorer</span></span>
<span data-ttu-id="d64ad-144">[IoT 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具，可以管理裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="d64ad-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="d64ad-145">您可以使用此工具管理身分識別登錄中的裝置、監視裝置到雲端訊息，以及傳送雲端到裝置命令。</span><span class="sxs-lookup"><span data-stu-id="d64ad-145">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="d64ad-146">若要安裝最新 (發行前版本) 版本 iothub-explorer 工具，請在命令列環境中執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d64ad-146">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="d64ad-147">您可以使用下列命令取得所有 iothub-explorer 命令及其參數的額外說明：</span><span class="sxs-lookup"><span data-stu-id="d64ad-147">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="d64ad-148">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d64ad-148">Azure portal</span></span>
<span data-ttu-id="d64ad-149">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d64ad-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="d64ad-150">您可能也會想要使用 [Azure 入口網站](../azure-portal-overview.md)以協助佈建、管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d64ad-150">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="d64ad-151">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="d64ad-151">Azure storage issues</span></span>
<span data-ttu-id="d64ad-152">[Microsoft Azure 儲存體總管 (預覽)](http://storageexplorer.com) 是 Microsoft 所提供的獨立應用程式，可供您在 Windows、macOS 和 Linux 上處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="d64ad-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="d64ad-153">透過使用此工具，您可以連接到資料表，並查看其中的資料。</span><span class="sxs-lookup"><span data-stu-id="d64ad-153">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="d64ad-154">您可以使用這項工具，對 Azure 儲存體問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="d64ad-154">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md