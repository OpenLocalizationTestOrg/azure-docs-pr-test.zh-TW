---
title: "aaaSimulate Azure IoT 邊緣 (Linux) 的裝置 |Microsoft 文件"
description: "如何在 Linux toocreate 模擬的裝置上的 Azure IoT 邊緣 toouse 傳送遙測透過 IoT 邊緣閘道 tooan IoT 中樞。"
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a>使用模擬的裝置 (Linux) 的 Azure IoT 邊緣 toosend 裝置到雲端訊息

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>如何 toorun hello 範例

hello **build.sh**指令碼會產生其輸出中 hello**建置**hello 的本機複本中的資料夾**iot 邊緣**儲存機制。 此輸出會包括 hello 這個範例中使用四個 IoT 邊緣模組。

hello 組建指令碼的位置:

* **liblogger.so**在 hello**組建/模組/記錄器**資料夾。
* **libiothub.so**在 hello **iot 中樞組建/模組**資料夾。
* **lib\_識別\_map.so**在 hello**組建/模組/identitymap**資料夾。
* **libsimulated\_device.so**在 hello**組建/模組/模擬\_裝置**資料夾。

使用這些路徑 hello**模組路徑**值 hello 下列 JSON 設定檔中所示：

模擬的 hello\_裝置\_雲端\_上傳\_範例程序需要 hello 路徑 tooa JSON 組態檔做為命令列引數。 hello 下列的範例 JSON 檔案中提供 hello SDK 儲存機制**範例\\模擬\_裝置\_雲端\_上傳\_範例\\src\\模擬\_裝置\_雲端\_上傳\_範例\_lin.json**。 此設定檔運作，除非您修改 hello 模組建置指令碼 tooplace hello IoT 邊緣或範例在非預設位置中的可執行檔。

> [!NOTE]
> hello 模組的路徑是相對 toohello 目錄從您用來執行模擬 hello\_裝置\_雲端\_上傳\_範例可執行檔，不會 hello hello 可執行檔所在的目錄。 hello 範例 JSON 組態檔的預設 toowriting too'deviceCloudUploadGatewaylog.log' 目前的工作目錄中。

在文字編輯器中，開啟 hello 檔案**模擬範例/\_裝置\_雲端\_上傳\_範例/src/模擬\_裝置\_雲端\_上載\_lin.json** hello 的本機複本中**iot 邊緣**儲存機制。 這個檔案設定 hello IoT 邊緣模組在以閘道 hello 範例：

* hello **iot 中樞**模組會連線 tooyour IoT 中樞。 您設定 toosend 資料 tooyour IoT 中樞。 具體來說，設定 hello **IoTHubName**值 toohello IoT 中樞名稱，並設定 hello **IoTHubSuffix**值太**azure devices.net**。 設定 hello**傳輸**的值 tooone: **HTTP**， **AMQP**，或**MQTT**。 目前只有 **HTTP** 會為所有裝置訊息共用一個 TCP 連線。 如果設定太 hello 值**AMQP**，或**MQTT**，hello 閘道會維護個別 TCP 連線 tooIoT 中樞的每個裝置。
* hello**對應**模組將模擬的裝置 tooyour IoT 中樞裝置識別碼的 hello MAC 位址。 請確定**deviceId**值符合 hello 識別碼 hello 兩個裝置，您加入 tooyour IoT 中樞，與該 hello **deviceKey**值包含兩個裝置 hello 索引鍵。
* hello **BLE1**和**BLE2**模組是 hello 模擬的裝置。 請注意其 MAC 位址比對的方式 hello 中 hello 位址**對應**模組。
* hello**記錄器**模組會記錄您的閘道活動 tooa 檔案。
* hello**模組路徑**hello 範例所示的值會假設您是從 hello 執行 hello 範例**建置**hello 的本機複本中的資料夾**iot 邊緣**儲存機制。
* hello**連結**底部 hello hello JSON 檔案的陣列會連接 hello **BLE1**和**BLE2**模組 toohello**對應**模組和 hello**對應**模組 toohello **iot 中樞**模組。 它也可確保所有訊息也會都記錄 hello**記錄器**模組。

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
            }
            },
            "args": {
              "IoTHubName": "<<insert here IoTHubName>>",
              "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
              "Transport": "HTTP"
            }
          },
        {
            "name": "mapping",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/identitymap/libidentity_map.so"
            }
            },
            "args": [
              {
                "macAddress": "01:01:01:01:01:01",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              },
              {
                "macAddress": "02:02:02:02:02:02",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              }
            ]
          },
        {
            "name": "BLE1",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "01:01:01:01:01:01"
            }
          },
        {
            "name": "BLE2",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "02:02:02:02:02:02"
            }
          },
        {
            "name": "Logger",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

儲存 hello 做的變更，您會進行 toohello 組態檔。

toorun hello 範例：

1. 在您的殼層，瀏覽 toohello **iot 邊緣/組建**資料夾。
2. 執行下列命令的 hello:
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. 您可以使用 hello[裝置總管][ lnk-device-explorer]或[iot 中樞總管][ lnk-iothub-explorer]工具 IoT 中樞收到 hello 的 toomonitor hello 訊息閘道。 例如，使用 iot 中樞總管您就可以監視裝置到雲端訊息使用 hello 下列命令：

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>後續步驟

toogain 進一步了解 Azure IoT 邊緣和實驗透過一些程式碼範例，請瀏覽 hello 下列開發人員教學課程和資源：

* [使用 Azure IoT Edge 從實體裝置傳送裝置到雲端訊息][lnk-physical-device]
* [Azure IoT Edge][lnk-iot-edge]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [IoT 中樞開發人員指南][lnk-devguide]
* [保護您的 IoT 解決方案從接地 hello][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
