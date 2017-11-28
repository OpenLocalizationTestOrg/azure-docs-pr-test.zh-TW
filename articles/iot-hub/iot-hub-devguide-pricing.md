---
title: "了解 Azure IoT 中樞價格 | Microsoft Docs"
description: "開發人員指南 - IoT 中樞計量和計價方式的相關資訊，含實用範例。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: 3470473e1b2aa107c32643a66092b68bfafd1a37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-pricing-information"></a><span data-ttu-id="12d89-103">Azure IoT 中樞定價資訊</span><span class="sxs-lookup"><span data-stu-id="12d89-103">Azure IoT Hub pricing information</span></span>

<span data-ttu-id="12d89-104">[Azure IoT 中樞定價][lnk-pricing]提供關於 IoT 中樞之不同 SKU 和定價的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="12d89-104">[Azure IoT Hub pricing][lnk-pricing] provides the general information on different SKUs and pricing for IoT Hub.</span></span> <span data-ttu-id="12d89-105">本文包含 IoT 中樞如何以訊息的形式來針對各種 IoT 中樞功能進行計量的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="12d89-105">This article contains additional details on how the various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>

## <a name="charges-per-operation"></a><span data-ttu-id="12d89-106">每種作業的費用</span><span class="sxs-lookup"><span data-stu-id="12d89-106">Charges per operation</span></span>

| <span data-ttu-id="12d89-107">作業</span><span class="sxs-lookup"><span data-stu-id="12d89-107">Operation</span></span> | <span data-ttu-id="12d89-108">帳單資訊</span><span class="sxs-lookup"><span data-stu-id="12d89-108">Billing information</span></span> | 
| --------- | ------------------- |
| <span data-ttu-id="12d89-109">身分識別登錄作業</span><span class="sxs-lookup"><span data-stu-id="12d89-109">Identity registry operations</span></span> <br/> <span data-ttu-id="12d89-110">(建立、擷取、列出、更新、刪除)</span><span class="sxs-lookup"><span data-stu-id="12d89-110">(create, retrieve, list, update, delete)</span></span> | <span data-ttu-id="12d89-111">不收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-111">Not charged.</span></span> |
| <span data-ttu-id="12d89-112">裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="12d89-112">Device-to-cloud messages</span></span> | <span data-ttu-id="12d89-113">成功傳送的訊息會以輸入至 IoT 中樞的 4 KB 區塊為單位來收費，例如，6 KB 的訊息會收取 2 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="12d89-113">Successfully sent messages are charged in 4-KB chunks on ingress into IoT Hub, for example a 6-KB message is charged 2 messages.</span></span> |
| <span data-ttu-id="12d89-114">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="12d89-114">Cloud-to-device messages</span></span> | <span data-ttu-id="12d89-115">成功傳送的訊息會以 4 KB 區塊為單位來收費，例如，6 KB 的訊息會收取 2 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="12d89-115">Successfully sent messages are charged in 4-KB chunks, for example a 6-KB message is charged 2 messages.</span></span> |
| <span data-ttu-id="12d89-116">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="12d89-116">File uploads</span></span> | <span data-ttu-id="12d89-117">IoT 中樞不會針對傳輸至 Azure 儲存體的檔案進計量。</span><span class="sxs-lookup"><span data-stu-id="12d89-117">File transfer to Azure Storage is not metered by IoT Hub.</span></span> <span data-ttu-id="12d89-118">檔案傳輸的啟始和完成訊息會以每 4 KB 的增量方式來就訊息計量收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-118">File transfer initiation and completion messages are charged as messaged metered in 4-KB increments.</span></span> <span data-ttu-id="12d89-119">例如，傳輸 10 MB 的檔案，除了 Azure 儲存體的費用外，還會收取兩則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="12d89-119">For instance, transferring a 10-MB file is charged two messages in addition to the Azure Storage cost.</span></span> |
| <span data-ttu-id="12d89-120">直接方法</span><span class="sxs-lookup"><span data-stu-id="12d89-120">Direct methods</span></span> | <span data-ttu-id="12d89-121">成功的方法要求會以 4 KB 區塊為單位來收費，具有非空白內文的回應會視為額外的訊息以 4 KB 為單位收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-121">Successful method requests are charged in 4-KB chunks, responses with non-empty bodies are charged in 4-KB as additional messages.</span></span> <span data-ttu-id="12d89-122">針對已中斷連線之裝置所提出的要求會視為訊息以 4 KB 區塊為單位收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-122">Requests to disconnected devices are charged as messages in 4-KB chunks.</span></span> <span data-ttu-id="12d89-123">例如，具有 6 KB 內文的方法若導致裝置傳回沒有內文的回應，將會視為兩則訊息來收費；具有 6 KB 內文的方法若導致裝置傳回 1 KB 的回應，則會以要求視為兩則訊息外加回應視為另一則訊息的方式來收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-123">For instance, a method with a 6-KB body that results in a response with no body from the device, is charged as two messages; a method with a 6-KB body that results in a 1-KB response from the device is charged as two messages for the request plus another message for the response.</span></span> |
| <span data-ttu-id="12d89-124">裝置對應項讀取</span><span class="sxs-lookup"><span data-stu-id="12d89-124">Device twin reads</span></span> | <span data-ttu-id="12d89-125">來自裝置和解決方案後端的裝置對應項讀取是以 512 位元組區塊為單位的訊息來收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-125">Device twin reads from the device and from the solution back end are charged as messages in 512-byte chunks.</span></span> <span data-ttu-id="12d89-126">例如，讀取 6 KB 的裝置對應項會收取 12 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="12d89-126">For instance, reading a 6-KB device twin is charged as 12 messages.</span></span> |
| <span data-ttu-id="12d89-127">裝置對應項更新 (標籤和屬性)</span><span class="sxs-lookup"><span data-stu-id="12d89-127">Device twin updates (tags and properties)</span></span> | <span data-ttu-id="12d89-128">來自裝置和裝置的裝置對應項更新會視為訊息以 512 位元組的區塊為單位來收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-128">Device twin updates from the device and the device are charged as messages in 512-byte chunks.</span></span> <span data-ttu-id="12d89-129">例如，讀取 6 KB 的裝置對應項會收取 12 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="12d89-129">For instance, reading a 6-KB device twin is charged as 12 messages.</span></span> |
| <span data-ttu-id="12d89-130">裝置對應項查詢</span><span class="sxs-lookup"><span data-stu-id="12d89-130">Device twin queries</span></span> | <span data-ttu-id="12d89-131">查詢會依結果大小以 512 位元組的區塊為單位來收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-131">Queries are charged as messages depending on the result size in 512-byte chunks.</span></span> |
| <span data-ttu-id="12d89-132">作業的操作</span><span class="sxs-lookup"><span data-stu-id="12d89-132">Jobs operations</span></span> <br/> <span data-ttu-id="12d89-133">(建立、更新、列出、刪除)</span><span class="sxs-lookup"><span data-stu-id="12d89-133">(create, update, list, delete)</span></span> | <span data-ttu-id="12d89-134">不收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-134">Not charged.</span></span> |
| <span data-ttu-id="12d89-135">作業的每一裝置操作</span><span class="sxs-lookup"><span data-stu-id="12d89-135">Jobs per-device operations</span></span> | <span data-ttu-id="12d89-136">作業的操作 (例如裝置對應項更新和方法) 會按正常方式收費。</span><span class="sxs-lookup"><span data-stu-id="12d89-136">Jobs operations (such as device twin updates, and methods) are charged as normal.</span></span> <span data-ttu-id="12d89-137">例如，產生 1000 個含 1 KB 要求和空白內文回應之方法呼叫的作業，會收取 1000 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="12d89-137">For instance, a job resulting in 1000 method calls with 1-KB requests and empty-body responses is charged 1000 messages.</span></span> |

> [!NOTE]
> <span data-ttu-id="12d89-138">所有大小在計算時都會考量到以位元組為單位的承載大小 (通訊協定框架則會忽略)。</span><span class="sxs-lookup"><span data-stu-id="12d89-138">All sizes are computed considering the payload size in bytes (protocol framing is ignored).</span></span> <span data-ttu-id="12d89-139">若為訊息 (具有屬性和內文) 時，則會以不限通訊協定的方式計算大小，如 [IoT 中樞傳訊開發人員指南][lnk-message-size]所述。</span><span class="sxs-lookup"><span data-stu-id="12d89-139">In case of messages (which have properties and body) the size is computed in a protocol-agnostic way, as described in the [IoT Hub messaging developer's guide][lnk-message-size].</span></span>

## <a name="example-1"></a><span data-ttu-id="12d89-140">範例 #1</span><span class="sxs-lookup"><span data-stu-id="12d89-140">Example #1</span></span>

<span data-ttu-id="12d89-141">某裝置每分鐘會傳送一則 1 KB 的裝置到雲端訊息給 IoT 中樞，再由 Azure 串流分析讀取。</span><span class="sxs-lookup"><span data-stu-id="12d89-141">A device sends one 1-KB device-to-cloud message per minute to IoT Hub, which is then read by Azure Stream Analytics.</span></span> <span data-ttu-id="12d89-142">解決方案後端每十分鐘會在裝置上叫用方法 (具有 512 位元組的承載) 以觸發特定動作。</span><span class="sxs-lookup"><span data-stu-id="12d89-142">The solution back end invokes a method (with 512-byte payload) on the device every ten minutes to trigger a specific action.</span></span> <span data-ttu-id="12d89-143">裝置會對方法回應 200 位元組的結果。</span><span class="sxs-lookup"><span data-stu-id="12d89-143">The device responds to the method with a result of 200 bytes.</span></span>

<span data-ttu-id="12d89-144">裝置耗用 1 則訊息 * 60 分鐘 * 24 小時 = 每天 1440 則訊息 (裝置到雲端訊息的部分)，以及 2 個要求加回應 * 每小時 6 次 * 24 小時 = 288 則訊息 (方法的部分)，總計每天 1728 則訊息。</span><span class="sxs-lookup"><span data-stu-id="12d89-144">The device consumes 1 message * 60 minutes * 24 hours = 1440 messages per day for the device-to-cloud messages, and 2 request plus response * 6 times per hour * 24 hours = 288 messages for the methods, for a total of 1728 messages per day.</span></span>

## <a name="example-2"></a><span data-ttu-id="12d89-145">範例 2：</span><span class="sxs-lookup"><span data-stu-id="12d89-145">Example #2</span></span>

<span data-ttu-id="12d89-146">某裝置每小時傳送一則 100 KB 的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="12d89-146">A device sends one 100-KB device-to-cloud message every hour.</span></span> <span data-ttu-id="12d89-147">另外，每 4 小時還會以 1KB 的承載更新其裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="12d89-147">It also updates its device twin with 1-KB payloads every 4 hours.</span></span> <span data-ttu-id="12d89-148">解決方案後端每天讀取一次 14 KB 的裝置對應項，並以 512 位元組的承載來更新以變更設定。</span><span class="sxs-lookup"><span data-stu-id="12d89-148">The solution back end, once per day, reads the 14-KB device twin and updates it with 512-byte payloads to change configurations.</span></span>

<span data-ttu-id="12d89-149">裝置耗用 25 (100 KB/4 KB) 則訊息 * 24 小時 (裝置到雲端訊息的部分)，加上 1 則訊息 * 每天 6 次 (裝置對應項更新的部分)，總計每天 156 則訊息。</span><span class="sxs-lookup"><span data-stu-id="12d89-149">The device consumes 25 (100KB / 4KB) messages * 24 hours for device-to-cloud messages, plus 1 message * 6 times per day for device twin updates, for a total of 156 messages per day.</span></span>
<span data-ttu-id="12d89-150">解決方案後端耗用 28 則訊息 (14KB / 0.5KB) 來讀取裝置對應項，加上 1 則來更新它，總計 29 則訊息。</span><span class="sxs-lookup"><span data-stu-id="12d89-150">The solution back end consumes 28 messages (14KB / 0.5KB) to read the device twin, plus 1 message to update it, for a total of 29 messages.</span></span>

<span data-ttu-id="12d89-151">裝置和解決方案後端每天合計耗用 185 則訊息。</span><span class="sxs-lookup"><span data-stu-id="12d89-151">In total, the device and the solution back end consume 185 messages per day.</span></span>


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
