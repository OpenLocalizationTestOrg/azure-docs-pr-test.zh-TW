---
title: "Connect Intel Edison (C) tooAzure IoT-疑難排解 |Microsoft 文件"
description: "Intel Edison C 經驗的疑難排解頁面"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 疑難排解"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c4a71983e3906cfc5ce7c832cf858852b9bd744a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="b3e5e-104">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b3e5e-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="b3e5e-105">硬體問題</span><span class="sxs-lookup"><span data-stu-id="b3e5e-105">Hardware issues</span></span>
<span data-ttu-id="b3e5e-106">如需解決 Intel Edison 中常見的問題資訊，請參閱 hello[正式的疑難排解頁面](https://software.intel.com/en-us/node/637974)。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="b3e5e-107">Node.js 套件問題</span><span class="sxs-lookup"><span data-stu-id="b3e5e-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="b3e5e-108">gulp 工作期間沒有回應</span><span class="sxs-lookup"><span data-stu-id="b3e5e-108">No response during gulp tasks</span></span>
<span data-ttu-id="b3e5e-109">如果您遇到執行 gulp 工作的問題，您可以新增 hello`--verbose`偵錯的選項。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="b3e5e-110">嘗試使用目前 gulp 工作 tooterminate `Ctrl + C`，然後執行的 hello 遵從在主控台視窗 toosee 偵錯訊息中的命令。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="b3e5e-111">您可能會在主控台輸出中看到詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="b3e5e-112">NPM 問題</span><span class="sxs-lookup"><span data-stu-id="b3e5e-112">NPM issues</span></span>
<span data-ttu-id="b3e5e-113">請嘗試 tooupdate NPM 封裝以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b3e5e-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="b3e5e-114">如果 hello 問題仍然存在，讓您在 hello 本文結尾的註解或建立 GitHub 問題我們[範例儲存機制][sample-repository]。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="b3e5e-115">Azure-CLI 問題</span><span class="sxs-lookup"><span data-stu-id="b3e5e-115">Azure-CLI issues</span></span>
<span data-ttu-id="b3e5e-116">hello Azure 命令列介面 (Azure CLI) 是預覽版。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-116">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="b3e5e-117">尋找方案中 hello[預覽安裝指南](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)tooseek 解決方案。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-117">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="b3e5e-118">當命令無法運作正常，再試一次 tooupgrade Azure cli toolatest 版本。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-118">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="b3e5e-119">如果您遇到任何錯誤的 hello 工具，[問題](https://github.com/Azure/azure-cli/issues)在 hello**問題**hello GitHub 儲存機制的區段。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-119">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="b3e5e-120">疑難排解一般問題的說明，請檢查 hello[讀我檔案](https://github.com/Azure/azure-cli/blob/master/README.rst)。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-120">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="b3e5e-121">如果您符合 「 找不到滿足 hello 需求的版本 」，請執行的 hello 下列的命令 tooupgrade pip toolastest 版本。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-121">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="b3e5e-122">Python 安裝問題</span><span class="sxs-lookup"><span data-stu-id="b3e5e-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="b3e5e-123">舊版安裝問題 (macOS)</span><span class="sxs-lookup"><span data-stu-id="b3e5e-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="b3e5e-124">安裝 **pip** 時，如果以 **su** 權限安裝舊版套件，則會擲回權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="b3e5e-125">之所以發生這個情況，是因為先前使用 brew (macOS) 所安裝的 Python 未完整解除安裝。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="b3e5e-126">某些**pip**從先前的安裝封裝所建立的根，會導致 hello 權限錯誤。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-126">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="b3e5e-127">hello 方案是 tooremove 由根安裝這些套件。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-127">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="b3e5e-128">使用下列步驟 toocomplete hello 這項工作：</span><span class="sxs-lookup"><span data-stu-id="b3e5e-128">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="b3e5e-129">請移至：/usr/local/lib/python2.7/site-packages</span><span class="sxs-lookup"><span data-stu-id="b3e5e-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="b3e5e-130">列出根目錄建立的套件：`ls -l | grep root`</span><span class="sxs-lookup"><span data-stu-id="b3e5e-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="b3e5e-131">從步驟 2 解除安裝套件：`sudo rm -rf {package name}`</span><span class="sxs-lookup"><span data-stu-id="b3e5e-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="b3e5e-132">重新安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="b3e5e-133">Azure IoT 中樞問題</span><span class="sxs-lookup"><span data-stu-id="b3e5e-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="b3e5e-134">如果您已成功佈建您的 Azure IoT 中樞與`azure-cli`，而且您需要連線 tooyour IoT 中樞，遵循工具再試一次 hello 工具 toomanage hello 裝置：</span><span class="sxs-lookup"><span data-stu-id="b3e5e-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="b3e5e-135">裝置總管</span><span class="sxs-lookup"><span data-stu-id="b3e5e-135">Device Explorer</span></span>
<span data-ttu-id="b3e5e-136">[裝置總管](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)Windows 本機電腦上執行並連接在 Azure 中的 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="b3e5e-137">它會與 hello 下列通訊[IoT 中樞端點](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="b3e5e-137">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="b3e5e-138">_裝置身分識別管理_tooprovision 和管理裝置與 IoT 中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-138">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="b3e5e-139">_接收裝置到雲端_讓您監視從您的裝置 tooyour IoT 中樞傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-139">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="b3e5e-140">_傳送雲端到裝置_讓您可以傳送訊息 tooyour 裝置從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-140">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="b3e5e-141">設定您`IoT hub connection string`這個工具 toouse 內所有其功能。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-141">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="b3e5e-142">IoT 中樞總管</span><span class="sxs-lookup"><span data-stu-id="b3e5e-142">IoT hub Explorer</span></span>
<span data-ttu-id="b3e5e-143">[IoT 中樞總管](https://github.com/Azure/iothub-explorer)是範例多平台 CLI 工具 toomanage 裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="b3e5e-144">您可以使用 hello 身分識別登錄中的 hello 工具 toomanage hello 裝置、 監控裝置到雲端訊息和傳送雲端到裝置命令。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-144">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="b3e5e-145">tooinstall hello 最新版本 （發行前版本） 的 hello iot 中樞總管工具，執行下列命令，命令列環境中的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3e5e-145">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="b3e5e-146">您可以使用下列命令 tooget 所有相關的其他說明 hello iot 中樞總管命令和其參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="b3e5e-146">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="b3e5e-147">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b3e5e-147">Azure portal</span></span>
<span data-ttu-id="b3e5e-148">完整的 CLI 體驗可協助您建立及管理您所有的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="b3e5e-149">您也可以 toouse hello [Azure 入口網站](../azure-portal-overview.md)toohelp 佈建、 管理和偵錯您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-149">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="b3e5e-150">Azure 儲存體問題</span><span class="sxs-lookup"><span data-stu-id="b3e5e-150">Azure storage issues</span></span>
<span data-ttu-id="b3e5e-151">[Microsoft Azure 儲存體總管 （預覽）](http://storageexplorer.com)是獨立的應用程式，您可以使用與 toowork microsoft [Azure 儲存體](https://azure.microsoft.com/en-us/services/storage/)Windows、 macOS 和 Linux 上的資料。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="b3e5e-152">使用此工具，您可以連接 tooyour 資料表，並查看 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-152">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="b3e5e-153">您可以使用此工具 tootroubleshoot 您 Azure 儲存體的問題。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-153">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3e5e-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3e5e-154">Next steps</span></span>
<span data-ttu-id="b3e5e-155">此頁面只會包含 hello Intel Edison 套件的最常見的問題。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-155">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="b3e5e-156">您也可以保留下註解 tooreport 問題，取得進一步的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b3e5e-156">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="b3e5e-157">請返回太[Intel Edison (C) 快速入門](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="b3e5e-157">Go back too[Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started