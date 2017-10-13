---
title: "Raspberry Pi 至 cloud (C) - 將 Raspberry Pi 連接至 Azure IoT 中樞 | Microsoft Docs"
description: "了解在本教學課程中如何設定及連線 Raspberry Pi 至 Azure IoT 中樞，讓 Raspberry Pi 將資料傳送到 Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot 中樞, raspberry pi 將資料傳送至雲端, raspberry pi 至 cloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b8fda17a8d1d1796d5299e3aba4b0fd5e719a4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-c"></a>將 Raspberry Pi 連接至 Azure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

在本教學課程中，您會開始了解執行 Raspbian 的 Raspberry Pi 在使用方面的基本知識。 接著會了解如何使用 [Azure IoT 中樞](iot-hub-what-is-iot-hub.md)讓您的裝置順暢地與雲端連線。 如需 Windows 10 IoT 核心範例，請移至 [Windows 開發人員中心](http://www.windowsondevices.com/)。

還沒有套件嗎？ 試用 [Raspberry Pi 線上模擬器](iot-hub-raspberry-pi-web-simulator-get-started.md)。 或在[這裡](https://azure.microsoft.com/develop/iot/starter-kits)購買新的套件。

## <a name="what-you-do"></a>您要做什麼

* 建立 IoT 中樞。
* 在 IoT 中樞對於 Pi 註冊裝置。
* 設定 Raspberry Pi。
* 在 Pi 上執行範例應用程式，將感應器資料傳送至 IoT 中樞。

將 Raspberry Pi 連接至您建立的 IoT 中樞。 然後，在 Pi 上執行範例應用程式，以收集 BME280 感應器中的溫度和溼度資料。 最後，將感應器資料傳送至 IoT 中樞。

## <a name="what-you-learn"></a>您學到什麼

* 如何建立 Azure IoT 中樞，並取得新的裝置連接字串。
* 如何連接 Pi 與 BME280 感應器。
* 如何在 Pi 上執行範例應用程式來收集感應器資料。
* 如何將感應器資料傳送至 IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

![您需要什麼](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* Raspberry Pi 2 或 Raspberry Pi 3 電路板。
* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。
* 連接至 Pi 的監視器、 USB 鍵盤和滑鼠。
* 執行 Windows 或 Linux 的 Mac 或 PC。
* 網際網路連線。
* 16 GB 以上的 microSD 記憶卡。
* 一個 USB-SD 配接器或 microSD 記憶卡，以將作業系統映像燒錄到 microSD 記憶卡中。
* 具備 6 英呎 micro USB 纜線的 5V 2A 電源供應器。

下列項目是選用項目︰

* 組裝的 Adafruit BME280 溫度、壓力溼度感應器。
* 麵包板。
* 6 條 F/M 跳線。
* 1 顆漫射型 10 mm LED。


> [!NOTE] 
這些項目都是選用項目，因為程式碼範例支援模擬感應器資料。


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>設定 Raspberry Pi

### <a name="install-the-raspbian-operating-system-for-pi"></a>安裝 Pi 的 Raspbian 作業系統

準備好用來安裝 Raspbian 映像的 microSD 記憶卡。

1. 下載 Raspbian。
   1. [下載具備 Desktop 的 Raspbian Jessie](https://www.raspberrypi.org/downloads/raspbian/) (.zip 檔案)。
   1. 將 Raspbian 映像解壓縮到您電腦上的資料夾。
1. 將 Raspbian 安裝到 microSD 記憶卡。
   1. [下載並安裝 Etcher SD 記憶卡燒錄器公用程式](https://etcher.io/)。
   1. 執行 Etcher 並選取您在步驟 1 中解壓縮的 Raspbian 映像。
   1. 選取 microSD 記憶卡磁碟機。 注意：Etcher 可能已經選取正確的磁碟機。
   1. 按一下 [Flash] 以將 Raspbian 安裝到 microSD 記憶卡。
   1. 安裝完成時，請將 microSD 記憶卡從電腦移除。 您可以放心地直接移除 microSD 記憶卡，因為 Etcher 會在完成時自動退出或卸載 microSD 記憶卡。
   1. 將 microSD 記憶卡插入 Pi。

### <a name="enable-ssh-and-spi"></a>啟用 SSH 和 SPI

1. 將 Pi 連接至監視器、鍵盤和滑鼠，並啟動 Pi，然後使用使用者名稱 `pi` 和密碼 `raspberry` 登入 Raspbian。
1. 按一下 Raspberry 圖示 > [偏好設定] > [Raspberry Pi 組態]。

   ![[Raspbian 偏好設定] 功能表](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. 在 [介面]索引標籤上，將 [SPI] 和 [SSH] 設定為 [啟用]，然後按一下 [確定]。 如果您沒有實體感應器，而且想要使用模擬的感應器資料，這便是選擇性步驟。

   ![在 Raspberry Pi 上啟用 SPI 和 SSH](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
若要啟用 SSH 和 SPI，您可以在 [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) 和[RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md) 找到更多參考文件。

### <a name="connect-the-sensor-to-pi"></a>將感應器連接至 Pi

使用麵包板和跳線將 LED 和 BME280 連接至 Pi，如下所示。 如果沒有感應器，請[略過本節](#connect-pi-to-the-network)。

![Raspberry Pi 和感應器連接](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

BME280 感應器可以收集溫度和溼度資料。 而如果裝置與雲端之間有通訊，LED 將會閃爍。 

針對感應器針腳，請使用下列接線方式：

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

按一下以檢視 [Raspberry Pi 2 和 3 針腳對應](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi)進行參考。

將 BME280 成功連接至 Raspberry Pi 之後，應該如下圖所示。

![連接的 Pi 和 BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a>將 Pi 連線到網路

透過 micro USB 纜線和電源供應器來開啟 Pi。 使用乙太網路纜線將 Pi 連接到有線網路，或遵循來自 Raspberry Pi Foundation 的[指示](https://www.raspberrypi.org/learning/software-guide/wifi/)，將 Pi 連接到無線網路。 在 Pi 成功連線到網路之後，您需要記下 [Pi 的 IP 位址](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)。

![已連接到有線網路](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a>在 Pi 上執行範例應用程式

### <a name="install-the-prerequisite-packages"></a>安裝必要條件套件

1. 使用下列其中一個 SSH 用戶端，從主機電腦連接到 Raspberry Pi。
   
   **Windows 使用者**
   1. 下載並安裝適用於 Windows 的 [PuTTY](http://www.putty.org/)。 
   1. 將 Pi 的 IP 位址複製到 [主機名稱] 或 [IP 位址] 區段，並且選取 SSH 作為連線類型。
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Mac 和 Ubuntu 使用者**
   
   在 Ubuntu 或 macOS 上使用內建的 SSH 用戶端。 您可能需要執行 `ssh pi@<ip address of pi>`，才能透過 SSH 來連線 Pi。
   > [!NOTE] 
   預設使用者名稱為 `pi`，密碼為 `raspberry`。

1. 執行下列命令，安裝 Microsoft Azure IoT Device SDK for C and Cmake 的必要條件套件︰

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


### <a name="configure-the-sample-application"></a>設定範例應用程式

1. 執行下列命令，複製範例應用程式：

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. 執行下列命令以開啟組態檔：

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![組態檔](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   此檔案中有兩個巨集可供您設定。 第一個是 `INTERVAL`，這可定義傳送至雲端的兩個訊息之間相隔的時間間隔 (以毫秒為單位)。 第二個是 `SIMULATED_DATA`，這是是否使用模擬感應器資料的布林值。

   如果**沒有感應器**，請將 `SIMULATED_DATA` 值設定為 `1`，使範例應用程式建立和使用模擬感應器資料。

1. 按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。

### <a name="build-and-run-the-sample-application"></a>建置並執行範例應用程式

1. 執行下列命令，建置範例應用程式：

   ```bash
   cmake . && make
   ```
   ![建置輸出](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. 執行下列命令，執行範例應用程式：

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   確定複製裝置連接字串，並貼到單引號中。


您應該會看見下列輸出，顯示傳送至 IoT 中樞的感應器資料和訊息。

![輸出 - 從 Raspberry Pi 傳送至 IoT 中樞的感應器資料](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a>後續步驟

您已執行範例應用程式收集感應器資料並傳送至 IoT 中樞。 若要查看 Raspberry Pi 傳送給 IoT 中樞的訊息，或者在命令列介面中將訊息傳送給 Raspberry Pi，請參閱[使用 iothub-explorer 管理雲端裝置訊息教學課程](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
