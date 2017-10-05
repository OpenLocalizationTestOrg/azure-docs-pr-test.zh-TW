---
title: "動作群組中的 SMS 警示行為 | Microsoft Docs"
description: "SMS 訊息格式和回應 SMS 訊息以取消訂閱、重新訂閱，或要求說明。"
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
ms.openlocfilehash: 3e4eca174209eeb9cbce1d45111d1e5cc30af8b0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="ac3c6-103">動作群組中的 SMS 警示行為</span><span class="sxs-lookup"><span data-stu-id="ac3c6-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="ac3c6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ac3c6-104">Overview</span></span> ##
<span data-ttu-id="ac3c6-105">動作群組可讓您設定接收者清單。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-105">Action groups enable you to configure a list of receivers.</span></span> <span data-ttu-id="ac3c6-106">然後這些群組就可在定義活動記錄警示時加以運用；確保觸發活動記錄警示時，特定的動作群組可以收到通知。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span></span> <span data-ttu-id="ac3c6-107">SMS 是其中一個可支援的警示機制；這些警示支援雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-107">One of the alerting mechanisms supported is SMS; the alerts support bi-directional communication.</span></span> <span data-ttu-id="ac3c6-108">使用者可回應警示以執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="ac3c6-108">A user can respond to an alert to:</span></span>

- <span data-ttu-id="ac3c6-109">**取消訂閱警示：**使用者可取消訂閱所有動作群組或單一動作群組的 SMS 警示。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="ac3c6-110">**重新訂閱警示：**使用者可重新訂閱所有動作群組或單一動作群組的 SMS 警示。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-110">**Resubscribe to alerts:** A user can resubscribe to all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="ac3c6-111">**要求說明︰**使用者可在 SMS 上要求其他資訊。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-111">**Request help:** A user can ask for more information on the SMS.</span></span> <span data-ttu-id="ac3c6-112">系統會將他們導向本文</span><span class="sxs-lookup"><span data-stu-id="ac3c6-112">They will be redirected to this article</span></span>

<span data-ttu-id="ac3c6-113">本文涵蓋 SMS 警示的行為，以及使用者可依據其所在位置採取的回應動作：</span><span class="sxs-lookup"><span data-stu-id="ac3c6-113">This article covers the behavior of the SMS alerts and the response actions the user can take based on the locale of the user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="ac3c6-114">美國/加拿大 SMS 行為</span><span class="sxs-lookup"><span data-stu-id="ac3c6-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="ac3c6-115">接收 SMS 警示</span><span class="sxs-lookup"><span data-stu-id="ac3c6-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="ac3c6-116">設定成動作群組一部分的 SMS 收件者，將會在警示啟動時收到 SMS。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="ac3c6-117">SMS 會傳達以下資訊：</span><span class="sxs-lookup"><span data-stu-id="ac3c6-117">The SMS will carry the following information:</span></span>
* <span data-ttu-id="ac3c6-118">會收到此警示的動作群組簡稱</span><span class="sxs-lookup"><span data-stu-id="ac3c6-118">Shortname of the action group this alert was sent to</span></span>
- <span data-ttu-id="ac3c6-119">警示的標題</span><span class="sxs-lookup"><span data-stu-id="ac3c6-119">Title of the alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="ac3c6-120">取消訂閱一個動作群組的 SMS 警示</span><span class="sxs-lookup"><span data-stu-id="ac3c6-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="ac3c6-121">如果使用者要從 SMS 取消一個動作群組的警示，可使用以下關鍵字來回應簡短代碼 20873："DISABLE &lt;動作群組的簡稱&gt;"。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-121">A user can unsubscribe from SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="ac3c6-122">例如</span><span class="sxs-lookup"><span data-stu-id="ac3c6-122">Ex.</span></span> <span data-ttu-id="ac3c6-123">使用者想取消訂閱簡稱為 "Azure" 的動作群組警示，則可傳送編寫 "DISABLE Azure" 的 SMS 至簡短代碼 20873</span><span class="sxs-lookup"><span data-stu-id="ac3c6-123">A user wishing to unsubscribe from alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="ac3c6-124">取消訂閱所有動作群組的 SMS 警示</span><span class="sxs-lookup"><span data-stu-id="ac3c6-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="ac3c6-125">如果使用者要取消所有動作群組的所 SMS 警示，可使用以下任一關鍵字來回應簡短代碼 20873：</span><span class="sxs-lookup"><span data-stu-id="ac3c6-125">A user can unsubscribe from all SMS alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="ac3c6-126">STOP</span><span class="sxs-lookup"><span data-stu-id="ac3c6-126">STOP</span></span>

<span data-ttu-id="ac3c6-127">例如</span><span class="sxs-lookup"><span data-stu-id="ac3c6-127">Ex.</span></span> <span data-ttu-id="ac3c6-128">使用者想取消訂閱所有動作群組的所有 SMS 警示，則可傳送編寫 "STOP" 的 SMS 至簡短代碼 20873</span><span class="sxs-lookup"><span data-stu-id="ac3c6-128">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="ac3c6-129">如果使用者已取消訂閱 SMS 警示，但又加入新的動作群組；則他們會接收到新動作群組的 SMS 警示，但對於所有之前的動作群組，仍是取消訂閱狀態。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-129">If a user has unsubscribed from SMS alerts, but is then added to a new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-to-sms-alerts-for-one-action-group"></a><span data-ttu-id="ac3c6-130">重新訂閱一個動作群組的 SMS 警示</span><span class="sxs-lookup"><span data-stu-id="ac3c6-130">Resubscribing to SMS alerts for one action group</span></span>
<span data-ttu-id="ac3c6-131">如果使用者要重新訂閱一個動作群組的 SMS 警示，可使用以下關鍵字來回應簡短代碼 20873："ENABLE &lt;動作群組的簡稱&gt;"。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-131">A user can resubscribe to SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="ac3c6-132">例如</span><span class="sxs-lookup"><span data-stu-id="ac3c6-132">Ex.</span></span> <span data-ttu-id="ac3c6-133">使用者想重新訂閱簡稱為 "Azure" 的動作群組警示，則可傳送編寫 "ENABLE Azure" 的 SMS 至簡短代碼 20873</span><span class="sxs-lookup"><span data-stu-id="ac3c6-133">A user wishing to resubscribe to alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-to-sms-alerts-for-all-action-groups"></a><span data-ttu-id="ac3c6-134">重新訂閱所有動作群組的 SMS 警示</span><span class="sxs-lookup"><span data-stu-id="ac3c6-134">Resubscribing to SMS alerts for all action groups</span></span>
<span data-ttu-id="ac3c6-135">如果使用者要重新訂閱所有動作群組的所有 SMS 警示，可使用以下任一關鍵字來回應簡短代碼 20873：</span><span class="sxs-lookup"><span data-stu-id="ac3c6-135">A user can resubscribe to all SMS for alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>

* <span data-ttu-id="ac3c6-136">START</span><span class="sxs-lookup"><span data-stu-id="ac3c6-136">START</span></span>

<span data-ttu-id="ac3c6-137">例如</span><span class="sxs-lookup"><span data-stu-id="ac3c6-137">Ex.</span></span> <span data-ttu-id="ac3c6-138">使用者想重新訂閱所有動作群組的所有 SMS 警示，則可傳送編寫 “START” 的 SMS 至簡短代碼 20873</span><span class="sxs-lookup"><span data-stu-id="ac3c6-138">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="ac3c6-139">透過 SMS 要求說明</span><span class="sxs-lookup"><span data-stu-id="ac3c6-139">Requesting help via SMS</span></span>
<span data-ttu-id="ac3c6-140">如果使用者要進一步了解他們收到的 SMS 訊息，可使用以下任一關鍵字來回應簡短代碼 20873：</span><span class="sxs-lookup"><span data-stu-id="ac3c6-140">A user can ask for more information about the SMS they have received by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="ac3c6-141">HELP</span><span class="sxs-lookup"><span data-stu-id="ac3c6-141">HELP</span></span>

<span data-ttu-id="ac3c6-142">使用者將會收到包含本文連結的回應。</span><span class="sxs-lookup"><span data-stu-id="ac3c6-142">A response will be sent to the user with a link to this article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac3c6-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac3c6-143">Next Steps</span></span>
<span data-ttu-id="ac3c6-144">取得[活動記錄警示的概觀](monitoring-overview-alerts.md)，並了解如何收到警示</span><span class="sxs-lookup"><span data-stu-id="ac3c6-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="ac3c6-145">深入了解 [SMS 速率限制](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="ac3c6-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="ac3c6-146">深入了解[動作群組](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="ac3c6-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
