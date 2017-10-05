---
title: "建立活動記錄警示 | Microsoft Docs"
description: "活動記錄中發生特定事件時，透過 SMS、Webhook 及電子郵件收到通知。"
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
ms.openlocfilehash: 3885469ec0e1fcc31386dd0ad7fe6cb5d03ab28e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="b699d-103">建立活動記錄警示</span><span class="sxs-lookup"><span data-stu-id="b699d-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="b699d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b699d-104">Overview</span></span>
<span data-ttu-id="b699d-105">活動記錄警示是發生符合警示中指定條件的新活動記錄事件時所啟動的警示。</span><span class="sxs-lookup"><span data-stu-id="b699d-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches the conditions specified in the alert.</span></span> <span data-ttu-id="b699d-106">它們是 Azure 資源，因此可以使用 Azure Resource Manager 範本來加以建立。</span><span class="sxs-lookup"><span data-stu-id="b699d-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="b699d-107">也可以在 Azure 入口網站中將它們建立、更新或刪除。</span><span class="sxs-lookup"><span data-stu-id="b699d-107">They also can be created, updated, or deleted in the Azure portal.</span></span> <span data-ttu-id="b699d-108">本文介紹活動記錄警示背後的概念。</span><span class="sxs-lookup"><span data-stu-id="b699d-108">This article introduces the concepts behind activity log alerts.</span></span> <span data-ttu-id="b699d-109">然後將說明如何使用 Azure 入口網站來設定活動記錄事件的警示。</span><span class="sxs-lookup"><span data-stu-id="b699d-109">It then shows you how to use the Azure portal to set up an alert on activity log events.</span></span>

<span data-ttu-id="b699d-110">通常，您在下列情況要建立活動記錄警示來接收通知：</span><span class="sxs-lookup"><span data-stu-id="b699d-110">Typically, you create activity log alerts to receive notifications when:</span></span>

* <span data-ttu-id="b699d-111">在 Azure 訂用帳戶中的資源發生特定變更時，通常會將範圍限定在特定資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="b699d-111">Specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resources.</span></span> <span data-ttu-id="b699d-112">例如，在 myProductionResourceGroup 中的任何虛擬機器被刪除時，您可能需要收到通知。</span><span class="sxs-lookup"><span data-stu-id="b699d-112">For example, you might want to be notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="b699d-113">或者，您需要在將任何新角色指派給訂用帳戶中的使用者時收到通知。</span><span class="sxs-lookup"><span data-stu-id="b699d-113">Or, you might want to be notified if any new roles are assigned to a user in your subscription.</span></span>
* <span data-ttu-id="b699d-114">隨即發生服務健康情況事件。</span><span class="sxs-lookup"><span data-stu-id="b699d-114">A service health event occurs.</span></span> <span data-ttu-id="b699d-115">服務健康狀態事件包括適用於訂用帳戶中資源的事件 (incident) 和維護事件 (event) 通知。</span><span class="sxs-lookup"><span data-stu-id="b699d-115">Service health events include notification of incidents and maintenance events that apply to resources in your subscription.</span></span>

<span data-ttu-id="b699d-116">在任一情況下，活動記錄警示只會監視建立警示所在之訂用帳戶中的事件。</span><span class="sxs-lookup"><span data-stu-id="b699d-116">In either case, an activity log alert monitors only for events in the subscription in which the alert is created.</span></span>

<span data-ttu-id="b699d-117">您可以針對活動記錄事件，以 JSON 物件中任何最上層屬性作為基礎設定活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="b699d-117">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span></span> <span data-ttu-id="b699d-118">不過，入口網站會顯示最常用的選項：</span><span class="sxs-lookup"><span data-stu-id="b699d-118">However, the portal shows the most common options:</span></span>

- <span data-ttu-id="b699d-119">**類別**：系統管理、服務健康狀態、自動調整規模及建議。</span><span class="sxs-lookup"><span data-stu-id="b699d-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="b699d-120">如需詳細資訊，請參閱 [Azure 活動記錄概觀](./monitoring-overview-activity-logs.md#categories-in-the-activity-log)。</span><span class="sxs-lookup"><span data-stu-id="b699d-120">For more information, see [Overview of the Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="b699d-121">若要深入了解服務健康情況事件，請參閱[在服務通知上接收活動記錄警示](./monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-121">To learn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="b699d-122">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="b699d-122">**Resource group**</span></span>
- <span data-ttu-id="b699d-123">**Resource**</span><span class="sxs-lookup"><span data-stu-id="b699d-123">**Resource**</span></span>
- <span data-ttu-id="b699d-124">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="b699d-124">**Resource type**</span></span>
- <span data-ttu-id="b699d-125">**作業名稱**：Resource Manager 角色型存取控制作業名稱。</span><span class="sxs-lookup"><span data-stu-id="b699d-125">**Operation name**: The Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="b699d-126">**層級**：事件的安全性層級 (詳細資訊、資訊、警告、錯誤或重大)。</span><span class="sxs-lookup"><span data-stu-id="b699d-126">**Level**: The severity level of the event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="b699d-127">**狀態**：事件的狀態，通常為「已啟動」、「失敗」或「成功」。</span><span class="sxs-lookup"><span data-stu-id="b699d-127">**Status**: The status of the event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="b699d-128">**事件起始者**：也稱為「呼叫者」。</span><span class="sxs-lookup"><span data-stu-id="b699d-128">**Event initiated by**: Also known as the "caller."</span></span> <span data-ttu-id="b699d-129">執行作業之使用者的電子郵件地址或 Azure Active Directory 識別碼。</span><span class="sxs-lookup"><span data-stu-id="b699d-129">The email address or Azure Active Directory identifier of the user who performed the operation.</span></span>

>[!NOTE]
><span data-ttu-id="b699d-130">您必須在您的警示中指定至少兩個上述準則，其中一個是類別。</span><span class="sxs-lookup"><span data-stu-id="b699d-130">You must specify at least two of the preceding criteria in your alert, with one being the category.</span></span> <span data-ttu-id="b699d-131">您不能建立會在每次活動記錄中建立事件時即啟動的警示。</span><span class="sxs-lookup"><span data-stu-id="b699d-131">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
>
>

<span data-ttu-id="b699d-132">當活動記錄警示啟動時，會使用動作群組來產生動作或通知。</span><span class="sxs-lookup"><span data-stu-id="b699d-132">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span></span> <span data-ttu-id="b699d-133">動作群組是一組可重複使用的通知接收者，例如電子郵件地址、Webhook URL 或 SMS 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="b699d-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="b699d-134">可以從多個警示參考接收者，將通知通道集中管理並群組。</span><span class="sxs-lookup"><span data-stu-id="b699d-134">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span></span> <span data-ttu-id="b699d-135">當您定義活動記錄警示時，會有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="b699d-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="b699d-136">您可以：</span><span class="sxs-lookup"><span data-stu-id="b699d-136">You can:</span></span>

* <span data-ttu-id="b699d-137">在您的活動記錄警示中使用現有的動作群組。</span><span class="sxs-lookup"><span data-stu-id="b699d-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="b699d-138">建立新的動作群組。</span><span class="sxs-lookup"><span data-stu-id="b699d-138">Create a new action group.</span></span> 

<span data-ttu-id="b699d-139">若要深入了解動作群組，請參閱[在 Azure 入口網站中建立和管理動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-139">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="b699d-140">若要深入了解服務健康情況通知，請參閱[在服務健康情況通知上接收活動記錄警示](monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-140">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="b699d-141">使用 Azure 入口網站為新動作群組建立活動記錄事件的警示</span><span class="sxs-lookup"><span data-stu-id="b699d-141">Create an alert on an activity log event with a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="b699d-142">在 [入口網站](https://portal.azure.com) 中，選取 [監視]。</span><span class="sxs-lookup"><span data-stu-id="b699d-142">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![監視」服務](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="b699d-144">在 [活動記錄] 區段中，選取 [警示]。</span><span class="sxs-lookup"><span data-stu-id="b699d-144">In the **Activity log** section, select **Alerts**.</span></span>

    ![「警示」索引標籤](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="b699d-146">選取 [新增活動記錄警示]，並填寫各欄位。</span><span class="sxs-lookup"><span data-stu-id="b699d-146">Select **Add activity log alert**, and fill in the fields.</span></span>

4. <span data-ttu-id="b699d-147">在 [活動記錄警示名稱] 方塊中輸入名稱，並選取 [描述]。</span><span class="sxs-lookup"><span data-stu-id="b699d-147">Enter a name in the **Activity log alert name** box, and select a **Description**.</span></span>

    ![[新增活動記錄警示] 命令](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="b699d-149">[訂用帳戶] 方塊會自動填入您目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b699d-149">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="b699d-150">訂用帳戶是要儲存動作群組的位置。</span><span class="sxs-lookup"><span data-stu-id="b699d-150">This subscription is the one in which the action group is saved.</span></span> <span data-ttu-id="b699d-151">警示資源會部署到此訂用帳戶，並從中監視活動記錄事件。</span><span class="sxs-lookup"><span data-stu-id="b699d-151">The alert resource is deployed to this subscription and monitors activity log events from it.</span></span>

    ![[新增活動記錄警示] 對話方塊](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="b699d-153">選取將在其中建立警示資源的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="b699d-153">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="b699d-154">這不是由警示所監視的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b699d-154">This is not the resource group that's monitored by the alert.</span></span> <span data-ttu-id="b699d-155">相反地，這是警示資源所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b699d-155">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="b699d-156">選擇性地選取 [事件類別]，從而修改所顯示的額外篩選條件。</span><span class="sxs-lookup"><span data-stu-id="b699d-156">Optionally, select an **Event category** to modify the additional filters that are shown.</span></span> <span data-ttu-id="b699d-157">在系統管理事件中，篩選條件包括 [資源群組]、[資源]、[資源類型]、作業名稱、層級、狀態 和 [事件初始化方式]。</span><span class="sxs-lookup"><span data-stu-id="b699d-157">For Administrative events, the filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="b699d-158">這些值會識別此警示應該監視的事件。</span><span class="sxs-lookup"><span data-stu-id="b699d-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b699d-159">您必須在您的警示中指定至少一個上述準則。</span><span class="sxs-lookup"><span data-stu-id="b699d-159">You must specify at least one of the preceding criteria in your alert.</span></span> <span data-ttu-id="b699d-160">您不能建立會在每次活動記錄中建立事件時即啟動的警示。</span><span class="sxs-lookup"><span data-stu-id="b699d-160">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
    >
    >

8. <span data-ttu-id="b699d-161">在 [動作群組名稱] 方塊中輸入名稱，然後在 [簡短名稱] 方塊中，輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="b699d-161">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="b699d-162">使用這個群組傳送通知時，會使用簡短名稱來取代完整的動作群組名稱。</span><span class="sxs-lookup"><span data-stu-id="b699d-162">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="b699d-163">透過提供動作的下列各項來定義動作的清單：</span><span class="sxs-lookup"><span data-stu-id="b699d-163">Define a list of actions by providing the action’s:</span></span>

    <span data-ttu-id="b699d-164">a.</span><span class="sxs-lookup"><span data-stu-id="b699d-164">a.</span></span> <span data-ttu-id="b699d-165">**名稱**：輸入動作的名稱、別名或識別碼。</span><span class="sxs-lookup"><span data-stu-id="b699d-165">**Name**: Enter the action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="b699d-166">b.</span><span class="sxs-lookup"><span data-stu-id="b699d-166">b.</span></span> <span data-ttu-id="b699d-167">**動作類型**：選取 SMS、電子郵件或 Webhook。</span><span class="sxs-lookup"><span data-stu-id="b699d-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="b699d-168">c.</span><span class="sxs-lookup"><span data-stu-id="b699d-168">c.</span></span> <span data-ttu-id="b699d-169">**詳細資料**：根據動作類型，輸入電話號碼、電子郵件地址或 Webhook URI。</span><span class="sxs-lookup"><span data-stu-id="b699d-169">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="b699d-170">選取 [確定] 可建立警示。</span><span class="sxs-lookup"><span data-stu-id="b699d-170">Select **OK** to create the alert.</span></span>

<span data-ttu-id="b699d-171">警示需要花幾分鐘時間完全傳播，然後就會變成作用中。</span><span class="sxs-lookup"><span data-stu-id="b699d-171">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="b699d-172">新的事件符合警示的準則時，就會將它觸發。</span><span class="sxs-lookup"><span data-stu-id="b699d-172">It triggers when new events match the alert's criteria.</span></span>

<span data-ttu-id="b699d-173">如需詳細資訊，請參閱[了解活動記錄警示中使用的 Webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-173">For more information, see [Understand the webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="b699d-174">在這些步驟中定義的動作群組，會以現有動作群組的形式提供所有未來的警示定義重複使用。</span><span class="sxs-lookup"><span data-stu-id="b699d-174">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="b699d-175">使用 Azure 入口網站為現有動作群組建立活動記錄事件的警示</span><span class="sxs-lookup"><span data-stu-id="b699d-175">Create an alert on an activity log event for an existing action group by using the Azure portal</span></span>
1. <span data-ttu-id="b699d-176">請遵循上一節的步驟 1 到 7，以建立您的活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="b699d-176">Follow steps 1 through 7 in the previous section to create your activity log alert.</span></span>

2. <span data-ttu-id="b699d-177">在 [通知媒介] 下，選取 [現有] 動作群組按鈕。</span><span class="sxs-lookup"><span data-stu-id="b699d-177">Under **Notify via**, select the **Existing** action group button.</span></span> <span data-ttu-id="b699d-178">從清單中選取現有的動作群組。</span><span class="sxs-lookup"><span data-stu-id="b699d-178">Select an existing action group from the list.</span></span>

3. <span data-ttu-id="b699d-179">選取 [確定] 可建立警示。</span><span class="sxs-lookup"><span data-stu-id="b699d-179">Select **OK** to create the alert.</span></span>

<span data-ttu-id="b699d-180">警示需要花幾分鐘時間完全傳播，然後就會變成作用中。</span><span class="sxs-lookup"><span data-stu-id="b699d-180">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="b699d-181">新的事件符合警示的準則時，就會將它觸發。</span><span class="sxs-lookup"><span data-stu-id="b699d-181">It triggers when new events match the alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="b699d-182">管理您的警示</span><span class="sxs-lookup"><span data-stu-id="b699d-182">Manage your alerts</span></span>

<span data-ttu-id="b699d-183">建立警示之後，它會顯示在 [監視] 刀鋒視窗的 [警示] 區段中。</span><span class="sxs-lookup"><span data-stu-id="b699d-183">After you create an alert, it's visible in the Alerts section of the Monitor blade.</span></span> <span data-ttu-id="b699d-184">選取您要管理的警示：</span><span class="sxs-lookup"><span data-stu-id="b699d-184">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="b699d-185">進行編輯。</span><span class="sxs-lookup"><span data-stu-id="b699d-185">Edit it.</span></span>
* <span data-ttu-id="b699d-186">進行刪除。</span><span class="sxs-lookup"><span data-stu-id="b699d-186">Delete it.</span></span>
* <span data-ttu-id="b699d-187">如果您需要暫時停止或恢復接收警示的通知，可以將警示停用或啟用。</span><span class="sxs-lookup"><span data-stu-id="b699d-187">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b699d-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b699d-188">Next steps</span></span>
- <span data-ttu-id="b699d-189">取得[警示概觀](monitoring-overview-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="b699d-190">深入了解[通知速率限制](monitoring-alerts-rate-limiting.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="b699d-191">檢閱[活動記錄警示 Webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-191">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="b699d-192">深入了解[動作群組](monitoring-action-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="b699d-193">深入了解[服務健康狀態通知](monitoring-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="b699d-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="b699d-194">[建立活動記錄警示以監視訂用帳戶的所有自動調整引擎作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)。</span><span class="sxs-lookup"><span data-stu-id="b699d-194">Create an [activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="b699d-195">[建立活動記錄警示以監視訂用帳戶中所有失敗的相應縮小/相應放大自動調整作業](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)。</span><span class="sxs-lookup"><span data-stu-id="b699d-195">Create an [activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
