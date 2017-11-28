---
title: "aaaSimulate Azure IoT 邊緣 (Windows) 的裝置 |Microsoft 文件"
description: "Toouse Azure IoT 邊緣 Windows toocreate 模擬的裝置上的傳送方式透過 Azure IoT 邊緣閘道 tooan IoT 中樞的遙測。"
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="275e1-103">使用模擬的裝置 (Windows) 的 Azure IoT 邊緣 toosend 裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="275e1-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="275e1-104">如何 toorun hello 範例</span><span class="sxs-lookup"><span data-stu-id="275e1-104">How toorun hello sample</span></span>

<span data-ttu-id="275e1-105">hello **build.cmd**指令碼會產生其輸出中 hello**建置**hello 的本機複本中的資料夾**iot 邊緣**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="275e1-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="275e1-106">此輸出會包括 hello 這個範例中使用四個 IoT 邊緣模組。</span><span class="sxs-lookup"><span data-stu-id="275e1-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="275e1-107">hello 組建指令碼的位置:</span><span class="sxs-lookup"><span data-stu-id="275e1-107">hello build script places the:</span></span>

* <span data-ttu-id="275e1-108">**logger.dll**在 hello**建置\\模組\\記錄器\\偵錯**資料夾。</span><span class="sxs-lookup"><span data-stu-id="275e1-108">**logger.dll** in hello **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="275e1-109">**iothub.dll**在 hello**建置\\模組\\iot 中樞\\偵錯**資料夾。</span><span class="sxs-lookup"><span data-stu-id="275e1-109">**iothub.dll** in hello **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="275e1-110">**識別\_map.dll**在 hello**建置\\模組\\identitymap\\偵錯**資料夾。</span><span class="sxs-lookup"><span data-stu-id="275e1-110">**identity\_map.dll** in hello **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="275e1-111">**模擬\_device.dll**在 hello**建置\\模組\\模擬\_裝置\\偵錯**資料夾。</span><span class="sxs-lookup"><span data-stu-id="275e1-111">**simulated\_device.dll** in hello **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="275e1-112">使用這些路徑 hello**模組路徑**值 hello 下列 JSON 設定檔中所示：</span><span class="sxs-lookup"><span data-stu-id="275e1-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="275e1-113">模擬的 hello\_裝置\_雲端\_上傳\_範例程序需要 hello 路徑 tooa JSON 組態檔做為命令列引數。</span><span class="sxs-lookup"><span data-stu-id="275e1-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="275e1-114">hello 下列的範例 JSON 檔案中提供 hello SDK 儲存機制**範例\\模擬\_裝置\_雲端\_上傳\_範例\\src\\模擬\_裝置\_雲端\_上傳\_範例\_win.json**。</span><span class="sxs-lookup"><span data-stu-id="275e1-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="275e1-115">此設定檔運作，除非您修改 hello 模組建置指令碼 tooplace hello IoT 邊緣或範例在非預設位置中的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="275e1-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="275e1-116">hello 模組路徑的相對 toohello 目錄 hello 其中模擬\_裝置\_雲端\_上傳\_sample.exe 所在。</span><span class="sxs-lookup"><span data-stu-id="275e1-116">hello module paths are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="275e1-117">hello 範例 JSON 組態檔的預設 toowriting too'deviceCloudUploadGatewaylog.log' 目前的工作目錄中。</span><span class="sxs-lookup"><span data-stu-id="275e1-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="275e1-118">在文字編輯器中，開啟 hello 檔案**範例\\模擬\_裝置\_雲端\_上傳\_範例\\src\\模擬\_裝置\_雲端\_上傳\_win.json** hello 的本機複本中**iot 邊緣**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="275e1-118">In a text editor, open hello file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="275e1-119">這個檔案設定 hello IoT 邊緣模組在以閘道 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="275e1-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="275e1-120">hello **iot 中樞**模組會連線 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="275e1-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="275e1-121">您設定 toosend 資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="275e1-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="275e1-122">具體來說，設定 hello **IoTHubName**值 toohello IoT 中樞名稱，並設定 hello **IoTHubSuffix**值太**azure devices.net**。</span><span class="sxs-lookup"><span data-stu-id="275e1-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="275e1-123">設定 hello**傳輸**的值 tooone: **HTTP**， **AMQP**，或**MQTT**。</span><span class="sxs-lookup"><span data-stu-id="275e1-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="275e1-124">目前只有 **HTTP** 會為所有裝置訊息共用一個 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="275e1-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="275e1-125">如果設定太 hello 值**AMQP**，或**MQTT**，hello 閘道會維護個別 TCP 連線 tooIoT 中樞的每個裝置。</span><span class="sxs-lookup"><span data-stu-id="275e1-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="275e1-126">hello**對應**模組將模擬的裝置 tooyour IoT 中樞裝置識別碼的 hello MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="275e1-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="275e1-127">請確定**deviceId**值符合 hello 識別碼 hello 兩個裝置，您加入 tooyour IoT 中樞，與該 hello **deviceKey**值包含兩個裝置 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="275e1-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="275e1-128">hello **BLE1**和**BLE2**模組是 hello 模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="275e1-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="275e1-129">請注意如何 hello 模組 MAC 位址會符合 hello 中的 hello 位址**對應**模組。</span><span class="sxs-lookup"><span data-stu-id="275e1-129">Note how hello module MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="275e1-130">hello**記錄器**模組會記錄您的閘道活動 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="275e1-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="275e1-131">hello**模組路徑**值 hello 下列範例所示為 hello 模擬位置的相對 toohello 目錄\_裝置\_雲端\_上傳\_sample.exe 所在。</span><span class="sxs-lookup"><span data-stu-id="275e1-131">hello **module path** values shown in hello following example are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="275e1-132">hello**連結**底部 hello hello JSON 檔案的陣列會連接 hello **BLE1**和**BLE2**模組 toohello**對應**模組和 hello**對應**模組 toohello **iot 中樞**模組。</span><span class="sxs-lookup"><span data-stu-id="275e1-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="275e1-133">它也可確保所有訊息也會都記錄 hello**記錄器**模組。</span><span class="sxs-lookup"><span data-stu-id="275e1-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
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
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
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
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
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
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
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
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

<span data-ttu-id="275e1-134">儲存 hello 做的變更，您會進行 toohello 組態檔。</span><span class="sxs-lookup"><span data-stu-id="275e1-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="275e1-135">toorun hello 範例：</span><span class="sxs-lookup"><span data-stu-id="275e1-135">toorun hello sample:</span></span>

1. <span data-ttu-id="275e1-136">在命令提示字元中，瀏覽 toohello**建置**hello 的本機複本中的資料夾**iot 邊緣**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="275e1-136">At a command prompt, navigate toohello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
2. <span data-ttu-id="275e1-137">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="275e1-137">Run hello following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="275e1-138">您可以使用 hello[裝置總管][ lnk-device-explorer]或[iot 中樞總管][ lnk-iothub-explorer]工具 IoT 中樞收到 hello 的 toomonitor hello 訊息閘道。</span><span class="sxs-lookup"><span data-stu-id="275e1-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="275e1-139">例如，使用 iot 中樞總管您就可以監視裝置到雲端訊息使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="275e1-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="275e1-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="275e1-140">Next steps</span></span>

<span data-ttu-id="275e1-141">toogain IoT 邊緣和實驗能進一步了解一些程式碼範例，請瀏覽 hello 下列開發人員教學課程和資源：</span><span class="sxs-lookup"><span data-stu-id="275e1-141">toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="275e1-142">[使用 IoT Edge 從實體裝置傳送裝置到雲端訊息][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="275e1-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="275e1-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="275e1-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="275e1-144">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="275e1-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="275e1-145">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="275e1-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="275e1-146">[保護您的 IoT 解決方案從接地 hello][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="275e1-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md