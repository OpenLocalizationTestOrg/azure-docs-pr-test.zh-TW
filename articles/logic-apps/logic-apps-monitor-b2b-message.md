---
title: "監視 B2B 交易並設定記錄 - Azure Logic Apps | Microsoft Docs"
description: "監視 AS2、X12 和 EDIFACT 訊息，並啟動整合帳戶的診斷記錄"
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
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f717dae9a70a96944b623f22b90cf8c5a943f382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="87d33-103">監視和設定整合帳戶中 B2B 通訊的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="87d33-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="87d33-104">在您透過整合帳戶設定兩個執行中商務程序或應用程式之間的 B2B 通訊之後，這些實體也可以彼此交換訊息。</span><span class="sxs-lookup"><span data-stu-id="87d33-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="87d33-105">若要確認此通訊如預期運作，您可以設定 AS2、X12 和 EDIFACT 訊息的監視，以及透過 [Azure Log Analytics](../log-analytics/log-analytics-overview.md) 服務之整合帳戶的診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="87d33-105">To confirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through the [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="87d33-106">[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) 中的這個服務會監視您的雲端和內部部署環境，協助您維護其可用性和效能，同時收集執行階段詳細資料和事件，進行更豐富的偵錯。</span><span class="sxs-lookup"><span data-stu-id="87d33-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="87d33-107">您也可以[搭配使用診斷資料與其他服務](#extend-diagnostic-data)，例如 Azure 儲存體和 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="87d33-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="87d33-108">需求</span><span class="sxs-lookup"><span data-stu-id="87d33-108">Requirements</span></span>

* <span data-ttu-id="87d33-109">已設定診斷記錄的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="87d33-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="87d33-110">了解[如何設定該邏輯應用程式的記錄](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="87d33-110">Learn [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="87d33-111">在您符合這項需求之後，[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) 中應該有工作區。</span><span class="sxs-lookup"><span data-stu-id="87d33-111">After you've met this requirement, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="87d33-112">當您設定整合帳戶的記錄時，應該使用相同的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="87d33-112">You should use the same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="87d33-113">如果您沒有 OMS 工作區，請了解[如何建立 OMS 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="87d33-113">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="87d33-114">連結至邏輯應用程式的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="87d33-114">An integration account that's linked to your logic app.</span></span> <span data-ttu-id="87d33-115">了解[如何建立具有邏輯應用程式連結的整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="87d33-115">Learn [how to create an integration account with a link to your logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="87d33-116">開啟整合帳戶的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="87d33-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="87d33-117">您可以直接從整合帳戶或[透過 Azure 監視器服務](#azure-monitor-service)來開啟記錄。</span><span class="sxs-lookup"><span data-stu-id="87d33-117">You can turn on logging either directly from your integration account or [through the Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="87d33-118">Azure 監視器提供基礎結構層級資料的基本監視。</span><span class="sxs-lookup"><span data-stu-id="87d33-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="87d33-119">深入了解 [Azure 監視器](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="87d33-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="87d33-120">直接從整合帳戶開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="87d33-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="87d33-121">在 [Azure 入口網站](https://portal.azure.com)中，尋找並選取整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="87d33-121">In the [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="87d33-122">在 [監視] 下，選擇 [診斷記錄]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="87d33-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![尋找並選取整合帳戶，然後選擇 [診斷記錄]。](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="87d33-124">在您選取整合帳戶之後，會自動選取下列值。</span><span class="sxs-lookup"><span data-stu-id="87d33-124">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="87d33-125">如果這些值正確，請選擇 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="87d33-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="87d33-126">否則，請選取您想要的值：</span><span class="sxs-lookup"><span data-stu-id="87d33-126">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="87d33-127">在 [訂用帳戶] 下，選取您要與整合帳戶搭配使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="87d33-127">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="87d33-128">在 [資源群組] 下，選取您要與整合帳戶搭配使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="87d33-128">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="87d33-129">在 [資源類型] 下，選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="87d33-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="87d33-130">在 [資源] 下，選取整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="87d33-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="87d33-131">選擇 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="87d33-131">Choose **Turn on diagnostics**.</span></span>

   ![針對整合帳戶設定診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="87d33-133">在 [診斷設定] 的 [狀態] 下，選擇 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="87d33-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![開啟 Azure 診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="87d33-135">現在選取要用於記錄的 OMS 工作區和資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="87d33-135">Now select the OMS workspace and data to use for logging as shown:</span></span>

   1. <span data-ttu-id="87d33-136">選取 [傳送至 Log Analytics]。</span><span class="sxs-lookup"><span data-stu-id="87d33-136">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="87d33-137">在 [Log Analytics] 下，選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="87d33-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="87d33-138">在 [OMS 工作區] 下，選取要用於記錄的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="87d33-138">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="87d33-139">在 [記錄] 下，選取 [IntegrationAccountTrackingEvents] 分類。</span><span class="sxs-lookup"><span data-stu-id="87d33-139">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="87d33-140">選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="87d33-140">Choose **Save**.</span></span>

   ![設定 Log Analytics 以將診斷資料傳送至記錄](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="87d33-142">現在[在 OMS 中設定 B2B 訊息的追蹤](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="87d33-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="87d33-143">透過 Azure 監視器開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="87d33-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="87d33-144">在 [Azure 入口網站](https://portal.azure.com)中，於主要 Azure 功能表上依序選擇 [監視器] 和 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="87d33-144">In the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="87d33-145">然後選取整合帳戶，如下所示：</span><span class="sxs-lookup"><span data-stu-id="87d33-145">Then select your integration account as shown here:</span></span>

   ![依序選擇 [監視器] 和 [診斷記錄]，然後選取整合帳戶](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="87d33-147">在您選取整合帳戶之後，會自動選取下列值。</span><span class="sxs-lookup"><span data-stu-id="87d33-147">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="87d33-148">如果這些值正確，請選擇 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="87d33-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="87d33-149">否則，請選取您想要的值：</span><span class="sxs-lookup"><span data-stu-id="87d33-149">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="87d33-150">在 [訂用帳戶] 下，選取您要與整合帳戶搭配使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="87d33-150">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="87d33-151">在 [資源群組] 下，選取您要與整合帳戶搭配使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="87d33-151">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="87d33-152">在 [資源類型] 下，選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="87d33-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="87d33-153">在 [資源] 下，選取整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="87d33-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="87d33-154">選擇 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="87d33-154">Choose **Turn on diagnostics**.</span></span>

   ![針對整合帳戶設定診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="87d33-156">在 [診斷設定] 下，選擇 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="87d33-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![開啟 Azure 診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="87d33-158">現在選取用於記錄的 OMS 工作區和事件類別目錄，如下所示：</span><span class="sxs-lookup"><span data-stu-id="87d33-158">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="87d33-159">選取 [傳送至 Log Analytics]。</span><span class="sxs-lookup"><span data-stu-id="87d33-159">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="87d33-160">在 [Log Analytics] 下，選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="87d33-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="87d33-161">在 [OMS 工作區] 下，選取要用於記錄的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="87d33-161">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="87d33-162">在 [記錄] 下，選取 [IntegrationAccountTrackingEvents] 分類。</span><span class="sxs-lookup"><span data-stu-id="87d33-162">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="87d33-163">完成之後，請選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="87d33-163">When you're done, choose **Save**.</span></span>

   ![設定 Log Analytics 以將診斷資料傳送至記錄](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="87d33-165">現在[在 OMS 中設定 B2B 訊息的追蹤](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="87d33-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="87d33-166">延伸搭配使用診斷資料與其他服務的方式和位置</span><span class="sxs-lookup"><span data-stu-id="87d33-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="87d33-167">使用 Azure Log Analytics，即可延伸如何搭配使用邏輯應用程式的診斷資料與其他 Azure services，例如：</span><span class="sxs-lookup"><span data-stu-id="87d33-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="87d33-168">在 Azure 儲存體中封存 Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="87d33-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="87d33-169">將 Azure 診斷記錄串流至 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="87d33-169">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="87d33-170">您可以接著使用其他服務的遙測和分析來取得即時監視，例如 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 和 [Power BI](../log-analytics/log-analytics-powerbi.md)。</span><span class="sxs-lookup"><span data-stu-id="87d33-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="87d33-171">例如：</span><span class="sxs-lookup"><span data-stu-id="87d33-171">For example:</span></span>

* [<span data-ttu-id="87d33-172">將資料從事件中樞串流至串流分析</span><span class="sxs-lookup"><span data-stu-id="87d33-172">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="87d33-173">使用串流分析分析串流資料並在 Power BI 中建立即時分析儀表板</span><span class="sxs-lookup"><span data-stu-id="87d33-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="87d33-174">根據您要設定的選項，確定您先[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)或[建立 Azure 事件中樞](../event-hubs/event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="87d33-174">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="87d33-175">然後選取您要傳送診斷資料的選項：</span><span class="sxs-lookup"><span data-stu-id="87d33-175">Then select the options for where you want to send diagnostic data:</span></span>

![將資料傳送至 Azure 儲存體帳戶或事件中樞](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="87d33-177">只有在您選擇使用儲存體帳戶時，才會套用保留期間。</span><span class="sxs-lookup"><span data-stu-id="87d33-177">Retention periods apply only when you choose to use a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="87d33-178">支援的追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="87d33-178">Supported tracking schemas</span></span>

<span data-ttu-id="87d33-179">Azure 支援下列追蹤結構描述類型，其中除了自訂類型外都有固定的結構描述。</span><span class="sxs-lookup"><span data-stu-id="87d33-179">Azure supports these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="87d33-180">AS2 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="87d33-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="87d33-181">X12 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="87d33-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="87d33-182">自訂追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="87d33-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="87d33-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87d33-183">Next steps</span></span>

* [<span data-ttu-id="87d33-184">在 OMS 中追蹤 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="87d33-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "在 OMS 中追蹤 B2B 訊息")
* [<span data-ttu-id="87d33-185">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="87d33-185">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "了解企業整合套件")

