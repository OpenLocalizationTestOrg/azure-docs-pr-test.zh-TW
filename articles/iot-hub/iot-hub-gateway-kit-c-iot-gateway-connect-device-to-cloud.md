---
title: "aaaUse IoT 閘道 tooconnect 裝置 tooAzure IoT 中樞 |Microsoft 文件"
description: "了解 toouse 為 IoT 閘道 tooconnect TI SensorTag Intel NUC 和傳送感應器資料 tooAzure IoT 中樞 hello 中的雲端。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 閘道連接裝置 toocloud"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>使用 IoT 閘道 tooconnect 事項 toohello 雲端 SensorTag tooAzure IoT 中樞

> [!NOTE]
> 開始本教學課程之前，請確定您已完成[將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)。 在[設定為 IoT 閘道 Intel NUC](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)，您設定 hello Intel NUC 裝置與 IoT 閘道。

## <a name="what-you-will-learn"></a>學習目標

您了解如何 toouse IoT 閘道 tooconnect 德州儀器 SensorTag (CC2650STK) tooAzure IoT 中樞。 hello IoT 閘道傳送溫度和溼度從收集的資料 hello SensorTag tooAzure IoT 中樞。

## <a name="what-you-will-do"></a>將執行的作業

- 建立 IoT 中樞。
- 在 hello SensorTag hello IoT 中樞註冊裝置。
- 啟用 hello hello IoT 閘道與 hello SensorTag 之間的連線。
- 執行 b 範例應用程式 toosend SensorTag 資料 tooyour IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

- 在[將 Intel NUC 設定為 IoT 閘道器](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)教學課程中，您已將 Intel NUC 設定為 IoT 閘道器。
- * 有效的 Azure 訂用帳戶。 如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。
- 在主機電腦上執行的 SSH 用戶端。 Windows 上建議使用 PuTTY。 Linux 和 macOS 已隨附 SSH 用戶端。
- hello IP 位址和 hello 使用者名稱和密碼 tooaccess hello hello SSH 用戶端的閘道。
- 網際網路連線。

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> 您將在這裡為 SensorTag 註冊這個新裝置

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>啟用 hello hello IoT 閘道與 hello SensorTag 之間的連線

在本節中，您可以執行下列工作的 hello:

- 取得藍芽連線 hello SensorTag hello MAC 位址。
- 起始從 hello IoT 閘道 toohello SensorTag 藍芽連線。

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>取得藍芽連線 hello SensorTag hello MAC 位址

1. Hello 主機電腦上，執行 hello SSH 用戶端，並連接 toohello IoT 閘道。
1. 解除封鎖藍芽，藉由執行下列命令的 hello:

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Hello IoT 閘道上啟動 hello 藍芽服務，並輸入 藍芽殼層 tooconfigure 藍芽執行 hello 下列命令：

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. 藉由執行 hello 藍芽控制站上的電源 hello 下列在 hello 藍芽介面的命令：

   ```bash
   power on
   ```

   ![hello 與 bluetoothctl hello IoT 閘道上的藍芽控制站上的電源](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. 啟動掃描附近的藍芽裝置執行下列命令的 hello:

   ```bash
   scan on
   ```

   ![使用 bluetoothctl 掃描附近的藍牙裝置](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. 按 hello 配對 hello SensorTag 按鈕。 hello 綠色 LED 上 hello SensorTag 閃爍。
1. 在 hello 藍芽介面，您應該會看到的 hello SensorTag 找到。 記下 hello hello SensorTag MAC 位址。 在此範例中，是 hello MAC 位址的 hello SensorTag `24:71:89:C0:7F:82`。
1. 執行下列命令的 hello 關閉 hello 掃描：

   ```bash
   scan off
   ```

   ![使用 bluetoothctl 停止掃描附近的藍牙裝置](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>起始從 hello IoT 閘道 toohello SensorTag 藍芽連線

1. 執行下列命令的 hello 連線 toohello SensorTag:

   ```bash
   connect <MAC address>
   ```

   ![連接 bluetoothctl toohello SensorTag](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Hello SensorTag 從中斷連線並執行下列命令的 hello 結束 hello 藍芽介面：

   ```bash
   disconnect
   exit
   ```

   ![中斷與 bluetoothctl hello SensorTag](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

您已成功啟用 hello hello SensorTag 與 hello IoT 閘道之間的連線。

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>執行 b 範例應用程式 toosend SensorTag 資料 tooyour IoT 中樞

hello 藍芽低能源 (B) 的範例應用程式會提供 Azure IoT 邊緣。 hello 範例應用程式會收集從 b 連接，並傳送嗨資料 tooyou IoT 中樞。 您需要 toorun hello 範例應用程式：

1. Hello 範例應用程式設定。
1. Hello IoT 閘道上執行 hello 範例應用程式。

### <a name="configure-hello-sample-application"></a>Hello 範例應用程式設定

1. 藉由執行下列命令的 hello 移 toohello hello 範例應用程式的資料夾：

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. 執行下列命令的 hello 開啟 hello 設定檔：

   ```bash
   vi ble_gateway.json
   ```

1. 在 hello 設定檔中，填入 hello 下列值：

   **IoTHubName**: hello IoT 中樞名稱。

   **IoTHubSuffix**： 取得 IoTHubSuffix 從 hello 主索引鍵的 hello 裝置連接字串，您記下下。 請確定您取得 hello 裝置連接字串 hello 主索引鍵，且不 hello IoT 中樞連接字串的主索引鍵。 hello 主索引鍵的 hello 裝置連接字串的格式的 hello `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`。

   **傳輸**: hello 預設值是`amqp`。 這個值會顯示 hello 通訊協定 transpotation 期間。 這可以是 `http`、`amqp` 或 `mqtt`。

   **macAddress**: hello hello SensorTag 您記下的 MAC 位址。

   **deviceID**： 您建立 IoT 中樞中的 hello 裝置識別碼。

   **deviceKey**: hello 裝置連接字串 hello 主索引鍵。

   ![完整的 hello 的 hello b 範例應用程式的組態檔](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. 按`ESC`和型別`:wq`toosave hello 檔案。

### <a name="run-hello-sample-application"></a>執行 hello 範例應用程式

1. 請確定 hello SensorTag 電源已開啟。
1. 執行下列命令的 hello:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>後續步驟

[搭配 Azure IoT Edge 使用 IoT 閘道進行感應器資料轉換](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
