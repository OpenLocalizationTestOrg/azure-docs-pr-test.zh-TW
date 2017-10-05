---
title: "透過 iothub-explorer 進行 Azure IoT 裝置管理 | Microsoft Docs"
description: "使用 iothub-explorer CLI 工具進行 Azure IoT 中樞裝置管理，採用直接方法和對應項所需的屬性管理選項。"
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
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="323ff-104">使用 iothub-explorer 進行 Azure IoT 中樞裝置管理</span><span class="sxs-lookup"><span data-stu-id="323ff-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="323ff-106">[iothub-explorer](https://github.com/azure/iothub-explorer) 是您在主機電腦上執行的 CLI 工具，用來管理您的 IoT 中樞登錄中的裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="323ff-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="323ff-107">它隨附的管理選項可供您用來執行各種工作。</span><span class="sxs-lookup"><span data-stu-id="323ff-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="323ff-108">管理選項</span><span class="sxs-lookup"><span data-stu-id="323ff-108">Management option</span></span>          | <span data-ttu-id="323ff-109">Task</span><span class="sxs-lookup"><span data-stu-id="323ff-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="323ff-110">直接方法</span><span class="sxs-lookup"><span data-stu-id="323ff-110">Direct methods</span></span>             | <span data-ttu-id="323ff-111">使裝置執行動作，例如啟動或停止傳送訊息，或是將裝置重新開機。</span><span class="sxs-lookup"><span data-stu-id="323ff-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="323ff-112">對應項的所需屬性</span><span class="sxs-lookup"><span data-stu-id="323ff-112">Twin desired properties</span></span>    | <span data-ttu-id="323ff-113">讓裝置進入特定狀態，例如將 LED 設定為綠色，或將遙測傳送間隔設定為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="323ff-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="323ff-114">對應項的報告屬性</span><span class="sxs-lookup"><span data-stu-id="323ff-114">Twin reported properties</span></span>   | <span data-ttu-id="323ff-115">取得裝置的報告狀態。</span><span class="sxs-lookup"><span data-stu-id="323ff-115">Get the reported state of a device.</span></span> <span data-ttu-id="323ff-116">例如，裝置會回報 LED 現在正閃爍不停。</span><span class="sxs-lookup"><span data-stu-id="323ff-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="323ff-117">對應項標記</span><span class="sxs-lookup"><span data-stu-id="323ff-117">Twin tags</span></span>                  | <span data-ttu-id="323ff-118">在雲端儲存裝置特定的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="323ff-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="323ff-119">例如，販賣機的部署位置。</span><span class="sxs-lookup"><span data-stu-id="323ff-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="323ff-120">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="323ff-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="323ff-121">將通知傳送至裝置。</span><span class="sxs-lookup"><span data-stu-id="323ff-121">Send notifications to a device.</span></span> <span data-ttu-id="323ff-122">例如，「今天很可能會下雨。</span><span class="sxs-lookup"><span data-stu-id="323ff-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="323ff-123">別忘了帶傘。」</span><span class="sxs-lookup"><span data-stu-id="323ff-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="323ff-124">裝置對應項查詢</span><span class="sxs-lookup"><span data-stu-id="323ff-124">Device twin queries</span></span>        | <span data-ttu-id="323ff-125">查詢所有裝置對應項以擷取具有任意條件的這些裝置，例如識別可供使用的裝置。</span><span class="sxs-lookup"><span data-stu-id="323ff-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="323ff-126">如需差異的詳細說明和使用這些選項的相關指引，請參閱[裝置對雲端通訊指引](iot-hub-devguide-d2c-guidance.md)和[雲端對裝置通訊指引](iot-hub-devguide-c2d-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="323ff-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="323ff-127">「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="323ff-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="323ff-128">IoT 中樞會為其連線的每個裝置保存裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="323ff-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="323ff-129">如需裝置對應項的詳細資訊，請參閱[開始使用裝置對應項](iot-hub-node-node-twin-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="323ff-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="323ff-130">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="323ff-130">What you learn</span></span>

<span data-ttu-id="323ff-131">您會學到在開發電腦上使用 iothub-explorer 搭配各種管理選項。</span><span class="sxs-lookup"><span data-stu-id="323ff-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="323ff-132">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="323ff-132">What you do</span></span>

<span data-ttu-id="323ff-133">執行 iothub-explorer 搭配各種管理選項。</span><span class="sxs-lookup"><span data-stu-id="323ff-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="323ff-134">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="323ff-134">What you need</span></span>

- <span data-ttu-id="323ff-135">完成涵蓋下列需求的[設定裝置](iot-hub-raspberry-pi-kit-node-get-started.md)教學課程︰</span><span class="sxs-lookup"><span data-stu-id="323ff-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="323ff-136">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="323ff-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="323ff-137">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="323ff-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="323ff-138">將訊息傳送到您 Azure IoT 中樞的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="323ff-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="323ff-139">請確定在本教學課程期間，您的裝置是和用戶端應用程式一起執行。</span><span class="sxs-lookup"><span data-stu-id="323ff-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="323ff-140">iothub-explorer，在開發電腦上[安裝 iothub-explorer](https://github.com/azure/iothub-explorer)。</span><span class="sxs-lookup"><span data-stu-id="323ff-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="323ff-141">連線至您的 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="323ff-141">Connect to your IoT hub</span></span>

<span data-ttu-id="323ff-142">執行下列命令來連線至 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="323ff-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="323ff-143">使用 iothub-explorer 搭配直接方法</span><span class="sxs-lookup"><span data-stu-id="323ff-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="323ff-144">透過執行下列命令，在裝置應用程式中叫用 `start` 方法，將訊息傳送至您的 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="323ff-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="323ff-145">透過執行下列命令，在裝置應用程式中叫用 `stop` 方法，停止將訊息傳送至您的 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="323ff-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="323ff-146">使用 iothub-explorer 搭配對應項所需的屬性</span><span class="sxs-lookup"><span data-stu-id="323ff-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="323ff-147">透過執行下列命令，設定需要的屬性間隔 = 3000：</span><span class="sxs-lookup"><span data-stu-id="323ff-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="323ff-148">此屬性可以由您的裝置讀取。</span><span class="sxs-lookup"><span data-stu-id="323ff-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="323ff-149">使用 iothub-explorer 搭配對應項的報告屬性</span><span class="sxs-lookup"><span data-stu-id="323ff-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="323ff-150">執行下列命令來取得裝置的報告屬性：</span><span class="sxs-lookup"><span data-stu-id="323ff-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="323ff-151">其中一個屬性是 $metadata.$lastUpdated，它會顯示此裝置上一次傳送或接收訊息的時間。</span><span class="sxs-lookup"><span data-stu-id="323ff-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="323ff-152">使用 iothub-explorer 搭配對應項標記</span><span class="sxs-lookup"><span data-stu-id="323ff-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="323ff-153">執行下列命令來顯示裝置的標記和屬性：</span><span class="sxs-lookup"><span data-stu-id="323ff-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="323ff-154">執行下列命令來將欄位 role = temperature&humidity 新增至裝置：</span><span class="sxs-lookup"><span data-stu-id="323ff-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="323ff-155">對雲端到裝置的訊息使用 iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="323ff-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="323ff-156">執行下列命令來將 "Hello World" 訊息傳送到裝置：</span><span class="sxs-lookup"><span data-stu-id="323ff-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="323ff-157">如需使用此命令的真實案例，請參閱[使用 iothub-explorer 在裝置與 IoT 中樞之間傳送及接收訊息](iot-hub-explorer-cloud-device-messaging.md)。</span><span class="sxs-lookup"><span data-stu-id="323ff-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="323ff-158">使用 iothub-explorer 搭配裝置對應項查詢</span><span class="sxs-lookup"><span data-stu-id="323ff-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="323ff-159">藉由執行下列命令，查詢具有標記 role = 'temperature&humidity' 的裝置：</span><span class="sxs-lookup"><span data-stu-id="323ff-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="323ff-160">藉由執行下列命令，查詢具有標記 role = 'temperature&humidity' 以外的所有裝置：</span><span class="sxs-lookup"><span data-stu-id="323ff-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="323ff-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="323ff-161">Next steps</span></span>

<span data-ttu-id="323ff-162">您已學到如何使用 iothub-explorer 搭配各種管理選項。</span><span class="sxs-lookup"><span data-stu-id="323ff-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
