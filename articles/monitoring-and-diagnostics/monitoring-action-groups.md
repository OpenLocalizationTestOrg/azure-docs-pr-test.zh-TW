---
title: "aaaCreate 及管理在 hello Azure 入口網站中的動作群組 |Microsoft 文件"
description: "深入了解如何 toocreate 及管理在 hello Azure 入口網站中的動作群組。"
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
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="74e31-103">建立及管理在 hello Azure 入口網站中的動作群組</span><span class="sxs-lookup"><span data-stu-id="74e31-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="74e31-104">概觀</span><span class="sxs-lookup"><span data-stu-id="74e31-104">Overview</span></span> ##
<span data-ttu-id="74e31-105">本文章將示範如何 toocreate 及管理在 hello Azure 入口網站中的動作群組。</span><span class="sxs-lookup"><span data-stu-id="74e31-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="74e31-106">您可以設定包含動作群組的動作清單。</span><span class="sxs-lookup"><span data-stu-id="74e31-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="74e31-107">接著，當您定義活動記錄警示時，可以使用這些群組。</span><span class="sxs-lookup"><span data-stu-id="74e31-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="74e31-108">這些群組則是每個活動記錄警示定義，請確保該 hello 會執行相同動作每次觸發 hello 活動記錄警示時重複使用。</span><span class="sxs-lookup"><span data-stu-id="74e31-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="74e31-109">動作群組可以有向上 too10 的每個動作類型。</span><span class="sxs-lookup"><span data-stu-id="74e31-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="74e31-110">每個動作所組成的 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="74e31-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="74e31-111">**名稱**: hello 動作群組內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="74e31-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="74e31-112">**動作類型**：傳送 SMS、傳送電子郵件或呼叫 Webhook。</span><span class="sxs-lookup"><span data-stu-id="74e31-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="74e31-113">**詳細資料**: hello 相對應的電話號碼、 電子郵件地址或 webhook URI。</span><span class="sxs-lookup"><span data-stu-id="74e31-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="74e31-114">如需詳細資訊 toouse Azure Resource Manager 範本 tooconfigure 動作群組，請參閱[動作群組的資源管理員範本](monitoring-create-action-group-with-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="74e31-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="74e31-115">使用 hello Azure 入口網站建立的動作群組</span><span class="sxs-lookup"><span data-stu-id="74e31-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="74e31-116">在 hello[入口網站](https://portal.azure.com)，選取**監視器**。</span><span class="sxs-lookup"><span data-stu-id="74e31-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="74e31-117">hello**監視器**刀鋒視窗中將合併所有將監視設定和資料在一個檢視中的。</span><span class="sxs-lookup"><span data-stu-id="74e31-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![hello 「 監視 」 服務](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="74e31-119">在 hello**活動記錄檔**區段中，選取**動作群組**。</span><span class="sxs-lookup"><span data-stu-id="74e31-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![hello 「 動作群組 」 索引標籤](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="74e31-121">選取**加入動作群組**，並填入 hello 欄位中。</span><span class="sxs-lookup"><span data-stu-id="74e31-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![hello 「 新增動作群組 」 命令](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="74e31-123">輸入的名稱在 hello**動作群組名稱**，然後輸入的名稱在 hello**簡短名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="74e31-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="74e31-124">hello 簡短名稱是在使用這個群組會傳送通知時，使用完整的動作群組名稱取代。</span><span class="sxs-lookup"><span data-stu-id="74e31-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![hello 新增動作群組 對話方塊](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="74e31-126">hello**訂用帳戶**方塊 autofills 與您目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="74e31-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="74e31-127">此訂用帳戶中儲存的 hello 動作群組是 hello 其中一個。</span><span class="sxs-lookup"><span data-stu-id="74e31-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="74e31-128">選取 hello**資源群組**hello 動作在儲存群組。</span><span class="sxs-lookup"><span data-stu-id="74e31-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="74e31-129">針對每個動作提供下列資訊，來定義動作的清單：</span><span class="sxs-lookup"><span data-stu-id="74e31-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="74e31-130">a.</span><span class="sxs-lookup"><span data-stu-id="74e31-130">a.</span></span> <span data-ttu-id="74e31-131">**名稱**：輸入此動作的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="74e31-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="74e31-132">b.</span><span class="sxs-lookup"><span data-stu-id="74e31-132">b.</span></span> <span data-ttu-id="74e31-133">**動作類型**：選取 SMS、電子郵件或 Webhook。</span><span class="sxs-lookup"><span data-stu-id="74e31-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="74e31-134">c.</span><span class="sxs-lookup"><span data-stu-id="74e31-134">c.</span></span> <span data-ttu-id="74e31-135">**詳細資料**： 根據 hello 動作類型，輸入電話號碼、 電子郵件地址或 webhook URI。</span><span class="sxs-lookup"><span data-stu-id="74e31-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="74e31-136">選取**確定**toocreate hello 動作群組。</span><span class="sxs-lookup"><span data-stu-id="74e31-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="74e31-137">管理您的動作群組</span><span class="sxs-lookup"><span data-stu-id="74e31-137">Manage your action groups</span></span> ##
<span data-ttu-id="74e31-138">建立動作群組之後，會顯示在 hello**動作群組**區段 hello**監視器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="74e31-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="74e31-139">選取您想要 toomanage hello 動作群組：</span><span class="sxs-lookup"><span data-stu-id="74e31-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="74e31-140">新增、編輯或移除動作。</span><span class="sxs-lookup"><span data-stu-id="74e31-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="74e31-141">刪除 hello 動作群組。</span><span class="sxs-lookup"><span data-stu-id="74e31-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74e31-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74e31-142">Next steps</span></span> ##
* <span data-ttu-id="74e31-143">進一步了解 [SMS 警示行為](monitoring-sms-alert-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="74e31-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="74e31-144">取得[hello 活動記錄警示 webhook 結構描述的了解](monitoring-activity-log-alerts-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="74e31-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="74e31-145">深入了解警示的[速率限制](monitoring-alerts-rate-limiting.md)。</span><span class="sxs-lookup"><span data-stu-id="74e31-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="74e31-146">取得[活動記錄檔警示概觀](monitoring-overview-alerts.md)，並了解如何 tooreceive 警示。</span><span class="sxs-lookup"><span data-stu-id="74e31-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="74e31-147">了解如何太[設定警示，每當張貼服務健康情況通知](monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="74e31-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
