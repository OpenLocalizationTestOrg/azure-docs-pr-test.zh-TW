---
title: "M0 toocloud： 連接羽毛 M0 WiFi tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 tooset 及 Adafruit 羽毛 M0 WiFi tooAzure IoT 中樞 toosend 資料 toohello Azure 雲端平台連接在此教學課程。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="f024e-103">連接 Adafruit 羽毛 M0 WiFi tooAzure hello 雲端中的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f024e-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280、Feather M0 WiFi 與 IoT 中樞之間的連線](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="f024e-105">在本教學課程中，您必須開始學習使用 Arduino 面板的 hello 基本。</span><span class="sxs-lookup"><span data-stu-id="f024e-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="f024e-106">然後您學習如何 tooseamlessly 裝置 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="f024e-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="f024e-107">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="f024e-107">What you do</span></span>

<span data-ttu-id="f024e-108">連接您所建立的 Adafruit 羽毛 M0 WiFi tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f024e-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="f024e-109">然後從 BME280 M0 WiFi toocollect hello 氣溫和溼度資料上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f024e-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="f024e-110">最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f024e-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="f024e-111">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="f024e-111">What you learn</span></span>

* <span data-ttu-id="f024e-112">如何 toocreate IoT 中樞和羽毛 M0 WiFi 如註冊裝置</span><span class="sxs-lookup"><span data-stu-id="f024e-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="f024e-113">如何 tooconnect 羽毛 M0 WiFi hello 感應器與您的電腦</span><span class="sxs-lookup"><span data-stu-id="f024e-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="f024e-114">如何執行範例應用程式上羽毛 M0 WiFi toocollect 感應器資料</span><span class="sxs-lookup"><span data-stu-id="f024e-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="f024e-115">如何 toosend hello 感應器資料 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f024e-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f024e-116">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="f024e-116">What you need</span></span>

![Hello 教學課程需要的組件](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="f024e-118">toocomplete 這項作業，您需要 hello 羽毛 M0 WiFi 入門套件中的下列部分：</span><span class="sxs-lookup"><span data-stu-id="f024e-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="f024e-119">hello 羽毛 M0 WiFi 面板</span><span class="sxs-lookup"><span data-stu-id="f024e-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="f024e-120">微 USB tooType USB 纜線</span><span class="sxs-lookup"><span data-stu-id="f024e-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="f024e-121">您還需要下列項目，為您的開發環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="f024e-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="f024e-122">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f024e-122">An active Azure subscription.</span></span> <span data-ttu-id="f024e-123">如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="f024e-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f024e-124">執行 Windows 或 Ubuntu 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="f024e-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="f024e-125">若要羽毛 M0 WiFi tooconnect 無線網路。</span><span class="sxs-lookup"><span data-stu-id="f024e-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="f024e-126">網際網路連線 toodownload hello 組態工具。</span><span class="sxs-lookup"><span data-stu-id="f024e-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="f024e-127">[Arduino IDE](https://www.arduino.cc/en/main/software) 1.6.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f024e-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="f024e-128">舊版未使用 hello Azure IoT 中樞程式庫。</span><span class="sxs-lookup"><span data-stu-id="f024e-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="f024e-129">如果您沒有感應器，hello 下列項目是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="f024e-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="f024e-130">您也可以使用模擬的感應器資料的 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="f024e-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="f024e-131">BME280 溫度和溼度感應器</span><span class="sxs-lookup"><span data-stu-id="f024e-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="f024e-132">麵包板</span><span class="sxs-lookup"><span data-stu-id="f024e-132">A breadboard</span></span>
* <span data-ttu-id="f024e-133">M/M 跳線</span><span class="sxs-lookup"><span data-stu-id="f024e-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="f024e-134">聯繫羽毛 M0 WiFi hello 感應器和您的電腦</span><span class="sxs-lookup"><span data-stu-id="f024e-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="f024e-135">在本節中，您可以連接 hello 感應器 tooyour 面板。</span><span class="sxs-lookup"><span data-stu-id="f024e-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="f024e-136">然後您插入以便進一步使用於您裝置的 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="f024e-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="f024e-137">連接 DHT22 氣溫和溼度感應器 tooFeather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="f024e-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="f024e-138">使用 hello breadboard 和跳接器線路 toomake hello 的連線。</span><span class="sxs-lookup"><span data-stu-id="f024e-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="f024e-139">如果您沒有感應器，請略過本節，因為您可以改為使用模擬的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="f024e-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![連接參考](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="f024e-141">感應器 pin 碼，使用下列配線 hello:</span><span class="sxs-lookup"><span data-stu-id="f024e-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="f024e-142">開始 (感應器)</span><span class="sxs-lookup"><span data-stu-id="f024e-142">Start (sensor)</span></span>           | <span data-ttu-id="f024e-143">結束 (電路版)</span><span class="sxs-lookup"><span data-stu-id="f024e-143">End (board)</span></span>            | <span data-ttu-id="f024e-144">纜線顏色</span><span class="sxs-lookup"><span data-stu-id="f024e-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="f024e-145">VDD (針腳 27A)</span><span class="sxs-lookup"><span data-stu-id="f024e-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="f024e-146">3V (針腳 3A)</span><span class="sxs-lookup"><span data-stu-id="f024e-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="f024e-147">紅色纜線</span><span class="sxs-lookup"><span data-stu-id="f024e-147">Red cable</span></span>     |
| <span data-ttu-id="f024e-148">GND (針腳 29A)</span><span class="sxs-lookup"><span data-stu-id="f024e-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="f024e-149">GND (針腳 6A)</span><span class="sxs-lookup"><span data-stu-id="f024e-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="f024e-150">黑色纜線</span><span class="sxs-lookup"><span data-stu-id="f024e-150">Black cable</span></span>   |
| <span data-ttu-id="f024e-151">SCK (針腳 30A)</span><span class="sxs-lookup"><span data-stu-id="f024e-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="f024e-152">SCK (針腳 12A)</span><span class="sxs-lookup"><span data-stu-id="f024e-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="f024e-153">黃色纜線</span><span class="sxs-lookup"><span data-stu-id="f024e-153">Yellow cable</span></span>  |
| <span data-ttu-id="f024e-154">SDO (針腳 31A)</span><span class="sxs-lookup"><span data-stu-id="f024e-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="f024e-155">MI (針腳 14A)</span><span class="sxs-lookup"><span data-stu-id="f024e-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="f024e-156">白色纜線</span><span class="sxs-lookup"><span data-stu-id="f024e-156">White cable</span></span>   |
| <span data-ttu-id="f024e-157">SDI (針腳 32A)</span><span class="sxs-lookup"><span data-stu-id="f024e-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="f024e-158">M0 (針腳 13A)</span><span class="sxs-lookup"><span data-stu-id="f024e-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="f024e-159">藍色纜線</span><span class="sxs-lookup"><span data-stu-id="f024e-159">Blue cable</span></span>    |
| <span data-ttu-id="f024e-160">cs (針腳 33A)</span><span class="sxs-lookup"><span data-stu-id="f024e-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="f024e-161">GPIO 5 (針腳 15J)</span><span class="sxs-lookup"><span data-stu-id="f024e-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="f024e-162">橘色纜線</span><span class="sxs-lookup"><span data-stu-id="f024e-162">Orange cable</span></span>  |

<span data-ttu-id="f024e-163">如需詳細資訊，請參閱 [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Adafruit BME280 溼度 + 氣壓 + 溫度感應器分組) 和 [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts) (Adafruit Feather M0 WiFi 接腳圖)。</span><span class="sxs-lookup"><span data-stu-id="f024e-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="f024e-164">現在，Feather M0 WiFi 應該已經和作用中的感應器連接。</span><span class="sxs-lookup"><span data-stu-id="f024e-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![連接 DHT22 與 Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="f024e-166">羽毛 M0 WiFi tooyour 電腦連線</span><span class="sxs-lookup"><span data-stu-id="f024e-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="f024e-167">使用 hello 微 USB tooType USB 纜線 tooconnect 羽毛 M0 WiFi tooyour 的電腦，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f024e-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![羽毛 Huzzah tooyour 電腦連線](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="f024e-169">新增序列埠權限 (僅限 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="f024e-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="f024e-170">如果您使用 Ubuntu，請確定您擁有 hello 權限 toooperate 上 hello USB 連接埠的羽毛 M0 WiFi。</span><span class="sxs-lookup"><span data-stu-id="f024e-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="f024e-171">tooadd 序列連接埠的權限，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f024e-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="f024e-172">在終端機中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f024e-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="f024e-173">您取得其中一個 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="f024e-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="f024e-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="f024e-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="f024e-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="f024e-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="f024e-176">在 hello 輸出中，請注意，`uucp`或`dialout`hello USB 連接埠 hello 群組擁有者名稱。</span><span class="sxs-lookup"><span data-stu-id="f024e-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="f024e-177">tooadd hello 使用者 toohello 群組，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f024e-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="f024e-178">您可以在 hello 先前步驟中，取得 hello 群組擁有者名稱`<group-owner-name>`。</span><span class="sxs-lookup"><span data-stu-id="f024e-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="f024e-179">`<username>` 是 Ubuntu 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f024e-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="f024e-180">Hello 變更 tooappear，如登出 Ubuntu 然後再重新登入。</span><span class="sxs-lookup"><span data-stu-id="f024e-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="f024e-181">收集感應器資料並傳送 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="f024e-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="f024e-182">在本節中，您可以在 Feather M0 WiFi 上部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f024e-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="f024e-183">hello 範例應用程式可讓 hello 羽毛 M0 WiFi 上的 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="f024e-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="f024e-184">然後會傳送 hello 溫度和溼度從收集的資料 hello BME280 感應器 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f024e-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="f024e-185">從 GitHub 取得 hello 範例應用程式，並準備 hello Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="f024e-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="f024e-186">hello 範例應用程式被裝載於 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="f024e-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="f024e-187">複製 hello 範例儲存機制包含從 GitHub hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f024e-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="f024e-188">tooclone hello 範例儲存機制，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f024e-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="f024e-189">開啟命令提示字元或終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="f024e-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="f024e-190">請您想要儲存的 hello 範例應用程式 toobe tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f024e-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="f024e-191">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f024e-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="f024e-192">安裝羽毛 M0 WiFi hello 套件 hello Arduino IDE 中</span><span class="sxs-lookup"><span data-stu-id="f024e-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="f024e-193">開啟 hello hello 範例應用程式所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f024e-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="f024e-194">Hello hello Arduino IDE 中的應用程式資料夾中開啟 hello app.ino 檔案。</span><span class="sxs-lookup"><span data-stu-id="f024e-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Arduino IDE 中開啟 hello 範例應用程式](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="f024e-196">按一下**檔案** > **喜好設定**(Windows/Linux) 或**Arduino** > **喜好設定**(Mac)，並複製和貼上的 hello 連結底下 hello**其他面板管理員 Url**選項 hello Arduino IDE 喜好設定。</span><span class="sxs-lookup"><span data-stu-id="f024e-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="f024e-197">按一下**工具** > **面板** > **面板管理員**，然後再安裝 hello`Arduino SAMD Boards`版本`1.6.2`或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f024e-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="f024e-198">接著在 hello 相同的視窗，請安裝`Adafruit SAMD Boards`封裝 tooadd hello 面板檔案定義。</span><span class="sxs-lookup"><span data-stu-id="f024e-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![hello esp8266 套件安裝](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="f024e-200">按一下 [工具] > [電路板] > [Adafruit M0 WiFi]。</span><span class="sxs-lookup"><span data-stu-id="f024e-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="f024e-201">安裝驅動程式 (僅限 Windows)。</span><span class="sxs-lookup"><span data-stu-id="f024e-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="f024e-202">當您插入羽毛 M0 WiFi 時，您可能需要 tooinstall 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="f024e-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="f024e-203">按一下[hello hello 網頁上的下載連結](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe)toodownload hello 驅動程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="f024e-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="f024e-204">請遵循 hello 步驟 tooinstall hello 想驅動程式。</span><span class="sxs-lookup"><span data-stu-id="f024e-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="f024e-205">安裝必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="f024e-205">Install necessary libraries</span></span>

1. <span data-ttu-id="f024e-206">在 hello Arduino IDE 中，按一下 **草圖** > **包含程式庫** > **管理程式庫**。</span><span class="sxs-lookup"><span data-stu-id="f024e-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="f024e-207">下列程式庫名稱一個 hello 搜尋。</span><span class="sxs-lookup"><span data-stu-id="f024e-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="f024e-208">為找到的每個程式庫，按一下 [安裝]：</span><span class="sxs-lookup"><span data-stu-id="f024e-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="f024e-209">手動安裝 `Adafruit_WINC1500`。</span><span class="sxs-lookup"><span data-stu-id="f024e-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="f024e-210">跳過[此網站](https://github.com/adafruit/Adafruit_WINC1500)按一下**複製或下載** > **Download ZIP**。</span><span class="sxs-lookup"><span data-stu-id="f024e-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="f024e-211">接著在 Arduino IDE 中，前往 太**草圖** > **包含程式庫** > **新增程式庫.zip**新增 hello 的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="f024e-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="f024e-212">使用 hello 範例應用程式，如果您不需要實際的 BME280 感應器</span><span class="sxs-lookup"><span data-stu-id="f024e-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="f024e-213">如果您不需要實際的 BME280 感應器，hello 範例應用程式可以模擬氣溫和溼度的資料。</span><span class="sxs-lookup"><span data-stu-id="f024e-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="f024e-214">tooset hello 範例應用程式 toouse 模擬資料，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f024e-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="f024e-215">開啟 hello`config.h`檔案在 hello`app`資料夾。</span><span class="sxs-lookup"><span data-stu-id="f024e-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="f024e-216">找出 hello 下列程式碼行並變更 hello 值`false`太`true`:</span><span class="sxs-lookup"><span data-stu-id="f024e-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![設定 hello 範例應用程式模擬 toouse 資料](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="f024e-218">儲存 hello 檔`Control-s`。</span><span class="sxs-lookup"><span data-stu-id="f024e-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="f024e-219">部署 hello 範例應用程式 tooFeather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="f024e-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="f024e-220">在 hello Arduino IDE 中，按一下 **工具** > **連接埠**，然後按一下羽毛 M0 WiFi hello 序列連接埠。</span><span class="sxs-lookup"><span data-stu-id="f024e-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="f024e-221">按一下**草圖** > **上傳**toobuild 和部署 hello 範例應用程式 tooFeather M0 WiFi。</span><span class="sxs-lookup"><span data-stu-id="f024e-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="f024e-222">輸入認證</span><span class="sxs-lookup"><span data-stu-id="f024e-222">Enter your credentials</span></span>

<span data-ttu-id="f024e-223">Hello 上傳成功完成之後，請遵循這些步驟 tooenter 您的認證：</span><span class="sxs-lookup"><span data-stu-id="f024e-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="f024e-224">在 hello Arduino IDE 中，按一下 **工具** > **序列監視器**。</span><span class="sxs-lookup"><span data-stu-id="f024e-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="f024e-225">在 hello hello 序列監視器視窗的右下角，選取 **沒有行尾結束符號**hello hello 左邊的下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="f024e-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="f024e-226">選取**115200 傳輸**hello hello 右邊的下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="f024e-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="f024e-227">Hello hello 上方的輸入方塊中輸入下列資訊，如果您的 hello，然後按一下問 tooprovide**傳送**:</span><span class="sxs-lookup"><span data-stu-id="f024e-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="f024e-228">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="f024e-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="f024e-229">Wi-Fi 密碼</span><span class="sxs-lookup"><span data-stu-id="f024e-229">Wi-Fi password</span></span>
   * <span data-ttu-id="f024e-230">裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="f024e-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="f024e-231">hello 認證資訊會儲存在 hello 羽毛 M0 WiFi EEPROM。</span><span class="sxs-lookup"><span data-stu-id="f024e-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="f024e-232">如果您按一下 hello 羽毛 M0 WiFi 面板 hello 重設 按鈕，hello 範例應用程式會詢問您是否 tooerase hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f024e-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="f024e-233">輸入`Y`tooerase hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="f024e-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="f024e-234">系統會詢問 tooprovide hello 資訊第二次。</span><span class="sxs-lookup"><span data-stu-id="f024e-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="f024e-235">確認已成功執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f024e-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="f024e-236">如果您看見 hello 下列輸出從 hello 序列監視器視窗並 hello 羽毛 M0 WiFi hello 範例應用程式上的 LED 閃爍不停執行成功：</span><span class="sxs-lookup"><span data-stu-id="f024e-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Arduino IDE 中的最終輸出](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="f024e-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f024e-238">Next steps</span></span>

<span data-ttu-id="f024e-239">您已成功連接羽毛 M0 WiFi tooyour IoT 中樞而傳送嗨擷取感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f024e-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

