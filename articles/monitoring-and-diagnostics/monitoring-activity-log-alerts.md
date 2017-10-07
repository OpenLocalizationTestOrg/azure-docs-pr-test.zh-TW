---
title: "aaaCreate 活動記錄檔警示 |Microsoft 文件"
description: "可透過 SMS、 webhook，與電子郵件通知，hello 活動記錄檔中發生特定事件時。"
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="38138-103">建立活動記錄警示</span><span class="sxs-lookup"><span data-stu-id="38138-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="38138-104">概觀</span><span class="sxs-lookup"><span data-stu-id="38138-104">Overview</span></span>
<span data-ttu-id="38138-105">活動記錄檔的警示會啟動新的活動記錄事件發生時的警示符合 hello hello 警示中指定的條件。</span><span class="sxs-lookup"><span data-stu-id="38138-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches hello conditions specified in hello alert.</span></span> <span data-ttu-id="38138-106">它們是 Azure 資源，因此可以使用 Azure Resource Manager 範本來加以建立。</span><span class="sxs-lookup"><span data-stu-id="38138-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="38138-107">它們也可以建立、 更新，或在 hello Azure 入口網站中刪除。</span><span class="sxs-lookup"><span data-stu-id="38138-107">They also can be created, updated, or deleted in hello Azure portal.</span></span> <span data-ttu-id="38138-108">本文介紹 hello 概念活動記錄檔的警示。</span><span class="sxs-lookup"><span data-stu-id="38138-108">This article introduces hello concepts behind activity log alerts.</span></span> <span data-ttu-id="38138-109">接著會說明如何 toouse hello Azure 入口網站的 tooset 向上活動記錄檔事件的警示。</span><span class="sxs-lookup"><span data-stu-id="38138-109">It then shows you how toouse hello Azure portal tooset up an alert on activity log events.</span></span>

<span data-ttu-id="38138-110">通常您會建立活動記錄檔警示 tooreceive 通知時：</span><span class="sxs-lookup"><span data-stu-id="38138-110">Typically, you create activity log alerts tooreceive notifications when:</span></span>

* <span data-ttu-id="38138-111">在您的 Azure 訂用帳戶、 通常已設定領域的 tooparticular 資源群組或資源的資源上發生特定變更。</span><span class="sxs-lookup"><span data-stu-id="38138-111">Specific changes occur on resources in your Azure subscription, often scoped tooparticular resource groups or resources.</span></span> <span data-ttu-id="38138-112">例如，您可能想 toobe 刪除 myProductionResourceGroup 中任何虛擬機器時收到通知。</span><span class="sxs-lookup"><span data-stu-id="38138-112">For example, you might want toobe notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="38138-113">或者，您可能會想 toobe 如果任何新的角色指派給您的訂用帳戶中的 tooa 使用者收到通知。</span><span class="sxs-lookup"><span data-stu-id="38138-113">Or, you might want toobe notified if any new roles are assigned tooa user in your subscription.</span></span>
* <span data-ttu-id="38138-114">隨即發生服務健康情況事件。</span><span class="sxs-lookup"><span data-stu-id="38138-114">A service health event occurs.</span></span> <span data-ttu-id="38138-115">服務健全狀況事件包括事件和套用 tooresources 您訂用帳戶中的維護事件的通知。</span><span class="sxs-lookup"><span data-stu-id="38138-115">Service health events include notification of incidents and maintenance events that apply tooresources in your subscription.</span></span>

<span data-ttu-id="38138-116">在任一情況下，活動記錄檔警示監視僅適用於在 hello 訂用帳戶中的 hello 建立警示的事件。</span><span class="sxs-lookup"><span data-stu-id="38138-116">In either case, an activity log alert monitors only for events in hello subscription in which hello alert is created.</span></span>

<span data-ttu-id="38138-117">您可以設定活動記錄檔警示 hello 活動記錄檔事件的 JSON 物件中任何最上層屬性為基礎。</span><span class="sxs-lookup"><span data-stu-id="38138-117">You can configure an activity log alert based on any top-level property in hello JSON object for an activity log event.</span></span> <span data-ttu-id="38138-118">不過，hello 入口網站會顯示 hello 最常用的選項：</span><span class="sxs-lookup"><span data-stu-id="38138-118">However, hello portal shows hello most common options:</span></span>

- <span data-ttu-id="38138-119">**類別**：系統管理、服務健康狀態、自動調整規模及建議。</span><span class="sxs-lookup"><span data-stu-id="38138-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="38138-120">如需詳細資訊，請參閱[hello Azure 活動記錄檔的概觀](./monitoring-overview-activity-logs.md#categories-in-the-activity-log)。</span><span class="sxs-lookup"><span data-stu-id="38138-120">For more information, see [Overview of hello Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="38138-121">toolearn 進一步了解服務健全狀況事件，請參閱[接收服務通知上的活動記錄檔警示](./monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-121">toolearn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="38138-122">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="38138-122">**Resource group**</span></span>
- <span data-ttu-id="38138-123">**Resource**</span><span class="sxs-lookup"><span data-stu-id="38138-123">**Resource**</span></span>
- <span data-ttu-id="38138-124">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="38138-124">**Resource type**</span></span>
- <span data-ttu-id="38138-125">**作業名稱**: hello 資源管理員角色型存取控制作業名稱。</span><span class="sxs-lookup"><span data-stu-id="38138-125">**Operation name**: hello Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="38138-126">**層級**: hello （詳細資訊、 資訊、 警告、 錯誤或重大） hello 事件嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="38138-126">**Level**: hello severity level of hello event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="38138-127">**狀態**: hello 的 hello 事件，通常啟動、 失敗或成功的狀態。</span><span class="sxs-lookup"><span data-stu-id="38138-127">**Status**: hello status of hello event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="38138-128">**由事件初始化**： 也稱為 hello 「 呼叫者。 」</span><span class="sxs-lookup"><span data-stu-id="38138-128">**Event initiated by**: Also known as hello "caller."</span></span> <span data-ttu-id="38138-129">hello 電子郵件地址或 Azure Active Directory 作業 hello hello 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="38138-129">hello email address or Azure Active Directory identifier of hello user who performed hello operation.</span></span>

>[!NOTE]
><span data-ttu-id="38138-130">您必須指定至少兩個準則中警示，具有一個在前面的 hello hello 類別。</span><span class="sxs-lookup"><span data-stu-id="38138-130">You must specify at least two of hello preceding criteria in your alert, with one being hello category.</span></span> <span data-ttu-id="38138-131">您可能無法建立警示，每次 hello 活動記錄檔中建立事件時，就會啟動。</span><span class="sxs-lookup"><span data-stu-id="38138-131">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
>
>

<span data-ttu-id="38138-132">啟動 活動記錄警示時，它會使用動作群組 toogenerate 動作或通知。</span><span class="sxs-lookup"><span data-stu-id="38138-132">When an activity log alert is activated, it uses an action group toogenerate actions or notifications.</span></span> <span data-ttu-id="38138-133">動作群組是一組可重複使用的通知接收者，例如電子郵件地址、Webhook URL 或 SMS 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="38138-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="38138-134">hello 接收者可以從多個警示 toocentralize 參考，並分組通知通道。</span><span class="sxs-lookup"><span data-stu-id="38138-134">hello receivers can be referenced from multiple alerts toocentralize and group your notification channels.</span></span> <span data-ttu-id="38138-135">當您定義活動記錄警示時，會有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="38138-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="38138-136">您可以：</span><span class="sxs-lookup"><span data-stu-id="38138-136">You can:</span></span>

* <span data-ttu-id="38138-137">在您的活動記錄警示中使用現有的動作群組。</span><span class="sxs-lookup"><span data-stu-id="38138-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="38138-138">建立新的動作群組。</span><span class="sxs-lookup"><span data-stu-id="38138-138">Create a new action group.</span></span> 

<span data-ttu-id="38138-139">toolearn 進一步了解動作群組，請參閱[建立及管理在 hello Azure 入口網站中的動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-139">toolearn more about action groups, see [Create and manage action groups in hello Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="38138-140">toolearn 進一步了解服務健全狀況通知，請參閱[接收服務健全狀況通知上的活動記錄檔警示](monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-140">toolearn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="38138-141">使用 hello Azure 入口網站建立與新的動作群組的活動記錄檔事件的警示</span><span class="sxs-lookup"><span data-stu-id="38138-141">Create an alert on an activity log event with a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="38138-142">在 hello[入口網站](https://portal.azure.com)，選取**監視器**。</span><span class="sxs-lookup"><span data-stu-id="38138-142">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![hello 「 監視 」 服務](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="38138-144">在 hello**活動記錄檔**區段中，選取**警示**。</span><span class="sxs-lookup"><span data-stu-id="38138-144">In hello **Activity log** section, select **Alerts**.</span></span>

    ![hello [警示] 索引標籤](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="38138-146">選取**新增活動記錄檔警示**，並填入 hello 欄位中。</span><span class="sxs-lookup"><span data-stu-id="38138-146">Select **Add activity log alert**, and fill in hello fields.</span></span>

4. <span data-ttu-id="38138-147">輸入的名稱在 hello**活動記錄檔的警示名稱**方塊，然後選取**描述**。</span><span class="sxs-lookup"><span data-stu-id="38138-147">Enter a name in hello **Activity log alert name** box, and select a **Description**.</span></span>

    ![hello 「 新增活動記錄警示 」 命令](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="38138-149">hello**訂用帳戶**方塊 autofills 與您目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="38138-149">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="38138-150">此訂用帳戶中儲存的 hello 動作群組是 hello 其中一個。</span><span class="sxs-lookup"><span data-stu-id="38138-150">This subscription is hello one in which hello action group is saved.</span></span> <span data-ttu-id="38138-151">hello 警示的資源是從它的已部署的 toothis 訂用帳戶和監視活動記錄事件。</span><span class="sxs-lookup"><span data-stu-id="38138-151">hello alert resource is deployed toothis subscription and monitors activity log events from it.</span></span>

    ![[新增活動記錄警示] 對話方塊中的 hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="38138-153">選取 hello**資源群組**哪些 hello 中建立警示的資源。</span><span class="sxs-lookup"><span data-stu-id="38138-153">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="38138-154">這不由 hello 警示所監視的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="38138-154">This is not hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="38138-155">相反地，它是 hello hello 警示資源所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="38138-155">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="38138-156">（選擇性） 選取**事件類別目錄**toomodify hello 所顯示的其他篩選。</span><span class="sxs-lookup"><span data-stu-id="38138-156">Optionally, select an **Event category** toomodify hello additional filters that are shown.</span></span> <span data-ttu-id="38138-157">對於系統管理事件，包括 hello 篩選**資源群組**，**資源**，**資源類型**，**作業名稱**， **層級**，**狀態**，和**由事件初始化**。</span><span class="sxs-lookup"><span data-stu-id="38138-157">For Administrative events, hello filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="38138-158">這些值會識別此警示應該監視的事件。</span><span class="sxs-lookup"><span data-stu-id="38138-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="38138-159">您必須指定至少一個在您的警示之前準則 hello。</span><span class="sxs-lookup"><span data-stu-id="38138-159">You must specify at least one of hello preceding criteria in your alert.</span></span> <span data-ttu-id="38138-160">您可能無法建立警示，每次 hello 活動記錄檔中建立事件時，就會啟動。</span><span class="sxs-lookup"><span data-stu-id="38138-160">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
    >
    >

8. <span data-ttu-id="38138-161">輸入的名稱在 hello**動作群組名稱**，然後輸入的名稱在 hello**簡短名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="38138-161">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="38138-162">hello 簡短名稱是在使用這個群組會傳送通知時，使用完整的動作群組名稱取代。</span><span class="sxs-lookup"><span data-stu-id="38138-162">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="38138-163">藉由提供 hello 動作定義動作的清單：</span><span class="sxs-lookup"><span data-stu-id="38138-163">Define a list of actions by providing hello action’s:</span></span>

    <span data-ttu-id="38138-164">a.</span><span class="sxs-lookup"><span data-stu-id="38138-164">a.</span></span> <span data-ttu-id="38138-165">**名稱**： 輸入 hello 動作名稱、 別名或識別項。</span><span class="sxs-lookup"><span data-stu-id="38138-165">**Name**: Enter hello action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="38138-166">b.</span><span class="sxs-lookup"><span data-stu-id="38138-166">b.</span></span> <span data-ttu-id="38138-167">**動作類型**：選取 SMS、電子郵件或 Webhook。</span><span class="sxs-lookup"><span data-stu-id="38138-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="38138-168">c.</span><span class="sxs-lookup"><span data-stu-id="38138-168">c.</span></span> <span data-ttu-id="38138-169">**詳細資料**： 根據 hello 動作類型，輸入電話號碼、 電子郵件地址或 webhook URI。</span><span class="sxs-lookup"><span data-stu-id="38138-169">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="38138-170">選取**確定**toocreate hello 警示。</span><span class="sxs-lookup"><span data-stu-id="38138-170">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="38138-171">hello 警示需要幾分鐘的時間 toofully 傳播，並再變成 作用中。</span><span class="sxs-lookup"><span data-stu-id="38138-171">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="38138-172">它時，會觸發新的事件符合 hello 警示的準則。</span><span class="sxs-lookup"><span data-stu-id="38138-172">It triggers when new events match hello alert's criteria.</span></span>

<span data-ttu-id="38138-173">如需詳細資訊，請參閱[活動記錄檔警示中使用的了解 hello webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-173">For more information, see [Understand hello webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="38138-174">這些步驟中所定義的 hello 動作群組是可重複使用與現有的動作群組的所有未來的警示定義。</span><span class="sxs-lookup"><span data-stu-id="38138-174">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="38138-175">建立使用 hello Azure 入口網站為現有的動作群組的活動記錄檔事件的警示</span><span class="sxs-lookup"><span data-stu-id="38138-175">Create an alert on an activity log event for an existing action group by using hello Azure portal</span></span>
1. <span data-ttu-id="38138-176">請遵循步驟 1 到 7 中前一個區段 toocreate hello 活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="38138-176">Follow steps 1 through 7 in hello previous section toocreate your activity log alert.</span></span>

2. <span data-ttu-id="38138-177">在下**透過通知**，選取 hello**現有**動作群組 按鈕。</span><span class="sxs-lookup"><span data-stu-id="38138-177">Under **Notify via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="38138-178">Hello 清單中選取現有的動作群組。</span><span class="sxs-lookup"><span data-stu-id="38138-178">Select an existing action group from hello list.</span></span>

3. <span data-ttu-id="38138-179">選取**確定**toocreate hello 警示。</span><span class="sxs-lookup"><span data-stu-id="38138-179">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="38138-180">hello 警示需要幾分鐘的時間 toofully 傳播，並再變成 作用中。</span><span class="sxs-lookup"><span data-stu-id="38138-180">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="38138-181">它時，會觸發新的事件符合 hello 警示的準則。</span><span class="sxs-lookup"><span data-stu-id="38138-181">It triggers when new events match hello alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="38138-182">管理警示</span><span class="sxs-lookup"><span data-stu-id="38138-182">Manage your alerts</span></span>

<span data-ttu-id="38138-183">建立警示之後，它會顯示在 hello hello 監視器] 刀鋒視窗的 [警示 > 一節。</span><span class="sxs-lookup"><span data-stu-id="38138-183">After you create an alert, it's visible in hello Alerts section of hello Monitor blade.</span></span> <span data-ttu-id="38138-184">選取您想要的 toomanage 的 hello 警示：</span><span class="sxs-lookup"><span data-stu-id="38138-184">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="38138-185">進行編輯。</span><span class="sxs-lookup"><span data-stu-id="38138-185">Edit it.</span></span>
* <span data-ttu-id="38138-186">進行刪除。</span><span class="sxs-lookup"><span data-stu-id="38138-186">Delete it.</span></span>
* <span data-ttu-id="38138-187">停用或啟用它，如果您想要 tootemporarily 停止或繼續收到 hello 警示的通知。</span><span class="sxs-lookup"><span data-stu-id="38138-187">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38138-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38138-188">Next steps</span></span>
- <span data-ttu-id="38138-189">取得[警示概觀](monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="38138-190">深入了解[通知速率限制](monitoring-alerts-rate-limiting.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="38138-191">檢閱 hello[活動記錄警示 webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-191">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="38138-192">深入了解[動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="38138-193">深入了解[服務健康狀態通知](monitoring-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="38138-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="38138-194">建立[活動記錄警示 toomonitor 所有訂用帳戶的自動調整引擎作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)。</span><span class="sxs-lookup"><span data-stu-id="38138-194">Create an [activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="38138-195">建立[活動記錄警示 toomonitor 訂用帳戶的所有失敗的自動調整規模輸入/向外作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)。</span><span class="sxs-lookup"><span data-stu-id="38138-195">Create an [activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
