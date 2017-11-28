---
title: "aaaESP8266 toocloud-連接羽毛 HUZZAH ESP8266 tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並在本教學課程中連接它 Adafruit 羽毛 HUZZAH ESP8266 tooAzure IoT 中樞 toosend 資料 toohello Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="946dd-103">連接 Adafruit 羽毛 HUZZAH ESP8266 tooAzure hello 雲端中的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="946dd-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22、Feather HUZZAH ESP8266 與 IoT 中樞之間的連線](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="946dd-105">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="946dd-105">What you do</span></span>


<span data-ttu-id="946dd-106">連接您所建立的 Adafruit 羽毛 HUZZAH ESP8266 tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="946dd-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="946dd-107">然後您範例應用程式上執行 ESP8266 toocollect hello 氣溫和溼度資料從 DHT22 感應器。</span><span class="sxs-lookup"><span data-stu-id="946dd-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="946dd-108">最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="946dd-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="946dd-109">如果您使用其他 ESP8266 面板，您仍然可以依照這些步驟 tooconnect 它 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="946dd-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="946dd-110">根據您所使用的 hello ESP8266 面板，您可能需要 tooreconfigure hello `LED_PIN`。</span><span class="sxs-lookup"><span data-stu-id="946dd-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="946dd-111">例如，如果您使用從 AI 思想家 ESP8266，您可能會變更從`0`太`2`。</span><span class="sxs-lookup"><span data-stu-id="946dd-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="946dd-112">還沒有套件嗎？</span><span class="sxs-lookup"><span data-stu-id="946dd-112">Don't have a kit yet?</span></span> <span data-ttu-id="946dd-113">收到 hello [Azure 網站](http://azure.com/iotstarterkits)。</span><span class="sxs-lookup"><span data-stu-id="946dd-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="946dd-114">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="946dd-114">What you learn</span></span>

* <span data-ttu-id="946dd-115">如何 toocreate IoT 中樞和羽毛 HUZZAH ESP8266 如註冊裝置</span><span class="sxs-lookup"><span data-stu-id="946dd-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="946dd-116">如何 tooconnect 羽毛 HUZZAH ESP8266 hello 感應器與您的電腦</span><span class="sxs-lookup"><span data-stu-id="946dd-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="946dd-117">如何執行範例應用程式上羽毛 HUZZAH ESP8266 toocollect 感應器資料</span><span class="sxs-lookup"><span data-stu-id="946dd-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="946dd-118">如何 toosend hello 感應器資料 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="946dd-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="946dd-119">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="946dd-119">What you need</span></span>

![Hello 教學課程需要的組件](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="946dd-121">toocomplete 這項作業，您需要 hello 羽毛 HUZZAH ESP8266 入門套件中的下列部分：</span><span class="sxs-lookup"><span data-stu-id="946dd-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="946dd-122">hello 羽毛 HUZZAH ESP8266 面板</span><span class="sxs-lookup"><span data-stu-id="946dd-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="946dd-123">微 USB tooType USB 纜線</span><span class="sxs-lookup"><span data-stu-id="946dd-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="946dd-124">您還需要下列項目，為您的開發環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="946dd-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="946dd-125">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="946dd-125">An active Azure subscription.</span></span> <span data-ttu-id="946dd-126">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="946dd-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="946dd-127">執行 Windows 或 Ubuntu 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="946dd-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="946dd-128">若要羽毛 HUZZAH ESP8266 tooconnect 的無線網路。</span><span class="sxs-lookup"><span data-stu-id="946dd-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="946dd-129">網際網路連線 toodownload hello 組態工具。</span><span class="sxs-lookup"><span data-stu-id="946dd-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="946dd-130">[Arduino IDE](https://www.arduino.cc/en/main/software) 1.6.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="946dd-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="946dd-131">舊版未使用 hello AzureIoT 程式庫。</span><span class="sxs-lookup"><span data-stu-id="946dd-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="946dd-132">hello 下列項目是選擇性的以防沒有感應器。</span><span class="sxs-lookup"><span data-stu-id="946dd-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="946dd-133">您也可以使用模擬的感應器資料的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="946dd-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="946dd-134">Adafruit DHT22 溫度和溼度感應器</span><span class="sxs-lookup"><span data-stu-id="946dd-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="946dd-135">麵包板</span><span class="sxs-lookup"><span data-stu-id="946dd-135">A breadboard</span></span>
* <span data-ttu-id="946dd-136">M/M 跳線</span><span class="sxs-lookup"><span data-stu-id="946dd-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="946dd-137">聯繫羽毛 HUZZAH ESP8266 hello 感應器和您的電腦</span><span class="sxs-lookup"><span data-stu-id="946dd-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="946dd-138">在本節中，您可以連接 hello 感應器 tooyour 面板。</span><span class="sxs-lookup"><span data-stu-id="946dd-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="946dd-139">然後您插入以便進一步使用於您裝置的 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="946dd-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="946dd-140">連接 DHT22 氣溫和溼度感應器 tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="946dd-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="946dd-141">請使用 hello breadboard 和跳接器線路 toomake hello 的連接，如下所示。</span><span class="sxs-lookup"><span data-stu-id="946dd-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="946dd-142">如果您沒有感應器，請略過本節，因為您可以改為使用模擬的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="946dd-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![連接參考](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="946dd-144">感應器 pin 碼，使用下列配線 hello:</span><span class="sxs-lookup"><span data-stu-id="946dd-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="946dd-145">開始 (感應器)</span><span class="sxs-lookup"><span data-stu-id="946dd-145">Start (Sensor)</span></span>           | <span data-ttu-id="946dd-146">結束 (電路版)</span><span class="sxs-lookup"><span data-stu-id="946dd-146">End (Board)</span></span>           | <span data-ttu-id="946dd-147">纜線顏色</span><span class="sxs-lookup"><span data-stu-id="946dd-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="946dd-148">VDD (針腳 31F)</span><span class="sxs-lookup"><span data-stu-id="946dd-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="946dd-149">3V (針腳 58H)</span><span class="sxs-lookup"><span data-stu-id="946dd-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="946dd-150">紅色纜線</span><span class="sxs-lookup"><span data-stu-id="946dd-150">Red cable</span></span>     |
| <span data-ttu-id="946dd-151">DATA (針腳 32F)</span><span class="sxs-lookup"><span data-stu-id="946dd-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="946dd-152">GPIO 2 (針腳 46A)</span><span class="sxs-lookup"><span data-stu-id="946dd-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="946dd-153">藍色纜線</span><span class="sxs-lookup"><span data-stu-id="946dd-153">Blue cable</span></span>    |
| <span data-ttu-id="946dd-154">GND (針腳 34F)</span><span class="sxs-lookup"><span data-stu-id="946dd-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="946dd-155">GND (針腳 56I)</span><span class="sxs-lookup"><span data-stu-id="946dd-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="946dd-156">黑色纜線</span><span class="sxs-lookup"><span data-stu-id="946dd-156">Black cable</span></span>   |

<span data-ttu-id="946dd-157">如需詳細資訊，請參閱 [Adafruit DHT22 感應器安裝](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor)和 [Adafruit Feather HUZZAH Esp8266 接腳圖](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts)。</span><span class="sxs-lookup"><span data-stu-id="946dd-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="946dd-158">現在，Feather Huzzah ESP8266 應該已經和作用中的感應器連接。</span><span class="sxs-lookup"><span data-stu-id="946dd-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![連接 DHT22 與 Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="946dd-160">羽毛 HUZZAH ESP8266 tooyour 電腦連線</span><span class="sxs-lookup"><span data-stu-id="946dd-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="946dd-161">如下所示，使用 hello 微 USB tooType USB 纜線 tooconnect 羽毛 HUZZAH ESP8266 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="946dd-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![羽毛 Huzzah tooyour 電腦連線](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="946dd-163">新增序列埠權限 (僅限 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="946dd-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="946dd-164">如果您使用 Ubuntu，請確定您擁有 hello 權限 toooperate 上 hello USB 連接埠的羽毛 HUZZAH ESP8266。</span><span class="sxs-lookup"><span data-stu-id="946dd-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="946dd-165">tooadd 序列連接埠的權限，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="946dd-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="946dd-166">執行下列命令，在終端機的 hello:</span><span class="sxs-lookup"><span data-stu-id="946dd-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="946dd-167">您取得其中一個 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="946dd-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="946dd-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="946dd-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="946dd-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="946dd-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="946dd-170">在 hello 輸出中，請注意，`uucp`或`dialout`hello USB 連接埠 hello 群組擁有者名稱。</span><span class="sxs-lookup"><span data-stu-id="946dd-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="946dd-171">藉由執行下列命令的 hello 加入 hello 使用者 toohello 群組：</span><span class="sxs-lookup"><span data-stu-id="946dd-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="946dd-172">`<group-owner-name>`hello 上一個步驟中為您取得 hello 群組擁有者名稱。</span><span class="sxs-lookup"><span data-stu-id="946dd-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="946dd-173">`<username>` 是 Ubuntu 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="946dd-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="946dd-174">登出 Ubuntu，然後再登入一次的 hello 變更 tooappear。</span><span class="sxs-lookup"><span data-stu-id="946dd-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="946dd-175">收集感應器資料並傳送 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="946dd-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="946dd-176">在本節中，您可以在 Feather HUZZAH ESP8266 上部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="946dd-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="946dd-177">hello 範例應用程式會閃爍 hello LED 上羽毛 HUZZAH ESP8266，並傳送 hello 溫度和溼度從收集的資料 hello DHT22 感應器 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="946dd-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="946dd-178">從 GitHub 取得 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="946dd-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="946dd-179">hello 範例應用程式被裝載於 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="946dd-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="946dd-180">複製 hello 範例儲存機制包含從 GitHub hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="946dd-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="946dd-181">tooclone hello 範例儲存機制，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="946dd-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="946dd-182">開啟命令提示字元或終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="946dd-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="946dd-183">請您想要儲存的 hello 範例應用程式 toobe tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="946dd-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="946dd-184">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="946dd-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="946dd-185">安裝在 hello Arduino IDE 羽毛 HUZZAH ESP8266 hello 封裝：</span><span class="sxs-lookup"><span data-stu-id="946dd-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="946dd-186">開啟 hello hello 範例應用程式所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="946dd-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="946dd-187">Hello hello Arduino IDE 中的應用程式資料夾中開啟 hello app.ino 檔案。</span><span class="sxs-lookup"><span data-stu-id="946dd-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Arduino IDE 中開啟 hello 範例應用程式](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="946dd-189">在 hello Arduino IDE 中，按一下 **檔案** > **喜好設定**。</span><span class="sxs-lookup"><span data-stu-id="946dd-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="946dd-190">在 hello**喜好設定**對話方塊方塊中，按一下 下一步 toohello 的 hello 圖示**其他面板管理員 Url**方塊。</span><span class="sxs-lookup"><span data-stu-id="946dd-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="946dd-191">在 hello 快顯視窗中，輸入下列 URL，hello，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="946dd-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![點 tooa Arduino IDE 中的套件 url。](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="946dd-193">在 hello**喜好設定**對話方塊中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="946dd-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="946dd-194">按一下 [工具] > [電路板] > [電路板管理員]，然後搜尋 esp8266。</span><span class="sxs-lookup"><span data-stu-id="946dd-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="946dd-195">[電路板管理員] 指出已安裝的 ESP8266 版本為 2.2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="946dd-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![hello esp8266 套件安裝](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="946dd-197">按一下 [工具] > [電路板] > [Adafruit HUZZAH ESP8266]。</span><span class="sxs-lookup"><span data-stu-id="946dd-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="946dd-198">安裝必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="946dd-198">Install necessary libraries</span></span>

1. <span data-ttu-id="946dd-199">在 hello Arduino IDE 中，按一下 **草圖** > **包含程式庫** > **管理程式庫**。</span><span class="sxs-lookup"><span data-stu-id="946dd-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="946dd-200">下列程式庫名稱一個 hello 搜尋。</span><span class="sxs-lookup"><span data-stu-id="946dd-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="946dd-201">對於找到的每個程式庫，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="946dd-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="946dd-202">沒有真正的 DHT22 感應器嗎？</span><span class="sxs-lookup"><span data-stu-id="946dd-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="946dd-203">如果您不需要實際的 DHT22 感應器 hello 範例應用程式可以模擬氣溫和溼度的資料。</span><span class="sxs-lookup"><span data-stu-id="946dd-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="946dd-204">tooset hello 範例應用程式 toouse 模擬資料，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="946dd-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="946dd-205">開啟 hello`config.h`檔案在 hello`app`資料夾。</span><span class="sxs-lookup"><span data-stu-id="946dd-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="946dd-206">找出 hello 下列程式碼行並變更 hello 值`false`太`true`:</span><span class="sxs-lookup"><span data-stu-id="946dd-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![設定 hello 範例應用程式模擬 toouse 資料](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="946dd-208">儲存 hello 檔`Control-s`。</span><span class="sxs-lookup"><span data-stu-id="946dd-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="946dd-209">部署 hello 範例應用程式 tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="946dd-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="946dd-210">在 hello Arduino IDE 中，按一下 **工具** > **連接埠**，然後按一下羽毛 HUZZAH ESP8266 hello 序列連接埠。</span><span class="sxs-lookup"><span data-stu-id="946dd-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="946dd-211">按一下**草圖** > **上傳**toobuild 和部署 hello 範例應用程式 tooFeather HUZZAH ESP8266。</span><span class="sxs-lookup"><span data-stu-id="946dd-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="946dd-212">輸入認證</span><span class="sxs-lookup"><span data-stu-id="946dd-212">Enter your credentials</span></span>

<span data-ttu-id="946dd-213">Hello 上傳成功完成之後，請遵循這些步驟 tooenter 您的認證：</span><span class="sxs-lookup"><span data-stu-id="946dd-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="946dd-214">在 hello Arduino IDE 中，按一下 **工具** > **序列監視器**。</span><span class="sxs-lookup"><span data-stu-id="946dd-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="946dd-215">在 hello 序列監視器視窗中，請注意在 hello 右下角中的 hello 兩個下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="946dd-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="946dd-216">選取**沒有行尾結束符號**hello 左邊的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="946dd-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="946dd-217">選取**115200 傳輸**hello 右邊下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="946dd-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="946dd-218">Hello 位於 hello hello 序列監視器 視窗的頂端輸入的方塊中輸入下列資訊，如果您要求 tooprovide hello 它們，然後按一下**傳送**。</span><span class="sxs-lookup"><span data-stu-id="946dd-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="946dd-219">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="946dd-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="946dd-220">Wi-Fi 密碼</span><span class="sxs-lookup"><span data-stu-id="946dd-220">Wi-Fi password</span></span>
   * <span data-ttu-id="946dd-221">裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="946dd-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="946dd-222">hello 認證資訊會儲存在 hello 羽毛 HUZZAH ESP8266 EEPROM。</span><span class="sxs-lookup"><span data-stu-id="946dd-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="946dd-223">如果您按一下 hello 羽毛 HUZZAH ESP8266 面板 hello 重設 按鈕，hello 範例應用程式會詢問您是否 tooerase hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="946dd-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="946dd-224">輸入`Y`toohave hello 資訊清除。</span><span class="sxs-lookup"><span data-stu-id="946dd-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="946dd-225">系統會詢問 tooprovide hello 資訊第二次。</span><span class="sxs-lookup"><span data-stu-id="946dd-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="946dd-226">確認順利執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="946dd-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="946dd-227">如果您看到 hello 下列輸出 hello 序列監視器視窗中，而且 hello 羽毛 HUZZAH ESP8266 hello 範例應用程式上的 LED 閃爍不停執行成功。</span><span class="sxs-lookup"><span data-stu-id="946dd-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Arduino IDE 中的最終輸出](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="946dd-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="946dd-229">Next steps</span></span>

<span data-ttu-id="946dd-230">您已成功連接羽毛 HUZZAH ESP8266 tooyour IoT 中樞，而傳送嗨擷取感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="946dd-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

