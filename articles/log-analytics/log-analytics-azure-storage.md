---
title: "aaaCollect Azure 記錄分析服務記錄檔和度量 |Microsoft 文件"
description: "在 Azure 資源 toowrite 記錄檔和度量 tooLog 分析設定診斷功能。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a><span data-ttu-id="56cef-103">收集 Azure 服務的記錄和計量以便使用於 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="56cef-103">Collect Azure service logs and metrics for use in Log Analytics</span></span>

<span data-ttu-id="56cef-104">有四種不同的方式可收集 Azure 服務的記錄和度量︰</span><span class="sxs-lookup"><span data-stu-id="56cef-104">There are four different ways of collecting logs and metrics for Azure services:</span></span>

1. <span data-ttu-id="56cef-105">Azure 診斷直接 tooLog 分析 (*診斷*hello 下表中)</span><span class="sxs-lookup"><span data-stu-id="56cef-105">Azure diagnostics direct tooLog Analytics (*Diagnostics* in hello following table)</span></span>
2. <span data-ttu-id="56cef-106">Azure 診斷 tooAzure 儲存體 tooLog 分析 (*儲存體*hello 下表中)</span><span class="sxs-lookup"><span data-stu-id="56cef-106">Azure diagnostics tooAzure storage tooLog Analytics (*Storage* in hello following table)</span></span>
3. <span data-ttu-id="56cef-107">Azure 服務的連接器 (*連接器*hello 下表中)</span><span class="sxs-lookup"><span data-stu-id="56cef-107">Connectors for Azure services (*Connectors* in hello following table)</span></span>
4. <span data-ttu-id="56cef-108">和編寫指令碼 toocollect 然後張貼資料到記錄分析 （空白下表中的 hello 和未列出的服務）</span><span class="sxs-lookup"><span data-stu-id="56cef-108">Scripts toocollect and then post data into Log Analytics (blanks in hello following table and for services that are not listed)</span></span>


| <span data-ttu-id="56cef-109">服務</span><span class="sxs-lookup"><span data-stu-id="56cef-109">Service</span></span>                 | <span data-ttu-id="56cef-110">資源類型</span><span class="sxs-lookup"><span data-stu-id="56cef-110">Resource Type</span></span>                           | <span data-ttu-id="56cef-111">記錄檔</span><span class="sxs-lookup"><span data-stu-id="56cef-111">Logs</span></span>        | <span data-ttu-id="56cef-112">度量</span><span class="sxs-lookup"><span data-stu-id="56cef-112">Metrics</span></span>     | <span data-ttu-id="56cef-113">方案</span><span class="sxs-lookup"><span data-stu-id="56cef-113">Solution</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="56cef-114">應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="56cef-114">Application gateways</span></span>    | <span data-ttu-id="56cef-115">Microsoft.Network/applicationGateways</span><span class="sxs-lookup"><span data-stu-id="56cef-115">Microsoft.Network/applicationGateways</span></span>   | <span data-ttu-id="56cef-116">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-116">Diagnostics</span></span> | <span data-ttu-id="56cef-117">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-117">Diagnostics</span></span> | [<span data-ttu-id="56cef-118">Azure 應用程式閘道分析</span><span class="sxs-lookup"><span data-stu-id="56cef-118">Azure Application Gateway Analytics</span></span>](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| <span data-ttu-id="56cef-119">Application insights</span><span class="sxs-lookup"><span data-stu-id="56cef-119">Application insights</span></span>    |                                         | <span data-ttu-id="56cef-120">連接器</span><span class="sxs-lookup"><span data-stu-id="56cef-120">Connector</span></span>   | <span data-ttu-id="56cef-121">連接器</span><span class="sxs-lookup"><span data-stu-id="56cef-121">Connector</span></span>   | <span data-ttu-id="56cef-122">[Application Insights Connector (Application Insights 連接器)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (預覽)</span><span class="sxs-lookup"><span data-stu-id="56cef-122">[Application Insights Connector](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (Preview)</span></span> |
| <span data-ttu-id="56cef-123">自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="56cef-123">Automation accounts</span></span>     | <span data-ttu-id="56cef-124">Microsoft.Automation/AutomationAccounts</span><span class="sxs-lookup"><span data-stu-id="56cef-124">Microsoft.Automation/AutomationAccounts</span></span> | <span data-ttu-id="56cef-125">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-125">Diagnostics</span></span> |             | [<span data-ttu-id="56cef-126">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="56cef-126">More information</span></span>](../automation/automation-manage-send-joblogs-log-analytics.md)|
| <span data-ttu-id="56cef-127">Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="56cef-127">Batch accounts</span></span>          | <span data-ttu-id="56cef-128">Microsoft.Batch/batchAccounts</span><span class="sxs-lookup"><span data-stu-id="56cef-128">Microsoft.Batch/batchAccounts</span></span>           | <span data-ttu-id="56cef-129">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-129">Diagnostics</span></span> | <span data-ttu-id="56cef-130">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-130">Diagnostics</span></span> | |
| <span data-ttu-id="56cef-131">傳統雲端服務</span><span class="sxs-lookup"><span data-stu-id="56cef-131">Classic cloud services</span></span>  |                                         | <span data-ttu-id="56cef-132">儲存體</span><span class="sxs-lookup"><span data-stu-id="56cef-132">Storage</span></span>     |             | [<span data-ttu-id="56cef-133">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="56cef-133">More information</span></span>](log-analytics-azure-storage-iis-table.md) |
| <span data-ttu-id="56cef-134">辨識服務</span><span class="sxs-lookup"><span data-stu-id="56cef-134">Cognitive services</span></span>      | <span data-ttu-id="56cef-135">Microsoft.CognitiveServices/accounts</span><span class="sxs-lookup"><span data-stu-id="56cef-135">Microsoft.CognitiveServices/accounts</span></span>    |             | <span data-ttu-id="56cef-136">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-136">Diagnostics</span></span> | |
| <span data-ttu-id="56cef-137">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="56cef-137">Data Lake analytics</span></span>     | <span data-ttu-id="56cef-138">Microsoft.DataLakeAnalytics/accounts</span><span class="sxs-lookup"><span data-stu-id="56cef-138">Microsoft.DataLakeAnalytics/accounts</span></span>    | <span data-ttu-id="56cef-139">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-139">Diagnostics</span></span> |             | |
| <span data-ttu-id="56cef-140">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="56cef-140">Data Lake store</span></span>         | <span data-ttu-id="56cef-141">Microsoft.DataLakeStore/accounts</span><span class="sxs-lookup"><span data-stu-id="56cef-141">Microsoft.DataLakeStore/accounts</span></span>        | <span data-ttu-id="56cef-142">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-142">Diagnostics</span></span> |             | |
| <span data-ttu-id="56cef-143">事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="56cef-143">Event Hub namespace</span></span>     | <span data-ttu-id="56cef-144">Microsoft.EventHub/namespaces</span><span class="sxs-lookup"><span data-stu-id="56cef-144">Microsoft.EventHub/namespaces</span></span>           | <span data-ttu-id="56cef-145">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-145">Diagnostics</span></span> | <span data-ttu-id="56cef-146">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-146">Diagnostics</span></span> | |
| <span data-ttu-id="56cef-147">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="56cef-147">IoT Hubs</span></span>                | <span data-ttu-id="56cef-148">Microsoft.Devices/IotHubs</span><span class="sxs-lookup"><span data-stu-id="56cef-148">Microsoft.Devices/IotHubs</span></span>               |             | <span data-ttu-id="56cef-149">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-149">Diagnostics</span></span> | |
| <span data-ttu-id="56cef-150">金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="56cef-150">Key Vault</span></span>               | <span data-ttu-id="56cef-151">Microsoft.KeyVault/vaults</span><span class="sxs-lookup"><span data-stu-id="56cef-151">Microsoft.KeyVault/vaults</span></span>               | <span data-ttu-id="56cef-152">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-152">Diagnostics</span></span> |             | [<span data-ttu-id="56cef-153">金鑰保存庫分析</span><span class="sxs-lookup"><span data-stu-id="56cef-153">KeyVault Analytics</span></span>](log-analytics-azure-key-vault.md) |
| <span data-ttu-id="56cef-154">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="56cef-154">Load Balancers</span></span>          | <span data-ttu-id="56cef-155">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="56cef-155">Microsoft.Network/loadBalancers</span></span>         | <span data-ttu-id="56cef-156">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-156">Diagnostics</span></span> |             |  |
| <span data-ttu-id="56cef-157">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="56cef-157">Logic Apps</span></span>              | <span data-ttu-id="56cef-158">Microsoft.Logic/workflows</span><span class="sxs-lookup"><span data-stu-id="56cef-158">Microsoft.Logic/workflows</span></span> <br> <span data-ttu-id="56cef-159">Microsoft.Logic/integrationAccounts</span><span class="sxs-lookup"><span data-stu-id="56cef-159">Microsoft.Logic/integrationAccounts</span></span> | <span data-ttu-id="56cef-160">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-160">Diagnostics</span></span> | <span data-ttu-id="56cef-161">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-161">Diagnostics</span></span> | |
| <span data-ttu-id="56cef-162">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="56cef-162">Network Security Groups</span></span> | <span data-ttu-id="56cef-163">Microsoft.Network/networksecuritygroups</span><span class="sxs-lookup"><span data-stu-id="56cef-163">Microsoft.Network/networksecuritygroups</span></span> | <span data-ttu-id="56cef-164">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-164">Diagnostics</span></span> |             | [<span data-ttu-id="56cef-165">Azure 網路安全性群組分析</span><span class="sxs-lookup"><span data-stu-id="56cef-165">Azure Network Security Group Analytics</span></span>](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| <span data-ttu-id="56cef-166">復原保存庫</span><span class="sxs-lookup"><span data-stu-id="56cef-166">Recovery vaults</span></span>         | <span data-ttu-id="56cef-167">Microsoft.RecoveryServices/vaults</span><span class="sxs-lookup"><span data-stu-id="56cef-167">Microsoft.RecoveryServices/vaults</span></span>       |             |             | [<span data-ttu-id="56cef-168">Azure 復原服務分析 (預覽)</span><span class="sxs-lookup"><span data-stu-id="56cef-168">Azure Recovery Services Analytics (Preview)</span></span>](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| <span data-ttu-id="56cef-169">搜尋服務</span><span class="sxs-lookup"><span data-stu-id="56cef-169">Search services</span></span>         | <span data-ttu-id="56cef-170">Microsoft.Search/searchServices</span><span class="sxs-lookup"><span data-stu-id="56cef-170">Microsoft.Search/searchServices</span></span>         | <span data-ttu-id="56cef-171">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-171">Diagnostics</span></span> | <span data-ttu-id="56cef-172">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-172">Diagnostics</span></span> | |
| <span data-ttu-id="56cef-173">服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="56cef-173">Service Bus namespace</span></span>   | <span data-ttu-id="56cef-174">Microsoft.ServiceBus/namespaces</span><span class="sxs-lookup"><span data-stu-id="56cef-174">Microsoft.ServiceBus/namespaces</span></span>         | <span data-ttu-id="56cef-175">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-175">Diagnostics</span></span> | <span data-ttu-id="56cef-176">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-176">Diagnostics</span></span> | [<span data-ttu-id="56cef-177">服務匯流排分析 (預覽)</span><span class="sxs-lookup"><span data-stu-id="56cef-177">Service Bus Analytics (Preview)</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| <span data-ttu-id="56cef-178">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="56cef-178">Service Fabric</span></span>          |                                         | <span data-ttu-id="56cef-179">儲存體</span><span class="sxs-lookup"><span data-stu-id="56cef-179">Storage</span></span>     |             | [<span data-ttu-id="56cef-180">Service Fabric Analytics (Service Fabric 分析) (預覽)</span><span class="sxs-lookup"><span data-stu-id="56cef-180">Service Fabric Analytics (Preview)</span></span>](log-analytics-service-fabric.md) |
| <span data-ttu-id="56cef-181">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="56cef-181">SQL (v12)</span></span>               | <span data-ttu-id="56cef-182">Microsoft.Sql/servers/databases</span><span class="sxs-lookup"><span data-stu-id="56cef-182">Microsoft.Sql/servers/databases</span></span> <br> <span data-ttu-id="56cef-183">Microsoft.Sql/servers/elasticPools</span><span class="sxs-lookup"><span data-stu-id="56cef-183">Microsoft.Sql/servers/elasticPools</span></span> |             | <span data-ttu-id="56cef-184">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-184">Diagnostics</span></span> | [<span data-ttu-id="56cef-185">Azure SQL Analytics (預覽)</span><span class="sxs-lookup"><span data-stu-id="56cef-185">Azure SQL Analytics (Preview)</span></span>](log-analytics-azure-sql.md) |
| <span data-ttu-id="56cef-186">儲存體</span><span class="sxs-lookup"><span data-stu-id="56cef-186">Storage</span></span>                 |                                         |             | <span data-ttu-id="56cef-187">指令碼</span><span class="sxs-lookup"><span data-stu-id="56cef-187">Script</span></span>      | [<span data-ttu-id="56cef-188">Azure 儲存體分析 (預覽)</span><span class="sxs-lookup"><span data-stu-id="56cef-188">Azure Storage Analytics (Preview)</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| <span data-ttu-id="56cef-189">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56cef-189">Virtual Machines</span></span>        | <span data-ttu-id="56cef-190">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="56cef-190">Microsoft.Compute/virtualMachines</span></span>       | <span data-ttu-id="56cef-191">分機</span><span class="sxs-lookup"><span data-stu-id="56cef-191">Extension</span></span>   | <span data-ttu-id="56cef-192">分機</span><span class="sxs-lookup"><span data-stu-id="56cef-192">Extension</span></span> <br> <span data-ttu-id="56cef-193">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-193">Diagnostics</span></span>  | |
| <span data-ttu-id="56cef-194">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="56cef-194">Virtual Machines scale sets</span></span> | <span data-ttu-id="56cef-195">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="56cef-195">Microsoft.Compute/virtualMachines</span></span> <br> <span data-ttu-id="56cef-196">Microsoft.Compute/virtualMachineScaleSets/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="56cef-196">Microsoft.Compute/virtualMachineScaleSets/virtualMachines</span></span> |             | <span data-ttu-id="56cef-197">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-197">Diagnostics</span></span> | |
| <span data-ttu-id="56cef-198">Web 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="56cef-198">Web Server farms</span></span>        | <span data-ttu-id="56cef-199">Microsoft.Web/serverfarms</span><span class="sxs-lookup"><span data-stu-id="56cef-199">Microsoft.Web/serverfarms</span></span>               |             | <span data-ttu-id="56cef-200">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-200">Diagnostics</span></span> | |
| <span data-ttu-id="56cef-201">網站</span><span class="sxs-lookup"><span data-stu-id="56cef-201">Web Sites</span></span>               | <span data-ttu-id="56cef-202">Microsoft.Web/sites</span><span class="sxs-lookup"><span data-stu-id="56cef-202">Microsoft.Web/sites</span></span> <br> <span data-ttu-id="56cef-203">Microsoft.Web/sites/slots</span><span class="sxs-lookup"><span data-stu-id="56cef-203">Microsoft.Web/sites/slots</span></span> |             | <span data-ttu-id="56cef-204">診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-204">Diagnostics</span></span> | [<span data-ttu-id="56cef-205">Azure Web Apps 分析 (預覽)</span><span class="sxs-lookup"><span data-stu-id="56cef-205">Azure Web Apps Analytics (Preview)</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> <span data-ttu-id="56cef-206">我們建議您監視 Azure 虛擬機器 （Linux 和 Windows），安裝 hello[記錄分析 VM 延伸模組](log-analytics-azure-vm-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="56cef-206">For monitoring Azure virtual machines (both Linux and Windows), we recommend installing hello [Log Analytics VM extension](log-analytics-azure-vm-extension.md).</span></span> <span data-ttu-id="56cef-207">hello 代理程式為您提供從收集您的虛擬機器內的深入資訊。</span><span class="sxs-lookup"><span data-stu-id="56cef-207">hello agent provides you with insights collected from within your virtual machines.</span></span> <span data-ttu-id="56cef-208">您也可以使用 hello 擴充功能的虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="56cef-208">You can also use hello extension for Virtual machine scale sets.</span></span>
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a><span data-ttu-id="56cef-209">直接 tooLog 分析 azure 診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-209">Azure diagnostics direct tooLog Analytics</span></span>
<span data-ttu-id="56cef-210">許多 Azure 資源都可以 toowrite 診斷記錄檔和度量直接 tooLog 分析，而這是慣用的 hello 方式收集 hello 資料以供分析。</span><span class="sxs-lookup"><span data-stu-id="56cef-210">Many Azure resources are able toowrite diagnostic logs and metrics directly tooLog Analytics and this is hello preferred way of collecting hello data for analysis.</span></span> <span data-ttu-id="56cef-211">當使用 Azure 診斷，資料會寫入立即 tooLog 分析，而且沒有任何需要 toofirst 寫入 hello 資料 toostorage。</span><span class="sxs-lookup"><span data-stu-id="56cef-211">When using Azure diagnostics, data is written immediately tooLog Analytics and there is no need toofirst write hello data toostorage.</span></span>

<span data-ttu-id="56cef-212">支援的 azure 資源[Azure 監視器](../monitoring-and-diagnostics/monitoring-overview.md)可以傳送其記錄檔和度量直接 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="56cef-212">Azure resources that support [Azure monitor](../monitoring-and-diagnostics/monitoring-overview.md) can send their logs and metrics directly tooLog Analytics.</span></span>

* <span data-ttu-id="56cef-213">Hello hello 可用度量的詳細資訊，請參閱太[支援的 Azure 監視的度量](../monitoring-and-diagnostics/monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="56cef-213">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="56cef-214">Hello 的 hello 可用的記錄檔的詳細資訊，請參閱太[支援診斷記錄檔的服務和結構描述](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="56cef-214">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

### <a name="enable-diagnostics-with-powershell"></a><span data-ttu-id="56cef-215">啟用 PowerShell 的診斷功能</span><span class="sxs-lookup"><span data-stu-id="56cef-215">Enable diagnostics with PowerShell</span></span>
<span data-ttu-id="56cef-216">您需要 hello 年 11 月 2016 (v2.3.0) 或更新版本的版本[Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="56cef-216">You need hello November 2016 (v2.3.0) or later release of [Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="56cef-217">hello 下列 PowerShell 範例會示範如何 toouse[組 AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable 診斷上的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="56cef-217">hello following PowerShell example shows how toouse [Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable diagnostics on a network security group.</span></span> <span data-ttu-id="56cef-218">hello 相同的方法適用於所有支援的資源-設定`$resourceId`toohello 想 tooenable 診斷的 hello 資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="56cef-218">hello same approach works for all supported resources - set `$resourceId` toohello resource id of hello resource you want tooenable diagnostics for.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a><span data-ttu-id="56cef-219">使用 Resource Manager 範本啟用診斷</span><span class="sxs-lookup"><span data-stu-id="56cef-219">Enable diagnostics with Resource Manager templates</span></span>

<span data-ttu-id="56cef-220">tooenable 診斷而建立，而且有 hello 診斷傳送 tooyour 記錄分析工作區，您可以使用其中一個範本類似 toohello 下方時，在資源上。</span><span class="sxs-lookup"><span data-stu-id="56cef-220">tooenable diagnostics on a resource when it is created, and have hello diagnostics sent tooyour Log Analytics workspace you can use a template similar toohello one below.</span></span> <span data-ttu-id="56cef-221">這個範例是針對自動化帳戶，但也適用於所有支援的資源類型。</span><span class="sxs-lookup"><span data-stu-id="56cef-221">This example is for an Automation account but works for all supported resource types.</span></span>

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a><span data-ttu-id="56cef-222">Azure 診斷 toostorage 然後 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="56cef-222">Azure diagnostics toostorage then tooLog Analytics</span></span>

<span data-ttu-id="56cef-223">收集來自某些資源內的記錄檔，可能 toosend hello 記錄檔 tooAzure 儲存體，並接著設定從儲存體的記錄分析 tooread hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="56cef-223">For collecting logs from within some resources, it is possible toosend hello logs tooAzure storage and then configure Log Analytics tooread hello logs from storage.</span></span>

<span data-ttu-id="56cef-224">記錄分析可使用此方法 toocollect 診斷從 Azure 儲存體 hello 下列資源和記錄檔：</span><span class="sxs-lookup"><span data-stu-id="56cef-224">Log Analytics can use this approach toocollect diagnostics from Azure storage for hello following resources and logs:</span></span>

| <span data-ttu-id="56cef-225">資源</span><span class="sxs-lookup"><span data-stu-id="56cef-225">Resource</span></span> | <span data-ttu-id="56cef-226">記錄檔</span><span class="sxs-lookup"><span data-stu-id="56cef-226">Logs</span></span> |
| --- | --- |
| <span data-ttu-id="56cef-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="56cef-227">Service Fabric</span></span> |<span data-ttu-id="56cef-228">ETWEvent</span><span class="sxs-lookup"><span data-stu-id="56cef-228">ETWEvent</span></span> <br> <span data-ttu-id="56cef-229">運作事件</span><span class="sxs-lookup"><span data-stu-id="56cef-229">Operational Event</span></span> <br> <span data-ttu-id="56cef-230">Reliable Actor 事件</span><span class="sxs-lookup"><span data-stu-id="56cef-230">Reliable Actor Event</span></span> <br> <span data-ttu-id="56cef-231">Reliable Service 事件</span><span class="sxs-lookup"><span data-stu-id="56cef-231">Reliable Service Event</span></span> |
| <span data-ttu-id="56cef-232">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="56cef-232">Virtual Machines</span></span> |<span data-ttu-id="56cef-233">Linux Syslog</span><span class="sxs-lookup"><span data-stu-id="56cef-233">Linux Syslog</span></span> <br> <span data-ttu-id="56cef-234">Windows 事件</span><span class="sxs-lookup"><span data-stu-id="56cef-234">Windows Event</span></span> <br> <span data-ttu-id="56cef-235">IIS 記錄</span><span class="sxs-lookup"><span data-stu-id="56cef-235">IIS Log</span></span> <br> <span data-ttu-id="56cef-236">Windows ETWEvent</span><span class="sxs-lookup"><span data-stu-id="56cef-236">Windows ETWEvent</span></span> |
| <span data-ttu-id="56cef-237">Web 角色</span><span class="sxs-lookup"><span data-stu-id="56cef-237">Web Roles</span></span> <br> <span data-ttu-id="56cef-238">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="56cef-238">Worker Roles</span></span> |<span data-ttu-id="56cef-239">Linux Syslog</span><span class="sxs-lookup"><span data-stu-id="56cef-239">Linux Syslog</span></span> <br> <span data-ttu-id="56cef-240">Windows 事件</span><span class="sxs-lookup"><span data-stu-id="56cef-240">Windows Event</span></span> <br> <span data-ttu-id="56cef-241">IIS 記錄</span><span class="sxs-lookup"><span data-stu-id="56cef-241">IIS Log</span></span> <br> <span data-ttu-id="56cef-242">Windows ETWEvent</span><span class="sxs-lookup"><span data-stu-id="56cef-242">Windows ETWEvent</span></span> |

> [!NOTE]
> <span data-ttu-id="56cef-243">您會將一般的 Azure 資料或是儲存和交易，當您將診斷傳送 tooa 儲存體帳戶，以及當記錄分析儲存體帳戶讀取 hello 資料支付費用。</span><span class="sxs-lookup"><span data-stu-id="56cef-243">You are charged normal Azure data rates for storage and transactions when you send diagnostics tooa storage account and for when Log Analytics reads hello data from your storage account.</span></span>
>
>

<span data-ttu-id="56cef-244">請參閱[事件的 IIS 和資料表儲存體使用 blob 儲存體](log-analytics-azure-storage-iis-table.md)toolearn 深入了解如何收集記錄分析這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="56cef-244">See [Use blob storage for IIS and table storage for events](log-analytics-azure-storage-iis-table.md) toolearn more about how Log Analytics can collect these logs.</span></span>

## <a name="connectors-for-azure-services"></a><span data-ttu-id="56cef-245">Azure 服務的連接器</span><span class="sxs-lookup"><span data-stu-id="56cef-245">Connectors for Azure services</span></span>

<span data-ttu-id="56cef-246">沒有 Application Insights，可讓傳送 tooLog 分析的 Application Insights toobe 所收集資料的連接器。</span><span class="sxs-lookup"><span data-stu-id="56cef-246">There is a connector for Application Insights, which allows data collected by Application Insights toobe sent tooLog Analytics.</span></span>

<span data-ttu-id="56cef-247">深入了解 hello [Application Insights 連接器](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)。</span><span class="sxs-lookup"><span data-stu-id="56cef-247">Learn more about hello [Application Insights connector](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).</span></span>

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a><span data-ttu-id="56cef-248">指令碼 toocollect 和 post 資料 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="56cef-248">Scripts toocollect and post data tooLog Analytics</span></span>

<span data-ttu-id="56cef-249">Azure 服務不提供直接的方式 toosend 記錄檔和度量 tooLog 分析，您可以使用 Azure 自動化指令碼 toocollect hello 記錄和度量。</span><span class="sxs-lookup"><span data-stu-id="56cef-249">For Azure services that do not provide a direct way toosend logs and metrics tooLog Analytics you can use an Azure Automation script toocollect hello log and metrics.</span></span> <span data-ttu-id="56cef-250">hello 指令碼可以再傳送嗨資料 tooLog 分析使用 hello[資料收集器 API](log-analytics-data-collector-api.md)</span><span class="sxs-lookup"><span data-stu-id="56cef-250">hello script can then send hello data tooLog Analytics using hello [data collector API](log-analytics-data-collector-api.md)</span></span>

<span data-ttu-id="56cef-251">hello Azure 範本庫具有[使用 Azure 自動化的範例](https://azure.microsoft.com/en-us/resources/templates/?term=OMS)toocollect 資料服務，將它傳送 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="56cef-251">hello Azure template gallery has [examples of using Azure Automation](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect data from services and sending it tooLog Analytics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56cef-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56cef-252">Next steps</span></span>

* <span data-ttu-id="56cef-253">[事件的 IIS 和資料表儲存體使用 blob 儲存體](log-analytics-azure-storage-iis-table.md)tooread hello 記錄檔寫入 tootable 診斷儲存體或 IIS 記錄檔中寫入的 tooblob 儲存體的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="56cef-253">[Use blob storage for IIS and table storage for events](log-analytics-azure-storage-iis-table.md) tooread hello logs for Azure services that write diagnostics tootable storage or IIS logs written tooblob storage.</span></span>
* <span data-ttu-id="56cef-254">[啟用方案](log-analytics-add-solutions.md)tooprovide 深入了解 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="56cef-254">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="56cef-255">[使用搜尋查詢](log-analytics-log-searches.md)tooanalyze hello 資料。</span><span class="sxs-lookup"><span data-stu-id="56cef-255">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>