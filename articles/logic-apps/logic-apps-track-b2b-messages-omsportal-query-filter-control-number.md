---
title: "在 Operations Management Suite 中查詢 B2B 訊息 - Azure Logic Apps  | Microsoft Docs"
description: "建立查詢以在 Operations Management Suite 中追蹤 AS2、X12 和 EDIFACT 訊息"
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
ms.openlocfilehash: 2748d3d3daf7c13dca05f663a4a088598e1b3605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-the-microsoft-operations-management-suite-oms"></a><span data-ttu-id="00cc6-103">在 Microsoft Operations Management Suite (OMS) 中查詢 AS2、X12 和 EDIFACT 訊息</span><span class="sxs-lookup"><span data-stu-id="00cc6-103">Query for AS2, X12, and EDIFACT messages in the Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="00cc6-104">若要尋找您在 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) 中使用 [Azure Log Analytics](../log-analytics/log-analytics-overview.md) 追蹤的 AS2、X12 或 EDIFACT 訊息，則可以建立查詢，以根據特定準則來篩選動作。</span><span class="sxs-lookup"><span data-stu-id="00cc6-104">To find the AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="00cc6-105">例如，您可以找到根據特定交換控制編號的訊息。</span><span class="sxs-lookup"><span data-stu-id="00cc6-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="00cc6-106">需求</span><span class="sxs-lookup"><span data-stu-id="00cc6-106">Requirements</span></span>

* <span data-ttu-id="00cc6-107">已設定診斷記錄的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="00cc6-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="00cc6-108">了解[如何建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)和[如何設定該邏輯應用程式的記錄](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="00cc6-108">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="00cc6-109">已設定監視和記錄的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="00cc6-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="00cc6-110">了解[如何建立整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)和[如何設定該帳戶的監視和記錄](../logic-apps/logic-apps-monitor-b2b-message.md)。</span><span class="sxs-lookup"><span data-stu-id="00cc6-110">Learn [how to create an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how to set up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="00cc6-111">如果您還沒有這麼做，請[在 OMS 中將診斷資料發佈至 Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)，並[在 OMS 中設定訊息追蹤](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="00cc6-111">If you haven't already, [publish diagnostic data to Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="00cc6-112">在您符合先前的需求之後，[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) 中應該有工作區。</span><span class="sxs-lookup"><span data-stu-id="00cc6-112">After you've met the previous requirements, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="00cc6-113">您應該在 OMS 中使用相同的 OMS 工作區來追蹤 B2B 通訊。</span><span class="sxs-lookup"><span data-stu-id="00cc6-113">You should use the same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="00cc6-114">如果您沒有 OMS 工作區，請了解[如何建立 OMS 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="00cc6-114">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-the-operations-management-suite-portal"></a><span data-ttu-id="00cc6-115">在 Operations Management Suite 入口網站中建立具有篩選的訊息查詢</span><span class="sxs-lookup"><span data-stu-id="00cc6-115">Create message queries with filters in the Operations Management Suite portal</span></span>

<span data-ttu-id="00cc6-116">此範例示範如何找到根據其交換控制編號的訊息。</span><span class="sxs-lookup"><span data-stu-id="00cc6-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="00cc6-117">如果您知道 OMS 工作區名稱，請移至工作區首頁 (`https://{your-workspace-name}.portal.mms.microsoft.com`)，然後在步驟 4 啟動。</span><span class="sxs-lookup"><span data-stu-id="00cc6-117">If you know your OMS workspace name, go to your workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="00cc6-118">否則，請從步驟 1 開始。</span><span class="sxs-lookup"><span data-stu-id="00cc6-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="00cc6-119">在 [Azure 入口網站](https://portal.azure.com)中，選擇 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-119">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="00cc6-120">搜尋 "log analytics"，然後選擇 [Log Analytics]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="00cc6-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![尋找 Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="00cc6-122">在 [Log Analytics] 下，尋找並選取 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="00cc6-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![選取 OMS 工作區](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="00cc6-124">在 [管理] 下，選擇 [OMS 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![選擇 OMS 入口網站](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="00cc6-126">在 OMS 首頁上，選擇 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-126">On your OMS home page, choose **Log Search**.</span></span>

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="00cc6-128">-或-</span><span class="sxs-lookup"><span data-stu-id="00cc6-128">-or-</span></span>

   ![在 OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="00cc6-130">在搜尋方塊中，輸入您想要尋找的欄位，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="00cc6-130">In the search box, enter a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="00cc6-131">當您開始鍵入時，OMS 會顯示您可以使用的可能相符項目和作業。</span><span class="sxs-lookup"><span data-stu-id="00cc6-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="00cc6-132">深入了解[如何在 Log Analytics 中尋找資料](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="00cc6-132">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="00cc6-133">此範例會搜尋具有 **Type=AzureDiagnostics** 的事件。</span><span class="sxs-lookup"><span data-stu-id="00cc6-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![開始鍵入查詢字串](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="00cc6-135">在左列中，選擇您想要檢視的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="00cc6-135">In the left bar, choose the timeframe that you want to view.</span></span> <span data-ttu-id="00cc6-136">若要將篩選新增至查詢，請選擇 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-136">To add a filter to your query, choose **+Add**.</span></span>

   ![將篩選新增至查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="00cc6-138">在 [新增篩選] 下，輸入篩選名稱，以找到您想要的篩選。</span><span class="sxs-lookup"><span data-stu-id="00cc6-138">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="00cc6-139">選取篩選，然後選擇 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-139">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="00cc6-140">為了尋找交換控制編號，此範例會搜尋 "interchange" 這個字，並選取 **event_record_messageProperties_interchangeControlNumber_s** 作為篩選。</span><span class="sxs-lookup"><span data-stu-id="00cc6-140">To find the interchange control number, this example searches for the word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as the filter.</span></span>

   ![選取篩選](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="00cc6-142">在左列中，選取您想要使用的篩選值，然後選擇 [套用]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-142">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   <span data-ttu-id="00cc6-143">此範例會選取我們想要之訊息的交換控制編號。</span><span class="sxs-lookup"><span data-stu-id="00cc6-143">This example selects the interchange control number for the messages we want.</span></span>

   ![選取篩選值](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="00cc6-145">現在，回到您要建置的查詢。</span><span class="sxs-lookup"><span data-stu-id="00cc6-145">Now return to the query that you're building.</span></span> <span data-ttu-id="00cc6-146">已使用您所選取的篩選事件和值來更新您的查詢。</span><span class="sxs-lookup"><span data-stu-id="00cc6-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="00cc6-147">現在也會篩選您的先前結果。</span><span class="sxs-lookup"><span data-stu-id="00cc6-147">Your previous results are now filtered too.</span></span>

    ![回到具有已篩選結果的查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="00cc6-149">儲存查詢供日後使用</span><span class="sxs-lookup"><span data-stu-id="00cc6-149">Save your query for future use</span></span>

1. <span data-ttu-id="00cc6-150">從 [記錄搜尋] 頁面上的查詢，選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-150">From your query on the **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="00cc6-151">提供查詢名稱，並選取分類，然後選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![提供查詢名稱和分類](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="00cc6-153">若要檢視您的查詢，請選擇 [我的最愛]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-153">To view your query, choose **Favorites**.</span></span>

   ![選擇 [我的最愛]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="00cc6-155">在 [儲存的搜尋] 下，選取您的查詢，以檢視結果。</span><span class="sxs-lookup"><span data-stu-id="00cc6-155">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="00cc6-156">若要更新查詢，以找到不同的結果，請編輯查詢。</span><span class="sxs-lookup"><span data-stu-id="00cc6-156">To update the query so you can find different results, edit the query.</span></span>

   ![選取查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-the-operations-management-suite-portal"></a><span data-ttu-id="00cc6-158">在 Operations Management Suite 入口網站中尋找並執行預存查詢</span><span class="sxs-lookup"><span data-stu-id="00cc6-158">Find and run saved queries in the Operations Management Suite portal</span></span>

1. <span data-ttu-id="00cc6-159">開啟 OMS 工作區首頁 (`https://{your-workspace-name}.portal.mms.microsoft.com`)，然後選擇 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![在 OMS 首頁上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="00cc6-161">-或-</span><span class="sxs-lookup"><span data-stu-id="00cc6-161">-or-</span></span>

   ![在 OMS 功能表上，選擇 [記錄搜尋]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="00cc6-163">在 [記錄搜尋] 首頁上，選擇 [我的最愛]。</span><span class="sxs-lookup"><span data-stu-id="00cc6-163">On the **Log Search** home page, choose **Favorites**.</span></span>

   ![選擇 [我的最愛]](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="00cc6-165">在 [儲存的搜尋] 下，選取您的查詢，以檢視結果。</span><span class="sxs-lookup"><span data-stu-id="00cc6-165">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="00cc6-166">若要更新查詢，以找到不同的結果，請編輯查詢。</span><span class="sxs-lookup"><span data-stu-id="00cc6-166">To update the query so you can find different results, edit the query.</span></span>

   ![選取查詢](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="00cc6-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00cc6-168">Next steps</span></span>

* [<span data-ttu-id="00cc6-169">AS2 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="00cc6-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="00cc6-170">X12 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="00cc6-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="00cc6-171">自訂追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="00cc6-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)