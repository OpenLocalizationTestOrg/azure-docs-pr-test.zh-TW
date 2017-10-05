---
title: "接收服務通知的活動記錄警示 | Microsoft Docs"
description: "在 Azure 服務發生時透過 SMS、電子郵件或 Webhook 獲得通知。"
author: johnkemnetz
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
ms.author: johnkem
ms.openlocfilehash: bf6a98fd7e7e11764bef174f9efd0635fa7efe9a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="16640-103">建立服務通知的活動記錄警示</span><span class="sxs-lookup"><span data-stu-id="16640-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="16640-104">概觀</span><span class="sxs-lookup"><span data-stu-id="16640-104">Overview</span></span>
<span data-ttu-id="16640-105">本文將說明如何使用 Azure 入口網站為服務健康情況通知設定活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="16640-105">This article shows you how to set up activity log alerts for service health notifications by using the Azure portal.</span></span>  

<span data-ttu-id="16640-106">您可以在 Azure 傳送服務健康狀態通知到您的 Azure 訂用帳戶時接收警示。</span><span class="sxs-lookup"><span data-stu-id="16640-106">You can receive an alert when Azure sends service health notifications to your Azure subscription.</span></span> <span data-ttu-id="16640-107">您可以針對下列設定警示：</span><span class="sxs-lookup"><span data-stu-id="16640-107">You can configure the alert based on:</span></span>

- <span data-ttu-id="16640-108">服務健康情況通知的類別 (事件、維護、資訊等)。</span><span class="sxs-lookup"><span data-stu-id="16640-108">The class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="16640-109">受影響的服務。</span><span class="sxs-lookup"><span data-stu-id="16640-109">The service(s) affected.</span></span>
- <span data-ttu-id="16640-110">受影響的區域。</span><span class="sxs-lookup"><span data-stu-id="16640-110">The region(s) affected.</span></span>
- <span data-ttu-id="16640-111">通知的狀態 (使用中與已解決)。</span><span class="sxs-lookup"><span data-stu-id="16640-111">The status of the notification (active vs. resolved).</span></span>
- <span data-ttu-id="16640-112">通知的層級 (資訊、警告、錯誤)。</span><span class="sxs-lookup"><span data-stu-id="16640-112">The level of the notifications (informational, warning, error).</span></span>

<span data-ttu-id="16640-113">您也可以設定應傳送警示的對象：</span><span class="sxs-lookup"><span data-stu-id="16640-113">You also can configure who the alert should be sent to:</span></span>

- <span data-ttu-id="16640-114">選取現有的動作群組。</span><span class="sxs-lookup"><span data-stu-id="16640-114">Select an existing action group.</span></span>
- <span data-ttu-id="16640-115">建立新動作群組 (可用於未來的警示)。</span><span class="sxs-lookup"><span data-stu-id="16640-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="16640-116">若要深入了解動作群組，請參閱[建立及管理動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="16640-116">To learn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="16640-117">若要了解如何使用 Azure Resource Manager 範本來設定服務健康情況通知警示，請參閱 [Resource Manager 範本](monitoring-create-activity-log-alerts-with-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="16640-117">For information on how to configure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="16640-118">使用 Azure 入口網站為新動作群組建立服務健康情況通知的警示</span><span class="sxs-lookup"><span data-stu-id="16640-118">Create an alert on a service health notification for a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="16640-119">在 [入口網站](https://portal.azure.com) 中，選取 **監視**。</span><span class="sxs-lookup"><span data-stu-id="16640-119">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![監視」服務](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="16640-121">在 [活動記錄] 區段中，選取 [警示]。</span><span class="sxs-lookup"><span data-stu-id="16640-121">In the **Activity log** section, select **Alerts**.</span></span>

    ![「警示」索引標籤](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="16640-123">選取 [新增活動記錄警示]，並填寫各欄位。</span><span class="sxs-lookup"><span data-stu-id="16640-123">Select **Add activity log alert**, and fill in the fields.</span></span>

    ![「新增活動記錄警示」命令](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="16640-125">在 [新增活動記錄警示] 方塊中輸入名稱，並提供 [描述]。</span><span class="sxs-lookup"><span data-stu-id="16640-125">Enter a name in the **Activity log alert name** box, and provide a **Description**.</span></span>

    ![「新增活動記錄警示」對話方塊](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="16640-127">[訂用帳戶] 方塊會自動填入您目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="16640-127">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="16640-128">此訂用帳戶會用來儲存活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="16640-128">This subscription is used to save the activity log alert.</span></span> <span data-ttu-id="16640-129">警示資源會部署到此訂用帳戶，並從中監視活動記錄事件。</span><span class="sxs-lookup"><span data-stu-id="16640-129">The alert resource is deployed to this subscription and monitors events in the activity log for it.</span></span>

6. <span data-ttu-id="16640-130">選取將在其中建立警示資源的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="16640-130">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="16640-131">這不是由警示所監視的資源群組，</span><span class="sxs-lookup"><span data-stu-id="16640-131">This isn't the resource group that's monitored by the alert.</span></span> <span data-ttu-id="16640-132">而是警示資源所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="16640-132">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="16640-133">在 [事件類別目錄] 方塊中，選取 [服務健康情況]，</span><span class="sxs-lookup"><span data-stu-id="16640-133">In the **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="16640-134">或是選擇您想要接收服務健康情況通知的 [服務]、[區域]、[類型]、[狀態]，以及 [等級]。</span><span class="sxs-lookup"><span data-stu-id="16640-134">Optionally, select the **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want to receive.</span></span>

8. <span data-ttu-id="16640-135">在 [Alert via]\(警示媒介\) 下，選取 [新增] 動作群組按鈕。</span><span class="sxs-lookup"><span data-stu-id="16640-135">Under **Alert via**, select the **New** action group button.</span></span> <span data-ttu-id="16640-136">在 [動作群組名稱] 方塊中輸入名稱，然後在 [簡短名稱] 方塊中，輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="16640-136">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="16640-137">當此警示發動時，通知中會引用該簡短名稱。</span><span class="sxs-lookup"><span data-stu-id="16640-137">The short name is referenced in the notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="16640-138">請提供接收者的下列各項，以定義接收者的清單：</span><span class="sxs-lookup"><span data-stu-id="16640-138">Define a list of receivers by providing the receiver's:</span></span>

    <span data-ttu-id="16640-139">a.</span><span class="sxs-lookup"><span data-stu-id="16640-139">a.</span></span> <span data-ttu-id="16640-140">**名稱**：輸入接收者名稱、別名或識別碼。</span><span class="sxs-lookup"><span data-stu-id="16640-140">**Name**: Enter the receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="16640-141">b.</span><span class="sxs-lookup"><span data-stu-id="16640-141">b.</span></span> <span data-ttu-id="16640-142">**動作類型**：選取 SMS、電子郵件或 Webhook。</span><span class="sxs-lookup"><span data-stu-id="16640-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="16640-143">c.</span><span class="sxs-lookup"><span data-stu-id="16640-143">c.</span></span> <span data-ttu-id="16640-144">**詳細資料**：根據選擇的動作類型，輸入電話號碼、電子郵件地址或 Webhook URI。</span><span class="sxs-lookup"><span data-stu-id="16640-144">**Details**: Based on the action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="16640-145">選取 [確定] 以建立警示。</span><span class="sxs-lookup"><span data-stu-id="16640-145">Select **OK** to create the alert.</span></span>

<span data-ttu-id="16640-146">在幾分鐘之內會啟用警示，開始根據建立時所指定的條件觸發警示。</span><span class="sxs-lookup"><span data-stu-id="16640-146">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

<span data-ttu-id="16640-147">如需活動記錄警示之 Webhook 結構描述的資訊，請參閱 [Azure 活動記錄警示的 Webhook](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="16640-147">For information on the webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="16640-148">在這些步驟中定義的動作群組，會以現有動作群組的形式提供給所有未來的警示定義重複使用。</span><span class="sxs-lookup"><span data-stu-id="16640-148">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="16640-149">使用 Azure 入口網站，為現有動作群組建立服務健康情況通知的警示</span><span class="sxs-lookup"><span data-stu-id="16640-149">Create an alert on a service health notification for an existing action group by using the Azure portal</span></span>

1. <span data-ttu-id="16640-150">請遵循上一節的步驟 1 到 7，以建立您的服務健康情況通知。</span><span class="sxs-lookup"><span data-stu-id="16640-150">Follow steps 1 through 7 in the previous section to create your service health notification.</span></span> 

2. <span data-ttu-id="16640-151">在 [Alert via]\(警示媒介\) 下，選取 [現有] 動作群組按鈕。</span><span class="sxs-lookup"><span data-stu-id="16640-151">Under **Alert via**, select the **Existing** action group button.</span></span> <span data-ttu-id="16640-152">選取適當的動作群組。</span><span class="sxs-lookup"><span data-stu-id="16640-152">Select the appropriate action group.</span></span>

3. <span data-ttu-id="16640-153">選取 [確定] 可建立警示。</span><span class="sxs-lookup"><span data-stu-id="16640-153">Select **OK** to create the alert.</span></span>

<span data-ttu-id="16640-154">在幾分鐘之內會啟用警示，開始根據建立時所指定的條件觸發警示。</span><span class="sxs-lookup"><span data-stu-id="16640-154">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="16640-155">管理警示</span><span class="sxs-lookup"><span data-stu-id="16640-155">Manage your alerts</span></span>

<span data-ttu-id="16640-156">警示建立之後，會顯示在 [監視] 刀鋒視窗的 [警示] 區段中。</span><span class="sxs-lookup"><span data-stu-id="16640-156">After you create an alert, it's visible in the **Alerts** section of the **Monitor** blade.</span></span> <span data-ttu-id="16640-157">選取您要管理的警示：</span><span class="sxs-lookup"><span data-stu-id="16640-157">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="16640-158">進行編輯。</span><span class="sxs-lookup"><span data-stu-id="16640-158">Edit it.</span></span>
* <span data-ttu-id="16640-159">進行刪除。</span><span class="sxs-lookup"><span data-stu-id="16640-159">Delete it.</span></span>
* <span data-ttu-id="16640-160">如果您需要暫時停止或恢復接收警示的通知，可以將警示停用或啟用。</span><span class="sxs-lookup"><span data-stu-id="16640-160">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16640-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16640-161">Next steps</span></span>
- <span data-ttu-id="16640-162">深入了解[服務健康狀態通知](monitoring-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="16640-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="16640-163">深入了解[通知速率限制](monitoring-alerts-rate-limiting.md)。</span><span class="sxs-lookup"><span data-stu-id="16640-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="16640-164">檢閱[活動記錄警示 Webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="16640-164">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="16640-165">取得[活動記錄警示的概觀](monitoring-overview-alerts.md)，並了解如何收到警示。</span><span class="sxs-lookup"><span data-stu-id="16640-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span> 
- <span data-ttu-id="16640-166">深入了解[動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="16640-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
