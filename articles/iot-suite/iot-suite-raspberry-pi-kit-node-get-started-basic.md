---
title: "aaaConnect 覆盆子 Pi tooAzure IoT 套件 Node.js 使用真實的感應器 |Microsoft 文件"
description: "使用 hello 覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件 hello 和 Azure IoT 套件。 使用 Node.js tooconnect 遠端監視解決方案程式覆盆子 Pi toohello、 感應器從 toohello 雲端傳送遙測和回應 toomethods hello 方案儀表板從叫用。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a>連接遠端監視解決方案程式覆盆子 Pi 3 toohello 並從實際的感應器會使用 Node.js 傳送遙測

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

本教學課程會示範如何 toouse hello Microsoft Azure IoT 入門套件覆盆子 Pi 3 toodevelop 氣溫和溼度的讀取器可與 hello 雲端通訊。 hello 教學課程使用：

- Raspbian OS hello Node.js 程式設計語言，以及 Microsoft Azure IoT SDK hello Node.js tooimplement 範例裝置。
- hello IoT 套件遠端監視預先設定的解決方案做為 hello 以雲端為基礎的後端。

## <a name="overview"></a>概觀

在本教學課程中，您完成下列步驟的 hello:

- 部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。 這個步驟會自動部署並設定多個 Azure 服務。
- 設定您的電腦與 hello 與您的裝置與感應器 toocommunicate 遠端監視解決方案。
- 更新 hello 範例裝置的程式碼 tooconnect toohello 遠端監視解決方案，並傳送嗨方案儀表板，您可以檢視的遙測。

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> hello 遠端監視解決方案會佈建一組您 Azure 訂用帳戶中的 Azure 服務。 hello 部署會反映實際的企業架構。 當您完成與其 tooavoid 不必要的 Azure 使用費用，會刪除 hello 預先設定的解決方案，在 azureiotsuite.com 您執行個體。 如果您需要再次 hello 預先設定的方案，您可以輕鬆地重新建立。 減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>下載及設定 hello 範例

現在，您可以下載並設定覆盆子 pi hello 遠端監視用戶端應用程式。

### <a name="install-nodejs"></a>安裝 Node.js

在 Raspberry Pi 上安裝 Node.js。 hello IoT SDK for Node.js 需要 0.11.5 Node.js 或更新版本。 hello 下列步驟將示範如何覆盆子 pi tooinstall Node.js v6.10.2:

1. 使用下列命令 tooupdate hello 覆盆子 Pi:

    ```sh
    sudo apt-get update
    ```

1. 使用下列命令 toodownload hello Node.js 二進位檔 tooyour 覆盆子 Pi hello:

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. 使用下列命令 tooinstall hello 二進位檔的 hello:

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. 使用下列命令 tooverify 您已成功安裝 Node.js v6.10.2 hello:

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>複製 hello 儲存機制

如果您尚未這樣做，請複製 hello 所需執行的儲存機制 hello 您 pi 下列命令：

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a>更新 hello 裝置連接字串

開啟 hello 範例原始程式檔中 hello **nano**編輯器使用下列命令的 hello:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

找出 hello 一行：

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Hello 預留位置值取代 hello 裝置和您建立並儲存在本教學課程中的 hello 開頭的 IoT 中樞資訊。 儲存您的變更 (**Ctrl-O**， **Enter**) 和結束 hello 編輯器 (**Ctrl X**)。

## <a name="run-hello-sample"></a>執行 hello 範例

Hello 執行的下列命令 tooinstall hello 必要條件套件 hello 範例：

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

您現在可以在 hello 覆盆子 Pi 執行 hello 範例程式。 輸入 hello 命令：

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

hello 下列範例輸出是您 hello 覆盆子 Pi hello 命令提示字元下，請參閱 hello 輸出的範例：

![Raspberry Pi 應用程式的輸出][img-raspberry-output]

按**CTRL-C** tooexit hello 程式在任何時間。

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>後續步驟

請瀏覽 hello [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)取得更多範例和 Azure IoT 文件。

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
