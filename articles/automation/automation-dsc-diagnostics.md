---
title: "將 Azure Automation DSC 報表資料轉送到 OMS Log Analytics | Microsoft Docs"
description: "這篇文章示範如何將期望的狀態設定 (DSC) 報表資料傳送到 Microsoft Operations Management Suite Log Analytics，以提供額外的深入解析和管理。"
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
ms.openlocfilehash: 316031c5297a0201c8db4a9e177298c78962c673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-to-oms-log-analytics"></a><span data-ttu-id="544aa-103">將 Azure Automation DSC 報表資料轉送到 OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="544aa-103">Forward Azure Automation DSC reporting data to OMS Log Analytics</span></span>

<span data-ttu-id="544aa-104">自動化可以將 DSC 節點狀態資料傳送到您的 Microsoft Operations Management Suite (OMS) Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="544aa-104">Automation can send DSC node status data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  
<span data-ttu-id="544aa-105">節點以及節點設定中個別 DSC 資源的合規性狀態會顯示在 Azure 入口網站中，或使用 PowerShell 顯示。</span><span class="sxs-lookup"><span data-stu-id="544aa-105">Compliance status is visible in the Azure portal, or with PowerShell, for nodes and for individual DSC resources in node configurations.</span></span> <span data-ttu-id="544aa-106">透過 Log Analytics，您可以：</span><span class="sxs-lookup"><span data-stu-id="544aa-106">With Log Analytics you can:</span></span>

* <span data-ttu-id="544aa-107">取得受管理節點與個別資源的合規性資訊</span><span class="sxs-lookup"><span data-stu-id="544aa-107">Get compliance information for managed nodes and individual resources</span></span>
* <span data-ttu-id="544aa-108">根據合規性狀態觸發電子郵件或警示</span><span class="sxs-lookup"><span data-stu-id="544aa-108">Trigger an email or alert based on compliance status</span></span>
* <span data-ttu-id="544aa-109">撰寫受管理節點之間的進階查詢</span><span class="sxs-lookup"><span data-stu-id="544aa-109">Write advanced queries across your managed nodes</span></span>
* <span data-ttu-id="544aa-110">相互關聯自動化帳戶之間的合規性狀態</span><span class="sxs-lookup"><span data-stu-id="544aa-110">Correlate compliance status across Automation accounts</span></span>
* <span data-ttu-id="544aa-111">以視覺化方式呈現一段時間的合規性歷程記錄</span><span class="sxs-lookup"><span data-stu-id="544aa-111">Visualize your node compliance history over time</span></span>

## <a name="prerequisites"></a><span data-ttu-id="544aa-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="544aa-112">Prerequisites</span></span>

<span data-ttu-id="544aa-113">若要開始將 Automation DSC 報表傳送到 Log Analytics，您需要：</span><span class="sxs-lookup"><span data-stu-id="544aa-113">To start sending your Automation DSC reports to Log Analytics, you need:</span></span>

* <span data-ttu-id="544aa-114">2016 年 11 月或更新版本的 [Azure PowerShell](/powershell/azure/overview) (v2.3.0)。</span><span class="sxs-lookup"><span data-stu-id="544aa-114">The November 2016 or later release of [Azure PowerShell](/powershell/azure/overview) (v2.3.0).</span></span>
* <span data-ttu-id="544aa-115">Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="544aa-115">An Azure Automation account.</span></span> <span data-ttu-id="544aa-116">如需詳細資訊，請參閱[開始使用 Azure 自動化](automation-offering-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="544aa-116">For more information, see [Getting Started with Azure Automation](automation-offering-get-started.md)</span></span>
* <span data-ttu-id="544aa-117">提供 [自動化與控制] 服務的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="544aa-117">A Log Analytics workspace with an **Automation & Control** service offering.</span></span> <span data-ttu-id="544aa-118">如需詳細資訊，請參閱[開始使用 Log Analytics](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="544aa-118">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span>
* <span data-ttu-id="544aa-119">至少一個 Azure Automation DSC 節點。</span><span class="sxs-lookup"><span data-stu-id="544aa-119">At least one Azure Automation DSC node.</span></span> <span data-ttu-id="544aa-120">如需詳細資訊，請參閱[將機器上架交由 Azure Automation DSC 管理](automation-dsc-onboarding.md)。</span><span class="sxs-lookup"><span data-stu-id="544aa-120">For more information, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span> 

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="544aa-121">設定與 Log Analytics 整合</span><span class="sxs-lookup"><span data-stu-id="544aa-121">Set up integration with Log Analytics</span></span>

<span data-ttu-id="544aa-122">若要開始從 Azure Automation DSC 將資料匯入 Log Analytics，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="544aa-122">To begin importing data from Azure Automation DSC into Log Analytics, complete the following steps:</span></span>

1. <span data-ttu-id="544aa-123">在 PowerShell 中登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="544aa-123">Log in to your Azure account in PowerShell.</span></span> <span data-ttu-id="544aa-124">請參閱[使用 Azure PowerShell 登入](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)</span><span class="sxs-lookup"><span data-stu-id="544aa-124">See [Log in with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)</span></span>
1. <span data-ttu-id="544aa-125">執行下列 PowerShell 命令以取得自動化帳戶的 _ResourceId_：(如有多個自動化帳戶，請選擇您想要設定的帳戶 _ResourceID_)。</span><span class="sxs-lookup"><span data-stu-id="544aa-125">Get the _ResourceId_ of your automation account by running the following PowerShell command: (if you have more than one automation account, choose the _ResourceID_ for the account you want to configure).</span></span>

  ```powershell
  # Find the ResourceId for the Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. <span data-ttu-id="544aa-126">執行下列 PowerShell 命令以取得 Log Analytics 工作區的 _ResourceId_：(如有多個工作區，請選擇您想要設定的工作區 _ResourceID_)。</span><span class="sxs-lookup"><span data-stu-id="544aa-126">Get the _ResourceId_ of your Log Analytics workspace by running the following PowerShell command: (if you have more than one workspace, choose the _ResourceID_ for the workspace you want to configure).</span></span>

  ```powershell
  # Find the ResourceId for the Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. <span data-ttu-id="544aa-127">執行下列 PowerShell 命令，以前述各步驟的 _ResourceId_ 值取代 `<AutomationResourceId>` 和 `<WorkspaceResourceId>`：</span><span class="sxs-lookup"><span data-stu-id="544aa-127">Run the following PowerShell command, replacing `<AutomationResourceId>` and `<WorkspaceResourceId>` with the _ResourceId_ values from each of the previous steps:</span></span>

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

<span data-ttu-id="544aa-128">如果您想要停止從 Azure Automation DSC 將資料匯入 Log Analytics，請執行下列 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="544aa-128">If you want to stop importing data from Azure Automation DSC into Log Analytics, run the following PowerShell command.</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-the-dsc-logs"></a><span data-ttu-id="544aa-129">檢視 DSC 記錄檔</span><span class="sxs-lookup"><span data-stu-id="544aa-129">View the DSC logs</span></span>

<span data-ttu-id="544aa-130">設定 Automation DSC 資料與 Log Analytics 的整合後，自動化帳戶的 [DSC 節點] 刀鋒視窗中就會出現 [記錄搜尋] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="544aa-130">After you set up integration with Log Analytics for your Automation DSC data, a **Log search** button will appear on the **DSC Nodes** blade of your automation account.</span></span> <span data-ttu-id="544aa-131">按一下 [記錄搜尋] 按鈕以檢視 DSC 節點資料的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="544aa-131">Click the **Log Search** button to view the logs for DSC node data.</span></span>

![記錄搜尋按鈕](media/automation-dsc-diagnostics/log-search-button.png)

<span data-ttu-id="544aa-133">[記錄搜尋] 刀鋒視窗隨即開啟，而且您會在套用到該節點的節點設定中，看到每個 DSC 節點呼叫 **DscNodeStatusData** 作業，和每個 [DSC 資源](https://msdn.microsoft.com/powershell/dsc/resources)呼叫 **DscResourceStatusData** 作業。</span><span class="sxs-lookup"><span data-stu-id="544aa-133">The **Log Search** blade opens, and you see a **DscNodeStatusData** operation for each DSC node, and a **DscResourceStatusData** operation for each [DSC resource](https://msdn.microsoft.com/powershell/dsc/resources) called in the Node configuration applied to that node.</span></span>

<span data-ttu-id="544aa-134">**DscResourceStatusData** 作業包含所有失敗 DSC 資源的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="544aa-134">The **DscResourceStatusData** operation contains error information for any DSC resources that failed.</span></span>

<span data-ttu-id="544aa-135">按一下清單中的每項作業可查看該作業的資料。</span><span class="sxs-lookup"><span data-stu-id="544aa-135">Click each operation in the list to see the data for that operation.</span></span>

<span data-ttu-id="544aa-136">您也可以搜尋 Log Analytics 來檢視記錄檔。</span><span class="sxs-lookup"><span data-stu-id="544aa-136">You can also view the logs by [searching in Log Analytics.</span></span> <span data-ttu-id="544aa-137">請參閱[使用記錄搜尋尋找資料](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="544aa-137">See [Find data using log searches](../log-analytics/log-analytics-log-searches.md).</span></span>
<span data-ttu-id="544aa-138">鍵入下列查詢來尋找 DSC 記錄：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`</span><span class="sxs-lookup"><span data-stu-id="544aa-138">Type the following query to find your DSC logs: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`</span></span>

<span data-ttu-id="544aa-139">您也可以依作業名稱縮小查詢範圍。</span><span class="sxs-lookup"><span data-stu-id="544aa-139">You can also narrow the query by the operation name.</span></span> <span data-ttu-id="544aa-140">例如：\`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"</span><span class="sxs-lookup"><span data-stu-id="544aa-140">For example: \`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"</span></span>

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a><span data-ttu-id="544aa-141">DSC 合規性檢查失敗時傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="544aa-141">Send an email when a DSC compliance check fails</span></span>

<span data-ttu-id="544aa-142">我們最常從客戶收到的其中一個問題，便是希望系統能在 DSC 設定發生問題時，傳送電子郵件或簡訊通知他們。</span><span class="sxs-lookup"><span data-stu-id="544aa-142">One of our top customer requests is for the ability to send an email or a text when something goes wrong with a DSC configuration.</span></span>   

<span data-ttu-id="544aa-143">若要建立警示規則，首先針對應叫用警示的 DSC 報表記錄，建立記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="544aa-143">To create an alert rule, you start by creating a log search for the DSC report records that should invoke the alert.</span></span>  <span data-ttu-id="544aa-144">按一下 [警示] 按鈕，以建立並設定警示規則。</span><span class="sxs-lookup"><span data-stu-id="544aa-144">Click the **Alert** button to create and configure the alert rule.</span></span>

1. <span data-ttu-id="544aa-145">從 [Log Analytics 概觀] 頁面，按一下 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="544aa-145">From the Log Analytics Overview page, click **Log Search**.</span></span>
1. <span data-ttu-id="544aa-146">在查詢欄位中鍵入下列搜尋內容來為您的警示建立記錄搜尋查詢：`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`。</span><span class="sxs-lookup"><span data-stu-id="544aa-146">Create a log search query for your alert by typing the following search into the query field:  `Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`</span></span>

  <span data-ttu-id="544aa-147">如果您已將來自多個自動化帳戶或訂用帳戶的記錄設定到您的工作區，就能依訂用帳戶或自動化帳戶來將警示分組。</span><span class="sxs-lookup"><span data-stu-id="544aa-147">If you have set up logs from more than one Automation account or subscription to your workspace, you can group your alerts by subscription and Automation account.</span></span>  
  <span data-ttu-id="544aa-148">自動化帳戶名稱可以衍生自 DscNodeStatusData 搜尋的 [資源] 欄位。</span><span class="sxs-lookup"><span data-stu-id="544aa-148">Automation account name can be derived from the Resource field in the search of DscNodeStatusData.</span></span>  
1. <span data-ttu-id="544aa-149">若要開啟 [新增警示規則] 畫面，按一下頁面頂端的 [警示]。</span><span class="sxs-lookup"><span data-stu-id="544aa-149">To open the **Add Alert Rule** screen, click **Alert** at the top of the page.</span></span> <span data-ttu-id="544aa-150">如需設定警示選項的詳細資訊，請參閱 [Log Analytics 中的警示](../log-analytics/log-analytics-alerts.md#alert-rules)。</span><span class="sxs-lookup"><span data-stu-id="544aa-150">For more information on the options to configure the alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-failed-dsc-resources-across-all-nodes"></a><span data-ttu-id="544aa-151">在所有節點間尋找失敗的 DSC 資源</span><span class="sxs-lookup"><span data-stu-id="544aa-151">Find failed DSC resources across all nodes</span></span>

<span data-ttu-id="544aa-152">使用 Log Analytics 的優點之一，是您可以在所有節點間搜尋失敗的檢查。</span><span class="sxs-lookup"><span data-stu-id="544aa-152">One advantage of using Log Analytics is that you can search for failed checks across nodes.</span></span>
<span data-ttu-id="544aa-153">尋找所有失敗的 DSC 資源執行個體。</span><span class="sxs-lookup"><span data-stu-id="544aa-153">To find all instances of DSC resources that failed.</span></span>

1. <span data-ttu-id="544aa-154">從 [Log Analytics 概觀] 頁面，按一下 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="544aa-154">From the Log Analytics Overview page, click **Log Search**.</span></span>
1. <span data-ttu-id="544aa-155">在查詢欄位中鍵入下列搜尋內容來為您的警示建立記錄搜尋查詢：`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`。</span><span class="sxs-lookup"><span data-stu-id="544aa-155">Create a log search query for your alert by typing the following search into the query field:  `Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`</span></span>

### <a name="view-historical-dsc-node-status"></a><span data-ttu-id="544aa-156">檢視歷程記錄 DSC 節點狀態</span><span class="sxs-lookup"><span data-stu-id="544aa-156">View historical DSC node status</span></span>

<span data-ttu-id="544aa-157">最後，您也許想要以視覺化方式呈現一段時間的 DSC 節點狀態歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="544aa-157">Finally, you may want to visualize your DSC node status history over time.</span></span>  
<span data-ttu-id="544aa-158">您可以使用此查詢來搜尋 DSC 節點狀態一段時間後的狀態。</span><span class="sxs-lookup"><span data-stu-id="544aa-158">You can use this query to search for the status of your DSC node status over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

<span data-ttu-id="544aa-159">這會顯示一段時間的節點狀態圖表。</span><span class="sxs-lookup"><span data-stu-id="544aa-159">This will display a chart of the node status over time.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="544aa-160">Log Analytics 記錄</span><span class="sxs-lookup"><span data-stu-id="544aa-160">Log Analytics records</span></span>

<span data-ttu-id="544aa-161">來自 Azure 自動化的診斷會在 Log Analytics 中建立兩種記錄類別。</span><span class="sxs-lookup"><span data-stu-id="544aa-161">Diagnostics from Azure Automation creates two categories of records in Log Analytics.</span></span>

### <a name="dscnodestatusdata"></a><span data-ttu-id="544aa-162">DscNodeStatusData</span><span class="sxs-lookup"><span data-stu-id="544aa-162">DscNodeStatusData</span></span>

| <span data-ttu-id="544aa-163">屬性</span><span class="sxs-lookup"><span data-stu-id="544aa-163">Property</span></span> | <span data-ttu-id="544aa-164">說明</span><span class="sxs-lookup"><span data-stu-id="544aa-164">Description</span></span> |
| --- | --- |
| <span data-ttu-id="544aa-165">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="544aa-165">TimeGenerated</span></span> |<span data-ttu-id="544aa-166">執行合規性檢查的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="544aa-166">Date and time when the compliance check ran.</span></span> |
| <span data-ttu-id="544aa-167">OperationName</span><span class="sxs-lookup"><span data-stu-id="544aa-167">OperationName</span></span> |<span data-ttu-id="544aa-168">DscNodeStatusData</span><span class="sxs-lookup"><span data-stu-id="544aa-168">DscNodeStatusData</span></span> |
| <span data-ttu-id="544aa-169">ResultType</span><span class="sxs-lookup"><span data-stu-id="544aa-169">ResultType</span></span> |<span data-ttu-id="544aa-170">節點是否符合規範。</span><span class="sxs-lookup"><span data-stu-id="544aa-170">Whether the node is compliant.</span></span> |
| <span data-ttu-id="544aa-171">NodeName_s</span><span class="sxs-lookup"><span data-stu-id="544aa-171">NodeName_s</span></span> |<span data-ttu-id="544aa-172">受管理的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-172">The name of the managed node.</span></span> |
| <span data-ttu-id="544aa-173">NodeComplianceStatus_s</span><span class="sxs-lookup"><span data-stu-id="544aa-173">NodeComplianceStatus_s</span></span> |<span data-ttu-id="544aa-174">節點是否符合規範。</span><span class="sxs-lookup"><span data-stu-id="544aa-174">Whether the node is compliant.</span></span> |
| <span data-ttu-id="544aa-175">DscReportStatus</span><span class="sxs-lookup"><span data-stu-id="544aa-175">DscReportStatus</span></span> |<span data-ttu-id="544aa-176">合規性檢查是否已順利執行。</span><span class="sxs-lookup"><span data-stu-id="544aa-176">Whether the compliance check ran successfully.</span></span> |
| <span data-ttu-id="544aa-177">ConfigurationMode</span><span class="sxs-lookup"><span data-stu-id="544aa-177">ConfigurationMode</span></span> | <span data-ttu-id="544aa-178">設定如何套用至節點。</span><span class="sxs-lookup"><span data-stu-id="544aa-178">How the configuration is applied to the node.</span></span> <span data-ttu-id="544aa-179">可能的值為 __"ApplyOnly"__、__"ApplyandMonitior"__ 和 __"ApplyandAutoCorrect"__。</span><span class="sxs-lookup"><span data-stu-id="544aa-179">Possible values are __"ApplyOnly"__,__"ApplyandMonitior"__, and __"ApplyandAutoCorrect"__.</span></span> <ul><li><span data-ttu-id="544aa-180">__ApplyOnly__：DSC 會套用設定但不執行任何進一步的動作，除非有新的設定發送到目標節點，或從伺服器提取新的設定時。</span><span class="sxs-lookup"><span data-stu-id="544aa-180">__ApplyOnly__: DSC applies the configuration and does nothing further unless a new configuration is pushed to the target node or when a new configuration is pulled from a server.</span></span> <span data-ttu-id="544aa-181">初始套用新的設定之後，DSC 不會檢查先前設定的狀態是否漂移。</span><span class="sxs-lookup"><span data-stu-id="544aa-181">After initial application of a new configuration, DSC does not check for drift from a previously configured state.</span></span> <span data-ttu-id="544aa-182">DSC 在 __ApplyOnly__ 生效之前會一直嘗試套用設定，直到成功為止。</span><span class="sxs-lookup"><span data-stu-id="544aa-182">DSC attempts to apply the configuration until it is successful before __ApplyOnly__ takes effect.</span></span> </li><li> <span data-ttu-id="544aa-183">__ApplyAndMonitor__：這是預設值。</span><span class="sxs-lookup"><span data-stu-id="544aa-183">__ApplyAndMonitor__: This is the default value.</span></span> <span data-ttu-id="544aa-184">LCM 會套用任何新的設定。</span><span class="sxs-lookup"><span data-stu-id="544aa-184">The LCM applies any new configurations.</span></span> <span data-ttu-id="544aa-185">初始套用新設定之後，如果目標節點從所需狀態漂移，DSC 會在記錄檔中報告差異。</span><span class="sxs-lookup"><span data-stu-id="544aa-185">After initial application of a new configuration, if the target node drifts from the desired state, DSC reports the discrepancy in logs.</span></span> <span data-ttu-id="544aa-186">DSC 在 __ApplyAndMonitor__ 生效之前會一直嘗試套用設定，直到成功為止。</span><span class="sxs-lookup"><span data-stu-id="544aa-186">DSC attempts to apply the configuration until it is successful before __ApplyAndMonitor__ takes effect.</span></span></li><li><span data-ttu-id="544aa-187">__ApplyAndAutoCorrect__：DSC 會套用任何新的設定。</span><span class="sxs-lookup"><span data-stu-id="544aa-187">__ApplyAndAutoCorrect__: DSC applies any new configurations.</span></span> <span data-ttu-id="544aa-188">初始套用新設定之後，如果目標節點從所需狀態漂移，DSC 會在記錄檔中報告差異，然後重新套用目前的設定。</span><span class="sxs-lookup"><span data-stu-id="544aa-188">After initial application of a new configuration, if the target node drifts from the desired state, DSC reports the discrepancy in logs, and then reapplies the current configuration.</span></span></li></ul> |
| <span data-ttu-id="544aa-189">HostName_s</span><span class="sxs-lookup"><span data-stu-id="544aa-189">HostName_s</span></span> | <span data-ttu-id="544aa-190">受管理的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-190">The name of the managed node.</span></span> |
| <span data-ttu-id="544aa-191">IPAddress</span><span class="sxs-lookup"><span data-stu-id="544aa-191">IPAddress</span></span> | <span data-ttu-id="544aa-192">受管理節點的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="544aa-192">The IPv4 address of the managed node.</span></span> |
| <span data-ttu-id="544aa-193">類別</span><span class="sxs-lookup"><span data-stu-id="544aa-193">Category</span></span> | <span data-ttu-id="544aa-194">DscNodeStatus</span><span class="sxs-lookup"><span data-stu-id="544aa-194">DscNodeStatus</span></span> |
| <span data-ttu-id="544aa-195">資源</span><span class="sxs-lookup"><span data-stu-id="544aa-195">Resource</span></span> | <span data-ttu-id="544aa-196">Azure 自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-196">The name of the Azure Automation account.</span></span> |
| <span data-ttu-id="544aa-197">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="544aa-197">Tenant_g</span></span> | <span data-ttu-id="544aa-198">識別呼叫端租用戶的 GUID。</span><span class="sxs-lookup"><span data-stu-id="544aa-198">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="544aa-199">NodeId_g</span><span class="sxs-lookup"><span data-stu-id="544aa-199">NodeId_g</span></span> |<span data-ttu-id="544aa-200">識別受管理節點的 GUID。</span><span class="sxs-lookup"><span data-stu-id="544aa-200">GUID that identifies the managed node.</span></span> |
| <span data-ttu-id="544aa-201">DscReportId_g</span><span class="sxs-lookup"><span data-stu-id="544aa-201">DscReportId_g</span></span> |<span data-ttu-id="544aa-202">識別報表的 GUID。</span><span class="sxs-lookup"><span data-stu-id="544aa-202">GUID that identifies the report.</span></span> |
| <span data-ttu-id="544aa-203">LastSeenTime_t</span><span class="sxs-lookup"><span data-stu-id="544aa-203">LastSeenTime_t</span></span> |<span data-ttu-id="544aa-204">上一次檢視報表的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="544aa-204">Date and time when the report was last viewed.</span></span> |
| <span data-ttu-id="544aa-205">ReportStartTime_t</span><span class="sxs-lookup"><span data-stu-id="544aa-205">ReportStartTime_t</span></span> |<span data-ttu-id="544aa-206">報表開始的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="544aa-206">Date and time when the report was started.</span></span> |
| <span data-ttu-id="544aa-207">ReportEndTime_t</span><span class="sxs-lookup"><span data-stu-id="544aa-207">ReportEndTime_t</span></span> |<span data-ttu-id="544aa-208">報表完成的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="544aa-208">Date and time when the report completed.</span></span> |
| <span data-ttu-id="544aa-209">NumberOfResources_d</span><span class="sxs-lookup"><span data-stu-id="544aa-209">NumberOfResources_d</span></span> |<span data-ttu-id="544aa-210">在節點套用的設定中呼叫的 DSC 資源數目。</span><span class="sxs-lookup"><span data-stu-id="544aa-210">The number of DSC resources called in the configuration applied to the node.</span></span> |
| <span data-ttu-id="544aa-211">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="544aa-211">SourceSystem</span></span> | <span data-ttu-id="544aa-212">Log Analytics 如何收集資料。</span><span class="sxs-lookup"><span data-stu-id="544aa-212">How Log Analytics collected the data.</span></span> <span data-ttu-id="544aa-213">針對 Azure 診斷，一律為 Azure 。</span><span class="sxs-lookup"><span data-stu-id="544aa-213">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="544aa-214">ResourceId</span><span class="sxs-lookup"><span data-stu-id="544aa-214">ResourceId</span></span> |<span data-ttu-id="544aa-215">指定 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="544aa-215">Specifies the Azure Automation account.</span></span> |
| <span data-ttu-id="544aa-216">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="544aa-216">ResultDescription</span></span> | <span data-ttu-id="544aa-217">此作業的描述。</span><span class="sxs-lookup"><span data-stu-id="544aa-217">The description for this operation.</span></span> |
| <span data-ttu-id="544aa-218">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="544aa-218">SubscriptionId</span></span> | <span data-ttu-id="544aa-219">自動化帳戶的 Azure 訂用帳戶識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="544aa-219">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="544aa-220">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="544aa-220">ResourceGroup</span></span> | <span data-ttu-id="544aa-221">自動化帳戶的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-221">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="544aa-222">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="544aa-222">ResourceProvider</span></span> | <span data-ttu-id="544aa-223">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="544aa-223">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="544aa-224">ResourceType</span><span class="sxs-lookup"><span data-stu-id="544aa-224">ResourceType</span></span> | <span data-ttu-id="544aa-225">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="544aa-225">AUTOMATIONACCOUNTS</span></span> |
| <span data-ttu-id="544aa-226">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="544aa-226">CorrelationId</span></span> |<span data-ttu-id="544aa-227">為更新狀態報告之相互關聯識別碼的 GUID。</span><span class="sxs-lookup"><span data-stu-id="544aa-227">GUID that is the Correlation Id of the compliance report.</span></span> |

### <a name="dscresourcestatusdata"></a><span data-ttu-id="544aa-228">DscResourceStatusData</span><span class="sxs-lookup"><span data-stu-id="544aa-228">DscResourceStatusData</span></span>

| <span data-ttu-id="544aa-229">屬性</span><span class="sxs-lookup"><span data-stu-id="544aa-229">Property</span></span> | <span data-ttu-id="544aa-230">說明</span><span class="sxs-lookup"><span data-stu-id="544aa-230">Description</span></span> |
| --- | --- |
| <span data-ttu-id="544aa-231">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="544aa-231">TimeGenerated</span></span> |<span data-ttu-id="544aa-232">執行合規性檢查的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="544aa-232">Date and time when the compliance check ran.</span></span> |
| <span data-ttu-id="544aa-233">OperationName</span><span class="sxs-lookup"><span data-stu-id="544aa-233">OperationName</span></span> |<span data-ttu-id="544aa-234">DscResourceStatusData</span><span class="sxs-lookup"><span data-stu-id="544aa-234">DscResourceStatusData</span></span>|
| <span data-ttu-id="544aa-235">ResultType</span><span class="sxs-lookup"><span data-stu-id="544aa-235">ResultType</span></span> |<span data-ttu-id="544aa-236">資源是否符合規範。</span><span class="sxs-lookup"><span data-stu-id="544aa-236">Whether the resource is compliant.</span></span> |
| <span data-ttu-id="544aa-237">NodeName_s</span><span class="sxs-lookup"><span data-stu-id="544aa-237">NodeName_s</span></span> |<span data-ttu-id="544aa-238">受管理的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-238">The name of the managed node.</span></span> |
| <span data-ttu-id="544aa-239">類別</span><span class="sxs-lookup"><span data-stu-id="544aa-239">Category</span></span> | <span data-ttu-id="544aa-240">DscNodeStatus</span><span class="sxs-lookup"><span data-stu-id="544aa-240">DscNodeStatus</span></span> |
| <span data-ttu-id="544aa-241">資源</span><span class="sxs-lookup"><span data-stu-id="544aa-241">Resource</span></span> | <span data-ttu-id="544aa-242">Azure 自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-242">The name of the Azure Automation account.</span></span> |
| <span data-ttu-id="544aa-243">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="544aa-243">Tenant_g</span></span> | <span data-ttu-id="544aa-244">識別呼叫端租用戶的 GUID。</span><span class="sxs-lookup"><span data-stu-id="544aa-244">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="544aa-245">NodeId_g</span><span class="sxs-lookup"><span data-stu-id="544aa-245">NodeId_g</span></span> |<span data-ttu-id="544aa-246">識別受管理節點的 GUID。</span><span class="sxs-lookup"><span data-stu-id="544aa-246">GUID that identifies the managed node.</span></span> |
| <span data-ttu-id="544aa-247">DscReportId_g</span><span class="sxs-lookup"><span data-stu-id="544aa-247">DscReportId_g</span></span> |<span data-ttu-id="544aa-248">識別報表的 GUID。</span><span class="sxs-lookup"><span data-stu-id="544aa-248">GUID that identifies the report.</span></span> |
| <span data-ttu-id="544aa-249">DscResourceId_s</span><span class="sxs-lookup"><span data-stu-id="544aa-249">DscResourceId_s</span></span> |<span data-ttu-id="544aa-250">DSC 資源執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-250">The name of the DSC resource instance.</span></span> |
| <span data-ttu-id="544aa-251">DscResourceName_s</span><span class="sxs-lookup"><span data-stu-id="544aa-251">DscResourceName_s</span></span> |<span data-ttu-id="544aa-252">DSC 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-252">The name of the DSC resource.</span></span> |
| <span data-ttu-id="544aa-253">DscResourceStatus_s</span><span class="sxs-lookup"><span data-stu-id="544aa-253">DscResourceStatus_s</span></span> |<span data-ttu-id="544aa-254">DSC 資源是否符合規範。</span><span class="sxs-lookup"><span data-stu-id="544aa-254">Whether the DSC resource is in compliance.</span></span> |
| <span data-ttu-id="544aa-255">DscModuleName_s</span><span class="sxs-lookup"><span data-stu-id="544aa-255">DscModuleName_s</span></span> |<span data-ttu-id="544aa-256">包含 DSC 資源的 PowerShell 模組名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-256">The name of the PowerShell module that contains the DSC resource.</span></span> |
| <span data-ttu-id="544aa-257">DscModuleVersion_s</span><span class="sxs-lookup"><span data-stu-id="544aa-257">DscModuleVersion_s</span></span> |<span data-ttu-id="544aa-258">包含 DSC 資源的 PowerShell 模組版本。</span><span class="sxs-lookup"><span data-stu-id="544aa-258">The version of the PowerShell module that contains the DSC resource.</span></span> |
| <span data-ttu-id="544aa-259">DscConfigurationName_s</span><span class="sxs-lookup"><span data-stu-id="544aa-259">DscConfigurationName_s</span></span> |<span data-ttu-id="544aa-260">節點套用的設定名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-260">The name of the configuration applied to the node.</span></span> |
| <span data-ttu-id="544aa-261">ErrorCode_s</span><span class="sxs-lookup"><span data-stu-id="544aa-261">ErrorCode_s</span></span> | <span data-ttu-id="544aa-262">資源失敗時的錯誤代碼。</span><span class="sxs-lookup"><span data-stu-id="544aa-262">The error code if the resource failed.</span></span> |
| <span data-ttu-id="544aa-263">ErrorMessage_s</span><span class="sxs-lookup"><span data-stu-id="544aa-263">ErrorMessage_s</span></span> |<span data-ttu-id="544aa-264">資源失敗時的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="544aa-264">The error message if the resource failed.</span></span> |
| <span data-ttu-id="544aa-265">DscResourceDuration_d</span><span class="sxs-lookup"><span data-stu-id="544aa-265">DscResourceDuration_d</span></span> |<span data-ttu-id="544aa-266">DSC 資源執行的時間，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="544aa-266">The time, in seconds, that the DSC resource ran.</span></span> |
| <span data-ttu-id="544aa-267">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="544aa-267">SourceSystem</span></span> | <span data-ttu-id="544aa-268">Log Analytics 如何收集資料。</span><span class="sxs-lookup"><span data-stu-id="544aa-268">How Log Analytics collected the data.</span></span> <span data-ttu-id="544aa-269">針對 Azure 診斷，一律為 Azure 。</span><span class="sxs-lookup"><span data-stu-id="544aa-269">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="544aa-270">ResourceId</span><span class="sxs-lookup"><span data-stu-id="544aa-270">ResourceId</span></span> |<span data-ttu-id="544aa-271">指定 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="544aa-271">Specifies the Azure Automation account.</span></span> |
| <span data-ttu-id="544aa-272">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="544aa-272">ResultDescription</span></span> | <span data-ttu-id="544aa-273">此作業的描述。</span><span class="sxs-lookup"><span data-stu-id="544aa-273">The description for this operation.</span></span> |
| <span data-ttu-id="544aa-274">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="544aa-274">SubscriptionId</span></span> | <span data-ttu-id="544aa-275">自動化帳戶的 Azure 訂用帳戶識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="544aa-275">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="544aa-276">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="544aa-276">ResourceGroup</span></span> | <span data-ttu-id="544aa-277">自動化帳戶的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="544aa-277">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="544aa-278">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="544aa-278">ResourceProvider</span></span> | <span data-ttu-id="544aa-279">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="544aa-279">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="544aa-280">ResourceType</span><span class="sxs-lookup"><span data-stu-id="544aa-280">ResourceType</span></span> | <span data-ttu-id="544aa-281">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="544aa-281">AUTOMATIONACCOUNTS</span></span> |
| <span data-ttu-id="544aa-282">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="544aa-282">CorrelationId</span></span> |<span data-ttu-id="544aa-283">為更新狀態報告之相互關聯識別碼的 GUID。</span><span class="sxs-lookup"><span data-stu-id="544aa-283">GUID that is the Correlation Id of the compliance report.</span></span> |

## <a name="summary"></a><span data-ttu-id="544aa-284">摘要</span><span class="sxs-lookup"><span data-stu-id="544aa-284">Summary</span></span>

<span data-ttu-id="544aa-285">只要將 Automation DSC 資料傳送到 Log Analytics，您就可以透過下列方式，更深入了解 Automation DSC 節點的狀態：</span><span class="sxs-lookup"><span data-stu-id="544aa-285">By sending your Automation DSC data to Log Analytics, you can get better insight into the status of your Automation DSC nodes by:</span></span>

* <span data-ttu-id="544aa-286">設定警示，在發生問題時通知您</span><span class="sxs-lookup"><span data-stu-id="544aa-286">Setting up alerts to notify you when there is an issue</span></span>
* <span data-ttu-id="544aa-287">使用自訂檢視和搜尋查詢，以視覺化方式檢視您的 Runbook 結果、Runbook 作業狀態，以及其他相關的關鍵指標或計量。</span><span class="sxs-lookup"><span data-stu-id="544aa-287">Using custom views and search queries to visualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="544aa-288">Log Analytics 可以為您的 Automation DSC 資料提供更高的操作可見性，有利於更快處理事件。</span><span class="sxs-lookup"><span data-stu-id="544aa-288">Log Analytics provides greater operational visibility to your Automation DSC data and can help address incidents more quickly.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="544aa-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="544aa-289">Next steps</span></span>

* <span data-ttu-id="544aa-290">若要深入了解如何建構不同的搜尋查詢，以及使用 Log Analytics 檢閱 Automation DSC 記錄檔，請參閱 [Log Analytics 中的記錄檔搜尋](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="544aa-290">To learn more about how to construct different search queries and review the Automation DSC logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="544aa-291">若要深入了解使用 Azure Automation DSC，請參閱[開始使用 Azure Automation DSC](automation-dsc-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="544aa-291">To learn more about using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="544aa-292">若要深入了解 OMS Log Analytics 和資料收集來源，請參閱 [在 Log Analytics 中收集 Azure 儲存體資料概觀](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="544aa-292">To learn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>

