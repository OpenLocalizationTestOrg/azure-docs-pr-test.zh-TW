---
title: "aaaRaspberry Pi toocloud (Node.js) 的連線覆盆子 Pi tooAzure IoT 中樞 |Microsoft 文件"
description: "連接覆盆子 Pi toosend 資料 toohello Azure 雲端的覆盆子 Pi tooAzure IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 木莓澆 pi 木莓澆 pi iot 中樞木莓澆 pi 傳送資料 toocloud 木莓澆 pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a>連接覆盆子 Pi tooAzure IoT 中樞 (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

在本教學課程中，您必須開始學習使用執行 Raspbian 覆盆子 Pi 的 hello 基本。 然後您學習如何 tooseamlessly 裝置 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。 如需 Windows 10 IoT 核心版範例，請移 toohello [Windows 開發人員中心](http://www.windowsondevices.com/)。

還沒有套件嗎？ 再試一次 hello[覆盆子 Pi 3 模擬器](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/)。 或在[這裡](https://azure.microsoft.com/develop/iot/starter-kits)購買新的套件。

## <a name="what-you-do"></a>您要做什麼

* 設定 Raspberry Pi。
* 建立 IoT 中樞。
* 在 IoT 中樞對於 Pi 註冊裝置。
* Pi toosend 感應器資料 tooyour IoT 中樞上執行範例應用程式。

連接您所建立的覆盆子 Pi tooan IoT 中樞。 然後您範例應用程式上執行 Pi toocollect 氣溫和溼度資料從 BME280 感應器。 最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。

## <a name="what-you-learn"></a>您學到什麼

* 如何 toocreate Azure IoT 中樞，並取得新的裝置連接字串。
* 如何 tooconnect Pi 與 BME280 感應器。
* 如何執行範例應用程式上 Pi toocollect 感應器資料。
* 如何 toosend 感應器資料 tooyour IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

![您需要什麼](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

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
   1. [下載與像素 Raspbian 潔](https://www.raspberrypi.org/downloads/raspbian/)（hello.zip 檔案）。
   1. 擷取 hello Raspbian 映像電腦上的 tooa 資料夾。
1. 安裝 Raspbian toohello microSD 卡。
   1. [下載並安裝 hello Etcher sd 記憶卡燒錄機公用程式](https://etcher.io/)。
   1. 執行 Etcher，並在步驟 1 中選取您要解壓縮的 hello Raspbian 映像。
   1. 選取 hello microSD 卡磁碟機。 請注意，Etcher 可能已經選取 hello 正確的磁碟機。
   1. 按一下快閃 tooinstall Raspbian toohello microSD 卡。
   1. 安裝完成時，請從電腦移除 hello microSD 卡。 因為它是安全的 tooremove hello microSD 卡直接 Etcher 自動退出，或取消掛接 hello microSD 卡在完成時。
   1. 插入 Pi hello microSD 卡。

### <a name="enable-ssh-and-i2c"></a>啟用 SSH 和 I2C

1. Pi toohello 監視器、 鍵盤和滑鼠連接、 啟動 Pi 後再登入 Raspbian 使用`pi`hello 使用者名稱和`raspberry`hello 密碼。
1. 按一下 hello 木莓澆圖示 >**喜好設定** > **覆盆子 Pi 組態**。

   ![hello Raspbian 偏好設定 功能表](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. 在 hello**介面**索引標籤上，設定**I2C**和**SSH**太**啟用**，然後按一下 **確定**。 如果沒有實體的感應器，然後想要模擬的 toouse 感應器資料，這個步驟是選擇性的。

   ![在 Raspberry Pi 上啟用 I2C 和 SSH](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH 和 I2C，您可以找到更多的參考文件上[raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/)和[Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c)。

### <a name="connect-hello-sensor-toopi"></a>連接 hello 感應器 tooPi

請使用 hello breadboard 和跳接器線路 tooconnect LED 和 BME280 tooPi，如下所示。 如果您沒有 hello 感應器，略過本節。

![hello 覆盆子 Pi 和感應器的連接](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

hello BME280 感應器可以收集溫度和溼度的資料。 如果沒有裝置和 hello 雲端之間的通訊，將會閃爍 hello LED。 

感應器 pin 碼，使用下列配線 hello:

| 啟動 (感應器和 LED)     | 結束 (電路版)            | 纜線顏色   |
| -----------------------  | ---------------------- | ------------: |
| VDD (針腳 5G)             | 3.3V PWR (針腳 1)       | 白色纜線   |
| GND (針腳 7G)             | GND (針腳 6)            | 棕色纜線   |
| SCK (針腳 8G)             | I2C1 SDA (針腳 3)       | 橘色纜線  |
| SDI (針腳 10G)            | I2C1 SCL (針腳 5)       | 紅色纜線     |
| LED VDD (針腳 18F)        | GPIO 24 (針腳 18)       | 白色纜線   |
| LED GND (針腳 17F)        | GND (針腳 20)           | 黑色纜線   |

按一下 tooview[覆盆子 Pi 2 & 3 Pin 對應](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi)供您參考。

您已成功連接 BME280 tooyour 覆盆子 Pi 之後，它應該類似影像下方。

![連接的 Pi 和 BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Pi toohello 網路連線

開啟 Pi 使用 hello 微 USB 纜線和 hello 電源供應器。 使用 hello 乙太網路纜線 tooconnect Pi tooyour 有線網路，或遵循 hello[指示從 hello 覆盆子 Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour 無線網路。 您 Pi 已成功連接的 toohello 網路之後，您需要 tootake hello 記下[您 Pi 的 IP 位址](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address)。

![連接的 toowired 網路](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> 請確定 Pi 為您的電腦相同網路的連線的 toohello。 例如，如果您的電腦是連線的 tooa 無線網路，Pi 是連接的 tooa 有線網路時，您可能不會看到 hello IP 位址 hello devdisco 輸出中的。

## <a name="run-a-sample-application-on-pi"></a>在 Pi 上執行範例應用程式

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a>複製範例應用程式並安裝 hello 必要條件套件

1. 使用其中一種您主機電腦 tooconnect tooyour 覆盆子 Pi 中的下列 SSH 用戶端 hello。
    - [PuTTY](http://www.putty.org/) 適用於 Windows。 您需要的 Pi tooconnect hello IP 位址透過 SSH 它。
    - hello 內建 SSH 用戶端上 Ubuntu 或 macOS。 您可能需要執行`ssh pi@<ip address of pi>`tooconnect 透過 SSH 的 Pi。

   > [!NOTE] 
   hello 預設使用者名稱是`pi`，hello 密碼為`raspberry`。

1. 安裝 Node.js 及 NPM tooyour Pi。
   
   首先，您應該以 hello 下列命令檢查 Node.js 版本。 
   
   ```bash
   node -v
   ```

   如果 hello 版本低於 4.x 或您 pi 沒有 Node.js，然後執行下列命令 tooinstall hello 或更新 Node.js。

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. 藉由執行下列命令的 hello 複製 hello 範例應用程式：

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Hello，下列命令安裝所有封裝。 其中包含 Azure IoT 裝置 SDK、BME280 感應器程式庫和接線 Pi 程式庫。

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   可能需要幾分鐘的時間 toofinish 這個安裝程序 denpening 上您的網路連線。

### <a name="configure-hello-sample-application"></a>Hello 範例應用程式設定

1. 執行下列命令的 hello 開啟 hello 設定檔：

   ```bash
   nano config.json
   ```

   ![組態檔](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   此檔案中有兩個項目可供您設定。 hello 第一次是`interval`，而後者可定義兩個訊息，傳送 toocloud hello 時間間隔。 hello 第二個`simulatedData`，這是 toouse 是否模擬感應器資料的布林值。

   如果您**沒有 hello 感應器**，將的 hello`simulatedData`值太`true`toomake hello 範例應用程式建立及使用模擬的感應器資料。

1. 按下 [Control-O] > 輸入 > [Control-X] 儲存並結束。

### <a name="run-hello-sample-application"></a>執行 hello 範例應用程式

1. 藉由執行下列命令的 hello 執行 hello 範例應用程式：

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   請確定您複製-貼上 hello 裝置連接字串到 hello 單引號。


您應該會看到 hello 下列輸出顯示 hello 傳送 tooyour IoT 中樞的感應器資料及 hello 訊息。

![輸出-從覆盆子 Pi tooyour IoT 中樞傳送的感應器資料](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>後續步驟

您已執行範例應用程式 toocollect 感應器資料，並將它傳送 tooyour IoT 中樞。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]