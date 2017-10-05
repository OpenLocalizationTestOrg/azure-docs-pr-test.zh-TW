---
title: "Intel Edison 到雲端 (C) - 將 Intel Edison 連線到 Azure IoT 中樞 | Microsoft Docs"
description: "了解如何設定及連線 Intel Edison 和 Azure IoT 中樞，在本教學課程中讓 Intel Edison 將資料傳送到 Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot intel edison, intel edison iot 中樞, intel edison 傳送資料到雲端, intel edison 到雲端"
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: edbdbe0230f742cd7228f04a4a83c9bd567527e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-c"></a><span data-ttu-id="0c490-104">將 Intel Edison 連線到 Azure IoT 中樞 (C)</span><span class="sxs-lookup"><span data-stu-id="0c490-104">Connect Intel Edison to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="0c490-105">在本教學課程中，您一開始會先了解使用 Intel Edison 的基本知識。</span><span class="sxs-lookup"><span data-stu-id="0c490-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="0c490-106">接著會了解如何使用 [Azure IoT 中樞](iot-hub-what-is-iot-hub.md)讓您的裝置順暢地與雲端連線。</span><span class="sxs-lookup"><span data-stu-id="0c490-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="0c490-107">還沒有套件嗎？</span><span class="sxs-lookup"><span data-stu-id="0c490-107">Don't have a kit yet?</span></span> <span data-ttu-id="0c490-108">從[這裡](https://azure.microsoft.com/develop/iot/starter-kits)開始</span><span class="sxs-lookup"><span data-stu-id="0c490-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="0c490-109">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="0c490-109">What you do</span></span>

* <span data-ttu-id="0c490-110">設置 Intel Edison 和 Grove 模組。</span><span class="sxs-lookup"><span data-stu-id="0c490-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="0c490-111">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0c490-111">Create an IoT hub.</span></span>
* <span data-ttu-id="0c490-112">在 IoT 中樞註冊 Edison 的裝置。</span><span class="sxs-lookup"><span data-stu-id="0c490-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="0c490-113">在 Edison 上執行範例應用程式，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0c490-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="0c490-114">將 Intel Edison 連線至您建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0c490-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="0c490-115">然後，在 Edison 上執行範例應用程式，以收集 Grove 溫度感應器中的溫度和溼度資料。</span><span class="sxs-lookup"><span data-stu-id="0c490-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="0c490-116">最後，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0c490-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="0c490-117">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="0c490-117">What you learn</span></span>

* <span data-ttu-id="0c490-118">如何建立 Azure IoT 中樞，並取得新的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="0c490-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="0c490-119">如何將 Edison 與 Grove 溫度感應器連接。</span><span class="sxs-lookup"><span data-stu-id="0c490-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="0c490-120">如何在 Edison 上執行範例應用程式來收集感應器資料。</span><span class="sxs-lookup"><span data-stu-id="0c490-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="0c490-121">如何將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0c490-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0c490-122">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="0c490-122">What you need</span></span>

![您需要什麼](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="0c490-124">Intel Edison 開發板</span><span class="sxs-lookup"><span data-stu-id="0c490-124">The Intel Edison board</span></span>
* <span data-ttu-id="0c490-125">Arduino 擴充板</span><span class="sxs-lookup"><span data-stu-id="0c490-125">Arduino expansion board</span></span>
* <span data-ttu-id="0c490-126">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c490-126">An active Azure subscription.</span></span> <span data-ttu-id="0c490-127">如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="0c490-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="0c490-128">執行 Windows 或 Linux 的 Mac 或 PC。</span><span class="sxs-lookup"><span data-stu-id="0c490-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="0c490-129">網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="0c490-129">An Internet connection.</span></span>
* <span data-ttu-id="0c490-130">Micro B 轉 Type A 的 USB 纜線</span><span class="sxs-lookup"><span data-stu-id="0c490-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="0c490-131">直流電 (DC) 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="0c490-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="0c490-132">電源供應器的額定值應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0c490-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="0c490-133">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="0c490-133">7-15V DC</span></span>
  - <span data-ttu-id="0c490-134">至少 1500mA</span><span class="sxs-lookup"><span data-stu-id="0c490-134">At least 1500mA</span></span>
  - <span data-ttu-id="0c490-135">中心/內部插銷應該是電源供應器的正極</span><span class="sxs-lookup"><span data-stu-id="0c490-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="0c490-136">下列項目是選用項目︰</span><span class="sxs-lookup"><span data-stu-id="0c490-136">The following items are optional:</span></span>

* <span data-ttu-id="0c490-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="0c490-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="0c490-138">Grove - 溫度感應器</span><span class="sxs-lookup"><span data-stu-id="0c490-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="0c490-139">Grove 纜線</span><span class="sxs-lookup"><span data-stu-id="0c490-139">Grove Cable</span></span>
* <span data-ttu-id="0c490-140">包裝內所含的任何間隔柱或螺絲，包括兩個用來將模組鎖到擴充板的螺絲，和四組螺絲和塑膠間隔柱。</span><span class="sxs-lookup"><span data-stu-id="0c490-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="0c490-141">這些項目都是選用項目，因為程式碼範例支援模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="0c490-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="0c490-142">安裝 Intel Edison</span><span class="sxs-lookup"><span data-stu-id="0c490-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="0c490-143">組裝面板</span><span class="sxs-lookup"><span data-stu-id="0c490-143">Assemble your board</span></span>

<span data-ttu-id="0c490-144">本節所含步驟會將 Intel® Edison 模組連接至擴充板。</span><span class="sxs-lookup"><span data-stu-id="0c490-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="0c490-145">將 Intel® Edison 模組放在擴充板的白框內，讓模組上的螺絲孔對齊擴充板上的螺絲。</span><span class="sxs-lookup"><span data-stu-id="0c490-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="0c490-146">在模組上的 `What will you make?` 字樣正下方往下按，直到您感覺到兩者咬合。</span><span class="sxs-lookup"><span data-stu-id="0c490-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![組裝面板 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="0c490-148">使用兩個六角螺帽 (包裝內含) 將模組鎖緊到擴充板上。</span><span class="sxs-lookup"><span data-stu-id="0c490-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![組裝面板 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="0c490-150">在擴充板四個角落的其中一個螺絲孔中插入螺絲。</span><span class="sxs-lookup"><span data-stu-id="0c490-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="0c490-151">將其中一個白色塑膠間隔柱旋緊到螺絲上。</span><span class="sxs-lookup"><span data-stu-id="0c490-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![組裝面板 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="0c490-153">重複裝上其他三個角落的間隔柱。</span><span class="sxs-lookup"><span data-stu-id="0c490-153">Repeat for the other three corner spacers.</span></span>

   ![組裝面板 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="0c490-155">面板現已組裝好。</span><span class="sxs-lookup"><span data-stu-id="0c490-155">Now your board is assembled.</span></span>

   ![組裝好的面板](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="0c490-157">連接 Grove Base Shield 和溫度感應器</span><span class="sxs-lookup"><span data-stu-id="0c490-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="0c490-158">將 Grove Base Shield 放上主機板。</span><span class="sxs-lookup"><span data-stu-id="0c490-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="0c490-159">確定所有針腳都緊密地插入主機板。</span><span class="sxs-lookup"><span data-stu-id="0c490-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="0c490-161">使用 Grove 纜線將 Grove 溫度感應器連接到 Grove Base Shield **A0** 連接埠。</span><span class="sxs-lookup"><span data-stu-id="0c490-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![連接到溫度感應器](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison 和感應器連接](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="0c490-164">現在您的感應器已就緒。</span><span class="sxs-lookup"><span data-stu-id="0c490-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="0c490-165">將 Edison 接上電源</span><span class="sxs-lookup"><span data-stu-id="0c490-165">Power up Edison</span></span>

1. <span data-ttu-id="0c490-166">插上電源供應器。</span><span class="sxs-lookup"><span data-stu-id="0c490-166">Plug in the power supply.</span></span>

   ![插上電源供應器](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="0c490-168">綠色 LED (在 Arduino* 擴充板上標示為 DS1) 應該會亮起，並持續亮著。</span><span class="sxs-lookup"><span data-stu-id="0c490-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="0c490-169">等候一分鐘，讓面板完成開機。</span><span class="sxs-lookup"><span data-stu-id="0c490-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0c490-170">如果您沒有 DC 電源供應器，也可以透過 USB 連接埠為面板供電。</span><span class="sxs-lookup"><span data-stu-id="0c490-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="0c490-171">如需詳細資訊，請參閱`Connect Edison to your computer`一節。</span><span class="sxs-lookup"><span data-stu-id="0c490-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="0c490-172">以此方式為面板供電，可能會讓面板發生無法預期的行為，尤其是在使用 Wi-Fi 或驅動馬達時。</span><span class="sxs-lookup"><span data-stu-id="0c490-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="0c490-173">將 Edison 連接到電腦</span><span class="sxs-lookup"><span data-stu-id="0c490-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="0c490-174">將微型開關往下扳動到靠近兩個 micro USB 連接埠的方向，使 Edison 進入裝置模式。</span><span class="sxs-lookup"><span data-stu-id="0c490-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="0c490-175">若要了解裝置模式與主機模式的差異，請參閱[這裡](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)。</span><span class="sxs-lookup"><span data-stu-id="0c490-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![將微型開關往下扳動](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="0c490-177">將 micro USB 纜線插入最上方的 micro USB 連接埠。</span><span class="sxs-lookup"><span data-stu-id="0c490-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![最上方的 micro USB 連接埠](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="0c490-179">將 USB 纜線的另一端插入電腦。</span><span class="sxs-lookup"><span data-stu-id="0c490-179">Plug the other end of USB cable into your computer.</span></span>

   ![電腦 USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="0c490-181">當電腦掛接新的磁碟機 (很像將 SD 卡插入電腦) 時，您就會知道面板已完全初始化。</span><span class="sxs-lookup"><span data-stu-id="0c490-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="0c490-182">下載並執行組態工具</span><span class="sxs-lookup"><span data-stu-id="0c490-182">Download and run the configuration tool</span></span>
<span data-ttu-id="0c490-183">從[此連結](https://software.intel.com/en-us/iot/hardware/edison/downloads)的 `Installers` 標題底下所列項目取得最新的組態工具。</span><span class="sxs-lookup"><span data-stu-id="0c490-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="0c490-184">執行工具，並依照其螢幕上的指示進行，視需要按 [Next]</span><span class="sxs-lookup"><span data-stu-id="0c490-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="0c490-185">更新韌體</span><span class="sxs-lookup"><span data-stu-id="0c490-185">Flash firmware</span></span>
1. <span data-ttu-id="0c490-186">在 `Set up options` 頁面上，按一下 `Flash Firmware`。</span><span class="sxs-lookup"><span data-stu-id="0c490-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="0c490-187">執行下列其中一項，選取要更新至面板的映像︰</span><span class="sxs-lookup"><span data-stu-id="0c490-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="0c490-188">若要下載 Intel 所提供之最新韌體映像並以此映像更新面板，請選取 `Download the latest image version xxxx`。</span><span class="sxs-lookup"><span data-stu-id="0c490-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="0c490-189">若要以電腦上已儲存的映像更新面板，請選取 `Select the local image`。</span><span class="sxs-lookup"><span data-stu-id="0c490-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="0c490-190">瀏覽並選取您要更新至面板的映像。</span><span class="sxs-lookup"><span data-stu-id="0c490-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="0c490-191">安裝工具會嘗試更新面板。</span><span class="sxs-lookup"><span data-stu-id="0c490-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="0c490-192">整個更新程序最多可能需要 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="0c490-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="0c490-193">設定密碼</span><span class="sxs-lookup"><span data-stu-id="0c490-193">Set password</span></span>
1. <span data-ttu-id="0c490-194">在 `Set up options` 頁面上，按一下 `Enable Security`。</span><span class="sxs-lookup"><span data-stu-id="0c490-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="0c490-195">您可以為 Intel® Edison 面板設定自訂名稱。</span><span class="sxs-lookup"><span data-stu-id="0c490-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="0c490-196">這是選擇性。</span><span class="sxs-lookup"><span data-stu-id="0c490-196">This is optional.</span></span>
3. <span data-ttu-id="0c490-197">輸入面板的密碼，然後按一下 `Set password`。</span><span class="sxs-lookup"><span data-stu-id="0c490-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="0c490-198">記下密碼，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="0c490-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="0c490-199">連接 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="0c490-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="0c490-200">在 `Set up options` 頁面上，按一下 `Connect Wi-Fi`。</span><span class="sxs-lookup"><span data-stu-id="0c490-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="0c490-201">最多請等候一分鐘，讓電腦掃描可用的 Wi-Fi 網路。</span><span class="sxs-lookup"><span data-stu-id="0c490-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="0c490-202">從 `Detected Networks` 下拉式清單中選取網路。</span><span class="sxs-lookup"><span data-stu-id="0c490-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="0c490-203">從 `Security` 下拉式清單中選取網路的安全性類型。</span><span class="sxs-lookup"><span data-stu-id="0c490-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="0c490-204">提供登入和密碼資訊，然後按一下 `Configure Wi-Fi`。</span><span class="sxs-lookup"><span data-stu-id="0c490-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="0c490-205">記下 IP 位址，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="0c490-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="0c490-206">請確定 Edison 是連接到與您電腦相同的網路。</span><span class="sxs-lookup"><span data-stu-id="0c490-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="0c490-207">電腦會使用該 IP 位址連接到 Edison。</span><span class="sxs-lookup"><span data-stu-id="0c490-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![連接到溫度感應器](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="0c490-209">恭喜！</span><span class="sxs-lookup"><span data-stu-id="0c490-209">Congratulations!</span></span> <span data-ttu-id="0c490-210">您已經成功設定 Edison。</span><span class="sxs-lookup"><span data-stu-id="0c490-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="0c490-211">在 Intel Edison 上執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="0c490-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="0c490-212">準備 Azure IoT 裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="0c490-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="0c490-213">使用下列其中一個 SSH 用戶端，從主機電腦連線到 Intel Edison。</span><span class="sxs-lookup"><span data-stu-id="0c490-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="0c490-214">IP 位址來自組態工具，密碼則是您在該工具中設定的密碼。</span><span class="sxs-lookup"><span data-stu-id="0c490-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="0c490-215">[PuTTY](http://www.putty.org/) 適用於 Windows。</span><span class="sxs-lookup"><span data-stu-id="0c490-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="0c490-216">Ubuntu 或 macOS 上的內建 SSH 用戶端 (執行 `ssh root@"the IP address"`)。</span><span class="sxs-lookup"><span data-stu-id="0c490-216">The built-in SSH client on Ubuntu or macOS (run `ssh root@"the IP address"`).</span></span>

2. <span data-ttu-id="0c490-217">將範例用戶端應用程式複製到裝置。</span><span class="sxs-lookup"><span data-stu-id="0c490-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="0c490-218">然後瀏覽到存放庫資料夾，執行下列命令來建置 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="0c490-218">Then navigate to the repo folder to run the following command to build Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-the-sample-application"></a><span data-ttu-id="0c490-219">設定範例應用程式</span><span class="sxs-lookup"><span data-stu-id="0c490-219">Configure the sample application</span></span>

1. <span data-ttu-id="0c490-220">執行下列命令以開啟組態檔：</span><span class="sxs-lookup"><span data-stu-id="0c490-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![組態檔](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="0c490-222">此檔案中有兩個巨集可供您設定。</span><span class="sxs-lookup"><span data-stu-id="0c490-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="0c490-223">第一個是 `INTERVAL`，這可定義傳送至雲端的兩個訊息之間相隔的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="0c490-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="0c490-224">第二個是 `SIMULATED_DATA`，這是是否使用模擬感應器資料的布林值。</span><span class="sxs-lookup"><span data-stu-id="0c490-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="0c490-225">如果**沒有感應器**，請將 `SIMULATED_DATA` 值設定為 `1`，使範例應用程式建立和使用模擬感應器資料。</span><span class="sxs-lookup"><span data-stu-id="0c490-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="0c490-226">按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。</span><span class="sxs-lookup"><span data-stu-id="0c490-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="0c490-227">建置並執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="0c490-227">Build and run the sample application</span></span>

1. <span data-ttu-id="0c490-228">執行下列命令，建置範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="0c490-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![建置輸出](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="0c490-230">執行下列命令，執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="0c490-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="0c490-231">確定複製裝置連接字串，並貼到單引號中。</span><span class="sxs-lookup"><span data-stu-id="0c490-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="0c490-232">您應該會看見下列輸出，顯示傳送至 IoT 中樞的感應器資料和訊息。</span><span class="sxs-lookup"><span data-stu-id="0c490-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![輸出 - 從 Intel Edison 傳送至 IoT 中樞的感應器資料](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="0c490-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c490-234">Next steps</span></span>

<span data-ttu-id="0c490-235">您已執行範例應用程式收集感應器資料並傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0c490-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
