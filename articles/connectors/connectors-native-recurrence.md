---
title: "在邏輯應用程式中新增循環觸發程序 | Microsoft Docs"
description: "循環觸發程序的概觀，以及如何搭配 Azure 邏輯應用程式使用。"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="602e6-103">開始使用循環觸發程序</span><span class="sxs-lookup"><span data-stu-id="602e6-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="602e6-104">透過循環觸發程序，您可以在雲端建立強大的工作流程。</span><span class="sxs-lookup"><span data-stu-id="602e6-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="602e6-105">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="602e6-105">For example, you can:</span></span>

* <span data-ttu-id="602e6-106">排程讓工作流程每天執行 SQL 預存程序。</span><span class="sxs-lookup"><span data-stu-id="602e6-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="602e6-107">以電子郵件傳送過去一週內所有關於特定主題標籤之推文的摘要。</span><span class="sxs-lookup"><span data-stu-id="602e6-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="602e6-108">若要使用邏輯應用程式中的循環觸發程序來開始作業，請參閱 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="602e6-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="602e6-109">使用循環觸發程序</span><span class="sxs-lookup"><span data-stu-id="602e6-109">Use a recurrence trigger</span></span>
<span data-ttu-id="602e6-110">觸發程序是一個事件，可用來啟動邏輯應用程式中定義的工作流程。</span><span class="sxs-lookup"><span data-stu-id="602e6-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="602e6-111">[深入了解觸發程序](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="602e6-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="602e6-112">以下是如何在邏輯應用程式中設定循環觸發程序的範例順序：</span><span class="sxs-lookup"><span data-stu-id="602e6-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="602e6-113">將 **循環** 觸發程序新增為邏輯應用程式中的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="602e6-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="602e6-114">填入循環間隔的參數。</span><span class="sxs-lookup"><span data-stu-id="602e6-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="602e6-115">邏輯應用程式現在會在每個時間間隔之後啟動執行。</span><span class="sxs-lookup"><span data-stu-id="602e6-115">The logic app now starts a run after each interval of time.</span></span>

![HTTP 觸發程序](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="602e6-117">觸發程序詳細資料</span><span class="sxs-lookup"><span data-stu-id="602e6-117">Trigger details</span></span>
<span data-ttu-id="602e6-118">循環觸發程序具有下列可設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="602e6-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="602e6-119">它會在指定的時間間隔之後引發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="602e6-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="602e6-120">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="602e6-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="602e6-121">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="602e6-121">Display name</span></span> | <span data-ttu-id="602e6-122">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="602e6-122">Property name</span></span> | <span data-ttu-id="602e6-123">說明</span><span class="sxs-lookup"><span data-stu-id="602e6-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="602e6-124">頻率 *</span><span class="sxs-lookup"><span data-stu-id="602e6-124">Frequency*</span></span> |<span data-ttu-id="602e6-125">frequency</span><span class="sxs-lookup"><span data-stu-id="602e6-125">frequency</span></span> |<span data-ttu-id="602e6-126">時間單位：`Second`、`Minute`、`Hour`、`Day` 或 `Year`。</span><span class="sxs-lookup"><span data-stu-id="602e6-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="602e6-127">間隔 *</span><span class="sxs-lookup"><span data-stu-id="602e6-127">Interval*</span></span> |<span data-ttu-id="602e6-128">interval</span><span class="sxs-lookup"><span data-stu-id="602e6-128">interval</span></span> |<span data-ttu-id="602e6-129">給定循環頻率的間隔。</span><span class="sxs-lookup"><span data-stu-id="602e6-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="602e6-130">時區</span><span class="sxs-lookup"><span data-stu-id="602e6-130">Time Zone</span></span> |<span data-ttu-id="602e6-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="602e6-131">timeZone</span></span> |<span data-ttu-id="602e6-132">如果提供開始時間時未指定 UTC 時差，將會使用此時區。</span><span class="sxs-lookup"><span data-stu-id="602e6-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="602e6-133">開始時間</span><span class="sxs-lookup"><span data-stu-id="602e6-133">Start time</span></span> |<span data-ttu-id="602e6-134">startTime</span><span class="sxs-lookup"><span data-stu-id="602e6-134">startTime</span></span> |<span data-ttu-id="602e6-135">[ISO 8601 格式](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations)的開始時間。</span><span class="sxs-lookup"><span data-stu-id="602e6-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="602e6-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="602e6-136">Next steps</span></span>
<span data-ttu-id="602e6-137">立即試用平台和 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="602e6-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="602e6-138">您可以查看我們的 [API 清單](apis-list.md)，以探索邏輯應用程式中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="602e6-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

