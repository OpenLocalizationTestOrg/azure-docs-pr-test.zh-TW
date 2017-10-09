---
title: "在 OMS 中的服務管理連接器 aaaIT |Microsoft 文件"
description: "使用 hello IT 服務管理連接器 toocentrally 監視和管理 hello ITSM 工作項目，在 OMS 中，以及快速解決任何問題。"
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
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="b7f0c-103">使用 IT 服務管理連接器 (預覽) 將 ITSM 工作項目集中管理</span><span class="sxs-lookup"><span data-stu-id="b7f0c-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![IT 服務管理連接器符號](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="b7f0c-105">您可以使用 OMS 記錄分析 toocentrally 監視器中的 hello IT 服務管理連接器 (ITSMC)，並管理工作項目到 ITSM 的產品/服務。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="b7f0c-106">hello IT 服務管理連接器與 OMS 記錄分析整合，您的現有 IT 服務管理 (ITSM) 產品和服務。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="b7f0c-107">hello 方案中有與 ITSM 產品/服務的雙向整合，它會提供在 hello OMS 使用者選項 toocreate 事件、 警示或 ITSM 方案中的事件。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="b7f0c-108">hello 連接器也會匯入資料，例如事件、 以及 ITSM 方案變更要求，到 OMS 記錄分析。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="b7f0c-109">利用 IT 服務管理連接器，您可以：</span><span class="sxs-lookup"><span data-stu-id="b7f0c-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="b7f0c-110">將您組織內使用的 ITSM 產品/服務之工作項目集中監視及管理。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="b7f0c-111">從 OMS 警示及透過記錄搜尋，在 ITSM 中建立 ITSM 工作項目 (例如警示、事件、活動)。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="b7f0c-112">讀取 ITSM 解決方案的事件和變更要求，並與 Log Analytics 工作區中的相關記錄資料相互關聯。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="b7f0c-113">尋找任何非預期且不尋常的事件並解決問題，甚至之前 hello 使用者呼叫，並回報 toohello 技術服務人員。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="b7f0c-114">將工作項目資料匯入 Log Analytics，並建立關鍵效能指標 (KPI) 報告。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="b7f0c-115">您可以使用這些報告來識別、評估和處理數個重要的項目，例如惡意程式碼評估。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="b7f0c-116">請檢視策劃儀表板，以獲得關於事件、變更要求及受影響系統的更深入見解。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="b7f0c-117">疑難排解更快建立相互關聯與 hello 記錄分析工作區中其他管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b7f0c-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="b7f0c-118">Prerequisites</span></span>

<span data-ttu-id="b7f0c-119">tooimport hello ITSM 工作項目到 OMS 記錄分析，hello 解決方案需要 hello OMS 中的 hello IT 服務管理連接器與 hello IT SM 產品/服務從中匯入 hello 工作項目之間的連線。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="b7f0c-120">組態</span><span class="sxs-lookup"><span data-stu-id="b7f0c-120">Configuration</span></span>

<span data-ttu-id="b7f0c-121">新增 hello IT 服務管理連接器方案 tooyour OMS 工作空間中，使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="b7f0c-122">IT 服務管理連接器磚 hello 解決方案資源庫中所示：</span><span class="sxs-lookup"><span data-stu-id="b7f0c-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![連接器圖格](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="b7f0c-124">之後成功時，您會看到 hello IT 服務管理連接器**OMS** > **設定** > **連接的來源。**</span><span class="sxs-lookup"><span data-stu-id="b7f0c-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC 已連線](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="b7f0c-126">根據預設，hello IT 服務管理連接器重新整理一次中每隔 24 小時 hello 連接的資料。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="b7f0c-127">toorefresh 連接的資料立即的任何編輯或範本更新您所做的按一下 hello 重新整理按鈕顯示 下一步 tooyour 連線。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![ITSMC 重新整理](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="b7f0c-129">管理組件</span><span class="sxs-lookup"><span data-stu-id="b7f0c-129">Management packs</span></span>
<span data-ttu-id="b7f0c-130">此解決方案不需要任何管理組件。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="b7f0c-131">連接的來源</span><span class="sxs-lookup"><span data-stu-id="b7f0c-131">Connected sources</span></span>

<span data-ttu-id="b7f0c-132">hello 下列 ITSM 產品/服務支援 IT 服務管理連接器 hello:</span><span class="sxs-lookup"><span data-stu-id="b7f0c-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="b7f0c-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="b7f0c-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="b7f0c-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="b7f0c-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="b7f0c-135">Provance</span><span class="sxs-lookup"><span data-stu-id="b7f0c-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="b7f0c-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="b7f0c-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="b7f0c-137">使用 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="b7f0c-137">Using hello solution</span></span>

<span data-ttu-id="b7f0c-138">一旦 ITSM 服務連線 hello OMS IT 服務管理連接器，hello 記錄分析服務會開始收集 hello 連接 ITSM 產品/服務的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="b7f0c-139">IT 服務管理連接器解決方案所匯入的資料會出現在 Log Analytics 中，作為名為 **ServiceDesk_CL** 的事件。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="b7f0c-140">事件會包含一個名為 **ServiceDeskWorkItemType_s** 的欄位。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="b7f0c-141">這可以接受做為事件，其值或變更要求、 hello 根據工作項目資料包含在 hello **ServiceDesk_CL**事件。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="b7f0c-142">輸入資料</span><span class="sxs-lookup"><span data-stu-id="b7f0c-142">Input data</span></span>
<span data-ttu-id="b7f0c-143">工作項目從 hello ITSM 產品/服務匯入。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="b7f0c-144">hello 下列資訊顯示 hello IT 服務管理連接器所收集資料的範例：</span><span class="sxs-lookup"><span data-stu-id="b7f0c-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="b7f0c-145">Hello 根據工作項目類型匯入到記錄分析**ServiceDesk_CL**包含下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7f0c-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="b7f0c-146">**工作項目︰****事件**</span><span class="sxs-lookup"><span data-stu-id="b7f0c-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="b7f0c-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="b7f0c-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="b7f0c-148">**欄位**</span><span class="sxs-lookup"><span data-stu-id="b7f0c-148">**Fields**</span></span>

- <span data-ttu-id="b7f0c-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="b7f0c-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="b7f0c-150">服務台識別碼</span><span class="sxs-lookup"><span data-stu-id="b7f0c-150">Service Desk ID</span></span>
- <span data-ttu-id="b7f0c-151">State</span><span class="sxs-lookup"><span data-stu-id="b7f0c-151">State</span></span>
- <span data-ttu-id="b7f0c-152">急迫性</span><span class="sxs-lookup"><span data-stu-id="b7f0c-152">Urgency</span></span>
- <span data-ttu-id="b7f0c-153">影響</span><span class="sxs-lookup"><span data-stu-id="b7f0c-153">Impact</span></span>
- <span data-ttu-id="b7f0c-154">優先順序</span><span class="sxs-lookup"><span data-stu-id="b7f0c-154">Priority</span></span>
- <span data-ttu-id="b7f0c-155">升級</span><span class="sxs-lookup"><span data-stu-id="b7f0c-155">Escalation</span></span>
- <span data-ttu-id="b7f0c-156">建立者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-156">Created By</span></span>
- <span data-ttu-id="b7f0c-157">解決者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-157">Resolved By</span></span>
- <span data-ttu-id="b7f0c-158">關閉者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-158">Closed By</span></span>
- <span data-ttu-id="b7f0c-159">來源</span><span class="sxs-lookup"><span data-stu-id="b7f0c-159">Source</span></span>
- <span data-ttu-id="b7f0c-160">指派對象</span><span class="sxs-lookup"><span data-stu-id="b7f0c-160">Assigned To</span></span>
- <span data-ttu-id="b7f0c-161">類別</span><span class="sxs-lookup"><span data-stu-id="b7f0c-161">Category</span></span>
- <span data-ttu-id="b7f0c-162">課程名稱</span><span class="sxs-lookup"><span data-stu-id="b7f0c-162">Title</span></span>
- <span data-ttu-id="b7f0c-163">說明</span><span class="sxs-lookup"><span data-stu-id="b7f0c-163">Description</span></span>
- <span data-ttu-id="b7f0c-164">建立日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-164">Created Date</span></span>
- <span data-ttu-id="b7f0c-165">關閉日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-165">Closed Date</span></span>
- <span data-ttu-id="b7f0c-166">解決日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-166">Resolved Date</span></span>
- <span data-ttu-id="b7f0c-167">上次修改日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-167">Last Modified Date</span></span>
- <span data-ttu-id="b7f0c-168">電腦</span><span class="sxs-lookup"><span data-stu-id="b7f0c-168">Computer</span></span>


<span data-ttu-id="b7f0c-169">**工作項目︰****變更要求**</span><span class="sxs-lookup"><span data-stu-id="b7f0c-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="b7f0c-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="b7f0c-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="b7f0c-171">**欄位**</span><span class="sxs-lookup"><span data-stu-id="b7f0c-171">**Fields**</span></span>
- <span data-ttu-id="b7f0c-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="b7f0c-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="b7f0c-173">服務台識別碼</span><span class="sxs-lookup"><span data-stu-id="b7f0c-173">Service Desk ID</span></span>
- <span data-ttu-id="b7f0c-174">建立者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-174">Created By</span></span>
- <span data-ttu-id="b7f0c-175">關閉者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-175">Closed By</span></span>
- <span data-ttu-id="b7f0c-176">來源</span><span class="sxs-lookup"><span data-stu-id="b7f0c-176">Source</span></span>
- <span data-ttu-id="b7f0c-177">指派對象</span><span class="sxs-lookup"><span data-stu-id="b7f0c-177">Assigned To</span></span>
- <span data-ttu-id="b7f0c-178">Title</span><span class="sxs-lookup"><span data-stu-id="b7f0c-178">Title</span></span>
- <span data-ttu-id="b7f0c-179">類型</span><span class="sxs-lookup"><span data-stu-id="b7f0c-179">Type</span></span>
- <span data-ttu-id="b7f0c-180">類別</span><span class="sxs-lookup"><span data-stu-id="b7f0c-180">Category</span></span>
- <span data-ttu-id="b7f0c-181">State</span><span class="sxs-lookup"><span data-stu-id="b7f0c-181">State</span></span>
- <span data-ttu-id="b7f0c-182">升級</span><span class="sxs-lookup"><span data-stu-id="b7f0c-182">Escalation</span></span>
- <span data-ttu-id="b7f0c-183">衝突狀態</span><span class="sxs-lookup"><span data-stu-id="b7f0c-183">Conflict Status</span></span>
- <span data-ttu-id="b7f0c-184">急迫性</span><span class="sxs-lookup"><span data-stu-id="b7f0c-184">Urgency</span></span>
- <span data-ttu-id="b7f0c-185">優先順序</span><span class="sxs-lookup"><span data-stu-id="b7f0c-185">Priority</span></span>
- <span data-ttu-id="b7f0c-186">風險</span><span class="sxs-lookup"><span data-stu-id="b7f0c-186">Risk</span></span>
- <span data-ttu-id="b7f0c-187">影響</span><span class="sxs-lookup"><span data-stu-id="b7f0c-187">Impact</span></span>
- <span data-ttu-id="b7f0c-188">指派對象</span><span class="sxs-lookup"><span data-stu-id="b7f0c-188">Assigned To</span></span>
- <span data-ttu-id="b7f0c-189">建立日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-189">Created Date</span></span>
- <span data-ttu-id="b7f0c-190">關閉日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-190">Closed Date</span></span>
- <span data-ttu-id="b7f0c-191">上次修改日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-191">Last Modified Date</span></span>
- <span data-ttu-id="b7f0c-192">要求日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-192">Requested Date</span></span>
- <span data-ttu-id="b7f0c-193">計劃開始日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-193">Planned Start Date</span></span>
- <span data-ttu-id="b7f0c-194">計劃結束日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-194">Planned End Date</span></span>
- <span data-ttu-id="b7f0c-195">工作開始日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-195">Work Start Date</span></span>
- <span data-ttu-id="b7f0c-196">工作結束日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-196">Work End Date</span></span>
- <span data-ttu-id="b7f0c-197">說明</span><span class="sxs-lookup"><span data-stu-id="b7f0c-197">Description</span></span>
- <span data-ttu-id="b7f0c-198">電腦</span><span class="sxs-lookup"><span data-stu-id="b7f0c-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="b7f0c-199">ServiceNow 事件的輸出資料</span><span class="sxs-lookup"><span data-stu-id="b7f0c-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="b7f0c-200">OMS 欄位</span><span class="sxs-lookup"><span data-stu-id="b7f0c-200">OMS field</span></span> | <span data-ttu-id="b7f0c-201">ITSM 欄位</span><span class="sxs-lookup"><span data-stu-id="b7f0c-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="b7f0c-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-202">ServiceDeskId_s</span></span>| <span data-ttu-id="b7f0c-203">數字</span><span class="sxs-lookup"><span data-stu-id="b7f0c-203">Number</span></span> |
| <span data-ttu-id="b7f0c-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-204">IncidentState_s</span></span> | <span data-ttu-id="b7f0c-205">State</span><span class="sxs-lookup"><span data-stu-id="b7f0c-205">State</span></span> |
| <span data-ttu-id="b7f0c-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-206">Urgency_s</span></span> |<span data-ttu-id="b7f0c-207">急迫性</span><span class="sxs-lookup"><span data-stu-id="b7f0c-207">Urgency</span></span> |
| <span data-ttu-id="b7f0c-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-208">Impact_s</span></span> |<span data-ttu-id="b7f0c-209">影響</span><span class="sxs-lookup"><span data-stu-id="b7f0c-209">Impact</span></span>|
| <span data-ttu-id="b7f0c-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-210">Priority_s</span></span> | <span data-ttu-id="b7f0c-211">優先順序</span><span class="sxs-lookup"><span data-stu-id="b7f0c-211">Priority</span></span> |
| <span data-ttu-id="b7f0c-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-212">CreatedBy_s</span></span> | <span data-ttu-id="b7f0c-213">開啟者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-213">Opened by</span></span> |
| <span data-ttu-id="b7f0c-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-214">ResolvedBy_s</span></span> | <span data-ttu-id="b7f0c-215">解決者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-215">Resolved by</span></span>|
| <span data-ttu-id="b7f0c-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-216">ClosedBy_s</span></span>  | <span data-ttu-id="b7f0c-217">關閉者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-217">Closed by</span></span> |
| <span data-ttu-id="b7f0c-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-218">Source_s</span></span>| <span data-ttu-id="b7f0c-219">連絡人型別</span><span class="sxs-lookup"><span data-stu-id="b7f0c-219">Contact type</span></span> |
| <span data-ttu-id="b7f0c-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-220">AssignedTo_s</span></span> | <span data-ttu-id="b7f0c-221">指派太</span><span class="sxs-lookup"><span data-stu-id="b7f0c-221">Assigned too</span></span> |
| <span data-ttu-id="b7f0c-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-222">Category_s</span></span> | <span data-ttu-id="b7f0c-223">類別</span><span class="sxs-lookup"><span data-stu-id="b7f0c-223">Category</span></span> |
| <span data-ttu-id="b7f0c-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-224">Title_s</span></span>|  <span data-ttu-id="b7f0c-225">簡短說明</span><span class="sxs-lookup"><span data-stu-id="b7f0c-225">Short description</span></span> |
| <span data-ttu-id="b7f0c-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-226">Description_s</span></span>|  <span data-ttu-id="b7f0c-227">注意事項</span><span class="sxs-lookup"><span data-stu-id="b7f0c-227">Notes</span></span> |
| <span data-ttu-id="b7f0c-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-228">CreatedDate_t</span></span>|  <span data-ttu-id="b7f0c-229">已開啟</span><span class="sxs-lookup"><span data-stu-id="b7f0c-229">Opened</span></span> |
| <span data-ttu-id="b7f0c-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-230">ClosedDate_t</span></span>| <span data-ttu-id="b7f0c-231">關閉</span><span class="sxs-lookup"><span data-stu-id="b7f0c-231">closed</span></span>|
| <span data-ttu-id="b7f0c-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-232">ResolvedDate_t</span></span>|<span data-ttu-id="b7f0c-233">已解決</span><span class="sxs-lookup"><span data-stu-id="b7f0c-233">Resolved</span></span>|
| <span data-ttu-id="b7f0c-234">電腦</span><span class="sxs-lookup"><span data-stu-id="b7f0c-234">Computer</span></span>  | <span data-ttu-id="b7f0c-235">設定項目</span><span class="sxs-lookup"><span data-stu-id="b7f0c-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="b7f0c-236">ServiceNow 變更要求的輸出資料</span><span class="sxs-lookup"><span data-stu-id="b7f0c-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="b7f0c-237">OMS 欄位</span><span class="sxs-lookup"><span data-stu-id="b7f0c-237">OMS field</span></span> | <span data-ttu-id="b7f0c-238">ITSM 欄位</span><span class="sxs-lookup"><span data-stu-id="b7f0c-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="b7f0c-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-239">ServiceDeskId_s</span></span>| <span data-ttu-id="b7f0c-240">數字</span><span class="sxs-lookup"><span data-stu-id="b7f0c-240">Number</span></span> |
| <span data-ttu-id="b7f0c-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-241">CreatedBy_s</span></span> | <span data-ttu-id="b7f0c-242">要求者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-242">Requested by</span></span> |
| <span data-ttu-id="b7f0c-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-243">ClosedBy_s</span></span> | <span data-ttu-id="b7f0c-244">關閉者</span><span class="sxs-lookup"><span data-stu-id="b7f0c-244">Closed by</span></span> |
| <span data-ttu-id="b7f0c-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-245">AssignedTo_s</span></span> | <span data-ttu-id="b7f0c-246">指派太</span><span class="sxs-lookup"><span data-stu-id="b7f0c-246">Assigned too</span></span> |
| <span data-ttu-id="b7f0c-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-247">Title_s</span></span>|  <span data-ttu-id="b7f0c-248">簡短說明</span><span class="sxs-lookup"><span data-stu-id="b7f0c-248">Short description</span></span> |
| <span data-ttu-id="b7f0c-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-249">Type_s</span></span>|  <span data-ttu-id="b7f0c-250">類型</span><span class="sxs-lookup"><span data-stu-id="b7f0c-250">Type</span></span> |
| <span data-ttu-id="b7f0c-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-251">Category_s</span></span>|  <span data-ttu-id="b7f0c-252">類別</span><span class="sxs-lookup"><span data-stu-id="b7f0c-252">Catgory</span></span> |
| <span data-ttu-id="b7f0c-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-253">CRState_s</span></span>|  <span data-ttu-id="b7f0c-254">State</span><span class="sxs-lookup"><span data-stu-id="b7f0c-254">State</span></span>|
| <span data-ttu-id="b7f0c-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-255">Urgency_s</span></span>|  <span data-ttu-id="b7f0c-256">急迫性</span><span class="sxs-lookup"><span data-stu-id="b7f0c-256">Urgency</span></span> |
| <span data-ttu-id="b7f0c-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-257">Priority_s</span></span>| <span data-ttu-id="b7f0c-258">優先順序</span><span class="sxs-lookup"><span data-stu-id="b7f0c-258">Priority</span></span>|
| <span data-ttu-id="b7f0c-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-259">Risk_s</span></span>| <span data-ttu-id="b7f0c-260">風險</span><span class="sxs-lookup"><span data-stu-id="b7f0c-260">Risk</span></span>|
| <span data-ttu-id="b7f0c-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-261">Impact_s</span></span>| <span data-ttu-id="b7f0c-262">影響</span><span class="sxs-lookup"><span data-stu-id="b7f0c-262">Impact</span></span>|
| <span data-ttu-id="b7f0c-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-263">RequestedDate_t</span></span>  | <span data-ttu-id="b7f0c-264">要求的日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-264">Requested by date</span></span> |
| <span data-ttu-id="b7f0c-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-265">ClosedDate_t</span></span> | <span data-ttu-id="b7f0c-266">關閉日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-266">Closed date</span></span> |
| <span data-ttu-id="b7f0c-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="b7f0c-268">計劃開始日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-268">Planned start date</span></span> |
| <span data-ttu-id="b7f0c-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="b7f0c-270">計劃結束日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-270">Planned end date</span></span> |
| <span data-ttu-id="b7f0c-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-271">WorkStartDate_t</span></span>  | <span data-ttu-id="b7f0c-272">實際開始日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-272">Actual start date</span></span> |
| <span data-ttu-id="b7f0c-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="b7f0c-273">WorkEndDate_t</span></span> | <span data-ttu-id="b7f0c-274">實際結束日期</span><span class="sxs-lookup"><span data-stu-id="b7f0c-274">Actual end date</span></span>|
| <span data-ttu-id="b7f0c-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="b7f0c-275">Description_s</span></span> | <span data-ttu-id="b7f0c-276">說明</span><span class="sxs-lookup"><span data-stu-id="b7f0c-276">Description</span></span> |
| <span data-ttu-id="b7f0c-277">電腦</span><span class="sxs-lookup"><span data-stu-id="b7f0c-277">Computer</span></span>  | <span data-ttu-id="b7f0c-278">設定項目</span><span class="sxs-lookup"><span data-stu-id="b7f0c-278">Configuration Item</span></span> |

<span data-ttu-id="b7f0c-279">**ITSM 資料的範例 Log Analytics 畫面︰**</span><span class="sxs-lookup"><span data-stu-id="b7f0c-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Log Analytics 畫面](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="b7f0c-281">IT 服務管理連接器 – 與其他 OMS 解決方案整合</span><span class="sxs-lookup"><span data-stu-id="b7f0c-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="b7f0c-282">IT 服務管理連接器，目前支援與 hello 服務對應解決方案整合。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="b7f0c-283">服務對應會自動探索 hello Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="b7f0c-284">它可讓您 tooview 您的伺服器，當您將它們 – 互連提供重要服務的系統。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="b7f0c-285">不需要進行任何設定，只要安裝了代理程式，服務對應就會顯示橫跨任何 TCP 連接架構的伺服器、處理程序和連接埠之間的連接。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="b7f0c-286">詳細資訊︰[服務對應](../operations-management-suite/operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="b7f0c-287">使用這項整合，您可以檢視 hello 下列範例所示，在 hello ITSM 方案中建立的 hello 服務支援項目：</span><span class="sxs-lookup"><span data-stu-id="b7f0c-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="b7f0c-288">整合式解決方案</span><span class="sxs-lookup"><span data-stu-id="b7f0c-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="b7f0c-289">建立 OMS 警示的 ITSM 工作項目</span><span class="sxs-lookup"><span data-stu-id="b7f0c-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="b7f0c-290">Hello OMS 警示，您可以在 hello 連接 ITSM 來源中建立相關聯的工作項目。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="b7f0c-291">toodo 程序後，使用 hello:</span><span class="sxs-lookup"><span data-stu-id="b7f0c-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="b7f0c-292">從**記錄搜尋**視窗中，執行記錄搜尋查詢 tooview 資料。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="b7f0c-293">查詢結果會 hello 來源工作項目。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="b7f0c-294">在**記錄搜尋**，按一下 **警示**tooopen hello**加入警示規則**頁面。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Log Analytics 畫面](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="b7f0c-296">在 hello**加入警示規則**視窗中，提供所需的 hello 詳細資料，如**名稱**，**嚴重性**，**搜尋查詢**，和**警示準則**（時間視窗度量的度量單位）。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="b7f0c-297">在 [ITSM 動作] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="b7f0c-298">選取您 ITSM 連線從 hello**選取連接**清單。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="b7f0c-299">提供所需的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="b7f0c-300">此警示，請選取 hello 的每個記錄項目不同的工作項目 toocreate**建立個別的工作項目，每個記錄項目**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="b7f0c-301">或</span><span class="sxs-lookup"><span data-stu-id="b7f0c-301">Or</span></span>

    <span data-ttu-id="b7f0c-302">將保留任意數目的記錄項目，這項警示之下此核取方塊未選取的 toocreate 只有一個工作項目。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="b7f0c-303">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-303">Click **Save**.</span></span>

<span data-ttu-id="b7f0c-304">底下建立 hello OMS 警示**警示**。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="b7f0c-305">hello 對應 ITSM 連線網路的工時 hello 指定的警示的條件符合時，會建立項目。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="b7f0c-306">從 OMS 記錄建立 ITSM 工作項目</span><span class="sxs-lookup"><span data-stu-id="b7f0c-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="b7f0c-307">您可以使用 OMS 記錄搜尋，連接的 hello ITSM 來源中建立工作項目。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="b7f0c-308">toodo 程序後，使用 hello:</span><span class="sxs-lookup"><span data-stu-id="b7f0c-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="b7f0c-309">從**記錄搜尋**，搜尋所需的 hello 資料、 選取 hello 詳細資料，然後按一下**建立工作項目**。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="b7f0c-310">hello**建立 ITSM 工作項目** 視窗隨即出現：</span><span class="sxs-lookup"><span data-stu-id="b7f0c-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Log Analytics 畫面](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="b7f0c-312">新增下列詳細資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7f0c-312">Add hello following details:</span></span>

  - <span data-ttu-id="b7f0c-313">**工作項目標題**: hello 工作項目的標題。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="b7f0c-314">**工作項目描述**: hello 新工作項目的描述。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="b7f0c-315">**受影響電腦**: hello 找此記錄資料的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="b7f0c-316">**選取連接**: ITSM 連接您想在其中 toocreate 這個工作項目。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="b7f0c-317">**工作項目**︰工作項目的類型。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="b7f0c-318">按一下 toouse 事件時，現有工作項目範本**是**下**hello 範本為基礎的產生工作項目**選項，然後再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="b7f0c-319">或者，</span><span class="sxs-lookup"><span data-stu-id="b7f0c-319">Or,</span></span>

    <span data-ttu-id="b7f0c-320">按一下**否**您希望 tooprovide 您自訂的值。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="b7f0c-321">提供 hello 適當的值在 hello**連絡人類型**，**影響**，**急迫性**，**類別**，和**子類別目錄**文字方塊中，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="b7f0c-322">hello 工作項目將會建立在 hello ITSM，您也可以在 OMS 中檢視。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="b7f0c-323">針對 OMS 中的 ITSM 連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b7f0c-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="b7f0c-324">如果從已連接的來源 UI 的連線失敗，且您 hello**儲存連接時發生錯誤**訊息，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="b7f0c-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="b7f0c-325">發生 ServiceNow、 Cherwell 和 Provance 連接，確保您正確輸入的 hello 使用者名稱/密碼與用戶端識別碼/用戶端密碼 hello 連線的每個。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="b7f0c-326">如果 hello 錯誤持續發生，請檢查是否有足夠的權限在 hello 對應 ITSM 產品 toomake hello 的連接。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="b7f0c-327">發生 Service Manager，請確認 hello Web 應用程式部署成功建立混合式連接。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="b7f0c-328">tooverify hello 連接已成功建立與 hello 內部的 Service Manager 電腦，請瀏覽 hello 文件以 hello 中所述的 hello Web 應用程式 URL[混合式連接](log-analytics-itsmc-connections.md#configure-the-hybrid-connection)。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="b7f0c-329">如果資料 servicenow 未取得 OMS 中同步處理，請確定該 hello ServiceNow 執行個體非睡眠中。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="b7f0c-330">可能造成此結果一段時間中 hello ServiceNow 開發人員執行個體閒置時。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="b7f0c-331">否則，報表 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="b7f0c-332">如果會取得從 OMS 來引發警示，但沒有取得 ITSM 產品在建立工作項目或設定項目不會進行建立/連結 toowork 項目或任何泛型資訊，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="b7f0c-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="b7f0c-333">在 OMS 入口網站中的 IT 服務管理連接器解決方案可能是使用的 tooget 連接/工作項目/電腦等的摘要。按一下 hello hello 狀態刀鋒視窗中的錯誤訊息，瀏覽過**記錄搜尋**並檢視 hello 連接具有 hello 錯誤 hello 錯誤訊息中使用 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="b7f0c-334">您可以直接檢視 hello 中的 hello/錯誤相關資訊**記錄搜尋**網頁的*類型 = ServiceDeskLog_CL*。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="b7f0c-335">針對 Service Manager Web 應用程式部署進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b7f0c-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="b7f0c-336">如果使用部署 web 應用程式的任何問題，請確定您有足夠的權限 hello 訂用帳戶中所述 toocreate/部署資源。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="b7f0c-337">如果**物件參考未設定物件的 tooinstance**執行 hello 時出現錯誤訊息[指令碼](log-analytics-itsmc-service-manager-script.md)請確認您輸入有效的值下,**使用者設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="b7f0c-338">如果您無法 toocreate 服務匯流排轉送命名空間，請確定該 hello 需要 hello 訂用帳戶中註冊資源提供者。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="b7f0c-339">如果未註冊，以手動方式建立從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="b7f0c-340">您也可以建立它時[建立 hello 混合式連接](log-analytics-itsmc-connections.md#configure-the-hybrid-connection)從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="b7f0c-341">與我們連絡</span><span class="sxs-lookup"><span data-stu-id="b7f0c-341">Contact us</span></span>

<span data-ttu-id="b7f0c-342">對於任何查詢或 hello IT 服務管理連接器上的意見反應，請與我們連絡[ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7f0c-343">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7f0c-343">Next steps</span></span>
<span data-ttu-id="b7f0c-344">[新增 ITSM 產品/服務 tooIT Service Management Connector](log-analytics-itsmc-connections.md)。</span><span class="sxs-lookup"><span data-stu-id="b7f0c-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
