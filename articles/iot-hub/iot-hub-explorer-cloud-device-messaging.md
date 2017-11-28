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
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="8ae09-104">使用 iot 中樞總管 toosend 之間和接收訊息裝置與 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8ae09-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="8ae09-106">[iothub-explorer](https://github.com/azure/iothub-explorer) 有數個命令可讓您更輕鬆管理 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8ae09-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="8ae09-107">本教學課程著重於如何 toouse iot 中樞總管 toosend 之間裝置與 IoT 中樞和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="8ae09-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8ae09-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="8ae09-108">What you will learn</span></span>

<span data-ttu-id="8ae09-109">您了解如何 toouse iot 中樞總管 toomonitor 裝置到雲端訊息和 toosend 雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="8ae09-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="8ae09-110">裝置到雲端訊息可能會收集您的裝置，並接著會傳送 tooyour IoT 中樞的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="8ae09-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="8ae09-111">雲端到裝置訊息可能是您的 IoT 中樞傳送 tooyour 裝置 tooblink 連接的 tooyour 裝置 LED 的命令。</span><span class="sxs-lookup"><span data-stu-id="8ae09-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8ae09-112">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="8ae09-112">What you will do</span></span>

- <span data-ttu-id="8ae09-113">使用 iot 中樞總管 toomonitor 裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="8ae09-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="8ae09-114">使用 iot 中樞總管 toosend 雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="8ae09-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8ae09-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="8ae09-115">What you need</span></span>

- <span data-ttu-id="8ae09-116">教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="8ae09-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="8ae09-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ae09-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="8ae09-118">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8ae09-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="8ae09-119">用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8ae09-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="8ae09-120">iothub-explorer。</span><span class="sxs-lookup"><span data-stu-id="8ae09-120">iothub-explorer.</span></span> <span data-ttu-id="8ae09-121">([安裝 iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="8ae09-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="8ae09-122">監視裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="8ae09-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="8ae09-123">toomonitor 傳送之訊息會從您的裝置 tooyour IoT 中樞，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8ae09-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="8ae09-124">開啟主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="8ae09-124">Open a console window.</span></span>
1. <span data-ttu-id="8ae09-125">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ae09-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="8ae09-126">從 IoT 中樞取得 `<device-id>` 和 `<IoTHubConnectionString>`。</span><span class="sxs-lookup"><span data-stu-id="8ae09-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="8ae09-127">請確定您已完成 hello 上一個教學課程。</span><span class="sxs-lookup"><span data-stu-id="8ae09-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="8ae09-128">您可以嘗試 toouse 或者`iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"`如果您有`HostName`，`SharedAccessKeyName`和`SharedAccessKey`。</span><span class="sxs-lookup"><span data-stu-id="8ae09-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="8ae09-129">傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="8ae09-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="8ae09-130">toosend 訊息從 IoT 中樞 tooyour 裝置，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8ae09-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="8ae09-131">開啟主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="8ae09-131">Open a console window.</span></span>
1. <span data-ttu-id="8ae09-132">IoT 中樞上啟動工作階段，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ae09-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="8ae09-133">藉由執行下列命令的 hello 傳送訊息 tooyour 裝置：</span><span class="sxs-lookup"><span data-stu-id="8ae09-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="8ae09-134">hello 命令會閃爍，是連接的 tooyour 裝置，並將傳送 hello 訊息 tooyour 裝置 hello LED。</span><span class="sxs-lookup"><span data-stu-id="8ae09-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="8ae09-135">沒有 hello 裝置 toosend 需要個別的 ack 命令後 tooyour IoT 中樞收到 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="8ae09-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ae09-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ae09-136">Next steps</span></span>

<span data-ttu-id="8ae09-137">您已經學會如何 toomonitor 裝置到雲端訊息，並將您的 Azure IoT 中樞與 IoT 裝置之間的雲端到裝置訊息傳送。</span><span class="sxs-lookup"><span data-stu-id="8ae09-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
