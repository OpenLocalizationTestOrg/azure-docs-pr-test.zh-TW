---
title: "將 Intel Edison (C) 連接到 Azure IoT - 第 1 課：設定裝置 | Microsoft Docs"
description: "設定 Intel Edison 以進行首次使用。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 設定, 將 arduino 連接到電腦, 設定 arduino, arduino 面板"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c92d9f7ba63b0a0929ff95599fd757ea425ef1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="989e2-104">設定 Intel Edison</span><span class="sxs-lookup"><span data-stu-id="989e2-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="989e2-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="989e2-105">What you will do</span></span>
<span data-ttu-id="989e2-106">設定 Intel Edison 以進行首次使用，方法是組裝面板、接上電源，並將組態工具安裝到桌面作業系統，以更新 Edison 的韌體、設定其密碼，然後將其連線至 Wi-Fi。</span><span class="sxs-lookup"><span data-stu-id="989e2-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="989e2-107">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="989e2-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="989e2-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="989e2-108">What you will learn</span></span>
<span data-ttu-id="989e2-109">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="989e2-109">In this article, you will learn:</span></span>

* <span data-ttu-id="989e2-110">如何組裝 Edison 面板，並將它接上電源。</span><span class="sxs-lookup"><span data-stu-id="989e2-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="989e2-111">如何更新 Edison 的韌體、設定密碼及連線至 Wi-Fi。</span><span class="sxs-lookup"><span data-stu-id="989e2-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="989e2-112">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="989e2-112">What you need</span></span>
<span data-ttu-id="989e2-113">若要完成此作業，您需要 Intel Edison 入門套件中的下列零件：</span><span class="sxs-lookup"><span data-stu-id="989e2-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="989e2-114">Intel® Edison 模組</span><span class="sxs-lookup"><span data-stu-id="989e2-114">Intel® Edison module</span></span>
* <span data-ttu-id="989e2-115">Arduino 擴充板</span><span class="sxs-lookup"><span data-stu-id="989e2-115">Arduino expansion board</span></span>
* <span data-ttu-id="989e2-116">包裝內所含的任何間隔柱或螺絲，包括兩個用來將模組鎖到擴充板的螺絲，和四組螺絲和塑膠間隔柱。</span><span class="sxs-lookup"><span data-stu-id="989e2-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="989e2-117">Micro B 轉 Type A 的 USB 纜線</span><span class="sxs-lookup"><span data-stu-id="989e2-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="989e2-118">直流電 (DC) 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="989e2-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="989e2-119">電源供應器的額定值應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="989e2-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="989e2-120">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="989e2-120">7-15V DC</span></span>
  - <span data-ttu-id="989e2-121">至少 1500mA</span><span class="sxs-lookup"><span data-stu-id="989e2-121">At least 1500mA</span></span>
  - <span data-ttu-id="989e2-122">中心/內部插銷應該是電源供應器的正極</span><span class="sxs-lookup"><span data-stu-id="989e2-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![入門套件中的零件](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="989e2-124">您也會需要：</span><span class="sxs-lookup"><span data-stu-id="989e2-124">You also need:</span></span>

* <span data-ttu-id="989e2-125">一部執行 Windows、Mac 或 Linux 的電腦。</span><span class="sxs-lookup"><span data-stu-id="989e2-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="989e2-126">可供 Edison 連線的無線連線。</span><span class="sxs-lookup"><span data-stu-id="989e2-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="989e2-127">用來下載組態工具的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="989e2-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="989e2-128">組裝面板</span><span class="sxs-lookup"><span data-stu-id="989e2-128">Assemble your board</span></span>

<span data-ttu-id="989e2-129">本節所含步驟會將 Intel® Edison 模組連接至擴充板。</span><span class="sxs-lookup"><span data-stu-id="989e2-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="989e2-130">將 Intel® Edison 模組放在擴充板的白框內，讓模組上的螺絲孔對齊擴充板上的螺絲。</span><span class="sxs-lookup"><span data-stu-id="989e2-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="989e2-131">在模組上的 `What will you make?` 字樣正下方往下按，直到您感覺到兩者咬合。</span><span class="sxs-lookup"><span data-stu-id="989e2-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![組裝面板 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="989e2-133">使用兩個六角螺帽 (包裝內含) 將模組鎖緊到擴充板上。</span><span class="sxs-lookup"><span data-stu-id="989e2-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![組裝面板 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="989e2-135">在擴充板四個角落的其中一個螺絲孔中插入螺絲。</span><span class="sxs-lookup"><span data-stu-id="989e2-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="989e2-136">將其中一個白色塑膠間隔柱旋緊到螺絲上。</span><span class="sxs-lookup"><span data-stu-id="989e2-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![組裝面板 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="989e2-138">重複裝上其他三個角落的間隔柱。</span><span class="sxs-lookup"><span data-stu-id="989e2-138">Repeat for the other three corner spacers.</span></span>

   ![組裝面板 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="989e2-140">面板現已組裝好。</span><span class="sxs-lookup"><span data-stu-id="989e2-140">Now your board is assembled.</span></span>

   ![組裝好的面板](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="989e2-142">將 Edison 接上電源</span><span class="sxs-lookup"><span data-stu-id="989e2-142">Power up Edison</span></span>

1. <span data-ttu-id="989e2-143">插上電源供應器。</span><span class="sxs-lookup"><span data-stu-id="989e2-143">Plug in the power supply.</span></span>

   ![插上電源供應器](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="989e2-145">綠色 LED (在 Arduino* 擴充板上標示為 DS1) 應該會亮起，並持續亮著。</span><span class="sxs-lookup"><span data-stu-id="989e2-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="989e2-146">等候一分鐘，讓面板完成開機。</span><span class="sxs-lookup"><span data-stu-id="989e2-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="989e2-147">如果您沒有 DC 電源供應器，也可以透過 USB 連接埠為面板供電。</span><span class="sxs-lookup"><span data-stu-id="989e2-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="989e2-148">如需詳細資訊，請參閱`Connect Edison to your computer`一節。</span><span class="sxs-lookup"><span data-stu-id="989e2-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="989e2-149">以此方式為面板供電，可能會讓面板發生無法預期的行為，尤其是在使用 Wi-Fi 或驅動馬達時。</span><span class="sxs-lookup"><span data-stu-id="989e2-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="989e2-150">將 Edison 連接到電腦</span><span class="sxs-lookup"><span data-stu-id="989e2-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="989e2-151">將微型開關往下扳動到靠近兩個 micro USB 連接埠的方向，使 Edison 進入裝置模式。</span><span class="sxs-lookup"><span data-stu-id="989e2-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="989e2-152">若要了解裝置模式與主機模式的差異，請參閱[這裡](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)。</span><span class="sxs-lookup"><span data-stu-id="989e2-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![將微型開關往下扳動](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="989e2-154">將 micro USB 纜線插入最上方的 micro USB 連接埠。</span><span class="sxs-lookup"><span data-stu-id="989e2-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![最上方的 micro USB 連接埠](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="989e2-156">將 USB 纜線的另一端插入電腦。</span><span class="sxs-lookup"><span data-stu-id="989e2-156">Plug the other end of USB cable into your computer.</span></span>

   ![電腦 USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="989e2-158">當電腦掛接新的磁碟機 (很像將 SD 卡插入電腦) 時，您就會知道面板已完全初始化。</span><span class="sxs-lookup"><span data-stu-id="989e2-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="989e2-159">下載並執行組態工具</span><span class="sxs-lookup"><span data-stu-id="989e2-159">Download and run the configuration tool</span></span>
<span data-ttu-id="989e2-160">從[此連結](https://software.intel.com/en-us/iot/hardware/edison/downloads)的 `Installers` 標題底下所列項目取得最新的組態工具。</span><span class="sxs-lookup"><span data-stu-id="989e2-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="989e2-161">執行工具，並依照其螢幕上的指示進行，視需要按 [Next]</span><span class="sxs-lookup"><span data-stu-id="989e2-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="989e2-162">更新韌體</span><span class="sxs-lookup"><span data-stu-id="989e2-162">Flash firmware</span></span>
1. <span data-ttu-id="989e2-163">在 `Set up options` 頁面上，按一下 `Flash Firmware`。</span><span class="sxs-lookup"><span data-stu-id="989e2-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="989e2-164">執行下列其中一項，選取要更新至面板的映像︰</span><span class="sxs-lookup"><span data-stu-id="989e2-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="989e2-165">若要下載 Intel 所提供之最新韌體映像並以此映像更新面板，請選取 `Download the latest image version xxxx`。</span><span class="sxs-lookup"><span data-stu-id="989e2-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="989e2-166">若要以電腦上已儲存的映像更新面板，請選取 `Select the local image`。</span><span class="sxs-lookup"><span data-stu-id="989e2-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="989e2-167">瀏覽並選取您要更新至面板的映像。</span><span class="sxs-lookup"><span data-stu-id="989e2-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="989e2-168">安裝工具會嘗試更新面板。</span><span class="sxs-lookup"><span data-stu-id="989e2-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="989e2-169">整個更新程序最多可能需要 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="989e2-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="989e2-170">設定密碼</span><span class="sxs-lookup"><span data-stu-id="989e2-170">Set password</span></span>
1. <span data-ttu-id="989e2-171">在 `Set up options` 頁面上，按一下 `Enable Security`。</span><span class="sxs-lookup"><span data-stu-id="989e2-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="989e2-172">您可以為 Intel® Edison 面板設定自訂名稱。</span><span class="sxs-lookup"><span data-stu-id="989e2-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="989e2-173">這是選擇性。</span><span class="sxs-lookup"><span data-stu-id="989e2-173">This is optional.</span></span>
3. <span data-ttu-id="989e2-174">輸入面板的密碼，然後按一下 `Set password`。</span><span class="sxs-lookup"><span data-stu-id="989e2-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="989e2-175">記下密碼，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="989e2-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="989e2-176">連接 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="989e2-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="989e2-177">在 `Set up options` 頁面上，按一下 `Connect Wi-Fi`。</span><span class="sxs-lookup"><span data-stu-id="989e2-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="989e2-178">最多請等候一分鐘，讓電腦掃描可用的 Wi-Fi 網路。</span><span class="sxs-lookup"><span data-stu-id="989e2-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="989e2-179">從 `Detected Networks` 下拉式清單中選取網路。</span><span class="sxs-lookup"><span data-stu-id="989e2-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="989e2-180">從 `Security` 下拉式清單中選取網路的安全性類型。</span><span class="sxs-lookup"><span data-stu-id="989e2-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="989e2-181">提供登入和密碼資訊，然後按一下 `Configure Wi-Fi`。</span><span class="sxs-lookup"><span data-stu-id="989e2-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="989e2-182">記下 IP 位址，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="989e2-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="989e2-183">請確定 Edison 是連接到與您電腦相同的網路。</span><span class="sxs-lookup"><span data-stu-id="989e2-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="989e2-184">電腦會使用該 IP 位址連接到 Edison。</span><span class="sxs-lookup"><span data-stu-id="989e2-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="989e2-185">恭喜！</span><span class="sxs-lookup"><span data-stu-id="989e2-185">Congratulations!</span></span> <span data-ttu-id="989e2-186">您已經成功設定 Edison。</span><span class="sxs-lookup"><span data-stu-id="989e2-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="989e2-187">摘要</span><span class="sxs-lookup"><span data-stu-id="989e2-187">Summary</span></span>
<span data-ttu-id="989e2-188">在本文中，您已了解如何組裝 Edison 面板、更新其韌體、設定密碼，以及使用組態工具將它連接至 Wi-Fi。</span><span class="sxs-lookup"><span data-stu-id="989e2-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="989e2-189">請注意，LED 目前尚未亮起。</span><span class="sxs-lookup"><span data-stu-id="989e2-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="989e2-190">下一個工作是安裝必要的工具和軟體，以準備在 Edison 上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="989e2-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="989e2-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="989e2-191">Next steps</span></span>
<span data-ttu-id="989e2-192">[取得工具][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="989e2-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md