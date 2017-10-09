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
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="6f4eb-104">使用 iothub-explorer 進行 Azure IoT 中樞裝置管理</span><span class="sxs-lookup"><span data-stu-id="6f4eb-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![端對端圖表](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6f4eb-106">[iot 中樞總管](https://github.com/azure/iothub-explorer)是 CLI 工具，您在主機電腦 toomanage 裝置身分識別執行您的 IoT 中樞登錄中。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="6f4eb-107">它提供的管理選項，您可以使用 tooperform 各種工作。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="6f4eb-108">管理選項</span><span class="sxs-lookup"><span data-stu-id="6f4eb-108">Management option</span></span>          | <span data-ttu-id="6f4eb-109">Task</span><span class="sxs-lookup"><span data-stu-id="6f4eb-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6f4eb-110">直接方法</span><span class="sxs-lookup"><span data-stu-id="6f4eb-110">Direct methods</span></span>             | <span data-ttu-id="6f4eb-111">使裝置，例如啟動或停止傳送訊息，或重新啟動裝置 hello 做。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="6f4eb-112">對應項的所需屬性</span><span class="sxs-lookup"><span data-stu-id="6f4eb-112">Twin desired properties</span></span>    | <span data-ttu-id="6f4eb-113">將裝置放入特定狀態，例如設定 LED toogreen 或設定 hello 遙測傳送間隔 too30 分鐘數。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="6f4eb-114">對應項的報告屬性</span><span class="sxs-lookup"><span data-stu-id="6f4eb-114">Twin reported properties</span></span>   | <span data-ttu-id="6f4eb-115">取得 hello 報告裝置的狀態。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-115">Get hello reported state of a device.</span></span> <span data-ttu-id="6f4eb-116">例如，hello 裝置報告 LED 閃爍不停現在 hello。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="6f4eb-117">對應項標記</span><span class="sxs-lookup"><span data-stu-id="6f4eb-117">Twin tags</span></span>                  | <span data-ttu-id="6f4eb-118">Hello 雲端中儲存裝置專屬的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="6f4eb-119">例如，hello 販賣的部署位置。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="6f4eb-120">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="6f4eb-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="6f4eb-121">傳送通知 tooa 裝置。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-121">Send notifications tooa device.</span></span> <span data-ttu-id="6f4eb-122">比方說，「 是很有可能 toorain 今天。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="6f4eb-123">別忘了 toobring 概括性。 」</span><span class="sxs-lookup"><span data-stu-id="6f4eb-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="6f4eb-124">裝置對應項查詢</span><span class="sxs-lookup"><span data-stu-id="6f4eb-124">Device twin queries</span></span>        | <span data-ttu-id="6f4eb-125">查詢所有裝置雙 tooretrieve 具有任意的條件，例如識別 hello 裝置可供使用。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="6f4eb-126">如需詳細 hello 差異的說明和使用這些選項的指引，請參閱[裝置到雲端通訊指引](iot-hub-devguide-d2c-guidance.md)和[雲端到裝置通訊指引](iot-hub-devguide-c2d-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6f4eb-127">「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="6f4eb-128">IoT 中樞保存每個裝置連接 tooit 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="6f4eb-129">如需裝置對應項的詳細資訊，請參閱[開始使用裝置對應項](iot-hub-node-node-twin-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6f4eb-130">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="6f4eb-130">What you learn</span></span>

<span data-ttu-id="6f4eb-131">您會學到在開發電腦上使用 iothub-explorer 搭配各種管理選項。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6f4eb-132">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="6f4eb-132">What you do</span></span>

<span data-ttu-id="6f4eb-133">執行 iothub-explorer 搭配各種管理選項。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6f4eb-134">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="6f4eb-134">What you need</span></span>

- <span data-ttu-id="6f4eb-135">教學課程[設定您的裝置](iot-hub-raspberry-pi-kit-node-get-started.md)完成其中涵蓋了 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="6f4eb-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="6f4eb-136">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="6f4eb-137">位於您訂用帳戶中的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="6f4eb-138">用戶端應用程式所傳送訊息 tooyour Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="6f4eb-139">請確定您的裝置正在執行與本教學課程期間 hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="6f4eb-140">iothub-explorer，在開發電腦上[安裝 iothub-explorer](https://github.com/azure/iothub-explorer)。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="6f4eb-141">連接 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="6f4eb-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="6f4eb-142">執行下列命令的 hello 連線 tooyour IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="6f4eb-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="6f4eb-143">使用 iothub-explorer 搭配直接方法</span><span class="sxs-lookup"><span data-stu-id="6f4eb-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="6f4eb-144">叫用 hello `start` hello 裝置應用程式 toosend 訊息 tooyour IoT 中樞中執行下列命令的 hello 方法：</span><span class="sxs-lookup"><span data-stu-id="6f4eb-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="6f4eb-145">叫用 hello `stop` hello 裝置應用程式 toostop 傳送的方法藉由執行下列命令的 hello 訊息 tooyour IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="6f4eb-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="6f4eb-146">使用 iothub-explorer 搭配對應項所需的屬性</span><span class="sxs-lookup"><span data-stu-id="6f4eb-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="6f4eb-147">設定所需的屬性間隔 = 3000 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f4eb-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="6f4eb-148">此屬性可以由您的裝置讀取。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="6f4eb-149">使用 iothub-explorer 搭配對應項的報告屬性</span><span class="sxs-lookup"><span data-stu-id="6f4eb-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="6f4eb-150">取得 hello 報告的屬性，藉由執行 hello hello 裝置的下列命令：</span><span class="sxs-lookup"><span data-stu-id="6f4eb-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6f4eb-151">Hello 屬性的其中一個是 $metadata。 $lastUpdated 會顯示 hello 最後一次此裝置傳送或接收訊息。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="6f4eb-152">使用 iothub-explorer 搭配對應項標記</span><span class="sxs-lookup"><span data-stu-id="6f4eb-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="6f4eb-153">藉由執行下列命令的 hello 顯示 hello 標記與 hello 裝置的內容：</span><span class="sxs-lookup"><span data-stu-id="6f4eb-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6f4eb-154">新增欄位角色執行下列命令的 hello = 溫度和溼度 toohello 裝置：</span><span class="sxs-lookup"><span data-stu-id="6f4eb-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="6f4eb-155">對雲端到裝置的訊息使用 iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="6f4eb-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="6f4eb-156">將"Hello World"訊息 toohello 裝置傳送藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f4eb-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="6f4eb-157">請參閱[使用 iot 中樞總管 toosend 和接收訊息，您的裝置與 IoT 中樞之間](iot-hub-explorer-cloud-device-messaging.md)真實案例中使用此命令。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="6f4eb-158">使用 iothub-explorer 搭配裝置對應項查詢</span><span class="sxs-lookup"><span data-stu-id="6f4eb-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="6f4eb-159">查詢與角色的標籤裝置 = '溫度和溼度'，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f4eb-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="6f4eb-160">查詢以外的角色有標記的所有裝置 = '溫度和溼度'，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f4eb-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="6f4eb-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f4eb-161">Next steps</span></span>

<span data-ttu-id="6f4eb-162">您所學到如何 toouse iot 中樞-總管 中有各種不同的管理選項。</span><span class="sxs-lookup"><span data-stu-id="6f4eb-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
