---
title: "aaaESP8266 toocloud-連接羽毛 HUZZAH ESP8266 tooAzure IoT 中樞 |Microsoft 文件"
description: "深入了解如何 toosetup 並在本教學課程中連接它 Adafruit 羽毛 HUZZAH ESP8266 tooAzure IoT 中樞 toosend 資料 toohello Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>連接 Adafruit 羽毛 HUZZAH ESP8266 tooAzure hello 雲端中的 IoT 中樞

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![DHT22、Feather HUZZAH ESP8266 與 IoT 中樞之間的連線](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>您要做什麼


連接您所建立的 Adafruit 羽毛 HUZZAH ESP8266 tooan IoT 中樞。 然後您範例應用程式上執行 ESP8266 toocollect hello 氣溫和溼度資料從 DHT22 感應器。 最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。

> [!NOTE]
> 如果您使用其他 ESP8266 面板，您仍然可以依照這些步驟 tooconnect 它 tooyour IoT 中樞。 根據您所使用的 hello ESP8266 面板，您可能需要 tooreconfigure hello `LED_PIN`。 例如，如果您使用從 AI 思想家 ESP8266，您可能會變更從`0`太`2`。 還沒有套件嗎？ 收到 hello [Azure 網站](http://azure.com/iotstarterkits)。




## <a name="what-you-learn"></a>您學到什麼

* 如何 toocreate IoT 中樞和羽毛 HUZZAH ESP8266 如註冊裝置
* 如何 tooconnect 羽毛 HUZZAH ESP8266 hello 感應器與您的電腦
* 如何執行範例應用程式上羽毛 HUZZAH ESP8266 toocollect 感應器資料
* 如何 toosend hello 感應器資料 tooyour IoT 中樞

## <a name="what-you-need"></a>您需要什麼

![Hello 教學課程需要的組件](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete 這項作業，您需要 hello 羽毛 HUZZAH ESP8266 入門套件中的下列部分：

* hello 羽毛 HUZZAH ESP8266 面板
* 微 USB tooType USB 纜線

您還需要下列項目，為您的開發環境的 hello:

* 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。
* 執行 Windows 或 Ubuntu 的 Mac 或 PC。
* 若要羽毛 HUZZAH ESP8266 tooconnect 的無線網路。
* 網際網路連線 toodownload hello 組態工具。
* [Arduino IDE](https://www.arduino.cc/en/main/software) 1.6.8 版或更新版本。 舊版未使用 hello AzureIoT 程式庫。

hello 下列項目是選擇性的以防沒有感應器。 您也可以使用模擬的感應器資料的 hello 選項。

* Adafruit DHT22 溫度和溼度感應器
* 麵包板
* M/M 跳線


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>聯繫羽毛 HUZZAH ESP8266 hello 感應器和您的電腦
在本節中，您可以連接 hello 感應器 tooyour 面板。 然後您插入以便進一步使用於您裝置的 tooyour 電腦。
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>連接 DHT22 氣溫和溼度感應器 tooFeather HUZZAH ESP8266

請使用 hello breadboard 和跳接器線路 toomake hello 的連接，如下所示。 如果您沒有感應器，請略過本節，因為您可以改為使用模擬的感應器資料。

![連接參考](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


感應器 pin 碼，使用下列配線 hello:


| 開始 (感應器)           | 結束 (電路版)           | 纜線顏色   |
| -----------------------  | ---------------------- | ------------: |
| VDD (針腳 31F)            | 3V (針腳 58H)           | 紅色纜線     |
| DATA (針腳 32F)           | GPIO 2 (針腳 46A)       | 藍色纜線    |
| GND (針腳 34F)            | GND (針腳 56I)          | 黑色纜線   |

如需詳細資訊，請參閱 [Adafruit DHT22 感應器安裝](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor)和 [Adafruit Feather HUZZAH Esp8266 接腳圖](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts)。



現在，Feather Huzzah ESP8266 應該已經和作用中的感應器連接。

![連接 DHT22 與 Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>羽毛 HUZZAH ESP8266 tooyour 電腦連線

如下所示，使用 hello 微 USB tooType USB 纜線 tooconnect 羽毛 HUZZAH ESP8266 tooyour 電腦。

![羽毛 Huzzah tooyour 電腦連線](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>新增序列埠權限 (僅限 Ubuntu)


如果您使用 Ubuntu，請確定您擁有 hello 權限 toooperate 上 hello USB 連接埠的羽毛 HUZZAH ESP8266。 tooadd 序列連接埠的權限，請遵循下列步驟：


1. 執行下列命令，在終端機的 hello:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   您取得其中一個 hello 下列輸出：

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   在 hello 輸出中，請注意，`uucp`或`dialout`hello USB 連接埠 hello 群組擁有者名稱。

1. 藉由執行下列命令的 hello 加入 hello 使用者 toohello 群組：

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`hello 上一個步驟中為您取得 hello 群組擁有者名稱。 `<username>` 是 Ubuntu 使用者名稱。

1. 登出 Ubuntu，然後再登入一次的 hello 變更 tooappear。

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>收集感應器資料並傳送 tooyour IoT 中樞

在本節中，您可以在 Feather HUZZAH ESP8266 上部署和執行範例應用程式。 hello 範例應用程式會閃爍 hello LED 上羽毛 HUZZAH ESP8266，並傳送 hello 溫度和溼度從收集的資料 hello DHT22 感應器 tooyour IoT 中樞。

### <a name="get-hello-sample-application-from-github"></a>從 GitHub 取得 hello 範例應用程式

hello 範例應用程式被裝載於 GitHub 上。 複製 hello 範例儲存機制包含從 GitHub hello 範例應用程式。 tooclone hello 範例儲存機制，請遵循下列步驟：

1. 開啟命令提示字元或終端機視窗。
1. 請您想要儲存的 hello 範例應用程式 toobe tooa 資料夾。
1. 執行下列命令的 hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

安裝在 hello Arduino IDE 羽毛 HUZZAH ESP8266 hello 封裝：

1. 開啟 hello hello 範例應用程式所在的資料夾。
1. Hello hello Arduino IDE 中的應用程式資料夾中開啟 hello app.ino 檔案。

   ![Arduino IDE 中開啟 hello 範例應用程式](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. 在 hello Arduino IDE 中，按一下 **檔案** > **喜好設定**。
1. 在 hello**喜好設定**對話方塊方塊中，按一下 下一步 toohello 的 hello 圖示**其他面板管理員 Url**方塊。
1. 在 hello 快顯視窗中，輸入下列 URL，hello，然後按一下**確定**。

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![點 tooa Arduino IDE 中的套件 url。](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. 在 hello**喜好設定**對話方塊中，按一下 **確定**。
1. 按一下 [工具] > [電路板] > [電路板管理員]，然後搜尋 esp8266。

   [電路板管理員] 指出已安裝的 ESP8266 版本為 2.2.0 版或更新版本。

   ![hello esp8266 套件安裝](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. 按一下 [工具] > [電路板] > [Adafruit HUZZAH ESP8266]。

### <a name="install-necessary-libraries"></a>安裝必要的程式庫

1. 在 hello Arduino IDE 中，按一下 **草圖** > **包含程式庫** > **管理程式庫**。
1. 下列程式庫名稱一個 hello 搜尋。 對於找到的每個程式庫，按一下 [安裝]。
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>沒有真正的 DHT22 感應器嗎？

如果您不需要實際的 DHT22 感應器 hello 範例應用程式可以模擬氣溫和溼度的資料。 tooset hello 範例應用程式 toouse 模擬資料，請遵循下列步驟：

1. 開啟 hello`config.h`檔案在 hello`app`資料夾。
1. 找出 hello 下列程式碼行並變更 hello 值`false`太`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![設定 hello 範例應用程式模擬 toouse 資料](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. 儲存 hello 檔`Control-s`。

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>部署 hello 範例應用程式 tooFeather HUZZAH ESP8266

1. 在 hello Arduino IDE 中，按一下 **工具** > **連接埠**，然後按一下羽毛 HUZZAH ESP8266 hello 序列連接埠。
1. 按一下**草圖** > **上傳**toobuild 和部署 hello 範例應用程式 tooFeather HUZZAH ESP8266。

### <a name="enter-your-credentials"></a>輸入認證

Hello 上傳成功完成之後，請遵循這些步驟 tooenter 您的認證：

1. 在 hello Arduino IDE 中，按一下 **工具** > **序列監視器**。
1. 在 hello 序列監視器視窗中，請注意在 hello 右下角中的 hello 兩個下拉式清單。
1. 選取**沒有行尾結束符號**hello 左邊的下拉式清單。
1. 選取**115200 傳輸**hello 右邊下拉式清單。
1. Hello 位於 hello hello 序列監視器 視窗的頂端輸入的方塊中輸入下列資訊，如果您要求 tooprovide hello 它們，然後按一下**傳送**。
   * Wi-Fi SSID
   * Wi-Fi 密碼
   * 裝置連接字串

> [!Note]
> hello 認證資訊會儲存在 hello 羽毛 HUZZAH ESP8266 EEPROM。 如果您按一下 hello 羽毛 HUZZAH ESP8266 面板 hello 重設 按鈕，hello 範例應用程式會詢問您是否 tooerase hello 資訊。 輸入`Y`toohave hello 資訊清除。 系統會詢問 tooprovide hello 資訊第二次。

### <a name="verify-hello-sample-application-is-running-successfully"></a>確認順利執行 hello 範例應用程式

如果您看到 hello 下列輸出 hello 序列監視器視窗中，而且 hello 羽毛 HUZZAH ESP8266 hello 範例應用程式上的 LED 閃爍不停執行成功。

![Arduino IDE 中的最終輸出](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>後續步驟

您已成功連接羽毛 HUZZAH ESP8266 tooyour IoT 中樞，而傳送嗨擷取感應器資料 tooyour IoT 中樞。 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

