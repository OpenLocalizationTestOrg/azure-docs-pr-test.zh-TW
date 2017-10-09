---
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 1 課： 設定裝置 |Microsoft 文件"
description: "設定覆盆子 Pi 3 供第一次使用並安裝 hello Raspbian OS，最適合用於 hello 覆盆子 Pi 硬體可用的作業系統。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "安裝 raspbian，raspbian 下載如何 tooinstall raspbian raspbian 安裝木莓澆 pi 安裝 raspbian 木莓澆 pi 安裝作業系統、 木莓澆 pi sd 記憶卡安裝、 木莓澆 pi connect 連接 tooraspberry pi 木莓澆 pi 連線"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="98669-104">設定裝置</span><span class="sxs-lookup"><span data-stu-id="98669-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="98669-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="98669-105">What you will do</span></span>
<span data-ttu-id="98669-106">設定第一次使用 Pi 和 hello Raspbian 作業系統安裝。</span><span class="sxs-lookup"><span data-stu-id="98669-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="98669-107">Raspbian 是可用的最適合用於 hello 覆盆子 Pi 硬體上的作業系統。</span><span class="sxs-lookup"><span data-stu-id="98669-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="98669-108">如果您有任何問題，您可以搜尋解決方案 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="98669-108">If you have any problems, you can seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="98669-109">學習目標</span><span class="sxs-lookup"><span data-stu-id="98669-109">What you will learn</span></span>
<span data-ttu-id="98669-110">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="98669-110">In this article, you will learn:</span></span>

* <span data-ttu-id="98669-111">如何 tooinstall Raspbian pi。</span><span class="sxs-lookup"><span data-stu-id="98669-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="98669-112">如何使用 USB 纜線向上 Pi toopower。</span><span class="sxs-lookup"><span data-stu-id="98669-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="98669-113">如何 tooconnect Pi toohello 網路使用乙太網路纜線或無線網路。</span><span class="sxs-lookup"><span data-stu-id="98669-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="98669-114">如何 tooadd LED toohello breadboard 並將它連接 tooPi。</span><span class="sxs-lookup"><span data-stu-id="98669-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="98669-115">必要元件</span><span class="sxs-lookup"><span data-stu-id="98669-115">What you will need</span></span>
<span data-ttu-id="98669-116">toocomplete 這項作業，您需要 hello 覆盆子 Pi 3 入門套件中的下列部分：</span><span class="sxs-lookup"><span data-stu-id="98669-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="98669-117">hello 覆盆子 Pi 3 面板</span><span class="sxs-lookup"><span data-stu-id="98669-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="98669-118">hello 16 GB microSD 卡</span><span class="sxs-lookup"><span data-stu-id="98669-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="98669-119">與 hello 6 英呎微 USB 纜線的 hello 5 volt 2 amp 電源供應器</span><span class="sxs-lookup"><span data-stu-id="98669-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="98669-120">hello breadboard</span><span class="sxs-lookup"><span data-stu-id="98669-120">hello breadboard</span></span>
* <span data-ttu-id="98669-121">接頭電線</span><span class="sxs-lookup"><span data-stu-id="98669-121">Connector wires</span></span>
* <span data-ttu-id="98669-122">一顆 560 歐姆的電阻</span><span class="sxs-lookup"><span data-stu-id="98669-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="98669-123">一顆漫射型 10 mm LED</span><span class="sxs-lookup"><span data-stu-id="98669-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="98669-124">hello 乙太網路纜線</span><span class="sxs-lookup"><span data-stu-id="98669-124">hello Ethernet cable</span></span>

![入門套件中的零件](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="98669-126">您也會需要：</span><span class="sxs-lookup"><span data-stu-id="98669-126">You also need:</span></span>

* <span data-ttu-id="98669-127">若要 Pi tooconnect 有線或無線連線。</span><span class="sxs-lookup"><span data-stu-id="98669-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="98669-128">USB SD 卡或 miniSD 卡 tooburn hello 作業系統映像到 hello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="98669-128">A USB-SD adapter or miniSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="98669-129">一部執行 Windows、Mac 或 Linux 的電腦。</span><span class="sxs-lookup"><span data-stu-id="98669-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="98669-130">hello 電腦是使用的 tooinstall Raspbian hello microSD 卡上。</span><span class="sxs-lookup"><span data-stu-id="98669-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="98669-131">網際網路連線 toodownload hello 必要工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="98669-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="98669-132">在 hello microSD 卡上安裝 Raspbian</span><span class="sxs-lookup"><span data-stu-id="98669-132">Install Raspbian on hello microSD card</span></span>
<span data-ttu-id="98669-133">準備安裝 hello Raspbian 映像的 hello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="98669-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="98669-134">下載 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="98669-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="98669-135">[下載](https://www.raspberrypi.org/downloads/raspbian/)Raspbian 潔與像素的 hello.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="98669-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="98669-136">擷取 hello Raspbian 映像電腦上的 tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="98669-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="98669-137">安裝 Raspbian toohello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="98669-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="98669-138">[下載](https://www.etcher.io)及安裝 hello Etcher sd 記憶卡燒錄機公用程式。</span><span class="sxs-lookup"><span data-stu-id="98669-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="98669-139">執行 Etcher，並在步驟 1 中選取您要解壓縮的 hello Raspbian 映像。</span><span class="sxs-lookup"><span data-stu-id="98669-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="98669-140">選取 hello microSD 卡磁碟機。</span><span class="sxs-lookup"><span data-stu-id="98669-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="98669-141">請注意，Etcher 可能已經選取 hello 正確的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="98669-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="98669-142">按一下**快閃**tooinstall Raspbian toohello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="98669-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="98669-143">安裝完成時，請從電腦移除 hello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="98669-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="98669-144">因為它是安全的 tooremove hello microSD 卡直接 Etcher 自動退出，或取消掛接 hello microSD 卡在完成時。</span><span class="sxs-lookup"><span data-stu-id="98669-144">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="98669-145">插入 Pi hello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="98669-145">Insert hello microSD card into Pi.</span></span>

![插入 hello sd 記憶卡](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="98669-147">開啟 Pi</span><span class="sxs-lookup"><span data-stu-id="98669-147">Turn on Pi</span></span>
<span data-ttu-id="98669-148">開啟 Pi 使用 hello 微 USB 纜線和 hello 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="98669-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![開啟](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="98669-150">它是至少為 hello 套件中的重要 toouse hello 電源供應器 2A toomake 確定您覆盆子具有足夠的電力 toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="98669-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="98669-151">啟用 SSH</span><span class="sxs-lookup"><span data-stu-id="98669-151">Enable SSH</span></span>
<span data-ttu-id="98669-152">截至 hello 2016 年 11 月發行，Raspbian 會提供預設停用的 hello SSH 伺服器。</span><span class="sxs-lookup"><span data-stu-id="98669-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="98669-153">您需要 tooenable 它以手動方式。</span><span class="sxs-lookup"><span data-stu-id="98669-153">You need tooenable it manually.</span></span> <span data-ttu-id="98669-154">您可以使用參照 toohello[官方指示](https://www.raspberrypi.org/documentation/remote-access/ssh/)或連接監視器，並跳過**喜好設定]-> [覆盆子 Pi 組態**tooenable SSH。</span><span class="sxs-lookup"><span data-stu-id="98669-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="98669-155">覆盆子 Pi 3 toohello 網路連線</span><span class="sxs-lookup"><span data-stu-id="98669-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="98669-156">您可以連接 Pi tooa 有線網路或 tooa 無線網路。</span><span class="sxs-lookup"><span data-stu-id="98669-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="98669-157">請確定 Pi 為您的電腦相同網路的連線的 toohello。</span><span class="sxs-lookup"><span data-stu-id="98669-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="98669-158">例如，您可以連接 Pi toohello 相同切換電腦連線到。</span><span class="sxs-lookup"><span data-stu-id="98669-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="98669-159">連接 tooa 有線網路</span><span class="sxs-lookup"><span data-stu-id="98669-159">Connect tooa wired network</span></span>
<span data-ttu-id="98669-160">使用 hello 乙太網路纜線 tooconnect Pi tooyour 有線網路。</span><span class="sxs-lookup"><span data-stu-id="98669-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="98669-161">hello pi 的兩個 Led，如果啟動 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="98669-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![使用乙太網路纜線連接](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="98669-163">Tooa 無線網路連線</span><span class="sxs-lookup"><span data-stu-id="98669-163">Connect tooa wireless network</span></span>
<span data-ttu-id="98669-164">請遵循 hello[指示](https://www.raspberrypi.org/learning/software-guide/wifi/)hello 覆盆子 Pi Foundation tooconnect Pi tooyour 無線網路。</span><span class="sxs-lookup"><span data-stu-id="98669-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="98669-165">這些指示需要您 toofirst 連接監視器與鍵盤 tooPi。</span><span class="sxs-lookup"><span data-stu-id="98669-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="98669-166">連接 hello LED tooPi</span><span class="sxs-lookup"><span data-stu-id="98669-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="98669-167">toocomplete 這個工作，使用 hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard)、 hello 連接器線路、 hello LED，和 hello 電阻。</span><span class="sxs-lookup"><span data-stu-id="98669-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="98669-168">將它們連接 toohello[一般用途輸入/輸出](https://www.raspberrypi.org/documentation/usage/gpio/)Pi (GPIO) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="98669-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![麵包板、LED 及電阻](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="98669-170">連接的 hello LED hello 短腳太**GPIO GND (Pin 6)**。</span><span class="sxs-lookup"><span data-stu-id="98669-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="98669-171">連接 hello hello 電阻 LED tooone 階段 hello 長的腳。</span><span class="sxs-lookup"><span data-stu-id="98669-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="98669-172">連接太 hello hello 電阻其他階段**GPIO 4 (Pin 7)**。</span><span class="sxs-lookup"><span data-stu-id="98669-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="98669-173">請注意 hello LED 極性是很重要。</span><span class="sxs-lookup"><span data-stu-id="98669-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="98669-174">此極性設定通稱為低態動作。</span><span class="sxs-lookup"><span data-stu-id="98669-174">This polarity setting is commonly known as Active Low.</span></span>

![接腳圖](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="98669-176">恭喜！</span><span class="sxs-lookup"><span data-stu-id="98669-176">Congratulations!</span></span> <span data-ttu-id="98669-177">您已經成功設定 Pi。</span><span class="sxs-lookup"><span data-stu-id="98669-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="98669-178">摘要</span><span class="sxs-lookup"><span data-stu-id="98669-178">Summary</span></span>
<span data-ttu-id="98669-179">在本文中，您學到如何 tooconfigure Pi 安裝 Raspbian，連接 Pi tooa 網路，並將連接 LED tooPi。</span><span class="sxs-lookup"><span data-stu-id="98669-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="98669-180">請注意該 hello LED 尚無法亮起。</span><span class="sxs-lookup"><span data-stu-id="98669-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="98669-181">hello 下一個工作是 tooinstall hello 必要工具和準備 Pi 上執行範例應用程式中的軟體。</span><span class="sxs-lookup"><span data-stu-id="98669-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![硬體已準備完畢](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="98669-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98669-183">Next steps</span></span>
[<span data-ttu-id="98669-184">取得 hello 工具</span><span class="sxs-lookup"><span data-stu-id="98669-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

