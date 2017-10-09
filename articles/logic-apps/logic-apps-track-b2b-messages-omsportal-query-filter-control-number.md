---
title: "Operations Management Suite Azure 邏輯應用程式中的 B2B 訊息的 aaaQuery |Microsoft 文件"
description: "在 hello Operations Management Suite 中建立查詢 tootrack AS2，x12 和 EDIFACT 訊息"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="a1439-103">As2，x12 和 EDIFACT 訊息 hello Microsoft Operations Management Suite (OMS) 中的查詢</span><span class="sxs-lookup"><span data-stu-id="a1439-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="a1439-104">x12，或您追蹤的 EDIFACT 訊息 toofind hello AS2 [Azure Log Analytics](../log-analytics/log-analytics-overview.md)在 hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)，您可以建立篩選器動作，根據特定的查詢準則。</span><span class="sxs-lookup"><span data-stu-id="a1439-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="a1439-105">例如，您可以找到根據特定交換控制編號的訊息。</span><span class="sxs-lookup"><span data-stu-id="a1439-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="a1439-106">需求</span><span class="sxs-lookup"><span data-stu-id="a1439-106">Requirements</span></span>

* <span data-ttu-id="a1439-107">已設定診斷記錄的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1439-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="a1439-108">深入了解[如何 toocreate 邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)和[如何該邏輯應用程式的記錄 tooset](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="a1439-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="a1439-109">已設定監視和記錄的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1439-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="a1439-110">深入了解[如何 toocreate 整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)和[如何監視和記錄該帳戶的總 tooset](../logic-apps/logic-apps-monitor-b2b-message.md)。</span><span class="sxs-lookup"><span data-stu-id="a1439-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="a1439-111">如果您還沒有這麼做，[發行分析的診斷資料 tooLog](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)和[設定郵件追蹤在 OMS 中](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="a1439-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a1439-112">您雖然符合 hello 先前的需求之後，您應該有 hello 中的工作區[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a1439-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="a1439-113">您應該使用 hello 追蹤您在 OMS 中的 B2B 通訊的同一個 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="a1439-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="a1439-114">如果您沒有 OMS 工作區，了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a1439-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="a1439-115">使用 hello Operations Management Suite 入口網站中的篩選器建立訊息查詢</span><span class="sxs-lookup"><span data-stu-id="a1439-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="a1439-116">此範例示範如何找到根據其交換控制編號的訊息。</span><span class="sxs-lookup"><span data-stu-id="a1439-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="a1439-117">如果您知道您的 OMS 工作區名稱，請移至 tooyour 工作區的首頁 (`https://{your-workspace-name}.portal.mms.microsoft.com`)，然後啟動在步驟 4。</span><span class="sxs-lookup"><span data-stu-id="a1439-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="a1439-118">否則，請從步驟 1 開始。</span><span class="sxs-lookup"><span data-stu-id="a1439-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="a1439-119">在 hello [Azure 入口網站](https://portal.azure.com)，選擇**更服務**。</span><span class="sxs-lookup"><span data-stu-id="a1439-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="a1439-120">搜尋 "log analytics"，然後選擇 [Log Analytics]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a1439-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![尋找 Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="a1439-122">在 [Log Analytics] 下，尋找並選取 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="a1439-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![選取 OMS 工作區](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="a1439-124">在 [管理] 下，選擇 [OMS 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="a1439-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![選擇 OMS 入口網站](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="a1439-126">在 OMS 首頁上，選擇 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="a1439-126">On your OMS home page, choose **Log Search**.</span></span>

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="a1439-128">-或-</span><span class="sxs-lookup"><span data-stu-id="a1439-128">-or-</span></span>

   ![Hello OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="a1439-130">在 hello 搜尋方塊中，輸入您想 toofind，欄位按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a1439-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="a1439-131">當您開始鍵入時，OMS 會顯示您可以使用的可能相符項目和作業。</span><span class="sxs-lookup"><span data-stu-id="a1439-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="a1439-132">深入了解[如何 toofind 記錄分析資料](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="a1439-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="a1439-133">此範例會搜尋具有 **Type=AzureDiagnostics** 的事件。</span><span class="sxs-lookup"><span data-stu-id="a1439-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![開始鍵入查詢字串](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="a1439-135">在 hello 左列上，選擇 hello 時間範圍內的 tooview。</span><span class="sxs-lookup"><span data-stu-id="a1439-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="a1439-136">tooadd 篩選 tooyour 查詢中，選擇**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="a1439-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![新增篩選器 tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="a1439-138">下**加入篩選**，因此您可以找到您想要的 hello 篩選輸入 hello 篩選器名稱。</span><span class="sxs-lookup"><span data-stu-id="a1439-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="a1439-139">選取 hello 篩選，然後選擇  **+ 加**。</span><span class="sxs-lookup"><span data-stu-id="a1439-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="a1439-140">toofind hello 交換控制編號，此範例中搜尋 hello word"交換 」，並選取**event_record_messageProperties_interchangeControlNumber_s**為 hello 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="a1439-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![選取篩選](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="a1439-142">在 hello 左列中，選取 hello 篩選值，您想 toouse，並選擇**套用**。</span><span class="sxs-lookup"><span data-stu-id="a1439-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="a1439-143">這個範例會選取 hello 我們想要的 hello 訊息的交換控制編號。</span><span class="sxs-lookup"><span data-stu-id="a1439-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![選取篩選值](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="a1439-145">現在會傳回 toohello 您要建置的查詢。</span><span class="sxs-lookup"><span data-stu-id="a1439-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="a1439-146">已使用您所選取的篩選事件和值來更新您的查詢。</span><span class="sxs-lookup"><span data-stu-id="a1439-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="a1439-147">現在也會篩選您的先前結果。</span><span class="sxs-lookup"><span data-stu-id="a1439-147">Your previous results are now filtered too.</span></span>

    ![傳回篩選的結果與 tooyour 查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="a1439-149">儲存查詢供日後使用</span><span class="sxs-lookup"><span data-stu-id="a1439-149">Save your query for future use</span></span>

1. <span data-ttu-id="a1439-150">從您的查詢上 hello**記錄搜尋**頁面上，選擇**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a1439-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="a1439-151">提供查詢名稱，並選取分類，然後選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="a1439-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![提供查詢名稱和分類](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="a1439-153">tooview 查詢，並選擇**我的最愛**。</span><span class="sxs-lookup"><span data-stu-id="a1439-153">tooview your query, choose **Favorites**.</span></span>

   ![選擇 [我的最愛]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="a1439-155">在下**已儲存的搜尋**，選取您的查詢，好讓您可以檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="a1439-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="a1439-156">因此，您可以找到不同的結果，tooupdate hello 查詢編輯 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="a1439-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![選取查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="a1439-158">尋找並執行已儲存的查詢在 hello Operations Management Suite 入口網站</span><span class="sxs-lookup"><span data-stu-id="a1439-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="a1439-159">開啟 OMS 工作區首頁 (`https://{your-workspace-name}.portal.mms.microsoft.com`)，然後選擇 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="a1439-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="a1439-161">-或-</span><span class="sxs-lookup"><span data-stu-id="a1439-161">-or-</span></span>

   ![Hello OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="a1439-163">在 hello**記錄搜尋**首頁上，選擇 **我的最愛**。</span><span class="sxs-lookup"><span data-stu-id="a1439-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   ![選擇 [我的最愛]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="a1439-165">在下**已儲存的搜尋**，選取您的查詢，好讓您可以檢視 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="a1439-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="a1439-166">因此，您可以找到不同的結果，tooupdate hello 查詢編輯 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="a1439-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![選取查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="a1439-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1439-168">Next steps</span></span>

* [<span data-ttu-id="a1439-169">AS2 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="a1439-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="a1439-170">X12 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="a1439-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="a1439-171">自訂追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="a1439-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)