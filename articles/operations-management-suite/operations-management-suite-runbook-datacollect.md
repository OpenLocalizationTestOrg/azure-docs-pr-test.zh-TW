---
title: "記錄分析資料與在 Azure 自動化 runbook aaaCollecting |Microsoft 文件"
description: "逐步教學課程會逐步引導您建立 runbook 在 Azure 自動化 toocollect 資料到記錄分析以進行分析的 hello OMS 儲存機制。"
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
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="481f8-103">使用 Azure 自動化 Runbook 在 Log Analytics 中收集資料</span><span class="sxs-lookup"><span data-stu-id="481f8-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="481f8-104">您可以在 Log Analytics 中收集來自各種來源 (包括代理程式上的[資料來源](../log-analytics/log-analytics-data-sources.md)) 的大量資料，以及[收集自 Azure 的資料](../log-analytics/log-analytics-azure-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="481f8-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="481f8-105">雖然需要 toocollect 資料，無法存取透過這些標準的來源，則需要有案例。</span><span class="sxs-lookup"><span data-stu-id="481f8-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="481f8-106">在這些情況下，您可以使用 hello [HTTP 資料收集器 API](../log-analytics/log-analytics-data-collector-api.md) toowrite 資料 tooLog 分析來自任何 REST API 用戶端。</span><span class="sxs-lookup"><span data-stu-id="481f8-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="481f8-107">常見的方法 tooperform 此資料集合使用 Azure 自動化中的 runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="481f8-108">本教學課程將引導 hello 程序建立和排定在 Azure 自動化 toowrite 資料 tooLog 分析中的 runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="481f8-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="481f8-109">Prerequisites</span></span>
<span data-ttu-id="481f8-110">此案例需要下列設定您的 Azure 訂用帳戶中資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="481f8-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="481f8-111">兩者都可以是免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="481f8-111">Both can be a free account.</span></span>

- <span data-ttu-id="481f8-112">[Log Analytics 工作區](../log-analytics/log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="481f8-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="481f8-113">[Azure 自動化帳戶](../automation/automation-offering-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="481f8-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="481f8-114">案例概觀</span><span class="sxs-lookup"><span data-stu-id="481f8-114">Overview of scenario</span></span>
<span data-ttu-id="481f8-115">在本教學課程中，您將撰寫 Runbook 來收集自動化工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="481f8-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="481f8-116">因此，您會藉由撰寫和測試指令碼在 hello Azure 自動化編輯器中啟動 PowerShell，以實作 Azure 自動化中的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="481f8-117">一旦您確認您要收集 hello 所需的資訊，請將寫入該資料 tooLog 分析，並確認 hello 自訂資料類型。</span><span class="sxs-lookup"><span data-stu-id="481f8-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="481f8-118">最後，您將固定間隔建立排程 toostart hello runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="481f8-119">您可以設定 Azure 自動化 toosend 作業資訊 tooLog 分析沒有此 runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="481f8-120">此案例中是主要使用的 toosupport hello 教學課程中，並建議您傳送嗨資料 tooa 測試工作區。</span><span class="sxs-lookup"><span data-stu-id="481f8-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="481f8-121">1.安裝資料收集器 API 模組</span><span class="sxs-lookup"><span data-stu-id="481f8-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="481f8-122">每個[hello HTTP 資料收集器 API 的要求](../log-analytics/log-analytics-data-collector-api.md#create-a-request)必須適當地格式化，並包含授權標頭。</span><span class="sxs-lookup"><span data-stu-id="481f8-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="481f8-123">您可以在您的 runbook，但您可以減少使用模組，可簡化此程序所需的程式碼的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="481f8-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="481f8-124">您可以使用的其中一個模組是[OMSIngestionAPI 模組](https://www.powershellgallery.com/packages/OMSIngestionAPI)hello PowerShell 資源庫中。</span><span class="sxs-lookup"><span data-stu-id="481f8-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="481f8-125">toouse[模組](../automation/automation-integration-modules.md)在 runbook 中使用，它必須安裝在您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="481f8-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="481f8-126">Hello 接著可以使用相同的帳戶中的任何 runbook hello hello 模組中的函式。</span><span class="sxs-lookup"><span data-stu-id="481f8-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="481f8-127">在自動化帳戶中選取 [資產] > [模組] > [新增模組]，即可安裝新的模組。</span><span class="sxs-lookup"><span data-stu-id="481f8-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="481f8-128">hello PowerShell 資源庫但是可讓您快速選項 toodeploy 模組直接 tooyour 自動化帳戶，因此您可以使用該選項在此教學課程。</span><span class="sxs-lookup"><span data-stu-id="481f8-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![OMSIngestionAPI 模組](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="481f8-130">跳過[PowerShell 資源庫](https://www.powershellgallery.com/)。</span><span class="sxs-lookup"><span data-stu-id="481f8-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="481f8-131">搜尋 **OMSIngestionAPI**。</span><span class="sxs-lookup"><span data-stu-id="481f8-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="481f8-132">按一下 hello**部署 tooAzure 自動化** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="481f8-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="481f8-133">選取您的自動化帳戶，然後按一下**確定**tooinstall hello 模組。</span><span class="sxs-lookup"><span data-stu-id="481f8-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="481f8-134">2.建立自動化變數</span><span class="sxs-lookup"><span data-stu-id="481f8-134">2. Create Automation variables</span></span>
<span data-ttu-id="481f8-135">[自動化變數](..\automation\automation-variables.md)會保留值，以供自動化帳戶中的所有 Runbook 使用。</span><span class="sxs-lookup"><span data-stu-id="481f8-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="481f8-136">它們會使 runbook 更多彈性，可讓您 toochange 而不需要編輯這些值 hello 實際的 runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="481f8-137">每個來自 hello HTTP 資料收集器 API 要求需要 hello 識別碼和金鑰的 hello OMS 工作區中，而且變數資產是理想的 toostore 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="481f8-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![變數](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="481f8-139">在 hello Azure 入口網站，瀏覽 tooyour 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="481f8-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="481f8-140">選取 [共用資源] 下方的 [變數]。</span><span class="sxs-lookup"><span data-stu-id="481f8-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="481f8-141">按一下**加入變數**和建立 hello hello 下表中的兩個變數。</span><span class="sxs-lookup"><span data-stu-id="481f8-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="481f8-142">屬性</span><span class="sxs-lookup"><span data-stu-id="481f8-142">Property</span></span> | <span data-ttu-id="481f8-143">工作區識別碼值</span><span class="sxs-lookup"><span data-stu-id="481f8-143">Workspace ID Value</span></span> | <span data-ttu-id="481f8-144">工作區索引鍵值</span><span class="sxs-lookup"><span data-stu-id="481f8-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="481f8-145">名稱</span><span class="sxs-lookup"><span data-stu-id="481f8-145">Name</span></span> | <span data-ttu-id="481f8-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="481f8-146">WorkspaceId</span></span> | <span data-ttu-id="481f8-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="481f8-147">WorkspaceKey</span></span> |
| <span data-ttu-id="481f8-148">類型</span><span class="sxs-lookup"><span data-stu-id="481f8-148">Type</span></span> | <span data-ttu-id="481f8-149">String</span><span class="sxs-lookup"><span data-stu-id="481f8-149">String</span></span> | <span data-ttu-id="481f8-150">String</span><span class="sxs-lookup"><span data-stu-id="481f8-150">String</span></span> |
| <span data-ttu-id="481f8-151">值</span><span class="sxs-lookup"><span data-stu-id="481f8-151">Value</span></span> | <span data-ttu-id="481f8-152">記錄分析工作區的工作區識別碼 hello 中貼上。</span><span class="sxs-lookup"><span data-stu-id="481f8-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="481f8-153">主要或次要金鑰，記錄分析工作區的 hello 入貼上。</span><span class="sxs-lookup"><span data-stu-id="481f8-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="481f8-154">已加密</span><span class="sxs-lookup"><span data-stu-id="481f8-154">Encrypted</span></span> | <span data-ttu-id="481f8-155">否</span><span class="sxs-lookup"><span data-stu-id="481f8-155">No</span></span> | <span data-ttu-id="481f8-156">是</span><span class="sxs-lookup"><span data-stu-id="481f8-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="481f8-157">3.建立 Runbook</span><span class="sxs-lookup"><span data-stu-id="481f8-157">3. Create runbook</span></span>

<span data-ttu-id="481f8-158">Azure 自動化有 hello 入口網站，您可以在其中編輯及測試您的 runbook 中的編輯器。</span><span class="sxs-lookup"><span data-stu-id="481f8-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="481f8-159">您已擁有 hello 選項 toouse hello 指令碼編輯器 toowork 與[直接 PowerShell](../automation/automation-edit-textual-runbook.md)或[建立圖形化 runbook](../automation/automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="481f8-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="481f8-160">在本教學課程中，您將使用 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="481f8-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![編輯 Runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="481f8-162">瀏覽 tooyour 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="481f8-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="481f8-163">按一下 [Runbook] > [新增 Runbook] > [建立新的 Runbook]。</span><span class="sxs-lookup"><span data-stu-id="481f8-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="481f8-164">Hello runbook 名稱 中輸入**收集自動化工作**。</span><span class="sxs-lookup"><span data-stu-id="481f8-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="481f8-165">Hello runbook 類型 選取**PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="481f8-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="481f8-166">按一下**建立**toocreate hello runbook 並開始 hello 編輯器。</span><span class="sxs-lookup"><span data-stu-id="481f8-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="481f8-167">複製並貼上下列程式碼至 hello runbook hello。</span><span class="sxs-lookup"><span data-stu-id="481f8-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="481f8-168">如需 hello 程式碼的說明，請參閱 toohello hello 指令碼中的註解。</span><span class="sxs-lookup"><span data-stu-id="481f8-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="481f8-169">4.測試 Runbook</span><span class="sxs-lookup"><span data-stu-id="481f8-169">4. Test runbook</span></span>
<span data-ttu-id="481f8-170">Azure 自動化中包含環境太[測試您的 runbook](../automation/automation-testing-runbook.md)之前將它發行。</span><span class="sxs-lookup"><span data-stu-id="481f8-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="481f8-171">您可以檢查 hello hello runbook 所收集的資料，並確認它寫入 tooLog 分析如預期般之前發行它 tooproduction。</span><span class="sxs-lookup"><span data-stu-id="481f8-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![測試 Runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="481f8-173">按一下**儲存**toosave hello runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="481f8-174">按一下**測試窗格**tooopen hello runbook hello 測試環境中的。</span><span class="sxs-lookup"><span data-stu-id="481f8-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="481f8-175">因為您的 runbook 具有參數，所以您提示的 tooenter 它們的值。</span><span class="sxs-lookup"><span data-stu-id="481f8-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="481f8-176">輸入 hello hello 資源群組名稱，然後 hello 自動化帳戶從您進行 toocollect 作業資訊。</span><span class="sxs-lookup"><span data-stu-id="481f8-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="481f8-177">按一下**啟動**toohello 啟動 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="481f8-178">hello runbook 的狀態將會開始**排入佇列**會太之前**執行**。</span><span class="sxs-lookup"><span data-stu-id="481f8-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="481f8-179">hello runbook 應該顯示 hello 工作收集 json 格式的詳細資訊輸出。</span><span class="sxs-lookup"><span data-stu-id="481f8-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="481f8-180">如果沒有列出任何工作，然後可能已有建立 hello 自動化帳戶中 hello 過去一小時內沒有工作。</span><span class="sxs-lookup"><span data-stu-id="481f8-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="481f8-181">嘗試啟動 hello 自動化帳戶中的任何 runbook，然後再次執行 hello 測試。</span><span class="sxs-lookup"><span data-stu-id="481f8-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="481f8-182">請確定 hello 輸出不會顯示 hello 中的任何錯誤張貼命令 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="481f8-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="481f8-183">您應該有類似 toohello 後的訊息。</span><span class="sxs-lookup"><span data-stu-id="481f8-183">You should have a message similar toohello following.</span></span>

    ![張貼輸出](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="481f8-185">5.確認 Log Analytics 中的記錄</span><span class="sxs-lookup"><span data-stu-id="481f8-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="481f8-186">一旦 hello runbook 完成在測試中，且您確認已成功收到 hello 輸出，您可以確認已建立使用 hello 記錄[中記錄分析記錄搜尋](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="481f8-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![記錄輸出](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="481f8-188">在 hello Azure 入口網站，選取您的記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="481f8-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="481f8-189">按一下 [記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="481f8-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="481f8-190">下列命令的型別 hello`Type=AutomationJob_CL`按一下 hello [搜尋] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="481f8-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="481f8-191">請注意 hello 記錄類型包含 _CL hello 指令碼中未指定的。</span><span class="sxs-lookup"><span data-stu-id="481f8-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="481f8-192">該尾碼是自動附加的 toohello 記錄類型 tooindicate 它是自訂的記錄檔類型。</span><span class="sxs-lookup"><span data-stu-id="481f8-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="481f8-193">您應該會看到傳回表示該 hello runbook 正常運作的一或多個記錄。</span><span class="sxs-lookup"><span data-stu-id="481f8-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="481f8-194">6.發行 hello runbook</span><span class="sxs-lookup"><span data-stu-id="481f8-194">6. Publish hello runbook</span></span>
<span data-ttu-id="481f8-195">一旦您確認該 hello runbook 正確運作，您需要 toopublish，讓您可以在生產環境中執行它。</span><span class="sxs-lookup"><span data-stu-id="481f8-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="481f8-196">您可以繼續 tooedit，並測試 hello runbook 而不需修改 hello 已發佈的版本。</span><span class="sxs-lookup"><span data-stu-id="481f8-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![發佈 Runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="481f8-198">傳回 tooyour 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="481f8-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="481f8-199">按一下 [Runbook]，並選取 [收集自動化工作]。</span><span class="sxs-lookup"><span data-stu-id="481f8-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="481f8-200">按一下 [編輯]，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="481f8-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="481f8-201">按一下**是**集的 tooverify 先前想 toooverwrite hello 當發行版本。</span><span class="sxs-lookup"><span data-stu-id="481f8-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="481f8-202">7.設定記錄選項</span><span class="sxs-lookup"><span data-stu-id="481f8-202">7. Set logging options</span></span> 
<span data-ttu-id="481f8-203">測試中，您不能 tooview[詳細資訊輸出](../automation/automation-runbook-output-and-messages.md#message-streams)因為您在 hello 指令碼中設定 hello $VerbosePreference 變數。</span><span class="sxs-lookup"><span data-stu-id="481f8-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="481f8-204">針對實際執行，您需要 hello runbook tooset hello 記錄內容，如果您想 tooview 詳細資訊輸出。</span><span class="sxs-lookup"><span data-stu-id="481f8-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="481f8-205">在本教學課程中使用的 hello runbook，這會顯示傳送 tooLog 分析 hello json 資料。</span><span class="sxs-lookup"><span data-stu-id="481f8-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![記錄和追蹤](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="481f8-207">在您的 runbook 的 hello 屬性選取**記錄與追蹤**下**Runbook 設定**。</span><span class="sxs-lookup"><span data-stu-id="481f8-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="481f8-208">變更 hello 設定**記錄詳細資訊記錄**太**上**。</span><span class="sxs-lookup"><span data-stu-id="481f8-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="481f8-209">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="481f8-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="481f8-210">8.排程 Runbook</span><span class="sxs-lookup"><span data-stu-id="481f8-210">8. Schedule runbook</span></span>
<span data-ttu-id="481f8-211">hello 最常見方式 toostart runbook 會收集監視的資料是 tooschedule 它 toorun 自動。</span><span class="sxs-lookup"><span data-stu-id="481f8-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="481f8-212">您可以建立[Azure 自動化中的排程](../automation/automation-schedules.md)並將它附加 tooyour runbook。</span><span class="sxs-lookup"><span data-stu-id="481f8-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![排程 Runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="481f8-214">在您的 runbook 的 hello 屬性，選取**排程**下**資源**。</span><span class="sxs-lookup"><span data-stu-id="481f8-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="481f8-215">按一下**加入排程** > **排程 tooyour runbook 連結** > **建立新的排程**。</span><span class="sxs-lookup"><span data-stu-id="481f8-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="481f8-216">Hello hello 排程，然後按一下值中的型別**建立**。</span><span class="sxs-lookup"><span data-stu-id="481f8-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="481f8-217">屬性</span><span class="sxs-lookup"><span data-stu-id="481f8-217">Property</span></span> | <span data-ttu-id="481f8-218">值</span><span class="sxs-lookup"><span data-stu-id="481f8-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="481f8-219">名稱</span><span class="sxs-lookup"><span data-stu-id="481f8-219">Name</span></span> | <span data-ttu-id="481f8-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="481f8-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="481f8-221">啟動</span><span class="sxs-lookup"><span data-stu-id="481f8-221">Starts</span></span> | <span data-ttu-id="481f8-222">選取任何至少 5 分鐘過去 hello 目前時間的時間。</span><span class="sxs-lookup"><span data-stu-id="481f8-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="481f8-223">週期性</span><span class="sxs-lookup"><span data-stu-id="481f8-223">Recurrence</span></span> | <span data-ttu-id="481f8-224">週期性</span><span class="sxs-lookup"><span data-stu-id="481f8-224">Recurring</span></span> |
| <span data-ttu-id="481f8-225">重複頻率</span><span class="sxs-lookup"><span data-stu-id="481f8-225">Recur every</span></span> | <span data-ttu-id="481f8-226">1 小時</span><span class="sxs-lookup"><span data-stu-id="481f8-226">1 hour</span></span> |
| <span data-ttu-id="481f8-227">設定到期日</span><span class="sxs-lookup"><span data-stu-id="481f8-227">Set expiration</span></span> | <span data-ttu-id="481f8-228">否</span><span class="sxs-lookup"><span data-stu-id="481f8-228">No</span></span> |

<span data-ttu-id="481f8-229">Hello 排程建立之後，您必須將用於每次這個排程啟動 hello runbook tooset hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="481f8-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="481f8-230">按一下 [設定參數與回合設定]。</span><span class="sxs-lookup"><span data-stu-id="481f8-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="481f8-231">填入 **ResourceGroupName** 和 **AutomationAccountName** 的值。</span><span class="sxs-lookup"><span data-stu-id="481f8-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="481f8-232">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="481f8-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="481f8-233">9.驗證 Runbook 會依排程啟動</span><span class="sxs-lookup"><span data-stu-id="481f8-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="481f8-234">每次啟動 Runbook 時，都會[建立作業](../automation/automation-runbook-execution.md)且會記錄任何輸出。</span><span class="sxs-lookup"><span data-stu-id="481f8-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="481f8-235">事實上，這些是的 hello 收集 hello runbook 的相同工作。</span><span class="sxs-lookup"><span data-stu-id="481f8-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="481f8-236">您可以確認該 hello runbook 啟動如預期般 hello hello 排程的開始時間經過後檢查 hello hello runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="481f8-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![工作](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="481f8-238">在您的 runbook 的 hello 屬性，選取**作業**下**資源**。</span><span class="sxs-lookup"><span data-stu-id="481f8-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="481f8-239">您應該會看到每個時間 hello runbook 工作的清單已啟動。</span><span class="sxs-lookup"><span data-stu-id="481f8-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="481f8-240">按一下其中一個 hello 作業 tooview 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="481f8-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="481f8-241">按一下**所有記錄檔**tooview hello 記錄檔和 hello runbook 的輸出。</span><span class="sxs-lookup"><span data-stu-id="481f8-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="481f8-242">捲動 toohello 底部 toofind 項目類似 toohello 下面的影像。</span><span class="sxs-lookup"><span data-stu-id="481f8-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![詳細資訊](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="481f8-244">按一下這個項目 tooview hello json 的詳細資料已傳送 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="481f8-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="481f8-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="481f8-245">Next steps</span></span>
- <span data-ttu-id="481f8-246">使用[檢視表設計工具](../log-analytics/log-analytics-view-designer.md)toocreate 檢視顯示 hello 您收集了 toohello 記錄分析儲存機制的資料。</span><span class="sxs-lookup"><span data-stu-id="481f8-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="481f8-247">封裝您的 runbook 中[管理解決方案](operations-management-suite-solutions-creating.md)toodistribute toocustomers。</span><span class="sxs-lookup"><span data-stu-id="481f8-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="481f8-248">深入了解 [Log Analytics](https://docs.microsoft.com/azure/log-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="481f8-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="481f8-249">深入了解 [Azure 自動化](https://docs.microsoft.com/azure/automation/)。</span><span class="sxs-lookup"><span data-stu-id="481f8-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="481f8-250">深入了解 hello [HTTP 資料收集器 API](../log-analytics/log-analytics-data-collector-api.md)。</span><span class="sxs-lookup"><span data-stu-id="481f8-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
