---
title: "aaaESP8266 toocloud-連接 Sparkfun ESP8266 事 Dev tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並在本教學課程中連接它 Sparkfun ESP8266 動作開發人員 tooAzure IoT 中樞 toosend 資料 toohello Azure 雲端平台。"
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
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="97fea-103">連接 Sparkfun ESP8266 動作開發人員 tooAzure hello 雲端中的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="97fea-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22、Thing Dev 及 IoT 中樞之間的連接](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="97fea-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="97fea-105">What you will do</span></span>

<span data-ttu-id="97fea-106">連接將會建立 Sparkfun ESP8266 動作開發人員 tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97fea-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="97fea-107">從 DHT22 感應器，然後 ESP8266 toocollect 氣溫和溼度資料上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="97fea-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="97fea-108">最後，傳送嗨感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97fea-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="97fea-109">如果您使用其他 ESP8266 面板，您仍然可以依照這些步驟 tooconnect 它 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97fea-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="97fea-110">根據您使用的 hello ESP8266 面板，您可能需要 tooreconfigure hello `LED_PIN`。</span><span class="sxs-lookup"><span data-stu-id="97fea-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="97fea-111">例如，如果您使用從 AI 思想家 ESP8266，您可能會變更從`0`太`2`。</span><span class="sxs-lookup"><span data-stu-id="97fea-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="97fea-112">還沒有套件嗎？請按一下[這裡](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="97fea-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="97fea-113">學習目標</span><span class="sxs-lookup"><span data-stu-id="97fea-113">What you will learn</span></span>

* <span data-ttu-id="97fea-114">如何 toocreate IoT 中樞和動作供開發的註冊裝置</span><span class="sxs-lookup"><span data-stu-id="97fea-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="97fea-115">如何 tooconnect 動作開發人員與 hello 感應器和您的電腦。</span><span class="sxs-lookup"><span data-stu-id="97fea-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="97fea-116">如何執行範例應用程式上的動作供開發 toocollect 感應器資料</span><span class="sxs-lookup"><span data-stu-id="97fea-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="97fea-117">如何 toosend hello 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97fea-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="97fea-118">必要元件</span><span class="sxs-lookup"><span data-stu-id="97fea-118">What you will need</span></span>

![Hello 教學課程需要的組件](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="97fea-120">toocomplete 這項作業，需要您的動作開發人員入門套件中的下列組件的 hello:</span><span class="sxs-lookup"><span data-stu-id="97fea-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="97fea-121">hello Sparkfun ESP8266 動作開發人員面板。</span><span class="sxs-lookup"><span data-stu-id="97fea-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="97fea-122">微 USB tooType USB 纜線。</span><span class="sxs-lookup"><span data-stu-id="97fea-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="97fea-123">您也需要 hello 下列開發環境：</span><span class="sxs-lookup"><span data-stu-id="97fea-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="97fea-124">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="97fea-124">An active Azure subscription.</span></span> <span data-ttu-id="97fea-125">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="97fea-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="97fea-126">執行 Windows 或 Ubuntu 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="97fea-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="97fea-127">Sparkfun ESP8266 動作開發人員 tooconnect 至無線網路。</span><span class="sxs-lookup"><span data-stu-id="97fea-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="97fea-128">網際網路連線 toodownload hello 組態工具。</span><span class="sxs-lookup"><span data-stu-id="97fea-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="97fea-129">[Arduino IDE](https://www.arduino.cc/en/main/software)版本 1.6.8 （或更新版本），舊版將不適用於 hello AzureIoT 程式庫。</span><span class="sxs-lookup"><span data-stu-id="97fea-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="97fea-130">hello 下列項目是選擇性的以防沒有感應器。</span><span class="sxs-lookup"><span data-stu-id="97fea-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="97fea-131">您也可以使用模擬的感應器資料的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="97fea-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="97fea-132">Adafruit DHT22 溫度和溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="97fea-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="97fea-133">麵包板。</span><span class="sxs-lookup"><span data-stu-id="97fea-133">A breadboard.</span></span>
* <span data-ttu-id="97fea-134">M/M 跳線。</span><span class="sxs-lookup"><span data-stu-id="97fea-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="97fea-135">連接 ESP8266 動作開發人員與 hello 感應器和您的電腦</span><span class="sxs-lookup"><span data-stu-id="97fea-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="97fea-136">連接 DHT22 氣溫和溼度感應器 tooESP8266 動作開發人員</span><span class="sxs-lookup"><span data-stu-id="97fea-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="97fea-137">請使用 hello breadboard 和跳接器線路 toomake hello 的連接，如下所示。</span><span class="sxs-lookup"><span data-stu-id="97fea-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="97fea-138">如果您沒有感應器，請略過本節，因為您可以改為使用模擬的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="97fea-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![連接參考](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="97fea-140">感應器 pin 碼，我們將使用下列配線 hello:</span><span class="sxs-lookup"><span data-stu-id="97fea-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="97fea-141">開始 (感應器)</span><span class="sxs-lookup"><span data-stu-id="97fea-141">Start (Sensor)</span></span>           | <span data-ttu-id="97fea-142">結束 (電路版)</span><span class="sxs-lookup"><span data-stu-id="97fea-142">End (Board)</span></span>           | <span data-ttu-id="97fea-143">纜線顏色</span><span class="sxs-lookup"><span data-stu-id="97fea-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="97fea-144">VDD (針腳 27F)</span><span class="sxs-lookup"><span data-stu-id="97fea-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="97fea-145">3V (針腳 8A)</span><span class="sxs-lookup"><span data-stu-id="97fea-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="97fea-146">紅色纜線</span><span class="sxs-lookup"><span data-stu-id="97fea-146">Red cable</span></span>     |
| <span data-ttu-id="97fea-147">DATA (針腳 28F)</span><span class="sxs-lookup"><span data-stu-id="97fea-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="97fea-148">GPIO 2 (針腳 9A)</span><span class="sxs-lookup"><span data-stu-id="97fea-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="97fea-149">白色纜線</span><span class="sxs-lookup"><span data-stu-id="97fea-149">White cable</span></span>    |
| <span data-ttu-id="97fea-150">GND (針腳 30F)</span><span class="sxs-lookup"><span data-stu-id="97fea-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="97fea-151">GND (針腳 7J)</span><span class="sxs-lookup"><span data-stu-id="97fea-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="97fea-152">黑色纜線</span><span class="sxs-lookup"><span data-stu-id="97fea-152">Black cable</span></span>   |


- <span data-ttu-id="97fea-153">如需詳細資訊，請參閱︰[DHT22 感應器安裝 (英文)](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) 和 [Sparkfun ESP8266 Thing Dev 規格 (英文)](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="97fea-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="97fea-154">現在，您的 Sparkfun ESP8266 Thing Dev 應該已經和作用中的感應器連接。</span><span class="sxs-lookup"><span data-stu-id="97fea-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![連接 dht22 和 ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="97fea-156">Sparkfun ESP8266 動作開發人員 tooyour 電腦連線</span><span class="sxs-lookup"><span data-stu-id="97fea-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="97fea-157">使用 hello 微 USB tooType USB 纜線 tooconnect Sparkfun ESP8266 動作開發人員 tooyour 的電腦，如下所示。</span><span class="sxs-lookup"><span data-stu-id="97fea-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![羽毛 huzzah tooyour 電腦連線](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="97fea-159">新增序列埠權限 - 僅限 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="97fea-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="97fea-160">如果您使用 Ubuntu，請確定一般使用者具有 hello 權限 toooperate 上 hello USB 連接埠的 Sparkfun ESP8266 動作供開發</span><span class="sxs-lookup"><span data-stu-id="97fea-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="97fea-161">tooadd 序列連接埠的權限的一般使用者，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="97fea-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="97fea-162">執行下列命令，在終端機的 hello:</span><span class="sxs-lookup"><span data-stu-id="97fea-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="97fea-163">您取得其中一個 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="97fea-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="97fea-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="97fea-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="97fea-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="97fea-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="97fea-166">在 hello 輸出，請注意`uucp`或`dialout`也就是 hello 群組擁有者名稱的 hello USB 連接埠。</span><span class="sxs-lookup"><span data-stu-id="97fea-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="97fea-167">藉由執行下列命令的 hello 加入 hello 使用者 toohello 群組：</span><span class="sxs-lookup"><span data-stu-id="97fea-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="97fea-168">`<group-owner-name>`hello 上一個步驟中為您取得 hello 群組擁有者名稱。</span><span class="sxs-lookup"><span data-stu-id="97fea-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="97fea-169">`<username>` 是 Ubuntu 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="97fea-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="97fea-170">登出 Ubuntu 和 hello 變更 tootake 效果重新登入它。</span><span class="sxs-lookup"><span data-stu-id="97fea-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="97fea-171">收集感應器資料並傳送 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="97fea-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="97fea-172">在本節中，您可以在 Sparkfun ESP8266 Thing Dev 上部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="97fea-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="97fea-173">閃爍 hello LED Sparkfun ESP8266 動作開發人員在 hello 範例應用程式，並傳送 hello 溫度和溼度從收集的資料 hello DHT22 感應器 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97fea-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="97fea-174">從 GitHub 取得 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="97fea-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="97fea-175">hello 範例應用程式被裝載於 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="97fea-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="97fea-176">複製 hello 範例儲存機制包含從 GitHub hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="97fea-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="97fea-177">tooclone hello 範例儲存機制，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="97fea-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="97fea-178">開啟命令提示字元或終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="97fea-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="97fea-179">請您想要儲存的 hello 範例應用程式 toobe tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="97fea-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="97fea-180">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="97fea-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="97fea-181">安裝適用於 Sparkfun ESP8266 動作開發人員在 Arduino IDE hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="97fea-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="97fea-182">開啟 hello hello 範例應用程式所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="97fea-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="97fea-183">Hello Arduino IDE 中的應用程式資料夾中開啟 hello app.ino 檔案。</span><span class="sxs-lookup"><span data-stu-id="97fea-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![arduino ide 中開啟 hello 範例應用程式](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="97fea-185">在 hello Arduino IDE 中，按一下 **檔案** > **喜好設定**。</span><span class="sxs-lookup"><span data-stu-id="97fea-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="97fea-186">在 hello**喜好設定**對話方塊方塊中，按一下 下一步 toohello 的 hello 圖示**其他面板管理員 Url**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="97fea-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="97fea-187">在 hello 快顯視窗中，輸入下列 URL，hello，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="97fea-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![點 tooa arduino ide 中的套件 url。](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="97fea-189">在 hello**喜好設定**對話方塊中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="97fea-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="97fea-190">按一下 [工具] > [電路板] > [電路板管理員]，然後搜尋 esp8266。</span><span class="sxs-lookup"><span data-stu-id="97fea-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="97fea-191">應該已安裝 ESP8266 2.2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="97fea-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![hello esp8266 套件安裝](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="97fea-193">按一下 [工具] > [面板] > [Sparkfun ESP8266 Thing Dev]。</span><span class="sxs-lookup"><span data-stu-id="97fea-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="97fea-194">安裝必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="97fea-194">Install necessary libraries</span></span>

1. <span data-ttu-id="97fea-195">在 hello Arduino IDE 中，按一下 **草圖** > **包含程式庫** > **管理程式庫**。</span><span class="sxs-lookup"><span data-stu-id="97fea-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="97fea-196">下列程式庫名稱一個 hello 搜尋。</span><span class="sxs-lookup"><span data-stu-id="97fea-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="97fea-197">針對每個您所尋找的 hello 程式庫中，按一下 **安裝**。</span><span class="sxs-lookup"><span data-stu-id="97fea-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="97fea-198">沒有真正的 DHT22 感應器嗎？</span><span class="sxs-lookup"><span data-stu-id="97fea-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="97fea-199">如果您不需要實際的 DHT22 感應器 hello 範例應用程式可以模擬氣溫和溼度的資料。</span><span class="sxs-lookup"><span data-stu-id="97fea-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="97fea-200">tooenable hello 範例應用程式 toouse 模擬資料，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="97fea-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="97fea-201">開啟 hello`config.h`檔案在 hello`app`資料夾。</span><span class="sxs-lookup"><span data-stu-id="97fea-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="97fea-202">找出 hello 下列程式碼行並變更 hello 值`false`太`true`:</span><span class="sxs-lookup"><span data-stu-id="97fea-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![設定 hello 範例應用程式模擬 toouse 資料](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="97fea-204">使用 `Control-s` 進行儲存。</span><span class="sxs-lookup"><span data-stu-id="97fea-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="97fea-205">部署 hello 範例應用程式 tooSparkfun ESP8266 動作開發人員</span><span class="sxs-lookup"><span data-stu-id="97fea-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="97fea-206">在 hello Arduino IDE 中，按一下 **工具** > **連接埠**，然後按一下 hello 序列埠 Sparkfun ESP8266 動作供開發的</span><span class="sxs-lookup"><span data-stu-id="97fea-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="97fea-207">按一下**草圖** > **上傳**toobuild 和部署 hello 範例應用程式 tooSparkfun ESP8266 動作供開發</span><span class="sxs-lookup"><span data-stu-id="97fea-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="97fea-208">如果您使用 macOS 您可能無法看到下列訊息期間上傳的 hello。</span><span class="sxs-lookup"><span data-stu-id="97fea-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="97fea-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="97fea-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="97fea-210">請開啟 ternimal 視窗，並完成下列動作 toosolve 此問題。</span><span class="sxs-lookup"><span data-stu-id="97fea-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="97fea-211">輸入認證</span><span class="sxs-lookup"><span data-stu-id="97fea-211">Enter your credentials</span></span>

<span data-ttu-id="97fea-212">Hello 上傳成功完成之後，請依照 hello 步驟 tooenter 您的認證：</span><span class="sxs-lookup"><span data-stu-id="97fea-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="97fea-213">在 hello Arduino IDE 中，按一下 **工具** > **序列監視器**。</span><span class="sxs-lookup"><span data-stu-id="97fea-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="97fea-214">在 hello 序列監視器視窗中，請注意在右下角的 hello 下方 hello 兩個下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="97fea-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="97fea-215">選取**沒有行尾結束符號**hello 左邊的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="97fea-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="97fea-216">選取**115200 傳輸**hello 右邊下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="97fea-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="97fea-217">Hello 位於 hello hello 序列監視器 視窗的頂端輸入的方塊中輸入下列資訊，如果您要求 tooprovide hello 它們，然後按一下**傳送**。</span><span class="sxs-lookup"><span data-stu-id="97fea-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="97fea-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="97fea-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="97fea-219">Wi-Fi 密碼</span><span class="sxs-lookup"><span data-stu-id="97fea-219">Wi-Fi password</span></span>
   * <span data-ttu-id="97fea-220">裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="97fea-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="97fea-221">hello 認證資訊會儲存在 hello EEPROM 的 Sparkfun ESP8266 動作供開發</span><span class="sxs-lookup"><span data-stu-id="97fea-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="97fea-222">如果您按一下 hello Sparkfun ESP8266 動作開發人員面板 hello 重設 按鈕，hello 範例應用程式會要求您如果要讓 tooerase hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="97fea-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="97fea-223">輸入`Y`清除 toohave hello 資訊，而您必須再次 tooprovide hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="97fea-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="97fea-224">確認順利執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="97fea-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="97fea-225">如果您看到 hello 下列輸出 hello 序列監視器視窗中，而且 hello Sparkfun ESP8266 動作開發人員，hello 範例應用程式上的 LED 閃爍不停執行成功。</span><span class="sxs-lookup"><span data-stu-id="97fea-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![arduino ide 中的最終輸出](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="97fea-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97fea-227">Next steps</span></span>

<span data-ttu-id="97fea-228">您已成功連接 Sparkfun ESP8266 動作開發人員 tooyour IoT 中樞而傳送嗨擷取感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="97fea-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
