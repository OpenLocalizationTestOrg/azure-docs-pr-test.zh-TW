---
title: "Azure 自動化中 runbook aaaStarting |Microsoft 文件"
description: "摘要說明 hello 不同的方法是使用的 toostart Azure 自動化中的 runbook，且提供詳細資料上使用這兩個 hello Azure 入口網站和 Windows PowerShell。"
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
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="f7dbd-103">在 Azure 自動化中啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="f7dbd-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="f7dbd-104">下表中的 hello 可協助您判斷 hello 方法 toostart 中是最適合 tooyour 特定案例的 Azure 自動化 runbook。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-104">hello following table will help you determine hello method toostart a runbook in Azure Automation that is most suitable tooyour particular scenario.</span></span> <span data-ttu-id="f7dbd-105">本文包含在 hello Azure 入口網站與 Windows PowerShell 啟動 runbook 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-105">This article includes details on starting a runbook with hello Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="f7dbd-106">詳細資料 hello 上您可以從下列 hello 連結存取其他文件中提供其他方法。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-106">Details on hello other methods are provided in other documentation that you can access from hello links below.</span></span>

| <span data-ttu-id="f7dbd-107">**方法**</span><span class="sxs-lookup"><span data-stu-id="f7dbd-107">**METHOD**</span></span> | <span data-ttu-id="f7dbd-108">**特性**</span><span class="sxs-lookup"><span data-stu-id="f7dbd-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="f7dbd-109">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f7dbd-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="f7dbd-110">互動式使用者介面的最簡單方法。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="f7dbd-111">表單 tooprovide 簡單的參數值。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-111">Form tooprovide simple parameter values.</span></span><br> <li><span data-ttu-id="f7dbd-112">輕鬆追蹤工作狀態。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-112">Easily track job state.</span></span><br> <li><span data-ttu-id="f7dbd-113">使用 Azure 登入資訊驗證存取。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="f7dbd-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7dbd-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="f7dbd-115">使用 Windows PowerShell Cmdlet 從命令列呼叫。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="f7dbd-116">可以包含在具有多個步驟的自動化解決方案中。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="f7dbd-117">使用憑證或 OAuth 使用者主體/服務主體來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="f7dbd-118">提供簡單和複雜的參數值。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="f7dbd-119">追蹤工作狀態。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-119">Track job state.</span></span><br> <li><span data-ttu-id="f7dbd-120">用戶端需要 toosupport PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-120">Client required toosupport PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="f7dbd-121">Azure 自動化 API</span><span class="sxs-lookup"><span data-stu-id="f7dbd-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="f7dbd-122">最有彈性的方法，但也最複雜。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="f7dbd-123">從任何可提出 HTTP 要求的自訂程式碼呼叫。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="f7dbd-124">使用憑證或 OAuth 使用者主體/服務主體來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="f7dbd-125">提供簡單和複雜的參數值。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="f7dbd-126">追蹤工作狀態。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-126">Track job state.</span></span> |
| [<span data-ttu-id="f7dbd-127">Webhook</span><span class="sxs-lookup"><span data-stu-id="f7dbd-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="f7dbd-128">從單一 HTTP 要求啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="f7dbd-129">在 URL 中使用安全性權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="f7dbd-130">用戶端無法覆寫建立 Webhook 時指定的參數值。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="f7dbd-131">Runbook 可以定義單一參數，其中會填入 hello HTTP 要求詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-131">Runbook can define single parameter that is populated with hello HTTP request details.</span></span><br> <li><span data-ttu-id="f7dbd-132">透過 webhook URL 沒有能力 tootrack 工作狀態。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-132">No ability tootrack job state through webhook URL.</span></span> |
| [<span data-ttu-id="f7dbd-133">回應 tooAzure 警示</span><span class="sxs-lookup"><span data-stu-id="f7dbd-133">Respond tooAzure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="f7dbd-134">回應 tooAzure 警示中啟動 runbook。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-134">Start a runbook in response tooAzure alert.</span></span><br> <li><span data-ttu-id="f7dbd-135">設定 webhook runbook，並將連結 tooalert。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-135">Configure webhook for runbook and link tooalert.</span></span><br> <li><span data-ttu-id="f7dbd-136">在 URL 中使用安全性權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-136">Authenticated with security token in URL.</span></span> |
| [<span data-ttu-id="f7dbd-137">排程</span><span class="sxs-lookup"><span data-stu-id="f7dbd-137">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="f7dbd-138">每小時、每天、每週或每月排程，自動啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-138">Automatically start runbook on hourly, daily, weekly, or monthly schedule.</span></span><br> <li><span data-ttu-id="f7dbd-139">透過 Azure 入口網站、PowerShell Cmdlet 或 Azure API 操縱排程。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-139">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="f7dbd-140">提供參數值 toobe 排程搭配使用。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-140">Provide parameter values toobe used with schedule.</span></span> |
| [<span data-ttu-id="f7dbd-141">另一個 Runbook</span><span class="sxs-lookup"><span data-stu-id="f7dbd-141">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="f7dbd-142">在另一個 Runbook 中使用 Runbook 作為活動。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-142">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="f7dbd-143">對多個 Runbook 使用的功能很有用。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-143">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="f7dbd-144">提供參數值 toochild runbook，然後在父 runbook 使用輸出。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-144">Provide parameter values toochild runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="f7dbd-145">hello 圖顯示詳細的逐步程序中的 runbook hello 生命週期。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-145">hello following image illustrates detailed step-by-step process in hello life cycle of a runbook.</span></span> <span data-ttu-id="f7dbd-146">它包含不同的方式在 Azure 自動化中啟動 runbook Hybrid Runbook Worker tooexecute Azure 自動化 runbook 和不同元件之間的互動所需的元件。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-146">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker tooexecute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="f7dbd-147">有關在您的資料中心中執行自動化 runbook toolearn 參照太[hybrid runbook worker](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="f7dbd-147">toolearn about executing Automation runbooks in your datacenter, refer too[hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook 架構](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="f7dbd-149">啟動 runbook 以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f7dbd-149">Starting a runbook with hello Azure portal</span></span>
1. <span data-ttu-id="f7dbd-150">在 hello Azure 入口網站，選取 **自動化**，然後按一下 hello 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-150">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="f7dbd-151">在 hello 中樞功能表中，選取  **Runbook**。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-151">On hello Hub menu, select **Runbooks**.</span></span>
3. <span data-ttu-id="f7dbd-152">在 hello **Runbook**刀鋒視窗中，選取 runbook，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-152">On hello **Runbooks** blade, select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="f7dbd-153">如果 hello runbook 有參數，您將會提示的 tooprovide 文字方塊中的每個參數的值。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-153">If hello runbook has parameters, you will be prompted tooprovide values with a text box for each parameter.</span></span> <span data-ttu-id="f7dbd-154">請參閱以下的 [Runbook 參數](#Runbook-parameters) ，以取得參數的進一步詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-154">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="f7dbd-155">在 hello**作業**刀鋒視窗中，您可以檢視 hello hello runbook 工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-155">On hello **Job** blade, you can view hello status of hello runbook job.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="f7dbd-156">使用 Windows PowerShell 啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="f7dbd-156">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="f7dbd-157">您可以使用 hello[開始 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart 使用 Windows PowerShell runbook。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-157">You can use hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a runbook with Windows PowerShell.</span></span> <span data-ttu-id="f7dbd-158">hello 下列範例程式碼會啟動呼叫測試 Runbook 的 runbook。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-158">hello following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="f7dbd-159">開始 AzureRmAutomationRunbook 傳回工作物件，您可以使用 tootrack 其狀態 hello runbook 啟動之後。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-159">Start-AzureRmAutomationRunbook returns a job object that you can use tootrack its status once hello runbook is started.</span></span> <span data-ttu-id="f7dbd-160">然後，您可以使用此作業物件搭配[Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello hello 工作狀態和[Get AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget 其輸出。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-160">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello status of hello job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget its output.</span></span> <span data-ttu-id="f7dbd-161">下列範例程式碼的 hello 啟動名的測試 Runbook，等待它完成，並接著會顯示其輸出。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-161">hello following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

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

<span data-ttu-id="f7dbd-162">如果 hello runbook 需要參數，則您必須提供其作為[雜湊表](http://technet.microsoft.com/library/hh847780.aspx)hello hello 雜湊表索引鍵符合 hello 參數名稱和 hello 值的位置是 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-162">If hello runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where hello key of hello hashtable matches hello parameter name and hello value is hello parameter value.</span></span> <span data-ttu-id="f7dbd-163">hello 下列範例顯示如何 toostart 具有兩個字串參數的 runbook 名為 FirstName 和 LastName、 名為 RepeatCount 的整數和名為 Show 的布林參數。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-163">hello following example shows how toostart a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="f7dbd-164">如需有關參數的詳細資訊，請參閱以下的 [Runbook 參數](#Runbook-parameters) 。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-164">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="f7dbd-165">Runbook 參數</span><span class="sxs-lookup"><span data-stu-id="f7dbd-165">Runbook parameters</span></span>
<span data-ttu-id="f7dbd-166">當您從 hello Azure 入口網站或 Windows PowerShell 啟動 runbook 時，會透過 hello Azure 自動化 web 服務傳送 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-166">When you start a runbook from hello Azure Portal or Windows PowerShell, hello instruction is sent through hello Azure Automation web service.</span></span> <span data-ttu-id="f7dbd-167">此服務不支援具有複雜資料型別的參數。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-167">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="f7dbd-168">如果您需要 tooprovide 值為複雜參數，則您必須呼叫它內嵌從另一個 runbook 中所述[Azure 自動化中的子系 runbook](automation-child-runbooks.md)。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-168">If you need tooprovide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="f7dbd-169">hello Azure 自動化 web 服務會提供特殊功能，如 hello 下列各節中所述，使用特定資料類型的參數。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-169">hello Azure Automation web service will provide special functionality for parameters using certain data types as described in hello following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="f7dbd-170">具名值</span><span class="sxs-lookup"><span data-stu-id="f7dbd-170">Named values</span></span>
<span data-ttu-id="f7dbd-171">如果 hello 參數的資料類型 [object]，然後您可以使用下列 JSON 格式 toosend 其一份名稱為值的 hello: *{Name1: 'Value1'，Name2: 'Value2'，Name3: 'Value3'}*。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-171">If hello parameter is data type [object], then you can use hello following JSON format toosend it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="f7dbd-172">這些值必須是簡單型別。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-172">These values must be simple types.</span></span> <span data-ttu-id="f7dbd-173">hello runbook 將會收到 hello 參數做為[PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx)有屬性對應 tooeach 名稱為 value。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-173">hello runbook will receive hello parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond tooeach named value.</span></span>

<span data-ttu-id="f7dbd-174">請考慮下列接受參數，呼叫使用者的測試 runbook 的 hello。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-174">Consider hello following test runbook that accepts a parameter called user.</span></span>

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

<span data-ttu-id="f7dbd-175">hello 下列文字無法用於 hello user 參數。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-175">hello following text could be used for hello user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="f7dbd-176">這會導致 hello 遵循輸出。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-176">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="f7dbd-177">陣列</span><span class="sxs-lookup"><span data-stu-id="f7dbd-177">Arrays</span></span>
<span data-ttu-id="f7dbd-178">如果 hello 參數是陣列，例如 [array] 或 [string []]，，然後您可以使用 hello 下列 JSON 格式 toosend 它的值清單： *[Value1，Value2，Value3]*。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-178">If hello parameter is an array such as [array] or [string[]], then you can use hello following JSON format toosend it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="f7dbd-179">這些值必須是簡單型別。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-179">These values must be simple types.</span></span>

<span data-ttu-id="f7dbd-180">請考慮下列接受參數的測試 runbook 的 hello*使用者*。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-180">Consider hello following test runbook that accepts a parameter called *user*.</span></span>

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

<span data-ttu-id="f7dbd-181">hello 下列文字無法用於 hello user 參數。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-181">hello following text could be used for hello user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="f7dbd-182">這會導致 hello 遵循輸出。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-182">This results in hello following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="f7dbd-183">認證</span><span class="sxs-lookup"><span data-stu-id="f7dbd-183">Credentials</span></span>
<span data-ttu-id="f7dbd-184">如果 hello 參數的資料類型**PSCredential**，您就可以提供的 Azure 自動化的 hello 名稱[認證資產](automation-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-184">If hello parameter is data type **PSCredential**, then you can provide hello name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="f7dbd-185">hello runbook 將會抓取具有您指定的 hello 名稱 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-185">hello runbook will retrieve hello credential with hello name that you specify.</span></span>

<span data-ttu-id="f7dbd-186">請考慮下列接受認證參數的測試 runbook 的 hello。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-186">Consider hello following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="f7dbd-187">hello 下列文字可用於假設有認證資產的 hello 使用者參數*My Credential*。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-187">hello following text could be used for hello user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="f7dbd-188">假設在 hello 認證中的 hello username *jsmith*，這會產生下列輸出的 hello。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-188">Assuming hello username in hello credential was *jsmith*, this results in hello following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="f7dbd-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7dbd-189">Next steps</span></span>
* <span data-ttu-id="f7dbd-190">目前的文件中的 hello runbook 架構會提供在 Azure 和內部部署與 hello 混合式 Runbook 背景工作中的 runbook 管理資源的高階概觀。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-190">hello runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premises with hello Hybrid Runbook Worker.</span></span>  <span data-ttu-id="f7dbd-191">有關在您的資料中心中執行自動化 runbook toolearn 參照太[Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-191">toolearn about executing Automation runbooks in your datacenter, refer too[Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="f7dbd-192">深入了解建立其他 runbook 所使用的特定或一般函式的模組化 runbook toobe hello toolearn 參照太[子系 Runbook](automation-child-runbooks.md)。</span><span class="sxs-lookup"><span data-stu-id="f7dbd-192">toolearn more about hello creating modular runbooks toobe used by other runbooks for specific or common functions, refer too[Child Runbooks](automation-child-runbooks.md).</span></span>

