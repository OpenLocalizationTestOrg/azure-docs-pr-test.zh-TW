---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 1 課：設定 Intel NUC | Microsoft Docs"
description: "設定 Intel NUC toowork 為 IoT 閘道之間的感應器和 Azure IoT 中樞 toocollect 感應器資訊，以傳送 tooIoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 閘道, intel nuc, nuc 電腦, DE3815TYKE"
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="aab60-104">將 Intel NUC 設定為 IoT 閘道器</span><span class="sxs-lookup"><span data-stu-id="aab60-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="aab60-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="aab60-105">What you will do</span></span>

- <span data-ttu-id="aab60-106">將 Intel NUC 設定為 IoT 閘道器。</span><span class="sxs-lookup"><span data-stu-id="aab60-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="aab60-107">Hello Azure IoT 邊緣上安裝套件 hello Intel NUC。</span><span class="sxs-lookup"><span data-stu-id="aab60-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="aab60-108">Hello Intel NUC tooverify hello 閘道功能上執行"hello_world 」 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="aab60-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="aab60-109">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="aab60-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="aab60-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="aab60-110">What you will learn</span></span>

<span data-ttu-id="aab60-111">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="aab60-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="aab60-112">如何 tooconnect Intel NUC 與週邊設備。</span><span class="sxs-lookup"><span data-stu-id="aab60-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="aab60-113">如何在使用 Intel NUC tooinstall 和更新所需的 hello 封裝 hello 智慧套件管理員。</span><span class="sxs-lookup"><span data-stu-id="aab60-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="aab60-114">如何 toorun hello"hello_world 」 的範例應用程式 tooverify hello 閘道功能。</span><span class="sxs-lookup"><span data-stu-id="aab60-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aab60-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="aab60-115">What you need</span></span>

- <span data-ttu-id="aab60-116">以 hello Intel IoT 閘道軟體套件 Intel NUC 套件 DE3815TYKE (Wind 河 Linux * 7.0.0.13) 預先安裝。</span><span class="sxs-lookup"><span data-stu-id="aab60-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="aab60-117">[按一下這裡 toopurchase Groove IoT 商業閘道套件](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html)。</span><span class="sxs-lookup"><span data-stu-id="aab60-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="aab60-118">乙太網路連接線。</span><span class="sxs-lookup"><span data-stu-id="aab60-118">An Ethernet cable.</span></span>
- <span data-ttu-id="aab60-119">鍵盤。</span><span class="sxs-lookup"><span data-stu-id="aab60-119">A keyboard.</span></span>
- <span data-ttu-id="aab60-120">HDMI 或 VGA 連接線。</span><span class="sxs-lookup"><span data-stu-id="aab60-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="aab60-121">具有 HDMI 或 VGA 連接埠的螢幕。</span><span class="sxs-lookup"><span data-stu-id="aab60-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="aab60-122">選擇性︰[Texas Instruments 的感應器標籤 (CC2650STK) (英文)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="aab60-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![閘道器套件](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="aab60-124">與 hello 週邊設備連接 Intel NUC</span><span class="sxs-lookup"><span data-stu-id="aab60-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="aab60-125">hello 圖是 Intel NUC 會連接到各種週邊設備的範例：</span><span class="sxs-lookup"><span data-stu-id="aab60-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="aab60-126">連接的 tooa 鍵盤。</span><span class="sxs-lookup"><span data-stu-id="aab60-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="aab60-127">VGA 纜線或 HDMI 纜線連接 tooa 監視器。</span><span class="sxs-lookup"><span data-stu-id="aab60-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="aab60-128">有線乙太網路纜線與網路連線的 tooa。</span><span class="sxs-lookup"><span data-stu-id="aab60-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="aab60-129">使用電源纜線連接的 tooa 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="aab60-129">Connected tooa power supply with a power cable.</span></span>

![Intel NUC 連接 tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="aab60-131">從主機電腦透過安全殼層 (SSH) 連線 toohello Intel NUC 系統</span><span class="sxs-lookup"><span data-stu-id="aab60-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="aab60-132">您必須使用鍵盤和 Intel NUC 裝置的監視 tooget hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aab60-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="aab60-133">如果您已經知道 hello IP 位址，您可以略過前 toostep 3 這一節。</span><span class="sxs-lookup"><span data-stu-id="aab60-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="aab60-134">開啟 hello Intel NUC 按 hello 電源按鈕，然後登入。</span><span class="sxs-lookup"><span data-stu-id="aab60-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="aab60-135">hello 預設使用者名稱和密碼都`root`。</span><span class="sxs-lookup"><span data-stu-id="aab60-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="aab60-136">藉由執行 hello 取得 hello IP 位址的 hello Intel NUC `ifconfig` hello Intel NUC 裝置上的命令。</span><span class="sxs-lookup"><span data-stu-id="aab60-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="aab60-137">以下是 hello 命令輸出的範例。</span><span class="sxs-lookup"><span data-stu-id="aab60-137">Here is an example of hello command output.</span></span>

   ![顯示 Intel NUC IP 的 ifconfig 輸出](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="aab60-139">在此範例中，hello 值後面`inet addr:`是您需要時從主機電腦連接 toohello Intel NUC hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aab60-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="aab60-140">使用其中一種您主機電腦 tooconnect tooIntel NUC 中的下列 SSH 用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="aab60-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="aab60-141">[PuTTY](http://www.putty.org/) 適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="aab60-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="aab60-142">hello 內建 SSH 用戶端上 Ubuntu 或 macOS。</span><span class="sxs-lookup"><span data-stu-id="aab60-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="aab60-143">更有效率且更有生產力 toooperate 從主機電腦 Intel NUC 它。</span><span class="sxs-lookup"><span data-stu-id="aab60-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="aab60-144">您需要 hello Intel NUC IP 位址，透過將 SSH 用戶端的使用者名稱和密碼 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="aab60-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="aab60-145">以下是在 macOS 上使用 SSH 用戶端的範例。</span><span class="sxs-lookup"><span data-stu-id="aab60-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="aab60-146">![在 macOS 上執行的 SSH 用戶端](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="aab60-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="aab60-147">安裝 hello Azure IoT 邊緣套件</span><span class="sxs-lookup"><span data-stu-id="aab60-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="aab60-148">hello Azure IoT 邊緣套件包含 hello IoT 邊緣和其相依性的先行編譯二進位檔。</span><span class="sxs-lookup"><span data-stu-id="aab60-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="aab60-149">這些二進位檔是 Azure IoT 邊緣、 hello Azure IoT SDK 和 hello 對應工具。</span><span class="sxs-lookup"><span data-stu-id="aab60-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="aab60-150">hello 封裝也包含 「 hello_world 」 範例應用程式是使用的 toovalidate hello 閘道功能。</span><span class="sxs-lookup"><span data-stu-id="aab60-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="aab60-151">IoT 邊緣屬於 hello 核心 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="aab60-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="aab60-152">請遵循這些步驟 tooinstall hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="aab60-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="aab60-153">藉由執行下列命令在 terminal 視窗中的 hello 新增 hello IoT 雲端儲存機制：</span><span class="sxs-lookup"><span data-stu-id="aab60-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="aab60-154">輸入 'y'，當提示您 too'Include 此通道嗎？ '</span><span class="sxs-lookup"><span data-stu-id="aab60-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="aab60-155">如果您收到`import read failed(-1)`錯誤，使用下列命令 tooresolve hello 問題的 hello:</span><span class="sxs-lookup"><span data-stu-id="aab60-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="aab60-156">hello`rpm`命令匯入 hello rpm 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="aab60-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="aab60-157">hello`smart channel`命令會加入 hello rpm 通道 toohello 智慧套件管理員。</span><span class="sxs-lookup"><span data-stu-id="aab60-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="aab60-158">執行 hello 之前`smart update`命令時，您會看到類似下面的的輸出。</span><span class="sxs-lookup"><span data-stu-id="aab60-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![rpm 和 smart channel 命令的輸出](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="aab60-160">執行 hello 智慧更新命令：</span><span class="sxs-lookup"><span data-stu-id="aab60-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="aab60-161">執行下列命令的 hello 安裝 hello Azure IoT 閘道套件：</span><span class="sxs-lookup"><span data-stu-id="aab60-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="aab60-162">`packagegroup-cloud-azure`這是 hello hello 封裝名稱。</span><span class="sxs-lookup"><span data-stu-id="aab60-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="aab60-163">hello`smart install`命令是使用的 tooinstall hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="aab60-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="aab60-164">如果您看到此錯誤的 hello 執行的下列命令: '公用金鑰無法使用'</span><span class="sxs-lookup"><span data-stu-id="aab60-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="aab60-165">如果您看到此錯誤，請重新啟動 hello Intel NUC: '沒有封裝所提供的開發人員 linux util '</span><span class="sxs-lookup"><span data-stu-id="aab60-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="aab60-166">安裝 hello 套件之後，Intel NUC 是準備 toofunction 閘道。</span><span class="sxs-lookup"><span data-stu-id="aab60-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="aab60-167">執行 hello Azure IoT 邊緣"hello_world 」 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="aab60-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="aab60-168">hello 遵循範例應用程式建立從閘道`hello_world.json`檔案，並每隔 5 秒使用的 Azure IoT 邊緣架構 toolog hello world 訊息 tooa 檔案 (.log.txt) hello 基礎元件。</span><span class="sxs-lookup"><span data-stu-id="aab60-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="aab60-169">您可以藉由執行下列命令的 hello 執行 hello Hello World 範例：</span><span class="sxs-lookup"><span data-stu-id="aab60-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="aab60-170">可讓 hello Hello World 應用程式執行幾分鐘，然後按下 hello Enter 鍵 toostop 它。</span><span class="sxs-lookup"><span data-stu-id="aab60-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="aab60-171">![應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="aab60-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="aab60-172">您可以忽略您按下 Enter 之後出現的任何「無效的引數控制代碼 (NULL)」錯誤。</span><span class="sxs-lookup"><span data-stu-id="aab60-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="aab60-173">您可以確認該 hello 閘道已順利執行開啟現在是 hello_world 資料夾中的 hello.log.txt 檔案![.log.txt 目錄檢視](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="aab60-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="aab60-174">開啟.log.txt 使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="aab60-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="aab60-175">然後，您會看到 hello.log.txt，將 JSON 格式的輸出則 hello 閘道 Hello World 模組來撰寫每隔 5 秒的 hello 記錄訊息內容。</span><span class="sxs-lookup"><span data-stu-id="aab60-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="aab60-176">![log.txt 目錄檢視](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="aab60-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="aab60-177">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="aab60-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="aab60-178">摘要</span><span class="sxs-lookup"><span data-stu-id="aab60-178">Summary</span></span>

<span data-ttu-id="aab60-179">恭喜！</span><span class="sxs-lookup"><span data-stu-id="aab60-179">Congratulations!</span></span> <span data-ttu-id="aab60-180">您已完成將 Intel NUC 設定為閘道器。</span><span class="sxs-lookup"><span data-stu-id="aab60-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="aab60-181">現在您已準備 toomove toohello 下一個課程 tooset 主機電腦時，在建立 Azure IoT 中樞，並註冊您的 Azure IoT 中樞邏輯裝置。</span><span class="sxs-lookup"><span data-stu-id="aab60-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aab60-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aab60-182">Next steps</span></span>
[<span data-ttu-id="aab60-183">使用 IoT 閘道 tooconnect 裝置 tooAzure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="aab60-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

