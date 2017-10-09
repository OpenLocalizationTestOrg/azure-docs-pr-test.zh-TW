---
title: "aaaMonitor B2B 交易並設定記錄-Azure 邏輯應用程式 |Microsoft 文件"
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
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="d850d-103">監視和設定整合帳戶中 B2B 通訊的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d850d-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="d850d-104">在您透過整合帳戶設定兩個執行中商務程序或應用程式之間的 B2B 通訊之後，這些實體也可以彼此交換訊息。</span><span class="sxs-lookup"><span data-stu-id="d850d-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="d850d-105">tooconfirm 此通訊如預期般運作，您可以設定 AS2，X12、 監視和 EDIFACT 訊息，以及透過 hello 整合帳戶的診斷記錄[Azure Log Analytics](../log-analytics/log-analytics-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="d850d-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="d850d-106">[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) 中的這個服務會監視您的雲端和內部部署環境，協助您維護其可用性和效能，同時收集執行階段詳細資料和事件，進行更豐富的偵錯。</span><span class="sxs-lookup"><span data-stu-id="d850d-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="d850d-107">您也可以[搭配使用診斷資料與其他服務](#extend-diagnostic-data)，例如 Azure 儲存體和 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="d850d-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="d850d-108">需求</span><span class="sxs-lookup"><span data-stu-id="d850d-108">Requirements</span></span>

* <span data-ttu-id="d850d-109">已設定診斷記錄的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d850d-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="d850d-110">深入了解[如何該邏輯應用程式的記錄 tooset](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)。</span><span class="sxs-lookup"><span data-stu-id="d850d-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="d850d-111">您雖然符合此需求之後，您應該有 hello 中的工作區[Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d850d-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="d850d-112">您應該使用 hello 同一個 OMS 工作區，當您設定為整合帳戶記錄。</span><span class="sxs-lookup"><span data-stu-id="d850d-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="d850d-113">如果您沒有 OMS 工作區，了解[如何 toocreate OMS 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d850d-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="d850d-114">已連結 tooyour 邏輯應用程式整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="d850d-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="d850d-115">深入了解[toocreate 整合與連結 tooyour 邏輯應用程式的帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="d850d-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="d850d-116">開啟整合帳戶的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d850d-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="d850d-117">您可以開啟記錄直接從整合帳戶或[hello Azure 監視服務透過](#azure-monitor-service)。</span><span class="sxs-lookup"><span data-stu-id="d850d-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="d850d-118">Azure 監視器提供基礎結構層級資料的基本監視。</span><span class="sxs-lookup"><span data-stu-id="d850d-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="d850d-119">深入了解 [Azure 監視器](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="d850d-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="d850d-120">直接從整合帳戶開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d850d-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="d850d-121">在 hello [Azure 入口網站](https://portal.azure.com)、 尋找並選取 integration 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d850d-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="d850d-122">在 [監視] 下，選擇 [診斷記錄]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d850d-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![尋找並選取整合帳戶，然後選擇 [診斷記錄]。](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="d850d-124">選取整合帳戶之後，會自動選取下列值的 hello。</span><span class="sxs-lookup"><span data-stu-id="d850d-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="d850d-125">如果這些值正確，請選擇 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="d850d-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="d850d-126">否則，請選取您想要的 hello 值：</span><span class="sxs-lookup"><span data-stu-id="d850d-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="d850d-127">在下**訂用帳戶**，選取 hello 您整合帳戶所使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d850d-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="d850d-128">在下**資源群組**，選取您整合帳戶所使用的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d850d-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="d850d-129">在 [資源類型] 下，選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="d850d-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="d850d-130">在 [資源] 下，選取整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="d850d-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="d850d-131">選擇 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="d850d-131">Choose **Turn on diagnostics**.</span></span>

   ![針對整合帳戶設定診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="d850d-133">在 [診斷設定] 的 [狀態] 下，選擇 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="d850d-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![開啟 Azure 診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="d850d-135">現在選取 hello OMS 工作區和資料 toouse 記錄，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d850d-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="d850d-136">選取**傳送 tooLog 分析**。</span><span class="sxs-lookup"><span data-stu-id="d850d-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="d850d-137">在 [Log Analytics] 下，選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="d850d-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="d850d-138">在下**OMS 工作區**，選取 hello OMS 工作區 toouse 進行記錄。</span><span class="sxs-lookup"><span data-stu-id="d850d-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="d850d-139">在下**記錄**，選取 hello **IntegrationAccountTrackingEvents**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="d850d-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="d850d-140">選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d850d-140">Choose **Save**.</span></span>

   ![設定記錄分析，讓您可以傳送診斷資料 tooa 記錄檔](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="d850d-142">現在[在 OMS 中設定 B2B 訊息的追蹤](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="d850d-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="d850d-143">透過 Azure 監視器開啟診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d850d-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="d850d-144">在 hello [Azure 入口網站](https://portal.azure.com)，在 hello Azure 的主功能表，選擇**監視器**，**診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="d850d-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="d850d-145">然後選取整合帳戶，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d850d-145">Then select your integration account as shown here:</span></span>

   ![依序選擇 [監視器] 和 [診斷記錄]，然後選取整合帳戶](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="d850d-147">選取整合帳戶之後，會自動選取下列值的 hello。</span><span class="sxs-lookup"><span data-stu-id="d850d-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="d850d-148">如果這些值正確，請選擇 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="d850d-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="d850d-149">否則，請選取您想要的 hello 值：</span><span class="sxs-lookup"><span data-stu-id="d850d-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="d850d-150">在下**訂用帳戶**，選取 hello 您整合帳戶所使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d850d-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="d850d-151">在下**資源群組**，選取您整合帳戶所使用的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d850d-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="d850d-152">在 [資源類型] 下，選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="d850d-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="d850d-153">在 [資源] 下，選取整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="d850d-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="d850d-154">選擇 [開啟診斷]。</span><span class="sxs-lookup"><span data-stu-id="d850d-154">Choose **Turn on diagnostics**.</span></span>

   ![針對整合帳戶設定診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="d850d-156">在 [診斷設定] 下，選擇 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="d850d-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![開啟 Azure 診斷](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="d850d-158">現在選取 hello OMS 工作區和事件類別目錄的記錄，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d850d-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="d850d-159">選取**傳送 tooLog 分析**。</span><span class="sxs-lookup"><span data-stu-id="d850d-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="d850d-160">在 [Log Analytics] 下，選擇 [設定]。</span><span class="sxs-lookup"><span data-stu-id="d850d-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="d850d-161">在下**OMS 工作區**，選取 hello OMS 工作區 toouse 進行記錄。</span><span class="sxs-lookup"><span data-stu-id="d850d-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="d850d-162">在下**記錄**，選取 hello **IntegrationAccountTrackingEvents**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="d850d-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="d850d-163">完成之後，請選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d850d-163">When you're done, choose **Save**.</span></span>

   ![設定記錄分析，讓您可以傳送診斷資料 tooa 記錄檔](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="d850d-165">現在[在 OMS 中設定 B2B 訊息的追蹤](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="d850d-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="d850d-166">延伸搭配使用診斷資料與其他服務的方式和位置</span><span class="sxs-lookup"><span data-stu-id="d850d-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="d850d-167">使用 Azure Log Analytics，即可延伸如何搭配使用邏輯應用程式的診斷資料與其他 Azure services，例如：</span><span class="sxs-lookup"><span data-stu-id="d850d-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="d850d-168">在 Azure 儲存體中封存 Azure 診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d850d-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="d850d-169">資料流 Azure 診斷記錄檔 tooAzure 事件中心</span><span class="sxs-lookup"><span data-stu-id="d850d-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="d850d-170">您可以接著使用其他服務的遙測和分析來取得即時監視，例如 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 和 [Power BI](../log-analytics/log-analytics-powerbi.md)。</span><span class="sxs-lookup"><span data-stu-id="d850d-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="d850d-171">例如：</span><span class="sxs-lookup"><span data-stu-id="d850d-171">For example:</span></span>

* [<span data-ttu-id="d850d-172">從事件中心 tooStream 分析的資料流資料</span><span class="sxs-lookup"><span data-stu-id="d850d-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="d850d-173">使用串流分析分析串流資料並在 Power BI 中建立即時分析儀表板</span><span class="sxs-lookup"><span data-stu-id="d850d-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="d850d-174">根據您想要設定的 hello 選項，請確定您第一次[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)或[建立 Azure 事件中樞](../event-hubs/event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="d850d-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="d850d-175">然後選取您想要 toosend 診斷資料的 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="d850d-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![傳送資料 tooAzure 儲存體帳戶或事件中心](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="d850d-177">Toouse 您選擇儲存體帳戶時，才會套用保留期限。</span><span class="sxs-lookup"><span data-stu-id="d850d-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="d850d-178">支援的追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="d850d-178">Supported tracking schemas</span></span>

<span data-ttu-id="d850d-179">Azure 支援這些追蹤結構描述類型，這些全都已修正除了 hello 自訂類型的結構描述。</span><span class="sxs-lookup"><span data-stu-id="d850d-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="d850d-180">AS2 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="d850d-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="d850d-181">X12 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="d850d-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="d850d-182">自訂追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="d850d-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="d850d-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d850d-183">Next steps</span></span>

* [<span data-ttu-id="d850d-184">在 OMS 中追蹤 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="d850d-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "在 OMS 中追蹤 B2B 訊息")
* [<span data-ttu-id="d850d-185">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="d850d-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")

