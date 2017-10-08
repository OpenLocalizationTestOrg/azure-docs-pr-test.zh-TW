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
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a>連接 Intel Edison tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

在本教學課程中，您必須開始學習使用 Intel Edison 的 hello 基本。 然後您學習如何 tooseamlessly 裝置 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。

還沒有套件嗎？ 從[這裡](https://azure.microsoft.com/develop/iot/starter-kits)開始

## <a name="what-you-do"></a>您要做什麼

* 設置 Intel Edison 和 Grove 模組。
* 建立 IoT 中樞。
* 在 IoT 中樞註冊 Edison 的裝置。
* 執行範例應用程式上 Edison toosend 感應器資料 tooyour IoT 中樞。

連接您所建立的 Intel Edison tooan IoT 中樞。 然後您範例應用程式上執行 Edison toocollect 氣溫和溼度資料從 Groove 溫度感應器。 最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。

## <a name="what-you-learn"></a>您學到什麼

* 如何 toocreate Azure IoT 中樞，並取得新的裝置連接字串。
* 如何 tooconnect Edison 與 Groove 溫度感應器。
* 如何執行範例應用程式上 Edison toocollect 感應器資料。
* 如何 toosend 感應器資料 tooyour IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

![您需要什麼](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* hello Intel Edison 面板
* Arduino 擴充板
* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。
* 執行 Windows 或 Linux 的 Mac 或 PC。
* 網際網路連線。
* 微 B tooType USB 纜線
* 直流電 (DC) 電源供應器。 電源供應器的額定值應如下所示︰
  - 7-15V DC
  - 至少 1500mA
  - hello 中心/內部 pin 應該 hello 正柵欄 hello 電源供應器

hello 下列項目是選擇性項目：

* Grove Base Shield V2
* Grove - 溫度感應器
* Grove 纜線
* 任何空格字元列或包含在 hello 封裝，包括兩顆螺絲 toofasten hello 模組 toohello 擴充面板和四組螺絲和塑膠空格的螺絲。

> [!NOTE] 
這些項目是選擇性的因為 hello 程式碼範例支援模擬感應器資料。

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>安裝 Intel Edison

### <a name="assemble-your-board"></a>組裝面板

本章節包含步驟 tooattach Intel® Edison 模組 tooyour 展開面板。

1. 在展開面板，排隊與 hello 螺絲 hello 擴充面板上的 hello 漏洞 hello 模組上的白色 hello 大綱內 hello Intel® Edison 模組位置。

2. Hello 字正下方的 hello 模組上按住`What will you make?`直到您覺得嵌入式管理單元。

   ![組裝面板 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. 使用 hello 兩個 （包含在 hello 封裝） 的十六進位具體 toosecure hello 模組 toohello 展開面板。

   ![組裝面板 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. 其中一種 hello 四個邊角孔 hello 擴充面板上插入螺絲。 扭曲，加強 hello 白色塑膠空格到 hello 螺絲的其中一個。

   ![組裝面板 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. 重複的 hello 其他三個角到空格字元。

   ![組裝面板 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

面板現已組裝好。

   ![組裝好的面板](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>連接 [hello] 保護盾 Groove 基底和 hello 溫度感應器

1. Hello Groove 基底保護盾置於 tooyour 面板。 確定所有針腳都緊密地插入主機板。
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. 使用 Groove 纜線 tooconnect Groove 溫度感應器到 hello Groove 基底保護盾**A0**連接埠。

   ![連接 tootemperature 感應器](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison 和感應器連接](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

現在您的感應器已就緒。

### <a name="power-up-edison"></a>將 Edison 接上電源

1. 插入 hello 電源供應器。

   ![插上電源供應器](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. （標示為 hello Arduino * 擴充面板上的 DS1） 綠色 LED 應亮起，保持 亮燈。

3. 等候一分鐘的 hello 面板 toofinish 開機。

   > [!NOTE]
   > 如果您沒有 DC 電源供應器，您仍然可以透過 USB 連接埠電源 hello 面板。 如需詳細資訊，請參閱`Connect Edison tooyour computer`一節。 以此方式為面板供電，可能會讓面板發生無法預期的行為，尤其是在使用 Wi-Fi 或驅動馬達時。

### <a name="connect-edison-tooyour-computer"></a>Edison tooyour 電腦連線

1. 使 Edison 裝置模式中，切換 hello microswitch hello 兩個微 USB 連接埠，向下。 若要了解裝置模式與主機模式的差異，請參閱[這裡](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode)。

   ![向下 hello microswitch 切換](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. 插入 hello 微 USB 纜線 hello 頂端微 USB 連接埠。

   ![最上方的 micro USB 連接埠](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. 隨插即用 hello USB 纜線的一端插入電腦。

   ![電腦 USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

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

   ![連接 tootemperature 感應器](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

恭喜！ 您已經成功設定 Edison。

## <a name="run-a-sample-application-on-intel-edison"></a>在 Intel Edison 上執行範例應用程式

### <a name="prepare-hello-azure-iot-device-sdk"></a>準備 hello Azure IoT 裝置 SDK

1. 使用其中一種您主機電腦 tooconnect tooyour Intel Edison 中的下列 SSH 用戶端 hello。 hello IP 位址來自 hello 組態工具，而且 hello 密碼為 hello 其中一個您已經設定該工具。
    - [PuTTY](http://www.putty.org/) 適用於 Windows。
    - hello 內建 SSH 用戶端上 Ubuntu 或 macOS (執行`ssh root@"hello IP address"`)。

2. 複製 hello 範例用戶端應用程式 tooyour 裝置。 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. 然後瀏覽下列命令 toobuild Azure IoT SDK toohello 儲存機制資料夾 toorun hello

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a>Hello 範例應用程式設定

1. 執行下列命令的 hello 開啟 hello 設定檔：

   ```bash
   nano config.h
   ```

   ![組態檔](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   此檔案中有兩個巨集可供您設定。 hello 第一次是`INTERVAL`，而後者可定義兩個訊息，傳送 toocloud hello 時間間隔。 hello 第二個`SIMULATED_DATA`，這是 toouse 是否模擬感應器資料的布林值。

   如果您**沒有 hello 感應器**，將的 hello`SIMULATED_DATA`值太`1`toomake hello 範例應用程式建立及使用模擬的感應器資料。

2. 按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。

### <a name="build-and-run-hello-sample-application"></a>建置並執行 hello 範例應用程式

1. 藉由執行下列命令的 hello 建置 hello 範例應用程式：

   ```bash
   cmake . && make
   ```
   ![建置輸出](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. 藉由執行下列命令的 hello 執行 hello 範例應用程式：

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   請確定您複製-貼上 hello 裝置連接字串到 hello 單引號。

您應該會看到 hello 下列輸出顯示 hello 傳送 tooyour IoT 中樞的感應器資料及 hello 訊息。

![輸出-從 Intel Edison tooyour IoT 中樞傳送的感應器資料](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a>後續步驟

您已執行範例應用程式 toocollect 感應器資料，並將它傳送 tooyour IoT 中樞。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
