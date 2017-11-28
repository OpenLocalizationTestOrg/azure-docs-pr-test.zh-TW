---
title: "將 Azure 自動化作業資料轉送到 OMS Log Analytics | Microsoft Docs"
description: "這篇文章示範如何將工作狀態和 Runbook 工作資料流傳送到 Microsoft Operations Management Suite Log Analytics，以提供額外的深入解析和管理。"
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
ms.openlocfilehash: 2c0ca7fc332963e5a5db3c20c400ed877ae0cc54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-to-log-analytics-oms"></a><span data-ttu-id="d5dfa-103">從「自動化」將工作狀態和工作資料流轉送到 Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-103">Forward job status and job streams from Automation to Log Analytics (OMS)</span></span>
<span data-ttu-id="d5dfa-104">「自動化」可以將 Runebook 工作狀態和工作資料流傳送到您的 Microsoft Operations Management Suite (OMS) Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-104">Automation can send runbook job status and job streams to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  <span data-ttu-id="d5dfa-105">作業記錄和作業串流會顯示於 Azure 入口網站中，或是使用 PowerShell，針對個別作業，而這可讓您執行簡單的調查。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-105">Job logs and job streams are visible in the Azure portal, or with PowerShell, for individual jobs and this allows you to perform simple investigations.</span></span> <span data-ttu-id="d5dfa-106">現在透過 Log Analytics，您可以：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-106">Now with Log Analytics you can:</span></span>

* <span data-ttu-id="d5dfa-107">針對自動化工作取得深入解析</span><span class="sxs-lookup"><span data-stu-id="d5dfa-107">Get insight on your Automation jobs</span></span>
* <span data-ttu-id="d5dfa-108">根據您的 Runbook 作業狀態 (例如已失敗或已暫停) 觸發電子郵件或警示</span><span class="sxs-lookup"><span data-stu-id="d5dfa-108">Trigger an email or alert based on your runbook job status (for example, failed or suspended)</span></span>
* <span data-ttu-id="d5dfa-109">撰寫工作資料流之間的進階查詢</span><span class="sxs-lookup"><span data-stu-id="d5dfa-109">Write advanced queries across your job streams</span></span>
* <span data-ttu-id="d5dfa-110">在自動化帳戶之間相互關聯工作</span><span class="sxs-lookup"><span data-stu-id="d5dfa-110">Correlate jobs across Automation accounts</span></span>
* <span data-ttu-id="d5dfa-111">視覺化一段時間的工作歷程記錄</span><span class="sxs-lookup"><span data-stu-id="d5dfa-111">Visualize your job history over time</span></span>     

## <a name="prerequisites-and-deployment-considerations"></a><span data-ttu-id="d5dfa-112">先決條件和部署考量</span><span class="sxs-lookup"><span data-stu-id="d5dfa-112">Prerequisites and deployment considerations</span></span>
<span data-ttu-id="d5dfa-113">若要開始將自動化記錄傳送到 Log Analytics，您必須擁有：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-113">To start sending your Automation logs to Log Analytics, you need:</span></span>

1. <span data-ttu-id="d5dfa-114">2016 年 11 月或更新版本的 [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0)。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-114">The November 2016 or later release of [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span></span>
2. <span data-ttu-id="d5dfa-115">Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-115">A Log Analytics workspace.</span></span> <span data-ttu-id="d5dfa-116">如需詳細資訊，請參閱[開始使用 Log Analytics](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-116">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span> 
3. <span data-ttu-id="d5dfa-117">Azure 自動化帳戶的 ResourceId</span><span class="sxs-lookup"><span data-stu-id="d5dfa-117">The ResourceId for your Azure Automation account</span></span>

<span data-ttu-id="d5dfa-118">若要尋找 Azure 自動化帳戶及 Log Analytics 工作區的 ResourceId，請執行下列 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-118">To find the ResourceId for your Azure Automation account and Log Analytics workspace, run the following PowerShell:</span></span>

```powershell
# Find the ResourceId for the Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find the ResourceId for the Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

<span data-ttu-id="d5dfa-119">如果您有多個自動化帳戶或工作區，可在先前命令的輸出中，尋找您必須設定的 Name，並複製 ResourceId 的值。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-119">If you have multiple Automation accounts, or workspaces, in the output of the preceding commands, find the *Name* you need to configure and copy the value for *ResourceId*.</span></span>

<span data-ttu-id="d5dfa-120">如果您需要尋找自動化帳戶的 Name，可在 Azure 入口網站中，從 [自動化帳戶] 刀鋒視窗選取您的自動化帳戶，然後選取 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-120">If you need to find the *Name* of your Automation account, in the Azure portal select your Automation account from the **Automation account** blade and select **All settings**.</span></span>  <span data-ttu-id="d5dfa-121">在 [所有設定] 刀鋒視窗中，選取 [帳戶設定] 之下的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-121">From the **All settings** blade, under **Account Settings** select **Properties**.</span></span>  <span data-ttu-id="d5dfa-122">在 [屬性] 刀鋒視窗中，您可以記下這些值。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-122">In the **Properties** blade, you can note these values.</span></span><br> <span data-ttu-id="d5dfa-123">![自動化帳戶屬性](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png)。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-123">![Automation Account properties](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span></span>

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="d5dfa-124">設定與 Log Analytics 整合</span><span class="sxs-lookup"><span data-stu-id="d5dfa-124">Set up integration with Log Analytics</span></span>
1. <span data-ttu-id="d5dfa-125">在您的電腦上，從 [開始] 畫面啟動 **Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-125">On your computer, start **Windows PowerShell** from the **Start** screen.</span></span>  
2. <span data-ttu-id="d5dfa-126">複製並貼上下列 PowerShell，然後編輯 `$workspaceId` 和 `$automationAccountId` 的值。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-126">Copy and paste the following PowerShell, and edit the value for the `$workspaceId` and `$automationAccountId`.</span></span>  <span data-ttu-id="d5dfa-127">`-Environment` 參數的有效值為 [AzureCloud] 或 [AzureUSGovernment]，視您工作時所在的雲端環境而定。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-127">For the `-Environment` parameter, valid values are *AzureCloud* or *AzureUSGovernment* depending on the cloud environment you are working in.</span></span>     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check to see which cloud environment to sign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use the following command to get the resource id of the workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

<span data-ttu-id="d5dfa-128">執行這個指令碼之後，您將會在寫入新 JobLogs 或 JobStreams 的 10 分鐘內，於 Log Analytics 中看見記錄。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-128">After running this script, you will see records in Log Analytics within 10 minutes of new JobLogs or JobStreams being written.</span></span>

<span data-ttu-id="d5dfa-129">若要查看記錄，請在 Log Analytics 記錄搜尋中執行下列查詢：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="d5dfa-129">To see the logs, run the following query in Log Analytics log search: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="verify-configuration"></a><span data-ttu-id="d5dfa-130">驗證組態</span><span class="sxs-lookup"><span data-stu-id="d5dfa-130">Verify configuration</span></span>
<span data-ttu-id="d5dfa-131">若要確認您的自動化帳戶正在將記錄傳送到 Log Analytics 工作區，請使用下列 PowerShell，來檢查已在自動化帳戶上正確設定診斷：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-131">To confirm that your Automation account is sending logs to your Log Analytics workspace, check that diagnostics are set correctly on the Automation account using the following PowerShell:</span></span>

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check to see which cloud environment to sign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use the following command to get the resource id of the workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

<span data-ttu-id="d5dfa-132">在輸出中，確定：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-132">In the output ensure that:</span></span>
+ <span data-ttu-id="d5dfa-133">在 [Logs] 下方，[Enabled] 的值為 True</span><span class="sxs-lookup"><span data-stu-id="d5dfa-133">Under *Logs*, the value for *Enabled* is *True*</span></span>
+ <span data-ttu-id="d5dfa-134">[WorkspaceId] 的值已設為 Log Analytics 工作區的 ResourceId</span><span class="sxs-lookup"><span data-stu-id="d5dfa-134">The value of *WorkspaceId* is set to the ResourceId of your Log Analytics workspace</span></span>


## <a name="log-analytics-records"></a><span data-ttu-id="d5dfa-135">Log Analytics 記錄</span><span class="sxs-lookup"><span data-stu-id="d5dfa-135">Log Analytics records</span></span>
<span data-ttu-id="d5dfa-136">來自 Azure 自動化的診斷會在 Log Analytics 中建立兩種類型的記錄，並標記為 **Type=AzureDiagnostics**。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-136">Diagnostics from Azure Automation creates two types of records in Log Analytics and are tagged as **Type=AzureDiagnostics**.</span></span>

### <a name="job-logs"></a><span data-ttu-id="d5dfa-137">作業記錄檔</span><span class="sxs-lookup"><span data-stu-id="d5dfa-137">Job Logs</span></span>
| <span data-ttu-id="d5dfa-138">屬性</span><span class="sxs-lookup"><span data-stu-id="d5dfa-138">Property</span></span> | <span data-ttu-id="d5dfa-139">說明</span><span class="sxs-lookup"><span data-stu-id="d5dfa-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5dfa-140">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d5dfa-140">TimeGenerated</span></span> |<span data-ttu-id="d5dfa-141">Runbook 作業的執行日期和時間。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-141">Date and time when the runbook job executed.</span></span> |
| <span data-ttu-id="d5dfa-142">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="d5dfa-142">RunbookName_s</span></span> |<span data-ttu-id="d5dfa-143">Runbook 的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-143">The name of the runbook.</span></span> |
| <span data-ttu-id="d5dfa-144">Caller_s</span><span class="sxs-lookup"><span data-stu-id="d5dfa-144">Caller_s</span></span> |<span data-ttu-id="d5dfa-145">起始作業的人員。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-145">Who initiated the operation.</span></span>  <span data-ttu-id="d5dfa-146">可能的值為電子郵件地址或排程作業的系統。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-146">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="d5dfa-147">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="d5dfa-147">Tenant_g</span></span> | <span data-ttu-id="d5dfa-148">識別呼叫端租用戶的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-148">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="d5dfa-149">JobId_g</span><span class="sxs-lookup"><span data-stu-id="d5dfa-149">JobId_g</span></span> |<span data-ttu-id="d5dfa-150">Runbook 作業之識別碼的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-150">GUID that is the Id of the runbook job.</span></span> |
| <span data-ttu-id="d5dfa-151">ResultType</span><span class="sxs-lookup"><span data-stu-id="d5dfa-151">ResultType</span></span> |<span data-ttu-id="d5dfa-152">Runbook 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-152">The status of the runbook job.</span></span>  <span data-ttu-id="d5dfa-153">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-153">Possible values are:</span></span><br><span data-ttu-id="d5dfa-154">- Started (已啟動)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-154">- Started</span></span><br><span data-ttu-id="d5dfa-155">- Stopped (已停止)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-155">- Stopped</span></span><br><span data-ttu-id="d5dfa-156">- Suspended (暫止)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-156">- Suspended</span></span><br><span data-ttu-id="d5dfa-157">- Failed (失敗)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-157">- Failed</span></span><br><span data-ttu-id="d5dfa-158">- Completed (已完成)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-158">- Completed</span></span> |
| <span data-ttu-id="d5dfa-159">類別</span><span class="sxs-lookup"><span data-stu-id="d5dfa-159">Category</span></span> | <span data-ttu-id="d5dfa-160">資料類型的分類。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-160">Classification of the type of data.</span></span>  <span data-ttu-id="d5dfa-161">對自動化來說，該值是 JobLogs。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-161">For Automation, the value is JobLogs.</span></span> |
| <span data-ttu-id="d5dfa-162">OperationName</span><span class="sxs-lookup"><span data-stu-id="d5dfa-162">OperationName</span></span> | <span data-ttu-id="d5dfa-163">指定在 Azure 中執行的作業類型。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-163">Specifies the type of operation performed in Azure.</span></span>  <span data-ttu-id="d5dfa-164">對自動化來說，該值是 Job。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-164">For Automation, the value is Job.</span></span> |
| <span data-ttu-id="d5dfa-165">資源</span><span class="sxs-lookup"><span data-stu-id="d5dfa-165">Resource</span></span> | <span data-ttu-id="d5dfa-166">自動化帳戶的名稱</span><span class="sxs-lookup"><span data-stu-id="d5dfa-166">Name of the Automation account</span></span> |
| <span data-ttu-id="d5dfa-167">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="d5dfa-167">SourceSystem</span></span> | <span data-ttu-id="d5dfa-168">Log Analytics 如何收集資料。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-168">How Log Analytics collected the data.</span></span> <span data-ttu-id="d5dfa-169">針對 Azure 診斷，一律為 Azure 。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-169">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="d5dfa-170">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="d5dfa-170">ResultDescription</span></span> |<span data-ttu-id="d5dfa-171">說明 Runbook 作業的結果狀態。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-171">Describes the runbook job result state.</span></span>  <span data-ttu-id="d5dfa-172">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-172">Possible values are:</span></span><br><span data-ttu-id="d5dfa-173">- Job is started (工作已啟動)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-173">- Job is started</span></span><br><span data-ttu-id="d5dfa-174">- Job Failed (工作失敗)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-174">- Job Failed</span></span><br><span data-ttu-id="d5dfa-175">- Job Completed</span><span class="sxs-lookup"><span data-stu-id="d5dfa-175">- Job Completed</span></span> |
| <span data-ttu-id="d5dfa-176">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="d5dfa-176">CorrelationId</span></span> |<span data-ttu-id="d5dfa-177">Runbook 作業之相互關聯識別碼的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-177">GUID that is the Correlation Id of the runbook job.</span></span> |
| <span data-ttu-id="d5dfa-178">ResourceId</span><span class="sxs-lookup"><span data-stu-id="d5dfa-178">ResourceId</span></span> |<span data-ttu-id="d5dfa-179">指定 Runbook 的 Azure 自動化帳戶資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-179">Specifies the Azure Automation account resource id of the runbook.</span></span> |
| <span data-ttu-id="d5dfa-180">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="d5dfa-180">SubscriptionId</span></span> | <span data-ttu-id="d5dfa-181">自動化帳戶的 Azure 訂用帳戶識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-181">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="d5dfa-182">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d5dfa-182">ResourceGroup</span></span> | <span data-ttu-id="d5dfa-183">自動化帳戶的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-183">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="d5dfa-184">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="d5dfa-184">ResourceProvider</span></span> | <span data-ttu-id="d5dfa-185">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="d5dfa-185">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="d5dfa-186">ResourceType</span><span class="sxs-lookup"><span data-stu-id="d5dfa-186">ResourceType</span></span> | <span data-ttu-id="d5dfa-187">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="d5dfa-187">AUTOMATIONACCOUNTS</span></span> |


### <a name="job-streams"></a><span data-ttu-id="d5dfa-188">作業串流</span><span class="sxs-lookup"><span data-stu-id="d5dfa-188">Job Streams</span></span>
| <span data-ttu-id="d5dfa-189">屬性</span><span class="sxs-lookup"><span data-stu-id="d5dfa-189">Property</span></span> | <span data-ttu-id="d5dfa-190">說明</span><span class="sxs-lookup"><span data-stu-id="d5dfa-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5dfa-191">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d5dfa-191">TimeGenerated</span></span> |<span data-ttu-id="d5dfa-192">Runbook 作業的執行日期和時間。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-192">Date and time when the runbook job executed.</span></span> |
| <span data-ttu-id="d5dfa-193">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="d5dfa-193">RunbookName_s</span></span> |<span data-ttu-id="d5dfa-194">Runbook 的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-194">The name of the runbook.</span></span> |
| <span data-ttu-id="d5dfa-195">Caller_s</span><span class="sxs-lookup"><span data-stu-id="d5dfa-195">Caller_s</span></span> |<span data-ttu-id="d5dfa-196">起始作業的人員。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-196">Who initiated the operation.</span></span>  <span data-ttu-id="d5dfa-197">可能的值為電子郵件地址或排程作業的系統。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-197">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="d5dfa-198">StreamType_s</span><span class="sxs-lookup"><span data-stu-id="d5dfa-198">StreamType_s</span></span> |<span data-ttu-id="d5dfa-199">作業串流的類型。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-199">The type of job stream.</span></span> <span data-ttu-id="d5dfa-200">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-200">Possible values are:</span></span><br><span data-ttu-id="d5dfa-201">-Progress (進度)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-201">-Progress</span></span><br><span data-ttu-id="d5dfa-202">- Output (輸出)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-202">- Output</span></span><br><span data-ttu-id="d5dfa-203">- Warning (警告)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-203">- Warning</span></span><br><span data-ttu-id="d5dfa-204">- Error (錯誤)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-204">- Error</span></span><br><span data-ttu-id="d5dfa-205">- Debug (偵錯)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-205">- Debug</span></span><br><span data-ttu-id="d5dfa-206">- Verbose</span><span class="sxs-lookup"><span data-stu-id="d5dfa-206">- Verbose</span></span> |
| <span data-ttu-id="d5dfa-207">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="d5dfa-207">Tenant_g</span></span> | <span data-ttu-id="d5dfa-208">識別呼叫端租用戶的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-208">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="d5dfa-209">JobId_g</span><span class="sxs-lookup"><span data-stu-id="d5dfa-209">JobId_g</span></span> |<span data-ttu-id="d5dfa-210">Runbook 作業之識別碼的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-210">GUID that is the Id of the runbook job.</span></span> |
| <span data-ttu-id="d5dfa-211">ResultType</span><span class="sxs-lookup"><span data-stu-id="d5dfa-211">ResultType</span></span> |<span data-ttu-id="d5dfa-212">Runbook 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-212">The status of the runbook job.</span></span>  <span data-ttu-id="d5dfa-213">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-213">Possible values are:</span></span><br><span data-ttu-id="d5dfa-214">- In Progress</span><span class="sxs-lookup"><span data-stu-id="d5dfa-214">- In Progress</span></span> |
| <span data-ttu-id="d5dfa-215">類別</span><span class="sxs-lookup"><span data-stu-id="d5dfa-215">Category</span></span> | <span data-ttu-id="d5dfa-216">資料類型的分類。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-216">Classification of the type of data.</span></span>  <span data-ttu-id="d5dfa-217">對自動化來說，該值是 JobStreams。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-217">For Automation, the value is JobStreams.</span></span> |
| <span data-ttu-id="d5dfa-218">OperationName</span><span class="sxs-lookup"><span data-stu-id="d5dfa-218">OperationName</span></span> | <span data-ttu-id="d5dfa-219">指定在 Azure 中執行的作業類型。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-219">Specifies the type of operation performed in Azure.</span></span>  <span data-ttu-id="d5dfa-220">對自動化來說，該值是 Job。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-220">For Automation, the value is Job.</span></span> |
| <span data-ttu-id="d5dfa-221">資源</span><span class="sxs-lookup"><span data-stu-id="d5dfa-221">Resource</span></span> | <span data-ttu-id="d5dfa-222">自動化帳戶的名稱</span><span class="sxs-lookup"><span data-stu-id="d5dfa-222">Name of the Automation account</span></span> |
| <span data-ttu-id="d5dfa-223">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="d5dfa-223">SourceSystem</span></span> | <span data-ttu-id="d5dfa-224">Log Analytics 如何收集資料。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-224">How Log Analytics collected the data.</span></span> <span data-ttu-id="d5dfa-225">針對 Azure 診斷，一律為 Azure 。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-225">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="d5dfa-226">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="d5dfa-226">ResultDescription</span></span> |<span data-ttu-id="d5dfa-227">包含來自 Runbook 的輸出串流。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-227">Includes the output stream from the runbook.</span></span> |
| <span data-ttu-id="d5dfa-228">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="d5dfa-228">CorrelationId</span></span> |<span data-ttu-id="d5dfa-229">Runbook 作業之相互關聯識別碼的 GUID。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-229">GUID that is the Correlation Id of the runbook job.</span></span> |
| <span data-ttu-id="d5dfa-230">ResourceId</span><span class="sxs-lookup"><span data-stu-id="d5dfa-230">ResourceId</span></span> |<span data-ttu-id="d5dfa-231">指定 Runbook 的 Azure 自動化帳戶資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-231">Specifies the Azure Automation account resource id of the runbook.</span></span> |
| <span data-ttu-id="d5dfa-232">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="d5dfa-232">SubscriptionId</span></span> | <span data-ttu-id="d5dfa-233">自動化帳戶的 Azure 訂用帳戶識別碼 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-233">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="d5dfa-234">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d5dfa-234">ResourceGroup</span></span> | <span data-ttu-id="d5dfa-235">自動化帳戶的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-235">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="d5dfa-236">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="d5dfa-236">ResourceProvider</span></span> | <span data-ttu-id="d5dfa-237">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="d5dfa-237">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="d5dfa-238">ResourceType</span><span class="sxs-lookup"><span data-stu-id="d5dfa-238">ResourceType</span></span> | <span data-ttu-id="d5dfa-239">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="d5dfa-239">AUTOMATIONACCOUNTS</span></span> |

## <a name="viewing-automation-logs-in-log-analytics"></a><span data-ttu-id="d5dfa-240">在 Log Analytics 中檢視自動化記錄檔</span><span class="sxs-lookup"><span data-stu-id="d5dfa-240">Viewing Automation Logs in Log Analytics</span></span>
<span data-ttu-id="d5dfa-241">既然您已經開始將自動化作業記錄傳送到 Log Analytics，讓我們來看看這些記錄在 Log Analytics 中的運用方式。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-241">Now that you have started sending your Automation job logs to Log Analytics, let’s see what you can do with these logs inside Log Analytics.</span></span>

<span data-ttu-id="d5dfa-242">若要查看記錄，請執行下列查詢：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="d5dfa-242">To see the logs, run the following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a><span data-ttu-id="d5dfa-243">在 Runbook 工作失敗或暫停時傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="d5dfa-243">Send an email when a runbook job fails or suspends</span></span>
<span data-ttu-id="d5dfa-244">我們最常從客戶收到的其中一個問題，便是希望系統能在 Runbook 工作發生問題時，傳送電子郵件或簡訊以通知他們。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-244">One of our top customer asks is for the ability to send an email or a text when something goes wrong with a runbook job.</span></span>   

<span data-ttu-id="d5dfa-245">若要建立警示規則，首先針對應叫用警示的 Runbook 工作記錄，建立記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-245">To create an alert rule, you start by creating a log search for the runbook job records that should invoke the alert.</span></span>  <span data-ttu-id="d5dfa-246">按一下 [警示] 按鈕，以建立並設定警示規則。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-246">Click the **Alert** button to create and configure the alert rule.</span></span>

1. <span data-ttu-id="d5dfa-247">從 [Log Analytics 概觀] 頁面，按一下 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-247">From the Log Analytics Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="d5dfa-248">在查詢欄位中輸入下列搜尋，來建立警示的記錄搜尋查詢：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` 您也可以使用下列內容，依 RunbookName 分組：`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span><span class="sxs-lookup"><span data-stu-id="d5dfa-248">Create a log search query for your alert by typing the following search into the query field:  `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  You can also group by the RunbookName by using: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span></span>   

   <span data-ttu-id="d5dfa-249">如果您已將來自多個自動化帳戶或訂用帳戶的記錄設定到您的工作區，就能依訂用帳戶或自動化帳戶來將警示分組。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-249">If you have set up logs from more than one Automation account or subscription to your workspace, you can group your alerts by subscription and Automation account.</span></span>  <span data-ttu-id="d5dfa-250">自動化帳戶名稱可以衍生自 JobLogs 搜尋的 [資源] 欄位。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-250">Automation account name can be derived from the Resource field in the search of JobLogs.</span></span>  
3. <span data-ttu-id="d5dfa-251">若要開啟 [新增警示規則] 畫面，按一下頁面頂端的 [警示]。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-251">To open the **Add Alert Rule** screen, click **Alert** at the top of the page.</span></span> <span data-ttu-id="d5dfa-252">如需設定警示選項的詳細資料，請參閱 [Log Analytics 中的警示](../log-analytics/log-analytics-alerts.md#alert-rules)。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-252">For further details on the options to configure the alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-all-jobs-that-have-completed-with-errors"></a><span data-ttu-id="d5dfa-253">尋找所有已完成但發生錯誤的工作</span><span class="sxs-lookup"><span data-stu-id="d5dfa-253">Find all jobs that have completed with errors</span></span>
<span data-ttu-id="d5dfa-254">除了失敗的警示，您還可以尋找 Runbook 作業發生非終止錯誤的時間。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-254">In addition to alerting on failures, you can find when a runbook job has a non-terminating error.</span></span> <span data-ttu-id="d5dfa-255">在這些情況下，PowerShell 會產生錯誤串流，但非終止錯誤不會造成您的作業暫止或失敗。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-255">In these cases PowerShell produces an error stream, but the non-terminating errors do not cause your job to suspend or fail.</span></span>    

1. <span data-ttu-id="d5dfa-256">在 Log Analytics 工作區中，按一下 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-256">In your Log Analytics workspace, click **Log Search**.</span></span>
2. <span data-ttu-id="d5dfa-257">在查詢欄位中，輸入 `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` ，然後按一下 [ **搜尋**]。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-257">In the query field, type `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` and then click **Search**.</span></span>

### <a name="view-job-streams-for-a-job"></a><span data-ttu-id="d5dfa-258">檢視工作的工作資料流</span><span class="sxs-lookup"><span data-stu-id="d5dfa-258">View job streams for a job</span></span>
<span data-ttu-id="d5dfa-259">當您在針對工作進行偵錯時，您可能也會想要查看工作資料流。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-259">When you are debugging a job, you may also want to look into the job streams.</span></span>  <span data-ttu-id="d5dfa-260">下列查詢會顯示單一作業具有 GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0 的所有資料流：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-260">The following query shows all the streams for a single job with GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:</span></span>   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a><span data-ttu-id="d5dfa-261">檢視歷史工作狀態</span><span class="sxs-lookup"><span data-stu-id="d5dfa-261">View historical job status</span></span>
<span data-ttu-id="d5dfa-262">最後，您可能會想要視覺化一段時間的工作歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-262">Finally, you may want to visualize your job history over time.</span></span>  <span data-ttu-id="d5dfa-263">您可以使用此查詢來搜尋您的工作在一段時間的狀態。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-263">You can use this query to search for the status of your jobs over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> <span data-ttu-id="d5dfa-264">![OMS 歷史工作狀態圖表](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-264">![OMS Historical Job Status Chart](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span></span><br>

## <a name="summary"></a><span data-ttu-id="d5dfa-265">摘要</span><span class="sxs-lookup"><span data-stu-id="d5dfa-265">Summary</span></span>
<span data-ttu-id="d5dfa-266">藉由將自動化作業狀態和串流資料傳送到 Log Analytics，您就能透過下列方式，更深入了解自動化作業的狀態：</span><span class="sxs-lookup"><span data-stu-id="d5dfa-266">By sending your Automation job status and stream data to Log Analytics, you can get better insight into the status of your Automation jobs by:</span></span>
+ <span data-ttu-id="d5dfa-267">設定警示，在發生問題時通知您</span><span class="sxs-lookup"><span data-stu-id="d5dfa-267">Setting up alerts to notify you when there is an issue</span></span>
+ <span data-ttu-id="d5dfa-268">使用自訂檢視和搜尋查詢，以視覺化方式檢視您的 Runbook 結果、Runbook 作業狀態，以及其他相關的關鍵指標或計量。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-268">Using custom views and search queries to visualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="d5dfa-269">Log Analytics 可以為您的自動化作業提供更高的操作可見性，並可協助更快速地處理事件。</span><span class="sxs-lookup"><span data-stu-id="d5dfa-269">Log Analytics provides greater operational visibility to your Automation jobs and can help address incidents quicker.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d5dfa-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5dfa-270">Next steps</span></span>
* <span data-ttu-id="d5dfa-271">若要深入了解如何建構不同的搜尋查詢，以及使用 Log Analytics 檢閱自動化工作記錄檔，請參閱 [Log Analytics 中的記錄檔搜尋](../log-analytics/log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-271">To learn more about how to construct different search queries and review the Automation job logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="d5dfa-272">若要了解如何建立及擷取 Runbook 的輸出與錯誤訊息，請參閱 [Runbook 輸出與訊息](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-272">To understand how to create and retrieve output and error messages from runbooks, see [Runbook output and messages](automation-runbook-output-and-messages.md)</span></span>
* <span data-ttu-id="d5dfa-273">若要深入了解 Runbook 執行方式、如何監視 Runbook 工作，以及其他技術性詳細資料，請參閱 [追蹤 Runbook 工作](automation-runbook-execution.md)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-273">To learn more about runbook execution, how to monitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md)</span></span>
* <span data-ttu-id="d5dfa-274">若要深入了解 OMS Log Analytics 和資料收集來源，請參閱 [在 Log Analytics 中收集 Azure 儲存體資料概觀](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d5dfa-274">To learn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>
