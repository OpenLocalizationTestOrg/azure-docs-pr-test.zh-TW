---
title: "OMS 中的 IT 服務管理連接器 | Microsoft Docs"
description: "使用 IT 服務管理連接器，在 OMS 中將 ITSM 工作項目集中監視及管理，並快速解決所有問題。"
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="af017-103">使用 IT 服務管理連接器 (預覽) 將 ITSM 工作項目集中管理</span><span class="sxs-lookup"><span data-stu-id="af017-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![IT 服務管理連接器符號](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="af017-105">您可以使用 OMS Log Analytics 中的 IT 服務管理連接器 (ITSMC)，將 ITSM 產品/服務之間的工作項目集中監視及管理。</span><span class="sxs-lookup"><span data-stu-id="af017-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="af017-106">IT 服務管理連接器會將您現有的 IT 服務管理 (ITSM) 產品和服務與 OMS Log Analytics 進行整合。</span><span class="sxs-lookup"><span data-stu-id="af017-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="af017-107">解決方案與 ITSM 產品/服務具有雙向整合，在其中讓 OMS 使用者可選擇在 ITSM 解決方案中建立事件、警示或活動。</span><span class="sxs-lookup"><span data-stu-id="af017-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="af017-108">連接器也會從 ITSM 解決方案將諸如事件和變更要求等資料匯入 OMS Log AnalyticsOMS。</span><span class="sxs-lookup"><span data-stu-id="af017-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="af017-109">利用 IT 服務管理連接器，您可以：</span><span class="sxs-lookup"><span data-stu-id="af017-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="af017-110">將您組織內使用的 ITSM 產品/服務之工作項目集中監視及管理。</span><span class="sxs-lookup"><span data-stu-id="af017-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="af017-111">從 OMS 警示及透過記錄搜尋，在 ITSM 中建立 ITSM 工作項目 (例如警示、事件、活動)。</span><span class="sxs-lookup"><span data-stu-id="af017-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="af017-112">讀取 ITSM 解決方案的事件和變更要求，並與 Log Analytics 工作區中的相關記錄資料相互關聯。</span><span class="sxs-lookup"><span data-stu-id="af017-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="af017-113">在使用者呼叫及將問題回報給支援人員之前，就找出任何非預期且不尋常的事件並加以解決。</span><span class="sxs-lookup"><span data-stu-id="af017-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="af017-114">將工作項目資料匯入 Log Analytics，並建立關鍵效能指標 (KPI) 報告。</span><span class="sxs-lookup"><span data-stu-id="af017-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="af017-115">您可以使用這些報告來識別、評估和處理數個重要的項目，例如惡意程式碼評估。</span><span class="sxs-lookup"><span data-stu-id="af017-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="af017-116">請檢視策劃儀表板，以獲得關於事件、變更要求及受影響系統的更深入見解。</span><span class="sxs-lookup"><span data-stu-id="af017-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="af017-117">與 Log Analytics 工作區中的其他管理解決方案建立相互關聯來加速疑難排解。</span><span class="sxs-lookup"><span data-stu-id="af017-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="af017-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="af017-118">Prerequisites</span></span>

<span data-ttu-id="af017-119">若要將 ITSM 工作項目匯入 OMS Log Analytics，解決方案會要求 OMS 中的 IT 服務管理連接器與您從中匯入工作項目的 ITSM 產品/服務之間的連線。</span><span class="sxs-lookup"><span data-stu-id="af017-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="af017-120">組態</span><span class="sxs-lookup"><span data-stu-id="af017-120">Configuration</span></span>

<span data-ttu-id="af017-121">使用[從方案庫新增 Log Analytics 解決方案](log-analytics-add-solutions.md)中所述的程序，將 IT 服務管理連接器新增至您的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="af017-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="af017-122">如您在方案庫中所見的 [IT 服務管理連接器] 圖格︰</span><span class="sxs-lookup"><span data-stu-id="af017-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![連接器圖格](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="af017-124">新增成功之後，您會在 [OMS] > [設定] > [連接的來源] 下看到 IT 服務管理連接器。</span><span class="sxs-lookup"><span data-stu-id="af017-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC 已連線](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="af017-126">根據預設，IT 服務管理連接器每 24 小時會重新整理一次連線的資料。</span><span class="sxs-lookup"><span data-stu-id="af017-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="af017-127">若要針對所做的任何編輯或範本更新立即重新整理連線的資料，按一下連線旁顯示的重新整理按鈕。</span><span class="sxs-lookup"><span data-stu-id="af017-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![ITSMC 重新整理](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="af017-129">管理組件</span><span class="sxs-lookup"><span data-stu-id="af017-129">Management packs</span></span>
<span data-ttu-id="af017-130">此解決方案不需要任何管理組件。</span><span class="sxs-lookup"><span data-stu-id="af017-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="af017-131">連接的來源</span><span class="sxs-lookup"><span data-stu-id="af017-131">Connected sources</span></span>

<span data-ttu-id="af017-132">IT 服務管理連接器支援下列 ITSM 產品/服務︰</span><span class="sxs-lookup"><span data-stu-id="af017-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- [<span data-ttu-id="af017-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="af017-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="af017-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="af017-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="af017-135">Provance</span><span class="sxs-lookup"><span data-stu-id="af017-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="af017-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="af017-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="af017-137">使用解決方案</span><span class="sxs-lookup"><span data-stu-id="af017-137">Using the solution</span></span>

<span data-ttu-id="af017-138">一旦將 OMS IT 服務管理連接器與 ITSM 服務連線，Log Analytics 服務就會開始從連線的 ITSM 產品/服務收集資料。</span><span class="sxs-lookup"><span data-stu-id="af017-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="af017-139">IT 服務管理連接器解決方案所匯入的資料會出現在 Log Analytics 中，作為名為 **ServiceDesk_CL** 的事件。</span><span class="sxs-lookup"><span data-stu-id="af017-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="af017-140">事件會包含一個名為 **ServiceDeskWorkItemType_s** 的欄位。</span><span class="sxs-lookup"><span data-stu-id="af017-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="af017-141">根據 **ServiceDesk_CL** 事件中所包含的工作項目資料，可採用其值作為事件或變更要求。</span><span class="sxs-lookup"><span data-stu-id="af017-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="af017-142">輸入資料</span><span class="sxs-lookup"><span data-stu-id="af017-142">Input data</span></span>
<span data-ttu-id="af017-143">從 ITSM 產品/服務匯入的工作項目。</span><span class="sxs-lookup"><span data-stu-id="af017-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="af017-144">下列資訊說明 IT 服務管理連接器所收集之資料的範例︰</span><span class="sxs-lookup"><span data-stu-id="af017-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="af017-145">根據匯入 Log Analytics 的工作項目類型，**ServiceDesk_CL** 會包含下列欄位︰</span><span class="sxs-lookup"><span data-stu-id="af017-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="af017-146">**工作項目︰****事件**</span><span class="sxs-lookup"><span data-stu-id="af017-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="af017-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="af017-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="af017-148">**欄位**</span><span class="sxs-lookup"><span data-stu-id="af017-148">**Fields**</span></span>

- <span data-ttu-id="af017-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="af017-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="af017-150">服務台識別碼</span><span class="sxs-lookup"><span data-stu-id="af017-150">Service Desk ID</span></span>
- <span data-ttu-id="af017-151">State</span><span class="sxs-lookup"><span data-stu-id="af017-151">State</span></span>
- <span data-ttu-id="af017-152">急迫性</span><span class="sxs-lookup"><span data-stu-id="af017-152">Urgency</span></span>
- <span data-ttu-id="af017-153">影響</span><span class="sxs-lookup"><span data-stu-id="af017-153">Impact</span></span>
- <span data-ttu-id="af017-154">優先順序</span><span class="sxs-lookup"><span data-stu-id="af017-154">Priority</span></span>
- <span data-ttu-id="af017-155">升級</span><span class="sxs-lookup"><span data-stu-id="af017-155">Escalation</span></span>
- <span data-ttu-id="af017-156">建立者</span><span class="sxs-lookup"><span data-stu-id="af017-156">Created By</span></span>
- <span data-ttu-id="af017-157">解決者</span><span class="sxs-lookup"><span data-stu-id="af017-157">Resolved By</span></span>
- <span data-ttu-id="af017-158">關閉者</span><span class="sxs-lookup"><span data-stu-id="af017-158">Closed By</span></span>
- <span data-ttu-id="af017-159">來源</span><span class="sxs-lookup"><span data-stu-id="af017-159">Source</span></span>
- <span data-ttu-id="af017-160">指派對象</span><span class="sxs-lookup"><span data-stu-id="af017-160">Assigned To</span></span>
- <span data-ttu-id="af017-161">類別</span><span class="sxs-lookup"><span data-stu-id="af017-161">Category</span></span>
- <span data-ttu-id="af017-162">課程名稱</span><span class="sxs-lookup"><span data-stu-id="af017-162">Title</span></span>
- <span data-ttu-id="af017-163">說明</span><span class="sxs-lookup"><span data-stu-id="af017-163">Description</span></span>
- <span data-ttu-id="af017-164">建立日期</span><span class="sxs-lookup"><span data-stu-id="af017-164">Created Date</span></span>
- <span data-ttu-id="af017-165">關閉日期</span><span class="sxs-lookup"><span data-stu-id="af017-165">Closed Date</span></span>
- <span data-ttu-id="af017-166">解決日期</span><span class="sxs-lookup"><span data-stu-id="af017-166">Resolved Date</span></span>
- <span data-ttu-id="af017-167">上次修改日期</span><span class="sxs-lookup"><span data-stu-id="af017-167">Last Modified Date</span></span>
- <span data-ttu-id="af017-168">電腦</span><span class="sxs-lookup"><span data-stu-id="af017-168">Computer</span></span>


<span data-ttu-id="af017-169">**工作項目︰****變更要求**</span><span class="sxs-lookup"><span data-stu-id="af017-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="af017-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="af017-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="af017-171">**欄位**</span><span class="sxs-lookup"><span data-stu-id="af017-171">**Fields**</span></span>
- <span data-ttu-id="af017-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="af017-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="af017-173">服務台識別碼</span><span class="sxs-lookup"><span data-stu-id="af017-173">Service Desk ID</span></span>
- <span data-ttu-id="af017-174">建立者</span><span class="sxs-lookup"><span data-stu-id="af017-174">Created By</span></span>
- <span data-ttu-id="af017-175">關閉者</span><span class="sxs-lookup"><span data-stu-id="af017-175">Closed By</span></span>
- <span data-ttu-id="af017-176">來源</span><span class="sxs-lookup"><span data-stu-id="af017-176">Source</span></span>
- <span data-ttu-id="af017-177">指派對象</span><span class="sxs-lookup"><span data-stu-id="af017-177">Assigned To</span></span>
- <span data-ttu-id="af017-178">Title</span><span class="sxs-lookup"><span data-stu-id="af017-178">Title</span></span>
- <span data-ttu-id="af017-179">類型</span><span class="sxs-lookup"><span data-stu-id="af017-179">Type</span></span>
- <span data-ttu-id="af017-180">類別</span><span class="sxs-lookup"><span data-stu-id="af017-180">Category</span></span>
- <span data-ttu-id="af017-181">State</span><span class="sxs-lookup"><span data-stu-id="af017-181">State</span></span>
- <span data-ttu-id="af017-182">升級</span><span class="sxs-lookup"><span data-stu-id="af017-182">Escalation</span></span>
- <span data-ttu-id="af017-183">衝突狀態</span><span class="sxs-lookup"><span data-stu-id="af017-183">Conflict Status</span></span>
- <span data-ttu-id="af017-184">急迫性</span><span class="sxs-lookup"><span data-stu-id="af017-184">Urgency</span></span>
- <span data-ttu-id="af017-185">優先順序</span><span class="sxs-lookup"><span data-stu-id="af017-185">Priority</span></span>
- <span data-ttu-id="af017-186">風險</span><span class="sxs-lookup"><span data-stu-id="af017-186">Risk</span></span>
- <span data-ttu-id="af017-187">影響</span><span class="sxs-lookup"><span data-stu-id="af017-187">Impact</span></span>
- <span data-ttu-id="af017-188">指派對象</span><span class="sxs-lookup"><span data-stu-id="af017-188">Assigned To</span></span>
- <span data-ttu-id="af017-189">建立日期</span><span class="sxs-lookup"><span data-stu-id="af017-189">Created Date</span></span>
- <span data-ttu-id="af017-190">關閉日期</span><span class="sxs-lookup"><span data-stu-id="af017-190">Closed Date</span></span>
- <span data-ttu-id="af017-191">上次修改日期</span><span class="sxs-lookup"><span data-stu-id="af017-191">Last Modified Date</span></span>
- <span data-ttu-id="af017-192">要求日期</span><span class="sxs-lookup"><span data-stu-id="af017-192">Requested Date</span></span>
- <span data-ttu-id="af017-193">計劃開始日期</span><span class="sxs-lookup"><span data-stu-id="af017-193">Planned Start Date</span></span>
- <span data-ttu-id="af017-194">計劃結束日期</span><span class="sxs-lookup"><span data-stu-id="af017-194">Planned End Date</span></span>
- <span data-ttu-id="af017-195">工作開始日期</span><span class="sxs-lookup"><span data-stu-id="af017-195">Work Start Date</span></span>
- <span data-ttu-id="af017-196">工作結束日期</span><span class="sxs-lookup"><span data-stu-id="af017-196">Work End Date</span></span>
- <span data-ttu-id="af017-197">說明</span><span class="sxs-lookup"><span data-stu-id="af017-197">Description</span></span>
- <span data-ttu-id="af017-198">電腦</span><span class="sxs-lookup"><span data-stu-id="af017-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="af017-199">ServiceNow 事件的輸出資料</span><span class="sxs-lookup"><span data-stu-id="af017-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="af017-200">OMS 欄位</span><span class="sxs-lookup"><span data-stu-id="af017-200">OMS field</span></span> | <span data-ttu-id="af017-201">ITSM 欄位</span><span class="sxs-lookup"><span data-stu-id="af017-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="af017-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="af017-202">ServiceDeskId_s</span></span>| <span data-ttu-id="af017-203">數字</span><span class="sxs-lookup"><span data-stu-id="af017-203">Number</span></span> |
| <span data-ttu-id="af017-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="af017-204">IncidentState_s</span></span> | <span data-ttu-id="af017-205">State</span><span class="sxs-lookup"><span data-stu-id="af017-205">State</span></span> |
| <span data-ttu-id="af017-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="af017-206">Urgency_s</span></span> |<span data-ttu-id="af017-207">急迫性</span><span class="sxs-lookup"><span data-stu-id="af017-207">Urgency</span></span> |
| <span data-ttu-id="af017-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="af017-208">Impact_s</span></span> |<span data-ttu-id="af017-209">影響</span><span class="sxs-lookup"><span data-stu-id="af017-209">Impact</span></span>|
| <span data-ttu-id="af017-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="af017-210">Priority_s</span></span> | <span data-ttu-id="af017-211">優先順序</span><span class="sxs-lookup"><span data-stu-id="af017-211">Priority</span></span> |
| <span data-ttu-id="af017-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="af017-212">CreatedBy_s</span></span> | <span data-ttu-id="af017-213">開啟者</span><span class="sxs-lookup"><span data-stu-id="af017-213">Opened by</span></span> |
| <span data-ttu-id="af017-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="af017-214">ResolvedBy_s</span></span> | <span data-ttu-id="af017-215">解決者</span><span class="sxs-lookup"><span data-stu-id="af017-215">Resolved by</span></span>|
| <span data-ttu-id="af017-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="af017-216">ClosedBy_s</span></span>  | <span data-ttu-id="af017-217">關閉者</span><span class="sxs-lookup"><span data-stu-id="af017-217">Closed by</span></span> |
| <span data-ttu-id="af017-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="af017-218">Source_s</span></span>| <span data-ttu-id="af017-219">連絡人型別</span><span class="sxs-lookup"><span data-stu-id="af017-219">Contact type</span></span> |
| <span data-ttu-id="af017-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="af017-220">AssignedTo_s</span></span> | <span data-ttu-id="af017-221">指派對象</span><span class="sxs-lookup"><span data-stu-id="af017-221">Assigned to</span></span>  |
| <span data-ttu-id="af017-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="af017-222">Category_s</span></span> | <span data-ttu-id="af017-223">類別</span><span class="sxs-lookup"><span data-stu-id="af017-223">Category</span></span> |
| <span data-ttu-id="af017-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="af017-224">Title_s</span></span>|  <span data-ttu-id="af017-225">簡短說明</span><span class="sxs-lookup"><span data-stu-id="af017-225">Short description</span></span> |
| <span data-ttu-id="af017-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="af017-226">Description_s</span></span>|  <span data-ttu-id="af017-227">注意事項</span><span class="sxs-lookup"><span data-stu-id="af017-227">Notes</span></span> |
| <span data-ttu-id="af017-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-228">CreatedDate_t</span></span>|  <span data-ttu-id="af017-229">已開啟</span><span class="sxs-lookup"><span data-stu-id="af017-229">Opened</span></span> |
| <span data-ttu-id="af017-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-230">ClosedDate_t</span></span>| <span data-ttu-id="af017-231">關閉</span><span class="sxs-lookup"><span data-stu-id="af017-231">closed</span></span>|
| <span data-ttu-id="af017-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-232">ResolvedDate_t</span></span>|<span data-ttu-id="af017-233">已解決</span><span class="sxs-lookup"><span data-stu-id="af017-233">Resolved</span></span>|
| <span data-ttu-id="af017-234">電腦</span><span class="sxs-lookup"><span data-stu-id="af017-234">Computer</span></span>  | <span data-ttu-id="af017-235">設定項目</span><span class="sxs-lookup"><span data-stu-id="af017-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="af017-236">ServiceNow 變更要求的輸出資料</span><span class="sxs-lookup"><span data-stu-id="af017-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="af017-237">OMS 欄位</span><span class="sxs-lookup"><span data-stu-id="af017-237">OMS field</span></span> | <span data-ttu-id="af017-238">ITSM 欄位</span><span class="sxs-lookup"><span data-stu-id="af017-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="af017-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="af017-239">ServiceDeskId_s</span></span>| <span data-ttu-id="af017-240">數字</span><span class="sxs-lookup"><span data-stu-id="af017-240">Number</span></span> |
| <span data-ttu-id="af017-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="af017-241">CreatedBy_s</span></span> | <span data-ttu-id="af017-242">要求者</span><span class="sxs-lookup"><span data-stu-id="af017-242">Requested by</span></span> |
| <span data-ttu-id="af017-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="af017-243">ClosedBy_s</span></span> | <span data-ttu-id="af017-244">關閉者</span><span class="sxs-lookup"><span data-stu-id="af017-244">Closed by</span></span> |
| <span data-ttu-id="af017-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="af017-245">AssignedTo_s</span></span> | <span data-ttu-id="af017-246">指派對象</span><span class="sxs-lookup"><span data-stu-id="af017-246">Assigned to</span></span>  |
| <span data-ttu-id="af017-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="af017-247">Title_s</span></span>|  <span data-ttu-id="af017-248">簡短說明</span><span class="sxs-lookup"><span data-stu-id="af017-248">Short description</span></span> |
| <span data-ttu-id="af017-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="af017-249">Type_s</span></span>|  <span data-ttu-id="af017-250">類型</span><span class="sxs-lookup"><span data-stu-id="af017-250">Type</span></span> |
| <span data-ttu-id="af017-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="af017-251">Category_s</span></span>|  <span data-ttu-id="af017-252">類別</span><span class="sxs-lookup"><span data-stu-id="af017-252">Catgory</span></span> |
| <span data-ttu-id="af017-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="af017-253">CRState_s</span></span>|  <span data-ttu-id="af017-254">State</span><span class="sxs-lookup"><span data-stu-id="af017-254">State</span></span>|
| <span data-ttu-id="af017-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="af017-255">Urgency_s</span></span>|  <span data-ttu-id="af017-256">急迫性</span><span class="sxs-lookup"><span data-stu-id="af017-256">Urgency</span></span> |
| <span data-ttu-id="af017-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="af017-257">Priority_s</span></span>| <span data-ttu-id="af017-258">優先順序</span><span class="sxs-lookup"><span data-stu-id="af017-258">Priority</span></span>|
| <span data-ttu-id="af017-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="af017-259">Risk_s</span></span>| <span data-ttu-id="af017-260">風險</span><span class="sxs-lookup"><span data-stu-id="af017-260">Risk</span></span>|
| <span data-ttu-id="af017-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="af017-261">Impact_s</span></span>| <span data-ttu-id="af017-262">影響</span><span class="sxs-lookup"><span data-stu-id="af017-262">Impact</span></span>|
| <span data-ttu-id="af017-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-263">RequestedDate_t</span></span>  | <span data-ttu-id="af017-264">要求的日期</span><span class="sxs-lookup"><span data-stu-id="af017-264">Requested by date</span></span> |
| <span data-ttu-id="af017-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-265">ClosedDate_t</span></span> | <span data-ttu-id="af017-266">關閉日期</span><span class="sxs-lookup"><span data-stu-id="af017-266">Closed date</span></span> |
| <span data-ttu-id="af017-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="af017-268">計劃開始日期</span><span class="sxs-lookup"><span data-stu-id="af017-268">Planned start date</span></span> |
| <span data-ttu-id="af017-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="af017-270">計劃結束日期</span><span class="sxs-lookup"><span data-stu-id="af017-270">Planned end date</span></span> |
| <span data-ttu-id="af017-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-271">WorkStartDate_t</span></span>  | <span data-ttu-id="af017-272">實際開始日期</span><span class="sxs-lookup"><span data-stu-id="af017-272">Actual start date</span></span> |
| <span data-ttu-id="af017-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="af017-273">WorkEndDate_t</span></span> | <span data-ttu-id="af017-274">實際結束日期</span><span class="sxs-lookup"><span data-stu-id="af017-274">Actual end date</span></span>|
| <span data-ttu-id="af017-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="af017-275">Description_s</span></span> | <span data-ttu-id="af017-276">說明</span><span class="sxs-lookup"><span data-stu-id="af017-276">Description</span></span> |
| <span data-ttu-id="af017-277">電腦</span><span class="sxs-lookup"><span data-stu-id="af017-277">Computer</span></span>  | <span data-ttu-id="af017-278">設定項目</span><span class="sxs-lookup"><span data-stu-id="af017-278">Configuration Item</span></span> |

<span data-ttu-id="af017-279">**ITSM 資料的範例 Log Analytics 畫面︰**</span><span class="sxs-lookup"><span data-stu-id="af017-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Log Analytics 畫面](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="af017-281">IT 服務管理連接器 – 與其他 OMS 解決方案整合</span><span class="sxs-lookup"><span data-stu-id="af017-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="af017-282">IT 服務管理連接器，目前支援與服務對應解決方案整合。</span><span class="sxs-lookup"><span data-stu-id="af017-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="af017-283">服務對應可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="af017-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="af017-284">如果您想到您的伺服器，ADM 可讓您以互連系統 (提供重要服務) 的形式檢視它們。</span><span class="sxs-lookup"><span data-stu-id="af017-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="af017-285">不需要進行任何設定，只要安裝了代理程式，服務對應就會顯示橫跨任何 TCP 連接架構的伺服器、處理程序和連接埠之間的連接。</span><span class="sxs-lookup"><span data-stu-id="af017-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="af017-286">詳細資訊︰[服務對應](../operations-management-suite/operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="af017-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="af017-287">透過這項整合，您可以檢視 ITSM 解決方案中建立的服務台項目，如下列範例中所示︰</span><span class="sxs-lookup"><span data-stu-id="af017-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="af017-288">整合式解決方案</span><span class="sxs-lookup"><span data-stu-id="af017-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="af017-289">建立 OMS 警示的 ITSM 工作項目</span><span class="sxs-lookup"><span data-stu-id="af017-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="af017-290">針對 OMS 警示，您可以在連線的 ITSM 來源中建立相關聯的工作項目。</span><span class="sxs-lookup"><span data-stu-id="af017-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="af017-291">若要這樣做，請使用下列程序：</span><span class="sxs-lookup"><span data-stu-id="af017-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="af017-292">從 [記錄搜尋] 視窗中，執行記錄搜尋查詢來檢視資料。</span><span class="sxs-lookup"><span data-stu-id="af017-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="af017-293">查詢結果為工作項目的來源。</span><span class="sxs-lookup"><span data-stu-id="af017-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="af017-294">在 [記錄搜尋] 中，按一下 [警示] 可開啟 [新增警示規則] 頁面。</span><span class="sxs-lookup"><span data-stu-id="af017-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Log Analytics 畫面](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="af017-296">在 **[新增警示規則]** 視窗中，提供 **[名稱]** 、 **[嚴重性]** 、 **[搜尋查詢]** 和 **[警示準則]** \(時間範圍/計量的度量單位) 的必要詳細資料。</span><span class="sxs-lookup"><span data-stu-id="af017-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="af017-297">在 [ITSM 動作] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="af017-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="af017-298">從 [選取連線] 清單中選取您的 ITSM 連線。</span><span class="sxs-lookup"><span data-stu-id="af017-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="af017-299">提供所需的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="af017-299">Provide the details as required.</span></span>
7. <span data-ttu-id="af017-300">若要為這項警示的每個記錄項目建立個別的工作項目，請選取 [為每個記錄項目建立個別的工作項目] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="af017-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="af017-301">或</span><span class="sxs-lookup"><span data-stu-id="af017-301">Or</span></span>

    <span data-ttu-id="af017-302">將此核取方塊取消選取，可在此警示下對任意數目的記錄項目只建立一個工作項目。</span><span class="sxs-lookup"><span data-stu-id="af017-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="af017-303">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="af017-303">Click **Save**.</span></span>

<span data-ttu-id="af017-304">將會在 [警示] 下建立 OMS 警示。</span><span class="sxs-lookup"><span data-stu-id="af017-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="af017-305">符合所指定警示的條件時，會建立對應 ITSM 連線的工作項目。</span><span class="sxs-lookup"><span data-stu-id="af017-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="af017-306">從 OMS 記錄建立 ITSM 工作項目</span><span class="sxs-lookup"><span data-stu-id="af017-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="af017-307">您可以使用 OMS 記錄搜尋，在連線的 ITSM 來源中建立工作項目。</span><span class="sxs-lookup"><span data-stu-id="af017-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="af017-308">若要這樣做，請使用下列程序：</span><span class="sxs-lookup"><span data-stu-id="af017-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="af017-309">從 [記錄搜尋] 中，搜尋必要的資料、選取詳細資料，然後按一下 [建立工作項目]。</span><span class="sxs-lookup"><span data-stu-id="af017-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="af017-310">[建立 ITSM 工作項目] 視窗隨即出現︰</span><span class="sxs-lookup"><span data-stu-id="af017-310">The **Create ITSM Work item** window appears:</span></span>

    ![Log Analytics 畫面](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="af017-312">新增下列詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="af017-312">Add the following details:</span></span>

  - <span data-ttu-id="af017-313">**工作項目標題**︰工作項目的標題。</span><span class="sxs-lookup"><span data-stu-id="af017-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="af017-314">**工作項目描述**︰新工作項目的描述。</span><span class="sxs-lookup"><span data-stu-id="af017-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="af017-315">**受影響電腦**︰找到此記錄資料的電腦之名稱。</span><span class="sxs-lookup"><span data-stu-id="af017-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="af017-316">**選取連線**：您要在其中建立此工作項目的 ITSM 連線。</span><span class="sxs-lookup"><span data-stu-id="af017-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="af017-317">**工作項目**︰工作項目的類型。</span><span class="sxs-lookup"><span data-stu-id="af017-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="af017-318">若要使用事件的現有工作項目範本，請在 [根據範本產生工作項目] 選項下按一下 [是]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="af017-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="af017-319">或者，</span><span class="sxs-lookup"><span data-stu-id="af017-319">Or,</span></span>

    <span data-ttu-id="af017-320">如果您想要提供自訂的值，請按一下 [否]。</span><span class="sxs-lookup"><span data-stu-id="af017-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="af017-321">在 [連絡人類型]、[影響]、[急迫性]、[類別] 和 [子類別] 文字方塊中提供適當的值，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="af017-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="af017-322">會在 ITSM 中建立工作項目，您也可以在 OMS 中加以檢視。</span><span class="sxs-lookup"><span data-stu-id="af017-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="af017-323">針對 OMS 中的 ITSM 連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="af017-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="af017-324">如果從已連線的來源 UI 連線失敗，且收到**儲存連線時發生錯誤**訊息，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="af017-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="af017-325">在 ServiceNow、Cherwell 和 Provance 連線的情況下，請確定您已正確輸入每個連線的使用者名稱/密碼與用戶端識別碼/用戶端祕密。</span><span class="sxs-lookup"><span data-stu-id="af017-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="af017-326">如果錯誤持續發生，請檢查您在對應的 ITSM 產品中是否擁有足夠權限來進行連線。</span><span class="sxs-lookup"><span data-stu-id="af017-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="af017-327">若問題發生在 Service Manager 中，請確定已成功部署 Web 應用程式，且已建立混合式連線。</span><span class="sxs-lookup"><span data-stu-id="af017-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="af017-328">若要確認是否已成功與內部部署 Service Manager 機器建立連線，請瀏覽 Web 應用程式 URL，如文件中針對建立[混合式連線](log-analytics-itsmc-connections.md#configure-the-hybrid-connection)所述。</span><span class="sxs-lookup"><span data-stu-id="af017-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="af017-329">如果 ServiceNow 的資料在 OMS 中未進行同步，請確定 ServiceNow 執行個體並非處在睡眠中。</span><span class="sxs-lookup"><span data-stu-id="af017-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="af017-330">這有時可能會發生在 ServiceNow 開發人員執行個體閒置時。</span><span class="sxs-lookup"><span data-stu-id="af017-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="af017-331">否則，請回報問題。</span><span class="sxs-lookup"><span data-stu-id="af017-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="af017-332">如果警示正從 OMS 引發，但工作項目在 ITSM 產品中並未進行建立，或設定項目並未進行建立/連結至工作項目，或需任何一般資訊，請執行下列：</span><span class="sxs-lookup"><span data-stu-id="af017-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="af017-333">OMS 入口網站中的 IT 服務管理連接器解決方案可用於取得連線/工作項目/電腦等的摘要。按一下 [狀態] 刀鋒視窗中的錯誤訊息，瀏覽至 [記錄搜尋]，並使用錯誤訊息中的詳細資料來檢視發生錯誤的連線。</span><span class="sxs-lookup"><span data-stu-id="af017-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="af017-334">您可以使用 [Type=ServiceDeskLog_CL] 直接檢視 [記錄搜尋] 頁面中的錯誤/相關資訊。</span><span class="sxs-lookup"><span data-stu-id="af017-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="af017-335">針對 Service Manager Web 應用程式部署進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="af017-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="af017-336">如果是有關 Web 應用程式部署的任何問題，請確定您在所述的訂用帳戶中擁有足夠權限來建立/部署資源。</span><span class="sxs-lookup"><span data-stu-id="af017-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="af017-337">如果在執行[指令碼](log-analytics-itsmc-service-manager-script.md)時，出現**物件參考未設定為物件的執行個體**錯誤訊息，請確定您在**使用者設定**一節中是否輸入有效值。</span><span class="sxs-lookup"><span data-stu-id="af017-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="af017-338">如果您無法建立服務匯流排轉送命名空間，請確定所需的資源提供者已在訂用帳戶中註冊。</span><span class="sxs-lookup"><span data-stu-id="af017-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="af017-339">如果未註冊，以手動方式從 Azure 入口網站建立。</span><span class="sxs-lookup"><span data-stu-id="af017-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="af017-340">您也可以在建立它時，同時從 Azure 入口網站[建立混合式連線](log-analytics-itsmc-connections.md#configure-the-hybrid-connection)。</span><span class="sxs-lookup"><span data-stu-id="af017-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="af017-341">與我們連絡</span><span class="sxs-lookup"><span data-stu-id="af017-341">Contact us</span></span>

<span data-ttu-id="af017-342">如需關於 IT 服務管理連接器的任何查詢或意見反應，請與我們連絡：[omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="af017-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af017-343">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af017-343">Next steps</span></span>
<span data-ttu-id="af017-344">[將 ITSM 產品/服務新增至 IT 服務管理連接器](log-analytics-itsmc-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="af017-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
