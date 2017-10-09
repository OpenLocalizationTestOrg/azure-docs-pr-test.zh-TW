---
title: "aaaAzure IoT 裝置管理與 iot 中樞總管 |Microsoft 文件"
description: "使用 hello iot 中樞總管 CLI 工具對於 Azure IoT 中心裝置管理，並且包含 hello 直接的方法與 hello 兩個所需的內容管理選項。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot 裝置管理, azure iot 中樞裝置管理, 裝置管理 iot, iot 中樞裝置管理"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>使用 iothub-explorer 進行 Azure IoT 中樞裝置管理

![端對端圖表](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iot 中樞總管](https://github.com/azure/iothub-explorer)是 CLI 工具，您在主機電腦 toomanage 裝置身分識別執行您的 IoT 中樞登錄中。 它提供的管理選項，您可以使用 tooperform 各種工作。

| 管理選項          | Task                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| 直接方法             | 使裝置，例如啟動或停止傳送訊息，或重新啟動裝置 hello 做。                                        |
| 對應項的所需屬性    | 將裝置放入特定狀態，例如設定 LED toogreen 或設定 hello 遙測傳送間隔 too30 分鐘數。         |
| 對應項的報告屬性   | 取得 hello 報告裝置的狀態。 例如，hello 裝置報告 LED 閃爍不停現在 hello。                                    |
| 對應項標記                  | Hello 雲端中儲存裝置專屬的中繼資料。 例如，hello 販賣的部署位置。                         |
| 雲端到裝置的訊息   | 傳送通知 tooa 裝置。 比方說，「 是很有可能 toorain 今天。 別忘了 toobring 概括性。 」              |
| 裝置對應項查詢        | 查詢所有裝置雙 tooretrieve 具有任意的條件，例如識別 hello 裝置可供使用。 |

如需詳細 hello 差異的說明和使用這些選項的指引，請參閱[裝置到雲端通訊指引](iot-hub-devguide-d2c-guidance.md)和[雲端到裝置通訊指引](iot-hub-devguide-c2d-guidance.md)。

> [!NOTE]
> 「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。 IoT 中樞保存每個裝置連接 tooit 裝置兩個。 如需裝置對應項的詳細資訊，請參閱[開始使用裝置對應項](iot-hub-node-node-twin-getstarted.md)。

## <a name="what-you-learn"></a>您學到什麼

您會學到在開發電腦上使用 iothub-explorer 搭配各種管理選項。

## <a name="what-you-do"></a>您要做什麼

執行 iothub-explorer 搭配各種管理選項。

## <a name="what-you-need"></a>您需要什麼

- 教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：
  - 有效的 Azure 訂用帳戶。
  - 位於您訂用帳戶中的 Azure IoT 中樞。
  - 用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。
- 請確定您的裝置正在執行與本教學課程期間 hello 用戶端應用程式。
- iothub-explorer，在開發電腦上[安裝 iothub-explorer](https://github.com/azure/iothub-explorer)。

## <a name="connect-tooyour-iot-hub"></a>連接 tooyour IoT 中樞

執行下列命令的 hello 連線 tooyour IoT 中樞：

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>使用 iothub-explorer 搭配直接方法

叫用 hello `start` hello 裝置應用程式 toosend 訊息 tooyour IoT 中樞中執行下列命令的 hello 方法：

```bash
iothub-explorer device-method <your device Id> start
```

叫用 hello `stop` hello 裝置應用程式 toostop 傳送的方法藉由執行下列命令的 hello 訊息 tooyour IoT 中樞：

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>使用 iothub-explorer 搭配對應項所需的屬性

設定所需的屬性間隔 = 3000 藉由執行下列命令的 hello:

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

此屬性可以由您的裝置讀取。

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>使用 iothub-explorer 搭配對應項的報告屬性

取得 hello 報告的屬性，藉由執行 hello hello 裝置的下列命令：

```bash
iothub-explorer get-twin <your device id>
```

Hello 屬性的其中一個是 $metadata。 $lastUpdated 會顯示 hello 最後一次此裝置傳送或接收訊息。

## <a name="use-iothub-explorer-with-twins-tags"></a>使用 iothub-explorer 搭配對應項標記

藉由執行下列命令的 hello 顯示 hello 標記與 hello 裝置的內容：

```bash
iothub-explorer get-twin <your device id>
```

新增欄位角色執行下列命令的 hello = 溫度和溼度 toohello 裝置：

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>對雲端到裝置的訊息使用 iothub-explorer

將"Hello World"訊息 toohello 裝置傳送藉由執行下列命令的 hello:

```bash
iothub-explorer send <device-id> "Hello World"
```

請參閱[使用 iot 中樞總管 toosend 和接收訊息，您的裝置與 IoT 中樞之間](iot-hub-explorer-cloud-device-messaging.md)真實案例中使用此命令。

## <a name="use-iothub-explorer-with-device-twins-queries"></a>使用 iothub-explorer 搭配裝置對應項查詢

查詢與角色的標籤裝置 = '溫度和溼度'，藉由執行下列命令的 hello:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

查詢以外的角色有標記的所有裝置 = '溫度和溼度'，藉由執行下列命令的 hello:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>後續步驟

您所學到如何 toouse iot 中樞-總管 中有各種不同的管理選項。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
