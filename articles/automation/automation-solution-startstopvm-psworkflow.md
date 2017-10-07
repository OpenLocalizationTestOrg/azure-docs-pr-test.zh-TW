---
title: "Azure 自動化的 PowerShell 工作流程的 aaaStarting 和停止虛擬機器 |Microsoft 文件"
description: "Azure 自動化案例，包括 runbook toostart 和停止傳統的虛擬機器的圖形化版本。"
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="8e72c-103">Azure 自動化案例 - 啟動和停止虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8e72c-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="8e72c-104">此 Azure 自動化案例中包括 runbook toostart 和停止傳統虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-104">This Azure Automation scenario includes runbooks toostart and stop classic virtual machines.</span></span>  <span data-ttu-id="8e72c-105">您可以使用此案例中的 hello 下列任何一項：</span><span class="sxs-lookup"><span data-stu-id="8e72c-105">You can use this scenario for any of hello following:</span></span>  

* <span data-ttu-id="8e72c-106">使用您自己的環境中的 hello runbook，而不需修改。</span><span class="sxs-lookup"><span data-stu-id="8e72c-106">Use hello runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="8e72c-107">修改 hello runbook tooperform 自訂功能。</span><span class="sxs-lookup"><span data-stu-id="8e72c-107">Modify hello runbooks tooperform customized functionality.</span></span>  
* <span data-ttu-id="8e72c-108">從做為整體解決方案的一部分的另一個 runbook 呼叫 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="8e72c-108">Call hello runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="8e72c-109">使用 hello runbook 撰寫概念的教學課程 toolearn runbook。</span><span class="sxs-lookup"><span data-stu-id="8e72c-109">Use hello runbooks as tutorials toolearn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e72c-110">圖形化</span><span class="sxs-lookup"><span data-stu-id="8e72c-110">Graphical</span></span>](automation-solution-startstopvm-graphical.md)
> * [<span data-ttu-id="8e72c-111">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="8e72c-111">PowerShell Workflow</span></span>](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="8e72c-112">這是 hello 這種情況的 PowerShell 工作流程 runbook 版本。</span><span class="sxs-lookup"><span data-stu-id="8e72c-112">This is hello PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="8e72c-113">也可以使用 [圖形化 Runbook](automation-solution-startstopvm-graphical.md)取得。</span><span class="sxs-lookup"><span data-stu-id="8e72c-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="8e72c-114">取得 hello 案例</span><span class="sxs-lookup"><span data-stu-id="8e72c-114">Getting hello scenario</span></span>
<span data-ttu-id="8e72c-115">此案例包含兩個您可以從下列連結查看 hello 的 PowerShell 工作流程 runbook。</span><span class="sxs-lookup"><span data-stu-id="8e72c-115">This scenario consists of two PowerShell Workflow runbooks that you can download from hello following links.</span></span>  <span data-ttu-id="8e72c-116">請參閱 hello[圖形化版本](automation-solution-startstopvm-graphical.md)此案例的連結 toohello 圖形化 runbook。</span><span class="sxs-lookup"><span data-stu-id="8e72c-116">See hello [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links toohello graphical runbooks.</span></span>

| <span data-ttu-id="8e72c-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="8e72c-117">Runbook</span></span> | <span data-ttu-id="8e72c-118">連結</span><span class="sxs-lookup"><span data-stu-id="8e72c-118">Link</span></span> | <span data-ttu-id="8e72c-119">類型</span><span class="sxs-lookup"><span data-stu-id="8e72c-119">Type</span></span> | <span data-ttu-id="8e72c-120">說明</span><span class="sxs-lookup"><span data-stu-id="8e72c-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8e72c-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e72c-121">Start-AzureVMs</span></span> |[<span data-ttu-id="8e72c-122">啟動 Azure 傳統 VM</span><span class="sxs-lookup"><span data-stu-id="8e72c-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="8e72c-123">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="8e72c-123">PowerShell Workflow</span></span> |<span data-ttu-id="8e72c-124">啟動 Azure 訂用帳戶中的所有傳統虛擬機器，或具有特定服務名稱的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="8e72c-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e72c-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="8e72c-126">停止 Azure 傳統 VM</span><span class="sxs-lookup"><span data-stu-id="8e72c-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="8e72c-127">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="8e72c-127">PowerShell Workflow</span></span> |<span data-ttu-id="8e72c-128">停止自動化帳戶中的所有虛擬機器，或具有特定服務名稱的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-hello-scenario"></a><span data-ttu-id="8e72c-129">安裝和設定 hello 案例</span><span class="sxs-lookup"><span data-stu-id="8e72c-129">Installing and configuring hello scenario</span></span>
### <a name="1-install-hello-runbooks"></a><span data-ttu-id="8e72c-130">1.安裝 hello runbook</span><span class="sxs-lookup"><span data-stu-id="8e72c-130">1. Install hello runbooks</span></span>
<span data-ttu-id="8e72c-131">下載之後 hello runbook，您可以匯入使用中的 hello 程序[匯入 Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook)。</span><span class="sxs-lookup"><span data-stu-id="8e72c-131">After downloading hello runbooks, you can import them using hello procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-hello-description-and-requirements"></a><span data-ttu-id="8e72c-132">2.檢閱 hello 描述和需求</span><span class="sxs-lookup"><span data-stu-id="8e72c-132">2. Review hello description and requirements</span></span>
<span data-ttu-id="8e72c-133">hello runbook 包含加上註解的說明文字，其中包含描述以及必要的資產。</span><span class="sxs-lookup"><span data-stu-id="8e72c-133">hello runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="8e72c-134">您也可以取得 hello 在此文件的相同資訊。</span><span class="sxs-lookup"><span data-stu-id="8e72c-134">You can also get hello same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="8e72c-135">3.設定資產</span><span class="sxs-lookup"><span data-stu-id="8e72c-135">3. Configure assets</span></span>
<span data-ttu-id="8e72c-136">hello runbook 需要 hello 下列的資產，您必須建立並填入適當的值。</span><span class="sxs-lookup"><span data-stu-id="8e72c-136">hello runbooks require hello following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="8e72c-137">資產類型</span><span class="sxs-lookup"><span data-stu-id="8e72c-137">Asset Type</span></span> | <span data-ttu-id="8e72c-138">資產名稱</span><span class="sxs-lookup"><span data-stu-id="8e72c-138">Asset Name</span></span> | <span data-ttu-id="8e72c-139">說明</span><span class="sxs-lookup"><span data-stu-id="8e72c-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8e72c-140">認證</span><span class="sxs-lookup"><span data-stu-id="8e72c-140">Credential</span></span> |<span data-ttu-id="8e72c-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="8e72c-141">AzureCredential</span></span> |<span data-ttu-id="8e72c-142">包含在 hello Azure 訂用帳戶中具有授權 toostart 並停止虛擬機器帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="8e72c-142">Contains credentials for an account that has authority toostart and stop virtual machines in hello Azure subscription.</span></span>  <span data-ttu-id="8e72c-143">或者，您可以指定其他認證資產中 hello**認證**hello 參數**Add-azureaccount**活動。</span><span class="sxs-lookup"><span data-stu-id="8e72c-143">Alternatively, you can specify another credential asset in hello **Credential** parameter of hello **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="8e72c-144">變數</span><span class="sxs-lookup"><span data-stu-id="8e72c-144">Variable</span></span> |<span data-ttu-id="8e72c-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="8e72c-145">AzureSubscriptionId</span></span> |<span data-ttu-id="8e72c-146">包含您的 Azure 訂閱 hello 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="8e72c-146">Contains hello subscription ID of your Azure subscription.</span></span> |

## <a name="using-hello-scenario"></a><span data-ttu-id="8e72c-147">使用 hello 案例</span><span class="sxs-lookup"><span data-stu-id="8e72c-147">Using hello scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="8e72c-148">參數</span><span class="sxs-lookup"><span data-stu-id="8e72c-148">Parameters</span></span>
<span data-ttu-id="8e72c-149">hello runbook 每個有下列參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="8e72c-149">hello runbooks each have hello following parameters.</span></span>  <span data-ttu-id="8e72c-150">您必須提供任何必要參數的值，另外可根據您的需求，選擇性地提供其他參數的值。</span><span class="sxs-lookup"><span data-stu-id="8e72c-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="8e72c-151">參數</span><span class="sxs-lookup"><span data-stu-id="8e72c-151">Parameter</span></span> | <span data-ttu-id="8e72c-152">類型</span><span class="sxs-lookup"><span data-stu-id="8e72c-152">Type</span></span> | <span data-ttu-id="8e72c-153">強制</span><span class="sxs-lookup"><span data-stu-id="8e72c-153">Mandatory</span></span> | <span data-ttu-id="8e72c-154">說明</span><span class="sxs-lookup"><span data-stu-id="8e72c-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8e72c-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="8e72c-155">ServiceName</span></span> |<span data-ttu-id="8e72c-156">string</span><span class="sxs-lookup"><span data-stu-id="8e72c-156">string</span></span> |<span data-ttu-id="8e72c-157">否</span><span class="sxs-lookup"><span data-stu-id="8e72c-157">No</span></span> |<span data-ttu-id="8e72c-158">如果提供一個值，則會啟動或停止具有該服務名稱的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="8e72c-159">如果未不提供任何值，然後 hello Azure 訂用帳戶中的所有傳統虛擬機器啟動或停止。</span><span class="sxs-lookup"><span data-stu-id="8e72c-159">If no value is provided, then all classic virtual machines in hello Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="8e72c-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="8e72c-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="8e72c-161">string</span><span class="sxs-lookup"><span data-stu-id="8e72c-161">string</span></span> |<span data-ttu-id="8e72c-162">否</span><span class="sxs-lookup"><span data-stu-id="8e72c-162">No</span></span> |<span data-ttu-id="8e72c-163">包含 hello hello 名稱[變數資產](#installing-and-configuring-the-scenario)，其中包含您的 Azure 訂閱 hello 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="8e72c-163">Contains hello name of hello [variable asset](#installing-and-configuring-the-scenario) that contains hello subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="8e72c-164">如果不指定任何值，則會使用 *AzureSubscriptionId* 。</span><span class="sxs-lookup"><span data-stu-id="8e72c-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="8e72c-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="8e72c-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="8e72c-166">string</span><span class="sxs-lookup"><span data-stu-id="8e72c-166">string</span></span> |<span data-ttu-id="8e72c-167">否</span><span class="sxs-lookup"><span data-stu-id="8e72c-167">No</span></span> |<span data-ttu-id="8e72c-168">包含 hello hello 名稱[認證資產](#installing-and-configuring-the-scenario)包含 hello runbook toouse hello 認證。</span><span class="sxs-lookup"><span data-stu-id="8e72c-168">Contains hello name of hello [credential asset](#installing-and-configuring-the-scenario) that contains hello credentials for hello runbook toouse.</span></span>  <span data-ttu-id="8e72c-169">如果不指定任何值，則會使用 *AzureCredential* 。</span><span class="sxs-lookup"><span data-stu-id="8e72c-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-hello-runbooks"></a><span data-ttu-id="8e72c-170">啟動 hello runbook</span><span class="sxs-lookup"><span data-stu-id="8e72c-170">Starting hello runbooks</span></span>
<span data-ttu-id="8e72c-171">您可以使用任何一種方法在 hello [Azure 自動化中啟動 runbook](automation-starting-a-runbook.md) toostart 任一 hello runbook 在這個案例中。</span><span class="sxs-lookup"><span data-stu-id="8e72c-171">You can use any of hello methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) toostart either of hello runbooks in this scenario.</span></span>

<span data-ttu-id="8e72c-172">hello 下列範例命令會使用 Windows PowerShell toorun **StartAzureVMs** toostart hello 服務名稱的所有虛擬機器*MyVMService*。</span><span class="sxs-lookup"><span data-stu-id="8e72c-172">hello following sample commands uses Windows PowerShell toorun **StartAzureVMs** toostart all virtual machines with hello service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="8e72c-173">輸出</span><span class="sxs-lookup"><span data-stu-id="8e72c-173">Output</span></span>
<span data-ttu-id="8e72c-174">hello runbook 將[輸出訊息](automation-runbook-output-and-messages.md)指出每個虛擬機器是否 hello 開始或已成功提交停止指令。</span><span class="sxs-lookup"><span data-stu-id="8e72c-174">hello runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not hello start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="8e72c-175">您可以尋找每個 runbook hello 輸出 toodetermine hello 結果中的特定字串。</span><span class="sxs-lookup"><span data-stu-id="8e72c-175">You can look for a specific string in hello output toodetermine hello result for each runbook.</span></span>  <span data-ttu-id="8e72c-176">hello 下表列出 hello 可能的輸出字串。</span><span class="sxs-lookup"><span data-stu-id="8e72c-176">hello possible output strings are listed in hello following table.</span></span>

| <span data-ttu-id="8e72c-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="8e72c-177">Runbook</span></span> | <span data-ttu-id="8e72c-178">條件</span><span class="sxs-lookup"><span data-stu-id="8e72c-178">Condition</span></span> | <span data-ttu-id="8e72c-179">訊息</span><span class="sxs-lookup"><span data-stu-id="8e72c-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8e72c-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e72c-180">Start-AzureVMs</span></span> |<span data-ttu-id="8e72c-181">虛擬機器已在執行中</span><span class="sxs-lookup"><span data-stu-id="8e72c-181">Virtual machine is already running</span></span> |<span data-ttu-id="8e72c-182">MyVM 已在執行中</span><span class="sxs-lookup"><span data-stu-id="8e72c-182">MyVM is already running</span></span> |
| <span data-ttu-id="8e72c-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e72c-183">Start-AzureVMs</span></span> |<span data-ttu-id="8e72c-184">成功提交虛擬機器的啟動要求</span><span class="sxs-lookup"><span data-stu-id="8e72c-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="8e72c-185">MyVM 已啟動</span><span class="sxs-lookup"><span data-stu-id="8e72c-185">MyVM has been started</span></span> |
| <span data-ttu-id="8e72c-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e72c-186">Start-AzureVMs</span></span> |<span data-ttu-id="8e72c-187">虛擬機器的啟動要求失敗</span><span class="sxs-lookup"><span data-stu-id="8e72c-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="8e72c-188">失敗的 MyVM toostart</span><span class="sxs-lookup"><span data-stu-id="8e72c-188">MyVM failed toostart</span></span> |
| <span data-ttu-id="8e72c-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e72c-189">Stop-AzureVMs</span></span> |<span data-ttu-id="8e72c-190">虛擬機器已停止</span><span class="sxs-lookup"><span data-stu-id="8e72c-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="8e72c-191">MyVM 已停止</span><span class="sxs-lookup"><span data-stu-id="8e72c-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="8e72c-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e72c-192">Stop-AzureVMs</span></span> |<span data-ttu-id="8e72c-193">成功提交虛擬機器的停止要求</span><span class="sxs-lookup"><span data-stu-id="8e72c-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="8e72c-194">MyVM 已停止</span><span class="sxs-lookup"><span data-stu-id="8e72c-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="8e72c-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="8e72c-195">Stop-AzureVMs</span></span> |<span data-ttu-id="8e72c-196">虛擬機器的停止要求失敗</span><span class="sxs-lookup"><span data-stu-id="8e72c-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="8e72c-197">失敗的 MyVM toostop</span><span class="sxs-lookup"><span data-stu-id="8e72c-197">MyVM failed toostop</span></span> |

<span data-ttu-id="8e72c-198">例如，runbook 中的下列程式碼片段的 hello 會嘗試 toostart hello 服務名稱的所有虛擬機器*MyServiceName*。</span><span class="sxs-lookup"><span data-stu-id="8e72c-198">For example, hello following code snippet from a runbook attempts toostart all virtual machines with hello service name *MyServiceName*.</span></span>  <span data-ttu-id="8e72c-199">如果任何 hello 啟動要求失敗，則可以採取錯誤動作。</span><span class="sxs-lookup"><span data-stu-id="8e72c-199">If any of hello start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="8e72c-200">詳細分解圖</span><span class="sxs-lookup"><span data-stu-id="8e72c-200">Detailed breakdown</span></span>
<span data-ttu-id="8e72c-201">以下是在此案例中的 hello runbook 的詳細的細目。</span><span class="sxs-lookup"><span data-stu-id="8e72c-201">Following is a detailed breakdown of hello runbooks in this scenario.</span></span>  <span data-ttu-id="8e72c-202">您可以使用這項資訊 tooeither 自訂 hello runbook 或只是 toolearn 從中來撰寫您自己的自動化案例。</span><span class="sxs-lookup"><span data-stu-id="8e72c-202">You can use this information tooeither customize hello runbooks or just toolearn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="8e72c-203">參數</span><span class="sxs-lookup"><span data-stu-id="8e72c-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="8e72c-204">hello 啟動工作流程藉由取得 hello 值 hello[輸入參數](#using-the-scenario)。</span><span class="sxs-lookup"><span data-stu-id="8e72c-204">hello workflow starts by getting hello values for hello [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="8e72c-205">如果沒有提供 hello 資產名稱則會使用預設名稱。</span><span class="sxs-lookup"><span data-stu-id="8e72c-205">If hello asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="8e72c-206">輸出</span><span class="sxs-lookup"><span data-stu-id="8e72c-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="8e72c-207">這一行會宣告 hello runbook 的 hello 輸出會是一個字串。</span><span class="sxs-lookup"><span data-stu-id="8e72c-207">This line declares that hello output of hello runbook will be a string.</span></span>  <span data-ttu-id="8e72c-208">這不是必要，但會作為使用 hello runbook 時的最佳作法[子系 runbook](automation-child-runbooks.md) ，以便在父 runbook 知道 hello 輸出輸入 tooexpect。</span><span class="sxs-lookup"><span data-stu-id="8e72c-208">This is not required but is a best practice for when hello runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know hello output type tooexpect.</span></span>

### <a name="authentication"></a><span data-ttu-id="8e72c-209">驗證</span><span class="sxs-lookup"><span data-stu-id="8e72c-209">Authentication</span></span>
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="8e72c-210">接下來幾行 hello 設定 hello[認證](automation-credentials.md)和 Azure 訂用帳戶將用於 hello runbook hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="8e72c-210">hello next lines set hello [credentials](automation-credentials.md) and Azure subscription that will be used for hello rest of hello runbook.</span></span>
<span data-ttu-id="8e72c-211">第一次使用**Get-automationpscredential** tooget hello 資產 hello Azure 訂用帳戶保留 hello 認證以存取 toostart 並停止虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-211">First we use **Get-AutomationPSCredential** tooget hello asset that holds hello credentials with access toostart and stop virtual machines in hello Azure subscription.</span></span> <span data-ttu-id="8e72c-212">**Add-azureaccount**接著會使用此資產 tooset hello 認證。</span><span class="sxs-lookup"><span data-stu-id="8e72c-212">**Add-AzureAccount** then uses this asset tooset hello credentials.</span></span>  <span data-ttu-id="8e72c-213">hello 輸出會指派 tooa 虛設變數，使它不包含在 hello runbook 輸出。</span><span class="sxs-lookup"><span data-stu-id="8e72c-213">hello output is assigned tooa dummy variable so that it isn't included in hello runbook output.</span></span>  

<span data-ttu-id="8e72c-214">hello 與 hello 訂用帳戶 ID 擷取與變數的資產**Get-automationvariable**和 hello 訂用帳戶與設定**Select-azuresubscription**。</span><span class="sxs-lookup"><span data-stu-id="8e72c-214">hello variable asset with hello subscription ID is then retrieved with **Get-AutomationVariable** and hello subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="8e72c-215">取得 VM</span><span class="sxs-lookup"><span data-stu-id="8e72c-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="8e72c-216">**Get-azurevm**是使用的 tooretrieve hello hello runbook 將會使用的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-216">**Get-AzureVM** is used tooretrieve hello virtual machines hello runbook will work with.</span></span>  <span data-ttu-id="8e72c-217">如果提供的值在 hello **ServiceName**輸入會擷取與該服務名稱的變數，則只 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-217">If a value is provided in hello **ServiceName** input variable, then only hello virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="8e72c-218">如果 **ServiceName** 是空的，則會擷取所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="8e72c-219">啟動/停止虛擬機器和傳送輸出</span><span class="sxs-lookup"><span data-stu-id="8e72c-219">Start/Stop virtual machines and send output</span></span>
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="8e72c-220">接下來幾行 hello 逐步執行每個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-220">hello next lines step through each virtual machine.</span></span>  <span data-ttu-id="8e72c-221">第一次 hello **PowerState** hello 的虛擬機器時，已檢查的 toosee 已經是執行中還是已停止，相依於 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="8e72c-221">First hello **PowerState** of hello virtual machine is checked toosee if it is already running or stopped, depending on hello runbook.</span></span>  <span data-ttu-id="8e72c-222">如果已經在 hello 目標狀態，然後會傳送一則訊息，toooutput，且 hello runbook 結尾。</span><span class="sxs-lookup"><span data-stu-id="8e72c-222">If it is already in hello target state, then a message is sent toooutput, and hello runbook ends.</span></span>  <span data-ttu-id="8e72c-223">如果沒有，然後**Start-azurevm**或**Stop-azurevm** hello 要求預存的 tooa 變數 hello 結果的使用的 tooattempt toostart 或停止 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e72c-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used tooattempt toostart or stop hello virtual machine with hello result of hello request stored tooa variable.</span></span>  <span data-ttu-id="8e72c-224">訊息會接著傳送 toooutput 指定是否已成功提交 hello 要求 toostart 或停止。</span><span class="sxs-lookup"><span data-stu-id="8e72c-224">A message is then sent toooutput specifying whether hello request toostart or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e72c-225">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e72c-225">Next steps</span></span>
* <span data-ttu-id="8e72c-226">toolearn 進一步了解使用子 runbook，請參閱[Azure 自動化中的子 runbook](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="8e72c-226">toolearn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="8e72c-227">深入了解 toolearn 輸出內執行 runbook 及記錄 toohelp 訊息進行疑難排解，請參閱[Runbook 輸出和在 Azure 自動化中的訊息](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="8e72c-227">toolearn more about output messages during runbook execution and logging toohelp troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

