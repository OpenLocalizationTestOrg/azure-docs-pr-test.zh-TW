---
title: "aaaRaspberry Pi toocloud (Node.js) 的連線覆盆子 Pi tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並在本教學課程中連接覆盆子 Pi tooAzure IoT 中樞覆盆子 Pi toosend 資料 toohello Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot 木莓澆 pi 木莓澆 pi iot 中樞木莓澆 pi 傳送資料 toocloud 木莓澆 pi toocloud"
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57a15ab3984021a9c18ff0aa1316a4d4c6ebdec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="f700a-104">連接覆盆子 Pi tooAzure IoT 中樞 (Node.js)</span><span class="sxs-lookup"><span data-stu-id="f700a-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="f700a-105">在本教學課程中，您必須開始學習使用執行 Raspbian 覆盆子 Pi 的 hello 基本。</span><span class="sxs-lookup"><span data-stu-id="f700a-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="f700a-106">然後您學習如何 tooseamlessly 裝置 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="f700a-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="f700a-107">如需 Windows 10 IoT 核心版範例，請移 toohello [Windows 開發人員中心](http://www.windowsondevices.com/)。</span><span class="sxs-lookup"><span data-stu-id="f700a-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="f700a-108">還沒有套件嗎？</span><span class="sxs-lookup"><span data-stu-id="f700a-108">Don't have a kit yet?</span></span> <span data-ttu-id="f700a-109">試用 [Raspberry Pi 線上模擬器](iot-hub-raspberry-pi-web-simulator-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f700a-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="f700a-110">或在[這裡](https://azure.microsoft.com/develop/iot/starter-kits)購買新的套件。</span><span class="sxs-lookup"><span data-stu-id="f700a-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>


## <a name="what-you-do"></a><span data-ttu-id="f700a-111">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="f700a-111">What you do</span></span>

* <span data-ttu-id="f700a-112">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f700a-112">Create an IoT hub.</span></span>
* <span data-ttu-id="f700a-113">在 IoT 中樞對於 Pi 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="f700a-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="f700a-114">設定 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="f700a-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="f700a-115">Pi toosend 感應器資料 tooyour IoT 中樞上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f700a-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="f700a-116">連接您所建立的覆盆子 Pi tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f700a-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="f700a-117">然後您範例應用程式上執行 Pi toocollect 氣溫和溼度資料從 BME280 感應器。</span><span class="sxs-lookup"><span data-stu-id="f700a-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="f700a-118">最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f700a-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="f700a-119">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="f700a-119">What you learn</span></span>

* <span data-ttu-id="f700a-120">如何 toocreate Azure IoT 中樞，並取得新的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="f700a-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="f700a-121">如何 tooconnect Pi 與 BME280 感應器。</span><span class="sxs-lookup"><span data-stu-id="f700a-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="f700a-122">如何執行範例應用程式上 Pi toocollect 感應器資料。</span><span class="sxs-lookup"><span data-stu-id="f700a-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="f700a-123">如何 toosend 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f700a-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f700a-124">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="f700a-124">What you need</span></span>

![您需要什麼](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="f700a-126">hello 覆盆子 Pi 2 或覆盆子 Pi 3 面板。</span><span class="sxs-lookup"><span data-stu-id="f700a-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="f700a-127">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f700a-127">An active Azure subscription.</span></span> <span data-ttu-id="f700a-128">如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="f700a-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f700a-129">監視、 USB 鍵盤和滑鼠連接 tooPi。</span><span class="sxs-lookup"><span data-stu-id="f700a-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="f700a-130">執行 Windows 或 Linux 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="f700a-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="f700a-131">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="f700a-131">An Internet connection.</span></span>
* <span data-ttu-id="f700a-132">16 GB 以上的 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="f700a-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="f700a-133">USB SD 卡或 microSD 卡 tooburn hello 作業系統映像到 hello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="f700a-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="f700a-134">5 volt 2 amp 電源提供 hello 6 英呎微 USB 纜線。</span><span class="sxs-lookup"><span data-stu-id="f700a-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="f700a-135">hello 下列項目是選擇性項目：</span><span class="sxs-lookup"><span data-stu-id="f700a-135">hello following items are optional:</span></span>

* <span data-ttu-id="f700a-136">組裝的 Adafruit BME280 溫度、壓力溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="f700a-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="f700a-137">麵包板。</span><span class="sxs-lookup"><span data-stu-id="f700a-137">A breadboard.</span></span>
* <span data-ttu-id="f700a-138">6 條 F/M 跳線。</span><span class="sxs-lookup"><span data-stu-id="f700a-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="f700a-139">1 顆漫射型 10 mm LED。</span><span class="sxs-lookup"><span data-stu-id="f700a-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="f700a-140">這些項目是選擇性的因為 hello 程式碼範例支援模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="f700a-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="f700a-141">設定 Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="f700a-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="f700a-142">Pi 安裝 hello Raspbian 作業系統</span><span class="sxs-lookup"><span data-stu-id="f700a-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="f700a-143">準備安裝 hello Raspbian 映像的 hello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="f700a-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="f700a-144">下載 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="f700a-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="f700a-145">[下載與桌面 Raspbian 潔](https://www.raspberrypi.org/downloads/raspbian/)（hello.zip 檔案）。</span><span class="sxs-lookup"><span data-stu-id="f700a-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="f700a-146">擷取 hello Raspbian 映像電腦上的 tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f700a-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="f700a-147">安裝 Raspbian toohello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="f700a-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="f700a-148">[下載並安裝 hello Etcher sd 記憶卡燒錄機公用程式](https://etcher.io/)。</span><span class="sxs-lookup"><span data-stu-id="f700a-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="f700a-149">執行 Etcher，並在步驟 1 中選取您要解壓縮的 hello Raspbian 映像。</span><span class="sxs-lookup"><span data-stu-id="f700a-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="f700a-150">選取 hello microSD 卡磁碟機。</span><span class="sxs-lookup"><span data-stu-id="f700a-150">Select hello microSD card drive.</span></span> <span data-ttu-id="f700a-151">請注意，Etcher 可能已經選取 hello 正確的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="f700a-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="f700a-152">按一下快閃 tooinstall Raspbian toohello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="f700a-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="f700a-153">安裝完成時，請從電腦移除 hello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="f700a-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="f700a-154">因為它是安全的 tooremove hello microSD 卡直接 Etcher 自動退出，或取消掛接 hello microSD 卡在完成時。</span><span class="sxs-lookup"><span data-stu-id="f700a-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="f700a-155">插入 Pi hello microSD 卡。</span><span class="sxs-lookup"><span data-stu-id="f700a-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="f700a-156">啟用 SSH 和 I2C</span><span class="sxs-lookup"><span data-stu-id="f700a-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="f700a-157">Pi toohello 監視器、 鍵盤和滑鼠連接、 啟動 Pi 後再登入 Raspbian 使用`pi`hello 使用者名稱和`raspberry`hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="f700a-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="f700a-158">按一下 hello 木莓澆圖示 >**喜好設定** > **覆盆子 Pi 組態**。</span><span class="sxs-lookup"><span data-stu-id="f700a-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![hello Raspbian 偏好設定 功能表](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="f700a-160">在 hello**介面**索引標籤上，設定**I2C**和**SSH**太**啟用**，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="f700a-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="f700a-161">如果沒有實體的感應器，然後想要模擬的 toouse 感應器資料，這個步驟是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="f700a-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![在 Raspberry Pi 上啟用 I2C 和 SSH](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="f700a-163">tooenable SSH 和 I2C，您可以找到更多的參考文件上[raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/)和[Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c)。</span><span class="sxs-lookup"><span data-stu-id="f700a-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="f700a-164">連接 hello 感應器 tooPi</span><span class="sxs-lookup"><span data-stu-id="f700a-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="f700a-165">請使用 hello breadboard 和跳接器線路 tooconnect LED 和 BME280 tooPi，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f700a-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="f700a-166">如果您沒有 hello 感應器，[略過本節](#connect-pi-to-the-network)。</span><span class="sxs-lookup"><span data-stu-id="f700a-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![hello 覆盆子 Pi 和感應器的連接](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="f700a-168">hello BME280 感應器可以收集溫度和溼度的資料。</span><span class="sxs-lookup"><span data-stu-id="f700a-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="f700a-169">如果沒有裝置和 hello 雲端之間的通訊，將會閃爍 hello LED。</span><span class="sxs-lookup"><span data-stu-id="f700a-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="f700a-170">感應器 pin 碼，使用下列配線 hello:</span><span class="sxs-lookup"><span data-stu-id="f700a-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="f700a-171">啟動 (感應器和 LED)</span><span class="sxs-lookup"><span data-stu-id="f700a-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="f700a-172">結束 (電路版)</span><span class="sxs-lookup"><span data-stu-id="f700a-172">End (Board)</span></span>            | <span data-ttu-id="f700a-173">纜線顏色</span><span class="sxs-lookup"><span data-stu-id="f700a-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="f700a-174">VDD (針腳 5G)</span><span class="sxs-lookup"><span data-stu-id="f700a-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="f700a-175">3.3V PWR (針腳 1)</span><span class="sxs-lookup"><span data-stu-id="f700a-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="f700a-176">白色纜線</span><span class="sxs-lookup"><span data-stu-id="f700a-176">White cable</span></span>   |
| <span data-ttu-id="f700a-177">GND (針腳 7G)</span><span class="sxs-lookup"><span data-stu-id="f700a-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="f700a-178">GND (針腳 6)</span><span class="sxs-lookup"><span data-stu-id="f700a-178">GND (Pin 6)</span></span>            | <span data-ttu-id="f700a-179">棕色纜線</span><span class="sxs-lookup"><span data-stu-id="f700a-179">Brown cable</span></span>   |
| <span data-ttu-id="f700a-180">SDI (針腳 10G)</span><span class="sxs-lookup"><span data-stu-id="f700a-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="f700a-181">I2C1 SDA (針腳 3)</span><span class="sxs-lookup"><span data-stu-id="f700a-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="f700a-182">紅色纜線</span><span class="sxs-lookup"><span data-stu-id="f700a-182">Red cable</span></span>     |
| <span data-ttu-id="f700a-183">SCK (針腳 8G)</span><span class="sxs-lookup"><span data-stu-id="f700a-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="f700a-184">I2C1 SCL (針腳 5)</span><span class="sxs-lookup"><span data-stu-id="f700a-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="f700a-185">橘色纜線</span><span class="sxs-lookup"><span data-stu-id="f700a-185">Orange cable</span></span>  |
| <span data-ttu-id="f700a-186">LED VDD (針腳 18F)</span><span class="sxs-lookup"><span data-stu-id="f700a-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="f700a-187">GPIO 24 (針腳 18)</span><span class="sxs-lookup"><span data-stu-id="f700a-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="f700a-188">白色纜線</span><span class="sxs-lookup"><span data-stu-id="f700a-188">White cable</span></span>   |
| <span data-ttu-id="f700a-189">LED GND (針腳 17F)</span><span class="sxs-lookup"><span data-stu-id="f700a-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="f700a-190">GND (針腳 20)</span><span class="sxs-lookup"><span data-stu-id="f700a-190">GND (Pin 20)</span></span>           | <span data-ttu-id="f700a-191">黑色纜線</span><span class="sxs-lookup"><span data-stu-id="f700a-191">Black cable</span></span>   |

<span data-ttu-id="f700a-192">按一下 tooview[覆盆子 Pi 2 & 3 Pin 對應](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi)供您參考。</span><span class="sxs-lookup"><span data-stu-id="f700a-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="f700a-193">您已成功連接 BME280 tooyour 覆盆子 Pi 之後，它應該類似影像下方。</span><span class="sxs-lookup"><span data-stu-id="f700a-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![連接的 Pi 和 BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="f700a-195">Pi toohello 網路連線</span><span class="sxs-lookup"><span data-stu-id="f700a-195">Connect Pi toohello network</span></span>

<span data-ttu-id="f700a-196">開啟 Pi 使用 hello 微 USB 纜線和 hello 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="f700a-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="f700a-197">使用 hello 乙太網路纜線 tooconnect Pi tooyour 有線網路，或遵循 hello[指示從 hello 覆盆子 Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour 無線網路。</span><span class="sxs-lookup"><span data-stu-id="f700a-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="f700a-198">您 Pi 已成功連接的 toohello 網路之後，您需要 tootake hello 記下[您 Pi 的 IP 位址](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)。</span><span class="sxs-lookup"><span data-stu-id="f700a-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![連接的 toowired 網路](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="f700a-200">請確定 Pi 為您的電腦相同網路的連線的 toohello。</span><span class="sxs-lookup"><span data-stu-id="f700a-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="f700a-201">例如，如果您的電腦是連線的 tooa 無線網路，Pi 是連接的 tooa 有線網路時，您可能不會看到 hello IP 位址 hello devdisco 輸出中的。</span><span class="sxs-lookup"><span data-stu-id="f700a-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="f700a-202">在 Pi 上執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f700a-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="f700a-203">複製範例應用程式並安裝 hello 必要條件套件</span><span class="sxs-lookup"><span data-stu-id="f700a-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="f700a-204">使用其中一種您主機電腦 tooconnect tooyour 覆盆子 Pi 中的下列 SSH 用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="f700a-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="f700a-205">**Windows 使用者**</span><span class="sxs-lookup"><span data-stu-id="f700a-205">**Windows Users**</span></span>
   1. <span data-ttu-id="f700a-206">下載並安裝適用於 Windows 的 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="f700a-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="f700a-207">複製 hello 主機名稱 （或 IP 位址） 到 Pi 區段 hello IP 位址，並選取 SSH 為 hello 的連接類型。</span><span class="sxs-lookup"><span data-stu-id="f700a-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="f700a-209">**Mac 和 Ubuntu 使用者**</span><span class="sxs-lookup"><span data-stu-id="f700a-209">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="f700a-210">使用內建 SSH 用戶端 hello Ubuntu 或 macOS 上。</span><span class="sxs-lookup"><span data-stu-id="f700a-210">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="f700a-211">您可能需要 toorun `ssh pi@<ip address of pi>` tooconnect 透過 SSH 的 Pi。</span><span class="sxs-lookup"><span data-stu-id="f700a-211">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="f700a-212">hello 預設使用者名稱是`pi`，hello 密碼為`raspberry`。</span><span class="sxs-lookup"><span data-stu-id="f700a-212">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="f700a-213">安裝 Node.js 及 NPM tooyour Pi。</span><span class="sxs-lookup"><span data-stu-id="f700a-213">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="f700a-214">首先，您應該以 hello 下列命令檢查 Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="f700a-214">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="f700a-215">如果 hello 版本低於 4.x 或您 pi 沒有 Node.js，然後執行下列命令 tooinstall hello 或更新 Node.js。</span><span class="sxs-lookup"><span data-stu-id="f700a-215">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="f700a-216">藉由執行下列命令的 hello 複製 hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="f700a-216">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="f700a-217">Hello，下列命令安裝所有封裝。</span><span class="sxs-lookup"><span data-stu-id="f700a-217">Install all packages by hello following command.</span></span> <span data-ttu-id="f700a-218">其中包含 Azure IoT 裝置 SDK、BME280 感應器程式庫和接線 Pi 程式庫。</span><span class="sxs-lookup"><span data-stu-id="f700a-218">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="f700a-219">此安裝程序，根據您的網路連線，可能需要幾分鐘的時間 toofinish。</span><span class="sxs-lookup"><span data-stu-id="f700a-219">It might take several minutes toofinish this installation process depending on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="f700a-220">Hello 範例應用程式設定</span><span class="sxs-lookup"><span data-stu-id="f700a-220">Configure hello sample application</span></span>

1. <span data-ttu-id="f700a-221">執行下列命令的 hello 開啟 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="f700a-221">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![組態檔](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="f700a-223">此檔案中有兩個項目可供您設定。</span><span class="sxs-lookup"><span data-stu-id="f700a-223">There are two items in this file you can configurate.</span></span> <span data-ttu-id="f700a-224">hello 第一次是`interval`，這兩個訊息，傳送 toocloud 之間定義 hello 時間間隔 （以毫秒為單位）。</span><span class="sxs-lookup"><span data-stu-id="f700a-224">hello first one is `interval`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="f700a-225">hello 第二個`simulatedData`，這是 toouse 是否模擬感應器資料的布林值。</span><span class="sxs-lookup"><span data-stu-id="f700a-225">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="f700a-226">如果您**沒有 hello 感應器**，將的 hello`simulatedData`值太`true`toomake hello 範例應用程式建立及使用模擬的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="f700a-226">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="f700a-227">按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。</span><span class="sxs-lookup"><span data-stu-id="f700a-227">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="f700a-228">執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f700a-228">Run hello sample application</span></span>

<span data-ttu-id="f700a-229">藉由執行下列命令的 hello 執行 hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="f700a-229">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="f700a-230">請確定您複製-貼上 hello 裝置連接字串到 hello 單引號。</span><span class="sxs-lookup"><span data-stu-id="f700a-230">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="f700a-231">您應該會看到 hello 下列輸出顯示 hello 傳送 tooyour IoT 中樞的感應器資料及 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="f700a-231">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![輸出-從覆盆子 Pi tooyour IoT 中樞傳送的感應器資料](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="f700a-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f700a-233">Next steps</span></span>

<span data-ttu-id="f700a-234">您已執行範例應用程式 toocollect 感應器資料，並將它傳送 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f700a-234">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="f700a-235">toosee 覆盆子 Pi 已傳送的 tooyour IoT 中樞或傳送訊息 tooyour 覆盆子 Pi 命令列介面中的 hello 訊息，請參閱 「 hello[管理雲端的裝置與 iot 中樞總管教學課程傳訊](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)。</span><span class="sxs-lookup"><span data-stu-id="f700a-235">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
