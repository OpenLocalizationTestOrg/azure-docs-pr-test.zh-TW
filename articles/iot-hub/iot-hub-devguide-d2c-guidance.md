---
title: "IoT 中樞裝置到雲端 aaaAzure 選項 |Microsoft 文件"
description: "開發人員指南-當 toouse 裝置到雲端訊息、 報告的屬性或檔案上傳雲端到裝置通訊的指引。"
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
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a><span data-ttu-id="6873f-103">Device-to-cloud communications guidance</span><span class="sxs-lookup"><span data-stu-id="6873f-103">Device-to-cloud communications guidance</span></span>
<span data-ttu-id="6873f-104">將資訊傳送從 hello 裝置應用程式 toohello 方案後端，IoT 中樞會公開三個選項：</span><span class="sxs-lookup"><span data-stu-id="6873f-104">When sending information from hello device app toohello solution back end, IoT Hub exposes three options:</span></span>

* <span data-ttu-id="6873f-105">[裝置到雲端訊息][lnk-d2c]，適用於時間序列遙測和警示。</span><span class="sxs-lookup"><span data-stu-id="6873f-105">[Device-to-cloud messages][lnk-d2c] for time series telemetry and alerts.</span></span>
* <span data-ttu-id="6873f-106">[報告內容][ lnk-twins]報告裝置狀態資訊，例如可用的功能、 條件或 hello 的長時間執行工作流程的狀態。</span><span class="sxs-lookup"><span data-stu-id="6873f-106">[Reported properties][lnk-twins] for reporting device state information such as available capabilities, conditions, or hello state of long-running workflows.</span></span> <span data-ttu-id="6873f-107">例如，組態和軟體更新。</span><span class="sxs-lookup"><span data-stu-id="6873f-107">For example, configuration and software updates.</span></span>
* <span data-ttu-id="6873f-108">[檔案上傳][ lnk-fileupload]媒體檔案和大型遙測批次上傳間斷連接裝置，或壓縮的 toosave 頻寬。</span><span class="sxs-lookup"><span data-stu-id="6873f-108">[File uploads][lnk-fileupload] for media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="6873f-109">以下是 hello 的詳細的比較裝置到雲端通訊的各種選項。</span><span class="sxs-lookup"><span data-stu-id="6873f-109">Here is a detailed comparison of hello various device-to-cloud communication options.</span></span>

|  | <span data-ttu-id="6873f-110">裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="6873f-110">Device-to-cloud messages</span></span> | <span data-ttu-id="6873f-111">報告屬性</span><span class="sxs-lookup"><span data-stu-id="6873f-111">Reported properties</span></span> | <span data-ttu-id="6873f-112">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="6873f-112">File uploads</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="6873f-113">案例</span><span class="sxs-lookup"><span data-stu-id="6873f-113">Scenario</span></span> | <span data-ttu-id="6873f-114">遙測時間序列和警示。</span><span class="sxs-lookup"><span data-stu-id="6873f-114">Telemetry time series and alerts.</span></span> <span data-ttu-id="6873f-115">例如，每隔 5 分鐘傳送一次的 256 KB 感應器資料批次。</span><span class="sxs-lookup"><span data-stu-id="6873f-115">For example, 256-KB sensor data batches sent every 5 minutes.</span></span> | <span data-ttu-id="6873f-116">可用的功能與條件。</span><span class="sxs-lookup"><span data-stu-id="6873f-116">Available capabilities and conditions.</span></span> <span data-ttu-id="6873f-117">例如，hello 目前裝置連線模式例如行動電話通訊或 Wi-fi。</span><span class="sxs-lookup"><span data-stu-id="6873f-117">For example, hello current device connectivity mode such as cellular or WiFi.</span></span> <span data-ttu-id="6873f-118">同步處理長時間執行的工作流程，例如組態與軟體更新。</span><span class="sxs-lookup"><span data-stu-id="6873f-118">Synchronizing long-running workflows, such as configuration and software updates.</span></span> | <span data-ttu-id="6873f-119">媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="6873f-119">Media files.</span></span> <span data-ttu-id="6873f-120">大型 (通常已壓縮的) 遙測批次。</span><span class="sxs-lookup"><span data-stu-id="6873f-120">Large (typically compressed) telemetry batches.</span></span> |
| <span data-ttu-id="6873f-121">儲存和擷取</span><span class="sxs-lookup"><span data-stu-id="6873f-121">Storage and retrieval</span></span> | <span data-ttu-id="6873f-122">IoT 中樞來暫時儲存向上 too7 天。</span><span class="sxs-lookup"><span data-stu-id="6873f-122">Temporarily stored by IoT Hub, up too7 days.</span></span> <span data-ttu-id="6873f-123">僅限循序讀取。</span><span class="sxs-lookup"><span data-stu-id="6873f-123">Only sequential reading.</span></span> | <span data-ttu-id="6873f-124">IoT 中樞存 hello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="6873f-124">Stored by IoT Hub in hello device twin.</span></span> <span data-ttu-id="6873f-125">擷取使用 hello [IoT 中樞的查詢語言][lnk-query]。</span><span class="sxs-lookup"><span data-stu-id="6873f-125">Retrievable using hello [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="6873f-126">儲存在使用者提供的 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="6873f-126">Stored in user-provided Azure Storage account.</span></span> |
| <span data-ttu-id="6873f-127">大小</span><span class="sxs-lookup"><span data-stu-id="6873f-127">Size</span></span> | <span data-ttu-id="6873f-128">Too256 KB 的訊息。</span><span class="sxs-lookup"><span data-stu-id="6873f-128">Up too256-KB messages.</span></span> | <span data-ttu-id="6873f-129">最大回報屬性大小為 8 KB。</span><span class="sxs-lookup"><span data-stu-id="6873f-129">Maximum reported properties size is 8 KB.</span></span> | <span data-ttu-id="6873f-130">Azure Blob 儲存體所支援的檔案大小上限。</span><span class="sxs-lookup"><span data-stu-id="6873f-130">Maximum file size supported by Azure Blob Storage.</span></span> |
| <span data-ttu-id="6873f-131">頻率</span><span class="sxs-lookup"><span data-stu-id="6873f-131">Frequency</span></span> | <span data-ttu-id="6873f-132">高。</span><span class="sxs-lookup"><span data-stu-id="6873f-132">High.</span></span> <span data-ttu-id="6873f-133">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="6873f-133">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="6873f-134">中。</span><span class="sxs-lookup"><span data-stu-id="6873f-134">Medium.</span></span> <span data-ttu-id="6873f-135">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="6873f-135">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="6873f-136">低。</span><span class="sxs-lookup"><span data-stu-id="6873f-136">Low.</span></span> <span data-ttu-id="6873f-137">如需詳細資訊，請參閱 [IoT 中樞限制][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="6873f-137">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="6873f-138">通訊協定</span><span class="sxs-lookup"><span data-stu-id="6873f-138">Protocol</span></span> | <span data-ttu-id="6873f-139">適用於所有通訊協定。</span><span class="sxs-lookup"><span data-stu-id="6873f-139">Available on all protocols.</span></span> | <span data-ttu-id="6873f-140">目前僅適用於使用 MQTT 時。</span><span class="sxs-lookup"><span data-stu-id="6873f-140">Currently available only when using MQTT.</span></span> | <span data-ttu-id="6873f-141">當使用任何通訊協定，但需要 HTTP hello 裝置上才能使用。</span><span class="sxs-lookup"><span data-stu-id="6873f-141">Available when using any protocol, but requires HTTP on hello device.</span></span> |

<span data-ttu-id="6873f-142">可能的應用程式需要為遙測時間序列或警示，且 toomake tooboth 傳送資訊提供 hello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="6873f-142">It is possible that an application requires tooboth send information as a telemetry time series or alert and also toomake it available in hello device twin.</span></span> <span data-ttu-id="6873f-143">在此案例中，您可以選擇使用的下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="6873f-143">In this scenario, you can chose one of hello following options:</span></span>

* <span data-ttu-id="6873f-144">hello 裝置應用程式傳送裝置到雲端訊息，並報告屬性變更。</span><span class="sxs-lookup"><span data-stu-id="6873f-144">hello device app sends a device-to-cloud message and reports a property change.</span></span>
* <span data-ttu-id="6873f-145">hello 方案後端在收到 hello 訊息時，可以在 hello 裝置兩個的標記儲存 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="6873f-145">hello solution back end can store hello information in hello device twin's tags when it receives hello message.</span></span>

<span data-ttu-id="6873f-146">因為裝置到雲端訊息啟用更高輸送量比裝置兩個更新，可能會很理想 tooavoid 更新 hello 裝置兩個的每一個裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="6873f-146">Since device-to-cloud messages enable a much higher throughput than device twin updates, it is sometimes desirable tooavoid updating hello device twin for every device-to-cloud message.</span></span>


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
