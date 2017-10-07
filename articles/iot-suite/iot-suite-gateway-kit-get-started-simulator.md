---
title: "aaaConnect 閘道 tooAzure IoT 套件使用 Intel NUC |Microsoft 文件"
description: "使用 hello Microsoft IoT 商業閘道套件和 hello 遠端監視預先設定的解決方案。 使用 hello Azure IoT 邊緣閘道 tooconnect toohello 遠端監視解決方案，傳送模擬的遙測 toohello 雲端，並回應 toomethods 叫用從 hello 方案儀表板。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>連接您 Azure IoT 邊緣閘道 toohello 遠端監視預先設定的解決方案並傳送模擬的遙測

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

本教學課程會示範如何在 toouse Azure IoT 邊緣 toosimulate 溫度和溼度資料 toosend toohello 遠端監視預先設定的解決方案。 hello 教學課程使用：

- Azure IoT 邊緣 tooimplement 閘道範例。
- hello IoT 套件遠端監視預先設定的解決方案做為 hello 以雲端為基礎的後端。

## <a name="overview"></a>概觀

在本教學課程中，您完成下列步驟的 hello:

- 部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。 這個步驟會自動部署並設定多個 Azure 服務。
- 設定電腦與 hello 遠端監視解決方案程式 Intel NUC 閘道裝置 toocommunicate。
- 設定的 hello IoT 邊緣閘道 toosend 模擬 hello 方案儀表板，您可以檢視的遙測。

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> hello 遠端監視解決方案會佈建一組您 Azure 訂用帳戶中的 Azure 服務。 hello 部署會反映實際的企業架構。 當您完成與其 tooavoid 不必要的 Azure 使用費用，會刪除 hello 預先設定的解決方案，在 azureiotsuite.com 您執行個體。 如果您需要再次 hello 預先設定的方案，您可以輕鬆地重新建立。 減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

第二台裝置，例如使用裝置識別碼重複上一個步驟 tooadd hello **device02**。 hello 範例會將資料從兩個模擬裝置傳送 hello 閘道 toohello 遠端監視解決方案中。

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>建置自訂 IoT 邊緣模組 hello

您現在可以建置 hello 自訂 IoT 邊緣模組，可讓 hello 閘道 toosend 訊息 toohello 遠端監視解決方案。 如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。

從使用下列命令的 hello GitHub 下載 hello 自訂 IoT 邊緣模組 hello 原始程式碼：

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

建置 hello 使用下列命令的 hello 自訂 IoT 邊緣模組：

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

hello 組建指令碼會置於 hello 組建資料夾中的 hello libsimulator.so 自訂 IoT 邊緣模組。

## <a name="configure-and-run-hello-iot-edge-gateway"></a>設定及執行 hello IoT 邊緣閘道

您現在可以設定 hello IoT 邊緣閘道 toosend 模擬的遙測 tooyour 遠端監視儀表板。 如需如何設定閘道和 IoT Edge 模組的詳細資訊，請參閱 [Azure IoT Edge 概念][lnk-gateway-concepts]。

> [!TIP]
> 在此教學課程中，您可以使用 hello 標準`vi`hello Intel NUC 上的文字編輯器。 如果您不使用`vi`之前，您應該先完成簡介教學課程中，例如[Unix hello vi 編輯器教學課程][ lnk-vi-tutorial] toofamiliarize 自己與這個編輯器。 或者，您可以安裝 hello 更加易懂易記[nano](https://www.nano-editor.org/)編輯器使用 hello 命令`smart install nano -y`。

開啟 hello 範例組態檔中 hello **vi**編輯器使用下列命令的 hello:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

找出下列行 hello hello iot 中樞模組的組態中的 hello:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

取代值以 hello IoT 中樞資訊您建立並儲存在 hello 開始本教學課程的 hello 預留位置。 IoTHubName hello 值看起來像**yourrmsolution37e08**，IoTSuffix hello 值通常是**azure devices.net**。

找出下列行 hello hello 對應模組的組態中的 hello:

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

取代 hello **deviceID**和**deviceKey**預留位置取代 hello 識別碼與您先前建立 hello 遠端監視解決方案中的 hello 兩個裝置的金鑰。

儲存您的變更。

您現在可以執行的 hello IoT 邊緣閘道使用 hello 下列命令：

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

hello 閘道上 hello Intel NUC 開始，並傳送遙測模擬的 toohello 遠端監視解決方案：

![IoT Edge 閘道會產生模擬的遙測資料][img-simulated telemetry]

按**CTRL-C** tooexit hello 程式在任何時間。

## <a name="view-hello-telemetry"></a>檢視 hello 遙測

hello IoT 邊緣閘道現在正在模擬的遙測 toohello 遠端監視解決方案。 您可以檢視 hello 遙測 hello 方案儀表板上。

- 瀏覽 toohello 方案儀表板。
- 選取您設定在 hello hello 閘道中的 hello 兩個裝置的其中一個**裝置 tooView**下拉式清單。
- 從 hello 閘道裝置 hello 遙測會顯示 hello 儀表板上。

![顯示從 hello 模擬的閘道裝置遙測][img-telemetry-display]

> [!WARNING]
> 如果您離開 hello 遠端監視您的 Azure 帳戶中執行的解決方案，您所要支付 hello 次執行。 減少 hello 遠端監視方案執行時的耗用量的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案基於示範目的][lnk-demo-config]。 使用完畢時，請從您的 Azure 帳戶刪除 hello 預先設定的解決方案。

## <a name="next-steps"></a>後續步驟

請瀏覽 hello [Azure IoT 開發人員中心](https://azure.microsoft.com/develop/iot/)取得更多範例和 Azure IoT 文件。

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started