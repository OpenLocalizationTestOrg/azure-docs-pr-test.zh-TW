---
title: "Connect Raspberry Pi (C) tooAzure IoT-疑難排解 |Microsoft 文件"
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
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="5a9c4-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5a9c4-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="5a9c4-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="5a9c4-106">hello 應用程式也會執行，但 hello LED 閃爍不</span><span class="sxs-lookup"><span data-stu-id="5a9c4-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="5a9c4-107">此問題，一律為相關的 toohello 硬體電路連線。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="5a9c4-108">使用下列步驟 tooidentify 問題 hello。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="5a9c4-109">請檢查您已選擇正確的 hello **GPIO**在面板。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="5a9c4-110">hello 兩個連接埠應**GPIO GND (Pin 6)**和**GPIO 04 (Pin 7)**。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="5a9c4-111">請檢查您的 LED hello 極性正確。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="5a9c4-112">hello 長腳應該指出 hello**正數**，anode pin。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="5a9c4-113">使用 hello **3.3V 釘選**和**GND Pin**覆盆子 Pi 3 為基礎。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="5a9c4-114">Pi 視為 hello DC 電源。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="5a9c4-115">請檢查該 hello LED 可正常運作。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-115">Check that hello LED works fine.</span></span>

![LED 規格](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="5a9c4-117">其他硬體問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-117">Other hardware issues</span></span>
<span data-ttu-id="5a9c4-118">如需解決常見的問題，在覆盆子 Pi 3 上的資訊，請參閱 hello[正式的疑難排解頁面](http://elinux.org/R-Pi_Troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="5a9c4-119">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="5a9c4-120">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="5a9c4-120">No response during gulp tasks</span></span>
<span data-ttu-id="5a9c4-121">如果您遇到執行 gulp 工作的問題，您可以新增 hello`--verbose`偵錯的選項。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="5a9c4-122">嘗試使用目前 gulp 工作 tooterminate `Ctrl + C`，然後執行的 hello 遵從在主控台視窗 toosee 偵錯訊息中的命令。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="5a9c4-123">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="5a9c4-124">裝置探索問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-124">Device discovery issues</span></span>
<span data-ttu-id="5a9c4-125">如需協助疑難排解常見問題 hello`devdisco`命令，檢查 hello[讀我檔案](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md)。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="5a9c4-126">NPM 問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-126">NPM issues</span></span>
<span data-ttu-id="5a9c4-127">請嘗試 tooupdate NPM 封裝以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="5a9c4-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="5a9c4-128">如果 hello 問題仍然存在，讓您在 hello 本文結尾的註解或建立 GitHub 問題我們[範例儲存機制](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="5a9c4-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="5a9c4-129">遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="5a9c4-129">Remote debugging</span></span>

<span data-ttu-id="5a9c4-130">Visual Studio Code C/C++ Extension 中即將提供遠端偵錯支援。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="5a9c4-131">目前，您可以透過您慣用 SSH 終端機來使用 GDB︰</span><span class="sxs-lookup"><span data-stu-id="5a9c4-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="5a9c4-132">Azure-CLI 問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-132">Azure-CLI issues</span></span>
<span data-ttu-id="5a9c4-133">hello Azure 命令列介面 (Azure CLI) 是預覽版。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="5a9c4-134">尋找方案中 hello[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)tooseek 解決方案。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="5a9c4-135">當命令無法運作正常，再試一次 tooupgrade Azure cli toolatest 版本。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="5a9c4-136">如果您遇到任何錯誤的 hello 工具，[問題](https://github.com/Azure/azure-cli/issues)在 hello**問題**hello GitHub 儲存機制的區段。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="5a9c4-137">疑難排解一般問題的說明，請檢查 hello[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="5a9c4-138">如果您符合 「 找不到滿足 hello 需求的版本 」，請執行的 hello 下列的命令 tooupgrade pip toolastest 版本。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="5a9c4-139">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="5a9c4-140">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="5a9c4-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="5a9c4-141">安裝 **pip** 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="5a9c4-142">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="5a9c4-143">某些**pip**從先前的安裝封裝所建立的根，會導致 hello 權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="5a9c4-144">hello 方案是 tooremove 由根安裝這些套件。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="5a9c4-145">使用下列步驟 toocomplete hello 這項工作：</span><span class="sxs-lookup"><span data-stu-id="5a9c4-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="5a9c4-146">請移至：/usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="5a9c4-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="5a9c4-147">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="5a9c4-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="5a9c4-148">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="5a9c4-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="5a9c4-149">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="5a9c4-150">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="5a9c4-151">如果您已成功佈建您的 Azure IoT 中樞與`azure-cli`，而且您需要連線 tooyour IoT 中樞，遵循工具再試一次 hello 工具 toomanage hello 裝置：</span><span class="sxs-lookup"><span data-stu-id="5a9c4-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="5a9c4-152">裝置總管</span><span class="sxs-lookup"><span data-stu-id="5a9c4-152">Device Explorer</span></span>
<span data-ttu-id="5a9c4-153">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer)Windows 本機電腦上執行並連接在 Azure 中的 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="5a9c4-154">它會與 hello 下列通訊[IoT 中樞端點](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="5a9c4-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="5a9c4-155">*裝置身分識別管理*tooprovision 和管理裝置與 IoT 中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="5a9c4-156">*接收裝置到雲端*讓您監視從您的裝置 tooyour IoT 中樞傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="5a9c4-157">*傳送雲端到裝置*讓您可以傳送訊息 tooyour 裝置從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="5a9c4-158">設定您`IoT hub connection string`這個工具 toouse 內所有其功能。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="5a9c4-159">IoT 中樞總管</span><span class="sxs-lookup"><span data-stu-id="5a9c4-159">IoT hub Explorer</span></span>
<span data-ttu-id="5a9c4-160">[IoT 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具 toomanage 裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="5a9c4-161">您可以使用 hello 身分識別登錄中的 hello 工具 toomanage hello 裝置、 監控裝置到雲端訊息和傳送雲端到裝置命令。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="5a9c4-162">tooinstall hello 最新版本 （發行前版本） 的 hello iot 中樞總管工具，執行下列命令，命令列環境中的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a9c4-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="5a9c4-163">您可以使用下列命令 tooget 所有相關的其他說明 hello iot 中樞總管命令和其參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a9c4-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="5a9c4-164">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5a9c4-164">Azure portal</span></span>
<span data-ttu-id="5a9c4-165">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="5a9c4-166">您也可以 toouse hello [Azure 入口網站](../azure-portal-overview.md)toohelp 佈建、 管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="5a9c4-167">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="5a9c4-167">Azure storage issues</span></span>
<span data-ttu-id="5a9c4-168">[Microsoft Azure 儲存體總管 （預覽）](http://storageexplorer.com)是獨立應用程式，microsoft 可讓您 toowork Windows、 macOS 和 Linux 的 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="5a9c4-169">使用此工具，您可以連接 tooyour 資料表，並查看 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="5a9c4-170">您可以使用此工具 tootroubleshoot 您 Azure 儲存體的問題。</span><span class="sxs-lookup"><span data-stu-id="5a9c4-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
