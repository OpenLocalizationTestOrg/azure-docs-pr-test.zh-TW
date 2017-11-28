---
title: "在 Azure 自動化中使用 Runbook 收集 Log Analytics 資料 | Microsoft Docs"
description: "逐步教學課程，可逐步解說如何在 Azure 自動化中建立 Runbook 以將資料收集到 OMS 存放庫，供 Log Analytics 進行分析。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="a2272-103">使用 Azure 自動化 Runbook 在 Log Analytics 中收集資料</span><span class="sxs-lookup"><span data-stu-id="a2272-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="a2272-104">您可以在 Log Analytics 中收集來自各種來源 (包括代理程式上的[資料來源](../log-analytics/log-analytics-data-sources.md)) 的大量資料，以及[收集自 Azure 的資料](../log-analytics/log-analytics-azure-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="a2272-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="a2272-105">在某些情況下，您需要收集無法透過這些標準來源存取到的資料。</span><span class="sxs-lookup"><span data-stu-id="a2272-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="a2272-106">在這些案例中，您可以使用 [HTTP 資料收集器 API](../log-analytics/log-analytics-data-collector-api.md) 將資料從任何 REST API 用戶端寫入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="a2272-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="a2272-107">執行此資料收集的常見方法是在 Azure 自動化中使用 Runbook。</span><span class="sxs-lookup"><span data-stu-id="a2272-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="a2272-108">本教學課程會逐步解說在 Azure 自動化中建立和排程 Runbook 以將資料寫入 Log Analytics 的程序。</span><span class="sxs-lookup"><span data-stu-id="a2272-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a2272-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="a2272-109">Prerequisites</span></span>
<span data-ttu-id="a2272-110">此案例要求您在 Azure 訂用帳戶中設定以下資源。</span><span class="sxs-lookup"><span data-stu-id="a2272-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="a2272-111">兩者都可以是免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2272-111">Both can be a free account.</span></span>

- <span data-ttu-id="a2272-112">[Log Analytics 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a2272-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="a2272-113">[Azure 自動化帳戶](../automation/automation-offering-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a2272-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="a2272-114">案例概觀</span><span class="sxs-lookup"><span data-stu-id="a2272-114">Overview of scenario</span></span>
<span data-ttu-id="a2272-115">在本教學課程中，您將撰寫 Runbook 來收集自動化工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a2272-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="a2272-116">Azure 自動化中的 Runbook 是使用 PowerShell 所實作，因此您會先在 Azure 自動化編輯器中撰寫和測試指令碼。</span><span class="sxs-lookup"><span data-stu-id="a2272-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="a2272-117">驗證已收集所需的資訊後，請將該資料寫入 Log Analytics，並驗證自訂資料類型。</span><span class="sxs-lookup"><span data-stu-id="a2272-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="a2272-118">最後，您將建立定期啟動 Runbook 的排程。</span><span class="sxs-lookup"><span data-stu-id="a2272-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="a2272-119">您可以設定 Azure 自動化將作業資訊傳送至 Log Analytics，而不需要使用此 Runbook。</span><span class="sxs-lookup"><span data-stu-id="a2272-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="a2272-120">此案例主要用來支援教學課程，並建議您將資料傳送至測試工作區。</span><span class="sxs-lookup"><span data-stu-id="a2272-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="a2272-121">1.安裝資料收集器 API 模組</span><span class="sxs-lookup"><span data-stu-id="a2272-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="a2272-122">[來自 HTTP 資料收集器 API 的每個要求](../log-analytics/log-analytics-data-collector-api.md#create-a-request)都必須適當地格式化，並包含授權標頭。</span><span class="sxs-lookup"><span data-stu-id="a2272-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="a2272-123">您可以在 Runbook 中執行這項作業，但可以減少使用可簡化此程序之模型所需的程式碼數量。</span><span class="sxs-lookup"><span data-stu-id="a2272-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="a2272-124">您可以使用的其中一個模組是 PowerShell 資源庫中的 [OMSIngestionAPI 模組](https://www.powershellgallery.com/packages/OMSIngestionAPI)。</span><span class="sxs-lookup"><span data-stu-id="a2272-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="a2272-125">若要在 Runbook 中使用[模組](../automation/automation-integration-modules.md)，則必須將它安裝在自動化帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a2272-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="a2272-126">相同帳戶中的任何 Runbook 接著可以在模組中使用函式。</span><span class="sxs-lookup"><span data-stu-id="a2272-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="a2272-127">在自動化帳戶中選取 [資產] > [模組] > [新增模組]，即可安裝新的模組。</span><span class="sxs-lookup"><span data-stu-id="a2272-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="a2272-128">PowerShell 資源庫提供快速選項讓您將模組直接部署至自動化帳戶，因此，您可以在本教學課程中使用該選項。</span><span class="sxs-lookup"><span data-stu-id="a2272-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![OMSIngestionAPI 模組](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="a2272-130">前往 [PowerShell 資源庫](https://www.powershellgallery.com/)。</span><span class="sxs-lookup"><span data-stu-id="a2272-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="a2272-131">搜尋 **OMSIngestionAPI**。</span><span class="sxs-lookup"><span data-stu-id="a2272-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="a2272-132">按一下 [部署至 Azure 自動化] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a2272-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="a2272-133">選取自動化帳戶，然後按一下 [確定] 安裝模組。</span><span class="sxs-lookup"><span data-stu-id="a2272-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="a2272-134">2.建立自動化變數</span><span class="sxs-lookup"><span data-stu-id="a2272-134">2. Create Automation variables</span></span>
<span data-ttu-id="a2272-135">[自動化變數](..\automation\automation-variables.md)會保留值，以供自動化帳戶中的所有 Runbook 使用。</span><span class="sxs-lookup"><span data-stu-id="a2272-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="a2272-136">它們可讓您變更這些值，而不需要編輯實際 Runbook，讓 Runbook 更具彈性。</span><span class="sxs-lookup"><span data-stu-id="a2272-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="a2272-137">來自 HTTP 資料收集器 API 的每個要求都需要 OMS 工作區的識別碼和索引鍵，而且變數資產最適合用來儲存這項資訊。</span><span class="sxs-lookup"><span data-stu-id="a2272-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![變數](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="a2272-139">在 Azure 入口網站中，瀏覽至您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2272-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="a2272-140">選取 [共用資源] 下方的 [變數]。</span><span class="sxs-lookup"><span data-stu-id="a2272-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="a2272-141">按一下 [新增變數]，然後建立下表中的兩個變數。</span><span class="sxs-lookup"><span data-stu-id="a2272-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="a2272-142">屬性</span><span class="sxs-lookup"><span data-stu-id="a2272-142">Property</span></span> | <span data-ttu-id="a2272-143">工作區識別碼值</span><span class="sxs-lookup"><span data-stu-id="a2272-143">Workspace ID Value</span></span> | <span data-ttu-id="a2272-144">工作區索引鍵值</span><span class="sxs-lookup"><span data-stu-id="a2272-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a2272-145">名稱</span><span class="sxs-lookup"><span data-stu-id="a2272-145">Name</span></span> | <span data-ttu-id="a2272-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="a2272-146">WorkspaceId</span></span> | <span data-ttu-id="a2272-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="a2272-147">WorkspaceKey</span></span> |
| <span data-ttu-id="a2272-148">類型</span><span class="sxs-lookup"><span data-stu-id="a2272-148">Type</span></span> | <span data-ttu-id="a2272-149">String</span><span class="sxs-lookup"><span data-stu-id="a2272-149">String</span></span> | <span data-ttu-id="a2272-150">String</span><span class="sxs-lookup"><span data-stu-id="a2272-150">String</span></span> |
| <span data-ttu-id="a2272-151">值</span><span class="sxs-lookup"><span data-stu-id="a2272-151">Value</span></span> | <span data-ttu-id="a2272-152">貼入 Log Analytics 工作區的工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="a2272-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="a2272-153">貼入 Log Analytics 工作區的主要或次要索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a2272-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="a2272-154">已加密</span><span class="sxs-lookup"><span data-stu-id="a2272-154">Encrypted</span></span> | <span data-ttu-id="a2272-155">否</span><span class="sxs-lookup"><span data-stu-id="a2272-155">No</span></span> | <span data-ttu-id="a2272-156">是</span><span class="sxs-lookup"><span data-stu-id="a2272-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="a2272-157">3.建立 Runbook</span><span class="sxs-lookup"><span data-stu-id="a2272-157">3. Create runbook</span></span>

<span data-ttu-id="a2272-158">Azure 自動化在入口網站中有一個編輯器，您可以在其中編輯和測試 Runbook。</span><span class="sxs-lookup"><span data-stu-id="a2272-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="a2272-159">您可以選擇使用指令碼編輯器來[直接使用 PowerShell](../automation/automation-edit-textual-runbook.md)，或[建立圖形化 Runbook](../automation/automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="a2272-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="a2272-160">在本教學課程中，您將使用 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a2272-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![編輯 Runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="a2272-162">瀏覽至您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2272-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="a2272-163">按一下 [Runbook] > [新增 Runbook] > [建立新的 Runbook]。</span><span class="sxs-lookup"><span data-stu-id="a2272-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="a2272-164">針對 Runbook 名稱，鍵入 **Collect-Automation-jobs**。</span><span class="sxs-lookup"><span data-stu-id="a2272-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="a2272-165">針對 Runbook 類型，選取 [PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="a2272-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="a2272-166">按一下 [建立]  來建立 Runbook，並啟動編輯器。</span><span class="sxs-lookup"><span data-stu-id="a2272-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="a2272-167">複製下列程式碼，並將其貼入 Runbook 中。</span><span class="sxs-lookup"><span data-stu-id="a2272-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="a2272-168">如需程式碼的說明，請參閱指令碼中的註解。</span><span class="sxs-lookup"><span data-stu-id="a2272-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="a2272-169">4.測試 Runbook</span><span class="sxs-lookup"><span data-stu-id="a2272-169">4. Test runbook</span></span>
<span data-ttu-id="a2272-170">Azure 自動化包含可在發佈之前[測試 Runbook](../automation/automation-testing-runbook.md) 的環境。</span><span class="sxs-lookup"><span data-stu-id="a2272-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="a2272-171">您可以先檢查 Runbook 所收集的資料，並驗證它如預期寫入 Log Analytics 中，再將它發佈至生產環境。</span><span class="sxs-lookup"><span data-stu-id="a2272-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![測試 Runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="a2272-173">按一下 [儲存] 以儲存 Runbook。</span><span class="sxs-lookup"><span data-stu-id="a2272-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="a2272-174">按一下 [測試] 窗格，以在測試環境中開啟 Runbook。</span><span class="sxs-lookup"><span data-stu-id="a2272-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="a2272-175">因為您的 Runbook 有參數，所以系統會提示您輸入值。</span><span class="sxs-lookup"><span data-stu-id="a2272-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="a2272-176">輸入您要從中收集作業資訊的資源群組和自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a2272-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="a2272-177">按一下 [啟動] 以啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="a2272-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="a2272-178">Runbook 會先以 [已排入佇列] 狀態啟動，再進入 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="a2272-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="a2272-179">Runbook 應該會以 json 格式顯示詳細資訊輸出以及收集到的作業。</span><span class="sxs-lookup"><span data-stu-id="a2272-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="a2272-180">如果未列出任何作業，則最後一個小時可能未在自動化帳戶中建立任何作業。</span><span class="sxs-lookup"><span data-stu-id="a2272-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="a2272-181">請嘗試在自動化帳戶中啟動任何 Runbook，然後重新執行測試。</span><span class="sxs-lookup"><span data-stu-id="a2272-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="a2272-182">請確定輸出中未顯示 Log Analytics 的 post 命令中的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="a2272-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="a2272-183">您應該會看見類似下方的訊息。</span><span class="sxs-lookup"><span data-stu-id="a2272-183">You should have a message similar to the following.</span></span>

    ![張貼輸出](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="a2272-185">5.確認 Log Analytics 中的記錄</span><span class="sxs-lookup"><span data-stu-id="a2272-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="a2272-186">在 Runbook 完成測試並確認成功收到輸出之後，即可確認已使用 [Log Analytics 中的記錄搜尋](../log-analytics/log-analytics-log-searches.md)來建立記錄。</span><span class="sxs-lookup"><span data-stu-id="a2272-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![記錄輸出](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="a2272-188">在 Azure 入口網站中，選取 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="a2272-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="a2272-189">按一下 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="a2272-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="a2272-190">鍵入下列命令 `Type=AutomationJob_CL`，然後按一下搜尋按鈕。</span><span class="sxs-lookup"><span data-stu-id="a2272-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="a2272-191">請注意，記錄類型會包括指令碼中未指定的 _CL。</span><span class="sxs-lookup"><span data-stu-id="a2272-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="a2272-192">該尾碼會自動附加至記錄類型，指出它是自訂記錄類型。</span><span class="sxs-lookup"><span data-stu-id="a2272-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="a2272-193">您應該會看到傳回一或多筆記錄，指出 Runbook 已如預期運作。</span><span class="sxs-lookup"><span data-stu-id="a2272-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="a2272-194">6.發佈 Runbook</span><span class="sxs-lookup"><span data-stu-id="a2272-194">6. Publish the runbook</span></span>
<span data-ttu-id="a2272-195">驗證 Runbook 正確運作之後，必須將其發佈，以在生產環境中執行。</span><span class="sxs-lookup"><span data-stu-id="a2272-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="a2272-196">您可以繼續編輯和測試 Runbook，而不需要修改已發佈的版本。</span><span class="sxs-lookup"><span data-stu-id="a2272-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![發佈 Runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="a2272-198">返回自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2272-198">Return to your automation account.</span></span>
2. <span data-ttu-id="a2272-199">按一下 [Runbook]，並選取 [收集自動化工作]。</span><span class="sxs-lookup"><span data-stu-id="a2272-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="a2272-200">按一下 [編輯]，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="a2272-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="a2272-201">系統要求您驗證是否要覆寫先前發佈的版本時，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="a2272-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="a2272-202">7.設定記錄選項</span><span class="sxs-lookup"><span data-stu-id="a2272-202">7. Set logging options</span></span> 
<span data-ttu-id="a2272-203">在測試環境中，因為您在指令碼中設定 $VerbosePreference 變數，所以可以檢視[詳細資訊輸出](../automation/automation-runbook-output-and-messages.md#message-streams)。</span><span class="sxs-lookup"><span data-stu-id="a2272-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="a2272-204">在生產環境中，如果您想要檢視詳細資訊輸出，則需要設定 Runbook 的記錄內容。</span><span class="sxs-lookup"><span data-stu-id="a2272-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="a2272-205">針對本教學課程中所使用的 Runbook，這會顯示傳送至 Log Analytics 的 json 資料。</span><span class="sxs-lookup"><span data-stu-id="a2272-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![記錄和追蹤](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="a2272-207">在 Runbook 的內容中，選取 [Runbook 設定] 下的 [記錄和追蹤]。</span><span class="sxs-lookup"><span data-stu-id="a2272-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="a2272-208">將 [記錄詳細記錄] 的設定變更為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="a2272-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="a2272-209">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a2272-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="a2272-210">8.排程 Runbook</span><span class="sxs-lookup"><span data-stu-id="a2272-210">8. Schedule runbook</span></span>
<span data-ttu-id="a2272-211">啟動 Runbook 以收集監視資料的最常見方式，是將其排程為自動執行。</span><span class="sxs-lookup"><span data-stu-id="a2272-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="a2272-212">作法是[在 Azure 自動化中建立排程](../automation/automation-schedules.md)，並將它連結至 Runbook。</span><span class="sxs-lookup"><span data-stu-id="a2272-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![排程 Runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="a2272-214">在 Runbook 的內容中，選取 [資源] 下的 [排程]。</span><span class="sxs-lookup"><span data-stu-id="a2272-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="a2272-215">按一下 [新增排程] > [將排程連結至您的 Runbook] > [建立新的排程]。</span><span class="sxs-lookup"><span data-stu-id="a2272-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="a2272-216">鍵入排程的下列值，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a2272-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="a2272-217">屬性</span><span class="sxs-lookup"><span data-stu-id="a2272-217">Property</span></span> | <span data-ttu-id="a2272-218">值</span><span class="sxs-lookup"><span data-stu-id="a2272-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="a2272-219">名稱</span><span class="sxs-lookup"><span data-stu-id="a2272-219">Name</span></span> | <span data-ttu-id="a2272-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="a2272-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="a2272-221">啟動</span><span class="sxs-lookup"><span data-stu-id="a2272-221">Starts</span></span> | <span data-ttu-id="a2272-222">選取至少超過目前時間 5 分鐘的任何時間。</span><span class="sxs-lookup"><span data-stu-id="a2272-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="a2272-223">週期性</span><span class="sxs-lookup"><span data-stu-id="a2272-223">Recurrence</span></span> | <span data-ttu-id="a2272-224">週期性</span><span class="sxs-lookup"><span data-stu-id="a2272-224">Recurring</span></span> |
| <span data-ttu-id="a2272-225">重複頻率</span><span class="sxs-lookup"><span data-stu-id="a2272-225">Recur every</span></span> | <span data-ttu-id="a2272-226">1 小時</span><span class="sxs-lookup"><span data-stu-id="a2272-226">1 hour</span></span> |
| <span data-ttu-id="a2272-227">設定到期日</span><span class="sxs-lookup"><span data-stu-id="a2272-227">Set expiration</span></span> | <span data-ttu-id="a2272-228">否</span><span class="sxs-lookup"><span data-stu-id="a2272-228">No</span></span> |

<span data-ttu-id="a2272-229">建立排程之後，您需要設定將在每次此排程啟動 Runbook 時使用的參數值。</span><span class="sxs-lookup"><span data-stu-id="a2272-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="a2272-230">按一下 [設定參數與回合設定]。</span><span class="sxs-lookup"><span data-stu-id="a2272-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="a2272-231">填入 **ResourceGroupName** 和 **AutomationAccountName** 的值。</span><span class="sxs-lookup"><span data-stu-id="a2272-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="a2272-232">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a2272-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="a2272-233">9.驗證 Runbook 會依排程啟動</span><span class="sxs-lookup"><span data-stu-id="a2272-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="a2272-234">每次啟動 Runbook 時，都會[建立作業](../automation/automation-runbook-execution.md)且會記錄任何輸出。</span><span class="sxs-lookup"><span data-stu-id="a2272-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="a2272-235">事實上，這些作業與 Runbook 所收集的作業相同。</span><span class="sxs-lookup"><span data-stu-id="a2272-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="a2272-236">在排程的開始時間過後，您可以檢查 Runbook 的作業來確認 Runbook 如預期啟動。</span><span class="sxs-lookup"><span data-stu-id="a2272-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![作業](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="a2272-238">在 Runbook 的內容中，選取 [資源] 下的 [作業]。</span><span class="sxs-lookup"><span data-stu-id="a2272-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="a2272-239">每次啟動 Runbook 時，您應該都會看到作業清單。</span><span class="sxs-lookup"><span data-stu-id="a2272-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="a2272-240">按一下其中一個作業，即可檢視其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a2272-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="a2272-241">按一下 [所有記錄]，以檢視來自 Runbook 的記錄和輸出。</span><span class="sxs-lookup"><span data-stu-id="a2272-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="a2272-242">捲動至底部，找到與下圖類似的項目。</span><span class="sxs-lookup"><span data-stu-id="a2272-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![詳細資訊](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="a2272-244">按一下此項目，檢視已傳送至 Log Analytics 的詳細 json 資料。</span><span class="sxs-lookup"><span data-stu-id="a2272-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a2272-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2272-245">Next steps</span></span>
- <span data-ttu-id="a2272-246">使用[檢視表設計工具](../log-analytics/log-analytics-view-designer.md)來建立檢視，以顯示您收集到 Log Analytics 存放庫的資料。</span><span class="sxs-lookup"><span data-stu-id="a2272-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="a2272-247">將 Runbook 封裝到[管理解決方案](operations-management-suite-solutions-creating.md)，以散發給客戶。</span><span class="sxs-lookup"><span data-stu-id="a2272-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="a2272-248">深入了解 [Log Analytics](https://docs.microsoft.com/azure/log-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="a2272-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="a2272-249">深入了解 [Azure 自動化](https://docs.microsoft.com/azure/automation/)。</span><span class="sxs-lookup"><span data-stu-id="a2272-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="a2272-250">深入了解 [HTTP 資料收集器 API](../log-analytics/log-analytics-data-collector-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a2272-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>