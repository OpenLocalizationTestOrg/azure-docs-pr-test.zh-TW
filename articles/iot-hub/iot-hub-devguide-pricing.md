---
title: "aaaUnderstand Azure IoT 中樞定價 |Microsoft 文件"
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
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a><span data-ttu-id="8232d-103">Azure IoT 中樞定價資訊</span><span class="sxs-lookup"><span data-stu-id="8232d-103">Azure IoT Hub pricing information</span></span>

<span data-ttu-id="8232d-104">[Azure IoT 中樞定價][ lnk-pricing]提供不同的 Sku 和價格的 IoT 中樞 hello 一般資訊。</span><span class="sxs-lookup"><span data-stu-id="8232d-104">[Azure IoT Hub pricing][lnk-pricing] provides hello general information on different SKUs and pricing for IoT Hub.</span></span> <span data-ttu-id="8232d-105">本文章包含如何為計量 IoT 中樞的各種不同功能的 hello 訊息進行 IoT 中樞的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8232d-105">This article contains additional details on how hello various IoT Hub functionalities are metered as messages by IoT Hub.</span></span>

## <a name="charges-per-operation"></a><span data-ttu-id="8232d-106">每種作業的費用</span><span class="sxs-lookup"><span data-stu-id="8232d-106">Charges per operation</span></span>

| <span data-ttu-id="8232d-107">作業</span><span class="sxs-lookup"><span data-stu-id="8232d-107">Operation</span></span> | <span data-ttu-id="8232d-108">帳單資訊</span><span class="sxs-lookup"><span data-stu-id="8232d-108">Billing information</span></span> | 
| --------- | ------------------- |
| <span data-ttu-id="8232d-109">身分識別登錄作業</span><span class="sxs-lookup"><span data-stu-id="8232d-109">Identity registry operations</span></span> <br/> <span data-ttu-id="8232d-110">(建立、擷取、列出、更新、刪除)</span><span class="sxs-lookup"><span data-stu-id="8232d-110">(create, retrieve, list, update, delete)</span></span> | <span data-ttu-id="8232d-111">不收費。</span><span class="sxs-lookup"><span data-stu-id="8232d-111">Not charged.</span></span> |
| <span data-ttu-id="8232d-112">裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="8232d-112">Device-to-cloud messages</span></span> | <span data-ttu-id="8232d-113">成功傳送的訊息會以輸入至 IoT 中樞的 4 KB 區塊為單位來收費，例如，6 KB 的訊息會收取 2 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="8232d-113">Successfully sent messages are charged in 4-KB chunks on ingress into IoT Hub, for example a 6-KB message is charged 2 messages.</span></span> |
| <span data-ttu-id="8232d-114">雲端到裝置的訊息</span><span class="sxs-lookup"><span data-stu-id="8232d-114">Cloud-to-device messages</span></span> | <span data-ttu-id="8232d-115">成功傳送的訊息會以 4 KB 區塊為單位來收費，例如，6 KB 的訊息會收取 2 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="8232d-115">Successfully sent messages are charged in 4-KB chunks, for example a 6-KB message is charged 2 messages.</span></span> |
| <span data-ttu-id="8232d-116">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="8232d-116">File uploads</span></span> | <span data-ttu-id="8232d-117">檔案傳輸 tooAzure IoT 中樞不計量存放區。</span><span class="sxs-lookup"><span data-stu-id="8232d-117">File transfer tooAzure Storage is not metered by IoT Hub.</span></span> <span data-ttu-id="8232d-118">檔案傳輸的啟始和完成訊息會以每 4 KB 的增量方式來就訊息計量收費。</span><span class="sxs-lookup"><span data-stu-id="8232d-118">File transfer initiation and completion messages are charged as messaged metered in 4-KB increments.</span></span> <span data-ttu-id="8232d-119">比方說，以便傳輸 10 MB 的檔案會負責在加法 toohello 成本的 Azure 儲存體中的兩個訊息。</span><span class="sxs-lookup"><span data-stu-id="8232d-119">For instance, transferring a 10-MB file is charged two messages in addition toohello Azure Storage cost.</span></span> |
| <span data-ttu-id="8232d-120">直接方法</span><span class="sxs-lookup"><span data-stu-id="8232d-120">Direct methods</span></span> | <span data-ttu-id="8232d-121">成功的方法要求會以 4 KB 區塊為單位來收費，具有非空白內文的回應會視為額外的訊息以 4 KB 為單位收費。</span><span class="sxs-lookup"><span data-stu-id="8232d-121">Successful method requests are charged in 4-KB chunks, responses with non-empty bodies are charged in 4-KB as additional messages.</span></span> <span data-ttu-id="8232d-122">要求 toodisconnected 裝置會以 4 KB 區塊 （chunk） 的訊息收費。</span><span class="sxs-lookup"><span data-stu-id="8232d-122">Requests toodisconnected devices are charged as messages in 4-KB chunks.</span></span> <span data-ttu-id="8232d-123">比方說，具有 hello 裝置沒有主體之回應中會產生 6 KB 主體的方法會產生費用視為兩則訊息。具有 1 KB 回應 hello 裝置會產生 6 KB 主體的方法會負責為 hello 要求兩個訊息加上另一個 hello 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="8232d-123">For instance, a method with a 6-KB body that results in a response with no body from hello device, is charged as two messages; a method with a 6-KB body that results in a 1-KB response from hello device is charged as two messages for hello request plus another message for hello response.</span></span> |
| <span data-ttu-id="8232d-124">裝置對應項讀取</span><span class="sxs-lookup"><span data-stu-id="8232d-124">Device twin reads</span></span> | <span data-ttu-id="8232d-125">裝置的兩個讀取從 hello 的裝置，並從上一步 hello 方案結束時才會收費為 512 位元組的區塊中的訊息。</span><span class="sxs-lookup"><span data-stu-id="8232d-125">Device twin reads from hello device and from hello solution back end are charged as messages in 512-byte chunks.</span></span> <span data-ttu-id="8232d-126">例如，讀取 6 KB 的裝置對應項會收取 12 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="8232d-126">For instance, reading a 6-KB device twin is charged as 12 messages.</span></span> |
| <span data-ttu-id="8232d-127">裝置對應項更新 (標籤和屬性)</span><span class="sxs-lookup"><span data-stu-id="8232d-127">Device twin updates (tags and properties)</span></span> | <span data-ttu-id="8232d-128">裝置 hello 裝置與 hello 裝置的兩個更新會為 512 位元組的區塊中的訊息收費。</span><span class="sxs-lookup"><span data-stu-id="8232d-128">Device twin updates from hello device and hello device are charged as messages in 512-byte chunks.</span></span> <span data-ttu-id="8232d-129">例如，讀取 6 KB 的裝置對應項會收取 12 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="8232d-129">For instance, reading a 6-KB device twin is charged as 12 messages.</span></span> |
| <span data-ttu-id="8232d-130">裝置對應項查詢</span><span class="sxs-lookup"><span data-stu-id="8232d-130">Device twin queries</span></span> | <span data-ttu-id="8232d-131">查詢會為 512 位元組的區塊中的 hello 結果大小而定的訊息收費。</span><span class="sxs-lookup"><span data-stu-id="8232d-131">Queries are charged as messages depending on hello result size in 512-byte chunks.</span></span> |
| <span data-ttu-id="8232d-132">作業的操作</span><span class="sxs-lookup"><span data-stu-id="8232d-132">Jobs operations</span></span> <br/> <span data-ttu-id="8232d-133">(建立、更新、列出、刪除)</span><span class="sxs-lookup"><span data-stu-id="8232d-133">(create, update, list, delete)</span></span> | <span data-ttu-id="8232d-134">不收費。</span><span class="sxs-lookup"><span data-stu-id="8232d-134">Not charged.</span></span> |
| <span data-ttu-id="8232d-135">作業的每一裝置操作</span><span class="sxs-lookup"><span data-stu-id="8232d-135">Jobs per-device operations</span></span> | <span data-ttu-id="8232d-136">作業的操作 (例如裝置對應項更新和方法) 會按正常方式收費。</span><span class="sxs-lookup"><span data-stu-id="8232d-136">Jobs operations (such as device twin updates, and methods) are charged as normal.</span></span> <span data-ttu-id="8232d-137">例如，產生 1000 個含 1 KB 要求和空白內文回應之方法呼叫的作業，會收取 1000 則訊息的費用。</span><span class="sxs-lookup"><span data-stu-id="8232d-137">For instance, a job resulting in 1000 method calls with 1-KB requests and empty-body responses is charged 1000 messages.</span></span> |

> [!NOTE]
> <span data-ttu-id="8232d-138">所有大小則會都計算考慮 hello 承載大小，以位元組為單位 （通訊協定框架會被忽略）。</span><span class="sxs-lookup"><span data-stu-id="8232d-138">All sizes are computed considering hello payload size in bytes (protocol framing is ignored).</span></span> <span data-ttu-id="8232d-139">如果訊息 （其中的屬性和內文） hello 大小的計算通訊協定無關的方式，hello 中所述[傳訊開發人員指南的 IoT 中樞][lnk-message-size]。</span><span class="sxs-lookup"><span data-stu-id="8232d-139">In case of messages (which have properties and body) hello size is computed in a protocol-agnostic way, as described in hello [IoT Hub messaging developer's guide][lnk-message-size].</span></span>

## <a name="example-1"></a><span data-ttu-id="8232d-140">範例 #1</span><span class="sxs-lookup"><span data-stu-id="8232d-140">Example #1</span></span>

<span data-ttu-id="8232d-141">裝置會傳送一個 1 KB 的裝置到雲端訊息每分鐘 tooIoT 集線器，然後讀取 Azure Stream analytics。</span><span class="sxs-lookup"><span data-stu-id="8232d-141">A device sends one 1-KB device-to-cloud message per minute tooIoT Hub, which is then read by Azure Stream Analytics.</span></span> <span data-ttu-id="8232d-142">hello 方案後端叫用方法 （具有 512 位元組裝載） hello 裝置上每十分鐘 tootrigger 特定動作。</span><span class="sxs-lookup"><span data-stu-id="8232d-142">hello solution back end invokes a method (with 512-byte payload) on hello device every ten minutes tootrigger a specific action.</span></span> <span data-ttu-id="8232d-143">hello 裝置會回應 200 個位元組的結果 toohello 方法。</span><span class="sxs-lookup"><span data-stu-id="8232d-143">hello device responds toohello method with a result of 200 bytes.</span></span>

<span data-ttu-id="8232d-144">hello 裝置消耗 1 則訊息 * 60 分鐘 * 24 小時 = 1440年每天 hello 裝置到雲端訊息，以及 2 要求加上回應的訊息 * 6 次每小時 * 24 小時 = 288 訊息 hello 方法，每日 1728年訊息總數。</span><span class="sxs-lookup"><span data-stu-id="8232d-144">hello device consumes 1 message * 60 minutes * 24 hours = 1440 messages per day for hello device-to-cloud messages, and 2 request plus response * 6 times per hour * 24 hours = 288 messages for hello methods, for a total of 1728 messages per day.</span></span>

## <a name="example-2"></a><span data-ttu-id="8232d-145">範例 2：</span><span class="sxs-lookup"><span data-stu-id="8232d-145">Example #2</span></span>

<span data-ttu-id="8232d-146">某裝置每小時傳送一則 100 KB 的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="8232d-146">A device sends one 100-KB device-to-cloud message every hour.</span></span> <span data-ttu-id="8232d-147">另外，每 4 小時還會以 1KB 的承載更新其裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="8232d-147">It also updates its device twin with 1-KB payloads every 4 hours.</span></span> <span data-ttu-id="8232d-148">hello 解決方案回每天一次，結束讀取 hello 14 KB 裝置兩個，並更新它的 512 位元組裝載 toochange 組態。</span><span class="sxs-lookup"><span data-stu-id="8232d-148">hello solution back end, once per day, reads hello 14-KB device twin and updates it with 512-byte payloads toochange configurations.</span></span>

<span data-ttu-id="8232d-149">hello 裝置消耗 25 (100 KB/4 KB) 的訊息 * 24 小時，讓裝置到雲端訊息加上 1 則訊息 * 6 次每天裝置的兩個更新，針對每日 156 訊息總數。</span><span class="sxs-lookup"><span data-stu-id="8232d-149">hello device consumes 25 (100KB / 4KB) messages * 24 hours for device-to-cloud messages, plus 1 message * 6 times per day for device twin updates, for a total of 156 messages per day.</span></span>
<span data-ttu-id="8232d-150">hello 方案後端取用 28 訊息 (14 KB/0.5 KB) tooread hello 裝置兩個，加上 1 訊息 tooupdate 它 29 訊息總數。</span><span class="sxs-lookup"><span data-stu-id="8232d-150">hello solution back end consumes 28 messages (14KB / 0.5KB) tooread hello device twin, plus 1 message tooupdate it, for a total of 29 messages.</span></span>

<span data-ttu-id="8232d-151">總共 hello 裝置和 hello 方案後端取用 185 每天的訊息。</span><span class="sxs-lookup"><span data-stu-id="8232d-151">In total, hello device and hello solution back end consume 185 messages per day.</span></span>


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
