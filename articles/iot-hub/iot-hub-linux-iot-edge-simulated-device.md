---
title: "使用 Azure IoT Edge 來模擬裝置 (Linux) | Microsoft Docs"
description: "如何在 Linux 上使用 Azure IoT Edge 來建立模擬裝置，以透過 IoT Edge 閘道將遙測資料傳送至 IoT 中樞。"
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
ms.openlocfilehash: 5349960373ae6815862c5f79a69dd6d5d9d624ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="72625-103">使用 Azure IoT Edge 搭配模擬裝置來傳送裝置到雲端訊息 (Linux)</span><span class="sxs-lookup"><span data-stu-id="72625-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="72625-104">如何執行範例</span><span class="sxs-lookup"><span data-stu-id="72625-104">How to run the sample</span></span>

<span data-ttu-id="72625-105">**build.sh** 指令碼會在 **iot-edge** 存放庫本機複本的 **build** 資料夾中產生其輸出。</span><span class="sxs-lookup"><span data-stu-id="72625-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="72625-106">此輸出包含本範例中使用的四個 IoT Edge 模組。</span><span class="sxs-lookup"><span data-stu-id="72625-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="72625-107">組建指令碼會放置：</span><span class="sxs-lookup"><span data-stu-id="72625-107">The build script places the:</span></span>

* <span data-ttu-id="72625-108">**liblogger.so** 於 **build/modules/logger** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="72625-108">**liblogger.so** in the **build/modules/logger** folder.</span></span>
* <span data-ttu-id="72625-109">**libiothub.so** 於 **build/modules/iothub** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="72625-109">**libiothub.so** in the **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="72625-110">**lib\_identity\_map.so** 於 **build/modules/identitymap** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="72625-110">**lib\_identity\_map.so** in the **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="72625-111">**libsimulated\_device.so** 於 **build/modules/simulated\_device** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="72625-111">**libsimulated\_device.so** in the **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="72625-112">使用這些路徑作為**模組路徑**值，如下列 JSON 設定檔所示：</span><span class="sxs-lookup"><span data-stu-id="72625-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="72625-113">simulated\_device\_cloud\_upload\_sample 程序會採用 JSON 組態檔的路徑作為命令列引數。</span><span class="sxs-lookup"><span data-stu-id="72625-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="72625-114">下列範例 JSON 檔會提供於 SDK 存放庫中，位置為：**samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="72625-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="72625-115">除非您修改 build 指令碼以將 IoT Edge 模組或範例可執行檔放置在非預設位置，否則此組態檔將保有原始功能。</span><span class="sxs-lookup"><span data-stu-id="72625-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="72625-116">模組路徑是您執行 simulated\_device\_cloud\_upload\_sample 可執行檔的相對路徑，不是可執行檔所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="72625-116">The module paths are relative to the directory from where you run the simulated\_device\_cloud\_upload\_sample executable, not the directory where the executable is located.</span></span> <span data-ttu-id="72625-117">範例 JSON 組態檔的預設值為在目前的工作目錄中寫入 'deviceCloudUploadGatewaylog.log'。</span><span class="sxs-lookup"><span data-stu-id="72625-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="72625-118">在文字編輯器中，開啟 **iot-edge** 存放庫之本機複本中的 **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="72625-118">In a text editor, open the file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="72625-119">這個檔案會設定閘道範例中的 IoT Edge 模組︰</span><span class="sxs-lookup"><span data-stu-id="72625-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="72625-120">**IoTHub** 模組會連接至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="72625-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="72625-121">您必須設定它，以將資料傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="72625-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="72625-122">特別是將 **IoTHubName** 值設定為 IoT 中樞的名稱，並將 **IoTHubSuffix** 值設定為 **azure-devices.net**。</span><span class="sxs-lookup"><span data-stu-id="72625-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="72625-123">將 **Transport** 值設定為 **HTTP**、**AMQP** 或 **MQTT** 其中一個。</span><span class="sxs-lookup"><span data-stu-id="72625-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="72625-124">目前只有 **HTTP** 會為所有裝置訊息共用一個 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="72625-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="72625-125">如果您將值設定為 **AMQP** 或 **MQTT**，閘道會為每個裝置維持一個連至 IoT 中樞的個別 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="72625-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="72625-126">**mapping** 模組會將您模擬裝置的 MAC 位址對應到您 IoT 中樞裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="72625-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="72625-127">請確定 **deviceId** 值符合您新增至 IoT 中樞之兩個裝置的識別碼，而且 **deviceKey** 值包含這兩個裝置的金鑰。</span><span class="sxs-lookup"><span data-stu-id="72625-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="72625-128">**BLE1** 和 **BLE2** 模組是模擬裝置。</span><span class="sxs-lookup"><span data-stu-id="72625-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="72625-129">請注意其 MAC 位址如何符合 **mapping** 模組中的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="72625-129">Note how their MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="72625-130">**Logger** 模組會將閘道活動記錄到檔案。</span><span class="sxs-lookup"><span data-stu-id="72625-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="72625-131">範例中顯示的 **module path** 值假設您要從 **iot-edge** 存放庫本機複本的 **build** 資料夾執行範例。</span><span class="sxs-lookup"><span data-stu-id="72625-131">The **module path** values shown in the example assume that you run the sample from the **build** folder in your local copy of the **iot-edge** repository.</span></span>
* <span data-ttu-id="72625-132">JSON 檔案底部的 **links** 陣列會將 **BLE1** 和 **BLE2** 模組連接至 **mapping** 模組，再將 **mapping** 模組連接至 **IoTHub** 模組。</span><span class="sxs-lookup"><span data-stu-id="72625-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="72625-133">它也可確保 **Logger** 模組會記錄所有訊息。</span><span class="sxs-lookup"><span data-stu-id="72625-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

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

<span data-ttu-id="72625-134">儲存您對組態檔進行的變更。</span><span class="sxs-lookup"><span data-stu-id="72625-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="72625-135">執行範例：</span><span class="sxs-lookup"><span data-stu-id="72625-135">To run the sample:</span></span>

1. <span data-ttu-id="72625-136">在您的殼層中，瀏覽至 **iot-edge/build** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="72625-136">In your shell, navigate to the **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="72625-137">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="72625-137">Run the following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="72625-138">您可以使用[裝置總管][lnk-device-explorer]或 [iothub-explorer][lnk-iothub-explorer] 工具，以監視 IoT 中樞從閘道接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="72625-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="72625-139">例如，您可以使用 iothub-explorer，然後使用以下命令監控裝置到雲端的訊息：</span><span class="sxs-lookup"><span data-stu-id="72625-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="72625-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72625-140">Next steps</span></span>

<span data-ttu-id="72625-141">如果要更進一步了解 Azure IoT Edge 並實驗一些程式碼範例，請瀏覽下列開發人員教學課程和資源：</span><span class="sxs-lookup"><span data-stu-id="72625-141">To gain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="72625-142">[使用 Azure IoT Edge 從實體裝置傳送裝置到雲端訊息][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="72625-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="72625-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="72625-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="72625-144">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="72625-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="72625-145">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="72625-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="72625-146">[徹底保護您的 IoT 解決方案][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="72625-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
