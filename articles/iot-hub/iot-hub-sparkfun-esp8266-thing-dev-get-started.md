---
title: "aaaESP8266 toocloud-連接 Sparkfun ESP8266 事 Dev tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並在本教學課程中連接它 Sparkfun ESP8266 動作開發人員 tooAzure IoT 中樞 toosend 資料 toohello Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>連接 Sparkfun ESP8266 動作開發人員 tooAzure hello 雲端中的 IoT 中樞

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22、Thing Dev 及 IoT 中樞之間的連接](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>將執行的作業

連接將會建立 Sparkfun ESP8266 動作開發人員 tooan IoT 中樞。 從 DHT22 感應器，然後 ESP8266 toocollect 氣溫和溼度資料上執行範例應用程式。 最後，傳送嗨感應器資料 tooyour IoT 中樞。

> [!NOTE]
> 如果您使用其他 ESP8266 面板，您仍然可以依照這些步驟 tooconnect 它 tooyour IoT 中樞。 根據您使用的 hello ESP8266 面板，您可能需要 tooreconfigure hello `LED_PIN`。 例如，如果您使用從 AI 思想家 ESP8266，您可能會變更從`0`太`2`。 還沒有套件嗎？請按一下[這裡](http://azure.com/iotstarterkits)

## <a name="what-you-will-learn"></a>學習目標

* 如何 toocreate IoT 中樞和動作供開發的註冊裝置
* 如何 tooconnect 動作開發人員與 hello 感應器和您的電腦。
* 如何執行範例應用程式上的動作供開發 toocollect 感應器資料
* 如何 toosend hello 感應器資料 tooyour IoT 中樞。

## <a name="what-you-will-need"></a>必要元件

![Hello 教學課程需要的組件](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete 這項作業，需要您的動作開發人員入門套件中的下列組件的 hello:

* hello Sparkfun ESP8266 動作開發人員面板。
* 微 USB tooType USB 纜線。

您也需要 hello 下列開發環境：

* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。
* 執行 Windows 或 Ubuntu 的 Mac 或 PC。
* Sparkfun ESP8266 動作開發人員 tooconnect 至無線網路。
* 網際網路連線 toodownload hello 組態工具。
* [Arduino IDE](https://www.arduino.cc/en/main/software)版本 1.6.8 （或更新版本），舊版將不適用於 hello AzureIoT 程式庫。

hello 下列項目是選擇性的以防沒有感應器。 您也可以使用模擬的感應器資料的 hello 選項。

* Adafruit DHT22 溫度和溼度感應器。
* 麵包板。
* M/M 跳線。

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>連接 ESP8266 動作開發人員與 hello 感應器和您的電腦

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>連接 DHT22 氣溫和溼度感應器 tooESP8266 動作開發人員

請使用 hello breadboard 和跳接器線路 toomake hello 的連接，如下所示。 如果您沒有感應器，請略過本節，因為您可以改為使用模擬的感應器資料。

![連接參考](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

感應器 pin 碼，我們將使用下列配線 hello:

| 開始 (感應器)           | 結束 (電路版)           | 纜線顏色   |
| -----------------------  | ---------------------- | ------------: |
| VDD (針腳 27F)            | 3V (針腳 8A)           | 紅色纜線     |
| DATA (針腳 28F)           | GPIO 2 (針腳 9A)       | 白色纜線    |
| GND (針腳 30F)            | GND (針腳 7J)          | 黑色纜線   |


- 如需詳細資訊，請參閱︰[DHT22 感應器安裝 (英文)](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) 和 [Sparkfun ESP8266 Thing Dev 規格 (英文)](https://www.sparkfun.com/products/13711)

現在，您的 Sparkfun ESP8266 Thing Dev 應該已經和作用中的感應器連接。

![連接 dht22 和 ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Sparkfun ESP8266 動作開發人員 tooyour 電腦連線

使用 hello 微 USB tooType USB 纜線 tooconnect Sparkfun ESP8266 動作開發人員 tooyour 的電腦，如下所示。

![羽毛 huzzah tooyour 電腦連線](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>新增序列埠權限 - 僅限 Ubuntu

如果您使用 Ubuntu，請確定一般使用者具有 hello 權限 toooperate 上 hello USB 連接埠的 Sparkfun ESP8266 動作供開發 tooadd 序列連接埠的權限的一般使用者，請遵循下列步驟：

1. 執行下列命令，在終端機的 hello:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   您取得其中一個 hello 下列輸出：

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   在 hello 輸出，請注意`uucp`或`dialout`也就是 hello 群組擁有者名稱的 hello USB 連接埠。

1. 藉由執行下列命令的 hello 加入 hello 使用者 toohello 群組：

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`hello 上一個步驟中為您取得 hello 群組擁有者名稱。 `<username>` 是 Ubuntu 使用者名稱。

1. 登出 Ubuntu 和 hello 變更 tootake 效果重新登入它。

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>收集感應器資料並傳送 tooyour IoT 中樞

在本節中，您可以在 Sparkfun ESP8266 Thing Dev 上部署和執行範例應用程式。 閃爍 hello LED Sparkfun ESP8266 動作開發人員在 hello 範例應用程式，並傳送 hello 溫度和溼度從收集的資料 hello DHT22 感應器 tooyour IoT 中樞。

### <a name="get-hello-sample-application-from-github"></a>從 GitHub 取得 hello 範例應用程式

hello 範例應用程式被裝載於 GitHub 上。 複製 hello 範例儲存機制包含從 GitHub hello 範例應用程式。 tooclone hello 範例儲存機制，請遵循下列步驟：

1. 開啟命令提示字元或終端機視窗。
1. 請您想要儲存的 hello 範例應用程式 toobe tooa 資料夾。
1. 執行下列命令的 hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

安裝適用於 Sparkfun ESP8266 動作開發人員在 Arduino IDE hello 封裝。

1. 開啟 hello hello 範例應用程式所在的資料夾。
1. Hello Arduino IDE 中的應用程式資料夾中開啟 hello app.ino 檔案。

   ![arduino ide 中開啟 hello 範例應用程式](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. 在 hello Arduino IDE 中，按一下 **檔案** > **喜好設定**。
1. 在 hello**喜好設定**對話方塊方塊中，按一下 下一步 toohello 的 hello 圖示**其他面板管理員 Url**文字方塊。
1. 在 hello 快顯視窗中，輸入下列 URL，hello，然後按一下**確定**。

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![點 tooa arduino ide 中的套件 url。](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. 在 hello**喜好設定**對話方塊中，按一下 **確定**。
1. 按一下 [工具] > [電路板] > [電路板管理員]，然後搜尋 esp8266。
   應該已安裝 ESP8266 2.2.0 版或更新版本。

   ![hello esp8266 套件安裝](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. 按一下 [工具] > [面板] > [Sparkfun ESP8266 Thing Dev]。

### <a name="install-necessary-libraries"></a>安裝必要的程式庫

1. 在 hello Arduino IDE 中，按一下 **草圖** > **包含程式庫** > **管理程式庫**。
1. 下列程式庫名稱一個 hello 搜尋。 針對每個您所尋找的 hello 程式庫中，按一下 **安裝**。
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>沒有真正的 DHT22 感應器嗎？

如果您不需要實際的 DHT22 感應器 hello 範例應用程式可以模擬氣溫和溼度的資料。 tooenable hello 範例應用程式 toouse 模擬資料，請遵循下列步驟：

1. 開啟 hello`config.h`檔案在 hello`app`資料夾。
1. 找出 hello 下列程式碼行並變更 hello 值`false`太`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![設定 hello 範例應用程式模擬 toouse 資料](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. 使用 `Control-s` 進行儲存。

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>部署 hello 範例應用程式 tooSparkfun ESP8266 動作開發人員

1. 在 hello Arduino IDE 中，按一下 **工具** > **連接埠**，然後按一下 hello 序列埠 Sparkfun ESP8266 動作供開發的
1. 按一下**草圖** > **上傳**toobuild 和部署 hello 範例應用程式 tooSparkfun ESP8266 動作供開發

> [!Note]
> 如果您使用 macOS 您可能無法看到下列訊息期間上傳的 hello。 `warning: espcomm_sync failed`,`error: espcomm_open failed`. 請開啟 ternimal 視窗，並完成下列動作 toosolve 此問題。
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>輸入認證

Hello 上傳成功完成之後，請依照 hello 步驟 tooenter 您的認證：

1. 在 hello Arduino IDE 中，按一下 **工具** > **序列監視器**。
1. 在 hello 序列監視器視窗中，請注意在右下角的 hello 下方 hello 兩個下拉式清單。
1. 選取**沒有行尾結束符號**hello 左邊的下拉式清單。
1. 選取**115200 傳輸**hello 右邊下拉式清單。
1. Hello 位於 hello hello 序列監視器 視窗的頂端輸入的方塊中輸入下列資訊，如果您要求 tooprovide hello 它們，然後按一下**傳送**。
   * Wi-Fi SSID
   * Wi-Fi 密碼
   * 裝置連接字串

> [!Note]
> hello 認證資訊會儲存在 hello EEPROM 的 Sparkfun ESP8266 動作供開發 如果您按一下 hello Sparkfun ESP8266 動作開發人員面板 hello 重設 按鈕，hello 範例應用程式會要求您如果要讓 tooerase hello 資訊。 輸入`Y`清除 toohave hello 資訊，而您必須再次 tooprovide hello 資訊。

### <a name="verify-hello-sample-application-is-running-successfully"></a>確認順利執行 hello 範例應用程式

如果您看到 hello 下列輸出 hello 序列監視器視窗中，而且 hello Sparkfun ESP8266 動作開發人員，hello 範例應用程式上的 LED 閃爍不停執行成功。

![arduino ide 中的最終輸出](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>後續步驟

您已成功連接 Sparkfun ESP8266 動作開發人員 tooyour IoT 中樞而傳送嗨擷取感應器資料 tooyour IoT 中樞。 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
