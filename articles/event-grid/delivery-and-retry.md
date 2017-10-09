---
title: "aaaAzure 事件方格傳遞和重試"
description: "說明 Azure Event Grid 如何傳遞事件，以及如何處理未傳遞的訊息。"
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="60610-103">Event Grid 訊息傳遞與重試</span><span class="sxs-lookup"><span data-stu-id="60610-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="60610-104">本文章說明未確認傳遞時，Azure Event Grid 如何處理事件。</span><span class="sxs-lookup"><span data-stu-id="60610-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="60610-105">Event Grid 提供持久的傳遞。</span><span class="sxs-lookup"><span data-stu-id="60610-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="60610-106">它針對每個訂用帳戶傳遞每則訊息至少一次。</span><span class="sxs-lookup"><span data-stu-id="60610-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="60610-107">事件會立即傳送每個訂用帳戶註冊 toohello webhook。</span><span class="sxs-lookup"><span data-stu-id="60610-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="60610-108">如果 webhook 不會通知事件的回條 hello 第一次傳遞的 60 秒內嘗試，會重試傳送嗨事件的事件方格。</span><span class="sxs-lookup"><span data-stu-id="60610-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="60610-109">訊息傳遞狀態</span><span class="sxs-lookup"><span data-stu-id="60610-109">Message delivery status</span></span>

<span data-ttu-id="60610-110">事件方格會使用 HTTP 回應代碼 tooacknowledge 回條的事件。</span><span class="sxs-lookup"><span data-stu-id="60610-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="60610-111">成功碼</span><span class="sxs-lookup"><span data-stu-id="60610-111">Success codes</span></span>

<span data-ttu-id="60610-112">hello 下列 HTTP 回應碼表示，事件已傳送成功 tooyour webhook。</span><span class="sxs-lookup"><span data-stu-id="60610-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="60610-113">Event Grid 會將傳遞視為完成。</span><span class="sxs-lookup"><span data-stu-id="60610-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="60610-114">200 確定</span><span class="sxs-lookup"><span data-stu-id="60610-114">200 OK</span></span>
- <span data-ttu-id="60610-115">202 已接受</span><span class="sxs-lookup"><span data-stu-id="60610-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="60610-116">失敗碼</span><span class="sxs-lookup"><span data-stu-id="60610-116">Failure codes</span></span>

<span data-ttu-id="60610-117">hello 遵循 HTTP 回應碼指出事件傳遞嘗試失敗。</span><span class="sxs-lookup"><span data-stu-id="60610-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="60610-118">事件方格會再次嘗試 toosend hello 事件。</span><span class="sxs-lookup"><span data-stu-id="60610-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="60610-119">400 不正確的要求</span><span class="sxs-lookup"><span data-stu-id="60610-119">400 Bad Request</span></span>
- <span data-ttu-id="60610-120">401 未經授權</span><span class="sxs-lookup"><span data-stu-id="60610-120">401 Unauthorized</span></span>
- <span data-ttu-id="60610-121">404 找不到</span><span class="sxs-lookup"><span data-stu-id="60610-121">404 Not Found</span></span>
- <span data-ttu-id="60610-122">408 要求逾時</span><span class="sxs-lookup"><span data-stu-id="60610-122">408 Request timeout</span></span>
- <span data-ttu-id="60610-123">414 URI 太長</span><span class="sxs-lookup"><span data-stu-id="60610-123">414 URI Too Long</span></span>
- <span data-ttu-id="60610-124">500 內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="60610-124">500 Internal Server Error</span></span>
- <span data-ttu-id="60610-125">503 服務無法使用</span><span class="sxs-lookup"><span data-stu-id="60610-125">503 Service Unavailable</span></span>
- <span data-ttu-id="60610-126">504 閘道逾時</span><span class="sxs-lookup"><span data-stu-id="60610-126">504 Gateway Timeout</span></span>

<span data-ttu-id="60610-127">任何其他回應碼或回應缺少回應表示失敗。</span><span class="sxs-lookup"><span data-stu-id="60610-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="60610-128">Event Grid 會重試傳遞。</span><span class="sxs-lookup"><span data-stu-id="60610-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="60610-129">重試間隔</span><span class="sxs-lookup"><span data-stu-id="60610-129">Retry intervals</span></span>

<span data-ttu-id="60610-130">Event Grid 針對事件傳遞使用指數輪詢重試原則。</span><span class="sxs-lookup"><span data-stu-id="60610-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="60610-131">如果您的 webhook 沒有回應，或是傳回失敗碼，事件方格重試傳送嗨下列排程上：</span><span class="sxs-lookup"><span data-stu-id="60610-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="60610-132">10 秒</span><span class="sxs-lookup"><span data-stu-id="60610-132">10 seconds</span></span>
2. <span data-ttu-id="60610-133">30 秒</span><span class="sxs-lookup"><span data-stu-id="60610-133">30 seconds</span></span>
3. <span data-ttu-id="60610-134">1 分鐘</span><span class="sxs-lookup"><span data-stu-id="60610-134">1 minute</span></span>
4. <span data-ttu-id="60610-135">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="60610-135">5 minutes</span></span>
5. <span data-ttu-id="60610-136">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="60610-136">10 minutes</span></span>
6. <span data-ttu-id="60610-137">30 分鐘</span><span class="sxs-lookup"><span data-stu-id="60610-137">30 minutes</span></span>
7. <span data-ttu-id="60610-138">1 小時</span><span class="sxs-lookup"><span data-stu-id="60610-138">1 hour</span></span>

<span data-ttu-id="60610-139">事件方格將小型隨機 tooall 重試間隔。</span><span class="sxs-lookup"><span data-stu-id="60610-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="60610-140">重試持續時間</span><span class="sxs-lookup"><span data-stu-id="60610-140">Retry duration</span></span>

<span data-ttu-id="60610-141">Hello 在預覽期間，Azure 事件方格會到期，不會傳遞兩個小時內的所有事件。</span><span class="sxs-lookup"><span data-stu-id="60610-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="60610-142">之前上市時，這次將會增加的 too24 小時。</span><span class="sxs-lookup"><span data-stu-id="60610-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="60610-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60610-143">Next steps</span></span>

* <span data-ttu-id="60610-144">如簡介 tooEvent 格線，請參閱[有關事件方格](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="60610-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="60610-145">使用事件方格啟動 tooquickly，請參閱[建立和路由的自訂事件，與 Azure 事件方格](custom-event-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="60610-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
