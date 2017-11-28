---
title: "aaaIntel Edison toocloud (C)-連接 Intel Edison tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並連接在此教學課程 Intel Edison toosend 資料 toohello Azure 雲端平台的 Intel Edison tooAzure IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot intel edison、 intel edison iot 中樞、 intel edison 傳送資料 toocloud，intel edison toocloud"
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a><span data-ttu-id="b1467-104">連接 Intel Edison tooAzure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="b1467-104">Connect Intel Edison tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="b1467-105">在本教學課程中，您必須開始學習使用 Intel Edison 的 hello 基本。</span><span class="sxs-lookup"><span data-stu-id="b1467-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="b1467-106">然後您學習如何 tooseamlessly 裝置 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="b1467-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="b1467-107">還沒有套件嗎？</span><span class="sxs-lookup"><span data-stu-id="b1467-107">Don't have a kit yet?</span></span> <span data-ttu-id="b1467-108">從[這裡](https://azure.microsoft.com/develop/iot/starter-kits)開始</span><span class="sxs-lookup"><span data-stu-id="b1467-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b1467-109">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="b1467-109">What you do</span></span>

* <span data-ttu-id="b1467-110">設置 Intel Edison 和 Grove 模組。</span><span class="sxs-lookup"><span data-stu-id="b1467-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="b1467-111">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1467-111">Create an IoT hub.</span></span>
* <span data-ttu-id="b1467-112">在 IoT 中樞註冊 Edison 的裝置。</span><span class="sxs-lookup"><span data-stu-id="b1467-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="b1467-113">執行範例應用程式上 Edison toosend 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1467-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="b1467-114">連接您所建立的 Intel Edison tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1467-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="b1467-115">然後您範例應用程式上執行 Edison toocollect 氣溫和溼度資料從 Groove 溫度感應器。</span><span class="sxs-lookup"><span data-stu-id="b1467-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="b1467-116">最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1467-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b1467-117">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="b1467-117">What you learn</span></span>

* <span data-ttu-id="b1467-118">如何 toocreate Azure IoT 中樞，並取得新的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="b1467-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="b1467-119">如何 tooconnect Edison 與 Groove 溫度感應器。</span><span class="sxs-lookup"><span data-stu-id="b1467-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="b1467-120">如何執行範例應用程式上 Edison toocollect 感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b1467-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="b1467-121">如何 toosend 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1467-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b1467-122">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b1467-122">What you need</span></span>

![您需要什麼](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="b1467-124">hello Intel Edison 面板</span><span class="sxs-lookup"><span data-stu-id="b1467-124">hello Intel Edison board</span></span>
* <span data-ttu-id="b1467-125">Arduino 擴充板</span><span class="sxs-lookup"><span data-stu-id="b1467-125">Arduino expansion board</span></span>
* <span data-ttu-id="b1467-126">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1467-126">An active Azure subscription.</span></span> <span data-ttu-id="b1467-127">如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="b1467-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b1467-128">執行 Windows 或 Linux 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="b1467-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="b1467-129">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="b1467-129">An Internet connection.</span></span>
* <span data-ttu-id="b1467-130">微 B tooType USB 纜線</span><span class="sxs-lookup"><span data-stu-id="b1467-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="b1467-131">直流電 (DC) 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="b1467-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="b1467-132">電源供應器的額定值應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="b1467-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="b1467-133">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="b1467-133">7-15V DC</span></span>
  - <span data-ttu-id="b1467-134">至少 1500mA</span><span class="sxs-lookup"><span data-stu-id="b1467-134">At least 1500mA</span></span>
  - <span data-ttu-id="b1467-135">hello 中心/內部 pin 應該 hello 正柵欄 hello 電源供應器</span><span class="sxs-lookup"><span data-stu-id="b1467-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="b1467-136">hello 下列項目是選擇性項目：</span><span class="sxs-lookup"><span data-stu-id="b1467-136">hello following items are optional:</span></span>

* <span data-ttu-id="b1467-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="b1467-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="b1467-138">Grove - 溫度感應器</span><span class="sxs-lookup"><span data-stu-id="b1467-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="b1467-139">Grove 纜線</span><span class="sxs-lookup"><span data-stu-id="b1467-139">Grove Cable</span></span>
* <span data-ttu-id="b1467-140">任何空格字元列或包含在 hello 封裝，包括兩顆螺絲 toofasten hello 模組 toohello 擴充面板和四組螺絲和塑膠空格的螺絲。</span><span class="sxs-lookup"><span data-stu-id="b1467-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="b1467-141">這些項目是選擇性的因為 hello 程式碼範例支援模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b1467-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="b1467-142">安裝 Intel Edison</span><span class="sxs-lookup"><span data-stu-id="b1467-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="b1467-143">組裝面板</span><span class="sxs-lookup"><span data-stu-id="b1467-143">Assemble your board</span></span>

<span data-ttu-id="b1467-144">本章節包含步驟 tooattach Intel® Edison 模組 tooyour 展開面板。</span><span class="sxs-lookup"><span data-stu-id="b1467-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="b1467-145">在展開面板，排隊與 hello 螺絲 hello 擴充面板上的 hello 漏洞 hello 模組上的白色 hello 大綱內 hello Intel® Edison 模組位置。</span><span class="sxs-lookup"><span data-stu-id="b1467-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="b1467-146">Hello 字正下方的 hello 模組上按住`What will you make?`直到您覺得嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="b1467-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![組裝面板 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="b1467-148">使用 hello 兩個 （包含在 hello 封裝） 的十六進位具體 toosecure hello 模組 toohello 展開面板。</span><span class="sxs-lookup"><span data-stu-id="b1467-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![組裝面板 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="b1467-150">其中一種 hello 四個邊角孔 hello 擴充面板上插入螺絲。</span><span class="sxs-lookup"><span data-stu-id="b1467-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="b1467-151">扭曲，加強 hello 白色塑膠空格到 hello 螺絲的其中一個。</span><span class="sxs-lookup"><span data-stu-id="b1467-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![組裝面板 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="b1467-153">重複的 hello 其他三個角到空格字元。</span><span class="sxs-lookup"><span data-stu-id="b1467-153">Repeat for hello other three corner spacers.</span></span>

   ![組裝面板 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="b1467-155">面板現已組裝好。</span><span class="sxs-lookup"><span data-stu-id="b1467-155">Now your board is assembled.</span></span>

   ![組裝好的面板](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="b1467-157">連接 [hello] 保護盾 Groove 基底和 hello 溫度感應器</span><span class="sxs-lookup"><span data-stu-id="b1467-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="b1467-158">Hello Groove 基底保護盾置於 tooyour 面板。</span><span class="sxs-lookup"><span data-stu-id="b1467-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="b1467-159">確定所有針腳都緊密地插入主機板。</span><span class="sxs-lookup"><span data-stu-id="b1467-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="b1467-161">使用 Groove 纜線 tooconnect Groove 溫度感應器到 hello Groove 基底保護盾**A0**連接埠。</span><span class="sxs-lookup"><span data-stu-id="b1467-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![連接 tootemperature 感應器](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison 和感應器連接](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="b1467-164">現在您的感應器已就緒。</span><span class="sxs-lookup"><span data-stu-id="b1467-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="b1467-165">將 Edison 接上電源</span><span class="sxs-lookup"><span data-stu-id="b1467-165">Power up Edison</span></span>

1. <span data-ttu-id="b1467-166">插入 hello 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="b1467-166">Plug in hello power supply.</span></span>

   ![插上電源供應器](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="b1467-168">（標示為 hello Arduino * 擴充面板上的 DS1） 綠色 LED 應亮起，保持 亮燈。</span><span class="sxs-lookup"><span data-stu-id="b1467-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="b1467-169">等候一分鐘的 hello 面板 toofinish 開機。</span><span class="sxs-lookup"><span data-stu-id="b1467-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b1467-170">如果您沒有 DC 電源供應器，您仍然可以透過 USB 連接埠電源 hello 面板。</span><span class="sxs-lookup"><span data-stu-id="b1467-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="b1467-171">如需詳細資訊，請參閱`Connect Edison tooyour computer`一節。</span><span class="sxs-lookup"><span data-stu-id="b1467-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="b1467-172">以此方式為面板供電，可能會讓面板發生無法預期的行為，尤其是在使用 Wi-Fi 或驅動馬達時。</span><span class="sxs-lookup"><span data-stu-id="b1467-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="b1467-173">Edison tooyour 電腦連線</span><span class="sxs-lookup"><span data-stu-id="b1467-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="b1467-174">使 Edison 裝置模式中，切換 hello microswitch hello 兩個微 USB 連接埠，向下。</span><span class="sxs-lookup"><span data-stu-id="b1467-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="b1467-175">若要了解裝置模式與主機模式的差異，請參閱[這裡](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)。</span><span class="sxs-lookup"><span data-stu-id="b1467-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![向下 hello microswitch 切換](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="b1467-177">插入 hello 微 USB 纜線 hello 頂端微 USB 連接埠。</span><span class="sxs-lookup"><span data-stu-id="b1467-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![最上方的 micro USB 連接埠](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="b1467-179">隨插即用 hello USB 纜線的一端插入電腦。</span><span class="sxs-lookup"><span data-stu-id="b1467-179">Plug hello other end of USB cable into your computer.</span></span>

   ![電腦 USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="b1467-181">當電腦掛接新的磁碟機 (很像將 SD 卡插入電腦) 時，您就會知道面板已完全初始化。</span><span class="sxs-lookup"><span data-stu-id="b1467-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="b1467-182">下載並執行 hello 組態工具</span><span class="sxs-lookup"><span data-stu-id="b1467-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="b1467-183">取得從 hello 最新組態工具[此連結](https://software.intel.com/en-us/iot/hardware/edison/downloads)列在 hello`Installers`標題。</span><span class="sxs-lookup"><span data-stu-id="b1467-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="b1467-184">執行 hello 工具並依照其螢幕上的指示，在需要時，請按一下下一步</span><span class="sxs-lookup"><span data-stu-id="b1467-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="b1467-185">更新韌體</span><span class="sxs-lookup"><span data-stu-id="b1467-185">Flash firmware</span></span>
1. <span data-ttu-id="b1467-186">在 hello`Set up options`頁面上，按一下`Flash Firmware`。</span><span class="sxs-lookup"><span data-stu-id="b1467-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="b1467-187">選取到您的面板 hello 映像 tooflash hello 下列其中一項動作：</span><span class="sxs-lookup"><span data-stu-id="b1467-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="b1467-188">您面板與 hello 最新的韌體映像可用 intel toodownload 和 flash 選取`Download hello latest image version xxxx`。</span><span class="sxs-lookup"><span data-stu-id="b1467-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="b1467-189">tooflash 您面板，您已經儲存您的電腦上的映像選取`Select hello local image`。</span><span class="sxs-lookup"><span data-stu-id="b1467-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="b1467-190">瀏覽要 tooflash tooyour 面板 tooand 選取 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="b1467-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="b1467-191">hello 安裝工具會嘗試 tooflash 您面板。</span><span class="sxs-lookup"><span data-stu-id="b1467-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="b1467-192">hello 整個閃爍程序可能佔用 too10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b1467-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="b1467-193">設定密碼</span><span class="sxs-lookup"><span data-stu-id="b1467-193">Set password</span></span>
1. <span data-ttu-id="b1467-194">在 hello`Set up options`頁面上，按一下`Enable Security`。</span><span class="sxs-lookup"><span data-stu-id="b1467-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="b1467-195">您可以為 Intel® Edison 面板設定自訂名稱。</span><span class="sxs-lookup"><span data-stu-id="b1467-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="b1467-196">這是選擇性。</span><span class="sxs-lookup"><span data-stu-id="b1467-196">This is optional.</span></span>
3. <span data-ttu-id="b1467-197">輸入面板的密碼，然後按一下 `Set password`。</span><span class="sxs-lookup"><span data-stu-id="b1467-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="b1467-198">標記下 hello 密碼，以便稍後用。</span><span class="sxs-lookup"><span data-stu-id="b1467-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="b1467-199">連接 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="b1467-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="b1467-200">在 hello`Set up options`頁面上，按一下`Connect Wi-Fi`。</span><span class="sxs-lookup"><span data-stu-id="b1467-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="b1467-201">設定可用的 Wi-fi 網路電腦掃描 tooone 分鐘的等候。</span><span class="sxs-lookup"><span data-stu-id="b1467-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="b1467-202">從 hello`Detected Networks`下拉式清單中，選取您的網路。</span><span class="sxs-lookup"><span data-stu-id="b1467-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="b1467-203">從 hello`Security`下拉式清單中，選取 hello 網路的安全性類型。</span><span class="sxs-lookup"><span data-stu-id="b1467-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="b1467-204">提供登入和密碼資訊，然後按一下 `Configure Wi-Fi`。</span><span class="sxs-lookup"><span data-stu-id="b1467-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="b1467-205">標記下 hello IP 位址，以便稍後用。</span><span class="sxs-lookup"><span data-stu-id="b1467-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="b1467-206">請確定 Edison 連接的 toohello 相同網路做為您的電腦。</span><span class="sxs-lookup"><span data-stu-id="b1467-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="b1467-207">您的電腦連線 tooyour Edison 使用 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b1467-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![連接 tootemperature 感應器](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="b1467-209">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b1467-209">Congratulations!</span></span> <span data-ttu-id="b1467-210">您已經成功設定 Edison。</span><span class="sxs-lookup"><span data-stu-id="b1467-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="b1467-211">在 Intel Edison 上執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b1467-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="b1467-212">準備 hello Azure IoT 裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="b1467-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="b1467-213">使用其中一種您主機電腦 tooconnect tooyour Intel Edison 中的下列 SSH 用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="b1467-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="b1467-214">hello IP 位址來自 hello 組態工具，而且 hello 密碼為 hello 其中一個您已經設定該工具。</span><span class="sxs-lookup"><span data-stu-id="b1467-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="b1467-215">[PuTTY](http://www.putty.org/) 適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="b1467-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="b1467-216">hello 內建 SSH 用戶端上 Ubuntu 或 macOS (執行`ssh root@"hello IP address"`)。</span><span class="sxs-lookup"><span data-stu-id="b1467-216">hello built-in SSH client on Ubuntu or macOS (run `ssh root@"hello IP address"`).</span></span>

2. <span data-ttu-id="b1467-217">複製 hello 範例用戶端應用程式 tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="b1467-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="b1467-218">然後瀏覽下列命令 toobuild Azure IoT SDK toohello 儲存機制資料夾 toorun hello</span><span class="sxs-lookup"><span data-stu-id="b1467-218">Then navigate toohello repo folder toorun hello following command toobuild Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a><span data-ttu-id="b1467-219">Hello 範例應用程式設定</span><span class="sxs-lookup"><span data-stu-id="b1467-219">Configure hello sample application</span></span>

1. <span data-ttu-id="b1467-220">執行下列命令的 hello 開啟 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="b1467-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![組態檔](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="b1467-222">此檔案中有兩個巨集可供您設定。</span><span class="sxs-lookup"><span data-stu-id="b1467-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="b1467-223">hello 第一次是`INTERVAL`，而後者可定義兩個訊息，傳送 toocloud hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="b1467-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="b1467-224">hello 第二個`SIMULATED_DATA`，這是 toouse 是否模擬感應器資料的布林值。</span><span class="sxs-lookup"><span data-stu-id="b1467-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="b1467-225">如果您**沒有 hello 感應器**，將的 hello`SIMULATED_DATA`值太`1`toomake hello 範例應用程式建立及使用模擬的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b1467-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="b1467-226">按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。</span><span class="sxs-lookup"><span data-stu-id="b1467-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="b1467-227">建置並執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b1467-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="b1467-228">藉由執行下列命令的 hello 建置 hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="b1467-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![建置輸出](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="b1467-230">藉由執行下列命令的 hello 執行 hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="b1467-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="b1467-231">請確定您複製-貼上 hello 裝置連接字串到 hello 單引號。</span><span class="sxs-lookup"><span data-stu-id="b1467-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="b1467-232">您應該會看到 hello 下列輸出顯示 hello 傳送 tooyour IoT 中樞的感應器資料及 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="b1467-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![輸出-從 Intel Edison tooyour IoT 中樞傳送的感應器資料](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="b1467-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1467-234">Next steps</span></span>

<span data-ttu-id="b1467-235">您已執行範例應用程式 toocollect 感應器資料，並將它傳送 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1467-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
