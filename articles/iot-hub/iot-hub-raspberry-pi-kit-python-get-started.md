---
title: "Raspberry Pi 至 cloud (Python) - 將 Raspberry Pi 連線至 Azure IoT 中樞 | Microsoft Docs"
description: "了解在本教學課程中如何設定及連線 Raspberry Pi 至 Azure IoT 中樞，讓 Raspberry Pi 將資料傳送到 Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot 中樞, raspberry pi 將資料傳送至雲端, raspberry pi 至 cloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 1b1a9dc960846cbc15ce09d0fd106e1492937439
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-python"></a><span data-ttu-id="f0f3f-104">將 Raspberry Pi 連線至 Azure IoT Hub (Python)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="f0f3f-105">在本教學課程中，您會開始了解執行 Raspbian 的 Raspberry Pi 在使用方面的基本知識。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="f0f3f-106">接著會了解如何使用 [Azure IoT 中樞](iot-hub-what-is-iot-hub.md)讓您的裝置順暢地與雲端連線。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="f0f3f-107">如需 Windows 10 IoT 核心範例，請移至 [Windows 開發人員中心](http://www.windowsondevices.com/)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="f0f3f-108">還沒有套件嗎？</span><span class="sxs-lookup"><span data-stu-id="f0f3f-108">Don't have a kit yet?</span></span> <span data-ttu-id="f0f3f-109">試用 [Raspberry Pi 線上模擬器](iot-hub-raspberry-pi-web-simulator-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="f0f3f-110">或在[這裡](https://azure.microsoft.com/develop/iot/starter-kits)購買新的套件。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="f0f3f-111">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="f0f3f-111">What you do</span></span>

* <span data-ttu-id="f0f3f-112">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-112">Create an IoT hub.</span></span>
* <span data-ttu-id="f0f3f-113">在 IoT 中樞對於 Pi 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="f0f3f-114">設定 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="f0f3f-115">在 Pi 上執行範例應用程式，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="f0f3f-116">將 Raspberry Pi 連接至您建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="f0f3f-117">然後，在 Pi 上執行範例應用程式，以收集 BME280 感應器中的溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="f0f3f-118">最後，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="f0f3f-119">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="f0f3f-119">What you learn</span></span>

* <span data-ttu-id="f0f3f-120">如何建立 Azure IoT 中樞，並取得新的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="f0f3f-121">如何連接 Pi 與 BME280 感應器。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="f0f3f-122">如何在 Pi 上執行範例應用程式來收集感應器資料。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="f0f3f-123">如何將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f0f3f-124">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="f0f3f-124">What you need</span></span>

![您需要什麼](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="f0f3f-126">Raspberry Pi 2 或 Raspberry Pi 3 電路板。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="f0f3f-127">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-127">An active Azure subscription.</span></span> <span data-ttu-id="f0f3f-128">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f0f3f-129">連接至 Pi 的監視器、 USB 鍵盤和滑鼠。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="f0f3f-130">執行 Windows 或 Linux 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="f0f3f-131">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-131">An Internet connection.</span></span>
* <span data-ttu-id="f0f3f-132">16 GB 以上的 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="f0f3f-133">一個 USB-SD 配接器或 microSD 記憶卡，以將作業系統映像燒錄到 microSD 記憶卡中。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="f0f3f-134">具備 6 英呎 micro USB 纜線的 5V 2A 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="f0f3f-135">下列項目是選用項目︰</span><span class="sxs-lookup"><span data-stu-id="f0f3f-135">The following items are optional:</span></span>

* <span data-ttu-id="f0f3f-136">組裝的 Adafruit BME280 溫度、壓力溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="f0f3f-137">麵包板。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-137">A breadboard.</span></span>
* <span data-ttu-id="f0f3f-138">6 條 F/M 跳線。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="f0f3f-139">1 顆漫射型 10 mm LED。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="f0f3f-140">這些項目都是選用項目，因為程式碼範例支援模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="f0f3f-141">設定 Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="f0f3f-141">Set up Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="f0f3f-142">安裝 Pi 的 Raspbian 作業系統</span><span class="sxs-lookup"><span data-stu-id="f0f3f-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="f0f3f-143">準備好用來安裝 Raspbian 映像的 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="f0f3f-144">下載 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="f0f3f-145">[下載具備 Desktop 的 Raspbian Jessie](https://www.raspberrypi.org/downloads/raspbian/) (.zip 檔案)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="f0f3f-146">將 Raspbian 映像解壓縮到您電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="f0f3f-147">將 Raspbian 安裝到 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="f0f3f-148">[下載並安裝 Etcher SD 記憶卡燒錄器公用程式](https://etcher.io/)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="f0f3f-149">執行 Etcher 並選取您在步驟 1 中解壓縮的 Raspbian 映像。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="f0f3f-150">選取 microSD 記憶卡磁碟機。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-150">Select the microSD card drive.</span></span> <span data-ttu-id="f0f3f-151">注意：Etcher 可能已經選取正確的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="f0f3f-152">按一下 [Flash] 以將 Raspbian 安裝到 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="f0f3f-153">安裝完成時，請將 microSD 記憶卡從電腦移除。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="f0f3f-154">您可以放心地直接移除 microSD 記憶卡，因為 Etcher 會在完成時自動退出或卸載 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="f0f3f-155">將 microSD 記憶卡插入 Pi。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="f0f3f-156">啟用 SSH 和 I2C</span><span class="sxs-lookup"><span data-stu-id="f0f3f-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="f0f3f-157">將 Pi 連接至監視器、鍵盤和滑鼠，並啟動 Pi，然後使用使用者名稱 `pi` 和密碼 `raspberry` 登入 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="f0f3f-158">按一下 Raspberry 圖示 > [偏好設定] > [Raspberry Pi 組態]。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![[Raspbian 偏好設定] 功能表](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="f0f3f-160">在 [介面]索引標籤上，將 [I2C] 和 [SSH] 設定為 [啟用]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="f0f3f-161">如果您沒有實體感應器，而且想要使用模擬的感應器資料，這便是選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![在 Raspberry Pi 上啟用 I2C 和 SSH](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="f0f3f-163">若要啟用 SSH 和 I2C，您可以在 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 和 [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md) 找到更多參考文件。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="f0f3f-164">將感應器連接至 Pi</span><span class="sxs-lookup"><span data-stu-id="f0f3f-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="f0f3f-165">使用麵包板和跳線將 LED 和 BME280 連接至 Pi，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="f0f3f-166">如果沒有感應器，請[略過本節](#connect-pi-to-the-network)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Raspberry Pi 和感應器連接](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="f0f3f-168">BME280 感應器可以收集溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="f0f3f-169">而如果裝置與雲端之間有通訊，LED 將會閃爍。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="f0f3f-170">針對感應器針腳，請使用下列接線方式：</span><span class="sxs-lookup"><span data-stu-id="f0f3f-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="f0f3f-171">啟動 (感應器和 LED)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="f0f3f-172">結束 (電路版)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-172">End (Board)</span></span>            | <span data-ttu-id="f0f3f-173">纜線顏色</span><span class="sxs-lookup"><span data-stu-id="f0f3f-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="f0f3f-174">VDD (針腳 5G)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="f0f3f-175">3.3V PWR (針腳 1)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="f0f3f-176">白色纜線</span><span class="sxs-lookup"><span data-stu-id="f0f3f-176">White cable</span></span>   |
| <span data-ttu-id="f0f3f-177">GND (針腳 7G)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="f0f3f-178">GND (針腳 6)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-178">GND (Pin 6)</span></span>            | <span data-ttu-id="f0f3f-179">棕色纜線</span><span class="sxs-lookup"><span data-stu-id="f0f3f-179">Brown cable</span></span>   |
| <span data-ttu-id="f0f3f-180">SDI (針腳 10G)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="f0f3f-181">I2C1 SDA (針腳 3)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="f0f3f-182">紅色纜線</span><span class="sxs-lookup"><span data-stu-id="f0f3f-182">Red cable</span></span>     |
| <span data-ttu-id="f0f3f-183">SCK (針腳 8G)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="f0f3f-184">I2C1 SCL (針腳 5)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="f0f3f-185">橘色纜線</span><span class="sxs-lookup"><span data-stu-id="f0f3f-185">Orange cable</span></span>  |
| <span data-ttu-id="f0f3f-186">LED VDD (針腳 18F)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="f0f3f-187">GPIO 24 (針腳 18)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="f0f3f-188">白色纜線</span><span class="sxs-lookup"><span data-stu-id="f0f3f-188">White cable</span></span>   |
| <span data-ttu-id="f0f3f-189">LED GND (針腳 17F)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="f0f3f-190">GND (針腳 20)</span><span class="sxs-lookup"><span data-stu-id="f0f3f-190">GND (Pin 20)</span></span>           | <span data-ttu-id="f0f3f-191">黑色纜線</span><span class="sxs-lookup"><span data-stu-id="f0f3f-191">Black cable</span></span>   |

<span data-ttu-id="f0f3f-192">按一下以檢視 [Raspberry Pi 2 和 3 針腳對應](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi)進行參考。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="f0f3f-193">將 BME280 成功連接至 Raspberry Pi 之後，應該如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![連接的 Pi 和 BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="f0f3f-195">將 Pi 連線到網路</span><span class="sxs-lookup"><span data-stu-id="f0f3f-195">Connect Pi to the network</span></span>

<span data-ttu-id="f0f3f-196">透過 micro USB 纜線和電源供應器來開啟 Pi。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="f0f3f-197">使用乙太網路纜線將 Pi 連接到有線網路，或遵循來自 Raspberry Pi Foundation 的[指示](https://www.raspberrypi.org/learning/software-guide/wifi/)，將 Pi 連接到無線網路。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="f0f3f-198">在 Pi 成功連線到網路之後，您需要記下 [Pi 的 IP 位址](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![已連接到有線網路](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="f0f3f-200">請確定 Pi 是連接到與您電腦相同的網路。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="f0f3f-201">例如，如果您的電腦連線到無線網路，而 Pi 連線到有線網路，您可能不會在 devdisco 輸出中看到 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="f0f3f-202">在 Pi 上執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f0f3f-202">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="f0f3f-203">安裝必要條件套件</span><span class="sxs-lookup"><span data-stu-id="f0f3f-203">Install the prerequisite packages</span></span>

<span data-ttu-id="f0f3f-204">使用下列其中一個 SSH 用戶端，從主機電腦連接到 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="f0f3f-205">**Windows 使用者**</span><span class="sxs-lookup"><span data-stu-id="f0f3f-205">**Windows Users**</span></span>
   1. <span data-ttu-id="f0f3f-206">下載並安裝適用於 Windows 的 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="f0f3f-207">將 Pi 的 IP 位址複製到 [主機名稱] 或 [IP 位址] 區段，並且選取 SSH 作為連線類型。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   
   <span data-ttu-id="f0f3f-208">**Mac 和 Ubuntu 使用者**</span><span class="sxs-lookup"><span data-stu-id="f0f3f-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="f0f3f-209">在 Ubuntu 或 macOS 上使用內建的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-209">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="f0f3f-210">您可能需要執行 `ssh pi@<ip address of pi>`，才能透過 SSH 來連線 Pi。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="f0f3f-211">預設使用者名稱為 `pi`，密碼為 `raspberry`。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-211">The default username is `pi` , and the password is `raspberry`.</span></span>


### <a name="configure-the-sample-application"></a><span data-ttu-id="f0f3f-212">設定範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f0f3f-212">Configure the sample application</span></span>

1. <span data-ttu-id="f0f3f-213">執行下列命令，複製範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="f0f3f-213">Clone the sample application by running the following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="f0f3f-214">執行下列命令以開啟組態檔：</span><span class="sxs-lookup"><span data-stu-id="f0f3f-214">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="f0f3f-215">此檔案中有 5 個巨集可供設定。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="f0f3f-216">第一個是 `MESSAGE_TIMESPAN`，這可定義傳送至雲端的兩個訊息之間相隔的時間間隔 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="f0f3f-217">第二個是 `SIMULATED_DATA`，這是是否使用模擬感應器資料的布林值。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span></span> <span data-ttu-id="f0f3f-218">`I2C_ADDRESS` 是 BME280 感應器連線的 I2C 位址。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="f0f3f-219">`GPIO_PIN_ADDRESS` 是 LED 的 GPIO 位址。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span></span> <span data-ttu-id="f0f3f-220">最後一個是 `BLINK_TIMESPAN`，可定義 LED 開啟時以毫秒為單位的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="f0f3f-221">如果**沒有感應器**，請將 `SIMULATED_DATA` 值設定為 `True`，使範例應用程式建立和使用模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="f0f3f-222">按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="f0f3f-223">建置並執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="f0f3f-223">Build and run the sample application</span></span>

1. <span data-ttu-id="f0f3f-224">執行下列命令，建置範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-224">Build the sample application by running the following command.</span></span> <span data-ttu-id="f0f3f-225">由於 Azure IoT SDK for Python 是 Azure IoT 裝置 C SDK 之上的包裝函式，如果您想要或需要從來源程式碼產生 Python 程式庫，則必須編譯 C 程式庫。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="f0f3f-226">您也可以執行 `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]` 指定想要的版本。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="f0f3f-227">如果執行不含參數的指令碼，指令碼會自動偵測已安裝的 python 版本 (搜尋序列 2.7->3.4->3.5)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="f0f3f-228">請確定 Python 版本在建置和執行期間保持一致。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="f0f3f-229">在 RAM 小於 1GB 的 Linux 裝置上建置 Python 用戶端程式庫 (iothub_client.so) 時，您可能會在建置 iothub_client_python.cpp 時看到組建卡在 98%，如下所示 `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="f0f3f-230">如果遇到此問題，請在該段期間內在另一個終端機視窗中使用 `free -m command` 來檢查裝置的記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="f0f3f-231">如果在編譯 iothub_client_python.cpp 檔案時記憶體不足，則需要暫時增加交換空間來取得更多可用記憶體，才能成功建置 Python 用戶端裝置 SDK 程式庫。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="f0f3f-232">執行下列命令，執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="f0f3f-232">Run the sample application by running the following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="f0f3f-233">確定複製裝置連接字串，並貼到單引號中。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-233">Make sure you copy-paste the device connection string into the single quotes.</span></span> <span data-ttu-id="f0f3f-234">如果您使用 python 3，則可以使用命令 `python3 app.py '<your Azure IoT hub device connection string>'`。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="f0f3f-235">您應該會看見下列輸出，顯示傳送至 IoT 中樞的感應器資料和訊息。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![輸出 - 從 Raspberry Pi 傳送至 IoT 中樞的感應器資料](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="f0f3f-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0f3f-237">Next steps</span></span>

<span data-ttu-id="f0f3f-238">您已執行範例應用程式收集感應器資料並傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="f0f3f-239">若要查看 Raspberry Pi 傳送給 IoT 中樞的訊息，或者在命令列介面中將訊息傳送給 Raspberry Pi，請參閱[使用 iothub-explorer 管理雲端裝置訊息教學課程](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)。</span><span class="sxs-lookup"><span data-stu-id="f0f3f-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
