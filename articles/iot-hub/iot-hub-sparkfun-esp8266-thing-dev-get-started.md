---
title: "ESP8266 到雲端 - 將 Sparkfun ESP8266 Thing Dev 連接到 Azure IoT 中樞 | Microsoft Docs"
description: "了解如何設定及連線 Sparkfun ESP8266 Thing Dev 和 Azure IoT 中樞，在本教學課程中將資料傳送到 Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="b354e-103">將 Sparkfun ESP8266 Thing Dev 連接到雲端的 Azure IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="b354e-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22、Thing Dev 及 IoT 中樞之間的連接](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="b354e-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="b354e-105">What you will do</span></span>

<span data-ttu-id="b354e-106">將 Sparkfun ESP8266 Thing Dev 連接到您將建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b354e-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="b354e-107">然後，在 ESP8266 上執行範例應用程式，以收集 DHT22 感應器中的溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="b354e-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="b354e-108">最後，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b354e-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b354e-109">如果您使用其他 ESP8266 電路版，仍舊可以遵循下列步驟來將它連線到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b354e-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="b354e-110">根據您使用的 ESP8266 電路板，您可能需要重新設定 `LED_PIN`。</span><span class="sxs-lookup"><span data-stu-id="b354e-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="b354e-111">例如，如果您使用 AI-Thinker 的 ESP8266，您可以將它從 `0` 變更為 `2`。</span><span class="sxs-lookup"><span data-stu-id="b354e-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="b354e-112">還沒有套件嗎？請按一下[這裡](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="b354e-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b354e-113">學習目標</span><span class="sxs-lookup"><span data-stu-id="b354e-113">What you will learn</span></span>

* <span data-ttu-id="b354e-114">如何建立 IoT 中樞並註冊 Thing Dev 適用的裝置。</span><span class="sxs-lookup"><span data-stu-id="b354e-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="b354e-115">如何連接 Thing Dev 與感應器和電腦。</span><span class="sxs-lookup"><span data-stu-id="b354e-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="b354e-116">如何在 Thing Dev 上執行範例應用程式來收集感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b354e-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="b354e-117">如何將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b354e-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="b354e-118">必要元件</span><span class="sxs-lookup"><span data-stu-id="b354e-118">What you will need</span></span>

![本教學課程所需的零件](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="b354e-120">若要完成此作業，您需要 Thing Dev 入門套件中的下列零件：</span><span class="sxs-lookup"><span data-stu-id="b354e-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="b354e-121">Sparkfun ESP8266 Thing Dev 電路板。</span><span class="sxs-lookup"><span data-stu-id="b354e-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="b354e-122">Micro USB 轉 Type A 的 USB 纜線。</span><span class="sxs-lookup"><span data-stu-id="b354e-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="b354e-123">您的開發環境還需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="b354e-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="b354e-124">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b354e-124">An active Azure subscription.</span></span> <span data-ttu-id="b354e-125">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="b354e-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b354e-126">執行 Windows 或 Ubuntu 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="b354e-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="b354e-127">Sparkfun ESP8266 Thing Dev 要連接的無線網路。</span><span class="sxs-lookup"><span data-stu-id="b354e-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="b354e-128">用來下載組態工具的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="b354e-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="b354e-129">[Arduino IDE](https://www.arduino.cc/en/main/software) 1.6.8 版 (或更新版本)，舊版無法與 AzureIoT 程式庫搭配運作。</span><span class="sxs-lookup"><span data-stu-id="b354e-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="b354e-130">如果您沒有感應器，下列項目可供選用。</span><span class="sxs-lookup"><span data-stu-id="b354e-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="b354e-131">您也可以選擇使用模擬的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b354e-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="b354e-132">Adafruit DHT22 溫度和溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="b354e-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="b354e-133">麵包板。</span><span class="sxs-lookup"><span data-stu-id="b354e-133">A breadboard.</span></span>
* <span data-ttu-id="b354e-134">M/M 跳線。</span><span class="sxs-lookup"><span data-stu-id="b354e-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="b354e-135">連接 ESP8266 Thing Dev 與感應器和電腦</span><span class="sxs-lookup"><span data-stu-id="b354e-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="b354e-136">將 DHT22 溫度和溼度感應器連接至 ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="b354e-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="b354e-137">使用麵包板和跳線來進行連接，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b354e-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="b354e-138">如果您沒有感應器，請略過本節，因為您可以改為使用模擬的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b354e-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![連接參考](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="b354e-140">感應器的針腳會使用下列接線方式︰</span><span class="sxs-lookup"><span data-stu-id="b354e-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="b354e-141">開始 (感應器)</span><span class="sxs-lookup"><span data-stu-id="b354e-141">Start (Sensor)</span></span>           | <span data-ttu-id="b354e-142">結束 (電路版)</span><span class="sxs-lookup"><span data-stu-id="b354e-142">End (Board)</span></span>           | <span data-ttu-id="b354e-143">纜線顏色</span><span class="sxs-lookup"><span data-stu-id="b354e-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="b354e-144">VDD (針腳 27F)</span><span class="sxs-lookup"><span data-stu-id="b354e-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="b354e-145">3V (針腳 8A)</span><span class="sxs-lookup"><span data-stu-id="b354e-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="b354e-146">紅色纜線</span><span class="sxs-lookup"><span data-stu-id="b354e-146">Red cable</span></span>     |
| <span data-ttu-id="b354e-147">DATA (針腳 28F)</span><span class="sxs-lookup"><span data-stu-id="b354e-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="b354e-148">GPIO 2 (針腳 9A)</span><span class="sxs-lookup"><span data-stu-id="b354e-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="b354e-149">白色纜線</span><span class="sxs-lookup"><span data-stu-id="b354e-149">White cable</span></span>    |
| <span data-ttu-id="b354e-150">GND (針腳 30F)</span><span class="sxs-lookup"><span data-stu-id="b354e-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="b354e-151">GND (針腳 7J)</span><span class="sxs-lookup"><span data-stu-id="b354e-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="b354e-152">黑色纜線</span><span class="sxs-lookup"><span data-stu-id="b354e-152">Black cable</span></span>   |


- <span data-ttu-id="b354e-153">如需詳細資訊，請參閱︰[DHT22 感應器安裝 (英文)](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) 和 [Sparkfun ESP8266 Thing Dev 規格 (英文)](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="b354e-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="b354e-154">現在，您的 Sparkfun ESP8266 Thing Dev 應該已經和作用中的感應器連接。</span><span class="sxs-lookup"><span data-stu-id="b354e-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![連接 dht22 和 ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="b354e-156">將 Sparkfun ESP8266 Thing Dev 連接到電腦</span><span class="sxs-lookup"><span data-stu-id="b354e-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="b354e-157">使用 Micro USB 轉 Type A 的 USB 纜線，將 Sparkfun ESP8266 Thing Dev 連接到電腦，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b354e-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![將 feather huzzah 連接到電腦](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="b354e-159">新增序列埠權限 - 僅限 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b354e-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="b354e-160">如果您使用 Ubuntu，請確定一般使用者具有操作 Sparkfun ESP8266 Thing Dev 之 USB 連接埠的權限。</span><span class="sxs-lookup"><span data-stu-id="b354e-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="b354e-161">若要為一般使用者新增序列埠權限，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="b354e-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="b354e-162">在終端機執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b354e-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="b354e-163">您會得到下列其中一個輸出︰</span><span class="sxs-lookup"><span data-stu-id="b354e-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="b354e-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b354e-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="b354e-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b354e-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="b354e-166">在輸出中，請注意 `uucp` 或 `dialout` 是 USB 連接埠的群組擁有者名稱。</span><span class="sxs-lookup"><span data-stu-id="b354e-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="b354e-167">執行下列命令，將使用者新增至群組︰</span><span class="sxs-lookup"><span data-stu-id="b354e-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="b354e-168">`<group-owner-name>` 是您在上一個步驟中取得的群組擁有者名稱。</span><span class="sxs-lookup"><span data-stu-id="b354e-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="b354e-169">`<username>` 是 Ubuntu 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b354e-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="b354e-170">先登出 Ubuntu 然後重新登入，以讓變更生效。</span><span class="sxs-lookup"><span data-stu-id="b354e-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="b354e-171">收集感應器資料，並將它傳送至 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="b354e-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="b354e-172">在本節中，您可以在 Sparkfun ESP8266 Thing Dev 上部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b354e-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="b354e-173">範例應用程式會在 Sparkfun ESP8266 Thing Dev 上使 LED 閃爍，並將收集自 DHT22 感應器的溫度和溼度資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b354e-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="b354e-174">從 GitHub 取得範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b354e-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="b354e-175">範例應用程式會裝載在 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="b354e-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="b354e-176">請從 GitHub 複製包含範例應用程式的範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="b354e-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="b354e-177">若要複製範例存放庫，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="b354e-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="b354e-178">開啟命令提示字元或終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="b354e-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="b354e-179">移至想要儲存範例應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b354e-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="b354e-180">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b354e-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="b354e-181">在 Arduino IDE 中安裝 Sparkfun ESP8266 Thing Dev 的封裝：</span><span class="sxs-lookup"><span data-stu-id="b354e-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="b354e-182">開啟範例應用程式儲存所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b354e-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="b354e-183">在 Arduino IDE 中開啟應用程式資料夾中的 app.ino 檔案。</span><span class="sxs-lookup"><span data-stu-id="b354e-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![在 Arduino IDE 中開啟範例應用程式](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="b354e-185">在 Arduino IDE 中，按一下 [檔案] > [喜好設定]。</span><span class="sxs-lookup"><span data-stu-id="b354e-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="b354e-186">在 [喜好設定] 對話方塊中，按一下 [其他電路板管理員 URL] 文字方塊旁的圖示。</span><span class="sxs-lookup"><span data-stu-id="b354e-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="b354e-187">在快顯視窗中，輸入下列 URL，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b354e-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![在 arduino ide 中指向套件 url](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="b354e-189">在 [喜好設定] 對話方塊中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b354e-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="b354e-190">按一下 [工具] > [電路板] > [電路板管理員]，然後搜尋 esp8266。</span><span class="sxs-lookup"><span data-stu-id="b354e-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="b354e-191">應該已安裝 ESP8266 2.2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b354e-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![已安裝 esp8266 套件](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="b354e-193">按一下 [工具] > [面板] > [Sparkfun ESP8266 Thing Dev]。</span><span class="sxs-lookup"><span data-stu-id="b354e-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="b354e-194">安裝必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="b354e-194">Install necessary libraries</span></span>

1. <span data-ttu-id="b354e-195">在 Arduino IDE 中，按一下 [草圖] > [包含程式庫] > [管理程式庫]。</span><span class="sxs-lookup"><span data-stu-id="b354e-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="b354e-196">逐一搜尋下列程式庫名稱。</span><span class="sxs-lookup"><span data-stu-id="b354e-196">Search for the following library names one by one.</span></span> <span data-ttu-id="b354e-197">對找到的每個程式庫按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="b354e-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="b354e-198">沒有真正的 DHT22 感應器嗎？</span><span class="sxs-lookup"><span data-stu-id="b354e-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="b354e-199">如果您沒有真正的 DHT22 感應器，範例應用程式可以模擬溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="b354e-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="b354e-200">若要讓範例應用程式使用模擬資料，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="b354e-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="b354e-201">開啟 `app` 資料夾中的 `config.h` 檔案。</span><span class="sxs-lookup"><span data-stu-id="b354e-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="b354e-202">找出下面這行程式碼，並將值從 `false` 變更為 `true`：</span><span class="sxs-lookup"><span data-stu-id="b354e-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![設定範例應用程式以使用模擬資料](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="b354e-204">使用 `Control-s` 進行儲存。</span><span class="sxs-lookup"><span data-stu-id="b354e-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="b354e-205">將範例應用程式部署到 Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="b354e-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="b354e-206">在 Arduino IDE 中，按一下 [工具] > [連接埠]，然後按一下 Sparkfun ESP8266 Thing Dev 的序列埠。</span><span class="sxs-lookup"><span data-stu-id="b354e-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="b354e-207">按一下 [草圖] > [上傳]，以建置範例應用程式並將其部署至 Sparkfun ESP8266 Thing Dev。</span><span class="sxs-lookup"><span data-stu-id="b354e-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="b354e-208">如果您使用的作業系統為 macOS，您可能會在上傳時看到下列訊息。</span><span class="sxs-lookup"><span data-stu-id="b354e-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="b354e-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="b354e-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="b354e-210">請開啟終端機視窗並完成下列動作來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="b354e-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="b354e-211">輸入認證</span><span class="sxs-lookup"><span data-stu-id="b354e-211">Enter your credentials</span></span>

<span data-ttu-id="b354e-212">上傳程序成功完成後，請遵循步驟來輸入認證︰</span><span class="sxs-lookup"><span data-stu-id="b354e-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="b354e-213">在 Arduino IDE 中，按一下 [工具] > [序列監視器]。</span><span class="sxs-lookup"><span data-stu-id="b354e-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="b354e-214">在 [序列監視器] 視窗中，請注意右下角的兩個下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="b354e-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="b354e-215">在左邊的下拉式清單中選取 [無行尾結束符號]。</span><span class="sxs-lookup"><span data-stu-id="b354e-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="b354e-216">在右邊的下拉式清單中選取 [115200 傳輸速率]。</span><span class="sxs-lookup"><span data-stu-id="b354e-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="b354e-217">在位於 [序列監視器] 視窗頂端的輸入方塊中，輸入系統要求您提供的下列資訊，然後按一下 [傳送]。</span><span class="sxs-lookup"><span data-stu-id="b354e-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="b354e-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="b354e-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="b354e-219">Wi-Fi 密碼</span><span class="sxs-lookup"><span data-stu-id="b354e-219">Wi-Fi password</span></span>
   * <span data-ttu-id="b354e-220">裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="b354e-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="b354e-221">認證資訊會儲存在 Sparkfun ESP8266 Thing Dev 的 EEPROM 中。</span><span class="sxs-lookup"><span data-stu-id="b354e-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="b354e-222">如果您按一下 Sparkfun ESP8266 Thing Dev 電路板上的重設按鈕，範例應用程式會詢問您是否要清除資訊。</span><span class="sxs-lookup"><span data-stu-id="b354e-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="b354e-223">輸入 `Y` 以清除資訊，此時系統會再次要求您提供資訊。</span><span class="sxs-lookup"><span data-stu-id="b354e-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="b354e-224">確認範例應用程式已成功執行</span><span class="sxs-lookup"><span data-stu-id="b354e-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="b354e-225">如果您在 [序列監視器] 視窗看到下列輸出，並在 Sparkfun ESP8266 Thing Dev 上看到閃爍的 LED，則表示範例應用程式已成功執行。</span><span class="sxs-lookup"><span data-stu-id="b354e-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![arduino ide 中的最終輸出](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="b354e-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b354e-227">Next steps</span></span>

<span data-ttu-id="b354e-228">您已成功將 Sparkfun ESP8266 Thing Dev 連接到 IoT 中樞，並將擷取到的感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b354e-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
