---
title: "在服務通知 aaaReceive 活動記錄檔警示 |Microsoft 文件"
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
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="ad95e-103">建立服務通知的活動記錄警示</span><span class="sxs-lookup"><span data-stu-id="ad95e-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="ad95e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ad95e-104">Overview</span></span>
<span data-ttu-id="ad95e-105">本文將說明您的服務健全狀況通知 tooset 活動記錄警示 hello Azure 入口網站的使用方式。</span><span class="sxs-lookup"><span data-stu-id="ad95e-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="ad95e-106">您可以收到通知時，Azure 都會傳送服務健全狀況通知 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad95e-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="ad95e-107">您可以設定為基礎的 hello 警示：</span><span class="sxs-lookup"><span data-stu-id="ad95e-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="ad95e-108">hello 類別的服務健全狀況通知 （事件、 維護、 資訊等等）。</span><span class="sxs-lookup"><span data-stu-id="ad95e-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="ad95e-109">受影響的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ad95e-109">hello service(s) affected.</span></span>
- <span data-ttu-id="ad95e-110">受影響的 hello 到區域。</span><span class="sxs-lookup"><span data-stu-id="ad95e-110">hello region(s) affected.</span></span>
- <span data-ttu-id="ad95e-111">hello hello 通知 （使用中和已解決的比較） 狀態。</span><span class="sxs-lookup"><span data-stu-id="ad95e-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="ad95e-112">hello 層級的 hello 通知 （資訊、 警告、 錯誤）。</span><span class="sxs-lookup"><span data-stu-id="ad95e-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="ad95e-113">您也可以設定 hello 警示應收件者：</span><span class="sxs-lookup"><span data-stu-id="ad95e-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="ad95e-114">選取現有的動作群組。</span><span class="sxs-lookup"><span data-stu-id="ad95e-114">Select an existing action group.</span></span>
- <span data-ttu-id="ad95e-115">建立新動作群組 (可用於未來的警示)。</span><span class="sxs-lookup"><span data-stu-id="ad95e-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="ad95e-116">toolearn 進一步了解動作群組，請參閱[建立及管理群組動作](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="ad95e-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="ad95e-117">如需如何 tooconfigure 服務健全狀況通知警示使用的 Azure Resource Manager 範本資訊，請參閱[資源管理員範本](monitoring-create-activity-log-alerts-with-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="ad95e-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="ad95e-118">使用 hello Azure 入口網站建立新的動作群組的服務健全狀況通知警示</span><span class="sxs-lookup"><span data-stu-id="ad95e-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="ad95e-119">在 hello[入口網站](https://portal.azure.com)，選取**監視器**。</span><span class="sxs-lookup"><span data-stu-id="ad95e-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![hello 「 監視 」 服務](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="ad95e-121">在 hello**活動記錄檔**區段中，選取**警示**。</span><span class="sxs-lookup"><span data-stu-id="ad95e-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![hello [警示] 索引標籤](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="ad95e-123">選取**新增活動記錄檔警示**，並填入 hello 欄位中。</span><span class="sxs-lookup"><span data-stu-id="ad95e-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![hello 「 新增活動記錄警示 」 命令](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="ad95e-125">輸入的名稱在 hello**活動記錄檔的警示名稱**方塊，並提供**描述**。</span><span class="sxs-lookup"><span data-stu-id="ad95e-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![[新增活動記錄警示] 對話方塊中的 hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="ad95e-127">hello**訂用帳戶**方塊 autofills 與您目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad95e-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="ad95e-128">此訂用帳戶是使用的 toosave hello 活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="ad95e-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="ad95e-129">hello 警示的資源是為它的 hello 活動記錄檔中的已部署的 toothis 訂用帳戶和監視事件。</span><span class="sxs-lookup"><span data-stu-id="ad95e-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="ad95e-130">選取 hello**資源群組**哪些 hello 中建立警示的資源。</span><span class="sxs-lookup"><span data-stu-id="ad95e-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="ad95e-131">這不由 hello 警示所監視的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ad95e-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="ad95e-132">相反地，它是 hello hello 警示資源所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ad95e-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="ad95e-133">在 hello**事件類別目錄**方塊中，選取**服務健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="ad95e-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="ad95e-134">（選擇性） 選取 hello**服務**，**區域**，**類型**，**狀態**，和**層級**的服務您想 tooreceive 健康情況通知。</span><span class="sxs-lookup"><span data-stu-id="ad95e-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="ad95e-135">在下**透過警示**，選取 hello**新增**動作群組 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ad95e-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="ad95e-136">輸入的名稱在 hello**動作群組名稱**，然後輸入的名稱在 hello**簡短名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="ad95e-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="ad95e-137">hello 簡短名稱參考時都會引發這個警示所傳送嗨通知中。</span><span class="sxs-lookup"><span data-stu-id="ad95e-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="ad95e-138">藉由提供 hello 接收器中定義接收者的清單：</span><span class="sxs-lookup"><span data-stu-id="ad95e-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="ad95e-139">a.</span><span class="sxs-lookup"><span data-stu-id="ad95e-139">a.</span></span> <span data-ttu-id="ad95e-140">**名稱**： 輸入 hello 接收器的名稱、 別名或識別項。</span><span class="sxs-lookup"><span data-stu-id="ad95e-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="ad95e-141">b.</span><span class="sxs-lookup"><span data-stu-id="ad95e-141">b.</span></span> <span data-ttu-id="ad95e-142">**動作類型**：選取 SMS、電子郵件或 Webhook。</span><span class="sxs-lookup"><span data-stu-id="ad95e-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="ad95e-143">c.</span><span class="sxs-lookup"><span data-stu-id="ad95e-143">c.</span></span> <span data-ttu-id="ad95e-144">**詳細資料**： 根據選擇的 hello 動作類型，輸入電話號碼、 電子郵件地址或 webhook URI。</span><span class="sxs-lookup"><span data-stu-id="ad95e-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="ad95e-145">選取**確定**toocreate hello 警示。</span><span class="sxs-lookup"><span data-stu-id="ad95e-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="ad95e-146">在幾分鐘的時間內 hello 警示為作用中，並且開始 tootrigger 根據您在建立期間指定的 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="ad95e-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="ad95e-147">如需活動記錄檔警示 hello webhook 結構描述資訊，請參閱[Webhook Azure 活動記錄警示](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="ad95e-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="ad95e-148">這些步驟中所定義的 hello 動作群組是可重複使用與現有的動作群組的所有未來的警示定義。</span><span class="sxs-lookup"><span data-stu-id="ad95e-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="ad95e-149">建立現有的動作群組的服務健全狀況通知警示使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ad95e-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="ad95e-150">請遵循步驟 1 到 7 中前一個區段 toocreate hello 您服務的健全狀況通知。</span><span class="sxs-lookup"><span data-stu-id="ad95e-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="ad95e-151">在下**透過警示**，選取 hello**現有**動作群組 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ad95e-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="ad95e-152">選取 hello 適當的動作群組。</span><span class="sxs-lookup"><span data-stu-id="ad95e-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="ad95e-153">選取**確定**toocreate hello 警示。</span><span class="sxs-lookup"><span data-stu-id="ad95e-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="ad95e-154">在幾分鐘的時間內 hello 警示為作用中，並且開始 tootrigger 根據您在建立期間指定的 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="ad95e-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="ad95e-155">管理警示</span><span class="sxs-lookup"><span data-stu-id="ad95e-155">Manage your alerts</span></span>

<span data-ttu-id="ad95e-156">建立警示之後，會顯示在 hello**警示**區段 hello**監視器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ad95e-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="ad95e-157">選取您想要的 toomanage 的 hello 警示：</span><span class="sxs-lookup"><span data-stu-id="ad95e-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="ad95e-158">進行編輯。</span><span class="sxs-lookup"><span data-stu-id="ad95e-158">Edit it.</span></span>
* <span data-ttu-id="ad95e-159">進行刪除。</span><span class="sxs-lookup"><span data-stu-id="ad95e-159">Delete it.</span></span>
* <span data-ttu-id="ad95e-160">停用或啟用它，如果您想要 tootemporarily 停止或繼續收到 hello 警示的通知。</span><span class="sxs-lookup"><span data-stu-id="ad95e-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad95e-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad95e-161">Next steps</span></span>
- <span data-ttu-id="ad95e-162">深入了解[服務健康狀態通知](monitoring-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="ad95e-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="ad95e-163">深入了解[通知速率限制](monitoring-alerts-rate-limiting.md)。</span><span class="sxs-lookup"><span data-stu-id="ad95e-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="ad95e-164">檢閱 hello[活動記錄警示 webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="ad95e-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="ad95e-165">取得[活動記錄檔警示概觀](monitoring-overview-alerts.md)，並了解如何 tooreceive 警示。</span><span class="sxs-lookup"><span data-stu-id="ad95e-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="ad95e-166">深入了解[動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="ad95e-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
