---
title: "在邏輯應用程式中新增延遲 | Microsoft Docs"
description: "延遲和延遲直到動作的概觀，以及如何搭配 Azure 邏輯應用程式使用它們。"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="e1773-103">開始使用延遲和延遲直到動作</span><span class="sxs-lookup"><span data-stu-id="e1773-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="e1773-104">透過延遲和「延遲直到」動作，您可以完成工作流程案例。</span><span class="sxs-lookup"><span data-stu-id="e1773-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="e1773-105">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="e1773-105">For example, you can:</span></span>

* <span data-ttu-id="e1773-106">等到工作日再透過電子郵件傳送狀態更新。</span><span class="sxs-lookup"><span data-stu-id="e1773-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="e1773-107">延遲工作流程，直到 HTTP 呼叫有時間來完成，才繼續進行並擷取結果。</span><span class="sxs-lookup"><span data-stu-id="e1773-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="e1773-108">若要開始在邏輯應用程式中使用延遲動作，請參閱 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="e1773-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="e1773-109">使用延遲動作</span><span class="sxs-lookup"><span data-stu-id="e1773-109">Use the delay actions</span></span>
<span data-ttu-id="e1773-110">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="e1773-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="e1773-111">[深入了解動作](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e1773-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="e1773-112">以下是如何在邏輯應用程式中使用延遲步驟的範例順序︰</span><span class="sxs-lookup"><span data-stu-id="e1773-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="e1773-113">在新增觸發程序之後，按一下 [新增步驟]  以新增動作。</span><span class="sxs-lookup"><span data-stu-id="e1773-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="e1773-114">搜尋「延遲」  以顯示延遲動作。</span><span class="sxs-lookup"><span data-stu-id="e1773-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="e1773-115">在此範例中，我們將會選取 [延遲] 。</span><span class="sxs-lookup"><span data-stu-id="e1773-115">In this example, we will select **Delay**.</span></span>
   
    ![延遲動作](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="e1773-117">完成任何動作屬性以設定延遲。</span><span class="sxs-lookup"><span data-stu-id="e1773-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![延遲設定](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="e1773-119">按一下 [儲存]  來發佈及啟動邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1773-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="e1773-120">動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="e1773-120">Action details</span></span>
<span data-ttu-id="e1773-121">循環觸發程序具有下列可設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="e1773-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="e1773-122">延遲動作</span><span class="sxs-lookup"><span data-stu-id="e1773-122">Delay action</span></span>
<span data-ttu-id="e1773-123">此動作會讓執行延遲一段時間間隔。</span><span class="sxs-lookup"><span data-stu-id="e1773-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="e1773-124">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="e1773-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="e1773-125">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="e1773-125">Display name</span></span> | <span data-ttu-id="e1773-126">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e1773-126">Property name</span></span> | <span data-ttu-id="e1773-127">說明</span><span class="sxs-lookup"><span data-stu-id="e1773-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1773-128">計數 *</span><span class="sxs-lookup"><span data-stu-id="e1773-128">Count*</span></span> |<span data-ttu-id="e1773-129">count</span><span class="sxs-lookup"><span data-stu-id="e1773-129">count</span></span> |<span data-ttu-id="e1773-130">要延遲的時間單位數</span><span class="sxs-lookup"><span data-stu-id="e1773-130">The number of time units to delay</span></span> |
| <span data-ttu-id="e1773-131">單位 *</span><span class="sxs-lookup"><span data-stu-id="e1773-131">Unit*</span></span> |<span data-ttu-id="e1773-132">unit</span><span class="sxs-lookup"><span data-stu-id="e1773-132">unit</span></span> |<span data-ttu-id="e1773-133">時間單位：`Second`、`Minute`、`Hour` 或 `Day`</span><span class="sxs-lookup"><span data-stu-id="e1773-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="e1773-134">延遲直到動作</span><span class="sxs-lookup"><span data-stu-id="e1773-134">Delay-until action</span></span>
<span data-ttu-id="e1773-135">此動作會讓執行延遲到指定的日期/時間。</span><span class="sxs-lookup"><span data-stu-id="e1773-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="e1773-136">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="e1773-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="e1773-137">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="e1773-137">Display name</span></span> | <span data-ttu-id="e1773-138">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e1773-138">Property name</span></span> | <span data-ttu-id="e1773-139">說明</span><span class="sxs-lookup"><span data-stu-id="e1773-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1773-140">年 *</span><span class="sxs-lookup"><span data-stu-id="e1773-140">Year*</span></span> |<span data-ttu-id="e1773-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="e1773-141">timestamp</span></span> |<span data-ttu-id="e1773-142">要延遲到的年度 (GMT)</span><span class="sxs-lookup"><span data-stu-id="e1773-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="e1773-143">月 *</span><span class="sxs-lookup"><span data-stu-id="e1773-143">Month*</span></span> |<span data-ttu-id="e1773-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="e1773-144">timestamp</span></span> |<span data-ttu-id="e1773-145">要延遲到的月份 (GMT)</span><span class="sxs-lookup"><span data-stu-id="e1773-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="e1773-146">日 *</span><span class="sxs-lookup"><span data-stu-id="e1773-146">Day*</span></span> |<span data-ttu-id="e1773-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="e1773-147">timestamp</span></span> |<span data-ttu-id="e1773-148">要延遲到的日期 (GMT)</span><span class="sxs-lookup"><span data-stu-id="e1773-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="e1773-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1773-149">Next steps</span></span>
<span data-ttu-id="e1773-150">立即試用平台和 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="e1773-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e1773-151">您可以查看我們的 [API 清單](apis-list.md)，以探索邏輯應用程式中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="e1773-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

