---
title: "Azure 自動化工作資料 tooOMS 記錄分析 aaaForward |Microsoft 文件"
description: "本文示範 toosend 工作狀態和 runbook 工作資料流 tooMicrosoft Operations Management Suite 記錄分析 toodeliver 其他深入資訊和管理。"
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a><span data-ttu-id="a153e-103">從自動化 tooLog 分析 (OMS) 轉送作業的狀態和作業資料流</span><span class="sxs-lookup"><span data-stu-id="a153e-103">Forward job status and job streams from Automation tooLog Analytics (OMS)</span></span>
<span data-ttu-id="a153e-104">自動化可以傳送 runbook 工作狀態和作業資料流 tooyour Microsoft Operations Management Suite (OMS) 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="a153e-104">Automation can send runbook job status and job streams tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  <span data-ttu-id="a153e-105">作業記錄和作業資料流會顯示在 hello Azure 入口網站，或使用 PowerShell，針對個別作業，而這可讓您 tooperform 簡單的調查。</span><span class="sxs-lookup"><span data-stu-id="a153e-105">Job logs and job streams are visible in hello Azure portal, or with PowerShell, for individual jobs and this allows you tooperform simple investigations.</span></span> <span data-ttu-id="a153e-106">現在透過 Log Analytics，您可以：</span><span class="sxs-lookup"><span data-stu-id="a153e-106">Now with Log Analytics you can:</span></span>

* <span data-ttu-id="a153e-107">針對自動化工作取得深入解析</span><span class="sxs-lookup"><span data-stu-id="a153e-107">Get insight on your Automation jobs</span></span>
* <span data-ttu-id="a153e-108">根據您的 Runbook 作業狀態 (例如已失敗或已暫停) 觸發電子郵件或警示</span><span class="sxs-lookup"><span data-stu-id="a153e-108">Trigger an email or alert based on your runbook job status (for example, failed or suspended)</span></span>
* <span data-ttu-id="a153e-109">撰寫工作資料流之間的進階查詢</span><span class="sxs-lookup"><span data-stu-id="a153e-109">Write advanced queries across your job streams</span></span>
* <span data-ttu-id="a153e-110">在自動化帳戶之間相互關聯工作</span><span class="sxs-lookup"><span data-stu-id="a153e-110">Correlate jobs across Automation accounts</span></span>
* <span data-ttu-id="a153e-111">視覺化一段時間的工作歷程記錄</span><span class="sxs-lookup"><span data-stu-id="a153e-111">Visualize your job history over time</span></span>     

## <a name="prerequisites-and-deployment-considerations"></a><span data-ttu-id="a153e-112">先決條件和部署考量</span><span class="sxs-lookup"><span data-stu-id="a153e-112">Prerequisites and deployment considerations</span></span>
<span data-ttu-id="a153e-113">傳送自動化 toostart 記錄 tooLog 分析，您需要：</span><span class="sxs-lookup"><span data-stu-id="a153e-113">toostart sending your Automation logs tooLog Analytics, you need:</span></span>

1. <span data-ttu-id="a153e-114">hello 2016 年 11 月版或更新版本的版本[Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0)。</span><span class="sxs-lookup"><span data-stu-id="a153e-114">hello November 2016 or later release of [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span></span>
2. <span data-ttu-id="a153e-115">Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="a153e-115">A Log Analytics workspace.</span></span> <span data-ttu-id="a153e-116">如需詳細資訊，請參閱[開始使用 Log Analytics](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a153e-116">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span> 
3. <span data-ttu-id="a153e-117">hello ResourceId Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="a153e-117">hello ResourceId for your Azure Automation account</span></span>

<span data-ttu-id="a153e-118">Azure 自動化帳戶，記錄分析工作區中，執行下列 PowerShell hello toofind hello ResourceId:</span><span class="sxs-lookup"><span data-stu-id="a153e-118">toofind hello ResourceId for your Azure Automation account and Log Analytics workspace, run hello following PowerShell:</span></span>

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

<span data-ttu-id="a153e-119">如果您有多個自動化帳戶，或工作區、 hello 輸出中的 hello 上述命令，尋找 hello*名稱*您需要 tooconfigure 並複製 hello 值*ResourceId*。</span><span class="sxs-lookup"><span data-stu-id="a153e-119">If you have multiple Automation accounts, or workspaces, in hello output of hello preceding commands, find hello *Name* you need tooconfigure and copy hello value for *ResourceId*.</span></span>

<span data-ttu-id="a153e-120">如果您需要 toofind hello*名稱*自動化帳戶、 在 hello Azure 入口網站選取自動化帳戶從 hello**自動化帳戶**刀鋒視窗，然後選取**的所有設定**.</span><span class="sxs-lookup"><span data-stu-id="a153e-120">If you need toofind hello *Name* of your Automation account, in hello Azure portal select your Automation account from hello **Automation account** blade and select **All settings**.</span></span>  <span data-ttu-id="a153e-121">從 hello**所有設定**刀鋒視窗底下**帳戶設定**選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="a153e-121">From hello **All settings** blade, under **Account Settings** select **Properties**.</span></span>  <span data-ttu-id="a153e-122">在 hello**屬性**刀鋒視窗中，您可以注意這些值。</span><span class="sxs-lookup"><span data-stu-id="a153e-122">In hello **Properties** blade, you can note these values.</span></span><br> <span data-ttu-id="a153e-123">![自動化帳戶屬性](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png)。</span><span class="sxs-lookup"><span data-stu-id="a153e-123">![Automation Account properties](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span></span>

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="a153e-124">設定與 Log Analytics 整合</span><span class="sxs-lookup"><span data-stu-id="a153e-124">Set up integration with Log Analytics</span></span>
1. <span data-ttu-id="a153e-125">在您的電腦上啟動**Windows PowerShell**從 hello**啟動**螢幕。</span><span class="sxs-lookup"><span data-stu-id="a153e-125">On your computer, start **Windows PowerShell** from hello **Start** screen.</span></span>  
2. <span data-ttu-id="a153e-126">複製並貼上 hello 下列 PowerShell，然後編輯 hello 的 hello 值`$workspaceId`和`$automationAccountId`。</span><span class="sxs-lookup"><span data-stu-id="a153e-126">Copy and paste hello following PowerShell, and edit hello value for hello `$workspaceId` and `$automationAccountId`.</span></span>  <span data-ttu-id="a153e-127">Hello`-Environment`參數，有效值為*AzureCloud*或*AzureUSGovernment*視您工作所在的 hello 雲端環境而定。</span><span class="sxs-lookup"><span data-stu-id="a153e-127">For hello `-Environment` parameter, valid values are *AzureCloud* or *AzureUSGovernment* depending on hello cloud environment you are working in.</span></span>     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

<span data-ttu-id="a153e-128">執行這個指令碼之後，您將會在寫入新 JobLogs 或 JobStreams 的 10 分鐘內，於 Log Analytics 中看見記錄。</span><span class="sxs-lookup"><span data-stu-id="a153e-128">After running this script, you will see records in Log Analytics within 10 minutes of new JobLogs or JobStreams being written.</span></span>

<span data-ttu-id="a153e-129">toosee hello 記錄檔，執行下列查詢在記錄分析記錄搜尋中的 hello:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="a153e-129">toosee hello logs, run hello following query in Log Analytics log search: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="verify-configuration"></a><span data-ttu-id="a153e-130">驗證組態</span><span class="sxs-lookup"><span data-stu-id="a153e-130">Verify configuration</span></span>
<span data-ttu-id="a153e-131">tooconfirm 傳送您的自動化帳戶記錄 tooyour 記錄分析工作區，請檢查診斷上使用下列 PowerShell hello hello 自動化帳戶已正確設定：</span><span class="sxs-lookup"><span data-stu-id="a153e-131">tooconfirm that your Automation account is sending logs tooyour Log Analytics workspace, check that diagnostics are set correctly on hello Automation account using hello following PowerShell:</span></span>

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

<span data-ttu-id="a153e-132">Hello 輸出中，請確定：</span><span class="sxs-lookup"><span data-stu-id="a153e-132">In hello output ensure that:</span></span>
+ <span data-ttu-id="a153e-133">在下*記錄*，hello 值*啟用*是*，則為 True*</span><span class="sxs-lookup"><span data-stu-id="a153e-133">Under *Logs*, hello value for *Enabled* is *True*</span></span>
+ <span data-ttu-id="a153e-134">hello 值*工作區識別碼*toohello ResourceId 記錄分析工作區的設定</span><span class="sxs-lookup"><span data-stu-id="a153e-134">hello value of *WorkspaceId* is set toohello ResourceId of your Log Analytics workspace</span></span>


## <a name="log-analytics-records"></a><span data-ttu-id="a153e-135">Log Analytics 記錄</span><span class="sxs-lookup"><span data-stu-id="a153e-135">Log Analytics records</span></span>
<span data-ttu-id="a153e-136">來自 Azure 自動化的診斷會在 Log Analytics 中建立兩種類型的記錄，並標記為 **Type=AzureDiagnostics**。</span><span class="sxs-lookup"><span data-stu-id="a153e-136">Diagnostics from Azure Automation creates two types of records in Log Analytics and are tagged as **Type=AzureDiagnostics**.</span></span>

### <a name="job-logs"></a><span data-ttu-id="a153e-137">作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="a153e-137">Job Logs</span></span>
| <span data-ttu-id="a153e-138">屬性</span><span class="sxs-lookup"><span data-stu-id="a153e-138">Property</span></span> | <span data-ttu-id="a153e-139">說明</span><span class="sxs-lookup"><span data-stu-id="a153e-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a153e-140">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a153e-140">TimeGenerated</span></span> |<span data-ttu-id="a153e-141">日期和時間 hello runbook 工作執行時。</span><span class="sxs-lookup"><span data-stu-id="a153e-141">Date and time when hello runbook job executed.</span></span> |
| <span data-ttu-id="a153e-142">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="a153e-142">RunbookName_s</span></span> |<span data-ttu-id="a153e-143">hello hello runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="a153e-143">hello name of hello runbook.</span></span> |
| <span data-ttu-id="a153e-144">Caller_s</span><span class="sxs-lookup"><span data-stu-id="a153e-144">Caller_s</span></span> |<span data-ttu-id="a153e-145">誰 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="a153e-145">Who initiated hello operation.</span></span>  <span data-ttu-id="a153e-146">可能的值為電子郵件地址或排程作業的系統。</span><span class="sxs-lookup"><span data-stu-id="a153e-146">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="a153e-147">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="a153e-147">Tenant_g</span></span> | <span data-ttu-id="a153e-148">識別 hello 呼叫端的 hello 租用戶的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a153e-148">GUID that identifies hello tenant for hello Caller.</span></span> |
| <span data-ttu-id="a153e-149">JobId_g</span><span class="sxs-lookup"><span data-stu-id="a153e-149">JobId_g</span></span> |<span data-ttu-id="a153e-150">為 hello 識別碼 hello runbook 工作的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a153e-150">GUID that is hello Id of hello runbook job.</span></span> |
| <span data-ttu-id="a153e-151">ResultType</span><span class="sxs-lookup"><span data-stu-id="a153e-151">ResultType</span></span> |<span data-ttu-id="a153e-152">hello hello runbook 工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="a153e-152">hello status of hello runbook job.</span></span>  <span data-ttu-id="a153e-153">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="a153e-153">Possible values are:</span></span><br><span data-ttu-id="a153e-154">- Started (已啟動)</span><span class="sxs-lookup"><span data-stu-id="a153e-154">- Started</span></span><br><span data-ttu-id="a153e-155">- Stopped (已停止)</span><span class="sxs-lookup"><span data-stu-id="a153e-155">- Stopped</span></span><br><span data-ttu-id="a153e-156">- Suspended (暫止)</span><span class="sxs-lookup"><span data-stu-id="a153e-156">- Suspended</span></span><br><span data-ttu-id="a153e-157">- Failed (失敗)</span><span class="sxs-lookup"><span data-stu-id="a153e-157">- Failed</span></span><br><span data-ttu-id="a153e-158">- Completed (已完成)</span><span class="sxs-lookup"><span data-stu-id="a153e-158">- Completed</span></span> |
| <span data-ttu-id="a153e-159">類別</span><span class="sxs-lookup"><span data-stu-id="a153e-159">Category</span></span> | <span data-ttu-id="a153e-160">Hello 的資料類型的分類。</span><span class="sxs-lookup"><span data-stu-id="a153e-160">Classification of hello type of data.</span></span>  <span data-ttu-id="a153e-161">自動化，hello 值為 JobLogs。</span><span class="sxs-lookup"><span data-stu-id="a153e-161">For Automation, hello value is JobLogs.</span></span> |
| <span data-ttu-id="a153e-162">OperationName</span><span class="sxs-lookup"><span data-stu-id="a153e-162">OperationName</span></span> | <span data-ttu-id="a153e-163">指定在 Azure 中執行作業的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="a153e-163">Specifies hello type of operation performed in Azure.</span></span>  <span data-ttu-id="a153e-164">自動化，hello 值會是工作。</span><span class="sxs-lookup"><span data-stu-id="a153e-164">For Automation, hello value is Job.</span></span> |
| <span data-ttu-id="a153e-165">資源</span><span class="sxs-lookup"><span data-stu-id="a153e-165">Resource</span></span> | <span data-ttu-id="a153e-166">Hello 自動化帳戶的名稱</span><span class="sxs-lookup"><span data-stu-id="a153e-166">Name of hello Automation account</span></span> |
| <span data-ttu-id="a153e-167">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a153e-167">SourceSystem</span></span> | <span data-ttu-id="a153e-168">記錄分析收集 hello 資料的方式。</span><span class="sxs-lookup"><span data-stu-id="a153e-168">How Log Analytics collected hello data.</span></span> <span data-ttu-id="a153e-169">針對 Azure 診斷，一律為 Azure 。</span><span class="sxs-lookup"><span data-stu-id="a153e-169">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="a153e-170">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="a153e-170">ResultDescription</span></span> |<span data-ttu-id="a153e-171">描述 hello runbook 工作的結果狀態。</span><span class="sxs-lookup"><span data-stu-id="a153e-171">Describes hello runbook job result state.</span></span>  <span data-ttu-id="a153e-172">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="a153e-172">Possible values are:</span></span><br><span data-ttu-id="a153e-173">- Job is started (工作已啟動)</span><span class="sxs-lookup"><span data-stu-id="a153e-173">- Job is started</span></span><br><span data-ttu-id="a153e-174">- Job Failed (工作失敗)</span><span class="sxs-lookup"><span data-stu-id="a153e-174">- Job Failed</span></span><br><span data-ttu-id="a153e-175">- Job Completed</span><span class="sxs-lookup"><span data-stu-id="a153e-175">- Job Completed</span></span> |
| <span data-ttu-id="a153e-176">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="a153e-176">CorrelationId</span></span> |<span data-ttu-id="a153e-177">為 hello 相互關聯識別碼 hello runbook 工作的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a153e-177">GUID that is hello Correlation Id of hello runbook job.</span></span> |
| <span data-ttu-id="a153e-178">ResourceId</span><span class="sxs-lookup"><span data-stu-id="a153e-178">ResourceId</span></span> |<span data-ttu-id="a153e-179">指定 hello runbook hello Azure 自動化帳戶資源的 id。</span><span class="sxs-lookup"><span data-stu-id="a153e-179">Specifies hello Azure Automation account resource id of hello runbook.</span></span> |
| <span data-ttu-id="a153e-180">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a153e-180">SubscriptionId</span></span> | <span data-ttu-id="a153e-181">hello hello 自動化帳戶的 Azure 訂閱識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="a153e-181">hello Azure subscription Id (GUID) for hello Automation account.</span></span> |
| <span data-ttu-id="a153e-182">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a153e-182">ResourceGroup</span></span> | <span data-ttu-id="a153e-183">Hello 自動化帳戶 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="a153e-183">Name of hello resource group for hello Automation account.</span></span> |
| <span data-ttu-id="a153e-184">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="a153e-184">ResourceProvider</span></span> | <span data-ttu-id="a153e-185">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="a153e-185">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="a153e-186">ResourceType</span><span class="sxs-lookup"><span data-stu-id="a153e-186">ResourceType</span></span> | <span data-ttu-id="a153e-187">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="a153e-187">AUTOMATIONACCOUNTS</span></span> |


### <a name="job-streams"></a><span data-ttu-id="a153e-188">作業串流</span><span class="sxs-lookup"><span data-stu-id="a153e-188">Job Streams</span></span>
| <span data-ttu-id="a153e-189">屬性</span><span class="sxs-lookup"><span data-stu-id="a153e-189">Property</span></span> | <span data-ttu-id="a153e-190">說明</span><span class="sxs-lookup"><span data-stu-id="a153e-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a153e-191">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a153e-191">TimeGenerated</span></span> |<span data-ttu-id="a153e-192">日期和時間 hello runbook 工作執行時。</span><span class="sxs-lookup"><span data-stu-id="a153e-192">Date and time when hello runbook job executed.</span></span> |
| <span data-ttu-id="a153e-193">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="a153e-193">RunbookName_s</span></span> |<span data-ttu-id="a153e-194">hello hello runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="a153e-194">hello name of hello runbook.</span></span> |
| <span data-ttu-id="a153e-195">Caller_s</span><span class="sxs-lookup"><span data-stu-id="a153e-195">Caller_s</span></span> |<span data-ttu-id="a153e-196">誰 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="a153e-196">Who initiated hello operation.</span></span>  <span data-ttu-id="a153e-197">可能的值為電子郵件地址或排程作業的系統。</span><span class="sxs-lookup"><span data-stu-id="a153e-197">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="a153e-198">StreamType_s</span><span class="sxs-lookup"><span data-stu-id="a153e-198">StreamType_s</span></span> |<span data-ttu-id="a153e-199">hello 工作資料流類型。</span><span class="sxs-lookup"><span data-stu-id="a153e-199">hello type of job stream.</span></span> <span data-ttu-id="a153e-200">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="a153e-200">Possible values are:</span></span><br><span data-ttu-id="a153e-201">-Progress (進度)</span><span class="sxs-lookup"><span data-stu-id="a153e-201">-Progress</span></span><br><span data-ttu-id="a153e-202">- Output (輸出)</span><span class="sxs-lookup"><span data-stu-id="a153e-202">- Output</span></span><br><span data-ttu-id="a153e-203">- Warning (警告)</span><span class="sxs-lookup"><span data-stu-id="a153e-203">- Warning</span></span><br><span data-ttu-id="a153e-204">- Error (錯誤)</span><span class="sxs-lookup"><span data-stu-id="a153e-204">- Error</span></span><br><span data-ttu-id="a153e-205">- Debug (偵錯)</span><span class="sxs-lookup"><span data-stu-id="a153e-205">- Debug</span></span><br><span data-ttu-id="a153e-206">- Verbose</span><span class="sxs-lookup"><span data-stu-id="a153e-206">- Verbose</span></span> |
| <span data-ttu-id="a153e-207">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="a153e-207">Tenant_g</span></span> | <span data-ttu-id="a153e-208">識別 hello 呼叫端的 hello 租用戶的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a153e-208">GUID that identifies hello tenant for hello Caller.</span></span> |
| <span data-ttu-id="a153e-209">JobId_g</span><span class="sxs-lookup"><span data-stu-id="a153e-209">JobId_g</span></span> |<span data-ttu-id="a153e-210">為 hello 識別碼 hello runbook 工作的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a153e-210">GUID that is hello Id of hello runbook job.</span></span> |
| <span data-ttu-id="a153e-211">ResultType</span><span class="sxs-lookup"><span data-stu-id="a153e-211">ResultType</span></span> |<span data-ttu-id="a153e-212">hello hello runbook 工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="a153e-212">hello status of hello runbook job.</span></span>  <span data-ttu-id="a153e-213">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="a153e-213">Possible values are:</span></span><br><span data-ttu-id="a153e-214">- In Progress</span><span class="sxs-lookup"><span data-stu-id="a153e-214">- In Progress</span></span> |
| <span data-ttu-id="a153e-215">類別</span><span class="sxs-lookup"><span data-stu-id="a153e-215">Category</span></span> | <span data-ttu-id="a153e-216">Hello 的資料類型的分類。</span><span class="sxs-lookup"><span data-stu-id="a153e-216">Classification of hello type of data.</span></span>  <span data-ttu-id="a153e-217">自動化，hello 值為 JobStreams。</span><span class="sxs-lookup"><span data-stu-id="a153e-217">For Automation, hello value is JobStreams.</span></span> |
| <span data-ttu-id="a153e-218">OperationName</span><span class="sxs-lookup"><span data-stu-id="a153e-218">OperationName</span></span> | <span data-ttu-id="a153e-219">指定在 Azure 中執行作業的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="a153e-219">Specifies hello type of operation performed in Azure.</span></span>  <span data-ttu-id="a153e-220">自動化，hello 值會是工作。</span><span class="sxs-lookup"><span data-stu-id="a153e-220">For Automation, hello value is Job.</span></span> |
| <span data-ttu-id="a153e-221">資源</span><span class="sxs-lookup"><span data-stu-id="a153e-221">Resource</span></span> | <span data-ttu-id="a153e-222">Hello 自動化帳戶的名稱</span><span class="sxs-lookup"><span data-stu-id="a153e-222">Name of hello Automation account</span></span> |
| <span data-ttu-id="a153e-223">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a153e-223">SourceSystem</span></span> | <span data-ttu-id="a153e-224">記錄分析收集 hello 資料的方式。</span><span class="sxs-lookup"><span data-stu-id="a153e-224">How Log Analytics collected hello data.</span></span> <span data-ttu-id="a153e-225">針對 Azure 診斷，一律為 Azure 。</span><span class="sxs-lookup"><span data-stu-id="a153e-225">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="a153e-226">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="a153e-226">ResultDescription</span></span> |<span data-ttu-id="a153e-227">包含從 hello runbook hello 輸出資料流。</span><span class="sxs-lookup"><span data-stu-id="a153e-227">Includes hello output stream from hello runbook.</span></span> |
| <span data-ttu-id="a153e-228">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="a153e-228">CorrelationId</span></span> |<span data-ttu-id="a153e-229">為 hello 相互關聯識別碼 hello runbook 工作的 GUID。</span><span class="sxs-lookup"><span data-stu-id="a153e-229">GUID that is hello Correlation Id of hello runbook job.</span></span> |
| <span data-ttu-id="a153e-230">ResourceId</span><span class="sxs-lookup"><span data-stu-id="a153e-230">ResourceId</span></span> |<span data-ttu-id="a153e-231">指定 hello runbook hello Azure 自動化帳戶資源的 id。</span><span class="sxs-lookup"><span data-stu-id="a153e-231">Specifies hello Azure Automation account resource id of hello runbook.</span></span> |
| <span data-ttu-id="a153e-232">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a153e-232">SubscriptionId</span></span> | <span data-ttu-id="a153e-233">hello hello 自動化帳戶的 Azure 訂閱識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="a153e-233">hello Azure subscription Id (GUID) for hello Automation account.</span></span> |
| <span data-ttu-id="a153e-234">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a153e-234">ResourceGroup</span></span> | <span data-ttu-id="a153e-235">Hello 自動化帳戶 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="a153e-235">Name of hello resource group for hello Automation account.</span></span> |
| <span data-ttu-id="a153e-236">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="a153e-236">ResourceProvider</span></span> | <span data-ttu-id="a153e-237">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="a153e-237">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="a153e-238">ResourceType</span><span class="sxs-lookup"><span data-stu-id="a153e-238">ResourceType</span></span> | <span data-ttu-id="a153e-239">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="a153e-239">AUTOMATIONACCOUNTS</span></span> |

## <a name="viewing-automation-logs-in-log-analytics"></a><span data-ttu-id="a153e-240">在 Log Analytics 中檢視自動化記錄檔</span><span class="sxs-lookup"><span data-stu-id="a153e-240">Viewing Automation Logs in Log Analytics</span></span>
<span data-ttu-id="a153e-241">既然您已經啟動傳送您的自動化作業記錄檔 tooLog 分析，我們來看看您可以使用達成這些記錄檔中記錄分析。</span><span class="sxs-lookup"><span data-stu-id="a153e-241">Now that you have started sending your Automation job logs tooLog Analytics, let’s see what you can do with these logs inside Log Analytics.</span></span>

<span data-ttu-id="a153e-242">toosee hello 記錄檔，執行下列查詢的 hello:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="a153e-242">toosee hello logs, run hello following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a><span data-ttu-id="a153e-243">在 Runbook 工作失敗或暫停時傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="a153e-243">Send an email when a runbook job fails or suspends</span></span>
<span data-ttu-id="a153e-244">其中一個最上層客戶要求，是 hello 能力 toosend 電子郵件或文字時出錯 runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="a153e-244">One of our top customer asks is for hello ability toosend an email or a text when something goes wrong with a runbook job.</span></span>   

<span data-ttu-id="a153e-245">toocreate 警示規則時，它會先建立 hello runbook 的記錄搜尋叫用 hello 警示的工作記錄。</span><span class="sxs-lookup"><span data-stu-id="a153e-245">toocreate an alert rule, you start by creating a log search for hello runbook job records that should invoke hello alert.</span></span>  <span data-ttu-id="a153e-246">按一下 hello**警示**按鈕 toocreate 及設定 hello 警示規則。</span><span class="sxs-lookup"><span data-stu-id="a153e-246">Click hello **Alert** button toocreate and configure hello alert rule.</span></span>

1. <span data-ttu-id="a153e-247">從 hello 記錄分析概觀] 頁面上，按一下 [**記錄搜尋**。</span><span class="sxs-lookup"><span data-stu-id="a153e-247">From hello Log Analytics Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="a153e-248">輸入下列搜尋到 hello 查詢欄位中的 hello 建立警示的記錄搜尋查詢：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`您也可以依分組 hello RunbookName 使用：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span><span class="sxs-lookup"><span data-stu-id="a153e-248">Create a log search query for your alert by typing hello following search into hello query field:  `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  You can also group by hello RunbookName by using: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span></span>   

   <span data-ttu-id="a153e-249">如果您已將設定從多個自動化帳戶或訂用帳戶 tooyour 工作區的記錄檔，您可以群組您的訂用帳戶和自動化帳戶的警示。</span><span class="sxs-lookup"><span data-stu-id="a153e-249">If you have set up logs from more than one Automation account or subscription tooyour workspace, you can group your alerts by subscription and Automation account.</span></span>  <span data-ttu-id="a153e-250">自動化帳戶名稱可以衍生自 JobLogs hello 搜尋中的 hello 資源欄位。</span><span class="sxs-lookup"><span data-stu-id="a153e-250">Automation account name can be derived from hello Resource field in hello search of JobLogs.</span></span>  
3. <span data-ttu-id="a153e-251">tooopen hello**加入警示規則**畫面上，按一下**警示**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="a153e-251">tooopen hello **Add Alert Rule** screen, click **Alert** at hello top of hello page.</span></span> <span data-ttu-id="a153e-252">如需 hello 選項 tooconfigure hello 警示的詳細資訊，請參閱[記錄分析中的警示](../log-analytics/log-analytics-alerts.md#alert-rules)。</span><span class="sxs-lookup"><span data-stu-id="a153e-252">For further details on hello options tooconfigure hello alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-all-jobs-that-have-completed-with-errors"></a><span data-ttu-id="a153e-253">尋找所有已完成但發生錯誤的工作</span><span class="sxs-lookup"><span data-stu-id="a153e-253">Find all jobs that have completed with errors</span></span>
<span data-ttu-id="a153e-254">此外 tooalerting 失敗，您可以找到當 runbook 作業有一個非終止錯誤。</span><span class="sxs-lookup"><span data-stu-id="a153e-254">In addition tooalerting on failures, you can find when a runbook job has a non-terminating error.</span></span> <span data-ttu-id="a153e-255">PowerShell 會在這些情況下產生的錯誤資料流，但不是會造成工作 toosuspend hello 非終止錯誤或失敗。</span><span class="sxs-lookup"><span data-stu-id="a153e-255">In these cases PowerShell produces an error stream, but hello non-terminating errors do not cause your job toosuspend or fail.</span></span>    

1. <span data-ttu-id="a153e-256">在 Log Analytics 工作區中，按一下 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="a153e-256">In your Log Analytics workspace, click **Log Search**.</span></span>
2. <span data-ttu-id="a153e-257">在 hello 查詢欄位中，輸入`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g`，然後按一下**搜尋**。</span><span class="sxs-lookup"><span data-stu-id="a153e-257">In hello query field, type `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` and then click **Search**.</span></span>

### <a name="view-job-streams-for-a-job"></a><span data-ttu-id="a153e-258">檢視工作的工作資料流</span><span class="sxs-lookup"><span data-stu-id="a153e-258">View job streams for a job</span></span>
<span data-ttu-id="a153e-259">當您偵錯工作時，您也可以 toolook hello 工作資料流。</span><span class="sxs-lookup"><span data-stu-id="a153e-259">When you are debugging a job, you may also want toolook into hello job streams.</span></span>  <span data-ttu-id="a153e-260">hello 下列查詢顯示具有 GUID 2ebd22ea-e05e-4eb9-9 d 76 d73cbd4356e0 的單一作業的所有 hello 資料流：</span><span class="sxs-lookup"><span data-stu-id="a153e-260">hello following query shows all hello streams for a single job with GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:</span></span>   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a><span data-ttu-id="a153e-261">檢視歷史工作狀態</span><span class="sxs-lookup"><span data-stu-id="a153e-261">View historical job status</span></span>
<span data-ttu-id="a153e-262">最後，您可能想 toovisualize 作業記錄一段時間。</span><span class="sxs-lookup"><span data-stu-id="a153e-262">Finally, you may want toovisualize your job history over time.</span></span>  <span data-ttu-id="a153e-263">您可以使用這個查詢 toosearch hello 狀態為您的作業，一段時間。</span><span class="sxs-lookup"><span data-stu-id="a153e-263">You can use this query toosearch for hello status of your jobs over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> <span data-ttu-id="a153e-264">![OMS 歷史工作狀態圖表](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span><span class="sxs-lookup"><span data-stu-id="a153e-264">![OMS Historical Job Status Chart](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span></span><br>

## <a name="summary"></a><span data-ttu-id="a153e-265">摘要</span><span class="sxs-lookup"><span data-stu-id="a153e-265">Summary</span></span>
<span data-ttu-id="a153e-266">藉由傳送您自動化工作的狀態和資料流資料 tooLog 分析，您可以取得更深入的自動化工作的 hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="a153e-266">By sending your Automation job status and stream data tooLog Analytics, you can get better insight into hello status of your Automation jobs by:</span></span>
+ <span data-ttu-id="a153e-267">設定警示 toonotify 您發生問題時</span><span class="sxs-lookup"><span data-stu-id="a153e-267">Setting up alerts toonotify you when there is an issue</span></span>
+ <span data-ttu-id="a153e-268">使用自訂檢視和搜尋查詢 toovisualize 您 runbook 結果、 runbook 工作狀態、 和其他相關的主要指標或度量。</span><span class="sxs-lookup"><span data-stu-id="a153e-268">Using custom views and search queries toovisualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="a153e-269">記錄分析會提供操作可見度 tooyour 自動化工作，並可協助更快速地址事件。</span><span class="sxs-lookup"><span data-stu-id="a153e-269">Log Analytics provides greater operational visibility tooyour Automation jobs and can help address incidents quicker.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a153e-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a153e-270">Next steps</span></span>
* <span data-ttu-id="a153e-271">toolearn 深入了解 tooconstruct 不同的搜尋查詢和檢閱 hello 自動化作業記錄檔記錄分析，請參閱[中記錄分析記錄搜尋](../log-analytics/log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="a153e-271">toolearn more about how tooconstruct different search queries and review hello Automation job logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="a153e-272">如何 toocreate 並擷取輸出和錯誤訊息從 runbook，請參閱的 toounderstand [Runbook 輸出和訊息](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="a153e-272">toounderstand how toocreate and retrieve output and error messages from runbooks, see [Runbook output and messages](automation-runbook-output-and-messages.md)</span></span>
* <span data-ttu-id="a153e-273">深入了解 runbook 執行時，如何 toomonitor runbook 作業和其他技術的詳細資訊，請參閱 toolearn[追蹤 runbook 工作](automation-runbook-execution.md)</span><span class="sxs-lookup"><span data-stu-id="a153e-273">toolearn more about runbook execution, how toomonitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md)</span></span>
* <span data-ttu-id="a153e-274">toolearn 深入了解 OMS 記錄分析和資料集合來源，請參閱[收集 Azure 儲存體中的資料記錄分析概觀](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="a153e-274">toolearn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>
