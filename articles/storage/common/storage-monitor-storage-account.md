---
title: "如何監視 Azure 儲存體帳戶 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站來監視 Azure 中的儲存體帳戶。"
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
ms.openlocfilehash: e8fbc4ecdffe62806019f494e1412cfedbccf71f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-a-storage-account-in-the-azure-portal"></a><span data-ttu-id="5a71f-103">在 Azure 入口網站中監視儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5a71f-103">Monitor a storage account in the Azure portal</span></span>

<span data-ttu-id="5a71f-104">[Azure 儲存體分析](../storage-analytics.md)會提供所有儲存體服務的計量以及 Blob、佇列和資料表的記錄。</span><span class="sxs-lookup"><span data-stu-id="5a71f-104">[Azure Storage Analytics](../storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="5a71f-105">您可以使用 [Azure 入口網站](https://portal.azure.com)設定要為帳戶記錄哪些計量和記錄，並設定可利用視覺方式呈現計量資料的圖表。</span><span class="sxs-lookup"><span data-stu-id="5a71f-105">You can use the [Azure portal](https://portal.azure.com) to configure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="5a71f-106">在 Azure 入口網站中查看監視資料會衍生相關成本。</span><span class="sxs-lookup"><span data-stu-id="5a71f-106">There are costs associated with examining monitoring data in the Azure portal.</span></span> <span data-ttu-id="5a71f-107">如需詳細資訊，請參閱 [儲存體分析及計費](/rest/api/storageservices/Storage-Analytics-and-Billing)。</span><span class="sxs-lookup"><span data-stu-id="5a71f-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="5a71f-108">Azure 檔案儲存體目前支援儲存體分析度量，但還不支援記錄。</span><span class="sxs-lookup"><span data-stu-id="5a71f-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="5a71f-109">複寫類型為區域備援儲存體 (ZRS) 的儲存體帳戶目前未啟用度量或記錄功能。</span><span class="sxs-lookup"><span data-stu-id="5a71f-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have the metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="5a71f-110">如需使用儲存體分析和其他工具來識別、診斷及疑難排解 Azure 儲存體相關問題的深入指南，請參閱 [監視、診斷及疑難排解 Microsoft Azure 儲存體](../storage-monitoring-diagnosing-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="5a71f-110">For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="5a71f-111">設定儲存體帳戶的監視</span><span class="sxs-lookup"><span data-stu-id="5a71f-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="5a71f-112">在 [Azure 入口網站](https://portal.azure.com)中，選取 [儲存體帳戶]，接著選取儲存體帳戶名稱以開啟帳戶儀表板。</span><span class="sxs-lookup"><span data-stu-id="5a71f-112">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the storage account name to open the account dashboard.</span></span>
1. <span data-ttu-id="5a71f-113">在功能表刀鋒視窗的 [監視] 區段中選取 [診斷]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-113">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="5a71f-115">針對您想要監視的每個 [服務] 選取計量資料的 [類型]，並選取資料的 [保留原則]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-115">Select the **type** of metrics data for each **service** you wish to monitor, and the **retention policy** for the data.</span></span> <span data-ttu-id="5a71f-116">您也可以將 [狀態] 設定為 [關閉] 來停用監視。</span><span class="sxs-lookup"><span data-stu-id="5a71f-116">You can also disable monitoring by setting **Status** to **Off**.</span></span>

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="5a71f-118">您可以為每個服務啟用兩種類型的計量，新的儲存體帳戶預設會同時啟用這兩種類型︰</span><span class="sxs-lookup"><span data-stu-id="5a71f-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="5a71f-119">**彙總**︰收集計量，例如入口流量/出口流量、可用性、延遲和成功百分比。</span><span class="sxs-lookup"><span data-stu-id="5a71f-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="5a71f-120">系統會為 Blob、佇列、資料表和檔案服務彙總這些計量。</span><span class="sxs-lookup"><span data-stu-id="5a71f-120">These metrics are aggregated for the blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="5a71f-121">**依 API**：除了彙總計量之外，還會為 Azure 儲存體服務 API 的每個儲存體作業收集一組相同的計量。</span><span class="sxs-lookup"><span data-stu-id="5a71f-121">**Per API**: In addition to the aggregate metrics, collects the same set of metrics for each storage operation in the Azure Storage service API.</span></span>

   <span data-ttu-id="5a71f-122">若要設定資料保留原則，請移動 [保留期 (天)] 滑桿，或輸入要保留資料的天數，範圍從 1 到 365 天。</span><span class="sxs-lookup"><span data-stu-id="5a71f-122">To set the data retention policy, move the **Retention (days)** slider or enter the number of days of data to retain, from 1 to 365.</span></span> <span data-ttu-id="5a71f-123">新儲存體帳戶的預設值是 7 天。</span><span class="sxs-lookup"><span data-stu-id="5a71f-123">The default for new storage accounts is seven days.</span></span> <span data-ttu-id="5a71f-124">如果不想設定保留原則，則請輸入零。</span><span class="sxs-lookup"><span data-stu-id="5a71f-124">If you do not want to set a retention policy, enter zero.</span></span> <span data-ttu-id="5a71f-125">如果沒有保留原則，您可以決定是否刪除監視資料。</span><span class="sxs-lookup"><span data-stu-id="5a71f-125">If there is no retention policy, it is up to you to delete the monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="5a71f-126">若您以手動方式刪除計量資料，將需要付費。</span><span class="sxs-lookup"><span data-stu-id="5a71f-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="5a71f-127">過時的分析資料 (存在時間超過保留原則的資料) 則會由系統刪除，不必付費。</span><span class="sxs-lookup"><span data-stu-id="5a71f-127">Stale analytics data (data older than your retention policy) is deleted by the system at no cost.</span></span> <span data-ttu-id="5a71f-128">建議您根據要將帳戶的儲存體分析資料保留多久來設定保留原則。</span><span class="sxs-lookup"><span data-stu-id="5a71f-128">We recommend setting a retention policy based on how long you want to retain storage analytics data for your account.</span></span> <span data-ttu-id="5a71f-129">如需詳細資訊，請參閱[當您啟用儲存體度量時，會產生哪些費用？](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics)。</span><span class="sxs-lookup"><span data-stu-id="5a71f-129">See [What charges do you incur when you enable storage metrics?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="5a71f-130">監視組態完成時，選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-130">When you finish the monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="5a71f-131">[儲存體帳戶] 刀鋒視窗以及個別服務的刀鋒視窗 (Blob、佇列、資料表和檔案) 會以圖表顯示一組預設的計量。</span><span class="sxs-lookup"><span data-stu-id="5a71f-131">A default set of metrics is displayed in charts on the storage account blade, as well as the individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="5a71f-132">為服務啟用計量後，資料最慢可能需要一小時才會出現在其圖表中。</span><span class="sxs-lookup"><span data-stu-id="5a71f-132">Once you've enabled metrics for a service, it may take up to an hour for data to appear in its charts.</span></span> <span data-ttu-id="5a71f-133">您可以在任何計量圖表上選取 [編輯]，以[設定哪些計量](#how-to-customize-metrics-charts)要顯示在圖表中。</span><span class="sxs-lookup"><span data-stu-id="5a71f-133">You can select **Edit** on any metric chart to [configure which metrics](#how-to-customize-metrics-charts) are displayed in the chart.</span></span>

<span data-ttu-id="5a71f-134">您可以將 [狀態] 設定為 [關閉] 來停用計量收集和記錄。</span><span class="sxs-lookup"><span data-stu-id="5a71f-134">You can disable metrics collection and logging by setting **Status** to **Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="5a71f-135">Azure 儲存體使用[表格儲存體](../common/storage-introduction.md#table-storage)來儲存儲存體帳戶的計量，並且會將計量以資料表形式儲存在帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5a71f-135">Azure Storage uses [table storage](../common/storage-introduction.md#table-storage) to store the metrics for your storage account, and stores the metrics in tables in your account.</span></span> <span data-ttu-id="5a71f-136">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5a71f-136">For more information, see.</span></span> <span data-ttu-id="5a71f-137">[度量的儲存方式](../common/storage-analytics.md#how-metrics-are-stored)。</span><span class="sxs-lookup"><span data-stu-id="5a71f-137">[How metrics are stored](../common/storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="5a71f-138">自訂計量圖表</span><span class="sxs-lookup"><span data-stu-id="5a71f-138">Customize metrics charts</span></span>

<span data-ttu-id="5a71f-139">使用下列程序可選擇要在計量圖表中檢視哪些儲存體計量。</span><span class="sxs-lookup"><span data-stu-id="5a71f-139">Use the following procedure to choose which storage metrics to view in a metrics chart.</span></span> 

1. <span data-ttu-id="5a71f-140">一開始先在 Azure 入口網站中顯示儲存體計量圖表。</span><span class="sxs-lookup"><span data-stu-id="5a71f-140">Start by displaying a storage metric chart in the Azure portal.</span></span> <span data-ttu-id="5a71f-141">您可以在 [儲存體帳戶] 刀鋒視窗上和個別服務 (Blob、佇列、資料表及檔案) 的 [計量] 刀鋒視窗中找到圖表。</span><span class="sxs-lookup"><span data-stu-id="5a71f-141">You can find charts on the **storage account blade** and in the **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="5a71f-142">在此範例中我們使用下列圖表，而此圖表會出現在 [儲存體帳戶] 刀鋒視窗 上：</span><span class="sxs-lookup"><span data-stu-id="5a71f-142">In this example, we work with the following chart that appears on the **storage account blade**:</span></span>

   ![Azure 入口網站中的圖表選擇](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="5a71f-144">接下來，在圖表內的任意位置按一下以開啟 [計量] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5a71f-144">Next, click anywhere within the chart to open the **Metric** blade.</span></span> <span data-ttu-id="5a71f-145">選取 [編輯圖表] 以開啟 [編輯圖表] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5a71f-145">Select **Edit chart** to open the **Edit Chart** blade.</span></span>

   ![[圖表] 刀鋒視窗上的 [編輯圖表] 按鈕](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="5a71f-147">在 [編輯圖表] 刀鋒視窗上，選取要在圖表中顯示之計量的 [時間範圍]，以及想要顯示其計量的 [服務] \(Blob、佇列、資料表、檔案)。</span><span class="sxs-lookup"><span data-stu-id="5a71f-147">On the **Edit Chart** blade, select the **Time Range** of the metrics to display in the chart, and the **service** (blob, queue, table, file) whose metrics you wish to display.</span></span> <span data-ttu-id="5a71f-148">這裡我們選擇要顯示 Blob 服務過去一週的計量︰</span><span class="sxs-lookup"><span data-stu-id="5a71f-148">Here we've selected to display the past week's metrics for the blob service:</span></span>

   ![[編輯圖表] 刀鋒視窗中的時間範圍和服務選擇](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="5a71f-150">選取要在圖表中顯示的個別 [計量]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-150">Select the individual **metrics** you'd like displayed in the chart, then click **OK**.</span></span> <span data-ttu-id="5a71f-151">例如，這裡我們選擇了要顯示 [ContainerCount] 和 [ObjectCount] 計量︰</span><span class="sxs-lookup"><span data-stu-id="5a71f-151">For example, here we've chosen to display the *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![[編輯圖表] 刀鋒視窗中的個別計量選擇](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="5a71f-153">圖表設定不會影響儲存體帳戶之監視資料的收集、彙總或儲存，只會影響計量資料的檢視。</span><span class="sxs-lookup"><span data-stu-id="5a71f-153">Your chart settings do not affect the collection, aggregation, or storage of monitoring data in the storage account, only the viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="5a71f-154">計量在圖表中的可用性</span><span class="sxs-lookup"><span data-stu-id="5a71f-154">Metrics availability in charts</span></span>

<span data-ttu-id="5a71f-155">可用計量清單會根據您在下拉式功能表中所選擇的服務以及您正在編輯之圖表的單位類型而有所變更。</span><span class="sxs-lookup"><span data-stu-id="5a71f-155">The list of available metrics changes based on which service you've chosen in the drop-down, and the unit type of the chart you're editing.</span></span> <span data-ttu-id="5a71f-156">例如，只有在編輯以百分比顯示單位的圖表時，才能選取百分比計量，例如 PercentNetworkError 和 PercentThrottlingError︰</span><span class="sxs-lookup"><span data-stu-id="5a71f-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![Azure 入口網站中的要求錯誤百分比圖表](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="5a71f-158">計量解析</span><span class="sxs-lookup"><span data-stu-id="5a71f-158">Metrics resolution</span></span>

<span data-ttu-id="5a71f-159">您在 [診斷] 中選取的計量會決定帳戶可用計量的解析︰</span><span class="sxs-lookup"><span data-stu-id="5a71f-159">The metrics you selected in Diagnostics determines the resolution of the metrics that are available for your account:</span></span>

* <span data-ttu-id="5a71f-160">**彙總**監視會提供入口流量/出口流量、可用性、延遲和成功百分比等計量。</span><span class="sxs-lookup"><span data-stu-id="5a71f-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="5a71f-161">這些計量是從 Blob、資料表、檔案和佇列服務彙總而來。</span><span class="sxs-lookup"><span data-stu-id="5a71f-161">These metrics are aggregated from the blob, table, file, and queue services.</span></span>
* <span data-ttu-id="5a71f-162">**依 API** 會提供更精細的解析，除了服務層級的彙總外，還能呈現個別儲存體作業可用的計量。</span><span class="sxs-lookup"><span data-stu-id="5a71f-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition to the service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="5a71f-163">設定計量警示</span><span class="sxs-lookup"><span data-stu-id="5a71f-163">Configure metrics alerts</span></span>

<span data-ttu-id="5a71f-164">您可以建立警示，以在儲存體資源計量達到閾值時通知您。</span><span class="sxs-lookup"><span data-stu-id="5a71f-164">You can create alerts to notify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="5a71f-165">若要開啟 [警示規則] 刀鋒視窗，請向下捲動至 [功能表] 刀鋒視窗的 [監視] 區段，然後選取 [警示規則]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-165">To open the **Alert rules blade**, scroll down to the **MONITORING** section of the **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="5a71f-166">選取 [新增警示] 以開啟 [新增警示規則] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="5a71f-166">Select **Add alert** to open the **Add an alert rule** blade</span></span>
1. <span data-ttu-id="5a71f-167">從下拉式清單中選取 [資源] \(Blob、檔案、佇列、資料表)，然後輸入新警示規則的 [名稱] 和 [描述]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-167">Select a **Resource** (blob, file, queue, table) from the drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="5a71f-168">選取要為其新增警示的 [計量]、警示 [條件] 和 [閾值]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-168">Select the **Metric** for which you'd like to add an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="5a71f-169">閾值的單位類型會隨您所選擇的計量而變更。</span><span class="sxs-lookup"><span data-stu-id="5a71f-169">The threshold unit type changes depending on the metric you've chosen.</span></span> <span data-ttu-id="5a71f-170">例如，「計數」是 ContainerCount 的單位類型，PercentNetworkError 計量的單位則是百分比。</span><span class="sxs-lookup"><span data-stu-id="5a71f-170">For example, "count" is the unit type for *ContainerCount*, while the unit for the *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="5a71f-171">選取 [期間]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-171">Select the **Period**.</span></span> <span data-ttu-id="5a71f-172">在期間內達到或超過閾值的計量會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="5a71f-172">Metrics that reach or exceed the Threshold within the period trigger an alert.</span></span>
1. <span data-ttu-id="5a71f-173">(選擇性) 設定 [電子郵件] 和 [Webhook] 通知。</span><span class="sxs-lookup"><span data-stu-id="5a71f-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="5a71f-174">如需 Webhook 的詳細資訊，請參閱[針對 Azure 度量警示設定 Webhook](../../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="5a71f-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="5a71f-175">如果未設定電子郵件或 Webhook 通知，則警示只會出現在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5a71f-175">If you do not configure email or webhook notifications, alerts will appear only in the Azure portal.</span></span>

![Azure 入口網站中的 [新增警示規則] 刀鋒視窗](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-to-the-portal-dashboard"></a><span data-ttu-id="5a71f-177">在入口網站儀表板中新增計量圖表</span><span class="sxs-lookup"><span data-stu-id="5a71f-177">Add metrics charts to the portal dashboard</span></span>

<span data-ttu-id="5a71f-178">您可以在入口網站儀表板中新增任何儲存體帳戶的 Azure 儲存體計量圖表。</span><span class="sxs-lookup"><span data-stu-id="5a71f-178">You can add Azure Storage metrics charts for any of your storage accounts to your portal dashboard.</span></span>

1. <span data-ttu-id="5a71f-179">在 [Azure 入口網站](https://portal.azure.com)中檢視儀表板時按一下 [編輯儀表板]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-179">Select click **Edit dashboard** while viewing your dashboard in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="5a71f-180">在 [圖格庫] 中，選取 [圖格尋找依據] > [類型]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-180">In the **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="5a71f-181">選取 [類型] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="5a71f-182">在 [資源] 中，選取您想要在儀表板中新增其計量的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a71f-182">In **Resources**, select the storage account whose metrics you wish to add to the dashboard.</span></span>
1. <span data-ttu-id="5a71f-183">選取 [類別] > [監視]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="5a71f-184">將想要顯示之計量的圖表圖格拖放到儀表板。</span><span class="sxs-lookup"><span data-stu-id="5a71f-184">Drag-and-drop the chart tile onto your dashboard for the metric you'd like displayed.</span></span> <span data-ttu-id="5a71f-185">針對想要顯示在儀表板上的所有計量重複此操作。</span><span class="sxs-lookup"><span data-stu-id="5a71f-185">Repeat for all metrics you'd like displayed on the dashboard.</span></span> <span data-ttu-id="5a71f-186">下圖醒目提示「Blob - 要求總數」圖表來做為範例，但所有圖表都可放置在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="5a71f-186">In the following image, the "Blobs - Total requests" chart is highlighted as an example, but all the charts are available for placement on your dashboard.</span></span>

   ![Azure 入口網站中的圖格庫](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="5a71f-188">新增完圖表時，請選取儀表板頂端附近的 [自訂完成]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-188">Select **Done customizing** near the top of the dashboard when you're done adding charts.</span></span>

<span data-ttu-id="5a71f-189">在儀表板中新增圖表後，您可以進一步自訂這些圖表，如[自訂計量圖表](#how-to-customize-metrics-charts)所述。</span><span class="sxs-lookup"><span data-stu-id="5a71f-189">Once you've added charts to your dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="5a71f-190">設定記錄</span><span class="sxs-lookup"><span data-stu-id="5a71f-190">Configure logging</span></span>

<span data-ttu-id="5a71f-191">您可以指示 Azure 儲存體，讓它將 Blob、資料表和佇列服務之讀取、寫入及刪除要求的診斷記錄儲存起來。</span><span class="sxs-lookup"><span data-stu-id="5a71f-191">You can instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services.</span></span> <span data-ttu-id="5a71f-192">您已設定的資料保留原則同樣適用於這些記錄。</span><span class="sxs-lookup"><span data-stu-id="5a71f-192">The data retention policy you set also applies to these logs.</span></span>

> [!NOTE]
> <span data-ttu-id="5a71f-193">Azure 檔案儲存體目前支援儲存體分析度量，但還不支援記錄。</span><span class="sxs-lookup"><span data-stu-id="5a71f-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="5a71f-194">在 [Azure 入口網站](https://portal.azure.com)中，選取 [儲存體帳戶]，然後選取儲存體帳戶名稱以開啟 [儲存體帳戶] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5a71f-194">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the name of the storage account to open the storage account blade.</span></span>
1. <span data-ttu-id="5a71f-195">在功能表刀鋒視窗的 [監視] 區段中選取 [診斷]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-195">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Azure 入口網站中 [監視] 底下的 [診斷] 功能表項目。](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="5a71f-197">確定 [狀態] 已設為 [開啟]，然後選取要為其啟用記錄的 [服務]。</span><span class="sxs-lookup"><span data-stu-id="5a71f-197">Ensure **Status** is set to **On**, and select the **services** for which you'd like to enable logging.</span></span>

    ![在 Azure 入口網站中設定記錄。](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="5a71f-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5a71f-199">Click **Save**.</span></span>

<span data-ttu-id="5a71f-200">診斷記錄檔儲存在儲存體帳戶中的 $logs Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5a71f-200">The diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="5a71f-201">若要檢視記錄資料，您可以使用 [Microsoft 儲存體總管](http://storageexplorer.com)之類的儲存體總管，或使用儲存體用戶端程式庫或 PowerShell 以程式設計方式進行檢視。</span><span class="sxs-lookup"><span data-stu-id="5a71f-201">You can view the log data using a storage explorer like the [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using the storage client library or PowerShell.</span></span>

<span data-ttu-id="5a71f-202">如需存取 $logs 容器的相關資訊，請參閱[啟用儲存體記錄和存取記錄檔資料](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data)。</span><span class="sxs-lookup"><span data-stu-id="5a71f-202">For information about accessing the $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a71f-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a71f-203">Next steps</span></span>

* <span data-ttu-id="5a71f-204">尋找更多關於儲存體分析之[計量、記錄和帳單](../storage-analytics.md)的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5a71f-204">Find more details about [metrics, logging, and billing](../storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="5a71f-205">使用 PowerShell 和程式設計方式 (利用 C#) [啟用 Azure 儲存體計量和檢視計量資料](../storage-enable-and-view-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="5a71f-205">[Enable Azure Storage metrics and view metrics data](../storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>
