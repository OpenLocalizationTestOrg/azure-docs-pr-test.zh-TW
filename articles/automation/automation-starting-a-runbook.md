---
title: "在 Azure 自動化中啟動 Runbook | Microsoft Docs"
description: "摘要說明可以用來在 Azure 自動化中啟動 Runbook 的不同的方法，並提供使用 Azure 入口網站和 Windows PowerShell 的詳細資訊。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 844831b63d5263987ed05370125fbe9f01913ab9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="172cb-103">在 Azure 自動化中啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="172cb-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="172cb-104">下表將協助您判斷在 Azure 自動化中啟動 Runbook 的方法，最適合您的特定案例。</span><span class="sxs-lookup"><span data-stu-id="172cb-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="172cb-105">這篇文章包含有關使用 Azure 入口網站和 Windows PowerShell 啟動 Runbook 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="172cb-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="172cb-106">其他方法的詳細資訊在其他文件中提供，您可以從下列連結來存取。</span><span class="sxs-lookup"><span data-stu-id="172cb-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="172cb-107">**方法**</span><span class="sxs-lookup"><span data-stu-id="172cb-107">**METHOD**</span></span> | <span data-ttu-id="172cb-108">**特性**</span><span class="sxs-lookup"><span data-stu-id="172cb-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="172cb-109">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="172cb-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="172cb-110">互動式使用者介面的最簡單方法。</span><span class="sxs-lookup"><span data-stu-id="172cb-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="172cb-111">提供簡單參數值的表單。</span><span class="sxs-lookup"><span data-stu-id="172cb-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="172cb-112">輕鬆追蹤工作狀態。</span><span class="sxs-lookup"><span data-stu-id="172cb-112">Easily track job state.</span></span><br> <li><span data-ttu-id="172cb-113">使用 Azure 登入資訊驗證存取。</span><span class="sxs-lookup"><span data-stu-id="172cb-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="172cb-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="172cb-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="172cb-115">使用 Windows PowerShell Cmdlet 從命令列呼叫。</span><span class="sxs-lookup"><span data-stu-id="172cb-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="172cb-116">可以包含在具有多個步驟的自動化解決方案中。</span><span class="sxs-lookup"><span data-stu-id="172cb-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="172cb-117">使用憑證或 OAuth 使用者主體/服務主體來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="172cb-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="172cb-118">提供簡單和複雜的參數值。</span><span class="sxs-lookup"><span data-stu-id="172cb-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="172cb-119">追蹤工作狀態。</span><span class="sxs-lookup"><span data-stu-id="172cb-119">Track job state.</span></span><br> <li><span data-ttu-id="172cb-120">支援 PowerShell Cmdlet 所需的用戶端。</span><span class="sxs-lookup"><span data-stu-id="172cb-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="172cb-121">Azure 自動化 API</span><span class="sxs-lookup"><span data-stu-id="172cb-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="172cb-122">最有彈性的方法，但也最複雜。</span><span class="sxs-lookup"><span data-stu-id="172cb-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="172cb-123">從任何可提出 HTTP 要求的自訂程式碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="172cb-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="172cb-124">使用憑證或 OAuth 使用者主體/服務主體來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="172cb-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="172cb-125">提供簡單和複雜的參數值。</span><span class="sxs-lookup"><span data-stu-id="172cb-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="172cb-126">追蹤工作狀態。</span><span class="sxs-lookup"><span data-stu-id="172cb-126">Track job state.</span></span> |
| [<span data-ttu-id="172cb-127">Webhook</span><span class="sxs-lookup"><span data-stu-id="172cb-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="172cb-128">從單一 HTTP 要求啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="172cb-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="172cb-129">在 URL 中使用安全性權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="172cb-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="172cb-130">用戶端無法覆寫建立 Webhook 時指定的參數值。</span><span class="sxs-lookup"><span data-stu-id="172cb-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="172cb-131">Runbook 可以定義填入了 HTTP 要求詳細資料的單一參數。</span><span class="sxs-lookup"><span data-stu-id="172cb-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="172cb-132">無法透過 Webhook URL 追蹤工作狀態。</span><span class="sxs-lookup"><span data-stu-id="172cb-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="172cb-133">回應 Azure 警示</span><span class="sxs-lookup"><span data-stu-id="172cb-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="172cb-134">啟動 Runbook 以回應 Azure 警示。</span><span class="sxs-lookup"><span data-stu-id="172cb-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="172cb-135">設定 Runbook 的 Webhook 以及警示的連結。</span><span class="sxs-lookup"><span data-stu-id="172cb-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="172cb-136">在 URL 中使用安全性權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="172cb-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="172cb-137">排程</span><span class="sxs-lookup"><span data-stu-id="172cb-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="172cb-138">每小時、每天、每週或每月排程，自動啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="172cb-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="172cb-139">透過 Azure 入口網站、PowerShell Cmdlet 或 Azure API 操縱排程。</span><span class="sxs-lookup"><span data-stu-id="172cb-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="172cb-140">提供參數值來搭配排程使用。</span><span class="sxs-lookup"><span data-stu-id="172cb-140">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="172cb-141">另一個 Runbook</span><span class="sxs-lookup"><span data-stu-id="172cb-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="172cb-142">在另一個 Runbook 中使用 Runbook 作為活動。</span><span class="sxs-lookup"><span data-stu-id="172cb-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="172cb-143">對多個 Runbook 使用的功能很有用。</span><span class="sxs-lookup"><span data-stu-id="172cb-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="172cb-144">提供參數值給子 Runbook，並在父 Runbook 中使用輸出。</span><span class="sxs-lookup"><span data-stu-id="172cb-144">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="172cb-145">下圖說明 Runbook 的生命週期的詳細逐步程序。</span><span class="sxs-lookup"><span data-stu-id="172cb-145">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="172cb-146">它包含了 Runbook 在 Azure 自動化中啟動的不同方式、Hybrid Runbook Worker 執行 Azure 自動化 Runbook 所需的元件，以及不同元件之間的互動。</span><span class="sxs-lookup"><span data-stu-id="172cb-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="172cb-147">若要了解如何在您的資料中心執行自動化 Runbook，請參閱 [混合式 Runbook 背景工作](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="172cb-147">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook 架構](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="172cb-149">使用 Azure 入口網站啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="172cb-149">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="172cb-150">在 Azure 入口網站中，選取 [ **自動化** ]，然後按一下自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="172cb-150">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="172cb-151">在 [中樞] 功能表中，選取 [Runbook]。</span><span class="sxs-lookup"><span data-stu-id="172cb-151">On the Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="172cb-152">在 [Runbook] 刀鋒視窗中，選取 Runbook，然後按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="172cb-152">On the **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="172cb-153">如果 Runbook 有參數，系統會提示您提供每個參數的文字方塊的值。</span><span class="sxs-lookup"><span data-stu-id="172cb-153">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="172cb-154">請參閱以下的 [Runbook 參數](#Runbook-parameters) ，以取得參數的進一步詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="172cb-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="172cb-155">在 [作業] 刀鋒視窗中，您可以檢視 Runbook 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="172cb-155">On the **Job** blade, you can view the status of the runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="172cb-156">使用 Windows PowerShell 啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="172cb-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="172cb-157">您可以使用 [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) ，利用 Windows PowerShell 來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="172cb-157">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="172cb-158">下列範例程式碼會啟動名稱為 Test-Runbook 的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="172cb-158">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="172cb-159">Start-AzureRmAutomationRunbook 會傳回工作物件，一旦啟動 Runbook，您即可用來追蹤其狀態。</span><span class="sxs-lookup"><span data-stu-id="172cb-159">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="172cb-160">然後您可以使用此作業物件搭配 [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) 來判斷作業的狀態，以及搭配 [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) 來取得其輸出。</span><span class="sxs-lookup"><span data-stu-id="172cb-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="172cb-161">下列範例程式碼會啟動名稱為 Test-Runbook 的 Runbook，等到它完成，然後顯示其輸出。</span><span class="sxs-lookup"><span data-stu-id="172cb-161">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="172cb-162">如果 Runbook 需要參數，則您必須提供其作為 [hashtable](http://technet.microsoft.com/library/hh847780.aspx) ，其中雜湊表的索引鍵符合參數名稱，而值是參數值。</span><span class="sxs-lookup"><span data-stu-id="172cb-162">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="172cb-163">下列範例顯示如何啟動 Runbook 具有名為 FirstName 和 LastName 的兩個參數、名為 RepeatCount 的整數，和名為 Show 的布林值參數。</span><span class="sxs-lookup"><span data-stu-id="172cb-163">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="172cb-164">如需有關參數的詳細資訊，請參閱以下的 [Runbook 參數](#Runbook-parameters) 。</span><span class="sxs-lookup"><span data-stu-id="172cb-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="172cb-165">Runbook 參數</span><span class="sxs-lookup"><span data-stu-id="172cb-165">Runbook parameters</span></span>
<span data-ttu-id="172cb-166">從 Azure 入口網站或 Windows PowerShell 啟動 Runbook 時，指示會透過 Azure 自動化 Web 服務傳送。</span><span class="sxs-lookup"><span data-stu-id="172cb-166">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="172cb-167">此服務不支援具有複雜資料型別的參數。</span><span class="sxs-lookup"><span data-stu-id="172cb-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="172cb-168">如 [Azure 自動化中的子 Runbook](automation-child-runbooks.md)中所述，如果您需要提供複雜參數的值，您必須從另一個 Runbook 呼叫它內嵌。</span><span class="sxs-lookup"><span data-stu-id="172cb-168">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="172cb-169">Azure 自動化 Web 服務會為特定資料型別的參數提供特殊功能，如下列小節所述。</span><span class="sxs-lookup"><span data-stu-id="172cb-169">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="172cb-170">具名值</span><span class="sxs-lookup"><span data-stu-id="172cb-170">Named values</span></span>
<span data-ttu-id="172cb-171">如果參數是資料類型 [object]，則您可以使用下列 JSON 格式，對它傳送具名值清單：{Name1:'Value1', Name2:'Value2', Name3:'Value3'} 。</span><span class="sxs-lookup"><span data-stu-id="172cb-171">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="172cb-172">這些值必須是簡單型別。</span><span class="sxs-lookup"><span data-stu-id="172cb-172">These values must be simple types.</span></span> <span data-ttu-id="172cb-173">Runbook 將接收參數做為 [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) ，並具有對應到每個具名值的屬性。</span><span class="sxs-lookup"><span data-stu-id="172cb-173">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="172cb-174">請考慮可接受稱為 user 的參數的下列測試 Runbook。</span><span class="sxs-lookup"><span data-stu-id="172cb-174">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="172cb-175">下列文字可用於 user 參數。</span><span class="sxs-lookup"><span data-stu-id="172cb-175">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="172cb-176">這會導致下列輸出。</span><span class="sxs-lookup"><span data-stu-id="172cb-176">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="172cb-177">陣列</span><span class="sxs-lookup"><span data-stu-id="172cb-177">Arrays</span></span>
<span data-ttu-id="172cb-178">如果參數是陣列，例如 [array] 或 [string[]]，則您可以使用下列 JSON 格式對其傳送值清單：*[Value1,Value2,Value3]*。</span><span class="sxs-lookup"><span data-stu-id="172cb-178">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="172cb-179">這些值必須是簡單型別。</span><span class="sxs-lookup"><span data-stu-id="172cb-179">These values must be simple types.</span></span>

<span data-ttu-id="172cb-180">請考慮可接受稱為 *user*的參數的下列測試 Runbook。</span><span class="sxs-lookup"><span data-stu-id="172cb-180">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="172cb-181">下列文字可用於 user 參數。</span><span class="sxs-lookup"><span data-stu-id="172cb-181">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="172cb-182">這會導致下列輸出。</span><span class="sxs-lookup"><span data-stu-id="172cb-182">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="172cb-183">認證</span><span class="sxs-lookup"><span data-stu-id="172cb-183">Credentials</span></span>
<span data-ttu-id="172cb-184">如果參數是資料型別 **PSCredential**，則可以提供 Azure 自動化 [認證資產](automation-credentials.md)的名稱。</span><span class="sxs-lookup"><span data-stu-id="172cb-184">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="172cb-185">Runbook 將會使用您所指定的名稱擷取認證。</span><span class="sxs-lookup"><span data-stu-id="172cb-185">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="172cb-186">請考慮可接受稱為 credential 的參數的下列測試 Runbook。</span><span class="sxs-lookup"><span data-stu-id="172cb-186">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="172cb-187">假設有稱為 *My Credential*的認證資產，則下列文字可用於 user 參數。</span><span class="sxs-lookup"><span data-stu-id="172cb-187">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="172cb-188">假設在認證中的使用者名稱是 *jsmith*，這會導致下列輸出。</span><span class="sxs-lookup"><span data-stu-id="172cb-188">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="172cb-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="172cb-189">Next steps</span></span>
* <span data-ttu-id="172cb-190">目前文件中的 Runbook 架構提供在 Azure 中管理資源的 Runbook 整體概觀，並利用 Hybrid Runbook Worker 進行內部部署。</span><span class="sxs-lookup"><span data-stu-id="172cb-190">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="172cb-191">若要了解如何在您的資料中心執行自動化 Runbook，請參閱 [混合式 Runbook 背景工作](automation-hybrid-runbook-worker.md)。</span><span class="sxs-lookup"><span data-stu-id="172cb-191">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="172cb-192">若要深入了解如何建立模組化 Runbook，以供其他 Runbook 用於特定或一般函式，請參閱 [子 Runbook](automation-child-runbooks.md)。</span><span class="sxs-lookup"><span data-stu-id="172cb-192">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>

