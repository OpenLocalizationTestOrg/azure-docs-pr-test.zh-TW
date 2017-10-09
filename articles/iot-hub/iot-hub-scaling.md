---
title: "aaaAzure IoT 中樞調整 |Microsoft 文件"
description: "如何 tooscale 您的 IoT 中樞 toosupport 預期的訊息輸送量。 包含摘要的 hello 支援的每一層的輸送量與分區化的選項。"
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="112f1-104">調整您的 IoT 中樞解決方案</span><span class="sxs-lookup"><span data-stu-id="112f1-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="112f1-105">Azure IoT 中樞可以支援 tooa 百萬個同時連接的裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="112f1-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="112f1-106">如需詳細資訊，請參閱 [IoT 中樞價格][lnk-pricing]。</span><span class="sxs-lookup"><span data-stu-id="112f1-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="112f1-107">每個 IoT 中樞單位允許一定數量的每日訊息。</span><span class="sxs-lookup"><span data-stu-id="112f1-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="112f1-108">tooproperly 調整您的方案，請考慮您的 IoT 中樞的特殊使用。</span><span class="sxs-lookup"><span data-stu-id="112f1-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="112f1-109">特別是，請考慮下列的作業類別目錄的 hello 的所需的 hello 尖峰輸送量：</span><span class="sxs-lookup"><span data-stu-id="112f1-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="112f1-110">裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="112f1-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="112f1-111">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="112f1-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="112f1-112">身分識別登錄作業</span><span class="sxs-lookup"><span data-stu-id="112f1-112">Identity registry operations</span></span>

<span data-ttu-id="112f1-113">在其他 toothis 輸送量資訊，請參閱[IoT 中樞配額與節流閥][ IoT Hub quotas and throttles]並據此設計您的方案。</span><span class="sxs-lookup"><span data-stu-id="112f1-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="112f1-114">裝置到雲端及雲端到裝置訊息輸送量</span><span class="sxs-lookup"><span data-stu-id="112f1-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="112f1-115">最佳的方式 toosize hello IoT 中樞方案是以每單位為基礎的 tooevaluate hello 流量。</span><span class="sxs-lookup"><span data-stu-id="112f1-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="112f1-116">裝置到雲端訊息會遵循這些持續的輸送量指導方針。</span><span class="sxs-lookup"><span data-stu-id="112f1-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="112f1-117">層</span><span class="sxs-lookup"><span data-stu-id="112f1-117">Tier</span></span> | <span data-ttu-id="112f1-118">持續的輸送量</span><span class="sxs-lookup"><span data-stu-id="112f1-118">Sustained throughput</span></span> | <span data-ttu-id="112f1-119">持續的傳送速率</span><span class="sxs-lookup"><span data-stu-id="112f1-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="112f1-120">S1</span><span class="sxs-lookup"><span data-stu-id="112f1-120">S1</span></span> |<span data-ttu-id="112f1-121">向上 too1111 KB/每單位分鐘</span><span class="sxs-lookup"><span data-stu-id="112f1-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="112f1-122">(1.5 GB/天/單位)</span><span class="sxs-lookup"><span data-stu-id="112f1-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="112f1-123">每個單位平均 278 個訊息/分鐘</span><span class="sxs-lookup"><span data-stu-id="112f1-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="112f1-124">(400,000 個訊息/天/單位)</span><span class="sxs-lookup"><span data-stu-id="112f1-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="112f1-125">S2</span><span class="sxs-lookup"><span data-stu-id="112f1-125">S2</span></span> |<span data-ttu-id="112f1-126">向上 too16 MB/每單位分鐘</span><span class="sxs-lookup"><span data-stu-id="112f1-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="112f1-127">(22.8 GB/天/單位)</span><span class="sxs-lookup"><span data-stu-id="112f1-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="112f1-128">每個單位平均 4,167 個訊息/分鐘</span><span class="sxs-lookup"><span data-stu-id="112f1-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="112f1-129">(600 萬個訊息/天/單位)</span><span class="sxs-lookup"><span data-stu-id="112f1-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="112f1-130">S3</span><span class="sxs-lookup"><span data-stu-id="112f1-130">S3</span></span> |<span data-ttu-id="112f1-131">向上 too814 MB/每單位分鐘</span><span class="sxs-lookup"><span data-stu-id="112f1-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="112f1-132">(1144.4 GB/天/單位)</span><span class="sxs-lookup"><span data-stu-id="112f1-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="112f1-133">每個單位平均 208,333 個訊息/分鐘</span><span class="sxs-lookup"><span data-stu-id="112f1-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="112f1-134">(3 億個訊息/天/單位)</span><span class="sxs-lookup"><span data-stu-id="112f1-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="112f1-135">身分識別登錄作業輸送量</span><span class="sxs-lookup"><span data-stu-id="112f1-135">Identity registry operation throughput</span></span>
<span data-ttu-id="112f1-136">IoT 中樞身分登錄作業不應 toobe 執行階段作業，因為它們通常是相關的 toodevice 佈建。</span><span class="sxs-lookup"><span data-stu-id="112f1-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="112f1-137">對於明顯暴增的效能數據，請參閱 [IoT 中樞配額和節流][IoT Hub quotas and throttles]。</span><span class="sxs-lookup"><span data-stu-id="112f1-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="112f1-138">分區化</span><span class="sxs-lookup"><span data-stu-id="112f1-138">Sharding</span></span>
<span data-ttu-id="112f1-139">雖然單一的 IoT 中樞可以調整 toomillions 的裝置，有時候您的方案需要特定的效能特性，單一的 IoT 中樞無法保證。</span><span class="sxs-lookup"><span data-stu-id="112f1-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="112f1-140">在此情況下，建議您將裝置分割成多個 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="112f1-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="112f1-141">多個 IoT 中樞 smooth 流量暴增，並取得 hello 必要的輸送量或所需的作業速率。</span><span class="sxs-lookup"><span data-stu-id="112f1-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="112f1-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="112f1-142">Next steps</span></span>
<span data-ttu-id="112f1-143">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="112f1-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="112f1-144">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="112f1-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="112f1-145">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="112f1-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
