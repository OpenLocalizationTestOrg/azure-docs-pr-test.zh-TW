---
title: "使用 Azure 自動化啟動和停止虛擬機器 - PowerShell 工作流程 | Microsoft Docs"
description: "Azure 自動化案例的圖形化版本，包含可啟動和停止傳統虛擬機器的 Runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="51a8d-103">Azure 自動化案例 - 啟動和停止虛擬機器</span><span class="sxs-lookup"><span data-stu-id="51a8d-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="51a8d-104">此 Azure 自動化案例包含可啟動和停止傳統虛擬機器的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="51a8d-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="51a8d-105">此案例可用來做為下列任何用途：</span><span class="sxs-lookup"><span data-stu-id="51a8d-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="51a8d-106">在您自己的環境中不修改而直接使用 Runbook。</span><span class="sxs-lookup"><span data-stu-id="51a8d-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="51a8d-107">修改 Runbook 來執行自訂的功能。</span><span class="sxs-lookup"><span data-stu-id="51a8d-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="51a8d-108">在整個解決方案中從另一個 Runbook 呼叫 Runbook。</span><span class="sxs-lookup"><span data-stu-id="51a8d-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="51a8d-109">將 Runbook 當作教學課程來了解 Runbook 撰寫概念。</span><span class="sxs-lookup"><span data-stu-id="51a8d-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="51a8d-110">圖形化</span><span class="sxs-lookup"><span data-stu-id="51a8d-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="51a8d-111">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="51a8d-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="51a8d-112">這是此案例的 PowerShell 工作流程 Runbook 版本。</span><span class="sxs-lookup"><span data-stu-id="51a8d-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="51a8d-113">也可以使用 [圖形化 Runbook](automation-solution-startstopvm-graphical.md)取得。</span><span class="sxs-lookup"><span data-stu-id="51a8d-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="51a8d-114">取得案例</span><span class="sxs-lookup"><span data-stu-id="51a8d-114">Getting the scenario</span></span>
<span data-ttu-id="51a8d-115">此案例包含兩個可以從下列連結下載的 PowerShell 工作流程 Runbook。</span><span class="sxs-lookup"><span data-stu-id="51a8d-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="51a8d-116">請參閱此案例的 [圖形化版本](automation-solution-startstopvm-graphical.md) ，以取得圖形化 Runbook 的連結。</span><span class="sxs-lookup"><span data-stu-id="51a8d-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="51a8d-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="51a8d-117">Runbook</span></span> | <span data-ttu-id="51a8d-118">連結</span><span class="sxs-lookup"><span data-stu-id="51a8d-118">Link</span></span> | <span data-ttu-id="51a8d-119">類型</span><span class="sxs-lookup"><span data-stu-id="51a8d-119">Type</span></span> | <span data-ttu-id="51a8d-120">說明</span><span class="sxs-lookup"><span data-stu-id="51a8d-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="51a8d-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51a8d-121">Start-AzureVMs</span></span> |[<span data-ttu-id="51a8d-122">啟動 Azure 傳統 VM</span><span class="sxs-lookup"><span data-stu-id="51a8d-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="51a8d-123">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="51a8d-123">PowerShell Workflow</span></span> |<span data-ttu-id="51a8d-124">啟動 Azure 訂用帳戶中的所有傳統虛擬機器，或具有特定服務名稱的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="51a8d-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51a8d-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="51a8d-126">停止 Azure 傳統 VM</span><span class="sxs-lookup"><span data-stu-id="51a8d-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="51a8d-127">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="51a8d-127">PowerShell Workflow</span></span> |<span data-ttu-id="51a8d-128">停止自動化帳戶中的所有虛擬機器，或具有特定服務名稱的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="51a8d-129">安裝和設定案例</span><span class="sxs-lookup"><span data-stu-id="51a8d-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="51a8d-130">1.安裝 Runbook</span><span class="sxs-lookup"><span data-stu-id="51a8d-130">1. Install the runbooks</span></span>
<span data-ttu-id="51a8d-131">下載 Runbook 之後，您可以使用 [匯入 Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook)中的程序匯入它們。</span><span class="sxs-lookup"><span data-stu-id="51a8d-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="51a8d-132">2.檢閱描述和需求</span><span class="sxs-lookup"><span data-stu-id="51a8d-132">2. Review the description and requirements</span></span>
<span data-ttu-id="51a8d-133">Runbook 包含註解說明文字，其中含有描述和所需的資產。</span><span class="sxs-lookup"><span data-stu-id="51a8d-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="51a8d-134">您也可以從這份文件取得相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="51a8d-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="51a8d-135">3.設定資產</span><span class="sxs-lookup"><span data-stu-id="51a8d-135">3. Configure assets</span></span>
<span data-ttu-id="51a8d-136">Runbook 需要下列資產，您必須建立這些資產並填入適當的值。</span><span class="sxs-lookup"><span data-stu-id="51a8d-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="51a8d-137">資產類型</span><span class="sxs-lookup"><span data-stu-id="51a8d-137">Asset Type</span></span> | <span data-ttu-id="51a8d-138">資產名稱</span><span class="sxs-lookup"><span data-stu-id="51a8d-138">Asset Name</span></span> | <span data-ttu-id="51a8d-139">說明</span><span class="sxs-lookup"><span data-stu-id="51a8d-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="51a8d-140">認證</span><span class="sxs-lookup"><span data-stu-id="51a8d-140">Credential</span></span> |<span data-ttu-id="51a8d-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="51a8d-141">AzureCredential</span></span> |<span data-ttu-id="51a8d-142">包含帳戶的認證，此帳戶有權啟動和停止 Azure 訂用帳戶中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="51a8d-143">或者，您也可以在 **Add-AzureAccount** 活動的 **Credential** 參數中指定其他認證資產。</span><span class="sxs-lookup"><span data-stu-id="51a8d-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="51a8d-144">變數</span><span class="sxs-lookup"><span data-stu-id="51a8d-144">Variable</span></span> |<span data-ttu-id="51a8d-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="51a8d-145">AzureSubscriptionId</span></span> |<span data-ttu-id="51a8d-146">包含 Azure 訂用帳戶的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="51a8d-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="51a8d-147">使用案例</span><span class="sxs-lookup"><span data-stu-id="51a8d-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="51a8d-148">參數</span><span class="sxs-lookup"><span data-stu-id="51a8d-148">Parameters</span></span>
<span data-ttu-id="51a8d-149">每個 Runbook 都有下列參數。</span><span class="sxs-lookup"><span data-stu-id="51a8d-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="51a8d-150">您必須提供任何必要參數的值，另外可根據您的需求，選擇性地提供其他參數的值。</span><span class="sxs-lookup"><span data-stu-id="51a8d-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="51a8d-151">參數</span><span class="sxs-lookup"><span data-stu-id="51a8d-151">Parameter</span></span> | <span data-ttu-id="51a8d-152">類型</span><span class="sxs-lookup"><span data-stu-id="51a8d-152">Type</span></span> | <span data-ttu-id="51a8d-153">強制</span><span class="sxs-lookup"><span data-stu-id="51a8d-153">Mandatory</span></span> | <span data-ttu-id="51a8d-154">說明</span><span class="sxs-lookup"><span data-stu-id="51a8d-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="51a8d-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="51a8d-155">ServiceName</span></span> |<span data-ttu-id="51a8d-156">string</span><span class="sxs-lookup"><span data-stu-id="51a8d-156">string</span></span> |<span data-ttu-id="51a8d-157">否</span><span class="sxs-lookup"><span data-stu-id="51a8d-157">No</span></span> |<span data-ttu-id="51a8d-158">如果提供一個值，則會啟動或停止具有該服務名稱的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="51a8d-159">如果不提供任何值，則會啟動或停止 Azure 訂用帳戶中的所有傳統虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="51a8d-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="51a8d-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="51a8d-161">string</span><span class="sxs-lookup"><span data-stu-id="51a8d-161">string</span></span> |<span data-ttu-id="51a8d-162">否</span><span class="sxs-lookup"><span data-stu-id="51a8d-162">No</span></span> |<span data-ttu-id="51a8d-163">包含 [變數資產](#installing-and-configuring-the-scenario) 的名稱，此資產含有 Azure 訂用帳戶的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="51a8d-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="51a8d-164">如果不指定任何值，則會使用 *AzureSubscriptionId* 。</span><span class="sxs-lookup"><span data-stu-id="51a8d-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="51a8d-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="51a8d-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="51a8d-166">string</span><span class="sxs-lookup"><span data-stu-id="51a8d-166">string</span></span> |<span data-ttu-id="51a8d-167">否</span><span class="sxs-lookup"><span data-stu-id="51a8d-167">No</span></span> |<span data-ttu-id="51a8d-168">包含 [認證資產](#installing-and-configuring-the-scenario) 的名稱，此資產含有要使用的 Runbook 認證。</span><span class="sxs-lookup"><span data-stu-id="51a8d-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="51a8d-169">如果不指定任何值，則會使用 *AzureCredential* 。</span><span class="sxs-lookup"><span data-stu-id="51a8d-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="51a8d-170">啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="51a8d-170">Starting the runbooks</span></span>
<span data-ttu-id="51a8d-171">您可以使用 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) 中的任何方法，啟動此案例中的任一個 Runbook。</span><span class="sxs-lookup"><span data-stu-id="51a8d-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="51a8d-172">下列範例命令使用 Windows PowerShell 執行 **StartAzureVMs** ，以啟動服務名稱為 *MyVMService*的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="51a8d-173">輸出</span><span class="sxs-lookup"><span data-stu-id="51a8d-173">Output</span></span>
<span data-ttu-id="51a8d-174">Runbook 將為每部虛擬機器 [輸出訊息](automation-runbook-output-and-messages.md) ，指出是否已成功提交啟動或停止指令。</span><span class="sxs-lookup"><span data-stu-id="51a8d-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="51a8d-175">您可以在輸出中尋找特定的字串，以判斷每一個 Runbook 的結果。</span><span class="sxs-lookup"><span data-stu-id="51a8d-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="51a8d-176">下表列出可能的輸出字串。</span><span class="sxs-lookup"><span data-stu-id="51a8d-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="51a8d-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="51a8d-177">Runbook</span></span> | <span data-ttu-id="51a8d-178">條件</span><span class="sxs-lookup"><span data-stu-id="51a8d-178">Condition</span></span> | <span data-ttu-id="51a8d-179">訊息</span><span class="sxs-lookup"><span data-stu-id="51a8d-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="51a8d-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51a8d-180">Start-AzureVMs</span></span> |<span data-ttu-id="51a8d-181">虛擬機器已在執行中</span><span class="sxs-lookup"><span data-stu-id="51a8d-181">Virtual machine is already running</span></span> |<span data-ttu-id="51a8d-182">MyVM 已在執行中</span><span class="sxs-lookup"><span data-stu-id="51a8d-182">MyVM is already running</span></span> |
| <span data-ttu-id="51a8d-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51a8d-183">Start-AzureVMs</span></span> |<span data-ttu-id="51a8d-184">成功提交虛擬機器的啟動要求</span><span class="sxs-lookup"><span data-stu-id="51a8d-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="51a8d-185">MyVM 已啟動</span><span class="sxs-lookup"><span data-stu-id="51a8d-185">MyVM has been started</span></span> |
| <span data-ttu-id="51a8d-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51a8d-186">Start-AzureVMs</span></span> |<span data-ttu-id="51a8d-187">虛擬機器的啟動要求失敗</span><span class="sxs-lookup"><span data-stu-id="51a8d-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="51a8d-188">MyVM 無法啟動</span><span class="sxs-lookup"><span data-stu-id="51a8d-188">MyVM failed to start</span></span> |
| <span data-ttu-id="51a8d-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51a8d-189">Stop-AzureVMs</span></span> |<span data-ttu-id="51a8d-190">虛擬機器已停止</span><span class="sxs-lookup"><span data-stu-id="51a8d-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="51a8d-191">MyVM 已停止</span><span class="sxs-lookup"><span data-stu-id="51a8d-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="51a8d-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51a8d-192">Stop-AzureVMs</span></span> |<span data-ttu-id="51a8d-193">成功提交虛擬機器的停止要求</span><span class="sxs-lookup"><span data-stu-id="51a8d-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="51a8d-194">MyVM 已停止</span><span class="sxs-lookup"><span data-stu-id="51a8d-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="51a8d-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="51a8d-195">Stop-AzureVMs</span></span> |<span data-ttu-id="51a8d-196">虛擬機器的停止要求失敗</span><span class="sxs-lookup"><span data-stu-id="51a8d-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="51a8d-197">MyVM 無法停止</span><span class="sxs-lookup"><span data-stu-id="51a8d-197">MyVM failed to stop</span></span> |

<span data-ttu-id="51a8d-198">例如，Runbook 的下列程式碼片段會嘗試啟動服務名稱為 *MyServiceName*的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="51a8d-199">如果有任何啟動要求失敗，則可以採取錯誤動作。</span><span class="sxs-lookup"><span data-stu-id="51a8d-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="51a8d-200">詳細分解圖</span><span class="sxs-lookup"><span data-stu-id="51a8d-200">Detailed breakdown</span></span>
<span data-ttu-id="51a8d-201">以下是此案例中所有 Runbook 的詳細分解圖。</span><span class="sxs-lookup"><span data-stu-id="51a8d-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="51a8d-202">您可以使用這項資訊來自訂 Runbook，或只是從中學習撰寫您自己的自動化案例。</span><span class="sxs-lookup"><span data-stu-id="51a8d-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="51a8d-203">參數</span><span class="sxs-lookup"><span data-stu-id="51a8d-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="51a8d-204">工作流程首先取得 [輸入參數](#using-the-scenario)的值。</span><span class="sxs-lookup"><span data-stu-id="51a8d-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="51a8d-205">如果沒有提供資產名稱，則會使用預設名稱。</span><span class="sxs-lookup"><span data-stu-id="51a8d-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="51a8d-206">輸出</span><span class="sxs-lookup"><span data-stu-id="51a8d-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="51a8d-207">下面這行宣告 Runbook 的輸出會是一個字串。</span><span class="sxs-lookup"><span data-stu-id="51a8d-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="51a8d-208">這並不需要，但卻是使用 Runbook 作為 [子 Runbook](automation-child-runbooks.md) 時的最佳作法，如此父 Runbook 就可知道預期的輸出類型。</span><span class="sxs-lookup"><span data-stu-id="51a8d-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="51a8d-209">驗證</span><span class="sxs-lookup"><span data-stu-id="51a8d-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="51a8d-210">下面幾行設定將用於 Runbook 其餘部分的 [認證](automation-credentials.md) 和 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="51a8d-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="51a8d-211">首先，我們使用 **Get-AutomationPSCredential** 取得資產，此資產中的認證有權啟動和停止 Azure 訂用帳戶中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="51a8d-212">**Add-AzureAccount** 接著使用此資產來設定認證。</span><span class="sxs-lookup"><span data-stu-id="51a8d-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="51a8d-213">輸出會指派給虛擬變數，所以不會併入 Runbook 輸出中。</span><span class="sxs-lookup"><span data-stu-id="51a8d-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="51a8d-214">然後，使用 **Get-AutomationVariable** 擷取含有訂用帳戶識別碼的變數資產，並使用 **Select-AzureSubscription** 設定訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="51a8d-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="51a8d-215">取得 VM</span><span class="sxs-lookup"><span data-stu-id="51a8d-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="51a8d-216">**Get-AzureVM** 用來擷取 Runbook 將使用的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="51a8d-217">如果在 **ServiceName** 輸入變數中提供一個值，則只會擷取具有該服務名稱的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="51a8d-218">如果 **ServiceName** 是空的，則會擷取所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="51a8d-219">啟動/停止虛擬機器和傳送輸出</span><span class="sxs-lookup"><span data-stu-id="51a8d-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="51a8d-220">接下來的幾行逐步執行每個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="51a8d-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="51a8d-221">首先，檢查虛擬機器的 **PowerState** ，查看它是否在執行中或已停止，視 Runbook 而定。</span><span class="sxs-lookup"><span data-stu-id="51a8d-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="51a8d-222">如果已處於目標狀態，則將訊息傳送至輸出，且 Runbook 會結束。</span><span class="sxs-lookup"><span data-stu-id="51a8d-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="51a8d-223">如果不是，則使用 **Start-AzureVM** 或 **Stop-AzureVM** 嘗試啟動或停止虛擬機器，並將要求的結果儲存至變數。</span><span class="sxs-lookup"><span data-stu-id="51a8d-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="51a8d-224">然後，將訊息傳送至輸出，指出是否已成功提交啟動或停止的要求。</span><span class="sxs-lookup"><span data-stu-id="51a8d-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51a8d-225">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51a8d-225">Next steps</span></span>
* <span data-ttu-id="51a8d-226">若要深入了解如何使用子系 Runbook，請參閱 [Azure 自動化中的子系 Runbook](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="51a8d-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="51a8d-227">若要深入了解 Runbook 執行和記錄期間的輸出訊息以協助進行疑難排解，請參閱 [Azure 自動化中的 Runbook 輸出和訊息](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="51a8d-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

