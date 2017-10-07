---
title: "動作群組在 aaaSMS 警示行為 |Microsoft 文件"
description: "SMS 訊息格式和回應 tooSMS 訊息 toounsubscribe，重新訂閱或要求協助。"
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
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="99524-103">動作群組中的 SMS 警示行為</span><span class="sxs-lookup"><span data-stu-id="99524-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="99524-104">概觀</span><span class="sxs-lookup"><span data-stu-id="99524-104">Overview</span></span> ##
<span data-ttu-id="99524-105">動作群組可讓您 tooconfigure 接收器的清單。</span><span class="sxs-lookup"><span data-stu-id="99524-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="99524-106">定義活動記錄檔的警示; 時，可以再運用這些群組確保特定的動作群組在 hello 活動記錄在警示觸發時收到通知。</span><span class="sxs-lookup"><span data-stu-id="99524-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="99524-107">Hello 警示機制支援的其中一個是 SMS;hello 警示支援雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="99524-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="99524-108">使用者可以回應 tooan 警示：</span><span class="sxs-lookup"><span data-stu-id="99524-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="99524-109">**取消訂閱警示：**使用者可取消訂閱所有動作群組或單一動作群組的 SMS 警示。</span><span class="sxs-lookup"><span data-stu-id="99524-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="99524-110">**重新訂閱 tooalerts:**使用者可以重新訂閱 tooall SMS 警示的所有動作群組或設為單數動作群組。</span><span class="sxs-lookup"><span data-stu-id="99524-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="99524-111">**要求協助：**使用者可以要求在 hello SMS 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="99524-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="99524-112">將其重新導向的 toothis 發行項</span><span class="sxs-lookup"><span data-stu-id="99524-112">They will be redirected toothis article</span></span>

<span data-ttu-id="99524-113">本文件涵蓋的 hello SMS 警示 hello 行為和 hello 回應動作 hello 使用者可以根據進行 hello hello 使用者地區設定：</span><span class="sxs-lookup"><span data-stu-id="99524-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="99524-114">美國/加拿大 SMS 行為</span><span class="sxs-lookup"><span data-stu-id="99524-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="99524-115">接收 SMS 警示</span><span class="sxs-lookup"><span data-stu-id="99524-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="99524-116">設定成動作群組一部分的 SMS 收件者，將會在警示啟動時收到 SMS。</span><span class="sxs-lookup"><span data-stu-id="99524-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="99524-117">hello SMS 對於將執行 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="99524-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="99524-118">此警示已傳送至 hello 動作群組的簡短名稱</span><span class="sxs-lookup"><span data-stu-id="99524-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="99524-119">Hello 警示的標題</span><span class="sxs-lookup"><span data-stu-id="99524-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="99524-120">取消訂閱一個動作群組的 SMS 警示</span><span class="sxs-lookup"><span data-stu-id="99524-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="99524-121">使用者可以取消訂閱 SMS 一個動作群組的警示所回應 toohello shortcode 20873 與 hello 關鍵字: 「 停用&lt;動作群組的簡短名稱&gt;"。</span><span class="sxs-lookup"><span data-stu-id="99524-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="99524-122">例如</span><span class="sxs-lookup"><span data-stu-id="99524-122">Ex.</span></span> <span data-ttu-id="99524-123">使用者希望 toounsubscribe 從與 hello shortname"Azure"，動作群組的警示就會傳送 SMS toohello shortcode 20873，指出 「 停用 Azure 」</span><span class="sxs-lookup"><span data-stu-id="99524-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="99524-124">取消訂閱所有動作群組的 SMS 警示</span><span class="sxs-lookup"><span data-stu-id="99524-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="99524-125">使用者可以取消訂閱的所有動作群組的所有 SMS 警示由回應 toohello shortcode 20873 與任何的 hello 下列關鍵字：</span><span class="sxs-lookup"><span data-stu-id="99524-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="99524-126">STOP</span><span class="sxs-lookup"><span data-stu-id="99524-126">STOP</span></span>

<span data-ttu-id="99524-127">例如</span><span class="sxs-lookup"><span data-stu-id="99524-127">Ex.</span></span> <span data-ttu-id="99524-128">使用者希望 toounsubscribe 從所有的動作群組的所有 SMS 警示就會傳送 SMS toohello shortcode 20873，指出 「 停止 」</span><span class="sxs-lookup"><span data-stu-id="99524-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="99524-129">如果使用者已取消訂用 SMS 發出警示通知，但接著會加入新的動作群組 tooa;這些接收 SMS 警示，該新的動作群組，但仍未訂閱的所有先前的動作群組。</span><span class="sxs-lookup"><span data-stu-id="99524-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="99524-130">有一個動作群組的 resubscribing tooSMS 警示</span><span class="sxs-lookup"><span data-stu-id="99524-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="99524-131">使用者可以重新 tooSMS 一個動作群組的警示訂閱的回應 toohello shortcode 20873 與 hello 關鍵字: 「 啟用&lt;動作群組的簡短名稱&gt;"。</span><span class="sxs-lookup"><span data-stu-id="99524-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="99524-132">例如</span><span class="sxs-lookup"><span data-stu-id="99524-132">Ex.</span></span> <span data-ttu-id="99524-133">希望 tooresubscribe tooalerts hello shortname"Azure"，動作群組的使用者就會傳送 SMS toohello shortcode 20873，指出 「 啟用 Azure 」</span><span class="sxs-lookup"><span data-stu-id="99524-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="99524-134">所有的動作群組的 resubscribing tooSMS 警示</span><span class="sxs-lookup"><span data-stu-id="99524-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="99524-135">使用者可以重新 tooall SMS 警示適用於所有的動作群組的訂閱所回應 toohello shortcode 20873 與任何的 hello 下列關鍵字：</span><span class="sxs-lookup"><span data-stu-id="99524-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="99524-136">START</span><span class="sxs-lookup"><span data-stu-id="99524-136">START</span></span>

<span data-ttu-id="99524-137">例如</span><span class="sxs-lookup"><span data-stu-id="99524-137">Ex.</span></span> <span data-ttu-id="99524-138">使用者希望 toounsubscribe 從所有的動作群組的所有 SMS 警示就會傳送 SMS toohello shortcode 20873，指出 「 啟動 」</span><span class="sxs-lookup"><span data-stu-id="99524-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="99524-139">透過 SMS 要求說明</span><span class="sxs-lookup"><span data-stu-id="99524-139">Requesting help via SMS</span></span>
<span data-ttu-id="99524-140">使用者可以要求 hello SMS 的詳細資訊均已接收回應 toohello shortcode 20873 與任何 hello 下列關鍵字：</span><span class="sxs-lookup"><span data-stu-id="99524-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="99524-141">HELP</span><span class="sxs-lookup"><span data-stu-id="99524-141">HELP</span></span>

<span data-ttu-id="99524-142">Toohello 搭配連結 toothis 發行項的使用者會傳送回應。</span><span class="sxs-lookup"><span data-stu-id="99524-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99524-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99524-143">Next Steps</span></span>
<span data-ttu-id="99524-144">取得[活動記錄檔警示概觀](monitoring-overview-alerts.md)並了解如何 tooget 警示</span><span class="sxs-lookup"><span data-stu-id="99524-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="99524-145">深入了解 [SMS 速率限制](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="99524-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="99524-146">深入了解[動作群組](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="99524-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
