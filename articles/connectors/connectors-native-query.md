---
title: "在邏輯應用程式中新增查詢動作 | Microsoft Docs"
description: "執行如篩選陣列等動作的查詢動作概觀。"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: a992fa17a07d6167297c4cf5fe9fb3b58181d7df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="8bc86-103">開始使用查詢動作</span><span class="sxs-lookup"><span data-stu-id="8bc86-103">Get started with the query action</span></span>
<span data-ttu-id="8bc86-104">您可以使用查詢動作來處理完成以下工作流程的批次和陣列︰</span><span class="sxs-lookup"><span data-stu-id="8bc86-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="8bc86-105">從資料庫建立所有高優先順序記錄的工作。</span><span class="sxs-lookup"><span data-stu-id="8bc86-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="8bc86-106">將電子郵件的所有 PDF 附件儲存到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="8bc86-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="8bc86-107">若要開始在邏輯應用程式中使用查詢動作，請參閱 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="8bc86-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="8bc86-108">使用查詢動作</span><span class="sxs-lookup"><span data-stu-id="8bc86-108">Use the query action</span></span>
<span data-ttu-id="8bc86-109">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="8bc86-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="8bc86-110">[深入了解動作](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8bc86-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="8bc86-111">查詢動作目前在設計工具中公開一項作業 (名為篩選陣列)。</span><span class="sxs-lookup"><span data-stu-id="8bc86-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="8bc86-112">這可讓您查詢陣列並傳回一組篩選結果。</span><span class="sxs-lookup"><span data-stu-id="8bc86-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="8bc86-113">以下說明如何將它新增至邏輯應用程式︰</span><span class="sxs-lookup"><span data-stu-id="8bc86-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="8bc86-114">選取 [新增步驟]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bc86-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="8bc86-115">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="8bc86-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="8bc86-116">在動作搜尋方塊中，輸入**篩選**以列出**篩選陣列**動作。</span><span class="sxs-lookup"><span data-stu-id="8bc86-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![使用查詢動作](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="8bc86-118">選取要篩選的陣列</span><span class="sxs-lookup"><span data-stu-id="8bc86-118">Select an array to filter.</span></span> <span data-ttu-id="8bc86-119">(以下螢幕擷取畫面顯示來自 Twitter 搜尋的結果陣列)。</span><span class="sxs-lookup"><span data-stu-id="8bc86-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="8bc86-120">建立要針對每個項目評估的條件</span><span class="sxs-lookup"><span data-stu-id="8bc86-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="8bc86-121">(以下螢幕擷取畫面會篩選來自有 100 個以上追隨者之使用者的推文)。</span><span class="sxs-lookup"><span data-stu-id="8bc86-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![使用查詢動作](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="8bc86-123">此動作會輸出新的陣列，其中僅包含符合篩選條件需求的結果。</span><span class="sxs-lookup"><span data-stu-id="8bc86-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="8bc86-124">按一下工具列左上角以便儲存，然後邏輯應用程式便會儲存並發佈 (啟動)。</span><span class="sxs-lookup"><span data-stu-id="8bc86-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="8bc86-125">查詢動作</span><span class="sxs-lookup"><span data-stu-id="8bc86-125">Query action</span></span>
<span data-ttu-id="8bc86-126">以下是此連接器所支援動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8bc86-126">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="8bc86-127">連接器有一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="8bc86-127">The connector has one possible action.</span></span>

| <span data-ttu-id="8bc86-128">動作</span><span class="sxs-lookup"><span data-stu-id="8bc86-128">Action</span></span> | <span data-ttu-id="8bc86-129">說明</span><span class="sxs-lookup"><span data-stu-id="8bc86-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8bc86-130">篩選陣列</span><span class="sxs-lookup"><span data-stu-id="8bc86-130">Filter array</span></span> |<span data-ttu-id="8bc86-131">評估陣列中的每個項目是否符合條件並傳回結果</span><span class="sxs-lookup"><span data-stu-id="8bc86-131">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="8bc86-132">動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="8bc86-132">Action details</span></span>
<span data-ttu-id="8bc86-133">查詢動作隨附 1 個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="8bc86-133">The query action comes with one possible action.</span></span> <span data-ttu-id="8bc86-134">下表說明動作的必要與選擇性輸入欄位，以及與使用動作相關聯的對應輸出詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8bc86-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="8bc86-135">篩選陣列</span><span class="sxs-lookup"><span data-stu-id="8bc86-135">Filter array</span></span>
<span data-ttu-id="8bc86-136">以下是動作的輸入欄位，可進行 HTTP 輸出要求。</span><span class="sxs-lookup"><span data-stu-id="8bc86-136">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="8bc86-137">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="8bc86-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="8bc86-138">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="8bc86-138">Display name</span></span> | <span data-ttu-id="8bc86-139">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="8bc86-139">Property name</span></span> | <span data-ttu-id="8bc86-140">說明</span><span class="sxs-lookup"><span data-stu-id="8bc86-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bc86-141">從*</span><span class="sxs-lookup"><span data-stu-id="8bc86-141">From*</span></span> |<span data-ttu-id="8bc86-142">from</span><span class="sxs-lookup"><span data-stu-id="8bc86-142">from</span></span> |<span data-ttu-id="8bc86-143">要篩選的陣列</span><span class="sxs-lookup"><span data-stu-id="8bc86-143">The array to filter</span></span> |
| <span data-ttu-id="8bc86-144">條件*</span><span class="sxs-lookup"><span data-stu-id="8bc86-144">Condition*</span></span> |<span data-ttu-id="8bc86-145">其中</span><span class="sxs-lookup"><span data-stu-id="8bc86-145">where</span></span> |<span data-ttu-id="8bc86-146">要針對每個項目評估的條件</span><span class="sxs-lookup"><span data-stu-id="8bc86-146">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="8bc86-147">輸出詳細資料</span><span class="sxs-lookup"><span data-stu-id="8bc86-147">Output details</span></span>
<span data-ttu-id="8bc86-148">以下是 HTTP 回應的輸出詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8bc86-148">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="8bc86-149">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="8bc86-149">Property name</span></span> | <span data-ttu-id="8bc86-150">資料類型</span><span class="sxs-lookup"><span data-stu-id="8bc86-150">Data type</span></span> | <span data-ttu-id="8bc86-151">說明</span><span class="sxs-lookup"><span data-stu-id="8bc86-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bc86-152">篩選的陣列</span><span class="sxs-lookup"><span data-stu-id="8bc86-152">Filtered array</span></span> |<span data-ttu-id="8bc86-153">array</span><span class="sxs-lookup"><span data-stu-id="8bc86-153">array</span></span> |<span data-ttu-id="8bc86-154">陣列，其中包含每筆篩選結果的物件</span><span class="sxs-lookup"><span data-stu-id="8bc86-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8bc86-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8bc86-155">Next steps</span></span>
<span data-ttu-id="8bc86-156">立即試用平台和 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="8bc86-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="8bc86-157">您可以查看我們的 [API 清單](apis-list.md)，以探索邏輯應用程式中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="8bc86-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

