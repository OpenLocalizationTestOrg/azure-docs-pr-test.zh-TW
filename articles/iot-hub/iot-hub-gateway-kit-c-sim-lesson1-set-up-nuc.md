---
title: "模擬裝置與 Azure IoT 閘道 - 第 1 課：設定 NUC | Microsoft Docs"
description: "將 Intel NUC 設定為在感應器和 Azure IoT 中樞之間做為 IoT 閘道器，以收集感應器資訊，並將資訊傳送至 IoT 中樞。"
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
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="97dcc-104">將 Intel NUC 設定為 IoT 閘道器</span><span class="sxs-lookup"><span data-stu-id="97dcc-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="97dcc-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="97dcc-105">What you will do</span></span>

- <span data-ttu-id="97dcc-106">將 Intel NUC 設定為 IoT 閘道器。</span><span class="sxs-lookup"><span data-stu-id="97dcc-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="97dcc-107">在 Intel NUC 上安裝 Azure IoT Edge 套件。</span><span class="sxs-lookup"><span data-stu-id="97dcc-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="97dcc-108">在 Intel NUC 上執行 "hello_world" 範例應用程式以確認閘道器的功能。</span><span class="sxs-lookup"><span data-stu-id="97dcc-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="97dcc-109">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="97dcc-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="97dcc-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="97dcc-110">What you will learn</span></span>

<span data-ttu-id="97dcc-111">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="97dcc-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="97dcc-112">如何連接 Intel NUC 與週邊設備。</span><span class="sxs-lookup"><span data-stu-id="97dcc-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="97dcc-113">如何使用智慧型套件管理員 (Smart Package Manager) 安裝及更新 Intel NUC 上的所需套件。</span><span class="sxs-lookup"><span data-stu-id="97dcc-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="97dcc-114">如何執行 "hello_world" 範例應用程式以確認閘道器的功能。</span><span class="sxs-lookup"><span data-stu-id="97dcc-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="97dcc-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="97dcc-115">What you need</span></span>

- <span data-ttu-id="97dcc-116">預先安裝的 Intel NUC 套件 DE3815TYKE 與 Intel IoT 閘道器軟體套件 (Wind River Linux *7.0.0.13)。</span><span class="sxs-lookup"><span data-stu-id="97dcc-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="97dcc-117">乙太網路連接線。</span><span class="sxs-lookup"><span data-stu-id="97dcc-117">An Ethernet cable.</span></span>
- <span data-ttu-id="97dcc-118">鍵盤。</span><span class="sxs-lookup"><span data-stu-id="97dcc-118">A keyboard.</span></span>
- <span data-ttu-id="97dcc-119">HDMI 或 VGA 連接線。</span><span class="sxs-lookup"><span data-stu-id="97dcc-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="97dcc-120">具有 HDMI 或 VGA 連接埠的螢幕。</span><span class="sxs-lookup"><span data-stu-id="97dcc-120">A monitor with an HDMI or VGA port.</span></span>

![閘道器套件](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="97dcc-122">連接 Intel NUC 與週邊設備</span><span class="sxs-lookup"><span data-stu-id="97dcc-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="97dcc-123">下圖是 Intel NUC 與各種週邊設備連接的範例︰</span><span class="sxs-lookup"><span data-stu-id="97dcc-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="97dcc-124">連接到鍵盤。</span><span class="sxs-lookup"><span data-stu-id="97dcc-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="97dcc-125">用 VGA 連接線或 HDMI 連接線連接到螢幕。</span><span class="sxs-lookup"><span data-stu-id="97dcc-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="97dcc-126">透過乙太網路連接線連接到有線網路。</span><span class="sxs-lookup"><span data-stu-id="97dcc-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="97dcc-127">用電源線連接到電源供應器。</span><span class="sxs-lookup"><span data-stu-id="97dcc-127">Connected to the power supply with a power cable.</span></span>

![連接到週邊設備的 Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="97dcc-129">從主機電腦透過安全殼層 (SSH) 連線至 Intel NUC 系統</span><span class="sxs-lookup"><span data-stu-id="97dcc-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="97dcc-130">此時您需要鍵盤和螢幕來取得 NUC 裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="97dcc-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="97dcc-131">如果您已經知道 IP 位址，可以跳至本節的步驟 3。</span><span class="sxs-lookup"><span data-stu-id="97dcc-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="97dcc-132">按下電源按鈕開啟 Intel NUC，登入系統。</span><span class="sxs-lookup"><span data-stu-id="97dcc-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="97dcc-133">預設的使用者名稱和密碼都是 `root`。</span><span class="sxs-lookup"><span data-stu-id="97dcc-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="97dcc-134">執行 `ifconfig` 命令取得 NUC 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="97dcc-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="97dcc-135">這個步驟是在 NUC 裝置上進行。</span><span class="sxs-lookup"><span data-stu-id="97dcc-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="97dcc-136">以下是命令的範例輸出。</span><span class="sxs-lookup"><span data-stu-id="97dcc-136">Here is an example of the command output.</span></span>

   ![ifconfig 輸出顯示 NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="97dcc-138">在此範例中，`inet addr:` 後的值是 IP 位址，您打算從主機電腦遠端連線 Intel NUC 時需要此值。</span><span class="sxs-lookup"><span data-stu-id="97dcc-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="97dcc-139">使用下列其中一個 SSH 用戶端，從主機電腦連線至 Intel NUC。</span><span class="sxs-lookup"><span data-stu-id="97dcc-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="97dcc-140">[PuTTY](http://www.putty.org/) 適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="97dcc-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="97dcc-141">在 Ubuntu 或 macOS 上有內建 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="97dcc-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="97dcc-142">從主機電腦操作 Intel NUC 會更有效率且更有生產力。</span><span class="sxs-lookup"><span data-stu-id="97dcc-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="97dcc-143">您需要 IP 位址、使用者名稱和密碼才能透 SSH 用戶端連線至 NUC。</span><span class="sxs-lookup"><span data-stu-id="97dcc-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="97dcc-144">以下是在 macOS 上 SSH 用戶端的範例。</span><span class="sxs-lookup"><span data-stu-id="97dcc-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="97dcc-145">![在 macOS 上執行的 SSH 用戶端](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="97dcc-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="97dcc-146">安裝 Azure IoT Edge 套件</span><span class="sxs-lookup"><span data-stu-id="97dcc-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="97dcc-147">Azure IoT Edge 套件包含預先編譯的 SDK 二進位檔及其相依性。</span><span class="sxs-lookup"><span data-stu-id="97dcc-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="97dcc-148">這些二進位檔是 Azure IoT Edge、Azure IoT SDK 和對應的工具。</span><span class="sxs-lookup"><span data-stu-id="97dcc-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="97dcc-149">套件也會包含 "hello_world" 範例應用程式，可用來確認閘道功能。</span><span class="sxs-lookup"><span data-stu-id="97dcc-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="97dcc-150">IoT Edge 是閘道的核心部分。</span><span class="sxs-lookup"><span data-stu-id="97dcc-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="97dcc-151">若要安裝套件，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="97dcc-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="97dcc-152">在終端機視窗中執行下列命令，新增 IoT 雲端存放庫：</span><span class="sxs-lookup"><span data-stu-id="97dcc-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="97dcc-153">`rpm` 命令會匯入 rpm 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="97dcc-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="97dcc-154">`smart channel` 命令會將 rpm 通道新增至智慧型套件管理員。</span><span class="sxs-lookup"><span data-stu-id="97dcc-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="97dcc-155">執行 `smart update` 命令前，您會看到如下的輸出。</span><span class="sxs-lookup"><span data-stu-id="97dcc-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![rpm 和 smart channel 命令的輸出](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="97dcc-157">執行下列命令安裝套件：</span><span class="sxs-lookup"><span data-stu-id="97dcc-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="97dcc-158">`packagegroup-cloud-azure` 是套件的名稱。</span><span class="sxs-lookup"><span data-stu-id="97dcc-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="97dcc-159">`smart install` 命令是用於安裝套件。</span><span class="sxs-lookup"><span data-stu-id="97dcc-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="97dcc-160">安裝套件後，Intel NUC 應該可以當做閘道運作。</span><span class="sxs-lookup"><span data-stu-id="97dcc-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="97dcc-161">執行 Azure IoT Edge "hello_world" 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="97dcc-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="97dcc-162">移至 `azureiotgatewaysdk/samples`，執行 "hello_world" 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="97dcc-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="97dcc-163">此範例應用程式會從 `hello_world.json` 檔案建立閘道，並使用 Azure IoT Edge 架構中的基礎元件，每隔 5 秒將 hello world 訊息記錄到檔案中。</span><span class="sxs-lookup"><span data-stu-id="97dcc-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="97dcc-164">您可以執行下列命令，執行 "hello_world" 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="97dcc-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="97dcc-165">如果閘道器功能正常運作，範例應用程式會產生下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="97dcc-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="97dcc-167">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="97dcc-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="97dcc-168">摘要</span><span class="sxs-lookup"><span data-stu-id="97dcc-168">Summary</span></span>

<span data-ttu-id="97dcc-169">恭喜！</span><span class="sxs-lookup"><span data-stu-id="97dcc-169">Congratulations!</span></span> <span data-ttu-id="97dcc-170">您已完成將 Intel NUC 設定為閘道器。</span><span class="sxs-lookup"><span data-stu-id="97dcc-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="97dcc-171">現在您可以開始進行下一課，設定主機電腦、建立 Azure IoT 中樞，並登錄您的 Azure IoT 中樞邏輯裝置。</span><span class="sxs-lookup"><span data-stu-id="97dcc-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97dcc-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97dcc-172">Next steps</span></span>
[<span data-ttu-id="97dcc-173">準備好您的主機電腦和 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="97dcc-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
