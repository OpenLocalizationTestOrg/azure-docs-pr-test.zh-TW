---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 1 課： 設定裝置 |Microsoft 文件"
description: "設定覆盆子 Pi 3 供第一次使用並安裝 hello Raspbian OS，最適合用於 hello 覆盆子 Pi 硬體可用的作業系統。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "安裝 raspbian，raspbian 下載如何 tooinstall raspbian raspbian 安裝木莓澆 pi 安裝 raspbian 木莓澆 pi 安裝作業系統、 木莓澆 pi sd 記憶卡安裝、 木莓澆 pi connect 連接 tooraspberry pi 木莓澆 pi 連線"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>設定裝置
## <a name="what-you-will-do"></a>將執行的作業
設定第一次使用 Pi 和 hello Raspbian 作業系統安裝。 Raspbian 是可用的最適合用於 hello 覆盆子 Pi 硬體上的作業系統。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：

* 如何 tooinstall Raspbian pi。
* 如何使用 USB 纜線向上 Pi toopower。
* 如何 tooconnect Pi toohello 網路使用乙太網路纜線或無線網路。
* 如何 tooadd LED toohello breadboard 並將它連接 tooPi。

## <a name="what-you-need"></a>您需要什麼
toocomplete 這項作業，您需要 hello 覆盆子 Pi 3 入門套件中的下列部分：

* hello 覆盆子 Pi 3 面板
* hello 16 GB microSD 卡
* 與 hello 6 英呎微 USB 纜線的 hello 5 volt 2 amp 電源供應器
* hello breadboard
* 接頭電線
* 一顆 560 歐姆的電阻
* 一顆漫射型 10 mm LED
* hello 乙太網路纜線

![入門套件中的零件](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

您也會需要：

* 若要 Pi tooconnect 有線或無線連線。
* USB SD 配接器或迷你 sd 記憶卡 tooburn hello OS 映像到 hello microSD 卡。
* 一部執行 Windows、Mac 或 Linux 的電腦。 hello 電腦是使用的 tooinstall Raspbian hello microSD 卡上。
* 網際網路連線 toodownload hello 必要工具和軟體。

## <a name="install-raspbian-on-hello-microsd-card"></a>在 hello MicroSD 卡上安裝 Raspbian
準備安裝 hello Raspbian 映像的 hello microSD 卡。

1. 下載 Raspbian。
   1. [下載](https://www.raspberrypi.org/downloads/raspbian/)Raspbian 潔與像素的 hello.zip 檔案。
   2. 擷取 hello Raspbian 映像電腦上的 tooa 資料夾。
2. 安裝 Raspbian toohello microSD 卡。
   1. [下載](https://www.etcher.io)及安裝 hello Etcher sd 記憶卡燒錄機公用程式。
   2. 執行 Etcher，並在步驟 1 中選取您要解壓縮的 hello Raspbian 映像。
   3. 選取 hello microSD 卡磁碟機。
      請注意，Etcher 可能已經選取 hello 正確的磁碟機。
   4. 按一下**快閃**tooinstall Raspbian toohello microSD 卡。
   5. 安裝完成時，請從電腦移除 hello microSD 卡。
      因為它是安全的 tooremove hello microSD 卡直接 Etcher 自動退出，或取消掛接 hello microSD 卡在完成時。
   6. 插入您 Pi hello microSD 卡。

![插入 hello sd 記憶卡](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>開啟 Pi
開啟 Pi 使用 hello 微 USB 纜線和 hello 電源供應器。

![開啟](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> 它是至少為 hello 套件中的重要 toouse hello 電源供應器 2A toomake 確定您覆盆子具有足夠的電力 toowork 正確。

## <a name="enable-ssh"></a>啟用 SSH
截至 hello 2016 年 11 月發行，Raspbian 會提供預設停用的 hello SSH 伺服器。 您需要 tooenable 它以手動方式。 您可以使用參照 toohello[官方指示](https://www.raspberrypi.org/documentation/remote-access/ssh/)或連接監視器，並跳過**喜好設定]-> [覆盆子 Pi 組態**tooenable SSH。

## <a name="connect-raspberry-pi-3-toohello-network"></a>覆盆子 Pi 3 toohello 網路連線
您可以連接 Pi tooa 有線網路或 tooa 無線網路。 請確定 Pi 為您的電腦相同網路的連線的 toohello。 例如，您可以連接 Pi toohello 相同切換電腦連線到。

### <a name="connect-tooa-wired-network"></a>連接 tooa 有線網路
使用 hello 乙太網路纜線 tooconnect Pi tooyour 有線網路。 hello pi 的兩個 Led，如果啟動 hello 連接。

![使用乙太網路纜線連接](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Tooa 無線網路連線
請遵循 hello[指示](https://www.raspberrypi.org/learning/software-guide/wifi/)hello 覆盆子 Pi Foundation tooconnect Pi tooyour 無線網路。 這些指示需要您 toofirst 連接監視器與鍵盤 tooPi。

## <a name="connect-hello-led-toopi"></a>連接 hello LED tooPi
toocomplete 這個工作，使用 hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard)、 hello 連接器線路、 hello LED，和 hello 電阻。 將它們連接 toohello[一般用途輸入/輸出](https://www.raspberrypi.org/documentation/usage/gpio/)Pi (GPIO) 連接埠。

![麵包板、LED 及電阻](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. 連接的 hello LED hello 短腳太**GPIO GND (Pin 6)**。
2. 連接 hello hello 電阻 LED tooone 階段 hello 長的腳。
3. 連接太 hello hello 電阻其他階段**GPIO 4 (Pin 7)**。

請注意 hello LED 極性是很重要。 此極性設定通稱為低態動作。

![接腳圖](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

恭喜！ 您已經成功設定 Pi。

## <a name="summary"></a>摘要
在本文中，您學到如何 tooconfigure Pi 安裝 Raspbian，連接 Pi tooa 網路，並將連接 LED tooPi。 請注意該 hello LED 尚無法亮起。 hello 下一個工作是 tooinstall hello 必要工具和準備 Pi 上執行範例應用程式中的軟體。

![硬體已準備完畢](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>後續步驟
[取得 hello 工具](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

