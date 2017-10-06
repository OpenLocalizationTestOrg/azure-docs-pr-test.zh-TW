---
title: "aaaAdd hello 循環觸發程序中的 logic apps |Microsoft 文件"
description: "Hello 循環觸發程序的概觀以及如何 toouse 它與 Azure 邏輯應用程式。"
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
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="9d26b-103">開始使用 hello 循環觸發程序</span><span class="sxs-lookup"><span data-stu-id="9d26b-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="9d26b-104">藉由使用 hello 循環觸發程序，您可以建立功能強大的工作流程 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="9d26b-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="9d26b-105">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="9d26b-105">For example, you can:</span></span>

* <span data-ttu-id="9d26b-106">每日排程工作流程 toorun SQL 預存程序。</span><span class="sxs-lookup"><span data-stu-id="9d26b-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="9d26b-107">電子郵件傳送 hello 特定說明有關過去一週內的所有推文的摘要。</span><span class="sxs-lookup"><span data-stu-id="9d26b-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="9d26b-108">tooget 開始使用 hello 循環觸發程序，在邏輯應用程式，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9d26b-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="9d26b-109">使用循環觸發程序</span><span class="sxs-lookup"><span data-stu-id="9d26b-109">Use a recurrence trigger</span></span>
<span data-ttu-id="9d26b-110">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中所定義的事件。</span><span class="sxs-lookup"><span data-stu-id="9d26b-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="9d26b-111">[深入了解觸發程序](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9d26b-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="9d26b-112">以下是 tooset 向上循環觸發程序邏輯應用程式中的範例順序：</span><span class="sxs-lookup"><span data-stu-id="9d26b-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="9d26b-113">新增 hello**循環**hello 邏輯應用程式中的第一個步驟的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="9d26b-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="9d26b-114">Hello 參數填入 hello 循環間隔。</span><span class="sxs-lookup"><span data-stu-id="9d26b-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="9d26b-115">hello 邏輯應用程式啟動的每個間隔後執行。</span><span class="sxs-lookup"><span data-stu-id="9d26b-115">hello logic app now starts a run after each interval of time.</span></span>

![HTTP 觸發程序](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="9d26b-117">觸發程序詳細資料</span><span class="sxs-lookup"><span data-stu-id="9d26b-117">Trigger details</span></span>
<span data-ttu-id="9d26b-118">hello 循環觸發程序有下列屬性，您可以設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="9d26b-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="9d26b-119">它會在指定的時間間隔之後引發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d26b-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="9d26b-120">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="9d26b-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="9d26b-121">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="9d26b-121">Display name</span></span> | <span data-ttu-id="9d26b-122">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="9d26b-122">Property name</span></span> | <span data-ttu-id="9d26b-123">說明</span><span class="sxs-lookup"><span data-stu-id="9d26b-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9d26b-124">頻率 *</span><span class="sxs-lookup"><span data-stu-id="9d26b-124">Frequency*</span></span> |<span data-ttu-id="9d26b-125">frequency</span><span class="sxs-lookup"><span data-stu-id="9d26b-125">frequency</span></span> |<span data-ttu-id="9d26b-126">時間單位 hello: `Second`， `Minute`， `Hour`， `Day`，或`Year`。</span><span class="sxs-lookup"><span data-stu-id="9d26b-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="9d26b-127">間隔 *</span><span class="sxs-lookup"><span data-stu-id="9d26b-127">Interval*</span></span> |<span data-ttu-id="9d26b-128">interval</span><span class="sxs-lookup"><span data-stu-id="9d26b-128">interval</span></span> |<span data-ttu-id="9d26b-129">hello hello 給 hello 循環頻率間隔。</span><span class="sxs-lookup"><span data-stu-id="9d26b-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="9d26b-130">時區</span><span class="sxs-lookup"><span data-stu-id="9d26b-130">Time Zone</span></span> |<span data-ttu-id="9d26b-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="9d26b-131">timeZone</span></span> |<span data-ttu-id="9d26b-132">如果提供開始時間時未指定 UTC 時差，將會使用此時區。</span><span class="sxs-lookup"><span data-stu-id="9d26b-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="9d26b-133">開始時間</span><span class="sxs-lookup"><span data-stu-id="9d26b-133">Start time</span></span> |<span data-ttu-id="9d26b-134">startTime</span><span class="sxs-lookup"><span data-stu-id="9d26b-134">startTime</span></span> |<span data-ttu-id="9d26b-135">hello 的開始時間[ISO 8601 格式](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations)。</span><span class="sxs-lookup"><span data-stu-id="9d26b-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="9d26b-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d26b-136">Next steps</span></span>
<span data-ttu-id="9d26b-137">現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9d26b-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="9d26b-138">您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="9d26b-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

