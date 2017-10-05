---
title: "Azure IoT 中樞雲端到裝置選項 | Microsoft Docs"
description: "開發人員指南 - 針對雲端到裝置通訊，提供直接方法、裝置對應項的所需屬性或雲端到裝置訊息的使用時機指引。"
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: e6cd4880c9bfcc670bd116d3dd8e5245d70f85cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-to-device-communications-guidance"></a><span data-ttu-id="bc169-103">Cloud-to-device communications guidance</span><span class="sxs-lookup"><span data-stu-id="bc169-103">Cloud-to-device communications guidance</span></span>
<span data-ttu-id="bc169-104">IoT 中樞提供三個選項以便裝置應用程式對後端應用程式公開功能︰</span><span class="sxs-lookup"><span data-stu-id="bc169-104">IoT Hub provides three options for device apps to expose functionality to a back-end app:</span></span>

* <span data-ttu-id="bc169-105">[直接方法][lnk-methods]，適用於需要立即確認結果的通訊。</span><span class="sxs-lookup"><span data-stu-id="bc169-105">[Direct methods][lnk-methods] for communications that require immediate confirmation of the result.</span></span> <span data-ttu-id="bc169-106">直接方法通常用於裝置的互動式控制，例如開啟風扇。</span><span class="sxs-lookup"><span data-stu-id="bc169-106">Direct methods are often used for interactive control of devices such as turning on a fan.</span></span>
* <span data-ttu-id="bc169-107">[對應項的所需屬性][lnk-twins]，適用於可讓裝置進入特定所需狀態的長時間執行命令。</span><span class="sxs-lookup"><span data-stu-id="bc169-107">[Twin's desired properties][lnk-twins] for long-running commands intended to put the device into a certain desired state.</span></span> <span data-ttu-id="bc169-108">例如，將遙測傳送間隔設定為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="bc169-108">For example, set the telemetry send interval to 30 minutes.</span></span>
* <span data-ttu-id="bc169-109">[雲端到裝置訊息][lnk-c2d]，適用於對裝置應用程式的單向通知。</span><span class="sxs-lookup"><span data-stu-id="bc169-109">[Cloud-to-device messages][lnk-c2d] for one-way notifications to the device app.</span></span>

<span data-ttu-id="bc169-110">以下是各種雲端到裝置通訊選項的詳細比較。</span><span class="sxs-lookup"><span data-stu-id="bc169-110">Here is a detailed comparison of the various cloud-to-device communication options.</span></span>

|  | <span data-ttu-id="bc169-111">直接方法</span><span class="sxs-lookup"><span data-stu-id="bc169-111">Direct methods</span></span> | <span data-ttu-id="bc169-112">對應項的所需屬性</span><span class="sxs-lookup"><span data-stu-id="bc169-112">Twin's desired properties</span></span> | <span data-ttu-id="bc169-113">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="bc169-113">Cloud-to-device messages</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="bc169-114">案例</span><span class="sxs-lookup"><span data-stu-id="bc169-114">Scenario</span></span> | <span data-ttu-id="bc169-115">需要立即確認的命令，例如開啟風扇。</span><span class="sxs-lookup"><span data-stu-id="bc169-115">Commands that require immediate confirmation, such as turning on a fan.</span></span> | <span data-ttu-id="bc169-116">可讓裝置進入特定所需狀態的長時間執行命令。</span><span class="sxs-lookup"><span data-stu-id="bc169-116">Long-running commands intended to put the device into a certain desired state.</span></span> <span data-ttu-id="bc169-117">例如，將遙測傳送間隔設定為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="bc169-117">For example, set the telemetry send interval to 30 minutes.</span></span> | <span data-ttu-id="bc169-118">對裝置應用程式的單向通知。</span><span class="sxs-lookup"><span data-stu-id="bc169-118">One-way notifications to the device app.</span></span> |
| <span data-ttu-id="bc169-119">資料流</span><span class="sxs-lookup"><span data-stu-id="bc169-119">Data flow</span></span> | <span data-ttu-id="bc169-120">雙向。</span><span class="sxs-lookup"><span data-stu-id="bc169-120">Two-way.</span></span> <span data-ttu-id="bc169-121">裝置應用程式可以立即回應方法。</span><span class="sxs-lookup"><span data-stu-id="bc169-121">The device app can respond to the method right away.</span></span> <span data-ttu-id="bc169-122">解決方案後端會接收到根據要求上下文的結果。</span><span class="sxs-lookup"><span data-stu-id="bc169-122">The solution back end receives the outcome contextually to the request.</span></span> | <span data-ttu-id="bc169-123">單向。</span><span class="sxs-lookup"><span data-stu-id="bc169-123">One-way.</span></span> <span data-ttu-id="bc169-124">裝置應用程式會收到屬性變更的通知。</span><span class="sxs-lookup"><span data-stu-id="bc169-124">The device app receives a notification with the property change.</span></span> | <span data-ttu-id="bc169-125">單向。</span><span class="sxs-lookup"><span data-stu-id="bc169-125">One-way.</span></span> <span data-ttu-id="bc169-126">裝置應用程式接收訊息</span><span class="sxs-lookup"><span data-stu-id="bc169-126">The device app receives the message</span></span>
| <span data-ttu-id="bc169-127">耐久性</span><span class="sxs-lookup"><span data-stu-id="bc169-127">Durability</span></span> | <span data-ttu-id="bc169-128">無法聯繫已中斷連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="bc169-128">Disconnected devices are not contacted.</span></span> <span data-ttu-id="bc169-129">解決方案後端會收到裝置未連線的通知。</span><span class="sxs-lookup"><span data-stu-id="bc169-129">The solution back end is notified that the device is not connected.</span></span> | <span data-ttu-id="bc169-130">屬性值會保留在裝置對應項中。</span><span class="sxs-lookup"><span data-stu-id="bc169-130">Property values are preserved in the device twin.</span></span> <span data-ttu-id="bc169-131">裝置會在下一次重新連線時讀取它。</span><span class="sxs-lookup"><span data-stu-id="bc169-131">Device will read it at next reconnection.</span></span> <span data-ttu-id="bc169-132">使用 [IoT 中樞查詢語言][lnk-query]可擷取屬性值。</span><span class="sxs-lookup"><span data-stu-id="bc169-132">Property values are retrievable with the [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="bc169-133">IoT 中樞可以保留訊息長達 48 小時。</span><span class="sxs-lookup"><span data-stu-id="bc169-133">Messages can be retained by IoT Hub for up to 48 hours.</span></span> |
| <span data-ttu-id="bc169-134">目標</span><span class="sxs-lookup"><span data-stu-id="bc169-134">Targets</span></span> | <span data-ttu-id="bc169-135">使用 **deviceId** 的單一裝置，或使用[作業][lnk-jobs]的多個裝置。</span><span class="sxs-lookup"><span data-stu-id="bc169-135">Single device using **deviceId**, or multiple devices using [jobs][lnk-jobs].</span></span> | <span data-ttu-id="bc169-136">使用 **deviceId** 的單一裝置，或使用[作業][lnk-jobs]的多個裝置。</span><span class="sxs-lookup"><span data-stu-id="bc169-136">Single device using **deviceId**, or multiple devices using [jobs][lnk-jobs].</span></span> | <span data-ttu-id="bc169-137">依照 **deviceId** 的單一裝置。</span><span class="sxs-lookup"><span data-stu-id="bc169-137">Single device by **deviceId**.</span></span> |
| <span data-ttu-id="bc169-138">大小</span><span class="sxs-lookup"><span data-stu-id="bc169-138">Size</span></span> | <span data-ttu-id="bc169-139">最多 8KB 要求和 8KB 回應。</span><span class="sxs-lookup"><span data-stu-id="bc169-139">Up to 8KB requests and 8KB responses.</span></span> | <span data-ttu-id="bc169-140">所需屬性大小上限為 8KB。</span><span class="sxs-lookup"><span data-stu-id="bc169-140">Maximum desired properties size is 8KB.</span></span> | <span data-ttu-id="bc169-141">最多 64KB 的訊息。</span><span class="sxs-lookup"><span data-stu-id="bc169-141">Up to 64KB messages.</span></span> |
| <span data-ttu-id="bc169-142">頻率</span><span class="sxs-lookup"><span data-stu-id="bc169-142">Frequency</span></span> | <span data-ttu-id="bc169-143">高。</span><span class="sxs-lookup"><span data-stu-id="bc169-143">High.</span></span> <span data-ttu-id="bc169-144">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="bc169-144">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="bc169-145">中。</span><span class="sxs-lookup"><span data-stu-id="bc169-145">Medium.</span></span> <span data-ttu-id="bc169-146">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="bc169-146">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="bc169-147">低。</span><span class="sxs-lookup"><span data-stu-id="bc169-147">Low.</span></span> <span data-ttu-id="bc169-148">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="bc169-148">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="bc169-149">通訊協定</span><span class="sxs-lookup"><span data-stu-id="bc169-149">Protocol</span></span> | <span data-ttu-id="bc169-150">目前僅適用於使用 MQTT 時。</span><span class="sxs-lookup"><span data-stu-id="bc169-150">Currently available only when using MQTT.</span></span> | <span data-ttu-id="bc169-151">目前僅適用於使用 MQTT 時。</span><span class="sxs-lookup"><span data-stu-id="bc169-151">Currently available only when using MQTT.</span></span> | <span data-ttu-id="bc169-152">適用於所有通訊協定。</span><span class="sxs-lookup"><span data-stu-id="bc169-152">Available on all protocols.</span></span> <span data-ttu-id="bc169-153">裝置必須在使用 HTTP 時進行輪詢。</span><span class="sxs-lookup"><span data-stu-id="bc169-153">Device must poll when using HTTP.</span></span> |

<span data-ttu-id="bc169-154">在下列教學課程中，了解如何使用直接方法、所需屬性和雲端到裝置訊息︰</span><span class="sxs-lookup"><span data-stu-id="bc169-154">Learn how to use direct methods, desired properties, and cloud-to-device messages in the following tutorials:</span></span>

* <span data-ttu-id="bc169-155">[使用直接方法][lnk-methods-tutorial]，適用於直接方法；</span><span class="sxs-lookup"><span data-stu-id="bc169-155">[Use direct methods][lnk-methods-tutorial], for direct methods;</span></span>
* <span data-ttu-id="bc169-156">[使用所需屬性來設定裝置][lnk-twin-properties]，適用於裝置對應項的所需屬性；</span><span class="sxs-lookup"><span data-stu-id="bc169-156">[Use desired properties to configure devices][lnk-twin-properties], for device twin's desired properties;</span></span> 
* <span data-ttu-id="bc169-157">[傳送雲端到裝置訊息][lnk-c2d-tutorial]，適用於雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="bc169-157">[Send cloud-to-device messages][lnk-c2d-tutorial], for cloud-to-device messages.</span></span>

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
