---
title: "使用 iothub-explorer 管理 Azure IoT 中樞雲端裝置傳訊 |Microsoft 文件"
description: "了解如何在 Azure IoT 中樞，使用 iothub-explorer CLI 工具來監視裝置到雲端 (D2C) 的訊息，以及傳送雲端到裝置 (C2D) 的訊息。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iothub explorer, 雲端裝置傳訊, iot 中樞雲端到裝置, 雲端到裝置傳訊"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 30151b7bdc544bc36e959cc3528d37897198fc7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-iothub-explorer-to-send-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="7ab66-104">使用 iothub-explorer 在裝置與 IoT 中樞之間傳送及接收訊息</span><span class="sxs-lookup"><span data-stu-id="7ab66-104">Use iothub-explorer to send and receive messages between your device and IoT Hub</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="7ab66-106">[iothub-explorer](https://github.com/azure/iothub-explorer) 有數個命令可讓您更輕鬆管理 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7ab66-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="7ab66-107">本學課程著重於如何使用 iothub-explorer，在裝置與 IoT 中樞之間傳送及接收訊息。</span><span class="sxs-lookup"><span data-stu-id="7ab66-107">This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7ab66-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="7ab66-108">What you will learn</span></span>

<span data-ttu-id="7ab66-109">您將了解如何使用 iothub-explorer 來監視裝置到雲端的訊息，以及傳送雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ab66-109">You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages.</span></span> <span data-ttu-id="7ab66-110">裝置到雲端的訊息可能是您的裝置所收集，然後傳送到 IoT 中樞的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="7ab66-110">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span></span> <span data-ttu-id="7ab66-111">雲端到裝置的訊息可能是 IoT 中樞傳送到裝置以使連接到裝置的 LED 閃爍的命令。</span><span class="sxs-lookup"><span data-stu-id="7ab66-111">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7ab66-112">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="7ab66-112">What you will do</span></span>

- <span data-ttu-id="7ab66-113">使用 iothub-explorer 來監視裝置到雲端的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ab66-113">Use iothub-explorer to monitor device-to-cloud messages.</span></span>
- <span data-ttu-id="7ab66-114">使用 iothub-explorer 來傳送雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ab66-114">Use iothub-explorer to send cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7ab66-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="7ab66-115">What you need</span></span>

- <span data-ttu-id="7ab66-116">完成涵蓋下列需求的[設定裝置](iot-hub-raspberry-pi-kit-node-get-started.md)教學課程︰</span><span class="sxs-lookup"><span data-stu-id="7ab66-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="7ab66-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ab66-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="7ab66-118">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7ab66-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="7ab66-119">將訊息傳送到您 Azure IoT 中樞的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ab66-119">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="7ab66-120">iothub-explorer。</span><span class="sxs-lookup"><span data-stu-id="7ab66-120">iothub-explorer.</span></span> <span data-ttu-id="7ab66-121">([安裝 iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="7ab66-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="7ab66-122">監視裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="7ab66-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="7ab66-123">若要監視從您的裝置傳送到IoT 中樞的訊息，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ab66-123">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="7ab66-124">開啟主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="7ab66-124">Open a console window.</span></span>
1. <span data-ttu-id="7ab66-125">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="7ab66-125">Run the following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="7ab66-126">從 IoT 中樞取得 `<device-id>` 和 `<IoTHubConnectionString>`。</span><span class="sxs-lookup"><span data-stu-id="7ab66-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="7ab66-127">確定您已經完成上一個教學課程。</span><span class="sxs-lookup"><span data-stu-id="7ab66-127">Make sure you've finished the previous tutorial.</span></span> <span data-ttu-id="7ab66-128">或者，如果您有 `HostName`、`SharedAccessKeyName` 和 `SharedAccessKey`，您可以嘗試使用 `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"`。</span><span class="sxs-lookup"><span data-stu-id="7ab66-128">Or you can try to use `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="7ab66-129">傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="7ab66-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="7ab66-130">若要從您的 IoT 中樞將訊息傳送到裝置，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ab66-130">To send a message from your IoT hub to your device, follow these steps:</span></span>

1. <span data-ttu-id="7ab66-131">開啟主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="7ab66-131">Open a console window.</span></span>
1. <span data-ttu-id="7ab66-132">執行下列命令來啟動 IoT 中樞上的工作階段：</span><span class="sxs-lookup"><span data-stu-id="7ab66-132">Start a session on your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="7ab66-133">執行下列命令來將訊息傳送到您的裝置：</span><span class="sxs-lookup"><span data-stu-id="7ab66-133">Send a message to your device by running the following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="7ab66-134">此命令會使連接到您裝置的 LED 閃爍，並將訊息傳送到您的裝置。</span><span class="sxs-lookup"><span data-stu-id="7ab66-134">The command blinks the LED that is connected to your device and sends the message to your device.</span></span>

> [!Note]
> <span data-ttu-id="7ab66-135">收到訊息之後，裝置不需將個別認可命令傳回您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7ab66-135">There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ab66-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ab66-136">Next steps</span></span>

<span data-ttu-id="7ab66-137">您已了解如何監視裝置到雲端的訊息，以及在 IoT 裝置和 Azure IoT 中樞之間傳送雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ab66-137">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
