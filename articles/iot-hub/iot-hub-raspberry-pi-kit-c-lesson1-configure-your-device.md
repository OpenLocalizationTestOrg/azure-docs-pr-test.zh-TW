---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 第 1 課：設定裝置 | Microsoft Docs"
description: "設定 Raspberry Pi 3 首次使用與安裝 Raspbian 作業系統，此為針對 Raspberry Pi 硬體最佳化的免費作業系統。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "安裝 raspbian, raspbian 下載, 如何安裝 raspbian, raspbian 安裝程式, raspberry pi 安裝 raspbian, raspberry pi 安裝 os, raspberry pi sd 記憶卡安裝, raspberry pi 連線, 連線至 raspberry pi, raspberry pi 連線能力"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="ca038-104">設定裝置</span><span class="sxs-lookup"><span data-stu-id="ca038-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="ca038-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="ca038-105">What you will do</span></span>
<span data-ttu-id="ca038-106">設定 Pi 以便進行首次使用，並安裝 Raspbian 作業系統。</span><span class="sxs-lookup"><span data-stu-id="ca038-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="ca038-107">Raspbian 是最適合用於 Raspberry Pi 硬體的免費作業系統。</span><span class="sxs-lookup"><span data-stu-id="ca038-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="ca038-108">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="ca038-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ca038-109">學習目標</span><span class="sxs-lookup"><span data-stu-id="ca038-109">What you will learn</span></span>
<span data-ttu-id="ca038-110">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="ca038-110">In this article, you will learn:</span></span>

* <span data-ttu-id="ca038-111">如何在 Pi 上安裝 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="ca038-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="ca038-112">如何使用 USB 纜線開啟 Pi 的電源。</span><span class="sxs-lookup"><span data-stu-id="ca038-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="ca038-113">如何使用乙太網路纜線或無線網路將 Pi 連接到網路。</span><span class="sxs-lookup"><span data-stu-id="ca038-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="ca038-114">如何將 LED 新增到麵包板並將它連接到 Pi。</span><span class="sxs-lookup"><span data-stu-id="ca038-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ca038-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="ca038-115">What you need</span></span>
<span data-ttu-id="ca038-116">若要完成此作業，您需要 Raspberry Pi 3 入門套件中的下列零件：</span><span class="sxs-lookup"><span data-stu-id="ca038-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="ca038-117">Raspberry Pi 3 電路板</span><span class="sxs-lookup"><span data-stu-id="ca038-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="ca038-118">16 GB 的 microSD 記憶卡</span><span class="sxs-lookup"><span data-stu-id="ca038-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="ca038-119">具備 6 英呎 micro USB 纜線的 5V 2A 電源供應器</span><span class="sxs-lookup"><span data-stu-id="ca038-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="ca038-120">麵包板</span><span class="sxs-lookup"><span data-stu-id="ca038-120">The breadboard</span></span>
* <span data-ttu-id="ca038-121">接頭電線</span><span class="sxs-lookup"><span data-stu-id="ca038-121">Connector wires</span></span>
* <span data-ttu-id="ca038-122">一顆 560 歐姆的電阻</span><span class="sxs-lookup"><span data-stu-id="ca038-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="ca038-123">一顆漫射型 10 mm LED</span><span class="sxs-lookup"><span data-stu-id="ca038-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="ca038-124">乙太網路纜線</span><span class="sxs-lookup"><span data-stu-id="ca038-124">The Ethernet cable</span></span>

![入門套件中的零件](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="ca038-126">您也會需要：</span><span class="sxs-lookup"><span data-stu-id="ca038-126">You also need:</span></span>

* <span data-ttu-id="ca038-127">可供 Pi 連線的有線或無線連線。</span><span class="sxs-lookup"><span data-stu-id="ca038-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="ca038-128">一個 USB-SD 配接器或 mini-SD 記憶卡，以將 OS 映像燒錄到 microSD 記憶卡中。</span><span class="sxs-lookup"><span data-stu-id="ca038-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="ca038-129">一部執行 Windows、Mac 或 Linux 的電腦。</span><span class="sxs-lookup"><span data-stu-id="ca038-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="ca038-130">該電腦是用來將 Raspbian 安裝到 microSD 記憶卡上。</span><span class="sxs-lookup"><span data-stu-id="ca038-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="ca038-131">網際網路連線，以下載必要的工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="ca038-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="ca038-132">在 MicroSD 記憶卡上安裝 Raspbian</span><span class="sxs-lookup"><span data-stu-id="ca038-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="ca038-133">準備好用來安裝 Raspbian 映像的 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="ca038-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="ca038-134">下載 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="ca038-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="ca038-135">[下載](https://www.raspberrypi.org/downloads/raspbian/)具備 Pixel 的 Raspbian Jessie .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="ca038-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="ca038-136">將 Raspbian 映像解壓縮到您電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ca038-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="ca038-137">將 Raspbian 安裝到 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="ca038-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="ca038-138">[下載](https://www.etcher.io)並安裝 Etcher SD 記憶卡燒錄器公用程式。</span><span class="sxs-lookup"><span data-stu-id="ca038-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="ca038-139">執行 Etcher 並選取您在步驟 1 中解壓縮的 Raspbian 映像。</span><span class="sxs-lookup"><span data-stu-id="ca038-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="ca038-140">選取 microSD 記憶卡磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ca038-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="ca038-141">注意：Etcher 可能已經選取正確的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ca038-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="ca038-142">按一下 [Flash] 以將 Raspbian 安裝到 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="ca038-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="ca038-143">安裝完成時，請將 microSD 記憶卡從電腦移除。</span><span class="sxs-lookup"><span data-stu-id="ca038-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="ca038-144">您可以放心地直接移除 microSD 記憶卡，因為 Etcher 會在完成時自動退出或卸載 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="ca038-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="ca038-145">將 microSD 記憶卡插入 Pi。</span><span class="sxs-lookup"><span data-stu-id="ca038-145">Insert the microSD card into your Pi.</span></span>

![插入 SD 記憶卡](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="ca038-147">開啟 Pi</span><span class="sxs-lookup"><span data-stu-id="ca038-147">Turn on Pi</span></span>
<span data-ttu-id="ca038-148">透過 micro USB 纜線和電源供應器來開啟 Pi。</span><span class="sxs-lookup"><span data-stu-id="ca038-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![開啟](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="ca038-150">請務必使用套件中具有至少 2A 電流強度的電源供應器，來確保 Raspberry 具有足夠的電力以正常運作。</span><span class="sxs-lookup"><span data-stu-id="ca038-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="ca038-151">啟用 SSH</span><span class="sxs-lookup"><span data-stu-id="ca038-151">Enable SSH</span></span>
<span data-ttu-id="ca038-152">截至 2016 年 11 月版本，Raspbian 預設已停用 SSH 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca038-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="ca038-153">您必須手動進行啟用。</span><span class="sxs-lookup"><span data-stu-id="ca038-153">You need to enable it manually.</span></span> <span data-ttu-id="ca038-154">您可以參考[官方指示 (英文)](https://www.raspberrypi.org/documentation/remote-access/ssh/)，或者連接監視器並移至 [喜好設定] -> [Raspberry Pi 組態] 來啟用 SSH。</span><span class="sxs-lookup"><span data-stu-id="ca038-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="ca038-155">將 Raspberry Pi 3 連接到網路</span><span class="sxs-lookup"><span data-stu-id="ca038-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="ca038-156">您可以將 Pi 連接到有線網路或無線網路。</span><span class="sxs-lookup"><span data-stu-id="ca038-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="ca038-157">請確定 Pi 是連接到與您電腦相同的網路。</span><span class="sxs-lookup"><span data-stu-id="ca038-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="ca038-158">例如，您可以將 Pi 連接到已和電腦連線的交換器。</span><span class="sxs-lookup"><span data-stu-id="ca038-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="ca038-159">連接到有線網路</span><span class="sxs-lookup"><span data-stu-id="ca038-159">Connect to a wired network</span></span>
<span data-ttu-id="ca038-160">使用乙太網路纜線將 Pi 連接到有線網路。</span><span class="sxs-lookup"><span data-stu-id="ca038-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="ca038-161">Pi 上的兩顆 LED 將會在連線建立時開啟。</span><span class="sxs-lookup"><span data-stu-id="ca038-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![使用乙太網路纜線連接](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="ca038-163">連接到無線網路</span><span class="sxs-lookup"><span data-stu-id="ca038-163">Connect to a wireless network</span></span>
<span data-ttu-id="ca038-164">請遵循來自 Raspberry Pi Foundation 的[指示](https://www.raspberrypi.org/learning/software-guide/wifi/)，將 Pi 連接到無線網路。</span><span class="sxs-lookup"><span data-stu-id="ca038-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="ca038-165">這些指示需要您先將 Pi 連接到監視器和鍵盤。</span><span class="sxs-lookup"><span data-stu-id="ca038-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="ca038-166">將 LED 連接到 Pi</span><span class="sxs-lookup"><span data-stu-id="ca038-166">Connect the LED to Pi</span></span>
<span data-ttu-id="ca038-167">若要完成此工作，請使用[麵包板](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard)、接頭電線、LED 及電阻。</span><span class="sxs-lookup"><span data-stu-id="ca038-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="ca038-168">將它們連接到 Pi 的 [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca038-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![麵包板、LED 及電阻](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="ca038-170">將 LED 的短腳連接到 **GPIO GND** (針腳 6)。</span><span class="sxs-lookup"><span data-stu-id="ca038-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="ca038-171">將 LED 的長腳連接到電阻的其中一隻腳。</span><span class="sxs-lookup"><span data-stu-id="ca038-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="ca038-172">將電阻的另一隻腳連接到 **GPIO 4** (針腳 7)。</span><span class="sxs-lookup"><span data-stu-id="ca038-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="ca038-173">請注意，LED 的極性很重要。</span><span class="sxs-lookup"><span data-stu-id="ca038-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="ca038-174">此極性設定通稱為低態動作。</span><span class="sxs-lookup"><span data-stu-id="ca038-174">This polarity setting is commonly known as Active Low.</span></span>

![接腳圖](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="ca038-176">恭喜！</span><span class="sxs-lookup"><span data-stu-id="ca038-176">Congratulations!</span></span> <span data-ttu-id="ca038-177">您已經成功設定 Pi。</span><span class="sxs-lookup"><span data-stu-id="ca038-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="ca038-178">摘要</span><span class="sxs-lookup"><span data-stu-id="ca038-178">Summary</span></span>
<span data-ttu-id="ca038-179">在本文中，您已了解如何透過安裝 Raspbian、將 Pi 連接到網路，以及將 LED 連接到 Pi 來設定 Pi。</span><span class="sxs-lookup"><span data-stu-id="ca038-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="ca038-180">請注意，LED 目前尚未亮起。</span><span class="sxs-lookup"><span data-stu-id="ca038-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="ca038-181">下一個工作是安裝必要的工具和軟體，以準備在 Pi 上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca038-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![硬體已準備完畢](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="ca038-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca038-183">Next steps</span></span>
[<span data-ttu-id="ca038-184">取得工具</span><span class="sxs-lookup"><span data-stu-id="ca038-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

