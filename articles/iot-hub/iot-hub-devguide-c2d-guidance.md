---
title: "IoT 中樞雲端到裝置 aaaAzure 選項 |Microsoft 文件"
description: "開發人員指南-指引 toouse 時直接的方法、 兩個裝置所需的屬性或雲端到裝置訊息雲端到裝置通訊。"
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
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a><span data-ttu-id="64468-103">Cloud-to-device communications guidance</span><span class="sxs-lookup"><span data-stu-id="64468-103">Cloud-to-device communications guidance</span></span>
<span data-ttu-id="64468-104">IoT 中心提供裝置應用程式 tooexpose 功能 tooa 後端應用程式的三個的選項：</span><span class="sxs-lookup"><span data-stu-id="64468-104">IoT Hub provides three options for device apps tooexpose functionality tooa back-end app:</span></span>

* <span data-ttu-id="64468-105">[直接方法][ lnk-methods]需要立即確認 hello 結果的通訊。</span><span class="sxs-lookup"><span data-stu-id="64468-105">[Direct methods][lnk-methods] for communications that require immediate confirmation of hello result.</span></span> <span data-ttu-id="64468-106">直接方法通常用於裝置的互動式控制，例如開啟風扇。</span><span class="sxs-lookup"><span data-stu-id="64468-106">Direct methods are often used for interactive control of devices such as turning on a fan.</span></span>
* <span data-ttu-id="64468-107">[兩個的所需屬性][ lnk-twins]的長時間執行的命令可讓您能 tooput hello 裝置插入特定預期狀態。</span><span class="sxs-lookup"><span data-stu-id="64468-107">[Twin's desired properties][lnk-twins] for long-running commands intended tooput hello device into a certain desired state.</span></span> <span data-ttu-id="64468-108">例如，設定 hello 遙測傳送間隔 too30 分鐘數。</span><span class="sxs-lookup"><span data-stu-id="64468-108">For example, set hello telemetry send interval too30 minutes.</span></span>
* <span data-ttu-id="64468-109">[雲端到裝置訊息][ lnk-c2d]單向通知 toohello 裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="64468-109">[Cloud-to-device messages][lnk-c2d] for one-way notifications toohello device app.</span></span>

<span data-ttu-id="64468-110">以下是 hello 的詳細的比較雲端到裝置通訊的各種選項。</span><span class="sxs-lookup"><span data-stu-id="64468-110">Here is a detailed comparison of hello various cloud-to-device communication options.</span></span>

|  | <span data-ttu-id="64468-111">直接方法</span><span class="sxs-lookup"><span data-stu-id="64468-111">Direct methods</span></span> | <span data-ttu-id="64468-112">對應項的所需屬性</span><span class="sxs-lookup"><span data-stu-id="64468-112">Twin's desired properties</span></span> | <span data-ttu-id="64468-113">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="64468-113">Cloud-to-device messages</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="64468-114">案例</span><span class="sxs-lookup"><span data-stu-id="64468-114">Scenario</span></span> | <span data-ttu-id="64468-115">需要立即確認的命令，例如開啟風扇。</span><span class="sxs-lookup"><span data-stu-id="64468-115">Commands that require immediate confirmation, such as turning on a fan.</span></span> | <span data-ttu-id="64468-116">長時間執行的命令適 tooput hello 裝置特定的所需的狀態。</span><span class="sxs-lookup"><span data-stu-id="64468-116">Long-running commands intended tooput hello device into a certain desired state.</span></span> <span data-ttu-id="64468-117">例如，設定 hello 遙測傳送間隔 too30 分鐘數。</span><span class="sxs-lookup"><span data-stu-id="64468-117">For example, set hello telemetry send interval too30 minutes.</span></span> | <span data-ttu-id="64468-118">單向通知 toohello 裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="64468-118">One-way notifications toohello device app.</span></span> |
| <span data-ttu-id="64468-119">資料流</span><span class="sxs-lookup"><span data-stu-id="64468-119">Data flow</span></span> | <span data-ttu-id="64468-120">雙向。</span><span class="sxs-lookup"><span data-stu-id="64468-120">Two-way.</span></span> <span data-ttu-id="64468-121">hello 裝置應用程式可以立即回應 toohello 方法。</span><span class="sxs-lookup"><span data-stu-id="64468-121">hello device app can respond toohello method right away.</span></span> <span data-ttu-id="64468-122">hello 方案後端收到 hello 結果客 toohello 要求。</span><span class="sxs-lookup"><span data-stu-id="64468-122">hello solution back end receives hello outcome contextually toohello request.</span></span> | <span data-ttu-id="64468-123">單向。</span><span class="sxs-lookup"><span data-stu-id="64468-123">One-way.</span></span> <span data-ttu-id="64468-124">hello 裝置應用程式會收到一則通知 hello 屬性變更。</span><span class="sxs-lookup"><span data-stu-id="64468-124">hello device app receives a notification with hello property change.</span></span> | <span data-ttu-id="64468-125">單向。</span><span class="sxs-lookup"><span data-stu-id="64468-125">One-way.</span></span> <span data-ttu-id="64468-126">hello 裝置應用程式收到 hello 訊息</span><span class="sxs-lookup"><span data-stu-id="64468-126">hello device app receives hello message</span></span>
| <span data-ttu-id="64468-127">耐久性</span><span class="sxs-lookup"><span data-stu-id="64468-127">Durability</span></span> | <span data-ttu-id="64468-128">無法聯繫已中斷連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="64468-128">Disconnected devices are not contacted.</span></span> <span data-ttu-id="64468-129">hello 方案後端會收到該 hello 裝置未連接。</span><span class="sxs-lookup"><span data-stu-id="64468-129">hello solution back end is notified that hello device is not connected.</span></span> | <span data-ttu-id="64468-130">屬性值會保留在 hello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="64468-130">Property values are preserved in hello device twin.</span></span> <span data-ttu-id="64468-131">裝置會在下一次重新連線時讀取它。</span><span class="sxs-lookup"><span data-stu-id="64468-131">Device will read it at next reconnection.</span></span> <span data-ttu-id="64468-132">屬性值會以 hello 可擷取[IoT 中樞的查詢語言][lnk-query]。</span><span class="sxs-lookup"><span data-stu-id="64468-132">Property values are retrievable with hello [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="64468-133">IoT 中樞可以保留訊息 too48 時數。</span><span class="sxs-lookup"><span data-stu-id="64468-133">Messages can be retained by IoT Hub for up too48 hours.</span></span> |
| <span data-ttu-id="64468-134">目標</span><span class="sxs-lookup"><span data-stu-id="64468-134">Targets</span></span> | <span data-ttu-id="64468-135">使用 **deviceId** 的單一裝置，或使用[作業][lnk-jobs]的多個裝置。</span><span class="sxs-lookup"><span data-stu-id="64468-135">Single device using **deviceId**, or multiple devices using [jobs][lnk-jobs].</span></span> | <span data-ttu-id="64468-136">使用 **deviceId** 的單一裝置，或使用[作業][lnk-jobs]的多個裝置。</span><span class="sxs-lookup"><span data-stu-id="64468-136">Single device using **deviceId**, or multiple devices using [jobs][lnk-jobs].</span></span> | <span data-ttu-id="64468-137">依照 **deviceId** 的單一裝置。</span><span class="sxs-lookup"><span data-stu-id="64468-137">Single device by **deviceId**.</span></span> |
| <span data-ttu-id="64468-138">大小</span><span class="sxs-lookup"><span data-stu-id="64468-138">Size</span></span> | <span data-ttu-id="64468-139">向上 too8KB 要求和 8 KB 的回應。</span><span class="sxs-lookup"><span data-stu-id="64468-139">Up too8KB requests and 8KB responses.</span></span> | <span data-ttu-id="64468-140">所需屬性大小上限為 8KB。</span><span class="sxs-lookup"><span data-stu-id="64468-140">Maximum desired properties size is 8KB.</span></span> | <span data-ttu-id="64468-141">Too64KB 訊息。</span><span class="sxs-lookup"><span data-stu-id="64468-141">Up too64KB messages.</span></span> |
| <span data-ttu-id="64468-142">頻率</span><span class="sxs-lookup"><span data-stu-id="64468-142">Frequency</span></span> | <span data-ttu-id="64468-143">高。</span><span class="sxs-lookup"><span data-stu-id="64468-143">High.</span></span> <span data-ttu-id="64468-144">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="64468-144">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="64468-145">中。</span><span class="sxs-lookup"><span data-stu-id="64468-145">Medium.</span></span> <span data-ttu-id="64468-146">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="64468-146">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="64468-147">低。</span><span class="sxs-lookup"><span data-stu-id="64468-147">Low.</span></span> <span data-ttu-id="64468-148">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="64468-148">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="64468-149">通訊協定</span><span class="sxs-lookup"><span data-stu-id="64468-149">Protocol</span></span> | <span data-ttu-id="64468-150">目前僅適用於使用 MQTT 時。</span><span class="sxs-lookup"><span data-stu-id="64468-150">Currently available only when using MQTT.</span></span> | <span data-ttu-id="64468-151">目前僅適用於使用 MQTT 時。</span><span class="sxs-lookup"><span data-stu-id="64468-151">Currently available only when using MQTT.</span></span> | <span data-ttu-id="64468-152">適用於所有通訊協定。</span><span class="sxs-lookup"><span data-stu-id="64468-152">Available on all protocols.</span></span> <span data-ttu-id="64468-153">裝置必須在使用 HTTP 時進行輪詢。</span><span class="sxs-lookup"><span data-stu-id="64468-153">Device must poll when using HTTP.</span></span> |

<span data-ttu-id="64468-154">了解 toouse 如何直接的方法、 所需的屬性和雲端到裝置訊息 hello 遵循教學課程中：</span><span class="sxs-lookup"><span data-stu-id="64468-154">Learn how toouse direct methods, desired properties, and cloud-to-device messages in hello following tutorials:</span></span>

* <span data-ttu-id="64468-155">[使用直接方法][lnk-methods-tutorial]，適用於直接方法；</span><span class="sxs-lookup"><span data-stu-id="64468-155">[Use direct methods][lnk-methods-tutorial], for direct methods;</span></span>
* <span data-ttu-id="64468-156">[使用所需的屬性 tooconfigure 裝置][lnk-twin-properties]，針對裝置的兩個的預期屬性。</span><span class="sxs-lookup"><span data-stu-id="64468-156">[Use desired properties tooconfigure devices][lnk-twin-properties], for device twin's desired properties;</span></span> 
* <span data-ttu-id="64468-157">[傳送雲端到裝置訊息][lnk-c2d-tutorial]，適用於雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="64468-157">[Send cloud-to-device messages][lnk-c2d-tutorial], for cloud-to-device messages.</span></span>

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
