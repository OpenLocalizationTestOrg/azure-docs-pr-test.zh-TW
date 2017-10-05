---
title: "M0 連線到雲端：將 Feather M0 WiFi 連線到 Azure IoT 中樞 | Microsoft Docs"
description: "了解如何設定及連線 Adafruit Feather M0 WiFi 和 Azure IoT 中樞，在本教學課程中將資料傳送到 Azure 雲端平台。"
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
ms.openlocfilehash: 0dcf6b46a4c6c743c713d24ce7844e801b278dcf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-adafruit-feather-m0-wifi-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="92423-103">將 Adafruit Feather M0 WiFi 連線到位於雲端的 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="92423-103">Connect Adafruit Feather M0 WiFi to Azure IoT Hub in the cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280、Feather M0 WiFi 與 IoT 中樞之間的連線](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="92423-105">在本教學課程中，您一開始會先了解使用 Arduino 面板的基本知識。</span><span class="sxs-lookup"><span data-stu-id="92423-105">In this tutorial, you begin by learning the basics of working with your Arduino board.</span></span> <span data-ttu-id="92423-106">接著會了解如何使用 [Azure IoT 中樞](iot-hub-what-is-iot-hub.md)讓您的裝置順暢地與雲端連線。</span><span class="sxs-lookup"><span data-stu-id="92423-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="92423-107">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="92423-107">What you do</span></span>

<span data-ttu-id="92423-108">將 Adafruit Feather M0 WiFi 連線到您將建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="92423-108">Connect Adafruit Feather M0 WiFi to an IoT hub that you create.</span></span> <span data-ttu-id="92423-109">然後，在 M0 WiF 上執行範例應用程式，以收集 BME280 感應器中的溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="92423-109">Then you run a sample application on M0 WiFi to collect the temperature and humidity data from a BME280.</span></span> <span data-ttu-id="92423-110">最後，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="92423-110">Finally, you send the sensor data to your IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="92423-111">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="92423-111">What you learn</span></span>

* <span data-ttu-id="92423-112">如何建立 IoT 中樞並為 Feather M0 WiFi 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="92423-112">How to create an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="92423-113">如何連接 Feather M0 WiFi 與感應器和電腦</span><span class="sxs-lookup"><span data-stu-id="92423-113">How to connect Feather M0 WiFi with the sensor and your computer</span></span>
* <span data-ttu-id="92423-114">如何在 Feather M0 WiFi 上執行範例應用程式來收集感應器資料</span><span class="sxs-lookup"><span data-stu-id="92423-114">How to collect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="92423-115">如何將感應器資料傳送至 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="92423-115">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="92423-116">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="92423-116">What you need</span></span>

![本教學課程所需的零件](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="92423-118">若要完成此作業，您需要 Feather M0 WiFi 入門套件中的下列零件：</span><span class="sxs-lookup"><span data-stu-id="92423-118">To complete this operation, you need the following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="92423-119">Feather M0 WiFi 面板</span><span class="sxs-lookup"><span data-stu-id="92423-119">The Feather M0 WiFi board</span></span>
* <span data-ttu-id="92423-120">Micro USB 轉 Type A 的 USB 纜線</span><span class="sxs-lookup"><span data-stu-id="92423-120">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="92423-121">您的開發環境還需要下列事項：</span><span class="sxs-lookup"><span data-stu-id="92423-121">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="92423-122">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="92423-122">An active Azure subscription.</span></span> <span data-ttu-id="92423-123">如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="92423-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="92423-124">執行 Windows 或 Ubuntu 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="92423-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="92423-125">供 Feather M0 WiFi 連線的無線網路。</span><span class="sxs-lookup"><span data-stu-id="92423-125">A wireless network for Feather M0 WiFi to connect to.</span></span>
* <span data-ttu-id="92423-126">用來下載設定工具的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="92423-126">An Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="92423-127">[Arduino IDE](https://www.arduino.cc/en/main/software) 1.6.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="92423-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="92423-128">舊版無法與 Azure IoT 中樞程式庫搭配運作。</span><span class="sxs-lookup"><span data-stu-id="92423-128">Earlier versions don't work with the Azure IoT Hub library.</span></span>

<span data-ttu-id="92423-129">如果您沒有感應器，下列項目可供選用。</span><span class="sxs-lookup"><span data-stu-id="92423-129">If you don’t have a sensor, the following items are optional.</span></span> <span data-ttu-id="92423-130">您也可以選擇使用模擬的感應器資料：</span><span class="sxs-lookup"><span data-stu-id="92423-130">You also have the option of using simulated sensor data:</span></span>

* <span data-ttu-id="92423-131">BME280 溫度和溼度感應器</span><span class="sxs-lookup"><span data-stu-id="92423-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="92423-132">麵包板</span><span class="sxs-lookup"><span data-stu-id="92423-132">A breadboard</span></span>
* <span data-ttu-id="92423-133">M/M 跳線</span><span class="sxs-lookup"><span data-stu-id="92423-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-the-sensor-and-your-computer"></a><span data-ttu-id="92423-134">連接 Feather M0 WiFi 與感應器和電腦</span><span class="sxs-lookup"><span data-stu-id="92423-134">Connect Feather M0 WiFi with the sensor and your computer</span></span>
<span data-ttu-id="92423-135">在本節中，您可以將感應器連接至您的面板。</span><span class="sxs-lookup"><span data-stu-id="92423-135">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="92423-136">然後您可以將您的裝置插入電腦持續使用。</span><span class="sxs-lookup"><span data-stu-id="92423-136">Then you plug in your device to your computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-m0-wifi"></a><span data-ttu-id="92423-137">將 DHT22 溫度和溼度感應器連接至 Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="92423-137">Connect a DHT22 temperature and humidity sensor to Feather M0 WiFi</span></span>

<span data-ttu-id="92423-138">使用試驗電路板 和跳線來進行連接。</span><span class="sxs-lookup"><span data-stu-id="92423-138">Use the breadboard and jumper wires to make the connection.</span></span> <span data-ttu-id="92423-139">如果您沒有感應器，請略過本節，因為您可以改為使用模擬的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="92423-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![連接參考](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="92423-141">針對感應器針腳，請使用下列接線方式：</span><span class="sxs-lookup"><span data-stu-id="92423-141">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="92423-142">開始 (感應器)</span><span class="sxs-lookup"><span data-stu-id="92423-142">Start (sensor)</span></span>           | <span data-ttu-id="92423-143">結束 (電路版)</span><span class="sxs-lookup"><span data-stu-id="92423-143">End (board)</span></span>            | <span data-ttu-id="92423-144">纜線顏色</span><span class="sxs-lookup"><span data-stu-id="92423-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="92423-145">VDD (針腳 27A)</span><span class="sxs-lookup"><span data-stu-id="92423-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="92423-146">3V (針腳 3A)</span><span class="sxs-lookup"><span data-stu-id="92423-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="92423-147">紅色纜線</span><span class="sxs-lookup"><span data-stu-id="92423-147">Red cable</span></span>     |
| <span data-ttu-id="92423-148">GND (針腳 29A)</span><span class="sxs-lookup"><span data-stu-id="92423-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="92423-149">GND (針腳 6A)</span><span class="sxs-lookup"><span data-stu-id="92423-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="92423-150">黑色纜線</span><span class="sxs-lookup"><span data-stu-id="92423-150">Black cable</span></span>   |
| <span data-ttu-id="92423-151">SCK (針腳 30A)</span><span class="sxs-lookup"><span data-stu-id="92423-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="92423-152">SCK (針腳 12A)</span><span class="sxs-lookup"><span data-stu-id="92423-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="92423-153">黃色纜線</span><span class="sxs-lookup"><span data-stu-id="92423-153">Yellow cable</span></span>  |
| <span data-ttu-id="92423-154">SDO (針腳 31A)</span><span class="sxs-lookup"><span data-stu-id="92423-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="92423-155">MI (針腳 14A)</span><span class="sxs-lookup"><span data-stu-id="92423-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="92423-156">白色纜線</span><span class="sxs-lookup"><span data-stu-id="92423-156">White cable</span></span>   |
| <span data-ttu-id="92423-157">SDI (針腳 32A)</span><span class="sxs-lookup"><span data-stu-id="92423-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="92423-158">M0 (針腳 13A)</span><span class="sxs-lookup"><span data-stu-id="92423-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="92423-159">藍色纜線</span><span class="sxs-lookup"><span data-stu-id="92423-159">Blue cable</span></span>    |
| <span data-ttu-id="92423-160">cs (針腳 33A)</span><span class="sxs-lookup"><span data-stu-id="92423-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="92423-161">GPIO 5 (針腳 15J)</span><span class="sxs-lookup"><span data-stu-id="92423-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="92423-162">橘色纜線</span><span class="sxs-lookup"><span data-stu-id="92423-162">Orange cable</span></span>  |

<span data-ttu-id="92423-163">如需詳細資訊，請參閱 [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Adafruit BME280 溼度 + 氣壓 + 溫度感應器分組) 和 [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts) (Adafruit Feather M0 WiFi 接腳圖)。</span><span class="sxs-lookup"><span data-stu-id="92423-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="92423-164">現在，Feather M0 WiFi 應該已經和作用中的感應器連接。</span><span class="sxs-lookup"><span data-stu-id="92423-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![連接 DHT22 與 Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-to-your-computer"></a><span data-ttu-id="92423-166">將 Feather M0 WiFi 連接到電腦</span><span class="sxs-lookup"><span data-stu-id="92423-166">Connect Feather M0 WiFi to your computer</span></span>

<span data-ttu-id="92423-167">請使用 Micro USB 轉 Type A 的 USB 纜線將 Feather M0 WiFi 連接到電腦，如下所示：</span><span class="sxs-lookup"><span data-stu-id="92423-167">Use the Micro USB to Type A USB cable to connect Feather M0 WiFi to your computer, as shown:</span></span>

![將 Feather Huzzah 連接到電腦](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="92423-169">新增序列埠權限 (僅限 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="92423-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="92423-170">如果您使用 Ubuntu，請確定您具有操作 Feather M0 WiFi 的 USB 連接埠所需的權限。</span><span class="sxs-lookup"><span data-stu-id="92423-170">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="92423-171">若要新增序列埠權限，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="92423-171">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="92423-172">在終端機中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="92423-172">At a terminal, run the following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="92423-173">您會得到下列其中一個輸出︰</span><span class="sxs-lookup"><span data-stu-id="92423-173">You get one of the following outputs:</span></span>

   * <span data-ttu-id="92423-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="92423-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="92423-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="92423-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="92423-176">在輸出中，請注意 `uucp` 或 `dialout` 是 USB 連接埠的群組擁有者名稱。</span><span class="sxs-lookup"><span data-stu-id="92423-176">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

2. <span data-ttu-id="92423-177">請執行下列命令，將使用者新增至群組︰</span><span class="sxs-lookup"><span data-stu-id="92423-177">To add the user to the group, run the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="92423-178">`<group-owner-name>` 是您在上一個步驟中取得的群組擁有者名稱。</span><span class="sxs-lookup"><span data-stu-id="92423-178">In the previous step, you obtained the group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="92423-179">`<username>` 是 Ubuntu 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="92423-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="92423-180">登出 Ubuntu，然後再次登入，以顯示變更。</span><span class="sxs-lookup"><span data-stu-id="92423-180">For the change to appear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="92423-181">收集感應器資料，並將它傳送至 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="92423-181">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="92423-182">在本節中，您可以在 Feather M0 WiFi 上部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="92423-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="92423-183">範例應用程式會讓 LED 在 Feather M0 WiFi 上閃爍。</span><span class="sxs-lookup"><span data-stu-id="92423-183">The sample application makes the LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="92423-184">然後，將從 BME280 感應器收集的溫度和溼度資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="92423-184">It then sends the temperature and humidity data collected from the BME280 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github-and-prepare-the-arduino-ide"></a><span data-ttu-id="92423-185">從 GitHub 取得範例應用程式，並準備 Arduino IDE。</span><span class="sxs-lookup"><span data-stu-id="92423-185">Get the sample application from GitHub and prepare the Arduino IDE</span></span>

<span data-ttu-id="92423-186">範例應用程式會裝載在 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="92423-186">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="92423-187">請從 GitHub 複製包含範例應用程式的範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="92423-187">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="92423-188">若要複製範例存放庫，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="92423-188">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="92423-189">開啟命令提示字元或終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="92423-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="92423-190">移至想要儲存範例應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="92423-190">Go to a folder where you want the sample application to be stored.</span></span>
3. <span data-ttu-id="92423-191">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="92423-191">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-the-package-for-feather-m0-wifi-in-the-arduino-ide"></a><span data-ttu-id="92423-192">在 Arduino IDE 中安裝 Feather M0 WiFi 套件</span><span class="sxs-lookup"><span data-stu-id="92423-192">Install the package for Feather M0 WiFi in the Arduino IDE</span></span>

1. <span data-ttu-id="92423-193">開啟範例應用程式儲存所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="92423-193">Open the folder where the sample application is stored.</span></span>

2. <span data-ttu-id="92423-194">在 Arduino IDE 中開啟應用程式資料夾中的 app.ino 檔案。</span><span class="sxs-lookup"><span data-stu-id="92423-194">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![在 Arduino IDE 中開啟範例應用程式](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="92423-196">按一下 [檔案] > [喜好設定] (Windows/Linux) 或 [Arduino] > [喜好設定] (Mac)，然後將下列連結複製貼入 Arduino IDE 喜好設定的 [Additional Boards Manager URLs] (其他面板管理員 URL) 選項。</span><span class="sxs-lookup"><span data-stu-id="92423-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste the link below into the **Additional Boards Manager URLs** option in the Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="92423-197">按一下 [工具] > [面板] > [面板管理員]，然後安裝 `Arduino SAMD Boards` 版本 `1.6.2` 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="92423-197">Click **Tools** > **Board** > **Boards Manager**, and then install the `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="92423-198">然後在相同的視窗中，安裝 `Adafruit SAMD Boards` 套件以新增面板檔案定義。</span><span class="sxs-lookup"><span data-stu-id="92423-198">Then in the same window, install `Adafruit SAMD Boards` package to add the board file definitions.</span></span>

   ![已安裝 esp8266 套件](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="92423-200">按一下 [工具] > [電路板] > [Adafruit M0 WiFi]。</span><span class="sxs-lookup"><span data-stu-id="92423-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="92423-201">安裝驅動程式 (僅限 Windows)。</span><span class="sxs-lookup"><span data-stu-id="92423-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="92423-202">當您插入 Feather M0 WiFi 時，您可能需要安裝驅動程式。</span><span class="sxs-lookup"><span data-stu-id="92423-202">When you plug in Feather M0 WiFi, you might need to install a driver.</span></span> <span data-ttu-id="92423-203">按一下[網頁上的下載連結](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe)下載驅動程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="92423-203">Click [the download link on the webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) to download the driver installer.</span></span> <span data-ttu-id="92423-204">請遵循步驟安裝想要的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="92423-204">Follow the steps to install the drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="92423-205">安裝必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="92423-205">Install necessary libraries</span></span>

1. <span data-ttu-id="92423-206">在 Arduino IDE 中，按一下 [草圖] > [包含程式庫] > [管理程式庫]。</span><span class="sxs-lookup"><span data-stu-id="92423-206">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="92423-207">逐一搜尋下列程式庫名稱。</span><span class="sxs-lookup"><span data-stu-id="92423-207">Search for the following library names one by one.</span></span> <span data-ttu-id="92423-208">為找到的每個程式庫，按一下 [安裝]：</span><span class="sxs-lookup"><span data-stu-id="92423-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="92423-209">手動安裝 `Adafruit_WINC1500`。</span><span class="sxs-lookup"><span data-stu-id="92423-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="92423-210">移至[此網站](https://github.com/adafruit/Adafruit_WINC1500)並按一下 [複製或下載] > [下載 ZIP]。</span><span class="sxs-lookup"><span data-stu-id="92423-210">Go to [this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="92423-211">然後在 Arduino IDE 中，移至 [草圖] > [包含程式庫] > [新增 .zip 程式庫]，然後新增 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="92423-211">Then in your Arduino IDE, go to **Sketch** > **Include Library** > **Add .zip Library** and add the zip file.</span></span>

### <a name="use-the-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="92423-212">如果沒有實體的 BME280 感應器，請使用範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="92423-212">Use the sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="92423-213">如果您沒有實體的 BME280 感應器，範例應用程式可以模擬溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="92423-213">If you don’t have a real BME280 sensor, the sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="92423-214">若要設讓範例應用程式以使用模擬資料，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="92423-214">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="92423-215">開啟 `app` 資料夾中的 `config.h` 檔案。</span><span class="sxs-lookup"><span data-stu-id="92423-215">Open the `config.h` file in the `app` folder.</span></span>

2. <span data-ttu-id="92423-216">找出下面這行程式碼，並將值從 `false` 變更為 `true`：</span><span class="sxs-lookup"><span data-stu-id="92423-216">Locate the following line of code and change the value from `false` to `true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![設定範例應用程式以使用模擬資料](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="92423-218">使用 `Control-s` 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="92423-218">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-m0-wifi"></a><span data-ttu-id="92423-219">將範例應用程式部署至 Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="92423-219">Deploy the sample application to Feather M0 WiFi</span></span>

1. <span data-ttu-id="92423-220">在 Arduino IDE 中，按一下 [工具] > [連接埠]，然後按一下 Feather M0 WiFi 的序列埠。</span><span class="sxs-lookup"><span data-stu-id="92423-220">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="92423-221">按一下 [草圖] > [上傳]，以建置範例應用程式並將其部署至 Feather M0 WiFi。</span><span class="sxs-lookup"><span data-stu-id="92423-221">Click **Sketch** > **Upload** to build and deploy the sample application to Feather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="92423-222">輸入認證</span><span class="sxs-lookup"><span data-stu-id="92423-222">Enter your credentials</span></span>

<span data-ttu-id="92423-223">上傳程序成功完成後，請遵循這些步驟來輸入認證：</span><span class="sxs-lookup"><span data-stu-id="92423-223">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="92423-224">在 Arduino IDE 中，按一下 [工具] > [序列監視器]。</span><span class="sxs-lookup"><span data-stu-id="92423-224">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="92423-225">在序列監視器視窗的右下角，在左邊的下拉式清單中選取 [No line ending] (沒有行尾結束符號)。</span><span class="sxs-lookup"><span data-stu-id="92423-225">In the lower-right corner of the serial monitor window, select **No line ending** in the drop-down list on the left.</span></span>
3. <span data-ttu-id="92423-226">在右邊的下拉式清單中選取 [115200 傳輸速率]。</span><span class="sxs-lookup"><span data-stu-id="92423-226">Select **115200 baud** in the drop-down list on the right.</span></span>
4. <span data-ttu-id="92423-227">如果系統要求您提供，請在上方的輸入方塊中輸入下列資訊，然後按一下 [傳送]：</span><span class="sxs-lookup"><span data-stu-id="92423-227">In the input box at the top, enter the following information if you're asked to provide it, and click **Send**:</span></span>

   * <span data-ttu-id="92423-228">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="92423-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="92423-229">Wi-Fi 密碼</span><span class="sxs-lookup"><span data-stu-id="92423-229">Wi-Fi password</span></span>
   * <span data-ttu-id="92423-230">裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="92423-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="92423-231">認證資訊會儲存在 Feather M0 WiFi 的 EEPROM 中。</span><span class="sxs-lookup"><span data-stu-id="92423-231">The credential information is stored in the EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="92423-232">如果您按一下 Feather M0 WiFi 電路板上的重設按鈕，範例應用程式會詢問您是否要清除資訊。</span><span class="sxs-lookup"><span data-stu-id="92423-232">If you click the reset button on the Feather M0 WiFi board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="92423-233">輸入 `Y` 清除資訊。</span><span class="sxs-lookup"><span data-stu-id="92423-233">Enter `Y` to erase the information.</span></span> <span data-ttu-id="92423-234">系統會再次要求您提供資訊。</span><span class="sxs-lookup"><span data-stu-id="92423-234">You're asked to provide the information a second time.</span></span>

### <a name="verify-that-the-sample-application-is-running-successfully"></a><span data-ttu-id="92423-235">確認範例應用程式已成功執行</span><span class="sxs-lookup"><span data-stu-id="92423-235">Verify that the sample application is running successfully</span></span>

<span data-ttu-id="92423-236">如果您在序列監視器視窗看到下列輸出，並在 Feather M0 WiFi 上看到閃爍的 LED，則表示範例應用程式已成功執行：</span><span class="sxs-lookup"><span data-stu-id="92423-236">If you see the following output from the serial monitor window and the blinking LED on Feather M0 WiFi, the sample application is running successfully:</span></span>

![Arduino IDE 中的最終輸出](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="92423-238">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92423-238">Next steps</span></span>

<span data-ttu-id="92423-239">Feather M0 WiFi 已成功連線到 IoT 中樞，並將擷取到的感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="92423-239">You have successfully connected Feather M0 WiFi to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

