---
title: "Azure 自動化 Runbook 類型 | Microsoft Docs"
description: "描述您在 Azure 自動化中可使用的各種 Runbook，以及您在決定使用何種類型時應該納入的考量。 "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: e859aef473b433fbf4efb639962f3a3ce0a23d7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-runbook-types"></a><span data-ttu-id="09870-103">Azure 自動化 Runbook 類型</span><span class="sxs-lookup"><span data-stu-id="09870-103">Azure Automation runbook types</span></span>
<span data-ttu-id="09870-104">Azure 自動化支援下表中簡短描述的四種 Runbook。</span><span class="sxs-lookup"><span data-stu-id="09870-104">Azure Automation supports four types of runbooks that are  briefly described in the following table.</span></span>  <span data-ttu-id="09870-105">下列各節提供各種類型的進一步資訊，包括每種類別何時使用的考量。</span><span class="sxs-lookup"><span data-stu-id="09870-105">The sections below provide further information about each type including considerations on when to use each.</span></span>

| <span data-ttu-id="09870-106">類型</span><span class="sxs-lookup"><span data-stu-id="09870-106">Type</span></span> | <span data-ttu-id="09870-107">說明</span><span class="sxs-lookup"><span data-stu-id="09870-107">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="09870-108">圖形化</span><span class="sxs-lookup"><span data-stu-id="09870-108">Graphical</span></span>](#graphical-runbooks) |<span data-ttu-id="09870-109">以 Windows PowerShell 為基礎，而且完全在 Azure 入口網站的圖形化編輯器中建立和編輯。</span><span class="sxs-lookup"><span data-stu-id="09870-109">Based on Windows PowerShell and created and edited completely in graphical editor in Azure portal.</span></span> |
| [<span data-ttu-id="09870-110">圖形化 PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="09870-110">Graphical PowerShell Workflow</span></span>](#graphical-runbooks) |<span data-ttu-id="09870-111">以 Windows PowerShell 工作流程為基礎，而且完全在 Azure 入口網站的圖形化編輯器中建立和編輯。</span><span class="sxs-lookup"><span data-stu-id="09870-111">Based on Windows PowerShell Workflow and created and edited completely in the graphical editor in Azure portal.</span></span> |
| [<span data-ttu-id="09870-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09870-112">PowerShell</span></span>](#powershell-runbooks) |<span data-ttu-id="09870-113">以 Windows PowerShell 指令碼為基礎的文字 Runbook。</span><span class="sxs-lookup"><span data-stu-id="09870-113">Text runbook based on Windows PowerShell script.</span></span> |
| [<span data-ttu-id="09870-114">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="09870-114">PowerShell Workflow</span></span>](#powershell-workflow-runbooks) |<span data-ttu-id="09870-115">以 Windows PowerShell 工作流程為基礎的文字 Runbook。</span><span class="sxs-lookup"><span data-stu-id="09870-115">Text runbook based on Windows PowerShell Workflow.</span></span> |

## <a name="graphical-runbooks"></a><span data-ttu-id="09870-116">圖形化 Runbook</span><span class="sxs-lookup"><span data-stu-id="09870-116">Graphical runbooks</span></span>
<span data-ttu-id="09870-117">[圖形化](automation-runbook-types.md#graphical-runbooks) 和圖形化 PowerShell 工作流程 Runbook 是以 Azure 入口網站中的圖形化編輯器來建立和編輯。</span><span class="sxs-lookup"><span data-stu-id="09870-117">[Graphical](automation-runbook-types.md#graphical-runbooks) and Graphical PowerShell Workflow runbooks are created and edited with the graphical editor in the Azure portal.</span></span>  <span data-ttu-id="09870-118">您可以將它們匯出至檔案，再匯入到另一個自動化帳戶，但無法使用另一種工具來建立或編輯。</span><span class="sxs-lookup"><span data-stu-id="09870-118">You can export them to a file and then import them into another automation account, but you cannot create or edit them with another tool.</span></span>  <span data-ttu-id="09870-119">圖形化 Runbook 會產生 PowerShell 程式碼，但您無法直接檢視或修改此程式碼。</span><span class="sxs-lookup"><span data-stu-id="09870-119">Graphical runbooks generate PowerShell code, but you can't directly view or modify the code.</span></span> <span data-ttu-id="09870-120">圖形化 Runbook 無法轉換成其中一種 [文字格式](automation-runbook-types.md)，而文字 Runbook 也無法轉換成圖形化格式。</span><span class="sxs-lookup"><span data-stu-id="09870-120">Graphical runbooks cannot be converted to one of the [text formats](automation-runbook-types.md), nor can a text runbook be converted to graphical format.</span></span> <span data-ttu-id="09870-121">圖形化 Runbook 可以在匯入期間轉換為圖形化 PowerShell 工作流程 Runbook，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="09870-121">Graphical runbooks can be converted to Graphical PowerShell Workflow runbooks during import and vice-versa.</span></span>

### <a name="advantages"></a><span data-ttu-id="09870-122">優點</span><span class="sxs-lookup"><span data-stu-id="09870-122">Advantages</span></span>
* <span data-ttu-id="09870-123">虛擬插入連結設定撰寫模型</span><span class="sxs-lookup"><span data-stu-id="09870-123">Visual insert-link-configure authoring model</span></span>  
* <span data-ttu-id="09870-124">將焦點放在資料如何透過此程序來流動</span><span class="sxs-lookup"><span data-stu-id="09870-124">Focus on how data flows through the process</span></span>  
* <span data-ttu-id="09870-125">以視覺方式呈現管理程序</span><span class="sxs-lookup"><span data-stu-id="09870-125">Visually represent management processes</span></span>  
* <span data-ttu-id="09870-126">包含其他 Runbook 做為子 Runbook 來建立高階工作流程</span><span class="sxs-lookup"><span data-stu-id="09870-126">Include other runbooks as child runbooks to create high level workflows</span></span>  
* <span data-ttu-id="09870-127">建議您採用模組化的程式設計</span><span class="sxs-lookup"><span data-stu-id="09870-127">Encourages modular programming</span></span>  


### <a name="limitations"></a><span data-ttu-id="09870-128">限制</span><span class="sxs-lookup"><span data-stu-id="09870-128">Limitations</span></span>
* <span data-ttu-id="09870-129">無法在 Azure 入口網站之外編輯 Runbook。</span><span class="sxs-lookup"><span data-stu-id="09870-129">Can't edit runbook outside of Azure portal.</span></span>
* <span data-ttu-id="09870-130">可能需要包含 PowerShell 程式碼的程式碼活動來執行複雜邏輯。</span><span class="sxs-lookup"><span data-stu-id="09870-130">May require a Code activity containing PowerShell code to perform complex logic.</span></span>
* <span data-ttu-id="09870-131">無法檢視或直接編輯圖形化工作流程所建立的 PowerShell 程式碼。</span><span class="sxs-lookup"><span data-stu-id="09870-131">Can't view or directly edit the PowerShell code that is created by the graphical workflow.</span></span> <span data-ttu-id="09870-132">請注意，您可以檢視您在任何程式碼活動中所建立的程式碼。</span><span class="sxs-lookup"><span data-stu-id="09870-132">Note that you can view the code you create in any Code activities.</span></span>

## <a name="powershell-runbooks"></a><span data-ttu-id="09870-133">PowerShell Runbook</span><span class="sxs-lookup"><span data-stu-id="09870-133">PowerShell runbooks</span></span>
<span data-ttu-id="09870-134">PowerShell Runbook 以 Windows PowerShell 為基礎。</span><span class="sxs-lookup"><span data-stu-id="09870-134">PowerShell runbooks are based on Windows PowerShell.</span></span>  <span data-ttu-id="09870-135">您可以直接使用 Azure 入口網站的文字編輯器來編輯 Runbook 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="09870-135">You directly edit the code of the runbook using the text editor in the Azure portal.</span></span>  <span data-ttu-id="09870-136">您也可以使用任何離線文字編輯器，並 [匯入 Runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) 到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="09870-136">You can also use any offline text editor and [import the runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) into Azure Automation.</span></span>

### <a name="advantages"></a><span data-ttu-id="09870-137">優點</span><span class="sxs-lookup"><span data-stu-id="09870-137">Advantages</span></span>
* <span data-ttu-id="09870-138">使用 PowerShell 程式碼實作所有複雜的邏輯，不必處理 PowerShell 工作流程的其他複雜性。</span><span class="sxs-lookup"><span data-stu-id="09870-138">Implement all complex logic with PowerShell code without the additional complexities of PowerShell Workflow.</span></span> 
* <span data-ttu-id="09870-139">Runbook 的啟動速度會比 PowerShell 工作流程 Runbook 更快，因為它在執行之前不需要編譯。</span><span class="sxs-lookup"><span data-stu-id="09870-139">Runbook starts faster than PowerShell Workflow runbooks since it doesn't need to be compiled before running.</span></span>

### <a name="limitations"></a><span data-ttu-id="09870-140">限制</span><span class="sxs-lookup"><span data-stu-id="09870-140">Limitations</span></span>
* <span data-ttu-id="09870-141">必須熟悉 PowerShell 指令碼處理。</span><span class="sxs-lookup"><span data-stu-id="09870-141">Must be familiar with PowerShell scripting.</span></span>
* <span data-ttu-id="09870-142">無法使用 [平行處理](automation-powershell-workflow.md#parallel-processing) 來平行執行多個動作。</span><span class="sxs-lookup"><span data-stu-id="09870-142">Can't use [parallel processing](automation-powershell-workflow.md#parallel-processing) to perform multiple actions in parallel.</span></span>
* <span data-ttu-id="09870-143">發生錯誤時無法使用 [檢查點](automation-powershell-workflow.md#checkpoints) 繼續執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="09870-143">Can't use [checkpoints](automation-powershell-workflow.md#checkpoints) to resume runbook in case of error.</span></span>
* <span data-ttu-id="09870-144">只有使用 Start-AzureAutomationRunbook Cmdlet 才能併入 PowerShell 工作流程 Runbook 和圖形化 Runbook 做為子 Runbook，此 Cmdlet 會建立新的工作。</span><span class="sxs-lookup"><span data-stu-id="09870-144">PowerShell Workflow runbooks and Graphical runbooks can only be included as child runbooks by using the Start-AzureAutomationRunbook cmdlet which creates a new job.</span></span>

### <a name="known-issues"></a><span data-ttu-id="09870-145">已知問題</span><span class="sxs-lookup"><span data-stu-id="09870-145">Known Issues</span></span>
<span data-ttu-id="09870-146">以下是 PowerShell Runbook 目前已知的問題。</span><span class="sxs-lookup"><span data-stu-id="09870-146">Following are current known issues with PowerShell runbooks.</span></span>

* <span data-ttu-id="09870-147">PowerShell Runbook 無法擷取具有 Null 值的未加密 [變數資產](automation-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="09870-147">PowerShell runbooks cannot cannot retrieve an unencrypted [variable asset](automation-variables.md) with a null value.</span></span>
* <span data-ttu-id="09870-148">PowerShell Runbook 無法擷取名稱中含有 [變數資產](automation-variables.md) 的 *~* 。</span><span class="sxs-lookup"><span data-stu-id="09870-148">PowerShell runbooks cannot retrieve a [variable asset](automation-variables.md) with *~* in the name.</span></span>
* <span data-ttu-id="09870-149">PowerShell Runbook 中落入迴圈的 Get-Process 大約在 80 次反覆運算之後就會損毀。</span><span class="sxs-lookup"><span data-stu-id="09870-149">Get-Process in a loop in a PowerShell runbook may crash after about 80 iterations.</span></span> 
* <span data-ttu-id="09870-150">如果 PowerShell Runbook 嘗試一次將非常大量的資料寫入輸出資料流，可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="09870-150">A PowerShell runbook may fail if it attempts to write a very large amount of data to the output stream at once.</span></span>   <span data-ttu-id="09870-151">在處理大型物件時，只輸出您所需的資訊，通常就可以解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="09870-151">You can typically work around this issue by outputting just the information you need when working with large objects.</span></span>  <span data-ttu-id="09870-152">例如，不要輸出類似 *Get-Process* 之類的資訊，您可以使用 *Get-Process | Select ProcessName, CPU*，只輸出需要的欄位。</span><span class="sxs-lookup"><span data-stu-id="09870-152">For example, instead of outputting something like *Get-Process*, you can output just the required fields with *Get-Process | Select ProcessName, CPU*.</span></span>

## <a name="powershell-workflow-runbooks"></a><span data-ttu-id="09870-153">PowerShell 工作流程 Runbook</span><span class="sxs-lookup"><span data-stu-id="09870-153">PowerShell Workflow runbooks</span></span>
<span data-ttu-id="09870-154">PowerShell Workflow Runbook 是以 [Windows PowerShell 工作流程](automation-powershell-workflow.md)為基礎的文字 Runbook。</span><span class="sxs-lookup"><span data-stu-id="09870-154">PowerShell Workflow runbooks are text runbooks based on [Windows PowerShell Workflow](automation-powershell-workflow.md).</span></span>  <span data-ttu-id="09870-155">您可以直接使用 Azure 入口網站的文字編輯器來編輯 Runbook 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="09870-155">You directly edit the code of the runbook using the text editor in the Azure portal.</span></span>  <span data-ttu-id="09870-156">您也可以使用任何離線文字編輯器，並 [匯入 Runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) 到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="09870-156">You can also use any offline text editor and [import the runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) into Azure Automation.</span></span>

### <a name="advantages"></a><span data-ttu-id="09870-157">優點</span><span class="sxs-lookup"><span data-stu-id="09870-157">Advantages</span></span>
* <span data-ttu-id="09870-158">使用 PowerShell 工作流程程式碼實作所有複雜的邏輯。</span><span class="sxs-lookup"><span data-stu-id="09870-158">Implement all complex logic with PowerShell Workflow code.</span></span>
* <span data-ttu-id="09870-159">發生錯誤時使用 [檢查點](automation-powershell-workflow.md#checkpoints) 繼續執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="09870-159">Use [checkpoints](automation-powershell-workflow.md#checkpoints) to resume runbook in case of error.</span></span>
* <span data-ttu-id="09870-160">使用 [平行處理](automation-powershell-workflow.md#parallel-processing) 以平行執行多個動作。</span><span class="sxs-lookup"><span data-stu-id="09870-160">Use [parallel processing](automation-powershell-workflow.md#parallel-processing) to perform multiple actions in parallel.</span></span>
* <span data-ttu-id="09870-161">可併入其他圖形化 Runbook 和 PowerShell 工作流程 Runbook 成為子 Runbook，以建立高階工作流程。</span><span class="sxs-lookup"><span data-stu-id="09870-161">Can include other Graphical runbooks and PowerShell Workflow runbooks as child runbooks to create high level workflows.</span></span>

### <a name="limitations"></a><span data-ttu-id="09870-162">限制</span><span class="sxs-lookup"><span data-stu-id="09870-162">Limitations</span></span>
* <span data-ttu-id="09870-163">作者必須熟悉 PowerShell 工作流程。</span><span class="sxs-lookup"><span data-stu-id="09870-163">Author must be familiar with PowerShell Workflow.</span></span>
* <span data-ttu-id="09870-164">Runbook 必須處理 PowerShell 工作流程額外的複雜性，例如 [已還原序列化的物件](automation-powershell-workflow.md#code-changes)。</span><span class="sxs-lookup"><span data-stu-id="09870-164">Runbook must deal with the additional complexity of PowerShell Workflow such as [deserialized objects](automation-powershell-workflow.md#code-changes).</span></span>
* <span data-ttu-id="09870-165">Runbook 所需的啟動時間比 PowerShell Runbook 更久，因為它在執行之前需要編譯。</span><span class="sxs-lookup"><span data-stu-id="09870-165">Runbook takes longer to start than PowerShell runbooks since it needs to be compiled before running.</span></span>
* <span data-ttu-id="09870-166">只有使用 Start-AzureAutomationRunbook Cmdlet 才能併入 PowerShell Runbook 做為子 Runbook，此 Cmdlet 會建立新的工作。</span><span class="sxs-lookup"><span data-stu-id="09870-166">PowerShell runbooks can only be included as child runbooks by using the Start-AzureAutomationRunbook cmdlet which creates a new job.</span></span>

## <a name="considerations"></a><span data-ttu-id="09870-167">考量</span><span class="sxs-lookup"><span data-stu-id="09870-167">Considerations</span></span>
<span data-ttu-id="09870-168">在決定特定 Runbook 要使用何種類型時，您應該考慮下列其他事項。</span><span class="sxs-lookup"><span data-stu-id="09870-168">You should take into account the following additional considerations when determining which type to use for a particular runbook.</span></span>

* <span data-ttu-id="09870-169">您無法將 Runbook 從圖形化轉換為文字類型，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="09870-169">You can't convert runbooks from graphical to textual type or vice-versa.</span></span>
* <span data-ttu-id="09870-170">使用不同類型的 Runbook 作為子 Runbook 時有所限制。</span><span class="sxs-lookup"><span data-stu-id="09870-170">There are limitations using runbooks of different types as a child runbook.</span></span>  <span data-ttu-id="09870-171">如需詳細資訊，請參閱 [Azure 自動化中的子 Runbook](automation-child-runbooks.md) 。</span><span class="sxs-lookup"><span data-stu-id="09870-171">See [Child runbooks in Azure Automation](automation-child-runbooks.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09870-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09870-172">Next steps</span></span>
* <span data-ttu-id="09870-173">若要深入了解如何編寫圖形化 Runbook，請參閱 [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="09870-173">To learn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>
* <span data-ttu-id="09870-174">若要了解適用於 Runbook 的 PowerShell 和 PowerShell 工作流程之間的差異，請參閱 [了解 Windows PowerShell 工作流程](automation-powershell-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="09870-174">To understand the differences between PowerShell and PowerShell workflows for runbooks, see [Learning Windows PowerShell Workflow](automation-powershell-workflow.md)</span></span>
* <span data-ttu-id="09870-175">如需如何建立或匯入 Runbook 的詳細資訊，請參閱 [建立或匯入 Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="09870-175">For more information on how to create or import a Runbook, see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span>

