---
title: "在 Azure 入口網站中建立和管理動作群組 | Microsoft Docs"
description: "了解如何在 Azure 入口網站中建立和管理動作群組。"
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: ea15705bf02d9773507c6cb59f2da4c1dd0f9d77
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a><span data-ttu-id="37ba0-103">在 Azure 入口網站中建立和管理動作群組</span><span class="sxs-lookup"><span data-stu-id="37ba0-103">Create and manage action groups in the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="37ba0-104">概觀</span><span class="sxs-lookup"><span data-stu-id="37ba0-104">Overview</span></span> ##
<span data-ttu-id="37ba0-105">本文將說明如何在 Azure 入口網站中建立和管理動作群組。</span><span class="sxs-lookup"><span data-stu-id="37ba0-105">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="37ba0-106">您可以設定包含動作群組的動作清單。</span><span class="sxs-lookup"><span data-stu-id="37ba0-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="37ba0-107">接著，當您定義活動記錄警示時，可以使用這些群組。</span><span class="sxs-lookup"><span data-stu-id="37ba0-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="37ba0-108">然後您所定義的每個活動記錄警示就可以使用這些群組，確保在每次觸發活動記錄警示時皆採取相同的動作。</span><span class="sxs-lookup"><span data-stu-id="37ba0-108">These groups can then be reused by each activity log alert you define, ensuring that the same actions are taken each time the activity log alert is triggered.</span></span>

<span data-ttu-id="37ba0-109">動作群組的每個動作類型可以有多達 10 個。</span><span class="sxs-lookup"><span data-stu-id="37ba0-109">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="37ba0-110">每個動作是由下列屬性所組成：</span><span class="sxs-lookup"><span data-stu-id="37ba0-110">Each action is made up of the following properties:</span></span>

* <span data-ttu-id="37ba0-111">**名稱**：動作群組內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="37ba0-111">**Name**: A unique identifier within the action group.</span></span>  
* <span data-ttu-id="37ba0-112">**動作類型**：傳送 SMS、傳送電子郵件或呼叫 Webhook。</span><span class="sxs-lookup"><span data-stu-id="37ba0-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="37ba0-113">**詳細資料**：對應的電話號碼、電子郵件地址或 Webhook URI。</span><span class="sxs-lookup"><span data-stu-id="37ba0-113">**Details**: The corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="37ba0-114">如需如何使用 Azure Resource Manager 範本設定動作群組的資訊，請參閱[動作群組 Resource Manager 範本](monitoring-create-action-group-with-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="37ba0-114">For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-the-azure-portal"></a><span data-ttu-id="37ba0-115">使用 Azure 入口網站建立動作群組</span><span class="sxs-lookup"><span data-stu-id="37ba0-115">Create an action group by using the Azure portal</span></span> ##
1. <span data-ttu-id="37ba0-116">在 [入口網站](https://portal.azure.com) 中，選取 [監視]。</span><span class="sxs-lookup"><span data-stu-id="37ba0-116">In the [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="37ba0-117">[監視] 刀鋒視窗會將所有監視設定和資料合併在一個檢視中。</span><span class="sxs-lookup"><span data-stu-id="37ba0-117">The **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![「監視」服務](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="37ba0-119">在 [活動記錄] 區段中，選取 [動作群組]。</span><span class="sxs-lookup"><span data-stu-id="37ba0-119">In the **Activity log** section, select **Action groups**.</span></span>

    ![使用 [動作群組] 索引標籤](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="37ba0-121">選取 [新增動作群組]，並填寫各欄位。</span><span class="sxs-lookup"><span data-stu-id="37ba0-121">Select **Add action group**, and fill in the fields.</span></span>

    ![「新增動作群組」命令](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="37ba0-123">在 [動作群組名稱] 方塊中輸入名稱，然後在 [簡短名稱] 方塊中，輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="37ba0-123">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="37ba0-124">使用這個群組傳送通知時，會使用簡短名稱來取代完整的動作群組名稱。</span><span class="sxs-lookup"><span data-stu-id="37ba0-124">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![「新增動作群組」對話方塊](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="37ba0-126">[訂用帳戶] 方塊會自動填入您目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="37ba0-126">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="37ba0-127">訂用帳戶是要儲存動作群組的位置。</span><span class="sxs-lookup"><span data-stu-id="37ba0-127">This subscription is the one in which the action group is saved.</span></span>

6. <span data-ttu-id="37ba0-128">選取要在其中儲存動作群組的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="37ba0-128">Select the **Resource group** in which the action group is saved.</span></span>

7. <span data-ttu-id="37ba0-129">針對每個動作提供下列資訊，來定義動作的清單：</span><span class="sxs-lookup"><span data-stu-id="37ba0-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="37ba0-130">a.</span><span class="sxs-lookup"><span data-stu-id="37ba0-130">a.</span></span> <span data-ttu-id="37ba0-131">**名稱**：輸入此動作的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="37ba0-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="37ba0-132">b.</span><span class="sxs-lookup"><span data-stu-id="37ba0-132">b.</span></span> <span data-ttu-id="37ba0-133">**動作類型**：選取 SMS、電子郵件或 Webhook。</span><span class="sxs-lookup"><span data-stu-id="37ba0-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="37ba0-134">c.</span><span class="sxs-lookup"><span data-stu-id="37ba0-134">c.</span></span> <span data-ttu-id="37ba0-135">**詳細資料**：根據動作類型，輸入電話號碼、電子郵件地址或 Webhook URI。</span><span class="sxs-lookup"><span data-stu-id="37ba0-135">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="37ba0-136">選取 [確定] 來建立動作群組。</span><span class="sxs-lookup"><span data-stu-id="37ba0-136">Select **OK** to create the action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="37ba0-137">管理您的動作群組</span><span class="sxs-lookup"><span data-stu-id="37ba0-137">Manage your action groups</span></span> ##
<span data-ttu-id="37ba0-138">建立動作群組之後，將會在 [監視] 刀鋒視窗的 [動作群組] 區段中顯示。</span><span class="sxs-lookup"><span data-stu-id="37ba0-138">After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade.</span></span> <span data-ttu-id="37ba0-139">選取您要管理的動作群組：</span><span class="sxs-lookup"><span data-stu-id="37ba0-139">Select the action group you want to manage to:</span></span>

* <span data-ttu-id="37ba0-140">新增、編輯或移除動作。</span><span class="sxs-lookup"><span data-stu-id="37ba0-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="37ba0-141">刪除動作群組。</span><span class="sxs-lookup"><span data-stu-id="37ba0-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37ba0-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37ba0-142">Next steps</span></span> ##
* <span data-ttu-id="37ba0-143">進一步了解 [SMS 警示行為](monitoring-sms-alert-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="37ba0-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="37ba0-144">了解[活動記錄警示 Webhook 結構描述](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="37ba0-144">Gain an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="37ba0-145">深入了解警示的[速率限制](monitoring-alerts-rate-limiting.md)。</span><span class="sxs-lookup"><span data-stu-id="37ba0-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="37ba0-146">取得[活動記錄警示的概觀](monitoring-overview-alerts.md)，並了解如何收到警示。</span><span class="sxs-lookup"><span data-stu-id="37ba0-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="37ba0-147">了解如何[設定每當服務健康狀態通知公佈時的警示](monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="37ba0-147">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
