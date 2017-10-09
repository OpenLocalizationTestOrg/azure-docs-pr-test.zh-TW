---
title: "aaaRaspberry Pi toocloud (C) 的連線覆盆子 Pi tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並在本教學課程中連接覆盆子 Pi tooAzure IoT 中樞覆盆子 Pi toosend 資料 toohello Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot 木莓澆 pi 木莓澆 pi iot 中樞木莓澆 pi 傳送資料 toocloud 木莓澆 pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a>連接覆盆子 Pi tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

在本教學課程中，您必須開始學習使用執行 Raspbian 覆盆子 Pi 的 hello 基本。 然後您學習如何 tooseamlessly 裝置 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。 如需 Windows 10 IoT 核心版範例，請移 toohello [Windows 開發人員中心](http://www.windowsondevices.com/)。

還沒有套件嗎？ 試用 [Raspberry Pi 線上模擬器](iot-hub-raspberry-pi-web-simulator-get-started.md)。 或在[這裡](https://azure.microsoft.com/develop/iot/starter-kits)購買新的套件。

## <a name="what-you-do"></a>您要做什麼

* 建立 IoT 中樞。
* 在 IoT 中樞對於 Pi 註冊裝置。
* 設定 Raspberry Pi。
* Pi toosend 感應器資料 tooyour IoT 中樞上執行範例應用程式。

連接您所建立的覆盆子 Pi tooan IoT 中樞。 然後您範例應用程式上執行 Pi toocollect 氣溫和溼度資料從 BME280 感應器。 最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。

## <a name="what-you-learn"></a>您學到什麼

* 如何 toocreate Azure IoT 中樞，並取得新的裝置連接字串。
* 如何 tooconnect Pi 與 BME280 感應器。
* 如何執行範例應用程式上 Pi toocollect 感應器資料。
* 如何 toosend 感應器資料 tooyour IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

![您需要什麼](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* hello 覆盆子 Pi 2 或覆盆子 Pi 3 面板。
* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。
* 監視、 USB 鍵盤和滑鼠連接 tooPi。
* 執行 Windows 或 Linux 的 Mac 或 PC。
* 網際網路連線。
* 16 GB 以上的 microSD 記憶卡。
* USB SD 卡或 microSD 卡 tooburn hello 作業系統映像到 hello microSD 卡。
* 5 volt 2 amp 電源提供 hello 6 英呎微 USB 纜線。

hello 下列項目是選擇性項目：

* 組裝的 Adafruit BME280 溫度、壓力溼度感應器。
* 麵包板。
* 6 條 F/M 跳線。
* 1 顆漫射型 10 mm LED。


> [!NOTE] 
這些項目是選擇性的因為 hello 程式碼範例支援模擬感應器資料。


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>設定 Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Pi 安裝 hello Raspbian 作業系統

準備安裝 hello Raspbian 映像的 hello microSD 卡。

1. 下載 Raspbian。
   1. [下載與桌面 Raspbian 潔](https://www.raspberrypi.org/downloads/raspbian/)（hello.zip 檔案）。
   1. 擷取 hello Raspbian 映像電腦上的 tooa 資料夾。
1. 安裝 Raspbian toohello microSD 卡。
   1. [下載並安裝 hello Etcher sd 記憶卡燒錄機公用程式](https://etcher.io/)。
   1. 執行 Etcher，並在步驟 1 中選取您要解壓縮的 hello Raspbian 映像。
   1. 選取 hello microSD 卡磁碟機。 請注意，Etcher 可能已經選取 hello 正確的磁碟機。
   1. 按一下快閃 tooinstall Raspbian toohello microSD 卡。
   1. 安裝完成時，請從電腦移除 hello microSD 卡。 因為它是安全的 tooremove hello microSD 卡直接 Etcher 自動退出，或取消掛接 hello microSD 卡在完成時。
   1. 插入 Pi hello microSD 卡。

### <a name="enable-ssh-and-spi"></a>啟用 SSH 和 SPI

1. Pi toohello 監視器、 鍵盤和滑鼠連接、 啟動 Pi 後再登入 Raspbian 使用`pi`hello 使用者名稱和`raspberry`hello 密碼。
1. 按一下 hello 木莓澆圖示 >**喜好設定** > **覆盆子 Pi 組態**。

   ![hello Raspbian 偏好設定 功能表](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. 在 hello**介面**索引標籤上，設定**SPI**和**SSH**太**啟用**，然後按一下 **確定**。 如果沒有實體的感應器，然後想要模擬的 toouse 感應器資料，這個步驟是選擇性的。

   ![在 Raspberry Pi 上啟用 SPI 和 SSH](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH 和 SPI，您可以找到更多的參考文件上[raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/)和[RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)。

### <a name="connect-hello-sensor-toopi"></a>連接 hello 感應器 tooPi

請使用 hello breadboard 和跳接器線路 tooconnect LED 和 BME280 tooPi，如下所示。 如果您沒有 hello 感應器，[略過本節](#connect-pi-to-the-network)。

![hello 覆盆子 Pi 和感應器的連接](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

hello BME280 感應器可以收集溫度和溼度的資料。 如果沒有裝置和 hello 雲端之間的通訊，將會閃爍 hello LED。 

感應器 pin 碼，使用下列配線 hello:

| 啟動 (感應器和 LED)     | 結束 (電路版)            | 纜線顏色   |
| -----------------------  | ---------------------- | ------------: |
| LED VDD (針腳 5G)         | GPIO 4 (針腳 7)         | 白色纜線   |
| LED GND (針腳 6G)         | GND (針腳 6)            | 黑色纜線   |
| VDD (針腳 18F)            | 3.3V PWR (針腳 17)      | 白色纜線   |
| GND (針腳 20F)            | GND (針腳 20)           | 黑色纜線   |
| SCK (針腳 21F)            | SPI0 SCLK (針腳 23)     | 橘色纜線  |
| SDO (針腳 22F)            | SPI0 MISO (針腳 21)     | 黃色纜線  |
| SDI (針腳 23F)            | SPI0 MOSI (針腳 19)     | 綠色纜線   |
| CS (針腳 24F)             | SPI0 CS (針腳 24)       | 藍色纜線    |

按一下 tooview[覆盆子 Pi 2 & 3 Pin 對應](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi)供您參考。

您已成功連接 BME280 tooyour 覆盆子 Pi 之後，它應該類似影像下方。

![連接的 Pi 和 BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Pi toohello 網路連線

開啟 Pi 使用 hello 微 USB 纜線和 hello 電源供應器。 使用 hello 乙太網路纜線 tooconnect Pi tooyour 有線網路，或遵循 hello[指示從 hello 覆盆子 Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour 無線網路。 您 Pi 已成功連接的 toohello 網路之後，您需要 tootake hello 記下[您 Pi 的 IP 位址](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)。

![連接的 toowired 網路](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a>在 Pi 上執行範例應用程式

### <a name="install-hello-prerequisite-packages"></a>安裝 hello 必要條件套件

1. 使用其中一種您主機電腦 tooconnect tooyour 覆盆子 Pi 中的下列 SSH 用戶端 hello。
   
   **Windows 使用者**
   1. 下載並安裝適用於 Windows 的 [PuTTY](http://www.putty.org/)。 
   1. 複製 hello 主機名稱 （或 IP 位址） 到 Pi 區段 hello IP 位址，並選取 SSH 為 hello 的連接類型。
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Mac 和 Ubuntu 使用者**
   
   使用內建 SSH 用戶端 hello Ubuntu 或 macOS 上。 您可能需要 toorun `ssh pi@<ip address of pi>` tooconnect 透過 SSH 的 Pi。
   > [!NOTE] 
   hello 預設使用者名稱是`pi`，hello 密碼為`raspberry`。

1. 安裝 C 和 Cmake hello hello Microsoft Azure IoT 裝置 SDK 的必要條件套件執行下列命令的 hello:

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a>Hello 範例應用程式設定

1. 藉由執行下列命令的 hello 複製 hello 範例應用程式：

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. 執行下列命令的 hello 開啟 hello 設定檔：

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![組態檔](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   此檔案中有兩個巨集可供您設定。 hello 第一次是`INTERVAL`，這兩個訊息，傳送 toocloud 之間定義 hello 時間間隔 （以毫秒為單位）。 hello 第二個`SIMULATED_DATA`，這是 toouse 是否模擬感應器資料的布林值。

   如果您**沒有 hello 感應器**，將的 hello`SIMULATED_DATA`值太`1`toomake hello 範例應用程式建立及使用模擬的感應器資料。

1. 按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。

### <a name="build-and-run-hello-sample-application"></a>建置並執行 hello 範例應用程式

1. 藉由執行下列命令的 hello 建置 hello 範例應用程式：

   ```bash
   cmake . && make
   ```
   ![建置輸出](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. 藉由執行下列命令的 hello 執行 hello 範例應用程式：

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   請確定您複製-貼上 hello 裝置連接字串到 hello 單引號。


您應該會看到 hello 下列輸出顯示 hello 傳送 tooyour IoT 中樞的感應器資料及 hello 訊息。

![輸出-從覆盆子 Pi tooyour IoT 中樞傳送的感應器資料](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a>後續步驟

您已執行範例應用程式 toocollect 感應器資料，並將它傳送 tooyour IoT 中樞。 toosee 覆盆子 Pi 已傳送的 tooyour IoT 中樞或傳送訊息 tooyour 覆盆子 Pi 命令列介面中的 hello 訊息，請參閱 「 hello[管理雲端的裝置與 iot 中樞總管教學課程傳訊](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
