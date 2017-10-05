---
title: "Azure IoT 中樞調整 | Microsoft Docs"
description: "如何調整 IoT 中樞以支援您預期的訊息輸送量。 包含每個層級支援的輸送量和分區化選項的摘要。"
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
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="8e344-104">調整您的 IoT 中樞解決方案</span><span class="sxs-lookup"><span data-stu-id="8e344-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="8e344-105">Azure IoT 中樞最多可支援百萬個同時連線的裝置。</span><span class="sxs-lookup"><span data-stu-id="8e344-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="8e344-106">如需詳細資訊，請參閱 [IoT 中樞價格][lnk-pricing]。</span><span class="sxs-lookup"><span data-stu-id="8e344-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="8e344-107">每個 IoT 中樞單位允許一定數量的每日訊息。</span><span class="sxs-lookup"><span data-stu-id="8e344-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="8e344-108">為了適當調整您的解決方案，您必須考慮 IoT 中樞的特定使用方式。</span><span class="sxs-lookup"><span data-stu-id="8e344-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="8e344-109">尤其要考慮以下類別的作業所需的尖峰輸送量：</span><span class="sxs-lookup"><span data-stu-id="8e344-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="8e344-110">裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="8e344-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="8e344-111">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="8e344-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="8e344-112">身分識別登錄作業</span><span class="sxs-lookup"><span data-stu-id="8e344-112">Identity registry operations</span></span>

<span data-ttu-id="8e344-113">除了此輸送量資訊，請參閱 [IoT 中樞配額和節流][IoT Hub quotas and throttles]，並據以設計您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="8e344-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="8e344-114">裝置到雲端及雲端到裝置訊息輸送量</span><span class="sxs-lookup"><span data-stu-id="8e344-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="8e344-115">若要評估每個單位的流量，最佳方式為調整 IoT 中樞解決方案的大小。</span><span class="sxs-lookup"><span data-stu-id="8e344-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="8e344-116">裝置到雲端訊息會遵循這些持續的輸送量指導方針。</span><span class="sxs-lookup"><span data-stu-id="8e344-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="8e344-117">層</span><span class="sxs-lookup"><span data-stu-id="8e344-117">Tier</span></span> | <span data-ttu-id="8e344-118">持續的輸送量</span><span class="sxs-lookup"><span data-stu-id="8e344-118">Sustained throughput</span></span> | <span data-ttu-id="8e344-119">持續的傳送速率</span><span class="sxs-lookup"><span data-stu-id="8e344-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e344-120">S1</span><span class="sxs-lookup"><span data-stu-id="8e344-120">S1</span></span> |<span data-ttu-id="8e344-121">每個單位最多 1111 KB/分鐘</span><span class="sxs-lookup"><span data-stu-id="8e344-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="8e344-122">(1.5 GB/天/單位)</span><span class="sxs-lookup"><span data-stu-id="8e344-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="8e344-123">每個單位平均 278 個訊息/分鐘</span><span class="sxs-lookup"><span data-stu-id="8e344-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="8e344-124">(400,000 個訊息/天/單位)</span><span class="sxs-lookup"><span data-stu-id="8e344-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="8e344-125">S2</span><span class="sxs-lookup"><span data-stu-id="8e344-125">S2</span></span> |<span data-ttu-id="8e344-126">每個單位最多 16 MB/分鐘</span><span class="sxs-lookup"><span data-stu-id="8e344-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="8e344-127">(22.8 GB/天/單位)</span><span class="sxs-lookup"><span data-stu-id="8e344-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="8e344-128">每個單位平均 4,167 個訊息/分鐘</span><span class="sxs-lookup"><span data-stu-id="8e344-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="8e344-129">(600 萬個訊息/天/單位)</span><span class="sxs-lookup"><span data-stu-id="8e344-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="8e344-130">S3</span><span class="sxs-lookup"><span data-stu-id="8e344-130">S3</span></span> |<span data-ttu-id="8e344-131">每個單位最多 814 MB/分鐘</span><span class="sxs-lookup"><span data-stu-id="8e344-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="8e344-132">(1144.4 GB/天/單位)</span><span class="sxs-lookup"><span data-stu-id="8e344-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="8e344-133">每個單位平均 208,333 個訊息/分鐘</span><span class="sxs-lookup"><span data-stu-id="8e344-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="8e344-134">(3 億個訊息/天/單位)</span><span class="sxs-lookup"><span data-stu-id="8e344-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="8e344-135">身分識別登錄作業輸送量</span><span class="sxs-lookup"><span data-stu-id="8e344-135">Identity registry operation throughput</span></span>
<span data-ttu-id="8e344-136">大部分的 IoT 中樞識別登錄作業都與裝置佈建有關，應該都不是執行階段作業。</span><span class="sxs-lookup"><span data-stu-id="8e344-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="8e344-137">對於明顯暴增的效能數據，請參閱 [IoT 中樞配額和節流][IoT Hub quotas and throttles]。</span><span class="sxs-lookup"><span data-stu-id="8e344-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="8e344-138">分區化</span><span class="sxs-lookup"><span data-stu-id="8e344-138">Sharding</span></span>
<span data-ttu-id="8e344-139">雖然單一 IoT 中樞可以擴充到數百萬個裝置，但有時候您的解決方案需要單一 IoT 中樞無法保證的特定效能特性。</span><span class="sxs-lookup"><span data-stu-id="8e344-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="8e344-140">在此情況下，建議您將裝置分割成多個 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8e344-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="8e344-141">多個 IoT 中心可減緩資料傳輸量暴增，並取得所需的輸送量或作業速率。</span><span class="sxs-lookup"><span data-stu-id="8e344-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e344-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e344-142">Next steps</span></span>
<span data-ttu-id="8e344-143">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="8e344-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8e344-144">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="8e344-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="8e344-145">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8e344-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
