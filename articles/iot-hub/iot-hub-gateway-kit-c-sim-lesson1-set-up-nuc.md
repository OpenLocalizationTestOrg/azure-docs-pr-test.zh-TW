---
title: "模擬裝置與 Azure IoT 閘道 - 第 1 課：設定 NUC | Microsoft Docs"
description: "設定 Intel NUC toowork 為 IoT 閘道之間的感應器和 Azure IoT 中樞 toocollect 感應器資訊，以傳送 tooIoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: "iot 閘道, intel nuc, nuc 電腦, DE3815TYKE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="3f572-104">將 Intel NUC 設定為 IoT 閘道器</span><span class="sxs-lookup"><span data-stu-id="3f572-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3f572-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="3f572-105">What you will do</span></span>

- <span data-ttu-id="3f572-106">將 Intel NUC 設定為 IoT 閘道器。</span><span class="sxs-lookup"><span data-stu-id="3f572-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="3f572-107">Intel NUC 上安裝 hello Azure IoT 邊緣套件。</span><span class="sxs-lookup"><span data-stu-id="3f572-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="3f572-108">在 Intel NUC tooverify hello 閘道功能上執行"hello_world 」 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f572-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="3f572-109">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="3f572-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3f572-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="3f572-110">What you will learn</span></span>

<span data-ttu-id="3f572-111">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="3f572-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="3f572-112">如何 tooconnect Intel NUC 與週邊設備。</span><span class="sxs-lookup"><span data-stu-id="3f572-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="3f572-113">如何在使用 Intel NUC tooinstall 和更新所需的 hello 封裝 hello 智慧套件管理員。</span><span class="sxs-lookup"><span data-stu-id="3f572-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="3f572-114">如何 toorun hello"hello_world 」 的範例應用程式 tooverify hello 閘道功能。</span><span class="sxs-lookup"><span data-stu-id="3f572-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3f572-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="3f572-115">What you need</span></span>

- <span data-ttu-id="3f572-116">以 hello Intel IoT 閘道軟體套件 Intel NUC 套件 DE3815TYKE (Wind 河 Linux * 7.0.0.13) 預先安裝。</span><span class="sxs-lookup"><span data-stu-id="3f572-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="3f572-117">乙太網路連接線。</span><span class="sxs-lookup"><span data-stu-id="3f572-117">An Ethernet cable.</span></span>
- <span data-ttu-id="3f572-118">鍵盤。</span><span class="sxs-lookup"><span data-stu-id="3f572-118">A keyboard.</span></span>
- <span data-ttu-id="3f572-119">HDMI 或 VGA 連接線。</span><span class="sxs-lookup"><span data-stu-id="3f572-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="3f572-120">具有 HDMI 或 VGA 連接埠的螢幕。</span><span class="sxs-lookup"><span data-stu-id="3f572-120">A monitor with an HDMI or VGA port.</span></span>

![閘道器套件](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="3f572-122">與 hello 週邊設備連接 Intel NUC</span><span class="sxs-lookup"><span data-stu-id="3f572-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="3f572-123">hello 圖是 Intel NUC 會連接到各種週邊設備的範例：</span><span class="sxs-lookup"><span data-stu-id="3f572-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="3f572-124">連接的 tooa 鍵盤。</span><span class="sxs-lookup"><span data-stu-id="3f572-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="3f572-125">連接 toohello 監視器 VGA 纜線或 HDMI 纜線。</span><span class="sxs-lookup"><span data-stu-id="3f572-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="3f572-126">透過乙太網路纜線有線網路連線的 tooa。</span><span class="sxs-lookup"><span data-stu-id="3f572-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="3f572-127">使用電源纜線連接的 toohello 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="3f572-127">Connected toohello power supply with a power cable.</span></span>

![Intel NUC 連接 tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="3f572-129">從主機電腦透過安全殼層 (SSH) 連線 toohello Intel NUC 系統</span><span class="sxs-lookup"><span data-stu-id="3f572-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="3f572-130">您需要在這裡鍵盤與監視器 tooget hello IP NUC 裝置位址。</span><span class="sxs-lookup"><span data-stu-id="3f572-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="3f572-131">如果您已經知道 hello IP 位址，您可以略過 toostep 3 這一節。</span><span class="sxs-lookup"><span data-stu-id="3f572-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="3f572-132">開啟 Intel NUC 按 hello 系統中的 hello 電源按鈕和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3f572-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="3f572-133">hello 預設使用者名稱和密碼都`root`。</span><span class="sxs-lookup"><span data-stu-id="3f572-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="3f572-134">藉由執行 hello 取得 NUC hello IP 位址`ifconfig`命令。</span><span class="sxs-lookup"><span data-stu-id="3f572-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="3f572-135">Hello NUC 裝置上執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="3f572-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="3f572-136">以下是 hello 命令輸出的範例。</span><span class="sxs-lookup"><span data-stu-id="3f572-136">Here is an example of hello command output.</span></span>

   ![ifconfig 輸出顯示 NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="3f572-138">在此範例中，hello 值後面`inet addr:`是您計劃從主機電腦 tooIntel NUC 遠端 tooconnect 時，您需要的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3f572-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="3f572-139">使用其中一種您主機機器 tooconnect tooIntel NUC 中的下列 SSH 用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="3f572-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="3f572-140">[PuTTY](http://www.putty.org/) 適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="3f572-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="3f572-141">hello 內建 SSH 用戶端上 Ubuntu 或 macOS。</span><span class="sxs-lookup"><span data-stu-id="3f572-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="3f572-142">它是更有效率且更有生產力 toooperate Intel NUC 上的從主機電腦。</span><span class="sxs-lookup"><span data-stu-id="3f572-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="3f572-143">您需要 hello hello IP 位址、 使用者名稱和密碼 tooconnect hello NUC 透過 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3f572-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="3f572-144">以下是範例使用 SSH 用戶端 hello macOS 上。</span><span class="sxs-lookup"><span data-stu-id="3f572-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="3f572-145">![在 macOS 上執行的 SSH 用戶端](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="3f572-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="3f572-146">安裝 hello Azure IoT 邊緣套件</span><span class="sxs-lookup"><span data-stu-id="3f572-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="3f572-147">hello Azure IoT 邊緣封裝包含的 hello SDK hello 預先編譯的二進位檔和其相依性。</span><span class="sxs-lookup"><span data-stu-id="3f572-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="3f572-148">這些二進位檔是 Azure IoT 邊緣、 hello Azure IoT SDK 和 hello 對應工具。</span><span class="sxs-lookup"><span data-stu-id="3f572-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="3f572-149">hello 封裝也包含 「 hello_world 」 範例應用程式所使用的 toovalidate hello 閘道功能。</span><span class="sxs-lookup"><span data-stu-id="3f572-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="3f572-150">IoT 邊緣屬於 hello 核心 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="3f572-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="3f572-151">tooinstall hello 封裝，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3f572-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="3f572-152">加入 hello IoT 雲端儲存機制，藉由執行下列命令在 terminal 視窗中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3f572-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="3f572-153">hello`rpm`命令匯入 hello rpm 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3f572-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="3f572-154">hello`smart channel`命令會加入 hello rpm 通道 toohello 智慧套件管理員。</span><span class="sxs-lookup"><span data-stu-id="3f572-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="3f572-155">執行 hello 之前`smart update`命令，您會看到類似的輸出如下。</span><span class="sxs-lookup"><span data-stu-id="3f572-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![rpm 和 smart channel 命令的輸出](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="3f572-157">藉由執行下列命令的 hello 安裝 hello 封裝：</span><span class="sxs-lookup"><span data-stu-id="3f572-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="3f572-158">`packagegroup-cloud-azure`這是 hello hello 封裝名稱。</span><span class="sxs-lookup"><span data-stu-id="3f572-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="3f572-159">hello`smart install`命令是使用的 tooinstall hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="3f572-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="3f572-160">安裝 hello 套件之後，Intel NUC 會是預期的 toowork 作為閘道。</span><span class="sxs-lookup"><span data-stu-id="3f572-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="3f572-161">執行 hello Azure IoT 邊緣"hello_world 」 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="3f572-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="3f572-162">跳過`azureiotgatewaysdk/samples`和執行 hello 範例 」 hello_world 」 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f572-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="3f572-163">此範例應用程式建立閘道從 hello`hello_world.json`檔案，並使用 hello 的 hello Azure IoT 邊緣架構 toolog hello world 訊息 tooa 檔案的基本元件每隔 5 秒。</span><span class="sxs-lookup"><span data-stu-id="3f572-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="3f572-164">您可以藉由執行下列命令的 hello 執行 hello 範例 」 hello_world 」 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="3f572-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="3f572-165">hello 範例應用程式會產生 hello 以下輸出如果 hello 閘道功能正常運作：</span><span class="sxs-lookup"><span data-stu-id="3f572-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="3f572-167">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="3f572-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="3f572-168">摘要</span><span class="sxs-lookup"><span data-stu-id="3f572-168">Summary</span></span>

<span data-ttu-id="3f572-169">恭喜！</span><span class="sxs-lookup"><span data-stu-id="3f572-169">Congratulations!</span></span> <span data-ttu-id="3f572-170">您已完成將 Intel NUC 設定為閘道器。</span><span class="sxs-lookup"><span data-stu-id="3f572-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="3f572-171">現在您已準備 toomove toohello 下一個課程 tooset 主機電腦時，在建立 Azure IoT 中樞，並註冊您的 Azure IoT 中樞邏輯裝置。</span><span class="sxs-lookup"><span data-stu-id="3f572-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f572-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3f572-172">Next steps</span></span>
[<span data-ttu-id="3f572-173">準備好您的主機電腦和 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3f572-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
