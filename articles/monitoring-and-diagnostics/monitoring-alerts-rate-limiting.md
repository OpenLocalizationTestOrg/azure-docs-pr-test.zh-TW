---
title: "SMS、 電子郵件，及 webhook 限制 aaaRate |Microsoft 文件"
description: "了解 Azure 將可能 SMS、 電子郵件或 webhook 通知動作群組的 hello 數目的限制。"
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="db79b-103">SMS 訊息、電子郵件和 Webhook 文章的速率限制</span><span class="sxs-lookup"><span data-stu-id="db79b-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="db79b-104">速率限制是 tooa 特定電話號碼或電子郵件地址傳送太多的通知時所發生的擱置的通知。</span><span class="sxs-lookup"><span data-stu-id="db79b-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="db79b-105">速率限制可確保警示為可管理且可採取動作。</span><span class="sxs-lookup"><span data-stu-id="db79b-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="db79b-106">hello 規則 SMS 和電子郵件的 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="db79b-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="db79b-107">hello 速率上限臨界值是：</span><span class="sxs-lookup"><span data-stu-id="db79b-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="db79b-108">**SMS**：1 小時 10 個訊息。</span><span class="sxs-lookup"><span data-stu-id="db79b-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="db79b-109">**電子郵件**：1 小時 100 個訊息。</span><span class="sxs-lookup"><span data-stu-id="db79b-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="db79b-110">速率限制規則</span><span class="sxs-lookup"><span data-stu-id="db79b-110">Rate limit rules</span></span>
- <span data-ttu-id="db79b-111">特定的電話號碼或電子郵件是有限收到比 hello 臨界值所允許的多個訊息時的速率。</span><span class="sxs-lookup"><span data-stu-id="db79b-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="db79b-112">電話號碼或電子郵件可以是跨許多訂用帳戶動作群組的一部分。</span><span class="sxs-lookup"><span data-stu-id="db79b-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="db79b-113">速率限制適用於所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="db79b-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="db79b-114">它會套用一旦達到 hello 閾值時，即使從多個訂閱傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="db79b-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="db79b-115">電話號碼或電子郵件時速率限制的其他通知會傳送 toocommunicate hello 速率限制。</span><span class="sxs-lookup"><span data-stu-id="db79b-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="db79b-116">hello 狀態時 hello 速率限制的通知將會到期。</span><span class="sxs-lookup"><span data-stu-id="db79b-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="db79b-117">Webhook 的速率限制</span><span class="sxs-lookup"><span data-stu-id="db79b-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="db79b-118">沒有對 Webhook 的既有速率限制。</span><span class="sxs-lookup"><span data-stu-id="db79b-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db79b-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db79b-119">Next steps</span></span> ##
* <span data-ttu-id="db79b-120">進一步了解 [SMS 警示行為](monitoring-sms-alert-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="db79b-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="db79b-121">取得[活動記錄檔警示概觀](monitoring-overview-alerts.md)，並了解如何 tooreceive 警示。</span><span class="sxs-lookup"><span data-stu-id="db79b-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="db79b-122">了解如何太[設定警示，每當張貼服務健康情況通知](monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="db79b-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
