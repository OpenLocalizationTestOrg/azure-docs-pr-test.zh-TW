---
title: "中的 logic apps aaaAdd hello 查詢動作 |Microsoft 文件"
description: "Hello 查詢動作執行動作篩選條件陣列類似的概觀。"
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
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="72810-103">開始使用 hello 查詢動作</span><span class="sxs-lookup"><span data-stu-id="72810-103">Get started with hello query action</span></span>
<span data-ttu-id="72810-104">藉由使用 hello 查詢動作，您可以使用批次和陣列 tooaccomplish 的工作流程：</span><span class="sxs-lookup"><span data-stu-id="72810-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="72810-105">從資料庫建立所有高優先順序記錄的工作。</span><span class="sxs-lookup"><span data-stu-id="72810-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="72810-106">將電子郵件的所有 PDF 附件儲存到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="72810-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="72810-107">請參閱 < 開始使用邏輯應用程式中的 hello 查詢動作 tooget[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="72810-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="72810-108">使用 hello 查詢動作</span><span class="sxs-lookup"><span data-stu-id="72810-108">Use hello query action</span></span>
<span data-ttu-id="72810-109">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="72810-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="72810-110">[深入了解動作](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="72810-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="72810-111">目前的 hello 查詢動作都有一個稱為 hello 篩選陣列、 在 hello 設計工具中公開的作業。</span><span class="sxs-lookup"><span data-stu-id="72810-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="72810-112">這可讓您 tooquery 陣列並傳回一組的篩選結果。</span><span class="sxs-lookup"><span data-stu-id="72810-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="72810-113">以下說明如何將它新增至邏輯應用程式︰</span><span class="sxs-lookup"><span data-stu-id="72810-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="72810-114">選取 hello**新步驟** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="72810-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="72810-115">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="72810-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="72810-116">在 hello 動作搜尋方塊中，輸入**篩選**toolist hello**篩選陣列**動作。</span><span class="sxs-lookup"><span data-stu-id="72810-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![選取 hello 查詢動作](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="72810-118">選取陣列 toofilter。</span><span class="sxs-lookup"><span data-stu-id="72810-118">Select an array toofilter.</span></span> <span data-ttu-id="72810-119">（hello 下列螢幕擷取畫面顯示 hello Twitter 搜尋結果陣列）。</span><span class="sxs-lookup"><span data-stu-id="72810-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="72810-120">建立條件 tooevaluate 上每個項目。</span><span class="sxs-lookup"><span data-stu-id="72810-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="72810-121">（下列螢幕擷取畫面的 hello 篩選具有 100 個以上的實行項目之使用者的推文）。</span><span class="sxs-lookup"><span data-stu-id="72810-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![完整的 hello 查詢動作](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="72810-123">hello 動作會輸出新的陣列，其中包含符合 hello 篩選需求的結果。</span><span class="sxs-lookup"><span data-stu-id="72810-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="72810-124">按一下 hello 左上角 hello 工具列 toosave 和您邏輯應用程式會同時將儲存並發行 （啟動）。</span><span class="sxs-lookup"><span data-stu-id="72810-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="72810-125">查詢動作</span><span class="sxs-lookup"><span data-stu-id="72810-125">Query action</span></span>
<span data-ttu-id="72810-126">以下是此連接器支援的 hello 動作的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="72810-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="72810-127">hello 連接器有一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="72810-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="72810-128">動作</span><span class="sxs-lookup"><span data-stu-id="72810-128">Action</span></span> | <span data-ttu-id="72810-129">說明</span><span class="sxs-lookup"><span data-stu-id="72810-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="72810-130">篩選陣列</span><span class="sxs-lookup"><span data-stu-id="72810-130">Filter array</span></span> |<span data-ttu-id="72810-131">評估的條件陣列中每個項目，並傳回 hello 結果</span><span class="sxs-lookup"><span data-stu-id="72810-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="72810-132">動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="72810-132">Action details</span></span>
<span data-ttu-id="72810-133">hello 查詢動作隨附一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="72810-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="72810-134">hello 下列表格說明必要的 hello 與 hello 動作和 hello 對應輸出的詳細資料與使用 hello 動作相關聯的選擇性輸入的欄位。</span><span class="sxs-lookup"><span data-stu-id="72810-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="72810-135">篩選陣列</span><span class="sxs-lookup"><span data-stu-id="72810-135">Filter array</span></span>
<span data-ttu-id="72810-136">hello 如下 hello 動作，使外送 HTTP 要求的輸入的欄位。</span><span class="sxs-lookup"><span data-stu-id="72810-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="72810-137">標示 * 代表必要欄位。</span><span class="sxs-lookup"><span data-stu-id="72810-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="72810-138">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="72810-138">Display name</span></span> | <span data-ttu-id="72810-139">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="72810-139">Property name</span></span> | <span data-ttu-id="72810-140">說明</span><span class="sxs-lookup"><span data-stu-id="72810-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72810-141">從*</span><span class="sxs-lookup"><span data-stu-id="72810-141">From*</span></span> |<span data-ttu-id="72810-142">from</span><span class="sxs-lookup"><span data-stu-id="72810-142">from</span></span> |<span data-ttu-id="72810-143">hello 陣列 toofilter</span><span class="sxs-lookup"><span data-stu-id="72810-143">hello array toofilter</span></span> |
| <span data-ttu-id="72810-144">條件*</span><span class="sxs-lookup"><span data-stu-id="72810-144">Condition*</span></span> |<span data-ttu-id="72810-145">其中</span><span class="sxs-lookup"><span data-stu-id="72810-145">where</span></span> |<span data-ttu-id="72810-146">hello 條件 tooevaluate 每個項目</span><span class="sxs-lookup"><span data-stu-id="72810-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="72810-147">輸出詳細資料</span><span class="sxs-lookup"><span data-stu-id="72810-147">Output details</span></span>
<span data-ttu-id="72810-148">hello 以下是輸出 hello HTTP 回應的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="72810-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="72810-149">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="72810-149">Property name</span></span> | <span data-ttu-id="72810-150">資料類型</span><span class="sxs-lookup"><span data-stu-id="72810-150">Data type</span></span> | <span data-ttu-id="72810-151">說明</span><span class="sxs-lookup"><span data-stu-id="72810-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72810-152">篩選的陣列</span><span class="sxs-lookup"><span data-stu-id="72810-152">Filtered array</span></span> |<span data-ttu-id="72810-153">array</span><span class="sxs-lookup"><span data-stu-id="72810-153">array</span></span> |<span data-ttu-id="72810-154">陣列，其中包含每筆篩選結果的物件</span><span class="sxs-lookup"><span data-stu-id="72810-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="72810-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72810-155">Next steps</span></span>
<span data-ttu-id="72810-156">現在，試用 hello 平台和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="72810-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="72810-157">您可以瀏覽 hello 邏輯應用程式中其他可用的連接器，藉由查看我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="72810-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

