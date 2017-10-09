---
title: "Connect Arduino (C) tooAzure IoT-第 1 課： 設定裝置 |Microsoft 文件"
description: "設定 Adafruit Feather M0 WiFi 以進行首次使用。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "設定好之後，arduino 連接 arduino toopc、 安裝 arduino、 arduino 面板"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>設定裝置
## <a name="what-you-will-do"></a>將執行的作業
藉由組裝 hello 面板，打開它來設定第一次您 Adafruit 羽毛 M0 WiFi Arduino 面板。 如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)。

## <a name="what-you-need"></a>您需要什麼
toocomplete 這項作業，您必須依照您 Adafruit 羽毛 M0 WiFi 的入門套件的組件的 hello:

* hello Adafruit 羽毛 M0 WiFi 面板
* 微 B tooType USB 纜線

![套件][kit]

您也會需要：

* 一部執行 Windows、Mac 或 Linux 的電腦。
* 若要您 Arduino 面板 tooconnect 無線連線。
* 網際網路連線 toodownload 組態工具。

## <a name="what-you-will-learn"></a>學習目標
在本文中，您將了解：

* 如何 tooassemble hello 遵循針對您 Arduino 面板和電源課程。
* 如何在 Ubuntu 上 tooadd 序列連接埠的權限。

## <a name="connect-your-arduino-board-tooyour-computer"></a>連接 Arduino 面板 tooyour 電腦

1. 插入 hello 微 USB 纜線 hello 頂端微 USB 連接埠。

   ![最上方的 micro USB 連接埠][top-micro-usb-port]

2. 隨插即用 hello USB 纜線的一端插入電腦。

   ![電腦 USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>在 Ubuntu 上新增序列連接埠權限

如果您使用 Windows 或 macOS，則可略過本節。 Ubuntu，您必須遵循步驟 toomake 確認 hello 一般 linux 使用者 Arduino 面板的 hello USB 連接埠上擁有 hello 權限 toooperate hello。

1. 現在從終端機以一般使用者身分︰

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   您會看到類似下面的內容：

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   hello"0"可能是不同的數字，或可能傳回多個項目。 在 hello 我們需要第一個案例的 hello 資料是`uucp`，hello 在第二個是`dialout`，即 hello hello 檔案群組擁有者。

2. 新增使用者 toohello toohello 群組：

   ```bash
   sudo usermod -a -G group-name username
   ```

   其中`group-name`hello 資料在 hello 第一個步驟中，找到並`username`是您的 linux 使用者名稱。

3. 您必須登出 toolog 一次此變更 tootake 效果和完整 hello 安裝程式。

## <a name="summary"></a>摘要
在本文中，您學到如何 tooconfigure Arduino 面板。 hello 下一個工作是 tooinstall hello 必要工具和準備 Arduino 面板上執行範例應用程式中的軟體。

![硬體已準備完畢][hardware-is-ready]

## <a name="next-steps"></a>後續步驟
[取得 hello 工具][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md