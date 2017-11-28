---
title: "Raspberry Pi 至 cloud (Node.js) - 將 Raspberry Pi 連接至 Azure IoT 中樞 | Microsoft Docs"
description: "了解在本教學課程中如何設定及連線 Raspberry Pi 至 Azure IoT 中樞，讓 Raspberry Pi 將資料傳送到 Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot 中樞, raspberry pi 將資料傳送至雲端, raspberry pi 至 cloud"
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f48c4bd27b1df1d02090ed51172f943e50c76c3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="1ac4d-104">將 Raspberry Pi 連接至 Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="1ac4d-105">在本教學課程中，您會開始了解執行 Raspbian 的 Raspberry Pi 在使用方面的基本知識。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="1ac4d-106">接著會了解如何使用 [Azure IoT 中樞](iot-hub-what-is-iot-hub.md)讓您的裝置順暢地與雲端連線。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="1ac4d-107">如需 Windows 10 IoT 核心範例，請移至 [Windows 開發人員中心](http://www.windowsondevices.com/)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="1ac4d-108">還沒有套件嗎？</span><span class="sxs-lookup"><span data-stu-id="1ac4d-108">Don't have a kit yet?</span></span> <span data-ttu-id="1ac4d-109">試用 [Raspberry Pi 線上模擬器](iot-hub-raspberry-pi-web-simulator-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="1ac4d-110">或在[這裡](https://azure.microsoft.com/develop/iot/starter-kits)購買新的套件。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>


## <a name="what-you-do"></a><span data-ttu-id="1ac4d-111">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="1ac4d-111">What you do</span></span>

* <span data-ttu-id="1ac4d-112">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-112">Create an IoT hub.</span></span>
* <span data-ttu-id="1ac4d-113">在 IoT 中樞對於 Pi 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="1ac4d-114">設定 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="1ac4d-115">在 Pi 上執行範例應用程式，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="1ac4d-116">將 Raspberry Pi 連接至您建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="1ac4d-117">然後，在 Pi 上執行範例應用程式，以收集 BME280 感應器中的溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="1ac4d-118">最後，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="1ac4d-119">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="1ac4d-119">What you learn</span></span>

* <span data-ttu-id="1ac4d-120">如何建立 Azure IoT 中樞，並取得新的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="1ac4d-121">如何連接 Pi 與 BME280 感應器。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="1ac4d-122">如何在 Pi 上執行範例應用程式來收集感應器資料。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="1ac4d-123">如何將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1ac4d-124">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="1ac4d-124">What you need</span></span>

![您需要什麼](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="1ac4d-126">Raspberry Pi 2 或 Raspberry Pi 3 電路板。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="1ac4d-127">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-127">An active Azure subscription.</span></span> <span data-ttu-id="1ac4d-128">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="1ac4d-129">連接至 Pi 的監視器、 USB 鍵盤和滑鼠。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="1ac4d-130">執行 Windows 或 Linux 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="1ac4d-131">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-131">An Internet connection.</span></span>
* <span data-ttu-id="1ac4d-132">16 GB 以上的 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="1ac4d-133">一個 USB-SD 配接器或 microSD 記憶卡，以將作業系統映像燒錄到 microSD 記憶卡中。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="1ac4d-134">具備 6 英呎 micro USB 纜線的 5V 2A 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="1ac4d-135">下列項目是選用項目︰</span><span class="sxs-lookup"><span data-stu-id="1ac4d-135">The following items are optional:</span></span>

* <span data-ttu-id="1ac4d-136">組裝的 Adafruit BME280 溫度、壓力溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="1ac4d-137">麵包板。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-137">A breadboard.</span></span>
* <span data-ttu-id="1ac4d-138">6 條 F/M 跳線。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="1ac4d-139">1 顆漫射型 10 mm LED。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="1ac4d-140">這些項目都是選用項目，因為程式碼範例支援模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="1ac4d-141">設定 Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="1ac4d-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="1ac4d-142">安裝 Pi 的 Raspbian 作業系統</span><span class="sxs-lookup"><span data-stu-id="1ac4d-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="1ac4d-143">準備好用來安裝 Raspbian 映像的 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="1ac4d-144">下載 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="1ac4d-145">[下載具備 Desktop 的 Raspbian Jessie](https://www.raspberrypi.org/downloads/raspbian/) (.zip 檔案)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="1ac4d-146">將 Raspbian 映像解壓縮到您電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="1ac4d-147">將 Raspbian 安裝到 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="1ac4d-148">[下載並安裝 Etcher SD 記憶卡燒錄器公用程式](https://etcher.io/)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="1ac4d-149">執行 Etcher 並選取您在步驟 1 中解壓縮的 Raspbian 映像。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="1ac4d-150">選取 microSD 記憶卡磁碟機。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-150">Select the microSD card drive.</span></span> <span data-ttu-id="1ac4d-151">注意：Etcher 可能已經選取正確的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="1ac4d-152">按一下 [Flash] 以將 Raspbian 安裝到 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="1ac4d-153">安裝完成時，請將 microSD 記憶卡從電腦移除。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="1ac4d-154">您可以放心地直接移除 microSD 記憶卡，因為 Etcher 會在完成時自動退出或卸載 microSD 記憶卡。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="1ac4d-155">將 microSD 記憶卡插入 Pi。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="1ac4d-156">啟用 SSH 和 I2C</span><span class="sxs-lookup"><span data-stu-id="1ac4d-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="1ac4d-157">將 Pi 連接至監視器、鍵盤和滑鼠，並啟動 Pi，然後使用使用者名稱 `pi` 和密碼 `raspberry` 登入 Raspbian。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="1ac4d-158">按一下 Raspberry 圖示 > [偏好設定] > [Raspberry Pi 組態]。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![[Raspbian 偏好設定] 功能表](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="1ac4d-160">在 [介面]索引標籤上，將 [I2C] 和 [SSH] 設定為 [啟用]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="1ac4d-161">如果您沒有實體感應器，而且想要使用模擬的感應器資料，這便是選擇性步驟。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![在 Raspberry Pi 上啟用 I2C 和 SSH](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="1ac4d-163">若要啟用 I2C 和 SPI，您可以在 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 和[Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c) 找到更多參考文件。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="1ac4d-164">將感應器連接至 Pi</span><span class="sxs-lookup"><span data-stu-id="1ac4d-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="1ac4d-165">使用麵包板和跳線將 LED 和 BME280 連接至 Pi，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="1ac4d-166">如果沒有感應器，請[略過本節](#connect-pi-to-the-network)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Raspberry Pi 和感應器連接](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="1ac4d-168">BME280 感應器可以收集溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="1ac4d-169">而如果裝置與雲端之間有通訊，LED 將會閃爍。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="1ac4d-170">針對感應器針腳，請使用下列接線方式：</span><span class="sxs-lookup"><span data-stu-id="1ac4d-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="1ac4d-171">啟動 (感應器和 LED)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="1ac4d-172">結束 (電路版)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-172">End (Board)</span></span>            | <span data-ttu-id="1ac4d-173">纜線顏色</span><span class="sxs-lookup"><span data-stu-id="1ac4d-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="1ac4d-174">VDD (針腳 5G)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="1ac4d-175">3.3V PWR (針腳 1)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="1ac4d-176">白色纜線</span><span class="sxs-lookup"><span data-stu-id="1ac4d-176">White cable</span></span>   |
| <span data-ttu-id="1ac4d-177">GND (針腳 7G)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="1ac4d-178">GND (針腳 6)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-178">GND (Pin 6)</span></span>            | <span data-ttu-id="1ac4d-179">棕色纜線</span><span class="sxs-lookup"><span data-stu-id="1ac4d-179">Brown cable</span></span>   |
| <span data-ttu-id="1ac4d-180">SDI (針腳 10G)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="1ac4d-181">I2C1 SDA (針腳 3)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="1ac4d-182">紅色纜線</span><span class="sxs-lookup"><span data-stu-id="1ac4d-182">Red cable</span></span>     |
| <span data-ttu-id="1ac4d-183">SCK (針腳 8G)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="1ac4d-184">I2C1 SCL (針腳 5)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="1ac4d-185">橘色纜線</span><span class="sxs-lookup"><span data-stu-id="1ac4d-185">Orange cable</span></span>  |
| <span data-ttu-id="1ac4d-186">LED VDD (針腳 18F)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="1ac4d-187">GPIO 24 (針腳 18)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="1ac4d-188">白色纜線</span><span class="sxs-lookup"><span data-stu-id="1ac4d-188">White cable</span></span>   |
| <span data-ttu-id="1ac4d-189">LED GND (針腳 17F)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="1ac4d-190">GND (針腳 20)</span><span class="sxs-lookup"><span data-stu-id="1ac4d-190">GND (Pin 20)</span></span>           | <span data-ttu-id="1ac4d-191">黑色纜線</span><span class="sxs-lookup"><span data-stu-id="1ac4d-191">Black cable</span></span>   |

<span data-ttu-id="1ac4d-192">按一下以檢視 [Raspberry Pi 2 和 3 針腳對應](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi)進行參考。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="1ac4d-193">將 BME280 成功連接至 Raspberry Pi 之後，應該如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![連接的 Pi 和 BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="1ac4d-195">將 Pi 連線到網路</span><span class="sxs-lookup"><span data-stu-id="1ac4d-195">Connect Pi to the network</span></span>

<span data-ttu-id="1ac4d-196">透過 micro USB 纜線和電源供應器來開啟 Pi。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="1ac4d-197">使用乙太網路纜線將 Pi 連接到有線網路，或遵循來自 Raspberry Pi Foundation 的[指示](https://www.raspberrypi.org/learning/software-guide/wifi/)，將 Pi 連接到無線網路。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="1ac4d-198">在 Pi 成功連線到網路之後，您需要記下 [Pi 的 IP 位址](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![已連接到有線網路](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="1ac4d-200">請確定 Pi 是連接到與您電腦相同的網路。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="1ac4d-201">例如，如果您的電腦連線到無線網路，而 Pi 連線到有線網路，您可能不會在 devdisco 輸出中看到 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="1ac4d-202">在 Pi 上執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="1ac4d-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="1ac4d-203">複製範例應用程式並安裝必要條件套件</span><span class="sxs-lookup"><span data-stu-id="1ac4d-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="1ac4d-204">使用下列其中一個 SSH 用戶端，從主機電腦連接到 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="1ac4d-205">**Windows 使用者**</span><span class="sxs-lookup"><span data-stu-id="1ac4d-205">**Windows Users**</span></span>
   1. <span data-ttu-id="1ac4d-206">下載並安裝適用於 Windows 的 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="1ac4d-207">將 Pi 的 IP 位址複製到 [主機名稱] 或 [IP 位址] 區段，並且選取 SSH 作為連線類型。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="1ac4d-209">**Mac 和 Ubuntu 使用者**</span><span class="sxs-lookup"><span data-stu-id="1ac4d-209">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="1ac4d-210">在 Ubuntu 或 macOS 上使用內建的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-210">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="1ac4d-211">您可能需要執行 `ssh pi@<ip address of pi>`，才能透過 SSH 來連線 Pi。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-211">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="1ac4d-212">預設使用者名稱為 `pi`，密碼為 `raspberry`。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-212">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="1ac4d-213">將 Node.js 和 NPM 安裝到 Pi。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-213">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="1ac4d-214">首先，您應該使用下列命令檢查 Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-214">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="1ac4d-215">如果版本低於 4.x 或 Pi 上沒有 Node.js，請執行下列命令以安裝或更新 Node.js。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-215">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="1ac4d-216">執行下列命令，複製範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="1ac4d-216">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="1ac4d-217">執行下列命令安裝所有封裝。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-217">Install all packages by the following command.</span></span> <span data-ttu-id="1ac4d-218">其中包含 Azure IoT 裝置 SDK、BME280 感應器程式庫和接線 Pi 程式庫。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-218">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="1ac4d-219">端視網路連線而定，可能需要幾分鐘才能完成此安裝程序。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-219">It might take several minutes to finish this installation process depending on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="1ac4d-220">設定範例應用程式</span><span class="sxs-lookup"><span data-stu-id="1ac4d-220">Configure the sample application</span></span>

1. <span data-ttu-id="1ac4d-221">執行下列命令以開啟組態檔：</span><span class="sxs-lookup"><span data-stu-id="1ac4d-221">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![組態檔](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="1ac4d-223">此檔案中有兩個項目可供您設定。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-223">There are two items in this file you can configurate.</span></span> <span data-ttu-id="1ac4d-224">第一個是 `interval`，這可定義傳送至雲端的兩個訊息之間相隔的時間間隔 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-224">The first one is `interval`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="1ac4d-225">第二個是 `simulatedData`，這是是否使用模擬感應器資料的布林值。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-225">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="1ac4d-226">如果**沒有感應器**，請將 `simulatedData` 值設定為 `true`，使範例應用程式建立和使用模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-226">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="1ac4d-227">按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-227">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="1ac4d-228">執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="1ac4d-228">Run the sample application</span></span>

<span data-ttu-id="1ac4d-229">執行下列命令，執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="1ac4d-229">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="1ac4d-230">確定複製裝置連接字串，並貼到單引號中。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-230">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="1ac4d-231">您應該會看見下列輸出，顯示傳送至 IoT 中樞的感應器資料和訊息。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-231">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![輸出 - 從 Raspberry Pi 傳送至 IoT 中樞的感應器資料](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="1ac4d-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ac4d-233">Next steps</span></span>

<span data-ttu-id="1ac4d-234">您已執行範例應用程式收集感應器資料並傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-234">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="1ac4d-235">若要查看 Raspberry Pi 傳送給 IoT 中樞的訊息，或者在命令列介面中將訊息傳送給 Raspberry Pi，請參閱[使用 iothub-explorer 管理雲端裝置訊息教學課程](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)。</span><span class="sxs-lookup"><span data-stu-id="1ac4d-235">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
