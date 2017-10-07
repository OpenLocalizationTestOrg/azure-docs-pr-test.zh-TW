---
title: "邏輯應用程式中的延遲 aaaAdd |Microsoft 文件"
description: "Hello 概觀延遲和延遲的動作，直到以及如何 toouse 其與 Azure 邏輯應用程式。"
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
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="4d68e-103">開始使用 hello 延遲，並且延遲-直到動作</span><span class="sxs-lookup"><span data-stu-id="4d68e-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="4d68e-104">使用 hello 延遲和 「 延遲-直到 」 動作，您可以完成的工作流程案例。</span><span class="sxs-lookup"><span data-stu-id="4d68e-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="4d68e-105">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="4d68e-105">For example, you can:</span></span>

* <span data-ttu-id="4d68e-106">請等到工作日 toosend 狀態更新透過電子郵件。</span><span class="sxs-lookup"><span data-stu-id="4d68e-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="4d68e-107">HTTP 呼叫的延遲 hello 工作流程有時間 toofinish 之前繼續並擷取 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="4d68e-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="4d68e-108">請參閱 < 開始使用邏輯應用程式中的 hello 動作延遲 tooget[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="4d68e-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="4d68e-109">使用 hello 延遲的動作</span><span class="sxs-lookup"><span data-stu-id="4d68e-109">Use hello delay actions</span></span>
<span data-ttu-id="4d68e-110">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="4d68e-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="4d68e-111">[深入了解動作](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4d68e-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="4d68e-112">以下是如何 toouse 延遲步驟在邏輯應用程式中的範例順序：</span><span class="sxs-lookup"><span data-stu-id="4d68e-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="4d68e-113">新增觸發程序後, 按一下**新步驟**tooadd 動作。</span><span class="sxs-lookup"><span data-stu-id="4d68e-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="4d68e-114">搜尋**延遲**toobring 向上 hello 延遲的動作。</span><span class="sxs-lookup"><span data-stu-id="4d68e-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="4d68e-115">在此範例中，我們將會選取 [延遲] 。</span><span class="sxs-lookup"><span data-stu-id="4d68e-115">In this example, we will select **Delay**.</span></span>
   
    ![延遲動作](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="4d68e-117">完成所有 hello 動作屬性 tooconfigure hello 延遲。</span><span class="sxs-lookup"><span data-stu-id="4d68e-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![延遲設定](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="4d68e-119">按一下**儲存**toopublish 並啟用 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d68e-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="4d68e-120">動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="4d68e-120">Action details</span></span>
<span data-ttu-id="4d68e-121">hello 循環觸發程序有下列屬性可設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="4d68e-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="4d68e-122">延遲動作</span><span class="sxs-lookup"><span data-stu-id="4d68e-122">Delay action</span></span>
<span data-ttu-id="4d68e-123">針對一段時間間隔執行此動作的延遲 hello。</span><span class="sxs-lookup"><span data-stu-id="4d68e-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="4d68e-124">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="4d68e-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="4d68e-125">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="4d68e-125">Display name</span></span> | <span data-ttu-id="4d68e-126">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="4d68e-126">Property name</span></span> | <span data-ttu-id="4d68e-127">說明</span><span class="sxs-lookup"><span data-stu-id="4d68e-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d68e-128">計數 *</span><span class="sxs-lookup"><span data-stu-id="4d68e-128">Count*</span></span> |<span data-ttu-id="4d68e-129">計數</span><span class="sxs-lookup"><span data-stu-id="4d68e-129">count</span></span> |<span data-ttu-id="4d68e-130">時間單位 toodelay 的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="4d68e-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="4d68e-131">單位 *</span><span class="sxs-lookup"><span data-stu-id="4d68e-131">Unit*</span></span> |<span data-ttu-id="4d68e-132">unit</span><span class="sxs-lookup"><span data-stu-id="4d68e-132">unit</span></span> |<span data-ttu-id="4d68e-133">時間單位 hello: `Second`， `Minute`， `Hour`，或`Day`</span><span class="sxs-lookup"><span data-stu-id="4d68e-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="4d68e-134">延遲直到動作</span><span class="sxs-lookup"><span data-stu-id="4d68e-134">Delay-until action</span></span>
<span data-ttu-id="4d68e-135">這個動作會延遲到指定的日期/時間執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="4d68e-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="4d68e-136">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="4d68e-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="4d68e-137">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="4d68e-137">Display name</span></span> | <span data-ttu-id="4d68e-138">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="4d68e-138">Property name</span></span> | <span data-ttu-id="4d68e-139">說明</span><span class="sxs-lookup"><span data-stu-id="4d68e-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d68e-140">年 *</span><span class="sxs-lookup"><span data-stu-id="4d68e-140">Year*</span></span> |<span data-ttu-id="4d68e-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="4d68e-141">timestamp</span></span> |<span data-ttu-id="4d68e-142">(GMT) 直到 hello 年 toodelay</span><span class="sxs-lookup"><span data-stu-id="4d68e-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="4d68e-143">月 *</span><span class="sxs-lookup"><span data-stu-id="4d68e-143">Month*</span></span> |<span data-ttu-id="4d68e-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="4d68e-144">timestamp</span></span> |<span data-ttu-id="4d68e-145">(GMT) 直到 hello 月份 toodelay</span><span class="sxs-lookup"><span data-stu-id="4d68e-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="4d68e-146">日 *</span><span class="sxs-lookup"><span data-stu-id="4d68e-146">Day*</span></span> |<span data-ttu-id="4d68e-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="4d68e-147">timestamp</span></span> |<span data-ttu-id="4d68e-148">(GMT) 直到 hello 天 toodelay</span><span class="sxs-lookup"><span data-stu-id="4d68e-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="4d68e-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d68e-149">Next steps</span></span>
<span data-ttu-id="4d68e-150">現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="4d68e-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="4d68e-151">您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="4d68e-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

