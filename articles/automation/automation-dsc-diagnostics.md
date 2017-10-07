---
title: "Azure 自動化 DSC 報告資料 tooOMS 記錄分析 aaaForward |Microsoft 文件"
description: "本文示範如何 toosend 預期狀態設定 (DSC) 報告資料 tooMicrosoft Operations Management Suite 記錄分析 toodeliver 見解，並管理。"
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a><span data-ttu-id="93fe4-103">轉送 Azure 自動化 DSC 報告資料 tooOMS 記錄分析</span><span class="sxs-lookup"><span data-stu-id="93fe4-103">Forward Azure Automation DSC reporting data tooOMS Log Analytics</span></span>

<span data-ttu-id="93fe4-104">自動化可以傳送 DSC 節點狀態資料 tooyour Microsoft Operations Management Suite (OMS) 的記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="93fe4-104">Automation can send DSC node status data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  
<span data-ttu-id="93fe4-105">相容性狀態會顯示在 hello Azure 入口網站或 PowerShell，針對節點和節點設定中個別的 DSC 資源。</span><span class="sxs-lookup"><span data-stu-id="93fe4-105">Compliance status is visible in hello Azure portal, or with PowerShell, for nodes and for individual DSC resources in node configurations.</span></span> <span data-ttu-id="93fe4-106">透過 Log Analytics，您可以：</span><span class="sxs-lookup"><span data-stu-id="93fe4-106">With Log Analytics you can:</span></span>

* <span data-ttu-id="93fe4-107">取得受管理節點與個別資源的合規性資訊</span><span class="sxs-lookup"><span data-stu-id="93fe4-107">Get compliance information for managed nodes and individual resources</span></span>
* <span data-ttu-id="93fe4-108">根據合規性狀態觸發電子郵件或警示</span><span class="sxs-lookup"><span data-stu-id="93fe4-108">Trigger an email or alert based on compliance status</span></span>
* <span data-ttu-id="93fe4-109">撰寫受管理節點之間的進階查詢</span><span class="sxs-lookup"><span data-stu-id="93fe4-109">Write advanced queries across your managed nodes</span></span>
* <span data-ttu-id="93fe4-110">相互關聯自動化帳戶之間的合規性狀態</span><span class="sxs-lookup"><span data-stu-id="93fe4-110">Correlate compliance status across Automation accounts</span></span>
* <span data-ttu-id="93fe4-111">以視覺化方式呈現一段時間的合規性歷程記錄</span><span class="sxs-lookup"><span data-stu-id="93fe4-111">Visualize your node compliance history over time</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93fe4-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="93fe4-112">Prerequisites</span></span>

<span data-ttu-id="93fe4-113">toostart 傳送自動化 DSC 報告 tooLog 分析，您需要：</span><span class="sxs-lookup"><span data-stu-id="93fe4-113">toostart sending your Automation DSC reports tooLog Analytics, you need:</span></span>

* <span data-ttu-id="93fe4-114">hello 2016 年 11 月版或更新版本的版本[Azure PowerShell](/powershell/azure/overview) (v2.3.0)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-114">hello November 2016 or later release of [Azure PowerShell](/powershell/azure/overview) (v2.3.0).</span></span>
* <span data-ttu-id="93fe4-115">Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="93fe4-115">An Azure Automation account.</span></span> <span data-ttu-id="93fe4-116">如需詳細資訊，請參閱[開始使用 Azure 自動化](automation-offering-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-116">For more information, see [Getting Started with Azure Automation](automation-offering-get-started.md)</span></span>
* <span data-ttu-id="93fe4-117">提供 [自動化與控制] 服務的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="93fe4-117">A Log Analytics workspace with an **Automation & Control** service offering.</span></span> <span data-ttu-id="93fe4-118">如需詳細資訊，請參閱[開始使用 Log Analytics](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-118">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span>
* <span data-ttu-id="93fe4-119">至少一個 Azure Automation DSC 節點。</span><span class="sxs-lookup"><span data-stu-id="93fe4-119">At least one Azure Automation DSC node.</span></span> <span data-ttu-id="93fe4-120">如需詳細資訊，請參閱[將機器上架交由 Azure Automation DSC 管理](automation-dsc-onboarding.md)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-120">For more information, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span> 

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="93fe4-121">設定與 Log Analytics 整合</span><span class="sxs-lookup"><span data-stu-id="93fe4-121">Set up integration with Log Analytics</span></span>

<span data-ttu-id="93fe4-122">將資料匯入從 Azure Automation DSC 記錄分析，完成下列步驟的 hello toobegin:</span><span class="sxs-lookup"><span data-stu-id="93fe4-122">toobegin importing data from Azure Automation DSC into Log Analytics, complete hello following steps:</span></span>

1. <span data-ttu-id="93fe4-123">在 PowerShell 中的 Azure 帳戶登入 tooyour 中。</span><span class="sxs-lookup"><span data-stu-id="93fe4-123">Log in tooyour Azure account in PowerShell.</span></span> <span data-ttu-id="93fe4-124">請參閱[使用 Azure PowerShell 登入](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)</span><span class="sxs-lookup"><span data-stu-id="93fe4-124">See [Log in with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)</span></span>
1. <span data-ttu-id="93fe4-125">取得 hello _ResourceId_您的自動化帳戶執行下列 PowerShell 命令的 hello: (如果您有多個自動化帳戶時，選擇 hello _ResourceID_ hello 您想要的帳戶tooconfigure)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-125">Get hello _ResourceId_ of your automation account by running hello following PowerShell command: (if you have more than one automation account, choose hello _ResourceID_ for hello account you want tooconfigure).</span></span>

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. <span data-ttu-id="93fe4-126">取得 hello _ResourceId_的記錄分析工作區中執行下列 PowerShell 命令的 hello: (如果您有多個工作區中，選擇 hello _ResourceID_ hello 您想要的工作區tooconfigure)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-126">Get hello _ResourceId_ of your Log Analytics workspace by running hello following PowerShell command: (if you have more than one workspace, choose hello _ResourceID_ for hello workspace you want tooconfigure).</span></span>

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. <span data-ttu-id="93fe4-127">下列 PowerShell 命令，取代執行的 hello`<AutomationResourceId>`和`<WorkspaceResourceId>`以 hello _ResourceId_ hello 前一步驟的每個值：</span><span class="sxs-lookup"><span data-stu-id="93fe4-127">Run hello following PowerShell command, replacing `<AutomationResourceId>` and `<WorkspaceResourceId>` with hello _ResourceId_ values from each of hello previous steps:</span></span>

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

<span data-ttu-id="93fe4-128">如果您想將資料匯入從 Azure Automation DSC 記錄分析 toostop，執行下列 PowerShell 命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="93fe4-128">If you want toostop importing data from Azure Automation DSC into Log Analytics, run hello following PowerShell command.</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a><span data-ttu-id="93fe4-129">檢視 hello DSC 記錄檔</span><span class="sxs-lookup"><span data-stu-id="93fe4-129">View hello DSC logs</span></span>

<span data-ttu-id="93fe4-130">Automation DSC 資料與記錄分析的整合設定之後**記錄搜尋**按鈕將會出現在 hello **DSC 節點**刀鋒視窗中的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="93fe4-130">After you set up integration with Log Analytics for your Automation DSC data, a **Log search** button will appear on hello **DSC Nodes** blade of your automation account.</span></span> <span data-ttu-id="93fe4-131">按一下 hello**記錄搜尋**按鈕 tooview hello 記錄檔以取得 DSC 節點資料。</span><span class="sxs-lookup"><span data-stu-id="93fe4-131">Click hello **Log Search** button tooview hello logs for DSC node data.</span></span>

![記錄搜尋按鈕](media/automation-dsc-diagnostics/log-search-button.png)

<span data-ttu-id="93fe4-133">hello**記錄搜尋**刀鋒視窗隨即開啟，而且您看見**DscNodeStatusData**每個 DSC 節點、 作業和**DscResourceStatusData**每個作業[DSC資源](https://msdn.microsoft.com/powershell/dsc/resources)呼叫 hello 節點組態套用的 toothat 節點中。</span><span class="sxs-lookup"><span data-stu-id="93fe4-133">hello **Log Search** blade opens, and you see a **DscNodeStatusData** operation for each DSC node, and a **DscResourceStatusData** operation for each [DSC resource](https://msdn.microsoft.com/powershell/dsc/resources) called in hello Node configuration applied toothat node.</span></span>

<span data-ttu-id="93fe4-134">hello **DscResourceStatusData**作業包含失敗的任何 DSC 資源資訊時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="93fe4-134">hello **DscResourceStatusData** operation contains error information for any DSC resources that failed.</span></span>

<span data-ttu-id="93fe4-135">按一下 hello 清單 toosee hello 資料中的每項作業，該作業。</span><span class="sxs-lookup"><span data-stu-id="93fe4-135">Click each operation in hello list toosee hello data for that operation.</span></span>

<span data-ttu-id="93fe4-136">您也可以檢視 hello 記錄檔 [記錄分析搜尋。</span><span class="sxs-lookup"><span data-stu-id="93fe4-136">You can also view hello logs by [searching in Log Analytics.</span></span> <span data-ttu-id="93fe4-137">請參閱[使用記錄搜尋尋找資料](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-137">See [Find data using log searches](../log-analytics/log-analytics-log-searches.md).</span></span>
<span data-ttu-id="93fe4-138">型別 hello 下列查詢會 toofind 您 DSC 記錄檔：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`</span><span class="sxs-lookup"><span data-stu-id="93fe4-138">Type hello following query toofind your DSC logs: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`</span></span>

<span data-ttu-id="93fe4-139">您也可以縮小 hello 查詢 hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-139">You can also narrow hello query by hello operation name.</span></span> <span data-ttu-id="93fe4-140">例如：\`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"</span><span class="sxs-lookup"><span data-stu-id="93fe4-140">For example: \`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"</span></span>

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a><span data-ttu-id="93fe4-141">DSC 合規性檢查失敗時傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="93fe4-141">Send an email when a DSC compliance check fails</span></span>

<span data-ttu-id="93fe4-142">我們最上層的客戶的要求是針對 hello 能力 toosend 電子郵件或文字時出錯 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="93fe4-142">One of our top customer requests is for hello ability toosend an email or a text when something goes wrong with a DSC configuration.</span></span>   

<span data-ttu-id="93fe4-143">toocreate 警示規則時，它會先建立應叫用 hello 警示的 hello DSC 報表記錄的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="93fe4-143">toocreate an alert rule, you start by creating a log search for hello DSC report records that should invoke hello alert.</span></span>  <span data-ttu-id="93fe4-144">按一下 hello**警示**按鈕 toocreate 及設定 hello 警示規則。</span><span class="sxs-lookup"><span data-stu-id="93fe4-144">Click hello **Alert** button toocreate and configure hello alert rule.</span></span>

1. <span data-ttu-id="93fe4-145">從 hello 記錄分析概觀] 頁面上，按一下 [**記錄搜尋**。</span><span class="sxs-lookup"><span data-stu-id="93fe4-145">From hello Log Analytics Overview page, click **Log Search**.</span></span>
1. <span data-ttu-id="93fe4-146">輸入下列搜尋到 hello 查詢欄位中的 hello 建立警示的記錄搜尋查詢：`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`</span><span class="sxs-lookup"><span data-stu-id="93fe4-146">Create a log search query for your alert by typing hello following search into hello query field:  `Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`</span></span>

  <span data-ttu-id="93fe4-147">如果您已將設定從多個自動化帳戶或訂用帳戶 tooyour 工作區的記錄檔，您可以群組您的訂用帳戶和自動化帳戶的警示。</span><span class="sxs-lookup"><span data-stu-id="93fe4-147">If you have set up logs from more than one Automation account or subscription tooyour workspace, you can group your alerts by subscription and Automation account.</span></span>  
  <span data-ttu-id="93fe4-148">自動化帳戶名稱可以衍生自 DscNodeStatusData hello 搜尋中的 hello 資源欄位。</span><span class="sxs-lookup"><span data-stu-id="93fe4-148">Automation account name can be derived from hello Resource field in hello search of DscNodeStatusData.</span></span>  
1. <span data-ttu-id="93fe4-149">tooopen hello**加入警示規則**畫面上，按一下**警示**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="93fe4-149">tooopen hello **Add Alert Rule** screen, click **Alert** at hello top of hello page.</span></span> <span data-ttu-id="93fe4-150">如需有關 hello 選項 tooconfigure hello 警示的詳細資訊，請參閱[記錄分析中的警示](../log-analytics/log-analytics-alerts.md#alert-rules)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-150">For more information on hello options tooconfigure hello alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-failed-dsc-resources-across-all-nodes"></a><span data-ttu-id="93fe4-151">在所有節點間尋找失敗的 DSC 資源</span><span class="sxs-lookup"><span data-stu-id="93fe4-151">Find failed DSC resources across all nodes</span></span>

<span data-ttu-id="93fe4-152">使用 Log Analytics 的優點之一，是您可以在所有節點間搜尋失敗的檢查。</span><span class="sxs-lookup"><span data-stu-id="93fe4-152">One advantage of using Log Analytics is that you can search for failed checks across nodes.</span></span>
<span data-ttu-id="93fe4-153">toofind 失敗的 DSC 資源的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="93fe4-153">toofind all instances of DSC resources that failed.</span></span>

1. <span data-ttu-id="93fe4-154">從 hello 記錄分析概觀] 頁面上，按一下 [**記錄搜尋**。</span><span class="sxs-lookup"><span data-stu-id="93fe4-154">From hello Log Analytics Overview page, click **Log Search**.</span></span>
1. <span data-ttu-id="93fe4-155">輸入下列搜尋到 hello 查詢欄位中的 hello 建立警示的記錄搜尋查詢：`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`</span><span class="sxs-lookup"><span data-stu-id="93fe4-155">Create a log search query for your alert by typing hello following search into hello query field:  `Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`</span></span>

### <a name="view-historical-dsc-node-status"></a><span data-ttu-id="93fe4-156">檢視歷程記錄 DSC 節點狀態</span><span class="sxs-lookup"><span data-stu-id="93fe4-156">View historical DSC node status</span></span>

<span data-ttu-id="93fe4-157">最後，您可能想 toovisualize DSC 節點狀態歷程記錄一段時間。</span><span class="sxs-lookup"><span data-stu-id="93fe4-157">Finally, you may want toovisualize your DSC node status history over time.</span></span>  
<span data-ttu-id="93fe4-158">您可以使用這個查詢 toosearch hello 狀態為您 DSC 節點的狀態，經過一段時間。</span><span class="sxs-lookup"><span data-stu-id="93fe4-158">You can use this query toosearch for hello status of your DSC node status over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

<span data-ttu-id="93fe4-159">經過一段時間，這會顯示 hello 節點狀態的圖表。</span><span class="sxs-lookup"><span data-stu-id="93fe4-159">This will display a chart of hello node status over time.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="93fe4-160">Log Analytics 記錄</span><span class="sxs-lookup"><span data-stu-id="93fe4-160">Log Analytics records</span></span>

<span data-ttu-id="93fe4-161">來自 Azure 自動化的診斷會在 Log Analytics 中建立兩種記錄類別。</span><span class="sxs-lookup"><span data-stu-id="93fe4-161">Diagnostics from Azure Automation creates two categories of records in Log Analytics.</span></span>

### <a name="dscnodestatusdata"></a><span data-ttu-id="93fe4-162">DscNodeStatusData</span><span class="sxs-lookup"><span data-stu-id="93fe4-162">DscNodeStatusData</span></span>

| <span data-ttu-id="93fe4-163">屬性</span><span class="sxs-lookup"><span data-stu-id="93fe4-163">Property</span></span> | <span data-ttu-id="93fe4-164">說明</span><span class="sxs-lookup"><span data-stu-id="93fe4-164">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93fe4-165">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="93fe4-165">TimeGenerated</span></span> |<span data-ttu-id="93fe4-166">日期和時間執行 hello 相容性檢查的時間。</span><span class="sxs-lookup"><span data-stu-id="93fe4-166">Date and time when hello compliance check ran.</span></span> |
| <span data-ttu-id="93fe4-167">OperationName</span><span class="sxs-lookup"><span data-stu-id="93fe4-167">OperationName</span></span> |<span data-ttu-id="93fe4-168">DscNodeStatusData</span><span class="sxs-lookup"><span data-stu-id="93fe4-168">DscNodeStatusData</span></span> |
| <span data-ttu-id="93fe4-169">ResultType</span><span class="sxs-lookup"><span data-stu-id="93fe4-169">ResultType</span></span> |<span data-ttu-id="93fe4-170">Hello 節點是否相容。</span><span class="sxs-lookup"><span data-stu-id="93fe4-170">Whether hello node is compliant.</span></span> |
| <span data-ttu-id="93fe4-171">NodeName_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-171">NodeName_s</span></span> |<span data-ttu-id="93fe4-172">hello hello 受管理的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-172">hello name of hello managed node.</span></span> |
| <span data-ttu-id="93fe4-173">NodeComplianceStatus_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-173">NodeComplianceStatus_s</span></span> |<span data-ttu-id="93fe4-174">Hello 節點是否相容。</span><span class="sxs-lookup"><span data-stu-id="93fe4-174">Whether hello node is compliant.</span></span> |
| <span data-ttu-id="93fe4-175">DscReportStatus</span><span class="sxs-lookup"><span data-stu-id="93fe4-175">DscReportStatus</span></span> |<span data-ttu-id="93fe4-176">Hello 相容性檢查是否已順利執行。</span><span class="sxs-lookup"><span data-stu-id="93fe4-176">Whether hello compliance check ran successfully.</span></span> |
| <span data-ttu-id="93fe4-177">ConfigurationMode</span><span class="sxs-lookup"><span data-stu-id="93fe4-177">ConfigurationMode</span></span> | <span data-ttu-id="93fe4-178">如何 hello 設定是套用的 toohello 節點。</span><span class="sxs-lookup"><span data-stu-id="93fe4-178">How hello configuration is applied toohello node.</span></span> <span data-ttu-id="93fe4-179">可能的值為 __"ApplyOnly"__、__"ApplyandMonitior"__ 和 __"ApplyandAutoCorrect"__。</span><span class="sxs-lookup"><span data-stu-id="93fe4-179">Possible values are __"ApplyOnly"__,__"ApplyandMonitior"__, and __"ApplyandAutoCorrect"__.</span></span> <ul><li><span data-ttu-id="93fe4-180">__ApplyOnly__: DSC 會套用 hello 組態，並且不執行進一步除非新的設定已推送 toohello 目標節點，或當從伺服器提取新的設定。</span><span class="sxs-lookup"><span data-stu-id="93fe4-180">__ApplyOnly__: DSC applies hello configuration and does nothing further unless a new configuration is pushed toohello target node or when a new configuration is pulled from a server.</span></span> <span data-ttu-id="93fe4-181">初始套用新的設定之後，DSC 不會檢查先前設定的狀態是否漂移。</span><span class="sxs-lookup"><span data-stu-id="93fe4-181">After initial application of a new configuration, DSC does not check for drift from a previously configured state.</span></span> <span data-ttu-id="93fe4-182">DSC 在成功完成之前嘗試 tooapply hello 組態__ApplyOnly__才會生效。</span><span class="sxs-lookup"><span data-stu-id="93fe4-182">DSC attempts tooapply hello configuration until it is successful before __ApplyOnly__ takes effect.</span></span> </li><li> <span data-ttu-id="93fe4-183">__ApplyAndMonitor__： 這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="93fe4-183">__ApplyAndMonitor__: This is hello default value.</span></span> <span data-ttu-id="93fe4-184">hello LCM 適用於任何新的設定。</span><span class="sxs-lookup"><span data-stu-id="93fe4-184">hello LCM applies any new configurations.</span></span> <span data-ttu-id="93fe4-185">初始新設定的應用程式之後, 如果 hello 目標節點偏離預期 hello 狀態，DSC 會報告記錄檔中的 hello 差異。</span><span class="sxs-lookup"><span data-stu-id="93fe4-185">After initial application of a new configuration, if hello target node drifts from hello desired state, DSC reports hello discrepancy in logs.</span></span> <span data-ttu-id="93fe4-186">DSC 在成功完成之前嘗試 tooapply hello 組態__ApplyAndMonitor__才會生效。</span><span class="sxs-lookup"><span data-stu-id="93fe4-186">DSC attempts tooapply hello configuration until it is successful before __ApplyAndMonitor__ takes effect.</span></span></li><li><span data-ttu-id="93fe4-187">__ApplyAndAutoCorrect__：DSC 會套用任何新的設定。</span><span class="sxs-lookup"><span data-stu-id="93fe4-187">__ApplyAndAutoCorrect__: DSC applies any new configurations.</span></span> <span data-ttu-id="93fe4-188">之後的新設定，如果 hello 目標節點偏離預期 hello 狀態，DSC 會報告記錄檔中的 hello 差異，然後重新套用目前設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="93fe4-188">After initial application of a new configuration, if hello target node drifts from hello desired state, DSC reports hello discrepancy in logs, and then reapplies hello current configuration.</span></span></li></ul> |
| <span data-ttu-id="93fe4-189">HostName_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-189">HostName_s</span></span> | <span data-ttu-id="93fe4-190">hello hello 受管理的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-190">hello name of hello managed node.</span></span> |
| <span data-ttu-id="93fe4-191">IPAddress</span><span class="sxs-lookup"><span data-stu-id="93fe4-191">IPAddress</span></span> | <span data-ttu-id="93fe4-192">hello hello IPv4 位址受管理節點。</span><span class="sxs-lookup"><span data-stu-id="93fe4-192">hello IPv4 address of hello managed node.</span></span> |
| <span data-ttu-id="93fe4-193">類別</span><span class="sxs-lookup"><span data-stu-id="93fe4-193">Category</span></span> | <span data-ttu-id="93fe4-194">DscNodeStatus</span><span class="sxs-lookup"><span data-stu-id="93fe4-194">DscNodeStatus</span></span> |
| <span data-ttu-id="93fe4-195">資源</span><span class="sxs-lookup"><span data-stu-id="93fe4-195">Resource</span></span> | <span data-ttu-id="93fe4-196">hello hello Azure 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-196">hello name of hello Azure Automation account.</span></span> |
| <span data-ttu-id="93fe4-197">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="93fe4-197">Tenant_g</span></span> | <span data-ttu-id="93fe4-198">識別 hello 呼叫端的 hello 租用戶的 GUID。</span><span class="sxs-lookup"><span data-stu-id="93fe4-198">GUID that identifies hello tenant for hello Caller.</span></span> |
| <span data-ttu-id="93fe4-199">NodeId_g</span><span class="sxs-lookup"><span data-stu-id="93fe4-199">NodeId_g</span></span> |<span data-ttu-id="93fe4-200">GUID，識別 hello 受管理的節點。</span><span class="sxs-lookup"><span data-stu-id="93fe4-200">GUID that identifies hello managed node.</span></span> |
| <span data-ttu-id="93fe4-201">DscReportId_g</span><span class="sxs-lookup"><span data-stu-id="93fe4-201">DscReportId_g</span></span> |<span data-ttu-id="93fe4-202">GUID，識別 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="93fe4-202">GUID that identifies hello report.</span></span> |
| <span data-ttu-id="93fe4-203">LastSeenTime_t</span><span class="sxs-lookup"><span data-stu-id="93fe4-203">LastSeenTime_t</span></span> |<span data-ttu-id="93fe4-204">日期和上次檢視 hello 報表時的時間。</span><span class="sxs-lookup"><span data-stu-id="93fe4-204">Date and time when hello report was last viewed.</span></span> |
| <span data-ttu-id="93fe4-205">ReportStartTime_t</span><span class="sxs-lookup"><span data-stu-id="93fe4-205">ReportStartTime_t</span></span> |<span data-ttu-id="93fe4-206">日期和時間啟動 hello 報表時。</span><span class="sxs-lookup"><span data-stu-id="93fe4-206">Date and time when hello report was started.</span></span> |
| <span data-ttu-id="93fe4-207">ReportEndTime_t</span><span class="sxs-lookup"><span data-stu-id="93fe4-207">ReportEndTime_t</span></span> |<span data-ttu-id="93fe4-208">日期和時間 hello 報表完成時。</span><span class="sxs-lookup"><span data-stu-id="93fe4-208">Date and time when hello report completed.</span></span> |
| <span data-ttu-id="93fe4-209">NumberOfResources_d</span><span class="sxs-lookup"><span data-stu-id="93fe4-209">NumberOfResources_d</span></span> |<span data-ttu-id="93fe4-210">DSC 資源的 hello 數目稱為 hello 套用設定 toohello 節點中。</span><span class="sxs-lookup"><span data-stu-id="93fe4-210">hello number of DSC resources called in hello configuration applied toohello node.</span></span> |
| <span data-ttu-id="93fe4-211">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="93fe4-211">SourceSystem</span></span> | <span data-ttu-id="93fe4-212">記錄分析收集 hello 資料的方式。</span><span class="sxs-lookup"><span data-stu-id="93fe4-212">How Log Analytics collected hello data.</span></span> <span data-ttu-id="93fe4-213">針對 Azure 診斷，一律為 Azure 。</span><span class="sxs-lookup"><span data-stu-id="93fe4-213">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="93fe4-214">ResourceId</span><span class="sxs-lookup"><span data-stu-id="93fe4-214">ResourceId</span></span> |<span data-ttu-id="93fe4-215">指定 hello Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="93fe4-215">Specifies hello Azure Automation account.</span></span> |
| <span data-ttu-id="93fe4-216">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="93fe4-216">ResultDescription</span></span> | <span data-ttu-id="93fe4-217">hello 描述這項作業。</span><span class="sxs-lookup"><span data-stu-id="93fe4-217">hello description for this operation.</span></span> |
| <span data-ttu-id="93fe4-218">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="93fe4-218">SubscriptionId</span></span> | <span data-ttu-id="93fe4-219">hello hello 自動化帳戶的 Azure 訂閱識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-219">hello Azure subscription Id (GUID) for hello Automation account.</span></span> |
| <span data-ttu-id="93fe4-220">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="93fe4-220">ResourceGroup</span></span> | <span data-ttu-id="93fe4-221">Hello 自動化帳戶 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-221">Name of hello resource group for hello Automation account.</span></span> |
| <span data-ttu-id="93fe4-222">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="93fe4-222">ResourceProvider</span></span> | <span data-ttu-id="93fe4-223">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="93fe4-223">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="93fe4-224">ResourceType</span><span class="sxs-lookup"><span data-stu-id="93fe4-224">ResourceType</span></span> | <span data-ttu-id="93fe4-225">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="93fe4-225">AUTOMATIONACCOUNTS</span></span> |
| <span data-ttu-id="93fe4-226">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="93fe4-226">CorrelationId</span></span> |<span data-ttu-id="93fe4-227">為 hello hello 符合性報告的相互關聯識別碼的 GUID。</span><span class="sxs-lookup"><span data-stu-id="93fe4-227">GUID that is hello Correlation Id of hello compliance report.</span></span> |

### <a name="dscresourcestatusdata"></a><span data-ttu-id="93fe4-228">DscResourceStatusData</span><span class="sxs-lookup"><span data-stu-id="93fe4-228">DscResourceStatusData</span></span>

| <span data-ttu-id="93fe4-229">屬性</span><span class="sxs-lookup"><span data-stu-id="93fe4-229">Property</span></span> | <span data-ttu-id="93fe4-230">說明</span><span class="sxs-lookup"><span data-stu-id="93fe4-230">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93fe4-231">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="93fe4-231">TimeGenerated</span></span> |<span data-ttu-id="93fe4-232">日期和時間執行 hello 相容性檢查的時間。</span><span class="sxs-lookup"><span data-stu-id="93fe4-232">Date and time when hello compliance check ran.</span></span> |
| <span data-ttu-id="93fe4-233">OperationName</span><span class="sxs-lookup"><span data-stu-id="93fe4-233">OperationName</span></span> |<span data-ttu-id="93fe4-234">DscResourceStatusData</span><span class="sxs-lookup"><span data-stu-id="93fe4-234">DscResourceStatusData</span></span>|
| <span data-ttu-id="93fe4-235">ResultType</span><span class="sxs-lookup"><span data-stu-id="93fe4-235">ResultType</span></span> |<span data-ttu-id="93fe4-236">Hello 資源是否相容。</span><span class="sxs-lookup"><span data-stu-id="93fe4-236">Whether hello resource is compliant.</span></span> |
| <span data-ttu-id="93fe4-237">NodeName_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-237">NodeName_s</span></span> |<span data-ttu-id="93fe4-238">hello hello 受管理的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-238">hello name of hello managed node.</span></span> |
| <span data-ttu-id="93fe4-239">類別</span><span class="sxs-lookup"><span data-stu-id="93fe4-239">Category</span></span> | <span data-ttu-id="93fe4-240">DscNodeStatus</span><span class="sxs-lookup"><span data-stu-id="93fe4-240">DscNodeStatus</span></span> |
| <span data-ttu-id="93fe4-241">資源</span><span class="sxs-lookup"><span data-stu-id="93fe4-241">Resource</span></span> | <span data-ttu-id="93fe4-242">hello hello Azure 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-242">hello name of hello Azure Automation account.</span></span> |
| <span data-ttu-id="93fe4-243">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="93fe4-243">Tenant_g</span></span> | <span data-ttu-id="93fe4-244">識別 hello 呼叫端的 hello 租用戶的 GUID。</span><span class="sxs-lookup"><span data-stu-id="93fe4-244">GUID that identifies hello tenant for hello Caller.</span></span> |
| <span data-ttu-id="93fe4-245">NodeId_g</span><span class="sxs-lookup"><span data-stu-id="93fe4-245">NodeId_g</span></span> |<span data-ttu-id="93fe4-246">GUID，識別 hello 受管理的節點。</span><span class="sxs-lookup"><span data-stu-id="93fe4-246">GUID that identifies hello managed node.</span></span> |
| <span data-ttu-id="93fe4-247">DscReportId_g</span><span class="sxs-lookup"><span data-stu-id="93fe4-247">DscReportId_g</span></span> |<span data-ttu-id="93fe4-248">GUID，識別 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="93fe4-248">GUID that identifies hello report.</span></span> |
| <span data-ttu-id="93fe4-249">DscResourceId_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-249">DscResourceId_s</span></span> |<span data-ttu-id="93fe4-250">hello hello DSC 資源執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-250">hello name of hello DSC resource instance.</span></span> |
| <span data-ttu-id="93fe4-251">DscResourceName_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-251">DscResourceName_s</span></span> |<span data-ttu-id="93fe4-252">hello hello DSC 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-252">hello name of hello DSC resource.</span></span> |
| <span data-ttu-id="93fe4-253">DscResourceStatus_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-253">DscResourceStatus_s</span></span> |<span data-ttu-id="93fe4-254">Hello DSC 資源是否處於相容性。</span><span class="sxs-lookup"><span data-stu-id="93fe4-254">Whether hello DSC resource is in compliance.</span></span> |
| <span data-ttu-id="93fe4-255">DscModuleName_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-255">DscModuleName_s</span></span> |<span data-ttu-id="93fe4-256">hello hello PowerShell 模組包含 hello DSC 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-256">hello name of hello PowerShell module that contains hello DSC resource.</span></span> |
| <span data-ttu-id="93fe4-257">DscModuleVersion_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-257">DscModuleVersion_s</span></span> |<span data-ttu-id="93fe4-258">hello hello PowerShell 模組包含 hello DSC 資源版本。</span><span class="sxs-lookup"><span data-stu-id="93fe4-258">hello version of hello PowerShell module that contains hello DSC resource.</span></span> |
| <span data-ttu-id="93fe4-259">DscConfigurationName_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-259">DscConfigurationName_s</span></span> |<span data-ttu-id="93fe4-260">hello hello 組態名稱套用 toohello 節點。</span><span class="sxs-lookup"><span data-stu-id="93fe4-260">hello name of hello configuration applied toohello node.</span></span> |
| <span data-ttu-id="93fe4-261">ErrorCode_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-261">ErrorCode_s</span></span> | <span data-ttu-id="93fe4-262">hello 錯誤碼 hello 資源失敗。</span><span class="sxs-lookup"><span data-stu-id="93fe4-262">hello error code if hello resource failed.</span></span> |
| <span data-ttu-id="93fe4-263">ErrorMessage_s</span><span class="sxs-lookup"><span data-stu-id="93fe4-263">ErrorMessage_s</span></span> |<span data-ttu-id="93fe4-264">hello 的錯誤訊息如果 hello 資源失敗。</span><span class="sxs-lookup"><span data-stu-id="93fe4-264">hello error message if hello resource failed.</span></span> |
| <span data-ttu-id="93fe4-265">DscResourceDuration_d</span><span class="sxs-lookup"><span data-stu-id="93fe4-265">DscResourceDuration_d</span></span> |<span data-ttu-id="93fe4-266">hello 時間 （秒），執行 hello DSC 資源。</span><span class="sxs-lookup"><span data-stu-id="93fe4-266">hello time, in seconds, that hello DSC resource ran.</span></span> |
| <span data-ttu-id="93fe4-267">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="93fe4-267">SourceSystem</span></span> | <span data-ttu-id="93fe4-268">記錄分析收集 hello 資料的方式。</span><span class="sxs-lookup"><span data-stu-id="93fe4-268">How Log Analytics collected hello data.</span></span> <span data-ttu-id="93fe4-269">針對 Azure 診斷，一律為 Azure 。</span><span class="sxs-lookup"><span data-stu-id="93fe4-269">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="93fe4-270">ResourceId</span><span class="sxs-lookup"><span data-stu-id="93fe4-270">ResourceId</span></span> |<span data-ttu-id="93fe4-271">指定 hello Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="93fe4-271">Specifies hello Azure Automation account.</span></span> |
| <span data-ttu-id="93fe4-272">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="93fe4-272">ResultDescription</span></span> | <span data-ttu-id="93fe4-273">hello 描述這項作業。</span><span class="sxs-lookup"><span data-stu-id="93fe4-273">hello description for this operation.</span></span> |
| <span data-ttu-id="93fe4-274">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="93fe4-274">SubscriptionId</span></span> | <span data-ttu-id="93fe4-275">hello hello 自動化帳戶的 Azure 訂閱識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="93fe4-275">hello Azure subscription Id (GUID) for hello Automation account.</span></span> |
| <span data-ttu-id="93fe4-276">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="93fe4-276">ResourceGroup</span></span> | <span data-ttu-id="93fe4-277">Hello 自動化帳戶 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="93fe4-277">Name of hello resource group for hello Automation account.</span></span> |
| <span data-ttu-id="93fe4-278">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="93fe4-278">ResourceProvider</span></span> | <span data-ttu-id="93fe4-279">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="93fe4-279">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="93fe4-280">ResourceType</span><span class="sxs-lookup"><span data-stu-id="93fe4-280">ResourceType</span></span> | <span data-ttu-id="93fe4-281">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="93fe4-281">AUTOMATIONACCOUNTS</span></span> |
| <span data-ttu-id="93fe4-282">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="93fe4-282">CorrelationId</span></span> |<span data-ttu-id="93fe4-283">為 hello hello 符合性報告的相互關聯識別碼的 GUID。</span><span class="sxs-lookup"><span data-stu-id="93fe4-283">GUID that is hello Correlation Id of hello compliance report.</span></span> |

## <a name="summary"></a><span data-ttu-id="93fe4-284">摘要</span><span class="sxs-lookup"><span data-stu-id="93fe4-284">Summary</span></span>

<span data-ttu-id="93fe4-285">藉由傳送您的自動化 DSC 資料 tooLog 分析，您可以取得更深入 hello 由您 Automation DSC 的節點狀態：</span><span class="sxs-lookup"><span data-stu-id="93fe4-285">By sending your Automation DSC data tooLog Analytics, you can get better insight into hello status of your Automation DSC nodes by:</span></span>

* <span data-ttu-id="93fe4-286">設定警示 toonotify 您發生問題時</span><span class="sxs-lookup"><span data-stu-id="93fe4-286">Setting up alerts toonotify you when there is an issue</span></span>
* <span data-ttu-id="93fe4-287">使用自訂檢視和搜尋查詢 toovisualize 您 runbook 結果、 runbook 工作狀態、 和其他相關的主要指標或度量。</span><span class="sxs-lookup"><span data-stu-id="93fe4-287">Using custom views and search queries toovisualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="93fe4-288">記錄分析會提供更大的操作的可見性 tooyour Automation DSC 資料，而且可以更快速地協助位址事件。</span><span class="sxs-lookup"><span data-stu-id="93fe4-288">Log Analytics provides greater operational visibility tooyour Automation DSC data and can help address incidents more quickly.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="93fe4-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93fe4-289">Next steps</span></span>

* <span data-ttu-id="93fe4-290">toolearn 有關 tooconstruct 不同的搜尋查詢，並檢閱 hello Automation DSC 的詳細資訊，記錄和記錄分析，請參閱[中記錄分析記錄搜尋](../log-analytics/log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="93fe4-290">toolearn more about how tooconstruct different search queries and review hello Automation DSC logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="93fe4-291">toolearn 進一步了解使用 Azure 自動化 DSC，請參閱[開始使用 Azure 自動化 DSC](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="93fe4-291">toolearn more about using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="93fe4-292">toolearn 深入了解 OMS 記錄分析和資料集合來源，請參閱[收集 Azure 儲存體中的資料記錄分析概觀](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="93fe4-292">toolearn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>

