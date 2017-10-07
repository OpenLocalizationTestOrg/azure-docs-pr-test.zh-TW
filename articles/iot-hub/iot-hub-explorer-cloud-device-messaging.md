---
title: "aaaManage Azure IoT 中樞雲端裝置與 iot 中樞總管傳訊 |Microsoft 文件"
description: "了解如何 toouse hello iot 中樞總管 CLI 工具 toomonitor 裝置 toocloud (D2C) 訊息，以及雲端 toodevice (C2D) 中的訊息傳送 Azure IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 中樞總管 中，訊息、 雲端裝置 iot 中樞雲端 toodevice，雲端 toodevice 傳訊"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>使用 iot 中樞總管 toosend 之間和接收訊息裝置與 IoT 中樞

![端對端圖表](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub-explorer](https://github.com/azure/iothub-explorer) 有數個命令可讓您更輕鬆管理 IoT 中樞。 本教學課程著重於如何 toouse iot 中樞總管 toosend 之間裝置與 IoT 中樞和接收訊息。

## <a name="what-you-will-learn"></a>學習目標

您了解如何 toouse iot 中樞總管 toomonitor 裝置到雲端訊息和 toosend 雲端到裝置訊息。 裝置到雲端訊息可能會收集您的裝置，並接著會傳送 tooyour IoT 中樞的感應器資料。 雲端到裝置訊息可能是您的 IoT 中樞傳送 tooyour 裝置 tooblink 連接的 tooyour 裝置 LED 的命令。

## <a name="what-you-will-do"></a>將執行的作業

- 使用 iot 中樞總管 toomonitor 裝置到雲端訊息。
- 使用 iot 中樞總管 toosend 雲端到裝置訊息。

## <a name="what-you-need"></a>您需要什麼

- 教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：
  - 有效的 Azure 訂用帳戶。
  - 位於您訂用帳戶中的 Azure IoT 中樞。
  - 用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。
- iothub-explorer。 ([安裝 iothub-explorer](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>監視裝置到雲端的訊息

toomonitor 傳送之訊息會從您的裝置 tooyour IoT 中樞，請遵循下列步驟：

1. 開啟主控台視窗。
1. 執行下列命令的 hello:

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > 從 IoT 中樞取得 `<device-id>` 和 `<IoTHubConnectionString>`。 請確定您已完成 hello 上一個教學課程。 您可以嘗試 toouse 或者`iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"`如果您有`HostName`，`SharedAccessKeyName`和`SharedAccessKey`。

## <a name="send-cloud-to-device-messages"></a>傳送雲端到裝置訊息

toosend 訊息從 IoT 中樞 tooyour 裝置，請遵循下列步驟：

1. 開啟主控台視窗。
1. IoT 中樞上啟動工作階段，執行下列命令的 hello:

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. 藉由執行下列命令的 hello 傳送訊息 tooyour 裝置：

   ```bash
   iothub-explorer send <device-id> <message>
   ```

hello 命令會閃爍，是連接的 tooyour 裝置，並將傳送 hello 訊息 tooyour 裝置 hello LED。

> [!Note]
> 沒有 hello 裝置 toosend 需要個別的 ack 命令後 tooyour IoT 中樞收到 hello 訊息。

## <a name="next-steps"></a>後續步驟

您已經學會如何 toomonitor 裝置到雲端訊息，並將您的 Azure IoT 中樞與 IoT 裝置之間的雲端到裝置訊息傳送。

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
