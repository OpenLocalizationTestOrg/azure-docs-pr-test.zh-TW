---
title: "Connect Intel Edison (C) tooAzure IoT-第 1 課： 設定裝置 |Microsoft 文件"
description: "設定 Intel Edison 以進行首次使用。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "設定好之後，arduino 連接 arduino toopc、 安裝 arduino、 arduino 面板"
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
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>設定 Intel Edison
## <a name="what-you-will-do"></a>將執行的作業
藉由組裝 hello 面板，打開它來設定第一次使用 Intel Edison 及安裝組態工具 tooyour 桌面 OS tooflash Edison 的韌體設定其密碼並將它連接 tooWi Wi-fi。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：

* 如何 tooassemble Edison 面板和電源設定。
* 如何 tooflash Edison 韌體設定的密碼，並連接 Wi-fi。

## <a name="what-you-need"></a>您需要什麼
toocomplete 這項作業，您需要 hello Intel Edison 的入門套件中的下列部分：

* Intel® Edison 模組
* Arduino 擴充板
* 任何空格字元列或包含在 hello 封裝，包括兩顆螺絲 toofasten hello 模組 toohello 擴充面板和四組螺絲和塑膠空格的螺絲。
* 微 B tooType USB 纜線
* 直流電 (DC) 電源供應器。 電源供應器的額定值應如下所示︰
  - 7-15V DC
  - 至少 1500mA
  - hello 中心/內部 pin 應該 hello 正柵欄 hello 電源供應器

  ![入門套件中的零件](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

您也會需要：

* 一部執行 Windows、Mac 或 Linux 的電腦。
* 若要 Edison tooconnect 無線連線。
* 網際網路連線 toodownload 組態工具。

## <a name="assemble-your-board"></a>組裝面板

本章節包含步驟 tooattach Intel® Edison 模組 tooyour 展開面板。

1. 在展開面板，排隊與 hello 螺絲 hello 擴充面板上的 hello 漏洞 hello 模組上的白色 hello 大綱內 hello Intel® Edison 模組位置。

2. Hello 字正下方的 hello 模組上按住`What will you make?`直到您覺得嵌入式管理單元。

   ![組裝面板 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. 使用 hello 兩個 （包含在 hello 封裝） 的十六進位具體 toosecure hello 模組 toohello 展開面板。

   ![組裝面板 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. 其中一種 hello 四個邊角孔 hello 擴充面板上插入螺絲。 扭曲，加強 hello 白色塑膠空格到 hello 螺絲的其中一個。

   ![組裝面板 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. 重複的 hello 其他三個角到空格字元。

   ![組裝面板 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

面板現已組裝好。

   ![組裝好的面板](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>將 Edison 接上電源

1. 插入 hello 電源供應器。

   ![插上電源供應器](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. （標示為 hello Arduino * 擴充面板上的 DS1） 綠色 LED 應亮起，保持 亮燈。

3. 等候一分鐘的 hello 面板 toofinish 開機。

   > [!NOTE]
   > 如果您沒有 DC 電源供應器，您仍然可以透過 USB 連接埠電源 hello 面板。 如需詳細資訊，請參閱`Connect Edison tooyour computer`一節。 以此方式為面板供電，可能會讓面板發生無法預期的行為，尤其是在使用 Wi-Fi 或驅動馬達時。

## <a name="connect-edison-tooyour-computer"></a>Edison tooyour 電腦連線

1. 使 Edison 裝置模式中，切換 hello microswitch hello 兩個微 USB 連接埠，向下。 若要了解裝置模式與主機模式的差異，請參閱[這裡](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)。

   ![向下 hello microswitch 切換](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. 插入 hello 微 USB 纜線 hello 頂端微 USB 連接埠。

   ![最上方的 micro USB 連接埠](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. 隨插即用 hello USB 纜線的一端插入電腦。

   ![電腦 USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. 當電腦掛接新的磁碟機 (很像將 SD 卡插入電腦) 時，您就會知道面板已完全初始化。

## <a name="download-and-run-hello-configuration-tool"></a>下載並執行 hello 組態工具
取得從 hello 最新組態工具[此連結](https://software.intel.com/en-us/iot/hardware/edison/downloads)列在 hello`Installers`標題。 執行 hello 工具並依照其螢幕上的指示，在需要時，請按一下下一步

### <a name="flash-firmware"></a>更新韌體
1. 在 hello`Set up options`頁面上，按一下`Flash Firmware`。
2. 選取到您的面板 hello 映像 tooflash hello 下列其中一項動作：
   - 您面板與 hello 最新的韌體映像可用 intel toodownload 和 flash 選取`Download hello latest image version xxxx`。
   - tooflash 您面板，您已經儲存您的電腦上的映像選取`Select hello local image`。 瀏覽要 tooflash tooyour 面板 tooand 選取 hello 映像。
3. hello 安裝工具會嘗試 tooflash 您面板。 hello 整個閃爍程序可能佔用 too10 分鐘。

### <a name="set-password"></a>設定密碼
1. 在 hello`Set up options`頁面上，按一下`Enable Security`。
2. 您可以為 Intel® Edison 面板設定自訂名稱。 這是選擇性。
3. 輸入面板的密碼，然後按一下 `Set password`。
4. 標記下 hello 密碼，以便稍後用。

### <a name="connect-wi-fi"></a>連接 Wi-Fi
1. 在 hello`Set up options`頁面上，按一下`Connect Wi-Fi`。 設定可用的 Wi-fi 網路電腦掃描 tooone 分鐘的等候。
2. 從 hello`Detected Networks`下拉式清單中，選取您的網路。
3. 從 hello`Security`下拉式清單中，選取 hello 網路的安全性類型。
4. 提供登入和密碼資訊，然後按一下 `Configure Wi-Fi`。
5. 標記下 hello IP 位址，以便稍後用。

> [!NOTE]
> 請確定 Edison 連接的 toohello 相同網路做為您的電腦。 您的電腦連線 tooyour Edison 使用 hello IP 位址。

恭喜！ 您已經成功設定 Edison。

## <a name="summary"></a>摘要
在本文中，您學到如何 tooassemble hello Edison 面板、 flash 其韌體、 設定密碼並將它連接 tooWi Fi 使用組態工具。 請注意該 hello LED 尚無法亮起。 hello 下一個工作是 tooinstall hello 必要工具和準備 Edison 上執行範例應用程式中的軟體。

## <a name="next-steps"></a>後續步驟
[取得 hello 工具][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md