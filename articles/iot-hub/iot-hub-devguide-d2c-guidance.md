---
title: "Azure IoT 中樞裝置到雲端選項 | Microsoft Docs"
description: "開發人員指南 - 針對雲端到裝置通訊，提供裝置到雲端訊息、報告屬性或檔案上傳的使用時機指引。"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: a36283053939ccd53856a394cd9efb66285271ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-communications-guidance"></a><span data-ttu-id="df1bc-103">Device-to-cloud communications guidance</span><span class="sxs-lookup"><span data-stu-id="df1bc-103">Device-to-cloud communications guidance</span></span>
<span data-ttu-id="df1bc-104">將資訊從裝置應用程式傳送到解決方案後端時，IoT 中樞會公開三個選項︰</span><span class="sxs-lookup"><span data-stu-id="df1bc-104">When sending information from the device app to the solution back end, IoT Hub exposes three options:</span></span>

* <span data-ttu-id="df1bc-105">[裝置到雲端訊息][lnk-d2c]，適用於時間序列遙測和警示。</span><span class="sxs-lookup"><span data-stu-id="df1bc-105">[Device-to-cloud messages][lnk-d2c] for time series telemetry and alerts.</span></span>
* <span data-ttu-id="df1bc-106">[報告屬性][lnk-twins]，適用於報告裝置狀態資訊，如長時間執行之工作流程可用的功能、條件和狀態。</span><span class="sxs-lookup"><span data-stu-id="df1bc-106">[Reported properties][lnk-twins] for reporting device state information such as available capabilities, conditions, or the state of long-running workflows.</span></span> <span data-ttu-id="df1bc-107">例如，組態和軟體更新。</span><span class="sxs-lookup"><span data-stu-id="df1bc-107">For example, configuration and software updates.</span></span>
* <span data-ttu-id="df1bc-108">[檔案上傳][lnk-fileupload]，適用於間歇性連線裝置所上傳或為了節省頻寬而壓縮的媒體檔案和大型遙測批次。</span><span class="sxs-lookup"><span data-stu-id="df1bc-108">[File uploads][lnk-fileupload] for media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="df1bc-109">以下是各種裝置到雲端通訊選項的詳細比較。</span><span class="sxs-lookup"><span data-stu-id="df1bc-109">Here is a detailed comparison of the various device-to-cloud communication options.</span></span>

|  | <span data-ttu-id="df1bc-110">裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="df1bc-110">Device-to-cloud messages</span></span> | <span data-ttu-id="df1bc-111">報告屬性</span><span class="sxs-lookup"><span data-stu-id="df1bc-111">Reported properties</span></span> | <span data-ttu-id="df1bc-112">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="df1bc-112">File uploads</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="df1bc-113">案例</span><span class="sxs-lookup"><span data-stu-id="df1bc-113">Scenario</span></span> | <span data-ttu-id="df1bc-114">遙測時間序列和警示。</span><span class="sxs-lookup"><span data-stu-id="df1bc-114">Telemetry time series and alerts.</span></span> <span data-ttu-id="df1bc-115">例如，每隔 5 分鐘傳送一次的 256 KB 感應器資料批次。</span><span class="sxs-lookup"><span data-stu-id="df1bc-115">For example, 256-KB sensor data batches sent every 5 minutes.</span></span> | <span data-ttu-id="df1bc-116">可用的功能與條件。</span><span class="sxs-lookup"><span data-stu-id="df1bc-116">Available capabilities and conditions.</span></span> <span data-ttu-id="df1bc-117">例如，目前裝置連線能力模式，例如行動電話或 WiFi。</span><span class="sxs-lookup"><span data-stu-id="df1bc-117">For example, the current device connectivity mode such as cellular or WiFi.</span></span> <span data-ttu-id="df1bc-118">同步處理長時間執行的工作流程，例如組態與軟體更新。</span><span class="sxs-lookup"><span data-stu-id="df1bc-118">Synchronizing long-running workflows, such as configuration and software updates.</span></span> | <span data-ttu-id="df1bc-119">媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="df1bc-119">Media files.</span></span> <span data-ttu-id="df1bc-120">大型 (通常已壓縮的) 遙測批次。</span><span class="sxs-lookup"><span data-stu-id="df1bc-120">Large (typically compressed) telemetry batches.</span></span> |
| <span data-ttu-id="df1bc-121">儲存和擷取</span><span class="sxs-lookup"><span data-stu-id="df1bc-121">Storage and retrieval</span></span> | <span data-ttu-id="df1bc-122">由 IoT 中樞暫時儲存 (最多 7 天)。</span><span class="sxs-lookup"><span data-stu-id="df1bc-122">Temporarily stored by IoT Hub, up to 7 days.</span></span> <span data-ttu-id="df1bc-123">僅限循序讀取。</span><span class="sxs-lookup"><span data-stu-id="df1bc-123">Only sequential reading.</span></span> | <span data-ttu-id="df1bc-124">由裝置對應項中的 IoT 中樞儲存。</span><span class="sxs-lookup"><span data-stu-id="df1bc-124">Stored by IoT Hub in the device twin.</span></span> <span data-ttu-id="df1bc-125">使用 [IoT 中樞查詢語言][lnk-query]擷取。</span><span class="sxs-lookup"><span data-stu-id="df1bc-125">Retrievable using the [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="df1bc-126">儲存在使用者提供的 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="df1bc-126">Stored in user-provided Azure Storage account.</span></span> |
| <span data-ttu-id="df1bc-127">大小</span><span class="sxs-lookup"><span data-stu-id="df1bc-127">Size</span></span> | <span data-ttu-id="df1bc-128">最多 256 KB 的訊息。</span><span class="sxs-lookup"><span data-stu-id="df1bc-128">Up to 256-KB messages.</span></span> | <span data-ttu-id="df1bc-129">最大回報屬性大小為 8 KB。</span><span class="sxs-lookup"><span data-stu-id="df1bc-129">Maximum reported properties size is 8 KB.</span></span> | <span data-ttu-id="df1bc-130">Azure Blob 儲存體所支援的檔案大小上限。</span><span class="sxs-lookup"><span data-stu-id="df1bc-130">Maximum file size supported by Azure Blob Storage.</span></span> |
| <span data-ttu-id="df1bc-131">頻率</span><span class="sxs-lookup"><span data-stu-id="df1bc-131">Frequency</span></span> | <span data-ttu-id="df1bc-132">高。</span><span class="sxs-lookup"><span data-stu-id="df1bc-132">High.</span></span> <span data-ttu-id="df1bc-133">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="df1bc-133">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="df1bc-134">中。</span><span class="sxs-lookup"><span data-stu-id="df1bc-134">Medium.</span></span> <span data-ttu-id="df1bc-135">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="df1bc-135">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="df1bc-136">低。</span><span class="sxs-lookup"><span data-stu-id="df1bc-136">Low.</span></span> <span data-ttu-id="df1bc-137">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="df1bc-137">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="df1bc-138">通訊協定</span><span class="sxs-lookup"><span data-stu-id="df1bc-138">Protocol</span></span> | <span data-ttu-id="df1bc-139">適用於所有通訊協定。</span><span class="sxs-lookup"><span data-stu-id="df1bc-139">Available on all protocols.</span></span> | <span data-ttu-id="df1bc-140">目前僅適用於使用 MQTT 時。</span><span class="sxs-lookup"><span data-stu-id="df1bc-140">Currently available only when using MQTT.</span></span> | <span data-ttu-id="df1bc-141">可用於使用任何通訊協定時，但需要是裝置上的 HTTP。</span><span class="sxs-lookup"><span data-stu-id="df1bc-141">Available when using any protocol, but requires HTTP on the device.</span></span> |

<span data-ttu-id="df1bc-142">應用程式可能需要以遙測時間序列或警示形式傳送資訊，而且使其可用於裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="df1bc-142">It is possible that an application requires to both send information as a telemetry time series or alert and also to make it available in the device twin.</span></span> <span data-ttu-id="df1bc-143">在此案例中，您可以選擇下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="df1bc-143">In this scenario, you can chose one of the following options:</span></span>

* <span data-ttu-id="df1bc-144">裝置應用程式可傳送裝置到雲端訊息及回報屬性變更。</span><span class="sxs-lookup"><span data-stu-id="df1bc-144">The device app sends a device-to-cloud message and reports a property change.</span></span>
* <span data-ttu-id="df1bc-145">解決方案後端可以在收到訊息時將資訊儲存在裝置對應項的標籤中。</span><span class="sxs-lookup"><span data-stu-id="df1bc-145">The solution back end can store the information in the device twin's tags when it receives the message.</span></span>

<span data-ttu-id="df1bc-146">由於裝置到雲端訊息允許高於裝置對應項更新的輸送量，所以有時希望避免針對每則裝置到雲端訊息更新裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="df1bc-146">Since device-to-cloud messages enable a much higher throughput than device twin updates, it is sometimes desirable to avoid updating the device twin for every device-to-cloud message.</span></span>


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
