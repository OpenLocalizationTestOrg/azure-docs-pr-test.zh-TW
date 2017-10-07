---
title: "aaaHow toomonitor Azure 儲存體帳戶 |Microsoft 文件"
description: "了解如何 toomonitor Azure 中使用的儲存體帳戶 hello Azure 入口網站。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a><span data-ttu-id="32e3b-103">監視 hello Azure 入口網站的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="32e3b-103">Monitor a storage account in hello Azure portal</span></span>

<span data-ttu-id="32e3b-104">[Azure 儲存體分析](../storage-analytics.md)會提供所有儲存體服務的計量以及 Blob、佇列和資料表的記錄。</span><span class="sxs-lookup"><span data-stu-id="32e3b-104">[Azure Storage Analytics](../storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="32e3b-105">您可以使用 hello [Azure 入口網站](https://portal.azure.com)tooconfigure 哪些度量和記錄檔會記錄為您的帳戶，並設定提供度量資料的視覺化呈現的圖表。</span><span class="sxs-lookup"><span data-stu-id="32e3b-105">You can use hello [Azure portal](https://portal.azure.com) tooconfigure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="32e3b-106">沒有與檢查 hello Azure 入口網站中的監視資料相關聯的成本。</span><span class="sxs-lookup"><span data-stu-id="32e3b-106">There are costs associated with examining monitoring data in hello Azure portal.</span></span> <span data-ttu-id="32e3b-107">如需詳細資訊，請參閱 [儲存體分析及計費](/rest/api/storageservices/Storage-Analytics-and-Billing)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="32e3b-108">Azure 檔案儲存體目前支援儲存體分析度量，但還不支援記錄。</span><span class="sxs-lookup"><span data-stu-id="32e3b-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="32e3b-109">儲存體帳戶的複寫類型的區域備援儲存體 (ZRS) 目前沒有 hello 度量或記錄功能已啟用。</span><span class="sxs-lookup"><span data-stu-id="32e3b-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have hello metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="32e3b-110">如需使用儲存體分析和其他工具 tooidentify 的深度指南，診斷和疑難排解 Azure 儲存體相關問題，請參閱[監視、 診斷和疑難排解 Microsoft Azure 儲存體](../storage-monitoring-diagnosing-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-110">For an in-depth guide on using Storage Analytics and other tools tooidentify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="32e3b-111">設定儲存體帳戶的監視</span><span class="sxs-lookup"><span data-stu-id="32e3b-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="32e3b-112">在 hello [Azure 入口網站](https://portal.azure.com)，選取**儲存體帳戶**，然後 hello 儲存體帳戶名稱 tooopen hello 帳戶儀表板。</span><span class="sxs-lookup"><span data-stu-id="32e3b-112">In hello [Azure portal](https://portal.azure.com), select **Storage accounts**, then hello storage account name tooopen hello account dashboard.</span></span>
1. <span data-ttu-id="32e3b-113">選取**診斷**在 hello**監視**hello 功能表 刀鋒視窗的區段。</span><span class="sxs-lookup"><span data-stu-id="32e3b-113">Select **Diagnostics** in hello **MONITORING** section of hello menu blade.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="32e3b-115">選取 hello**類型**的每個度量資料**服務**toomonitor，並 hello**保留原則**hello 資料。</span><span class="sxs-lookup"><span data-stu-id="32e3b-115">Select hello **type** of metrics data for each **service** you wish toomonitor, and hello **retention policy** for hello data.</span></span> <span data-ttu-id="32e3b-116">您也可以停用監視，可設定**狀態**太**關閉**。</span><span class="sxs-lookup"><span data-stu-id="32e3b-116">You can also disable monitoring by setting **Status** too**Off**.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="32e3b-118">您可以為每個服務啟用兩種類型的計量，新的儲存體帳戶預設會同時啟用這兩種類型︰</span><span class="sxs-lookup"><span data-stu-id="32e3b-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="32e3b-119">**彙總**︰收集計量，例如入口流量/出口流量、可用性、延遲和成功百分比。</span><span class="sxs-lookup"><span data-stu-id="32e3b-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="32e3b-120">這些度量會彙總的 hello blob、 佇列、 表格和檔案服務。</span><span class="sxs-lookup"><span data-stu-id="32e3b-120">These metrics are aggregated for hello blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="32e3b-121">**每個應用程式開發介面**： 在加法 toohello 彙總度量資訊，會收集 hello 同一組 hello Azure 儲存體服務 API 中的每個儲存體作業的度量。</span><span class="sxs-lookup"><span data-stu-id="32e3b-121">**Per API**: In addition toohello aggregate metrics, collects hello same set of metrics for each storage operation in hello Azure Storage service API.</span></span>

   <span data-ttu-id="32e3b-122">tooset hello 資料保留原則，移動 hello**保留 （天）**滑桿或輸入 hello 天數的資料 tooretain，從 1 too365。</span><span class="sxs-lookup"><span data-stu-id="32e3b-122">tooset hello data retention policy, move hello **Retention (days)** slider or enter hello number of days of data tooretain, from 1 too365.</span></span> <span data-ttu-id="32e3b-123">新的儲存體帳戶的 hello 預設值是七天。</span><span class="sxs-lookup"><span data-stu-id="32e3b-123">hello default for new storage accounts is seven days.</span></span> <span data-ttu-id="32e3b-124">如果您不想 tooset 保留原則，請輸入零。</span><span class="sxs-lookup"><span data-stu-id="32e3b-124">If you do not want tooset a retention policy, enter zero.</span></span> <span data-ttu-id="32e3b-125">如果沒有任何保留原則，是由 tooyou toodelete hello 監視資料。</span><span class="sxs-lookup"><span data-stu-id="32e3b-125">If there is no retention policy, it is up tooyou toodelete hello monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="32e3b-126">若您以手動方式刪除計量資料，將需要付費。</span><span class="sxs-lookup"><span data-stu-id="32e3b-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="32e3b-127">不花一毛錢 hello 系統會刪除過時的分析資料 （早於保留原則的資料）。</span><span class="sxs-lookup"><span data-stu-id="32e3b-127">Stale analytics data (data older than your retention policy) is deleted by hello system at no cost.</span></span> <span data-ttu-id="32e3b-128">我們建議您將設定保留原則，根據您的帳戶為您想 tooretain 儲存體分析資料的時間長度。</span><span class="sxs-lookup"><span data-stu-id="32e3b-128">We recommend setting a retention policy based on how long you want tooretain storage analytics data for your account.</span></span> <span data-ttu-id="32e3b-129">如需詳細資訊，請參閱[當您啟用儲存體度量時，會產生哪些費用？](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-129">See [What charges do you incur when you enable storage metrics?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="32e3b-130">當您完成 hello 監視組態時，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="32e3b-130">When you finish hello monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="32e3b-131">一組預設的度量資訊會顯示在圖表上 hello 儲存體帳戶 刀鋒視窗，以及 hello 個別服務刀鋒視窗 （blob、 佇列、 表格和檔案）。</span><span class="sxs-lookup"><span data-stu-id="32e3b-131">A default set of metrics is displayed in charts on hello storage account blade, as well as hello individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="32e3b-132">一旦您啟用度量服務，就會在其圖表中的資料 tooappear tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="32e3b-132">Once you've enabled metrics for a service, it may take up tooan hour for data tooappear in its charts.</span></span> <span data-ttu-id="32e3b-133">您可以選取**編輯**上任何的度量圖表 太[設定的度量](#how-to-customize-metrics-charts)hello 圖表中會顯示。</span><span class="sxs-lookup"><span data-stu-id="32e3b-133">You can select **Edit** on any metric chart too[configure which metrics](#how-to-customize-metrics-charts) are displayed in hello chart.</span></span>

<span data-ttu-id="32e3b-134">您可以設定停用度量收集和記錄**狀態**太**關閉**。</span><span class="sxs-lookup"><span data-stu-id="32e3b-134">You can disable metrics collection and logging by setting **Status** too**Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="32e3b-135">Azure 儲存體使用[資料表儲存體](../common/storage-introduction.md#table-storage)toostore hello 和度量資訊，您儲存體帳戶，帳戶中的資料表中的存放區 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="32e3b-135">Azure Storage uses [table storage](../common/storage-introduction.md#table-storage) toostore hello metrics for your storage account, and stores hello metrics in tables in your account.</span></span> <span data-ttu-id="32e3b-136">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="32e3b-136">For more information, see.</span></span> <span data-ttu-id="32e3b-137">[度量的儲存方式](../common/storage-analytics.md#how-metrics-are-stored)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-137">[How metrics are stored](../common/storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="32e3b-138">自訂計量圖表</span><span class="sxs-lookup"><span data-stu-id="32e3b-138">Customize metrics charts</span></span>

<span data-ttu-id="32e3b-139">使用下列程序 toochoose hello 的儲存體度量 tooview 度量圖表中。</span><span class="sxs-lookup"><span data-stu-id="32e3b-139">Use hello following procedure toochoose which storage metrics tooview in a metrics chart.</span></span> 

1. <span data-ttu-id="32e3b-140">啟動儲存體度量的圖表顯示 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="32e3b-140">Start by displaying a storage metric chart in hello Azure portal.</span></span> <span data-ttu-id="32e3b-141">您可以找到上 hello 圖表**儲存體帳戶 刀鋒視窗**在 hello**度量**刀鋒視窗中的個別服務 （blob、 佇列、 表格及檔案）。</span><span class="sxs-lookup"><span data-stu-id="32e3b-141">You can find charts on hello **storage account blade** and in hello **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="32e3b-142">在此範例中，我們使用下列圖表顯示在 [hello hello**儲存體帳戶] 刀鋒視窗**:</span><span class="sxs-lookup"><span data-stu-id="32e3b-142">In this example, we work with hello following chart that appears on hello **storage account blade**:</span></span>

   ![Azure 入口網站中的圖表選擇](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="32e3b-144">接下來，按一下 hello 圖表 tooopen hello 內的任何位置**度量**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="32e3b-144">Next, click anywhere within hello chart tooopen hello **Metric** blade.</span></span> <span data-ttu-id="32e3b-145">選取**編輯圖表**tooopen hello**編輯圖表**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="32e3b-145">Select **Edit chart** tooopen hello **Edit Chart** blade.</span></span>

   ![[圖表] 刀鋒視窗上的 [編輯圖表] 按鈕](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="32e3b-147">在 hello**編輯圖表**刀鋒視窗中，選取 hello**時間範圍**hello 度量 toodisplay hello 圖表和 hello 的**服務**（blob、 佇列、 資料表、 檔案） 您希望其度量toodisplay。</span><span class="sxs-lookup"><span data-stu-id="32e3b-147">On hello **Edit Chart** blade, select hello **Time Range** of hello metrics toodisplay in hello chart, and hello **service** (blob, queue, table, file) whose metrics you wish toodisplay.</span></span> <span data-ttu-id="32e3b-148">這裡我們選取 toodisplay hello 過去一週的度量 hello blob 服務：</span><span class="sxs-lookup"><span data-stu-id="32e3b-148">Here we've selected toodisplay hello past week's metrics for hello blob service:</span></span>

   ![在 hello 編輯圖表 刀鋒視窗的時間範圍和服務選項](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="32e3b-150">選取 hello 個別**度量**像您具有 hello 圖表中顯示，請按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="32e3b-150">Select hello individual **metrics** you'd like displayed in hello chart, then click **OK**.</span></span> <span data-ttu-id="32e3b-151">例如，這裡我們選擇 toodisplay hello *ContainerCount*和*ObjectCount*度量：</span><span class="sxs-lookup"><span data-stu-id="32e3b-151">For example, here we've chosen toodisplay hello *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![[編輯圖表] 刀鋒視窗中的個別計量選擇](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="32e3b-153">圖表設定不會影響 hello 集合、 彙總或儲存體監視 hello 儲存體帳戶中的資料，請只 hello 度量資料的檢視。</span><span class="sxs-lookup"><span data-stu-id="32e3b-153">Your chart settings do not affect hello collection, aggregation, or storage of monitoring data in hello storage account, only hello viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="32e3b-154">計量在圖表中的可用性</span><span class="sxs-lookup"><span data-stu-id="32e3b-154">Metrics availability in charts</span></span>

<span data-ttu-id="32e3b-155">可用的度量變更 hello 清單已選擇 hello 下拉式清單中的服務和您正在編輯的 hello 圖表 hello 單位類型。</span><span class="sxs-lookup"><span data-stu-id="32e3b-155">hello list of available metrics changes based on which service you've chosen in hello drop-down, and hello unit type of hello chart you're editing.</span></span> <span data-ttu-id="32e3b-156">例如，只有在編輯以百分比顯示單位的圖表時，才能選取百分比計量，例如 PercentNetworkError 和 PercentThrottlingError︰</span><span class="sxs-lookup"><span data-stu-id="32e3b-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![Hello Azure 入口網站中的要求錯誤百分比圖表](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="32e3b-158">計量解析</span><span class="sxs-lookup"><span data-stu-id="32e3b-158">Metrics resolution</span></span>

<span data-ttu-id="32e3b-159">您選取診斷中的 hello 度量資訊會決定 hello 解析度 hello 度量可供您的帳戶：</span><span class="sxs-lookup"><span data-stu-id="32e3b-159">hello metrics you selected in Diagnostics determines hello resolution of hello metrics that are available for your account:</span></span>

* <span data-ttu-id="32e3b-160">**彙總**監視會提供入口流量/出口流量、可用性、延遲和成功百分比等計量。</span><span class="sxs-lookup"><span data-stu-id="32e3b-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="32e3b-161">這些度量會彙總從 hello blob、 資料表、 檔案和佇列服務。</span><span class="sxs-lookup"><span data-stu-id="32e3b-161">These metrics are aggregated from hello blob, table, file, and queue services.</span></span>
* <span data-ttu-id="32e3b-162">**每個應用程式開發介面**提供更精細的解析度 （包括計量） 適用於個別儲存作業，此外 toohello 服務層級彙總。</span><span class="sxs-lookup"><span data-stu-id="32e3b-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition toohello service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="32e3b-163">設定計量警示</span><span class="sxs-lookup"><span data-stu-id="32e3b-163">Configure metrics alerts</span></span>

<span data-ttu-id="32e3b-164">您可以建立警示 toonotify 時已達到儲存體資源度量的閾值。</span><span class="sxs-lookup"><span data-stu-id="32e3b-164">You can create alerts toonotify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="32e3b-165">tooopen hello**警示規則 刀鋒視窗**，捲動 toohello**監視**區段 hello**功能表刀鋒視窗**選取**警示規則**。</span><span class="sxs-lookup"><span data-stu-id="32e3b-165">tooopen hello **Alert rules blade**, scroll down toohello **MONITORING** section of hello **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="32e3b-166">選取**新增警示**tooopen hello**加入警示規則**刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="32e3b-166">Select **Add alert** tooopen hello **Add an alert rule** blade</span></span>
1. <span data-ttu-id="32e3b-167">選取**資源**（blob、 檔案、 佇列、 資料表） 從 hello 下拉式清單中，然後輸入**名稱**和**描述**針對新的警示規則。</span><span class="sxs-lookup"><span data-stu-id="32e3b-167">Select a **Resource** (blob, file, queue, table) from hello drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="32e3b-168">選取 hello**度量**，您想要 tooadd 警示，警示**條件**，和**閾值**。</span><span class="sxs-lookup"><span data-stu-id="32e3b-168">Select hello **Metric** for which you'd like tooadd an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="32e3b-169">您選擇 hello 閾值單位類型而有所不同 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="32e3b-169">hello threshold unit type changes depending on hello metric you've chosen.</span></span> <span data-ttu-id="32e3b-170">例如，「 計數 」 是 hello 的單位類型*ContainerCount*，hello hello 單位時*PercentNetworkError*度量是百分比。</span><span class="sxs-lookup"><span data-stu-id="32e3b-170">For example, "count" is hello unit type for *ContainerCount*, while hello unit for hello *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="32e3b-171">選取 hello**期間**。</span><span class="sxs-lookup"><span data-stu-id="32e3b-171">Select hello **Period**.</span></span> <span data-ttu-id="32e3b-172">度量達到或超過 hello 臨界值內 hello 期間觸發警示。</span><span class="sxs-lookup"><span data-stu-id="32e3b-172">Metrics that reach or exceed hello Threshold within hello period trigger an alert.</span></span>
1. <span data-ttu-id="32e3b-173">(選擇性) 設定 [電子郵件] 和 [Webhook] 通知。</span><span class="sxs-lookup"><span data-stu-id="32e3b-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="32e3b-174">如需 Webhook 的詳細資訊，請參閱[針對 Azure 度量警示設定 Webhook](../../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="32e3b-175">如果您未設定電子郵件或 webhook 通知，通知只會出現在 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="32e3b-175">If you do not configure email or webhook notifications, alerts will appear only in hello Azure portal.</span></span>

![Hello Azure 入口網站中的 [新增警示規則] 刀鋒視窗](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a><span data-ttu-id="32e3b-177">新增度量圖表 toohello 入口網站儀表板</span><span class="sxs-lookup"><span data-stu-id="32e3b-177">Add metrics charts toohello portal dashboard</span></span>

<span data-ttu-id="32e3b-178">您可以針對任何儲存體帳戶 tooyour 入口網站儀表板新增 Azure 儲存體度量圖表。</span><span class="sxs-lookup"><span data-stu-id="32e3b-178">You can add Azure Storage metrics charts for any of your storage accounts tooyour portal dashboard.</span></span>

1. <span data-ttu-id="32e3b-179">選取按一下**編輯儀表板**hello 中檢視儀表板時[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-179">Select click **Edit dashboard** while viewing your dashboard in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="32e3b-180">在 hello**並排組件庫**，選取**尋找磚所** > **類型**。</span><span class="sxs-lookup"><span data-stu-id="32e3b-180">In hello **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="32e3b-181">選取 [類型] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="32e3b-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="32e3b-182">在**資源**，選取您想 tooadd toohello 儀表板的度量的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="32e3b-182">In **Resources**, select hello storage account whose metrics you wish tooadd toohello dashboard.</span></span>
1. <span data-ttu-id="32e3b-183">選取 [類別] > [監視]。</span><span class="sxs-lookup"><span data-stu-id="32e3b-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="32e3b-184">拖放 hello 圖表圖層到 hello 度量您想要顯示的儀表板。</span><span class="sxs-lookup"><span data-stu-id="32e3b-184">Drag-and-drop hello chart tile onto your dashboard for hello metric you'd like displayed.</span></span> <span data-ttu-id="32e3b-185">針對所有您想要顯示的度量 hello 儀表板上重複。</span><span class="sxs-lookup"><span data-stu-id="32e3b-185">Repeat for all metrics you'd like displayed on hello dashboard.</span></span> <span data-ttu-id="32e3b-186">在下列映像的 hello，hello"Blob 的總要求 」 圖表會反白顯示為例，但所有 hello 圖表都可供儀表板上的位置。</span><span class="sxs-lookup"><span data-stu-id="32e3b-186">In hello following image, hello "Blobs - Total requests" chart is highlighted as an example, but all hello charts are available for placement on your dashboard.</span></span>

   ![Azure 入口網站中的圖格庫](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="32e3b-188">選取**完成自訂**hello hello 儀表板當您完成新增圖表頂端附近。</span><span class="sxs-lookup"><span data-stu-id="32e3b-188">Select **Done customizing** near hello top of hello dashboard when you're done adding charts.</span></span>

<span data-ttu-id="32e3b-189">一旦您已經新增圖表 tooyour 儀表板，您可以進一步自訂這些中所述[自訂度量圖表](#how-to-customize-metrics-charts)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-189">Once you've added charts tooyour dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="32e3b-190">設定記錄</span><span class="sxs-lookup"><span data-stu-id="32e3b-190">Configure logging</span></span>

<span data-ttu-id="32e3b-191">您可以指示 Azure 儲存體 toosave 診斷記錄檔的讀取、 寫入和刪除 hello blob、 資料表和佇列服務的要求。</span><span class="sxs-lookup"><span data-stu-id="32e3b-191">You can instruct Azure Storage toosave diagnostics logs for read, write, and delete requests for hello blob, table, and queue services.</span></span> <span data-ttu-id="32e3b-192">hello 資料保留原則設定也適用於 toothese 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="32e3b-192">hello data retention policy you set also applies toothese logs.</span></span>

> [!NOTE]
> <span data-ttu-id="32e3b-193">Azure 檔案儲存體目前支援儲存體分析度量，但還不支援記錄。</span><span class="sxs-lookup"><span data-stu-id="32e3b-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="32e3b-194">在 [hello [Azure 入口網站](https://portal.azure.com)，選取**儲存體帳戶**，然後 hello 儲存體帳戶 tooopen hello 儲存體帳戶] 刀鋒視窗的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="32e3b-194">In hello [Azure portal](https://portal.azure.com), select **Storage accounts**, then hello name of hello storage account tooopen hello storage account blade.</span></span>
1. <span data-ttu-id="32e3b-195">選取**診斷**在 hello**監視**hello 功能表 刀鋒視窗的區段。</span><span class="sxs-lookup"><span data-stu-id="32e3b-195">Select **Diagnostics** in hello **MONITORING** section of hello menu blade.</span></span>

    ![診斷功能表項目 監視中 hello Azure 入口網站。](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="32e3b-197">確保**狀態**設定得**上**，並選取 hello**服務**，您想要 tooenable 記錄。</span><span class="sxs-lookup"><span data-stu-id="32e3b-197">Ensure **Status** is set too**On**, and select hello **services** for which you'd like tooenable logging.</span></span>

    ![設定登入 hello Azure 入口網站。](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="32e3b-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="32e3b-199">Click **Save**.</span></span>

<span data-ttu-id="32e3b-200">hello 診斷記錄檔會儲存在名為 $logs 儲存體帳戶中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="32e3b-200">hello diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="32e3b-201">您可以檢視 hello 記錄資料使用儲存體總管類似 hello [Microsoft 儲存體總管](http://storageexplorer.com)，或以程式設計方式使用 hello 儲存體用戶端程式庫或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="32e3b-201">You can view hello log data using a storage explorer like hello [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using hello storage client library or PowerShell.</span></span>

<span data-ttu-id="32e3b-202">如需存取 hello $logs 容器資訊，請參閱[啟用儲存體記錄和存取記錄資料](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-202">For information about accessing hello $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32e3b-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32e3b-203">Next steps</span></span>

* <span data-ttu-id="32e3b-204">尋找更多關於儲存體分析之[計量、記錄和帳單](../storage-analytics.md)的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="32e3b-204">Find more details about [metrics, logging, and billing](../storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="32e3b-205">使用 PowerShell 和程式設計方式 (利用 C#) [啟用 Azure 儲存體計量和檢視計量資料](../storage-enable-and-view-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="32e3b-205">[Enable Azure Storage metrics and view metrics data](../storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>
