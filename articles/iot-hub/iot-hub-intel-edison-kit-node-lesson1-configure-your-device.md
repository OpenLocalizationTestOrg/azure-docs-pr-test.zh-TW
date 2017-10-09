---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 1 課： 設定裝置 |Microsoft 文件"
description: "設定 Intel Edison 以進行首次使用。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "設定好之後，arduino 連接 arduino toopc、 安裝 arduino、 arduino 面板"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="6178a-104">設定 Intel Edison</span><span class="sxs-lookup"><span data-stu-id="6178a-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="6178a-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="6178a-105">What you will do</span></span>
<span data-ttu-id="6178a-106">藉由組裝 hello 面板，打開它來設定第一次使用 Intel Edison 及安裝組態工具 tooyour 桌面 OS tooflash Edison 的韌體設定其密碼並將它連接 tooWi Wi-fi。</span><span class="sxs-lookup"><span data-stu-id="6178a-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="6178a-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="6178a-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6178a-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="6178a-108">What you will learn</span></span>
<span data-ttu-id="6178a-109">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="6178a-109">In this article, you will learn:</span></span>

* <span data-ttu-id="6178a-110">如何 tooassemble Edison 面板和電源設定。</span><span class="sxs-lookup"><span data-stu-id="6178a-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="6178a-111">如何 tooflash Edison 韌體設定的密碼，並連接 Wi-fi。</span><span class="sxs-lookup"><span data-stu-id="6178a-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6178a-112">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="6178a-112">What you need</span></span>
<span data-ttu-id="6178a-113">toocomplete 這項作業，您需要 hello Intel Edison 的入門套件中的下列部分：</span><span class="sxs-lookup"><span data-stu-id="6178a-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="6178a-114">Intel® Edison 模組</span><span class="sxs-lookup"><span data-stu-id="6178a-114">Intel® Edison module</span></span>
* <span data-ttu-id="6178a-115">Arduino 擴充板</span><span class="sxs-lookup"><span data-stu-id="6178a-115">Arduino expansion board</span></span>
* <span data-ttu-id="6178a-116">任何空格字元列或包含在 hello 封裝，包括兩顆螺絲 toofasten hello 模組 toohello 擴充面板和四組螺絲和塑膠空格的螺絲。</span><span class="sxs-lookup"><span data-stu-id="6178a-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="6178a-117">微 B tooType USB 纜線</span><span class="sxs-lookup"><span data-stu-id="6178a-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="6178a-118">直流電 (DC) 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="6178a-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="6178a-119">電源供應器的額定值應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6178a-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="6178a-120">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="6178a-120">7-15V DC</span></span>
  - <span data-ttu-id="6178a-121">至少 1500mA</span><span class="sxs-lookup"><span data-stu-id="6178a-121">At least 1500mA</span></span>
  - <span data-ttu-id="6178a-122">hello 中心/內部 pin 應該 hello 正柵欄 hello 電源供應器</span><span class="sxs-lookup"><span data-stu-id="6178a-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![入門套件中的零件](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="6178a-124">您也會需要：</span><span class="sxs-lookup"><span data-stu-id="6178a-124">You also need:</span></span>

* <span data-ttu-id="6178a-125">一部執行 Windows、Mac 或 Linux 的電腦。</span><span class="sxs-lookup"><span data-stu-id="6178a-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="6178a-126">若要 Edison tooconnect 無線連線。</span><span class="sxs-lookup"><span data-stu-id="6178a-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="6178a-127">網際網路連線 toodownload 組態工具。</span><span class="sxs-lookup"><span data-stu-id="6178a-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="6178a-128">組裝面板</span><span class="sxs-lookup"><span data-stu-id="6178a-128">Assemble your board</span></span>

<span data-ttu-id="6178a-129">本章節包含步驟 tooattach Intel® Edison 模組 tooyour 展開面板。</span><span class="sxs-lookup"><span data-stu-id="6178a-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="6178a-130">在展開面板，排隊與 hello 螺絲 hello 擴充面板上的 hello 漏洞 hello 模組上的白色 hello 大綱內 hello Intel® Edison 模組位置。</span><span class="sxs-lookup"><span data-stu-id="6178a-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="6178a-131">Hello 字正下方的 hello 模組上按住`What will you make?`直到您覺得嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="6178a-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![組裝面板 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="6178a-133">使用 hello 兩個 （包含在 hello 封裝） 的十六進位具體 toosecure hello 模組 toohello 展開面板。</span><span class="sxs-lookup"><span data-stu-id="6178a-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![組裝面板 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="6178a-135">其中一種 hello 四個邊角孔 hello 擴充面板上插入螺絲。</span><span class="sxs-lookup"><span data-stu-id="6178a-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="6178a-136">扭曲，加強 hello 白色塑膠空格到 hello 螺絲的其中一個。</span><span class="sxs-lookup"><span data-stu-id="6178a-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![組裝面板 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="6178a-138">重複的 hello 其他三個角到空格字元。</span><span class="sxs-lookup"><span data-stu-id="6178a-138">Repeat for hello other three corner spacers.</span></span>

   ![組裝面板 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="6178a-140">面板現已組裝好。</span><span class="sxs-lookup"><span data-stu-id="6178a-140">Now your board is assembled.</span></span>

   ![組裝好的面板](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="6178a-142">將 Edison 接上電源</span><span class="sxs-lookup"><span data-stu-id="6178a-142">Power up Edison</span></span>

1. <span data-ttu-id="6178a-143">插入 hello 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="6178a-143">Plug in hello power supply.</span></span>

   ![插上電源供應器](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="6178a-145">（標示為 hello Arduino * 擴充面板上的 DS1） 綠色 LED 應亮起，保持 亮燈。</span><span class="sxs-lookup"><span data-stu-id="6178a-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="6178a-146">等候一分鐘的 hello 面板 toofinish 開機。</span><span class="sxs-lookup"><span data-stu-id="6178a-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6178a-147">如果您沒有 DC 電源供應器，您仍然可以透過 USB 連接埠電源 hello 面板。</span><span class="sxs-lookup"><span data-stu-id="6178a-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="6178a-148">如需詳細資訊，請參閱`Connect Edison tooyour computer`一節。</span><span class="sxs-lookup"><span data-stu-id="6178a-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="6178a-149">以此方式為面板供電，可能會讓面板發生無法預期的行為，尤其是在使用 Wi-Fi 或驅動馬達時。</span><span class="sxs-lookup"><span data-stu-id="6178a-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="6178a-150">Edison tooyour 電腦連線</span><span class="sxs-lookup"><span data-stu-id="6178a-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="6178a-151">使 Edison 裝置模式中，切換 hello microswitch hello 兩個微 USB 連接埠，向下。</span><span class="sxs-lookup"><span data-stu-id="6178a-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="6178a-152">若要了解裝置模式與主機模式的差異，請參閱[這裡](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)。</span><span class="sxs-lookup"><span data-stu-id="6178a-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![向下 hello microswitch 切換](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="6178a-154">插入 hello 微 USB 纜線 hello 頂端微 USB 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6178a-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![最上方的 micro USB 連接埠](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="6178a-156">隨插即用 hello USB 纜線的一端插入電腦。</span><span class="sxs-lookup"><span data-stu-id="6178a-156">Plug hello other end of USB cable into your computer.</span></span>

   ![電腦 USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="6178a-158">當電腦掛接新的磁碟機 (很像將 SD 卡插入電腦) 時，您就會知道面板已完全初始化。</span><span class="sxs-lookup"><span data-stu-id="6178a-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="6178a-159">下載並執行 hello 組態工具</span><span class="sxs-lookup"><span data-stu-id="6178a-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="6178a-160">取得從 hello 最新組態工具[此連結](https://software.intel.com/en-us/iot/hardware/edison/downloads)列在 hello`Installers`標題。</span><span class="sxs-lookup"><span data-stu-id="6178a-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="6178a-161">執行 hello 工具並依照其螢幕上的指示，在需要時，請按一下下一步</span><span class="sxs-lookup"><span data-stu-id="6178a-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="6178a-162">更新韌體</span><span class="sxs-lookup"><span data-stu-id="6178a-162">Flash firmware</span></span>
1. <span data-ttu-id="6178a-163">在 hello`Set up options`頁面上，按一下`Flash Firmware`。</span><span class="sxs-lookup"><span data-stu-id="6178a-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="6178a-164">選取到您的面板 hello 映像 tooflash hello 下列其中一項動作：</span><span class="sxs-lookup"><span data-stu-id="6178a-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="6178a-165">您面板與 hello 最新的韌體映像可用 intel toodownload 和 flash 選取`Download hello latest image version xxxx`。</span><span class="sxs-lookup"><span data-stu-id="6178a-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="6178a-166">tooflash 您面板，您已經儲存您的電腦上的映像選取`Select hello local image`。</span><span class="sxs-lookup"><span data-stu-id="6178a-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="6178a-167">瀏覽要 tooflash tooyour 面板 tooand 選取 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="6178a-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="6178a-168">hello 安裝工具會嘗試 tooflash 您面板。</span><span class="sxs-lookup"><span data-stu-id="6178a-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="6178a-169">hello 整個閃爍程序可能佔用 too10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6178a-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="6178a-170">設定密碼</span><span class="sxs-lookup"><span data-stu-id="6178a-170">Set password</span></span>
1. <span data-ttu-id="6178a-171">在 hello`Set up options`頁面上，按一下`Enable Security`。</span><span class="sxs-lookup"><span data-stu-id="6178a-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="6178a-172">您可以為 Intel® Edison 面板設定自訂名稱。</span><span class="sxs-lookup"><span data-stu-id="6178a-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="6178a-173">這是選擇性。</span><span class="sxs-lookup"><span data-stu-id="6178a-173">This is optional.</span></span>
3. <span data-ttu-id="6178a-174">輸入面板的密碼，然後按一下 `Set password`。</span><span class="sxs-lookup"><span data-stu-id="6178a-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="6178a-175">標記下 hello 密碼，以便稍後用。</span><span class="sxs-lookup"><span data-stu-id="6178a-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="6178a-176">連接 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="6178a-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="6178a-177">在 hello`Set up options`頁面上，按一下`Connect Wi-Fi`。</span><span class="sxs-lookup"><span data-stu-id="6178a-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="6178a-178">設定可用的 Wi-fi 網路電腦掃描 tooone 分鐘的等候。</span><span class="sxs-lookup"><span data-stu-id="6178a-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="6178a-179">從 hello`Detected Networks`下拉式清單中，選取您的網路。</span><span class="sxs-lookup"><span data-stu-id="6178a-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="6178a-180">從 hello`Security`下拉式清單中，選取 hello 網路的安全性類型。</span><span class="sxs-lookup"><span data-stu-id="6178a-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="6178a-181">提供登入和密碼資訊，然後按一下 `Configure Wi-Fi`。</span><span class="sxs-lookup"><span data-stu-id="6178a-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="6178a-182">標記下 hello IP 位址，以便稍後用。</span><span class="sxs-lookup"><span data-stu-id="6178a-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="6178a-183">請確定 Edison 連接的 toohello 相同網路做為您的電腦。</span><span class="sxs-lookup"><span data-stu-id="6178a-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="6178a-184">您的電腦連線 tooyour Edison 使用 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6178a-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="6178a-185">恭喜！</span><span class="sxs-lookup"><span data-stu-id="6178a-185">Congratulations!</span></span> <span data-ttu-id="6178a-186">您已經成功設定 Edison。</span><span class="sxs-lookup"><span data-stu-id="6178a-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="6178a-187">摘要</span><span class="sxs-lookup"><span data-stu-id="6178a-187">Summary</span></span>
<span data-ttu-id="6178a-188">在本文中，您學到如何 tooassemble hello Edison 面板、 flash 其韌體、 設定密碼並將它連接 tooWi Fi 使用組態工具。</span><span class="sxs-lookup"><span data-stu-id="6178a-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="6178a-189">請注意該 hello LED 尚無法亮起。</span><span class="sxs-lookup"><span data-stu-id="6178a-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="6178a-190">hello 下一個工作是 tooinstall hello 必要工具和準備 Edison 上執行範例應用程式中的軟體。</span><span class="sxs-lookup"><span data-stu-id="6178a-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6178a-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6178a-191">Next steps</span></span>
<span data-ttu-id="6178a-192">[取得 hello 工具][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="6178a-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md