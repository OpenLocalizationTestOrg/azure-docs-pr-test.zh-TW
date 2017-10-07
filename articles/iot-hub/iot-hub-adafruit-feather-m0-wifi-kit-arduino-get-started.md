---
title: "M0 toocloud： 連接羽毛 M0 WiFi tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 tooset 及 Adafruit 羽毛 M0 WiFi tooAzure IoT 中樞 toosend 資料 toohello Azure 雲端平台連接在此教學課程。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>連接 Adafruit 羽毛 M0 WiFi tooAzure hello 雲端中的 IoT 中樞
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![BME280、Feather M0 WiFi 與 IoT 中樞之間的連線](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

在本教學課程中，您必須開始學習使用 Arduino 面板的 hello 基本。 然後您學習如何 tooseamlessly 裝置 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。

## <a name="what-you-do"></a>您要做什麼

連接您所建立的 Adafruit 羽毛 M0 WiFi tooan IoT 中樞。 然後從 BME280 M0 WiFi toocollect hello 氣溫和溼度資料上執行範例應用程式。 最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。


## <a name="what-you-learn"></a>您學到什麼

* 如何 toocreate IoT 中樞和羽毛 M0 WiFi 如註冊裝置
* 如何 tooconnect 羽毛 M0 WiFi hello 感應器與您的電腦
* 如何執行範例應用程式上羽毛 M0 WiFi toocollect 感應器資料
* 如何 toosend hello 感應器資料 tooyour IoT 中樞

## <a name="what-you-need"></a>您需要什麼

![Hello 教學課程需要的組件](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete 這項作業，您需要 hello 羽毛 M0 WiFi 入門套件中的下列部分：

* hello 羽毛 M0 WiFi 面板
* 微 USB tooType USB 纜線

您還需要下列項目，為您的開發環境的 hello:

* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。
* 執行 Windows 或 Ubuntu 的 Mac 或 PC。
* 若要羽毛 M0 WiFi tooconnect 無線網路。
* 網際網路連線 toodownload hello 組態工具。
* [Arduino IDE](https://www.arduino.cc/en/main/software) 1.6.8 版或更新版本。 舊版未使用 hello Azure IoT 中樞程式庫。

如果您沒有感應器，hello 下列項目是選擇性的。 您也可以使用模擬的感應器資料的 hello 選項：

* BME280 溫度和溼度感應器
* 麵包板
* M/M 跳線

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>聯繫羽毛 M0 WiFi hello 感應器和您的電腦
在本節中，您可以連接 hello 感應器 tooyour 面板。 然後您插入以便進一步使用於您裝置的 tooyour 電腦。

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>連接 DHT22 氣溫和溼度感應器 tooFeather M0 WiFi

使用 hello breadboard 和跳接器線路 toomake hello 的連線。 如果您沒有感應器，請略過本節，因為您可以改為使用模擬的感應器資料。

![連接參考](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


感應器 pin 碼，使用下列配線 hello:


| 開始 (感應器)           | 結束 (電路版)            | 纜線顏色   |
| -----------------------  | ---------------------- | ------------: |
| VDD (針腳 27A)            | 3V (針腳 3A)            | 紅色纜線     |
| GND (針腳 29A)            | GND (針腳 6A)           | 黑色纜線   |
| SCK (針腳 30A)            | SCK (針腳 12A)          | 黃色纜線  |
| SDO (針腳 31A)            | MI (針腳 14A)           | 白色纜線   |
| SDI (針腳 32A)            | M0 (針腳 13A)           | 藍色纜線    |
| cs (針腳 33A)             | GPIO 5 (針腳 15J)       | 橘色纜線  |

如需詳細資訊，請參閱 [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Adafruit BME280 溼度 + 氣壓 + 溫度感應器分組) 和 [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts) (Adafruit Feather M0 WiFi 接腳圖)。



現在，Feather M0 WiFi 應該已經和作用中的感應器連接。

![連接 DHT22 與 Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>羽毛 M0 WiFi tooyour 電腦連線

使用 hello 微 USB tooType USB 纜線 tooconnect 羽毛 M0 WiFi tooyour 的電腦，如下所示：

![羽毛 Huzzah tooyour 電腦連線](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>新增序列埠權限 (僅限 Ubuntu)

如果您使用 Ubuntu，請確定您擁有 hello 權限 toooperate 上 hello USB 連接埠的羽毛 M0 WiFi。 tooadd 序列連接埠的權限，請遵循下列步驟：


1. 在終端機中，執行下列命令的 hello:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   您取得其中一個 hello 下列輸出：

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   在 hello 輸出中，請注意，`uucp`或`dialout`hello USB 連接埠 hello 群組擁有者名稱。

2. tooadd hello 使用者 toohello 群組，執行下列命令的 hello:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   您可以在 hello 先前步驟中，取得 hello 群組擁有者名稱`<group-owner-name>`。 `<username>` 是 Ubuntu 使用者名稱。

3. Hello 變更 tooappear，如登出 Ubuntu 然後再重新登入。

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>收集感應器資料並傳送 tooyour IoT 中樞

在本節中，您可以在 Feather M0 WiFi 上部署和執行範例應用程式。 hello 範例應用程式可讓 hello 羽毛 M0 WiFi 上的 LED 閃爍。 然後會傳送 hello 溫度和溼度從收集的資料 hello BME280 感應器 tooyour IoT 中樞。

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>從 GitHub 取得 hello 範例應用程式，並準備 hello Arduino IDE

hello 範例應用程式被裝載於 GitHub 上。 複製 hello 範例儲存機制包含從 GitHub hello 範例應用程式。 tooclone hello 範例儲存機制，請遵循下列步驟：

1. 開啟命令提示字元或終端機視窗。

2. 請您想要儲存的 hello 範例應用程式 toobe tooa 資料夾。
3. 執行下列命令的 hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>安裝羽毛 M0 WiFi hello 套件 hello Arduino IDE 中

1. 開啟 hello hello 範例應用程式所在的資料夾。

2. Hello hello Arduino IDE 中的應用程式資料夾中開啟 hello app.ino 檔案。

   ![Arduino IDE 中開啟 hello 範例應用程式](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. 按一下**檔案** > **喜好設定**(Windows/Linux) 或**Arduino** > **喜好設定**(Mac)，並複製和貼上的 hello 連結底下 hello**其他面板管理員 Url**選項 hello Arduino IDE 喜好設定。
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. 按一下**工具** > **面板** > **面板管理員**，然後再安裝 hello`Arduino SAMD Boards`版本`1.6.2`或更新版本。 

1. 接著在 hello 相同的視窗，請安裝`Adafruit SAMD Boards`封裝 tooadd hello 面板檔案定義。

   ![hello esp8266 套件安裝](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. 按一下 [工具] > [電路板] > [Adafruit M0 WiFi]。

5. 安裝驅動程式 (僅限 Windows)。 當您插入羽毛 M0 WiFi 時，您可能需要 tooinstall 驅動程式。 按一下[hello hello 網頁上的下載連結](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe)toodownload hello 驅動程式安裝程式。 請遵循 hello 步驟 tooinstall hello 想驅動程式。

### <a name="install-necessary-libraries"></a>安裝必要的程式庫

1. 在 hello Arduino IDE 中，按一下 **草圖** > **包含程式庫** > **管理程式庫**。

2. 下列程式庫名稱一個 hello 搜尋。 為找到的每個程式庫，按一下 [安裝]：

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. 手動安裝 `Adafruit_WINC1500`。 跳過[此網站](https://github.com/adafruit/Adafruit_WINC1500)按一下**複製或下載** > **Download ZIP**。 接著在 Arduino IDE 中，前往 太**草圖** > **包含程式庫** > **新增程式庫.zip**新增 hello 的 zip 檔案。

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>使用 hello 範例應用程式，如果您不需要實際的 BME280 感應器

如果您不需要實際的 BME280 感應器，hello 範例應用程式可以模擬氣溫和溼度的資料。 tooset hello 範例應用程式 toouse 模擬資料，請遵循下列步驟：

1. 開啟 hello`config.h`檔案在 hello`app`資料夾。

2. 找出 hello 下列程式碼行並變更 hello 值`false`太`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![設定 hello 範例應用程式模擬 toouse 資料](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. 儲存 hello 檔`Control-s`。

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>部署 hello 範例應用程式 tooFeather M0 WiFi

1. 在 hello Arduino IDE 中，按一下 **工具** > **連接埠**，然後按一下羽毛 M0 WiFi hello 序列連接埠。

2. 按一下**草圖** > **上傳**toobuild 和部署 hello 範例應用程式 tooFeather M0 WiFi。

### <a name="enter-your-credentials"></a>輸入認證

Hello 上傳成功完成之後，請遵循這些步驟 tooenter 您的認證：

1. 在 hello Arduino IDE 中，按一下 **工具** > **序列監視器**。

2. 在 hello hello 序列監視器視窗的右下角，選取 **沒有行尾結束符號**hello hello 左邊的下拉式清單中。
3. 選取**115200 傳輸**hello hello 右邊的下拉式清單中。
4. Hello hello 上方的輸入方塊中輸入下列資訊，如果您的 hello，然後按一下問 tooprovide**傳送**:

   * Wi-Fi SSID
   * Wi-Fi 密碼
   * 裝置連接字串

> [!Note]
> hello 認證資訊會儲存在 hello 羽毛 M0 WiFi EEPROM。 如果您按一下 hello 羽毛 M0 WiFi 面板 hello 重設 按鈕，hello 範例應用程式會詢問您是否 tooerase hello 資訊。 輸入`Y`tooerase hello 資訊。 系統會詢問 tooprovide hello 資訊第二次。

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>確認已成功執行 hello 範例應用程式

如果您看見 hello 下列輸出從 hello 序列監視器視窗並 hello 羽毛 M0 WiFi hello 範例應用程式上的 LED 閃爍不停執行成功：

![Arduino IDE 中的最終輸出](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>後續步驟

您已成功連接羽毛 M0 WiFi tooyour IoT 中樞而傳送嗨擷取感應器資料 tooyour IoT 中樞。 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

