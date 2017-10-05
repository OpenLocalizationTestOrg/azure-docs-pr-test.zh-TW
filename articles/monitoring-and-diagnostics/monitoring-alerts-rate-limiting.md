---
title: "SMS、電子郵件和 Webhook 的速率限制 | Microsoft Docs"
description: "了解 Azure 如何限制可能來自動作群組的 SMS、電子郵件或 Webhook 通知數目。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: bde645624ab1860d19ba18470f55845855a7d1fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="1f888-103">SMS 訊息、電子郵件和 Webhook 文章的速率限制</span><span class="sxs-lookup"><span data-stu-id="1f888-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="1f888-104">速率限制是當傳送了太多通知給特定電話號碼或電子郵件地址時所發生的通知暫停。</span><span class="sxs-lookup"><span data-stu-id="1f888-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent to a particular phone number or email address.</span></span> <span data-ttu-id="1f888-105">速率限制可確保警示為可管理且可採取動作。</span><span class="sxs-lookup"><span data-stu-id="1f888-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="1f888-106">SMS 和電子郵件的規則相同。</span><span class="sxs-lookup"><span data-stu-id="1f888-106">The rules for SMS and email are the same.</span></span> <span data-ttu-id="1f888-107">以下項目的速率限制閾值：</span><span class="sxs-lookup"><span data-stu-id="1f888-107">The rate limit threshold is:</span></span>

 - <span data-ttu-id="1f888-108">**SMS**：1 小時 10 個訊息。</span><span class="sxs-lookup"><span data-stu-id="1f888-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="1f888-109">**電子郵件**：1 小時 100 個訊息。</span><span class="sxs-lookup"><span data-stu-id="1f888-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="1f888-110">速率限制規則</span><span class="sxs-lookup"><span data-stu-id="1f888-110">Rate limit rules</span></span>
- <span data-ttu-id="1f888-111">當特定電話號碼或電子郵件收到的訊息超過閾值允許數量時，會受到速率限制。</span><span class="sxs-lookup"><span data-stu-id="1f888-111">A particular phone number or email is rate limited when it receives more messages than the threshold allows.</span></span>
- <span data-ttu-id="1f888-112">電話號碼或電子郵件可以是跨許多訂用帳戶動作群組的一部分。</span><span class="sxs-lookup"><span data-stu-id="1f888-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="1f888-113">速率限制適用於所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1f888-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="1f888-114">它適用於觸達閾值時，即使是從多個訂用帳戶傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="1f888-114">It applies as soon as the threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="1f888-115">當電話號碼或電子郵件受到速率限制時，將會傳送另一個通知來溝通速率限制。</span><span class="sxs-lookup"><span data-stu-id="1f888-115">When a phone number or email is rate limited, an additional notification is sent to communicate the rate limiting.</span></span> <span data-ttu-id="1f888-116">通知會說明速率限制到期的時間。</span><span class="sxs-lookup"><span data-stu-id="1f888-116">The notification states when the rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="1f888-117">Webhook 的速率限制</span><span class="sxs-lookup"><span data-stu-id="1f888-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="1f888-118">沒有對 Webhook 的既有速率限制。</span><span class="sxs-lookup"><span data-stu-id="1f888-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f888-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f888-119">Next steps</span></span> ##
* <span data-ttu-id="1f888-120">進一步了解 [SMS 警示行為](monitoring-sms-alert-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="1f888-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="1f888-121">取得[活動記錄警示的概觀](monitoring-overview-alerts.md)，並了解如何收到警示。</span><span class="sxs-lookup"><span data-stu-id="1f888-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="1f888-122">了解如何[設定每當服務健康狀態通知公佈時的警示](monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="1f888-122">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
