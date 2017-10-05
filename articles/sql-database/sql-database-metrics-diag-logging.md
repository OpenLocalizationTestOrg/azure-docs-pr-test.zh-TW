---
title: "Azure SQL Database 計量和診斷記錄 | Microsoft Docs"
description: "了解如何設定 Azure SQL Database 資源，以儲存資源使用量、連線及查詢執行統計資料。"
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: bf41aa530c68ea0e94a09d1dab63237c6f42bce7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="51bf9-103">Azure SQL Database 計量和診斷記錄</span><span class="sxs-lookup"><span data-stu-id="51bf9-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="51bf9-104">Azure SQL Database 可以發出計量和診斷記錄，以便進行監視。</span><span class="sxs-lookup"><span data-stu-id="51bf9-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="51bf9-105">您可以將 Azure SQL Database 設定為將資源使用量、背景工作與工作階段及連線儲存到下列其中一項 Azure 資源：</span><span class="sxs-lookup"><span data-stu-id="51bf9-105">You can configure Azure SQL Database to store resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="51bf9-106">**Azure 儲存體**：用於封存大量遙測資料，價格低廉</span><span class="sxs-lookup"><span data-stu-id="51bf9-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="51bf9-107">**Azure 事件中樞**：用於整合 Azure SQL Database 遙測與自訂監視解決方案或管線</span><span class="sxs-lookup"><span data-stu-id="51bf9-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="51bf9-108">**Azure Log Analytics**：適用於具有報告、警示及緩和功能的現成監視解決方案</span><span class="sxs-lookup"><span data-stu-id="51bf9-108">**Azure Log Analytics**: For out of the box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![架構](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="51bf9-110">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="51bf9-110">Enable logging</span></span>

<span data-ttu-id="51bf9-111">預設未啟用計量和診斷記錄功能。</span><span class="sxs-lookup"><span data-stu-id="51bf9-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="51bf9-112">您可以使用下列其中一種方法來啟用及管理計量和診斷記錄功能︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-112">You can enable and manage metrics and diagnostics logging using one of the following methods:</span></span>
- <span data-ttu-id="51bf9-113">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="51bf9-113">Azure portal</span></span>
- <span data-ttu-id="51bf9-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51bf9-114">PowerShell</span></span>
- <span data-ttu-id="51bf9-115">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="51bf9-115">Azure CLI</span></span>
- <span data-ttu-id="51bf9-116">REST API</span><span class="sxs-lookup"><span data-stu-id="51bf9-116">REST API</span></span> 
- <span data-ttu-id="51bf9-117">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="51bf9-117">Resource Manager template</span></span>

<span data-ttu-id="51bf9-118">當您啟用計量和診斷記錄功能時，您必須指定要收集所選資料的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="51bf9-118">When you enable metrics and diagnostics logging, you need to specify the Azure resource where selected data is collected.</span></span> <span data-ttu-id="51bf9-119">可用的選項︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-119">Options available:</span></span>
- <span data-ttu-id="51bf9-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="51bf9-120">Log analytics</span></span>
- <span data-ttu-id="51bf9-121">事件中樞</span><span class="sxs-lookup"><span data-stu-id="51bf9-121">Event Hub</span></span>
- <span data-ttu-id="51bf9-122">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="51bf9-122">Azure Storage</span></span> 

<span data-ttu-id="51bf9-123">您可以佈建新的 Azure 資源，或選取現有的資源。</span><span class="sxs-lookup"><span data-stu-id="51bf9-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="51bf9-124">選取儲存體資源之後，您需要指定要收集的資料。</span><span class="sxs-lookup"><span data-stu-id="51bf9-124">After selecting the storage resource, you need to specify which data to collect.</span></span> <span data-ttu-id="51bf9-125">可用的選項包括︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-125">Options available include:</span></span>

- <span data-ttu-id="51bf9-126">**[1 分鐘的計量](sql-database-metrics-diag-logging.md#1-minute-metrics)** - 包含 DTU 百分比、DTU 限制、CPU 百分比、實體資料讀取百分比、記錄寫入百分比、成功/失敗/防火牆封鎖的連線、工作階段百分比、背景工作百分比、儲存體、儲存體百分比、XTP 儲存體百分比</span><span class="sxs-lookup"><span data-stu-id="51bf9-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="51bf9-127">如果您指定事件中樞或 Azure 儲存體帳戶，您可指定保留原則，以指定刪除早於所選期間的資料。</span><span class="sxs-lookup"><span data-stu-id="51bf9-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy to specify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="51bf9-128">如果您指定 Log Analytics，則保留原則取決於所選的定價層。</span><span class="sxs-lookup"><span data-stu-id="51bf9-128">If you specify Log Analytics, the retention policy depends on the selected pricing tier.</span></span> <span data-ttu-id="51bf9-129">深入了解 [Log Analytics 價格](https://azure.microsoft.com/pricing/details/log-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="51bf9-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="51bf9-130">建議您閱讀 [Microsoft Azure 中的計量概觀](../monitoring-and-diagnostics/monitoring-overview-metrics.md)和 [Azure 診斷記錄概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)文章，以了解如何啟用記錄和各種 Azure 服務支援的計量和記錄類別。</span><span class="sxs-lookup"><span data-stu-id="51bf9-130">We recommend that you read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="51bf9-131">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="51bf9-131">Azure portal</span></span>

<span data-ttu-id="51bf9-132">若要在 Azure 入口網站中啟用計量和診斷記錄收集功能，請瀏覽至您的 Azure SQL 資料庫或彈性集區頁面，然後按一下 [診斷設定]。</span><span class="sxs-lookup"><span data-stu-id="51bf9-132">To enable metrics and diagnostic logs collection in the Azure portal, navigate to your Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![在 Azure 入口網站中啟用](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="51bf9-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="51bf9-134">PowerShell</span></span>

<span data-ttu-id="51bf9-135">若要使用 Powershell 啟用計量和診斷記錄功能，請使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="51bf9-135">To enable metrics and diagnostics logging using PowerShell, use the following commands:</span></span>

- <span data-ttu-id="51bf9-136">若要啟用儲存體帳戶中的診斷記錄檔的儲存體，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-136">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="51bf9-137">儲存體帳戶識別碼是您要將記錄檔傳送至此的儲存體帳戶的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="51bf9-137">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="51bf9-138">若要啟用將診斷記錄檔串流至事件中樞，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-138">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="51bf9-139">服務匯流排規則識別碼是此格式的字串︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-139">The Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="51bf9-140">若要啟用將診斷記錄檔傳送到 Log Analytics 工作區，請使用此命令︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-140">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="51bf9-141">您可以使用下列命令取得 Log Analytics 工作區的資源識別碼︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-141">You can obtain the resource id of your Log Analytics workspace using the following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="51bf9-142">您可以結合這些參數讓多個輸出選項。</span><span class="sxs-lookup"><span data-stu-id="51bf9-142">You can combine these parameters to enable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="51bf9-143">CLI</span><span class="sxs-lookup"><span data-stu-id="51bf9-143">CLI</span></span>

<span data-ttu-id="51bf9-144">若要使用 Azure CLI 啟用計量和診斷記錄功能，請使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="51bf9-144">To enable metrics and diagnostics logging using the Azure CLI, use the following commands:</span></span>

- <span data-ttu-id="51bf9-145">若要啟用儲存體帳戶中的診斷記錄檔的儲存體，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-145">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="51bf9-146">儲存體帳戶識別碼是您要將記錄檔傳送至此的儲存體帳戶的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="51bf9-146">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="51bf9-147">若要啟用將診斷記錄檔串流至事件中樞，使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-147">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="51bf9-148">服務匯流排規則識別碼是此格式的字串︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-148">The Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="51bf9-149">若要啟用將診斷記錄檔傳送到 Log Analytics 工作區，請使用此命令︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-149">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

<span data-ttu-id="51bf9-150">您可以結合這些參數讓多個輸出選項。</span><span class="sxs-lookup"><span data-stu-id="51bf9-150">You can combine these parameters to enable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="51bf9-151">REST API</span><span class="sxs-lookup"><span data-stu-id="51bf9-151">REST API</span></span>

<span data-ttu-id="51bf9-152">了解如何[使用 Azure 監視器 REST API 變更診斷設定](https://msdn.microsoft.com/library/azure/dn931931.aspx)。</span><span class="sxs-lookup"><span data-stu-id="51bf9-152">Read about how to [change Diagnostic settings using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="51bf9-153">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="51bf9-153">Resource Manager template</span></span>

<span data-ttu-id="51bf9-154">了解如何[使用 Resource Manager 範本在建立資源時啟用診斷設定](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md)。</span><span class="sxs-lookup"><span data-stu-id="51bf9-154">Read about how to [enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="51bf9-155">串流到 Log Analytics 中</span><span class="sxs-lookup"><span data-stu-id="51bf9-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="51bf9-156">使用 Azure 入口網站中內建的「傳送到 Log Analytics」選項，或透過 Azure PowerShell Cmdlet、Azure CLI 或 Azure 監視器 REST API 在診斷設定中啟用 Log Analytics，即可將 Azure SQL Database 計量和診斷記錄串流到 Log Analytics 中。</span><span class="sxs-lookup"><span data-stu-id="51bf9-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using the built-in “Send to Log Analytics” option in the portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="51bf9-157">安裝概觀</span><span class="sxs-lookup"><span data-stu-id="51bf9-157">Installation overview</span></span>

<span data-ttu-id="51bf9-158">透過 Log Analytics 可以輕易監視 Azure SQL Database Fleet。</span><span class="sxs-lookup"><span data-stu-id="51bf9-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="51bf9-159">需要三個步驟：</span><span class="sxs-lookup"><span data-stu-id="51bf9-159">Three steps are required:</span></span>

1.  <span data-ttu-id="51bf9-160">建立 Log Analytics 資源</span><span class="sxs-lookup"><span data-stu-id="51bf9-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="51bf9-161">將資料庫設定為將計量和診斷記錄記錄到已建立的 Log Analytics 中</span><span class="sxs-lookup"><span data-stu-id="51bf9-161">Configure databases to record metrics and diagnostic logs into the created Log Analytics</span></span>
3.  <span data-ttu-id="51bf9-162">在 Log Analytics 中從資源庫安裝 **Azure SQL 分析**解決方案</span><span class="sxs-lookup"><span data-stu-id="51bf9-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="51bf9-163">建立 Log Analytics 資源</span><span class="sxs-lookup"><span data-stu-id="51bf9-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="51bf9-164">按一下左側功能表中的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="51bf9-164">Click **New** in the left-hand menu.</span></span>
2. <span data-ttu-id="51bf9-165">按一下 [監視 + 管理]</span><span class="sxs-lookup"><span data-stu-id="51bf9-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="51bf9-166">按一下 [Log Analytics]</span><span class="sxs-lookup"><span data-stu-id="51bf9-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="51bf9-167">在 Log Analytics 表單中填入所需的其他資訊：工作區名稱、訂用帳戶、資源群組、位置及定價層。</span><span class="sxs-lookup"><span data-stu-id="51bf9-167">Fill in the Log Analytics form with the additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-to-record-metrics-and-diagnostic-logs"></a><span data-ttu-id="51bf9-169">將資料庫設定為記錄計量和診斷記錄</span><span class="sxs-lookup"><span data-stu-id="51bf9-169">Configure databases to record metrics and diagnostic logs</span></span>

<span data-ttu-id="51bf9-170">若要設定資料庫記錄其計量的位置，最簡單的方法就是透過 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="51bf9-170">The easiest way to configure where databases record their metrics is through the Azure portal.</span></span> <span data-ttu-id="51bf9-171">在 Azure 入口網站中，瀏覽至您的 Azure SQL Database 資源，然後按一下 [診斷設定]。</span><span class="sxs-lookup"><span data-stu-id="51bf9-171">In the Azure portal, navigate to your Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-the-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="51bf9-172">從資源庫安裝 Azure SQL 分析解決方案</span><span class="sxs-lookup"><span data-stu-id="51bf9-172">Install the Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="51bf9-173">一旦建立 Log Analytics 資源，您的資料會流入其中，請安裝 Azure SQL 分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="51bf9-173">Once the Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="51bf9-174">這可以透過**解決方案資源庫**完成，您可以在 OMS 首頁上和側邊功能表中找到該資源庫。</span><span class="sxs-lookup"><span data-stu-id="51bf9-174">This can be done through the **Solutions Gallery** that you can find on the OMS homepage and in the side menu.</span></span> <span data-ttu-id="51bf9-175">在資源庫中，尋找並按一下 [Azure SQL 分析] 解決方案，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="51bf9-175">In the gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![監視解決方案](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="51bf9-177">您的 OMS 首頁上隨即出現名為 [Azure SQL 分析] 的新圖格。</span><span class="sxs-lookup"><span data-stu-id="51bf9-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="51bf9-178">選取此圖格可開啟 [Azure SQL 分析] 儀表板。</span><span class="sxs-lookup"><span data-stu-id="51bf9-178">Selecting this tile opens the Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="51bf9-179">使用 Azure SQL 分析解決方案</span><span class="sxs-lookup"><span data-stu-id="51bf9-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="51bf9-180">Azure SQL 分析是一個階層式儀表板，可讓您瀏覽 Azure SQL Database 資源階層。</span><span class="sxs-lookup"><span data-stu-id="51bf9-180">Azure SQL Analytics is a hierarchical dashboard that allows you to navigate through the hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="51bf9-181">這項功能可讓您執行高階監視，但也可讓您將監視範圍設定為適當的資源集合。</span><span class="sxs-lookup"><span data-stu-id="51bf9-181">This capability enables you to do high-level monitoring but it also enables you to scope your monitoring to just the right set of resources.</span></span>
<span data-ttu-id="51bf9-182">儀表板在所選的資源之下包含不同的資源清單。</span><span class="sxs-lookup"><span data-stu-id="51bf9-182">Dashboard contains the lists of different resources under the selected resource.</span></span> <span data-ttu-id="51bf9-183">例如，對於所選的訂用帳戶，您可以看到屬於所選訂用帳戶的所有伺服器、彈性集區和資料庫。</span><span class="sxs-lookup"><span data-stu-id="51bf9-183">For example, for a selected subscription you can see the all servers, elastic pools and databases that belong to the selected subscription.</span></span> <span data-ttu-id="51bf9-184">此外，對於彈性集區和資料庫，您可以看到該資源的資源使用量計量。</span><span class="sxs-lookup"><span data-stu-id="51bf9-184">Additionally, for Elastic Pools and databases, you can see the resource usage metrics of that resource.</span></span> <span data-ttu-id="51bf9-185">這包括 DTU、CPU、IO、LOG、工作階段、背景工作、連線和儲存體 (以 GB 為單位) 的圖表。</span><span class="sxs-lookup"><span data-stu-id="51bf9-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="51bf9-186">串流到 Azure 事件中樞中</span><span class="sxs-lookup"><span data-stu-id="51bf9-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="51bf9-187">使用 Azure 入口網站中內建的「串流到事件中樞」選項，或透過 Azure PowerShell Cmdlet、Azure CLI 或 Azure 監視器 REST API 在診斷設定中啟用服務匯流排規則，即可將 Azure SQL Database 計量和診斷記錄串流到事件中樞中。</span><span class="sxs-lookup"><span data-stu-id="51bf9-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using the built-in “Stream to an event hub” option in the portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-to-do-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="51bf9-188">如何在事件中樞處理計量和診斷記錄？</span><span class="sxs-lookup"><span data-stu-id="51bf9-188">What to do with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="51bf9-189">一旦所選的資料串流到事件中樞，您很快就能啟用進階監視案例。</span><span class="sxs-lookup"><span data-stu-id="51bf9-189">Once the selected data is streamed into Event Hub, you are one step closer to enabling advanced monitoring scenarios.</span></span> <span data-ttu-id="51bf9-190">事件中樞能做為事件管線的「大門」，一旦收集的資料進入事件中樞，它可以使用任何即時分析提供者或批次/儲存配接器轉換及儲存資料。</span><span class="sxs-lookup"><span data-stu-id="51bf9-190">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="51bf9-191">事件中樞能分隔事件串流的生產與這些事件的使用，讓事件消費者依照自己的排程存取事件。</span><span class="sxs-lookup"><span data-stu-id="51bf9-191">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span> <span data-ttu-id="51bf9-192">如需事件中樞的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="51bf9-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="51bf9-193">[Azure 事件中樞是什麼](../event-hubs/event-hubs-what-is-event-hubs.md)？</span><span class="sxs-lookup"><span data-stu-id="51bf9-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="51bf9-194">開始使用事件中樞</span><span class="sxs-lookup"><span data-stu-id="51bf9-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="51bf9-195">這裡有一些您可以使用串流功能的方法：</span><span class="sxs-lookup"><span data-stu-id="51bf9-195">Here are just a few ways you might use the streaming capability:</span></span>

-   <span data-ttu-id="51bf9-196">透過將「最忙碌路徑」串流至 PowerBI 以檢視服務健康情況 – 您可以使用事件中樞、串流分析和 PowerBI，輕鬆快速地將計量和診斷資料轉換為 Azure 服務上的深入解析。</span><span class="sxs-lookup"><span data-stu-id="51bf9-196">View service health by streaming “hot path” data to PowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="51bf9-197">如需如何設定事件中樞、使用串流分析處理資料，以及使用 PowerBI 作為輸出的概觀，請參閱[串流分析和 Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="51bf9-197">For an overview of how to set up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="51bf9-198">將記錄串流至第三方記錄和遙測資料流 – 使用事件中樞串流，您可以將計量和診斷記錄放入不同的第三方監視和記錄分析解決方案中。</span><span class="sxs-lookup"><span data-stu-id="51bf9-198">Stream logs to third-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in to different third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="51bf9-199">建置自訂遙測及記錄平台 – 如果您已有自建遙測平台或正好在考慮建置一個，事件中樞所具備的高度可調整的發佈訂閱特質可讓您靈活擷取診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="51bf9-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="51bf9-200">請參閱 [Dan Rosanova 指南，以在全球級別的遙測平台中使用事件中樞](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)。</span><span class="sxs-lookup"><span data-stu-id="51bf9-200">See [Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="51bf9-201">串流到 Azure 儲存體中</span><span class="sxs-lookup"><span data-stu-id="51bf9-201">Stream into Azure Storage</span></span>

<span data-ttu-id="51bf9-202">使用 Azure 入口網站中內建的「封存到儲存體帳戶」選項，或透過 Azure PowerShell Cmdlet、Azure CLI 或 Azure 監視器 REST API 在診斷設定中啟用 Azure 儲存體，即可將 Azure SQL Database 計量和診斷記錄儲存到 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="51bf9-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using the built-in "Archive to a storage account” option in the Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="51bf9-203">儲存體帳戶中的計量和診斷記錄結構描述</span><span class="sxs-lookup"><span data-stu-id="51bf9-203">Schema of metrics and diagnostic logs in the storage account</span></span>

<span data-ttu-id="51bf9-204">設定計量和診斷記錄集合後，當第一批資料列可用時，系統會在您選取的儲存體帳戶中建立儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="51bf9-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in the storage account you selected when the first rows of data are available.</span></span> <span data-ttu-id="51bf9-205">這些 blob 的結構為：</span><span class="sxs-lookup"><span data-stu-id="51bf9-205">The structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="51bf9-206">或者，形式更簡單：</span><span class="sxs-lookup"><span data-stu-id="51bf9-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="51bf9-207">例如，1 分鐘計量的 blob 名稱可能是︰</span><span class="sxs-lookup"><span data-stu-id="51bf9-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="51bf9-208">如果您想要記錄彈性集區中的資料，blob 名稱會有點不同：</span><span class="sxs-lookup"><span data-stu-id="51bf9-208">In case you want to record the data from the Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="51bf9-209">從 Azure 儲存體下載計量和記錄</span><span class="sxs-lookup"><span data-stu-id="51bf9-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="51bf9-210">請參閱[從 Azure 儲存體下載計量和診斷記錄](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="51bf9-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="51bf9-211">1 分鐘計量</span><span class="sxs-lookup"><span data-stu-id="51bf9-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="51bf9-212">**Resource**</span><span class="sxs-lookup"><span data-stu-id="51bf9-212">**Resource**</span></span>|<span data-ttu-id="51bf9-213">**計量**</span><span class="sxs-lookup"><span data-stu-id="51bf9-213">**Metrics**</span></span>|
|<span data-ttu-id="51bf9-214">資料庫</span><span class="sxs-lookup"><span data-stu-id="51bf9-214">Database</span></span>|<span data-ttu-id="51bf9-215">DTU 百分比、使用的 DTU、DTU 限制、CPU 百分比、實體資料讀取百分比、記錄寫入百分比、成功/失敗/防火牆封鎖的連線、工作階段百分比、背景工作百分比、儲存體、儲存體百分比、XTP 儲存體百分比、死結</span><span class="sxs-lookup"><span data-stu-id="51bf9-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="51bf9-216">彈性集區</span><span class="sxs-lookup"><span data-stu-id="51bf9-216">Elastic pool</span></span>|<span data-ttu-id="51bf9-217">eDTU 百分比、使用的 eDTU、eDTU 限制、CPU 百分比、實體資料讀取百分比、記錄寫入百分比、工作階段百分比、背景工作百分比、儲存體、儲存體百分比、儲存體限制、XTP 儲存體百分比</span><span class="sxs-lookup"><span data-stu-id="51bf9-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="51bf9-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51bf9-218">Next steps</span></span>

- <span data-ttu-id="51bf9-219">閱讀 [Microsoft Azure 中的計量概觀](../monitoring-and-diagnostics/monitoring-overview-metrics.md)和 [Azure 診斷記錄概觀](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)文章，以了解如何啟用記錄和各種 Azure 服務支援的計量和記錄類別。</span><span class="sxs-lookup"><span data-stu-id="51bf9-219">Read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>
- <span data-ttu-id="51bf9-220">閱讀下列文章來了解事件中樞：</span><span class="sxs-lookup"><span data-stu-id="51bf9-220">Read these articles to learn about event hubs:</span></span>
   - <span data-ttu-id="51bf9-221">[Azure 事件中樞是什麼](../event-hubs/event-hubs-what-is-event-hubs.md)？</span><span class="sxs-lookup"><span data-stu-id="51bf9-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="51bf9-222">開始使用事件中樞</span><span class="sxs-lookup"><span data-stu-id="51bf9-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="51bf9-223">請參閱[從 Azure 儲存體下載計量和診斷記錄](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="51bf9-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
